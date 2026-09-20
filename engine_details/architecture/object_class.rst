.. _doc_object_class:

Lớp Object
==========

.. seealso::

    Trang này mô tả cách triển khai object trong C++ của Godot. Bạn đang tìm tài liệu tham chiếu về lớp Object? :ref:`Have a look here. <class_Object>`

Định nghĩa chung
----------------

:ref:`Object <class_object>` is the base class for almost everything. Most classes in Godot
kế thừa trực tiếp hoặc gián tiếp từ nó. Việc khai báo chúng chỉ cần sử dụng một macro đơn như sau:

.. code-block:: cpp

    class CustomObject : public Object {
        GDCLASS(CustomObject, Object); // Điều này là bắt buộc để kế thừa từ Object.
    };

Object có sẵn nhiều chức năng tích hợp, chẳng hạn như reflection và các thuộc tính có thể chỉnh sửa:

.. code-block:: cpp

    CustomObject *obj = memnew(CustomObject);
    print_line("Object class: ", obj->get_class()); // in lớp object

    OtherClass *obj2 = Object::cast_to<OtherClass>(obj); // Chuyển đổi giữa các lớp, tương tự như dynamic_cast

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `core/object/object.h <https://github.com/godotengine/godot/blob/master/core/object/object.h>`__

Đăng ký các lớp Object
----------------------

Hầu hết các lớp con của ``Object`` được đăng ký bằng cách gọi ``GDREGISTER_CLASS``.

.. code-block:: cpp

    GDREGISTER_CLASS(MyCustomClass)

Thao tác này sẽ đăng ký lớp dưới dạng một lớp công khai có tên trong ``ClassDB``, cho phép khởi tạo lớp bằng script, code hoặc quá trình deserialization. Lưu ý rằng các lớp được đăng ký dưới dạng ``GDREGISTER_CLASS`` nên được thiết kế để hệ thống tự động khởi tạo hoặc giải phóng, chẳng hạn như bởi editor hoặc hệ thống tài liệu.

Ngoài ``GDREGISTER_CLASS``, còn có một số chế độ riêng tư khác:

.. code-block:: cpp

    // Đăng ký lớp ở chế độ công khai, nhưng ngăn việc tự động khởi tạo thông qua ClassDB.
    GDREGISTER_VIRTUAL_CLASS(MyCustomClass);

    // Đăng ký lớp ở chế độ công khai, nhưng ngăn mọi việc khởi tạo thông qua ClassDB.
    GDREGISTER_ABSTRACT_CLASS(MyCustomClass);

    // Đăng ký lớp trong ClassDB, nhưng đánh dấu lớp là riêng tư,
    // khiến lớp không hiển thị với script hoặc extension.
    // Điều này tương đương với việc hoàn toàn không đăng ký lớp một cách tường minh
    // - trong trường hợp này, lớp sẽ tự động được đăng ký là internal
    // khi được khởi tạo lần đầu.
    GDREGISTER_INTERNAL_CLASS(MyCustomClass);

    // Đăng ký lớp để lớp chỉ khả dụng tại runtime (nhưng không khả dụng trong editor).
    GDREGISTER_RUNTIME_CLASS(MyCustomClass);

Bạn cũng có thể sử dụng ``GDSOFTCLASS(MyCustomClass, SuperClass)`` thay cho ``GDCLASS(MyCustomClass, SuperClass)``. Các lớp được định nghĩa theo cách này hoàn toàn không được đăng ký trong ``ClassDB``. Cách này đôi khi được sử dụng cho các lớp con dành riêng cho từng platform.

Đăng ký binding
~~~~~~~~~~~~~~~

Các lớp kế thừa từ Object có thể override hàm static ``static void _bind_methods()``. Khi lớp được đăng ký, hàm static này được gọi để đăng ký tất cả method, property, constant của object, v.v. Hàm này chỉ được gọi một lần.

Bên trong ``_bind_methods``, có một vài thao tác có thể thực hiện. Đăng ký function là một trong số đó:

.. code-block:: cpp

    ClassDB::bind_method(D_METHOD("methodname", "arg1name", "arg2name", "arg3name"), &MyCustomType::method);

Có thể truyền các giá trị mặc định cho argument dưới dạng các parameter ở cuối:

