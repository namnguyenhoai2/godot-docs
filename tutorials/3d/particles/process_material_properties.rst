.. _doc_process_material_properties:

Xử lý các thuộc tính vật liệu
-----------------------------

.. figure:: img/particle_minmaxcurve.webp
   :alt: Các thuộc tính của ParticleProcessMaterial
   :align: right

   Các thuộc tính min, max và đường cong

Các thuộc tính trong vật liệu này kiểm soát cách các particle hoạt động và thay đổi trong suốt vòng đời của chúng. Nhiều thuộc tính có các giá trị ``Min``, ``Max`` và ``Curve``, cho phép bạn tinh chỉnh hành vi của chúng. Mối quan hệ giữa các giá trị này như sau: Khi một particle được sinh ra, thuộc tính sẽ được đặt thành một giá trị ngẫu nhiên nằm giữa ``Min`` và ``Max``. Nếu ``Min`` và ``Max`` giống nhau, giá trị sẽ luôn giống nhau đối với mọi particle. Nếu ``Curve`` cũng được đặt, giá trị của thuộc tính sẽ được nhân với giá trị của đường cong tại điểm hiện tại trong vòng đời của particle. Sử dụng đường cong để thay đổi một thuộc tính trong suốt vòng đời của particle. Bằng cách này, bạn có thể biểu diễn những hành vi rất phức tạp.

.. note::
  Trang này trình bày cụ thể cách sử dụng ParticleProcessMaterial cho các cảnh 3D. Để biết thông tin về cách sử dụng nó trong một Scene 2D, hãy xem :ref:`doc_particle_process_material_2d`.

Thời gian
~~~~~~~~~

Thuộc tính ``Lifetime Randomness`` kiểm soát mức độ ngẫu nhiên được áp dụng cho vòng đời của từng particle. Giá trị ``0`` nghĩa là hoàn toàn không có tính ngẫu nhiên và mọi particle sống trong cùng một khoảng thời gian, được đặt bởi thuộc tính :ref:`Lifetime <doc_3d_particles_properties_time>`. Giá trị ``1`` nghĩa là vòng đời của particle hoàn toàn ngẫu nhiên trong phạm vi [0.0, ``Lifetime``].

Cờ particle
-----------

Thuộc tính ``Align Y`` căn trục Y của mỗi particle theo vận tốc của nó. Bật thuộc tính này tương đương với việc đặt thuộc tính :ref:`Transform Align <doc_3d_particles_properties_draw>` thành ``Y to Velocity``.

Thuộc tính ``Rotate Y`` hoạt động cùng với các thuộc tính trong các nhóm `Angle <#angle>`__ và `Angular Velocity <#angular-velocity>`__ để kiểm soát việc xoay particle. Phải bật ``Rotate Y`` nếu bạn muốn áp dụng bất kỳ phép xoay nào cho particle. Ngoại lệ là các particle sử dụng :ref:`Standard Material <doc_standard_material_3d>` trong đó thuộc tính ``Billboard`` được đặt thành ``Particle Billboard``. Trong trường hợp đó, particle vẫn xoay ngay cả khi chưa bật ``Rotate Y``.

Khi thuộc tính ``Disable Z`` được bật, particle sẽ không di chuyển dọc theo trục Z. Việc đó là trục Z cục bộ của hệ thống particle hay trục Z của thế giới được xác định bởi thuộc tính :ref:`Local Coords <doc_3d_particles_properties_draw>`.

Thuộc tính ``Damping as Friction`` thay đổi hành vi của damping từ giảm tốc không đổi thành giảm tốc dựa trên tốc độ.

Sinh particle
-------------

.. _doc_process_material_properties_shapes:

Hình dạng phát xạ
~~~~~~~~~~~~~~~~~

Particle có thể phát ra từ một điểm duy nhất trong không gian hoặc theo cách lấp đầy một hình dạng. Thuộc tính ``Shape`` kiểm soát hình dạng đó. ``Point`` là giá trị mặc định. Mọi particle đều phát ra từ một điểm duy nhất ở giữa hệ thống particle. Khi được đặt thành ``Sphere`` hoặc ``Box``, particle sẽ phát ra theo cách lấp đầy đều một hình cầu hoặc hình hộp. Bạn có toàn quyền kiểm soát kích thước của các hình dạng này. ``Sphere Surface`` hoạt động giống ``Sphere``, nhưng thay vì lấp đầy hình dạng, mọi particle sẽ sinh ra trên bề mặt hình cầu.

