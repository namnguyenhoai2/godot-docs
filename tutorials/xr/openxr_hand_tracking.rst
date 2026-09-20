.. _doc_openxr_hand_tracking:

Theo dõi bàn tay OpenXR
=======================

Giới thiệu
----------

.. note::

    Trang này tập trung cụ thể vào tập hợp tính năng được cung cấp thông qua OpenXR. Một phần chức năng được trình bày ở đây cũng áp dụng cho WebXR và có thể được cung cấp bởi các giao diện XR khác.

Khi thảo luận về tính năng theo dõi bàn tay, điều quan trọng là phải biết rằng có nhiều quan điểm khác nhau về ranh giới được đặt ở đâu. Kết quả thực tế là có sự khác biệt trong cách triển khai giữa các OpenXR runtime khác nhau. Bạn có thể gặp trường hợp phần cứng đã chọn không hỗ trợ một mảnh ghép nào đó, hoặc hoạt động đủ khác so với các nền tảng khác khiến bạn phải thực hiện thêm công việc.

Dù vậy, những cải tiến gần đây đối với đặc tả OpenXR đang thu hẹp các khoảng cách này, và khi các nền tảng triển khai những cải tiến đó, chúng ta đang tiến gần hơn đến một tương lai trong đó hoặc là có khả năng chuyển đổi hoàn toàn giữa các nền tảng, hoặc ít nhất có một cách rõ ràng để phát hiện các capability của một nền tảng.

Khi nhìn lại những ngày đầu của VR, trọng tâm của các nền tảng lớn là input dựa trên controller được theo dõi. Ở đây, chúng ta theo dõi một thiết bị vật lý cũng có các nút để nhận thêm input. Từ dữ liệu theo dõi, chúng ta có thể suy ra vị trí bàn tay của người chơi, nhưng không biết thêm thông tin nào khác; theo cách truyền thống, game phải tự triển khai cơ chế để hiển thị bàn tay của người chơi và animate các ngón tay dựa trên input bổ sung từ controller, dù input đó đến từ việc nhấn nút hay từ các cảm biến tiệm cận. Các ngón tay thường cũng được đặt dựa trên ngữ cảnh, thứ người dùng đang cầm và hành động người dùng đang thực hiện.

Gần đây hơn, optical hand tracking đã trở thành một giải pháp phổ biến, trong đó camera theo dõi bàn tay người dùng và cung cấp đầy đủ dữ liệu theo dõi vị trí bàn tay, ngón tay. Nhiều nhà cung cấp xem đây là một hệ thống hoàn toàn tách biệt với controller tracking và giới thiệu các API độc lập để truy cập vị trí bàn tay, ngón tay và dữ liệu orientation. Khi xử lý input, game developer phải tự triển khai cơ chế phát hiện gesture.

Sự phân tách này cũng tồn tại trong OpenXR, trong đó controller tracking chủ yếu được xử lý bởi hệ thống action map, còn optical hand tracking chủ yếu được xử lý bởi extension hand tracking API.

Tuy nhiên, thế giới không chỉ có hai màu trắng và đen, và chúng ta đang thấy một số tình huống trong đó hai phạm vi này giao nhau:

 *  Các thiết bị phù hợp với cả hai nhóm, chẳng hạn như găng tay được theo dõi và các controller như Index controller, vốn cũng thực hiện finger tracking. * Các XR Runtime triển khai inferred hand tracking từ dữ liệu controller nhằm giải quyết việc đặt ngón tay chính xác cho nhiều controller. * Các XR application muốn chuyển đổi liền mạch giữa controller và hand tracking, mang lại cùng một trải nghiệm người dùng bất kể sử dụng phương pháp nào.

OpenXR đang đáp lại nhu cầu này bằng cách giới thiệu thêm các extension cho phép chúng ta truy vấn capability của XR runtime/hardware hoặc bổ sung thêm chức năng vượt qua ranh giới này. Vấn đề hiện vẫn còn là các extension này chưa được áp dụng đồng đều, nên một số nền tảng chưa báo cáo đầy đủ capability của mình. Vì vậy, bạn có thể cần kiểm tra các feature có sẵn trên phần cứng cụ thể và điều chỉnh cách tiếp cận cho phù hợp.

