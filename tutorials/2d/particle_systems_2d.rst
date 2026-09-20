:article_outdated: True

.. _doc_particle_systems_2d:

Hệ thống hạt 2D
===============

Giới thiệu
----------

Hệ thống hạt được sử dụng để mô phỏng các hiệu ứng vật lý phức tạp, chẳng hạn như tia lửa, lửa, hạt ma thuật, khói, sương mù, v.v.

Ý tưởng là một "hạt" được phát ra theo một khoảng thời gian cố định và có thời gian tồn tại cố định. Trong suốt thời gian tồn tại, mọi hạt sẽ có cùng hành vi cơ bản. Điều khiến mỗi hạt khác biệt với những hạt còn lại và tạo ra vẻ ngoài tự nhiên hơn là "tính ngẫu nhiên" gắn với từng tham số. Về bản chất, việc tạo một hệ thống hạt có nghĩa là thiết lập các tham số vật lý cơ bản rồi thêm tính ngẫu nhiên vào chúng.

Các node hạt
~~~~~~~~~~~~

Godot cung cấp hai node khác nhau cho hạt 2D, :ref:`class_GPUParticles2D` và :ref:`class_CPUParticles2D`. GPUParticles2D nâng cao hơn và sử dụng GPU để xử lý các hiệu ứng hạt. CPUParticles2D là tùy chọn dựa trên CPU với tập tính năng gần như tương đương GPUParticles2D, nhưng hiệu năng thấp hơn khi sử dụng số lượng hạt lớn. Mặt khác, CPUParticles2D có thể hoạt động tốt hơn trên các hệ thống cấp thấp hoặc trong các tình huống bị nghẽn ở GPU.

Trong khi GPUParticles2D được cấu hình thông qua một :ref:`class_ParticleProcessMaterial` (và tùy chọn bằng shader tùy chỉnh), các tùy chọn tương ứng được cung cấp thông qua các thuộc tính node trong CPUParticles2D (ngoại trừ các thiết lập vệt).

Trong tương lai, không có kế hoạch thêm tính năng mới vào CPUParticles2D, mặc dù các pull request để thêm những tính năng đã có trong GPUParticles2D sẽ được chấp nhận. Vì lý do đó, chúng tôi khuyến nghị sử dụng GPUParticles2D trừ khi bạn có lý do rõ ràng để không sử dụng nó.

Bạn có thể chuyển đổi một node CPUParticles2D thành node GPUParticles2D bằng cách nhấp vào node trong cây cảnh, chọn không gian làm việc 2D, rồi chọn **CPUParticles2D > Convert to GPUParticles2D** trên thanh công cụ.

.. image:: img/particles_convert.webp

Bạn cũng có thể chuyển đổi một node GPUParticles2D thành node CPUParticles2D, tuy nhiên có thể phát sinh vấn đề nếu bạn sử dụng các tính năng chỉ dành cho GPU.

Phần còn lại của hướng dẫn này sẽ sử dụng node GPUParticles2D. Trước tiên, hãy thêm một node GPUParticles2D vào cảnh của bạn. Sau khi tạo node đó, bạn sẽ nhận thấy chỉ có một chấm trắng được tạo ra và có biểu tượng cảnh báo bên cạnh node GPUParticles2D trong bảng cảnh. Điều này là do node cần một ParticleProcessMaterial để hoạt động.

ParticleProcessMaterial
~~~~~~~~~~~~~~~~~~~~~~~

Để thêm process material vào node hạt, hãy đi tới ``Process Material`` trong bảng inspector. Nhấp vào ô bên cạnh ``Material``, rồi chọn ``New ParticleProcessMaterial`` từ menu thả xuống.

.. image:: img/particles_material.webp

Node GPUParticles2D của bạn giờ đây sẽ phát ra các điểm trắng hướng xuống dưới.

.. image:: img/particles1.png

Texture
~~~~~~~

Một hệ thống hạt có thể sử dụng một texture duy nhất hoặc một *flipbook* hoạt ảnh. Flipbook là một texture chứa nhiều khung hình hoạt ảnh có thể được phát lại hoặc chọn ngẫu nhiên trong quá trình phát hạt. Điều này tương đương với spritesheet dành cho hạt.

Texture được thiết lập thông qua thuộc tính **Texture**:

.. image:: img/particles2.webp

.. _doc_particle_systems_2d_using_flipbook:

Sử dụng flipbook hoạt ảnh
^^^^^^^^^^^^^^^^^^^^^^^^^