.. code-block:: cpp

    ClassDB::bind_method(D_METHOD("methodname", "arg1name", "arg2name", "arg3name"), &MyCustomType::method, DEFVAL(-1), DEFVAL(-2)); // Giá trị mặc định cho arg2name (-1) và arg3name (-2).

Các giá trị mặc định phải được cung cấp theo đúng thứ tự khai báo, bỏ qua các argument bắt buộc rồi cung cấp giá trị mặc định cho các argument tùy chọn. Điều này phù hợp với cú pháp khai báo method trong C++.

``D_METHOD`` là một macro chuyển đổi "methodname" thành StringName để tăng hiệu quả. Tên argument được sử dụng cho introspection, nhưng khi compile ở chế độ release, macro sẽ bỏ qua chúng, vì vậy các string không được sử dụng và sẽ được tối ưu hóa loại bỏ.

Hãy xem ``_bind_methods`` của Control hoặc Object để có thêm ví dụ.

Nếu chỉ thêm module và chức năng không cần được ghi tài liệu chi tiết, bạn có thể bỏ qua macro ``D_METHOD()`` một cách an toàn và truyền một string chứa tên để viết ngắn gọn hơn.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/object/class_db.h <https://github.com/godotengine/godot/blob/master/core/object/class_db.h>`__

Constant
~~~~~~~~

Các lớp thường có enum, chẳng hạn như:

.. code-block:: cpp

    enum SomeMode {
       MODE_FIRST,
       MODE_SECOND
    };

Để hoạt động khi binding với method, enum phải được khai báo là có thể chuyển đổi thành int. Có một macro hỗ trợ việc này:

.. code-block:: cpp

    VARIANT_ENUM_CAST(MyClass::SomeMode); // giờ đây có thể binding các function nhận SomeMode.

Các constant cũng có thể được binding bên trong ``_bind_methods`` bằng cách sử dụng:

.. code-block:: cpp

    BIND_CONSTANT(MODE_FIRST);
    BIND_CONSTANT(MODE_SECOND);

Property (set/get)
~~~~~~~~~~~~~~~~~~

Object export các property; property hữu ích cho những mục đích sau:

-  Serialize và deserialize object. - Tạo danh sách các giá trị có thể chỉnh sửa cho lớp kế thừa từ Object.

Property thường được định nghĩa bởi lớp PropertyInfo() và được khởi tạo như sau:

.. code-block:: cpp

    PropertyInfo(type, name, hint, hint_string, usage_flags)

Ví dụ:

.. code-block:: cpp

    PropertyInfo(Variant::INT, "amount", PROPERTY_HINT_RANGE, "0,49,1", PROPERTY_USAGE_EDITOR)

Đây là một property kiểu integer có tên "amount". Hint là một range, với phạm vi từ 0 đến 49 và bước là 1 (số nguyên). Property này chỉ có thể được sử dụng trong editor (để chỉnh sửa giá trị bằng giao diện), nhưng sẽ không được serialize.

Một ví dụ khác:

.. code-block:: cpp

    PropertyInfo(Variant::STRING, "modes", PROPERTY_HINT_ENUM, "Enabled,Disabled,Turbo")

Đây là một property kiểu string, có thể nhận bất kỳ string nào nhưng editor chỉ cho phép các giá trị hint đã định nghĩa. Vì không chỉ định usage flag nào, các flag mặc định là PROPERTY_USAGE_STORAGE và PROPERTY_USAGE_EDITOR.

object.h cung cấp rất nhiều hint và usage flag; hãy xem qua chúng.

Property cũng có thể hoạt động giống property trong C# và được truy cập từ script bằng indexing, nhưng nhìn chung không nên sử dụng cách này vì function được ưu tiên để code dễ đọc hơn. Nhiều property cũng được binding với category, chẳng hạn như "animation/frame", khiến việc indexing không thể thực hiện trừ khi sử dụng operator [].

Từ ``_bind_methods()``, có thể tạo và binding property miễn là các function set/get tồn tại. Ví dụ:

.. code-block:: cpp

    ADD_PROPERTY(PropertyInfo(Variant::INT, "amount"), "set_amount", "get_amount")

Thao tác này tạo property bằng setter và getter.

.. _doc_binding_properties_using_set_get_property_list:

Binding properties using ``_set``/``_get``/``_get_property_list``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có một phương thức bổ sung để tạo property khi cần tính linh hoạt cao hơn (tức là thêm hoặc xóa property theo context).

