.. _doc_process_material_properties:

Thuộc tính xử lý vật liệu
-------------------------

.. figure:: img/particle_minmaxcurve.webp
   :alt: ParticleProcessMaterial properties
   :align: right

   Min, max, and curve properties

Các thuộc tính trong vật liệu này kiểm soát cách các particle hoạt động và thay đổi trong suốt vòng đời của chúng. Nhiều thuộc tính có các giá trị ``Min``, ``Max`` và ``Curve``, cho phép bạn tinh chỉnh hành vi của chúng. Mối quan hệ giữa các giá trị này như sau: Khi một particle được sinh ra, thuộc tính sẽ được gán một giá trị ngẫu nhiên nằm giữa ``Min`` và ``Max``. Nếu ``Min`` và ``Max`` giống nhau, giá trị này sẽ luôn giống nhau đối với mọi particle. Nếu ``Curve`` cũng được thiết lập, giá trị của thuộc tính sẽ được nhân với giá trị của curve tại điểm hiện tại trong vòng đời của particle. Hãy sử dụng curve để thay đổi một thuộc tính trong suốt vòng đời của particle. Bạn có thể biểu diễn các hành vi rất phức tạp theo cách này.

.. note::
  Trang này trình bày cách sử dụng ParticleProcessMaterial, cụ thể cho các scene 3D. Để biết thông tin về cách sử dụng nó trong Scene 2D, hãy xem :ref:`doc_particle_process_material_2d`.

Thời gian
~~~~~~~~~

Thuộc tính ``Lifetime Randomness`` kiểm soát mức độ ngẫu nhiên được áp dụng cho vòng đời của mỗi particle. Giá trị ``0`` có nghĩa là hoàn toàn không có tính ngẫu nhiên và mọi particle đều tồn tại trong cùng một khoảng thời gian, được thiết lập bởi thuộc tính :ref:`Lifetime <doc_3d_particles_properties_time>`. Giá trị ``1`` có nghĩa là vòng đời của một particle hoàn toàn ngẫu nhiên trong phạm vi [0.0, ``Lifetime``].

Cờ particle
-----------

Thuộc tính ``Align Y`` căn trục Y của mỗi particle theo vận tốc của nó. Bật thuộc tính này tương đương với việc đặt thuộc tính :ref:`Transform Align <doc_3d_particles_properties_draw>` thành ``Y to Velocity``.

Thuộc tính ``Rotate Y`` hoạt động cùng với các thuộc tính trong các nhóm `Angle <#angle>`__ và `Angular Velocity <#angular-velocity>`__ để kiểm soát rotation của particle. Phải bật ``Rotate Y`` nếu bạn muốn áp dụng rotation cho particle. Ngoại lệ là các particle sử dụng :ref:`Standard Material <doc_standard_material_3d>`, trong đó thuộc tính ``Billboard`` được đặt thành ``Particle Billboard``. Trong trường hợp đó, các particle sẽ rotate ngay cả khi chưa bật ``Rotate Y``.

Khi thuộc tính ``Disable Z`` được bật, các particle sẽ không di chuyển dọc theo trục Z. Trục Z cục bộ của particle system hay trục Z của world sẽ được xác định bởi thuộc tính :ref:`Local Coords <doc_3d_particles_properties_draw>`.

Thuộc tính ``Damping as Friction`` thay đổi hành vi của damping từ giảm tốc không đổi thành giảm tốc dựa trên speed.

Sinh particle
-------------

.. _doc_process_material_properties_shapes:

Hình dạng phát sinh
~~~~~~~~~~~~~~~~~~~

Particle có thể phát sinh từ một điểm duy nhất trong không gian hoặc theo cách lấp đầy một hình dạng. Thuộc tính ``Shape`` kiểm soát hình dạng đó. ``Point`` là giá trị mặc định. Tất cả particle đều phát sinh từ một điểm duy nhất ở trung tâm của particle system. Khi được đặt thành ``Sphere`` hoặc ``Box``, particle sẽ phát sinh theo cách lấp đầy đều một hình cầu hoặc hình hộp. Bạn có toàn quyền kiểm soát kích thước của các hình dạng này. ``Sphere Surface`` hoạt động giống ``Sphere``, nhưng thay vì lấp đầy hình dạng, tất cả particle sẽ phát sinh trên bề mặt hình cầu.

