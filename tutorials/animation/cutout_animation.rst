:article_outdated: True

.. _doc_cutout_animation:

Hoạt ảnh cắt dán
================

Đó là gì?
~~~~~~~~~

Theo truyền thống, `cutout animation <https://en.wikipedia.org/wiki/Cutout_animation>`__ là một dạng `stop motion animation <https://en.wikipedia.org/wiki/Stop_motion>`__ trong đó các mảnh giấy (hoặc vật liệu mỏng khác) được cắt thành những hình dạng đặc biệt và sắp xếp thành các biểu diễn hai chiều của nhân vật và vật thể. Cơ thể nhân vật thường được tạo thành từ nhiều mảnh. Các mảnh được sắp xếp và chụp ảnh một lần cho mỗi khung hình của bộ phim. Họa sĩ hoạt hình di chuyển và xoay các bộ phận theo từng bước nhỏ giữa mỗi lần chụp để tạo ảo giác chuyển động khi các hình ảnh được phát lại nhanh liên tiếp.

Ngày nay, mô phỏng hoạt ảnh cắt dán có thể được tạo bằng phần mềm như trong `South Park <https://en.wikipedia.org/wiki/South_Park>`__ và `Jake and the Never Land Pirates <https://en.wikipedia.org/wiki/Jake_and_the_Never_Land_Pirates>`__.

Trong trò chơi điện tử, kỹ thuật này cũng trở nên phổ biến. Ví dụ về kỹ thuật này là `Paper Mario <https://en.wikipedia.org/wiki/Super_Paper_Mario>`__ hoặc `Rayman Origins <https://en.wikipedia.org/wiki/Rayman_Origins>`__ .

Hoạt ảnh cắt dán trong Godot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot cung cấp các công cụ để làm việc với cutout rig và rất phù hợp với quy trình sau:

-  **Hệ thống animation được tích hợp hoàn toàn với engine**: Điều này có nghĩa là animation có thể điều khiển nhiều thứ hơn chỉ là chuyển động của các vật thể. Texture, kích thước sprite, pivot, độ mờ, điều biến màu và nhiều thuộc tính khác đều có thể được animate và blend. - **Kết hợp các kiểu animation**: AnimatedSprite2D cho phép sử dụng cel animation truyền thống cùng với cutout animation. Trong cel animation, các khung hình animation khác nhau sử dụng những bản vẽ hoàn toàn khác nhau thay vì cùng một mảnh được đặt ở các vị trí khác nhau. Trong một animation vốn dựa trên cutout, cel animation có thể được dùng có chọn lọc cho các phần phức tạp như bàn tay, bàn chân, biểu cảm khuôn mặt thay đổi, v.v. - **Phần tử có hình dạng tùy chỉnh**: Có thể tạo các hình dạng tùy chỉnh bằng
   :ref:`Polygon2D <class_Polygon2D>`
   cho phép animation UV, biến dạng, v.v. - **Hệ thống particle**: Một cutout animation rig có thể được kết hợp với hệ thống particle. Điều này hữu ích cho các hiệu ứng phép thuật, jetpack, v.v. - **Collider tùy chỉnh**: Thiết lập collider và vùng ảnh hưởng ở các phần khác nhau của skeleton, rất phù hợp cho boss và trò chơi đối kháng. - **Animation Tree**: Cho phép kết hợp phức tạp và blend giữa nhiều animation, tương tự như cách hoạt động trong 3D.

Và còn nhiều hơn thế nữa!

Quá trình tạo GBot
~~~~~~~~~~~~~~~~~~

Trong hướng dẫn này, chúng ta sẽ sử dụng các mảnh của nhân vật `GBot <https://www.youtube.com/watch?v=S13FrWuBMx4&list=UUckpus81gNin1aV8WSffRKw>`__ do Andreas Esau tạo làm nội dung minh họa.

.. image:: img/tuto_cutout_walk.gif

Lấy các asset của bạn: `cutout_animation_assets.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/cutout_animation_assets.zip>`_.

Thiết lập rig
~~~~~~~~~~~~~

Tạo một Node2D trống làm root của scene; chúng ta sẽ làm việc bên dưới node này:

.. image:: img/tuto_cutout1.png

Node đầu tiên của model là hông. Nhìn chung, cả trong 2D lẫn 3D, hông là root của skeleton. Điều này giúp animation dễ dàng hơn:

.. image:: img/tuto_cutout2.png

Tiếp theo là thân mình. Thân mình phải là con của hông, vì vậy hãy tạo một sprite con và nạp texture thân mình, sau đó điều chỉnh vị trí cho phù hợp:

.. image:: img/tuto_cutout3.png

