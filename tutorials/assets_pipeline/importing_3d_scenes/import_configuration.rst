.. _doc_importing_3d_scenes_import_configuration:

Nhập cấu hình
=============

Godot cung cấp một số cách để tùy chỉnh dữ liệu đã nhập, chẳng hạn như dock Import, hộp thoại Advanced Import Settings và các scene kế thừa. Bạn có thể sử dụng các cách này để thực hiện thêm những thay đổi đối với scene đã nhập, chẳng hạn như điều chỉnh mesh, thêm thông tin vật lý và thêm node mới. Bạn cũng có thể viết một script chạy code ở cuối quá trình nhập để thực hiện các tùy chỉnh tùy ý.

Lưu ý rằng, khi có thể, nên ưu tiên sửa đổi dữ liệu gốc thay vì cấu hình scene sau khi nhập. Điều này giúp giảm thiểu khác biệt giữa ứng dụng tạo mô hình 3D và scene đã nhập. Xem
:ref:`doc_importing_3d_scenes_model_export_considerations` and
:ref:`doc_importing_3d_scenes_node_type_customization` articles
để biết thêm thông tin.

Quy trình nhập
--------------

Since Godot can only save its own scene format (``.tscn``/``.scn``), Godot cannot save over the original 3D scene file (which uses a different format). This is also a safer approach as it avoids making accidental changes to the source file.

Để cho phép tùy chỉnh scene và các material của scene, scene importer của Godot cho phép sử dụng các quy trình khác nhau liên quan đến cách dữ liệu được nhập.

.. figure:: img/importing_3d_scenes_import_dock.webp
   :align: center
   :alt: Import dock after selecting a 3D scene in the FileSystem dock

   Import dock after selecting a 3D scene in the FileSystem dock

Quy trình nhập này có thể được tùy chỉnh bằng 3 giao diện riêng biệt, tùy theo nhu cầu của bạn:

- Dock **Import**, sau khi chọn scene 3D bằng cách nhấp một lần vào scene đó trong dock FileSystem. - Hộp thoại **Advanced Import Settings**, có thể mở bằng cách nhấp đúp vào scene 3D trong dock FileSystem hoặc nhấp vào nút **Advanced…** trong dock Import. Hộp thoại này cho phép bạn tùy chỉnh các tùy chọn cho từng object trong Godot, đồng thời xem trước model và animation. Vui lòng xem trang :ref:`doc_advanced_import_settings` để biết thêm thông tin. - :ref:`Import hints <doc_importing_3d_scenes_node_type_customization>`, là các hậu tố đặc biệt được thêm vào tên object trong phần mềm tạo mô hình 3D. Điều này cho phép bạn tùy chỉnh các tùy chọn cho từng object trong phần mềm tạo mô hình 3D.

Đối với các tùy chỉnh cơ bản, sử dụng dock Import là đủ. Tuy nhiên, đối với các thao tác phức tạp hơn như xác định material override cho từng material, bạn sẽ cần sử dụng hộp thoại Advanced Import Settings, import hints hoặc có thể là cả hai.

.. _doc_importing_3d_scenes_using_the_import_dock:

Sử dụng dock Import
~~~~~~~~~~~~~~~~~~~

Bạn có thể điều chỉnh các tùy chọn sau trong dock Import sau khi chọn một scene 3D trong dock FileSystem:

- **Root Type:** Loại node được sử dụng làm root node. Bạn nên sử dụng các loại node kế thừa từ Node3D. Nếu không, bạn sẽ mất khả năng định vị node trực tiếp trong trình chỉnh sửa 3D. - **Root Name:** Tên của root node trong scene đã nhập. Thông thường, điều này không dễ nhận thấy khi instance scene trong trình chỉnh sửa (hoặc kéo và thả từ dock FileSystem), vì trong trường hợp này root node được đổi tên để khớp với tên tệp. - **Apply Root Scale:** Nếu bật, **Root Scale** sẽ được *áp dụng* trực tiếp lên các mesh và animation, đồng thời giữ scale của root node ở giá trị mặc định `(1, 1, 1)`. Điều này có nghĩa là nếu sau đó bạn thêm một child node bên trong scene đã nhập, node đó sẽ không bị scale. Nếu tắt, **Root Scale** sẽ nhân với scale của root node.