.. figure:: img/particle_shapes_simple.webp
   :alt: Simple particle emission shapes

   Particles emitting from a point (left), in a sphere (middle), and in a box (right)

.. figure:: img/particle_ring.webp
   :alt: Ring-shaped particle system
   :align: right

   A ring-shaped particle system

Hình dạng phát sinh ``Ring`` khiến particle phát sinh theo hình một vòng tròn. Bạn có thể kiểm soát hướng của vòng tròn bằng cách thay đổi thuộc tính ``Ring Axis``. ``Ring Height`` kiểm soát độ dày của vòng tròn dọc theo trục của nó. ``Ring Radius`` và ``Ring Inner Radius`` kiểm soát độ rộng của vòng tròn và kích thước của lỗ ở giữa. Hình ảnh cho thấy một particle system có bán kính ``2`` và bán kính trong ``1.5``, với trục hướng dọc theo trục Z toàn cục.

Ngoài các hình dạng tương đối đơn giản này, bạn có thể chọn tùy chọn ``Points`` hoặc ``Directed Points`` để tạo các hình dạng phát sinh rất phức tạp. Xem
:ref:`Complex emission shapes <doc_3d_particles_complex_shapes>` section for a detailed
phần giải thích về cách thiết lập chúng.

Góc
~~~

Thuộc tính ``Angle`` kiểm soát rotation ban đầu của particle `như đã mô tả ở trên <#process-material-properties>`__. Để thực sự tạo ra hiệu ứng trên particle, bạn phải bật một trong hai thuộc tính: `Rotate Y <#particle-flags>`__ rotate particle quanh trục Y của particle system. Thuộc tính ``Billboard`` trong :ref:`Standard Material <doc_standard_material_3d>`, nếu được đặt thành ``Particle Billboard``, sẽ rotate particle quanh trục hướng từ particle đến camera.

Hướng
~~~~~

.. note::

   Chỉ riêng thuộc tính ``Direction`` là chưa đủ để nhìn thấy bất kỳ chuyển động nào của particle. Bất kể bạn đặt các giá trị nào ở đây, chúng chỉ có hiệu lực sau khi các thuộc tính velocity hoặc acceleration cũng được thiết lập.

Thuộc tính ``Direction`` là một vector kiểm soát hướng di chuyển của mỗi particle tại thời điểm nó được sinh ra. Giá trị ``(X=1,Y=0,Z=0)`` sẽ khiến tất cả particle di chuyển ngang dọc theo trục X. Đối với những trường hợp như đài phun nước, nơi các particle bắn lên không trung, giá trị ``(X=0,Y=1,Z=0)`` sẽ là một điểm khởi đầu phù hợp.

.. figure:: img/particle_direction.webp
   :alt: Different values for particle direction

   Different direction values: Y-axis only (left), equal values for X and Y (middle), X and Y with gravity enabled (right)

Sau khi thiết lập hướng, bạn sẽ nhận thấy tất cả particle di chuyển theo cùng một hướng trên một đường thẳng. Thuộc tính ``Spread`` thêm sự biến thiên và tính ngẫu nhiên vào hướng của mỗi particle. Giá trị càng cao thì độ lệch khỏi đường đi ban đầu càng lớn. Giá trị ``0`` có nghĩa là hoàn toàn không có độ tỏa, trong khi giá trị ``180`` khiến particle bắn ra theo mọi hướng. Bạn có thể dùng thuộc tính này cho những mảnh vỡ trong hiệu ứng vụ nổ chẳng hạn.

.. figure:: img/particle_spread.webp
   :alt: Different values for particle spread

   No spread (left), 45 degree angle (middle), full 180 degrees (right)

