:article_outdated: True

.. _doc_import_plugins:

Import plugins
==============

.. note:: This tutorial assumes you already know how to make generic plugins. If
          khi không chắc chắn, hãy tham khảo trang :ref:`doc_making_plugins`. Điều này cũng giả định rằng bạn đã quen với hệ thống import của Godot.

Giới thiệu
----------

Import plugin là một loại công cụ editor đặc biệt, cho phép Godot import các resource tùy chỉnh và xử lý chúng như các resource hạng nhất. Bản thân editor đi kèm với nhiều import plugin để xử lý các resource phổ biến như ảnh PNG, model Collada và glTF, âm thanh Ogg Vorbis, cùng nhiều loại khác.

Tutorial này hướng dẫn cách tạo một import plugin để load một file text tùy chỉnh dưới dạng material resource. File text này sẽ chứa ba giá trị số được phân tách bằng dấu phẩy, biểu thị ba kênh của một màu, và màu thu được sẽ được dùng làm albedo (màu chính) của material đã import. Trong ví dụ này, file chứa màu xanh dương thuần (red bằng không, green bằng không và blue ở mức tối đa):

.. code-block:: none

    0,0,255

Cấu hình
--------

Trước tiên, chúng ta cần một plugin tổng quát để xử lý việc khởi tạo và hủy import plugin. Hãy thêm file ``plugin.cfg`` trước:

.. code-block:: ini

    [plugin]

    name="Silly Material Importer"
    description="Imports a 3D Material from an external text file."
    author="Yours Truly"
    version="1.0"
    script="material_import.gd"

Tiếp theo, chúng ta cần file ``material_import.gd`` để thêm và xóa import plugin khi cần:

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

Khi plugin này được kích hoạt, nó sẽ tạo một instance mới của import plugin (chúng ta sẽ sớm tạo plugin này) và thêm nó vào editor bằng
:ref:`add_import_plugin() <class_EditorPlugin_method_add_import_plugin>` method. We store
một tham chiếu đến nó trong class member ``import_plugin`` để chúng ta có thể tham chiếu đến nó sau này khi xóa nó. Lệnh
:ref:`remove_import_plugin() <class_EditorPlugin_method_remove_import_plugin>` method is
được gọi khi plugin bị vô hiệu hóa để dọn dẹp bộ nhớ và cho editor biết rằng import plugin không còn khả dụng nữa.

Lưu ý rằng import plugin là một reference type, nên không cần giải phóng nó khỏi bộ nhớ một cách tường minh bằng function ``free()``. Engine sẽ tự động giải phóng nó khi nó ra khỏi scope.

Class EditorImportPlugin
------------------------

Nhân vật chính ở đây là
:ref:`EditorImportPlugin class <class_EditorImportPlugin>`. It is responsible for
triển khai các method được Godot gọi khi cần biết cách xử lý các file.

Hãy bắt đầu viết code cho plugin, từng method một:

::

    # import_plugin.gd
    @tool
    extends EditorImportPlugin


    func _get_importer_name():
        return "demos.sillymaterial"

Method đầu tiên là
:ref:`_get_importer_name()<class_EditorImportPlugin_private_method__get_importer_name>`. This is a
tên duy nhất cho plugin của bạn, được Godot sử dụng để biết import nào đã được dùng cho một file cụ thể. Khi các file cần được reimport, editor sẽ biết phải gọi plugin nào.

::

    func _get_visible_name():
        return "Silly Material"

Method :ref:`_get_visible_name()<class_EditorImportPlugin_private_method__get_visible_name>` chịu trách nhiệm trả về tên của type mà nó import, và tên này sẽ được hiển thị cho người dùng trong Import dock.

Bạn nên chọn tên này như phần tiếp nối của "Import as", ví dụ: *"Import as Silly Material"*. Bạn có thể đặt tên tùy ý, nhưng chúng tôi khuyến nghị dùng một tên mô tả rõ plugin của bạn.

::

    func _get_recognized_extensions():
        return ["mtxt"]

Hệ thống import của Godot phát hiện các loại file dựa trên phần mở rộng của chúng. Trong method
:ref:`_get_recognized_extensions()<class_EditorImportPlugin_private_method__get_recognized_extensions>`
bạn trả về một array các string để biểu thị từng phần mở rộng mà plugin này có thể hiểu. Nếu một phần mở rộng được nhiều plugin nhận diện, người dùng có thể chọn plugin sẽ dùng khi import các file.

