.. _doc_xr_action_map:

Bản đồ hành động XR
===================

Godot có tính năng bản đồ hành động (action map) như một phần của hệ thống XR. Hiện tại, hệ thống này là một phần của module OpenXR. Có kế hoạch tích hợp WebXR vào đây trong tương lai gần, vì vậy trong tài liệu này, chúng tôi gọi đây là hệ thống bản đồ hành động XR. Hệ thống này triển khai gần như chính xác hệ thống bản đồ hành động tích hợp sẵn của OpenXR.

Hệ thống bản đồ hành động XR cung cấp dữ liệu đầu vào, dữ liệu vị trí và đầu ra cho các controller XR trong game/ứng dụng của bạn. Hệ thống thực hiện điều này bằng cách cung cấp các hành động có tên, có thể được tùy chỉnh cho game/ứng dụng của bạn, rồi liên kết chúng với các đầu vào và đầu ra thực tế trên thiết bị XR của bạn.

Vì bản đồ hành động XR hiện là một phần của module OpenXR, bạn cần bật OpenXR trong cài đặt project để sử dụng nó:

.. image:: img/openxr_enabled.webp

Sau đó, bạn sẽ thấy giao diện XR Action Map ở cuối màn hình:

.. image:: img/xr_action_map.webp

.. note::
  Hệ thống input tích hợp sẵn của Godot có nhiều điểm chung với hệ thống bản đồ hành động XR. Thực tế, ý tưởng ban đầu của chúng tôi là bổ sung chức năng vào hệ thống input hiện có và cung cấp dữ liệu cho hệ thống bản đồ hành động OpenXR. Có thể chúng tôi sẽ xem xét lại ý tưởng đó vào một thời điểm nào đó, nhưng hóa ra có quá nhiều vấn đề cần giải quyết. Chẳng hạn:

    * Hệ thống input của Godot chủ yếu tập trung vào đầu vào dạng nút, còn XR bổ sung trigger, trục, pose và haptic (đầu ra). Điều này sẽ khiến hệ thống input trở nên phức tạp hơn nhiều với những tính năng không hoạt động với các controller thông thường hoặc không phù hợp với cách tiếp cận hiện tại. Người ta cho rằng điều này sẽ gây nhầm lẫn cho phần lớn người dùng Godot. * Hệ thống input của Godot hoạt động với dữ liệu input thô, được phân tích cú pháp và kích hoạt các hành động. Dữ liệu input này được cung cấp cho người dùng cuối. OpenXR hoàn toàn ẩn dữ liệu thô và thực hiện toàn bộ việc phân tích cú pháp, chúng ta chỉ truy cập được dữ liệu hành động đã được phân tích cú pháp. Sự không nhất quán này có thể dẫn đến lỗi khi một người dùng không ngờ rằng họ đang sử dụng thiết bị XR như một thiết bị input thông thường. * Hệ thống input của Godot cho phép thay đổi các input được liên kết với hành động trong runtime, còn OpenXR thì không. * Hệ thống input của Godot dựa trên device id, vốn không có ý nghĩa trong OpenXR.

  Điều này có nghĩa là game/ứng dụng kết hợp input truyền thống với controller XR sẽ có sự phân tách. Với hầu hết ứng dụng, chỉ một trong hai loại được sử dụng và đây không được xem là vấn đề. Suy cho cùng, đây là một giới hạn của hệ thống.

Bản đồ hành động mặc định
-------------------------

Godot sẽ tự động tạo một bản đồ hành động mặc định nếu không tìm thấy tệp bản đồ hành động nào.

.. warning::
  Bản đồ mặc định này được thiết kế để giúp các developer chuyển game/ứng dụng XR từ Godot 3 sang Godot 4. Vì vậy, về cơ bản bản đồ này liên kết tất cả input đã biết trên mọi controller được hỗ trợ theo mặc định với các hành động tương ứng một-một. Đây không phải là ví dụ tốt về cách thiết lập bản đồ hành động. Tuy nhiên, nó giúp một developer mới có điểm bắt đầu khi muốn làm quen với Godot XR. Bạn không cần thiết kế một bản đồ hành động phù hợp cho game/ứng dụng của mình trước.