.. figure:: img/particle_shapes_simple.webp
   :alt: Các hình dạng phát xạ particle đơn giản

   Particle phát ra từ một điểm (bên trái), trong một hình cầu (ở giữa) và trong một hình hộp (bên phải)

.. figure:: img/particle_ring.webp
   :alt: Hệ thống particle hình vòng
   :align: right

   Một hệ thống particle hình vòng

Hình dạng phát xạ ``Ring`` khiến particle phát ra theo hình vòng. Bạn có thể kiểm soát hướng của vòng bằng cách thay đổi thuộc tính ``Ring Axis``. ``Ring Height`` kiểm soát độ dày của vòng dọc theo trục của nó. ``Ring Radius`` và ``Ring Inner Radius`` kiểm soát độ rộng của vòng và kích thước của lỗ ở giữa. Hình ảnh cho thấy một hệ thống particle có bán kính ``2`` và bán kính trong ``1.5``, với trục hướng theo trục Z toàn cục.

Ngoài các hình dạng tương đối đơn giản này, bạn có thể chọn tùy chọn ``Points`` hoặc ``Directed Points`` để tạo các hình dạng phát xạ rất phức tạp. Xem
phần :ref:`Complex emission shapes <doc_3d_particles_complex_shapes>` để biết giải thích chi tiết về cách thiết lập chúng.

Góc
~~~

Thuộc tính ``Angle`` kiểm soát góc xoay ban đầu của particle `như đã mô tả ở trên <#process-material-properties>`__. Để thuộc tính này thực sự ảnh hưởng đến particle, bạn phải bật một trong hai thuộc tính: `Rotate Y <#particle-flags>`__ xoay particle quanh trục Y của hệ thống particle. Thuộc tính ``Billboard`` trong :ref:`Standard Material <doc_standard_material_3d>`, nếu được đặt thành ``Particle Billboard``, sẽ xoay particle quanh trục hướng từ particle đến camera.

Hướng
~~~~~

.. note::

   Chỉ riêng thuộc tính ``Direction`` thì chưa đủ để thấy particle di chuyển. Bất kỳ giá trị nào bạn đặt ở đây chỉ có hiệu lực khi các thuộc tính velocity hoặc acceleration cũng được đặt.

Thuộc tính ``Direction`` là một vector kiểm soát hướng di chuyển của từng particle tại thời điểm nó được sinh ra. Giá trị ``(X=1,Y=0,Z=0)`` sẽ khiến mọi particle di chuyển ngang dọc theo trục X. Với một thứ như vòi phun nước, nơi particle bắn lên không trung, giá trị ``(X=0,Y=1,Z=0)`` sẽ là điểm khởi đầu phù hợp.

.. figure:: img/particle_direction.webp
   :alt: Các giá trị hướng particle khác nhau

   Các giá trị hướng khác nhau: chỉ trục Y (bên trái), các giá trị X và Y bằng nhau (ở giữa), X và Y khi bật gravity (bên phải)

Sau khi đặt hướng, bạn sẽ nhận thấy mọi particle di chuyển cùng hướng theo một đường thẳng. Thuộc tính ``Spread`` thêm sự biến thiên và tính ngẫu nhiên vào hướng của từng particle. Giá trị càng cao thì độ lệch khỏi đường đi ban đầu càng lớn. Giá trị ``0`` nghĩa là hoàn toàn không có độ phân tán, trong khi giá trị ``180`` khiến particle bắn ra theo mọi hướng. Bạn có thể dùng thuộc tính này cho những thứ như các mảnh vỡ trong hiệu ứng vụ nổ.

.. figure:: img/particle_spread.webp
   :alt: Các giá trị độ phân tán particle khác nhau

   Không phân tán (bên trái), góc 45 độ (ở giữa), toàn bộ 180 độ (bên phải)

