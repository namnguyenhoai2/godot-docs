.. _doc_openxr_settings:

Cài đặt OpenXR
==============

OpenXR có một nhóm cài đặt riêng được áp dụng khi OpenXR khởi động. Mặc dù các extension của OpenXR được triển khai thông qua plugin Godot có thể thêm các cài đặt bổ sung, ở đây chúng ta chỉ thảo luận về các cài đặt trong core của Godot.

.. image:: img/openxr_settings.webp

Cài đặt chung
-------------

Đã bật
~~~~~~

Cài đặt này bật module OpenXR khi Godot khởi động. Đây là yêu cầu bắt buộc khi sử dụng Vulkan backend. Với các backend khác, bạn có thể bật OpenXR bất cứ lúc nào bằng cách gọi ``initialize`` trên :ref:`OpenXRInterface <class_openxrinterface>`.

Bạn cũng cần bật tùy chọn này để truy cập action map editor.

Bạn có thể sử dụng command-line switch ``--xr-mode on`` để buộc tùy chọn này bật.

Action Map mặc định
~~~~~~~~~~~~~~~~~~~

Tùy chọn này chỉ định đường dẫn đến file action map mà OpenXR sẽ tải và dùng để giao tiếp với XR Runtime.

Form Factor
~~~~~~~~~~~

Tùy chọn này chỉ định game của bạn được thiết kế cho:

- các thiết bị ``Head Mounted`` như Meta Quest, Valve Index hoặc Magic Leap, - các thiết bị ``Handheld`` như điện thoại.

Nếu thiết bị mà bạn chạy game không khớp với lựa chọn này, OpenXR sẽ không thể khởi tạo.

View Configuration
~~~~~~~~~~~~~~~~~~

Tùy chọn này chỉ định view configuration mà game của bạn được thiết kế cho:

- ``Mono``, game của bạn cung cấp một đầu ra hình ảnh duy nhất. Ví dụ: AR dựa trên điện thoại; - ``Stereo``, game của bạn cung cấp đầu ra hình ảnh stereo. Ví dụ: các thiết bị đeo trên đầu.

Nếu thiết bị mà bạn chạy game không khớp với lựa chọn này, OpenXR sẽ không thể khởi tạo.

.. note::
  OpenXR có thêm các view configuration dành cho những thiết bị rất đặc thù mà Godot chưa hỗ trợ. Ví dụ, các headset Varjo có một quad view configuration, xuất ra hai bộ hình ảnh stereo. Những cấu hình này có thể được hỗ trợ trong tương lai gần.

Reference Space
~~~~~~~~~~~~~~~

Trong XR, tất cả các phần tử như đầu và tay của người chơi đều được tracking trong một tracking volume. Tại đáy của tracking volume này là điểm gốc của chúng ta, dùng để ánh xạ không gian ảo với không gian thực. Tuy nhiên, có nhiều kịch bản khác nhau đặt điểm này ở những vị trí khác nhau, tùy thuộc vào XR system được sử dụng. Trong OpenXR, các kịch bản này được định nghĩa rõ ràng và được chọn bằng cách thiết lập reference space.

Local
^^^^^

Local reference space mặc định đặt điểm gốc tại đầu của người chơi. Một số XR runtime sẽ thực hiện việc này mỗi khi game khởi động, trong khi các runtime khác sẽ duy trì vị trí này qua các session.

Tuy nhiên, reference space này không ngăn người dùng đi ra xa, vì vậy bạn sẽ cần phát hiện việc đó nếu muốn ngăn người dùng rời khỏi phương tiện mà họ đang điều khiển, điều có thể khiến game bị hỏng.

Reference space này là lựa chọn tốt nhất cho các game mô phỏng bay hoặc mô phỏng đua xe, trong đó chúng ta muốn đặt node :ref:`XROrigin3D <class_xrorigin3d>` tại vị trí đầu của người chơi.

