:article_outdated: Đúng

.. _doc_import_plugins:

Import plugin
=============

.. note:: Hướng dẫn này giả định rằng bạn đã biết cách tạo generic plugin. Nếu chưa chắc, hãy tham khảo trang :ref:`doc_making_plugins`. Hướng dẫn này cũng giả định rằng bạn đã quen với hệ thống import của Godot.

Giới thiệu
----------

Import plugin là một loại editor tool đặc biệt, cho phép Godot import các resource tùy chỉnh và xử lý chúng như các resource hạng nhất. Bản thân editor đi kèm rất nhiều import plugin để xử lý các resource phổ biến như ảnh PNG, model Collada và glTF, âm thanh Ogg Vorbis cùng nhiều loại khác.

Hướng dẫn này chỉ cách tạo một import plugin để tải một tệp văn bản tùy chỉnh dưới dạng material resource. Tệp văn bản này sẽ chứa ba giá trị số được phân tách bằng dấu phẩy, biểu thị ba kênh của một màu; màu kết quả sẽ được dùng làm albedo (màu chính) của material đã import. Trong ví dụ này, tệp chứa màu xanh dương thuần (đỏ bằng không, xanh lá bằng không và xanh dương tối đa):

.. code-block:: none

    0,0,255

Cấu hình
--------

Trước tiên, chúng ta cần một generic plugin để xử lý việc khởi tạo và hủy import plugin. Trước hết, hãy thêm tệp ``plugin.cfg``:

.. code-block:: ini

    [plugin]

    name="Silly Material Importer"
    description="Imports a 3D Material from an external text file."
    author="Yours Truly"
    version="1.0"
    script="material_import.gd"

Tiếp theo, chúng ta cần tệp ``material_import.gd`` để thêm và xóa import plugin khi cần:

::

    # material_import.gd
    @tool
    extends EditorPlugin


    var import_plugin


    func _enter_tree():
        import_plugin = preload("import_plugin.gd").new()
        add_import_plugin(import_plugin)


    func _exit_tree():
        remove_import_plugin(import_plugin)
        import_plugin = null

Khi plugin này được kích hoạt, nó sẽ tạo một instance mới của import plugin (chúng ta sẽ sớm tạo plugin này) và thêm nó vào editor bằng cách sử dụng
phương thức :ref:`add_import_plugin() <class_EditorPlugin_method_add_import_plugin>`. Chúng ta lưu một tham chiếu đến nó trong thành viên lớp ``import_plugin`` để có thể dùng tham chiếu này sau đó khi xóa nó. Phương thức
:ref:`remove_import_plugin() <class_EditorPlugin_method_remove_import_plugin>` được gọi khi plugin bị tắt để dọn dẹp bộ nhớ và cho editor biết rằng import plugin không còn khả dụng.

Lưu ý rằng import plugin là một reference type, vì vậy không cần giải phóng nó khỏi bộ nhớ một cách rõ ràng bằng hàm ``free()``. Engine sẽ tự động giải phóng nó khi nó ra khỏi scope.

Lớp EditorImportPlugin
----------------------

Nhân vật chính ở đây là
:ref:`lớp EditorImportPlugin <class_EditorImportPlugin>`. Lớp này chịu trách nhiệm triển khai các phương thức được Godot gọi khi cần biết cách xử lý tệp.

Hãy bắt đầu viết plugin của chúng ta, từng phương thức một:

::

    # import_plugin.gd
    @tool
    extends EditorImportPlugin


    func _get_importer_name():
        return "demos.sillymaterial"

Phương thức đầu tiên là
:ref:`_get_importer_name()<class_EditorImportPlugin_private_method__get_importer_name>`. Đây là tên duy nhất cho plugin của bạn, được Godot sử dụng để biết import nào đã được dùng cho một tệp cụ thể. Khi tệp cần được import lại, editor sẽ biết cần gọi plugin nào.

::

    func _get_visible_name():
        return "Silly Material"