Thuộc tính ``Flatness`` giới hạn độ phân tán dọc theo trục Y. Giá trị ``0`` nghĩa là không có giới hạn, còn giá trị ``1`` sẽ loại bỏ mọi chuyển động của particle dọc theo trục Y. Particle sẽ phân tán hoàn toàn theo dạng "phẳng".

Bạn sẽ không thấy chuyển động thực sự nào cho đến khi cũng đặt một số giá trị cho các thuộc tính velocity và acceleration bên dưới, vì vậy hãy cùng xem xét chúng tiếp theo.

Vận tốc ban đầu
~~~~~~~~~~~~~~~

Trong khi thuộc tính ``Direction`` kiểm soát hướng di chuyển của particle, ``Initial Velocity`` kiểm soát tốc độ di chuyển. Thuộc tính này được tách thành ``Velocity Min`` và ``Velocity Max``, cả hai đều được đặt thành ``0`` theo mặc định, đó là lý do ban đầu bạn không thấy chuyển động nào. Ngay khi bạn đặt giá trị cho một trong hai thuộc tính này `như đã mô tả ở trên <#process-material-properties>`__, particle sẽ bắt đầu di chuyển. Hướng được nhân với các giá trị này, vì vậy bạn có thể khiến particle di chuyển theo hướng ngược lại bằng cách đặt vận tốc âm.

Gia tốc
-------

Trọng lực
~~~~~~~~~

Một vài nhóm thuộc tính tiếp theo phối hợp chặt chẽ với nhau để điều khiển chuyển động và phép xoay của particle. ``Gravity`` kéo particle theo hướng mà nó chỉ tới, mặc định là thẳng xuống với cường độ bằng trọng lực của Trái Đất. Trọng lực ảnh hưởng đến mọi chuyển động của particle. Nếu game của bạn sử dụng physics và trọng lực của thế giới có thể thay đổi trong runtime, bạn có thể dùng thuộc tính này để giữ trọng lực của game đồng bộ với trọng lực của particle. Giá trị ``Gravity`` bằng ``(X=0,Y=0,Z=0)`` có nghĩa là particle sẽ không bao giờ di chuyển nếu không đặt các thuộc tính chuyển động khác.

.. figure:: img/particle_gravity.webp
   :alt: Các giá trị khác nhau của trọng lực particle

   Bên trái\: (X=0,Y=-9.8,Z=0), ở giữa\: (X=0,Y=9.8,Z=0), bên phải\: (X=4,Y=2,Z=0).

Vận tốc góc
~~~~~~~~~~~

``Angular Velocity`` điều khiển tốc độ xoay của particle `như đã mô tả ở trên <#process-material-properties>`__. Bạn có thể đảo hướng bằng cách sử dụng các số âm cho ``Velocity Min`` hoặc ``Velocity Max``. Giống như thuộc tính `Angle <#angle>`__, phép xoay chỉ hiển thị nếu cờ `Rotate Y <#particle-flags>`__ được bật hoặc chế độ ``Particle Billboard`` được chọn trong :ref:`Standard Material <doc_standard_material_3d>`.

.. note::

   Thuộc tính `Damping <#damping>`__ không ảnh hưởng đến vận tốc góc.

Gia tốc tuyến tính
~~~~~~~~~~~~~~~~~~

Vận tốc của particle là một giá trị không đổi: sau khi được thiết lập, nó không thay đổi và particle luôn di chuyển với cùng một tốc độ. Bạn có thể sử dụng thuộc tính ``Linear Accel`` để thay đổi tốc độ chuyển động trong suốt vòng đời của particle `như đã mô tả ở trên <#process-material-properties>`__. Các giá trị dương sẽ tăng tốc particle và khiến nó di chuyển nhanh hơn. Các giá trị âm sẽ làm particle chậm lại cho đến khi dừng và bắt đầu di chuyển theo hướng ngược lại.

.. figure:: img/particle_accel_linear.webp
   :alt: Các giá trị khác nhau của gia tốc tuyến tính particle

   Gia tốc tuyến tính âm (trên) và dương (dưới)

