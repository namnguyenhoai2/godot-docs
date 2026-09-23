:article_outdated: Đúng

.. _doc_particle_systems_2d:

Hệ thống particle 2D
====================

Giới thiệu
----------

Hệ thống particle được dùng để mô phỏng các hiệu ứng vật lý phức tạp, chẳng hạn như tia lửa, lửa, particle ma thuật, khói, sương mù, v.v.

Ý tưởng là một "particle" được phát ra theo một khoảng thời gian cố định và có thời gian tồn tại cố định. Trong suốt thời gian tồn tại, mọi particle đều có cùng hành vi cơ bản. Điều khiến mỗi particle khác với những particle còn lại và tạo ra vẻ ngoài tự nhiên hơn là "tính ngẫu nhiên" gắn với từng tham số. Về cơ bản, việc tạo một hệ thống particle nghĩa là thiết lập các tham số vật lý cơ bản rồi thêm tính ngẫu nhiên vào chúng.

Node particle
~~~~~~~~~~~~~

Godot cung cấp hai node khác nhau cho particle 2D, :ref:`class_GPUParticles2D` và :ref:`class_CPUParticles2D`. GPUParticles2D nâng cao hơn và sử dụng GPU để xử lý các hiệu ứng particle. CPUParticles2D là tùy chọn do CPU điều khiển, có mức độ tương đương về tính năng gần như GPUParticles2D, nhưng hiệu năng thấp hơn khi sử dụng số lượng particle lớn. Mặt khác, CPUParticles2D có thể hoạt động tốt hơn trên các hệ thống cấp thấp hoặc trong những trường hợp GPU là điểm nghẽn.

Trong khi GPUParticles2D được cấu hình thông qua một :ref:`class_ParticleProcessMaterial` (và tùy chọn bằng shader tùy chỉnh), các tùy chọn tương ứng được cung cấp thông qua các thuộc tính node trong CPUParticles2D (ngoại trừ các thiết lập trail).

Trong tương lai, không có kế hoạch bổ sung tính năng mới cho CPUParticles2D, dù các pull request bổ sung những tính năng đã có trong GPUParticles2D vẫn sẽ được chấp nhận. Vì lý do đó, chúng tôi khuyến nghị sử dụng GPUParticles2D trừ khi bạn có lý do cụ thể để không sử dụng.

Bạn có thể chuyển một node CPUParticles2D thành node GPUParticles2D bằng cách nhấp vào node trong scene tree, chọn không gian làm việc 2D, rồi chọn **CPUParticles2D > Convert to GPUParticles2D** trên thanh công cụ.

.. image:: img/particles_convert.webp

Bạn cũng có thể chuyển một node GPUParticles2D thành node CPUParticles2D, tuy nhiên có thể phát sinh vấn đề nếu bạn sử dụng các tính năng chỉ có trên GPU.

Phần còn lại của tutorial này sẽ sử dụng node GPUParticles2D. Trước tiên, hãy thêm một node GPUParticles2D vào scene. Sau khi tạo node đó, bạn sẽ nhận thấy chỉ có một chấm trắng được tạo ra và có biểu tượng cảnh báo bên cạnh node GPUParticles2D trong scene dock. Đó là vì node cần một ParticleProcessMaterial để hoạt động.

ParticleProcessMaterial
~~~~~~~~~~~~~~~~~~~~~~~

Để thêm process material vào node particle, hãy đi đến ``Process Material`` trong bảng inspector. Nhấp vào ô bên cạnh ``Material``, rồi chọn ``New ParticleProcessMaterial`` từ menu thả xuống.

.. image:: img/particles_material.webp

Node GPUParticles2D của bạn giờ sẽ phát ra các điểm trắng hướng xuống dưới.

.. image:: img/particles1.png

Texture
~~~~~~~

Một hệ thống particle có thể sử dụng một texture duy nhất hoặc một animation *flipbook*. Flipbook là một texture chứa nhiều frame animation có thể được phát lại hoặc chọn ngẫu nhiên trong quá trình phát. Điều này tương đương với spritesheet dành cho particle.

Texture được thiết lập thông qua thuộc tính **Texture**:

.. image:: img/particles2.webp

.. _doc_particle_systems_2d_using_flipbook:

Sử dụng flipbook animation
^^^^^^^^^^^^^^^^^^^^^^^^^^

