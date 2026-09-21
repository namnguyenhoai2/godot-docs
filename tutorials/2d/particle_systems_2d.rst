:article_outdated: True

.. _doc_particle_systems_2d:

Hệ thống particle 2D
====================

Giới thiệu
----------

Hệ thống particle được dùng để mô phỏng các hiệu ứng vật lý phức tạp, chẳng hạn như tia lửa, lửa, particle ma thuật, khói, sương mù, v.v.

Ý tưởng là một "particle" được phát ra theo một khoảng thời gian cố định và có thời gian tồn tại cố định. Trong suốt thời gian tồn tại, mọi particle đều có cùng hành vi cơ bản. Điều khiến mỗi particle khác với những particle còn lại và tạo ra vẻ tự nhiên hơn là "tính ngẫu nhiên" gắn với từng tham số. Về bản chất, việc tạo một hệ thống particle nghĩa là thiết lập các tham số vật lý cơ bản rồi thêm tính ngẫu nhiên vào chúng.

Các node particle
~~~~~~~~~~~~~~~~~

Godot cung cấp hai node khác nhau cho particle 2D, :ref:`class_GPUParticles2D` và :ref:`class_CPUParticles2D`. GPUParticles2D nâng cao hơn và sử dụng GPU để xử lý các hiệu ứng particle. CPUParticles2D là tùy chọn do CPU điều khiển, có gần như đầy đủ các tính năng của GPUParticles2D nhưng hiệu năng thấp hơn khi sử dụng số lượng particle lớn. Mặt khác, CPUParticles2D có thể hoạt động tốt hơn trên các hệ thống cấu hình thấp hoặc trong những tình huống GPU là nút thắt cổ chai.

Trong khi GPUParticles2D được cấu hình thông qua một :ref:`class_ParticleProcessMaterial` (và tùy chọn với shader tùy chỉnh), các tùy chọn tương ứng được cung cấp thông qua các thuộc tính node trong CPUParticles2D (ngoại trừ các thiết lập trail).

Trong thời gian tới, không có kế hoạch thêm tính năng mới vào CPUParticles2D, mặc dù các pull request bổ sung những tính năng đã có trong GPUParticles2D vẫn sẽ được chấp nhận. Vì lý do đó, chúng tôi khuyến nghị sử dụng GPUParticles2D trừ khi bạn có lý do cụ thể để không dùng.

Bạn có thể chuyển đổi một node CPUParticles2D thành node GPUParticles2D bằng cách nhấp vào node trong scene tree, chọn workspace 2D, rồi chọn **CPUParticles2D > Convert to GPUParticles2D** trên thanh công cụ.

.. image:: img/particles_convert.webp

Bạn cũng có thể chuyển đổi node GPUParticles2D thành node CPUParticles2D, tuy nhiên có thể phát sinh vấn đề nếu bạn sử dụng các tính năng chỉ dành cho GPU.

Phần còn lại của tutorial này sẽ sử dụng node GPUParticles2D. Trước tiên, hãy thêm một node GPUParticles2D vào scene. Sau khi tạo node đó, bạn sẽ nhận thấy chỉ có một chấm trắng được tạo ra và có biểu tượng cảnh báo bên cạnh node GPUParticles2D trong scene dock. Điều này là do node cần một ParticleProcessMaterial để hoạt động.

ParticleProcessMaterial
~~~~~~~~~~~~~~~~~~~~~~~

Để thêm process material vào node particle, hãy đi tới ``Process Material`` trong inspector panel. Nhấp vào ô bên cạnh ``Material``, rồi chọn ``New ParticleProcessMaterial`` từ menu thả xuống.

.. image:: img/particles_material.webp

Node GPUParticles2D của bạn giờ sẽ phát ra các điểm trắng hướng xuống dưới.

.. image:: img/particles1.png

Texture
~~~~~~~

Một hệ thống particle có thể sử dụng một texture duy nhất hoặc một *flipbook* animation. Flipbook là một texture chứa nhiều frame animation có thể được phát lại hoặc chọn ngẫu nhiên trong quá trình phát particle. Đây tương đương với spritesheet dành cho particle.

Texture được thiết lập thông qua thuộc tính **Texture**:

.. image:: img/particles2.webp

.. _doc_particle_systems_2d_using_flipbook:

Sử dụng flipbook animation
^^^^^^^^^^^^^^^^^^^^^^^^^^

Flipbook particle phù hợp để tái tạo các hiệu ứng phức tạp như khói, lửa, vụ nổ. Chúng cũng có thể được dùng để tạo biến thể texture ngẫu nhiên bằng cách cho mỗi particle sử dụng một texture khác nhau. Bạn có thể tìm các hình ảnh flipbook particle có sẵn trên mạng hoặc pre-render chúng bằng các công cụ bên ngoài như `Blender <https://www.blender.org/>`__ hoặc `EmberGen <https://jangafx.com/software/embergen/>`__.

