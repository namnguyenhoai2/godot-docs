.. _doc_xr_next_steps:

Tiếp theo nên làm gì
====================

Giờ đây, khi đã nắm được những kiến thức cơ bản, bạn có một số lựa chọn để tiếp tục hành trình phát triển game XR của mình:

* Bạn có thể xem phần :ref:`Chủ đề nâng cao <openxr-advanced-topics>`.
* Bạn có thể xem một số `bản demo XR tại đây <https://github.com/godotengine/godot-demo-projects/tree/master/xr>`_.
* Bạn có thể tìm các tutorial của bên thứ ba trên trang :ref:`Tutorials and resources <doc_community_tutorials>` của chúng tôi.

Godot OpenXR vendor plugin
--------------------------

Vendor plugin không chỉ dành cho việc :ref:`deploy lên Android <doc_deploying_to_android>`. Trong vendor plugin, chúng tôi triển khai nhiều OpenXR vendor extension, giúp mở khóa các tính năng độc đáo trên một số thiết bị hoặc các tính năng còn mới đến mức chưa có implementation được chuẩn hóa.

Cùng với OpenXR working group, chúng tôi duy trì một `ma trận hỗ trợ client <https://github.khronos.org/OpenXR-Inventory/extension_support.html#client_matrix>`_, trong đó liệt kê tất cả OpenXR extension mà Godot hỗ trợ và cho biết chúng có yêu cầu vendor plugin hay không.

XR Toolkit
----------

Hiện có nhiều XR toolkit triển khai các logic XR phức tạp hơn để bạn sử dụng ngay. Chúng tôi có một :Ref:`phần giới thiệu ngắn về Godot XR Tools <doc_introducing_xr_tools>` mà bạn có thể tham khảo; đây là một toolkit được phát triển bởi các core contributor của Godot.

Có thêm các toolkit dành cho Godot:

* `Godot XR handtracking toolkit <https://github.com/RevolNoom/godot_xr_handtracking>`_ (GDScript)
* `Godot XR Kit <https://github.com/patrykkalinowski/godot-xr-kit>`_ (GDScript)
* `Godot XR Tools <https://github.com/godotvr/godot-xr-tools>`_ (GDScript)
* `NXR <https://github.com/stumpynub/NXR>`_ (C#)

.. _`XR demos here`: https://github.com/godotengine/godot-demo-projects/tree/master/xr
.. _`client support matrix`: https://github.khronos.org/OpenXR-Inventory/extension_support.html#client_matrix
.. _`Godot XR handtracking toolkit`: https://github.com/RevolNoom/godot_xr_handtracking
.. _`Godot XR Kit`: https://github.com/patrykkalinowski/godot-xr-kit
.. _`Godot XR Tools`: https://github.com/godotvr/godot-xr-tools
.. _`NXR`: https://github.com/stumpynub/NXR
