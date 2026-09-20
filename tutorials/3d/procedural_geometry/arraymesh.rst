.. _doc_arraymesh:

Sử dụng ArrayMesh
=================

Hướng dẫn này sẽ trình bày những kiến thức cơ bản về cách sử dụng :ref:`ArrayMesh <class_arraymesh>`.

Để thực hiện việc này, chúng ta sẽ sử dụng hàm :ref:`add_surface_from_arrays() <class_ArrayMesh_method_add_surface_from_arrays>`, hàm này nhận tối đa năm tham số. Hai tham số đầu tiên là bắt buộc, còn ba tham số cuối là tùy chọn.

Tham số đầu tiên là ``PrimitiveType``, một khái niệm của OpenGL dùng để chỉ dẫn cho GPU cách sắp xếp primitive dựa trên các vertex được cung cấp, tức là chúng biểu diễn triangle, line, point, v.v. Xem :ref:`Mesh.PrimitiveType <enum_Mesh_PrimitiveType>` để biết các tùy chọn hiện có.

Tham số thứ hai, ``arrays``, là Array thực tế lưu trữ thông tin mesh. Array này là một Godot array thông thường được tạo bằng cặp ngoặc vuông rỗng ``[]``. Nó lưu một ``Packed**Array`` (ví dụ: PackedVector3Array, PackedInt32Array, v.v.) cho mỗi loại thông tin sẽ được sử dụng để xây dựng surface.

Các phần tử phổ biến của ``arrays`` được liệt kê bên dưới, cùng với vị trí mà chúng phải có trong ``arrays``. Xem :ref:`Mesh.ArrayType <enum_Mesh_ArrayType>` để biết danh sách đầy đủ.


.. list-table::
    :class: wrap-normal
    :width: 100%
    :widths: auto
    :header-rows: 1

    * - Index
      - Enum Mesh.ArrayType
      - Loại Array

    * - 0
      - ``ARRAY_VERTEX``
      - :ref:`PackedVector3Array <class_PackedVector3Array>` hoặc :ref:`PackedVector2Array <class_PackedVector2Array>`

    * - 1
      - ``ARRAY_NORMAL``
      - :ref:`PackedVector3Array <class_PackedVector3Array>`

    * - 2
      - ``ARRAY_TANGENT``
      - :ref:`PackedFloat32Array <class_PackedFloat32Array>` hoặc :ref:`PackedFloat64Array <class_PackedFloat64Array>` gồm các nhóm 4 float. 3 float đầu tiên xác định tangent, còn float cuối xác định hướng binormal
        theo giá trị -1 hoặc 1.

    * - 3
      - ``ARRAY_COLOR``
      - :ref:`PackedColorArray <class_PackedColorArray>`

    * - 4
      - ``ARRAY_TEX_UV``
      - :ref:`PackedVector2Array <class_PackedVector2Array>` hoặc :ref:`PackedVector3Array <class_PackedVector3Array>`

    * - 5
      - ``ARRAY_TEX_UV2``
      - :ref:`PackedVector2Array <class_PackedVector2Array>` hoặc :ref:`PackedVector3Array <class_PackedVector3Array>`

    * - 10
      - ``ARRAY_BONES``
      - :ref:`PackedFloat32Array <class_PackedFloat32Array>` gồm các nhóm 4 float hoặc :ref:`PackedInt32Array <class_PackedInt32Array>` gồm các nhóm 4 int. Mỗi nhóm liệt kê index của 4 bone ảnh hưởng đến một vertex nhất định.

    * - 11
      - ``ARRAY_WEIGHTS``
      - :ref:`PackedFloat32Array <class_PackedFloat32Array>` hoặc :ref:`PackedFloat64Array <class_PackedFloat64Array>` gồm các nhóm 4 float. Mỗi float liệt kê mức độ ảnh hưởng của bone tương ứng trong ``ARRAY_BONES`` lên một vertex nhất định.

    * - 12
      - ``ARRAY_INDEX``
      - :ref:`PackedInt32Array <class_PackedInt32Array>`

Trong hầu hết trường hợp khi tạo mesh, chúng ta xác định mesh bằng vị trí các vertex. Vì vậy, array vertex (ở index 0) thường là bắt buộc, còn array index (ở index 12) là tùy chọn và chỉ được sử dụng nếu được đưa vào. Cũng có thể tạo mesh chỉ với array index mà không có array vertex, nhưng nội dung đó nằm ngoài phạm vi của hướng dẫn này.