.. figure:: img/particles_flipbook_result.webp
   :align: center
   :alt: Example of a particle system that uses a flipbook texture

   Example of a particle system that uses a flipbook texture

Sử dụng flipbook animation yêu cầu cấu hình bổ sung so với texture đơn. Để minh họa, chúng ta sẽ sử dụng texture này với 5 cột và 7 hàng (nhấp chuột phải và chọn **Save as…**):

.. figure:: img/particles_flipbook_example.webp
   :align: center
   :width: 240
   :alt: Particle flipbook texture example

   Credit: `JoesAlotofthings <https://opengameart.org/content/alot-of-particles-indispersal-special-effect-alotofparticles30>`__
   (CC BY 4.0)

Để sử dụng flipbook animation, bạn phải tạo một CanvasItemMaterial mới trong phần Material của node GPUParticles2D (hoặc CPUParticles2D):

.. figure:: img/particles_flipbook_create_canvasitemmaterial.webp
   :align: center
   :alt: Creating a CanvasItemMaterial at the bottom of the particles node inspector

   Creating a CanvasItemMaterial at the bottom of the particles node inspector

Trong CanvasItemMaterial này, bật **Particle Animation** và đặt **H Frames** cùng **V Frames** thành số cột và hàng có trong texture flipbook của bạn:

.. figure:: img/particles_flipbook_configure_canvasitemmaterial.webp
   :align: center
   :alt: Configuring the CanvasItemMaterial for the example flipbook texture

   Configuring the CanvasItemMaterial for the example flipbook texture

Sau khi hoàn tất, :ref:`Animation section <doc_particle_systems_2d_animation>` trong ParticleProcessMaterial (đối với GPUParticles2D) hoặc trong inspector của CPUParticles2D sẽ có hiệu lực.

.. tip::

    Nếu texture flipbook của bạn có nền đen thay vì nền trong suốt, bạn cũng cần đặt chế độ blend thành **Add** thay vì **Mix** để hiển thị chính xác. Ngoài ra, bạn có thể chỉnh sửa texture để có nền trong suốt bằng trình chỉnh sửa hình ảnh. Trong `GIMP <https://gimp.org>`__, bạn có thể thực hiện việc này bằng menu **Color > Color to Alpha**.

Các tham số thời gian
---------------------

Lifetime
~~~~~~~~

Thời gian tính bằng giây mà mỗi particle sẽ tồn tại. Khi lifetime kết thúc, một particle mới sẽ được tạo để thay thế nó.

Lifetime: 0.5

.. image:: img/paranim14.gif

Lifetime: 4.0

.. image:: img/paranim15.gif

One Shot
~~~~~~~~

Khi được bật, node GPUParticles2D sẽ phát ra toàn bộ particle của nó một lần rồi không phát ra nữa.

Preprocess
~~~~~~~~~~

Hệ thống particle bắt đầu với không particle nào được phát ra, sau đó mới bắt đầu phát. Điều này có thể gây bất tiện khi tải một scene và các hệ thống như đuốc, sương mù, v.v. bắt đầu phát ngay khi bạn bước vào. Preprocess được dùng để cho hệ thống xử lý trong một số giây nhất định trước khi thực sự được vẽ lần đầu tiên.

Speed Scale
~~~~~~~~~~~

Speed scale có giá trị mặc định là ``1`` và được dùng để điều chỉnh tốc độ của hệ thống particle. Giảm giá trị sẽ khiến particle chậm hơn, trong khi tăng giá trị sẽ khiến particle nhanh hơn nhiều.

Explosiveness
~~~~~~~~~~~~~

Nếu lifetime là ``1`` và có 10 particle, điều đó có nghĩa là một particle sẽ được phát ra sau mỗi 0.1 giây. Tham số explosiveness thay đổi điều này và buộc các particle được phát ra cùng lúc. Các khoảng giá trị là:

-  0: Phát particle theo các khoảng thời gian đều đặn (giá trị mặc định). - 1: Phát tất cả particle đồng thời.

Các giá trị ở giữa cũng được cho phép. Tính năng này hữu ích để tạo các vụ nổ hoặc những đợt particle bùng phát đột ngột:

.. image:: img/paranim18.gif

Randomness
~~~~~~~~~~

Tất cả tham số vật lý đều có thể được tạo ngẫu nhiên. Các giá trị ngẫu nhiên nằm trong khoảng từ ``0`` đến ``1``. Công thức để tạo ngẫu nhiên một tham số là:

::

    initial_value = param_value + param_value * randomness

Fixed FPS
~~~~~~~~~

Thiết lập này có thể được dùng để đặt hệ thống particle render ở một FPS cố định. Ví dụ, thay đổi giá trị thành ``2`` sẽ khiến particle render ở 2 frame mỗi giây. Lưu ý rằng điều này không làm chậm bản thân hệ thống particle.

