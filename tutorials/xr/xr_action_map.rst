.. _doc_xr_action_map:

Bản đồ hành động XR
===================

Godot có tính năng bản đồ hành động (action map) như một phần của hệ thống XR. Hiện tại, hệ thống này là một phần của module OpenXR. Có kế hoạch tích hợp WebXR vào đây trong tương lai gần, vì vậy trong tài liệu này chúng tôi gọi đây là hệ thống bản đồ hành động XR. Hệ thống này triển khai gần như chính xác hệ thống bản đồ hành động tích hợp sẵn của OpenXR.

Hệ thống bản đồ hành động XR cung cấp dữ liệu đầu vào, dữ liệu vị trí và đầu ra của các bộ điều khiển XR cho game/ứng dụng của bạn. Hệ thống thực hiện điều đó bằng cách cung cấp các action có tên, có thể được tùy chỉnh cho game/ứng dụng của bạn, rồi liên kết chúng với các đầu vào và đầu ra thực tế trên thiết bị XR của bạn.

Vì bản đồ hành động XR hiện là một phần của module OpenXR, bạn cần bật OpenXR trong cài đặt dự án để hiển thị nó:

.. image:: img/openxr_enabled.webp

Sau đó, bạn sẽ tìm thấy giao diện XR Action Map ở cuối màn hình:

.. image:: img/xr_action_map.webp

.. note::
  Hệ thống đầu vào tích hợp sẵn của Godot có nhiều điểm chung với hệ thống bản đồ hành động XR. Trên thực tế, ý tưởng ban đầu của chúng tôi là bổ sung chức năng vào hệ thống đầu vào hiện có và cung cấp dữ liệu cho hệ thống bản đồ hành động OpenXR. Có thể chúng tôi sẽ xem xét lại ý tưởng đó vào một thời điểm nào đó, nhưng hóa ra có quá nhiều vấn đề cần giải quyết. Có thể kể đến:

    * Hệ thống đầu vào của Godot chủ yếu xoay quanh các đầu vào dạng nút, còn XR bổ sung trigger, trục, pose và haptics (đầu ra) vào đó. Điều này sẽ khiến hệ thống đầu vào trở nên phức tạp hơn nhiều với các tính năng không hoạt động với những bộ điều khiển thông thường hoặc không phù hợp với cách tiếp cận hiện tại. Người ta cho rằng điều này sẽ gây nhầm lẫn cho phần lớn người dùng Godot.
    * Hệ thống đầu vào của Godot hoạt động với dữ liệu đầu vào thô được phân tích cú pháp và kích hoạt các action. Dữ liệu đầu vào này được cung cấp cho người dùng cuối. OpenXR hoàn toàn ẩn dữ liệu thô và thực hiện toàn bộ việc phân tích cú pháp thay chúng ta; chúng ta chỉ có quyền truy cập vào dữ liệu action đã được phân tích cú pháp. Sự không nhất quán này có thể dẫn đến lỗi khi một người dùng không ngờ tới cố sử dụng thiết bị XR như một thiết bị đầu vào thông thường.
    * Hệ thống đầu vào của Godot cho phép thay đổi các đầu vào được liên kết với action trong runtime, còn OpenXR thì không.
    * Hệ thống đầu vào của Godot dựa trên device id, vốn không có ý nghĩa trong OpenXR.

  Điều này có nghĩa là game/ứng dụng kết hợp các đầu vào truyền thống với bộ điều khiển XR sẽ có sự phân tách. Với hầu hết ứng dụng, chỉ một trong hai loại được sử dụng và đây không được xem là vấn đề. Cuối cùng, đây là một giới hạn của hệ thống.

Bản đồ hành động mặc định
-------------------------

Godot sẽ tự động tạo một bản đồ hành động mặc định nếu không tìm thấy tệp bản đồ hành động nào.

.. warning::
  Bản đồ mặc định này được thiết kế để giúp các nhà phát triển chuyển game/ứng dụng XR của họ từ Godot 3 sang Godot 4. Do đó, về cơ bản bản đồ này liên kết tất cả đầu vào đã biết trên mọi bộ điều khiển được hỗ trợ mặc định với các action tương ứng một-một. Đây không phải là ví dụ tốt về cách thiết lập bản đồ hành động. Tuy vậy, nó cho phép một nhà phát triển mới có điểm bắt đầu khi muốn làm quen với Godot XR. Bản đồ này giúp họ không phải thiết kế trước một bản đồ hành động phù hợp cho game/ứng dụng của mình.