Thuộc tính ``Flatness`` giới hạn độ tỏa dọc theo trục Y. Giá trị ``0`` có nghĩa là không có giới hạn, còn giá trị ``1`` sẽ loại bỏ mọi chuyển động của particle dọc theo trục Y. Các particle sẽ tỏa ra hoàn toàn "phẳng".

Bạn sẽ không thấy bất kỳ chuyển động thực tế nào cho đến khi thiết lập một số giá trị cho các thuộc tính velocity và acceleration bên dưới, vì vậy hãy cùng xem qua chúng.

Vận tốc ban đầu
~~~~~~~~~~~~~~~

Trong khi thuộc tính ``Direction`` kiểm soát hướng di chuyển của particle, ``Initial Velocity`` kiểm soát tốc độ di chuyển của nó. Thuộc tính này được tách thành ``Velocity Min`` và ``Velocity Max``, cả hai đều mặc định là ``0``, đó là lý do ban đầu bạn không thấy chuyển động nào. Ngay khi bạn đặt giá trị cho một trong hai thuộc tính này `như đã mô tả ở trên <#process-material-properties>`__, các particle sẽ bắt đầu di chuyển. Hướng được nhân với các giá trị này, vì vậy bạn có thể khiến particle di chuyển theo hướng ngược lại bằng cách đặt velocity âm.

Gia tốc
-------

Trọng lực
~~~~~~~~~

Các nhóm thuộc tính tiếp theo phối hợp chặt chẽ với nhau để kiểm soát chuyển động và rotation của particle. ``Gravity`` kéo các particle theo hướng mà nó chỉ tới, theo mặc định là thẳng xuống với cường độ bằng trọng lực của Trái Đất. Trọng lực ảnh hưởng đến mọi chuyển động của particle. Nếu game của bạn sử dụng physics và trọng lực của world có thể thay đổi trong runtime, bạn có thể sử dụng thuộc tính này để giữ cho trọng lực của game đồng bộ với trọng lực của particle. Giá trị ``Gravity`` bằng ``(X=0,Y=0,Z=0)`` có nghĩa là particle sẽ không bao giờ di chuyển nếu không thiết lập các thuộc tính chuyển động khác.

.. figure:: img/particle_gravity.webp
   :alt: Different values for particle gravity

   Left\: (X=0,Y=-9.8,Z=0), middle\: (X=0,Y=9.8,Z=0), right\: (X=4,Y=2,Z=0).

Vận tốc góc
~~~~~~~~~~~

``Angular Velocity`` kiểm soát tốc độ rotation của particle `như đã mô tả ở trên <#process-material-properties>`__. Bạn có thể đảo ngược hướng bằng cách sử dụng các số âm cho ``Velocity Min`` hoặc ``Velocity Max``. Giống như thuộc tính `Angle <#angle>`__, rotation chỉ hiển thị nếu cờ `Rotate Y <#particle-flags>`__ được bật hoặc mode ``Particle Billboard`` được chọn trong :ref:`Standard Material <doc_standard_material_3d>`.

.. note::

   Thuộc tính `Damping <#damping>`__ không ảnh hưởng đến angular velocity.

Gia tốc tuyến tính
~~~~~~~~~~~~~~~~~~

Velocity của particle là một giá trị không đổi: sau khi được thiết lập, nó không thay đổi và particle sẽ luôn di chuyển với cùng một tốc độ. Bạn có thể sử dụng thuộc tính ``Linear Accel`` để thay đổi tốc độ di chuyển trong suốt vòng đời của particle `như đã mô tả ở trên <#process-material-properties>`__. Các giá trị dương sẽ làm particle tăng tốc và di chuyển nhanh hơn. Các giá trị âm sẽ làm particle chậm lại cho đến khi dừng rồi bắt đầu di chuyển theo hướng ngược lại.

.. figure:: img/particle_accel_linear.webp
   :alt: Different values for particle linear acceleration

   Negative (top) and positive (bottom) linear acceleration

