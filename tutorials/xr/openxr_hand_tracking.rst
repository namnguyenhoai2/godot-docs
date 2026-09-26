.. _doc_openxr_hand_tracking:

Theo dõi bàn tay OpenXR
=======================

Giới thiệu
----------

.. note::

    Trang này tập trung cụ thể vào bộ tính năng được cung cấp thông qua OpenXR. Một phần chức năng được trình bày ở đây cũng áp dụng cho WebXR và có thể được cung cấp bởi các giao diện XR khác.

Khi thảo luận về theo dõi bàn tay, điều quan trọng là phải biết rằng có nhiều quan điểm khác nhau về ranh giới được phân định ở đâu. Kết quả thực tế là có sự khác biệt trong cách triển khai giữa các OpenXR runtime khác nhau. Bạn có thể gặp trường hợp phần cứng đã chọn không hỗ trợ một phần của giải pháp hoặc hoạt động khác biệt đủ nhiều so với các nền tảng khác khiến bạn phải thực hiện thêm công việc.

Tuy vậy, những cải tiến gần đây đối với đặc tả OpenXR đang thu hẹp các khoảng cách này, và khi các nền tảng triển khai những cải tiến đó, chúng ta đang tiến gần hơn đến một tương lai trong đó либо có khả năng chuyển đổi hoàn toàn giữa các nền tảng, hoặc ít nhất có một cách rõ ràng để phát hiện các khả năng của một nền tảng.

Khi nhìn lại những ngày đầu của VR, trọng tâm của các nền tảng lớn là input dựa trên controller được theo dõi. Ở đây, chúng ta theo dõi một thiết bị vật lý cũng có các nút để nhận thêm input. Từ dữ liệu theo dõi, chúng ta có thể suy ra vị trí bàn tay của người chơi, nhưng không biết thêm thông tin nào khác; theo truyền thống, game phải tự triển khai cơ chế hiển thị bàn tay của người chơi và tạo chuyển động cho các ngón tay dựa trên input bổ sung từ controller, dù là do nhấn nút hay thông qua cảm biến tiệm cận. Các ngón tay thường cũng được đặt dựa trên ngữ cảnh, vật người dùng đang cầm và hành động người dùng đang thực hiện.

Gần đây hơn, theo dõi bàn tay bằng quang học đã trở thành một giải pháp phổ biến, trong đó camera theo dõi bàn tay người dùng và cung cấp đầy đủ dữ liệu theo dõi vị trí bàn tay, ngón tay. Nhiều nhà cung cấp coi đây là một hệ thống hoàn toàn tách biệt với việc theo dõi controller và giới thiệu các API độc lập để truy cập vị trí, hướng của bàn tay và ngón tay. Khi xử lý input, nhà phát triển game phải tự triển khai cơ chế phát hiện cử chỉ.

Sự phân tách này cũng tồn tại trong OpenXR, trong đó việc theo dõi controller chủ yếu được xử lý bởi hệ thống action map, còn theo dõi bàn tay bằng quang học chủ yếu được xử lý bởi extension hand tracking API.

Tuy nhiên, thế giới không chỉ có hai màu đen trắng như vậy, và chúng ta đang thấy nhiều tình huống vượt qua ranh giới này:

 *  Các thiết bị phù hợp với cả hai nhóm, chẳng hạn như găng tay được theo dõi và những controller như controller Index cũng thực hiện việc theo dõi ngón tay.
 *  Các XR Runtime triển khai việc suy luận theo dõi bàn tay từ dữ liệu controller nhằm giải quyết việc đặt ngón tay chính xác cho nhiều controller.
 *  Các ứng dụng XR muốn chuyển đổi liền mạch giữa theo dõi controller và theo dõi bàn tay, cung cấp cùng một trải nghiệm người dùng bất kể sử dụng phương pháp nào.

OpenXR đang đáp ứng nhu cầu này bằng cách giới thiệu thêm các extension cho phép chúng ta truy vấn các khả năng của XR runtime/phần cứng hoặc bổ sung chức năng trên ranh giới này. Vấn đề vẫn còn tồn tại hiện nay là việc áp dụng các extension này chưa đồng đều, khiến một số nền tảng không báo cáo đầy đủ các khả năng của mình. Vì vậy, bạn có thể cần kiểm tra các tính năng có trên phần cứng cụ thể và điều chỉnh cách tiếp cận cho phù hợp.

Dự án demo
----------

Thông tin được trình bày trên trang này đã được dùng để tạo một dự án demo, có thể tìm thấy `tại đây <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_hand_tracking_demo>`_.