Phương thức :ref:`_get_visible_name()<class_EditorImportPlugin_private_method__get_visible_name>` chịu trách nhiệm trả về tên của loại mà plugin import và tên này sẽ được hiển thị cho người dùng trong Import dock.

Bạn nên chọn tên này như phần tiếp nối của "Import as", ví dụ *"Import as Silly Material"*. Bạn có thể đặt tên tùy ý, nhưng chúng tôi khuyến nghị dùng tên mô tả rõ plugin của bạn.

::

    func _get_recognized_extensions():
        return ["mtxt"]

Hệ thống import của Godot nhận diện loại tệp dựa trên phần mở rộng. Trong phương thức
:ref:`_get_recognized_extensions()<class_EditorImportPlugin_private_method__get_recognized_extensions>`, bạn trả về một mảng các chuỗi để biểu thị từng phần mở rộng mà plugin này có thể hiểu. Nếu một phần mở rộng được nhiều plugin nhận diện, người dùng có thể chọn plugin sẽ dùng khi import tệp.

.. tip:: Các phần mở rộng phổ biến như ``.json`` và ``.txt`` có thể được nhiều plugin sử dụng. Ngoài ra, trong project có thể có những tệp chỉ chứa dữ liệu cho game và không nên được import. Bạn phải cẩn thận khi import và xác thực dữ liệu. Đừng bao giờ giả định tệp có định dạng hợp lệ.

::

    func _get_save_extension():
        return "material"

Các tệp đã import được lưu trong thư mục ``.import`` ở thư mục gốc của project. Phần mở rộng của chúng phải khớp với loại resource bạn đang import, nhưng vì Godot không thể biết bạn sẽ sử dụng loại nào (do cùng một resource có thể có nhiều phần mở rộng hợp lệ), bạn cần khai báo phần mở rộng sẽ được dùng trong quá trình import.

Vì chúng ta đang import một Material, chúng ta sẽ dùng phần mở rộng đặc biệt dành cho loại resource này. Nếu đang import một scene, bạn có thể dùng phần mở rộng ``scn``. Generic resource có thể dùng phần mở rộng ``res``. Tuy nhiên, engine không bắt buộc điều này theo bất kỳ cách nào.

::

    func _get_resource_type():
        return "StandardMaterial3D"

Resource đã import có một loại cụ thể, vì vậy editor có thể biết nó thuộc về property slot nào. Điều này cho phép kéo và thả từ FileSystem dock vào một property trong Inspector.

Trong trường hợp của chúng ta, đó là một :ref:`class_StandardMaterial3D`, có thể được áp dụng cho các đối tượng 3D.

.. note:: Nếu cần import các loại khác nhau từ cùng một phần mở rộng, bạn phải tạo nhiều import plugin. Bạn có thể tách code import sang một tệp khác để tránh trùng lặp trong trường hợp này.

Tùy chọn và preset
------------------

Plugin của bạn có thể cung cấp nhiều tùy chọn khác nhau để người dùng kiểm soát cách resource được import. Nếu một tập hợp tùy chọn được chọn thường xuyên, bạn cũng có thể tạo các preset khác nhau để người dùng thao tác dễ hơn. Hình ảnh sau cho thấy các tùy chọn sẽ xuất hiện trong editor như thế nào:

.. image:: img/import_plugin_options.png

Vì có thể có nhiều preset và chúng được xác định bằng một số, nên sử dụng enum là một cách tốt để bạn có thể tham chiếu đến chúng bằng tên.

::

    @tool
    extends EditorImportPlugin


    enum Presets { DEFAULT }


    ...

Sau khi đã định nghĩa enum, hãy tiếp tục xem xét các phương thức của một import plugin:

::

    func _get_preset_count():
        return Presets.size()

Phương thức :ref:`_get_preset_count() <class_EditorImportPlugin_private_method__get_preset_count>` trả về số lượng preset mà plugin này định nghĩa. Hiện tại chúng ta chỉ có một preset, nhưng có thể làm cho phương thức này có khả năng mở rộng trong tương lai bằng cách trả về kích thước của enum ``Presets``.

