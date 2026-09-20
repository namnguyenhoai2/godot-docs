.. _doc_object_class:

Lớp Object
==========

.. seealso::

    Trang này mô tả cách triển khai các đối tượng C++ trong Godot. Bạn đang tìm tài liệu tham khảo về lớp Object? :ref:`Have a look here. <class_Object>`

Định nghĩa chung
----------------

:ref:`Object <class_object>` is the base class for almost everything. Most classes in Godot
kế thừa trực tiếp hoặc gián tiếp từ lớp này. Việc khai báo chúng chỉ cần sử dụng một macro duy nhất như sau:

.. code-block:: cpp

    class CustomObject : public Object {
        GDCLASS(CustomObject, Object); // This is required to inherit from Object.
    };

Các đối tượng có nhiều chức năng tích hợp, chẳng hạn như phản chiếu và các thuộc tính có thể chỉnh sửa:

.. code-block:: cpp

    CustomObject *obj = memnew(CustomObject);
    print_line("Object class: ", obj->get_class()); // print object class

    OtherClass *obj2 = Object::cast_to<OtherClass>(obj); // Converting between classes, similar to dynamic_cast

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `core/object/object.h <https://github.com/godotengine/godot/blob/master/core/object/object.h>`__

Đăng ký các lớp Object
----------------------

Hầu hết các lớp con của ``Object`` được đăng ký bằng cách gọi ``GDREGISTER_CLASS``.

.. code-block:: cpp

    GDREGISTER_CLASS(MyCustomClass)

Thao tác này sẽ đăng ký lớp đó dưới dạng một lớp công khai có tên trong ``ClassDB``, cho phép khởi tạo lớp bằng script, mã nguồn hoặc quá trình giải tuần tự hóa. Lưu ý rằng các lớp được đăng ký dưới dạng ``GDREGISTER_CLASS`` nên dự kiến sẽ được khởi tạo hoặc giải phóng tự động, chẳng hạn bởi trình chỉnh sửa hoặc hệ thống tài liệu.

Ngoài ``GDREGISTER_CLASS``, còn có một vài chế độ riêng tư khác:

.. code-block:: cpp

    // Registers the class publicly, but prevents automatic instantiation through ClassDB.
    GDREGISTER_VIRTUAL_CLASS(MyCustomClass);

    // Registers the class publicly, but prevents all instantiation through ClassDB.
    GDREGISTER_ABSTRACT_CLASS(MyCustomClass);

    // Registers the class in ClassDB, but marks it as private,
    // such that it is not visible to scripts or extensions.
    // This is the same as not registering the class explicitly at all
    // - in this case, the class is registered as internal automatically
    // when it is first constructed.
    GDREGISTER_INTERNAL_CLASS(MyCustomClass);

    // Registers the class such that it is only available at runtime (but not in the editor).
    GDREGISTER_RUNTIME_CLASS(MyCustomClass);

Bạn cũng có thể sử dụng ``GDSOFTCLASS(MyCustomClass, SuperClass)`` thay cho ``GDCLASS(MyCustomClass, SuperClass)``. Các lớp được định nghĩa theo cách này hoàn toàn không được đăng ký trong ``ClassDB``. Cách này đôi khi được sử dụng cho các lớp con dành riêng cho nền tảng.

Đăng ký các liên kết
~~~~~~~~~~~~~~~~~~~~

Các lớp dẫn xuất từ Object có thể ghi đè hàm tĩnh ``static void _bind_methods()``. Khi lớp được đăng ký, hàm tĩnh này được gọi để đăng ký tất cả phương thức, thuộc tính, hằng số của đối tượng, v.v. Hàm này chỉ được gọi một lần.

Bên trong ``_bind_methods``, bạn có thể thực hiện một vài thao tác. Đăng ký hàm là một trong số đó:

.. code-block:: cpp

    ClassDB::bind_method(D_METHOD("methodname", "arg1name", "arg2name", "arg3name"), &MyCustomType::method);

Có thể truyền giá trị mặc định cho các đối số dưới dạng tham số ở cuối:

.. code-block:: cpp

    ClassDB::bind_method(D_METHOD("methodname", "arg1name", "arg2name", "arg3name"), &MyCustomType::method, DEFVAL(-1), DEFVAL(-2)); // Default values for arg2name (-1) and arg3name (-2).

Các giá trị mặc định phải được cung cấp theo đúng thứ tự khai báo, bỏ qua các đối số bắt buộc rồi cung cấp giá trị mặc định cho những đối số tùy chọn. Điều này tương ứng với cú pháp khai báo phương thức trong C++.