Tất cả các array khác chứa thông tin về vertex. Chúng là tùy chọn và chỉ được sử dụng nếu được đưa vào. Một số array trong đó (ví dụ: ``ARRAY_COLOR``) sử dụng một phần tử cho mỗi vertex để cung cấp thêm thông tin về vertex. Chúng phải có cùng kích thước với array vertex. Các array khác (ví dụ: ``ARRAY_TANGENT``) sử dụng bốn phần tử để mô tả một vertex. Các array này phải lớn hơn array vertex chính xác bốn lần.

Trong cách sử dụng thông thường, ba tham số cuối trong :ref:`add_surface_from_arrays() <class_arraymesh_method_add_surface_from_arrays>` thường được để trống.

Thiết lập ArrayMesh
-------------------

Trong editor, tạo một :ref:`MeshInstance3D <class_meshinstance3d>` rồi thêm một :ref:`ArrayMesh <class_arraymesh>` vào đó trong Inspector. Thông thường, việc thêm ArrayMesh trong editor không hữu ích, nhưng trong trường hợp này, nó cho phép chúng ta truy cập ArrayMesh từ code mà không cần tạo một ArrayMesh mới.

Tiếp theo, thêm một script vào MeshInstance3D.

Bên dưới ``_ready()``, tạo một Array mới.

.. tabs::
  .. code-tab:: gdscript GDScript

    var surface_array = []

  .. code-tab:: csharp C#

    Godot.Collections.Array surfaceArray = [];

Đây sẽ là array dùng để lưu thông tin surface — nó sẽ chứa tất cả các array dữ liệu mà surface cần. Godot sẽ yêu cầu array này có kích thước ``Mesh.ARRAY_MAX``, vì vậy hãy thay đổi kích thước cho phù hợp.

.. tabs::
 .. code-tab:: gdscript GDScript

    var surface_array = []
    surface_array.resize(Mesh.ARRAY_MAX)

 .. code-tab:: csharp C#

    Godot.Collections.Array surfaceArray = [];
    surfaceArray.Resize((int)Mesh.ArrayType.Max);

Tiếp theo, tạo các array cho từng loại dữ liệu mà bạn sẽ sử dụng.

.. tabs::
 .. code-tab:: gdscript GDScript

    var verts = PackedVector3Array()
    var uvs = PackedVector2Array()
    var normals = PackedVector3Array()
    var indices = PackedInt32Array()

 .. code-tab:: csharp C#

    List<Vector3> verts = [];
    List<Vector2> uvs = [];
    List<Vector3> normals = [];
    List<int> indices = [];

Sau khi điền geometry vào các array dữ liệu, bạn có thể tạo mesh bằng cách thêm từng array vào ``surface_array``, sau đó commit vào mesh.

.. tabs::
 .. code-tab:: gdscript GDScript

    surface_array[Mesh.ARRAY_VERTEX] = verts
    surface_array[Mesh.ARRAY_TEX_UV] = uvs
    surface_array[Mesh.ARRAY_NORMAL] = normals
    surface_array[Mesh.ARRAY_INDEX] = indices

    # Không sử dụng blendshape, lod hoặc compression.
    mesh.add_surface_from_arrays(Mesh.PRIMITIVE_TRIANGLES, surface_array)

 .. code-tab:: csharp C#

    surfaceArray[(int)Mesh.ArrayType.Vertex] = verts.ToArray();
    surfaceArray[(int)Mesh.ArrayType.TexUV] = uvs.ToArray();
    surfaceArray[(int)Mesh.ArrayType.Normal] = normals.ToArray();
    surfaceArray[(int)Mesh.ArrayType.Index] = indices.ToArray();

    var arrMesh = Mesh as ArrayMesh;
    if (arrMesh != null)
    {
        // Không sử dụng blendshape, lod hoặc compression.
        arrMesh.AddSurfaceFromArrays(Mesh.PrimitiveType.Triangles, surfaceArray);
    }

.. note:: In this example, we used ``Mesh.PRIMITIVE_TRIANGLES``, but you can use any primitive type
          có sẵn từ mesh.

