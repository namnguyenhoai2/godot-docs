.. _doc_meshdatatool:

Sử dụng MeshDataTool
====================

:ref:`MeshDataTool <class_meshdatatool>` không được dùng để tạo hình học. Tuy nhiên, nó hữu ích khi cần thay đổi hình học một cách linh động, chẳng hạn nếu bạn muốn viết một script để tessellate, đơn giản hóa hoặc biến dạng các mesh.

MeshDataTool không nhanh bằng việc thay đổi trực tiếp các array bằng :ref:`ArrayMesh <class_arraymesh>`. Tuy nhiên, nó cung cấp nhiều thông tin và công cụ để làm việc với mesh hơn ArrayMesh. Khi sử dụng MeshDataTool, công cụ này sẽ tính toán dữ liệu mesh không có trong ArrayMesh, chẳng hạn như các mặt và cạnh, vốn cần thiết cho một số thuật toán mesh. Nếu không cần những thông tin bổ sung này, bạn nên sử dụng ArrayMesh.

.. note:: MeshDataTool chỉ có thể được sử dụng trên các Mesh sử dụng PrimitiveType ``Mesh.PRIMITIVE_TRIANGLES``.

Chúng ta khởi tạo MeshDataTool từ một ArrayMesh bằng cách gọi :ref:`create_from_surface() <class_meshdatatool_method_create_from_surface>`. Nếu MeshDataTool đã có dữ liệu được khởi tạo, việc gọi ``create_from_surface()`` sẽ xóa dữ liệu đó. Ngoài ra, bạn có thể tự gọi :ref:`clear() <class_meshdatatool_method_clear>` trước khi sử dụng lại MeshDataTool.

Trong các ví dụ dưới đây, giả sử một ArrayMesh có tên ``mesh`` đã được tạo. Xem :ref:`ArrayMesh tutorial <doc_arraymesh>` để biết ví dụ về cách tạo mesh.

.. tabs::
 .. code-tab:: gdscript GDScript

    var mdt = MeshDataTool.new()
    mdt.create_from_surface(mesh, 0)

 .. code-tab:: csharp C#

    var mdt = new MeshDataTool();
    mdt.CreateFromSurface(mesh, 0);

``create_from_surface()`` sử dụng các vertex array từ ArrayMesh để tính toán thêm hai array, một cho các cạnh và một cho các mặt, tổng cộng là ba array.

Một cạnh là kết nối giữa hai đỉnh bất kỳ. Mỗi cạnh trong edge array chứa tham chiếu đến hai đỉnh tạo nên nó và tối đa hai mặt mà nó nằm trong đó.

Một mặt là một tam giác gồm ba đỉnh và ba cạnh tương ứng. Mỗi mặt trong face array chứa tham chiếu đến ba đỉnh và ba cạnh tạo nên nó.

Vertex array chứa thông tin về cạnh, mặt, normal, màu, tangent, uv, uv2, bone và weight liên kết với mỗi đỉnh.

Để truy cập thông tin từ các array này, bạn sử dụng một function có dạng ``get_****()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    mdt.get_vertex_count() # Trả về số lượng đỉnh trong vertex array.
    mdt.get_vertex_faces(0) # Trả về một array gồm các mặt chứa vertex[0].
    mdt.get_face_normal(1) # Tính toán và trả về face normal của mặt thứ hai.
    mdt.get_edge_vertex(10, 1) # Trả về đỉnh thứ hai tạo nên cạnh tại index 10.

 .. code-tab:: csharp C#

    mdt.GetVertexCount(); // Trả về số lượng đỉnh trong vertex array.
    mdt.GetVertexFaces(0); // Trả về một array gồm các mặt chứa vertex[0].
    mdt.GetFaceNormal(1); // Tính toán và trả về face normal của mặt thứ hai.
    mdt.GetEdgeVertex(10, 1); // Trả về đỉnh thứ hai tạo nên cạnh tại index 10.

Bạn có thể tùy ý quyết định cách sử dụng các function này. Một trường hợp sử dụng phổ biến là lặp qua tất cả các đỉnh và biến đổi chúng theo một cách nào đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    for i in range(mdt.get_vertex_count()):
        var vert = mdt.get_vertex(i)
        vert *= 2.0 # Scale đỉnh lên gấp đôi kích thước.
        mdt.set_vertex(i, vert)

 .. code-tab:: csharp C#

    for (var i = 0; i < mdt.GetVertexCount(); i++)
    {
        Vector3 vert = mdt.GetVertex(i);
        vert *= 2.0f; // Scale đỉnh lên gấp đôi kích thước.
        mdt.SetVertex(i, vert);
    }

