.. _doc_navigation_optimizing_performance:

Tối ưu hóa hiệu năng điều hướng
===============================

.. image:: img/nav_optimization.webp

Các vấn đề hiệu năng phổ biến liên quan đến điều hướng có thể được phân loại thành các chủ đề sau:

- Các vấn đề hiệu năng khi phân tích cú pháp các node trong scene tree để bake navigation mesh. - Các vấn đề hiệu năng khi bake navigation mesh thực tế. - Các vấn đề hiệu năng với các truy vấn path của NavigationAgent. - Các vấn đề hiệu năng với quá trình tìm path thực tế. - Các vấn đề hiệu năng khi đồng bộ hóa navigation map.

Trong các phần sau, bạn có thể tìm thấy thông tin về cách xác định và khắc phục, hoặc ít nhất là giảm thiểu, ảnh hưởng của chúng đến framerate.

Các vấn đề hiệu năng khi phân tích cú pháp các node trong scene tree
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Ưu tiên sử dụng các shape đơn giản với ít cạnh nhất có thể, chẳng hạn như không sử dụng các shape bo tròn như hình tròn, hình cầu hoặc hình xuyến.

    Ưu tiên sử dụng các physics collision shape thay vì visual mesh phức tạp làm geometry nguồn, vì mesh cần được sao chép từ GPU và thường có nhiều chi tiết hơn mức cần thiết.

Nhìn chung, hãy tránh sử dụng geometry quá phức tạp làm geometry nguồn để bake navigation mesh. Ví dụ, không bao giờ sử dụng visual mesh có quá nhiều chi tiết, vì việc phân tích shape của nó thành các mảng dữ liệu và voxelize nó để bake navigation mesh sẽ mất nhiều thời gian mà không mang lại cải thiện chất lượng thực tế nào cho navigation mesh cuối cùng. Thay vào đó, hãy sử dụng phiên bản shape có level of detail được đơn giản hóa rất nhiều. Tốt hơn nữa, hãy sử dụng các shape nguyên thủy như box và rectangle, chỉ bao phủ tương đối cùng geometry nhưng vẫn tạo ra kết quả bake đủ tốt cho pathfinding.

Ưu tiên sử dụng các physics collision shape đơn giản thay vì visual mesh làm geometry nguồn để bake navigation mesh. Physics shape mặc định là các shape được giới hạn và tối ưu hóa rất nhiều, nên dễ và nhanh phân tích cú pháp. Ngược lại, visual mesh có thể từ đơn giản đến phức tạp. Ngoài ra, để truy cập dữ liệu visual mesh, parser cần yêu cầu các mảng dữ liệu mesh từ RenderingServer, vì dữ liệu visual mesh được lưu trực tiếp trên GPU và không được cache trên CPU. Việc này yêu cầu khóa thread của RenderingServer và có thể ảnh hưởng nghiêm trọng đến framerate trong runtime khi rendering chạy đa thread. Nếu rendering chạy đơn thread, ảnh hưởng đến framerate thậm chí có thể tệ hơn và việc phân tích mesh có thể làm toàn bộ game bị treo trong vài giây với các mesh phức tạp.

Các vấn đề hiệu năng khi bake navigation mesh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Trong runtime, luôn ưu tiên sử dụng background thread để bake navigation mesh.

    Tăng NavigationMesh ``cell_size`` và ``cell_height`` để tạo ít voxel hơn.

    Thay đổi ``SamplePartitionType`` từ watershed thành monotone hoặc layers để cải thiện hiệu năng baking.

.. warning::
    KHÔNG BAO GIỜ scale geometry nguồn bằng node để tránh lỗi precision. Phần lớn việc scale chỉ áp dụng về mặt hiển thị, và các shape có kích thước rất lớn ở scale gốc vẫn cần nhiều bước xử lý bổ sung ngay cả khi đã được thu nhỏ.

Việc bake navigation mesh trong runtime luôn nên được thực hiện trên background thread nếu có thể. Ngay cả navigation mesh có kích thước nhỏ cũng có thể mất nhiều thời gian bake hơn mức có thể hoàn tất trong một frame, ít nhất là nếu muốn giữ framerate ở mức có thể chấp nhận được.

Độ phức tạp của dữ liệu geometry nguồn được phân tích từ các node trong scene tree ảnh hưởng lớn đến hiệu năng baking, vì mọi thứ cần được ánh xạ vào một grid / voxel. Để cải thiện hiệu năng baking trong runtime, NavigationMesh cell size và cell height nên được đặt ở mức cao nhất có thể mà không gây ra vấn đề về chất lượng navigation mesh trong game. Nếu cell size hoặc cell height được đặt quá thấp, quá trình baking sẽ buộc phải tạo ra số lượng voxel quá lớn để xử lý geometry nguồn. Nếu geometry nguồn trải rộng trên một game world rất lớn, quá trình baking thậm chí có thể hết memory giữa chừng và làm game bị crash. Partition type cũng có thể được hạ xuống tùy theo độ phức tạp của geometry nguồn trong game để cải thiện hiệu năng. Ví dụ, các game chủ yếu có bề mặt phẳng với geometry dạng khối có thể sử dụng chế độ monotone hoặc layers, vốn bake nhanh hơn rất nhiều (chẳng hạn vì không yêu cầu distance field pass).

Không bao giờ scale geometry nguồn bằng node. Điều này không chỉ có thể gây ra nhiều lỗi precision với các vertex và edge không khớp, mà một số việc scale còn chỉ tồn tại dưới dạng hình ảnh chứ không có trong dữ liệu thực tế đã được phân tích. Ví dụ, nếu một mesh được thu nhỏ về mặt hiển thị trong Editor, chẳng hạn scale được đặt thành 0.001 trên một MeshInstance, mesh đó vẫn yêu cầu một voxel grid khổng lồ và rất phức tạp để xử lý khi baking.

