.. _doc_3d_particles_properties:

Các thuộc tính của hệ thống hạt 3D
----------------------------------

Các thuộc tính của bộ phát
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_props_emitter.webp
   :align: right

Ô kiểm bên cạnh thuộc tính ``Emitting`` sẽ kích hoạt và tắt hệ thống hạt. Hạt chỉ được xử lý và kết xuất khi ô này được chọn. Bạn có thể đặt thuộc tính này trong runtime nếu muốn kích hoạt hoặc tắt hệ thống hạt một cách linh động.

Thuộc tính ``Amount`` kiểm soát số hạt tối đa hiển thị tại một thời điểm bất kỳ. Tăng giá trị này để tạo ra nhiều hạt hơn, nhưng sẽ ảnh hưởng đến hiệu năng.

Thuộc tính ``Amount Ratio`` là tỷ lệ số hạt so với số lượng sẽ được phát ra. Nếu giá trị này nhỏ hơn ``1.0``, số hạt được phát ra trong suốt vòng đời sẽ là ``Amount`` * ``Amount Ratio``. Việc thay đổi giá trị này trong khi đang phát hạt không ảnh hưởng đến các hạt đã được tạo và không khiến hệ thống hạt khởi động lại. Thuộc tính này hữu ích khi tạo các hiệu ứng có số lượng hạt phát ra thay đổi theo thời gian.

Bạn có thể đặt một node hạt khác làm ``Sub Emitter``, node này sẽ được tạo dưới dạng node con của mỗi hạt. Xem phần :ref:`Bộ phát phụ <doc_3d_particles_subemitters>` trong tài liệu này để biết giải thích chi tiết về cách thêm một bộ phát phụ vào hệ thống hạt.

.. _doc_3d_particles_properties_time:

Các thuộc tính thời gian
~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_props_time.webp
   :align: right

Thuộc tính ``Lifetime`` kiểm soát thời gian tồn tại của mỗi hạt trước khi biến mất. Giá trị được tính bằng giây. Nhiều thuộc tính của hạt có thể được đặt để thay đổi trong suốt vòng đời của hạt và chuyển mượt mà từ giá trị này sang giá trị khác.

``Lifetime`` và ``Amount`` có liên quan với nhau. Chúng xác định tốc độ phát của hệ thống hạt. Khi muốn biết mỗi giây tạo ra bao nhiêu hạt, bạn sẽ dùng công thức sau:

.. math::

   Particles per second = \frac{Amount}{Lifetime}

Ví dụ: Phát 32 hạt, mỗi hạt có vòng đời 4 giây, nghĩa là hệ thống phát 8 hạt mỗi giây.

Thuộc tính ``Interp to End`` khiến tất cả hạt trong node nội suy hướng đến thời điểm cuối vòng đời của chúng.

Nếu ô kiểm bên cạnh thuộc tính ``One Shot`` được chọn, hệ thống hạt sẽ phát ``amount`` hạt rồi tự tắt. Hệ thống chỉ "chạy" một lần. Theo mặc định, thuộc tính này không được chọn, nên hệ thống sẽ tiếp tục phát hạt cho đến khi bị tắt hoặc hủy thủ công. Hạt one-shot phù hợp với các hiệu ứng phản ứng với một sự kiện đơn lẻ, chẳng hạn như nhặt vật phẩm hoặc các mảnh vụn văng ra khi một viên đạn va vào tường.

Thuộc tính ``Preprocess`` cho phép tua nhanh đến một thời điểm giữa vòng đời của hệ thống hạt và bắt đầu kết xuất từ đó. Giá trị được tính bằng giây. Giá trị ``1`` nghĩa là khi hệ thống hạt bắt đầu, nó sẽ trông như đã chạy được một giây.

Điều này hữu ích nếu bạn muốn hệ thống hạt trông như đã hoạt động được một lúc dù vừa mới được tải vào scene. Hãy xem ví dụ bên dưới. Cả hai hệ thống hạt đều mô phỏng bụi bay trong khu vực. Với giá trị preprocess là ``0``, sẽ không có bụi trong vài giây đầu vì hệ thống chưa phát đủ hạt để hiệu ứng trở nên rõ ràng. Điều này có thể thấy trong video bên trái. Hãy so sánh với video bên phải, trong đó hệ thống hạt được preprocess trong ``4`` giây. Bụi hiển thị đầy đủ ngay từ đầu vì chúng ta đã bỏ qua bốn giây "thiết lập" đầu tiên.