Trong phần hướng dẫn này, chúng ta sẽ bắt đầu với một bản đồ hành động trống. Bạn có thể xóa mục "Godot action set" ở trên cùng bằng cách nhấn biểu tượng thùng rác. Thao tác này sẽ xóa tất cả hành động. Bạn cũng có thể muốn xóa các controller mà mình không muốn thiết lập; chúng ta sẽ nói thêm về việc này sau.

Các tập hợp hành động
---------------------

.. note::
  Trước khi đi sâu hơn, bạn sẽ thấy thuật ngữ XR runtime được sử dụng xuyên suốt tài liệu này. XR runtime là phần mềm điều khiển và tương tác với headset AR hoặc VR. Sau đó, XR runtime cung cấp các chức năng này cho chúng ta thông qua một API như OpenXR. Cụ thể:

    * với Steam, đó là SteamVR, * với Meta trên desktop, đó là Oculus Client (bao gồm cả khi sử dụng Quest link), * với Meta trên Quest, đó là OpenXR client gốc của Quest, * trên Linux, đó có thể là Monado, v.v.

Bản đồ hành động cho phép chúng ta tổ chức các hành động thành các tập hợp. Mỗi tập hợp có thể được bật hoặc tắt độc lập.

Ý tưởng ở đây là bạn có thể có các tập hợp khác nhau, cung cấp các liên kết trong những tình huống khác nhau. Bạn có thể có:

  * một tập hợp ``Character control`` khi bạn đang đi lại, * một tập hợp ``Vehicle control`` khi bạn đang điều khiển phương tiện, * một tập hợp ``Menu`` khi một menu đang mở.

Sau đó, chỉ cần bật tập hợp hành động phù hợp với trạng thái hiện tại của game/ứng dụng.

Điều này đặc biệt quan trọng nếu bạn muốn liên kết cùng một input trên controller với một hành động khác. Ví dụ:

  * trong tập hợp ``Character control``, bạn có thể có một hành động ``Jump``, * trong tập hợp ``Vehicle control``, bạn có thể có một hành động ``Accelerate``, * trong tập hợp ``Menu``, bạn có thể có một hành động ``Select``.

Tất cả đều được liên kết với trigger trên controller của bạn.

OpenXR chỉ liên kết một input hoặc output với một hành động duy nhất. Nếu cùng một input hoặc output được liên kết với nhiều hành động, hành động nằm trong tập hợp hành động đang hoạt động và có độ ưu tiên cao nhất sẽ là hành động được cập nhật/sử dụng. Vì vậy, trong ví dụ trên, điều quan trọng là chỉ có một tập hợp hành động đang hoạt động.

Đối với game/ứng dụng XR đầu tiên, chúng tôi thực sự khuyến nghị bạn bắt đầu chỉ với một tập hợp hành động duy nhất và không thiết kế quá phức tạp.

Vì vậy, trong phần hướng dẫn này, chúng ta sẽ tạo một tập hợp hành động duy nhất có tên ``my_first_action_set``. Chúng ta thực hiện việc này bằng cách nhấn nút :button:`Add action set`:

.. image:: img/xr_my_first_action_set.webp

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
    - my_first_action_set
    - Đây là tên nội bộ của tập hợp hành động.
      OpenXR không quy định giới hạn cụ thể nào đối với tên này ngoài kích thước, tuy nhiên
      một số XR runtime sẽ không chấp nhận khoảng trắng hoặc ký tự đặc biệt.
  * - 2
    - My first action set
    - Đây là tên dễ đọc đối với con người của tập hợp hành động.
      Một số XR runtime sẽ hiển thị tên này cho người dùng cuối, chẳng hạn trong
      các hộp thoại cấu hình.
  * - 3
    - 0
    - Đây là độ ưu tiên của tập hợp hành động.
      Nếu nhiều tập hợp hành động đang hoạt động có các hành động được liên kết với input hoặc
      output trên cùng một controller, tập hợp hành động có giá trị độ ưu tiên cao nhất sẽ xác định hành động
      được cập nhật.

Các hành động
-------------

Trong bản đồ hành động XR, các hành động là những thực thể mà game/ứng dụng của bạn sẽ tương tác. Ví dụ, chúng ta có thể định nghĩa một hành động ``Shoot``, và input được liên kết với hành động đó sẽ kích hoạt signal ``button_pressed`` trên node :ref:`XRController3D <class_xrcontroller3d>` tương ứng trong scene của bạn, với ``Shoot`` là tham số ``name`` của signal.

