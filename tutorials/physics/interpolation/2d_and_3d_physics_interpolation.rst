.. _doc_2d_and_3d_physics_interpolation:

Nội suy vật lý 2D và 3D
=======================

Nhìn chung, nội suy vật lý 2D và 3D hoạt động theo những cách rất tương tự nhau. Tuy nhiên, có một vài điểm khác biệt sẽ được mô tả ở đây.

Hạt 2D
------

Hiện tại, chỉ ``CPUParticles2D`` được hỗ trợ nội suy vật lý trong 2D. Bạn nên sử dụng tốc độ tick vật lý ít nhất 20-30 tick mỗi giây để giữ cho các hạt trông mượt mà.

``Particles2D`` (hạt GPU) hiện chưa được nội suy, vì vậy hiện tại bạn nên chuyển đổi sang ``CPUParticles2D`` (nhưng hãy giữ bản sao lưu của ``Particles2D`` phòng khi chúng ta làm cho chúng hoạt động được).

Khác
----

- ``get_global_transform_interpolated()`` hiện chỉ khả dụng cho 3D.
- ``MultiMeshes`` được hỗ trợ trong cả 2D và 3D.
- Nội suy vật lý trong 2D được triển khai ở phía server, nghĩa là nó có hiệu lực đối với các physics body được tạo bằng :ref:`low-level servers <doc_using_servers>`. Ngược lại, nội suy vật lý trong 3D được triển khai ở phía scene. Điều này có nghĩa là nó không ảnh hưởng đến các physics body được tạo bằng servers. Thay vào đó, bạn phải tự nội suy các physics body này. Xem `pull request description <https://github.com/godotengine/godot/pull/104269>`__ để biết lý do của quyết định thiết kế này.
