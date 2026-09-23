.. _doc_importing_3d_scenes_import_configuration:

Cấu hình import
===============

Godot cung cấp một số cách để tùy chỉnh dữ liệu đã import, chẳng hạn như dock import, hộp thoại cài đặt import nâng cao và các scene kế thừa. Bạn có thể sử dụng những cách này để thực hiện thêm các thay đổi đối với scene đã import, chẳng hạn như điều chỉnh mesh, thêm thông tin vật lý và thêm node mới. Bạn cũng có thể viết một script chạy code ở cuối quá trình import để thực hiện các tùy chỉnh bất kỳ.

Lưu ý rằng khi có thể, bạn nên ưu tiên sửa đổi dữ liệu gốc thay vì cấu hình scene sau khi import. Điều này giúp giảm thiểu khác biệt giữa ứng dụng modeling 3D và scene đã import. Xem
:ref:`doc_importing_3d_scenes_model_export_considerations` và
:ref:`doc_importing_3d_scenes_node_type_customization` để biết thêm thông tin.

Quy trình import
----------------

Vì Godot chỉ có thể lưu định dạng scene riêng của mình (``.tscn``/``.scn``), Godot không thể ghi đè lên tệp scene 3D gốc (sử dụng một định dạng khác). Đây cũng là cách an toàn hơn vì tránh việc vô tình thay đổi tệp nguồn.

Để cho phép tùy chỉnh scene và material, scene importer của Godot hỗ trợ các quy trình khác nhau liên quan đến cách import dữ liệu.

.. figure:: img/importing_3d_scenes_import_dock.webp
   :align: center
   :alt: Dock import sau khi chọn một scene 3D trong dock FileSystem

   Dock import sau khi chọn một scene 3D trong dock FileSystem

Quy trình import này có thể được tùy chỉnh bằng 3 giao diện riêng biệt, tùy theo nhu cầu của bạn:

- Dock **Import**, sau khi chọn scene 3D bằng cách nhấp một lần vào scene đó trong dock FileSystem.
- Hộp thoại **Advanced Import Settings**, có thể truy cập bằng cách nhấp đúp vào scene 3D trong dock FileSystem hoặc nhấp vào nút **Advanced…** trong dock Import. Hộp thoại này cho phép bạn tùy chỉnh các tùy chọn theo từng object trong Godot, đồng thời xem trước model và animation. Vui lòng xem trang :ref:`doc_advanced_import_settings` để biết thêm thông tin.
- :ref:`Import hints <doc_importing_3d_scenes_node_type_customization>`, là các hậu tố đặc biệt được thêm vào tên object trong ứng dụng modeling 3D. Điều này cho phép bạn tùy chỉnh các tùy chọn theo từng object trong ứng dụng modeling 3D.

Đối với việc tùy chỉnh cơ bản, sử dụng dock Import là đủ. Tuy nhiên, đối với các thao tác phức tạp hơn, chẳng hạn như xác định material override theo từng material, bạn sẽ cần sử dụng hộp thoại Advanced Import Settings, import hints hoặc có thể là cả hai.

.. _doc_importing_3d_scenes_using_the_import_dock:

Sử dụng dock Import
~~~~~~~~~~~~~~~~~~~

Bạn có thể điều chỉnh các tùy chọn sau trong dock Import sau khi chọn một scene 3D trong dock FileSystem:

- **Root Type:** Loại node được sử dụng làm node gốc. Bạn nên sử dụng các loại node kế thừa từ Node3D. Nếu không, bạn sẽ mất khả năng định vị node trực tiếp trong trình chỉnh sửa 3D.
- **Root Name:** Tên của node gốc trong scene đã import. Điều này thường không dễ nhận thấy khi tạo instance của scene trong trình chỉnh sửa (hoặc kéo và thả từ dock FileSystem), vì trong trường hợp này node gốc được đổi tên để khớp với tên tệp.
- **Apply Root Scale:** Nếu được bật, **Root Scale** sẽ được *áp dụng* trực tiếp lên mesh và animation, đồng thời giữ scale của node gốc ở giá trị mặc định `(1, 1, 1)`. Điều này có nghĩa là nếu sau đó bạn thêm một node con vào scene đã import, node đó sẽ không được scale. Nếu bị tắt, **Root Scale** sẽ nhân với scale của node gốc.