Đặt giá trị này thành ``0`` để particle được mô phỏng ở mỗi frame được render. Điều này có thể làm tăng yêu cầu GPU đối với các thiết lập particle phức tạp, nhưng đảm bảo mô phỏng particle mượt nhất có thể. Đối với particle đã bật collision, điều này cũng có thể cải thiện độ tin cậy của collision.

Interpolate
~~~~~~~~~~~

Khi được bật, hệ thống particle sẽ nội suy vị trí của particle giữa mỗi lần tick Fixed FPS (xem ở trên). Điều này tạo ra hình ảnh mượt hơn. Chỉ chuyển động của particle được nội suy; các curve scale và color hiện chưa được nội suy.

Thuộc tính này không có tác dụng nếu :inspector:`Fixed FPS` là ``0``, vì particle sẽ được mô phỏng ở mỗi frame được render.

.. note::

    Hiện tại Godot không hỗ trợ :ref:`physics interpolation <doc_physics_interpolation_introduction>` cho GPUParticles2D. Lưu ý rằng physics interpolation không nên bị nhầm với thuộc tính :inspector:`Interpolate` trên GPUParticles2D.

    Để khắc phục tạm thời, hãy tắt physics interpolation cho node particle bằng cách đặt :menu:`Node > Physics Interpolation > Mode` ở cuối inspector hoặc chuyển node thành CPUParticles2D, node có hỗ trợ physics interpolation.

Fract Delta
~~~~~~~~~~~

Đặt Fract Delta thành ``true`` sẽ dẫn đến phép tính delta phân số, tạo hiệu ứng hiển thị particle mượt hơn. Độ mượt tăng lên này bắt nguồn từ độ chính xác cao hơn. Sự khác biệt dễ nhận thấy hơn trong các hệ thống có tính ngẫu nhiên cao hoặc particle chuyển động nhanh. Tính năng này giúp duy trì tính nhất quán về hình ảnh của hệ thống particle, đảm bảo chuyển động của mỗi particle khớp với thời gian tồn tại thực tế của nó. Nếu không có tính năng này, particle có thể trông như bị giật hoặc di chuyển nhiều hơn mức cần thiết trong một frame nếu chúng được phát ra tại một điểm nằm giữa frame. Độ chính xác cao hơn đi kèm với đánh đổi về hiệu năng, đặc biệt trong các hệ thống có số lượng particle lớn.

Các tham số vẽ
--------------

Visibility Rect
~~~~~~~~~~~~~~~


Visibility rectangle kiểm soát khả năng hiển thị của particle trên màn hình. Nếu hình chữ nhật này nằm ngoài viewport, engine sẽ không render particle trên màn hình.

Các thuộc tính ``W`` và ``H`` của hình chữ nhật lần lượt kiểm soát Width và Height của nó. Các thuộc tính ``X`` và ``Y`` kiểm soát vị trí góc trên bên trái của hình chữ nhật, tương đối so với particle emitter.

Bạn có thể để Godot tự động tạo Visibility Rect bằng thanh công cụ phía trên chế độ xem 2d. Để làm vậy, hãy chọn node GPUParticles2D và nhấp vào ``Particles > Generate Visibility Rect``. Godot sẽ mô phỏng node Particles2D phát particle trong vài giây rồi đặt hình chữ nhật vừa với phạm vi mà particle bao phủ.

Bạn có thể kiểm soát thời lượng phát bằng tùy chọn ``Generation Time (sec)``. Giá trị tối đa là 25 giây. Nếu cần thêm thời gian để particle di chuyển, bạn có thể tạm thời thay đổi thời lượng ``preprocess`` trên node Particles2D.

Local Coords
~~~~~~~~~~~~

Theo mặc định, tùy chọn này đang tắt. Điều đó có nghĩa là không gian mà các hạt được phát ra là không gian global, **không** phải không gian tương đối so với node. Nếu node được di chuyển, các hạt hiện có sẽ không di chuyển theo:

.. image:: img/paranim21.gif

Khi được bật, các hạt sẽ được phát ra trong không gian local, nghĩa là nếu node được di chuyển, các hạt đã được phát ra cũng sẽ bị ảnh hưởng:

.. image:: img/paranim20.gif

Thứ tự vẽ
~~~~~~~~~

Tùy chọn này kiểm soát thứ tự vẽ của từng hạt. ``Index`` nghĩa là các hạt được vẽ theo thứ tự phát ra (mặc định). ``Lifetime`` nghĩa là chúng được vẽ theo thứ tự thời gian sống còn lại.

Cài đặt ParticleProcessMaterial
-------------------------------

Để biết thông tin về các cài đặt trong ParticleProcessMaterial, hãy xem :ref:`this page<doc_particle_process_material_2d>`.