Gộp lại, toàn bộ code sẽ như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends MeshInstance3D

    func _ready():
        var surface_array = []
        surface_array.resize(Mesh.ARRAY_MAX)

        # PackedVector**Arrays để xây dựng mesh.
        var verts = PackedVector3Array()
        var uvs = PackedVector2Array()
        var normals = PackedVector3Array()
        var indices = PackedInt32Array()

        #######################################
        ## Chèn code ở đây để tạo mesh ##
        #######################################

        # Gán các array vào surface array.
        surface_array[Mesh.ARRAY_VERTEX] = verts
        surface_array[Mesh.ARRAY_TEX_UV] = uvs
        surface_array[Mesh.ARRAY_NORMAL] = normals
        surface_array[Mesh.ARRAY_INDEX] = indices

        # Tạo mesh surface từ mesh array.
        # Không sử dụng blendshape, lod hoặc compression.
        mesh.add_surface_from_arrays(Mesh.PRIMITIVE_TRIANGLES, surface_array)

 .. code-tab:: csharp C#

    public partial class MyMeshInstance3D : MeshInstance3D
    {
        public override void _Ready()
        {
            Godot.Collections.Array surfaceArray = [];
            surfaceArray.Resize((int)Mesh.ArrayType.Max);

            // C# array không thể được resize hoặc mở rộng, vì vậy hãy sử dụng List để tạo geometry.
            List<Vector3> verts = [];
            List<Vector2> uvs = [];
            List<Vector3> normals = [];
            List<int> indices = [];

            /***********************************
            * Chèn code ở đây để tạo mesh.
            * *********************************/

            // Chuyển List thành array và gán vào surface array
            surfaceArray[(int)Mesh.ArrayType.Vertex] = verts.ToArray();
            surfaceArray[(int)Mesh.ArrayType.TexUV] = uvs.ToArray();
            surfaceArray[(int)Mesh.ArrayType.Normal] = normals.ToArray();
            surfaceArray[(int)Mesh.ArrayType.Index] = indices.ToArray();

            var arrMesh = Mesh as ArrayMesh;
            if (arrMesh != null)
            {
                // Tạo mesh surface từ mesh array
                // Không sử dụng blendshape, lod hoặc compression.
                arrMesh.AddSurfaceFromArrays(Mesh.PrimitiveType.Triangles, surfaceArray);
            }
        }
    }


Phần code ở giữa có thể là bất cứ thứ gì bạn muốn. Bên dưới, chúng ta sẽ trình bày một số code mẫu để tạo hình dạng, bắt đầu với một hình chữ nhật.

Tạo hình chữ nhật
-----------------

Vì chúng ta sử dụng ``Mesh.PRIMITIVE_TRIANGLES`` để render, chúng ta sẽ tạo một hình chữ nhật bằng các triangle.

Một hình chữ nhật được tạo thành từ hai triangle dùng chung bốn vertex. Trong ví dụ này, chúng ta sẽ tạo một hình chữ nhật có điểm trên cùng bên trái tại ``(0, 0, 0)``, với chiều rộng và chiều dài đều bằng một, như minh họa bên dưới:

.. image:: img/array_mesh_rectangle_as_triangles.webp
  :scale: 33%
  :alt: A rectangle made of two triangles sharing four vertices.

Để vẽ hình chữ nhật này, hãy xác định tọa độ của từng vertex trong array ``verts``.

.. tabs::
  .. code-tab:: gdscript GDScript

    verts = PackedVector3Array([
            Vector3(0, 0, 0),
            Vector3(0, 0, 1),
            Vector3(1, 0, 0),
            Vector3(1, 0, 1),
        ])

  .. code-tab:: csharp C#

    verts.AddRange(new Vector3[]
    {
        new Vector3(0, 0, 0),
        new Vector3(0, 0, 1),
        new Vector3(1, 0, 0),
        new Vector3(1, 0, 1),
    });

Array ``uvs`` giúp mô tả vị trí các phần của texture trên mesh. Các giá trị nằm trong khoảng từ 0 đến 1. Tùy thuộc vào texture, bạn có thể muốn thay đổi các giá trị này.

.. tabs::
  .. code-tab:: gdscript GDScript

    uvs = PackedVector2Array([
            Vector2(0, 0),
            Vector2(1, 0),
            Vector2(0, 1),
            Vector2(1, 1),
        ])

  .. code-tab:: csharp C#

    uvs.AddRange(new Vector2[]
    {
        new Vector2(0, 0),
        new Vector2(1, 0),
        new Vector2(0, 1),
        new Vector2(1, 1),
    });