::

    func _get_preset_name(preset_index):
        match preset_index:
            Presets.DEFAULT:
                return "Default"
            _:
                return "Unknown"


Ở đây chúng ta có phương thức
:ref:`_get_preset_name() <class_EditorImportPlugin_private_method__get_preset_name>`, dùng để đặt tên cho các preset khi chúng được hiển thị cho người dùng, vì vậy hãy đảm bảo dùng tên ngắn gọn và rõ ràng.

Ở đây, chúng ta có thể sử dụng câu lệnh ``match`` để làm cho code có cấu trúc hơn. Nhờ vậy, việc thêm preset mới trong tương lai sẽ dễ dàng. Chúng ta cũng dùng mẫu catch all để trả về một giá trị. Mặc dù Godot sẽ không yêu cầu các preset vượt quá số lượng preset bạn đã định nghĩa, luôn thận trọng vẫn tốt hơn.

Nếu chỉ có một preset, bạn có thể trả về trực tiếp tên của preset đó, nhưng nếu làm vậy, bạn phải cẩn thận khi thêm các preset khác.

::

    func _get_import_options(path, preset_index):
        match preset_index:
            Presets.DEFAULT:
                return [{
                           "name": "use_red_anyway",
                           "default_value": false
                        }]
            _:
                return []

Đây là phương thức định nghĩa các tùy chọn khả dụng.
:ref:`_get_import_options() <class_EditorImportPlugin_private_method__get_import_options>` trả về một mảng các dictionary, trong đó mỗi dictionary chứa một số key được kiểm tra để tùy chỉnh tùy chọn khi hiển thị cho người dùng. Bảng sau đây liệt kê các key có thể dùng:

+-------------------+------------+------------------------------------------------------------------------------------------------------------------+
| Key               | Type       | Description                                                                                                      |
+===================+============+==================================================================================================================+
| ``name``          | String     | Tên của tùy chọn. Khi hiển thị, dấu gạch dưới sẽ trở thành khoảng trắng và chữ cái đầu tiên được viết hoa.       |
+-------------------+------------+------------------------------------------------------------------------------------------------------------------+
| ``default_value`` | Any        | Giá trị mặc định của tùy chọn cho preset này.                                                                    |
+-------------------+------------+------------------------------------------------------------------------------------------------------------------+
| ``property_hint`` | Enum value | Một trong các giá trị :ref:`PropertyHint <enum_@GlobalScope_PropertyHint>` được dùng làm gợi ý.                  |
+-------------------+------------+------------------------------------------------------------------------------------------------------------------+
| ``hint_string``   | String     | Văn bản gợi ý của property. Giống như phần bạn thêm vào câu lệnh ``export`` trong GDScript.                      |
+-------------------+------------+------------------------------------------------------------------------------------------------------------------+
| ``usage``         | Enum value | Một trong các giá trị :ref:`PropertyUsageFlags <enum_@GlobalScope_PropertyUsageFlags>` để xác định cách sử dụng. |
+-------------------+------------+------------------------------------------------------------------------------------------------------------------+

Các khóa ``name`` và ``default_value`` là **mandatory**, những khóa còn lại là tùy chọn.

Lưu ý rằng phương thức ``_get_import_options`` nhận số preset, vì vậy bạn có thể cấu hình các tùy chọn cho từng preset khác nhau, đặc biệt là giá trị mặc định. Trong ví dụ này, chúng ta sử dụng câu lệnh ``match``, nhưng nếu có nhiều tùy chọn và các preset chỉ thay đổi giá trị, bạn có thể muốn tạo mảng tùy chọn trước rồi thay đổi mảng đó dựa trên preset.