**Mesh**

- **Ensure Tangents:** Nếu được chọn, tạo tangent cho vertex bằng `Mikktspace <http://www.mikktspace.com/>`__ nếu mesh đầu vào không có dữ liệu tangent. Khi có thể, bạn nên để ứng dụng modeling 3D tạo tangent khi export thay vì dựa vào tùy chọn này. Tangent là yêu cầu cần thiết để hiển thị chính xác normal map và height map, cùng với mọi tính năng material/shader yêu cầu tangent. Nếu bạn không cần các tính năng material yêu cầu tangent, việc tắt tùy chọn này có thể giảm kích thước tệp đầu ra và tăng tốc quá trình import nếu tệp 3D nguồn không chứa tangent.
- **Generate LODs:** Nếu được chọn, tạo các biến thể mesh có mức độ chi tiết thấp hơn để hiển thị ở khoảng cách xa nhằm cải thiện hiệu năng render. Không phải mesh nào cũng hưởng lợi từ LOD, đặc biệt nếu chúng không bao giờ được render từ xa. Việc tắt tùy chọn này có thể giảm kích thước tệp đầu ra và tăng tốc quá trình import. Xem :ref:`doc_mesh_lod` để biết thêm thông tin.
- **Create Shadow Meshes:** Nếu được chọn, bật việc tạo shadow mesh khi import. Tùy chọn này tối ưu hóa việc render bóng mà không làm giảm chất lượng bằng cách nối các vertex với nhau khi có thể. Nhờ đó, băng thông bộ nhớ cần thiết để render bóng cũng giảm xuống. Hiện tại, việc tạo shadow mesh không hỗ trợ sử dụng mức độ chi tiết thấp hơn mesh nguồn (nhưng việc render bóng sẽ sử dụng LOD khi phù hợp).
- **Light Baking:** Cấu hình
  :ref:`chế độ global illumination <class_GeometryInstance3D_property_gi_mode>` của mesh trong scene 3D. Nếu được đặt thành **Static Lightmaps**, đặt chế độ GI của mesh thành **Static** và tạo UV2 khi import để :ref:`bake lightmap <doc_using_lightmap_gi>`.
- **Lightmap Texel Size:** Chỉ hiển thị khi **Light Baking** được đặt thành **Static Lightmaps**. Kiểm soát kích thước của mỗi texel trên lightmap đã bake. Giá trị nhỏ hơn tạo ra lightmap chính xác hơn, đổi lại là kích thước lightmap lớn hơn và thời gian bake lâu hơn.

**Skin**

- **Use Named Skins:** Nếu được chọn, sử dụng :ref:`Skins <class_Skin>` có tên để animation. Node :ref:`class_MeshInstance3D` chứa 3 thuộc tính liên quan ở đây: một Skeleton NodePath trỏ đến node Skeleton3D (thường là ``..``), một mesh và một skin:

  - Node :ref:`class_Skeleton3D` chứa danh sách bone cùng tên, pose và rest của chúng, một tên và một bone cha.
  - Mesh chứa toàn bộ dữ liệu vertex thô cần thiết để hiển thị mesh. Xét về mesh, nó biết các vertex được weight-paint như thế nào và sử dụng một số đánh số nội bộ thường được import từ ứng dụng modeling 3D.
  - Skin chứa thông tin cần thiết để liên kết mesh này với Skeleton3D. Với mỗi ID bone nội bộ do ứng dụng modeling 3D lựa chọn, nó chứa hai thành phần. Thứ nhất là một Matrix được gọi là Bind Pose Matrix, Inverse Bind Matrix hoặc viết tắt là IBM. Thứ hai, Skin chứa tên của từng bone (nếu **Use Named Skins** được bật) hoặc chỉ mục của bone trong danh sách Skeleton3D (nếu **Use Named Skins** bị tắt).