Trong phần hướng dẫn này, chúng ta sẽ bắt đầu với một bản đồ hành động trống. Bạn có thể xóa mục "Godot action set" ở trên cùng bằng cách nhấn biểu tượng thùng rác. Thao tác này sẽ xóa tất cả action. Bạn cũng có thể muốn xóa các bộ điều khiển mà mình không muốn thiết lập; nội dung này sẽ được nói thêm sau.

Các action set
--------------

.. note::
  Trước khi đi sâu vào nội dung, bạn sẽ thấy thuật ngữ XR runtime được sử dụng xuyên suốt tài liệu này. XR runtime là phần mềm điều khiển và tương tác với kính AR hoặc VR. Sau đó, XR runtime cung cấp các chức năng này cho chúng ta thông qua một API như OpenXR. Cụ thể:

    * với Steam, đó là SteamVR,
    * với Meta trên máy tính để bàn, đó là Oculus Client (kể cả khi sử dụng Quest link),
    * với Meta trên Quest, đó là OpenXR client gốc của Quest,
    * trên Linux, đó có thể là Monado, v.v.

Bản đồ hành động cho phép chúng ta tổ chức các action thành các set. Mỗi set có thể được bật hoặc tắt riêng.

Ý tưởng ở đây là bạn có thể có các set khác nhau, cung cấp các liên kết trong những tình huống khác nhau. Bạn có thể có:

  * một set ``Character control`` khi bạn đang đi bộ,
  * một set ``Vehicle control`` khi bạn đang điều khiển phương tiện,
  * một set ``Menu`` khi một menu đang mở.

Khi đó, chỉ action set phù hợp với trạng thái hiện tại của game/ứng dụng mới được bật.

Điều này đặc biệt quan trọng nếu bạn muốn liên kết cùng một đầu vào trên bộ điều khiển với một action khác. Ví dụ:

  * trong set ``Character control`` của bạn, bạn có thể có một action ``Jump``,
  * trong set ``Vehicle control`` của bạn, bạn có thể có một action ``Accelerate``,
  * trong set ``Menu`` của bạn, bạn có thể có một action ``Select``.

Tất cả đều được liên kết với trigger trên bộ điều khiển của bạn.

OpenXR chỉ liên kết một đầu vào hoặc đầu ra với một action duy nhất. Nếu cùng một đầu vào hoặc đầu ra được liên kết với nhiều action, action nằm trong action set đang hoạt động và có mức ưu tiên cao nhất sẽ là action được cập nhật/sử dụng. Vì vậy, trong ví dụ trên, điều quan trọng là chỉ một action set được hoạt động.

Đối với game/ứng dụng XR đầu tiên, chúng tôi đặc biệt khuyến nghị bạn chỉ bắt đầu với một action set duy nhất và không thiết kế quá phức tạp.

Do đó, trong phần hướng dẫn này, chúng ta sẽ tạo một action set duy nhất có tên là ``my_first_action_set``. Chúng ta thực hiện việc này bằng cách nhấn nút :button:`Add action set`:

.. image:: img/xr_my_first_action_set.webp

Các cột trong bảng của chúng ta như sau:

.. list-table::
  :class: wrap-normal
  :width: 100%
  :widths: 7 23 70
  :header-rows: 1

  * - Col
    - Value
    - Description
  * - 1
    - my_first_action_set
    - Đây là tên nội bộ của action set. OpenXR không quy định các hạn chế cụ thể đối với tên này ngoài giới hạn về kích thước, tuy nhiên một số XR runtime sẽ không chấp nhận khoảng trắng hoặc ký tự đặc biệt.
  * - 2
    - My first action set
    - Đây là tên dễ đọc đối với con người của action set. Một số XR runtime sẽ hiển thị tên này cho người dùng cuối, chẳng hạn trong các hộp thoại cấu hình.
  * - 3
    - 0
    - Đây là mức ưu tiên của action set. Nếu nhiều action set đang hoạt động có các action được liên kết với cùng đầu vào hoặc đầu ra của bộ điều khiển, action set có giá trị ưu tiên cao nhất sẽ quyết định action được cập nhật.

Các action
----------

Trong bản đồ hành động XR, các action là những thực thể mà game/ứng dụng của bạn sẽ tương tác. Ví dụ, chúng ta có thể định nghĩa một action ``Shoot``, và đầu vào được liên kết với action đó sẽ kích hoạt signal ``button_pressed`` trên node :ref:`XRController3D <class_xrcontroller3d>` tương ứng trong scene của bạn, với ``Shoot`` là tham số ``name`` của signal.