Hand Tracking API
-----------------

Như đã đề cập trong phần giới thiệu, hand tracking API chủ yếu được sử dụng với theo dõi bàn tay bằng quang học và trên nhiều nền tảng chỉ hoạt động khi người dùng không cầm controller. Một số nền tảng hỗ trợ theo dõi bàn tay được suy luận từ controller, nghĩa là bạn vẫn nhận được dữ liệu theo dõi bàn tay ngay cả khi người dùng đang cầm controller. Các nền tảng này bao gồm SteamVR, Meta Quest (hiện chỉ hỗ trợ native nhưng khả năng hỗ trợ Meta link có thể sẽ sớm được bổ sung) và hy vọng là sắp tới sẽ có thêm các nền tảng khác.

Việc triển khai theo dõi bàn tay trong Godot được chuẩn hóa dựa trên Godot Humanoid Skeleton và hoạt động cả trong OpenXR lẫn WebXR. Vì vậy, các hướng dẫn dưới đây áp dụng cho cả hai môi trường.

Để sử dụng hand tracking API với OpenXR, trước tiên bạn cần bật API này. Bạn có thể thực hiện việc đó trong project settings:

.. image:: img/xr_enable_handtracking.webp

Đối với một số thiết bị XR độc lập, bạn cũng cần cấu hình hand tracking extension trong export settings, chẳng hạn như với Meta Quest:

.. image:: img/openxr_enable_hand_tracking_meta.webp

Bây giờ bạn cần thêm 3 component vào scene cho mỗi bàn tay:

 *  Một node được theo dõi để định vị bàn tay.
 *  Một hand mesh đã được skin đúng cách cùng skeleton.
 *  Một skeleton modifier áp dụng dữ liệu theo dõi ngón tay vào skeleton.

.. image:: img/openxr_hand_tracking_nodes.webp

Hand tracking node
~~~~~~~~~~~~~~~~~~

Hệ thống theo dõi bàn tay sử dụng các hand tracker riêng biệt để theo dõi vị trí bàn tay của người chơi trong không gian theo dõi của chúng ta.

Thông tin này được tách riêng để phục vụ các trường hợp sử dụng sau:

 *  Việc theo dõi diễn ra trong không gian cục bộ của node :ref:`XROrigin3D <class_xrorigin3d>`. Node này phải là node con của node `XROrigin3D` để được đặt đúng vị trí.
 *  Node này có thể được dùng làm mục tiêu IK khi sử dụng upper body mesh có cánh tay thay vì các hand mesh riêng biệt.
 *  Vị trí thực tế của bàn tay có thể chỉ liên kết lỏng lẻo với dữ liệu theo dõi trong những tình huống như UI tạo avatar, gương giả hoặc các trường hợp tương tự, dẫn đến hand mesh và việc theo dõi ngón tay được định vị ở nơi khác.

Chúng ta sẽ chỉ tập trung vào trường hợp sử dụng đầu tiên.

Để thực hiện việc này, bạn cần thêm một node :ref:`XRNode3D <class_xrnode3d>` vào node ``XROrigin3D``.

 *  Trên node này, ``tracker`` phải được đặt thành ``/user/hand_tracker/left`` hoặc ``/user/hand_tracker/right`` tương ứng với bàn tay trái hoặc phải.
 *  ``pose`` phải giữ nguyên giá trị ``default``; không tùy chọn nào khác hoạt động trong trường hợp này.
 *  Checkbox ``Show When Tracked`` sẽ tự động ẩn node này nếu không có dữ liệu theo dõi, hoặc làm node này hiển thị nếu có dữ liệu theo dõi.

Hand mesh có rig
~~~~~~~~~~~~~~~~

Để hiển thị bàn tay, chúng ta cần một hand mesh được rig và skin đúng cách. Vì mục đích này, Godot sử dụng cấu trúc xương bàn tay được định nghĩa cho :ref:`Godot Humanoid <class_skeletonprofilehumanoid>`, đồng thời tùy chọn hỗ trợ thêm một xương đầu cho mỗi ngón tay.

`OpenXR hand tracking demo <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_hand_tracking_demo>`_ chứa các tệp glTF mẫu của những bàn tay được rig đúng cách.

Chúng ta sẽ sử dụng các tệp đó ở đây và thêm chúng làm node con của node ``XRNode3D``. Chúng ta cũng cần bật editable children để truy cập node :ref:`Skeleton3D <class_skeleton3d>`.

Hand skeleton modifier
~~~~~~~~~~~~~~~~~~~~~~