Kết hợp lại, những thông tin này đủ để cho Godot biết cách sử dụng các pose của bone trong node Skeleton3D để render mesh từ mỗi MeshInstance3D. Lưu ý rằng mỗi MeshInstance3D có thể dùng chung các bind, như thường thấy trong model được export từ Blender, hoặc mỗi MeshInstance3D có thể sử dụng một đối tượng Skin riêng, như thường thấy trong model được export từ các công cụ khác như Maya.


**Animation**

- **Import:** Nếu được chọn, import animation từ scene 3D.
- **FPS:** Số khung hình mỗi giây được sử dụng để chuyển các đường cong animation thành một chuỗi điểm bằng phép nội suy tuyến tính. Bạn nên cấu hình giá trị này khớp với giá trị đang được sử dụng làm cơ sở trong phần mềm tạo mô hình 3D. Giá trị cao hơn tạo ra animation chính xác hơn khi chuyển động thay đổi nhanh, nhưng làm tăng kích thước tệp và mức sử dụng bộ nhớ. Nhờ phép nội suy, thường không có nhiều lợi ích khi vượt quá 30 FPS (vì animation vẫn sẽ trông mượt mà ở framerate kết xuất cao hơn).
- **Trimming:** Cắt phần đầu và cuối của animation nếu không có thay đổi keyframe. Điều này có thể giảm kích thước tệp đầu ra và mức sử dụng bộ nhớ với một số cảnh 3D, tùy thuộc vào nội dung của các animation track.
- **Remove Immutable Tracks:** Xóa các animation track chỉ chứa các giá trị mặc định. Điều này có thể giảm kích thước tệp đầu ra và mức sử dụng bộ nhớ với một số cảnh 3D, tùy thuộc vào nội dung của các animation track.

**Import Script**

- **Path:** Đường dẫn đến import script, có thể chạy mã *after* khi quá trình import hoàn tất để thực hiện xử lý tùy chỉnh. Xem :ref:`doc_importing_3d_scenes_import_script` để biết thêm thông tin.

**glTF**

- **Embedded Texture Handling:** Kiểm soát cách xử lý các texture được nhúng trong cảnh glTF. **Discard All Textures** sẽ không import bất kỳ texture nào, hữu ích nếu bạn muốn thiết lập materials thủ công trong Godot. **Extract Textures** trích xuất texture thành các image bên ngoài, giúp giảm kích thước tệp và cho phép kiểm soát nhiều hơn đối với các tùy chọn import. **Embed as Basis Universal** và **Embed as Uncompressed** giữ texture được nhúng trong cảnh đã import, lần lượt có và không có tính năng nén VRAM.

**FBX**

- **Importer** Phương thức import được sử dụng. ufbx xử lý các tệp fbx dưới dạng tệp fbx. FBX2glTF chuyển đổi tệp FBX thành glTF khi import và yêu cầu thiết lập bổ sung. Không khuyến nghị sử dụng FBX2glTF trừ khi bạn có lý do cụ thể để dùng nó thay cho ufbx hoặc đang làm việc với một định dạng tệp khác.
- **Allow Geometry Helper Nodes** bật hoặc tắt các geometry helper node
- **Embedded Texture Handling:** Kiểm soát cách xử lý các texture được nhúng trong cảnh fbx. **Discard All Textures** sẽ không import bất kỳ texture nào, hữu ích nếu bạn muốn thiết lập materials thủ công trong Godot. **Extract Textures** trích xuất texture thành các image bên ngoài, giúp giảm kích thước tệp và cho phép kiểm soát nhiều hơn đối với các tùy chọn import. **Embed as Basis Universal** và **Embed as Uncompressed** giữ texture được nhúng trong cảnh đã import, lần lượt có và không có tính năng nén VRAM.

**Blender-specific options**

Chỉ hiển thị đối với các tệp ``.blend``.

**Nodes**