Điều quan trọng cần nhớ là khi thay đổi acceleration, chúng ta không thay đổi velocity trực tiếp mà thay đổi *mức thay đổi* của velocity. Giá trị ``0`` trên acceleration curve không dừng chuyển động của particle mà dừng sự thay đổi trong chuyển động của particle. Dù velocity của particle tại thời điểm đó là bao nhiêu, nó sẽ tiếp tục di chuyển với velocity đó cho đến khi acceleration lại thay đổi.

Gia tốc hướng tâm
~~~~~~~~~~~~~~~~~

Thuộc tính ``Radial Accel`` tạo thêm một lực giống trọng lực lên tất cả particle, với gốc của lực nằm tại vị trí hiện tại của particle system. Các giá trị âm khiến particle di chuyển về tâm, giống như lực hấp dẫn của một hành tinh tác động lên các vật thể quay quanh nó. Các giá trị dương khiến particle di chuyển ra xa tâm.

.. figure:: img/particle_accel_radial.webp
   :alt: Different values for particle radial acceleration

   Negative (left) and positive (right) radial acceleration

Gia tốc tiếp tuyến
~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_tangent.webp
   :alt: Tangents on a circle
   :align: right

   Tangents on a circle

Thuộc tính này thêm gia tốc cho particle theo hướng tiếp tuyến của một đường tròn trên mặt phẳng XZ của particle system, với gốc tại tâm của system và bán kính bằng khoảng cách giữa vị trí hiện tại của mỗi particle với tâm của system, được chiếu lên mặt phẳng đó.

Hãy cùng phân tích điều này.

Tiếp tuyến của một đường tròn là một đường thẳng "tiếp xúc" với đường tròn theo một góc vuông với bán kính của đường tròn tại điểm tiếp xúc. Đường tròn trên mặt phẳng XZ của particle system là đường tròn bạn nhìn thấy khi nhìn thẳng xuống particle system từ phía trên.

.. figure:: img/particle_accel_tangent.webp
   :alt: Tangential acceleration from above
   :align: right

   Tangential acceleration from above

``Tangential Accel`` luôn bị giới hạn trong mặt phẳng đó và không bao giờ di chuyển particle dọc theo trục Y của system. Vị trí của một particle đủ để xác định một đường tròn như vậy, trong đó khoảng cách đến tâm của system là bán kính nếu bỏ qua thành phần Y của vector.

Thuộc tính ``Tangential Accel`` sẽ khiến các hạt quay quanh tâm của hệ thống hạt, nhưng bán kính sẽ liên tục tăng. Khi nhìn từ trên xuống, các hạt sẽ di chuyển ra xa tâm theo hình xoắn ốc. Các giá trị âm sẽ đảo ngược hướng.

Giảm chấn
~~~~~~~~~

Thuộc tính ``Damping`` dần dần dừng mọi chuyển động. Ở mỗi frame, chuyển động của một hạt sẽ chậm lại một chút, trừ khi tổng gia tốc lớn hơn hiệu ứng giảm chấn. Nếu không, hạt sẽ tiếp tục chậm lại cho đến khi hoàn toàn không chuyển động. Giá trị càng lớn thì thời gian đưa các hạt đến trạng thái dừng hẳn càng ngắn.

Tương tác với attractor
~~~~~~~~~~~~~~~~~~~~~~~

Nếu muốn hệ thống hạt tương tác với :ref:`particle attractors <doc_3d_particles_attractors>`, bạn phải bật thuộc tính ``Enabled``. Khi bị tắt, hệ thống hạt sẽ bỏ qua tất cả particle attractor.

Hiển thị
--------

Tỷ lệ
~~~~~

``Scale`` điều khiển kích thước của một hạt `như đã mô tả ở trên <#process-material-properties>`__. Bạn có thể đặt các giá trị khác nhau cho ``Scale Min`` và ``Scale Max`` để ngẫu nhiên hóa kích thước của từng hạt. Không cho phép các giá trị âm, vì vậy bạn không thể lật các hạt bằng thuộc tính này. Nếu phát hạt dưới dạng billboard, thuộc tính ``Keep Size`` trên :ref:`Standard Material <doc_standard_material_3d>` trong các draw pass của bạn phải được bật thì việc scale mới có hiệu lực.

