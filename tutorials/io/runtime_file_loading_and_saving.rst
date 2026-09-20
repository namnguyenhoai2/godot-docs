.. _doc_runtime_loading_and_saving:

Tải và lưu tệp trong runtime
============================

.. seealso::

    Xem :ref:`doc_saving_games` để biết thông tin về việc lưu và tải tiến trình trò chơi.

Đôi khi, :ref:`exporting packs, patches, and mods <doc_exporting_pcks>` không phải là lựa chọn lý tưởng nếu bạn muốn người chơi có thể tải nội dung do người dùng tạo trong dự án của mình. Cách này yêu cầu người dùng tạo tệp PCK hoặc ZIP thông qua Godot editor, trong đó chứa các tài nguyên đã được Godot import.

Các trường hợp sử dụng điển hình cho việc tải và lưu tệp trong runtime bao gồm:

- Tải các texture pack được thiết kế cho trò chơi. - Tải các bản nhạc do người dùng cung cấp và phát chúng trong một đài radio trong trò chơi. - Tải các level hoặc model 3D tùy chỉnh, có thể được thiết kế bằng bất kỳ 3D DCC nào có thể export sang glTF hoặc FBX (bao gồm các scene glTF được Godot lưu trong runtime). - Sử dụng font do người dùng cung cấp cho menu và HUD. - Lưu/tải một định dạng tệp có thể chứa nhiều tệp nhưng vẫn dễ dàng được các ứng dụng khác đọc (ZIP). - Tải các tệp được tạo bởi một trò chơi hoặc chương trình khác, hoặc thậm chí các tệp dữ liệu trò chơi từ một trò chơi khác không được tạo bằng Godot.

Có thể kết hợp việc tải tệp trong runtime với :ref:`HTTP requests <doc_http_request_class>` để tải tài nguyên trực tiếp từ Internet.

.. warning::

    **Không** sử dụng cách tải trong runtime này để tải các tài nguyên thuộc về dự án, vì cách này kém hiệu quả hơn và không cho phép tận dụng chức năng quản lý tài nguyên của Godot (chẳng hạn như translation remap). Xem
    :ref:`doc_import_process` for details.

.. seealso::

    Bạn có thể xem cách hoạt động của việc lưu và tải thông qua `Run-time File Saving and Loading (Serialization) demo project <https://github.com/godotengine/godot-demo-projects/blob/master/loading/runtime_save_load>`__.

Tệp văn bản thuần túy và tệp nhị phân
-------------------------------------

Class :ref:`class_FileAccess` của Godot cung cấp các method để truy cập các tệp trên filesystem nhằm đọc và ghi:

.. tabs::
 .. code-tab:: gdscript

    func save_file(content):
        var file = FileAccess.open("/path/to/file.txt", FileAccess.WRITE)
        file.store_string(content)

    func load_file():
        var file = FileAccess.open("/path/to/file.txt", FileAccess.READ)
        var content = file.get_as_text()
        return content

 .. code-tab:: csharp

    private void SaveFile(string content)
    {
        using var file = FileAccess.Open("/Path/To/File.txt", FileAccess.ModeFlags.Write);
        file.StoreString(content);
    }

    private string LoadFile()
    {
        using var file = FileAccess.Open("/Path/To/File.txt", FileAccess.ModeFlags.Read);
        string content = file.GetAsText();
        return content;
    }

Để xử lý các định dạng nhị phân tùy chỉnh (chẳng hạn như tải các định dạng tệp không được Godot hỗ trợ), :ref:`class_FileAccess` cung cấp một số method để đọc/ghi integer, float, string và nhiều kiểu dữ liệu khác. Các method FileAccess này có tên bắt đầu bằng ``get_`` và ``store_``.

Nếu cần kiểm soát nhiều hơn khi đọc tệp nhị phân hoặc cần đọc các binary stream không thuộc về một tệp, :ref:`class_PackedByteArray` cung cấp một số helper method để decode/encode chuỗi byte thành integer, float, string và nhiều kiểu dữ liệu khác. Các method PackedByteArray này có tên bắt đầu bằng ``decode_`` và ``encode_``. Xem thêm :ref:`doc_binary_serialization_api`.

.. _doc_runtime_file_loading_and_saving_images:

Hình ảnh
--------

Static method :ref:`Image.load_from_file <class_Image_method_load_from_file>` của Image xử lý mọi thứ, từ việc nhận diện định dạng dựa trên phần mở rộng tệp cho đến đọc tệp từ ổ đĩa.