- **Visible:** **All** import mọi thứ, kể cả các object không hiển thị. **Visible Only** chỉ import các object hiển thị. **Renderable** chỉ import các object được đánh dấu là có thể kết xuất trong Blender, bất kể chúng có thực sự hiển thị hay không. Trong Blender, khả năng kết xuất được bật hoặc tắt bằng cách nhấp vào biểu tượng camera bên cạnh mỗi object trong Outliner, còn khả năng hiển thị được bật hoặc tắt bằng biểu tượng con mắt.
- **Active Collection Only:** Nếu được chọn, chỉ import các node nằm trong collection đang hoạt động trong Blender.
- **Punctual Lights:** Nếu được chọn, import các đèn (directional, omni và spot) từ Blender. "Punctual" không nên bị nhầm với "positional", vì vậy đèn directional cũng được bao gồm.
- **Cameras:** Nếu được chọn, import các camera từ Blender.
- **Custom Properties:** Nếu được chọn, import các custom property từ Blender dưới dạng glTF extras. Dữ liệu này sau đó có thể được sử dụng từ một editor plugin sử dụng
  :ref:`GLTFDocument.register_gltf_document_extension() <class_GLTFDocument_method_register_gltf_document_extension>`, có thể thiết lập metadata của node khi import (cùng với các trường hợp sử dụng khác).
- **Modifiers:** Nếu đặt thành **No Modifiers**, các modifier của object sẽ bị bỏ qua khi import. Nếu đặt thành **All Modifiers**, áp dụng các modifier cho object khi import.

**Mesh**

- **Colors:** Nếu được chọn, import các màu vertex từ Blender.
- **UVs:** Nếu được chọn, import UV1 và UV2 của vertex từ Blender.
- **Normals:** Nếu được chọn, import các normal của vertex từ Blender.
- **Export Geometry Nodes Instances:** Nếu được chọn, import các instance của `geometry node <https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/introduction.html>`__ từ Blender.
- **GPU Instances** Nếu được chọn, import các instance và hệ thống particle dưới dạng dữ liệu buffer/accessor của GLTF thay vì nhiều object Mesh3D riêng lẻ. Tùy chọn này không bao gồm việc instancing Geometry Nodes.
- **Tangents:** Nếu được chọn, import các tangent của vertex từ Blender.
- **Skins:** **None** bỏ qua việc import dữ liệu skin của skeleton từ Blender. **4 Influences (Compatible)** import dữ liệu skin để tương thích với mọi renderer, nhưng phải đánh đổi bằng độ chính xác thấp hơn đối với một số rig nhất định. **All Influences** import dữ liệu skin với tất cả influence (tối đa 8 trong Godot), chính xác hơn nhưng có thể không tương thích với mọi renderer.
- **Export Bones Deforming Mesh Only:** Nếu được chọn, chỉ import các bone làm biến dạng mesh từ Blender.

**Materials**

- **Unpack Enabled:** Nếu được chọn, giải nén các image gốc vào filesystem của Godot và sử dụng chúng. Điều này cho phép thay đổi các thiết lập import image như nén VRAM. Nếu không được chọn, cho phép Blender chuyển đổi các image gốc, chẳng hạn như đóng gói lại roughness và metallic vào một texture roughness + metallic. Trong hầu hết trường hợp, nên giữ tùy chọn này được chọn, nhưng nếu các image của tệp ``.blend`` không ở đúng định dạng, phải tắt tùy chọn này để có hành vi chính xác.
- **Export Materials:** Nếu đặt thành **Placeholder**, không import materials nhưng vẫn giữ các surface slot để có thể gán các material riêng biệt cho những surface khác nhau. Nếu đặt thành **Export**, import materials nguyên trạng (lưu ý rằng materials dạng procedural của Blender có thể không hoạt động chính xác). Nếu đặt thành **Named Placeholder**, import materials nhưng không import các image được đóng gói trong tệp ``.blend``. Các texture sẽ phải được gán lại thủ công trong materials đã import.

**Animation**