**Meshes**

- **Ensure Tangents:** Nếu được chọn, tạo vertex tangent bằng `Mikktspace <http://www.mikktspace.com/>`__ nếu các mesh đầu vào không có dữ liệu tangent. Khi có thể, bạn nên để phần mềm tạo mô hình 3D tạo tangent khi export thay vì dựa vào tùy chọn này. Tangent cần thiết để hiển thị chính xác normal map và height map, cùng với mọi tính năng material/shader yêu cầu tangent. Nếu bạn không cần các tính năng material yêu cầu tangent, việc tắt tùy chọn này có thể giảm kích thước tệp đầu ra và tăng tốc quá trình nhập nếu tệp 3D nguồn không chứa tangent. - **Generate LODs:** Nếu được chọn, tạo các biến thể mesh có độ chi tiết thấp hơn, được hiển thị ở khoảng cách xa để cải thiện hiệu năng render. Không phải mesh nào cũng hưởng lợi từ LOD, đặc biệt nếu chúng không bao giờ được render từ xa. Việc tắt tùy chọn này có thể giảm kích thước tệp đầu ra và tăng tốc quá trình nhập. Xem :ref:`doc_mesh_lod` để biết thêm thông tin. - **Create Shadow Meshes:** Nếu được chọn, bật việc tạo shadow mesh khi nhập. Tùy chọn này tối ưu hóa việc render bóng mà không làm giảm chất lượng bằng cách hợp nhất các vertex khi có thể. Nhờ đó, băng thông bộ nhớ cần thiết để render bóng cũng giảm. Hiện tại, việc tạo shadow mesh không hỗ trợ sử dụng mức độ chi tiết thấp hơn mesh nguồn (nhưng quá trình render bóng sẽ sử dụng LOD khi phù hợp). - **Light Baking:** Cấu hình các mesh
  :ref:`global illumination mode <class_GeometryInstance3D_property_gi_mode>`
  trong scene 3D. Nếu được đặt thành **Static Lightmaps**, tùy chọn này đặt chế độ GI của các mesh thành **Static** và tạo UV2 khi nhập cho :ref:`lightmap baking <doc_using_lightmap_gi>`. - **Lightmap Texel Size:** Chỉ hiển thị khi **Light Baking** được đặt thành **Static Lightmaps**. Kiểm soát kích thước của mỗi texel trên lightmap đã bake. Giá trị nhỏ hơn sẽ tạo ra lightmap chính xác hơn, đổi lại là kích thước lightmap lớn hơn và thời gian bake lâu hơn.

**Skins**

- **Use Named Skins:** Nếu được chọn, sử dụng :ref:`Skins <class_Skin>` có tên cho animation. Node :ref:`class_MeshInstance3D` chứa 3 thuộc tính liên quan ở đây: một Skeleton NodePath trỏ đến node Skeleton3D (thường là ``..``), một mesh và một skin:

  - Node :ref:`class_Skeleton3D` chứa danh sách các bone cùng với tên, pose và rest của chúng, một tên và một bone cha. - Mesh là toàn bộ dữ liệu vertex thô cần thiết để hiển thị một mesh. Xét về mesh, nó biết cách các vertex được weight-paint và sử dụng một số thứ tự nội bộ thường được nhập từ phần mềm tạo mô hình 3D. - Skin chứa thông tin cần thiết để bind mesh này vào Skeleton3D. Với mỗi ID bone nội bộ được phần mềm tạo mô hình 3D chọn, nó chứa hai thành phần. Thứ nhất là một Matrix được gọi là Bind Pose Matrix, Inverse Bind Matrix hoặc viết tắt là IBM. Thứ hai, Skin chứa tên của từng bone (nếu **Use Named Skins** được bật) hoặc chỉ số của bone trong danh sách Skeleton3D (nếu **Use Named Skins** bị tắt).

