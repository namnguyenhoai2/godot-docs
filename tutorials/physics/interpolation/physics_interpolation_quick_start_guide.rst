.. _doc_physics_interpolation_quick_start_guide:

Hướng dẫn bắt đầu nhanh
=======================

- Bật nội suy vật lý: :ref:`Project Settings > Physics > Common > Physics Interpolation<class_ProjectSettings_property_physics/common/physics_interpolation>` - Đảm bảo bạn di chuyển các đối tượng và chạy logic game trong ``_physics_process()`` thay vì ``_process()``. Điều này bao gồm cả việc di chuyển đối tượng trực tiếp *và gián tiếp* (ví dụ: di chuyển một đối tượng cha hoặc sử dụng một cơ chế khác để tự động di chuyển các node). - Hãy nhớ gọi :ref:`Node.reset_physics_interpolation<class_Node_method_reset_physics_interpolation>` trên các node *sau khi* bạn định vị hoặc dịch chuyển chúng lần đầu, để tránh hiện tượng "kéo vệt". - Tạm thời thử đặt :ref:`Project Settings > Physics > Common > Physics Ticks per Second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>` thành 10 để thấy sự khác biệt giữa việc có và không có nội suy.
