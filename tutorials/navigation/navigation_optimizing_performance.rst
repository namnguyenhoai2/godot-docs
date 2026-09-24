.. _doc_navigation_optimizing_performance:

Tối ưu hiệu năng điều hướng
===========================

.. image:: img/nav_optimization.webp

Các vấn đề hiệu năng liên quan đến điều hướng thường được phân loại thành các chủ đề sau:

- Các vấn đề hiệu năng khi phân tích cú pháp các node trong scene tree để bake navigation mesh.
- Các vấn đề hiệu năng khi bake navigation mesh thực tế.
- Các vấn đề hiệu năng với các truy vấn đường đi của NavigationAgent.
- Các vấn đề hiệu năng với quá trình tìm đường thực tế.
- Các vấn đề hiệu năng khi đồng bộ navigation map.

Các phần sau trình bày cách xác định và khắc phục, hoặc ít nhất giảm thiểu, tác động của các vấn đề này lên framerate.

Các vấn đề hiệu năng khi phân tích cú pháp các node trong scene tree
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Ưu tiên sử dụng các hình dạng đơn giản với số cạnh ít nhất có thể, chẳng hạn như không sử dụng các hình dạng bo tròn như hình tròn, hình cầu hoặc hình xuyến.

    Ưu tiên sử dụng các hình dạng collision vật lý thay cho các visual mesh phức tạp làm hình học nguồn, vì mesh cần được sao chép từ GPU và thường có mức độ chi tiết cao hơn nhiều so với mức cần thiết.

Nhìn chung, hãy tránh sử dụng hình học quá phức tạp làm hình học nguồn để bake navigation mesh. Ví dụ, không bao giờ sử dụng một visual mesh quá chi tiết, vì việc phân tích hình dạng của nó thành các mảng dữ liệu rồi voxelize để bake navigation mesh sẽ mất nhiều thời gian nhưng không đem lại cải thiện chất lượng thực tế nào cho navigation mesh cuối cùng. Thay vào đó, hãy sử dụng một phiên bản hình dạng có level of detail được đơn giản hóa đáng kể. Tốt hơn nữa, hãy sử dụng các hình dạng nguyên thủy như hình hộp và hình chữ nhật, chỉ cần bao phủ gần đúng cùng hình học nhưng vẫn tạo ra kết quả bake đủ tốt cho việc tìm đường.

Ưu tiên sử dụng các hình dạng collision vật lý đơn giản thay cho visual mesh làm hình học nguồn để bake navigation mesh. Theo mặc định, các hình dạng vật lý bị giới hạn đáng kể và được tối ưu hóa, nên dễ dàng và nhanh chóng phân tích cú pháp. Ngược lại, visual mesh có thể đơn giản hoặc phức tạp. Ngoài ra, để truy cập dữ liệu visual mesh, parser cần yêu cầu các mảng dữ liệu mesh từ RenderingServer, vì dữ liệu visual mesh được lưu trực tiếp trên GPU và không được cache trên CPU. Việc này yêu cầu khóa thread của RenderingServer và có thể ảnh hưởng nghiêm trọng đến framerate tại runtime trong khi quá trình rendering chạy đa luồng. Nếu rendering chạy đơn luồng, tác động lên framerate có thể còn nghiêm trọng hơn, và việc phân tích mesh có thể làm toàn bộ game bị đóng băng trong vài giây đối với các mesh phức tạp.

Các vấn đề hiệu năng khi bake navigation mesh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Khi chạy runtime, luôn ưu tiên sử dụng background thread để bake navigation mesh.

    Tăng NavigationMesh ``cell_size`` và ``cell_height`` để tạo ít voxel hơn.

    Thay đổi ``SamplePartitionType`` từ watershed sang monotone hoặc layers để tăng hiệu năng baking.