Kết hợp lại, những thông tin này đủ để cho Godot biết cách sử dụng các pose của bone trong node Skeleton3D để render mesh từ từng MeshInstance3D. Lưu ý rằng mỗi MeshInstance3D có thể dùng chung các bind, như thường thấy ở các model được export từ Blender, hoặc mỗi MeshInstance3D có thể sử dụng một object Skin riêng, như thường thấy ở các model được export từ các công cụ khác như Maya.


**Animation**

- **Import:** Nếu được chọn, nhập các animation từ scene 3D. - **FPS:** Số frame mỗi giây được sử dụng để bake các đường cong animation thành một chuỗi điểm với phép nội suy tuyến tính. Bạn nên cấu hình giá trị này khớp với giá trị đang được sử dụng làm cơ sở trong phần mềm tạo mô hình 3D. Giá trị cao hơn tạo ra animation chính xác hơn với các thay đổi chuyển động nhanh, đổi lại là kích thước tệp và mức sử dụng bộ nhớ cao hơn. Nhờ phép nội suy, thông thường không có nhiều lợi ích khi vượt quá 30 FPS (vì animation vẫn sẽ trông mượt ở các framerate render cao hơn). - **Trimming:** Cắt phần đầu và cuối của animation nếu không có thay đổi keyframe. Điều này có thể giảm kích thước tệp đầu ra và mức sử dụng bộ nhớ với một số scene 3D, tùy thuộc vào nội dung của các animation track. - **Remove Immutable Tracks:** Xóa các animation track chỉ chứa giá trị mặc định. Điều này có thể giảm kích thước tệp đầu ra và mức sử dụng bộ nhớ với một số scene 3D, tùy thuộc vào nội dung của các animation track.

**Import Script**

- **Path:** Đường dẫn đến một import script, có thể chạy code *sau khi* quá trình nhập hoàn tất để thực hiện xử lý tùy chỉnh. Xem :ref:`doc_importing_3d_scenes_import_script` để biết thêm thông tin.

**glTF**

- **Embedded Texture Handling:** Kiểm soát cách xử lý các texture được nhúng trong scene glTF. **Discard All Textures** sẽ không nhập bất kỳ texture nào, hữu ích nếu bạn muốn tự thiết lập material trong Godot. **Extract Textures** trích xuất texture thành các image bên ngoài, giúp kích thước tệp nhỏ hơn và cho phép kiểm soát nhiều hơn đối với các tùy chọn nhập. **Embed as Basis Universal** và **Embed as Uncompressed** giữ texture được nhúng trong scene đã nhập, lần lượt có và không có nén VRAM.

**FBX**

- **Importer** Phương thức nhập được sử dụng. ubfx xử lý các tệp fbx dưới dạng tệp fbx. FBX2glTF chuyển đổi các tệp FBX thành glTF khi nhập và yêu cầu thiết lập bổ sung. Không nên sử dụng FBX2glTF trừ khi bạn có lý do cụ thể để dùng nó thay cho ufbx hoặc cần làm việc với một định dạng tệp khác. - **Allow Geometry Helper Nodes** bật hoặc tắt các geometry helper node - **Embedded Texture Handling:** Kiểm soát cách xử lý các texture được nhúng trong scene fbx. **Discard All Textures** sẽ không nhập bất kỳ texture nào, hữu ích nếu bạn muốn tự thiết lập material trong Godot. **Extract Textures** trích xuất texture thành các image bên ngoài, giúp kích thước tệp nhỏ hơn và cho phép kiểm soát nhiều hơn đối với các tùy chọn nhập. **Embed as Basis Universal** và **Embed as Uncompressed** giữ texture được nhúng trong scene đã nhập, lần lượt có và không có nén VRAM.

**Blender-specific options**

Chỉ hiển thị đối với các tệp ``.blend``.

**Nodes**