.. figure:: img/particle_preprocess.webp

   Không preprocess (bên trái) so với preprocess 4 giây (bên phải)

Bạn có thể làm chậm hoặc tăng tốc hệ thống hạt bằng thuộc tính ``Speed Scale``. Thuộc tính này áp dụng cho cả việc xử lý dữ liệu lẫn kết xuất hạt. Đặt giá trị là ``0`` để tạm dừng hoàn toàn hệ thống hạt hoặc đặt thành một giá trị như ``2`` để hệ thống chuyển động nhanh gấp đôi.

.. figure:: img/particle_speed_scale.webp

   Các giá trị speed scale khác nhau: 0.1 (bên trái), 0.5 (ở giữa), 1.0 (bên phải)

Thuộc tính ``Explosiveness`` kiểm soát việc các hạt được phát tuần tự hay đồng thời. Giá trị ``0`` nghĩa là các hạt được phát lần lượt từng hạt một. Giá trị ``1`` nghĩa là tất cả ``amount`` hạt được phát cùng lúc, khiến hiệu ứng có vẻ "bùng nổ" hơn.

Thuộc tính ``Randomness`` thêm tính ngẫu nhiên vào thời điểm phát hạt. Khi được đặt thành ``0``, hoàn toàn không có tính ngẫu nhiên và khoảng thời gian giữa lúc phát một hạt với hạt tiếp theo luôn giống nhau: các hạt được phát theo những khoảng *đều*. Giá trị ``Randomness`` là ``1`` khiến khoảng thời gian này hoàn toàn ngẫu nhiên. Bạn có thể dùng thuộc tính này để giảm bớt sự đồng nhất trong các hiệu ứng. Khi ``Explosiveness`` được đặt thành ``1``, thuộc tính này không có tác dụng.

.. figure:: img/particle_interpolate.webp
   :alt: Hạt chạy ở FPS thấp
   :align: right

   Tắt nội suy (bên trái) so với bật nội suy (bên phải)

Thuộc tính ``Fixed FPS`` giới hạn tần suất xử lý hệ thống hạt. Việc này bao gồm cập nhật thuộc tính cũng như xử lý va chạm và attractor. Thuộc tính này có thể cải thiện hiệu năng đáng kể, đặc biệt trong các scene sử dụng nhiều va chạm hạt. Lưu ý rằng thuộc tính này không thay đổi tốc độ hạt di chuyển hoặc xoay. Để làm điều đó, bạn sẽ dùng thuộc tính ``Speed Scale``.

Khi đặt ``Fixed FPS`` thành các giá trị rất thấp, bạn sẽ nhận thấy hoạt ảnh hạt bắt đầu bị giật. Điều này đôi khi là chủ ý nếu phù hợp với định hướng nghệ thuật, nhưng phần lớn thời gian, bạn sẽ muốn hệ thống hạt chuyển động mượt mà. Đó là tác dụng của thuộc tính ``Interpolate``. Thuộc tính này chuyển đổi mượt các thuộc tính của hạt giữa những lần cập nhật, để ngay cả hệ thống hạt chạy ở ``10`` FPS cũng trông mượt như khi chạy ở ``60``.

.. note::

    Khi sử dụng :ref:`va chạm hạt <doc_3d_particles_collision>`, hiện tượng xuyên có thể xảy ra nếu hạt di chuyển nhanh và collider mỏng. Có thể khắc phục bằng cách tăng ``Fixed FPS`` (đổi lại sẽ ảnh hưởng đến hiệu năng).

.. _doc_3d_particles_properties_collision:

Các thuộc tính va chạm
~~~~~~~~~~~~~~~~~~~~~~

.. seealso::

    Việc thiết lập va chạm hạt yêu cầu thực hiện thêm các bước được mô tả trong
    :ref:`doc_3d_particles_collision`.

Thuộc tính ``Base Size`` xác định kích thước va chạm mặc định của mỗi hạt, được dùng để kiểm tra xem hạt có đang va chạm với môi trường hay không. Thông thường, bạn nên đặt giá trị này xấp xỉ kích thước của hạt. Việc tăng giá trị này có thể hợp lý đối với các hạt rất nhỏ và di chuyển rất nhanh, nhằm ngăn chúng xuyên qua hình học va chạm.

