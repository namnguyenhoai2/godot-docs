.. _doc_importing_3d_scenes_available_formats:

Các định dạng 3D được hỗ trợ
============================

Khi làm việc với các asset 3D, Godot có một importer linh hoạt và có thể cấu hình.

Godot làm việc với *scene*. Điều này có nghĩa là toàn bộ scene đang được xử lý trong phần mềm modeling 3D yêu thích của bạn sẽ được chuyển sang gần nhất có thể.

Godot hỗ trợ các *định dạng tệp scene* 3D sau:

- glTF 2.0 **(khuyến nghị)**. Godot hỗ trợ cả định dạng dạng văn bản (``.gltf``) và nhị phân (``.glb``). - ``.blend`` (Blender). Cách này gọi Blender để xuất sang glTF một cách trong suốt (yêu cầu đã cài đặt Blender). - DAE (COLLADA), một định dạng cũ vẫn được hỗ trợ. - Định dạng OBJ (Wavefront) + các tệp material MTL tương ứng. Định dạng này cũng được hỗ trợ, nhưng khá hạn chế do những giới hạn của nó (không hỗ trợ pivot, skeleton, animation, UV2, material PBR, ...). - FBX, được hỗ trợ thông qua thư viện `ufbx <https://github.com/ufbx/ufbx>`__. Quy trình import trước đây sử dụng tích hợp `FBX2glTF <https://github.com/godotengine/FBX2glTF>`__. Cách này yêu cầu cài đặt một chương trình bên ngoài liên kết với FBX SDK độc quyền, vì vậy chúng tôi khuyến nghị sử dụng phương thức ufbx mặc định hoặc các định dạng khác được liệt kê ở trên (nếu phù hợp với quy trình làm việc của bạn).

Sao chép tệp scene cùng với texture và dữ liệu mesh (nếu tách riêng) vào repository của project, sau đó Godot sẽ thực hiện import đầy đủ khi cửa sổ editor được focus.

Xuất tệp glTF 2.0 từ Blender (khuyến nghị)
------------------------------------------

Có 3 cách để xuất tệp glTF từ Blender:

- Dưới dạng tệp nhị phân glTF (``.glb``). - Dưới dạng tệp glTF dựa trên văn bản với dữ liệu nhị phân và texture tách riêng (tệp ``.gltf`` + tệp ``.bin`` + texture).

Các tệp nhị phân glTF (``.glb``) là lựa chọn nhỏ gọn hơn. Chúng bao gồm mesh và texture được thiết lập trong Blender. Khi được đưa vào Godot, các texture sẽ là một phần của tệp material của object.

Có hai lý do để sử dụng glTF với texture tách riêng. Một là để phần mô tả scene ở định dạng dựa trên văn bản và dữ liệu nhị phân nằm trong một tệp nhị phân riêng. Điều này hữu ích cho việc version control nếu bạn muốn xem xét các thay đổi ở định dạng dựa trên văn bản. Lý do thứ hai là bạn cần các tệp texture tách riêng khỏi tệp material. Nếu không cần hai điều này, các tệp nhị phân glTF là lựa chọn phù hợp.

Quy trình import glTF trước tiên tải dữ liệu của tệp glTF vào một class GLTFState trong bộ nhớ. Dữ liệu này sau đó được dùng để tạo một scene Godot. Khi import tệp tại runtime, scene này có thể được thêm trực tiếp vào tree. Quy trình export diễn ra ngược lại: một scene Godot được chuyển đổi thành class GLTFState, sau đó tệp glTF được tạo từ class đó.

.. figure:: img/importing_3d_scenes_available_formats_gltf_runtime.webp
   :align: center
   :alt: Diagram explaining the runtime import and export process for glTF files in Godot

Khi import tệp glTF trong editor, có thêm hai bước nữa. Sau khi tạo scene Godot, class ResourceImporterScene được dùng để áp dụng các thiết lập import bổ sung, bao gồm những thiết lập bạn đặt thông qua dock Import và hộp thoại Advanced Import Settings. Sau đó, scene này được lưu thành tệp scene Godot, là tệp được sử dụng khi bạn chạy/export game.