Điều quan trọng cần nhớ là khi thay đổi gia tốc, chúng ta không trực tiếp thay đổi vận tốc mà thay đổi *change* của vận tốc. Giá trị ``0`` trên đường cong gia tốc không dừng chuyển động của particle mà dừng sự thay đổi trong chuyển động của particle. Dù vận tốc của particle tại thời điểm đó là bao nhiêu, nó sẽ tiếp tục di chuyển với vận tốc đó cho đến khi gia tốc lại thay đổi.

Gia tốc hướng tâm
~~~~~~~~~~~~~~~~~

Thuộc tính ``Radial Accel`` thêm một lực giống trọng lực vào tất cả particle, với điểm gốc của lực nằm tại vị trí hiện tại của particle system. Các giá trị âm khiến particle di chuyển về phía tâm, giống như lực hấp dẫn của một hành tinh tác động lên các vật thể trên quỹ đạo của nó. Các giá trị dương khiến particle di chuyển ra xa tâm.

.. figure:: img/particle_accel_radial.webp
   :alt: Các giá trị khác nhau của gia tốc hướng tâm particle

   Gia tốc hướng tâm âm (trái) và dương (phải)

Gia tốc tiếp tuyến
~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_tangent.webp
   :alt: Các tiếp tuyến trên một đường tròn
   :align: right

   Các tiếp tuyến trên một đường tròn

Thuộc tính này thêm gia tốc cho particle theo hướng tiếp tuyến của một đường tròn trên mặt phẳng XZ của particle system, với tâm tại tâm của system và bán kính là khoảng cách giữa vị trí hiện tại của từng particle với tâm của system, được chiếu lên mặt phẳng đó.

Hãy phân tích từng phần.

Tiếp tuyến của một đường tròn là một đường thẳng "tiếp xúc" với đường tròn tại một góc vuông so với bán kính của đường tròn ở điểm tiếp xúc. Đường tròn trên mặt phẳng XZ của particle system là đường tròn bạn nhìn thấy khi nhìn thẳng xuống particle system từ phía trên.

.. figure:: img/particle_accel_tangent.webp
   :alt: Gia tốc tiếp tuyến nhìn từ phía trên
   :align: right

   Gia tốc tiếp tuyến nhìn từ phía trên

``Tangential Accel`` luôn bị giới hạn trong mặt phẳng đó và không bao giờ di chuyển particle dọc theo trục Y của system. Chỉ cần vị trí của một particle là đủ để xác định một đường tròn như vậy, trong đó khoảng cách đến tâm của system là bán kính nếu bỏ qua thành phần Y của vector.

Thuộc tính ``Tangential Accel`` sẽ khiến particle quay quanh tâm của particle system, nhưng bán kính sẽ liên tục tăng. Khi nhìn từ phía trên, particle sẽ di chuyển ra xa tâm theo hình xoắn ốc. Các giá trị âm sẽ đảo ngược hướng.

Damping
~~~~~~~

Thuộc tính ``Damping`` dần dần dừng mọi chuyển động. Ở mỗi frame, chuyển động của particle chậm lại một chút, trừ khi tổng gia tốc lớn hơn hiệu ứng damping. Nếu không, particle sẽ tiếp tục chậm lại cho đến khi hoàn toàn không di chuyển. Giá trị càng lớn thì thời gian đưa particle về trạng thái dừng hoàn toàn càng ngắn.

Tương tác với attractor
~~~~~~~~~~~~~~~~~~~~~~~

Nếu muốn particle system tương tác với :ref:`particle attractors <doc_3d_particles_attractors>`, bạn phải đánh dấu thuộc tính ``Enabled``. Khi bị tắt, particle system sẽ bỏ qua mọi particle attractor.

Hiển thị
--------

Tỷ lệ
~~~~~

``Scale`` điều khiển kích thước của particle `như đã mô tả ở trên <#process-material-properties>`__. Bạn có thể đặt các giá trị khác nhau cho ``Scale Min`` và ``Scale Max`` để tạo kích thước ngẫu nhiên cho từng particle. Không được phép sử dụng các giá trị âm, vì vậy bạn không thể lật particle bằng thuộc tính này. Nếu phát particle dưới dạng billboard, thuộc tính ``Keep Size`` trên :ref:`Standard Material <doc_standard_material_3d>` trong các draw pass phải được bật thì việc scale mới có hiệu lực.

