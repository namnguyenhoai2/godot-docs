.. _doc_particle_process_material_2d:

Cách sử dụng ParticleProcessMaterial 2D
=======================================

Các thuộc tính của process material
-----------------------------------

.. figure:: img/particle_minmaxcurve.webp
   :alt: Các thuộc tính của ParticleProcessMaterial
   :align: right

   Các thuộc tính min, max và curve

Các thuộc tính trong material này kiểm soát cách các particle hoạt động và thay đổi trong suốt vòng đời của chúng. Nhiều thuộc tính có các giá trị ``Min``, ``Max`` và ``Curve`` cho phép bạn tinh chỉnh hành vi của chúng. Mối quan hệ giữa các giá trị này như sau: Khi một particle được spawn, thuộc tính sẽ được đặt thành một giá trị ngẫu nhiên nằm giữa ``Min`` và ``Max``. Nếu ``Min`` và ``Max`` giống nhau, giá trị sẽ luôn giống nhau đối với mọi particle. Nếu ``Curve`` cũng được đặt, giá trị của thuộc tính sẽ được nhân với giá trị của curve tại điểm hiện tại trong vòng đời của particle. Sử dụng curve để thay đổi một thuộc tính trong suốt vòng đời của particle. Bằng cách này, bạn có thể biểu diễn những hành vi rất phức tạp.

.. note::
  Trang này trình bày cách sử dụng ParticleProcessMaterial dành riêng cho các scene 2D. Để biết thông tin về cách sử dụng nó trong scene 3D, hãy xem :ref:`doc_process_material_properties`.

Độ ngẫu nhiên của vòng đời
~~~~~~~~~~~~~~~~~~~~~~~~~~

Thuộc tính ``Lifetime Randomness`` kiểm soát mức độ ngẫu nhiên áp dụng cho vòng đời của mỗi particle. Giá trị ``0`` có nghĩa là hoàn toàn không có tính ngẫu nhiên và mọi particle sống trong cùng một khoảng thời gian, được thiết lập bởi thuộc tính :ref:`Lifetime <doc_3d_particles_properties_time>`. Giá trị ``1`` có nghĩa là vòng đời của particle hoàn toàn ngẫu nhiên trong phạm vi [0.0, ``Lifetime``].

Các cờ của particle
-------------------

Spawn
-----

Angle
~~~~~

Xác định góc ban đầu của particle (tính theo độ). Tham số này chủ yếu hữu ích khi được random.

.. image:: img/paranim11.gif

Velocity
~~~~~~~~

Direction
^^^^^^^^^

Đây là hướng cơ sở mà các particle phát ra. Giá trị mặc định là ``Vector3(1, 0, 0)``, khiến các particle phát ra về bên phải. Tuy nhiên, với thiết lập gravity mặc định, các particle sẽ đi thẳng xuống dưới.

.. image:: img/direction1.png

Để có thể nhận thấy tác động của thuộc tính này, bạn cần một *initial velocity* lớn hơn 0. Ở đây, chúng ta đặt initial velocity là 40. Bạn sẽ nhận thấy các particle phát ra về bên phải, sau đó đi xuống do gravity.

.. image:: img/direction2.png

Spread
^^^^^^

Tham số này là góc tính theo độ, được cộng ngẫu nhiên theo một trong hai hướng vào ``Direction`` cơ sở. Spread bằng ``180`` sẽ khiến particle phát ra theo mọi hướng (+/- 180). Để spread có tác dụng, tham số "Initial Velocity" phải lớn hơn 0.

.. image:: img/paranim3.gif

Flatness
^^^^^^^^

Thuộc tính này chỉ hữu ích đối với particle 3D.

Initial Velocity
^^^^^^^^^^^^^^^^

Initial velocity là tốc độ mà các particle được phát ra (tính bằng pixel/giây). Tốc độ sau đó có thể bị gravity hoặc các gia tốc khác thay đổi (như mô tả bên dưới).

