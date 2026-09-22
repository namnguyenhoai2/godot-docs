.. _doc_object_class:

Lớp Object
==========

.. seealso::

    Trang này mô tả cách triển khai các object trong Godot bằng C++. Bạn đang tìm tài liệu tham chiếu về lớp Object? :ref:`Hãy xem tại đây. <class_Object>`

Định nghĩa chung
----------------

:ref:`Object <class_object>` là lớp cơ sở cho hầu hết mọi thứ. Hầu hết các lớp trong Godot kế thừa trực tiếp hoặc gián tiếp từ lớp này. Việc khai báo chúng chỉ cần sử dụng một macro duy nhất như sau:

.. code-block:: cpp

    class CustomObject : public Object {
        GDCLASS(CustomObject, Object); // Điều này là bắt buộc để kế thừa từ Object.
    };

Object đi kèm nhiều chức năng tích hợp sẵn, chẳng hạn như reflection và các thuộc tính có thể chỉnh sửa:

.. code-block:: cpp

    CustomObject *obj = memnew(CustomObject);
    print_line("Object class: ", obj->get_class()); // in lớp của object

    OtherClass *obj2 = Object::cast_to<OtherClass>(obj); // Chuyển đổi giữa các lớp, tương tự như dynamic_cast

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `core/object/object.h <https://github.com/godotengine/godot/blob/master/core/object/object.h>`__

Đăng ký các lớp Object
----------------------

Hầu hết các lớp con của ``Object`` được đăng ký bằng cách gọi ``GDREGISTER_CLASS``.

.. code-block:: cpp

    GDREGISTER_CLASS(MyCustomClass)

Thao tác này sẽ đăng ký lớp dưới dạng một lớp công khai có tên trong ``ClassDB``, cho phép khởi tạo lớp bằng script, code hoặc quá trình deserialization. Lưu ý rằng các lớp được đăng ký dưới dạng ``GDREGISTER_CLASS`` nên được tạo hoặc giải phóng tự động, chẳng hạn như bởi editor hoặc hệ thống tài liệu.

Ngoài ``GDREGISTER_CLASS``, còn có một số chế độ riêng tư khác:

.. code-block:: cpp

    // Đăng ký lớp công khai nhưng ngăn không cho tự động khởi tạo thông qua ClassDB.
    GDREGISTER_VIRTUAL_CLASS(MyCustomClass);

    // Đăng ký lớp công khai nhưng ngăn mọi hoạt động khởi tạo thông qua ClassDB.
    GDREGISTER_ABSTRACT_CLASS(MyCustomClass);

    // Đăng ký lớp trong ClassDB nhưng đánh dấu lớp là riêng tư,
    // do đó lớp không hiển thị với script hoặc extension.
    // Điều này tương đương với việc hoàn toàn không đăng ký lớp một cách tường minh
    // - trong trường hợp này, class được tự động đăng ký là internal
    // khi được khởi tạo lần đầu.
    GDREGISTER_INTERNAL_CLASS(MyCustomClass);

    // Đăng ký lớp để lớp chỉ khả dụng trong runtime (nhưng không khả dụng trong editor).
    GDREGISTER_RUNTIME_CLASS(MyCustomClass);

Cũng có thể sử dụng ``GDSOFTCLASS(MyCustomClass, SuperClass)`` thay cho ``GDCLASS(MyCustomClass, SuperClass)``. Các lớp được định nghĩa theo cách này hoàn toàn không được đăng ký trong ``ClassDB``. Cách này đôi khi được sử dụng cho các lớp con dành riêng cho từng nền tảng.

Đăng ký binding
~~~~~~~~~~~~~~~

Các lớp kế thừa từ Object có thể override hàm static ``static void _bind_methods()``. Khi lớp được đăng ký, hàm static này được gọi để đăng ký tất cả method, property, constant, v.v. của object. Hàm này chỉ được gọi một lần.

Bên trong ``_bind_methods``, có một số việc có thể thực hiện. Một trong số đó là đăng ký function:

.. code-block:: cpp

    ClassDB::bind_method(D_METHOD("methodname", "arg1name", "arg2name", "arg3name"), &MyCustomType::method);

Có thể truyền giá trị mặc định cho các argument dưới dạng tham số ở cuối:

.. code-block:: cpp

    ClassDB::bind_method(D_METHOD("methodname", "arg1name", "arg2name", "arg3name"), &MyCustomType::method, DEFVAL(-1), DEFVAL(-2)); // Giá trị mặc định cho arg2name (-1) và arg3name (-2).

Giá trị mặc định phải được cung cấp theo đúng thứ tự khai báo, bỏ qua các argument bắt buộc rồi cung cấp giá trị mặc định cho các argument tùy chọn. Điều này khớp với cú pháp khai báo method trong C++.

``D_METHOD`` là một macro chuyển đổi "methodname" thành một StringName để tăng hiệu quả. Tên argument được sử dụng cho mục đích introspection, nhưng khi biên dịch bản release, macro sẽ bỏ qua chúng, nên các string này không được sử dụng và sẽ được tối ưu loại bỏ.

Hãy xem ``_bind_methods`` của Control hoặc Object để biết thêm ví dụ.

Nếu chỉ thêm module và chức năng không cần được tài liệu hóa quá chi tiết, có thể an toàn bỏ qua macro ``D_METHOD()`` và truyền một string chứa tên để viết ngắn gọn hơn.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/object/class_db.h <https://github.com/godotengine/godot/blob/master/core/object/class_db.h>`__

Constant
~~~~~~~~

Các lớp thường có enum như sau:

.. code-block:: cpp

    enum SomeMode {
       MODE_FIRST,
       MODE_SECOND
    };

Để hoạt động khi binding với method, enum phải được khai báo có thể chuyển đổi thành int. Có một macro được cung cấp để hỗ trợ việc này:

.. code-block:: cpp

    VARIANT_ENUM_CAST(MyClass::SomeMode); // giờ đây có thể binding các function nhận SomeMode.

Các constant cũng có thể được binding bên trong ``_bind_methods`` bằng cách sử dụng:

.. code-block:: cpp

    BIND_CONSTANT(MODE_FIRST);
    BIND_CONSTANT(MODE_SECOND);

Property (set/get)
~~~~~~~~~~~~~~~~~~

Object export các property; property hữu ích cho những mục đích sau:

-  Serialize và deserialize object.
-  Tạo danh sách các giá trị có thể chỉnh sửa cho lớp kế thừa từ Object.

Property thường được định nghĩa bằng lớp PropertyInfo() và được khởi tạo như sau:

.. code-block:: cpp

    PropertyInfo(type, name, hint, hint_string, usage_flags)

Ví dụ:

.. code-block:: cpp

    PropertyInfo(Variant::INT, "amount", PROPERTY_HINT_RANGE, "0,49,1", PROPERTY_USAGE_EDITOR)

Đây là một property kiểu integer có tên "amount". Hint là một range, với phạm vi từ 0 đến 49 và bước là 1 (số nguyên). Property này chỉ dùng được trong editor (chỉnh sửa giá trị bằng giao diện trực quan) nhưng sẽ không được serialize.

Một ví dụ khác:

.. code-block:: cpp

    PropertyInfo(Variant::STRING, "modes", PROPERTY_HINT_ENUM, "Enabled,Disabled,Turbo")

Đây là một property kiểu string, có thể nhận mọi string nhưng editor chỉ cho phép các giá trị hint đã định nghĩa. Vì không chỉ định usage flag nào, các flag mặc định là PROPERTY_USAGE_STORAGE và PROPERTY_USAGE_EDITOR.

Có rất nhiều hint và usage flag khả dụng trong object.h, hãy xem qua chúng.

Property cũng có thể hoạt động giống property trong C# và được truy cập từ script bằng indexing, nhưng cách sử dụng này thường không được khuyến khích vì dùng function dễ đọc hơn. Nhiều property cũng được binding với category, chẳng hạn như "animation/frame", khiến việc indexing không thể thực hiện trừ khi sử dụng operator [].

Từ ``_bind_methods()``, có thể tạo và binding property miễn là tồn tại các function set/get. Ví dụ:

.. code-block:: cpp

    ADD_PROPERTY(PropertyInfo(Variant::INT, "amount"), "set_amount", "get_amount")

Thao tác này tạo property bằng setter và getter.

.. _doc_binding_properties_using_set_get_property_list:

Binding property bằng ``_set``/``_get``/``_get_property_list``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có một phương pháp bổ sung để tạo property khi cần sự linh hoạt cao hơn (ví dụ: thêm hoặc xóa property trong context).

