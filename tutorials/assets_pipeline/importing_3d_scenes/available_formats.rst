.. _doc_importing_3d_scenes_available_formats:

Các định dạng 3D hiện có
========================

Khi làm việc với các tài sản 3D, Godot có trình nhập linh hoạt và có thể cấu hình.

Godot làm việc với *các scene*. Điều này có nghĩa là toàn bộ scene đang được xử lý trong phần mềm tạo mô hình 3D yêu thích của bạn sẽ được chuyển sang gần nhất có thể.

Godot hỗ trợ các *định dạng tệp scene* 3D sau:

- glTF 2.0 **(được khuyến nghị)**. Godot hỗ trợ cả định dạng văn bản (``.gltf``) và nhị phân (``.glb``).
- ``.blend`` (Blender). Định dạng này hoạt động bằng cách gọi Blender để xuất sang glTF một cách trong suốt (yêu cầu đã cài đặt Blender).
- DAE (COLLADA), một định dạng cũ hơn được hỗ trợ.
- Định dạng OBJ (Wavefront) cùng các tệp vật liệu MTL tương ứng. Định dạng này cũng được hỗ trợ, nhưng khá hạn chế do những giới hạn của nó (không hỗ trợ pivot, skeleton, animation, UV2, vật liệu PBR, ...).
- FBX, được hỗ trợ thông qua thư viện `ufbx <https://github.com/ufbx/ufbx>`__. Quy trình nhập trước đây sử dụng tích hợp `FBX2glTF <https://github.com/godotengine/FBX2glTF>`__. Quy trình này yêu cầu cài đặt một chương trình bên ngoài liên kết với FBX SDK độc quyền, vì vậy chúng tôi khuyến nghị sử dụng phương thức ufbx mặc định hoặc các định dạng khác được liệt kê ở trên (nếu phù hợp với quy trình làm việc của bạn).

Sao chép tệp scene cùng với các texture và dữ liệu mesh (nếu nằm riêng) vào repository của dự án, sau đó Godot sẽ thực hiện quá trình nhập đầy đủ khi cửa sổ editor được kích hoạt.

Xuất tệp glTF 2.0 từ Blender (được khuyến nghị)
-----------------------------------------------

Có 3 cách để xuất tệp glTF từ Blender:

- Dưới dạng tệp nhị phân glTF (``.glb``).
- Dưới dạng tệp glTF dựa trên văn bản với dữ liệu nhị phân và texture riêng biệt (tệp ``.gltf`` + tệp ``.bin`` + texture).

Các tệp nhị phân glTF (``.glb``) có kích thước nhỏ hơn. Chúng bao gồm mesh và texture được thiết lập trong Blender. Khi được đưa vào Godot, các texture sẽ là một phần của tệp vật liệu của đối tượng.

Có hai lý do để sử dụng glTF với texture riêng biệt. Một là để có phần mô tả scene ở định dạng văn bản và dữ liệu nhị phân trong một tệp nhị phân riêng. Điều này hữu ích cho việc kiểm soát phiên bản nếu bạn muốn xem xét các thay đổi ở định dạng dựa trên văn bản. Lý do thứ hai là bạn cần các tệp texture tách biệt khỏi tệp vật liệu. Nếu không cần điều nào trong hai điều này, các tệp nhị phân glTF là lựa chọn phù hợp.

Quy trình nhập glTF trước tiên tải dữ liệu của tệp glTF vào một lớp GLTFState trong bộ nhớ. Dữ liệu này sau đó được dùng để tạo một scene Godot. Khi nhập tệp lúc runtime, scene này có thể được thêm trực tiếp vào cây. Quy trình xuất là ngược lại: một scene Godot được chuyển đổi thành lớp GLTFState, sau đó tệp glTF được tạo từ lớp đó.

.. figure:: img/importing_3d_scenes_available_formats_gltf_runtime.webp
   :align: center
   :alt: Sơ đồ giải thích quy trình nhập và xuất glTF lúc runtime trong Godot

Khi nhập tệp glTF trong editor, có thêm hai bước. Sau khi tạo scene Godot, lớp ResourceImporterScene được sử dụng để áp dụng các thiết lập nhập bổ sung, bao gồm những thiết lập bạn đặt thông qua dock Import và hộp thoại Advanced Import Settings. Sau đó, kết quả được lưu thành một tệp scene Godot, là tệp được sử dụng khi bạn chạy/xuất game.