Bạn cũng có thể truy vấn trạng thái hiện tại của một hành động.
:ref:`XRController3D <class_xrcontroller3d>` for instance has
một phương thức ``is_button_pressed``.

Hành động có thể được sử dụng cho cả input và output, và mỗi hành động có một type xác định cách nó hoạt động.

* Type ``Bool`` được sử dụng cho input rời rạc như các nút. * Type ``Float`` được sử dụng cho input analog như trigger.

Hai type này đặc biệt vì chúng là những type duy nhất có thể thay thế cho nhau. OpenXR sẽ xử lý việc chuyển đổi giữa các input và hành động ``Bool`` và ``Float``. Bạn có thể lấy giá trị của hành động type ``Float`` bằng cách gọi phương thức ``get_float`` trên node :ref:`XRController3D <class_xrcontroller3d>` của mình. Phương thức này phát signal ``input_float_changed`` khi giá trị thay đổi.

.. note::
  Khi input analog được truy vấn dưới dạng nút, một ngưỡng sẽ được áp dụng. Hiện tại, ngưỡng này được XR runtime quản lý hoàn toàn. Có kế hoạch mở rộng Godot để cung cấp một mức độ kiểm soát nhất định đối với các ngưỡng này trong tương lai.

Type ``Vector2`` định nghĩa input là input dạng trục. Touchpad, thumbstick và các input tương tự được cung cấp dưới dạng vector. Bạn có thể lấy giá trị của hành động type ``Vector2`` bằng cách gọi phương thức ``get_vector2`` trên node :ref:`XRController3D <class_xrcontroller3d>` của mình. Phương thức này phát signal ``input_vector2_changed`` khi giá trị thay đổi.

Type ``Pose`` định nghĩa một input được theo dõi trong không gian. OpenXR cung cấp nhiều input "pose": ``aim``, ``grip`` và ``palm``. Node :ref:`XRController3D <class_xrcontroller3d>` của bạn sẽ tự động được định vị dựa trên action pose được gán cho property ``pose`` của node này. Chúng ta sẽ nói thêm về pose sau.

.. note::
  Triển khai OpenXR trong Godot cũng cung cấp một pose đặc biệt có tên ``Skeleton``. Đây là một phần của chức năng hand tracking. Pose này được cung cấp thông qua action ``skeleton``, được hỗ trợ bên ngoài hệ thống bản đồ hành động. Vì vậy, pose này luôn tồn tại nếu hand tracking được hỗ trợ. Bạn không cần liên kết hành động với pose này để sử dụng nó.

Cuối cùng, type output duy nhất là ``Haptic``, cho phép chúng ta thiết lập cường độ phản hồi haptic, chẳng hạn như độ rung của controller. Controller có thể có nhiều output haptic và OpenXR sẽ sớm hỗ trợ áo haptic.

Vậy hãy thêm một hành động cho aim pose của chúng ta. Chúng ta thực hiện việc này bằng cách nhấp vào nút ``+`` cho tập hợp hành động của mình:

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
    - Đây là tên nội bộ của hành động.
      OpenXR không quy định giới hạn cụ thể nào đối với tên này ngoài kích thước, tuy nhiên
      một số XR runtime sẽ không chấp nhận khoảng trắng hoặc ký tự đặc biệt.
  * - 2
    - Aim pose
    - Đây là tên thân thiện với người dùng cho hành động.
      Một số XR runtime sẽ hiển thị tên này cho người dùng cuối, chẳng hạn trong
      các hộp thoại cấu hình.
  * - 3
    - Pose
    - Kiểu của hành động này.

OpenXR định nghĩa một số pose đầu vào có thể bind, thường có sẵn cho các controller. Không có quy tắc nào về việc pose nào được hỗ trợ trên các controller khác nhau. Các pose mà OpenXR hiện định nghĩa là:

  * Aim pose trên hầu hết controller được đặt hơi phía trước controller và hướng về phía trước. Đây là pose rất phù hợp để dùng cho laser pointer hoặc căn nòng vũ khí. * Grip pose trên hầu hết controller được đặt tại vị trí nút grip trên controller. Hướng của pose này khác nhau giữa các controller và có thể khác nhau trên cùng một controller trong các XR runtime khác nhau. * Palm pose trên hầu hết controller được đặt ở giữa lòng bàn tay đang cầm controller. Đây là pose mới, không có trên tất cả XR runtime.

