.. _doc_openxr_settings:

Cài đặt OpenXR
==============

OpenXR có bộ cài đặt riêng được áp dụng khi OpenXR khởi động. Mặc dù các extension OpenXR được triển khai thông qua plugin Godot có thể thêm các cài đặt bổ sung, ở đây chúng ta chỉ thảo luận về các cài đặt trong phần lõi của Godot.

.. image:: img/openxr_settings.webp

Cài đặt chung
-------------

Đã bật
~~~~~~

Cài đặt này bật module OpenXR khi Godot khởi động. Cài đặt này bắt buộc khi sử dụng backend Vulkan. Với các backend khác, bạn có thể bật OpenXR bất kỳ lúc nào bằng cách gọi ``initialize`` trên :ref:`OpenXRInterface <class_openxrinterface>`.

Bạn cũng cần bật cài đặt này để truy cập trình chỉnh sửa action map.

Bạn có thể sử dụng tùy chọn dòng lệnh ``--xr-mode on`` để buộc bật cài đặt này.

Action Map mặc định
~~~~~~~~~~~~~~~~~~~

Cài đặt này chỉ định đường dẫn đến tệp action map mà OpenXR sẽ tải và giao tiếp với XR Runtime.

Form Factor
~~~~~~~~~~~

Cài đặt này chỉ định game của bạn được thiết kế cho:

- thiết bị ``Head Mounted`` như Meta Quest, Valve Index hoặc Magic Leap,
- thiết bị ``Handheld`` như điện thoại.

Nếu thiết bị chạy game của bạn không khớp với lựa chọn ở đây, OpenXR sẽ không thể khởi tạo.

Cấu hình chế độ xem
~~~~~~~~~~~~~~~~~~~

Cài đặt này chỉ định cấu hình chế độ xem mà game của bạn được thiết kế cho:

- ``Mono``, game của bạn cung cấp đầu ra một hình ảnh. Ví dụ: AR dựa trên điện thoại;
- ``Stereo``, game của bạn cung cấp đầu ra hình ảnh stereo. Ví dụ: các thiết bị đeo trên đầu.

Nếu thiết bị chạy game của bạn không khớp với lựa chọn ở đây, OpenXR sẽ không thể khởi tạo.

.. note::
  OpenXR có thêm các cấu hình chế độ xem dành cho những thiết bị rất đặc thù mà Godot chưa hỗ trợ. Chẳng hạn, headset Varjo có cấu hình chế độ xem quad, xuất ra hai bộ hình ảnh stereo. Các cấu hình này có thể được hỗ trợ trong tương lai gần.

Không gian tham chiếu
~~~~~~~~~~~~~~~~~~~~~

Trong XR, mọi thành phần như đầu và tay của người chơi đều được theo dõi trong một vùng tracking. Ở đáy của vùng tracking này là điểm gốc, dùng để ánh xạ không gian ảo với không gian thực. Tuy nhiên, có những tình huống khác nhau đặt điểm này ở các vị trí khác nhau, tùy thuộc vào hệ thống XR được sử dụng. Trong OpenXR, các tình huống này được định nghĩa rõ ràng và được chọn bằng cách thiết lập một không gian tham chiếu.

Cục bộ
^^^^^^

Không gian tham chiếu cục bộ mặc định đặt điểm gốc tại đầu của người chơi. Một số XR runtime sẽ thực hiện việc này mỗi khi game khởi động, trong khi các runtime khác sẽ duy trì vị trí này qua các phiên.

Tuy nhiên, không gian tham chiếu này không ngăn người dùng đi ra xa, vì vậy bạn sẽ cần phát hiện việc đó nếu muốn ngăn người dùng rời khỏi phương tiện mà họ đang điều khiển, điều có thể khiến game bị phá vỡ.

Không gian tham chiếu này là lựa chọn tốt nhất cho các game như trình mô phỏng bay hoặc trình mô phỏng đua xe, trong đó chúng ta muốn đặt node :ref:`XROrigin3D <class_xrorigin3d>` tại vị trí đầu của người chơi.

