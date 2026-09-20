.. _doc_surfacetool:

Sử dụng SurfaceTool
===================

:ref:`SurfaceTool <class_surfacetool>` cung cấp một interface hữu ích để xây dựng hình học. Interface này tương tự như class :ref:`ImmediateMesh <class_ImmediateMesh>`. Bạn thiết lập từng thuộc tính trên mỗi vertex (ví dụ: normal, uv, color), sau đó khi thêm một vertex, các thuộc tính đó sẽ được ghi nhận.

SurfaceTool cũng cung cấp một số helper function hữu ích như ``index()`` và ``generate_normals()``.

Các thuộc tính được thêm trước khi thêm từng vertex:

.. tabs::
 .. code-tab:: gdscript GDScript

    var st = SurfaceTool.new()

    st.begin(Mesh.PRIMITIVE_TRIANGLES)

    st.set_normal() # Bị ghi đè bởi normal bên dưới.
    st.set_normal() # Được thêm vào vertex tiếp theo.
    st.set_color() # Được thêm vào vertex tiếp theo.
    st.add_vertex() # Ghi nhận normal và color ở trên.
    st.set_normal() # Normal không bao giờ được thêm vào vertex.

 .. code-tab:: csharp

    st.SetNormal(); // Bị ghi đè bởi normal bên dưới.
    st.SetNormal(); // Được thêm vào vertex tiếp theo.
    st.SetColor(); // Được thêm vào vertex tiếp theo.
    st.AddVertex(); // Ghi nhận normal và color ở trên.
    st.SetNormal(); // Normal không bao giờ được thêm vào vertex.

Khi hoàn tất việc tạo hình học bằng :ref:`SurfaceTool <class_surfacetool>`, hãy gọi ``commit()`` để hoàn tất việc tạo mesh. Nếu truyền một :ref:`ArrayMesh <class_ArrayMesh>` vào ``commit()``, nó sẽ thêm một surface mới vào cuối ArrayMesh. Còn nếu không truyền gì, ``commit()`` sẽ trả về một ArrayMesh.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thêm surface vào ArrayMesh hiện có.
    st.commit(mesh)

    # -- Hoặc thay thế --

    # Tạo ArrayMesh mới.
    var mesh = st.commit()

 .. code-tab:: csharp

    st.Commit(mesh);
    // Hoặc:
    var mesh = st.Commit();

Đoạn code bên dưới tạo một triangle không có index.

.. tabs::
 .. code-tab:: gdscript GDScript

    var st = SurfaceTool.new()

    st.begin(Mesh.PRIMITIVE_TRIANGLES)

    # Chuẩn bị các thuộc tính cho add_vertex.
    st.set_normal(Vector3(0, 0, 1))
    st.set_uv(Vector2(0, 0))
    # Gọi hàm này sau cùng cho mỗi vertex; hàm sẽ thêm các thuộc tính ở trên.
    st.add_vertex(Vector3(-1, -1, 0))

    st.set_normal(Vector3(0, 0, 1))
    st.set_uv(Vector2(0, 1))
    st.add_vertex(Vector3(-1, 1, 0))

    st.set_normal(Vector3(0, 0, 1))
    st.set_uv(Vector2(1, 1))
    st.add_vertex(Vector3(1, 1, 0))

    # Commit vào một mesh.
    var mesh = st.commit()

 .. code-tab:: csharp

    var st = new SurfaceTool();

    st.Begin(Mesh.PrimitiveType.Triangles);

    // Chuẩn bị các thuộc tính cho AddVertex.
    st.SetNormal(new Vector3(0, 0, 1));
    st.SetUV(new Vector2(0, 0));
    // Gọi hàm này sau cùng cho mỗi vertex; hàm sẽ thêm các thuộc tính ở trên.
    st.AddVertex(new Vector3(-1, -1, 0));

    st.SetNormal(new Vector3(0, 0, 1));
    st.SetUV(new Vector2(0, 1));
    st.AddVertex(new Vector3(-1, 1, 0));

    st.SetNormal(new Vector3(0, 0, 1));
    st.SetUV(new Vector2(1, 1));
    st.AddVertex(new Vector3(1, 1, 0));

    // Commit vào một mesh.
    var mesh = st.Commit();