Màu
~~~

Thuộc tính ``Color`` điều khiển màu ban đầu của particle. Nó chỉ có hiệu lực sau khi thuộc tính ``Use As Albedo`` trong nhóm ``Vertex Color`` của :ref:`Standard Material <doc_standard_material_3d>` được bật. Thuộc tính này được nhân với màu lấy từ thuộc tính ``Color`` hoặc ``Texture`` của material riêng của particle.

.. figure:: img/particle_ramp.webp
   :alt: Dải màu của particle
   :align: right

   Thiết lập dải màu

Có hai thuộc tính ``Ramp`` trong nhóm ``Color``. Các thuộc tính này cho phép bạn xác định một dải màu dùng để đặt màu cho particle. Thuộc tính ``Color Ramp`` thay đổi màu của particle trong suốt vòng đời của nó. Nó đi qua toàn bộ dải màu bạn đã xác định. Thuộc tính ``Color Initial Ramp`` chọn màu ban đầu của particle từ một vị trí ngẫu nhiên trên dải màu.

Để thiết lập dải màu, hãy nhấp vào ô bên cạnh tên thuộc tính và chọn ``New GradientTexture1D`` từ menu thả xuống. Nhấp lại vào ô để mở thông tin chi tiết của texture. Tìm thuộc tính ``Gradient``, nhấp vào ô bên cạnh thuộc tính đó và chọn ``New Gradient``. Nhấp lại vào ô đó để xem một dải màu. Nhấp vào bất kỳ vị trí nào trên dải màu để chèn marker mới. Bạn có thể di chuyển marker bằng chuột và xóa marker bằng cách nhấp chuột phải. Khi một marker được chọn, bạn có thể dùng bộ chọn màu bên cạnh dải màu để thay đổi màu của marker.

Biến thiên sắc độ
~~~~~~~~~~~~~~~~~

Giống như thuộc tính ``Color``, ``Hue Variation`` điều khiển màu của particle, nhưng theo một cách khác. Nó không thực hiện bằng cách đặt trực tiếp các giá trị màu mà bằng cách *dịch chuyển sắc độ của màu*.

Hue mô tả sắc tố của một màu: đỏ, cam, vàng, xanh lá cây, v.v. Nó không cho biết gì về độ sáng hoặc độ bão hòa của màu. Thuộc tính ``Hue Variation`` kiểm soát phạm vi các sắc độ khả dụng `như đã mô tả ở trên <#process-material-properties>`__.

Thuộc tính này hoạt động dựa trên màu hiện tại của particle. Các giá trị bạn đặt cho ``Variation Min`` và ``Variation Max`` kiểm soát mức độ hue được phép dịch chuyển theo mỗi hướng. Giá trị cao hơn tạo ra nhiều biến thể màu hơn, trong khi giá trị thấp giới hạn các màu khả dụng ở những màu gần nhất với màu gốc.

.. figure:: img/particle_hue.webp
   :alt: Các giá trị khác nhau của biến thiên hue

   Các giá trị khác nhau của biến thiên hue, cả hai lần đều sử dụng màu xanh dương làm màu cơ sở: 0.6 (bên trái) và 0.1 (bên phải)

.. _doc_process_material_properties_animation:

Animation
~~~~~~~~~

Nhóm thuộc tính ``Animation`` kiểm soát hoạt động của các animation sprite sheet trong :ref:`Standard Material <doc_standard_material_3d>` của particle. Các giá trị ``Min``, ``Max`` và ``Curve`` hoạt động `như đã mô tả ở trên <#process-material-properties>`__.

Sprite sheet được animate là một texture chứa nhiều hình ảnh nhỏ hơn được sắp xếp trên một lưới. Các hình ảnh được hiển thị lần lượt nhanh đến mức kết hợp lại thành một animation ngắn, giống như sách lật. Bạn có thể dùng chúng cho các particle được animate như khói hoặc lửa. Sau đây là các bước để tạo một hệ thống particle được animate:

.. figure:: img/particle_sprite.webp
   :alt: Một sprite sheet
   :align: right

   Một sprite sheet khói được animate 8x8