.. warning::
    KHÔNG BAO GIỜ scale hình học nguồn bằng node để tránh lỗi độ chính xác. Hầu hết việc scale chỉ áp dụng về mặt hiển thị, còn các hình dạng rất lớn ở scale cơ sở vẫn cần nhiều xử lý bổ sung ngay cả khi được thu nhỏ.

Việc bake navigation mesh tại runtime luôn nên được thực hiện trong background thread nếu có thể. Ngay cả navigation mesh có kích thước nhỏ cũng có thể mất nhiều thời gian bake hơn mức có thể thực hiện trong một frame, ít nhất là nếu muốn duy trì framerate ở mức có thể chấp nhận được.

Độ phức tạp của dữ liệu hình học nguồn được phân tích từ các node trong scene tree ảnh hưởng lớn đến hiệu năng baking, vì mọi thứ đều cần được ánh xạ vào grid / voxel. Để đạt hiệu năng baking tốt tại runtime, cell size và cell height của NavigationMesh nên được đặt cao nhất có thể mà không gây ra vấn đề về chất lượng navigation mesh đối với game. Nếu cell size hoặc cell height được đặt quá thấp, quá trình baking sẽ phải tạo ra số lượng voxel quá lớn để xử lý hình học nguồn. Nếu hình học nguồn trải rộng trên một game world rất lớn, quá trình baking thậm chí có thể hết bộ nhớ giữa chừng và làm game crash. Có thể giảm partition type tùy theo độ phức tạp của hình học nguồn trong game để cải thiện hiệu năng. Ví dụ, các game chủ yếu có bề mặt phẳng với hình học dạng khối có thể sử dụng chế độ monotone hoặc layers, vốn bake nhanh hơn nhiều (chẳng hạn vì không yêu cầu distance field pass).

Không bao giờ scale hình học nguồn bằng node. Việc này không chỉ có thể gây ra nhiều lỗi độ chính xác với các vertex và edge bị khớp sai, mà một số phép scale còn chỉ tồn tại dưới dạng hiển thị chứ không có trong dữ liệu thực tế được phân tích. Ví dụ, nếu một mesh được thu nhỏ về mặt hiển thị trong Editor, chẳng hạn scale được đặt thành 0.001 trên một MeshInstance, mesh đó vẫn yêu cầu một voxel grid khổng lồ và rất phức tạp để xử lý trong quá trình baking.

Các vấn đề hiệu năng với các truy vấn đường đi của NavigationAgent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Tránh reset và truy vấn đường đi không cần thiết trong mỗi frame trong các script NavigationAgent.

    Tránh cập nhật đường đi của tất cả NavigationAgent trong cùng một frame.

Các lỗi logic và thao tác gây lãng phí trong các script NavigationAgent tùy chỉnh là những nguyên nhân rất phổ biến gây ra vấn đề hiệu năng; chẳng hạn, hãy chú ý không reset đường đi trong từng frame. Theo mặc định, NavigationAgent được tối ưu để chỉ truy vấn đường đi mới khi vị trí mục tiêu thay đổi, navigation map thay đổi hoặc chúng bị buộc phải cách quá xa khoảng cách đường đi mong muốn.

Ví dụ, khi AI cần di chuyển đến player, không nên đặt vị trí mục tiêu thành vị trí của player trong từng frame, vì việc này sẽ truy vấn đường đi mới ở mỗi frame. Thay vào đó, hãy so sánh khoảng cách từ vị trí mục tiêu hiện tại đến vị trí của player, và chỉ đặt vị trí mục tiêu mới khi player đã di chuyển quá xa.

Không kiểm tra trước trong từng frame xem một vị trí mục tiêu có thể đi tới được hay không. Một kiểm tra có vẻ vô hại thực chất tương đương với một truy vấn đường đi tốn kém ở phía sau. Nếu dự định sẽ yêu cầu đường đi mới khi vị trí có thể đi tới được, hãy truy vấn đường đi trực tiếp. Bằng cách xem xét vị trí cuối cùng của đường đi được trả về và kiểm tra xem vị trí đó có nằm trong khoảng cách "reachable" với vị trí đang được kiểm tra hay không, ta có thể trả lời câu hỏi "vị trí này có thể đi tới được không?". Cách này tránh thực hiện tương đương hai truy vấn đường đi đầy đủ trong mỗi frame cho cùng một NavigationAgent.