.. figure:: img/importing_3d_scenes_available_formats_gltf_editor.webp
   :align: center
   :alt: Sơ đồ giải thích quy trình nhập glTF trong editor của Godot

.. warning::

    Nếu mô hình của bạn chứa blend shape (còn gọi là "shape key" và "morph target"), thiết lập xuất glTF **Data > Armature > Export Deformation Bones Only** cần được cấu hình thành **Enabled**.

    Việc vẫn xuất các bone không biến dạng sẽ dẫn đến shading không chính xác.

.. note::

    Các phiên bản Blender cũ hơn 3.2 không xuất texture emissive cùng tệp glTF. Nếu mô hình của bạn sử dụng texture này và bạn đang dùng phiên bản Blender cũ hơn, texture đó phải được đưa vào riêng.

    Theo mặc định, Blender tắt tính năng loại bỏ mặt sau trên vật liệu và sẽ xuất vật liệu sao cho khớp với cách chúng được render trong Blender. Điều này có nghĩa là các vật liệu trong Godot sẽ có chế độ cull được đặt thành **Disabled**. Điều này có thể làm giảm hiệu năng vì các mặt sau sẽ được render, ngay cả khi chúng đang bị các mặt khác loại bỏ. Để khắc phục, hãy bật **Backface Culling** trong thẻ Materials của Blender, sau đó xuất lại scene sang glTF.

Nhập trực tiếp các tệp ``.blend`` trong Godot
---------------------------------------------

.. note::

    Tính năng này yêu cầu Blender 3.0 trở lên. Để có kết quả tốt nhất, chúng tôi khuyến nghị sử dụng Blender 3.5 trở lên, vì phiên bản này bao gồm nhiều bản sửa lỗi cho trình xuất glTF.

    **Rất** khuyến nghị sử dụng bản phát hành Blender chính thức được tải xuống từ blender.org, thay vì gói của bản phân phối Linux hoặc Flatpak. Điều này tránh các vấn đề liên quan đến việc đóng gói, chẳng hạn như các phiên bản thư viện khác nhau có thể gây ra tình trạng không tương thích hoặc các hạn chế do sandbox.

Editor có thể nhập trực tiếp các tệp ``.blend`` bằng cách gọi chức năng xuất glTF của `Blender <https://www.blender.org/>`__ một cách trong suốt.

Điều này cho phép bạn lặp lại quá trình phát triển các scene 3D nhanh hơn, vì bạn có thể lưu scene trong Blender, alt-tab trở lại Godot rồi thấy ngay các thay đổi. Khi làm việc với kiểm soát phiên bản, cách này cũng hiệu quả hơn vì bạn không còn cần commit một bản sao của tệp glTF đã xuất vào hệ thống kiểm soát phiên bản.

Để sử dụng tính năng nhập ``.blend``, bạn phải cài đặt Blender trước khi mở editor Godot (nếu mở một dự án đã chứa các tệp ``.blend``). Nếu giữ Blender ở vị trí mặc định, Godot sẽ có thể tự động phát hiện đường dẫn của Blender. Nếu không, hãy cấu hình đường dẫn đến tệp thực thi Blender trong Editor Settings (**Filesystem > Import > Blender > Blender Path**).

Nếu giữ các tệp ``.blend`` trong thư mục dự án nhưng không muốn Godot nhập chúng, hãy tắt **Filesystem > Import > Blender > Enabled** trong Project Settings nâng cao.

Quy trình nhập ``.blend`` trước tiên chuyển đổi sang glTF, vì vậy vẫn sử dụng mã nhập glTF của Godot. Do đó, quy trình nhập ``.blend`` giống với quy trình nhập glTF, nhưng có thêm một bước ở đầu.

.. figure:: img/importing_3d_scenes_available_formats_blend.webp
   :align: center
   :alt: Sơ đồ giải thích quy trình nhập tệp Blender trong Godot