Các vấn đề hiệu năng với các truy vấn path của NavigationAgent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Tránh reset path và thực hiện truy vấn không cần thiết trong mỗi frame ở các script NavigationAgent.

    Tránh cập nhật path của tất cả NavigationAgent trong cùng một frame.

Các lỗi logic và thao tác gây lãng phí trong những script NavigationAgent tùy chỉnh là các nguyên nhân rất phổ biến gây ra vấn đề hiệu năng. Ví dụ, hãy chú ý không reset path trong từng frame. Theo mặc định, NavigationAgent được tối ưu để chỉ truy vấn path mới khi vị trí mục tiêu thay đổi, navigation map thay đổi hoặc chúng bị buộc phải cách quá xa khoảng cách path mong muốn.

Ví dụ, khi AI cần di chuyển đến player, không nên đặt vị trí mục tiêu thành vị trí của player trong từng frame, vì điều này sẽ truy vấn path mới trong từng frame. Thay vào đó, hãy so sánh khoảng cách từ vị trí mục tiêu hiện tại đến vị trí của player, và chỉ đặt vị trí mục tiêu mới khi player đã di chuyển quá xa.

Không kiểm tra trước trong từng frame xem vị trí mục tiêu có thể đi tới được hay không. Một kiểm tra tưởng như vô hại thực chất tương đương với một truy vấn path tốn kém ở phía sau. Nếu dự định vẫn yêu cầu path mới khi vị trí có thể đi tới được, hãy truy vấn path trực tiếp. Bằng cách xem xét vị trí cuối cùng của path được trả về và kiểm tra xem vị trí đó có nằm trong khoảng cách "reachable" với vị trí đã kiểm tra hay không, bạn có thể trả lời câu hỏi "vị trí này có thể đi tới được không?". Cách này tránh thực hiện tương đương hai truy vấn path đầy đủ trong mỗi frame cho cùng một NavigationAgent.

Chia tổng số NavigationAgent thành các nhóm cập nhật hoặc sử dụng timer ngẫu nhiên để chúng không cùng yêu cầu path mới trong một frame.

Các vấn đề hiệu năng với quá trình tìm path thực tế
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Tối ưu navigation mesh có quá nhiều chi tiết bằng cách giảm số lượng polygon và edge.

Chi phí của quá trình tìm path thực tế tương quan trực tiếp với số lượng polygon và edge của navigation mesh, chứ không phải kích thước thực tế của game world. Nếu một game world khổng lồ sử dụng navigation mesh được tối ưu tốt với chỉ vài polygon bao phủ các khu vực rộng lớn, hiệu năng sẽ ở mức chấp nhận được. Nếu game world bị chia nhỏ thành các navigation mesh rất nhỏ, mỗi mesh lại có các polygon nhỏ (như trong TileMap), hiệu năng pathfinding sẽ giảm.

Một vấn đề phổ biến là hiệu năng đột ngột giảm khi không thể đi tới vị trí mục tiêu trong một truy vấn path. Sự sụt giảm hiệu năng này là "bình thường" và là kết quả của một navigation mesh quá lớn, chưa được tối ưu, với quá nhiều polygon và edge cần tìm kiếm. Trong các lần tìm path thông thường khi có thể nhanh chóng đi tới vị trí mục tiêu, pathfinding sẽ thoát sớm ngay khi đạt đến vị trí đó, tạm thời che giấu sự thiếu tối ưu này. Nếu không thể đi tới vị trí mục tiêu, pathfinding phải tìm kiếm lâu hơn nhiều qua các polygon hiện có để xác nhận rằng hoàn toàn không thể đi tới vị trí đó.

Các vấn đề hiệu năng khi đồng bộ hóa navigation map
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Gộp polygon của navigation mesh theo vertex thay vì theo kết nối edge ở bất cứ nơi nào có thể.

Khi có thay đổi, chẳng hạn với navigation mesh hoặc navigation region, NavigationServer cần đồng bộ hóa navigation map. Tùy thuộc vào độ phức tạp của navigation mesh, việc này có thể mất một khoảng thời gian đáng kể và ảnh hưởng đến framerate.

NavigationServer gộp navigation mesh theo vertex hoặc theo kết nối edge. Việc gộp theo vertex xảy ra khi hai vertex của hai edge khác nhau nằm trong cùng các map grid cell. Đây là một thao tác khá nhanh và ít tốn chi phí. Việc gộp theo kết nối edge xảy ra trong pass thứ hai đối với tất cả edge vẫn chưa được gộp. Tất cả free edge được kiểm tra các kết nối edge có thể có dựa trên cả khoảng cách và góc, nên khá tốn chi phí.

Vì vậy, ngoài quy tắc chung là giữ số lượng polygon edge ở mức thấp nhất có thể, nên gộp trước càng nhiều edge càng tốt theo vertex để chỉ còn lại một vài edge cho phép tính kết nối edge tốn kém hơn. Debug Navigation PerformanceMonitor có thể được sử dụng để lấy thống kê về số lượng polygon và edge hiện có, cũng như số lượng chưa được gộp hoặc chưa được gộp theo vertex. Nếu tỷ lệ giữa vertex được gộp và kết nối edge chênh lệch quá lớn (vertex nên cao hơn đáng kể), navigation mesh có thể đã được tạo hoặc đặt không hiệu quả.
