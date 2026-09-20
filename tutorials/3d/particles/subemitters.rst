.. _doc_3d_particles_subemitters:

Các sub-emitter của particle
----------------------------

.. figure:: img/particle_sub_chain.webp
   :alt: Chained sub-emitters

Đôi khi không thể tạo một hiệu ứng hình ảnh chỉ với một particle system duy nhất. Đôi khi một particle system cần được spawn để phản hồi một điều xảy ra trong particle system khác. Pháo hoa là một ví dụ điển hình cho trường hợp này. Pháo hoa thường gồm nhiều giai đoạn phát nổ diễn ra theo trình tự. Sub-emitter là một cách hiệu quả để tạo loại hiệu ứng này.

.. figure:: img/particle_sub_assign.webp
   :alt: Assign sub-emitter
   :align: right

   Click to assign a sub-emitter...

.. figure:: img/particle_sub_list.webp
   :alt: List particle systems
   :align: right

   \...and select one from the scene

Sub-emitter là một particle system được spawn dưới dạng con của một particle system khác. Bạn có thể thêm sub-emitter vào các sub-emitter, nối chuỗi các hiệu ứng particle với độ sâu tùy ý.

Để tạo một sub-emitter, bạn cần ít nhất hai particle system trong cùng một scene. Một particle system sẽ là parent và một particle system sẽ được đặt làm child. Tìm thuộc tính ``Sub Emitter`` trên parent rồi nhấp vào ô bên cạnh để gán sub-emitter. Bạn sẽ thấy danh sách các particle system hiện có trong scene. Chọn một particle system rồi nhấp vào nút xác nhận.

Các particle system từ những scene được instanced cũng có thể được đặt làm sub-emitter, miễn là thuộc tính ``Editable Children`` được bật trên scene được instanced. Điều này cũng hoạt động theo chiều ngược lại: Bạn có thể gán một sub-emitter cho một particle system trong scene được instanced, kể cả khi sub-emitter đó đến từ một scene được instanced khác.

.. note::

   Khi bạn đặt một particle system làm sub-emitter của particle system khác, particle system đó sẽ dừng phát, ngay cả khi thuộc tính ``Emitting`` đã được chọn. Đừng lo, nó không bị hỏng. Điều này xảy ra với mọi particle system ngay khi nó trở thành sub-emitter. Bạn cũng sẽ không thể bật lại thuộc tính này chừng nào particle system còn được sử dụng làm sub-emitter.

.. warning::

   Mặc dù parent particle system có thể được chọn từ danh sách các particle system hiện có, một particle system là sub-emitter của chính nó sẽ không hoạt động trong Godot. Nó đơn giản là sẽ không spawn. Điều tương tự cũng đúng với mọi thiết lập sub-emitter đệ quy hoặc tự tham chiếu khác.

Chế độ emitter
~~~~~~~~~~~~~~

Khi gán một sub-emitter, bạn sẽ không thấy nó spawn ngay lập tức. Theo mặc định, emitting bị tắt và cần được bật trước. Đặt thuộc tính ``Mode`` trong nhóm ``Sub Emitter`` của :ref:`ParticleProcessMaterial <doc_process_material_properties_subemitter>` thành một giá trị khác ``Disabled``.

Chế độ emitter cũng xác định số lượng particle của sub-emitter được spawn. ``Constant`` spawn một particle duy nhất với tần suất được đặt bởi thuộc tính ``Frequency``. Đối với ``At End`` và ``At Collision``, bạn có thể đặt trực tiếp số lượng bằng các thuộc tính ``Amount At End`` và ``Amount At Collision``.

Các giới hạn
~~~~~~~~~~~~

Một điều cần lưu ý là tổng số particle đang hoạt động từ sub-emitter luôn bị giới hạn bởi thuộc tính ``Amount`` trên particle system của sub-emitter. Nếu bạn thấy sub-emitter spawn không đủ particle, có thể bạn cần tăng số lượng trong particle system.

Một số thuộc tính emitter bị bỏ qua khi một particle system được spawn dưới dạng sub-emitter. Ví dụ, thuộc tính ``Explosiveness`` không có tác dụng. Tùy thuộc vào chế độ emitter, các particle либо được spawn tuần tự theo các khoảng thời gian cố định, либо được spawn bùng nổ cùng một lúc.