Các thay đổi này không được thực hiện trực tiếp trên ArrayMesh. Nếu đang cập nhật động một ArrayMesh hiện có, trước tiên hãy xóa surface hiện tại rồi thêm một surface mới bằng :ref:`commit_to_surface() <class_meshdatatool_method_commit_to_surface>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    mesh.clear_surfaces() # Xóa tất cả surface của mesh.
    mdt.commit_to_surface(mesh)

 .. code-tab:: csharp C#

    mesh.ClearSurfaces(); // Xóa tất cả surface của mesh.
    mdt.CommitToSurface(mesh);

Dưới đây là một ví dụ hoàn chỉnh biến một mesh hình cầu có tên ``mesh`` thành một khối biến dạng ngẫu nhiên, đồng thời cập nhật normal và màu của các đỉnh. Xem :ref:`ArrayMesh tutorial <doc_arraymesh>` để biết cách tạo mesh cơ sở.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends MeshInstance3D

    var fnl = FastNoiseLite.new()
    var mdt = MeshDataTool.new()

    func _ready():
        fnl.frequency = 0.7

        mdt.create_from_surface(mesh, 0)

        for i in range(mdt.get_vertex_count()):
            var vertex = mdt.get_vertex(i).normalized()
            # Scale các đỉnh bằng noise.
            vertex = vertex * (fnl.get_noise_3dv(vertex) * 0.5 + 0.75)
            mdt.set_vertex(i, vertex)

        # Tính toán normal của các đỉnh, theo từng mặt.
        for i in range(mdt.get_face_count()):
            # Lấy index trong vertex array.
            var a = mdt.get_face_vertex(i, 0)
            var b = mdt.get_face_vertex(i, 1)
            var c = mdt.get_face_vertex(i, 2)
            # Lấy vị trí đỉnh bằng index của đỉnh.
            var ap = mdt.get_vertex(a)
            var bp = mdt.get_vertex(b)
            var cp = mdt.get_vertex(c)
            # Tính toán normal của mặt.
            var n = (bp - cp).cross(ap - bp).normalized()
            # Cộng face normal này vào các normal hiện tại của đỉnh.
            # Kết quả sẽ không có normal hoàn hảo, nhưng sẽ gần đúng.
            mdt.set_vertex_normal(a, n + mdt.get_vertex_normal(a))
            mdt.set_vertex_normal(b, n + mdt.get_vertex_normal(b))
            mdt.set_vertex_normal(c, n + mdt.get_vertex_normal(c))

        # Duyệt qua các đỉnh lần cuối để chuẩn hóa các normal của chúng và
        # đặt màu của các đỉnh thành các normal mới này.
        for i in range(mdt.get_vertex_count()):
            var v = mdt.get_vertex_normal(i).normalized()
            mdt.set_vertex_normal(i, v)
            mdt.set_vertex_color(i, Color(v.x, v.y, v.z))

        mesh.clear_surfaces()
        mdt.commit_to_surface(mesh)

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyMeshInstance3D : MeshInstance3D
    {
        MeshDataTool mdt = new MeshDataTool();
        FastNoiseLite fnl = new FastNoiseLite();

        public override void _Ready()
        {
            fnl.Frequency = 0.7f;

            ArrayMesh mesh = Mesh as ArrayMesh; // Mesh được gán cho MeshInstance3D phải là một ArrayMesh.
            mdt.CreateFromSurface(mesh, 0);

            for (var i = 0; i < mdt.GetVertexCount(); i++)
            {
                Vector3 vertex = mdt.GetVertex(i).Normalized();
                // Scale các đỉnh bằng noise.
                vertex = vertex * (fnl.GetNoise3Dv(vertex) * 0.5f + 0.75f);
                mdt.SetVertex(i, vertex);
            }

            // Tính toán normal của các đỉnh, theo từng mặt.
            for (var i = 0; i < mdt.GetFaceCount(); i++)
            {
                // Lấy index trong vertex array.
                var a = mdt.GetFaceVertex(i, 0);
                var b = mdt.GetFaceVertex(i, 1);
                var c = mdt.GetFaceVertex(i, 2);
                // Lấy vị trí đỉnh bằng index của đỉnh.
                var ap = mdt.GetVertex(a);
                var bp = mdt.GetVertex(b);
                var cp = mdt.GetVertex(c);
                // Tính toán normal của mặt.
                var n = (bp - cp).Cross(ap - bp).Normalized();
                // Cộng face normal này vào các normal hiện tại của đỉnh.
                // Kết quả sẽ không có normal hoàn hảo, nhưng sẽ gần đúng.
                mdt.SetVertexNormal(a, n + mdt.GetVertexNormal(a));
                mdt.SetVertexNormal(b, n + mdt.GetVertexNormal(b));
                mdt.SetVertexNormal(c, n + mdt.GetVertexNormal(c));
            }

            // Duyệt qua các đỉnh lần cuối để chuẩn hóa các normal của chúng và
            // đặt màu của các đỉnh thành các normal mới này.
            for (var i = 0; i < mdt.GetVertexCount(); i++)
            {
                var v = mdt.GetVertexNormal(i).Normalized();
                mdt.SetVertexNormal(i, v);
                mdt.SetVertexColor(i, new Color(v.X, v.Y, v.Z));
            }

            mesh.ClearSurfaces();
            mdt.CommitToSurface(mesh);
        }
    }