Array ``normals`` được dùng để mô tả hướng mà các vertex quay về và được sử dụng trong các phép tính lighting. Trong ví dụ này, chúng ta sẽ mặc định sử dụng hướng ``Vector3.UP``.

.. tabs::
  .. code-tab:: gdscript GDScript

    normals = PackedVector3Array([
            Vector3.UP,
            Vector3.UP,
            Vector3.UP,
            Vector3.UP,
        ])

  .. code-tab:: csharp C#

    normals.AddRange(new Vector3[]
    {
        Vector3.Up,
        Vector3.Up,
        Vector3.Up,
        Vector3.Up,
    });

Array ``indices`` xác định thứ tự các vertex được vẽ. Godot render theo hướng *clockwise*, nghĩa là chúng ta phải chỉ định các vertex của một triangle muốn vẽ theo thứ tự clockwise.

Ví dụ, để vẽ triangle đầu tiên, chúng ta sẽ muốn vẽ các vertex ``(0, 0, 0)``, ``(1, 0, 0)`` và ``(0, 0, 1)`` theo thứ tự đó. Điều này tương đương với việc vẽ ``vert[0]``, ``vert[2]`` và ``vert[1]``, tức là các index 0, 2 và 1, trong array ``verts``. Các giá trị index này được xác định bởi array ``indices``.

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Index
     - ``verts[Index]``
     - ``uvs[Index]``
     - ``normals[Index]``

   * - 0
     - (0, 0, 0)
     - (0, 0)
     - Vector3.UP

   * - 1
     - (0, 0, 1)
     - (1, 0)
     - Vector3.UP

   * - 2
     - (1, 0, 0)
     - (0, 1)
     - Vector3.UP

   * - 3
     - (1, 0, 1)
     - (1, 1)
     - Vector3.UP

.. tabs::
  .. code-tab:: gdscript GDScript

    indices = PackedInt32Array([
            0, 2, 1, # Vẽ triangle đầu tiên.
            2, 3, 1, # Vẽ triangle thứ hai.
        ])

  .. code-tab:: csharp C#

    indices.AddRange(new int[]
    {
        0, 2, 1, // Vẽ triangle đầu tiên.
        2, 3, 1, // Vẽ triangle thứ hai.
    });

Gộp lại, code tạo hình chữ nhật sẽ như sau:

.. tabs::
  .. code-tab:: gdscript GDScript

    extends MeshInstance3D

    func _ready():

      # Chèn phần thiết lập PackedVector**Arrays ở đây.

      verts = PackedVector3Array([
              Vector3(0, 0, 0),
              Vector3(0, 0, 1),
              Vector3(1, 0, 0),
              Vector3(1, 0, 1),
          ])

      uvs = PackedVector2Array([
              Vector2(0, 0),
              Vector2(1, 0),
              Vector2(0, 1),
              Vector2(1, 1),
          ])

      normals = PackedVector3Array([
              Vector3.UP,
              Vector3.UP,
              Vector3.UP,
              Vector3.UP,
          ])

      indices = PackedInt32Array([
              0, 2, 1,
              2, 3, 1,
          ])

      # Chèn phần commit vào ArrayMesh ở đây.

  .. code-tab:: csharp C#

    using System.Collections.Generic;

    public partial class MeshInstance3d : MeshInstance3D
    {
      public override void _Ready()
      {
          // Chèn phần thiết lập surface array và List ở đây.

          verts.AddRange(new Vector3[]
          {
              new Vector3(0, 0, 0),
              new Vector3(0, 0, 1),
              new Vector3(1, 0, 0),
              new Vector3(1, 0, 1),
          });

          uvs.AddRange(new Vector2[]
          {
              new Vector2(0, 0),
              new Vector2(1, 0),
              new Vector2(0, 1),
              new Vector2(1, 1),
          });

          normals.AddRange(new Vector3[]
          {
              Vector3.Up,
              Vector3.Up,
              Vector3.Up,
              Vector3.Up,
          });

          indices.AddRange(new int[]
          {
              0, 2, 1,
              2, 3, 1,
          });

          // Chèn phần commit vào ArrayMesh ở đây.
      }
    }