.. note::
  Nếu sử dụng hand tracking, hiện có sự khác biệt rất lớn giữa các cách triển khai của những XR runtime khác nhau. Vì vậy, action map hiện chưa phù hợp cho hand tracking. Công việc cải thiện vấn đề này đang được thực hiện, hãy đón chờ các cập nhật.

Hãy hoàn thiện danh sách action cho một game/ứng dụng bắn súng rất đơn giản:

.. image:: img/xr_all_actions.webp

Các action chúng ta đã thêm là:

  * movement, cho phép người dùng di chuyển bên ngoài phạm vi room scale tracking thông thường. * grab, phát hiện khi người dùng muốn cầm một vật gì đó. * shoot, phát hiện khi người dùng muốn bắn vũ khí đang cầm. * haptic, cho phép chúng ta xuất phản hồi xúc giác.

Bây giờ hãy lưu ý rằng chúng ta không phân biệt tay trái và tay phải. Đây là điều được xác định ở bước tiếp theo. Chúng ta đã triển khai hệ thống action theo cách cho phép bind cùng một action cho cả hai tay. Node :ref:`XRController3D <class_xrcontroller3d>` tương ứng sẽ phát signal.

.. warning::
  Đối với cả grab và shoot, chúng ta đã sử dụng kiểu ``Bool``. Như đã đề cập trước đó, OpenXR tự động chuyển đổi từ các điều khiển analogue, tuy nhiên hiện không phải XR Runtime nào cũng áp dụng các ngưỡng hợp lý.

  Để khắc phục tạm thời, chúng tôi khuyến nghị sử dụng kiểu ``Float`` khi tương tác với trigger và nút grip, sau đó tự áp dụng ngưỡng của bạn.

  Đối với các nút như A/B/X/Y và những nút tương tự không có tùy chọn analogue, kiểu ``Bool`` hoạt động tốt.

.. note::
  Bạn có thể bind cùng một action với nhiều input trên cùng một controller trong cùng một profile. Trong trường hợp này, XR runtime sẽ cố gắng kết hợp các input.

  * Đối với input ``Bool``, thao tác này sẽ thực hiện phép ``OR`` giữa các nút. * Đối với input ``Float``, thao tác này sẽ lấy giá trị cao nhất trong các input đã bind. * Hành vi đối với input ``Pose`` chưa được xác định, nhưng nhiều khả năng input được bind đầu tiên sẽ được sử dụng.

  Bạn không nên bind nhiều action thuộc cùng một action set với cùng một input của controller. Nếu làm vậy, hoặc nếu các action được bind từ nhiều action set nhưng có mức ưu tiên chồng lấn, hành vi sẽ không được xác định. XR runtime có thể đơn giản là không chấp nhận action map của bạn, hoặc có thể xử lý theo nguyên tắc ai đến trước được phục vụ trước.

  Chúng tôi vẫn đang tìm hiểu các hạn chế liên quan đến việc bind nhiều action với cùng một output, vì đây là một tình huống hợp lý. Đặc tả OpenXR có vẻ không cho phép điều này.

Giờ khi đã định nghĩa các action cơ bản, đã đến lúc kết nối chúng.

Profiles
--------

Trong OpenXR, các binding của controller được lưu trong cái gọi là "Interaction Profiles". Chúng tôi rút gọn thành "Profiles" vì cách này chiếm ít không gian hơn.

Tên gọi chung này được chọn vì controller không bao phủ toàn bộ hệ thống. Hiện tại cũng có profile cho tracker, remote và bút được tracking. Ngoài ra còn có quy định dành cho các thiết bị như máy chạy bộ, áo vest haptic và các thiết bị tương tự, dù chúng chưa thuộc đặc tả.

