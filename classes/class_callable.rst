:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Callable.xml.

.. _class_Callable:

Callable
========

Một kiểu tích hợp biểu diễn một method hoặc một function độc lập.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Callable** là một kiểu :ref:`Variant<class_Variant>` tích hợp, biểu diễn một function. Nó có thể là một method bên trong một instance :ref:`Object<class_Object>`, hoặc một callable tùy chỉnh được dùng cho các mục đích khác nhau (xem :ref:`is_custom()<class_Callable_method_is_custom>`). Giống như mọi kiểu :ref:`Variant<class_Variant>`, nó có thể được lưu trữ trong các biến và truyền cho các function khác. Nó thường được dùng nhất cho các signal callback.


.. tabs::

 .. code-tab:: gdscript

    func print_args(arg1, arg2, arg3 = ""):
        prints(arg1, arg2, arg3)

    func test():
        var callable = Callable(self, "print_args")
        callable.call("hello", "world")  # In "hello world ".
        callable.call(Vector2.UP, 42, callable)  # In "(0.0, -1.0) 42 Node(node.gd)::print_args"
        callable.call("invalid")  # Lệnh gọi không hợp lệ, phải có ít nhất 2 đối số.

 .. code-tab:: csharp

    // Không hỗ trợ giá trị tham số mặc định.
    public void PrintArgs(Variant arg1, Variant arg2, Variant arg3 = default)
    {
        GD.PrintS(arg1, arg2, arg3);
    }

    public void Test()
    {
        // Các lệnh gọi không hợp lệ sẽ âm thầm thất bại.
        Callable callable = new Callable(this, MethodName.PrintArgs);
        callable.Call("hello", "world"); // Không hỗ trợ giá trị tham số mặc định, phải có 3 đối số.
        callable.Call(Vector2.Up, 42, callable); // In "(0, -1) 42 Node(Node.cs)::PrintArgs"
        callable.Call("invalid"); // Lệnh gọi không hợp lệ, phải có 3 đối số.
    }



Trong GDScript, bạn có thể tạo các hàm lambda bên trong một method. Các hàm lambda là những callable tùy chỉnh không liên kết với một instance :ref:`Object<class_Object>`. Ngoài ra, hàm lambda cũng có thể được đặt tên. Tên này sẽ được hiển thị trong debugger hoặc khi gọi :ref:`get_method()<class_Callable_method_get_method>`.

::

    func _init():
        var my_lambda = func (message):
            print(message)

        # In "Hello everyone!"
        my_lambda.call("Hello everyone!")

        # In "Attack!" khi signal button_pressed được phát.
        button_pressed.connect(func(): print("Attack!"))

Trong GDScript, bạn có thể truy cập các method và function toàn cục dưới dạng **Callable**\ s:

::

    tween.tween_callback(node.queue_free)  # Các method của object.
    tween.tween_callback(array.clear)  # Các method của kiểu tích hợp.
    tween.tween_callback(print.bind("Test"))  # Các function toàn cục.

\ **Lưu ý:** :ref:`Dictionary<class_Dictionary>` không hỗ trợ những điều trên do có thể gây nhầm lẫn với các key.

::

    var dictionary = { "hello": "world" }

    # Cách này sẽ không hoạt động vì `clear` được xem là một key.
    tween.tween_callback(dictionary.clear)

    # Cách này sẽ hoạt động.
    tween.tween_callback(Callable.create(dictionary, "clear"))

\ **Lưu ý:** Trong ngữ cảnh boolean, một callable sẽ được đánh giá là ``false`` nếu nó là null (xem :ref:`is_null()<class_Callable_method_is_null>`). Nếu không, callable sẽ luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-reftable-group

Constructors
------------

