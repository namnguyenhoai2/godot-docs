.. _doc_3d_particles_subemitters:

Các sub-emitter của particle
----------------------------

.. figure:: img/particle_sub_chain.webp
   :alt: Sub-emitter liên kết

Đôi khi không thể tạo hiệu ứng hình ảnh chỉ bằng một particle system. Đôi khi một particle system cần được khởi tạo để phản hồi một sự kiện xảy ra trong particle system khác. Pháo hoa là một ví dụ điển hình. Chúng thường gồm nhiều giai đoạn phát nổ diễn ra tuần tự. Sub-emitter là một cách hiệu quả để tạo loại hiệu ứng này.

.. figure:: img/particle_sub_assign.webp
   :alt: Gán sub-emitter
   :align: right

   Nhấp để gán một sub-emitter...

.. figure:: img/particle_sub_list.webp
   :alt: Liệt kê particle system
   :align: right

   \...và chọn một particle system trong scene

Sub-emitter là một particle system được khởi tạo dưới dạng con của particle system khác. Bạn có thể thêm sub-emitter vào các sub-emitter, liên kết các hiệu ứng particle với độ sâu tùy ý.

Để tạo một sub-emitter, bạn cần ít nhất hai particle system trong cùng một scene. Một particle system sẽ là parent và một particle system sẽ được đặt làm child. Tìm thuộc tính ``Sub Emitter`` trên parent rồi nhấp vào ô bên cạnh để gán sub-emitter. Bạn sẽ thấy danh sách các particle system hiện có trong scene. Chọn một particle system rồi nhấp vào nút xác nhận.

Particle system từ các scene được instanced cũng có thể được đặt làm sub-emitter, miễn là thuộc tính ``Editable Children`` được bật trên scene được instanced. Điều này cũng hoạt động theo chiều ngược lại: Bạn có thể gán một sub-emitter cho particle system trong scene được instanced, kể cả particle system đến từ một scene được instanced khác.

.. note::

   Khi bạn đặt một particle system làm sub-emitter của particle system khác, hệ thống sẽ ngừng phát, ngay cả khi thuộc tính ``Emitting`` đã được bật. Đừng lo, hệ thống không bị hỏng. Điều này xảy ra với mọi particle system ngay khi nó trở thành sub-emitter. Bạn cũng sẽ không thể bật lại thuộc tính này chừng nào particle system còn được sử dụng làm sub-emitter.

.. warning::

   Mặc dù parent particle system có thể được chọn từ danh sách các particle system hiện có, một particle system là sub-emitter của chính nó sẽ không hoạt động trong Godot. Nó đơn giản là sẽ không được khởi tạo. Điều tương tự cũng đúng với mọi kiểu thiết lập sub-emitter đệ quy hoặc tự tham chiếu khác.

Chế độ emitter
~~~~~~~~~~~~~~

Khi gán một sub-emitter, bạn sẽ không thấy nó được khởi tạo ngay. Tính năng phát bị tắt theo mặc định và cần được bật trước. Đặt thuộc tính ``Mode`` trong nhóm ``Sub Emitter`` của :ref:`ParticleProcessMaterial <doc_process_material_properties_subemitter>` thành một giá trị khác ``Disabled``.

Chế độ emitter cũng quyết định số lượng particle của sub-emitter được khởi tạo. ``Constant`` khởi tạo một particle duy nhất theo tần suất được đặt bởi thuộc tính ``Frequency``. Với ``At End`` và ``At Collision``, bạn có thể đặt trực tiếp số lượng bằng các thuộc tính ``Amount At End`` và ``Amount At Collision``.

Giới hạn
~~~~~~~~

Một điều cần lưu ý là tổng số particle đang hoạt động từ sub-emitter luôn bị giới hạn bởi thuộc tính ``Amount`` trên particle system của sub-emitter. Nếu nhận thấy sub-emitter khởi tạo không đủ particle, bạn có thể cần tăng số lượng trong particle system.

Một số thuộc tính emitter bị bỏ qua khi particle system được khởi tạo dưới dạng sub-emitter. Ví dụ, thuộc tính ``Explosiveness`` không có tác dụng. Tùy thuộc vào chế độ emitter, các particle sẽ được khởi tạo tuần tự theo những khoảng thời gian cố định hoặc phát nổ và khởi tạo tất cả cùng lúc.
