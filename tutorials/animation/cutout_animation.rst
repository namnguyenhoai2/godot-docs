:article_outdated: Đúng

.. _doc_cutout_animation:

Hoạt ảnh cắt giấy
=================

Đó là gì?
~~~~~~~~~

Theo truyền thống, `hoạt ảnh cắt giấy <https://en.wikipedia.org/wiki/Cutout_animation>`__ là một loại `hoạt ảnh stop motion <https://en.wikipedia.org/wiki/Stop_motion>`__ trong đó các mảnh giấy (hoặc vật liệu mỏng khác) được cắt thành những hình dạng đặc biệt và sắp xếp thành các hình biểu diễn nhân vật và vật thể trong không gian hai chiều. Cơ thể nhân vật thường được tạo thành từ nhiều mảnh. Các mảnh này được sắp xếp và chụp ảnh một lần cho mỗi khung hình của bộ phim. Người làm hoạt ảnh di chuyển và xoay các bộ phận theo từng bước nhỏ giữa mỗi lần chụp để tạo ảo giác chuyển động khi các hình ảnh được phát lại nhanh liên tiếp.

Ngày nay, các mô phỏng hoạt ảnh cắt giấy có thể được tạo bằng phần mềm, như trong `South Park <https://en.wikipedia.org/wiki/South_Park>`__ và `Jake and the Never Land Pirates <https://en.wikipedia.org/wiki/Jake_and_the_Never_Land_Pirates>`__.

Trong trò chơi điện tử, kỹ thuật này cũng trở nên phổ biến. Ví dụ như `Paper Mario <https://en.wikipedia.org/wiki/Super_Paper_Mario>`__ hoặc `Rayman Origins <https://en.wikipedia.org/wiki/Rayman_Origins>`__ .

Hoạt ảnh cắt giấy trong Godot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot cung cấp các công cụ để làm việc với các rig cắt giấy và rất phù hợp với quy trình sau:

-  **Hệ thống hoạt ảnh được tích hợp hoàn toàn với engine**: Điều này có nghĩa là hoạt ảnh có thể điều khiển nhiều thứ hơn là chỉ chuyển động của các vật thể. Texture, kích thước sprite, pivot, độ mờ, điều chỉnh màu và nhiều thuộc tính khác đều có thể được tạo hoạt ảnh và blend.
-  **Kết hợp các kiểu hoạt ảnh**: AnimatedSprite2D cho phép sử dụng hoạt ảnh cel truyền thống cùng với hoạt ảnh cắt giấy. Trong hoạt ảnh cel, các khung hình khác nhau sử dụng những hình vẽ hoàn toàn khác nhau thay vì cùng một nhóm mảnh được định vị khác nhau. Trong một hoạt ảnh chủ yếu dựa trên kỹ thuật cắt giấy, hoạt ảnh cel có thể được sử dụng có chọn lọc cho các bộ phận phức tạp như bàn tay, bàn chân, biểu cảm khuôn mặt thay đổi, v.v.
-  **Các phần tử có hình dạng tùy chỉnh**: Có thể tạo các hình dạng tùy chỉnh bằng
   :ref:`Polygon2D <class_Polygon2D>` để cho phép tạo hoạt ảnh UV, biến dạng, v.v.
-  **Hệ thống hạt**: Có thể kết hợp rig hoạt ảnh cắt giấy với hệ thống hạt. Điều này hữu ích cho các hiệu ứng phép thuật, jetpack, v.v.
-  **Collider tùy chỉnh**: Thiết lập collider và vùng ảnh hưởng ở các phần khác nhau của skeleton, rất phù hợp cho boss và trò chơi đối kháng.
-  **Animation Tree**: Cho phép kết hợp phức tạp và blend giữa nhiều hoạt ảnh, giống như cách hoạt động trong 3D.

Và còn nhiều hơn thế nữa!

Quá trình tạo GBot
~~~~~~~~~~~~~~~~~~

