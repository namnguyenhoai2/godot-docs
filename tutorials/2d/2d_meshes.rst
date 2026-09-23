:article_outdated: Đúng

.. _doc_2d_meshes:

Lưới 2D
=======

Giới thiệu
----------

Trong 3D, các mesh được dùng để hiển thị thế giới. Trong 2D, chúng hiếm khi được sử dụng vì hình ảnh thường được dùng nhiều hơn. Engine 2D của Godot là một engine thuần hai chiều, nên về cơ bản không thể hiển thị trực tiếp các mesh 3D (mặc dù có thể thực hiện thông qua ``Viewport`` và ``ViewportTexture``).

.. seealso:: Nếu bạn muốn hiển thị các mesh 3D trên viewport 2D, hãy xem tutorial :ref:`doc_viewport_as_texture`.

Mesh 2D là các mesh chứa hình học hai chiều (có thể lược bỏ hoặc bỏ qua Z) thay vì 3D. Bạn có thể tự thử tạo chúng bằng ``SurfaceTool`` từ code và hiển thị chúng trong node ``MeshInstance2D``.

Hiện tại, cách duy nhất để tạo mesh 2D trong editor là nhập tệp OBJ dưới dạng mesh hoặc chuyển đổi từ Sprite2D.

Tối ưu hóa số pixel được vẽ
---------------------------

Quy trình này hữu ích để tối ưu hóa việc vẽ 2D trong một số trường hợp. Khi vẽ các hình ảnh lớn có độ trong suốt, Godot sẽ vẽ toàn bộ quad lên màn hình. Các vùng trong suốt lớn vẫn sẽ được vẽ.

Điều này có thể ảnh hưởng đến hiệu năng, đặc biệt trên các thiết bị di động, khi vẽ những hình ảnh rất lớn (thường có kích thước bằng màn hình) hoặc xếp chồng nhiều hình ảnh lên nhau với các vùng trong suốt lớn (ví dụ khi sử dụng ``ParallaxBackground``).

Việc chuyển đổi sang mesh sẽ đảm bảo chỉ các phần không trong suốt được vẽ, còn phần còn lại sẽ bị bỏ qua.

Chuyển đổi Sprite2D thành mesh 2D
---------------------------------

Bạn có thể tận dụng việc tối ưu hóa này bằng cách chuyển đổi một ``Sprite2D`` thành một ``MeshInstance2D``. Hãy bắt đầu với một hình ảnh có nhiều vùng trong suốt ở các cạnh, như cây này:

.. image:: img/mesh2d1.png

Đặt nó vào một ``Sprite2D`` và chọn "Convert to MeshInstance2D" từ menu:

.. image:: img/mesh2d2.webp

Một hộp thoại sẽ xuất hiện, hiển thị bản xem trước cách mesh 2D sẽ được tạo:

.. image:: img/mesh2d3.webp

Các giá trị mặc định phù hợp với nhiều trường hợp, nhưng bạn có thể thay đổi growth và simplification theo nhu cầu:

.. image:: img/mesh2d4.webp

Cuối cùng, nhấn nút :button:`Convert 2D Mesh` và Sprite2D của bạn sẽ được thay thế:

.. image:: img/mesh2d5.webp
