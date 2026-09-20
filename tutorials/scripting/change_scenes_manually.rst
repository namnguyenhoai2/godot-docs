.. _doc_change_scenes_manually:

Chuyển scene theo cách thủ công
===============================

Đôi khi, bạn sẽ muốn kiểm soát nhiều hơn cách chuyển đổi giữa các scene. Các node con của :ref:`Viewport <class_Viewport>` sẽ được render vào hình ảnh mà nó tạo ra. Điều này vẫn đúng ngay cả với các node nằm ngoài scene "hiện tại". Autoload thuộc nhóm này, cũng như các scene mà bạn khởi tạo và thêm vào tree trong runtime:

.. tabs::
 .. code-tab:: gdscript GDScript

    var simultaneous_scene = preload("res://levels/level2.tscn").instantiate()

    func _add_a_scene_manually():
        # Điều này giống như autoload scene, chỉ là
        # nó diễn ra sau khi scene chính đã được load.
        get_tree().root.add_child(simultaneous_scene)

 .. code-tab:: csharp

    public Node simultaneousScene;

    public MyClass()
    {
        simultaneousScene = ResourceLoader.Load<PackedScene>("res://levels/level2.tscn").Instantiate();
    }

    public void _AddASceneManually()
    {
        // Điều này giống như autoload scene, chỉ là
        // nó diễn ra sau khi scene chính đã được load.
        GetTree().Root.AddChild(simultaneousScene);
    }

Để hoàn tất quá trình và thay scene mới cho scene cũ, bạn có một lựa chọn cần đưa ra. Có nhiều chiến lược để loại bỏ một scene khỏi chế độ hiển thị của :ref:`Viewport <class_Viewport>`. Sự đánh đổi nằm ở việc cân bằng tốc độ thao tác và mức tiêu thụ bộ nhớ, cũng như cân bằng khả năng truy cập và tính toàn vẹn của dữ liệu.

1. **Xóa scene hiện có.**
   :ref:`SceneTree.change_scene_to_file() <class_SceneTree_method_change_scene_to_file>` and
   :ref:`SceneTree.change_scene_to_packed() <class_SceneTree_method_change_scene_to_packed>`
   sẽ xóa scene hiện tại ngay lập tức. Bạn cũng có thể xóa scene chính. Giả sử tên của node gốc là "Main", bạn có thể dùng ``get_node("/root/Main").free()`` để xóa toàn bộ scene.

    - Giải phóng bộ nhớ.

        - Ưu điểm: RAM không còn phải gánh phần dữ liệu không cần thiết.

        - Nhược điểm: Việc quay lại scene đó sẽ tốn kém hơn vì scene phải được load lại vào bộ nhớ (mất cả thời gian VÀ bộ nhớ). Đây không phải vấn đề nếu không cần quay lại scene đó sớm.

        - Nhược điểm: Không còn truy cập được dữ liệu của scene đó. Đây không phải vấn đề nếu không cần sử dụng dữ liệu đó sớm.

        - Lưu ý: Bạn có thể giữ lại dữ liệu trong một scene sắp bị xóa bằng cách gắn lại một hoặc nhiều node của scene đó vào một scene khác, hoặc thậm chí trực tiếp vào :ref:`SceneTree <class_SceneTree>`.

    - Quá trình xử lý dừng lại.

        - Ưu điểm: Không có node nghĩa là không có quá trình xử lý, xử lý physics hoặc xử lý input. CPU có thể dành tài nguyên để làm việc với nội dung của scene mới.

        - Nhược điểm: Quá trình xử lý và xử lý input của các node đó không còn hoạt động. Đây không phải vấn đề nếu không cần sử dụng dữ liệu đã cập nhật.

2. **Ẩn scene hiện có.** Bằng cách thay đổi khả năng hiển thị hoặc phát hiện va chạm của các node, bạn có thể ẩn toàn bộ cây con của node khỏi góc nhìn của người chơi. Sử dụng
   :ref:`CanvasItem.hide() <class_CanvasItem_method_hide>` to hide a scene and
   :ref:`CanvasItem.show() <class_CanvasItem_method_show>` to show it again.

    - Bộ nhớ vẫn tồn tại.

        - Ưu điểm: Bạn vẫn có thể truy cập dữ liệu khi cần.

        - Ưu điểm: Không cần di chuyển thêm node nào để lưu dữ liệu.

        - Nhược điểm: Nhiều dữ liệu hơn được giữ trong bộ nhớ, điều này sẽ trở thành vấn đề trên các nền tảng nhạy cảm với bộ nhớ như web hoặc mobile.

    - Quá trình xử lý tiếp tục.

        - Ưu điểm: Dữ liệu tiếp tục nhận được các bản cập nhật xử lý, vì vậy scene sẽ tiếp tục cập nhật mọi dữ liệu bên trong nó phụ thuộc vào delta time hoặc dữ liệu frame.

        - Ưu điểm: Các node vẫn là thành viên của các group (vì group thuộc về
          :ref:`SceneTree <class_SceneTree>`).

        - Nhược điểm: Sự chú ý của CPU giờ đây bị chia sẻ giữa cả hai scene. Tải quá lớn có thể khiến frame rate thấp. Bạn nên kiểm tra hiệu năng trong quá trình phát triển để đảm bảo nền tảng mục tiêu có thể đáp ứng tải từ cách tiếp cận này.

3. **Gỡ scene hiện có khỏi tree.** Gán một biến cho node gốc của scene hiện có. Sau đó sử dụng
   :ref:`Node.remove_child(Node) <class_Node_method_remove_child>` to detach the entire
   scene khỏi tree. Để gắn nó lại sau này, hãy sử dụng
   :ref:`Node.add_child(Node) <class_Node_method_add_child>`.

    - Bộ nhớ vẫn tồn tại (các ưu/nhược điểm tương tự như khi ẩn scene khỏi chế độ hiển thị).

    - Quá trình xử lý dừng lại (các ưu/nhược điểm tương tự như khi xóa hoàn toàn scene).

    - Ưu điểm: Biến thể "ẩn" này dễ hiển thị/ẩn hơn nhiều. Thay vì phải theo dõi nhiều thay đổi trong scene, bạn chỉ cần gọi các phương thức add/remove_child. Cách này tương tự như việc vô hiệu hóa game object trong các engine khác.

    - Nhược điểm: Không giống như chỉ ẩn scene khỏi chế độ hiển thị, dữ liệu chứa trong scene sẽ trở nên lỗi thời nếu phụ thuộc vào delta time, input, group hoặc dữ liệu khác được lấy từ quyền truy cập :ref:`SceneTree <class_SceneTree>`.

Cũng có những trường hợp bạn muốn có nhiều scene cùng hiện diện một lúc, chẳng hạn như thêm singleton của riêng bạn trong runtime hoặc giữ lại dữ liệu của một scene giữa các lần thay đổi scene (thêm scene vào node gốc).

.. tabs::
 .. code-tab:: gdscript GDScript

        get_tree().root.add_child(scene)

 .. code-tab:: csharp

        GetTree().Root.AddChild(scene);

Một trường hợp khác có thể là hiển thị nhiều scene cùng lúc bằng cách
:ref:`SubViewportContainers <class_SubViewportContainer>`. This is optimal for
render các nội dung khác nhau ở những phần khác nhau của màn hình (ví dụ: minimap, multiplayer chia màn hình).

Mỗi tùy chọn sẽ phù hợp nhất với những trường hợp khác nhau, vì vậy bạn phải xem xét tác động của từng cách tiếp cận và xác định hướng đi phù hợp nhất với tình huống riêng của mình.
