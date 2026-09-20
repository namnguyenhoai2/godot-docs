.. _doc_particle_process_material_2d:

Cách sử dụng ParticleProcessMaterial 2D
=======================================

Các thuộc tính của vật liệu xử lý
---------------------------------

.. figure:: img/particle_minmaxcurve.webp
   :alt: ParticleProcessMaterial properties
   :align: right

   Min, max, and curve properties

Các thuộc tính trong vật liệu này điều khiển cách các hạt hoạt động và thay đổi trong suốt vòng đời của chúng. Nhiều thuộc tính trong số đó có các giá trị ``Min``, ``Max`` và ``Curve``, cho phép bạn tinh chỉnh hành vi của chúng. Mối quan hệ giữa các giá trị này như sau: Khi một hạt được tạo, thuộc tính sẽ được đặt thành một giá trị ngẫu nhiên nằm giữa ``Min`` và ``Max``. Nếu ``Min`` và ``Max`` giống nhau, giá trị sẽ luôn giống nhau đối với mọi hạt. Nếu ``Curve`` cũng được đặt, giá trị của thuộc tính sẽ được nhân với giá trị của đường cong tại thời điểm hiện tại trong vòng đời của hạt. Sử dụng đường cong để thay đổi một thuộc tính trong suốt vòng đời của hạt. Bạn có thể biểu diễn các hành vi rất phức tạp theo cách này.

.. note::
  Trang này trình bày cụ thể cách sử dụng ParticleProcessMaterial cho các cảnh 2D. Để biết thông tin về cách sử dụng nó trong cảnh 3D, hãy xem :ref:`doc_process_material_properties`.

Độ ngẫu nhiên của vòng đời
~~~~~~~~~~~~~~~~~~~~~~~~~~

Thuộc tính ``Lifetime Randomness`` kiểm soát mức độ ngẫu nhiên được áp dụng cho vòng đời của từng hạt. Giá trị ``0`` nghĩa là hoàn toàn không có tính ngẫu nhiên và mọi hạt đều tồn tại trong cùng một khoảng thời gian, được đặt bởi thuộc tính :ref:`Lifetime <doc_3d_particles_properties_time>`. Giá trị ``1`` nghĩa là vòng đời của một hạt hoàn toàn ngẫu nhiên trong phạm vi [0.0, ``Lifetime``].

Cờ hạt
------

Tạo hạt
-------

Góc
~~~

Xác định góc ban đầu của hạt (theo độ). Tham số này chủ yếu hữu ích khi được ngẫu nhiên hóa.

.. image:: img/paranim11.gif

Vận tốc
~~~~~~~

Hướng
^^^^^

Đây là hướng cơ sở mà các hạt được phát ra. Giá trị mặc định là ``Vector3(1, 0, 0)``, khiến các hạt được phát ra về bên phải. Tuy nhiên, với cài đặt trọng lực mặc định, các hạt sẽ đi thẳng xuống dưới.

.. image:: img/direction1.png

Để thuộc tính này dễ nhận thấy, bạn cần *vận tốc ban đầu* lớn hơn 0. Ở đây, chúng ta đặt vận tốc ban đầu là 40. Bạn sẽ nhận thấy các hạt được phát ra về bên phải, sau đó đi xuống do trọng lực.

.. image:: img/direction2.png

Độ tỏa
^^^^^^

Tham số này là góc tính theo độ, được cộng ngẫu nhiên theo một trong hai hướng vào ``Direction`` cơ sở. Độ tỏa ``180`` sẽ khiến các hạt được phát ra theo mọi hướng (+/- 180). Để độ tỏa có tác dụng, tham số "Initial Velocity" phải lớn hơn 0.

.. image:: img/paranim3.gif

Độ phẳng
^^^^^^^^

Thuộc tính này chỉ hữu ích cho các hạt 3D.

Vận tốc ban đầu
^^^^^^^^^^^^^^^

Vận tốc ban đầu là tốc độ phát ra của các hạt (theo pixel/giây). Tốc độ sau đó có thể bị thay đổi bởi trọng lực hoặc các gia tốc khác (như được mô tả chi tiết hơn bên dưới).