Bạn cũng có thể truy vấn trạng thái hiện tại của một action.
Ví dụ, :ref:`XRController3D <class_xrcontroller3d>` có một phương thức ``is_button_pressed``.

Action có thể được sử dụng cho cả đầu vào và đầu ra, và mỗi action có một kiểu xác định hành vi của nó.

* Loại ``Bool`` được dùng cho đầu vào rời rạc như các nút.
* Loại ``Float`` được dùng cho đầu vào analog như các cần trigger.

Hai loại này đặc biệt vì chúng là những loại duy nhất có thể thay thế cho nhau. OpenXR sẽ xử lý việc chuyển đổi giữa các đầu vào và action ``Bool`` và ``Float``. Bạn có thể lấy giá trị của action loại ``Float`` bằng cách gọi phương thức ``get_float`` trên node :ref:`XRController3D <class_xrcontroller3d>` của mình. Node này phát tín hiệu ``input_float_changed`` khi giá trị thay đổi.

.. note::
  Khi đầu vào analog được truy vấn dưới dạng nút, một ngưỡng sẽ được áp dụng. Hiện tại, ngưỡng này chỉ được XR runtime quản lý. Trong tương lai, Godot có kế hoạch mở rộng để cung cấp một mức độ kiểm soát nhất định đối với các ngưỡng này.

Loại ``Vector2`` xác định đầu vào là đầu vào trục. Touchpad, cần analog và các đầu vào tương tự được cung cấp dưới dạng vector. Bạn có thể lấy giá trị của action loại ``Vector2`` bằng cách gọi phương thức ``get_vector2`` trên node :ref:`XRController3D <class_xrcontroller3d>` của mình. Node này phát tín hiệu ``input_vector2_changed`` khi giá trị thay đổi.

Loại ``Pose`` xác định một đầu vào được theo dõi trong không gian. OpenXR cung cấp nhiều đầu vào "pose": ``aim``, ``grip`` và ``palm``. Node :ref:`XRController3D <class_xrcontroller3d>` của bạn sẽ tự động được định vị dựa trên pose action được gán cho thuộc tính ``pose`` của node này. Chúng ta sẽ tìm hiểu thêm về pose sau.

.. note::
  OpenXR trong Godot cũng cung cấp một pose đặc biệt có tên ``Skeleton``. Đây là một phần của tính năng theo dõi bàn tay. Pose này được cung cấp thông qua action ``skeleton``, được hỗ trợ bên ngoài hệ thống action map. Vì vậy, pose này luôn hiện diện nếu tính năng theo dõi bàn tay được hỗ trợ. Bạn không cần bind action vào pose này để sử dụng nó.

Cuối cùng, loại đầu ra duy nhất là ``Haptic``, cho phép chúng ta đặt cường độ phản hồi haptic, chẳng hạn như độ rung của controller. Controller có thể có nhiều đầu ra haptic và OpenXR sắp hỗ trợ cả áo haptic.

Vậy hãy thêm một action cho aim pose của chúng ta. Ta thực hiện việc này bằng cách nhấp vào nút ``+`` cho action set của mình:

.. image:: img/xr_aim_pose.webp

Các cột trong bảng của chúng ta như sau:

.. list-table::
  :class: wrap-normal
  :width: 100%
  :widths: 7 23 70
  :header-rows: 1

  * - Cột
    - Giá trị
    - Mô tả
  * - 1
    - aim_pose
    - Đây là tên nội bộ của action. OpenXR không quy định hạn chế cụ thể nào đối với tên này ngoài kích thước, tuy nhiên một số XR runtime sẽ không chấp nhận khoảng trắng hoặc ký tự đặc biệt.
  * - 2
    - Tư thế ngắm
    - Đây là tên dễ đọc đối với người dùng của action. Một số XR runtime sẽ hiển thị tên này cho người dùng cuối, chẳng hạn như trong các hộp thoại cấu hình.
  * - 3
    - Pose
    - Loại của action này.