Chia tổng số NavigationAgent thành các nhóm cập nhật hoặc sử dụng timer ngẫu nhiên để chúng không cùng yêu cầu đường đi mới trong một frame.

Các vấn đề hiệu năng với quá trình tìm đường thực tế
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Tối ưu các navigation mesh có quá nhiều chi tiết bằng cách giảm số lượng polygon và edge.

Chi phí của quá trình tìm đường thực tế tương quan trực tiếp với số lượng polygon và edge của navigation mesh, chứ không phải kích thước thực của game world. Nếu một game world khổng lồ sử dụng navigation mesh được tối ưu tốt với chỉ một vài polygon bao phủ các khu vực rộng lớn, hiệu năng sẽ ở mức chấp nhận được. Nếu game world bị chia nhỏ thành các navigation mesh rất nhỏ, mỗi mesh có các polygon nhỏ (như trong TileMaps), hiệu năng tìm đường sẽ giảm.

Một vấn đề phổ biến là hiệu suất đột ngột giảm khi không thể đi tới vị trí đích trong một truy vấn đường đi. Sự sụt giảm hiệu suất này là "bình thường" và là kết quả của một navigation mesh quá lớn, chưa được tối ưu đầy đủ, với quá nhiều polygon và edge cần tìm kiếm. Trong các lần tìm đường thông thường, khi có thể nhanh chóng đi tới vị trí đích, hệ thống tìm đường sẽ thoát sớm ngay khi tới được vị trí đó, nhờ vậy có thể che giấu việc thiếu tối ưu hóa này trong một thời gian. Nếu không thể đi tới vị trí đích, hệ thống tìm đường phải thực hiện một lượt tìm kiếm lâu hơn nhiều qua các polygon hiện có để xác nhận rằng hoàn toàn không thể đi tới vị trí đó.

Các vấn đề về hiệu suất khi đồng bộ hóa navigation map
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Gộp các polygon của navigation mesh theo vertex thay vì theo kết nối edge ở mọi nơi có thể.

Khi có thay đổi đối với navigation mesh hoặc navigation region chẳng hạn, NavigationServer cần đồng bộ hóa navigation map. Tùy thuộc vào độ phức tạp của navigation mesh, quá trình này có thể mất một khoảng thời gian đáng kể và ảnh hưởng đến framerate.

NavigationServer gộp các navigation mesh theo vertex hoặc theo kết nối edge. Việc gộp theo vertex xảy ra khi hai vertex của hai edge khác nhau nằm trong cùng các ô của lưới bản đồ. Đây là một thao tác khá nhanh và ít tốn tài nguyên. Việc gộp theo kết nối edge diễn ra ở lượt thứ hai đối với tất cả các edge vẫn chưa được gộp. Tất cả các edge tự do đều được kiểm tra khả năng kết nối với edge khác dựa trên cả khoảng cách và góc, nên thao tác này khá tốn tài nguyên.

Vì vậy, ngoài quy tắc chung là giữ số lượng edge của polygon ở mức thấp nhất có thể, cần gộp trước càng nhiều edge càng tốt theo vertex để chỉ còn lại một vài edge cho phép tính kết nối edge tốn kém hơn. Có thể sử dụng debug Navigation PerformanceMonitor để lấy thống kê về số lượng polygon và edge hiện có, cũng như số lượng polygon và edge chưa được gộp hoặc chưa được gộp theo vertex. Nếu tỷ lệ giữa các kết nối được gộp theo vertex và các kết nối edge chênh lệch quá nhiều (số kết nối theo vertex phải cao hơn đáng kể), thì các navigation mesh chưa được tạo hoặc đặt đúng cách, dẫn đến hiệu suất rất kém.