Flipbook hạt phù hợp để tái tạo các hiệu ứng phức tạp như khói, lửa, vụ nổ. Chúng cũng có thể được sử dụng để tạo biến thể texture ngẫu nhiên, bằng cách cho mỗi hạt sử dụng một texture khác nhau. Bạn có thể tìm các hình ảnh flipbook hạt có sẵn trên mạng hoặc kết xuất trước chúng bằng các công cụ bên ngoài như `Blender <https://www.blender.org/>`__ hoặc `EmberGen <https://jangafx.com/software/embergen/>`__.

.. figure:: img/particles_flipbook_result.webp
   :align: center
   :alt: Example of a particle system that uses a flipbook texture

   Example of a particle system that uses a flipbook texture

Sử dụng flipbook hoạt ảnh cần cấu hình bổ sung so với texture duy nhất. Để minh họa, chúng ta sẽ sử dụng texture này với 5 cột và 7 hàng (nhấp chuột phải và chọn **Save as…**):

.. figure:: img/particles_flipbook_example.webp
   :align: center
   :width: 240
   :alt: Particle flipbook texture example

   Credit: `JoesAlotofthings <https://opengameart.org/content/alot-of-particles-indispersal-special-effect-alotofparticles30>`__
   (CC BY 4.0)

Để sử dụng flipbook hoạt ảnh, bạn phải tạo một CanvasItemMaterial mới trong phần Material của node GPUParticles2D (hoặc CPUParticles2D):

.. figure:: img/particles_flipbook_create_canvasitemmaterial.webp
   :align: center
   :alt: Creating a CanvasItemMaterial at the bottom of the particles node inspector

   Creating a CanvasItemMaterial at the bottom of the particles node inspector

Trong CanvasItemMaterial này, bật **Particle Animation** và đặt **H Frames** cũng như **V Frames** thành số cột và hàng có trong texture flipbook của bạn:

.. figure:: img/particles_flipbook_configure_canvasitemmaterial.webp
   :align: center
   :alt: Configuring the CanvasItemMaterial for the example flipbook texture

   Configuring the CanvasItemMaterial for the example flipbook texture

Sau khi hoàn tất, :ref:`Animation section <doc_particle_systems_2d_animation>` trong ParticleProcessMaterial (đối với GPUParticles2D) hoặc trong inspector của CPUParticles2D sẽ có hiệu lực.

.. tip::

    Nếu texture flipbook của bạn có nền đen thay vì nền trong suốt, bạn cũng cần đặt chế độ hòa trộn thành **Add** thay vì **Mix** để hiển thị chính xác. Ngoài ra, bạn có thể chỉnh sửa texture để có nền trong suốt bằng trình chỉnh sửa hình ảnh. Trong `GIMP <https://gimp.org>`__, bạn có thể thực hiện việc này bằng menu **Color > Color to Alpha**.

Các tham số thời gian
---------------------

Lifetime
~~~~~~~~

Khoảng thời gian tính bằng giây mà mỗi hạt sẽ tồn tại. Khi lifetime kết thúc, một hạt mới được tạo ra để thay thế nó.

Lifetime: 0.5

.. image:: img/paranim14.gif

Lifetime: 4.0

.. image:: img/paranim15.gif

One Shot
~~~~~~~~

Khi được bật, một node GPUParticles2D sẽ phát ra toàn bộ hạt của nó một lần rồi không phát ra nữa.

Preprocess
~~~~~~~~~~

Hệ thống hạt bắt đầu với không có hạt nào được phát ra, sau đó mới bắt đầu phát hạt. Điều này có thể gây bất tiện khi tải một cảnh và các hệ thống như đuốc, sương mù, v.v. bắt đầu phát hạt ngay khi bạn bước vào. Preprocess được sử dụng để cho phép hệ thống xử lý trong một số giây nhất định trước khi thực sự được vẽ lần đầu tiên.

Speed Scale
~~~~~~~~~~~

Tỷ lệ tốc độ có giá trị mặc định là ``1`` và được sử dụng để điều chỉnh tốc độ của một hệ thống hạt. Giảm giá trị sẽ khiến các hạt chậm hơn, trong khi tăng giá trị sẽ khiến các hạt nhanh hơn nhiều.

Explosiveness
~~~~~~~~~~~~~

Nếu lifetime là ``1`` và có 10 hạt, điều đó có nghĩa là một hạt sẽ được phát ra sau mỗi 0.1 giây. Tham số explosiveness thay đổi điều này và buộc các hạt được phát ra cùng lúc. Các phạm vi là:

-  0: Phát các hạt theo các khoảng thời gian đều đặn (giá trị mặc định). - 1: Phát tất cả các hạt đồng thời.