Trong tutorial này, chúng ta sẽ sử dụng các mảnh của nhân vật `GBot <https://www.youtube.com/watch?v=S13FrWuBMx4&list=UUckpus81gNin1aV8WSffRKw>`__ do Andreas Esau tạo ra làm nội dung minh họa.

.. image:: img/tuto_cutout_walk.gif

Lấy asset của bạn: `cutout_animation_assets.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/cutout_animation_assets.zip>`_.

Thiết lập rig
~~~~~~~~~~~~~

Tạo một Node2D trống làm root của scene, chúng ta sẽ làm việc bên dưới node này:

.. image:: img/tuto_cutout1.png

Node đầu tiên của model là hông. Nhìn chung, trong cả 2D và 3D, hông là root của skeleton. Điều này giúp việc tạo hoạt ảnh dễ dàng hơn:

.. image:: img/tuto_cutout2.png

Tiếp theo là thân. Thân cần là một child của hông, vì vậy hãy tạo một sprite con và nạp texture thân, sau đó điều chỉnh vị trí cho phù hợp:

.. image:: img/tuto_cutout3.png

Trông khá ổn. Hãy xem hierarchy của chúng ta có hoạt động như một skeleton không bằng cách xoay thân. Bạn có thể thực hiện việc này bằng cách nhấn :kbd:`E` để vào chế độ xoay, rồi kéo bằng nút chuột trái. Để thoát khỏi chế độ xoay, hãy nhấn :kbd:`ESC`.

.. image:: img/tutovec_torso1.gif

Pivot xoay bị sai và cần được điều chỉnh.

Dấu thập nhỏ ở giữa :ref:`Sprite2D <class_Sprite2D>` là pivot xoay:

.. image:: img/tuto_cutout4.png

Điều chỉnh pivot
~~~~~~~~~~~~~~~~

Có thể điều chỉnh pivot bằng cách thay đổi thuộc tính *offset* trong Sprite2D:

.. image:: img/tuto_cutout5.png

Pivot cũng có thể được điều chỉnh *trực quan*. Khi di con trỏ lên điểm pivot mong muốn, hãy nhấn :kbd:`V` để di chuyển pivot đến đó cho Sprite2D đang được chọn. Trên thanh công cụ cũng có một công cụ với chức năng tương tự.

.. image:: img/tutovec_torso2.gif

Tiếp tục thêm các mảnh cơ thể, bắt đầu với cánh tay phải. Đảm bảo đặt mỗi sprite vào đúng vị trí trong hierarchy để các phép xoay và tịnh tiến của nó là tương đối so với parent:

.. image:: img/tuto_cutout6.png

Với cánh tay trái, chúng ta gặp một vấn đề. Trong 2D, các node con xuất hiện phía trước node cha:

.. image:: img/tuto_cutout7.png

Chúng ta muốn cánh tay trái xuất hiện *phía sau* hông và thân. Chúng ta có thể di chuyển các node của cánh tay trái ra phía sau hông (lên trên node hông trong hierarchy của scene), nhưng khi đó cánh tay trái không còn ở đúng vị trí trong hierarchy nữa. Điều này có nghĩa là nó sẽ không bị ảnh hưởng bởi chuyển động của thân. Chúng ta sẽ khắc phục vấn đề này bằng các node ``RemoteTransform2D``.

.. note:: Bạn cũng có thể khắc phục các vấn đề về thứ tự chiều sâu bằng cách điều chỉnh thuộc tính Z của bất kỳ node nào kế thừa từ Node2D.

Node RemoteTransform2D
~~~~~~~~~~~~~~~~~~~~~~

Node :ref:`RemoteTransform2D <class_RemoteTransform2D>` biến đổi các node ở một vị trí khác trong hierarchy. Node này áp dụng transform của chính nó (bao gồm mọi phép biến đổi mà nó kế thừa từ các parent) lên node từ xa mà nó nhắm đến.

Điều này cho phép chúng ta điều chỉnh thứ tự hiển thị của các phần tử độc lập với vị trí của các phần đó trong hierarchy cắt giấy.