Khi người dùng thực hiện tùy chọn căn giữa lại trên headset, với cách thực hiện khác nhau tùy XR runtime, XR runtime sẽ di chuyển :ref:`XRCamera3D <class_xrcamera3d>` đến node :ref:`XROrigin3D <class_xrorigin3d>`. :ref:`OpenXRInterface <class_openxrinterface>` cũng sẽ phát signal ``pose_recentered`` để game của bạn có thể phản ứng tương ứng.

.. Note::
  Mọi thành phần XR được theo dõi khác, chẳng hạn như controller hoặc anchor, cũng sẽ được điều chỉnh tương ứng.

.. Warning::
  Bạn **không** nên gọi ``center_on_hmd`` khi sử dụng không gian tham chiếu này.

Sân khấu
^^^^^^^^

Không gian tham chiếu sân khấu là không gian tham chiếu mặc định của chúng ta và đặt điểm gốc tại trung tâm không gian chơi. Đối với các XR runtime cho phép bạn vẽ ranh giới guardian, vị trí và hướng của ranh giới này thường do người dùng thiết lập. Các XR runtime khác có thể quyết định vị trí của điểm này bằng những cách khác. Tuy nhiên, đây là một điểm cố định trong thế giới thực.

Không gian tham chiếu này là lựa chọn tốt nhất cho các game quy mô phòng, trong đó người dùng dự kiến sẽ đi lại trong một không gian lớn hơn, hoặc cho các game cần chuyển đổi giữa các chế độ chơi. Xem :ref:`Room Scale <doc_xr_room_scale>` để biết thêm thông tin.

Khi người dùng thực hiện tùy chọn căn giữa lại trên headset, với cách thực hiện khác nhau tùy XR runtime, XR runtime sẽ không thay đổi điểm gốc. :ref:`OpenXRInterface <class_openxrinterface>` sẽ phát signal ``pose_recentered`` và game phải tự phản ứng phù hợp. Nếu không làm vậy, game của bạn sẽ không được chấp nhận trên nhiều store khác nhau.

Trong Godot, bạn có thể thực hiện việc này bằng cách gọi hàm ``center_on_hmd`` trên :ref:`XRServer <class_xrserver>`:

- Gọi ``XRServer.center_on_hmd(XRServer.RESET_BUT_KEEP_TILT, false)`` sẽ di chuyển node :ref:`XRCamera3D <class_xrcamera3d>` đến node :ref:`XROrigin3D <class_xrorigin3d>`, tương tự như không gian tham chiếu ``Local``.
- Gọi ``XRServer.center_on_hmd(XRServer.RESET_BUT_KEEP_TILT, true)`` sẽ di chuyển node :ref:`XRCamera3D <class_xrcamera3d>` lên phía trên node :ref:`XROrigin3D <class_xrorigin3d>` trong khi giữ nguyên chiều cao của người chơi, tương tự như không gian tham chiếu ``Local Floor``.

.. Note::
  Mọi thành phần XR được theo dõi khác, chẳng hạn như controller hoặc anchor, cũng sẽ được điều chỉnh tương ứng.

Sàn cục bộ
^^^^^^^^^^

Không gian tham chiếu sàn cục bộ tương tự không gian tham chiếu cục bộ vì nó đặt điểm gốc tại vị trí của người chơi. Tuy nhiên, trong chế độ này, chiều cao của người chơi được giữ nguyên. Tương tự không gian tham chiếu cục bộ, một số XR runtime sẽ duy trì vị trí này qua các phiên.

Do đó, không đảm bảo người chơi sẽ đứng trên điểm gốc; điều duy nhất được đảm bảo là họ đã đứng ở đó khi người dùng căn giữa lại lần cuối. Vì vậy, người chơi cũng có thể tự do đi ra xa.

Không gian tham chiếu này là lựa chọn tốt nhất cho các game trong đó người dùng dự kiến đứng tại cùng một vị trí, hoặc cho các game dạng AR trong đó các thành phần giao diện của người dùng gắn với node gốc và nhanh chóng được đặt tại vị trí của người chơi khi căn giữa lại.

