:article_outdated: True

.. _doc_using_multimesh:

Tối ưu hóa bằng MultiMesh
=========================

Đối với một số lượng lớn instances (lên đến hàng nghìn) cần được xử lý liên tục (và vẫn cần duy trì một mức độ kiểm soát nhất định),
:ref:`using servers directly <doc_using_servers>` is the recommended optimization.

Khi số lượng đối tượng lên đến hàng trăm nghìn hoặc hàng triệu, không cách tiếp cận nào trong số này còn hiệu quả nữa. Tuy nhiên, tùy thuộc vào yêu cầu, vẫn còn một khả năng tối ưu hóa khác.

MultiMesh
---------

Một :ref:`MultiMesh<class_MultiMesh>` là một primitive vẽ duy nhất có thể vẽ đến hàng triệu đối tượng trong một lần. Nó cực kỳ hiệu quả vì sử dụng phần cứng GPU để thực hiện việc này.

Nhược điểm duy nhất là không thể thực hiện *screen* culling hoặc *frustum* culling cho từng instance riêng lẻ. Điều này có nghĩa là hàng triệu đối tượng sẽ *luôn được* hoặc *không bao giờ được* vẽ, tùy thuộc vào khả năng hiển thị của toàn bộ MultiMesh. Có thể cung cấp một visibility rect tùy chỉnh cho chúng, nhưng khả năng hiển thị sẽ luôn là kiểu *tất cả hoặc không có gì*.

Nếu các đối tượng đủ đơn giản (chỉ có vài vertex), điều này nhìn chung không gây nhiều vấn đề, vì hầu hết GPU hiện đại đều được tối ưu cho trường hợp sử dụng này. Một cách khắc phục là tạo nhiều MultiMesh cho các khu vực khác nhau trong thế giới.

Cũng có thể thực thi một số logic bên trong vertex shader (sử dụng các hằng số dựng sẵn ``INSTANCE_ID`` hoặc ``INSTANCE_CUSTOM``). Để xem ví dụ về việc tạo animation cho hàng nghìn đối tượng trong một MultiMesh, hãy xem tutorial :ref:`Animating thousands of fish <doc_animating_thousands_of_fish>`. Có thể cung cấp thông tin cho shader thông qua texture (có các format :ref:`Image<class_Image>` dấu phẩy động lý tưởng cho việc này).

Một lựa chọn khác là sử dụng GDExtension và C++, cách này sẽ cực kỳ hiệu quả (có thể thiết lập toàn bộ state cho tất cả đối tượng bằng bộ nhớ tuyến tính thông qua
:ref:`RenderingServer.multimesh_set_buffer() <class_RenderingServer_method_multimesh_set_buffer>`
function). Theo cách này, có thể tạo array bằng nhiều thread, sau đó thiết lập nó trong một lần gọi, mang lại hiệu suất cache cao.

Cuối cùng, không bắt buộc phải hiển thị tất cả các instance của MultiMesh. Có thể kiểm soát số lượng instance hiển thị bằng property :ref:`MultiMesh.visible_instance_count <class_MultiMesh_property_visible_instance_count>`. Quy trình thông thường là cấp phát số lượng instance tối đa sẽ được sử dụng, sau đó thay đổi số lượng hiển thị tùy thuộc vào số lượng hiện đang cần.

Ví dụ về MultiMesh
------------------

Sau đây là ví dụ về cách sử dụng MultiMesh từ code. Các ngôn ngữ khác ngoài GDScript có thể hiệu quả hơn khi xử lý hàng triệu đối tượng, nhưng với vài nghìn đối tượng thì GDScript là đủ.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends MultiMeshInstance3D


    func _ready():
        # Tạo multimesh.
        multimesh = MultiMesh.new()
        # Trước tiên, thiết lập format.
        multimesh.transform_format = MultiMesh.TRANSFORM_3D
        # Thiết lập mesh sẽ được nhân bản.
        multimesh.mesh = BoxMesh.new()
        # Sau đó thay đổi kích thước (nếu không, không được phép thay đổi format).
        multimesh.instance_count = 10000
        # Có thể ban đầu không nên hiển thị tất cả chúng.
        multimesh.visible_instance_count = 1000

        # Thiết lập transform của các instance.
        for i in multimesh.visible_instance_count:
            multimesh.set_instance_transform(i, Transform3D(Basis(), Vector3(i * 20, 0, 0)))

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyMultiMeshInstance3D : MultiMeshInstance3D
    {
        public override void _Ready()
        {
            // Tạo multimesh.
            Multimesh = new MultiMesh();
            // Trước tiên, thiết lập format.
            Multimesh.TransformFormat = MultiMesh.TransformFormatEnum.Transform3D;
            // Sau đó thay đổi kích thước (nếu không, không được phép thay đổi format)
            Multimesh.InstanceCount = 1000;
            // Có thể ban đầu không nên hiển thị tất cả chúng.
            Multimesh.VisibleInstanceCount = 1000;

            // Thiết lập transform của các instance.
            for (int i = 0; i < Multimesh.VisibleInstanceCount; i++)
            {
                Multimesh.SetInstanceTransform(i, new Transform3D(Basis.Identity, new Vector3(i * 20, 0, 0)));
            }
        }
    }
