.. _doc_3d_particles_properties:

Các thuộc tính của hệ thống Particle 3D
---------------------------------------

Các thuộc tính của Emitter
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_props_emitter.webp
   :align: right

Ô kiểm bên cạnh thuộc tính ``Emitting`` sẽ kích hoạt và vô hiệu hóa hệ thống particle. Các particle chỉ được xử lý và kết xuất khi ô này được chọn. Bạn có thể thiết lập thuộc tính này trong runtime nếu muốn kích hoạt hoặc vô hiệu hóa các hệ thống particle một cách linh động.

Thuộc tính ``Amount`` kiểm soát số lượng particle tối đa hiển thị tại bất kỳ thời điểm nào. Tăng giá trị này để tạo ra nhiều particle hơn, nhưng sẽ ảnh hưởng đến hiệu năng.

Thuộc tính ``Amount Ratio`` là tỷ lệ particle so với số lượng sẽ được phát ra. Nếu giá trị này nhỏ hơn ``1.0``, số lượng particle được phát ra trong suốt vòng đời sẽ là ``Amount`` * ``Amount Ratio``. Việc thay đổi giá trị này trong khi đang phát không ảnh hưởng đến các particle đã được tạo và không khiến hệ thống particle khởi động lại. Thuộc tính này hữu ích khi tạo các hiệu ứng có số lượng particle phát ra thay đổi theo thời gian.

Bạn có thể đặt một node particle khác làm ``Sub Emitter``, node này sẽ được tạo dưới dạng node con của mỗi particle. Xem phần :ref:`Sub-emitters <doc_3d_particles_subemitters>` trong tài liệu hướng dẫn này để biết giải thích chi tiết về cách thêm một sub-emitter vào hệ thống particle.

.. _doc_3d_particles_properties_time:

Các thuộc tính thời gian
~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_props_time.webp
   :align: right

Thuộc tính ``Lifetime`` kiểm soát thời gian tồn tại của mỗi particle trước khi biến mất. Giá trị này được tính bằng giây. Nhiều thuộc tính particle có thể được thiết lập để thay đổi trong suốt vòng đời của particle và chuyển đổi mượt mà từ giá trị này sang giá trị khác.

``Lifetime`` và ``Amount`` có liên quan với nhau. Chúng xác định tốc độ phát của hệ thống particle. Khi muốn biết mỗi giây có bao nhiêu particle được tạo ra, bạn sẽ sử dụng công thức sau:

.. math::

   Particles per second = \frac{Amount}{Lifetime}

Ví dụ: Phát 32 particle, mỗi particle có vòng đời 4 giây, nghĩa là hệ thống phát 8 particle mỗi giây.

Thuộc tính ``Interp to End`` khiến tất cả particle trong node nội suy về thời điểm kết thúc vòng đời của chúng.

Nếu ô kiểm bên cạnh thuộc tính ``One Shot`` được chọn, hệ thống particle sẽ phát ``amount`` particle rồi tự vô hiệu hóa. Hệ thống chỉ "chạy" một lần. Theo mặc định, thuộc tính này không được chọn, vì vậy hệ thống sẽ tiếp tục phát particle cho đến khi bị vô hiệu hóa hoặc bị hủy thủ công. Particle one-shot phù hợp với các hiệu ứng phản hồi một sự kiện duy nhất, chẳng hạn như vật phẩm được nhặt hoặc các mảnh vụn văng ra khi một viên đạn va vào tường.

Thuộc tính ``Preprocess`` cho phép tua nhanh đến một thời điểm ở giữa vòng đời của hệ thống particle và bắt đầu kết xuất từ đó. Giá trị này được tính bằng giây. Giá trị ``1`` có nghĩa là khi hệ thống particle bắt đầu, nó sẽ trông như đã chạy được một giây.

Điều này hữu ích khi bạn muốn hệ thống particle trông như đã hoạt động được một thời gian, dù nó chỉ vừa được tải vào scene. Hãy xem ví dụ bên dưới. Cả hai hệ thống particle đều mô phỏng bụi bay trong khu vực. Với giá trị preprocess là ``0``, sẽ không có bụi trong vài giây đầu tiên vì hệ thống chưa phát đủ particle để hiệu ứng trở nên dễ nhận thấy. Điều này có thể thấy trong video bên trái. Hãy so sánh với video bên phải, nơi hệ thống particle được preprocess trong ``4`` giây. Bụi hiển thị đầy đủ ngay từ đầu vì chúng ta đã bỏ qua bốn giây đầu tiên của thời gian "thiết lập".