.. image:: img/paranim4.gif

Animated Velocity
-----------------

Angular Velocity
~~~~~~~~~~~~~~~~

Angular velocity là tốc độ mà các particle xoay quanh tâm của chúng (tính bằng độ/giây).

.. image:: img/paranim5.gif

Orbit Velocity
~~~~~~~~~~~~~~

Orbit velocity được sử dụng để khiến các particle quay quanh tâm của chúng.

.. image:: img/paranim6.gif

Các gia tốc
-----------

Gravity
~~~~~~~

Gravity được áp dụng cho mọi particle.

.. image:: img/paranim7.gif

Linear Acceleration
~~~~~~~~~~~~~~~~~~~

Linear acceleration được áp dụng cho từng particle.

Radial Acceleration
~~~~~~~~~~~~~~~~~~~

Nếu gia tốc này dương, các particle sẽ được gia tốc ra xa tâm. Nếu âm, chúng sẽ bị hút về phía tâm.

.. image:: img/paranim8.gif

Tangential Acceleration
~~~~~~~~~~~~~~~~~~~~~~~

Gia tốc này sẽ sử dụng vector tiếp tuyến với tâm. Kết hợp với radial acceleration có thể tạo ra các hiệu ứng đẹp mắt.

.. image:: img/paranim9.gif

Damping
~~~~~~~

Damping áp dụng lực ma sát lên các particle, buộc chúng dừng lại. Nó đặc biệt hữu ích cho tia lửa hoặc vụ nổ, vốn thường bắt đầu với linear velocity cao rồi dừng lại khi mờ dần.

.. image:: img/paranim10.gif

Hiển thị
--------

Scale
~~~~~

Xác định scale ban đầu của các particle.

.. image:: img/paranim12.gif

Color Curves
~~~~~~~~~~~~

Color
^^^^^

Được sử dụng để thay đổi màu của các particle đang được phát ra.

Hue Variation
~~~~~~~~~~~~~

Giá trị ``Variation`` đặt độ biến thiên hue ban đầu áp dụng cho mỗi particle. Giá trị ``Variation Random`` kiểm soát tỷ lệ ngẫu nhiên của độ biến thiên hue.

.. _doc_particle_systems_2d_animation:

Animation
~~~~~~~~~

.. note::

    Animation flipbook của particle chỉ có hiệu lực nếu CanvasItemMaterial được sử dụng trên node GPUParticles2D hoặc CPUParticles2D đã được
    :ref:`cấu hình tương ứng <doc_particle_systems_2d_using_flipbook>`.

Để thiết lập flipbook của particle phát theo thứ tự, hãy đặt các giá trị **Speed Min** và **Speed Max** thành 1:

.. figure:: img/particles_flipbook_configure_animation_speed.webp
   :align: center
   :alt: Thiết lập animation của particle để phát trong suốt vòng đời của particle

   Thiết lập animation của particle để phát trong suốt vòng đời của particle

Theo mặc định, việc lặp lại bị tắt. Nếu particle phát xong trước khi vòng đời kết thúc, particle sẽ tiếp tục sử dụng frame cuối cùng của flipbook (frame này có thể hoàn toàn trong suốt tùy vào cách thiết kế texture flipbook). Nếu bật lặp, animation sẽ quay lại frame đầu tiên và tiếp tục phát.

Tùy thuộc vào số lượng hình ảnh trong sprite sheet và thời gian particle tồn tại, animation có thể trông không mượt. Mối quan hệ giữa vòng đời particle, tốc độ animation và số lượng hình ảnh trong sprite sheet như sau:

.. note::

   Ở tốc độ animation ``1.0``, animation sẽ đến hình ảnh cuối cùng trong chuỗi đúng lúc vòng đời của particle kết thúc.

   .. math::
      Animation\ FPS = \frac{Number\ of\ images}{Lifetime}

