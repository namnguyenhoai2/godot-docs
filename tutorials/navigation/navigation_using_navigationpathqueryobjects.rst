.. _doc_navigation_using_navigationpathqueryobjects:

Sử dụng NavigationPathQueryObjects
==================================

.. tip::

    Các tham số truy vấn đường đi cung cấp nhiều tùy chọn để cải thiện hiệu năng tìm đường hoặc giảm mức tiêu thụ bộ nhớ.

    Chúng phục vụ các nhu cầu tìm đường nâng cao mà các node cấp cao không phải lúc nào cũng đáp ứng được.

    Xem các phần tùy chọn tương ứng bên dưới.

``NavigationPathQueryObjects`` có thể được sử dụng cùng với ``NavigationServer.query_path()`` để nhận một đường đi điều hướng được **tùy chỉnh** ở mức cao, bao gồm **siêu dữ liệu** tùy chọn về đường đi.

Cách này yêu cầu thiết lập nhiều hơn so với việc nhận một NavigationPath thông thường, nhưng cho phép bạn điều chỉnh việc tìm đường và dữ liệu đường đi được cung cấp theo các nhu cầu khác nhau của dự án.

NavigationPathQueryObjects bao gồm một cặp object: một object ``NavigationPathQueryParameters`` chứa các tùy chọn tùy chỉnh cho truy vấn và một ``NavigationPathQueryResult`` nhận các cập nhật (thông thường) về đường đi kết quả cùng siêu dữ liệu từ truy vấn.

Các phiên bản 2D và 3D của ``NavigationPathQueryParameters`` có sẵn dưới dạng
:ref:`NavigationPathQueryParameters2D<class_NavigationPathQueryParameters2D>` và
:ref:`NavigationPathQueryParameters3D<class_NavigationPathQueryParameters3D>` tương ứng.

Các phiên bản 2D và 3D của ``NavigationPathQueryResult`` có sẵn dưới dạng
:ref:`NavigationPathQueryResult2D<class_NavigationPathQueryResult2D>` và
:ref:`NavigationPathQueryResult3D<class_NavigationPathQueryResult3D>` tương ứng.

Tạo một truy vấn đường đi cơ bản
--------------------------------

Cả tham số và kết quả đều được sử dụng theo cặp với hàm ``NavigationServer.query_path()``.

Để xem các tùy chọn tùy chỉnh hiện có, hãy xem phần bên dưới. Đồng thời xem phần mô tả cho từng tham số trong tài liệu tham chiếu lớp.

Mặc dù không bắt buộc nghiêm ngặt, hai object này được thiết kế để tạo một lần từ trước, lưu trong một biến persistent cho agent và tái sử dụng cho mỗi truy vấn đường đi tiếp theo với các tham số được cập nhật.

Việc tái sử dụng cùng các object sẽ cải thiện hiệu năng khi thường xuyên tạo object hoặc cấp phát bộ nhớ.

Script sau đây tạo các object và cung cấp một hàm ``query_path()`` để tạo các đường đi điều hướng mới. Đường đi kết quả giống hệt như khi sử dụng ``NavigationServer.map_get_path()``, đồng thời tái sử dụng các object.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    # Chuẩn bị các object truy vấn.
    var query_parameters := NavigationPathQueryParameters2D.new()
    var query_result := NavigationPathQueryResult2D.new()

    func query_path(p_start_position: Vector2, p_target_position: Vector2, p_navigation_layers: int = 1) -> PackedVector2Array:
        if not is_inside_tree():
            return PackedVector2Array()

        var map: RID = get_world_2d().get_navigation_map()

        if NavigationServer2D.map_get_iteration_id(map) == 0:
            # Bản đồ này chưa bao giờ được đồng bộ hóa và đang trống, không có lý do gì để truy vấn nó.
            return PackedVector2Array()

        query_parameters.map = map
        query_parameters.start_position = p_start_position
        query_parameters.target_position = p_target_position
        query_parameters.navigation_layers = p_navigation_layers

        NavigationServer2D.query_path(query_parameters, query_result)
        var path: PackedVector2Array = query_result.get_path()

        return path

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    # Chuẩn bị các object truy vấn.
    var query_parameters := NavigationPathQueryParameters3D.new()
    var query_result := NavigationPathQueryResult3D.new()

    func query_path(p_start_position: Vector3, p_target_position: Vector3, p_navigation_layers: int = 1) -> PackedVector3Array:
        if not is_inside_tree():
            return PackedVector3Array()

        var map: RID = get_world_3d().get_navigation_map()

        if NavigationServer3D.map_get_iteration_id(map) == 0:
            # Bản đồ này chưa bao giờ được đồng bộ hóa và đang trống, không có lý do gì để truy vấn nó.
            return PackedVector3Array()

        query_parameters.map = map
        query_parameters.start_position = p_start_position
        query_parameters.target_position = p_target_position
        query_parameters.navigation_layers = p_navigation_layers

        NavigationServer3D.query_path(query_parameters, query_result)
        var path: PackedVector3Array = query_result.get_path()

        return path