Các hàm sau đây có thể được override trong một class dẫn xuất từ Object; chúng KHÔNG phải là virtual, KHÔNG biến chúng thành virtual; chúng được gọi cho mọi override và các hàm trước đó không bị vô hiệu hóa (lời gọi đa cấp).

.. code-block:: cpp

    protected:
         void _get_property_list(List<PropertyInfo> *r_props) const;      // trả về danh sách thuộc tính
         bool _get(const StringName &p_property, Variant &r_value) const; // trả về true nếu tìm thấy thuộc tính
         bool _set(const StringName &p_property, const Variant &p_value); // trả về true nếu tìm thấy thuộc tính

Điều này cũng kém hiệu quả hơn một chút vì ``p_property`` phải được so sánh tuần tự với các tên mong muốn.


Tín hiệu
~~~~~~~~

Các Object có thể có một tập hợp tín hiệu được định nghĩa (tương tự Delegates trong các ngôn ngữ khác). Ví dụ này cho biết cách kết nối với chúng:

.. code-block:: cpp

    // Đây là chữ ký của hàm:
    //
    // Error connect(const StringName &p_signal, const Callable &p_callable, uint32_t p_flags = 0)
    //
    // Ví dụ:
    obj->connect("signal_name_here", callable_mp(this, &MyCustomType::method), CONNECT_DEFERRED);

``callable_mp`` là một macro để tạo con trỏ hàm callable tùy chỉnh đến các hàm thành viên. Để biết các giá trị của ``p_flags``, hãy xem :ref:`ConnectFlags <enum_Object_ConnectFlags>`.

Có thể thêm tín hiệu vào một class trong ``_bind_methods``, bằng macro ``ADD_SIGNAL``, chẳng hạn như:

.. code-block:: cpp

    ADD_SIGNAL(MethodInfo("been_killed"))

Quyền sở hữu và ép kiểu Object
------------------------------

Các Object được cấp phát trên heap. Có hai mô hình quyền sở hữu khác nhau:

- Các Object dẫn xuất từ ``RefCounted`` được đếm tham chiếu.
- Tất cả các Object khác được quản lý bộ nhớ thủ công.

Các mô hình quyền sở hữu này khác nhau về bản chất. Hãy tham khảo phần tương ứng để tìm hiểu cách tạo, lưu trữ và giải phóng Object.

Khi không biết một Object được truyền cho bạn (thông qua ``Object *``) có phải là ``RefCounted`` hay không và cần lưu trữ nó, bạn nên lưu trữ ``ObjectID`` của nó thay vì một con trỏ (như được giải thích bên dưới, trong phần quản lý bộ nhớ thủ công).

Khi một Object được truyền cho bạn thông qua :ref:`Variant<class_Variant>`, đặc biệt là khi sử dụng các callback trì hoãn, có thể ``Object *`` bên trong đã được giải phóng trước khi hàm của bạn chạy. Thay vì chuyển đổi trực tiếp sang ``Object *``, bạn nên sử dụng ``get_validated_object``:

.. code-block:: cpp

    void do_something(Variant p_variant) {
        Object *object = p_variant.get_validated_object();
        ERR_FAIL_NULL(object);
    }

Quản lý bộ nhớ thủ công
~~~~~~~~~~~~~~~~~~~~~~~

Các Object được quản lý bộ nhớ thủ công được tạo bằng ``memnew`` và được giải phóng bằng ``memdelete``:

.. code-block:: cpp

    Node *node = memnew(Node);
    // ...
    memdelete(node);
    node = nullptr;

Khi bạn không phải là chủ sở hữu duy nhất của một Object, việc lưu trữ con trỏ đến nó rất nguy hiểm: Object có thể bị giải phóng bất kỳ lúc nào thông qua các tham chiếu khác đến nó, khiến con trỏ của bạn trở thành dangling pointer, cuối cùng dẫn đến crash.

Khi lưu trữ các Object mà bạn không phải là chủ sở hữu duy nhất, bạn nên lưu trữ ``ObjectID`` của nó thay vì một con trỏ:

.. code-block:: cpp

    Node *node = memnew(Node);
    ObjectID node_id = node.get_instance_id();
    // ...
    Object *maybe_node = ObjectDB::get_instance(node_id);
    ERR_FAIL_NULL(maybe_node); // Node có thể đã được giải phóng giữa các lần gọi.