Khi người dùng thực hiện tùy chọn căn giữa lại trên headset, với cách thực hiện khác nhau tùy XR runtime, XR runtime sẽ di chuyển :ref:`XRCamera3D <class_xrcamera3d>` lên phía trên node :ref:`XROrigin3D <class_xrorigin3d>` nhưng vẫn giữ nguyên chiều cao của người chơi. :ref:`OpenXRInterface <class_openxrinterface>` cũng sẽ phát signal ``pose_recentered`` để game của bạn có thể phản ứng tương ứng.

.. Warning::
  Hãy cẩn thận khi sử dụng chế độ này kết hợp với chuyển động ảo của người chơi. Việc người dùng căn giữa lại trong tình huống này có thể không dự đoán được, trừ khi bạn bù lại chuyển động khi xử lý signal căn giữa lại. Điều này thậm chí có thể khiến game bị phá vỡ, vì trong tình huống này, người chơi sẽ dịch chuyển tức thời đến bất kỳ vị trí trừu tượng nào mà điểm gốc được đặt vào trong quá trình di chuyển ảo, bao gồm cả khả năng người chơi dịch chuyển vào những vị trí lẽ ra không được phép vào. Trong tình huống này, tốt hơn nên sử dụng chế độ Sân khấu và chỉ giới hạn việc đặt lại hướng khi nhận được signal ``pose_recentered``.

.. Note::
  Mọi thành phần XR được theo dõi khác, chẳng hạn như controller hoặc anchor, cũng sẽ được điều chỉnh tương ứng.

.. Warning::
  Bạn **không** nên gọi ``center_on_hmd`` khi sử dụng không gian tham chiếu này.

Chế độ hòa trộn môi trường
~~~~~~~~~~~~~~~~~~~~~~~~~~

Chế độ hòa trộn môi trường xác định cách đầu ra đã kết xuất của chúng ta được hòa trộn vào "thế giới thực", nếu headset hỗ trợ tính năng này.

- ``Opaque`` nghĩa là đầu ra của chúng ta che khuất thế giới thực, tức là chúng ta đang ở chế độ VR.
- ``Additive`` nghĩa là đầu ra của chúng ta được thêm vào thế giới thực; đây là chế độ AR trong đó hệ thống quang học không cho phép chúng ta che khuất hoàn toàn thế giới thực (ví dụ: Hololens),
- ``Alpha`` nghĩa là đầu ra của chúng ta được hòa trộn với thế giới thực bằng đầu ra alpha (viewport phải bật nền trong suốt); đây là chế độ AR trong đó hệ thống quang học có thể che khuất hoàn toàn thế giới thực (Magic Leap, tất cả thiết bị passthrough, v.v.).

Nếu chọn một chế độ không được headset hỗ trợ, chế độ khả dụng đầu tiên sẽ được chọn.

.. Note::
  Một số thiết bị OpenXR có các hệ thống riêng để bật/tắt passthrough. Từ Godot 4.3 trở đi, việc chọn chế độ hòa trộn alpha cũng sẽ thực hiện các bước bổ sung này. Điều này yêu cầu đã cài đặt plugin mới nhất của nhà cung cấp.

.. _doc_openxr_settings_foveation_level:

Mức độ Foveation
~~~~~~~~~~~~~~~~

Thiết lập mức độ foveation được sử dụng khi kết xuất, nếu phần cứng đang dùng hỗ trợ tính năng này. Foveation là kỹ thuật trong đó nội dung càng được kết xuất xa tâm viewport thì độ phân giải kết xuất càng thấp. Hầu hết runtime XR chỉ hỗ trợ foveation cố định, nhưng một số runtime sẽ tính đến việc theo dõi mắt và sử dụng điểm hội tụ cho hiệu ứng này.

Mức càng cao thì hiệu năng đạt được càng tốt, nhưng chất lượng trong vùng nhìn ngoại vi của người dùng cũng bị giảm nhiều hơn.

.. Note::
  **Chỉ renderer Compatibility**, đối với renderer Mobile và Forward+, hãy đặt thuộc tính ``vrs_mode`` trên :ref:`Viewport <class_viewport>` thành ``VRS_XR``.

.. Warning::
  Tính năng này bị vô hiệu hóa nếu sử dụng các hiệu ứng hậu kỳ như glow, bloom hoặc DOF.

Foveation động
~~~~~~~~~~~~~~