Các tùy chọn hậu xử lý đường đi
-------------------------------

.. figure:: img/path_postprocess_diff.webp
   :align: center
   :alt: Sự khác biệt trong hậu xử lý đường đi tùy thuộc vào bố cục đa giác của lưới điều hướng

   Sự khác biệt trong hậu xử lý đường đi tùy thuộc vào bố cục đa giác của lưới điều hướng.

Một tìm kiếm truy vấn đường đi di chuyển từ cạnh đa giác lưới điều hướng gần nhất đến cạnh gần nhất dọc theo các đa giác hiện có. Nếu có thể, nó sẽ xây dựng một hành lang đa giác hướng đến đa giác chứa vị trí đích.

Đường đi hành lang đa giác "tìm kiếm" thô này chưa được tối ưu nhiều và thường không phù hợp để agent di chuyển theo. Ví dụ, điểm cạnh gần nhất trên một đa giác lưới điều hướng có thể khiến agent phải đi vòng rất xa trên các đa giác lớn. Để cải thiện chất lượng đường đi do truy vấn trả về, có nhiều tùy chọn ``path_postprocessing``.

- Hậu xử lý ``PATH_POSTPROCESSING_CORRIDORFUNNEL`` rút ngắn đường đi bằng cách dẫn đường đi vòng qua các góc **bên trong hành lang đa giác hiện có**.

  Đây là hậu xử lý mặc định và thường cũng hữu ích nhất vì tạo ra kết quả đường đi ngắn nhất **bên trong hành lang đa giác hiện có**. Nếu hành lang đa giác vốn đã không tối ưu, chẳng hạn do bố cục lưới điều hướng không tối ưu, funnel có thể bám vào các góc đa giác không mong đợi và gây ra đường vòng.

- Hậu xử lý ``PATH_POSTPROCESSING_EDGECENTERED`` buộc tất cả các điểm trên đường đi được đặt ở giữa các cạnh đa giác đã đi qua **bên trong hành lang đa giác hiện có**.

  Hậu xử lý này thường chỉ hữu ích khi được sử dụng với các đa giác lưới điều hướng có dạng ô một cách nghiêm ngặt, tất cả có kích thước đồng đều, và việc đi theo đường dự kiến cũng bị giới hạn ở tâm các ô, chẳng hạn như trong game dạng lưới điển hình với chuyển động bị giới hạn ở tâm các ô lưới.

- Hậu xử lý ``PATH_POSTPROCESSING_NONE`` trả về đường đi đúng như cách hệ thống tìm đường đã di chuyển **bên trong hành lang đa giác hiện có**.

  Hậu xử lý này rất hữu ích cho việc debug vì nó cho thấy quá trình tìm kiếm đường đi đã di chuyển như thế nào từ điểm cạnh gần nhất đến điểm cạnh gần nhất và đã chọn những đa giác nào. Nhiều kết quả đường đi bất ngờ hoặc không tối ưu có thể được giải thích ngay bằng cách xem đường đi thô và hành lang đa giác này.

Đơn giản hóa đường đi
---------------------

.. tip::

    Đơn giản hóa đường đi có thể giúp điều khiển agent hoặc xử lý các agent bị rung trên những cạnh đa giác hẹp.

.. figure:: img/path_simplification_diff.webp
   :align: center
   :alt: Sự khác biệt giữa các điểm trên đường đi khi có và không có đơn giản hóa đường đi

   Sự khác biệt giữa các điểm trên đường đi khi có và không có đơn giản hóa đường đi.

Nếu ``simplify_path`` được bật, một biến thể của thuật toán đơn giản hóa đường đi Ramer-Douglas-Peucker sẽ được áp dụng cho đường đi. Thuật toán này làm thẳng đường đi bằng cách loại bỏ các điểm trên đường đi ít quan trọng hơn, tùy thuộc vào ``simplify_epsilon`` được sử dụng.

Đơn giản hóa đường đi giúp xử lý mọi loại vấn đề chuyển động của agent trong "cánh đồng trống", vốn phát sinh do có quá nhiều cạnh đa giác không cần thiết. Ví dụ, một mesh địa hình khi được bake thành lưới điều hướng có thể tạo ra số lượng đa giác quá lớn do có nhiều biến thiên độ cao nhỏ (nhưng hầu như không có ý nghĩa đối với việc tìm đường) trên địa hình.