Khi người dùng thực hiện tùy chọn recenter trên headset của họ, với cách thực hiện khác nhau tùy theo XR runtime, XR runtime sẽ di chuyển :ref:`XRCamera3D <class_xrcamera3d>` đến node :ref:`XROrigin3D <class_xrorigin3d>`. :ref:`OpenXRInterface <class_openxrinterface>` cũng sẽ phát signal ``pose_recentered`` để game của bạn có thể phản hồi tương ứng.

.. Note::
  Mọi phần tử khác được XR tracking, chẳng hạn như controller hoặc anchor, cũng sẽ được điều chỉnh tương ứng.

.. Warning::
  Bạn **không** nên gọi ``center_on_hmd`` khi sử dụng reference space này.

Stage
^^^^^

Stage reference space là reference space mặc định của chúng ta và đặt điểm gốc tại tâm của play space. Với các XR runtime cho phép bạn vẽ ranh giới guardian, vị trí và hướng của ranh giới này thường do người dùng thiết lập. Các XR runtime khác có thể quyết định vị trí của điểm này bằng những cách khác. Tuy nhiên, đây là một điểm cố định trong thế giới thực.

Reference space này là lựa chọn tốt nhất cho các game room-scale, nơi người dùng được kỳ vọng sẽ đi lại trong một không gian lớn hơn, hoặc cho các game cần chuyển đổi giữa các game mode. Xem :ref:`Room Scale <doc_xr_room_scale>` để biết thêm thông tin.

Khi người dùng thực hiện tùy chọn recenter trên headset của họ, với cách thực hiện khác nhau tùy theo XR runtime, XR runtime sẽ không thay đổi điểm gốc. :ref:`OpenXRInterface <class_openxrinterface>` sẽ phát signal ``pose_recentered`` và game phải tự phản hồi phù hợp. Nếu không làm vậy, game của bạn sẽ không được chấp nhận trên nhiều store khác nhau.

Trong Godot, bạn có thể thực hiện việc này bằng cách gọi function ``center_on_hmd`` trên :ref:`XRServer <class_xrserver>`:

- Gọi ``XRServer.center_on_hmd(XRServer.RESET_BUT_KEEP_TILT, false)`` sẽ di chuyển node :ref:`XRCamera3D <class_xrcamera3d>` đến node :ref:`XROrigin3D <class_xrorigin3d>`, tương tự reference space ``Local``. - Gọi ``XRServer.center_on_hmd(XRServer.RESET_BUT_KEEP_TILT, true)`` sẽ di chuyển node :ref:`XRCamera3D <class_xrcamera3d>` lên trên node :ref:`XROrigin3D <class_xrorigin3d>`, giữ nguyên chiều cao của người chơi, tương tự reference space ``Local Floor``.

.. Note::
  Mọi phần tử khác được XR tracking, chẳng hạn như controller hoặc anchor, cũng sẽ được điều chỉnh tương ứng.

Local Floor
^^^^^^^^^^^

Local floor reference space tương tự local reference space vì đặt điểm gốc tại vị trí của người chơi. Tuy nhiên, trong mode này, chiều cao của người chơi được giữ nguyên. Cũng như với local reference space, một số XR runtime sẽ duy trì vị trí này qua các session.

Do đó, không có gì đảm bảo người chơi sẽ đứng trên điểm gốc; điều duy nhất được đảm bảo là họ đã đứng ở đó khi người dùng recenter lần cuối. Vì vậy, người chơi cũng có thể tự do đi ra xa.

Reference space này là lựa chọn tốt nhất cho các game mà người dùng được kỳ vọng đứng tại cùng một vị trí, hoặc cho các game kiểu AR, trong đó các phần tử giao diện của người dùng gắn với origin node và nhanh chóng được đặt tại vị trí của người chơi khi recenter.