.. tip:: Common extensions like ``.json`` and ``.txt`` might be used by many
         plugin. Ngoài ra, trong project có thể có những file chỉ chứa dữ liệu cho game và không nên được import. Bạn phải cẩn thận khi import và validate dữ liệu. Đừng bao giờ cho rằng file luôn có định dạng hợp lệ.

::

    func _get_save_extension():
        return "material"

Các file đã import được lưu trong folder ``.import`` ở thư mục gốc của project. Phần mở rộng của chúng nên khớp với type của resource bạn đang import, nhưng vì Godot không thể biết bạn sẽ sử dụng loại nào (do có thể có nhiều phần mở rộng hợp lệ cho cùng một resource), bạn cần khai báo phần mở rộng sẽ được dùng trong quá trình import.

Vì chúng ta đang import một Material, chúng ta sẽ dùng phần mở rộng đặc biệt dành cho các loại resource này. Nếu đang import một scene, bạn có thể dùng ``scn``. Các generic resource có thể dùng phần mở rộng ``res``. Tuy nhiên, engine không bắt buộc điều này dưới bất kỳ hình thức nào.

::

    func _get_resource_type():
        return "StandardMaterial3D"

Resource đã import có một type cụ thể, để editor biết nó thuộc về property slot nào. Điều này cho phép kéo và thả từ FileSystem dock vào một property trong Inspector.

Trong trường hợp của chúng ta, đó là một :ref:`class_StandardMaterial3D`, có thể được áp dụng cho các object 3D.

.. note:: If you need to import different types from the same extension, you
          phải tạo nhiều import plugin. Bạn có thể tách code import sang một file khác để tránh lặp code trong trường hợp này.

Các option và preset
--------------------

Plugin của bạn có thể cung cấp nhiều option khác nhau để người dùng kiểm soát cách resource được import. Nếu một tập hợp option đã chọn thường được dùng, bạn cũng có thể tạo các preset khác nhau để người dùng dễ sử dụng hơn. Hình ảnh sau đây cho thấy các option sẽ xuất hiện trong editor như thế nào:

.. image:: img/import_plugin_options.png

Vì có thể có nhiều preset và chúng được xác định bằng một số, một cách tốt là dùng enum để bạn có thể tham chiếu đến chúng bằng tên.

::

    @tool
    extends EditorImportPlugin


    enum Presets { DEFAULT }


    ...

Bây giờ enum đã được định nghĩa, hãy tiếp tục xem các method của một import plugin:

::

    func _get_preset_count():
        return Presets.size()

Method :ref:`_get_preset_count() <class_EditorImportPlugin_private_method__get_preset_count>` trả về số lượng preset mà plugin này định nghĩa. Hiện tại chúng ta chỉ có một preset, nhưng có thể làm cho method này tương thích với các thay đổi trong tương lai bằng cách trả về kích thước của enum ``Presets``.

::

    func _get_preset_name(preset_index):
        match preset_index:
            Presets.DEFAULT:
                return "Default"
            _:
                return "Unknown"


Ở đây chúng ta có
:ref:`_get_preset_name() <class_EditorImportPlugin_private_method__get_preset_name>` method, which
cung cấp tên cho các preset khi chúng được hiển thị cho người dùng, vì vậy hãy nhớ dùng các tên ngắn gọn và rõ ràng.

Chúng ta có thể dùng câu lệnh ``match`` ở đây để làm cho code có cấu trúc hơn. Nhờ vậy, việc thêm preset mới trong tương lai sẽ dễ dàng. Chúng ta cũng dùng pattern catch-all để trả về một giá trị. Mặc dù Godot sẽ không yêu cầu các preset vượt quá số lượng preset bạn đã định nghĩa, tốt nhất vẫn nên xử lý an toàn.

Nếu chỉ có một preset, bạn có thể đơn giản trả về trực tiếp tên của nó, nhưng nếu làm vậy, bạn phải cẩn thận khi thêm nhiều preset hơn.

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

Đây là method định nghĩa các option khả dụng.
:ref:`_get_import_options() <class_EditorImportPlugin_private_method__get_import_options>` returns
một array các dictionary, trong đó mỗi dictionary chứa một số key được kiểm tra để tùy chỉnh option khi hiển thị cho người dùng. Bảng sau đây liệt kê các key có thể dùng:

+-------------------+------------+----------------------------------------------------------------------------------------------------------+
| Key               | Type       | Description                                                                                              |
+===================+============+==========================================================================================================+
| ``name``          | String     | The name of the option. When showed, underscores become spaces and first letters are capitalized.        |
+-------------------+------------+----------------------------------------------------------------------------------------------------------+
| ``default_value`` | Any        | The default value of the option for this preset.                                                         |
+-------------------+------------+----------------------------------------------------------------------------------------------------------+
| ``property_hint`` | Enum value | One of the :ref:`PropertyHint <enum_@GlobalScope_PropertyHint>` values to use as hint.                   |
+-------------------+------------+----------------------------------------------------------------------------------------------------------+
| ``hint_string``   | String     | The hint text of the property. The same as you'd add in the ``export`` statement in GDScript.            |
+-------------------+------------+----------------------------------------------------------------------------------------------------------+
| ``usage``         | Enum value | One of the :ref:`PropertyUsageFlags <enum_@GlobalScope_PropertyUsageFlags>` values to define the usage.  |
+-------------------+------------+----------------------------------------------------------------------------------------------------------+

Các key ``name`` và ``default_value`` là **bắt buộc**, những key còn lại là tùy chọn.

Lưu ý rằng method ``_get_import_options`` nhận số hiệu preset, nên bạn có thể cấu hình các option cho từng preset khác nhau (đặc biệt là giá trị mặc định). Trong ví dụ này, chúng ta dùng câu lệnh ``match``, nhưng nếu có nhiều option và các preset chỉ thay đổi giá trị, bạn có thể muốn tạo array option trước rồi thay đổi nó dựa trên preset.

.. warning:: The ``_get_import_options`` method is called even if you don't
             định nghĩa các preset (bằng cách để ``_get_preset_count`` trả về số không). Bạn phải trả về một array ngay cả khi nó rỗng, nếu không có thể xảy ra lỗi.

::

    func _get_option_visibility(path, option_name, options):
        return true

Đối với method
:ref:`_get_option_visibility() <class_EditorImportPlugin_private_method__get_option_visibility>`
chúng ta chỉ cần trả về ``true`` vì tất cả option của chúng ta (tức là option duy nhất đã định nghĩa) đều luôn hiển thị.

Nếu cần chỉ hiển thị một option nhất định khi một option khác được đặt thành một giá trị cụ thể, bạn có thể thêm logic vào method này.

Method ``import``
-----------------

Phần quan trọng nhất của quy trình, chịu trách nhiệm chuyển đổi các file thành resource, được xử lý bởi method :ref:`_import() <class_EditorImportPlugin_private_method__import>`. Code mẫu của chúng ta hơi dài, vì vậy hãy chia thành một vài phần:

::

    func _import(source_file, save_path, options, r_platform_variants, r_gen_files):
        var file = FileAccess.open(source_file, FileAccess.READ)
        if file == null:
            return FileAccess.get_open_error()

        var line = file.get_line()

Phần đầu tiên của import method mở và đọc file nguồn. Chúng ta sử dụng
:ref:`FileAccess <class_FileAccess>` class to do that, passing the ``source_file``
parameter được editor cung cấp.

Nếu xảy ra lỗi khi mở file, chúng ta trả về lỗi đó để editor biết rằng quá trình import không thành công.

::

    var channels = line.split(",")
    if channels.size() != 3:
        return ERR_PARSE_ERROR

    var color
    if options.use_red_anyway:
        color = Color.from_rgba8(255, 0, 0)
    else:
        color = Color.from_rgba8(int(channels[0]), int(channels[1]), int(channels[2]))

Code này lấy dòng mà nó vừa đọc từ file và tách dòng đó thành các phần được phân tách bằng dấu phẩy. Nếu có nhiều hơn hoặc ít hơn ba giá trị, code sẽ coi file là không hợp lệ và báo lỗi.

Sau đó, code tạo một biến :ref:`Color <class_Color>` mới và đặt các giá trị của biến theo file đầu vào. Nếu option ``use_red_anyway`` được bật, code sẽ đặt màu thành đỏ thuần thay thế.

::

    var material = StandardMaterial3D.new()
    material.albedo_color = color

Phần này tạo một :ref:`StandardMaterial3D <class_StandardMaterial3D>` mới, chính là resource đã import. Chúng ta tạo một instance mới của nó, sau đó đặt màu albedo của nó thành giá trị đã nhận được trước đó.