Nếu muốn sử dụng flipbook của particle làm nguồn texture particle ngẫu nhiên cho từng particle, hãy giữ các giá trị speed ở 0 và thay vào đó đặt **Offset Max** thành 1:

.. figure:: img/particles_flipbook_configure_animation_offset.webp
   :align: center
   :alt: Thiết lập animation của particle để có offset ngẫu nhiên khi phát sinh

   Thiết lập animation của particle để có offset ngẫu nhiên khi phát sinh

Lưu ý rằng **Fixed FPS** của nút GPUParticles2D cũng ảnh hưởng đến việc phát animation. Để animation phát mượt mà, bạn nên đặt giá trị này thành 0 để hạt được mô phỏng trên mọi khung hình được render. Nếu trường hợp sử dụng của bạn không cho phép điều này, hãy đặt **Fixed FPS** bằng với tốc độ khung hình hiệu dụng được animation flipbook sử dụng (xem công thức ở trên).

Hình dạng phát sinh
-------------------

ParticleProcessMaterial cho phép bạn thiết lập Emission Mask, xác định khu vực và hướng mà các hạt được phát sinh. Bạn có thể tạo các mask này từ những texture trong project của mình.

Đảm bảo đã thiết lập một ParticleProcessMaterial và đã chọn nút GPUParticles2D. Menu "Particles" sẽ xuất hiện trên Toolbar:

.. image:: img/emission_shapes1.webp

Mở menu đó và chọn "Load Emission Mask":

.. image:: img/emission_shapes2.webp

Sau đó chọn texture mà bạn muốn dùng làm mask:

.. image:: img/emission_shapes3.webp

Một hộp thoại với một số thiết lập sẽ xuất hiện.

Emission Mask
~~~~~~~~~~~~~

Có thể tạo ba loại emission mask từ một texture:

-  Pixel đặc: Hạt sẽ được phát sinh từ mọi khu vực của texture, ngoại trừ các khu vực trong suốt.

.. image:: img/emission_mask_solid.gif

-  Pixel viền: Hạt sẽ được phát sinh từ các cạnh ngoài của texture.

.. image:: img/emission_mask_border.gif

-  Pixel viền có hướng: Tương tự như Pixel viền, nhưng bổ sung thông tin cho mask để hạt có khả năng phát ra xa khỏi các đường viền. Lưu ý rằng cần thiết lập một ``Initial Velocity`` để sử dụng tính năng này.

.. image:: img/emission_mask_directed_border.gif

Emission Colors
~~~~~~~~~~~~~~~

``Capture from Pixel`` sẽ khiến các hạt kế thừa màu của mask tại các điểm phát sinh.

Sau khi bạn nhấp vào "OK", mask sẽ được tạo và thiết lập cho ParticleProcessMaterial, trong ``Spawn`` rồi đến ``Position``

.. image:: img/emission_shapes4.webp

Tất cả giá trị trong phần này đã được menu "Load Emission Mask" tự động tạo, vì vậy nhìn chung bạn nên giữ nguyên chúng.

.. note:: Không nên thêm trực tiếp một hình ảnh vào ``Point Texture`` hoặc ``Color Texture``. Luôn sử dụng menu "Load Emission Mask" thay thế.

Tùy chỉnh process material
--------------------------

Nếu cần thay đổi hoặc triển khai các hành vi mới trong mã shader, bạn có thể thực hiện bằng cách chuyển đổi ParticleProcessMaterial hiện tại thành một :ref:`class_ShaderMaterial`. Quá trình chuyển đổi sẽ giữ lại các thuộc tính hiện có. Những tính năng được bật cũng sẽ ảnh hưởng đến nội dung có trong mã shader sau khi chuyển đổi.

Để thực hiện việc này, hãy nhấp chuột phải vào material trong dock FileSystem và chọn **Convert to ShaderMaterial**. Bạn cũng có thể thực hiện bằng cách nhấp chuột phải vào bất kỳ thuộc tính nào trong inspector đang giữ tham chiếu đến material.