#. Import texture sprite sheet vào engine. Nếu bạn không có sẵn, bạn có thể tải xuống :download:`phiên bản độ phân giải cao của hình ảnh mẫu <img/particle_sprite_smoke.webp>`.
#. Thiết lập một hệ thống particle với ít nhất một draw pass và gán một ``Standard Material`` cho mesh trong draw pass đó.
#. Gán sprite sheet cho thuộc tính ``Texture`` trong nhóm ``Albedo``
#. Đặt thuộc tính ``Billboard`` của material thành ``Particle Billboard``. Khi đó, nhóm ``Particles Anim`` sẽ khả dụng trong material.
#. Đặt ``H Frames`` thành số cột và ``V Frames`` thành số hàng trong sprite sheet.
#. Chọn ``Loop`` nếu bạn muốn animation tiếp tục lặp lại.

Vậy là xong phần Standard Material. Bạn sẽ chưa thấy animation ngay lập tức. Đây là lúc các thuộc tính ``Animation`` phát huy tác dụng. Các thuộc tính ``Speed`` kiểm soát tốc độ animate của sprite sheet. Đặt ``Speed Min`` và ``Speed Max`` thành ``1`` thì bạn sẽ thấy animation đang phát. Các thuộc tính ``Offset`` kiểm soát vị trí bắt đầu của animation trên một particle mới được spawn. Theo mặc định, nó luôn là hình ảnh đầu tiên trong chuỗi. Bạn có thể tạo thêm sự đa dạng bằng cách thay đổi ``Offset Min`` và ``Offset Max`` để ngẫu nhiên hóa vị trí bắt đầu.

.. figure:: img/particle_animate.webp
   :alt: Các particle được animate

   Ba hệ thống particle khác nhau sử dụng cùng một sprite sheet khói

Tùy thuộc vào số lượng hình ảnh trong sprite sheet và thời gian particle tồn tại, animation có thể trông không mượt. Mối quan hệ giữa thời gian tồn tại của particle, tốc độ animation và số lượng hình ảnh trong sprite sheet như sau:

.. note::

   Ở tốc độ animation ``1.0``, animation sẽ đến hình ảnh cuối cùng trong chuỗi đúng lúc thời gian tồn tại của particle kết thúc.

   .. math::
      Animation\ FPS = \frac{Number\ of\ images}{Lifetime}

Nếu sprite sheet của bạn chứa 64 hình ảnh (8x8) và thời gian tồn tại của particle được đặt thành ``1 second``, animation sẽ rất mượt ở **64 FPS** (1 giây / 64 hình ảnh). Nếu thời gian tồn tại được đặt thành ``2 seconds``, animation vẫn khá mượt ở **32 FPS**. Nhưng nếu particle tồn tại trong ``8 seconds``, animation sẽ giật thấy rõ ở **8 FPS**. Để animation mượt trở lại, bạn cần tăng tốc độ animation lên khoảng ``3`` để đạt tốc độ khung hình chấp nhận được.

.. figure:: img/particle_animate_lifetime.webp
   :alt: Thời gian tồn tại của các particle được animate

   Cùng một hệ thống particle với các thời gian tồn tại khác nhau: 1 giây (bên trái), 2 giây (ở giữa), 8 giây (bên phải)

Lưu ý rằng **Fixed FPS** của node GPUParticles3D cũng ảnh hưởng đến việc phát animation. Để animation phát mượt, bạn nên đặt giá trị này thành 0 để particle được mô phỏng ở mọi frame được render. Nếu đây không phải là lựa chọn phù hợp với trường hợp sử dụng của bạn, hãy đặt **Fixed FPS** bằng tốc độ khung hình hiệu dụng được animation flipbook sử dụng (xem công thức ở trên).

.. _doc_process_material_properties_turbulence:

Turbulence
~~~~~~~~~~

Turbulence thêm noise vào chuyển động của particle, tạo ra các mẫu thú vị và sống động. Chọn ô bên cạnh thuộc tính ``Enabled`` để kích hoạt. Một số thuộc tính mới sẽ xuất hiện, dùng để kiểm soát tốc độ chuyển động, mẫu noise và mức độ ảnh hưởng tổng thể lên hệ thống particle. Bạn có thể tìm thấy phần giải thích chi tiết về các thuộc tính này trong phần
:ref:`particle turbulence <doc_3d_particles_turbulence>`.

