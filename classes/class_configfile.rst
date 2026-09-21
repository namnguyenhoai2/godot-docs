:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ConfigFile.xml.

.. _class_ConfigFile:

ConfigFile
==========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp hỗ trợ để xử lý các tệp kiểu INI.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp hỗ trợ này có thể được dùng để lưu trữ các giá trị :ref:`Variant<class_Variant>` trên hệ thống tệp bằng định dạng kiểu INI. Các giá trị được lưu trữ được xác định bởi một section và một key:

.. code:: text

    [section]
    some_key=42
    string_example="Hello World3D!"
    a_vector=Vector3(1, 0, 2)

Dữ liệu được lưu trữ có thể được lưu vào hoặc phân tích từ một tệp, mặc dù các đối tượng ConfigFile cũng có thể được sử dụng trực tiếp mà không cần truy cập hệ thống tệp.

Ví dụ sau đây minh họa cách tạo một **ConfigFile** đơn giản và lưu nó vào đĩa:


.. tabs::

 .. code-tab:: gdscript

    # Tạo đối tượng ConfigFile mới.
    var config = ConfigFile.new()

    # Lưu trữ một số giá trị.
    config.set_value("Player1", "player_name", "Steve")
    config.set_value("Player1", "best_score", 10)
    config.set_value("Player2", "player_name", "V3geta")
    config.set_value("Player2", "best_score", 9001)

    # Lưu vào một tệp (ghi đè nếu tệp đã tồn tại).
    config.save("user://scores.cfg")

 .. code-tab:: csharp

    // Tạo đối tượng ConfigFile mới.
    var config = new ConfigFile();

    // Lưu trữ một số giá trị.
    config.SetValue("Player1", "player_name", "Steve");
    config.SetValue("Player1", "best_score", 10);
    config.SetValue("Player2", "player_name", "V3geta");
    config.SetValue("Player2", "best_score", 9001);

    // Lưu vào một tệp (ghi đè nếu tệp đã tồn tại).
    config.Save("user://scores.cfg");



Ví dụ này minh họa cách tải tệp ở trên:


.. tabs::

 .. code-tab:: gdscript

    var score_data = {}
    var config = ConfigFile.new()

    # Tải dữ liệu từ một tệp.
    var err = config.load("user://scores.cfg")

    # Nếu tệp không được tải, hãy bỏ qua.
    if err != OK:
        return

    # Lặp qua tất cả các section.
    for player in config.get_sections():
        # Lấy dữ liệu cho từng section.
        var player_name = config.get_value(player, "player_name")
        var player_score = config.get_value(player, "best_score")
        score_data[player_name] = player_score

 .. code-tab:: csharp

    var score_data = new Godot.Collections.Dictionary();
    var config = new ConfigFile();

    // Tải dữ liệu từ một tệp.
    Error err = config.Load("user://scores.cfg");

    // Nếu tệp không được tải, hãy bỏ qua.
    if (err != Error.Ok)
    {
        return;
    }

    // Lặp qua tất cả các section.
    foreach (String player in config.GetSections())
    {
        // Lấy dữ liệu cho từng section.
        var player_name = (String)config.GetValue(player, "player_name");
        var player_score = (int)config.GetValue(player, "best_score");
        score_data[player_name] = player_score;
    }



Mọi thao tác làm thay đổi ConfigFile, chẳng hạn như :ref:`set_value()<class_ConfigFile_method_set_value>`, :ref:`clear()<class_ConfigFile_method_clear>` hoặc :ref:`erase_section()<class_ConfigFile_method_erase_section>`, chỉ thay đổi dữ liệu đã được tải trong bộ nhớ. Nếu muốn ghi thay đổi vào tệp, bạn phải lưu các thay đổi bằng :ref:`save()<class_ConfigFile_method_save>`, :ref:`save_encrypted()<class_ConfigFile_method_save_encrypted>` hoặc :ref:`save_encrypted_pass()<class_ConfigFile_method_save_encrypted_pass>`.

Hãy lưu ý rằng tên section và property không được chứa khoảng trắng. Mọi nội dung sau khoảng trắng sẽ bị bỏ qua khi lưu và khi tải.