Đơn giản hóa đường đi cũng giúp ích cho các agent cần "steering" vì chúng chỉ cần hướng đến các điểm góc quan trọng hơn trên đường đi.

.. Warning::

    Đơn giản hóa đường đi là một bước hậu xử lý cuối bổ sung cho đường đi. Nó làm tăng chi phí hiệu năng của truy vấn, vì vậy chỉ nên bật khi thực sự cần thiết.

.. note::

    Đơn giản hóa đường đi được cung cấp trên NavigationServer dưới dạng một hàm dùng chung. Bạn cũng có thể sử dụng hàm này bên ngoài các truy vấn điều hướng cho mọi loại mảng vị trí.

Siêu dữ liệu đường đi
---------------------

.. tip::

    Tắt các tùy chọn siêu dữ liệu đường đi không cần thiết có thể cải thiện hiệu năng và giảm mức tiêu thụ bộ nhớ.

Một truy vấn đường đi có thể trả về siêu dữ liệu bổ sung cho mỗi điểm trên đường đi.

- Cờ ``PATH_METADATA_INCLUDE_TYPES`` thu thập một mảng chứa thông tin primitive về các đối tượng sở hữu điểm, chẳng hạn như điểm đó thuộc về một region hay link.
- Cờ ``PATH_METADATA_INCLUDE_RIDS`` thu thập một mảng chứa :ref:`RIDs<class_RID>` của các đối tượng sở hữu điểm. Tùy thuộc vào primitive của đối tượng sở hữu điểm, các RID này có thể được sử dụng với nhiều hàm NavigationServer liên quan đến region hoặc link.
- Cờ ``PATH_METADATA_INCLUDE_OWNERS`` thu thập một mảng chứa ``ObjectIDs`` của các đối tượng sở hữu điểm. Các object ID này có thể được sử dụng với :ref:`@GlobalScope.instance_from_id() <class_@GlobalScope_method_instance_from_id>` để lấy node đứng sau instance đối tượng đó, chẳng hạn như node NavigationRegion hoặc NavigationLink.

Theo mặc định, toàn bộ path metadata đều được thu thập vì metadata này có thể rất cần thiết cho gameplay điều hướng nâng cao hơn.

- Ví dụ, để biết point nào trong path tương ứng với đối tượng hoặc node owner nào trong SceneTree.
- Ví dụ, để biết một point trong path là điểm bắt đầu hay điểm kết thúc của một navigation link cần được tiếp quản bằng script.

Đối với những cách sử dụng path cơ bản nhất, metadata không phải lúc nào cũng cần thiết. Có thể tắt chọn lọc việc thu thập path metadata để cải thiện hiệu năng và giảm mức tiêu thụ bộ nhớ.

Loại trừ hoặc bao gồm các region
--------------------------------

.. tip::

    Các bộ lọc region có thể cải thiện đáng kể hiệu năng trên những navigation map lớn được phân vùng thành các region.

Các tham số truy vấn cho phép giới hạn việc tìm path vào những navigation mesh cụ thể của region.

Nếu một navigation map lớn được phân vùng hợp lý thành các region nhỏ hơn, điều này có thể cải thiện đáng kể hiệu năng vì truy vấn có thể bỏ qua một số lượng lớn polygon ngay từ một trong những bước kiểm tra đầu tiên của quá trình tìm path.

- Theo mặc định, nếu để trống, tất cả region của navigation map được truy vấn đều được bao gồm.
- Nếu một region :ref:`RID<class_RID>` được thêm vào mảng ``excluded_regions``, navigation mesh của region đó sẽ bị bỏ qua trong quá trình tìm path.
- Nếu một region :ref:`RID<class_RID>` được thêm vào mảng ``included_regions``, navigation mesh của region đó sẽ được xem xét trong quá trình tìm path, đồng thời tất cả các region khác không được đưa vào cũng sẽ bị bỏ qua.
- Nếu một region đồng thời nằm trong danh sách bao gồm và loại trừ, region đó được xem là bị loại trừ.

Các bộ lọc region rất hiệu quả về mặt hiệu năng khi được kết hợp với các chunk navigation region được căn chỉnh theo một grid. Nhờ đó, bộ lọc có thể chỉ bao gồm chunk chứa vị trí bắt đầu và các chunk xung quanh thay vì toàn bộ navigation map.

Ngay cả khi target nằm ngoài các chunk xung quanh này (luôn có thể thêm các "vòng"), quá trình tìm path vẫn sẽ cố tạo path đến polygon gần target nhất. Điều này thường tạo ra các half-path đi theo hướng tổng quát phù hợp, với chỉ một phần nhỏ chi phí hiệu năng so với việc tìm trên toàn bộ map.

