:allow_comments: False

.. _doc_performance:

Hiệu năng
=========

Giới thiệu
----------

Godot tuân theo triết lý hiệu năng cân bằng. Trong lĩnh vực hiệu năng, luôn có những sự đánh đổi, bao gồm việc đánh đổi tốc độ để lấy khả năng sử dụng và tính linh hoạt. Một số ví dụ thực tế là:

-  Việc render hiệu quả một lượng lớn đối tượng là điều dễ dàng, nhưng khi cần render một scene lớn, quá trình này có thể trở nên kém hiệu quả. Để giải quyết vấn đề này, cần bổ sung việc tính toán khả năng hiển thị vào quá trình render. Điều này khiến việc render kém hiệu quả hơn, nhưng đồng thời cũng làm giảm số lượng đối tượng được render. Vì vậy, hiệu quả render tổng thể được cải thiện.

-  Việc cấu hình các thuộc tính của từng material cho mọi đối tượng cần được render cũng chậm. Để giải quyết vấn đề này, các đối tượng được sắp xếp theo material nhằm giảm chi phí xử lý. Đồng thời, việc sắp xếp cũng có chi phí riêng.

-  Trong physics 3D, tình huống tương tự cũng xảy ra. Các thuật toán tốt nhất để xử lý một lượng lớn đối tượng physics (chẳng hạn như SAP) lại chậm khi thêm/xóa đối tượng và thực hiện raycasting. Các thuật toán cho phép thêm và xóa nhanh hơn, cũng như raycasting nhanh hơn, sẽ không thể xử lý nhiều đối tượng đang hoạt động bằng.

Và còn rất nhiều ví dụ khác nữa! Game engine luôn hướng đến tính chất đa dụng. Các thuật toán cân bằng luôn được ưu tiên hơn những thuật toán có thể nhanh trong một số tình huống nhưng chậm trong các tình huống khác, hoặc những thuật toán nhanh nhưng khó sử dụng hơn.

Godot cũng không ngoại lệ. Mặc dù được thiết kế để có thể thay thế các backend bằng những thuật toán khác nhau, các backend mặc định ưu tiên sự cân bằng và tính linh hoạt hơn hiệu năng.

Sau khi đã hiểu rõ điều này, mục tiêu của phần hướng dẫn này là giải thích cách đạt được hiệu năng tối đa từ Godot. Mặc dù có thể đọc các bài hướng dẫn theo bất kỳ thứ tự nào, bạn nên bắt đầu từ :ref:`doc_general_optimization`.

Thông dụng
----------

.. toctree::
   :maxdepth: 1
   :name: toc-learn-features-general-optimization

   general_optimization
   using_servers

CPU
---

.. toctree::
   :maxdepth: 1
   :name: toc-learn-features-cpu-optimization

   cpu_optimization

GPU
---

.. toctree::
   :maxdepth: 1
   :name: toc-learn-features-gpu-optimization

   gpu_optimization
   using_multimesh
   pipeline_compilations

3D --

.. toctree::
   :maxdepth: 1
   :name: toc-learn-features-3d-optimization

   optimizing_3d_performance
   vertex_animation/index


Luồng
-----

.. toctree::
   :maxdepth: 1
   :name: toc-learn-features-threads

   using_multiple_threads
   thread_safe_apis