- **Visible:** **All** nhập mọi thứ, kể cả các đối tượng không hiển thị. **Visible Only** chỉ nhập các đối tượng đang hiển thị. **Renderable** chỉ nhập các đối tượng được đánh dấu là có thể render trong Blender, bất kể chúng có thực sự hiển thị hay không. Trong Blender, khả năng render được bật/tắt bằng cách nhấp vào biểu tượng camera bên cạnh từng đối tượng trong Outliner, còn khả năng hiển thị được bật/tắt bằng biểu tượng con mắt. - **Active Collection Only:** Nếu được chọn, chỉ nhập các node nằm trong collection đang hoạt động trong Blender. - **Punctual Lights:** Nếu được chọn, nhập các đèn (directional, omni và spot) từ Blender. Không nên nhầm "Punctual" với "positional", đó là lý do directional lights cũng được bao gồm. - **Cameras:** Nếu được chọn, nhập các camera từ Blender. - **Custom Properties:** Nếu được chọn, nhập các thuộc tính tùy chỉnh từ Blender dưới dạng glTF extras. Dữ liệu này sau đó có thể được sử dụng từ một editor plugin sử dụng
  :ref:`GLTFDocument.register_gltf_document_extension() <class_GLTFDocument_method_register_gltf_document_extension>`,
  có thể thiết lập metadata của node khi import (ngoài các trường hợp sử dụng khác). - **Modifiers:** Nếu được đặt thành **No Modifiers**, các object modifier sẽ bị bỏ qua khi import. Nếu được đặt thành **All Modifiers**, các modifier sẽ được áp dụng cho các object khi import.

**Meshes**

- **Colors:** Nếu được chọn, nhập vertex colors từ Blender. - **UVs:** Nếu được chọn, nhập vertex UV1 và UV2 từ Blender. - **Normals:** Nếu được chọn, nhập vertex normals từ Blender. - **Export Geometry Nodes Instances:** Nếu được chọn, nhập các instance `geometry node <https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/introduction.html>`__ từ Blender. - **GPU Instances** Nếu được chọn, nhập các instance và particle system dưới dạng dữ liệu buffer/accessor của GLTF thay vì nhiều Mesh3D object riêng lẻ. Tùy chọn này không bao gồm Geometry Nodes instancing. - **Tangents:** Nếu được chọn, nhập vertex tangents từ Blender. - **Skins:** **None** bỏ qua việc import dữ liệu skeleton skin từ Blender. **4 Influences (Compatible)** nhập dữ liệu skin để tương thích với tất cả renderer, nhưng phải đánh đổi bằng độ chính xác thấp hơn đối với một số rig. **All Influences** nhập dữ liệu skin với tất cả influence (tối đa 8 trong Godot), cho độ chính xác cao hơn nhưng có thể không tương thích với mọi renderer. - **Export Bones Deforming Mesh Only:** Nếu được chọn, chỉ nhập các bone làm biến dạng mesh từ Blender.

**Materials**

- **Unpack Enabled:** Nếu được chọn, giải nén các ảnh gốc vào hệ thống tệp của Godot và sử dụng chúng. Điều này cho phép thay đổi các thiết lập import ảnh như nén VRAM. Nếu không được chọn, cho phép Blender chuyển đổi các ảnh gốc, chẳng hạn như đóng gói lại roughness và metallic vào một texture roughness + metallic. Trong hầu hết trường hợp, nên giữ tùy chọn này ở trạng thái được chọn, nhưng nếu các ảnh của file ``.blend`` không ở đúng định dạng, phải tắt tùy chọn này để hoạt động chính xác. - **Export Materials:** Nếu được đặt thành **Placeholder**, không import materials nhưng vẫn giữ các surface slot để có thể gán các material riêng biệt cho những surface khác nhau. Nếu được đặt thành **Export**, import materials nguyên trạng (lưu ý rằng các material Blender dạng procedural có thể không hoạt động chính xác). Nếu được đặt thành **Named Placeholder**, import materials nhưng không import các ảnh được đóng gói trong file ``.blend``. Các texture sẽ phải được gán lại thủ công trong các material đã import.

**Animation**