.. warning::
  Điều quan trọng cần biết là OpenXR kiểm tra nghiêm ngặt các thiết bị được hỗ trợ. Đặc tả cốt lõi xác định một số controller và thiết bị tương tự, cùng với các input và output được hỗ trợ. Mọi XR runtime đều phải chấp nhận các interaction profile này, ngay cả khi chúng không áp dụng được.

  Các thiết bị mới được thêm thông qua extension và XR runtime phải chỉ định những extension nào chúng hỗ trợ. XR runtime không hỗ trợ một thiết bị được thêm thông qua extension sẽ không chấp nhận các profile tương ứng. XR runtime không hỗ trợ các kiểu input hoặc output được thêm vào thường sẽ bị crash nếu được cung cấp chúng.

  Do đó, Godot lưu metadata về tất cả thiết bị hiện có, các input và output của chúng, cũng như extension bổ sung hỗ trợ cho chúng. Bạn có thể tạo interaction profile cho mọi thiết bị muốn hỗ trợ. Godot sẽ lọc bỏ những profile không được XR runtime mà người dùng đang sử dụng hỗ trợ.

  Điều này có nghĩa là để hỗ trợ các thiết bị mới, bạn có thể cần cập nhật lên phiên bản Godot mới hơn.

Tuy nhiên, cũng cần lưu ý rằng action map đã được thiết kế có tính đến điều này. Khi các thiết bị mới xuất hiện trên thị trường, hoặc khi người dùng sử dụng những thiết bị mà bạn không có, hệ thống action map sẽ dựa vào XR runtime. XR runtime có nhiệm vụ chọn interaction profile phù hợp nhất đã được chỉ định và điều chỉnh nó cho controller mà người dùng đang sử dụng.

Cách XR runtime thực hiện việc này phụ thuộc vào triển khai của runtime, vì vậy có sự khác biệt rất lớn giữa các runtime. Một số runtime thậm chí có thể cho phép người dùng tự chỉnh sửa binding.

Một cách tiếp cận phổ biến của runtime là trước tiên tìm interaction profile tương ứng. Nếu không tìm thấy, nó sẽ kiểm tra các profile phổ biến nhất, chẳng hạn profile của "Touch controller", rồi thực hiện chuyển đổi. Nếu mọi cách khác đều không thành công, nó sẽ kiểm tra :ref:`"Simple controller" <doc_xr_action_map_simple>` chung.

.. note::
  Có một kết luận quan trọng ở đây: Khi một controller được tìm thấy và action map được áp dụng cho nó, XR runtime không bị giới hạn ở chính xác các cấu hình bạn thiết lập trong trình chỉnh sửa action map của Godot. Mặc dù runtime thường sẽ chọn mapping phù hợp dựa trên một trong các binding bạn thiết lập trong action map, nó vẫn có thể khác với binding đó.

  Ví dụ, khi profile của Touch controller được sử dụng, bất kỳ kịch bản nào sau đây cũng có thể xảy ra:

    * chúng ta có thể đang sử dụng controller Quest 1, * chúng ta có thể đang sử dụng controller Quest 2, * chúng ta có thể đang sử dụng controller Quest Pro nhưng không cung cấp profile Quest Pro hoặc XR runtime đang sử dụng không hỗ trợ controller Quest Pro, * đó có thể là một controller hoàn toàn khác không có profile được cung cấp, nhưng XR runtime đang dùng các binding của Touch làm cơ sở.

  Do đó, hiện không có cách nào để biết chắc chắn người dùng thực sự đang sử dụng controller nào.

.. warning::
  Cuối cùng, đây là điều khiến nhiều người nhầm lẫn: các binding không cố định. XR runtime hoàn toàn được phép, và thậm chí được kỳ vọng, cho phép người dùng tùy chỉnh binding.

  Hiện tại chưa có XR runtime nào cung cấp chức năng này, mặc dù SteamVR có một UI hiện có từ hệ thống action map của OpenVR vẫn có thể truy cập. Tuy nhiên, vấn đề này đang được tích cực phát triển.

Binding controller đầu tiên của chúng ta
----------------------------------------

Hãy thiết lập binding controller đầu tiên, sử dụng Touch controller làm ví dụ.

Nhấn "Add profile", tìm Touch controller và thêm nó. Nếu nó không có trong danh sách thì có thể nó đã được thêm trước đó.

.. image:: img/xr_add_touch_controller.webp