Tạo một node ``RemoteTransform2D`` làm child của thân. Đặt tên cho node này là ``remote_arm_l``. Tạo một node RemoteTransform2D khác bên trong node đầu tiên và đặt tên là ``remote_hand_l``. Sử dụng thuộc tính ``Remote Path`` của hai node mới để lần lượt nhắm đến các sprite ``arm_l`` và ``hand_l``:

.. image:: img/tuto_cutout9.png

Giờ đây, việc di chuyển các node ``RemoteTransform2D`` sẽ di chuyển các sprite. Vì vậy, chúng ta có thể tạo hoạt ảnh bằng cách điều chỉnh các transform ``RemoteTransform2D``:

.. image:: img/tutovec_torso4.gif

Hoàn thiện skeleton
~~~~~~~~~~~~~~~~~~~

Hoàn thiện skeleton bằng cách thực hiện các bước tương tự cho những phần còn lại. Scene sau cùng sẽ trông tương tự như sau:

.. image:: img/tuto_cutout10.png

Rig sau khi hoàn thiện sẽ dễ tạo hoạt ảnh. Bằng cách chọn các node và xoay chúng, bạn có thể tạo hoạt ảnh forward kinematics (FK) một cách hiệu quả.

Với các object và rig đơn giản thì cách này phù hợp, nhưng có một số hạn chế:

-  Việc chọn các sprite trong viewport chính có thể trở nên khó khăn với các rig phức tạp. Khi đó, scene tree thường được dùng để chọn các phần, nhưng cách này có thể chậm hơn.
-  Inverse Kinematics (IK) hữu ích khi tạo hoạt ảnh cho các chi như bàn tay và bàn chân, nhưng không thể sử dụng với rig hiện tại của chúng ta.

Để giải quyết những vấn đề này, chúng ta sẽ sử dụng skeleton của Godot.

Skeleton
~~~~~~~~

Trong Godot có một helper để tạo "bone" giữa các node. Các node được liên kết bằng bone được gọi là skeleton.

Ví dụ, hãy biến cánh tay phải thành một skeleton. Để tạo skeleton, cần chọn một chuỗi node từ trên xuống dưới:

.. image:: img/tuto_cutout11.png

Sau đó, nhấp vào menu Skeleton và chọn ``Make Bones``.

.. image:: img/tuto_cutout12.png

Thao tác này sẽ thêm các bone bao phủ cánh tay, nhưng kết quả có thể khiến bạn ngạc nhiên.

.. image:: img/tuto_cutout13.png

Tại sao bàn tay lại không có bone? Trong Godot, một bone kết nối một node với node cha của nó. Và hiện tại node bàn tay không có node con nào. Với hiểu biết này, hãy thử lại.

Bước đầu tiên là tạo một node endpoint. Có thể dùng bất kỳ loại node nào, nhưng nên dùng :ref:`Marker2D <class_Marker2D>` vì node này hiển thị trong editor. Node endpoint sẽ đảm bảo bone cuối cùng có hướng.

.. image:: img/tuto_cutout14.png

Bây giờ hãy chọn toàn bộ chuỗi, từ endpoint đến cánh tay, rồi tạo các bone:

.. image:: img/tuto_cutout15.png

Kết quả trông giống skeleton hơn nhiều, và giờ bạn có thể chọn cũng như animate cánh tay và cẳng tay.

Tạo endpoint cho tất cả các đầu mút quan trọng. Tạo bone cho tất cả các bộ phận có thể khớp nối của hình cắt, với hông là điểm kết nối cuối cùng giữa tất cả các bộ phận.

Bạn có thể nhận thấy một bone thừa được tạo khi kết nối hông và thân. Godot đã kết nối node hông với root của scene bằng một bone, nhưng chúng ta không muốn điều đó. Để khắc phục, hãy chọn root và node hông, mở menu Skeleton, nhấp vào ``clear bones``.

.. image:: img/tuto_cutout15_2.png