Nếu cần xử lý lỗi hoặc kiểm soát nhiều hơn (chẳng hạn như thay đổi scale mà SVG được load), hãy sử dụng một trong các method sau tùy theo định dạng tệp:

- :ref:`Image.load_jpg_from_buffer <class_Image_method_load_jpg_from_buffer>` - :ref:`Image.load_ktx_from_buffer <class_Image_method_load_ktx_from_buffer>` - :ref:`Image.load_png_from_buffer <class_Image_method_load_png_from_buffer>` - :ref:`Image.load_svg_from_buffer <class_Image_method_load_svg_from_buffer>` hoặc :ref:`Image.load_svg_from_string <class_Image_method_load_svg_from_string>` - :ref:`Image.load_tga_from_buffer <class_Image_method_load_tga_from_buffer>` - :ref:`Image.load_webp_from_buffer <class_Image_method_load_webp_from_buffer>` - :ref:`Image.load_exr_from_buffer <class_Image_method_load_exr_from_buffer>`

Một số định dạng hình ảnh cũng có thể được Godot lưu trong runtime bằng các method sau:

- :ref:`Image.save_png <class_Image_method_save_png>` hoặc :ref:`Image.save_png_to_buffer <class_Image_method_save_png_to_buffer>` - :ref:`Image.save_webp <class_Image_method_save_webp>` hoặc :ref:`Image.save_webp_to_buffer <class_Image_method_save_webp_to_buffer>` - :ref:`Image.save_jpg <class_Image_method_save_jpg>` hoặc :ref:`Image.save_jpg_to_buffer <class_Image_method_save_jpg_to_buffer>` - :ref:`Image.save_exr <class_Image_method_save_exr>` hoặc :ref:`Image.save_exr_to_buffer <class_Image_method_save_exr_to_buffer>`

Các method có hậu tố ``to_buffer`` sẽ lưu hình ảnh vào một PackedByteArray thay vì filesystem. Điều này hữu ích khi gửi hình ảnh qua network hoặc vào một ZIP archive mà không cần ghi hình ảnh lên filesystem. Cách này có thể tăng performance bằng cách giảm mức sử dụng I/O.

.. note::

    Nếu hiển thị hình ảnh đã load trên một bề mặt 3D, hãy nhớ gọi
    :ref:`Image.generate_mipmaps <class_Image_method_generate_mipmaps>`
    để texture không bị nhiễu hạt khi xem từ xa. Điều này cũng hữu ích trong 2D khi làm theo hướng dẫn trên
    :ref:`reducing aliasing when downsampling <doc_multiple_resolutions_reducing_aliasing_on_downsampling>`.

Ví dụ về cách load một hình ảnh và hiển thị hình ảnh đó trong một node :ref:`class_TextureRect` (yêu cầu chuyển đổi sang :ref:`class_ImageTexture`):

.. tabs::
 .. code-tab:: gdscript

    # Load một hình ảnh thuộc bất kỳ định dạng nào được Godot hỗ trợ từ filesystem.
    var image = Image.load_from_file(path)
    # Tùy chọn, tạo mipmap nếu hiển thị texture trên một bề mặt 3D
    # để texture không bị nhiễu hạt khi xem từ xa.
    #image.generate_mipmaps()
    $TextureRect.texture = ImageTexture.create_from_image(image)

    # Lưu Image đã load thành một hình ảnh PNG.
    image.save_png("/path/to/file.png")

    # Lưu ImageTexture đã chuyển đổi thành một hình ảnh PNG.
    $TextureRect.texture.get_image().save_png("/path/to/file.png")

 .. code-tab:: csharp

    // Load một hình ảnh thuộc bất kỳ định dạng nào được Godot hỗ trợ từ filesystem.
    var image = Image.LoadFromFile(path);
    // Tùy chọn, tạo mipmap nếu hiển thị texture trên một bề mặt 3D
    // để texture không bị nhiễu hạt khi xem từ xa.
    // image.GenerateMipmaps();
    GetNode<TextureRect>("TextureRect").Texture = ImageTexture.CreateFromImage(image);

    // Lưu Image đã load thành một hình ảnh PNG.
    image.SavePng("/Path/To/File.png");

    // Lưu ImageTexture đã chuyển đổi thành một hình ảnh PNG.
    GetNode<TextureRect>("TextureRect").Texture.GetImage().SavePng("/Path/To/File.png");

.. _doc_runtime_file_loading_and_saving_audio_video_files:

Tệp audio/video
---------------