Dự án demo
----------

Thông tin được trình bày trên trang này đã được dùng để tạo một dự án demo có thể tìm thấy `here <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_hand_tracking_demo>`_.


Hand Tracking API
-----------------

Như đã đề cập trong phần giới thiệu, hand tracking API chủ yếu được sử dụng với optical hand tracking và trên nhiều nền tảng chỉ hoạt động khi người dùng không cầm controller. Một số nền tảng hỗ trợ controller inferred hand tracking, nghĩa là bạn vẫn nhận được dữ liệu hand tracking ngay cả khi người dùng đang cầm controller. Các nền tảng này bao gồm SteamVR, Meta Quest (hiện chỉ native, nhưng hỗ trợ Meta link có khả năng sẽ sớm được bổ sung), và hy vọng sắp tới sẽ có thêm các nền tảng khác.

Cách triển khai hand tracking trong Godot đã được chuẩn hóa xoay quanh Godot Humanoid Skeleton và hoạt động cả trong OpenXR lẫn WebXR. Do đó, các hướng dẫn bên dưới sẽ hoạt động trong cả hai môi trường.

Để sử dụng hand tracking API với OpenXR, trước tiên bạn cần bật nó. Bạn có thể thực hiện việc này trong project settings:

.. image:: img/xr_enable_handtracking.webp

Đối với một số thiết bị XR độc lập, bạn cũng cần cấu hình hand tracking extension trong export settings, chẳng hạn như với Meta Quest:

.. image:: img/openxr_enable_hand_tracking_meta.webp

Bây giờ bạn cần thêm 3 component vào scene cho mỗi bàn tay:

 *  Một tracked node để định vị bàn tay. * Một hand mesh có skeleton, được skin đúng cách. * Một skeleton modifier áp dụng dữ liệu finger tracking vào skeleton.

.. image:: img/openxr_hand_tracking_nodes.webp

Hand tracking node
~~~~~~~~~~~~~~~~~~

Hệ thống hand tracking sử dụng các hand tracker riêng biệt để theo dõi vị trí bàn tay của người chơi trong tracking space của chúng ta.

Thông tin này được tách riêng để phục vụ các trường hợp sử dụng sau:

 *  Việc tracking diễn ra trong local space của node :ref:`XROrigin3D <class_xrorigin3d>`. Node này phải là child của node `XROrigin3D` để được đặt đúng vị trí. * Node này có thể được sử dụng làm IK target khi dùng upper body mesh có cánh tay thay vì các hand mesh riêng biệt. * Vị trí thực tế của bàn tay có thể chỉ ràng buộc lỏng lẻo với tracking trong các tình huống như UI tạo avatar, fake mirror hoặc các trường hợp tương tự, khiến hand mesh và finger tracking được localize ở nơi khác.

Chúng ta sẽ chỉ tập trung vào trường hợp sử dụng đầu tiên.

Để làm việc này, bạn cần thêm một node :ref:`XRNode3D <class_xrnode3d>` vào node ``XROrigin3D``.

 *  Trên node này, ``tracker`` phải được đặt thành ``/user/hand_tracker/left`` hoặc ``/user/hand_tracker/right``, tương ứng với bàn tay trái hoặc phải. * ``pose`` phải được giữ ở giá trị ``default``; không tùy chọn nào khác hoạt động ở đây. * Checkbox ``Show When Tracked`` sẽ tự động ẩn node này nếu không có dữ liệu tracking, hoặc làm node này hiển thị nếu có dữ liệu tracking.

Hand mesh có rig
~~~~~~~~~~~~~~~~

Để hiển thị bàn tay, chúng ta cần một hand mesh đã được rig và skin đúng cách. Để thực hiện việc này, Godot sử dụng cấu trúc hand bone được định nghĩa cho :ref:`Godot Humanoid <class_skeletonprofilehumanoid>`, nhưng tùy chọn hỗ trợ thêm một tip bone cho mỗi ngón tay.