UI của chúng ta hiện hiển thị các panel cho cả controller bên trái và bên phải. Các panel chứa tất cả input và output có thể có của mỗi controller. Chúng ta có thể sử dụng ``+`` bên cạnh mỗi mục để bind mục đó với một action:

.. image:: img/xr_select_action.webp

Hãy hoàn tất cấu hình của chúng ta:

.. image:: img/xr_touch_completed.webp

Mỗi action được bind với input hoặc output tương ứng trên cả hai controller để cho biết rằng chúng ta hỗ trợ action đó trên một trong hai controller. Ngoại lệ là action movement, chỉ được bind với controller tay phải. Có khả năng chúng ta sẽ muốn dùng thumbstick tay trái cho một mục đích khác, chẳng hạn chức năng dịch chuyển tức thời.

Khi phát triển game/ứng dụng, bạn phải tính đến khả năng người dùng thay đổi binding và bind movement với thumbstick tay trái.

Cũng lưu ý rằng các action boolean shoot và grab của chúng ta được liên kết với các input kiểu ``Float``. Như đã đề cập trước đó, OpenXR sẽ chuyển đổi giữa hai kiểu này, nhưng hãy đọc cảnh báo về chủ đề đó ở phần trước của tài liệu.

.. note::
  Một số input dường như xuất hiện nhiều lần trong danh sách của chúng ta.

  Ví dụ, chúng ta có thể tìm thấy nút ``X`` hai lần, một lần dưới dạng ``X click`` và sau đó dưới dạng ``X touch``. Điều này là do Touch controller có cảm biến điện dung.

  * ``X touch`` sẽ có giá trị true nếu người dùng chỉ chạm vào nút X. * ``X click`` sẽ có giá trị true khi người dùng thực sự nhấn nút.

  Tương tự, đối với thumbstick, chúng ta có:

  * ``Thumbstick touch`` sẽ có giá trị true nếu người dùng đang chạm vào thumbstick. * ``Thumbstick`` cung cấp giá trị cho hướng mà thumbstick được đẩy tới. * ``Thumbstick click`` có giá trị true khi người dùng nhấn thumbstick.

  Điều quan trọng cần lưu ý là chỉ một số ít controller XR hỗ trợ cảm biến cảm ứng hoặc có tính năng click trên cần analog. Hãy ghi nhớ điều này khi thiết kế game/ứng dụng của bạn. Hãy đảm bảo các tính năng này chỉ được dùng cho những chức năng tùy chọn của game/ứng dụng.

.. _doc_xr_action_map_simple:

Controller đơn giản
-------------------

"Simple controller" là một controller chung được OpenXR cung cấp làm phương án dự phòng. Chúng ta sẽ áp dụng mapping của mình:

.. image:: img/xr_simple_controller.webp

Như có thể thấy một cách khá rõ ràng, simple controller thường quá đơn giản và không đáp ứng được bất cứ điều gì ngoài những game/ứng dụng VR đơn giản nhất.

Đây là lý do nhiều XR runtime chỉ sử dụng nó như phương án cuối cùng và trước tiên sẽ cố gắng sử dụng các binding từ một trong những hệ thống phổ biến hơn làm phương án dự phòng.

.. note::
  Vì simple controller nhiều khả năng không đáp ứng đủ nhu cầu của game, bạn có thể muốn cung cấp binding cho mọi controller được OpenXR hỗ trợ. Action map mặc định dường như gợi ý đây là một hướng xử lý hợp lệ. Như đã đề cập trước đó, action map mặc định được thiết kế để dễ dàng migration từ Godot 3.

  OpenXR Working Group khuyến nghị chỉ thiết lập binding cho những controller mà developer đã thực sự kiểm thử. Các XR runtime được thiết kế với điều này. Chúng có thể thực hiện việc rebind một binding đã cung cấp tốt hơn khả năng phỏng đoán có cơ sở của developer. Đặc biệt là vì developer không thể kiểm thử xem việc này có dẫn đến trải nghiệm thoải mái cho người dùng cuối hay không.

  Đây cũng là lời khuyên của chúng tôi: hãy giới hạn action map ở các interaction profile của những thiết bị mà bạn đã thực sự kiểm thử game. Oculus Touch controller được nhiều runtime sử dụng rộng rãi làm controller dự phòng. Nếu bạn có thể kiểm thử game bằng Meta Rift hoặc Quest và thêm profile này, khả năng cao game của bạn sẽ hoạt động với các headset khác.

