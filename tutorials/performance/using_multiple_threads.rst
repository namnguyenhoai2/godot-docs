.. _doc_using_multiple_threads:

Sử dụng nhiều thread
====================

.. seealso::

    Để xem danh sách các primitive multithreading trong C++, hãy xem :ref:`doc_core_concurrency_types`.

Thread
------

Thread cho phép thực thi code đồng thời. Nhờ đó, bạn có thể chuyển bớt công việc khỏi thread chính.

Godot hỗ trợ thread và cung cấp nhiều hàm tiện dụng để sử dụng chúng.

.. note:: Nếu sử dụng các ngôn ngữ khác (C#, C++), bạn có thể dễ dàng hơn khi dùng các lớp threading mà chúng hỗ trợ.

.. warning::

    Trước khi sử dụng một lớp tích hợp trong thread, trước tiên hãy đọc tài liệu :ref:`doc_thread_safe_apis` để kiểm tra xem lớp đó có thể được sử dụng an toàn trong thread hay không.

Tạo một Thread
--------------

Để tạo một thread, hãy sử dụng code sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var thread: Thread

    # Thread sẽ bắt đầu tại đây.
    func _ready():
        thread = Thread.new()
        # Bạn có thể liên kết nhiều đối số với một Callable.
        thread.start(_thread_function.bind("Wafflecopter"))


    # Chạy tại đây rồi thoát.
    # Đối số này là dữ liệu đã liên kết được truyền từ start().
    func _thread_function(userdata):
        # In userdata ("Wafflecopter")
        print("I'm a thread! Userdata is: ", userdata)


    # Để đảm bảo tính khả chuyển, Thread phải được giải phóng (hoặc "join").
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
        // Ngăn đoạn này chạy trong editor, chỉ chạy ở chế độ game. Trong Godot 4.3+ hãy sử dụng các lớp Runtime.
        if (Engine::get_singleton()->is_editor_hint()) {
            return;
        }

        switch (p_what) {
            case NOTIFICATION_READY: {
                worker.instantiate();
                worker->start(callable_mp(this, &MultithreadingDemo::demo_threaded_function), Thread::PRIORITY_NORMAL);
            } break;
            case NOTIFICATION_EXIT_TREE: { // Để đảm bảo tính khả chuyển, Thread phải được giải phóng (hoặc "join").
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

Sau đó, hàm của bạn sẽ chạy trong một thread riêng cho đến khi nó trả về. Ngay cả khi hàm đã trả về, thread vẫn phải thu thập nó, vì vậy hãy gọi
:ref:`Thread.wait_to_finish()<class_Thread_method_wait_to_finish>`, hàm này sẽ chờ cho đến khi thread hoàn tất (nếu chưa hoàn tất), sau đó giải phóng thread đúng cách.

.. warning::

    Việc tạo thread là một thao tác chậm, đặc biệt trên Windows. Để tránh overhead hiệu năng không cần thiết, hãy tạo thread trước khi cần xử lý nặng thay vì chỉ tạo chúng đúng lúc cần.

    Ví dụ: nếu cần nhiều thread trong khi chơi game, bạn có thể tạo thread khi level đang được tải và chỉ thực sự bắt đầu xử lý bằng chúng sau đó.

    Ngoài ra, việc lock và unlock mutex cũng có thể là một thao tác tốn kém. Cần lock cẩn thận; tránh lock quá thường xuyên (hoặc trong thời gian quá lâu).

.. _doc_using_multiple_threads_mutexes:

Mutex
-----

Việc truy cập các object hoặc dữ liệu từ nhiều thread không phải lúc nào cũng được hỗ trợ (nếu thực hiện, việc này sẽ gây ra hành vi không mong muốn hoặc crash). Hãy đọc tài liệu
:ref:`doc_thread_safe_apis` để biết những engine API nào hỗ trợ truy cập từ nhiều thread.

Khi xử lý dữ liệu của riêng bạn hoặc gọi các hàm của riêng mình, theo nguyên tắc chung, hãy cố gắng tránh truy cập trực tiếp cùng một dữ liệu từ các thread khác nhau. Bạn có thể gặp vấn đề đồng bộ hóa, vì dữ liệu không phải lúc nào cũng được cập nhật giữa các CPU core khi bị thay đổi. Luôn sử dụng một :ref:`Mutex<class_Mutex>` khi truy cập một phần dữ liệu từ các thread khác nhau.

Khi gọi :ref:`Mutex.lock()<class_Mutex_method_lock>`, một thread đảm bảo rằng tất cả thread khác sẽ bị chặn (chuyển sang trạng thái tạm dừng) nếu chúng cố *lock* cùng mutex đó. Khi mutex được unlock bằng cách gọi
:ref:`Mutex.unlock()<class_Mutex_method_unlock>`, các thread khác sẽ được phép tiếp tục lock (nhưng mỗi lần chỉ một thread).

Sau đây là ví dụ sử dụng một Mutex:

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


    # Để đảm bảo tính khả chuyển, Thread phải được giải phóng (hoặc "join").
    func _exit_tree():
        thread.wait_to_finish()
        print("Counter is: ", counter) # Lẽ ra phải là 2.

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
        // Ngăn đoạn này chạy trong editor, chỉ chạy ở chế độ game.
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
            case NOTIFICATION_EXIT_TREE: { // Để đảm bảo tính khả chuyển, Thread phải được giải phóng (hoặc "join").
                // Chờ cho đến khi nó thoát.
                if (thread.is_valid()) {
                    thread->wait_to_finish();
                }
                thread.unref();

                UtilityFunctions::print("Mutex Demo Counter is ", counter, " at EXIT_TREE."); // Lẽ ra phải là 2.
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

Đôi khi bạn muốn thread của mình hoạt động *"theo yêu cầu"*. Nói cách khác, hãy cho thread biết khi nào cần hoạt động và để nó tạm dừng khi không làm gì. Để thực hiện việc này, :ref:`Semaphores<class_Semaphore>` được sử dụng. Hàm
:ref:`Semaphore.wait()<class_Semaphore_method_wait>` được sử dụng trong thread để tạm dừng thread cho đến khi có dữ liệu đến.

Ngược lại, thread chính sử dụng
:ref:`Semaphore.post()<class_Semaphore_method_post>` để báo hiệu rằng dữ liệu đã sẵn sàng được xử lý:

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
        semaphore.post() # Cho thread xử lý.


    func get_counter():
        mutex.lock()
        # Sao chép counter và bảo vệ bằng Mutex.
        var counter_value = counter
        mutex.unlock()
        return counter_value


    # Để đảm bảo tính khả chuyển, Thread phải được giải phóng (hoặc "join").
    func _exit_tree():
        # Đặt điều kiện thoát thành true.
        mutex.lock()
        exit_thread = true # Bảo vệ bằng Mutex.
        mutex.unlock()

        # Bỏ chặn bằng cách post.
        semaphore.post()

        # Chờ đến khi nó thoát.
        thread.wait_to_finish()

        # In bộ đếm.
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
        // Ngăn không cho đoạn này chạy trong editor, chỉ chạy khi ở chế độ game.
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

                increment_counter(); // Gọi increment counter để kiểm thử.
            } break;
            case NOTIFICATION_EXIT_TREE: { // Thread phải được giải phóng (hoặc "joined") để đảm bảo tính portable.
                // Đặt điều kiện thoát thành true.
                mutex->lock();
                exit_thread = true; // Bảo vệ bằng Mutex.
                mutex->unlock();

                // Bỏ chặn bằng cách post.
                semaphore->post();

                // Chờ đến khi nó thoát.
                if (thread.is_valid()) {
                    thread->wait_to_finish();
                }
                thread.unref();

                // In bộ đếm.
                UtilityFunctions::print("Semaphore Demo Counter is ", get_counter(),  " at EXIT_TREE.");
            } break;
        }
    }

    SemaphoreDemo::SemaphoreDemo() {
        // Khởi tạo mọi biến ở đây.
    }

    SemaphoreDemo::~SemaphoreDemo() {
        // Thêm phần cleanup của bạn ở đây.
    }

    // Tăng giá trị từ thread nữa.
    void SemaphoreDemo::thread_function() {
        while (true) {
            semaphore->wait(); // Chờ đến khi được post.

            mutex->lock();
            bool should_exit = exit_thread; // Bảo vệ bằng Mutex.
            mutex->unlock();

            if (should_exit) {
                break;
            }

            mutex->lock();
            counter += 1; // Tăng bộ đếm, bảo vệ bằng Mutex.
            mutex->unlock();
        }
    }

    void SemaphoreDemo::increment_counter() {
        semaphore->post(); // Tạo process cho thread.
    }

    int SemaphoreDemo::get_counter() {
        mutex->lock();
        // Sao chép bộ đếm, bảo vệ bằng Mutex.
        int counter_value = counter;
        mutex->unlock();
        return counter_value;
    }