Phần bổ sung sau đây vào script truy vấn path cơ bản minh họa cách tích hợp ánh xạ region chunk với các bộ lọc region. Đây không phải là một ví dụ hoàn chỉnh có thể chạy.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    # ...

    var chunk_id_to_region_rid: Dictionary[Vector2i, RID] = {}

    func query_path(p_start_position: Vector2, p_target_position: Vector2, p_navigation_layers: int = 1) -> PackedVector2Array:

        # ...

        var regions_around_start_position: Array[RID] = []

        var chunk_rings: int = 1 # Tăng giá trị cho các region rất nhỏ hoặc để có chất lượng cao hơn.
        var start_chunk_id: Vector2i = floor(p_start_position / float(chunk_size))

        for y: int in range(start_chunk_id.y - chunk_rings, start_chunk_id.y + chunk_rings):
            for x: int in range(start_chunk_id.x - chunk_rings, start_chunk_id.x + chunk_rings):
                var chunk_id: Vector2i = Vector2i(x, y)
                if chunk_id_to_region_rid.has(chunk_id):
                    var region: RID = chunk_id_to_region_rid[chunk_id]
                    regions_around_start_position.push_back(region)

        query_parameters.included_regions = regions_around_start_position

        # ...

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    # ...

    var chunk_id_to_region_rid: Dictionary[Vector3i, RID] = {}

    func query_path(p_start_position: Vector3, p_target_position: Vector3, p_navigation_layers: int = 1) -> PackedVector3Array:

        # ...

        var regions_around_start_position: Array[RID] = []

        var chunk_rings: int = 1 # Tăng giá trị cho các region rất nhỏ hoặc để có chất lượng cao hơn.
        var start_chunk_id: Vector3i = floor(p_start_position / float(chunk_size))
        var y: int = 0 # Giả định navigation map dạng phẳng để đơn giản hóa.

        for z: int in range(start_chunk_id.z - chunk_rings, start_chunk_id.z + chunk_rings):
            for x: int in range(start_chunk_id.x - chunk_rings, start_chunk_id.x + chunk_rings):
                var chunk_id: Vector3i = Vector3i(x, y, z)
                if chunk_id_to_region_rid.has(chunk_id):
                    var region: RID = chunk_id_to_region_rid[chunk_id]
                    regions_around_start_position.push_back(region)

        query_parameters.included_regions = regions_around_start_position

        # ...

Cắt path và các giới hạn
------------------------

.. tip::

    Việc thiết lập các giới hạn hợp lý có thể cải thiện đáng kể hiệu năng trên những navigation map lớn, đặc biệt khi target không thể tiếp cận.

.. figure:: img/path_clip_and_limits.gif
   :align: center
   :alt: Cắt các path trả về theo khoảng cách cụ thể

   Cắt các path trả về theo khoảng cách cụ thể.

Các tham số truy vấn cho phép cắt các path trả về theo độ dài cụ thể. Các tùy chọn này cắt path trong bước hậu xử lý. Path vẫn được tìm như thể có độ dài đầy đủ, vì vậy chất lượng path vẫn giữ nguyên. Việc cắt độ dài path có thể hữu ích khi tạo các path phù hợp hơn với gameplay bị giới hạn, chẳng hạn như trong các game chiến thuật có phạm vi di chuyển hạn chế.

- Có thể sử dụng thuộc tính ``path_return_max_length`` để cắt path trả về theo một độ dài tối đa cụ thể.
- Có thể sử dụng thuộc tính ``path_return_max_radius`` để cắt path trả về nằm bên trong bán kính hình tròn (2D) hoặc hình cầu (3D) quanh vị trí bắt đầu.

Các tham số truy vấn cho phép giới hạn quá trình tìm path để chỉ tìm đến một khoảng cách cụ thể hoặc một số lượng polygon được tìm cụ thể. Các tùy chọn này phục vụ hiệu năng và tác động trực tiếp đến quá trình tìm path.

- Có thể sử dụng thuộc tính ``path_search_max_distance`` để dừng quá trình tìm path khi vượt quá khoảng cách này tính từ vị trí bắt đầu.
- Có thể sử dụng thuộc tính ``path_search_max_polygons`` để dừng quá trình tìm path khi vượt quá số polygon đã tìm này.

Khi quá trình tìm path bị dừng do đạt đến một giới hạn, path sẽ được đặt lại và tạo từ polygon tại vị trí bắt đầu đến polygon được tìm thấy cho đến thời điểm đó và gần vị trí target nhất.

.. warning::

    Mặc dù có lợi cho hiệu năng, nếu đặt các giá trị giới hạn tìm path quá thấp, chất lượng path có thể bị ảnh hưởng rất tiêu cực. Tùy thuộc vào cách bố trí polygon và mẫu tìm kiếm, các path trả về có thể đi hoàn toàn sai hướng thay vì hướng về target.