Godot hỗ trợ load audio Ogg Vorbis, MP3 và WAV trong runtime. Lưu ý rằng *không phải tất cả* các tệp có phần mở rộng ``.ogg`` đều là tệp Ogg Vorbis. Một số tệp có thể là video Ogg Theora hoặc chứa audio Opus bên trong một Ogg container. Những tệp này sẽ **không** được load chính xác dưới dạng tệp audio trong Godot.

Ví dụ về cách load một tệp audio Ogg Vorbis trong một node :ref:`class_AudioStreamPlayer`:

.. tabs::
 .. code-tab:: gdscript

    $AudioStreamPlayer.stream = AudioStreamOggVorbis.load_from_file(path)

 .. code-tab:: csharp

    GetNode<AudioStreamPlayer>("AudioStreamPlayer").Stream = AudioStreamOggVorbis.LoadFromFile(path);

Ví dụ về cách load một tệp video Ogg Theora trong một node :ref:`class_VideoStreamPlayer`:

.. tabs::
 .. code-tab:: gdscript

    var video_stream_theora = VideoStreamTheora.new()
    # Phần mở rộng tệp bị bỏ qua, vì vậy có thể load các video Ogg Theora
    # có phần mở rộng `.ogg` theo cách này.
    video_stream_theora.file = "/path/to/file.ogv"
    $VideoStreamPlayer.stream = video_stream_theora

    # Property Autoplay của VideoStreamPlayer sẽ không hoạt động nếu stream đang rỗng
    # trước khi property này được thiết lập, vì vậy hãy gọi `play()` sau khi thiết lập `stream`.
    $VideoStreamPlayer.play()

 .. code-tab:: csharp

    var videoStreamTheora = new VideoStreamTheora();
    // Phần mở rộng tệp bị bỏ qua, vì vậy có thể load các video Ogg Theora
    // có phần mở rộng `.ogg` theo cách này.
    videoStreamTheora.File = "/Path/To/File.ogv";
    GetNode<VideoStreamPlayer>("VideoStreamPlayer").Stream = videoStreamTheora;

    // Property Autoplay của VideoStreamPlayer sẽ không hoạt động nếu stream đang rỗng
    // trước khi property này được thiết lập, vì vậy hãy gọi `Play()` sau khi thiết lập `Stream`.
    GetNode<VideoStreamPlayer>("VideoStreamPlayer").Play();

.. _doc_runtime_file_loading_and_saving_3d_scenes:

Scene 3D
--------

Godot hỗ trợ glTF 2.0 toàn diện, cả trong editor lẫn các project đã export. Khi sử dụng :ref:`class_gltfdocument` và :ref:`class_gltfstate` cùng nhau, Godot có thể load và lưu các tệp glTF trong các project đã export, ở cả định dạng văn bản (``.gltf``) và nhị phân (``.glb``). Nên ưu tiên định dạng nhị phân vì định dạng này ghi nhanh hơn và có kích thước nhỏ hơn, nhưng định dạng văn bản dễ debug hơn.

Kể từ Godot 4.3, các scene FBX cũng có thể được load (nhưng không thể lưu) trong runtime bằng cách sử dụng
:ref:`class_fbxdocument` and :ref:`class_fbxstate` classes. The code to do so
hoạt động giống glTF, nhưng bạn sẽ cần thay thế tất cả các instance của ``GLTFDocument`` và ``GLTFState`` bằng ``FBXDocument`` và ``FBXState`` trong các code sample bên dưới.

Ví dụ về cách load một scene glTF và thêm node gốc của scene đó vào scene:

.. tabs::
 .. code-tab:: gdscript

    # Load một scene glTF hiện có.
    # GLTFState được GLTFDocument sử dụng để lưu state của scene đã load.
    # GLTFDocument là class thực sự xử lý việc load dữ liệu glTF vào một cây node Godot,
    # điều đó có nghĩa là class này hỗ trợ các tính năng glTF như ánh sáng và camera.
    var gltf_document_load = GLTFDocument.new()
    var gltf_state_load = GLTFState.new()
    var error = gltf_document_load.append_from_file("/path/to/file.gltf", gltf_state_load)
    if error == OK:
        var gltf_scene_root_node = gltf_document_load.generate_scene(gltf_state_load)
        add_child(gltf_scene_root_node)
    else:
        show_error("Couldn't load glTF scene (error code: %s)." % error_string(error))

    # Lưu một scene glTF mới.
    var gltf_document_save := GLTFDocument.new()
    var gltf_state_save := GLTFState.new()
    gltf_document_save.append_from_scene(gltf_scene_root_node, gltf_state_save)
    # Phần mở rộng tệp trong `path` đầu ra (`.gltf` hoặc `.glb`) xác định
    # liệu đầu ra sử dụng định dạng văn bản hay nhị phân.
    # `GLTFDocument.generate_buffer()` cũng có sẵn để lưu vào memory.
    gltf_document_save.write_to_filesystem(gltf_state_save, path)

 .. code-tab:: csharp

    // Load một scene glTF hiện có.
    // GLTFState được GLTFDocument sử dụng để lưu state của scene đã load.
    // GLTFDocument là class thực sự xử lý việc load dữ liệu glTF vào một cây node Godot,
    // điều đó có nghĩa là class này hỗ trợ các tính năng glTF như ánh sáng và camera.
    var gltfDocumentLoad = new GltfDocument();
    var gltfStateLoad = new GltfState();
    var error = gltfDocumentLoad.AppendFromFile("/Path/To/File.gltf", gltfStateLoad);
    if (error == Error.Ok)
    {
        var gltfSceneRootNode = gltfDocumentLoad.GenerateScene(gltfStateLoad);
        AddChild(gltfSceneRootNode);
    }
    else
    {
        GD.PrintErr($"Couldn't load glTF scene (error code: {error}).");
    }

    // Lưu một scene glTF mới.
    var gltfDocumentSave = new GltfDocument();
    var gltfStateSave = new GltfState();
    gltfDocumentSave.AppendFromScene(gltfSceneRootNode, gltfStateSave);
    // Phần mở rộng tệp trong `path` đầu ra (`.gltf` hoặc `.glb`) xác định
    // liệu đầu ra sử dụng định dạng văn bản hay nhị phân.
    // `GltfDocument.GenerateBuffer()` cũng có sẵn để lưu vào memory.
    gltfDocumentSave.WriteToFilesystem(gltfStateSave, path);

.. note::

    Khi load một scene glTF, phải thiết lập *base path* để các tài nguyên bên ngoài như texture có thể được load chính xác. Khi load từ một tệp, base path được tự động thiết lập thành thư mục chứa tệp đó. Khi load từ một buffer, phải thiết lập base path thủ công vì Godot không có cách nào suy ra path này.

    Để thiết lập base path, hãy thiết lập
    :ref:`GLTFState.base_path <class_GLTFState_property_base_path>` on your
    instance GLTFState *trước khi* gọi
    :ref:`GLTFDocument.append_from_buffer <class_GLTFDocument_method_append_from_buffer>`
    hoặc :ref:`GLTFDocument.append_from_file <class_GLTFDocument_method_append_from_file>`.

.. _doc_runtime_file_loading_and_saving_fonts:

Font
----

:ref:`FontFile.load_dynamic_font <class_FontFile_method_load_bitmap_font>` supports the following
các định dạng tệp font: TTF, OTF, WOFF, WOFF2, PFB, PFM

Mặt khác, :ref:`FontFile.load_bitmap_font <class_FontFile_method_load_bitmap_font>` hỗ trợ định dạng `BMFont <https://www.angelcode.com/products/bmfont/>`__ (``.fnt`` hoặc ``.font``).

Ngoài ra, có thể load bất kỳ font nào được cài đặt trên hệ thống bằng cách sử dụng tính năng hỗ trợ :ref:`doc_using_fonts_system_fonts` của Godot.

Ví dụ về cách tự động load một tệp font dựa trên phần mở rộng tệp, sau đó thêm font đó làm theme override cho một node :ref:`class_Label`:

.. tabs::
 .. code-tab:: gdscript

    var path = "/path/to/font.ttf"
    var path_lower = path.to_lower()
    var font_file = FontFile.new()
    if (
            path_lower.ends_with(".ttf")
            or path_lower.ends_with(".otf")
            or path_lower.ends_with(".woff")
            or path_lower.ends_with(".woff2")
            or path_lower.ends_with(".pfb")
            or path_lower.ends_with(".pfm")
    ):
        font_file.load_dynamic_font(path)
    elif path_lower.ends_with(".fnt") or path_lower.ends_with(".font"):
        font_file.load_bitmap_font(path)
    else:
        push_error("Invalid font file format.")

    if not font_file.data.is_empty():
        # Nếu font được load thành công, hãy thêm font đó làm theme override.
        $Label.add_theme_font_override("font", font_file)

 .. code-tab:: csharp

    string path = "/Path/To/Font.ttf";
    var fontFile = new FontFile();

    if (
        path.EndsWith(".ttf", StringComparison.OrdinalIgnoreCase)
        || path.EndsWith(".otf", StringComparison.OrdinalIgnoreCase)
        || path.EndsWith(".woff", StringComparison.OrdinalIgnoreCase)
        || path.EndsWith(".woff2", StringComparison.OrdinalIgnoreCase)
        || path.EndsWith(".pfb", StringComparison.OrdinalIgnoreCase)
        || path.EndsWith(".pfm", StringComparison.OrdinalIgnoreCase)
    )
    {
        fontFile.LoadDynamicFont(path);
    }
    else if (path.EndsWith(".fnt", StringComparison.OrdinalIgnoreCase) || path.EndsWith(".font", StringComparison.OrdinalIgnoreCase))
    {
        fontFile.LoadBitmapFont(path);
    }
    else
    {
        GD.PrintErr("Invalid font file format.");
    }

    if (!fontFile.Data.IsEmpty())
    {
        // Nếu font được load thành công, hãy thêm font đó làm theme override.
        GetNode<Label>("Label").AddThemeFontOverride("font", fontFile);
    }