- **Limit Playback:** Nếu được chọn, giới hạn việc import animation trong phạm vi playback được xác định trong Blender (các tùy chọn **Start** và **End** ở bên phải timeline animation trong Blender). Điều này có thể tránh đưa vào dữ liệu animation không được sử dụng, giúp scene đã import nhỏ hơn và tải nhanh hơn. Tuy nhiên, điều này cũng có thể khiến dữ liệu animation bị thiếu nếu phạm vi playback không được thiết lập chính xác trong Blender. - **Always Sample:** Nếu được chọn, buộc thực hiện animation sampling khi import để đảm bảo tính nhất quán giữa cách Blender và glTF thực hiện animation interpolation, nhưng phải đánh đổi bằng kích thước file lớn hơn. Nếu không được chọn, có thể có khác biệt trong cách animation được nội suy giữa những gì bạn thấy trong Blender và scene đã import trong Godot, do semantics nội suy khác nhau giữa hai bên. - **Group Tracks:** Nếu được chọn, import các animation (actives và trên NLA track) dưới dạng các track riêng biệt. Nếu không được chọn, tất cả action hiện được gán sẽ trở thành một glTF animation.

.. _doc_importing_3d_scenes_import_script:

Sử dụng import script để tự động hóa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể cung cấp một script đặc biệt để xử lý toàn bộ scene sau khi import. Script này rất hữu ích cho việc post-processing, thay đổi material, thực hiện các thao tác thú vị với geometry và nhiều việc khác.

Tạo một script không được gắn vào node nào bằng cách nhấp chuột phải trong FileSystem dock và chọn **New > Script…**. Trong script editor, hãy viết như sau:

::

    @tool # Cần thiết để script chạy trong editor.
    extends EditorScenePostImport

    # Mẫu này thay đổi tất cả tên node.
    # Được gọi ngay sau khi scene được import và nhận root node.
    func _post_import(scene):
        # Đổi tất cả tên node thành "modified_[oldnodename]"
        iterate(scene)
        return scene # Nhớ trả về scene đã import

    # Hàm đệ quy được gọi trên mọi node
    # (cho mục đích minh họa; EditorScenePostImport chỉ yêu cầu một hàm `_post_import(scene)`).
    func iterate(node):
        if node != null:
            print_rich("Post-import: [b]%s[/b] -> [b]%s[/b]" % [node.name, "modified_" + node.name])
            node.name = "modified_" + node.name
            for child in node.get_children():
                iterate(child)


Hàm ``_post_import(scene: Node)`` nhận scene đã import làm đối số (tham số này thực tế là root node của scene). Scene cuối cùng sẽ được sử dụng **phải** được trả về (ngay cả khi scene đó hoàn toàn khác).

Để sử dụng script, tìm script trong tùy chọn "Path" của import tab, bên dưới danh mục "Import Script".

Sử dụng animation library
~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn cũng có thể chọn chỉ import **các animation** từ một file glTF và không import gì khác. Cách này được sử dụng trong một số asset pipeline để phân phối animation riêng biệt khỏi model. Ví dụ, cách này cho phép bạn sử dụng một bộ animation cho nhiều character mà không phải sao chép dữ liệu animation vào từng character.

Để thực hiện việc này, chọn file glTF trong FileSystem dock, sau đó đổi import mode thành Animation Library trong Import dock:

.. figure:: img/importing_3d_scenes_changing_import_type.webp
   :align: center
   :alt: Changing the import type to Animation Library in the Import dock

   Changing the import type to Animation Library in the Import dock

Nhấp **Reimport** và khởi động lại editor khi được nhắc. Sau khi khởi động lại, file glTF sẽ được import dưới dạng :ref:`class_AnimationLibrary` thay vì một
:ref:`class_PackedScene`. This animation library can then be referenced in an
:ref:`class_AnimationPlayer` node.

Các tùy chọn import hiển thị sau khi đổi import mode thành Animation Library hoạt động giống như khi sử dụng Scene import mode. Xem
:ref:`doc_importing_3d_scenes_using_the_import_dock` for more information.

Filter script
~~~~~~~~~~~~~