Khi được bật, mức độ foveation sẽ tự động được điều chỉnh tùy theo tải GPU hiện tại. Mức này sẽ được điều chỉnh trong khoảng từ thấp đến mức foveation đã chọn ở thiết lập trước đó. Vì vậy, tốt nhất nên kết hợp thiết lập này với mức foveation được đặt là cao.

.. Note::
  **Chỉ renderer Compatibility**

Gửi bộ đệm độ sâu
~~~~~~~~~~~~~~~~~

Nếu được bật, một bộ đệm độ sâu do OpenXR cung cấp sẽ được sử dụng trong quá trình kết xuất và gửi cùng với hình ảnh đã kết xuất. Runtime XR có thể sử dụng bộ đệm này để cải thiện reprojection.

.. Note::
  Việc bật tính năng này sẽ vô hiệu hóa hỗ trợ stencil trong quá trình kết xuất. Không nhiều runtime XR sử dụng tính năng này; bạn nên tắt thiết lập này trừ khi nó mang lại lợi ích rõ rệt cho trường hợp sử dụng của mình.

Cảnh báo khi khởi động
~~~~~~~~~~~~~~~~~~~~~~

Nếu được bật, tùy chọn này sẽ hiển thị thông báo cảnh báo cho người dùng nếu OpenXR không khởi động được. Không phải lúc nào chúng ta cũng nhận được phản hồi từ hệ thống XR về lý do khởi động thất bại. Nếu có, chúng ta sẽ ghi lại thông tin này vào console. Các lý do thất bại thường gặp là:

- Không cài đặt runtime OpenXR nào trên hệ thống máy chủ.
- Runtime OpenXR WMR của Microsoft hiện đang hoạt động; runtime này chỉ hỗ trợ DirectX và sẽ thất bại nếu sử dụng OpenGL hoặc Vulkan.
- SteamVR được sử dụng nhưng không có headset nào được kết nối/bật.

Tắt tùy chọn này nếu game của bạn hỗ trợ chế độ dự phòng để có thể chơi ở chế độ desktop khi không kết nối headset VR, hoặc nếu bạn tự xử lý điều kiện thất bại bằng cách kiểm tra ``OpenXRInterface.is_initialized()``.

Extensions
----------

Phân mục này cho phép bạn bật nhiều OpenXR extension tùy chọn khác nhau. Lưu ý rằng các extension chỉ hoạt động nếu runtime OpenXR (SteamVR, Oculus, v.v.) mà dự án chạy cùng hỗ trợ chúng.

Debug Utils
~~~~~~~~~~~

Việc bật tùy chọn này sẽ ghi các thông báo debug từ runtime XR.

Loại thông báo debug
~~~~~~~~~~~~~~~~~~~~

Tùy chọn này cho phép bạn chọn những thông báo debug được ghi lại.

Tổng hợp khung hình
~~~~~~~~~~~~~~~~~~~

Khi được bật, nếu runtime XR hỗ trợ, các vector chuyển động và bộ đệm độ sâu có độ phân giải thấp hơn sẽ được kết xuất và cung cấp cho runtime XR. Khi đó, runtime XR có thể chèn các khung hình reprojection và bù đắp cho tốc độ khung hình thấp hơn.

Tính năng này hiện có các hạn chế sau:

- KHÔNG hoạt động trong renderer Forward+.
- Chỉ hoạt động với kết xuất stereo.

Theo dõi bàn tay
~~~~~~~~~~~~~~~~

Tùy chọn này bật hand tracking extension khi thiết bị đang sử dụng hỗ trợ. Theo mặc định, tùy chọn này được bật vì lý do tương thích với phiên bản cũ. Hand tracking extension cung cấp quyền truy cập vào dữ liệu cho phép bạn hiển thị bàn tay của người dùng với vị trí ngón tay chính xác. Tùy theo khả năng của nền tảng, dữ liệu hand tracking có thể được suy ra từ đầu vào của controller, lấy từ găng tay dữ liệu, lấy từ các cảm biến theo dõi bàn tay quang học hoặc từ bất kỳ nguồn phù hợp nào khác.

Nếu game của bạn chỉ hỗ trợ controller, bạn nên tắt tùy chọn này.

Xem trang về :ref:`theo dõi bàn tay <doc_openxr_hand_tracking>` để biết thêm chi tiết.