Các giá trị ở giữa cũng được cho phép. Tính năng này hữu ích để tạo ra các vụ nổ hoặc những đợt hạt bùng phát đột ngột:

.. image:: img/paranim18.gif

Randomness
~~~~~~~~~~

Tất cả các tham số vật lý đều có thể được tạo ngẫu nhiên. Các giá trị ngẫu nhiên nằm trong khoảng từ ``0`` đến ``1``. Công thức để tạo ngẫu nhiên một tham số là:

::

    initial_value = param_value + param_value * randomness

Fixed FPS
~~~~~~~~~

Thiết lập này có thể được sử dụng để đặt hệ thống hạt kết xuất ở FPS cố định. Ví dụ, thay đổi giá trị thành ``2`` sẽ khiến các hạt được kết xuất ở tốc độ 2 khung hình mỗi giây. Lưu ý rằng điều này không làm chậm bản thân hệ thống hạt.

.. note::

    Godot 4.3 hiện chưa hỗ trợ nội suy vật lý cho hạt 2D. Một cách khắc phục là tắt nội suy vật lý cho node hạt bằng cách đặt **Node > Physics Interpolation > Mode** ở cuối inspector.

Fract Delta
~~~~~~~~~~~

Đặt Fract Delta thành ``true`` sẽ tạo ra phép tính delta phân số, mang lại hiệu ứng hiển thị hạt mượt hơn. Độ mượt tăng lên này bắt nguồn từ độ chính xác cao hơn. Sự khác biệt dễ nhận thấy hơn trong các hệ thống có tính ngẫu nhiên cao hoặc các hạt chuyển động nhanh. Tính năng này giúp duy trì tính nhất quán về hình ảnh của hệ thống hạt, đảm bảo chuyển động của mỗi hạt khớp với thời gian tồn tại thực tế của nó. Nếu không có tính năng này, các hạt có thể trông như bị nhảy hoặc di chuyển nhiều hơn mức cần thiết trong một khung hình nếu chúng được phát ra tại một thời điểm nằm giữa khung hình. Độ chính xác cao hơn đi kèm với đánh đổi về hiệu năng, đặc biệt trong các hệ thống có số lượng hạt lớn hơn.

Các tham số vẽ
--------------

Visibility Rect
~~~~~~~~~~~~~~~


Hình chữ nhật khả kiến kiểm soát khả năng hiển thị của các hạt trên màn hình. Nếu hình chữ nhật này nằm ngoài viewport, engine sẽ không kết xuất các hạt trên màn hình.

Các thuộc tính ``W`` và ``H`` của hình chữ nhật lần lượt kiểm soát Width và Height của nó. Các thuộc tính ``X`` và ``Y`` kiểm soát vị trí góc trên bên trái của hình chữ nhật, tương đối so với bộ phát hạt.

Bạn có thể yêu cầu Godot tự động tạo Visibility Rect bằng thanh công cụ phía trên chế độ xem 2D. Để thực hiện việc này, hãy chọn node GPUParticles2D rồi nhấp vào ``Particles > Generate Visibility Rect``. Godot sẽ mô phỏng node Particles2D phát hạt trong vài giây và thiết lập hình chữ nhật vừa với bề mặt mà các hạt chiếm.

Bạn có thể kiểm soát thời lượng phát bằng tùy chọn ``Generation Time (sec)``. Giá trị tối đa là 25 giây. Nếu cần thêm thời gian để các hạt di chuyển, bạn có thể tạm thời thay đổi thời lượng ``preprocess`` trên node Particles2D.

Local Coords
~~~~~~~~~~~~

Theo mặc định, tùy chọn này bị tắt. Điều đó có nghĩa là không gian mà các hạt được phát ra là không gian toàn cục và **không** tương đối so với node. Nếu node được di chuyển, các hạt hiện có sẽ không di chuyển theo nó:

.. image:: img/paranim21.gif

Nếu được bật, các hạt sẽ được phát vào không gian cục bộ, nghĩa là khi node được di chuyển, các hạt đã phát ra cũng bị ảnh hưởng:

.. image:: img/paranim20.gif

Draw Order
~~~~~~~~~~

Thiết lập này kiểm soát thứ tự vẽ của từng hạt. ``Index`` có nghĩa là các hạt được vẽ theo thứ tự phát ra (mặc định). ``Lifetime`` có nghĩa là chúng được vẽ theo thứ tự thời gian tồn tại còn lại.

Thiết lập Particle Process Material
-----------------------------------

Để biết thông tin về các thiết lập trong ParticleProcessMaterial, hãy xem :ref:`this page<doc_particle_process_material_2d>`.