Các function sau đây có thể được override trong lớp kế thừa từ Object; chúng KHÔNG phải virtual, KHÔNG được biến chúng thành virtual. Chúng được gọi cho mỗi lần override và các function trước đó không bị vô hiệu hóa (multilevel call).

.. code-block:: cpp

    protected:
         void _get_property_list(List<PropertyInfo> *r_props) const;      // trả về danh sách property
         bool _get(const StringName &p_property, Variant &r_value) const; // trả về true nếu tìm thấy property
         bool _set(const StringName &p_property, const Variant &p_value); // trả về true nếu tìm thấy property

Cách này cũng kém hiệu quả hơn một chút vì ``p_property`` phải được so sánh tuần tự với các tên mong muốn.


Signal
~~~~~~

Object có thể có một tập hợp signal được định nghĩa (tương tự Delegate trong các ngôn ngữ khác). Ví dụ này cho biết cách kết nối với chúng:

.. code-block:: cpp

    // Đây là function signature:
    //
    // Error connect(const StringName &p_signal, const Callable &p_callable, uint32_t p_flags = 0)
    //
    // Ví dụ:
    obj->connect("signal_name_here", callable_mp(this, &MyCustomType::method), CONNECT_DEFERRED);

``callable_mp`` là một macro để tạo function pointer callable tùy chỉnh tới các member function. Để biết các giá trị của ``p_flags``, hãy xem :ref:`ConnectFlags <enum_Object_ConnectFlags>`.

Việc thêm signal vào một lớp được thực hiện trong ``_bind_methods``, bằng macro ``ADD_SIGNAL``, ví dụ:

.. code-block:: cpp

    ADD_SIGNAL(MethodInfo("been_killed"))

Quyền sở hữu và ép kiểu Object
------------------------------

Object được cấp phát trên heap. Có hai mô hình quyền sở hữu khác nhau:

- Các object kế thừa từ ``RefCounted`` được quản lý bằng reference counting. - Tất cả object khác được quản lý bộ nhớ thủ công.

Hai mô hình quyền sở hữu này khác nhau về bản chất. Hãy tham khảo phần tương ứng để biết cách tạo, lưu trữ và giải phóng object.

Khi không biết object được truyền cho bạn (thông qua ``Object *``) có phải là ``RefCounted`` hay không và cần lưu trữ object đó, bạn nên lưu ``ObjectID`` của nó thay vì một pointer (như giải thích bên dưới, trong phần quản lý bộ nhớ thủ công).

Khi một object được truyền cho bạn thông qua :ref:`Variant<class_Variant>`, đặc biệt khi sử dụng deferred callback, có khả năng ``Object *`` chứa bên trong đã được giải phóng trước khi function của bạn chạy. Thay vì chuyển đổi trực tiếp sang ``Object *``, bạn nên sử dụng ``get_validated_object``:

.. code-block:: cpp

    void do_something(Variant p_variant) {
        Object *object = p_variant.get_validated_object();
        ERR_FAIL_NULL(object);
    }

Quản lý bộ nhớ thủ công
~~~~~~~~~~~~~~~~~~~~~~~

Các object được quản lý bộ nhớ thủ công được tạo bằng ``memnew`` và giải phóng bằng ``memdelete``:

.. code-block:: cpp

    Node *node = memnew(Node);
    // ...
    memdelete(node);
    node = nullptr;

Khi bạn không phải là chủ sở hữu duy nhất của một object, việc lưu pointer tới object đó rất nguy hiểm: Object có thể bị giải phóng bất kỳ lúc nào thông qua các reference khác, khiến pointer của bạn trở thành dangling pointer và cuối cùng gây crash.

Khi lưu trữ object mà bạn không phải là chủ sở hữu duy nhất, bạn nên lưu ``ObjectID`` của nó thay vì một pointer:

.. code-block:: cpp

    Node *node = memnew(Node);
    ObjectID node_id = node.get_instance_id();
    // ...
    Object *maybe_node = ObjectDB::get_instance(node_id);
    ERR_FAIL_NULL(maybe_node); // Node có thể đã được giải phóng giữa các lần gọi.