.. note::

    Khi làm việc theo nhóm, hãy lưu ý rằng việc sử dụng các tệp ``.blend`` trong dự án sẽ yêu cầu *tất cả* thành viên trong nhóm phải cài đặt Blender. Mặc dù Blender được tải xuống miễn phí, điều này có thể gây thêm trở ngại khi làm việc trên dự án. Tính năng nhập ``.blend`` cũng không khả dụng trên editor Android và web, vì các nền tảng này không thể gọi các chương trình bên ngoài.

    Nếu điều này gây ra vấn đề, hãy cân nhắc sử dụng các scene glTF được export từ Blender thay thế.

Export file DAE từ Blender
--------------------------

Blender có hỗ trợ COLLADA tích hợp, nhưng tính năng này không hoạt động phù hợp với nhu cầu của game engine và không nên được sử dụng nguyên trạng. Tuy nhiên, các scene được export bằng tính năng hỗ trợ Collada tích hợp vẫn có thể hoạt động với các scene đơn giản không có animation.

Đối với các scene phức tạp hoặc có animation, bạn nên sử dụng glTF thay thế.

Import file OBJ trong Godot
---------------------------

OBJ là một trong những format 3D đơn giản nhất hiện nay, vì vậy Godot sẽ có thể import thành công hầu hết các file OBJ. Tuy nhiên, OBJ cũng là một format rất hạn chế: nó không hỗ trợ skinning, animation, UV2 hoặc vật liệu PBR.

Có 2 cách sử dụng mesh OBJ trong Godot:

- Load trực tiếp chúng trong node MeshInstance3D hoặc bất kỳ thuộc tính nào khác yêu cầu một mesh (chẳng hạn như GPUParticles3D). Đây là chế độ mặc định.
- Thay đổi chế độ import của chúng thành **OBJ as Scene** trong Import dock, sau đó khởi động lại editor. Điều này cho phép bạn sử dụng các tùy chọn import giống như scene glTF hoặc Collada, chẳng hạn như unwrap UV2 khi import (cho :ref:`doc_using_lightmap_gi`).

.. note::

    Blender 3.4 trở lên có thể export màu vertex RGB trong các file OBJ (đây là một phần mở rộng không chuẩn của format OBJ). Godot có thể import các màu vertex đó, nhưng chúng sẽ không được hiển thị trên vật liệu trừ khi bạn bật **Vertex Color > Use As Albedo** trên vật liệu.

    Màu vertex từ các mesh OBJ vẫn giữ nguyên không gian màu ban đầu sau khi import (sRGB/linear), nhưng độ sáng của chúng bị giới hạn ở mức 1.0 (chúng không thể sáng vượt mức).

Import file FBX trong Godot
---------------------------

Theo mặc định, mọi file FBX được thêm vào một project Godot trong Godot 4.3 trở lên sẽ sử dụng phương thức import ufbx. Mọi file đã được thêm vào một project ở phiên bản trước đó, chẳng hạn như 4.2, sẽ tiếp tục được import thông qua phương thức FBX2glTF, trừ khi bạn mở cài đặt import của file đó và thay đổi importer thành ``ufbx``.

Nếu bạn giữ các file ``.fbx`` trong thư mục project nhưng không muốn Godot import chúng, hãy tắt **Filesystem > Import > FBX > Enabled** trong Project Settings nâng cao.

Nếu muốn thiết lập workflow FBX2glTF, vốn thường không được khuyến nghị trừ khi bạn có lý do cụ thể để sử dụng, bạn cần tải executable `FBX2glTF <https://github.com/godotengine/FBX2glTF>`__ xuống, sau đó chỉ định đường dẫn đến executable đó trong phần cài đặt editor tại **Filesystem > Import > FBX > FBX2glTFPath**

Quy trình import FBX trước tiên sẽ chuyển đổi sang glTF, vì vậy nó vẫn sử dụng code import glTF của Godot. Do đó, quy trình import FBX giống với quy trình import glTF, nhưng có thêm một bước ở đầu.

.. figure:: img/importing_3d_scenes_available_formats_fbx.webp
   :align: center
   :alt: Sơ đồ giải thích quy trình import file FBX trong Godot thông qua FBX2glTF

.. seealso::

    Toàn bộ quy trình cài đặt để sử dụng FBX2glTF trong Godot được mô tả trên `trang import FBX của website Godot <https://godotengine.org/fbx-import>`__.