Cuối cùng, chúng ta cần thêm một node :ref:`XRHandModifier3D <class_xrhandmodifier3d>` làm node con của node ``Skeleton3D``. Node này sẽ nhận dữ liệu theo dõi ngón tay từ OpenXR và áp dụng dữ liệu đó vào hand model.

Bạn cần đặt thuộc tính ``Hand Tracker`` thành ``/user/hand_tracker/left`` hoặc ``/user/hand_tracker/right``, tùy theo việc chúng ta đang áp dụng dữ liệu theo dõi tương ứng cho bàn tay trái hay phải.

Bạn cũng có thể đặt chế độ ``Bone Update`` trên node này.

 *  ``Full`` áp dụng đầy đủ dữ liệu tracking bàn tay. Điều này có nghĩa là việc định vị skeleton có thể phản ánh kích thước bàn tay thực tế của người dùng. Điều này có thể dẫn đến hiệu ứng co dúm nếu các mesh không được weight đúng cách để xử lý trường hợp này. Hãy đảm bảo bạn kiểm thử game với người chơi có mọi kích thước khi sử dụng optical hand tracking!
 *  ``Rotation Only`` chỉ áp dụng rotation cho các bone của bàn tay và giữ nguyên độ dài bone. Ở chế độ này, kích thước hand mesh không thay đổi.

Sau khi thêm phần này, khi chạy project, chúng ta sẽ thấy bàn tay được hiển thị chính xác nếu hand tracking được hỗ trợ.

Nguồn dữ liệu hand tracking
---------------------------

Đây là một extension của OpenXR, cung cấp thông tin về nguồn dữ liệu hand tracking. Hiện tại chỉ có một vài runtime triển khai extension này, nhưng nếu extension khả dụng, Godot sẽ kích hoạt nó.

Nếu extension này không được hỗ trợ và do đó trả về unknown, bạn có thể đưa ra các giả định sau:

 *  Nếu bạn đang sử dụng SteamVR (bao gồm Steam link), chỉ hand tracking dựa trên controller được hỗ trợ.
 *  Với mọi runtime khác, nếu hand tracking được hỗ trợ thì chỉ optical hand tracking được hỗ trợ (Lưu ý: Meta Link hiện thuộc nhóm này).
 *  Trong mọi trường hợp khác, hand tracking hoàn toàn không được hỗ trợ.

Bạn có thể truy cập thông tin này thông qua code:

.. code-block:: gdscript

    var hand_tracker : XRHandTracker = XRServer.get_tracker('/user/hand_tracker/left')
    if hand_tracker:
        if hand_tracker.has_tracking_data:
            if hand_tracker.hand_tracking_source == XRHandTracker.HAND_TRACKING_SOURCE_UNKNOWN:
                print("Hand tracking source unknown")
            elif hand_tracker.hand_tracking_source == XRHandTracker.HAND_TRACKING_SOURCE_UNOBSTRUCTED:
                print("Hand tracking source is optical hand tracking")
            elif hand_tracker.hand_tracking_source == XRHandTracker.HAND_TRACKING_SOURCE_CONTROLLER:
                print("Hand tracking data is inferred from controller data")
            else:
                print("Unknown hand tracking source ", hand_tracker.hand_tracking_source)
        else:
            print("Hand is currently not being tracked")
    else:
        print("No hand tracker registered")

Ví dụ này ghi log trạng thái của bàn tay trái.

Nếu trong ví dụ này không có hand tracker nào được ``get_tracker`` trả về, điều đó có nghĩa là hand tracking API hoàn toàn không được hỗ trợ trên XR runtime.

Nếu có tracker nhưng `has_tracking_data` là false, bàn tay của người dùng hiện không được tracking. Nguyên nhân có thể là một trong những lý do sau:

 *  Bàn tay của người chơi không nhìn thấy được bởi bất kỳ camera tracking nào trên headset
 *  Người chơi hiện đang sử dụng controller và headset chỉ hỗ trợ optical hand tracking
 *  Controller đã tắt và chỉ hand tracking bằng controller được hỗ trợ.

Xử lý input của người dùng
--------------------------

Việc phản hồi các action do người dùng thực hiện được xử lý thông qua :ref:`doc_xr_action_map` khi sử dụng controller. Trong action map, bạn có thể ánh xạ nhiều input khác nhau như trigger hoặc joystick trên controller vào một action. Sau đó, action này có thể điều khiển logic trong game.

Khi sử dụng hand tracking, ban đầu chúng ta không có các input như vậy; input được tạo ra bởi các cử chỉ của người dùng, chẳng hạn như nắm tay để grab hoặc chụm ngón cái và ngón trỏ lại với nhau để chọn một thứ gì đó. Nhà phát triển game phải tự triển khai cơ chế này.