.. table::
   :widths: auto

   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Callable<class_Callable>` | :ref:`Callable<class_Callable_constructor_Callable>`\ (\ )                                                                                     |
   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Callable<class_Callable>` | :ref:`Callable<class_Callable_constructor_Callable>`\ (\ from\: :ref:`Callable<class_Callable>`\ )                                             |
   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Callable<class_Callable>` | :ref:`Callable<class_Callable_constructor_Callable>`\ (\ object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`\ ) |
   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Callable<class_Callable>`     | :ref:`bind<class_Callable_method_bind>`\ (\ ...\ ) |vararg| |const|                                                                               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Callable<class_Callable>`     | :ref:`bindv<class_Callable_method_bindv>`\ (\ arguments\: :ref:`Array<class_Array>`\ )                                                            |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`call<class_Callable_method_call>`\ (\ ...\ ) |vararg| |const|                                                                               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`call_deferred<class_Callable_method_call_deferred>`\ (\ ...\ ) |vararg| |const|                                                             |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`callv<class_Callable_method_callv>`\ (\ arguments\: :ref:`Array<class_Array>`\ ) |const|                                                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Callable<class_Callable>`     | :ref:`create<class_Callable_method_create>`\ (\ variant\: :ref:`Variant<class_Variant>`, method\: :ref:`StringName<class_StringName>`\ ) |static| |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_argument_count<class_Callable_method_get_argument_count>`\ (\ ) |const|                                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`get_bound_arguments<class_Callable_method_get_bound_arguments>`\ (\ ) |const|                                                               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_bound_arguments_count<class_Callable_method_get_bound_arguments_count>`\ (\ ) |const|                                                   |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_method<class_Callable_method_get_method>`\ (\ ) |const|                                                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`         | :ref:`get_object<class_Callable_method_get_object>`\ (\ ) |const|                                                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_object_id<class_Callable_method_get_object_id>`\ (\ ) |const|                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_unbound_arguments_count<class_Callable_method_get_unbound_arguments_count>`\ (\ ) |const|                                               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`hash<class_Callable_method_hash>`\ (\ ) |const|                                                                                             |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_custom<class_Callable_method_is_custom>`\ (\ ) |const|                                                                                   |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_null<class_Callable_method_is_null>`\ (\ ) |const|                                                                                       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_standard<class_Callable_method_is_standard>`\ (\ ) |const|                                                                               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_valid<class_Callable_method_is_valid>`\ (\ ) |const|                                                                                     |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`rpc<class_Callable_method_rpc>`\ (\ ...\ ) |vararg| |const|                                                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`rpc_id<class_Callable_method_rpc_id>`\ (\ peer_id\: :ref:`int<class_int>`, ...\ ) |vararg| |const|                                          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Callable<class_Callable>`     | :ref:`unbind<class_Callable_method_unbind>`\ (\ argcount\: :ref:`int<class_int>`\ ) |const|                                                       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Operators
---------

.. table::
   :widths: auto

   +-------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator !=<class_Callable_operator_neq_Callable>`\ (\ right\: :ref:`Callable<class_Callable>`\ ) |
   +-------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator ==<class_Callable_operator_eq_Callable>`\ (\ right\: :ref:`Callable<class_Callable>`\ )  |
   +-------------------------+---------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Constructor
-----------------

.. _class_Callable_constructor_Callable:

.. rst-class:: classref-constructor

:ref:`Callable<class_Callable>` **Callable**\ (\ ) :ref:`🔗<class_Callable_constructor_Callable>`