Skeleton hoàn chỉnh của bạn sẽ trông примерно như sau:

.. image:: img/tuto_cutout16.png

Có thể bạn đã nhận thấy một bộ endpoint thứ hai ở hai bàn tay. Điều này sẽ sớm trở nên dễ hiểu.

Giờ toàn bộ hình đã được rig, bước tiếp theo là thiết lập các chuỗi IK. Chuỗi IK cho phép điều khiển các đầu mút tự nhiên hơn.

Chuỗi IK
~~~~~~~~

IK là viết tắt của inverse kinematics. Đây là một kỹ thuật tiện lợi để animate vị trí của bàn tay, bàn chân và các đầu mút khác của những rig như rig chúng ta vừa tạo. Hãy tưởng tượng bạn muốn đặt bàn chân của một nhân vật vào một vị trí cụ thể trên mặt đất. Nếu không có chuỗi IK, mỗi chuyển động của bàn chân sẽ yêu cầu xoay và định vị một số bone khác (ít nhất là xương ống chân và xương đùi). Việc này khá phức tạp và dẫn đến kết quả thiếu chính xác. IK cho phép chúng ta di chuyển trực tiếp bàn chân, trong khi xương ống chân và xương đùi tự điều chỉnh.

.. note::

    **Các chuỗi IK trong Godot hiện chỉ hoạt động trong editor**, không hoạt động khi runtime. Chúng nhằm đơn giản hóa quá trình thiết lập keyframe và hiện chưa hữu ích cho các kỹ thuật như procedural animation.

Để tạo một chuỗi IK, hãy chọn một chuỗi bone từ endpoint đến base của chuỗi. Ví dụ, để tạo chuỗi IK cho chân phải, hãy chọn như sau:

.. image:: img/tuto_cutout17.png

Sau đó bật chuỗi này cho IK. Đi tới Edit > Make IK Chain.

.. image:: img/tuto_cutout18.png

Kết quả là base của chuỗi sẽ chuyển thành *Yellow*.

.. image:: img/tuto_cutout19.png

Sau khi thiết lập chuỗi IK, hãy lấy bất kỳ node con hoặc node cháu nào của base của chuỗi (ví dụ: bàn chân) và di chuyển nó. Bạn sẽ thấy phần còn lại của chuỗi điều chỉnh theo khi bạn thay đổi vị trí của nó.

.. image:: img/tutovec_torso5.gif

Mẹo về animation
~~~~~~~~~~~~~~~~

Phần sau là tập hợp các mẹo để tạo animation cho các rig hình cắt của bạn. Để biết thêm thông tin về cách hệ thống animation trong Godot hoạt động, hãy xem :ref:`doc_introduction_animation`.

Thiết lập keyframe và loại trừ thuộc tính
-----------------------------------------

Khi cửa sổ animation editor được mở, các phần tử theo ngữ cảnh đặc biệt sẽ xuất hiện trên thanh công cụ phía trên:

.. image:: img/tuto_cutout20.png

Nút key chèn các keyframe về vị trí, góc xoay và tỷ lệ cho các object hoặc bone được chọn tại vị trí playhead hiện tại.

Các nút chuyển đổi "loc", "rot" và "scl" ở bên trái nút key sẽ thay đổi chức năng của nút này, cho phép bạn chỉ định keyframe sẽ được tạo cho thuộc tính nào trong ba thuộc tính.

Dưới đây là một ví dụ cho thấy tính năng này hữu ích như thế nào: Hãy tưởng tượng bạn có một node đã có hai keyframe chỉ animate tỷ lệ. Bạn muốn thêm một chuyển động xoay chồng lên cùng node đó. Chuyển động xoay phải bắt đầu và kết thúc vào các thời điểm khác với thay đổi tỷ lệ đã được thiết lập. Bạn có thể dùng các nút chuyển đổi để chỉ thêm thông tin về góc xoay khi thêm keyframe mới. Nhờ vậy, bạn tránh được việc thêm các keyframe tỷ lệ không mong muốn, vốn sẽ làm gián đoạn animation tỷ lệ hiện có.