Màu
~~~

Thuộc tính ``Color`` điều khiển màu ban đầu của một hạt. Nó chỉ có hiệu lực sau khi thuộc tính ``Use As Albedo`` trong nhóm ``Vertex Color`` của :ref:`Standard Material <doc_standard_material_3d>` được bật. Thuộc tính này được nhân với màu đến từ thuộc tính ``Color`` hoặc ``Texture`` của chính particle material.

.. figure:: img/particle_ramp.webp
   :alt: Particle color ramp
   :align: right

   Setting up a color ramp

Có hai thuộc tính ``Ramp`` trong nhóm ``Color``. Các thuộc tính này cho phép bạn xác định một dải màu dùng để thiết lập màu của hạt. Thuộc tính ``Color Ramp`` thay đổi màu của hạt trong suốt vòng đời của nó. Nó di chuyển qua toàn bộ dải màu bạn đã xác định. Thuộc tính ``Color Initial Ramp`` chọn màu ban đầu của hạt từ một vị trí ngẫu nhiên trên color ramp.

Để thiết lập color ramp, hãy nhấp vào ô bên cạnh tên thuộc tính và chọn ``New GradientTexture1D`` từ menu thả xuống. Nhấp lại vào ô đó để mở thông tin chi tiết của texture. Tìm thuộc tính ``Gradient``, nhấp vào ô bên cạnh thuộc tính này và chọn ``New Gradient``. Nhấp lại vào ô đó và bạn sẽ thấy một dải màu. Nhấp vào bất kỳ vị trí nào trên dải màu để chèn một marker mới. Bạn có thể di chuyển marker bằng chuột và xóa marker bằng cách nhấp chuột phải. Khi một marker được chọn, bạn có thể sử dụng color picker bên cạnh dải màu để thay đổi màu của marker.

Biến thiên sắc độ
~~~~~~~~~~~~~~~~~

Giống như thuộc tính ``Color``, ``Hue Variation`` điều khiển màu của một hạt, nhưng theo cách khác. Nó không thực hiện việc này bằng cách trực tiếp thiết lập các giá trị màu, mà bằng cách *dịch chuyển sắc độ của màu*.

Sắc độ mô tả sắc tố của một màu: đỏ, cam, vàng, xanh lá và vân vân. Nó không cho biết độ sáng hay độ bão hòa của màu. Thuộc tính ``Hue Variation`` điều khiển phạm vi các sắc độ khả dụng `như đã mô tả ở trên <#process-material-properties>`__.

Nó hoạt động dựa trên màu hiện tại của hạt. Các giá trị bạn đặt cho ``Variation Min`` và ``Variation Max`` điều khiển khoảng cách mà sắc độ được phép dịch chuyển theo mỗi hướng. Giá trị cao hơn tạo ra nhiều biến thiên màu hơn, trong khi giá trị thấp giới hạn các màu khả dụng ở những màu gần nhất với màu gốc.

.. figure:: img/particle_hue.webp
   :alt: Different values for hue variation

   Different values for hue variation, both times with blue as base color: 0.6 (left) and 0.1 (right)

.. _doc_process_material_properties_animation:

Animation
~~~~~~~~~

Nhóm thuộc tính ``Animation`` điều khiển hành vi của các animation sprite sheet trong :ref:`Standard Material <doc_standard_material_3d>` của hạt. Các giá trị ``Min``, ``Max`` và ``Curve`` hoạt động `như đã mô tả ở trên <#process-material-properties>`__.

Sprite sheet animated là một texture chứa nhiều hình ảnh nhỏ hơn được sắp xếp trên một lưới. Các hình ảnh được hiển thị nối tiếp nhau nhanh đến mức kết hợp lại thành một animation ngắn, giống như flipbook. Bạn có thể dùng chúng cho các hạt animated như khói hoặc lửa. Sau đây là các bước để tạo một hệ thống hạt animated:

.. figure:: img/particle_sprite.webp
   :alt: A sprite sheet
   :align: right

   An 8x8 animated smoke sprite sheet