- **Giới hạn phát lại:** Nếu được chọn, giới hạn việc nhập animation trong phạm vi phát lại được xác định trong Blender (các tùy chọn **Start** và **End** ở bên phải timeline animation trong Blender). Điều này có thể tránh đưa vào dữ liệu animation không được sử dụng, giúp scene đã nhập nhỏ hơn và tải nhanh hơn. Tuy nhiên, điều này cũng có thể khiến thiếu dữ liệu animation nếu phạm vi phát lại không được thiết lập chính xác trong Blender.
- **Luôn lấy mẫu:** Nếu được chọn, buộc lấy mẫu animation khi nhập để đảm bảo tính nhất quán giữa cách Blender và glTF thực hiện nội suy animation, nhưng phải đánh đổi bằng kích thước tệp lớn hơn. Nếu không được chọn, có thể có khác biệt trong cách nội suy animation giữa những gì bạn thấy trong Blender và scene đã nhập trong Godot, do ngữ nghĩa nội suy khác nhau giữa hai bên.
- **Nhóm track:** Nếu được chọn, nhập các animation (các action đang hoạt động và trên các track NLA) thành các track riêng biệt. Nếu không được chọn, tất cả action hiện được gán sẽ trở thành một animation glTF.

.. _doc_importing_3d_scenes_import_script:

Sử dụng import script để tự động hóa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể cung cấp một script đặc biệt để xử lý toàn bộ scene sau khi nhập. Điều này rất hữu ích cho việc xử lý hậu kỳ, thay đổi material, thực hiện những thao tác thú vị với geometry và nhiều việc khác.

Tạo một script không được gắn vào node nào bằng cách nhấp chuột phải trong dock FileSystem và chọn **New > Script…**. Trong trình chỉnh sửa script, hãy viết nội dung sau:

::

    @tool # Cần có để đoạn mã chạy được trong editor.
    extends EditorScenePostImport

    # Ví dụ này thay đổi tên của tất cả các nút.
    # Hàm được gọi ngay sau khi cảnh được nhập và nhận nút gốc.
    func _post_import(scene):
        # Đổi tên tất cả các nút thành "modified_[oldnodename]"
        iterate(scene)
        return scene # Remember to return the imported scene

    # Hàm đệ quy được gọi trên từng nút.
    # (Chỉ để minh họa; EditorScenePostImport chỉ yêu cầu hàm `_post_import(scene)`.)
    func iterate(node):
        if node != null:
            print_rich("Post-import: [b]%s[/b] -> [b]%s[/b]" % [node.name, "modified_" + node.name])
            node.name = "modified_" + node.name
            for child in node.get_children():
                iterate(child)


Hàm ``_post_import(scene: Node)`` nhận scene đã nhập làm đối số (tham số này thực tế là node gốc của scene). Scene cuối cùng sẽ được sử dụng **phải** được trả về (ngay cả khi scene có thể hoàn toàn khác).

Để sử dụng script của bạn, tìm script trong tùy chọn "Path" của tab import, bên dưới danh mục "Import Script".

Sử dụng thư viện animation
~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn cũng có thể chọn chỉ nhập **duy nhất** các animation từ tệp glTF mà không nhập gì khác. Cách này được sử dụng trong một số asset pipeline để phân phối animation riêng khỏi model. Ví dụ, cách này cho phép bạn sử dụng một bộ animation cho nhiều nhân vật mà không phải nhân bản dữ liệu animation trong từng nhân vật.

Để thực hiện việc này, chọn tệp glTF trong dock FileSystem, sau đó đổi chế độ nhập thành Animation Library trong dock Import:

.. figure:: img/importing_3d_scenes_changing_import_type.webp
   :align: center
   :alt: Đổi kiểu nhập thành Animation Library trong dock Import

   Đổi kiểu nhập thành Animation Library trong dock Import

Nhấp **Reimport** và khởi động lại editor khi được nhắc. Sau khi khởi động lại, tệp glTF sẽ được nhập dưới dạng một :ref:`class_AnimationLibrary` thay vì một
:ref:`class_PackedScene`. Sau đó, có thể tham chiếu thư viện animation này trong một
node :ref:`class_AnimationPlayer`.

Các tùy chọn nhập hiển thị sau khi đổi chế độ nhập thành Animation Library hoạt động giống như khi sử dụng chế độ nhập Scene. Xem
:ref:`doc_importing_3d_scenes_using_the_import_dock` để biết thêm thông tin.

Script bộ lọc
~~~~~~~~~~~~~

Có thể chỉ định một script bộ lọc bằng cú pháp đặc biệt để quyết định những track nào của những animation nào sẽ được giữ lại.

