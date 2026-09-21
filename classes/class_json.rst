:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/JSON.xml.

.. _class_JSON:

JSON
====

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp trợ giúp để tạo và phân tích dữ liệu JSON.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp **JSON** cho phép chuyển đổi mọi kiểu dữ liệu thành và từ chuỗi JSON. Điều này hữu ích khi serialize dữ liệu, chẳng hạn để lưu vào tệp hoặc gửi qua mạng.

\ :ref:`stringify()<class_JSON_method_stringify>` được dùng để chuyển đổi mọi kiểu dữ liệu thành một chuỗi JSON.

\ :ref:`parse()<class_JSON_method_parse>` được dùng để chuyển đổi mọi dữ liệu JSON hiện có thành một :ref:`Variant<class_Variant>` có thể được sử dụng trong Godot. Nếu phân tích thành công, hãy dùng :ref:`data<class_JSON_property_data>` để lấy :ref:`Variant<class_Variant>`, và dùng :ref:`@GlobalScope.typeof()<class_@GlobalScope_method_typeof>` để kiểm tra xem kiểu của Variant có đúng như mong đợi hay không. Các đối tượng JSON được chuyển đổi thành một :ref:`Dictionary<class_Dictionary>`, nhưng dữ liệu JSON có thể được dùng để lưu trữ :ref:`Array<class_Array>`\ s, số, :ref:`String<class_String>`\ s và thậm chí chỉ một giá trị boolean.

::

    var data_to_send = ["a", "b", "c"]
    var json_string = JSON.stringify(data_to_send)
    # Lưu dữ liệu
    # ...
    # Lấy dữ liệu
    var json = JSON.new()
    var error = json.parse(json_string)
    if error == OK:
        var data_received = json.data
        if typeof(data_received) == TYPE_ARRAY:
            print(data_received) # In mảng.
        else:
            print("Unexpected data")
    else:
        print("JSON Parse Error: ", json.get_error_message(), " in ", json_string, " at line ", json.get_error_line())

Ngoài ra, bạn có thể phân tích chuỗi bằng phương thức static :ref:`parse_string()<class_JSON_method_parse_string>`, nhưng phương thức này không xử lý lỗi.

::

    var data = JSON.parse_string(json_string) # Trả về null nếu phân tích thất bại.

\ **Lưu ý:** Cả hai phương thức parse đều không hoàn toàn tuân thủ đặc tả JSON:

- Dấu phẩy ở cuối trong mảng hoặc đối tượng sẽ bị bỏ qua, thay vì gây ra lỗi parser.

- Các ký tự dòng mới và tab được chấp nhận trong các literal chuỗi và được xử lý như các escape sequence tương ứng ``\n`` và ``\t``.

- Các số được phân tích bằng :ref:`String.to_float()<class_String_method_to_float>`, vốn thường linh hoạt hơn đặc tả JSON.

- Một số lỗi, chẳng hạn như các chuỗi Unicode không hợp lệ, không gây ra lỗi parser. Thay vào đó, chuỗi sẽ được làm sạch và một lỗi được ghi vào console.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+---------------------------------------+----------+
   | :ref:`Variant<class_Variant>` | :ref:`data<class_JSON_property_data>` | ``null`` |
   +-------------------------------+---------------------------------------+----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`         | :ref:`from_native<class_JSON_method_from_native>`\ (\ variant\: :ref:`Variant<class_Variant>`, full_objects\: :ref:`bool<class_bool>` = false\ ) |static|                                                                                   |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                 | :ref:`get_error_line<class_JSON_method_get_error_line>`\ (\ ) |const|                                                                                                                                                                       |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`get_error_message<class_JSON_method_get_error_message>`\ (\ ) |const|                                                                                                                                                                 |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`get_parsed_text<class_JSON_method_get_parsed_text>`\ (\ ) |const|                                                                                                                                                                     |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`parse<class_JSON_method_parse>`\ (\ json_text\: :ref:`String<class_String>`, keep_text\: :ref:`bool<class_bool>` = false\ )                                                                                                           |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`         | :ref:`parse_string<class_JSON_method_parse_string>`\ (\ json_string\: :ref:`String<class_String>`\ ) |static|                                                                                                                               |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`stringify<class_JSON_method_stringify>`\ (\ data\: :ref:`Variant<class_Variant>`, indent\: :ref:`String<class_String>` = "", sort_keys\: :ref:`bool<class_bool>` = true, full_precision\: :ref:`bool<class_bool>` = false\ ) |static| |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`         | :ref:`to_native<class_JSON_method_to_native>`\ (\ json\: :ref:`Variant<class_Variant>`, allow_objects\: :ref:`bool<class_bool>` = false\ ) |static|                                                                                         |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_JSON_property_data:

.. rst-class:: classref-property

:ref:`Variant<class_Variant>` **data** = ``null`` :ref:`🔗<class_JSON_property_data>`

.. rst-class:: classref-property-setget

- |void| **set_data**\ (\ value\: :ref:`Variant<class_Variant>`\ ) - :ref:`Variant<class_Variant>` **get_data**\ (\ )

Chứa dữ liệu JSON đã phân tích dưới dạng :ref:`Variant<class_Variant>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_JSON_method_from_native:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **from_native**\ (\ variant\: :ref:`Variant<class_Variant>`, full_objects\: :ref:`bool<class_bool>` = false\ ) |static| :ref:`🔗<class_JSON_method_from_native>`