OpenXR định nghĩa một số pose đầu vào có thể bind, thường có sẵn trên controller. Không có quy tắc nào quy định những pose nào được hỗ trợ trên các controller khác nhau. Các pose hiện được OpenXR định nghĩa là:

  * Aim pose trên hầu hết controller được đặt hơi chếch về phía trước controller và hướng về phía trước. Đây là một pose rất phù hợp để dùng cho con trỏ laser hoặc căn nòng vũ khí.
  * Grip pose trên hầu hết controller được đặt tại vị trí của nút grip trên controller. Hướng của pose này khác nhau giữa các controller và có thể khác nhau đối với cùng một controller trên các XR runtime khác nhau.
  * Palm pose trên hầu hết controller được đặt ở chính giữa lòng bàn tay đang cầm controller. Đây là một pose mới, không có trên tất cả XR runtime.

.. note::
  Nếu sử dụng tính năng theo dõi bàn tay, hiện có những khác biệt lớn giữa các cách triển khai của những XR runtime khác nhau. Do đó, action map hiện chưa phù hợp cho việc theo dõi bàn tay. Công việc cải thiện vấn đề này đang được tiến hành, vì vậy hãy đón chờ các cập nhật tiếp theo.

Hãy hoàn thiện danh sách action cho một game/ứng dụng bắn súng rất đơn giản:

.. image:: img/xr_all_actions.webp

Các action chúng ta đã thêm là:

  * movement, cho phép người dùng di chuyển bên ngoài phạm vi theo dõi room scale thông thường.
  * grab, phát hiện khi người dùng muốn cầm một vật gì đó.
  * shoot, phát hiện khi người dùng muốn bắn vũ khí đang cầm.
  * haptic, cho phép chúng ta xuất phản hồi haptic.

Lưu ý rằng chúng ta không phân biệt tay trái và tay phải. Điều này được xác định ở giai đoạn tiếp theo. Chúng ta đã triển khai hệ thống action theo cách cho phép bind cùng một action vào cả hai tay. Node :ref:`XRController3D <class_xrcontroller3d>` tương ứng sẽ phát tín hiệu.

.. warning::
  Đối với cả grab và shoot, chúng ta đã sử dụng loại ``Bool``. Như đã đề cập trước đó, OpenXR tự động chuyển đổi từ các điều khiển analog, tuy nhiên hiện không phải tất cả XR runtime đều áp dụng các ngưỡng hợp lý.

  Để khắc phục tạm thời, chúng tôi khuyến nghị sử dụng loại ``Float`` khi tương tác với trigger và nút grip, đồng thời tự áp dụng ngưỡng của bạn.

  Đối với các nút như A/B/X/Y và những nút tương tự không có tùy chọn analog, loại ``Bool`` hoạt động tốt.

.. note::
  Bạn có thể bind cùng một action vào nhiều đầu vào trên cùng một controller trong cùng một profile. Trong trường hợp này, XR runtime sẽ cố gắng kết hợp các đầu vào.

  * Đối với các đầu vào ``Bool``, thao tác này sẽ thực hiện phép ``OR`` giữa các nút.
  * Đối với các đầu vào ``Float``, thao tác này sẽ lấy giá trị cao nhất trong các đầu vào đã bind.
  * Hành vi đối với các đầu vào ``Pose`` là không xác định, nhưng nhiều khả năng đầu vào được bind đầu tiên sẽ được sử dụng.

  Bạn không nên bind nhiều action thuộc cùng một action set vào cùng một đầu vào của controller. Nếu làm vậy, hoặc nếu các action được bind từ nhiều action set nhưng có độ ưu tiên chồng lấn, hành vi sẽ không xác định. XR runtime có thể đơn giản là không chấp nhận action map của bạn, hoặc có thể xử lý theo nguyên tắc action nào đến trước được phục vụ trước.

  Chúng tôi vẫn đang tìm hiểu các hạn chế liên quan đến việc bind nhiều action vào cùng một đầu ra, vì trường hợp này có ý nghĩa sử dụng. Đặc tả OpenXR dường như không cho phép điều này.

Giờ chúng ta đã xác định các action cơ bản, đã đến lúc kết nối chúng.

Profiles
--------

Trong OpenXR, các binding của controller được gọi là "Interaction Profiles". Chúng tôi rút gọn thành "Profiles" vì cách viết này chiếm ít không gian hơn.

Tên gọi chung này được chọn vì controller không bao phủ toàn bộ hệ thống. Hiện tại cũng có profile dành cho tracker, remote và bút được theo dõi. Ngoài ra còn có các quy định dành cho những thiết bị như máy chạy bộ, áo haptic và các thiết bị tương tự, dù chúng vẫn chưa thuộc đặc tả.