`OpenXR hand tracking demo <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_hand_tracking_demo>`_ chứa các tệp glTF mẫu của những bàn tay đã được rig đúng cách.

Chúng ta sẽ sử dụng các tệp đó ở đây và thêm chúng làm child của node ``XRNode3D``. Chúng ta cũng cần bật editable children để truy cập node :ref:`Skeleton3D <class_skeleton3d>`.

Skeleton modifier của bàn tay
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cuối cùng, chúng ta cần thêm một node :ref:`XRHandModifier3D <class_xrhandmodifier3d>` làm child của node ``Skeleton3D``. Node này sẽ nhận dữ liệu finger tracking từ OpenXR và áp dụng dữ liệu đó vào hand model.

Bạn cần đặt property ``Hand Tracker`` thành ``/user/hand_tracker/left`` hoặc ``/user/hand_tracker/right``, tùy thuộc vào việc chúng ta đang áp dụng dữ liệu tracking của bàn tay trái hay phải.

Bạn cũng có thể đặt mode ``Bone Update`` trên node này.

 *  ``Full`` áp dụng đầy đủ dữ liệu hand tracking. Điều này có nghĩa là vị trí skeleton có thể phản ánh kích thước bàn tay thực tế của người dùng. Việc này có thể dẫn đến hiệu ứng co dúm nếu mesh không được weight đúng cách để tính đến điều đó. Hãy đảm bảo bạn kiểm thử game với người chơi có mọi kích thước khi sử dụng optical hand tracking! * ``Rotation Only`` chỉ áp dụng rotation cho các bone của bàn tay và giữ nguyên độ dài bone. Ở mode này, kích thước của hand mesh không thay đổi.

Sau khi thêm thành phần này, khi chạy project, chúng ta sẽ thấy bàn tay được hiển thị chính xác nếu hand tracking được hỗ trợ.

Nguồn dữ liệu hand tracking
---------------------------

Đây là một OpenXR extension cung cấp thông tin về nguồn của dữ liệu hand tracking. Hiện tại chỉ có một vài runtime triển khai extension này, nhưng nếu extension khả dụng, Godot sẽ kích hoạt nó.

Nếu extension này không được hỗ trợ và do đó trả về unknown, bạn có thể đưa ra các giả định sau:

 *  Nếu bạn đang sử dụng SteamVR (bao gồm Steam link), chỉ controller based hand tracking được hỗ trợ. * Với mọi runtime khác, nếu hand tracking được hỗ trợ thì chỉ optical hand tracking được hỗ trợ (Lưu ý: Meta Link hiện thuộc trường hợp này). * Trong mọi trường hợp còn lại, hand tracking hoàn toàn không được hỗ trợ.

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

Nếu trong ví dụ này không có hand tracker nào được ``get_tracker`` trả về, điều đó có nghĩa là hand tracking API hoàn toàn không được XR runtime hỗ trợ.

Nếu có tracker nhưng `has_tracking_data` là false, bàn tay của người dùng hiện không được tracking. Nguyên nhân có thể là một trong những lý do sau:

 *  Bàn tay của người chơi không hiển thị trong bất kỳ camera tracking nào trên headset * Người chơi hiện đang sử dụng controller và headset chỉ hỗ trợ optical hand tracking * Controller đã tắt và chỉ controller hand tracking được hỗ trợ.

Xử lý user input
----------------

Việc phản hồi các action do người dùng thực hiện được xử lý thông qua :ref:`doc_xr_action_map` nếu sử dụng controller. Trong action map, bạn có thể ánh xạ nhiều input khác nhau, chẳng hạn như trigger hoặc joystick trên controller, vào một action. Sau đó, action này có thể điều khiển logic trong game.

Khi sử dụng hand tracking, ban đầu chúng ta không có những input như vậy; input được tạo ra bởi các gesture do người dùng thực hiện, chẳng hạn như nắm tay để grab hoặc chụm ngón cái và ngón trỏ lại với nhau để chọn một thứ gì đó. Game developer phải tự triển khai cơ chế này.