Quản lý bộ nhớ ``RefCounted``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`RefCounted <class_RefCounted>` subclasses are memory managed with
`ngữ nghĩa reference counting <https://en.wikipedia.org/wiki/Reference_counting>`__.

Chúng được tạo bằng ``memnew`` và nên được lưu trữ trong các instance ``Ref``. Khi instance ``Ref`` cuối cùng bị loại bỏ, object sẽ tự động tự hủy.

.. code-block:: cpp

    class MyRefCounted: public RefCounted {
        GDCLASS(MyRefCounted, RefCounted);
    };

    Ref<MyRefCounted> my_ref = memnew(MyRefCounted);
    // ...
    // Ref nắm quyền sở hữu chia sẻ đối với object, vì vậy object
    // sẽ không bị giải phóng. Chừng nào bạn còn một
    // Ref hợp lệ, khác null, bạn có thể an toàn giả định rằng object vẫn hợp lệ.
    my_ref->get_class_name();

Bạn không bao giờ được gọi ``memdelete`` đối với các lớp con của ``RefCounted``, vì có thể còn những owner khác của object.

Bạn cũng không bao giờ được lưu các lớp con của ``RefCounted`` bằng raw pointer, chẳng hạn như ``RefCounted *object = memnew(RefCounted)``. Điều này không an toàn vì các owner khác có thể hủy object, khiến bạn có một dangling pointer và cuối cùng gây crash.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/object/ref_counted.h <https://github.com/godotengine/godot/blob/master/core/object/ref_counted.h>`__

Ép kiểu động
~~~~~~~~~~~~

Godot cung cấp khả năng ép kiểu động giữa các lớp kế thừa từ Object, ví dụ:

.. code-block:: cpp

    void some_func(Object *p_object) {
         Button *button = Object::cast_to<Button>(p_object);
    }

Nếu ép kiểu thất bại, ``nullptr`` sẽ được trả về. Cách này hoạt động giống ``dynamic_cast``, nhưng không sử dụng `C++ RTTI <https://en.wikipedia.org/wiki/Run-time_type_information>`__.

Thông báo
---------

Tất cả các object trong Godot đều có phương thức :ref:`_notification <class_Object_private_method__notification>`, cho phép chúng phản hồi các callback ở cấp engine có thể liên quan đến chúng. Bạn có thể tìm thêm thông tin trên trang :ref:`doc_godot_notifications`.


Resource
--------

:ref:`Resource <class_resource>` inherits from RefCounted, so all resources
được đếm tham chiếu. Resource có thể tùy chọn chứa một đường dẫn tham chiếu đến một tệp trên đĩa. Bạn có thể thiết lập đường dẫn này bằng ``resource.set_path(path)``, mặc dù thông thường việc này được thực hiện bởi resource loader. Không có hai resource khác nhau nào có thể có cùng một đường dẫn; cố gắng làm như vậy sẽ dẫn đến lỗi.

Resource không có đường dẫn cũng hoàn toàn hợp lệ.

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `core/io/resource.h <https://github.com/godotengine/godot/blob/master/core/io/resource.h>`__

Tải resource
~~~~~~~~~~~~

Có thể tải resource bằng API ResourceLoader như sau:

.. code-block:: cpp

    Ref<Resource> res = ResourceLoader::load("res://someresource.res")

Nếu một tham chiếu đến resource đó đã được tải trước đó và đang nằm trong bộ nhớ, :ref:`ResourceLoader <class_ResourceLoader>` sẽ trả về tham chiếu đó. Điều này có nghĩa là tại một thời điểm chỉ có thể tải một resource từ một tệp được tham chiếu trên đĩa.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/io/resource_loader.h <https://github.com/godotengine/godot/blob/master/core/io/resource_loader.h>`__

Lưu resource
~~~~~~~~~~~~

Có thể lưu resource bằng API resource saver:

.. code-block:: cpp

    ResourceSaver::save("res://someresource.res", instance)

Instance sẽ được lưu, và các sub-resource có đường dẫn đến một tệp sẽ được lưu dưới dạng tham chiếu đến resource đó. Các sub-resource không có đường dẫn sẽ được đóng gói cùng resource đã lưu và được gán sub-ID, như ``res://someresource.res::1``. Điều này cũng giúp cache chúng khi được tải.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/io/resource_saver.h <https://github.com/godotengine/godot/blob/master/core/io/resource_saver.h>`__