Khi người dùng thực hiện tùy chọn recenter trên headset của họ, với cách thực hiện khác nhau tùy theo XR runtime, XR runtime sẽ di chuyển :ref:`XRCamera3D <class_xrcamera3d>` lên trên node :ref:`XROrigin3D <class_xrorigin3d>` nhưng vẫn giữ nguyên chiều cao của người chơi. :ref:`OpenXRInterface <class_openxrinterface>` cũng sẽ phát signal ``pose_recentered`` để game của bạn có thể phản hồi tương ứng.

.. Warning::
  Hãy cẩn thận khi sử dụng mode này kết hợp với chuyển động ảo của người chơi. Việc người dùng recenter trong kịch bản này có thể không dự đoán được, trừ khi bạn bù lại chuyển động khi xử lý signal recenter. Điều này thậm chí có thể khiến game bị hỏng, vì trong kịch bản này, người chơi sẽ dịch chuyển đến vị trí trừu tượng mà điểm gốc được đặt tại đó trong quá trình di chuyển ảo, bao gồm cả khả năng người chơi bị dịch chuyển vào những vị trí đáng lẽ bị giới hạn. Tốt hơn hết là sử dụng mode Stage trong kịch bản này và chỉ giới hạn việc reset ở hướng khi nhận được signal ``pose_recentered``.

.. Note::
  Mọi phần tử khác được XR tracking, chẳng hạn như controller hoặc anchor, cũng sẽ được điều chỉnh tương ứng.

.. Warning::
  Bạn **không** nên gọi ``center_on_hmd`` khi sử dụng reference space này.

Environment Blend Mode
~~~~~~~~~~~~~~~~~~~~~~

Environment blend mode xác định cách đầu ra được render của chúng ta hòa trộn vào "thế giới thực", với điều kiện headset hỗ trợ tính năng này.

- ``Opaque`` nghĩa là đầu ra của chúng ta che khuất thế giới thực, tức đang ở VR mode. - ``Additive`` nghĩa là đầu ra của chúng ta được thêm vào thế giới thực; đây là AR mode trong đó hệ thống quang học không cho phép che khuất hoàn toàn thế giới thực (ví dụ: Hololens), - ``Alpha`` nghĩa là đầu ra của chúng ta được hòa trộn với thế giới thực bằng alpha output (viewport phải bật nền trong suốt); đây là AR mode trong đó hệ thống quang học có thể che khuất hoàn toàn thế giới thực (Magic Leap, tất cả thiết bị pass-through, v.v.).

Nếu chọn một mode không được headset hỗ trợ, mode khả dụng đầu tiên sẽ được chọn.

.. Note::
  Một số thiết bị OpenXR có các system riêng để bật/tắt passthrough. Từ Godot 4.3 trở đi, việc chọn alpha blend mode cũng sẽ thực hiện các bước bổ sung này. Tuy nhiên, yêu cầu phải cài đặt vendor plugin mới nhất.

.. _doc_openxr_settings_foveation_level:

Foveation Level
~~~~~~~~~~~~~~~

Thiết lập foveation level được sử dụng khi render, với điều kiện phần cứng được sử dụng hỗ trợ tính năng này. Foveation là kỹ thuật trong đó nội dung được render ở độ phân giải càng thấp khi càng xa tâm viewport. Hầu hết XR runtime chỉ hỗ trợ fixed foveation, nhưng một số runtime sẽ tính đến eye tracking và sử dụng tiêu điểm cho hiệu ứng này.

Level càng cao thì mức tăng hiệu năng càng tốt, nhưng chất lượng ở vùng nhìn ngoại vi của người dùng cũng bị giảm nhiều hơn.

.. Note::
  **Chỉ dành cho Compatibility renderer**, với Mobile và Forward+ renderer, hãy thiết lập property ``vrs_mode`` trên :ref:`Viewport <class_viewport>` thành ``VRS_XR``.

.. Warning::
  Tính năng này bị tắt nếu sử dụng các post effect như glow, bloom hoặc DOF.

Foveation Dynamic
~~~~~~~~~~~~~~~~~