Trông ổn rồi. Hãy xem hierarchy của chúng ta có hoạt động như một skeleton hay không bằng cách xoay thân mình. Bạn có thể làm việc này bằng cách nhấn :kbd:`E` để vào chế độ xoay, rồi kéo bằng nút chuột trái. Để thoát khỏi chế độ xoay, nhấn :kbd:`ESC`.

.. image:: img/tutovec_torso1.gif

Pivot xoay đang sai và cần được điều chỉnh.

Dấu thập nhỏ ở giữa :ref:`Sprite2D <class_Sprite2D>` này là pivot xoay:

.. image:: img/tuto_cutout4.png

Điều chỉnh pivot
~~~~~~~~~~~~~~~~

Có thể điều chỉnh pivot bằng cách thay đổi thuộc tính *offset* trong Sprite2D:

.. image:: img/tuto_cutout5.png

Pivot cũng có thể được điều chỉnh *trực quan*. Khi di con trỏ lên điểm pivot mong muốn, nhấn :kbd:`V` để di chuyển pivot đến đó cho Sprite2D đang được chọn. Ngoài ra còn có một công cụ trên thanh công cụ với chức năng tương tự.

.. image:: img/tutovec_torso2.gif

Tiếp tục thêm các mảnh cơ thể, bắt đầu với cánh tay phải. Hãy đảm bảo đặt từng sprite vào đúng vị trí trong hierarchy để các phép xoay và tịnh tiến của nó là tương đối so với node cha:

.. image:: img/tuto_cutout6.png

Với cánh tay trái, chúng ta gặp một vấn đề. Trong 2D, các node con xuất hiện phía trước node cha:

.. image:: img/tuto_cutout7.png

Chúng ta muốn cánh tay trái xuất hiện *phía sau* hông và thân mình. Ta có thể di chuyển các node của cánh tay trái ra phía sau hông (lên trên node hông trong scene hierarchy), nhưng khi đó cánh tay trái không còn ở đúng vị trí trong hierarchy. Điều này có nghĩa là nó sẽ không bị ảnh hưởng bởi chuyển động của thân mình. Chúng ta sẽ khắc phục vấn đề này bằng các node ``RemoteTransform2D``.

.. note:: You can also fix depth ordering problems by adjusting the Z property
   của bất kỳ node nào kế thừa từ Node2D.

Node RemoteTransform2D
~~~~~~~~~~~~~~~~~~~~~~

Node :ref:`RemoteTransform2D <class_RemoteTransform2D>` biến đổi các node ở một vị trí khác trong hierarchy. Node này áp dụng transform của chính nó (bao gồm mọi phép biến đổi mà nó kế thừa từ các node cha) lên node từ xa mà nó nhắm đến.

Điều này cho phép chúng ta điều chỉnh thứ tự hiển thị của các phần tử một cách độc lập với vị trí của những phần đó trong cutout hierarchy.

Tạo một node ``RemoteTransform2D`` làm con của thân mình. Đặt tên nó là ``remote_arm_l``. Tạo một node RemoteTransform2D khác bên trong node đầu tiên và đặt tên là ``remote_hand_l``. Sử dụng thuộc tính ``Remote Path`` của hai node mới để nhắm đến các sprite ``arm_l`` và ``hand_l`` tương ứng:

.. image:: img/tuto_cutout9.png

Giờ đây, việc di chuyển các node ``RemoteTransform2D`` sẽ di chuyển các sprite. Vì vậy, chúng ta có thể tạo animation bằng cách điều chỉnh các transform ``RemoteTransform2D``:

.. image:: img/tutovec_torso4.gif

Hoàn thiện skeleton
~~~~~~~~~~~~~~~~~~~

Hoàn thiện skeleton bằng cách thực hiện các bước tương tự cho những phần còn lại. Scene tạo được sẽ trông tương tự như sau:

.. image:: img/tuto_cutout10.png

Rig tạo được sẽ dễ animate. Bằng cách chọn các node và xoay chúng, bạn có thể animate forward kinematics (FK) một cách hiệu quả.

Với các vật thể và rig đơn giản thì cách này ổn, nhưng có một số hạn chế:

-  Việc chọn các sprite trong main viewport có thể trở nên khó khăn ở những rig phức tạp. Khi đó scene tree thường được dùng để chọn các phần thay thế, nhưng việc này có thể chậm hơn. - Inverse Kinematics (IK) hữu ích để animate các đầu mút như bàn tay và bàn chân, nhưng hiện tại không thể dùng với rig của chúng ta.

Để giải quyết những vấn đề này, chúng ta sẽ sử dụng skeleton của Godot.

Skeleton
~~~~~~~~

Trong Godot có một trợ giúp để tạo "bone" giữa các node. Các node được liên kết bằng bone được gọi là skeleton.