.. figure:: img/importing_3d_scenes_available_formats_gltf_editor.webp
   :align: center
   :alt: Diagram explaining the editor import process for glTF files in Godot

.. warning::

    Nếu model của bạn chứa blend shape (còn được gọi là "shape key" và "morph target"), thiết lập export glTF **Data > Armature > Export Deformation Bones Only** của bạn cần được cấu hình thành **Enabled**.

    Việc vẫn export các bone không biến dạng sẽ dẫn đến shading không chính xác.

.. note::

    Các phiên bản Blender cũ hơn 3.2 không export texture emissive cùng với tệp glTF. Nếu model của bạn sử dụng texture này và bạn đang dùng phiên bản Blender cũ, texture đó phải được đưa vào riêng.

    Theo mặc định, Blender tắt backface culling trên material và sẽ export material sao cho khớp với cách chúng được render trong Blender. Điều này có nghĩa là material trong Godot sẽ có chế độ cull được đặt thành **Disabled**. Điều này có thể làm giảm hiệu năng vì các mặt sau sẽ được render, ngay cả khi chúng đang bị các mặt khác cull. Để khắc phục, hãy bật **Backface Culling** trong tab Materials của Blender, sau đó export lại scene sang glTF.

Import trực tiếp các tệp ``.blend`` trong Godot
-----------------------------------------------

.. note::

    Chức năng này yêu cầu Blender 3.0 trở lên. Để đạt kết quả tốt nhất, chúng tôi khuyến nghị sử dụng Blender 3.5 trở lên, vì phiên bản này bao gồm nhiều bản sửa lỗi cho glTF exporter.

    **Bạn đặc biệt nên** sử dụng bản phát hành Blender chính thức được tải xuống từ blender.org, thay vì package của bản phân phối Linux hoặc Flatpak. Điều này giúp tránh các vấn đề liên quan đến việc đóng gói, chẳng hạn như các phiên bản library khác nhau có thể gây ra lỗi không tương thích hoặc các hạn chế do sandbox.

Editor có thể import trực tiếp các tệp ``.blend`` bằng cách gọi chức năng export glTF của `Blender <https://www.blender.org/>`__ một cách trong suốt.

Điều này cho phép bạn lặp lại trên các scene 3D nhanh hơn, vì bạn có thể lưu scene trong Blender, alt-tab trở lại Godot rồi thấy các thay đổi ngay lập tức. Khi làm việc với version control, cách này cũng hiệu quả hơn vì bạn không còn cần commit một bản sao của tệp glTF đã export vào version control.

Để sử dụng import ``.blend``, bạn phải cài đặt Blender trước khi mở editor Godot (nếu mở một project đã chứa các tệp ``.blend``). Nếu giữ Blender ở vị trí mặc định, Godot có thể tự động phát hiện đường dẫn của nó. Nếu không, hãy cấu hình đường dẫn đến executable của Blender trong Editor Settings (**Filesystem > Import > Blender > Blender Path**).

Nếu giữ các tệp ``.blend`` trong thư mục project nhưng không muốn chúng được Godot import, hãy tắt **Filesystem > Import > Blender > Enabled** trong Project Settings nâng cao.

Quy trình import ``.blend`` trước tiên chuyển đổi sang glTF, vì vậy vẫn sử dụng code import glTF của Godot. Do đó, quy trình import ``.blend`` giống với quy trình import glTF, nhưng có thêm một bước ở đầu.

.. figure:: img/importing_3d_scenes_available_formats_blend.webp
   :align: center
   :alt: Diagram explaining the import process for Blender files in Godot

.. note::

    Khi làm việc theo nhóm, hãy lưu ý rằng việc sử dụng các tệp ``.blend`` trong project sẽ yêu cầu *tất cả* thành viên trong nhóm phải cài đặt Blender. Mặc dù Blender được tải xuống miễn phí, điều này có thể gây thêm trở ngại khi làm việc trên project. Import ``.blend`` cũng không khả dụng trên editor Android và web, vì các nền tảng này không thể gọi chương trình bên ngoài.

    Nếu đây là vấn đề, hãy cân nhắc sử dụng các scene glTF được export từ Blender.