Để xem một ví dụ phức tạp hơn, hãy xem phần tạo sphere bên dưới.

Tạo sphere
----------

Dưới đây là code mẫu để tạo sphere. Mặc dù code được trình bày bằng GDScript, cách tiếp cận để tạo sphere không có gì đặc thù của Godot. Cách triển khai này không liên quan cụ thể đến ArrayMesh mà chỉ là một cách tiếp cận tổng quát để tạo sphere. Nếu bạn gặp khó khăn khi hiểu code hoặc muốn tìm hiểu thêm về procedural geometry nói chung, bạn có thể sử dụng bất kỳ hướng dẫn nào tìm được trên mạng.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends MeshInstance3D

    var rings = 50
    var radial_segments = 50
    var radius = 1

    func _ready():

        # Chèn phần thiết lập PackedVector**Arrays ở đây.

        # Index của vertex.
        var thisrow = 0
        var prevrow = 0
        var point = 0

        # Lặp qua các ring.
        for i in range(rings + 1):
            var v = float(i) / rings
            var w = sin(PI * v)
            var y = cos(PI * v)

            # Lặp qua các segment trong ring.
            for j in range(radial_segments + 1):
                var u = float(j) / radial_segments
                var x = sin(u * PI * 2.0)
                var z = cos(u * PI * 2.0)
                var vert = Vector3(x * radius * w, y * radius, z * radius * w)
                verts.append(vert)
                normals.append(vert.normalized())
                uvs.append(Vector2(u, v))
                point += 1

                # Tạo các triangle trong ring bằng index.
                if i > 0 and j > 0:
                    indices.append(prevrow + j - 1)
                    indices.append(prevrow + j)
                    indices.append(thisrow + j - 1)

                    indices.append(prevrow + j)
                    indices.append(thisrow + j)
                    indices.append(thisrow + j - 1)

            prevrow = thisrow
            thisrow = point

      # Chèn phần commit vào ArrayMesh ở đây.

 .. code-tab:: csharp C#

    public partial class MyMeshInstance3D : MeshInstance3D
    {
        private int _rings = 50;
        private int _radialSegments = 50;
        private float _radius = 1;

        public override void _Ready()
        {
            // Chèn phần thiết lập surface array và List ở đây.

            // Index của vertex.
            var thisRow = 0;
            var prevRow = 0;
            var point = 0;

            // Lặp qua các ring.
            for (var i = 0; i < _rings + 1; i++)
            {
                var v = ((float)i) / _rings;
                var w = Mathf.Sin(Mathf.Pi * v);
                var y = Mathf.Cos(Mathf.Pi * v);

                // Lặp qua các segment trong ring.
                for (var j = 0; j < _radialSegments + 1; j++)
                {
                    var u = ((float)j) / _radialSegments;
                    var x = Mathf.Sin(u * Mathf.Pi * 2);
                    var z = Mathf.Cos(u * Mathf.Pi * 2);
                    var vert = new Vector3(x * _radius * w, y * _radius, z * _radius * w);
                    verts.Add(vert);
                    normals.Add(vert.Normalized());
                    uvs.Add(new Vector2(u, v));
                    point += 1;

                    // Tạo các triangle trong ring bằng index.
                    if (i > 0 && j > 0)
                    {
                        indices.Add(prevRow + j - 1);
                        indices.Add(prevRow + j);
                        indices.Add(thisRow + j - 1);

                        indices.Add(prevRow + j);
                        indices.Add(thisRow + j);
                        indices.Add(thisRow + j - 1);
                    }
                }

                prevRow = thisRow;
                thisRow = point;
            }

            // Chèn phần commit vào ArrayMesh ở đây.
        }
    }

Lưu
---

Cuối cùng, chúng ta có thể sử dụng class :ref:`ResourceSaver <class_resourcesaver>` để lưu ArrayMesh. Điều này hữu ích khi bạn muốn tạo một mesh rồi sử dụng nó sau đó mà không phải tạo lại.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Lưu mesh vào file .tres với compression được bật.
    ResourceSaver.save(mesh, "res://sphere.tres", ResourceSaver.FLAG_COMPRESS)

 .. code-tab:: csharp C#

    // Lưu mesh vào file .tres với compression được bật.
    ResourceSaver.Save(Mesh, "res://sphere.tres", ResourceSaver.SaverFlags.Compress);