``RefCounted`` quản lý bộ nhớ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Các subclass của :ref:`RefCounted <class_RefCounted>` được quản lý bộ nhớ bằng `cơ chế đếm tham chiếu <https://en.wikipedia.org/wiki/Reference_counting>`__.

Chúng được tạo bằng ``memnew`` và nên được lưu trữ trong các instance ``Ref``. Khi instance ``Ref`` cuối cùng bị loại bỏ, Object sẽ tự động tự hủy.

.. code-block:: cpp

    class MyRefCounted: public RefCounted {
        GDCLASS(MyRefCounted, RefCounted);
    };

    Ref<MyRefCounted> my_ref = memnew(MyRefCounted);
    // ...
    // Ref nắm quyền sở hữu dùng chung đối với Object, vì vậy Object
    // sẽ không bị giải phóng. Chừng nào bạn còn có một
    // Ref hợp lệ, khác null, có thể an toàn giả định rằng Object vẫn còn hợp lệ.
    my_ref->get_class_name();

Bạn không bao giờ được gọi ``memdelete`` cho các subclass ``RefCounted``, vì có thể còn những chủ sở hữu khác của chúng.

Bạn cũng không bao giờ được lưu trữ các subclass ``RefCounted`` bằng con trỏ thô, chẳng hạn như ``RefCounted *object = memnew(RefCounted)``. Điều này không an toàn vì các chủ sở hữu khác có thể hủy Object, khiến bạn còn một dangling pointer, cuối cùng dẫn đến crash.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/object/ref_counted.h <https://github.com/godotengine/godot/blob/master/core/object/ref_counted.h>`__

Ép kiểu động
~~~~~~~~~~~~

Godot cung cấp khả năng ép kiểu động giữa các class dẫn xuất từ Object, chẳng hạn như:

.. code-block:: cpp

    void some_func(Object *p_object) {
         Button *button = Object::cast_to<Button>(p_object);
    }

Nếu ép kiểu thất bại, ``nullptr`` sẽ được trả về. Cách này hoạt động giống như ``dynamic_cast``, nhưng không sử dụng `RTTI C++ <https://en.wikipedia.org/wiki/Run-time_type_information>`__.

Thông báo
---------

Tất cả Object trong Godot đều có một phương thức :ref:`_notification <class_Object_private_method__notification>`, cho phép chúng phản hồi các callback cấp engine có thể liên quan đến chúng. Bạn có thể tìm thêm thông tin trên trang :ref:`doc_godot_notifications`.


Resource
--------

:ref:`Resource <class_resource>` kế thừa từ RefCounted, vì vậy tất cả resource đều được đếm tham chiếu. Resource có thể tùy chọn chứa một path tham chiếu đến một file trên đĩa. Có thể thiết lập path này bằng ``resource.set_path(path)``, mặc dù thông thường resource loader sẽ thực hiện việc đó. Không có hai resource khác nhau nào có thể có cùng một path; nếu cố thực hiện, sẽ xảy ra lỗi.

Resource không có path cũng hoàn toàn hợp lệ.

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `core/io/resource.h <https://github.com/godotengine/godot/blob/master/core/io/resource.h>`__

Tải resource
~~~~~~~~~~~~

Có thể tải resource bằng ResourceLoader API như sau:

.. code-block:: cpp

    Ref<Resource> res = ResourceLoader::load("res://someresource.res")

Nếu một tham chiếu đến resource đó đã được tải trước đó và đang ở trong bộ nhớ, :ref:`ResourceLoader <class_ResourceLoader>` sẽ trả về tham chiếu đó. Điều này có nghĩa là tại cùng một thời điểm chỉ có thể tải một resource từ một file được tham chiếu trên đĩa.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/io/resource_loader.h <https://github.com/godotengine/godot/blob/master/core/io/resource_loader.h>`__

Lưu resource
~~~~~~~~~~~~

Có thể lưu resource bằng resource saver API:

.. code-block:: cpp

    ResourceSaver::save("res://someresource.res", instance)

Instance sẽ được lưu, còn các sub-resource có path đến một file sẽ được lưu dưới dạng tham chiếu đến resource đó. Các sub-resource không có path sẽ được đóng gói cùng resource đã lưu và được gán sub-ID, chẳng hạn như ``res://someresource.res::1``. Điều này cũng giúp lưu chúng vào cache khi được tải.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/io/resource_saver.h <https://github.com/godotengine/godot/blob/master/core/io/resource_saver.h>`__