.. _doc_binding_modifiers:

Binding modifier
----------------

Một trong những mục tiêu chính của action map là loại bỏ nhu cầu để ứng dụng biết phần cứng đang được sử dụng. Tuy nhiên, đôi khi phần cứng có những khác biệt vật lý đòi hỏi input phải được điều chỉnh theo những cách khác với cách chúng được bind vào các action. Nhu cầu này có thể bao gồm việc thiết lập threshold cho đến thay đổi các input có sẵn trên một controller.

Binding modifier không được bật theo mặc định và cần được bật trong project settings của OpenXR. Ngoài ra, không có gì đảm bảo rằng mọi runtime đều hỗ trợ các modifier này. Bạn sẽ cần tham khảo khả năng hỗ trợ của những runtime mà mình nhắm đến và quyết định có dựa vào modifier hay triển khai một dạng fallback mechanism nào đó.

Nếu bạn nhắm đến nhiều runtime cùng hỗ trợ các controller giống nhau, bạn có thể cần tạo action map riêng cho từng runtime. Bạn có thể kiểm soát action map mà Godot sử dụng bằng cách dùng các export template khác nhau cho từng runtime và dùng một :ref:`feature tag <doc_feature_tags>` tùy chỉnh để thiết lập action map.

Trong Godot, binding modifier được chia thành hai nhóm: modifier hoạt động ở cấp interaction profile và modifier hoạt động trên từng binding riêng lẻ.

Binding modifier trên interaction profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể truy cập binding modifier được áp dụng cho toàn bộ interaction profile thông qua nút modifier ở bên phải trình chỉnh sửa interaction profile.

.. image:: img/openxr_ip_binding_modifier.webp

Bạn có thể thêm modifier mới bằng cách nhấn nút :button:`Add binding modifier`.

.. warning::
  Vì Godot không biết controller và runtime nào hỗ trợ một modifier, nên không có hạn chế nào đối với việc thêm modifier. Các modifier không được hỗ trợ sẽ bị bỏ qua.

Dpad Binding modifier
^^^^^^^^^^^^^^^^^^^^^

Dpad binding modifier thêm input mới vào interaction profile cho mỗi input joystick và thumbpad trên controller này. Nó chuyển input thành một dpad với các input lên, xuống, trái và phải riêng biệt, được hiển thị dưới dạng các button:

.. image:: img/openxr_thumbstick_dpad.webp

.. note::
  Các input liên quan đến extension được đánh dấu bằng dấu hoa thị.

Để sử dụng dpad binding modifier, bạn cần bật extension dpad binding modifier trong project settings:

.. image:: img/openxr_project_settings_dpad_modifier.webp

Chỉ cần bật extension là đủ để chức năng này hoạt động với các thiết lập mặc định.

Việc thêm modifier là tùy chọn và cho phép bạn tinh chỉnh cách hoạt động của chức năng dpad. Bạn có thể thêm modifier nhiều lần để thiết lập các tùy chọn khác nhau cho những input khác nhau.

.. image:: img/openxr_dpad_modifier.webp

Các thiết lập này được sử dụng như sau:

  * ``Action Set`` xác định action set mà các thiết lập này được áp dụng cho. * ``Input Path`` xác định input gốc được mapping vào các input dpad mới. * ``Threshold`` chỉ định giá trị threshold để kích hoạt một action dpad, ví dụ: giá trị ``0.6`` có nghĩa là nếu khoảng cách từ tâm vượt quá ``0.6`` thì action dpad được nhấn. * ``Threshold Released`` chỉ định giá trị threshold để tắt một action dpad, ví dụ: giá trị ``0.4`` có nghĩa là nếu khoảng cách từ tâm giảm xuống dưới ``0.4`` thì action dpad được nhả. * ``Center Region`` chỉ định khoảng cách từ tâm để kích hoạt action trung tâm; tùy chọn này chỉ được hỗ trợ cho trackpad. * ``Wedge Angle`` chỉ định góc của mỗi phần hình quạt. Giá trị ``90 degrees`` hoặc thấp hơn có nghĩa là lên, xuống, trái và phải đều có một phần riêng biệt, trong đó chúng ở trạng thái được nhấn. Giá trị lớn hơn ``90 degrees`` có nghĩa là các phần chồng lấn lên nhau và nhiều action có thể ở trạng thái được nhấn. * ``Is Sticky``, khi được bật, có nghĩa là một action vẫn ở trạng thái được nhấn cho đến khi thumbstick hoặc trackpad di chuyển vào một phần hình quạt khác, ngay cả khi nó đã rời khỏi phần hình quạt của action đó. * ``On Haptic`` cho phép chúng ta xác định một haptic output được tự động kích hoạt khi một action chuyển sang trạng thái được nhấn. * ``Off Haptic`` cho phép chúng ta xác định một haptic output được tự động kích hoạt khi một action được nhả.