.. figure:: img/particle_preprocess.webp

   No preprocess (left) vs. 4 seconds of preprocess (right)

Bạn có thể làm chậm hoặc tăng tốc hệ thống particle bằng thuộc tính ``Speed Scale``. Thuộc tính này áp dụng cho cả việc xử lý dữ liệu và kết xuất particle. Đặt giá trị là ``0`` để tạm dừng hoàn toàn hệ thống particle, hoặc đặt thành một giá trị như ``2`` để khiến hệ thống chuyển động nhanh gấp đôi.

.. figure:: img/particle_speed_scale.webp

   Different speed scale values: 0.1 (left), 0.5 (middle), 1.0 (right)

Thuộc tính ``Explosiveness`` kiểm soát việc particle được phát tuần tự hay đồng thời. Giá trị ``0`` có nghĩa là các particle được phát lần lượt. Giá trị ``1`` có nghĩa là toàn bộ ``amount`` particle được phát cùng lúc, khiến hiệu ứng có vẻ "bùng nổ" hơn.

Thuộc tính ``Randomness`` thêm một mức ngẫu nhiên vào thời điểm phát particle. Khi được đặt thành ``0``, hoàn toàn không có tính ngẫu nhiên và khoảng thời gian giữa việc phát particle này với particle tiếp theo luôn giống nhau: các particle được phát theo các khoảng thời gian *đều đặn*. Giá trị ``Randomness`` là ``1`` khiến khoảng thời gian này hoàn toàn ngẫu nhiên. Bạn có thể sử dụng thuộc tính này để giảm bớt sự đồng nhất trong các hiệu ứng. Khi ``Explosiveness`` được đặt thành ``1``, thuộc tính này không có tác dụng.

.. figure:: img/particle_interpolate.webp
   :alt: Particles running at low FPS
   :align: right

   Interpolation off (left) vs. on (right)

Thuộc tính ``Fixed FPS`` giới hạn tần suất hệ thống particle được xử lý. Điều này bao gồm việc cập nhật thuộc tính, cũng như collision và attractor. Thuộc tính này có thể cải thiện hiệu năng đáng kể, đặc biệt trong các scene sử dụng nhiều particle collision. Lưu ý rằng thuộc tính này không thay đổi tốc độ particle di chuyển hoặc xoay. Bạn sẽ sử dụng thuộc tính ``Speed Scale`` cho mục đích đó.

Khi đặt ``Fixed FPS`` thành các giá trị rất thấp, bạn sẽ nhận thấy animation của particle bắt đầu trông giật cục. Đôi khi điều này là mong muốn nếu phù hợp với định hướng nghệ thuật, nhưng phần lớn thời gian, bạn sẽ muốn các hệ thống particle được animate mượt mà. Đó là tác dụng của thuộc tính ``Interpolate``. Thuộc tính này blend các thuộc tính của particle giữa các lần cập nhật, để ngay cả một hệ thống particle chạy ở ``10`` FPS cũng trông mượt như khi chạy ở ``60``.

.. note::

    Khi sử dụng :ref:`particle collision <doc_3d_particles_collision>`, hiện tượng tunneling có thể xảy ra nếu particle di chuyển nhanh và collider mỏng. Bạn có thể khắc phục điều này bằng cách tăng ``Fixed FPS`` (đổi lại sẽ ảnh hưởng đến hiệu năng).

.. _doc_3d_particles_properties_collision:

Các thuộc tính collision
~~~~~~~~~~~~~~~~~~~~~~~~

.. seealso::

    Việc thiết lập particle collision yêu cầu thực hiện thêm các bước được mô tả trong
    :ref:`doc_3d_particles_collision`.

Thuộc tính ``Base Size`` xác định kích thước collision mặc định của mỗi particle, được sử dụng để kiểm tra xem particle có đang collision với môi trường hay không. Thông thường, bạn nên đặt giá trị này xấp xỉ kích thước của particle. Việc tăng giá trị này có thể hợp lý đối với các particle rất nhỏ và di chuyển rất nhanh, nhằm ngăn chúng xuyên qua hình học collision.