Nhận thấy nhu cầu ngày càng tăng đối với các ứng dụng có thể chuyển đổi liền mạch giữa controller và hand tracking, cũng như nhu cầu về một số khả năng input cơ bản, đặc tả đã được bổ sung một số extension cung cấp khả năng nhận diện cử chỉ cơ bản và có thể được sử dụng với action map.

Hand interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~

Extension `hand interaction profile extension <https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_EXT_hand_interaction>`_ là một core extension mới, hỗ trợ các cử chỉ pinch, grasp và poke cùng các pose liên quan. Extension này hiện vẫn được hỗ trợ hạn chế, nhưng sẽ sớm khả dụng trên nhiều runtime hơn.

.. image:: img/openxr_hand_interaction_profile.webp

Cử chỉ pinch được kích hoạt bằng cách chụm ngón cái và ngón trỏ lại với nhau. Cử chỉ này thường được dùng làm cử chỉ select cho các hệ thống menu, tương tự việc dùng controller để trỏ vào một đối tượng rồi nhấn trigger để chọn, và do đó thường được ánh xạ theo cách này.

 *  ``pinch pose`` là một pose nằm ở chính giữa đầu ngón cái và đầu ngón trỏ, đồng thời được định hướng để có thể sử dụng ray cast nhằm xác định target.
 *  Input float ``pinch`` là một giá trị nằm trong khoảng từ 0.0 (đầu ngón cái và ngón trỏ cách nhau) đến 1.0 (đầu ngón cái và ngón trỏ chạm nhau).
 *  Input ``pinch ready`` là true khi các đầu ngón tay (gần như) chạm nhau.

Cử chỉ grasp được kích hoạt bằng cách nắm tay và thường được dùng để nhặt các item, tương tự việc kích hoạt input squeeze trên controller.

 *  Input float ``grasp`` là một giá trị nằm trong khoảng từ 0.0 (bàn tay mở) đến 1.0 (nắm tay).
 *  Input ``grasp ready`` là true khi người dùng nắm tay.

Cử chỉ poke được kích hoạt bằng cách duỗi ngón trỏ; đây là một ngoại lệ nhỏ vì pose ở đầu ngón trỏ thường được dùng để poke một đối tượng có thể tương tác. ``poke pose`` là một pose nằm ở đầu ngón trỏ.

Cuối cùng, input ``aim activate (ready)`` được định nghĩa là một input có giá trị 1.0/true khi ngón trỏ duỗi ra và trỏ vào một target có thể được kích hoạt. Cách các runtime diễn giải input này vẫn chưa rõ.

Với thiết lập này, các tracker ``left_hand`` và ``right_hand`` thông thường được sử dụng, nhờ đó bạn có thể chuyển đổi liền mạch giữa input từ controller và hand tracking.

.. note::

    Bạn cần bật extension hand interaction profile trong phần cài đặt project OpenXR.

Microsoft hand interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Extension `Microsoft hand interaction profile extension <https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_MSFT_hand_interaction>`_ do Microsoft giới thiệu và mô phỏng tương đối đơn giản profile controller. Meta cũng đã bổ sung hỗ trợ cho extension này, nhưng chỉ trên OpenXR client gốc của họ; hiện extension này chưa khả dụng qua Meta Link.

.. image:: img/openxr_msft_hand_interaction_profile.webp

Hỗ trợ pinch được cung cấp thông qua input ``select``; giá trị của input là 0.0 khi đầu ngón cái và ngón trỏ cách nhau, và 1.0 khi chúng chạm nhau.

Lưu ý rằng trong profile này, ``aim pose`` được định nghĩa lại thành một pose nằm giữa ngón cái và ngón trỏ, được định hướng để có thể sử dụng ray cast nhằm xác định target.

Hỗ trợ grasp được cung cấp thông qua input ``squeeze``; giá trị của input là 0.0 khi bàn tay mở và 1.0 khi nắm tay.

Với thiết lập này, các tracker ``left_hand`` và ``right_hand`` thông thường được sử dụng, nhờ đó bạn có thể chuyển đổi liền mạch giữa input từ controller và hand tracking.

HTC hand interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Extension `HTC hand interaction profile extension <https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_HTC_hand_interaction>`_ do HTC giới thiệu và được định nghĩa tương tự extension của Microsoft. Extension này chỉ được HTC hỗ trợ trên các headset Focus 3 và Elite XR.

.. image:: img/openxr_htc_hand_interaction_profile.webp