Binding modifier trên từng binding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể truy cập binding modifier được áp dụng cho từng binding thông qua nút binding modifier bên cạnh action được gắn với một input:

.. image:: img/openxr_action_binding_modifier.webp

Bạn có thể thêm modifier mới bằng cách nhấn nút :button:`Add binding modifier`.

.. warning::
  Vì Godot không biết input nào trên mỗi runtime hỗ trợ một modifier, nên không có hạn chế nào đối với việc thêm modifier. Nếu extension của modifier không được hỗ trợ, các modifier sẽ bị lọc bỏ tại runtime. Modifier được thêm vào sai input có thể dẫn đến lỗi runtime.

  Bạn nên kiểm thử action map trên phần cứng và runtime thực tế để xác minh thiết lập chính xác.

Analog threshold modifier
^^^^^^^^^^^^^^^^^^^^^^^^^

Analog threshold modifier cho phép bạn chỉ định các threshold được sử dụng cho mọi analog input, chẳng hạn như trigger, có boolean input. Modifier này kiểm soát thời điểm input ở trạng thái được nhấn.

Để sử dụng modifier này, bạn phải bật extension analog threshold trong project settings:

.. image:: img/openxr_project_settings_analog_threshold_modifier.webp

Analog threshold modifier có các thiết lập sau:

.. image:: img/openxr_analog_threshold_modifier.webp

Các thiết lập này được xác định như sau:

  * ``On Threshold`` chỉ định giá trị threshold để kích hoạt action, ví dụ: giá trị ``0.6`` có nghĩa là khi giá trị analog vượt quá ``0.6`` thì action được chuyển sang trạng thái được nhấn. * ``Off Threshold`` chỉ định giá trị threshold để tắt action, ví dụ: giá trị ``0.4`` có nghĩa là khi giá trị analog giảm xuống dưới ``0.4`` thì action được chuyển sang trạng thái được nhả. * ``On Haptic`` cho phép chúng ta xác định một haptic output được tự động kích hoạt khi input được nhấn. * ``Off Haptic`` cho phép chúng ta xác định một haptic output được tự động kích hoạt khi input được nhả.

Haptics trên modifier
~~~~~~~~~~~~~~~~~~~~~

Modifier có thể hỗ trợ haptic output tự động, được kích hoạt khi đạt đến các threshold.

.. note::
  Hiện tại, cả hai modifier hiện có đều hỗ trợ tính năng này, tuy nhiên không có quy tắc nào đảm bảo các modifier trong tương lai cũng có khả năng này. Chỉ một loại haptic feedback được hỗ trợ, nhưng trong tương lai có thể sẽ có thêm các tùy chọn khác.

Haptic vibration
^^^^^^^^^^^^^^^^

Haptic vibration cho phép chúng ta chỉ định một haptic pulse đơn giản:

.. image:: img/openxr_haptic_vibration.webp

Nó có các tùy chọn sau:

  * ``Duration`` là thời lượng của pulse tính bằng nanosecond. ``-1`` cho phép runtime chọn một giá trị tối ưu cho pulse ngắn, phù hợp với phần cứng hiện tại. * ``Frequency`` là tần số của pulse tính bằng Hz. ``0`` cho phép runtime chọn tần số tối ưu cho pulse ngắn, phù hợp với phần cứng hiện tại. * ``Amplitude`` là biên độ của pulse.