Chuyển đổi một kiểu engine native thành một giá trị tuân thủ JSON.

Theo mặc định, các đối tượng sẽ bị bỏ qua vì lý do bảo mật, trừ khi ``full_objects`` là ``true``.

Bạn có thể chuyển đổi một giá trị native thành chuỗi JSON như sau:

::

    func encode_data(value, full_objects = false):
        return JSON.stringify(JSON.from_native(value, full_objects))

.. rst-class:: classref-item-separator

----

.. _class_JSON_method_get_error_line:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_error_line**\ (\ ) |const| :ref:`🔗<class_JSON_method_get_error_line>`

Trả về ``0`` nếu lần gọi :ref:`parse()<class_JSON_method_parse>` gần nhất thành công, hoặc số dòng nơi quá trình phân tích thất bại.

.. rst-class:: classref-item-separator

----

.. _class_JSON_method_get_error_message:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_error_message**\ (\ ) |const| :ref:`🔗<class_JSON_method_get_error_message>`

Trả về một chuỗi rỗng nếu lần gọi :ref:`parse()<class_JSON_method_parse>` gần nhất thành công, hoặc thông báo lỗi nếu thất bại.

.. rst-class:: classref-item-separator

----

.. _class_JSON_method_get_parsed_text:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_parsed_text**\ (\ ) |const| :ref:`🔗<class_JSON_method_get_parsed_text>`

Trả về văn bản được phân tích bởi :ref:`parse()<class_JSON_method_parse>` (yêu cầu truyền ``keep_text`` cho :ref:`parse()<class_JSON_method_parse>`).

.. rst-class:: classref-item-separator

----