Xuất tệp DAE từ Blender
-----------------------

Blender có hỗ trợ COLLADA tích hợp sẵn, nhưng tính năng này không hoạt động đúng với nhu cầu của game engine và không nên được sử dụng nguyên trạng. Tuy nhiên, các scene được export bằng tính năng hỗ trợ Collada tích hợp sẵn vẫn có thể hoạt động với các scene đơn giản không có animation.

Đối với các scene phức tạp hoặc scene có animation, bạn rất nên sử dụng glTF thay thế.

Import tệp OBJ trong Godot
--------------------------

OBJ là một trong những định dạng 3D đơn giản nhất, vì vậy Godot có thể import thành công hầu hết các tệp OBJ. Tuy nhiên, OBJ cũng là một định dạng rất hạn chế: nó không hỗ trợ skinning, animation, UV2 hoặc material PBR.

Có 2 cách sử dụng mesh OBJ trong Godot:

- Tải trực tiếp chúng vào một node MeshInstance3D hoặc bất kỳ property nào khác yêu cầu mesh (chẳng hạn như GPUParticles3D). Đây là chế độ mặc định. - Thay đổi chế độ import của chúng thành **OBJ as Scene** trong dock Import, sau đó khởi động lại editor. Điều này cho phép bạn sử dụng các tùy chọn import giống như scene glTF hoặc Collada, chẳng hạn như unwrap UV2 khi import (cho :ref:`doc_using_lightmap_gi`).

.. note::

    Blender 3.4 trở lên có thể export màu vertex RGB trong các tệp OBJ (đây là một extension không chuẩn của định dạng OBJ). Godot có thể import các màu vertex đó, nhưng chúng sẽ không hiển thị trên material trừ khi bạn bật **Vertex Color > Use As Albedo** trên material.

    Màu vertex từ mesh OBJ giữ nguyên color space ban đầu sau khi được import (sRGB/linear), nhưng độ sáng của chúng bị giới hạn ở 1.0 (chúng không thể sáng hơn mức đó).

Import tệp FBX trong Godot
--------------------------

Theo mặc định, mọi tệp FBX được thêm vào một project Godot trong Godot 4.3 trở lên sẽ sử dụng phương thức import ufbx. Mọi tệp đã được thêm vào project ở một phiên bản trước đó, chẳng hạn như 4.2, sẽ tiếp tục được import thông qua phương thức FBX2glTF, trừ khi bạn mở thiết lập import của tệp đó và thay đổi importer thành ``ufbx``.

Nếu giữ các tệp ``.fbx`` trong thư mục project nhưng không muốn chúng được Godot import, hãy tắt **Filesystem > Import > FBX > Enabled** trong Project Settings nâng cao.

Nếu muốn thiết lập quy trình FBX2glTF, vốn nhìn chung không được khuyến nghị trừ khi bạn có lý do cụ thể để sử dụng, bạn cần tải xuống executable `FBX2glTF <https://github.com/godotengine/FBX2glTF>`__, sau đó chỉ định đường dẫn đến executable đó trong editor settings tại **Filesystem > Import > FBX > FBX2glTFPath**

Quy trình import FBX2glTF trước tiên chuyển đổi sang glTF, vì vậy vẫn sử dụng code import glTF của Godot. Do đó, quy trình import FBX giống với quy trình import glTF, nhưng có thêm một bước ở đầu.

.. figure:: img/importing_3d_scenes_available_formats_fbx.webp
   :align: center
   :alt: Diagram explaining the import process for FBX files in Godot  via FBX2glTF

.. seealso::

    Quy trình cài đặt đầy đủ để sử dụng FBX2glTF trong Godot được mô tả trên `FBX import page of the Godot website <https://godotengine.org/fbx-import>`_.