Có thể chỉ định một filter script theo cú pháp đặc biệt để quyết định những track nào từ những animation nào sẽ được giữ lại.

Filter script được thực thi trên từng animation đã import. Cú pháp bao gồm hai loại câu lệnh: loại đầu tiên dùng để chọn những animation cần lọc, loại thứ hai dùng để lọc từng track trong animation phù hợp. Tất cả name pattern đều được thực hiện bằng phép so khớp biểu thức không phân biệt chữ hoa chữ thường, với hỗ trợ wildcard ``?`` và ``*`` (sử dụng
:ref:`String.matchn() <class_String_method_matchn>` under the hood).

Script phải bắt đầu bằng một câu lệnh animation filter (được biểu thị bằng dòng bắt đầu với ``@``). Ví dụ: nếu muốn áp dụng filter cho tất cả animation đã import có tên kết thúc bằng ``"_Loop"``:

.. code:: text

    @+*_Loop

Tương tự, có thể thêm các pattern bổ sung vào cùng một dòng, được phân tách bằng dấu phẩy. Đây là một ví dụ đã chỉnh sửa để *include* thêm tất cả animation có tên bắt đầu bằng ``"Arm_Left"``, nhưng cũng *exclude* tất cả animation có tên kết thúc bằng ``"Attack"``:

.. code:: text

    @+*_Loop, +Arm_Left*, -*Attack

Sau câu lệnh animation selection filter, chúng ta thêm các pattern lọc track để chỉ ra những animation track nào cần được giữ lại hoặc loại bỏ. Nếu không chỉ định pattern lọc track nào, tất cả track trong các animation phù hợp sẽ bị loại bỏ!

Điều quan trọng cần lưu ý là các câu lệnh lọc track được áp dụng theo thứ tự cho từng track trong animation; điều này có nghĩa là một dòng có thể include một track, nhưng một rule xuất hiện sau đó vẫn có thể discard track này. Tương tự, một track bị exclude bởi rule trước đó có thể được include lại bởi một filter rule ở vị trí sau trong filter script.

Ví dụ: include tất cả track trong các animation có tên kết thúc bằng ``"_Loop"``, nhưng discard mọi track tác động lên một ``"Skeleton"`` và kết thúc bằng ``"Control"``, trừ khi tên của chúng có ``"Arm"``:

::

    @+*_Loop
    +*
    -Skeleton:*Control
    +*Arm*

Trong ví dụ trên, các track như ``"Skeleton:Leg_Control"`` sẽ bị discard, trong khi các track như ``"Skeleton:Head"`` hoặc ``"Skeleton:Arm_Left_Control"`` sẽ được giữ lại.

Mọi dòng lọc track không bắt đầu bằng ``+`` hoặc ``-`` đều bị bỏ qua.

Kế thừa scene
-------------

Trong nhiều trường hợp, bạn có thể muốn thực hiện các chỉnh sửa thủ công đối với scene đã import. Theo mặc định, điều này không thể thực hiện vì nếu asset 3D nguồn thay đổi, Godot sẽ import lại *toàn bộ* scene.

Tuy nhiên, có thể thực hiện các chỉnh sửa cục bộ bằng cách sử dụng *scene inheritance*. Nếu bạn thử mở scene đã import bằng **Scene > Open Scene…** hoặc **Scene > Quick Open Scene…**, hộp thoại sau sẽ xuất hiện:

.. figure:: img/importing_3d_scenes_create_inherited_scene_dialog.webp
   :align: center
   :alt: Dialog when opening an imported 3D scene in the editor

   Dialog when opening an imported 3D scene in the editor

Trong các scene được kế thừa, những giới hạn duy nhất đối với việc chỉnh sửa là:

- Không thể xóa các node từ scene cơ sở, nhưng có thể thêm các node bổ sung ở bất kỳ đâu. - Không thể chỉnh sửa subresource. Thay vào đó, bạn cần lưu chúng ra bên ngoài như mô tả ở trên.

Ngoài những điều đó, mọi thao tác đều được phép.
