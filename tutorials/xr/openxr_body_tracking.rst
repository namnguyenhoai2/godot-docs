.. _doc_openxr_body_tracking:

Theo dõi cơ thể OpenXR
======================

Tính năng theo dõi toàn bộ cơ thể trong OpenXR hiện mới chỉ bắt đầu khả dụng trên một số ít nền tảng. Khi khả năng hỗ trợ trở nên ổn định hơn, thông tin sẽ được bổ sung vào trang này.

Hỗ trợ HTC Tracker
------------------

Một tùy chọn đã khả dụng từ lâu là thực hiện theo dõi toàn bộ cơ thể bằng HTC tracker. Hiện tại, các thiết bị này được hỗ trợ thông qua SteamVR và trên các headset HTC Elite XR. Chúng được cung cấp thông qua hệ thống action map.

Các tracker này được xác định bằng vai trò (role) được gán cho chúng trong quá trình cấu hình. Chỉ cần thêm các node :ref:`XRController3D <class_xrcontroller3d>` làm node con của node :ref:`XROrigin3D <class_xrorigin3d>` và gán một trong các tracker sau:

.. list-table:: HTC trackers
  :widths: 100
  :header-rows: 0

  * - /user/vive_tracker_htcx/role/handheld_object
  * - /user/vive_tracker_htcx/role/left_foot
  * - /user/vive_tracker_htcx/role/right_foot
  * - /user/vive_tracker_htcx/role/left_shoulder
  * - /user/vive_tracker_htcx/role/right_shoulder
  * - /user/vive_tracker_htcx/role/left_elbow
  * - /user/vive_tracker_htcx/role/right_elbow
  * - /user/vive_tracker_htcx/role/left_knee
  * - /user/vive_tracker_htcx/role/right_knee
  * - /user/vive_tracker_htcx/role/waist
  * - /user/vive_tracker_htcx/role/chest
  * - /user/vive_tracker_htcx/role/camera
  * - /user/vive_tracker_htcx/role/keyboard

Giờ đây, bạn có thể sử dụng các tracker này làm mục tiêu cho các IK modifier trên avatar toàn thân.