.. warning::
  Điều quan trọng cần biết là OpenXR kiểm tra nghiêm ngặt các thiết bị được hỗ trợ. Đặc tả cốt lõi xác định một số controller và thiết bị tương tự cùng với các đầu vào và đầu ra được hỗ trợ. Mọi XR runtime đều phải chấp nhận các interaction profile này, ngay cả khi chúng không áp dụng được.

  Các thiết bị mới được thêm thông qua extension và XR runtime phải chỉ rõ những extension nào chúng hỗ trợ. XR runtime không hỗ trợ thiết bị được thêm thông qua extension sẽ không chấp nhận các profile này. XR runtime không hỗ trợ các loại đầu vào hoặc đầu ra mới được thêm thường sẽ bị crash nếu được cung cấp các loại đó.

  Do đó, Godot lưu siêu dữ liệu của tất cả các thiết bị hiện có, đầu vào và đầu ra của chúng, cũng như extension nào bổ sung hỗ trợ cho chúng. Bạn có thể tạo interaction profile cho tất cả thiết bị mà mình muốn hỗ trợ. Godot sẽ lọc ra những thiết bị không được XR runtime mà người dùng đang sử dụng hỗ trợ.

  Điều này có nghĩa là để hỗ trợ các thiết bị mới, bạn có thể cần cập nhật lên phiên bản Godot mới hơn.

Tuy nhiên, cũng cần lưu ý rằng action map đã được thiết kế với điều này. Khi các thiết bị mới xuất hiện trên thị trường hoặc khi người dùng sử dụng những thiết bị mà bạn không có quyền truy cập, hệ thống action map sẽ dựa vào XR runtime. XR runtime có nhiệm vụ chọn interaction profile phù hợp nhất đã được chỉ định và điều chỉnh nó cho bộ điều khiển mà người dùng đang sử dụng.

Cách XR runtime thực hiện việc này phụ thuộc vào cách triển khai runtime, vì vậy có sự khác biệt rất lớn giữa các runtime. Một số runtime thậm chí có thể cho phép người dùng tự chỉnh sửa các binding.

Một cách tiếp cận phổ biến của runtime là trước tiên tìm interaction profile phù hợp. Nếu không tìm thấy, nó sẽ kiểm tra các profile phổ biến nhất, chẳng hạn như profile của "Touch controller", rồi thực hiện chuyển đổi. Nếu mọi cách khác đều thất bại, nó sẽ kiểm tra :ref:`"Simple controller" <doc_xr_action_map_simple>` chung.

.. note::
  Ở đây có một kết luận quan trọng: Khi một bộ điều khiển được tìm thấy và action map được áp dụng cho nó, XR runtime không bị giới hạn bởi các cấu hình chính xác mà bạn đã thiết lập trong trình chỉnh sửa action map của Godot. Mặc dù runtime thường sẽ chọn một ánh xạ phù hợp dựa trên một trong các binding bạn đã thiết lập trong action map, nó vẫn có thể điều chỉnh khác đi.

  Ví dụ, khi profile Touch controller được sử dụng, bất kỳ kịch bản nào sau đây cũng có thể xảy ra:

    * chúng ta có thể đang sử dụng bộ điều khiển Quest 1,
    * chúng ta có thể đang sử dụng bộ điều khiển Quest 2,
    * chúng ta có thể đang sử dụng bộ điều khiển Quest Pro nhưng không cung cấp profile Quest Pro, hoặc XR runtime đang được sử dụng không hỗ trợ bộ điều khiển Quest Pro,
    * đó có thể là một bộ điều khiển hoàn toàn khác, không được cung cấp profile, nhưng XR runtime đang sử dụng các binding của touch làm cơ sở.

  Vì vậy, hiện tại không có cách nào để biết chắc chắn người dùng thực sự đang sử dụng bộ điều khiển nào.

.. warning::
  Cuối cùng, và đây là điều khiến nhiều người nhầm lẫn, các binding không cố định. Việc XR runtime cho phép người dùng tùy chỉnh các binding là hoàn toàn hợp lệ, thậm chí còn được mong đợi.

  Hiện tại, không XR runtime nào cung cấp chức năng này, mặc dù SteamVR có một UI hiện có từ hệ thống action map của OpenVR vẫn có thể truy cập được. Tuy nhiên, chức năng này đang được tích cực phát triển.

Binding bộ điều khiển đầu tiên của chúng ta
-------------------------------------------

Hãy thiết lập binding bộ điều khiển đầu tiên, sử dụng Touch controller làm ví dụ.

Nhấn "Add profile", tìm Touch controller và thêm nó. Nếu nó không có trong danh sách thì có thể nó đã được thêm rồi.

