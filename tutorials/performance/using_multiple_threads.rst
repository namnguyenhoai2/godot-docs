.. _doc_using_multiple_threads:

Sử dụng nhiều luồng
===================

.. seealso::

    Để xem danh sách các primitive multithreading trong C++, hãy xem :ref:`doc_core_concurrency_types`.

Luồng
-----

Luồng cho phép thực thi mã đồng thời. Điều này cho phép chuyển bớt công việc khỏi luồng chính.

Godot hỗ trợ các luồng và cung cấp nhiều hàm tiện dụng để sử dụng chúng.

.. note:: If using other languages (C#, C++), it may be easier to use the
          các lớp threading mà chúng hỗ trợ.

.. warning::

    Trước khi sử dụng một lớp tích hợp trong một luồng, trước tiên hãy đọc :ref:`doc_thread_safe_apis` để kiểm tra xem lớp đó có thể được sử dụng an toàn trong luồng hay không.

Tạo một Thread
--------------

Để tạo một thread, hãy sử dụng đoạn mã sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var thread: Thread

    # Thread sẽ bắt đầu tại đây.
    func _ready():
        thread = Thread.new()
        # Bạn có thể bind nhiều đối số vào một Callable.
        thread.start(_thread_function.bind("Wafflecopter"))


    # Chạy tại đây rồi thoát.
    # Đối số là dữ liệu đã bind được truyền từ start().
    func _thread_function(userdata):
        # In userdata ("Wafflecopter")
        print("I'm a thread! Userdata is: ", userdata)


    # Thread phải được giải phóng (hoặc "joined") để đảm bảo tính portable.
    func _exit_tree():
        thread.wait_to_finish()

 .. code-tab:: cpp C++ .H File

    #pragma once

    #include <godot_cpp/classes/node.hpp>
    #include <godot_cpp/classes/thread.hpp>

    namespace godot {
        class MultithreadingDemo : public Node {
            GDCLASS(MultithreadingDemo, Node);

        private:
            Ref<Thread> worker;

        protected:
            static void _bind_methods();
            void _notification(int p_what);

        public:
            MultithreadingDemo();
            ~MultithreadingDemo();

            void demo_threaded_function();
        };
    } // namespace godot

 .. code-tab:: cpp C++ .CPP File

    #include "multithreading_demo.h"

    #include <godot_cpp/classes/engine.hpp>
    #include <godot_cpp/classes/os.hpp>
    #include <godot_cpp/classes/time.hpp>
    #include <godot_cpp/core/class_db.hpp>
    #include <godot_cpp/variant/utility_functions.hpp>

    using namespace godot;

    void MultithreadingDemo::_bind_methods() {
        ClassDB::bind_method(D_METHOD("threaded_function"), &MultithreadingDemo::demo_threaded_function);
    }

    void MultithreadingDemo::_notification(int p_what) {
        // Ngăn đoạn này chạy trong editor, chỉ chạy trong game mode. Trong Godot 4.3+ hãy sử dụng Runtime classes.
        if (Engine::get_singleton()->is_editor_hint()) {
            return;
        }

        switch (p_what) {
            case NOTIFICATION_READY: {
                worker.instantiate();
                worker->start(callable_mp(this, &MultithreadingDemo::demo_threaded_function), Thread::PRIORITY_NORMAL);
            } break;
            case NOTIFICATION_EXIT_TREE: { // Thread phải được giải phóng (hoặc "joined") để đảm bảo tính portable.
                // Chờ cho đến khi nó thoát.
                if (worker.is_valid()) {
                    worker->wait_to_finish();
                }

                worker.unref();
            } break;
        }
    }

    MultithreadingDemo::MultithreadingDemo() {
        // Khởi tạo mọi biến tại đây.
    }

    MultithreadingDemo::~MultithreadingDemo() {
        // Thêm phần cleanup của bạn tại đây.
    }

    void MultithreadingDemo::demo_threaded_function() {
        UtilityFunctions::print("demo_threaded_function started!");
        int i = 0;
        uint64_t start = Time::get_singleton()->get_ticks_msec();
        while (Time::get_singleton()->get_ticks_msec() - start < 5000) {
            OS::get_singleton()->delay_msec(10);
            i++;
        }

        UtilityFunctions::print("demo_threaded_function counted to: ", i, ".");
    }

Sau đó, hàm của bạn sẽ chạy trong một thread riêng cho đến khi hàm trả về. Ngay cả khi hàm đã trả về, thread vẫn phải thu thập nó, vì vậy hãy gọi
:ref:`Thread.wait_to_finish()<class_Thread_method_wait_to_finish>`, which will
chờ cho đến khi thread hoàn tất (nếu chưa hoàn tất), sau đó giải phóng nó đúng cách.

.. warning::

    Việc tạo thread là một thao tác chậm, đặc biệt là trên Windows. Để tránh overhead hiệu năng không cần thiết, hãy đảm bảo tạo các thread trước khi cần xử lý nặng thay vì chỉ tạo thread đúng lúc cần dùng.

    Ví dụ: nếu bạn cần nhiều thread trong khi chơi game, bạn có thể tạo các thread trong lúc level đang tải và chỉ thực sự bắt đầu xử lý bằng chúng sau đó.

    Ngoài ra, việc lock và unlock mutex cũng có thể là một thao tác tốn kém. Cần lock cẩn thận; tránh lock quá thường xuyên (hoặc trong thời gian quá lâu).

.. _doc_using_multiple_threads_mutexes:

Mutex
-----

Việc truy cập các object hoặc dữ liệu từ nhiều thread không phải lúc nào cũng được hỗ trợ (nếu thực hiện, bạn sẽ gây ra các hành vi không mong muốn hoặc crash). Hãy đọc
:ref:`doc_thread_safe_apis` documentation to understand which engine APIs
hỗ trợ truy cập từ nhiều thread.

Khi xử lý dữ liệu của riêng bạn hoặc gọi các hàm của riêng bạn, theo nguyên tắc chung, hãy cố gắng tránh truy cập trực tiếp cùng một dữ liệu từ các thread khác nhau. Bạn có thể gặp vấn đề đồng bộ hóa, vì dữ liệu không phải lúc nào cũng được cập nhật giữa các CPU core khi bị thay đổi. Luôn sử dụng một :ref:`Mutex<class_Mutex>` khi truy cập một phần dữ liệu từ các thread khác nhau.

Khi gọi :ref:`Mutex.lock()<class_Mutex_method_lock>`, một thread sẽ đảm bảo rằng tất cả các thread khác bị block (được đặt ở trạng thái suspended) nếu chúng cố *lock* cùng một mutex. Khi mutex được unlock bằng cách gọi
:ref:`Mutex.unlock()<class_Mutex_method_unlock>`, the other threads will be
được phép tiếp tục với lock (nhưng mỗi lần chỉ một thread).

Sau đây là ví dụ về cách sử dụng một Mutex:

.. tabs::
 .. code-tab:: gdscript GDScript

    var counter := 0
    var mutex: Mutex
    var thread: Thread


    # Thread sẽ bắt đầu tại đây.
    func _ready():
        mutex = Mutex.new()
        thread = Thread.new()
        thread.start(_thread_function)

        # Tăng giá trị và bảo vệ nó bằng Mutex.
        mutex.lock()
        counter += 1
        mutex.unlock()


    # Cũng tăng giá trị từ thread.
    func _thread_function():
        mutex.lock()
        counter += 1
        mutex.unlock()


    # Thread phải được giải phóng (hoặc "joined") để đảm bảo tính portable.
    func _exit_tree():
        thread.wait_to_finish()
        print("Counter is: ", counter) # Phải là 2.

 .. code-tab:: cpp C++ .H File

    #pragma once

    #include <godot_cpp/classes/mutex.hpp>
    #include <godot_cpp/classes/node.hpp>
    #include <godot_cpp/classes/thread.hpp>

    namespace godot {
        class MutexDemo : public Node {
            GDCLASS(MutexDemo, Node);

        private:
            int counter = 0;
            Ref<Mutex> mutex;
            Ref<Thread> thread;

        protected:
            static void _bind_methods();
            void _notification(int p_what);

        public:
            MutexDemo();
            ~MutexDemo();

            void thread_function();
        };
    } // namespace godot

 .. code-tab:: cpp C++ .CPP File

    #include "mutex_demo.h"

    #include <godot_cpp/classes/engine.hpp>
    #include <godot_cpp/classes/time.hpp>
    #include <godot_cpp/core/class_db.hpp>
    #include <godot_cpp/variant/utility_functions.hpp>

    using namespace godot;

    void MutexDemo::_bind_methods() {
        ClassDB::bind_method(D_METHOD("thread_function"), &MutexDemo::thread_function);
    }

    void MutexDemo::_notification(int p_what) {
        // Ngăn đoạn này chạy trong editor, chỉ chạy trong game mode.
        if (Engine::get_singleton()->is_editor_hint()) {
            return;
        }

        switch (p_what) {
            case NOTIFICATION_READY: {
                UtilityFunctions::print("Mutex Demo Counter is starting at: ", counter);
                mutex.instantiate();
                thread.instantiate();
                thread->start(callable_mp(this, &MutexDemo::thread_function), Thread::PRIORITY_NORMAL);

                // Tăng giá trị và bảo vệ nó bằng Mutex.
                mutex->lock();
                counter += 1;
                UtilityFunctions::print("Mutex Demo Counter is ", counter, " after adding with Mutex protection.");
                mutex->unlock();
            } break;
            case NOTIFICATION_EXIT_TREE: { // Thread phải được giải phóng (hoặc "joined") để đảm bảo tính portable.
                // Chờ cho đến khi nó thoát.
                if (thread.is_valid()) {
                    thread->wait_to_finish();
                }
                thread.unref();

                UtilityFunctions::print("Mutex Demo Counter is ", counter, " at EXIT_TREE."); // Phải là 2.
            } break;
        }
    }

    MutexDemo::MutexDemo() {
        // Khởi tạo mọi biến tại đây.
    }

    MutexDemo::~MutexDemo() {
        // Thêm phần cleanup của bạn tại đây.
    }

    // Cũng tăng giá trị từ thread.
    void MutexDemo::thread_function() {
        mutex->lock();
        counter += 1;
        mutex->unlock();
    }

Semaphore
---------

Đôi khi bạn muốn thread của mình làm việc *"theo yêu cầu"*. Nói cách khác, hãy cho thread biết khi nào cần làm việc và để nó suspend khi không làm gì. Để thực hiện việc này, :ref:`Semaphores<class_Semaphore>` được sử dụng. Hàm
:ref:`Semaphore.wait()<class_Semaphore_method_wait>` is used in the thread to
suspend thread cho đến khi có dữ liệu đến.

Ngược lại, thread chính sử dụng
:ref:`Semaphore.post()<class_Semaphore_method_post>` to signal that data is
sẵn sàng để được xử lý:

.. tabs::
 .. code-tab:: gdscript GDScript

    var counter := 0
    var mutex: Mutex
    var semaphore: Semaphore
    var thread: Thread
    var exit_thread := false


    # Thread sẽ bắt đầu tại đây.
    func _ready():
        mutex = Mutex.new()
        semaphore = Semaphore.new()
        exit_thread = false

        thread = Thread.new()
        thread.start(_thread_function)


    func _thread_function():
        while true:
            semaphore.wait() # Chờ cho đến khi được post.

            mutex.lock()
            var should_exit = exit_thread # Bảo vệ bằng Mutex.
            mutex.unlock()

            if should_exit:
                break

            mutex.lock()
            counter += 1 # Tăng counter và bảo vệ bằng Mutex.
            mutex.unlock()


    func increment_counter():
        semaphore.post() # Cho thread thực hiện xử lý.


    func get_counter():
        mutex.lock()
        # Sao chép counter và bảo vệ bằng Mutex.
        var counter_value = counter
        mutex.unlock()
        return counter_value


    # Thread phải được giải phóng (hoặc "joined") để đảm bảo tính portable.
    func _exit_tree():
        # Đặt điều kiện thoát thành true.
        mutex.lock()
        exit_thread = true # Bảo vệ bằng Mutex.
        mutex.unlock()

        # Bỏ block bằng cách post.
        semaphore.post()

        # Chờ cho đến khi nó thoát.
        thread.wait_to_finish()

        # In counter.
        print("Counter is: ", counter)

 .. code-tab:: cpp C++ .H File

    #pragma once

    #include <godot_cpp/classes/mutex.hpp>
    #include <godot_cpp/classes/node.hpp>
    #include <godot_cpp/classes/semaphore.hpp>
    #include <godot_cpp/classes/thread.hpp>

    namespace godot {
        class SemaphoreDemo : public Node {
            GDCLASS(SemaphoreDemo, Node);

        private:
            int counter = 0;
            Ref<Mutex> mutex;
            Ref<Semaphore> semaphore;
            Ref<Thread> thread;
            bool exit_thread = false;

        protected:
            static void _bind_methods();
            void _notification(int p_what);

        public:
            SemaphoreDemo();
            ~SemaphoreDemo();

            void thread_function();
            void increment_counter();
            int get_counter();
        };
    } // namespace godot

 .. code-tab:: cpp C++ .CPP File

    #include "semaphore_demo.h"

    #include <godot_cpp/classes/engine.hpp>
    #include <godot_cpp/classes/time.hpp>
    #include <godot_cpp/core/class_db.hpp>
    #include <godot_cpp/variant/utility_functions.hpp>

    using namespace godot;

    void SemaphoreDemo::_bind_methods() {
        ClassDB::bind_method(D_METHOD("thread_function"), &SemaphoreDemo::thread_function);
    }

    void SemaphoreDemo::_notification(int p_what) {
        // Ngăn đoạn này chạy trong editor, chỉ chạy trong game mode.
        if (Engine::get_singleton()->is_editor_hint()) {
            return;
        }

        switch (p_what) {
            case NOTIFICATION_READY: {
                UtilityFunctions::print("Semaphore Demo Counter is starting at: ", counter);
                mutex.instantiate();
                semaphore.instantiate();
                exit_thread = false;

                thread.instantiate();
                thread->start(callable_mp(this, &SemaphoreDemo::thread_function), Thread::PRIORITY_NORMAL);

                increment_counter(); // Gọi increment counter để kiểm tra.
            } break;
            case NOTIFICATION_EXIT_TREE: { // Thread phải được giải phóng (hoặc "joined") để đảm bảo tính portable.
                // Đặt điều kiện thoát thành true.
                mutex->lock();
                exit_thread = true; // Bảo vệ bằng Mutex.
                mutex->unlock();

                // Bỏ block bằng cách post.
                semaphore->post();

                // Chờ cho đến khi nó thoát.
                if (thread.is_valid()) {
                    thread->wait_to_finish();
                }
                thread.unref();

                // In counter.
                UtilityFunctions::print("Semaphore Demo Counter is ", get_counter(),  " at EXIT_TREE.");
            } break;
        }
    }

    SemaphoreDemo::SemaphoreDemo() {
        // Khởi tạo mọi biến tại đây.
    }

    SemaphoreDemo::~SemaphoreDemo() {
        // Thêm phần cleanup của bạn tại đây.
    }

    // Cũng tăng giá trị từ thread.
    void SemaphoreDemo::thread_function() {
        while (true) {
            semaphore->wait(); // Chờ cho đến khi được post.

            mutex->lock();
            bool should_exit = exit_thread; // Bảo vệ bằng Mutex.
            mutex->unlock();

            if (should_exit) {
                break;
            }

            mutex->lock();
            counter += 1; // Tăng counter và bảo vệ bằng Mutex.
            mutex->unlock();
        }
    }

    void SemaphoreDemo::increment_counter() {
        semaphore->post(); // Cho thread thực hiện xử lý.
    }

    int SemaphoreDemo::get_counter() {
        mutex->lock();
        // Sao chép counter và bảo vệ bằng Mutex.
        int counter_value = counter;
        mutex->unlock();
        return counter_value;
    }