Tạo tư thế nghỉ
~~~~~~~~~~~~~~~

Hãy xem tư thế nghỉ như tư thế mặc định mà rig hình cắt của bạn sẽ ở đó khi không có tư thế nào khác đang hoạt động trong game. Tạo tư thế nghỉ như sau:

1. Đảm bảo các bộ phận của rig được đặt ở vị trí trông giống như một "tư thế nghỉ"
sắp xếp.

2. Tạo một animation mới và đổi tên thành "rest".

3. Chọn tất cả node trong rig (chọn bằng khung sẽ hoạt động tốt).

4. Đảm bảo các nút chuyển đổi "loc", "rot" và "scl" đều đang bật trên
thanh công cụ.

5. Nhấn nút key. Các key sẽ được chèn cho tất cả bộ phận được chọn để lưu lại
cách sắp xếp hiện tại của chúng. Giờ đây có thể gọi lại tư thế này khi cần trong game bằng cách phát animation "rest" bạn đã tạo.

.. image:: img/tuto_cutout21.png

Chỉ sửa đổi góc xoay
~~~~~~~~~~~~~~~~~~~~

Khi animate một rig hình cắt, thường chỉ cần thay đổi góc xoay của các node. Vị trí và tỷ lệ hiếm khi được sử dụng.

Vì vậy, khi chèn key, bạn có thể thấy thuận tiện nếu hầu hết thời gian chỉ bật nút chuyển đổi "rot":

.. image:: img/tuto_cutout22.png

Điều này sẽ tránh tạo các track animation không mong muốn cho vị trí và tỷ lệ.

Tạo keyframe cho chuỗi IK
~~~~~~~~~~~~~~~~~~~~~~~~~

Khi chỉnh sửa chuỗi IK, không cần chọn toàn bộ chuỗi để thêm keyframe. Việc chọn endpoint của chuỗi và chèn một keyframe sẽ tự động chèn keyframe cho tất cả các bộ phận khác trong chuỗi.

Di chuyển trực quan một sprite ra phía sau node cha
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đôi khi cần để một node thay đổi độ sâu hiển thị so với node cha trong khi animate. Hãy hình dung một nhân vật đang quay mặt về phía camera, kéo một vật từ phía sau lưng ra và cầm nó đưa ra trước mặt. Trong animation này, toàn bộ cánh tay và vật trong tay nhân vật sẽ cần thay đổi độ sâu hiển thị so với thân nhân vật.

Để hỗ trợ việc này, tất cả node kế thừa từ Node2D đều có thuộc tính "Behind Parent" có thể tạo keyframe. Khi lập kế hoạch cho rig, hãy nghĩ đến các chuyển động mà nó cần thực hiện và cân nhắc cách bạn sẽ sử dụng các node "Behind Parent" và/hoặc RemoteTransform2D. Chúng cung cấp chức năng chồng lấp nhau.

.. image:: img/tuto_cutout23.png

Thiết lập đường cong easing cho nhiều key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để áp dụng cùng một đường cong easing cho nhiều keyframe cùng lúc:

1. Chọn các key liên quan.
2. Nhấp vào biểu tượng bút chì ở góc dưới bên phải của animation panel. Thao tác này sẽ mở trình chỉnh sửa transition.
3. Trong trình chỉnh sửa transition, nhấp vào curve mong muốn để áp dụng.

.. image:: img/tuto_cutout24.png

Biến dạng skeletal 2D
~~~~~~~~~~~~~~~~~~~~~

Biến dạng skeletal có thể được dùng để bổ trợ cho một cutout rig, cho phép từng mảnh riêng lẻ biến dạng tự nhiên (ví dụ: các râu rung lắc khi một nhân vật côn trùng bước đi).

Quy trình này được mô tả trong :ref:`một hướng dẫn riêng <doc_2d_skeletons>`.

.. _`cutout_animation_assets.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/cutout_animation_assets.zip