.. image:: img/paranim4.gif

Vận tốc động
------------

Vận tốc góc
~~~~~~~~~~~

Vận tốc góc là tốc độ các hạt xoay quanh tâm của chúng (theo độ/giây).

.. image:: img/paranim5.gif

Vận tốc quỹ đạo
~~~~~~~~~~~~~~~

Vận tốc quỹ đạo được sử dụng để khiến các hạt xoay quanh tâm của chúng.

.. image:: img/paranim6.gif

Gia tốc
-------

Trọng lực
~~~~~~~~~

Trọng lực được áp dụng cho mọi hạt.

.. image:: img/paranim7.gif

Gia tốc tuyến tính
~~~~~~~~~~~~~~~~~~

Gia tốc tuyến tính được áp dụng cho từng hạt.

Gia tốc hướng tâm
~~~~~~~~~~~~~~~~~

Nếu gia tốc này dương, các hạt sẽ được gia tốc ra xa tâm. Nếu âm, chúng sẽ bị hút về phía tâm.

.. image:: img/paranim8.gif

Gia tốc tiếp tuyến
~~~~~~~~~~~~~~~~~~

Gia tốc này sẽ sử dụng vector tiếp tuyến với tâm. Kết hợp với gia tốc hướng tâm có thể tạo ra các hiệu ứng đẹp mắt.

.. image:: img/paranim9.gif

Giảm chấn
~~~~~~~~~

Giảm chấn tạo ma sát lên các hạt, buộc chúng dừng lại. Nó đặc biệt hữu ích cho tia lửa hoặc vụ nổ, vốn thường bắt đầu với vận tốc tuyến tính cao rồi dừng lại khi mờ dần.

.. image:: img/paranim10.gif

Hiển thị
--------

Tỷ lệ
~~~~~

Xác định tỷ lệ ban đầu của các hạt.

.. image:: img/paranim12.gif

Đường cong màu
~~~~~~~~~~~~~~

Màu
^^^

Được sử dụng để thay đổi màu của các hạt đang được phát ra.

Biến thiên sắc độ
~~~~~~~~~~~~~~~~~

Giá trị ``Variation`` đặt biến thiên sắc độ ban đầu được áp dụng cho từng hạt. Giá trị ``Variation Random`` kiểm soát tỷ lệ ngẫu nhiên của biến thiên sắc độ.

.. _doc_particle_systems_2d_animation:

Hoạt ảnh
~~~~~~~~

.. note::

    Hoạt ảnh flipbook của hạt chỉ có hiệu lực nếu CanvasItemMaterial được sử dụng trên nút GPUParticles2D hoặc CPUParticles2D đã được
    :ref:`configured accordingly <doc_particle_systems_2d_using_flipbook>`.

Để thiết lập flipbook của hạt phát theo thứ tự, hãy đặt các giá trị **Speed Min** và **Speed Max** thành 1:

.. figure:: img/particles_flipbook_configure_animation_speed.webp
   :align: center
   :alt: Setting up particle animation for playback during the particle's lifetime

   Setting up particle animation for playback during the particle's lifetime

Theo mặc định, tính năng lặp bị tắt. Nếu hạt phát xong trước khi vòng đời kết thúc, hạt sẽ tiếp tục sử dụng khung hình cuối cùng của flipbook (khung hình này có thể hoàn toàn trong suốt, tùy thuộc vào cách thiết kế kết cấu flipbook). Nếu bật tính năng lặp, hoạt ảnh sẽ quay lại khung hình đầu tiên và tiếp tục phát.

Tùy thuộc vào số lượng hình ảnh mà sprite sheet chứa và thời gian hạt tồn tại, hoạt ảnh có thể không trông mượt mà. Mối quan hệ giữa vòng đời hạt, tốc độ hoạt ảnh và số lượng hình ảnh trong sprite sheet như sau:

.. note::

   Với tốc độ hoạt ảnh là ``1.0``, hoạt ảnh sẽ đến hình ảnh cuối cùng trong chuỗi đúng lúc vòng đời của hạt kết thúc.

   .. math::
      Animation\ FPS = \frac{Number\ of\ images}{Lifetime}