#. Import một texture sprite sheet vào engine. Nếu bạn không có sẵn, bạn có thể tải xuống :download:`high-res version of the example image <img/particle_sprite_smoke.webp>`. #. Thiết lập một hệ thống hạt có ít nhất một draw pass và gán ``Standard Material`` cho mesh trong draw pass đó. #. Gán sprite sheet cho thuộc tính ``Texture`` trong nhóm ``Albedo`` #. Đặt thuộc tính ``Billboard`` của material thành ``Particle Billboard``. Việc này làm cho nhóm ``Particles Anim`` khả dụng trong material. #. Đặt ``H Frames`` thành số cột và ``V Frames`` thành số hàng trong sprite sheet. #. Bật ``Loop`` nếu bạn muốn animation tiếp tục lặp lại.

Vậy là xong phần Standard Material. Bạn sẽ chưa thấy animation ngay lập tức. Đây là lúc các thuộc tính ``Animation`` phát huy tác dụng. Các thuộc tính ``Speed`` điều khiển tốc độ animation của sprite sheet. Đặt ``Speed Min`` và ``Speed Max`` thành ``1`` và bạn sẽ thấy animation phát. Các thuộc tính ``Offset`` điều khiển vị trí bắt đầu của animation trên một hạt mới được tạo. Theo mặc định, đó luôn là hình ảnh đầu tiên trong chuỗi. Bạn có thể thêm một chút đa dạng bằng cách thay đổi ``Offset Min`` và ``Offset Max`` để ngẫu nhiên hóa vị trí bắt đầu.

.. figure:: img/particle_animate.webp
   :alt: Animated particles

   Three different particle systems using the same smoke sprite sheet

Tùy thuộc vào số lượng hình ảnh trong sprite sheet và thời gian hạt tồn tại, animation có thể không trông mượt mà. Mối quan hệ giữa vòng đời của hạt, tốc độ animation và số lượng hình ảnh trong sprite sheet là:

.. note::

   Ở tốc độ animation ``1.0``, animation sẽ đến hình ảnh cuối cùng trong chuỗi đúng lúc vòng đời của hạt kết thúc.

   .. math::
      Animation\ FPS = \frac{Number\ of\ images}{Lifetime}

Nếu sprite sheet của bạn chứa 64 (8x8) hình ảnh và vòng đời của hạt được đặt thành ``1 second``, animation sẽ rất mượt ở **64 FPS** (1 giây / 64 hình ảnh). Nếu vòng đời được đặt thành ``2 seconds``, animation vẫn khá mượt ở **32 FPS**. Nhưng nếu hạt tồn tại trong ``8 seconds``, animation sẽ giật thấy rõ ở **8 FPS**. Để animation trở nên mượt lại, bạn cần tăng tốc độ animation lên khoảng ``3`` để đạt framerate chấp nhận được.

.. figure:: img/particle_animate_lifetime.webp
   :alt: Animated particles lifetimes

   The same particle system at different lifetimes: 1 second (left), 2 seconds (middle), 8 seconds (right)

Lưu ý rằng **Fixed FPS** của node GPUParticles3D cũng ảnh hưởng đến việc phát animation. Để animation phát mượt mà, bạn nên đặt giá trị này thành 0 để hạt được mô phỏng trong mỗi frame được render. Nếu đây không phải là lựa chọn phù hợp với trường hợp sử dụng của bạn, hãy đặt **Fixed FPS** bằng framerate hiệu dụng được animation flipbook sử dụng (xem công thức ở trên).

.. _doc_process_material_properties_turbulence:

Turbulence
~~~~~~~~~~

Turbulence thêm noise vào chuyển động của hạt, tạo ra các pattern thú vị và sống động. Bật ô bên cạnh thuộc tính ``Enabled`` để kích hoạt. Một số thuộc tính mới sẽ xuất hiện, dùng để điều khiển tốc độ chuyển động, pattern noise và mức độ ảnh hưởng tổng thể lên hệ thống hạt. Bạn có thể tìm thấy phần giải thích chi tiết về các thuộc tính này trong phần
:ref:`particle turbulence <doc_3d_particles_turbulence>`.