Khi được bật, foveation level sẽ tự động điều chỉnh tùy theo GPU load hiện tại. Level sẽ được điều chỉnh trong khoảng từ low đến foveation level được chọn ở cài đặt trước đó. Vì vậy, tốt nhất nên kết hợp cài đặt này với foveation level được đặt ở high.

.. Note::
  **Chỉ dành cho Compatibility renderer**

Submit Depth Buffer
~~~~~~~~~~~~~~~~~~~

Nếu được bật, depth buffer do OpenXR cung cấp sẽ được sử dụng trong quá trình render và được submit cùng với hình ảnh đã render. XR runtime có thể sử dụng buffer này để cải thiện reprojection.

.. Note::
  Bật tính năng này sẽ tắt stencil support trong quá trình render. Không có nhiều XR runtime sử dụng tính năng này; bạn nên để cài đặt này tắt, trừ khi nó mang lại lợi ích rõ rệt cho use case của bạn.

Startup Alert
~~~~~~~~~~~~~

Nếu được bật, tùy chọn này sẽ hiển thị thông báo cảnh báo cho người dùng nếu OpenXR không khởi động được. Không phải lúc nào chúng ta cũng nhận được phản hồi từ hệ thống XR về lý do khởi động thất bại. Nếu có, chúng ta sẽ ghi lại thông tin này vào console. Các lý do thường gặp là:

- Không cài đặt OpenXR runtime trên hệ thống máy chủ. - OpenXR runtime WMR của Microsoft hiện đang hoạt động; runtime này chỉ hỗ trợ DirectX và sẽ thất bại nếu sử dụng OpenGL hoặc Vulkan. - SteamVR được sử dụng nhưng chưa kết nối/bật headset.

Tắt tùy chọn này nếu game của bạn hỗ trợ chế độ fallback để có thể chơi ở chế độ desktop khi không kết nối headset VR, hoặc nếu bạn tự xử lý điều kiện thất bại bằng cách kiểm tra ``OpenXRInterface.is_initialized()``.

Extensions
----------

Phân mục này cho phép bạn bật nhiều OpenXR extension tùy chọn khác nhau. Hãy lưu ý rằng các extension chỉ hoạt động nếu OpenXR runtime (SteamVR, Oculus, v.v.) mà project đang chạy cùng hỗ trợ chúng.

Debug Utils
~~~~~~~~~~~

Bật tùy chọn này sẽ ghi các debug message từ XR runtime.

Debug Message Types
~~~~~~~~~~~~~~~~~~~

Tùy chọn này cho phép bạn chọn những debug message nào được ghi lại.

Frame Synthesis
~~~~~~~~~~~~~~~

Khi được bật, với điều kiện XR runtime hỗ trợ, các buffer motion vector và depth ở độ phân giải thấp hơn sẽ được render và cung cấp cho XR runtime. Sau đó, XR runtime có thể chèn các frame reprojection và bù cho framerate thấp hơn.

Hiện tại có các hạn chế sau:

- KHÔNG hoạt động trong Forward+ renderer. - Chỉ hoạt động với stereo rendering.

Hand Tracking
~~~~~~~~~~~~~

Tùy chọn này bật hand tracking extension khi được device đang sử dụng hỗ trợ. Theo mặc định, tùy chọn này được bật vì lý do tương thích với legacy. Hand tracking extension cung cấp quyền truy cập vào dữ liệu cho phép bạn hiển thị bàn tay của người dùng với vị trí ngón tay chính xác. Tùy thuộc vào khả năng của platform, dữ liệu hand tracking có thể được suy ra từ input của controller, lấy từ găng tay dữ liệu, lấy từ các cảm biến optical hand tracking hoặc bất kỳ nguồn phù hợp nào khác.

Nếu game của bạn chỉ hỗ trợ controller, tùy chọn này nên được tắt.

Xem trang về :ref:`hand tracking <doc_openxr_hand_tracking>` để biết thêm chi tiết.