::

    return ResourceSaver.save(material, "%s.%s" % [save_path, _get_save_extension()])

Đây là phần cuối cùng và khá quan trọng, vì ở đây chúng ta lưu resource đã tạo vào disk. Path của file được lưu được tạo và truyền cho editor thông qua parameter ``save_path``. Lưu ý rằng path này **không bao gồm** phần mở rộng, nên chúng ta thêm phần mở rộng bằng :ref:`string formatting <doc_gdscript_printf>`. Để làm việc này, chúng ta gọi method ``_get_save_extension`` đã định nghĩa trước đó, nhờ vậy có thể chắc chắn rằng chúng sẽ không bị lệch nhau.

Chúng ta cũng trả về kết quả từ
:ref:`ResourceSaver.save() <class_ResourceSaver_method_save>` method, so if there's an
nếu xảy ra lỗi ở bước này, editor sẽ biết về lỗi đó.

Các biến thể theo platform và file được tạo
-------------------------------------------

Có thể bạn đã nhận thấy plugin của chúng ta đã bỏ qua hai argument của method ``import``. Đây là các *return argument* (do đó có ``r`` ở đầu tên), nghĩa là editor sẽ đọc chúng sau khi gọi import method của bạn. Cả hai đều là array mà bạn có thể điền thông tin vào.

Đối số ``r_platform_variants`` được sử dụng nếu bạn cần import resource theo cách khác nhau tùy thuộc vào platform đích. Mặc dù được gọi là các biến thể *platform*, chúng dựa trên sự hiện diện của :ref:`feature tags <doc_feature_tags>`, vì vậy ngay cả cùng một platform cũng có thể có nhiều biến thể tùy thuộc vào thiết lập.

Để import một biến thể platform, bạn cần lưu nó với feature tag trước phần mở rộng, sau đó đưa tag vào mảng ``r_platform_variants`` để editor biết rằng bạn đã thực hiện việc đó.

Ví dụ, giả sử chúng ta lưu một material khác cho một platform di động. Chúng ta cần thực hiện như sau:

::

    r_platform_variants.push_back("mobile")
    return ResourceSaver.save(mobile_material, "%s.%s.%s" % [save_path, "mobile", _get_save_extension()])

Đối số ``r_gen_files`` dùng cho các file bổ sung được tạo trong quá trình import và cần được giữ lại. Editor sẽ kiểm tra đối số này để hiểu các dependency và đảm bảo file bổ sung không bị xóa ngoài ý muốn.

Đây cũng là một mảng và cần được điền bằng full path của các file bạn lưu. Ví dụ, hãy tạo một material khác cho pass tiếp theo và lưu nó vào một file khác:

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

Cho đến đây mọi thứ mới chỉ mang tính lý thuyết, nhưng giờ plugin import đã hoàn tất, hãy thử nghiệm nó. Hãy đảm bảo bạn đã tạo sample file (với nội dung được mô tả trong phần giới thiệu) và lưu nó thành ``test.mtxt``. Sau đó, hãy kích hoạt plugin trong Project Settings.

Nếu mọi việc diễn ra suôn sẻ, plugin import sẽ được thêm vào editor và file system sẽ được quét, khiến custom resource xuất hiện trong FileSystem dock. Nếu bạn chọn nó và chuyển sang Import dock, bạn sẽ thấy tùy chọn duy nhất có thể chọn tại đó.

Tạo một node MeshInstance3D trong scene, rồi thiết lập một SphereMesh mới cho thuộc tính Mesh. Mở rộng phần Material trong Inspector, sau đó kéo file từ FileSystem dock vào thuộc tính material. Đối tượng sẽ được cập nhật trong viewport với màu xanh dương của material đã import.

.. image:: img/import_plugin_trying.png

Đi đến Import dock, bật tùy chọn "Use Red Anyway", rồi nhấp vào "Reimport". Thao tác này sẽ cập nhật material đã import và tự động cập nhật chế độ xem để hiển thị màu đỏ thay thế.

Vậy là xong! Plugin import đầu tiên của bạn đã hoàn tất! Giờ hãy thỏa sức sáng tạo và tạo plugin cho các format yêu thích của riêng bạn. Việc này có thể rất hữu ích khi bạn muốn ghi dữ liệu ở một format tùy chỉnh, sau đó sử dụng dữ liệu đó trong Godot như thể chúng là native resource. Điều này cho thấy hệ thống import mạnh mẽ và có khả năng mở rộng đến mức nào.