Xem Microsoft hand interaction profile để biết về hỗ trợ cử chỉ.

Điểm khác biệt cốt lõi là extension này giới thiệu hai tracker mới, ``/user/hand_htc/left`` và ``/user/hand_htc/right``. Điều này có nghĩa là cần triển khai thêm logic để chuyển đổi giữa các tracker mặc định và các tracker dành riêng cho HTC khi người dùng đặt bộ điều khiển xuống hoặc nhấc bộ điều khiển lên.

Profile bộ điều khiển đơn giản
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Profile bộ điều khiển đơn giản là một core profile tiêu chuẩn, được định nghĩa làm profile dự phòng khi sử dụng một bộ điều khiển chưa có profile tương ứng.

Có một số OpenXR runtime sẽ mô phỏng bộ điều khiển thông qua profile bộ điều khiển đơn giản khi sử dụng hand tracking.

Đáng tiếc là không có cách đáng tin cậy nào để xác định liệu một bộ điều khiển không xác định đang được sử dụng hay hand tracking đang mô phỏng một bộ điều khiển thông qua profile này.

.. image:: img/openxr_simple_controller_hand.webp

Các XR runtime được tự do xác định cách profile bộ điều khiển đơn giản hoạt động, vì vậy cũng không có gì đảm bảo về cách profile này được ánh xạ tới các gesture.

Cách ánh xạ phổ biến nhất dường như là ``select click`` có giá trị true khi đầu ngón cái và ngón trỏ chạm nhau trong lúc lòng bàn tay của người dùng hướng ra xa người dùng. ``menu click`` sẽ có giá trị true khi đầu ngón cái và ngón trỏ chạm nhau trong lúc lòng bàn tay của người dùng hướng về phía người dùng.

Với thiết lập này, các tracker ``left_hand`` và ``right_hand`` thông thường sẽ được sử dụng, nhờ đó bạn có thể chuyển đổi liền mạch giữa đầu vào từ bộ điều khiển và hand tracking.

.. note::

    Vì một số interaction profile này có phần chồng lấn, điều quan trọng là bạn cần biết rằng có thể thêm từng profile vào action map, và XR runtime sẽ chọn profile phù hợp nhất.

    Ví dụ, Meta Quest hỗ trợ cả Microsoft hand interaction profile và simple controller profile. Nếu chỉ định cả hai, Microsoft hand interaction profile sẽ được ưu tiên và sử dụng.

    Dự kiến khi Meta hỗ trợ core hand interaction profile extension, profile đó sẽ được ưu tiên hơn cả Microsoft hand interaction profile và simple controller profile.

Đầu vào dựa trên gesture
~~~~~~~~~~~~~~~~~~~~~~~~

Nếu nền tảng không hỗ trợ bất kỳ interaction profile nào khi sử dụng hand tracking, hoặc nếu bạn đang xây dựng một ứng dụng cần hỗ trợ các gesture phức tạp hơn, bạn sẽ cần tự xây dựng hệ thống nhận dạng gesture.

Bạn có thể lấy toàn bộ dữ liệu hand tracking thông qua resource :ref:`XRHandTracker <class_xrhandtracker>` cho mỗi bàn tay. Bạn có thể lấy hand tracker bằng cách gọi ``XRServer.get_tracker`` và sử dụng ``/user/hand_tracker/left`` hoặc ``/user/hand_tracker/left`` làm tracker. Resource này cung cấp quyền truy cập vào toàn bộ thông tin joint của bàn tay tương ứng.

Việc trình bày chi tiết một thuật toán nhận dạng gesture hoàn chỉnh nằm ngoài phạm vi của tài liệu này, tuy nhiên có một số dự án cộng đồng mà bạn có thể tham khảo:

 *  `Thư viện Auto hands của Julian Todd <https://github.com/Godot-Dojo/Godot-XR-AH>`_
 *  `Hand Pose Detector của Malcolm Nixon <https://github.com/Malcolmnixon/GodotXRHandPoseDetector>`_

.. _`here`: https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_hand_tracking_demo
.. _`OpenXR hand tracking demo`: https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_hand_tracking_demo
.. _`hand interaction profile extension`: https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_EXT_hand_interaction
.. _`Microsoft hand interaction profile extension`: https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_MSFT_hand_interaction
.. _`HTC hand interaction profile extension`: https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_HTC_hand_interaction
.. _`Julian Todd's Auto hands library`: https://github.com/Godot-Dojo/Godot-XR-AH
.. _`Malcolm Nixons Hand Pose Detector`: https://github.com/Malcolmnixon/GodotXRHandPoseDetector