Nếu muốn sử dụng flipbook của hạt làm nguồn kết cấu hạt ngẫu nhiên cho từng hạt, hãy giữ các giá trị tốc độ ở mức 0 và thay vào đó đặt **Offset Max** thành 1:

.. figure:: img/particles_flipbook_configure_animation_offset.webp
   :align: center
   :alt: Setting up particle animation for random offset on emission

   Setting up particle animation for random offset on emission

Lưu ý rằng **Fixed FPS** của nút GPUParticles2D cũng ảnh hưởng đến quá trình phát hoạt ảnh. Để hoạt ảnh phát mượt mà, bạn nên đặt giá trị này thành 0 để hạt được mô phỏng trên mỗi khung hình được kết xuất. Nếu đây không phải là lựa chọn phù hợp với trường hợp sử dụng của bạn, hãy đặt **Fixed FPS** bằng tốc độ khung hình thực tế được flipbook sử dụng (xem công thức ở trên).

Hình dạng phát hạt
------------------

ParticleProcessMaterial cho phép bạn đặt Mặt nạ phát hạt, xác định khu vực và hướng phát hạt. Các mặt nạ này có thể được tạo từ các kết cấu trong dự án của bạn.

Đảm bảo đã đặt ParticleProcessMaterial và chọn nút GPUParticles2D. Một menu "Particles" sẽ xuất hiện trên Thanh công cụ:

.. image:: img/emission_shapes1.webp

Mở menu đó và chọn "Load Emission Mask":

.. image:: img/emission_shapes2.webp

Sau đó, chọn kết cấu bạn muốn sử dụng làm mặt nạ:

.. image:: img/emission_shapes3.webp

Một hộp thoại với một số cài đặt sẽ xuất hiện.

Mặt nạ phát hạt
~~~~~~~~~~~~~~~

Có thể tạo ba loại mặt nạ phát hạt từ một kết cấu:

-  Pixel đặc: Các hạt sẽ được tạo từ bất kỳ khu vực nào của kết cấu, ngoại trừ các khu vực trong suốt.

.. image:: img/emission_mask_solid.gif

-  Pixel viền: Các hạt sẽ được tạo từ các cạnh bên ngoài của kết cấu.

.. image:: img/emission_mask_border.gif

-  Pixel viền có hướng: Tương tự Pixel viền, nhưng bổ sung thông tin cho mặt nạ để cho phép các hạt phát ra theo hướng ra xa các đường viền. Lưu ý rằng cần đặt ``Initial Velocity`` để sử dụng tính năng này.

.. image:: img/emission_mask_directed_border.gif

Màu phát hạt
~~~~~~~~~~~~

``Capture from Pixel`` sẽ khiến các hạt kế thừa màu của mặt nạ tại điểm tạo hạt.

Sau khi bạn nhấp vào "OK", mặt nạ sẽ được tạo và đặt cho ParticleProcessMaterial, trong ``Spawn`` rồi đến ``Position``

.. image:: img/emission_shapes4.webp

Tất cả các giá trị trong phần này đã được menu "Load Emission Mask" tự động tạo, vì vậy nhìn chung bạn nên giữ nguyên chúng.

.. note:: An image should not be added to ``Point Texture`` or ``Color Texture`` directly.
          Thay vào đó, luôn sử dụng menu "Load Emission Mask".

Tùy chỉnh vật liệu xử lý
------------------------

Nếu cần thay đổi hoặc triển khai các hành vi mới trong mã shader, bạn có thể thực hiện bằng cách chuyển đổi ParticleProcessMaterial hiện tại thành :ref:`class_ShaderMaterial`. Các thuộc tính hiện có sẽ được giữ lại trong quá trình chuyển đổi. Những tính năng được bật cũng sẽ ảnh hưởng đến nội dung có trong mã shader sau khi chuyển đổi.

Để thực hiện việc này, hãy nhấp chuột phải vào vật liệu trong dock FileSystem và chọn **Convert to ShaderMaterial**. Bạn cũng có thể thực hiện bằng cách nhấp chuột phải vào bất kỳ thuộc tính nào đang chứa tham chiếu đến vật liệu trong trình kiểm tra.