.. image:: img/xr_add_touch_controller.webp

UI của chúng ta hiện hiển thị các bảng cho cả bộ điều khiển bên trái và bên phải. Các bảng chứa tất cả đầu vào và đầu ra có thể có của từng bộ điều khiển. Chúng ta có thể sử dụng ``+`` bên cạnh mỗi mục để binding mục đó với một action:

.. image:: img/xr_select_action.webp

Hãy hoàn tất cấu hình của chúng ta:

.. image:: img/xr_touch_completed.webp

Mỗi action được binding với đầu vào hoặc đầu ra đã cho trên cả hai bộ điều khiển để cho biết rằng chúng ta hỗ trợ action đó trên một trong hai bộ điều khiển. Ngoại lệ là action di chuyển, chỉ được binding với bộ điều khiển tay phải. Có thể chúng ta sẽ muốn sử dụng cần analog tay trái cho một mục đích khác, chẳng hạn như chức năng dịch chuyển.

Khi phát triển game/application, bạn phải tính đến khả năng người dùng thay đổi binding và binding chuyển động với cần analog tay trái.

Cũng lưu ý rằng các action boolean bắn và nắm của chúng ta được liên kết với các đầu vào thuộc loại ``Float``. Như đã đề cập trước đó, OpenXR sẽ thực hiện chuyển đổi giữa hai loại này, nhưng hãy đọc cảnh báo về chủ đề đó ở phần trước của tài liệu này.

.. note::
  Một số đầu vào dường như xuất hiện nhiều lần trong danh sách của chúng ta.

  Chẳng hạn, chúng ta có thể tìm thấy nút ``X`` hai lần, một lần dưới dạng ``X click`` và sau đó dưới dạng ``X touch``. Điều này là do Touch controller có cảm biến điện dung.

  * ``X touch`` sẽ là true nếu người dùng chỉ chạm vào nút X.
  * ``X click`` sẽ là true khi người dùng thực sự nhấn nút xuống.

  Tương tự, với cần analog, chúng ta có:

  * ``Thumbstick touch`` sẽ là true nếu người dùng chạm vào cần analog.
  * ``Thumbstick`` cung cấp giá trị cho hướng mà cần analog được đẩy tới.
  * ``Thumbstick click`` là true khi người dùng nhấn cần analog xuống.

  Điều quan trọng cần lưu ý là chỉ một số ít XR controller hỗ trợ cảm biến chạm hoặc có tính năng click trên cần analog. Hãy ghi nhớ điều này khi thiết kế game/application. Đảm bảo những tính năng này chỉ được dùng cho các tính năng tùy chọn của game/application.

.. _doc_xr_action_map_simple:

Bộ điều khiển đơn giản
----------------------

"Simple controller" là một bộ điều khiển chung mà OpenXR cung cấp để dự phòng. Hãy áp dụng ánh xạ của chúng ta:

.. image:: img/xr_simple_controller.webp

Như đã thấy rất rõ, bộ điều khiển đơn giản thường quá đơn giản và không đáp ứng được nhu cầu của bất kỳ game/application VR nào ngoài những game/application đơn giản nhất.

Đó là lý do nhiều XR runtime chỉ sử dụng nó như phương án cuối cùng và trước tiên sẽ cố gắng sử dụng các binding từ một trong những hệ thống phổ biến hơn làm phương án dự phòng.

.. note::
  Vì bộ điều khiển đơn giản có thể không đáp ứng đủ nhu cầu của game, bạn có thể muốn cung cấp binding cho mọi bộ điều khiển được OpenXR hỗ trợ. Action map mặc định dường như gợi ý rằng đây là một hướng xử lý hợp lệ. Như đã đề cập trước đó, action map mặc định được thiết kế để dễ dàng chuyển đổi từ Godot 3.

  OpenXR Working Group khuyến nghị chỉ thiết lập binding cho những bộ điều khiển mà nhà phát triển thực sự đã kiểm thử. Các XR runtime được thiết kế với điều này. Chúng có thể thực hiện việc binding lại cho một binding được cung cấp tốt hơn so với việc nhà phát triển đưa ra các phỏng đoán có cơ sở. Đặc biệt là vì nhà phát triển không thể kiểm thử xem việc này có mang lại trải nghiệm thoải mái cho người dùng cuối hay không.

  Đây cũng là lời khuyên của chúng tôi: giới hạn action map ở các interaction profile của những thiết bị mà bạn thực sự đã kiểm thử game của mình. Oculus Touch controller được nhiều runtime sử dụng rộng rãi làm bộ điều khiển dự phòng. Nếu bạn có thể kiểm thử game bằng Meta Rift hoặc Quest và thêm profile này, khả năng cao game của bạn sẽ hoạt động với các headset khác.