ZIP archive
-----------

Godot hỗ trợ đọc và ghi ZIP archive bằng các class :ref:`class_zipreader` và :ref:`class_zippacker`. Tính năng này hỗ trợ mọi tệp ZIP, bao gồm các tệp được tạo bởi chức năng "Export PCK/ZIP" của Godot (mặc dù các tệp này sẽ chứa các tài nguyên Godot đã import thay vì các tệp project gốc).

.. note::

    Sử dụng :ref:`ProjectSettings.load_resource_pack <class_ProjectSettings_method_load_resource_pack>` để load các tệp PCK hoặc ZIP được Godot export làm
    :ref:`additional data packs <doc_exporting_pcks>`. That approach is preferred
    cho DLC, vì cách này giúp việc tương tác với các data pack bổ sung trở nên liền mạch (virtual filesystem).

Tính năng hỗ trợ ZIP archive này có thể được kết hợp với việc load image, scene 3D và audio trong runtime để mang lại trải nghiệm modding liền mạch mà không yêu cầu người dùng phải sử dụng Godot editor để tạo tệp PCK/ZIP.

Ví dụ liệt kê các tệp trong một kho lưu trữ ZIP trong node :ref:`class_ItemList`, sau đó ghi nội dung đọc được từ đó vào một kho lưu trữ ZIP mới (về cơ bản là sao chép kho lưu trữ):

.. tabs::
 .. code-tab:: gdscript

    # Tải một kho lưu trữ ZIP hiện có.
    var zip_reader = ZIPReader.new()
    zip_reader.open(path)
    var files = zip_reader.get_files()
    # Danh sách tệp không được sắp xếp theo mặc định. Hãy sắp xếp danh sách để quá trình xử lý nhất quán hơn.
    files.sort()
    for file in files:
        $ItemList.add_item(file, null)
        # Tắt các thư mục trong danh sách.
        $ItemList.set_item_disabled(-1, file.ends_with("/"))

    # Lưu một kho lưu trữ ZIP mới.
    var zip_packer = ZIPPacker.new()
    var error = zip_packer.open(path)
    if error != OK:
        push_error("Couldn't open path for saving ZIP archive (error code: %s)." % error_string(error))
        return

    # Tái sử dụng instance ZIPReader ở trên để đọc các tệp từ một kho lưu trữ ZIP hiện có.
    for file in zip_reader.get_files():
        zip_packer.start_file(file)
        zip_packer.write_file(zip_reader.read_file(file))
        zip_packer.close_file()

    zip_packer.close()

 .. code-tab:: csharp

    // Tải một kho lưu trữ ZIP hiện có.
    var zipReader = new ZipReader();
    zipReader.Open(path);
    string[] files = zipReader.GetFiles();
    // Danh sách tệp không được sắp xếp theo mặc định. Hãy sắp xếp danh sách để quá trình xử lý nhất quán hơn.
    Array.Sort(files);
    foreach (string file in files)
    {
        GetNode<ItemList>("ItemList").AddItem(file);
        // Tắt các thư mục trong danh sách.
        GetNode<ItemList>("ItemList").SetItemDisabled(-1, file.EndsWith('/'));
    }

    // Lưu một kho lưu trữ ZIP mới.
    var zipPacker = new ZipPacker();
    var error = zipPacker.Open(path);
    if (error != Error.Ok)
    {
        GD.PrintErr($"Couldn't open path for saving ZIP archive (error code: {error}).");
        return;
    }

    // Tái sử dụng instance ZIPReader ở trên để đọc các tệp từ một kho lưu trữ ZIP hiện có.
    foreach (string file in zipReader.GetFiles())
    {
        zipPacker.StartFile(file);
        zipPacker.WriteFile(zipReader.ReadFile(file));
        zipPacker.CloseFile();
    }

    zipPacker.Close();