.. _class_JSON_method_parse:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **parse**\ (\ json_text\: :ref:`String<class_String>`, keep_text\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_JSON_method_parse>`

Cố gắng phân tích ``json_text`` được cung cấp.

Trả về một :ref:`Error<enum_@GlobalScope_Error>`. Nếu phân tích thành công, phương thức trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` và có thể lấy kết quả bằng :ref:`data<class_JSON_property_data>`. Nếu thất bại, hãy dùng :ref:`get_error_line()<class_JSON_method_get_error_line>` và :ref:`get_error_message()<class_JSON_method_get_error_message>` để xác định nguyên nhân thất bại.

Biến thể không static của :ref:`parse_string()<class_JSON_method_parse_string>`, nếu bạn muốn tự xử lý lỗi.

Đối số tùy chọn ``keep_text`` yêu cầu parser giữ một bản sao của văn bản gốc. Sau đó có thể lấy văn bản này bằng hàm :ref:`get_parsed_text()<class_JSON_method_get_parsed_text>`, và văn bản được dùng khi lưu resource (thay vì tạo văn bản mới từ :ref:`data<class_JSON_property_data>`).

.. rst-class:: classref-item-separator

----

.. _class_JSON_method_parse_string:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **parse_string**\ (\ json_string\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_JSON_method_parse_string>`

Cố gắng phân tích ``json_string`` được cung cấp và trả về dữ liệu đã phân tích. Trả về ``null`` nếu phân tích thất bại.

.. rst-class:: classref-item-separator

----

.. _class_JSON_method_stringify:

.. rst-class:: classref-method

:ref:`String<class_String>` **stringify**\ (\ data\: :ref:`Variant<class_Variant>`, indent\: :ref:`String<class_String>` = "", sort_keys\: :ref:`bool<class_bool>` = true, full_precision\: :ref:`bool<class_bool>` = false\ ) |static| :ref:`🔗<class_JSON_method_stringify>`

Chuyển đổi một biến :ref:`Variant<class_Variant>` thành văn bản JSON và trả về kết quả. Hữu ích khi serialize dữ liệu để lưu trữ hoặc gửi qua mạng.

\ **Lưu ý:** Đặc tả JSON không định nghĩa kiểu integer hoặc float mà chỉ định nghĩa kiểu *number*. Do đó, khi chuyển đổi một Variant thành văn bản JSON, tất cả giá trị số sẽ được chuyển thành các kiểu :ref:`float<class_float>`.

\ **Lưu ý:** Nếu ``full_precision`` là ``true``, khi stringify các số thực, các chữ số không đáng tin cậy sẽ được stringify cùng với các chữ số đáng tin cậy để đảm bảo giải mã chính xác tuyệt đối.

Tham số ``indent`` kiểm soát việc một nội dung có được thụt lề hay không và thụt lề như thế nào; nội dung của tham số sẽ được dùng tại vị trí cần thụt lề trong đầu ra. Ngay cả các khoảng trắng như ``" "`` cũng hoạt động. ``\t`` và ``\n`` cũng có thể được dùng để thụt lề bằng tab hoặc tạo một dòng mới cho mỗi mức thụt lề tương ứng.

\ **Cảnh báo:** Các số không hữu hạn không được JSON hỗ trợ. Mọi trường hợp xuất hiện :ref:`@GDScript.INF<class_@GDScript_constant_INF>` sẽ được thay thế bằng ``1e99999``, và :ref:`@GDScript.INF<class_@GDScript_constant_INF>` âm sẽ được thay thế bằng ``-1e99999``, nhưng hầu hết parser JSON sẽ diễn giải chúng chính xác là vô cực. :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` sẽ được thay thế bằng ``null``, và sẽ không được các parser JSON diễn giải là NaN. Nếu bạn dự kiến có các số không hữu hạn, hãy cân nhắc truyền dữ liệu qua :ref:`from_native()<class_JSON_method_from_native>` trước.

\ **Ví dụ đầu ra:**\

::

    ## JSON.stringify(my_dictionary)
    {"name":"my_dictionary","version":"1.0.0","entities":[{"name":"entity_0","value":"value_0"},{"name":"entity_1","value":"value_1"}]}

    ## JSON.stringify(my_dictionary, "\t")
    {
        "name": "my_dictionary",
        "version": "1.0.0",
        "entities": [
            {
                "name": "entity_0",
                "value": "value_0"
            },
            {
                "name": "entity_1",
                "value": "value_1"
            }
        ]
    }

    ## JSON.stringify(my_dictionary, "...")
    {
    ..."name": "my_dictionary",
    ..."version": "1.0.0",
    ..."entities": [
    ......{
    ........."name": "entity_0",
    ........."value": "value_0"
    ......},
    ......{
    ........."name": "entity_1",
    ........."value": "value_1"
    ......}
    ...]
    }

.. rst-class:: classref-item-separator

----

.. _class_JSON_method_to_native:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **to_native**\ (\ json\: :ref:`Variant<class_Variant>`, allow_objects\: :ref:`bool<class_bool>` = false\ ) |static| :ref:`🔗<class_JSON_method_to_native>`

Chuyển đổi một giá trị tuân thủ JSON được tạo bằng :ref:`from_native()<class_JSON_method_from_native>` trở lại thành các kiểu engine native.

Theo mặc định, các đối tượng sẽ bị bỏ qua vì lý do bảo mật, trừ khi ``allow_objects`` là ``true``.

Bạn có thể chuyển đổi một chuỗi JSON trở lại thành giá trị native như sau:

::

    func decode_data(string, allow_objects = false):
        return JSON.to_native(JSON.parse_string(string), allow_objects)

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