Bạn có thể tùy chọn thêm một index array, bằng cách gọi ``add_index()`` rồi thêm các vertex vào index array theo cách thủ công, hoặc gọi ``index()`` một lần để tự động tạo index array và thu nhỏ vertex array nhằm loại bỏ các vertex trùng lặp.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Giả sử chúng ta có một quad được định nghĩa bởi 6 vertex như sau
    st.add_vertex(Vector3(-1, 1, 0))
    st.add_vertex(Vector3(1, 1, 0))
    st.add_vertex(Vector3(-1, -1, 0))

    st.add_vertex(Vector3(1, 1, 0))
    st.add_vertex(Vector3(1, -1, 0))
    st.add_vertex(Vector3(-1, -1, 0))

    # Chúng ta có thể làm quad hiệu quả hơn bằng cách sử dụng index array và chỉ dùng 4 vertex:

    st.add_vertex(Vector3(-1, 1, 0))
    st.add_vertex(Vector3(1, 1, 0))
    st.add_vertex(Vector3(-1, -1, 0))
    st.add_vertex(Vector3(1, -1, 0))

    # Tạo một quad từ bốn vertex ở các góc.
    # add_index() có thể được gọi trước hoặc sau add_vertex()
    # vì nó không phải là thuộc tính của chính vertex.
    st.add_index(0)
    st.add_index(1)
    st.add_index(2)

    st.add_index(1)
    st.add_index(3)
    st.add_index(2)

    # Ngoài ra, chúng ta có thể sử dụng ``st.index()``, hàm này sẽ tạo quad cho chúng ta và loại bỏ các vertex trùng lặp
    st.index()

 .. code-tab:: csharp

    // Giả sử chúng ta có một quad được định nghĩa bởi 6 vertex như sau.
    st.AddVertex(new Vector3(-1, 1, 0));
    st.AddVertex(new Vector3(1, 1, 0));
    st.AddVertex(new Vector3(-1, -1, 0));

    st.AddVertex(new Vector3(1, 1, 0));
    st.AddVertex(new Vector3(1, -1, 0));
    st.AddVertex(new Vector3(-1, -1, 0));

    // Chúng ta có thể làm quad hiệu quả hơn bằng cách sử dụng index array và chỉ dùng 4 vertex:
    st.AddVertex(new Vector3(-1, -1, 0));
    st.AddVertex(new Vector3(1, 1, 0));
    st.AddVertex(new Vector3(-1, -1, 0));
    st.AddVertex(new Vector3(1, 1, 0));

    // Tạo một quad từ bốn vertex ở các góc.
    // Không cần gọi AddIndex trước AddVertex.
    st.AddIndex(0);
    st.AddIndex(1);
    st.AddIndex(2);

    st.AddIndex(1);
    st.AddIndex(3);
    st.AddIndex(2);

    // Ngoài ra, chúng ta có thể sử dụng `st.Index()`, hàm này sẽ tạo quad cho chúng ta và loại bỏ các vertex trùng lặp.
    st.Index();

Tương tự, nếu bạn có một index array nhưng muốn mỗi vertex là duy nhất (ví dụ: vì bạn muốn sử dụng normal hoặc color riêng cho từng face thay vì cho từng vertex), bạn có thể gọi ``deindex()``.

.. tabs::
 .. code-tab:: gdscript GDScript

    st.deindex()

 .. code-tab:: csharp

    st.Deindex();

Nếu bạn không tự thêm custom normal, bạn có thể thêm chúng bằng ``generate_normals()``, hàm này nên được gọi sau khi tạo hình học và trước khi commit mesh bằng ``commit()`` hoặc ``commit_to_arrays()``. Việc gọi ``generate_normals(true)`` sẽ lật các normal thu được. Ngoài ra, ``generate_normals()`` chỉ hoạt động nếu primitive type được đặt thành ``Mesh.PRIMITIVE_TRIANGLES``.

Bạn có thể nhận thấy normal mapping hoặc các thuộc tính material khác trông không đúng trên mesh được tạo. Nguyên nhân là normal mapping **yêu cầu** mesh phải có *tangent*, vốn tách biệt với *normal*. Bạn có thể tự thêm custom tangent hoặc tự động tạo chúng bằng ``generate_tangents()``. Phương thức này yêu cầu mỗi vertex đã được thiết lập UV và normal.

.. tabs::
 .. code-tab:: gdscript GDScript

    st.generate_normals()
    st.generate_tangents()

    st.commit(mesh)

 .. code-tab:: csharp

    st.GenerateNormals();
    st.GenerateTangents();

Theo mặc định, khi tạo normal, chúng sẽ được tính trên cơ sở từng vertex (tức là chúng sẽ là "smooth normal"). Nếu bạn muốn flat vertex normal (tức là một vector normal duy nhất cho mỗi face), khi thêm vertex, hãy gọi ``add_smooth_group(i)``, trong đó ``i`` là một số duy nhất cho mỗi vertex. Cần gọi ``add_smooth_group()`` trong khi xây dựng hình học, chẳng hạn trước lệnh gọi ``add_vertex()``.