.. _doc_binding_modifiers:

Bộ sửa đổi binding
------------------

Một trong những mục tiêu chính của action map là loại bỏ nhu cầu để application biết phần cứng được sử dụng. Tuy nhiên, đôi khi phần cứng có những khác biệt vật lý đòi hỏi đầu vào phải được điều chỉnh theo cách khác với cách chúng được binding với các action. Nhu cầu này có thể bao gồm từ việc thiết lập các ngưỡng cho đến thay đổi những đầu vào có sẵn trên một bộ điều khiển.

Các binding modifier không được bật theo mặc định và cần được bật trong phần cài đặt dự án OpenXR. Ngoài ra, không có gì đảm bảo rằng mọi runtime đều hỗ trợ các modifier này. Bạn cần kiểm tra khả năng hỗ trợ của các runtime mà mình nhắm đến và quyết định xem có nên dựa vào các modifier hay triển khai một dạng cơ chế dự phòng nào đó.

Nếu nhắm đến nhiều runtime hỗ trợ cùng một bộ điều khiển, bạn có thể cần tạo action map riêng cho từng runtime. Bạn có thể kiểm soát action map mà Godot sử dụng bằng cách dùng các export template khác nhau cho từng runtime và dùng một :ref:`thẻ feature <doc_feature_tags>` tùy chỉnh để thiết lập action map.

Trong Godot, binding modifier được chia thành hai nhóm: các modifier hoạt động ở cấp interaction profile và các modifier hoạt động trên từng binding riêng lẻ.

Binding modifier trên một interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể truy cập các binding modifier được áp dụng cho toàn bộ interaction profile thông qua nút modifier ở bên phải trình chỉnh sửa interaction profile.

.. image:: img/openxr_ip_binding_modifier.webp

Bạn có thể thêm một modifier mới bằng cách nhấn nút :button:`Add binding modifier`.

.. warning::
  Vì Godot không biết bộ điều khiển và runtime nào hỗ trợ một modifier, nên không có hạn chế nào đối với việc thêm modifier. Các modifier không được hỗ trợ sẽ bị bỏ qua.

Dpad Binding modifier
^^^^^^^^^^^^^^^^^^^^^

Dpad binding modifier thêm các input mới vào một interaction profile cho mỗi input joystick và thumbpad trên bộ điều khiển này. Modifier này chuyển input thành một dpad với các input riêng biệt cho lên, xuống, trái và phải, được hiển thị dưới dạng các nút:

.. image:: img/openxr_thumbstick_dpad.webp

.. note::
  Các input liên quan đến extension được đánh dấu bằng dấu hoa thị.

Để sử dụng dpad binding modifier, bạn cần bật extension dpad binding modifier trong phần cài đặt dự án:

.. image:: img/openxr_project_settings_dpad_modifier.webp

Chỉ cần bật extension là đủ để chức năng này hoạt động với các cài đặt mặc định.

Việc thêm modifier là tùy chọn và cho phép bạn tinh chỉnh cách hoạt động của chức năng dpad. Bạn có thể thêm modifier nhiều lần để thiết lập các cài đặt khác nhau cho những input khác nhau.

.. image:: img/openxr_dpad_modifier.webp

Các cài đặt này được sử dụng như sau:

  * ``Action Set`` xác định action set mà các cài đặt này được áp dụng cho.
  * ``Input Path`` xác định input gốc được ánh xạ tới các input dpad mới.
  * ``Threshold`` chỉ định giá trị ngưỡng để kích hoạt một hành động dpad; ví dụ, giá trị ``0.6`` có nghĩa là nếu khoảng cách từ tâm vượt quá ``0.6`` thì hành động dpad được nhấn.
  * ``Threshold Released`` chỉ định giá trị ngưỡng để tắt một hành động dpad; ví dụ, giá trị ``0.4`` có nghĩa là nếu khoảng cách từ tâm nhỏ hơn ``0.4`` thì hành động dpad được nhả.
  * ``Center Region`` chỉ định khoảng cách từ tâm để kích hoạt hành động trung tâm; tính năng này chỉ được hỗ trợ cho trackpad.
  * ``Wedge Angle`` chỉ định góc của mỗi phần hình quạt. Giá trị ``90 degrees`` hoặc nhỏ hơn có nghĩa là lên, xuống, trái và phải đều có một phần riêng mà trong đó chúng ở trạng thái được nhấn. Giá trị lớn hơn ``90 degrees`` có nghĩa là các phần bị chồng lấn và nhiều hành động có thể ở trạng thái được nhấn.
  * ``Is Sticky``, khi được bật, có nghĩa là một hành động vẫn ở trạng thái được nhấn cho đến khi thumbstick hoặc trackpad di chuyển vào một phần hình quạt khác, ngay cả khi nó đã rời khỏi phần hình quạt tương ứng với hành động đó.
  * ``On Haptic`` cho phép chúng ta xác định một đầu ra haptic sẽ tự động được kích hoạt khi một hành động chuyển sang trạng thái được nhấn.
  * ``Off Haptic`` cho phép chúng ta xác định một đầu ra haptic sẽ tự động được kích hoạt khi một hành động được nhả.