Ví dụ, hãy biến cánh tay phải thành một skeleton. Để tạo skeleton, cần chọn một chuỗi node từ trên xuống dưới:

.. image:: img/tuto_cutout11.png

Sau đó, nhấp vào menu Skeleton và chọn ``Make Bones``.

.. image:: img/tuto_cutout12.png

Thao tác này sẽ thêm các bone bao phủ cánh tay, nhưng kết quả có thể gây bất ngờ.

.. image:: img/tuto_cutout13.png

Tại sao bàn tay lại không có bone? Trong Godot, một bone kết nối một node với node cha của nó. Hiện tại node bàn tay không có node con nào. Với hiểu biết này, hãy thử lại.

Bước đầu tiên là tạo một endpoint node. Có thể dùng bất kỳ loại node nào, nhưng :ref:`Marker2D <class_Marker2D>` được ưu tiên vì nó hiển thị trong editor. Endpoint node sẽ đảm bảo bone cuối cùng có hướng.

.. image:: img/tuto_cutout14.png

Bây giờ hãy chọn toàn bộ chuỗi, từ endpoint đến cánh tay, rồi tạo các bone:

.. image:: img/tuto_cutout15.png

Kết quả trông giống skeleton hơn nhiều, và giờ đây có thể chọn và animate cánh tay cũng như cẳng tay.

Tạo endpoint cho tất cả các đầu mút quan trọng. Tạo bone cho mọi phần có thể khớp nối của cutout, với hông là điểm kết nối cuối cùng giữa tất cả các phần.

Bạn có thể nhận thấy một bone thừa được tạo khi kết nối hông và thân mình. Godot đã kết nối node hông với scene root bằng một bone, nhưng chúng ta không muốn điều đó. Để khắc phục, hãy chọn root và node hông, mở menu Skeleton rồi nhấp vào ``clear bones``.

.. image:: img/tuto_cutout15_2.png

Skeleton cuối cùng của bạn sẽ trông gần giống như sau:

.. image:: img/tuto_cutout16.png

Có thể bạn đã nhận thấy một bộ endpoint thứ hai ở hai bàn tay. Điều này sẽ sớm trở nên hữu ích.

Giờ đây toàn bộ hình người đã được rig, bước tiếp theo là thiết lập các IK chain. IK chain cho phép điều khiển các đầu mút tự nhiên hơn.

IK chain
~~~~~~~~

IK là viết tắt của inverse kinematics. Đây là một kỹ thuật thuận tiện để animate vị trí của bàn tay, bàn chân và các đầu mút khác của những rig như rig chúng ta vừa tạo. Hãy tưởng tượng bạn muốn đặt bàn chân của nhân vật vào một vị trí cụ thể trên mặt đất. Nếu không có IK chain, mỗi chuyển động của bàn chân sẽ yêu cầu xoay và định vị nhiều bone khác (ít nhất là xương cẳng chân và xương đùi). Việc này khá phức tạp và dẫn đến kết quả thiếu chính xác. IK cho phép chúng ta di chuyển trực tiếp bàn chân, trong khi xương cẳng chân và xương đùi tự điều chỉnh.

.. note::

    **IK chain trong Godot hiện chỉ hoạt động trong editor**, không hoạt động tại runtime. Chúng được dùng để giúp quá trình thiết lập keyframe dễ dàng hơn và hiện chưa hữu ích cho các kỹ thuật như procedural animation.

Để tạo một IK chain, hãy chọn một chuỗi bone từ endpoint đến base của chain. Ví dụ, để tạo IK chain cho chân phải, hãy chọn các node sau:

.. image:: img/tuto_cutout17.png

Sau đó bật IK cho chain này. Vào Edit > Make IK Chain.

.. image:: img/tuto_cutout18.png

Kết quả là base của chain sẽ chuyển thành màu *Vàng*.

.. image:: img/tuto_cutout19.png

Sau khi thiết lập IK chain, hãy nắm bất kỳ node con hoặc node cháu nào của base của chain (ví dụ như bàn chân) và di chuyển nó. Bạn sẽ thấy phần còn lại của chain điều chỉnh theo khi bạn thay đổi vị trí của nó.

.. image:: img/tutovec_torso5.gif

Mẹo animation
~~~~~~~~~~~~~

Phần sau đây là tập hợp các mẹo để tạo animation cho cutout rig của bạn. Để biết thêm thông tin về cách hệ thống animation trong Godot hoạt động, hãy xem :ref:`doc_introduction_animation`.

Thiết lập keyframe và loại trừ thuộc tính
-----------------------------------------

Các phần tử theo ngữ cảnh đặc biệt sẽ xuất hiện trên thanh công cụ phía trên khi cửa sổ animation editor đang mở:

.. image:: img/tuto_cutout20.png

Nút key sẽ chèn keyframe vị trí, xoay và scale cho các object hoặc bone được chọn tại vị trí hiện tại của playhead.

Các nút chuyển đổi "loc", "rot" và "scl" ở bên trái nút key sẽ thay đổi chức năng của nút này, cho phép bạn chỉ định keyframe sẽ được tạo cho thuộc tính nào trong ba thuộc tính.

Sau đây là một ví dụ minh họa về tính hữu ích của chức năng này: Hãy tưởng tượng bạn có một node đã có hai keyframe chỉ tạo animation cho scale. Bạn muốn thêm một chuyển động xoay chồng lên cùng node đó. Chuyển động xoay phải bắt đầu và kết thúc ở các thời điểm khác với thay đổi scale đã được thiết lập. Bạn có thể sử dụng các nút chuyển đổi để chỉ thêm thông tin rotation khi thêm keyframe mới. Nhờ vậy, bạn có thể tránh thêm các keyframe scale không mong muốn, vốn sẽ làm gián đoạn animation scale hiện có.

Tạo rest pose
~~~~~~~~~~~~~

Hãy xem rest pose như một pose mặc định mà cutout rig của bạn sẽ được đặt về khi không có pose nào khác đang hoạt động trong game. Tạo rest pose như sau:

1. Đảm bảo các phần của rig được sắp xếp theo một bố cục trông giống như đang "nghỉ".

2. Tạo một animation mới và đổi tên thành "rest".

3. Chọn tất cả các node trong rig của bạn (chọn bằng khung sẽ hoạt động tốt).

4. Đảm bảo các nút chuyển đổi "loc", "rot" và "scl" đều đang bật trên thanh công cụ.

5. Nhấn nút key. Các key sẽ được chèn cho tất cả các phần đã chọn, lưu lại cách sắp xếp hiện tại của chúng. Giờ đây, bạn có thể gọi lại pose này khi cần trong game bằng cách phát animation "rest" mà bạn đã tạo.

.. image:: img/tuto_cutout21.png

Chỉ chỉnh sửa rotation
~~~~~~~~~~~~~~~~~~~~~~

Khi tạo animation cho cutout rig, thường chỉ cần thay đổi rotation của các node. Location và scale hiếm khi được sử dụng.

Vì vậy, khi chèn key, bạn có thể thấy thuận tiện hơn nếu hầu hết thời gian chỉ bật nút chuyển đổi "rot":

.. image:: img/tuto_cutout22.png

Điều này sẽ tránh tạo các animation track không mong muốn cho position và scale.

Tạo keyframe cho các chuỗi IK
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi chỉnh sửa các chuỗi IK, bạn không cần chọn toàn bộ chuỗi để thêm keyframe. Việc chọn endpoint của chuỗi và chèn một keyframe sẽ tự động chèn keyframe cho tất cả các phần còn lại của chuỗi.

Di chuyển một sprite ra phía sau parent theo chiều sâu hiển thị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đôi khi cần để một node thay đổi độ sâu hiển thị so với parent node trong một animation. Hãy hình dung một nhân vật đang quay mặt về phía camera, lấy một vật gì đó ra từ phía sau lưng rồi đưa ra trước mặt. Trong animation này, toàn bộ cánh tay và vật mà nhân vật cầm sẽ cần thay đổi độ sâu hiển thị so với cơ thể của nhân vật.

Để hỗ trợ việc này, tất cả các node kế thừa từ Node2D đều có thuộc tính "Behind Parent" có thể tạo keyframe. Khi lập kế hoạch cho rig, hãy nghĩ đến những chuyển động mà nó cần thực hiện và cân nhắc cách bạn sẽ sử dụng "Behind Parent" và/hoặc các node RemoteTransform2D. Chúng cung cấp chức năng chồng lấp nhau.

.. image:: img/tuto_cutout23.png

Thiết lập đường cong easing cho nhiều key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để áp dụng cùng một đường cong easing cho nhiều keyframe cùng lúc:

1. Chọn các key liên quan. 2. Nhấp vào biểu tượng bút chì ở góc dưới bên phải của animation panel. Thao tác này sẽ mở transition editor. 3. Trong transition editor, nhấp vào đường cong mong muốn để áp dụng.

.. image:: img/tuto_cutout24.png

Biến dạng skeletal 2D
~~~~~~~~~~~~~~~~~~~~~

Skeletal deform có thể được sử dụng để bổ trợ cho cutout rig, cho phép các mảnh riêng lẻ biến dạng tự nhiên (ví dụ: các râu rung rinh khi một nhân vật côn trùng bước đi).

Quy trình này được mô tả trong :ref:`separate tutorial <doc_2d_skeletons>`.