.. warning:: Phương thức ``_get_import_options`` vẫn được gọi ngay cả khi bạn không định nghĩa preset (bằng cách để ``_get_preset_count`` trả về số 0). Bạn phải trả về một mảng, kể cả khi mảng đó rỗng, nếu không bạn có thể gặp lỗi.

::

    func _get_option_visibility(path, option_name, options):
        return true

Đối với
phương thức :ref:`_get_option_visibility() <class_EditorImportPlugin_private_method__get_option_visibility>`, chúng ta chỉ cần trả về ``true`` vì tất cả tùy chọn của chúng ta (tức là tùy chọn duy nhất đã định nghĩa) luôn hiển thị.

Nếu cần chỉ hiển thị một tùy chọn nhất định khi một tùy chọn khác được đặt thành một giá trị cụ thể, bạn có thể thêm logic vào phương thức này.

Phương thức ``import``
----------------------

Phần chính của quy trình, chịu trách nhiệm chuyển đổi các tệp thành resource, được thực hiện bởi phương thức :ref:`_import() <class_EditorImportPlugin_private_method__import>`. Mã mẫu của chúng ta hơi dài, vì vậy hãy chia thành một vài phần:

::

    func _import(source_file, save_path, options, r_platform_variants, r_gen_files):
        var file = FileAccess.open(source_file, FileAccess.READ)
        if file == null:
            return FileAccess.get_open_error()

        var line = file.get_line()

Phần đầu tiên của phương thức import mở và đọc tệp nguồn. Chúng ta sử dụng
class :ref:`FileAccess <class_FileAccess>` để thực hiện việc đó, truyền tham số ``source_file`` do editor cung cấp.

Nếu xảy ra lỗi khi mở tệp, chúng ta trả về lỗi đó để editor biết rằng quá trình import không thành công.

::

    var channels = line.split(",")
    if channels.size() != 3:
        return ERR_PARSE_ERROR

    var color
    if options.use_red_anyway:
        color = Color.from_rgba8(255, 0, 0)
    else:
        color = Color.from_rgba8(int(channels[0]), int(channels[1]), int(channels[2]))

Đoạn mã này lấy dòng mà nó vừa đọc từ tệp và tách dòng đó thành các phần được phân cách bằng dấu phẩy. Nếu có nhiều hơn hoặc ít hơn ba giá trị, đoạn mã coi tệp là không hợp lệ và báo lỗi.

Sau đó, đoạn mã tạo một biến :ref:`Color <class_Color>` mới và đặt các giá trị của biến theo tệp đầu vào. Nếu tùy chọn ``use_red_anyway`` được bật, đoạn mã sẽ đặt màu thành đỏ hoàn toàn.

::

    var material = StandardMaterial3D.new()
    material.albedo_color = color

Phần này tạo một :ref:`StandardMaterial3D <class_StandardMaterial3D>` mới, chính là resource đã import. Chúng ta tạo một instance mới của nó rồi đặt màu albedo thành giá trị đã nhận được trước đó.

::

    return ResourceSaver.save(material, "%s.%s" % [save_path, _get_save_extension()])

Đây là phần cuối cùng và khá quan trọng, vì tại đây chúng ta lưu resource đã tạo vào ổ đĩa. Đường dẫn của tệp đã lưu được tạo và truyền cho editor thông qua tham số ``save_path``. Lưu ý rằng đường dẫn này không bao gồm phần mở rộng, tức là **without**, nên chúng ta thêm phần mở rộng bằng :ref:`string formatting <doc_gdscript_printf>`. Để thực hiện việc này, chúng ta gọi phương thức ``_get_save_extension`` đã định nghĩa trước đó, nhờ vậy có thể đảm bảo chúng không bị lệch nhau.

Chúng ta cũng trả về kết quả từ
phương thức :ref:`ResourceSaver.save() <class_ResourceSaver_method_save>`, vì vậy nếu xảy ra lỗi ở bước này, editor sẽ biết về lỗi đó.

Các biến thể nền tảng và tệp được tạo
-------------------------------------