Nhận thấy nhu cầu ngày càng tăng đối với các ứng dụng có thể chuyển đổi liền mạch giữa tracking bằng controller và tracking bằng tay, cũng như nhu cầu về một dạng khả năng nhập liệu cơ bản, một số extension đã được thêm vào specification để cung cấp khả năng nhận diện gesture cơ bản và có thể được sử dụng với action map.

Hand interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~

`hand interaction profile extension <https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_EXT_hand_interaction>`_ là một core extension mới hỗ trợ các gesture pinch, grasp và poke, cùng các pose liên quan. Extension này hiện vẫn được hỗ trợ hạn chế, nhưng dự kiến sẽ khả dụng trong nhiều runtime hơn trong tương lai gần.

.. image:: img/openxr_hand_interaction_profile.webp

Gesture pinch được kích hoạt bằng cách chụm ngón cái và ngón trỏ lại với nhau. Gesture này thường được sử dụng như một gesture select cho các hệ thống menu, tương tự như việc dùng controller để trỏ vào một đối tượng và nhấn trigger để chọn, vì vậy thường được mapping theo cách này.

 *  ``pinch pose`` là một pose được đặt ở chính giữa đầu ngón cái và đầu ngón trỏ, đồng thời được định hướng để có thể sử dụng ray cast nhằm xác định target. * Input float ``pinch`` là một giá trị từ 0.0 (đầu ngón cái và ngón trỏ cách nhau) đến 1.0 (đầu ngón cái và ngón trỏ chạm nhau). * Input ``pinch ready`` có giá trị true khi các đầu ngón tay (gần như) chạm nhau.

Gesture grasp được kích hoạt bằng cách nắm bàn tay thành nắm đấm và thường được dùng để nhặt các vật thể lên, tương tự như việc kích hoạt input squeeze trên controller.

 *  Input float ``grasp`` là một giá trị từ 0.0 (bàn tay mở) đến 1.0 (nắm đấm). * Input ``grasp ready`` có giá trị true khi người dùng nắm tay thành nắm đấm.

Gesture poke được kích hoạt bằng cách duỗi ngón trỏ; đây là một ngoại lệ nhỏ vì pose ở đầu ngón trỏ thường được dùng để chọc vào một đối tượng có thể tương tác. ``poke pose`` là một pose được đặt ở đầu ngón trỏ.

Cuối cùng, input ``aim activate (ready)`` được định nghĩa là một input có giá trị 1.0/true khi ngón trỏ được duỗi ra và đang trỏ vào một target có thể được kích hoạt. Cách các runtime diễn giải điều này vẫn chưa rõ.

Với thiết lập này, các tracker ``left_hand`` và ``right_hand`` thông thường được sử dụng, do đó bạn có thể chuyển đổi liền mạch giữa input tracking bằng controller và tracking bằng tay.

.. note::

    Bạn cần bật extension hand interaction profile trong phần cài đặt project OpenXR.

Microsoft hand interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Microsoft hand interaction profile extension <https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_MSFT_hand_interaction>`_ được Microsoft giới thiệu và mô phỏng tương đối giống profile controller đơn giản. Meta cũng đã thêm hỗ trợ cho extension này, nhưng chỉ trên OpenXR client native của họ; hiện extension này chưa khả dụng qua Meta Link.

.. image:: img/openxr_msft_hand_interaction_profile.webp

Hỗ trợ pinch được cung cấp thông qua input ``select``; giá trị của input này là 0.0 khi đầu ngón cái và ngón trỏ cách nhau, và 1.0 khi chúng chạm nhau.

Lưu ý rằng trong profile này, ``aim pose`` được định nghĩa lại thành một pose nằm giữa ngón cái và ngón trỏ, được định hướng để có thể sử dụng ray cast nhằm xác định target.

Hỗ trợ grasp được cung cấp thông qua input ``squeeze``; giá trị của input này là 0.0 khi bàn tay mở và 1.0 khi bàn tay nắm thành nắm đấm.

Với thiết lập này, các tracker ``left_hand`` và ``right_hand`` thông thường được sử dụng, do đó bạn có thể chuyển đổi liền mạch giữa input tracking bằng controller và tracking bằng tay.

HTC hand interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`HTC hand interaction profile extension <https://github.khronos.org/OpenXR-Inventory/extension_support.html#XR_HTC_hand_interaction>`_ được HTC giới thiệu và được định nghĩa tương tự extension của Microsoft. Extension này chỉ được HTC hỗ trợ trên các headset Focus 3 và Elite XR.