.. _doc_3d_particles_properties_draw:

Các thuộc tính vẽ
~~~~~~~~~~~~~~~~~

.. figure:: img/particle_drawing.webp
   :alt: Particle drawing properties
   :align: right

Thuộc tính ``Visibility AABB`` xác định một hình hộp xung quanh origin của hệ thống particle. Chỉ cần bất kỳ phần nào của hình hộp này nằm trong trường nhìn của camera thì hệ thống particle vẫn hiển thị. Ngay khi hình hộp rời khỏi trường nhìn của camera, hệ thống particle sẽ hoàn toàn không còn được kết xuất. Bạn có thể sử dụng thuộc tính này để cải thiện hiệu năng bằng cách giữ cho hình hộp nhỏ nhất có thể.

Một điều cần lưu ý khi đặt kích thước cho ``Visibility AABB`` là các particle nằm ngoài phạm vi của nó sẽ biến mất ngay lập tức khi rời khỏi trường nhìn của camera. Particle collision cũng sẽ không xảy ra bên ngoài ``Visibility AABB``. Dù về mặt kỹ thuật đây không phải là lỗi, điều này có thể ảnh hưởng tiêu cực đến trải nghiệm hình ảnh.

Khi thuộc tính ``Local Coords`` được chọn, mọi phép tính particle đều sử dụng hệ tọa độ cục bộ để xác định những yếu tố như hướng lên và xuống, trọng lực, cũng như hướng chuyển động. Ví dụ, hướng lên và xuống sẽ tuân theo rotation của hệ thống particle hoặc node cha của nó. Khi thuộc tính này không được chọn, không gian thế giới toàn cục được sử dụng cho các phép tính này: hướng xuống sẽ luôn là -Y trong không gian thế giới, bất kể rotation của hệ thống particle.

.. figure:: img/particle_coords.webp

   Local space coordinates (left) vs. world space coordinates (right)

Thuộc tính ``Draw Order`` kiểm soát thứ tự vẽ từng particle. ``Index`` có nghĩa là chúng được vẽ theo thứ tự phát: các particle được tạo sau sẽ được vẽ bên trên các particle được tạo trước. ``Lifetime`` có nghĩa là chúng được vẽ theo thứ tự vòng đời còn lại. ``Reverse Lifetime`` đảo ngược thứ tự vẽ ``Lifetime``. ``View Depth`` có nghĩa là các particle được vẽ dựa trên khoảng cách đến camera: các particle gần camera hơn được vẽ bên trên các particle ở xa hơn.

Thuộc tính ``Transform Align`` kiểm soát rotation mặc định của particle. ``Disabled`` có nghĩa là chúng không căn chỉnh theo bất kỳ hướng cụ thể nào. Thay vào đó, rotation của chúng được xác định bởi các giá trị được thiết lập trong process material. ``Z-Billboard`` có nghĩa là các particle luôn hướng về camera. Điều này tương tự thuộc tính ``Billboard`` trong :ref:`Standard Material <doc_standard_material_3d>`. ``Y to Velocity`` có nghĩa là trục Y của mỗi particle căn chỉnh theo hướng chuyển động của nó. Điều này hữu ích cho những thứ như viên đạn hoặc mũi tên, khi bạn muốn particle luôn hướng "về phía trước". ``Z-Billboard + Y to Velocity`` kết hợp hai chế độ trước đó. Trục Z của mỗi particle sẽ hướng về camera, trong khi trục Y căn chỉnh theo velocity của chúng.

Các thuộc tính trail
~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_trail.webp
   :alt: Particle trails
   :align: right

   Particle trail properties

Thuộc tính ``Enabled`` kiểm soát việc particle có được kết xuất dưới dạng trail hay không. Bạn cần chọn ô này nếu muốn sử dụng particle trail.

Thuộc tính ``Length Secs`` kiểm soát thời gian một trail được phát. Thời lượng này càng dài thì trail càng dài.

Xem phần :ref:`Particle trails <doc_3d_particles_trails>` trong tài liệu hướng dẫn này để biết giải thích chi tiết về cách particle trail hoạt động và cách thiết lập chúng.