Script bộ lọc được thực thi trên từng animation đã nhập. Cú pháp gồm hai loại câu lệnh: loại đầu tiên dùng để chọn những animation cần lọc, loại thứ hai dùng để lọc các track riêng lẻ trong animation đã khớp. Tất cả mẫu tên đều được xử lý bằng phép so khớp biểu thức không phân biệt chữ hoa chữ thường, hỗ trợ các wildcard ``?`` và ``*`` (sử dụng
:ref:`String.matchn() <class_String_method_matchn>` ở bên dưới).

Script phải bắt đầu bằng một câu lệnh lọc animation (được biểu thị bằng dòng bắt đầu với một ``@``). Ví dụ, nếu muốn áp dụng bộ lọc cho tất cả animation đã nhập có tên kết thúc bằng ``"_Loop"``:

.. code:: text

    @+*_Loop

Tương tự, có thể thêm các mẫu bổ sung vào cùng một dòng, được phân tách bằng dấu phẩy. Đây là một ví dụ đã sửa đổi để *bao gồm* thêm tất cả animation có tên bắt đầu bằng ``"Arm_Left"``, nhưng cũng *loại trừ* tất cả animation có tên kết thúc bằng ``"Attack"``:

.. code:: text

    @+*_Loop, +Arm_Left*, -*Attack

Sau câu lệnh bộ lọc chọn animation, chúng ta thêm các mẫu lọc track để chỉ ra những track animation nào cần được giữ lại hoặc loại bỏ. Nếu không chỉ định mẫu lọc track nào, tất cả track trong các animation đã khớp sẽ bị loại bỏ!

Điều quan trọng cần lưu ý là các câu lệnh lọc track được áp dụng theo thứ tự cho từng track trong animation; điều này có nghĩa là một dòng có thể thêm một track, nhưng một quy tắc sau đó vẫn có thể loại bỏ track đó. Tương tự, một track bị loại trừ bởi quy tắc trước đó có thể được thêm lại bởi một quy tắc lọc ở phía dưới trong script bộ lọc.

Ví dụ: bao gồm tất cả track trong các animation có tên kết thúc bằng ``"_Loop"``, nhưng loại bỏ mọi track tác động đến một ``"Skeleton"`` kết thúc bằng ``"Control"``, trừ khi tên của chúng có ``"Arm"``:

::

    @+*_Loop
    +*
    -Skeleton:*Control
    +*Arm*

Trong ví dụ trên, các track như ``"Skeleton:Leg_Control"`` sẽ bị loại bỏ, còn các track như ``"Skeleton:Head"`` hoặc ``"Skeleton:Arm_Left_Control"`` sẽ được giữ lại.

Mọi dòng lọc track không bắt đầu bằng ``+`` hoặc ``-`` đều bị bỏ qua.

Kế thừa scene
-------------

Trong nhiều trường hợp, bạn có thể muốn thực hiện các sửa đổi thủ công đối với scene đã nhập. Theo mặc định, điều này không thể thực hiện được vì nếu asset 3D nguồn thay đổi, Godot sẽ nhập lại *toàn bộ* scene.

Tuy nhiên, có thể thực hiện các sửa đổi cục bộ bằng cách sử dụng *kế thừa scene*. Nếu bạn cố mở scene đã nhập bằng **Scene > Open Scene…** hoặc **Scene > Quick Open Scene…**, hộp thoại sau sẽ xuất hiện:

.. figure:: img/importing_3d_scenes_create_inherited_scene_dialog.webp
   :align: center
   :alt: Hộp thoại khi mở scene 3D đã nhập trong editor

   Hộp thoại khi mở scene 3D đã nhập trong editor

Trong các scene được kế thừa, những giới hạn duy nhất đối với việc sửa đổi là:

- Không thể xóa các node từ scene cơ sở, nhưng có thể thêm node ở bất kỳ đâu.
- Không thể chỉnh sửa các subresource. Thay vào đó, bạn cần lưu chúng bên ngoài như mô tả ở trên.

Ngoài những điều đó, mọi thao tác đều được phép.