Flipbook particle phù hợp để tái tạo các hiệu ứng phức tạp như khói, lửa và vụ nổ. Chúng cũng có thể được dùng để tạo ra sự biến đổi texture ngẫu nhiên, bằng cách cho mỗi particle sử dụng một texture khác nhau. Bạn có thể tìm các hình ảnh flipbook particle có sẵn trên mạng hoặc pre-render chúng bằng các công cụ bên ngoài như `Blender <https://www.blender.org/>`__ hoặc `EmberGen <https://jangafx.com/software/embergen/>`__.

.. figure:: img/particles_flipbook_result.webp
   :align: center
   :alt: Ví dụ về một hệ thống particle sử dụng texture flipbook

   Ví dụ về một hệ thống particle sử dụng texture flipbook

Việc sử dụng flipbook animation cần cấu hình bổ sung so với texture duy nhất. Để minh họa, chúng ta sẽ sử dụng texture này với 5 cột và 7 hàng (nhấp chuột phải và chọn **Save as…**):

.. figure:: img/particles_flipbook_example.webp
   :align: center
   :width: 240
   :alt: Ví dụ về texture flipbook particle

   Ghi công: `JoesAlotofthings <https://opengameart.org/content/alot-of-particles-indispersal-special-effect-alotofparticles30>`__ (CC BY 4.0)

Để sử dụng flipbook animation, bạn phải tạo một CanvasItemMaterial mới trong phần Material của node GPUParticles2D (hoặc CPUParticles2D):

.. figure:: img/particles_flipbook_create_canvasitemmaterial.webp
   :align: center
   :alt: Tạo CanvasItemMaterial ở cuối inspector của node particle

   Tạo CanvasItemMaterial ở cuối inspector của node particle

Trong CanvasItemMaterial này, bật **Particle Animation** và đặt **H Frames** cùng **V Frames** thành số cột và hàng có trong texture flipbook của bạn:

.. figure:: img/particles_flipbook_configure_canvasitemmaterial.webp
   :align: center
   :alt: Cấu hình CanvasItemMaterial cho texture flipbook mẫu

   Cấu hình CanvasItemMaterial cho texture flipbook mẫu

Sau khi hoàn tất, phần :ref:`Animation section <doc_particle_systems_2d_animation>` trong ParticleProcessMaterial (đối với GPUParticles2D) hoặc trong inspector CPUParticles2D sẽ có hiệu lực.

.. tip::

    Nếu texture flipbook của bạn có nền đen thay vì nền trong suốt, bạn cũng cần đặt blend mode thành **Add** thay vì **Mix** để hiển thị chính xác. Ngoài ra, bạn có thể chỉnh sửa texture để có nền trong suốt bằng trình chỉnh sửa hình ảnh. Trong `GIMP <https://gimp.org>`__, bạn có thể thực hiện việc này bằng menu **Color > Color to Alpha**.

Các tham số thời gian
---------------------

Lifetime
~~~~~~~~

Số giây mà mỗi particle sẽ tồn tại. Khi lifetime kết thúc, một particle mới được tạo để thay thế nó.

Lifetime: 0.5

.. image:: img/paranim14.gif

Lifetime: 4.0

.. image:: img/paranim15.gif

One Shot
~~~~~~~~

Khi được bật, node GPUParticles2D sẽ phát ra toàn bộ particle một lần rồi không phát ra nữa.

Preprocess
~~~~~~~~~~

Hệ thống particle bắt đầu với không có particle nào được phát ra, sau đó mới bắt đầu phát. Điều này có thể gây bất tiện khi tải một scene và các hệ thống như đuốc, sương mù, v.v. bắt đầu phát ngay khi bạn bước vào. Preprocess được dùng để cho hệ thống xử lý trong một số giây nhất định trước khi thực sự được vẽ lần đầu tiên.

Speed Scale
~~~~~~~~~~~

Speed scale có giá trị mặc định là ``1`` và được dùng để điều chỉnh tốc độ của hệ thống particle. Giảm giá trị này sẽ khiến các particle chậm hơn, còn tăng giá trị sẽ khiến chúng nhanh hơn đáng kể.

Explosiveness
~~~~~~~~~~~~~

Nếu lifetime là ``1`` và có 10 particle, điều đó có nghĩa là một particle sẽ được phát ra sau mỗi 0.1 giây. Tham số explosiveness thay đổi điều này và buộc các particle được phát ra cùng lúc. Các phạm vi là:

-  0: Phát ra các particle theo các khoảng thời gian đều đặn (giá trị mặc định).
-  1: Phát ra tất cả particle đồng thời.

Các giá trị ở giữa cũng được phép. Tính năng này hữu ích để tạo ra các vụ nổ hoặc những đợt bùng phát hạt đột ngột:

.. image:: img/paranim18.gif

Randomness
~~~~~~~~~~

Tất cả các tham số vật lý đều có thể được ngẫu nhiên hóa. Các giá trị ngẫu nhiên nằm trong khoảng từ ``0`` đến ``1``. Công thức để ngẫu nhiên hóa một tham số là:

::

    initial_value = param_value + param_value * randomness

Fixed FPS
~~~~~~~~~

Bạn có thể sử dụng thiết lập này để đặt hệ thống hạt kết xuất ở FPS cố định. Ví dụ: thay đổi giá trị thành ``2`` sẽ khiến các hạt được kết xuất ở tốc độ 2 khung hình mỗi giây. Lưu ý rằng điều này không làm chậm bản thân hệ thống hạt.

.. note::

    Godot 4.3 hiện chưa hỗ trợ nội suy vật lý cho hạt 2D. Để khắc phục, hãy tắt nội suy vật lý cho node hạt bằng cách đặt **Node > Physics Interpolation > Mode** ở cuối inspector.

Fract Delta
~~~~~~~~~~~

Đặt Fract Delta thành ``true`` sẽ thực hiện tính toán delta phân số, tạo hiệu ứng hiển thị hạt mượt hơn. Độ mượt tăng lên này bắt nguồn từ độ chính xác cao hơn. Sự khác biệt dễ nhận thấy hơn trong các hệ thống có độ ngẫu nhiên cao hoặc các hạt chuyển động nhanh. Thiết lập này giúp duy trì tính nhất quán về hình ảnh của hệ thống hạt, đảm bảo chuyển động của mỗi hạt khớp với thời gian tồn tại thực tế của nó. Nếu không có thiết lập này, các hạt có thể trông như bị nhảy hoặc di chuyển nhiều hơn mức cần thiết trong một khung hình nếu chúng được phát ra tại một thời điểm nằm giữa khung hình. Độ chính xác cao hơn đi kèm với đánh đổi về hiệu năng, đặc biệt là trong các hệ thống có nhiều hạt.

Drawing parameters
------------------

Visibility Rect
~~~~~~~~~~~~~~~


Hình chữ nhật khả kiến kiểm soát khả năng hiển thị của các hạt trên màn hình. Nếu hình chữ nhật này nằm ngoài viewport, engine sẽ không kết xuất các hạt trên màn hình.

Các thuộc tính ``W`` và ``H`` của hình chữ nhật lần lượt kiểm soát Width và Height của nó. Các thuộc tính ``X`` và ``Y`` kiểm soát vị trí của góc trên bên trái hình chữ nhật, tính tương đối so với particle emitter.

Bạn có thể để Godot tự động tạo Visibility Rect bằng thanh công cụ phía trên chế độ xem 2D. Để thực hiện, hãy chọn node GPUParticles2D và nhấp vào ``Particles > Generate Visibility Rect``. Godot sẽ mô phỏng node Particles2D phát ra các hạt trong vài giây, rồi đặt hình chữ nhật vừa với bề mặt mà các hạt bao phủ.

Bạn có thể kiểm soát thời lượng phát ra bằng tùy chọn ``Generation Time (sec)``. Giá trị tối đa là 25 giây. Nếu cần thêm thời gian để các hạt di chuyển, bạn có thể tạm thời thay đổi thời lượng ``preprocess`` trên node Particles2D.

Local Coords
~~~~~~~~~~~~

Theo mặc định, tùy chọn này bị tắt. Điều đó có nghĩa là không gian nơi các hạt được phát ra là không gian toàn cục, và **not** tương đối so với node. Nếu node được di chuyển, các hạt hiện có sẽ không di chuyển theo nó:

.. image:: img/paranim21.gif

Nếu được bật, các hạt sẽ được phát ra vào không gian cục bộ, nghĩa là khi node được di chuyển, các hạt đã phát ra cũng bị ảnh hưởng:

.. image:: img/paranim20.gif

Draw Order
~~~~~~~~~~

Thiết lập này kiểm soát thứ tự vẽ từng hạt. ``Index`` có nghĩa là các hạt được vẽ theo thứ tự phát ra (mặc định). ``Lifetime`` có nghĩa là chúng được vẽ theo thứ tự thời gian tồn tại còn lại.

Particle Process Material Settings
----------------------------------

Để biết thông tin về các thiết lập trong ParticleProcessMaterial, hãy xem :ref:`this page <doc_particle_process_material_2d>`.