``D_METHOD`` là một macro chuyển đổi "methodname" thành StringName để tăng hiệu quả. Tên đối số được sử dụng cho việc xem xét nội bộ, nhưng khi biên dịch bản phát hành, macro sẽ bỏ qua chúng, vì vậy các chuỗi này không được sử dụng và sẽ được tối ưu hóa loại bỏ.

Hãy xem ``_bind_methods`` của Control hoặc Object để biết thêm ví dụ.

Nếu chỉ thêm các mô-đun và chức năng không cần được lập tài liệu chi tiết, bạn có thể bỏ qua macro ``D_METHOD()`` một cách an toàn và truyền một chuỗi chứa tên để viết ngắn gọn hơn.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/object/class_db.h <https://github.com/godotengine/godot/blob/master/core/object/class_db.h>`__

Hằng số
~~~~~~~

Các lớp thường có những enum như sau:

.. code-block:: cpp

    enum SomeMode {
       MODE_FIRST,
       MODE_SECOND
    };

Để chúng hoạt động khi liên kết với các phương thức, enum phải được khai báo là có thể chuyển đổi thành int. Có một macro hỗ trợ việc này:

.. code-block:: cpp

    VARIANT_ENUM_CAST(MyClass::SomeMode); // now functions that take SomeMode can be bound.

Bạn cũng có thể liên kết các hằng số bên trong ``_bind_methods`` bằng cách sử dụng:

.. code-block:: cpp

    BIND_CONSTANT(MODE_FIRST);
    BIND_CONSTANT(MODE_SECOND);

Thuộc tính (set/get)
~~~~~~~~~~~~~~~~~~~~

Các đối tượng xuất thuộc tính; thuộc tính hữu ích cho những việc sau:

-  Tuần tự hóa và giải tuần tự hóa đối tượng. - Tạo danh sách các giá trị có thể chỉnh sửa cho lớp dẫn xuất từ Object.

Các thuộc tính thường được định nghĩa bằng lớp PropertyInfo() và được tạo như sau:

.. code-block:: cpp

    PropertyInfo(type, name, hint, hint_string, usage_flags)

Ví dụ:

.. code-block:: cpp

    PropertyInfo(Variant::INT, "amount", PROPERTY_HINT_RANGE, "0,49,1", PROPERTY_USAGE_EDITOR)

Đây là một thuộc tính số nguyên có tên "amount". Gợi ý là một khoảng giá trị, từ 0 đến 49 với bước nhảy 1 (số nguyên). Thuộc tính này chỉ có thể được sử dụng trong trình chỉnh sửa (để chỉnh sửa giá trị trực quan), nhưng sẽ không được tuần tự hóa.

Một ví dụ khác:

.. code-block:: cpp

    PropertyInfo(Variant::STRING, "modes", PROPERTY_HINT_ENUM, "Enabled,Disabled,Turbo")

Đây là một thuộc tính chuỗi, có thể nhận mọi chuỗi nhưng trình chỉnh sửa chỉ cho phép các chuỗi được xác định trong gợi ý. Vì không chỉ định cờ sử dụng nào, các cờ mặc định là PROPERTY_USAGE_STORAGE và PROPERTY_USAGE_EDITOR.

Có rất nhiều gợi ý và cờ sử dụng trong object.h, hãy xem qua chúng.

Các thuộc tính cũng có thể hoạt động giống như thuộc tính C# và được truy cập từ script bằng phép lập chỉ mục, nhưng cách sử dụng này nhìn chung không được khuyến khích, vì nên ưu tiên sử dụng các hàm để mã dễ đọc hơn. Nhiều thuộc tính cũng được liên kết với các danh mục, chẳng hạn như "animation/frame", điều này cũng khiến việc lập chỉ mục là bất khả thi trừ khi sử dụng toán tử [].

Từ ``_bind_methods()``, có thể tạo và liên kết các thuộc tính miễn là tồn tại các hàm set/get. Ví dụ:

.. code-block:: cpp

    ADD_PROPERTY(PropertyInfo(Variant::INT, "amount"), "set_amount", "get_amount")

Thao tác này tạo thuộc tính bằng setter và getter.

.. _doc_binding_properties_using_set_get_property_list:

Liên kết thuộc tính bằng ``_set``/``_get``/``_get_property_list``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có một phương pháp bổ sung để tạo thuộc tính khi cần sự linh hoạt cao hơn (ví dụ: thêm hoặc xóa thuộc tính theo ngữ cảnh).