ConfigFile cũng có thể chứa các dòng chú thích được viết thủ công, bắt đầu bằng dấu chấm phẩy (``;``). Các dòng này sẽ bị bỏ qua khi phân tích tệp. Lưu ý rằng chú thích sẽ bị mất khi lưu ConfigFile. Điều này vẫn có thể hữu ích cho các tệp cấu hình dedicated server, vốn thường không bao giờ bị ghi đè nếu không có thao tác rõ ràng từ người dùng.

\ **Lưu ý:** Phần mở rộng tệp được cung cấp cho ConfigFile không ảnh hưởng đến định dạng hoặc hành vi của nó. Theo quy ước, phần mở rộng ``.cfg`` được sử dụng ở đây, nhưng bất kỳ phần mở rộng nào khác, chẳng hạn như ``.ini``, cũng hợp lệ. Vì cả ``.cfg`` lẫn ``.ini`` đều chưa được chuẩn hóa, định dạng ConfigFile của Godot có thể khác với các tệp được ghi bởi những chương trình khác.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`clear<class_ConfigFile_method_clear>`\ (\ )                                                                                                                                           |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`encode_to_text<class_ConfigFile_method_encode_to_text>`\ (\ ) |const|                                                                                                                 |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`erase_section<class_ConfigFile_method_erase_section>`\ (\ section\: :ref:`String<class_String>`\ )                                                                                    |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`erase_section_key<class_ConfigFile_method_erase_section_key>`\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`\ )                                         |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_section_keys<class_ConfigFile_method_get_section_keys>`\ (\ section\: :ref:`String<class_String>`\ ) |const|                                                                      |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_sections<class_ConfigFile_method_get_sections>`\ (\ ) |const|                                                                                                                     |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                     | :ref:`get_value<class_ConfigFile_method_get_value>`\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`, default\: :ref:`Variant<class_Variant>` = null\ ) |const| |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`has_section<class_ConfigFile_method_has_section>`\ (\ section\: :ref:`String<class_String>`\ ) |const|                                                                                |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`has_section_key<class_ConfigFile_method_has_section_key>`\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`\ ) |const|                                     |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`load<class_ConfigFile_method_load>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                         |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`load_encrypted<class_ConfigFile_method_load_encrypted>`\ (\ path\: :ref:`String<class_String>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`load_encrypted_pass<class_ConfigFile_method_load_encrypted_pass>`\ (\ path\: :ref:`String<class_String>`, password\: :ref:`String<class_String>`\ )                                   |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`parse<class_ConfigFile_method_parse>`\ (\ data\: :ref:`String<class_String>`\ )                                                                                                       |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`save<class_ConfigFile_method_save>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                         |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`save_encrypted<class_ConfigFile_method_save_encrypted>`\ (\ path\: :ref:`String<class_String>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`save_encrypted_pass<class_ConfigFile_method_save_encrypted_pass>`\ (\ path\: :ref:`String<class_String>`, password\: :ref:`String<class_String>`\ )                                   |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_value<class_ConfigFile_method_set_value>`\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`, value\: :ref:`Variant<class_Variant>`\ )                  |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ConfigFile_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_ConfigFile_method_clear>`

Xóa toàn bộ nội dung của config.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_encode_to_text:

.. rst-class:: classref-method

:ref:`String<class_String>` **encode_to_text**\ (\ ) |const| :ref:`🔗<class_ConfigFile_method_encode_to_text>`

Lấy phiên bản văn bản của tệp config này (chính là văn bản sẽ được ghi vào tệp).

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_erase_section:

.. rst-class:: classref-method

|void| **erase_section**\ (\ section\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ConfigFile_method_erase_section>`

Xóa section được chỉ định cùng với tất cả các cặp key-value bên trong. Phát sinh lỗi nếu section không tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_erase_section_key:

.. rst-class:: classref-method

|void| **erase_section_key**\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ConfigFile_method_erase_section_key>`

Xóa key được chỉ định trong một section. Phát sinh lỗi nếu section hoặc key không tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_get_section_keys:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_section_keys**\ (\ section\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_ConfigFile_method_get_section_keys>`

Trả về một mảng chứa tất cả các mã định danh key đã được định nghĩa trong section được chỉ định. Phát sinh lỗi và trả về một mảng rỗng nếu section không tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_get_sections:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_sections**\ (\ ) |const| :ref:`🔗<class_ConfigFile_method_get_sections>`

Trả về một mảng chứa tất cả các mã định danh section đã được định nghĩa.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_get_value:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_value**\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`, default\: :ref:`Variant<class_Variant>` = null\ ) |const| :ref:`🔗<class_ConfigFile_method_get_value>`

Trả về giá trị hiện tại của section và key được chỉ định. Nếu section hoặc key không tồn tại, phương thức sẽ trả về giá trị ``default`` dự phòng. Nếu ``default`` không được chỉ định hoặc được đặt thành ``null``, một lỗi cũng sẽ được phát sinh.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_has_section:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_section**\ (\ section\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_ConfigFile_method_has_section>`

Trả về ``true`` nếu section được chỉ định tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_has_section_key:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_section_key**\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_ConfigFile_method_has_section_key>`

Trả về ``true`` nếu cặp section-key được chỉ định tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_load:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ConfigFile_method_load>`

Tải tệp config được chỉ định dưới dạng tham số. Nội dung tệp được phân tích và tải vào đối tượng **ConfigFile** mà phương thức được gọi trên đó.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các giá trị :ref:`Error<enum_@GlobalScope_Error>` khác nếu thao tác thất bại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_load_encrypted:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load_encrypted**\ (\ path\: :ref:`String<class_String>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_ConfigFile_method_load_encrypted>`

Tải tệp config đã mã hóa được chỉ định dưới dạng tham số, sử dụng ``key`` được cung cấp để giải mã tệp. Nội dung tệp được phân tích và tải vào đối tượng **ConfigFile** mà phương thức được gọi trên đó.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các giá trị :ref:`Error<enum_@GlobalScope_Error>` khác nếu thao tác thất bại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_load_encrypted_pass:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load_encrypted_pass**\ (\ path\: :ref:`String<class_String>`, password\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ConfigFile_method_load_encrypted_pass>`

Tải tệp config đã mã hóa được chỉ định dưới dạng tham số, sử dụng ``password`` được cung cấp để giải mã tệp. Nội dung tệp được phân tích và tải vào đối tượng **ConfigFile** mà phương thức được gọi trên đó.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các giá trị :ref:`Error<enum_@GlobalScope_Error>` khác nếu thao tác thất bại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_parse:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **parse**\ (\ data\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ConfigFile_method_parse>`

Phân tích chuỗi được truyền vào dưới dạng nội dung của một tệp config. Chuỗi được phân tích và tải vào đối tượng ConfigFile mà phương thức được gọi trên đó.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các giá trị :ref:`Error<enum_@GlobalScope_Error>` khác nếu thao tác thất bại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_save:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **save**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ConfigFile_method_save>`

Lưu nội dung của đối tượng **ConfigFile** vào tệp được chỉ định dưới dạng tham số. Tệp đầu ra sử dụng cấu trúc kiểu INI.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các giá trị :ref:`Error<enum_@GlobalScope_Error>` khác nếu thao tác thất bại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_save_encrypted:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **save_encrypted**\ (\ path\: :ref:`String<class_String>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_ConfigFile_method_save_encrypted>`

Lưu nội dung của đối tượng **ConfigFile** vào tệp được mã hóa AES-256 được chỉ định dưới dạng tham số, sử dụng ``key`` được cung cấp để mã hóa tệp. Tệp đầu ra sử dụng cấu trúc kiểu INI.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các giá trị :ref:`Error<enum_@GlobalScope_Error>` khác nếu thao tác thất bại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_save_encrypted_pass:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **save_encrypted_pass**\ (\ path\: :ref:`String<class_String>`, password\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ConfigFile_method_save_encrypted_pass>`

Lưu nội dung của đối tượng **ConfigFile** vào tệp được mã hóa AES-256 được chỉ định dưới dạng tham số, sử dụng ``password`` được cung cấp để mã hóa tệp. Tệp đầu ra sử dụng cấu trúc kiểu INI.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các giá trị :ref:`Error<enum_@GlobalScope_Error>` khác nếu thao tác thất bại.

.. rst-class:: classref-item-separator

----

.. _class_ConfigFile_method_set_value:

.. rst-class:: classref-method

|void| **set_value**\ (\ section\: :ref:`String<class_String>`, key\: :ref:`String<class_String>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_ConfigFile_method_set_value>`

Gán một giá trị cho key được chỉ định của section được chỉ định. Nếu section hoặc key không tồn tại, chúng sẽ được tạo. Truyền một giá trị ``null`` sẽ xóa key được chỉ định nếu key đó tồn tại, đồng thời xóa section nếu section trở nên rỗng sau khi key bị xóa.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