Có thể bạn đã nhận thấy plugin của chúng ta bỏ qua hai đối số của phương thức ``import``. Đây là các *return arguments* (do đó có ``r`` ở đầu tên), nghĩa là editor sẽ đọc chúng sau khi gọi phương thức import của bạn. Cả hai đều là các mảng mà bạn có thể điền thông tin vào.

Đối số ``r_platform_variants`` được dùng khi bạn cần import resource theo cách khác nhau tùy thuộc vào nền tảng đích. Mặc dù được gọi là các biến thể *platform*, chúng dựa trên sự hiện diện của :ref:`feature tags <doc_feature_tags>`, vì vậy ngay cả cùng một nền tảng cũng có thể có nhiều biến thể tùy theo thiết lập.

Để import một biến thể nền tảng, bạn cần lưu biến thể đó với feature tag đặt trước phần mở rộng, sau đó đưa tag vào mảng ``r_platform_variants`` để editor biết rằng bạn đã thực hiện việc đó.

Ví dụ, giả sử chúng ta lưu một material khác cho nền tảng di động. Chúng ta cần làm như sau:

::

    r_platform_variants.push_back("mobile")
    return ResourceSaver.save(mobile_material, "%s.%s.%s" % [save_path, "mobile", _get_save_extension()])

Đối số ``r_gen_files`` được dùng cho các tệp bổ sung được tạo trong quá trình import và cần được giữ lại. Editor sẽ kiểm tra đối số này để hiểu các dependency và đảm bảo tệp bổ sung không bị xóa ngoài ý muốn.

Đây cũng là một mảng và cần được điền bằng các đường dẫn đầy đủ của những tệp bạn lưu. Ví dụ, hãy tạo một material khác cho lần xử lý tiếp theo và lưu nó vào một tệp khác:

::

    var next_pass = StandardMaterial3D.new()
    next_pass.albedo_color = color.inverted()
    var next_pass_path = "%s.next_pass.%s" % [save_path, _get_save_extension()]

    err = ResourceSaver.save(next_pass, next_pass_path)
    if err != OK:
        return err
    r_gen_files.push_back(next_pass_path)

Thử plugin
----------

Cho đến đây mọi thứ chỉ là lý thuyết, nhưng giờ plugin import đã hoàn tất, hãy thử nghiệm plugin. Hãy đảm bảo bạn đã tạo tệp mẫu (với nội dung được mô tả trong phần giới thiệu) và lưu tệp đó dưới dạng ``test.mtxt``. Sau đó, kích hoạt plugin trong Project Settings.

Nếu mọi việc diễn ra suôn sẻ, plugin import sẽ được thêm vào editor và hệ thống tệp sẽ được quét, khiến resource tùy chỉnh xuất hiện trong dock FileSystem. Nếu chọn resource đó và chuyển đến dock Import, bạn sẽ thấy tùy chọn duy nhất có thể chọn ở đó.

Tạo một node MeshInstance3D trong scene, rồi thiết lập một SphereMesh mới cho property Mesh của node đó. Mở rộng phần Material trong Inspector, sau đó kéo tệp từ dock FileSystem vào property material. Đối tượng sẽ được cập nhật trong viewport với màu xanh dương của material đã import.

.. image:: img/import_plugin_trying.png

Đi đến dock Import, bật tùy chọn "Use Red Anyway", rồi nhấp vào "Reimport". Thao tác này sẽ cập nhật material đã import và tự động cập nhật chế độ xem để hiển thị màu đỏ.

Vậy là xong! Plugin import đầu tiên của bạn đã hoàn thành! Bây giờ hãy thỏa sức sáng tạo và tạo plugin cho các định dạng yêu thích của riêng bạn. Đây có thể là cách rất hữu ích để ghi dữ liệu ở một định dạng tùy chỉnh rồi sử dụng dữ liệu đó trong Godot như thể chúng là resource gốc. Điều này cho thấy hệ thống import mạnh mẽ và có thể mở rộng đến mức nào.