Các hàm sau đây có thể được ghi đè trong một lớp dẫn xuất từ Object; chúng KHÔNG phải là hàm ảo, KHÔNG biến chúng thành hàm ảo; chúng được gọi cho mọi lần ghi đè và các hàm trước đó không bị vô hiệu hóa (lời gọi đa cấp).

.. code-block:: cpp

    protected:
         void _get_property_list(List<PropertyInfo> *r_props) const;      // return list of properties
         bool _get(const StringName &p_property, Variant &r_value) const; // return true if property was found
         bool _set(const StringName &p_property, const Variant &p_value); // return true if property was found

Cách này cũng kém hiệu quả hơn một chút vì ``p_property`` phải được so sánh tuần tự với các tên mong muốn.


Tín hiệu
~~~~~~~~

Các đối tượng có thể định nghĩa một tập hợp tín hiệu (tương tự Delegate trong các ngôn ngữ khác). Ví dụ này cho thấy cách kết nối với chúng:

.. code-block:: cpp

    // This is the function signature:
    //
    // Error connect(const StringName &p_signal, const Callable &p_callable, uint32_t p_flags = 0)
    //
    // For example:
    obj->connect("signal_name_here", callable_mp(this, &MyCustomType::method), CONNECT_DEFERRED);

``callable_mp`` là một macro để tạo con trỏ hàm callable tùy chỉnh đến các hàm thành viên. Để biết các giá trị của ``p_flags``, hãy xem :ref:`ConnectFlags <enum_Object_ConnectFlags>`.

Việc thêm tín hiệu vào một lớp được thực hiện trong ``_bind_methods``, bằng cách sử dụng macro ``ADD_SIGNAL``, ví dụ:

.. code-block:: cpp

    ADD_SIGNAL(MethodInfo("been_killed"))

Quyền sở hữu đối tượng và ép kiểu
---------------------------------

Các đối tượng được cấp phát trên heap. Có hai mô hình sở hữu khác nhau:

- Các đối tượng dẫn xuất từ ``RefCounted`` được đếm tham chiếu. - Tất cả các đối tượng khác được quản lý bộ nhớ thủ công.

Các mô hình sở hữu này khác nhau về bản chất. Hãy tham khảo phần tương ứng để tìm hiểu cách tạo, lưu trữ và giải phóng đối tượng.

Khi không biết đối tượng được truyền cho mình (thông qua ``Object *``) có phải là ``RefCounted`` hay không và cần lưu trữ đối tượng đó, bạn nên lưu trữ ``ObjectID`` của nó thay vì một con trỏ (như được giải thích bên dưới, trong phần quản lý bộ nhớ thủ công).

Khi một đối tượng được truyền cho bạn thông qua :ref:`Variant<class_Variant>`, đặc biệt khi sử dụng các callback trì hoãn, có khả năng ``Object *`` chứa bên trong đã được giải phóng trước khi hàm của bạn chạy. Thay vì chuyển đổi trực tiếp sang ``Object *``, bạn nên sử dụng ``get_validated_object``:

.. code-block:: cpp

    void do_something(Variant p_variant) {
        Object *object = p_variant.get_validated_object();
        ERR_FAIL_NULL(object);
    }

Quản lý bộ nhớ thủ công
~~~~~~~~~~~~~~~~~~~~~~~

Các đối tượng được quản lý bộ nhớ thủ công được tạo bằng ``memnew`` và giải phóng bằng ``memdelete``:

.. code-block:: cpp

    Node *node = memnew(Node);
    // ...
    memdelete(node);
    node = nullptr;

Khi bạn không phải là chủ sở hữu duy nhất của một đối tượng, việc lưu trữ con trỏ đến đối tượng đó rất nguy hiểm: Đối tượng có thể bị giải phóng bất kỳ lúc nào thông qua các tham chiếu khác đến nó, khiến con trỏ của bạn trở thành con trỏ treo và cuối cùng gây ra lỗi.

Khi lưu trữ các đối tượng mà bạn không phải là chủ sở hữu duy nhất, bạn nên lưu trữ ``ObjectID`` của đối tượng thay vì một con trỏ:

.. code-block:: cpp

    Node *node = memnew(Node);
    ObjectID node_id = node.get_instance_id();
    // ...
    Object *maybe_node = ObjectDB::get_instance(node_id);
    ERR_FAIL_NULL(maybe_node); // The node may have been freed between calls.