Hand Tracking Unobstructed Data Source
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bật tùy chọn này có nghĩa là hand tracking có thể sử dụng vị trí chính xác của các ngón tay, thường là vị trí mà camera của headset nhìn thấy.

Hand Tracking Controller Data Source
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bật tùy chọn này có nghĩa là hand tracking có thể sử dụng chính controller và suy ra vị trí các ngón tay dựa trên input của controller hoặc các cảm biến trên controller.

Hand Interaction Profile
~~~~~~~~~~~~~~~~~~~~~~~~

Bật extension này cho phép sử dụng hai hand tracking pose mới. Pinch pose là vị trí giữa ngón cái và ngón trỏ hướng về phía trước, còn poke pose nằm ở đầu ngón trỏ.

Tùy chọn này cũng cho phép thêm 3 input dựa trên gesture. Pinch, khi người dùng chụm ngón cái và ngón trỏ lại với nhau. Aim activation, khi ngón trỏ duỗi hoàn toàn. Và Grasps, khi người dùng nắm chặt bàn tay.

Khi hand interaction profile và controller interaction profile được cung cấp, runtime sẽ chuyển đổi giữa các profile tùy thuộc vào việc có sử dụng optical tracking hay người dùng đang cầm controller.

Nếu chỉ cung cấp hand interaction profile, mọi runtime sẽ sử dụng hand interaction ngay cả khi đang cầm controller.

Spatial Entities
~~~~~~~~~~~~~~~~

Extension này và các thiết lập của nó được sử dụng để lấy và tương tác với thông tin về môi trường thực tế của người dùng. Bạn có thể tìm thông tin chi tiết hơn về cách hoạt động của nó tại :ref:`spatial entities page <doc_openxr_spatial_entities>`.

Eye Gaze Interaction
~~~~~~~~~~~~~~~~~~~~

Tùy chọn này bật eye gaze interaction extension khi được device đang sử dụng hỗ trợ. Khi được bật, chúng ta sẽ nhận phản hồi từ eye tracking thông qua một pose nằm giữa hai mắt của người dùng và hướng theo hướng người dùng đang nhìn. Đây sẽ là một orientation thống nhất.

Để sử dụng chức năng này, bạn cần chỉnh sửa action map và thêm một pose action mới, chẳng hạn như ``eye_pose``. Tiếp theo, hãy thêm một interaction profile mới cho eye gaze interaction và ánh xạ ``eye_pose``:

.. image:: img/openxr_eye_gaze_interaction.webp

Đừng quên lưu!

Tiếp theo, hãy thêm một node :ref:`XRController3D <class_xrcontroller3d>` mới vào origin node của bạn, đặt thuộc tính ``tracker`` của node này thành ``/user/eyes_ext`` và đặt thuộc tính ``pose`` thành ``eye_pose``.

Giờ bạn có thể thêm các thành phần như raycast vào controller node này và điều khiển chúng bằng mắt.

Render Models
~~~~~~~~~~~~~

Extension này được sử dụng để truy vấn XR runtime nhằm lấy các tài sản 3D của phần cứng đang được sử dụng, thường là controller, cũng như vị trí của phần cứng đó. Bạn có thể tìm hướng dẫn chi tiết về cách sử dụng nó tại :ref:`here <doc_openxr_render_models>`.

Binding Modifiers
-----------------

Các tùy chọn này kiểm soát việc có thể sử dụng binding modifiers hay không. Binding modifiers được dùng để áp dụng các ngưỡng hoặc giá trị offset. Bạn có thể tìm thông tin về cách sử dụng và thiết lập chúng trên trang XR action map tại :ref:`here <doc_binding_modifiers>`.

Analog Threshold
~~~~~~~~~~~~~~~~

Cho phép các binding modifier analog threshold.

Dpad Binding
~~~~~~~~~~~~

Cho phép các binding modifier D-pad.