Tạo một **Callable** rỗng, không liên kết với object hay method nào.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Callable<class_Callable>` **Callable**\ (\ from\: :ref:`Callable<class_Callable>`\ )

Tạo một **Callable** dưới dạng bản sao của **Callable** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Callable<class_Callable>` **Callable**\ (\ object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`\ )

Tạo một **Callable** mới cho method có tên ``method`` trong ``object`` được chỉ định.

\ **Lưu ý:** Đối với các method của kiểu :ref:`Variant<class_Variant>` tích hợp, hãy dùng :ref:`create()<class_Callable_method_create>` thay thế.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_Callable_method_bind:

.. rst-class:: classref-method

:ref:`Callable<class_Callable>` **bind**\ (\ ...\ ) |vararg| |const| :ref:`🔗<class_Callable_method_bind>`

Trả về một bản sao của **Callable** này với một hoặc nhiều đối số được bind. Khi được gọi, các đối số đã bind sẽ được truyền *sau* các đối số do :ref:`call()<class_Callable_method_call>` cung cấp. Xem thêm :ref:`unbind()<class_Callable_method_unbind>`.

\ **Lưu ý:** Khi method này được chain với các method tương tự khác, thứ tự sửa đổi danh sách đối số được đọc từ phải sang trái.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_bindv:

.. rst-class:: classref-method

:ref:`Callable<class_Callable>` **bindv**\ (\ arguments\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Callable_method_bindv>`

Trả về một bản sao của **Callable** này với một hoặc nhiều đối số được bind, đọc chúng từ một array. Khi được gọi, các đối số đã bind sẽ được truyền *sau* các đối số do :ref:`call()<class_Callable_method_call>` cung cấp. Xem thêm :ref:`unbind()<class_Callable_method_unbind>`.

\ **Lưu ý:** Khi method này được chain với các method tương tự khác, thứ tự sửa đổi danh sách đối số được đọc từ phải sang trái.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_call:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **call**\ (\ ...\ ) |vararg| |const| :ref:`🔗<class_Callable_method_call>`

Gọi method được **Callable** này biểu diễn. Có thể truyền các đối số và chúng phải khớp với signature của method.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_call_deferred:

.. rst-class:: classref-method

|void| **call_deferred**\ (\ ...\ ) |vararg| |const| :ref:`🔗<class_Callable_method_call_deferred>`

Gọi method được **Callable** này biểu diễn ở chế độ deferred, tức là vào cuối frame hiện tại. Có thể truyền các đối số và chúng phải khớp với signature của method.


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        grab_focus.call_deferred()

 .. code-tab:: csharp

    public override void _Ready()
    {
        Callable.From(GrabFocus).CallDeferred();
    }



\ **Lưu ý:** Các deferred call được xử lý trong thời gian idle. Thời gian idle chủ yếu diễn ra ở cuối các frame process và physics. Trong thời gian này, các deferred call sẽ được chạy cho đến khi không còn call nào, nghĩa là bạn có thể defer các call từ những deferred call khác và chúng vẫn sẽ được chạy trong cùng chu kỳ idle hiện tại. Điều này có nghĩa là bạn không nên gọi một method ở chế độ deferred từ chính nó (hoặc từ một method được nó gọi), vì việc này gây ra đệ quy vô hạn giống như khi bạn gọi method trực tiếp.

Xem thêm :ref:`Object.call_deferred()<class_Object_method_call_deferred>`.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_callv:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **callv**\ (\ arguments\: :ref:`Array<class_Array>`\ ) |const| :ref:`🔗<class_Callable_method_callv>`

Gọi method được **Callable** này biểu diễn. Không giống :ref:`call()<class_Callable_method_call>`, method này yêu cầu tất cả đối số phải nằm bên trong ``arguments`` :ref:`Array<class_Array>`.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_create:

.. rst-class:: classref-method

:ref:`Callable<class_Callable>` **create**\ (\ variant\: :ref:`Variant<class_Variant>`, method\: :ref:`StringName<class_StringName>`\ ) |static| :ref:`🔗<class_Callable_method_create>`

Tạo một **Callable** mới cho method có tên ``method`` trong ``variant`` được chỉ định. Để biểu diễn một method của kiểu :ref:`Variant<class_Variant>` tích hợp, một callable tùy chỉnh sẽ được sử dụng (xem :ref:`is_custom()<class_Callable_method_is_custom>`). Nếu ``variant`` là :ref:`Object<class_Object>`, thì thay vào đó một callable tiêu chuẩn sẽ được tạo.

\ **Lưu ý:** Method này luôn cần thiết cho kiểu :ref:`Dictionary<class_Dictionary>`, vì cú pháp property được dùng để truy cập các entry của nó. Bạn cũng có thể dùng method này khi chưa biết trước kiểu của ``variant`` (cho tính đa hình).

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_get_argument_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_argument_count**\ (\ ) |const| :ref:`🔗<class_Callable_method_get_argument_count>`

Trả về tổng số đối số mà **Callable** này phải nhận, bao gồm cả các đối số tùy chọn. Điều này có nghĩa là mọi đối số được bind bằng :ref:`bind()<class_Callable_method_bind>` sẽ được *trừ* khỏi kết quả, còn mọi đối số được unbind bằng :ref:`unbind()<class_Callable_method_unbind>` sẽ được *cộng* vào kết quả.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_get_bound_arguments:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_bound_arguments**\ (\ ) |const| :ref:`🔗<class_Callable_method_get_bound_arguments>`

Trả về array gồm các đối số được bind thông qua các lệnh gọi :ref:`bind()<class_Callable_method_bind>` hoặc :ref:`unbind()<class_Callable_method_unbind>` liên tiếp. Các đối số này sẽ được thêm *sau* các đối số được truyền vào lệnh gọi, trong đó :ref:`get_unbound_arguments_count()<class_Callable_method_get_unbound_arguments_count>` đối số ở bên phải đã bị loại trừ trước đó.

::

    func get_effective_arguments(callable, call_args):
        assert(call_args.size() - callable.get_unbound_arguments_count() >= 0)
        var result = call_args.slice(0, call_args.size() - callable.get_unbound_arguments_count())
        result.append_array(callable.get_bound_arguments())
        return result

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_get_bound_arguments_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_bound_arguments_count**\ (\ ) |const| :ref:`🔗<class_Callable_method_get_bound_arguments_count>`

Trả về tổng số đối số được bind thông qua các lệnh gọi :ref:`bind()<class_Callable_method_bind>` hoặc :ref:`unbind()<class_Callable_method_unbind>` liên tiếp. Đây là kích thước của array được :ref:`get_bound_arguments()<class_Callable_method_get_bound_arguments>` trả về. Xem :ref:`get_bound_arguments()<class_Callable_method_get_bound_arguments>` để biết chi tiết.

\ **Lưu ý:** Các method :ref:`get_bound_arguments_count()<class_Callable_method_get_bound_arguments_count>` và :ref:`get_unbound_arguments_count()<class_Callable_method_get_unbound_arguments_count>` đều có thể trả về giá trị dương.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_get_method:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_method**\ (\ ) |const| :ref:`🔗<class_Callable_method_get_method>`

Trả về tên của method được **Callable** này biểu diễn. Nếu callable là một hàm lambda GDScript, trả về tên của function hoặc ``"<anonymous lambda>"``.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_get_object:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_object**\ (\ ) |const| :ref:`🔗<class_Callable_method_get_object>`

Trả về object mà **Callable** này được gọi trên đó.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_get_object_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_object_id**\ (\ ) |const| :ref:`🔗<class_Callable_method_get_object_id>`

Trả về ID của object thuộc **Callable** này (xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`).

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_get_unbound_arguments_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_unbound_arguments_count**\ (\ ) |const| :ref:`🔗<class_Callable_method_get_unbound_arguments_count>`

Trả về tổng số đối số được unbind thông qua các lệnh gọi :ref:`bind()<class_Callable_method_bind>` hoặc :ref:`unbind()<class_Callable_method_unbind>` liên tiếp. Xem :ref:`get_bound_arguments()<class_Callable_method_get_bound_arguments>` để biết chi tiết.

\ **Lưu ý:** Các method :ref:`get_bound_arguments_count()<class_Callable_method_get_bound_arguments_count>` và :ref:`get_unbound_arguments_count()<class_Callable_method_get_unbound_arguments_count>` đều có thể trả về giá trị dương.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_hash:

.. rst-class:: classref-method

:ref:`int<class_int>` **hash**\ (\ ) |const| :ref:`🔗<class_Callable_method_hash>`

Trả về giá trị hash 32-bit của object thuộc **Callable** này.

\ **Lưu ý:** Các **Callable**\ s có nội dung giống nhau sẽ luôn tạo ra các giá trị hash giống hệt nhau. Tuy nhiên, điều ngược lại không đúng. Việc trả về các giá trị hash giống hệt nhau *không* có nghĩa là các callable bằng nhau, vì những callable khác nhau có thể có các giá trị hash giống nhau do xảy ra va chạm hash. Engine sử dụng thuật toán hash 32-bit cho :ref:`hash()<class_Callable_method_hash>`.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_is_custom:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_custom**\ (\ ) |const| :ref:`🔗<class_Callable_method_is_custom>`

Trả về ``true`` nếu **Callable** này là một callable tùy chỉnh. Callable tùy chỉnh được dùng để:

- bind/unbind các đối số (xem :ref:`bind()<class_Callable_method_bind>` và :ref:`unbind()<class_Callable_method_unbind>`);

- biểu diễn các method của kiểu :ref:`Variant<class_Variant>` tích hợp (xem :ref:`create()<class_Callable_method_create>`);

- biểu diễn các function global, lambda và RPC trong GDScript;

- các mục đích khác trong core, GDExtension và C#.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_is_null:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_null**\ (\ ) |const| :ref:`🔗<class_Callable_method_is_null>`

Trả về ``true`` nếu **Callable** này không có target để gọi method. Tương đương với ``callable == Callable()``.

\ **Lưu ý:** Điều này *không* giống ``not is_valid()`` và việc sử dụng ``not is_null()`` sẽ *không* đảm bảo callable này có thể được gọi. Thay vào đó, hãy dùng :ref:`is_valid()<class_Callable_method_is_valid>`.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_is_standard:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_standard**\ (\ ) |const| :ref:`🔗<class_Callable_method_is_standard>`

Trả về ``true`` nếu **Callable** là một callable tiêu chuẩn. Method này ngược với :ref:`is_custom()<class_Callable_method_is_custom>`. Trả về ``false`` nếu callable này là một hàm lambda.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_is_valid:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_valid**\ (\ ) |const| :ref:`🔗<class_Callable_method_is_valid>`

Trả về ``true`` nếu object của callable tồn tại và có tên method hợp lệ được gán, hoặc là một callable tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_rpc:

.. rst-class:: classref-method

|void| **rpc**\ (\ ...\ ) |vararg| |const| :ref:`🔗<class_Callable_method_rpc>`

Thực hiện một RPC (Remote Procedure Call) trên tất cả peer đã kết nối. Tính năng này được dùng cho multiplayer và thường không khả dụng, trừ khi function được gọi đã được đánh dấu là *RPC* (bằng :ref:`@GDScript.@rpc<class_@GDScript_annotation_@rpc>` hoặc :ref:`Node.rpc_config()<class_Node_method_rpc_config>`). Gọi method này trên các function không được hỗ trợ sẽ gây ra lỗi. Xem :ref:`Node.rpc()<class_Node_method_rpc>`.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_rpc_id:

.. rst-class:: classref-method

|void| **rpc_id**\ (\ peer_id\: :ref:`int<class_int>`, ...\ ) |vararg| |const| :ref:`🔗<class_Callable_method_rpc_id>`

Thực hiện một RPC (Remote Procedure Call) trên một peer ID cụ thể (xem tài liệu về multiplayer để tham khảo). Tính năng này được dùng cho multiplayer và thường không khả dụng trừ khi hàm được gọi đã được đánh dấu là *RPC* (bằng :ref:`@GDScript.@rpc<class_@GDScript_annotation_@rpc>` hoặc :ref:`Node.rpc_config()<class_Node_method_rpc_config>`). Việc gọi phương thức này trên các hàm không được hỗ trợ sẽ gây ra lỗi. Xem :ref:`Node.rpc_id()<class_Node_method_rpc_id>`.

.. rst-class:: classref-item-separator

----

.. _class_Callable_method_unbind:

.. rst-class:: classref-method

:ref:`Callable<class_Callable>` **unbind**\ (\ argcount\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Callable_method_unbind>`

Trả về một bản sao của **Callable** với một số đối số không được liên kết. Nói cách khác, khi callable mới được gọi, một vài đối số cuối cùng do người dùng cung cấp sẽ bị bỏ qua, theo ``argcount``. Các đối số còn lại được truyền cho callable. Điều này cho phép sử dụng callable ban đầu trong một ngữ cảnh cố gắng truyền nhiều đối số hơn số đối số mà callable này có thể xử lý, chẳng hạn như một signal có số lượng đối số cố định. Xem thêm :ref:`bind()<class_Callable_method_bind>`.

\ **Lưu ý:** Khi phương thức này được nối chuỗi với các phương thức tương tự khác, thứ tự sửa đổi danh sách đối số được đọc từ phải sang trái.

::

    func _ready():
        foo.unbind(1).call(1, 2) # Gọi foo(1).
        foo.bind(3, 4).unbind(1).call(1, 2) # Gọi foo(1, 3, 4), lưu ý rằng các đối số từ bind không bị thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_Callable_operator_neq_Callable:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_Callable_operator_neq_Callable>`

Trả về ``true`` nếu cả hai **Callable**\ s gọi các target khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_Callable_operator_eq_Callable:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_Callable_operator_eq_Callable>`

Trả về ``true`` nếu cả hai **Callable**\ s gọi cùng một custom target.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