.. image:: img/openxr_htc_hand_interaction_profile.webp

Xem Microsoft hand interaction profile để biết về hỗ trợ gesture.

Điểm khác biệt chính là extension này giới thiệu hai tracker mới, ``/user/hand_htc/left`` và ``/user/hand_htc/right``. Điều này có nghĩa là cần triển khai logic bổ sung để chuyển đổi giữa các tracker mặc định và các tracker riêng của HTC khi người dùng đặt controller xuống hoặc cầm controller lên.

Simple controller profile
~~~~~~~~~~~~~~~~~~~~~~~~~

Simple controller profile là một core profile tiêu chuẩn, được định nghĩa làm profile dự phòng khi sử dụng một controller chưa có profile tương ứng.

Có một số OpenXR runtime sẽ mô phỏng controller thông qua simple controller profile khi sử dụng hand tracking.

Đáng tiếc là không có cách đáng tin cậy để xác định liệu một controller không xác định đang được sử dụng hay hand tracking đang mô phỏng controller thông qua profile này.

.. image:: img/openxr_simple_controller_hand.webp

Các XR runtime được tự do định nghĩa cách simple controller profile hoạt động, vì vậy cũng không chắc chắn profile này được mapping với gesture như thế nào.

Cách mapping phổ biến nhất dường như là ``select click`` có giá trị true khi đầu ngón cái và ngón trỏ chạm nhau trong khi lòng bàn tay của người dùng hướng ra xa người dùng. ``menu click`` sẽ có giá trị true khi đầu ngón cái và ngón trỏ chạm nhau trong khi lòng bàn tay của người dùng hướng về phía người dùng.

Với thiết lập này, các tracker ``left_hand`` và ``right_hand`` thông thường được sử dụng, do đó bạn có thể chuyển đổi liền mạch giữa input tracking bằng controller và tracking bằng tay.

.. note::

    Vì một số interaction profile có phần chồng lấp, điều quan trọng cần biết là bạn có thể thêm từng profile vào action map, và XR runtime sẽ chọn profile phù hợp nhất.

    Chẳng hạn, Meta Quest hỗ trợ cả Microsoft hand interaction profile và simple controller profile. Nếu chỉ định cả hai, Microsoft hand interaction profile sẽ được ưu tiên và được sử dụng.

    Dự kiến một khi Meta hỗ trợ core hand interaction profile extension, profile đó sẽ được ưu tiên hơn cả Microsoft profile và simple controller profile.

Input dựa trên gesture
~~~~~~~~~~~~~~~~~~~~~~

Nếu platform không hỗ trợ interaction profile nào khi sử dụng hand tracking, hoặc nếu bạn đang xây dựng một ứng dụng cần hỗ trợ gesture phức tạp hơn, bạn sẽ cần xây dựng hệ thống nhận diện gesture của riêng mình.

Bạn có thể lấy toàn bộ dữ liệu hand tracking thông qua resource :ref:`XRHandTracker <class_xrhandtracker>` cho mỗi bàn tay. Bạn có thể lấy hand tracker bằng cách gọi ``XRServer.get_tracker`` và sử dụng ``/user/hand_tracker/left`` hoặc ``/user/hand_tracker/left`` làm tracker. Resource này cung cấp quyền truy cập vào toàn bộ thông tin joint của bàn tay tương ứng.

Việc trình bày chi tiết một thuật toán nhận diện gesture hoàn chỉnh nằm ngoài phạm vi của manual này, tuy nhiên có một số dự án cộng đồng mà bạn có thể tham khảo:

 *  `Julian Todd's Auto hands library <https://github.com/Godot-Dojo/Godot-XR-AH>`_ * `Malcolm Nixons Hand Pose Detector <https://github.com/Malcolmnixon/GodotXRHandPoseDetector>`_