Quản lý bộ nhớ ``RefCounted``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`RefCounted <class_RefCounted>` subclasses are memory managed with
`ngữ nghĩa đếm tham chiếu <https://en.wikipedia.org/wiki/Reference_counting>`__.

Chúng được tạo bằng ``memnew`` và nên được lưu trữ trong các thực thể ``Ref``. Khi thực thể ``Ref`` cuối cùng bị loại bỏ, đối tượng sẽ tự động tự hủy.

.. code-block:: cpp

    class MyRefCounted: public RefCounted {
        GDCLASS(MyRefCounted, RefCounted);
    };

    Ref<MyRefCounted> my_ref = memnew(MyRefCounted);
    // ...
    // Ref holds shared ownership over the object, so the object
    // will not be freed. As long as you have a valid, non-null
    // Ref, it can be safely assumed the object is still valid.
    my_ref->get_class_name();

Bạn không bao giờ được gọi ``memdelete`` cho các lớp con của ``RefCounted``, vì có thể còn những chủ sở hữu khác của đối tượng.

Bạn cũng không bao giờ được lưu trữ các lớp con của ``RefCounted`` bằng con trỏ thô, chẳng hạn như ``RefCounted *object = memnew(RefCounted)``. Điều này không an toàn vì các chủ sở hữu khác có thể hủy đối tượng, khiến bạn có một con trỏ treo và cuối cùng gây ra lỗi.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/object/ref_counted.h <https://github.com/godotengine/godot/blob/master/core/object/ref_counted.h>`__

Ép kiểu động
~~~~~~~~~~~~

Godot cung cấp khả năng ép kiểu động giữa các lớp dẫn xuất từ Object, ví dụ:

.. code-block:: cpp

    void some_func(Object *p_object) {
         Button *button = Object::cast_to<Button>(p_object);
    }

Nếu ép kiểu thất bại, ``nullptr`` sẽ được trả về. Cách này hoạt động giống như ``dynamic_cast``, nhưng không sử dụng `C++ RTTI <https://en.wikipedia.org/wiki/Run-time_type_information>`__.

Thông báo
---------

Tất cả đối tượng trong Godot đều có một phương thức :ref:`_notification <class_Object_private_method__notification>` cho phép chúng phản hồi các callback cấp engine có thể liên quan đến chúng. Bạn có thể tìm thêm thông tin trên trang :ref:`doc_godot_notifications`.


Resource
--------

:ref:`Resource <class_resource>` inherits from RefCounted, so all resources
được đếm tham chiếu. Resource có thể tùy chọn chứa một đường dẫn trỏ đến một tệp trên đĩa. Bạn có thể thiết lập đường dẫn này bằng ``resource.set_path(path)``, mặc dù thông thường việc này được thực hiện bởi trình tải resource. Không có hai resource khác nhau nào có thể có cùng một đường dẫn; cố gắng làm vậy sẽ gây ra lỗi.

Resource không có đường dẫn cũng hoàn toàn hợp lệ.

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `core/io/resource.h <https://github.com/godotengine/godot/blob/master/core/io/resource.h>`__

Tải resource
~~~~~~~~~~~~

Có thể tải resource bằng API ResourceLoader như sau:

.. code-block:: cpp

    Ref<Resource> res = ResourceLoader::load("res://someresource.res")

Nếu một tham chiếu đến resource đó đã được tải trước đó và đang nằm trong bộ nhớ, :ref:`ResourceLoader <class_ResourceLoader>` sẽ trả về tham chiếu đó. Điều này có nghĩa là tại cùng một thời điểm, chỉ có thể có một resource được tải từ một tệp được tham chiếu trên đĩa.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/io/resource_loader.h <https://github.com/godotengine/godot/blob/master/core/io/resource_loader.h>`__

Lưu resource
~~~~~~~~~~~~

Có thể lưu resource bằng API resource saver:

.. code-block:: cpp

    ResourceSaver::save("res://someresource.res", instance)

Instance sẽ được lưu, còn các sub-resource có đường dẫn đến tệp sẽ được lưu dưới dạng tham chiếu đến resource đó. Các sub-resource không có đường dẫn sẽ được đóng gói cùng resource đã lưu và được gán các sub-ID, chẳng hạn như ``res://someresource.res::1``. Điều này cũng giúp lưu chúng vào bộ nhớ đệm khi được tải.

Tài liệu tham khảo:
^^^^^^^^^^^^^^^^^^^

-  `core/io/resource_saver.h <https://github.com/godotengine/godot/blob/master/core/io/resource_saver.h>`__