.. _doc_3d_particles_properties_draw:

Các thuộc tính vẽ
~~~~~~~~~~~~~~~~~

.. figure:: img/particle_drawing.webp
   :alt: Các thuộc tính vẽ hạt
   :align: right

Thuộc tính ``Visibility AABB`` xác định một hộp bao quanh gốc của hệ thống hạt. Miễn là bất kỳ phần nào của hộp này nằm trong trường nhìn của camera, hệ thống hạt vẫn hiển thị. Ngay khi hộp rời khỏi trường nhìn của camera, hệ thống hạt sẽ hoàn toàn ngừng được kết xuất. Bạn có thể dùng thuộc tính này để cải thiện hiệu năng bằng cách giữ hộp nhỏ nhất có thể.

Một điều cần lưu ý khi đặt kích thước cho ``Visibility AABB`` là các hạt nằm ngoài giới hạn của nó sẽ biến mất ngay lập tức khi rời khỏi trường nhìn của camera. Va chạm hạt cũng sẽ không xảy ra bên ngoài ``Visibility AABB``. Mặc dù về mặt kỹ thuật đây không phải lỗi, điều này có thể ảnh hưởng tiêu cực đến trải nghiệm hình ảnh.

Khi thuộc tính ``Local Coords`` được chọn, mọi phép tính hạt đều sử dụng hệ tọa độ cục bộ để xác định những yếu tố như hướng lên và xuống, trọng lực và hướng di chuyển. Ví dụ, hướng lên và xuống sẽ tuân theo phép xoay của hệ thống hạt hoặc node cha của nó. Khi thuộc tính này không được chọn, không gian thế giới toàn cục được dùng cho các phép tính này: hướng xuống luôn là -Y trong không gian thế giới, bất kể hệ thống hạt được xoay như thế nào.

.. figure:: img/particle_coords.webp

   Tọa độ trong không gian cục bộ (bên trái) so với tọa độ trong không gian thế giới (bên phải)

Thuộc tính ``Draw Order`` điều khiển thứ tự vẽ từng hạt. ``Index`` nghĩa là các hạt được vẽ theo thứ tự phát: những hạt được tạo ra sau sẽ được vẽ chồng lên những hạt được tạo ra trước. ``Lifetime`` nghĩa là chúng được vẽ theo thứ tự thời gian sống còn lại. ``Reverse Lifetime`` đảo ngược thứ tự vẽ ``Lifetime``. ``View Depth`` nghĩa là các hạt được vẽ dựa trên khoảng cách của chúng đến camera: Những hạt gần camera hơn sẽ được vẽ chồng lên những hạt ở xa hơn.

Thuộc tính ``Transform Align`` điều khiển góc xoay mặc định của hạt. ``Disabled`` nghĩa là chúng không căn chỉnh theo bất kỳ hướng cụ thể nào. Thay vào đó, góc xoay của chúng được xác định bởi các giá trị được đặt trong process material. ``Z-Billboard`` nghĩa là các hạt sẽ luôn hướng về phía camera. Điều này tương tự thuộc tính ``Billboard`` trong :ref:`Standard Material <doc_standard_material_3d>`. ``Y to Velocity`` nghĩa là trục Y của mỗi hạt căn chỉnh theo hướng chuyển động của nó. Điều này có thể hữu ích cho những thứ như đạn hoặc mũi tên, khi bạn muốn các hạt luôn hướng "về phía trước". ``Z-Billboard + Y to Velocity`` kết hợp hai chế độ trước đó. Trục Z của mỗi hạt sẽ hướng về phía camera, còn trục Y sẽ căn chỉnh theo vận tốc của chúng.

Thuộc tính vệt
~~~~~~~~~~~~~~

.. figure:: img/particle_trail.webp
   :alt: Vệt hạt
   :align: right

   Thuộc tính vệt hạt

Thuộc tính ``Enabled`` điều khiển việc các hạt có được kết xuất dưới dạng vệt hay không. Bạn cần đánh dấu vào ô này nếu muốn sử dụng vệt hạt.

Thuộc tính ``Length Secs`` điều khiển thời gian phát vệt. Thời lượng này càng dài thì vệt sẽ càng dài.

Xem phần :ref:`Vệt hạt <doc_3d_particles_trails>` trong tài liệu hướng dẫn này để biết giải thích chi tiết về cách vệt hạt hoạt động và cách thiết lập chúng.
