.. _doc_3d_particles_complex_shapes:

Các hình dạng phát xạ phức tạp
------------------------------

.. figure:: img/particle_complex_emission.webp
   :alt: Complex emission shapes

Khi việc phát hạt từ một trong các hình dạng đơn giản có sẵn trong :ref:`process material <doc_process_material_properties_shapes>` là chưa đủ, Godot cung cấp cách phát hạt từ các hình dạng phức tạp, tùy ý. Các hình dạng này được tạo từ các mesh trong scene và được lưu dưới dạng texture trong particle process material. Đây là một quy trình làm việc rất linh hoạt, cho phép người dùng sử dụng particle system cho những mục đích vượt xa các trường hợp sử dụng truyền thống, chẳng hạn như thảm thực vật, lá cây hoặc các hiệu ứng holographic phức tạp.

.. note::

    Khi tạo các điểm phát xạ từ mesh, bạn chỉ có thể chọn một node duy nhất làm nguồn phát xạ. Nếu muốn hạt phát ra từ nhiều hình dạng, bạn phải tạo nhiều particle system hoặc gộp các mesh thành một mesh trong phần mềm DCC bên ngoài.

.. figure:: img/particle_create_emission_points.webp
   :alt: Creating emission points
   :align: right

   Create particle emission points...

.. figure:: img/particle_select_emission_mesh.webp
   :alt: Select mesh for emission
   :align: right

   \...from a mesh instance as the source

.. figure:: img/particle_emission_density.webp
   :alt: Set emission density
   :align: right

   More points = higher particle density

Để sử dụng tính năng này, trước tiên hãy tạo một particle system trong scene hiện tại. Thêm một mesh instance làm nguồn cho các điểm phát xạ của hạt. Khi đã chọn particle system, hãy đi tới menu viewport và chọn mục *GPUParticles3D*. Từ đó, chọn ``Create Emission Points From Node``.

Một hộp thoại sẽ xuất hiện và yêu cầu bạn chọn một node làm nguồn phát xạ. Chọn một trong các mesh instance trong scene rồi xác nhận lựa chọn. Hộp thoại tiếp theo liên quan đến số lượng điểm và cách tạo chúng.

``Emission Points`` kiểm soát tổng số điểm mà bạn sắp tạo. Hạt sẽ xuất hiện từ các điểm này, vì vậy giá trị cần nhập phụ thuộc vào kích thước của mesh nguồn (diện tích cần bao phủ) và mật độ hạt mong muốn.

``Emission Source`` cung cấp 3 tùy chọn khác nhau về cách tạo các điểm. Chọn ``Surface Points`` nếu bạn chỉ muốn phân bố các điểm phát xạ trên bề mặt mesh. Chọn ``Surface Points + Normal (Directed)`` nếu bạn cũng muốn tạo thông tin về các pháp tuyến của bề mặt và làm cho hạt di chuyển theo hướng mà các pháp tuyến chỉ tới. Tùy chọn cuối cùng, ``Volume``, tạo các điểm phát xạ ở mọi vị trí bên trong mesh, không chỉ trên bề mặt.

Các điểm phát xạ được lưu trong hệ tọa độ cục bộ của particle system, vì vậy bạn có thể di chuyển particle node và các điểm phát xạ sẽ di chuyển theo. Điều này có thể hữu ích khi bạn muốn sử dụng cùng một particle system ở nhiều vị trí khác nhau. Mặt khác, bạn có thể phải tạo lại các điểm phát xạ khi di chuyển particle system hoặc mesh nguồn.

Texture hình dạng phát xạ
~~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_emission_textures.webp
   :alt: Emission textures
   :align: right

   The available emission shape textures

Toàn bộ dữ liệu cho các hình dạng phát xạ hạt phức tạp được lưu trong một tập hợp texture. Số lượng texture phụ thuộc vào loại hình dạng phát xạ bạn sử dụng. Nếu đặt thuộc tính ``Shape`` trong nhóm ``Emission Shape`` trên particle process material thành ``Points``, bạn sẽ có quyền truy cập vào 2 thuộc tính texture là ``Point Texture`` và ``Color Texture``. Đặt thành ``Directed Points`` thì sẽ có thêm thuộc tính thứ ba là ``Normal Texture``.

``Point Texture`` chứa tất cả các điểm phát xạ có thể có được tạo ở bước trước. Mỗi khi một hạt xuất hiện, một điểm sẽ được chọn ngẫu nhiên. ``Normal Texture``, nếu tồn tại, cung cấp một vector hướng tại cùng vị trí đó. Nếu thuộc tính ``Color Texture`` cũng được đặt, thuộc tính này cung cấp màu cho hạt, được lấy mẫu tại cùng vị trí với hai texture còn lại và điều chỉnh mọi màu khác đã được thiết lập trên process material.

Ngoài ra còn có thuộc tính ``Point Count``, bạn có thể dùng thuộc tính này để thay đổi số lượng điểm phát xạ bất kỳ lúc nào sau khi tạo hình dạng phát xạ, kể cả một cách động trong runtime khi game đang chạy.