Nguồn dữ liệu theo dõi bàn tay không bị che khuất
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Việc bật tùy chọn này có nghĩa là hand tracking có thể sử dụng vị trí chính xác của các ngón tay, thường là vị trí mà camera của headset nhìn thấy.

Nguồn dữ liệu controller cho theo dõi bàn tay
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Việc bật tùy chọn này có nghĩa là hand tracking có thể sử dụng chính controller và suy ra vị trí các ngón tay dựa trên đầu vào của controller hoặc các cảm biến trên controller.

Hồ sơ tương tác bằng tay
~~~~~~~~~~~~~~~~~~~~~~~~

Việc bật extension này cho phép sử dụng hai tư thế hand tracking mới. Tư thế pinch là vị trí giữa ngón cái và ngón trỏ hướng về phía trước, còn tư thế poke nằm ở đầu ngón trỏ.

Tùy chọn này cũng cho phép thêm 3 đầu vào dựa trên cử chỉ. Pinch là khi người dùng chụm ngón cái và ngón trỏ vào nhau. Aim activation là khi ngón trỏ duỗi hoàn toàn. Và Grasps là khi người dùng nắm tay lại.

Khi hand interaction profile và controller interaction profile được cung cấp, runtime sẽ chuyển đổi giữa các profile tùy thuộc vào việc có sử dụng theo dõi quang học hay người dùng đang cầm controller.

Nếu chỉ cung cấp hand interaction profile, mọi runtime đều phải sử dụng tương tác bằng tay ngay cả khi người dùng đang cầm controller.

Thực thể không gian
~~~~~~~~~~~~~~~~~~~

Extension này và các thiết lập của nó được sử dụng để lấy và tương tác với thông tin về môi trường thế giới thực của người dùng. Bạn có thể tìm thông tin chi tiết hơn về cách hoạt động của extension này trên :ref:`trang về thực thể không gian <doc_openxr_spatial_entities>`.

Tương tác bằng ánh mắt
~~~~~~~~~~~~~~~~~~~~~~

Tính năng này bật extension tương tác bằng ánh mắt khi thiết bị được sử dụng hỗ trợ. Khi được bật, chúng ta sẽ nhận được phản hồi từ tính năng theo dõi mắt thông qua một pose nằm giữa hai mắt của người dùng và định hướng theo hướng người dùng đang nhìn. Đây sẽ là một hướng thống nhất.

Để sử dụng chức năng này, bạn cần chỉnh sửa action map và thêm một pose action mới, chẳng hạn ``eye_pose``. Bây giờ hãy thêm một interaction profile mới cho tương tác bằng ánh mắt và ánh xạ ``eye_pose``:

.. image:: img/openxr_eye_gaze_interaction.webp

Đừng quên lưu!

Tiếp theo, hãy thêm một node :ref:`XRController3D <class_xrcontroller3d>` mới vào origin node của bạn, đặt thuộc tính ``tracker`` thành ``/user/eyes_ext`` và đặt thuộc tính ``pose`` thành ``eye_pose``.

Bây giờ bạn có thể thêm các thành phần vào controller node này, chẳng hạn như raycast, và điều khiển chúng bằng mắt.

Mô hình Render
~~~~~~~~~~~~~~

Extension này được dùng để truy vấn XR runtime nhằm lấy các tài sản 3D của phần cứng đang được sử dụng, thường là một controller, cũng như vị trí của phần cứng đó. Bạn có thể tìm thấy hướng dẫn chi tiết về cách sử dụng :ref:`tại đây <doc_openxr_render_models>`.

Bộ điều chỉnh Binding
---------------------

Các tùy chọn này kiểm soát việc có thể sử dụng binding modifier hay không. Binding modifier được dùng để áp dụng các ngưỡng hoặc giá trị offset. Bạn có thể tìm thông tin về cách sử dụng và thiết lập chúng trên trang XR action map :ref:`tại đây <doc_binding_modifiers>`.

Ngưỡng Analog
~~~~~~~~~~~~~

Cho phép các binding modifier ngưỡng analog.

Binding Dpad
~~~~~~~~~~~~

Cho phép các binding modifier D-pad.