.. _doc_process_material_properties_subemitter:

Va chạm
-------

Thuộc tính ``Mode`` điều khiển cách thức và việc các emitter có va chạm với các node particle collision hay không. Đặt thành ``Disabled`` để tắt mọi va chạm cho hệ thống hạt này. Đặt thành ``Hide On Contact`` nếu muốn các hạt biến mất ngay khi va chạm. Đặt thành ``Constant`` để các hạt va chạm và nảy xung quanh. Bạn sẽ thấy hai thuộc tính mới xuất hiện trong inspector. Chúng điều khiển cách các hạt hoạt động trong các sự kiện va chạm.

Giá trị ``Friction`` cao sẽ giảm hiện tượng trượt dọc theo các bề mặt. Điều này đặc biệt hữu ích nếu các hạt va chạm với các bề mặt dốc và bạn muốn chúng đứng yên thay vì trượt xuống tận đáy, chẳng hạn như tuyết rơi trên núi. Giá trị ``Bounce`` cao sẽ khiến các hạt nảy khỏi những bề mặt mà chúng va chạm, giống như các quả bóng cao su trên sàn cứng.

Nếu thuộc tính ``Use Scale`` được bật, :ref:`collision base size <doc_3d_particles_properties_collision>` sẽ được nhân với `scale hiện tại <#scale>`__ của hạt. Bạn có thể dùng điều này để đảm bảo kích thước được render và kích thước va chạm khớp nhau đối với các hạt có scale ngẫu nhiên hoặc scale thay đổi theo thời gian.

Bạn có thể tìm hiểu thêm về va chạm của hạt trong phần :ref:`Collisions <doc_3d_particles_collision>` của tài liệu này.

Sub-emitter
-----------

.. figure:: img/particle_sub_mode.webp
   :alt: Sub-emitter modes
   :align: right

   The available sub-emitter modes

Thuộc tính ``Mode`` điều khiển cách thức và thời điểm sub-emitter được tạo. Đặt thành ``Disabled`` để không bao giờ tạo sub-emitter. Đặt thành ``Constant`` để sub-emitter được tạo liên tục với tốc độ không đổi. Thuộc tính ``Frequency`` điều khiển tần suất việc này xảy ra trong khoảng thời gian một giây. Đặt mode thành ``At End`` để sub-emitter được tạo vào cuối vòng đời của hạt cha, ngay trước khi hạt đó bị hủy. Thuộc tính ``Amount At End`` điều khiển số lượng sub-emitter sẽ được tạo. Đặt mode thành ``At Collision`` để sub-emitter được tạo khi một hạt va chạm với môi trường. Thuộc tính ``Amount At Collision`` điều khiển số lượng sub-emitter sẽ được tạo.

Khi thuộc tính ``Keep Velocity`` được bật, sub-emitter mới được tạo sẽ bắt đầu với vận tốc của hạt cha tại thời điểm sub-emitter được tạo.

Xem phần :ref:`Sub-emitters <doc_3d_particles_subemitters>` trong tài liệu này để biết giải thích chi tiết về cách thêm sub-emitter vào một hệ thống hạt.

Tùy chỉnh process material
--------------------------

Nếu cần thay đổi hoặc triển khai các hành vi mới trong mã shader, bạn có thể thực hiện việc này bằng cách chuyển đổi ParticleProcessMaterial hiện tại thành một :ref:`class_ShaderMaterial`. Các thuộc tính hiện có sẽ được giữ nguyên trong quá trình chuyển đổi. Những tính năng được bật cũng sẽ ảnh hưởng đến nội dung có trong mã shader sau khi chuyển đổi.

Để thực hiện việc này, hãy nhấp chuột phải vào material trong dock FileSystem và chọn **Convert to ShaderMaterial**. Bạn cũng có thể thực hiện việc này bằng cách nhấp chuột phải vào bất kỳ thuộc tính nào đang chứa tham chiếu đến material trong inspector.