Binding modifier trên từng binding riêng lẻ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể truy cập các binding modifier được áp dụng cho từng binding riêng lẻ thông qua nút binding modifier bên cạnh action được gắn với một input:

.. image:: img/openxr_action_binding_modifier.webp

Bạn có thể thêm một modifier mới bằng cách nhấn nút :button:`Add binding modifier`.

.. warning::
  Vì Godot không biết input nào trên từng runtime hỗ trợ một modifier, nên không có hạn chế nào đối với việc thêm modifier. Nếu extension của modifier không được hỗ trợ, các modifier sẽ bị lọc tại runtime. Các modifier được thêm vào sai input có thể gây ra lỗi runtime.

  Bạn nên kiểm tra action map trên phần cứng và runtime thực tế để xác minh thiết lập chính xác.

Analog threshold modifier
^^^^^^^^^^^^^^^^^^^^^^^^^

Analog threshold modifier cho phép bạn chỉ định các ngưỡng được sử dụng cho bất kỳ analog input nào, chẳng hạn như trigger, có boolean input. Modifier này kiểm soát thời điểm input ở trạng thái được nhấn.

Để sử dụng modifier này, bạn phải bật extension analog threshold trong phần cài đặt dự án:

.. image:: img/openxr_project_settings_analog_threshold_modifier.webp

Analog threshold modifier có các cài đặt sau:

.. image:: img/openxr_analog_threshold_modifier.webp

Các cài đặt này được xác định như sau:

  * ``On Threshold`` chỉ định giá trị ngưỡng để kích hoạt hành động; ví dụ, giá trị ``0.6`` có nghĩa là khi giá trị analog lớn hơn ``0.6`` thì hành động được đặt ở trạng thái được nhấn.
  * ``Off Threshold`` chỉ định giá trị ngưỡng để tắt hành động; ví dụ, giá trị ``0.4`` có nghĩa là khi giá trị analog nhỏ hơn ``0.4`` thì hành động được đặt ở trạng thái đã nhả.
  * ``On Haptic`` cho phép chúng ta xác định một đầu ra haptic sẽ tự động được kích hoạt khi input được nhấn.
  * ``Off Haptic`` cho phép chúng ta xác định một đầu ra haptic sẽ tự động được kích hoạt khi input được nhả.

Haptic trên modifier
~~~~~~~~~~~~~~~~~~~~

Modifier có thể hỗ trợ đầu ra haptic tự động, được kích hoạt khi đạt đến các ngưỡng.

.. note::
  Hiện tại, cả hai modifier hiện có đều hỗ trợ tính năng này, tuy nhiên không có quy định nào đảm bảo các modifier trong tương lai cũng có khả năng này. Chỉ một loại phản hồi haptic được hỗ trợ, nhưng trong tương lai có thể sẽ có thêm các tùy chọn khác.

Rung haptic
^^^^^^^^^^^

Rung haptic cho phép chúng ta chỉ định một xung haptic đơn giản:

.. image:: img/openxr_haptic_vibration.webp

Nó có các tùy chọn sau:

  * ``Duration`` là thời lượng của xung tính bằng nanosecond. ``-1`` cho phép runtime chọn một giá trị tối ưu cho xung ngắn, phù hợp với phần cứng hiện tại.
  * ``Frequency`` là tần số của xung tính bằng Hz. ``0`` cho phép runtime chọn một tần số tối ưu cho xung ngắn, phù hợp với phần cứng hiện tại.
  * ``Amplitude`` là biên độ của xung.