.. _doc_process_material_properties_subemitter:

Collision
---------

Thuộc tính ``Mode`` kiểm soát cách thức và việc các emitter có va chạm với các node particle collision hay không. Đặt thành ``Disabled`` để tắt mọi va chạm cho hệ thống particle này. Đặt thành ``Hide On Contact`` nếu bạn muốn particle biến mất ngay khi va chạm. Đặt thành ``Constant`` để particle va chạm và nảy xung quanh. Bạn sẽ thấy hai thuộc tính mới xuất hiện trong inspector. Chúng kiểm soát cách particle hoạt động trong các sự kiện va chạm.

Giá trị ``Friction`` cao sẽ giảm hiện tượng trượt dọc theo các bề mặt. Điều này đặc biệt hữu ích nếu particle va chạm với các bề mặt dốc và bạn muốn chúng đứng yên thay vì trượt xuống tận đáy, chẳng hạn như tuyết rơi trên núi. Giá trị ``Bounce`` cao sẽ khiến particle nảy khỏi các bề mặt mà chúng va chạm, giống như những quả bóng cao su trên sàn cứng.

Nếu thuộc tính ``Use Scale`` được bật, :ref:`kích thước cơ sở va chạm <doc_3d_particles_properties_collision>` sẽ được nhân với `tỷ lệ hiện tại <#scale>`__ của particle. Bạn có thể dùng cách này để đảm bảo kích thước được render và kích thước va chạm khớp nhau đối với các particle có tỷ lệ ngẫu nhiên hoặc tỷ lệ thay đổi theo thời gian.

Bạn có thể tìm hiểu thêm về va chạm của particle trong phần :ref:`Collisions <doc_3d_particles_collision>` của tài liệu hướng dẫn này.

Sub-emitter
-----------

.. figure:: img/particle_sub_mode.webp
   :alt: Các chế độ sub-emitter
   :align: right

   Các chế độ sub-emitter khả dụng

Thuộc tính ``Mode`` kiểm soát cách thức và thời điểm sub-emitter được spawn. Đặt thành ``Disabled`` thì sẽ không có sub-emitter nào được spawn. Đặt thành ``Constant`` để sub-emitter được spawn liên tục với tốc độ không đổi. Thuộc tính ``Frequency`` kiểm soát tần suất việc đó xảy ra trong khoảng thời gian một giây. Đặt chế độ thành ``At End`` để sub-emitter được spawn khi thời gian tồn tại của particle cha kết thúc, ngay trước khi particle đó bị hủy. Thuộc tính ``Amount At End`` kiểm soát số lượng sub-emitter sẽ được spawn. Đặt chế độ thành ``At Collision`` để sub-emitter được spawn khi particle va chạm với môi trường. Thuộc tính ``Amount At Collision`` kiểm soát số lượng sub-emitter sẽ được spawn.

Khi thuộc tính ``Keep Velocity`` được bật, sub-emitter mới được spawn sẽ bắt đầu với vận tốc của particle cha tại thời điểm sub-emitter được tạo.

Xem phần :ref:`Sub-emitters <doc_3d_particles_subemitters>` trong tài liệu hướng dẫn này để biết giải thích chi tiết về cách thêm sub-emitter vào một hệ thống particle.

Tùy chỉnh process material
--------------------------

Nếu cần thay đổi hoặc triển khai hành vi mới trong mã shader, bạn có thể thực hiện việc đó bằng cách chuyển đổi ParticleProcessMaterial hiện tại thành một :ref:`class_ShaderMaterial`. Các thuộc tính hiện có sẽ được giữ nguyên trong quá trình chuyển đổi. Những tính năng được bật cũng sẽ ảnh hưởng đến nội dung có trong mã shader đã chuyển đổi.

Để thực hiện việc này, hãy nhấp chuột phải vào material trong dock FileSystem rồi chọn **Convert to ShaderMaterial**. Bạn cũng có thể thực hiện việc này bằng cách nhấp chuột phải vào bất kỳ thuộc tính nào đang tham chiếu đến material trong inspector.
