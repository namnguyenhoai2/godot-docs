.. _doc_change_scenes_manually:

Thay đổi scene theo cách thủ công
=================================

Đôi khi, việc kiểm soát nhiều hơn cách bạn chuyển đổi giữa các scene sẽ rất hữu ích. Các nút con của :ref:`Viewport <class_Viewport>` sẽ được render thành hình ảnh mà nó tạo ra. Điều này vẫn đúng ngay cả với các nút nằm ngoài scene "hiện tại". Autoload thuộc trường hợp này, cũng như các scene mà bạn khởi tạo và thêm vào tree trong runtime:

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

Để hoàn tất chu trình và thay scene mới cho scene cũ, bạn cần đưa ra một lựa chọn. Có nhiều chiến lược để loại bỏ một scene khỏi tầm nhìn của :ref:`Viewport <class_Viewport>`. Những đánh đổi liên quan đến việc cân bằng tốc độ hoạt động và mức tiêu thụ bộ nhớ, cũng như cân bằng khả năng truy cập và tính toàn vẹn của dữ liệu.

1. **Xóa scene hiện có.**
   :ref:`SceneTree.change_scene_to_file() <class_SceneTree_method_change_scene_to_file>` và
   :ref:`SceneTree.change_scene_to_packed() <class_SceneTree_method_change_scene_to_packed>` sẽ xóa scene hiện tại ngay lập tức. Bạn cũng có thể xóa scene chính. Giả sử tên của nút gốc là "Main", bạn có thể dùng ``get_node("/root/Main").free()`` để xóa toàn bộ scene.

    - Giải phóng bộ nhớ.

        - Ưu điểm: RAM không còn phải giữ phần dữ liệu thừa không cần thiết.

        - Nhược điểm: Việc quay lại scene đó giờ sẽ tốn kém hơn vì scene phải được load lại vào bộ nhớ (tốn cả thời gian VÀ bộ nhớ). Đây không phải vấn đề nếu bạn không cần sớm quay lại scene đó.

        - Nhược điểm: Không còn quyền truy cập vào dữ liệu của scene đó. Đây không phải vấn đề nếu bạn không cần sớm sử dụng dữ liệu đó.

        - Lưu ý: Bạn có thể muốn bảo toàn dữ liệu trong một scene sắp bị xóa bằng cách gắn lại một hoặc nhiều nút của scene đó vào một scene khác, hoặc thậm chí trực tiếp vào :ref:`SceneTree <class_SceneTree>`.

    - Dừng xử lý.

        - Ưu điểm: Không có nút nghĩa là không có xử lý, xử lý vật lý hoặc xử lý input. CPU có thể dành để làm việc với nội dung của scene mới.

        - Nhược điểm: Việc xử lý và xử lý input của các nút đó sẽ không còn hoạt động. Đây không phải vấn đề nếu bạn không cần sử dụng dữ liệu đã cập nhật.

2. **Ẩn scene hiện có.** Bằng cách thay đổi khả năng hiển thị hoặc phát hiện va chạm của các nút, bạn có thể ẩn toàn bộ cây con của nút khỏi góc nhìn của người chơi. Dùng
   :ref:`CanvasItem.hide() <class_CanvasItem_method_hide>` để ẩn một scene và
   :ref:`CanvasItem.show() <class_CanvasItem_method_show>` để hiển thị lại scene đó.

    - Bộ nhớ vẫn được giữ lại.

        - Ưu điểm: Bạn vẫn có thể truy cập dữ liệu khi cần.

        - Ưu điểm: Không cần di chuyển thêm bất kỳ nút nào để lưu dữ liệu.

        - Nhược điểm: Nhiều dữ liệu hơn được giữ trong bộ nhớ, điều này sẽ trở thành vấn đề trên các nền tảng nhạy cảm với bộ nhớ như web hoặc mobile.

    - Tiếp tục xử lý.

        - Ưu điểm: Dữ liệu tiếp tục nhận được các bản cập nhật xử lý, vì vậy scene sẽ tiếp tục cập nhật mọi dữ liệu bên trong phụ thuộc vào delta time hoặc dữ liệu frame.

        - Ưu điểm: Các nút vẫn là thành viên của các nhóm (vì các nhóm thuộc về
          :ref:`SceneTree <class_SceneTree>`).

        - Nhược điểm: Sự chú ý của CPU giờ bị chia cho cả hai scene. Tải quá lớn có thể khiến frame rate thấp. Bạn nên kiểm tra hiệu năng trong quá trình phát triển để đảm bảo nền tảng mục tiêu có thể đáp ứng tải từ cách tiếp cận này.

3. **Xóa scene hiện có khỏi tree.** Gán một biến cho nút gốc của scene hiện có. Sau đó dùng
   :ref:`Node.remove_child(Node) <class_Node_method_remove_child>` để tách toàn bộ scene khỏi tree. Để gắn scene lại sau đó, hãy dùng
   :ref:`Node.add_child(Node) <class_Node_method_add_child>`.

    - Bộ nhớ vẫn được giữ lại (các ưu và nhược điểm tương tự như khi ẩn scene khỏi tầm nhìn).

    - Dừng xử lý (các ưu và nhược điểm tương tự như khi xóa hoàn toàn scene).

    - Ưu điểm: Biến thể "ẩn" này dễ hiển thị/ẩn hơn nhiều. Thay vì có thể phải theo dõi nhiều thay đổi đối với scene, bạn chỉ cần gọi các phương thức add/remove_child. Cách này tương tự việc vô hiệu hóa các game object trong những engine khác.

    - Nhược điểm: Không giống như chỉ ẩn scene khỏi tầm nhìn, dữ liệu chứa trong scene sẽ trở nên lỗi thời nếu phụ thuộc vào delta time, input, groups hoặc dữ liệu khác được lấy từ quyền truy cập :ref:`SceneTree <class_SceneTree>`.

Cũng có những trường hợp bạn muốn nhiều scene hiện diện cùng lúc, chẳng hạn như thêm singleton của riêng bạn trong runtime hoặc bảo toàn dữ liệu của một scene giữa các lần thay đổi scene (thêm scene vào nút gốc).

.. tabs::
 .. code-tab:: gdscript GDScript

        get_tree().root.add_child(scene)

 .. code-tab:: csharp

        GetTree().Root.AddChild(scene);

Một trường hợp khác là hiển thị nhiều scene cùng lúc bằng
:ref:`SubViewportContainers <class_SubViewportContainer>`. Cách này tối ưu để render nội dung khác nhau ở các phần khác nhau trên màn hình (ví dụ: minimap, multiplayer chia đôi màn hình).

Mỗi tùy chọn sẽ phù hợp nhất với những trường hợp khác nhau, vì vậy bạn phải xem xét tác động của từng cách tiếp cận và xác định hướng đi phù hợp nhất với tình huống cụ thể của mình.
