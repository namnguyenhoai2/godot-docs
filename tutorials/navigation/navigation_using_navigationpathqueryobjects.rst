.. _doc_navigation_using_navigationpathqueryobjects:

Sử dụng NavigationPathQueryObjects
==================================

.. tip::

    Các tham số truy vấn path cung cấp nhiều tùy chọn để cải thiện hiệu năng tìm path hoặc giảm mức tiêu thụ bộ nhớ.

    Chúng đáp ứng các nhu cầu tìm path nâng cao hơn mà các node cấp cao không phải lúc nào cũng hỗ trợ.

    Xem các phần tùy chọn tương ứng bên dưới.

``NavigationPathQueryObjects`` có thể được sử dụng cùng với ``NavigationServer.query_path()`` để nhận một path điều hướng được **tùy chỉnh** sâu, bao gồm **metadata** tùy chọn về path.

Cách này yêu cầu thiết lập nhiều hơn so với việc nhận một NavigationPath thông thường, nhưng cho phép bạn điều chỉnh việc tìm path và dữ liệu path được cung cấp theo các nhu cầu khác nhau của project.

NavigationPathQueryObjects bao gồm một cặp object: một object ``NavigationPathQueryParameters`` chứa các tùy chọn tùy chỉnh cho query và một ``NavigationPathQueryResult`` nhận các bản cập nhật (thông thường) về path kết quả và metadata từ query.

Các phiên bản 2D và 3D của ``NavigationPathQueryParameters`` có sẵn dưới dạng
:ref:`NavigationPathQueryParameters2D<class_NavigationPathQueryParameters2D>` and
:ref:`NavigationPathQueryParameters3D<class_NavigationPathQueryParameters3D>` respectively.

Các phiên bản 2D và 3D của ``NavigationPathQueryResult`` có sẵn dưới dạng
:ref:`NavigationPathQueryResult2D<class_NavigationPathQueryResult2D>` and
:ref:`NavigationPathQueryResult3D<class_NavigationPathQueryResult3D>` respectively.

Tạo một path query cơ bản
-------------------------

Cả hai tham số và kết quả đều được sử dụng theo cặp với function ``NavigationServer.query_path()``.

Xem thêm bên dưới để biết các tùy chọn tùy chỉnh hiện có. Đồng thời xem phần mô tả cho từng tham số trong tài liệu tham chiếu của class.

Mặc dù không bắt buộc nghiêm ngặt, cả hai object được dự định tạo trước một lần, lưu trong một biến persistent của agent và tái sử dụng cho mọi path query tiếp theo với các tham số được cập nhật.

Việc tái sử dụng cùng các object giúp cải thiện hiệu năng khi thường xuyên tạo object hoặc cấp phát bộ nhớ.

Script sau đây tạo các object và cung cấp một function ``query_path()`` để tạo các path điều hướng mới. Path kết quả giống hệt như khi sử dụng ``NavigationServer.map_get_path()``, đồng thời tái sử dụng các object.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    # Chuẩn bị các object query.
    var query_parameters := NavigationPathQueryParameters2D.new()
    var query_result := NavigationPathQueryResult2D.new()

    func query_path(p_start_position: Vector2, p_target_position: Vector2, p_navigation_layers: int = 1) -> PackedVector2Array:
        if not is_inside_tree():
            return PackedVector2Array()

        var map: RID = get_world_2d().get_navigation_map()

        if NavigationServer2D.map_get_iteration_id(map) == 0:
            # Map này chưa từng được đồng bộ và đang trống, không có lý do gì để query nó.
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

    # Chuẩn bị các object query.
    var query_parameters := NavigationPathQueryParameters3D.new()
    var query_result := NavigationPathQueryResult3D.new()

    func query_path(p_start_position: Vector3, p_target_position: Vector3, p_navigation_layers: int = 1) -> PackedVector3Array:
        if not is_inside_tree():
            return PackedVector3Array()

        var map: RID = get_world_3d().get_navigation_map()

        if NavigationServer3D.map_get_iteration_id(map) == 0:
            # Map này chưa từng được đồng bộ và đang trống, không có lý do gì để query nó.
            return PackedVector3Array()

        query_parameters.map = map
        query_parameters.start_position = p_start_position
        query_parameters.target_position = p_target_position
        query_parameters.navigation_layers = p_navigation_layers

        NavigationServer3D.query_path(query_parameters, query_result)
        var path: PackedVector3Array = query_result.get_path()

        return path

Các tùy chọn hậu xử lý path
---------------------------

.. figure:: img/path_postprocess_diff.webp
   :align: center
   :alt: Path post-processing differences depending on navigation mesh polygon layout

   Path post-processing differences depending on navigation mesh polygon layout.

Một path query sẽ tìm kiếm từ cạnh polygon navigation mesh gần nhất đến cạnh gần nhất dọc theo các polygon hiện có. Nếu có thể, nó sẽ xây dựng một polygon corridor hướng đến polygon chứa vị trí đích.

Path polygon corridor "search" thô này chưa được tối ưu nhiều và thường không phù hợp để agent di chuyển theo. Ví dụ, điểm cạnh gần nhất trên một polygon navigation mesh có thể khiến agent phải đi vòng rất xa trên các polygon lớn. Để cải thiện chất lượng path được query trả về, có nhiều tùy chọn ``path_postprocessing``.

- Hậu xử lý ``PATH_POSTPROCESSING_CORRIDORFUNNEL`` rút ngắn path bằng cách đưa path qua các góc **bên trong polygon corridor hiện có**.

  Đây là hậu xử lý mặc định và thường cũng hữu ích nhất vì cho kết quả path ngắn nhất **bên trong polygon corridor hiện có**. Nếu polygon corridor vốn đã không tối ưu, chẳng hạn do bố cục navigation mesh chưa tối ưu, funnel có thể bám vào các góc polygon không ngờ tới và gây đường vòng.

- Hậu xử lý ``PATH_POSTPROCESSING_EDGECENTERED`` buộc tất cả các điểm path được đặt ở giữa các cạnh polygon đã đi qua **bên trong polygon corridor hiện có**.

  Hậu xử lý này thường chỉ hữu ích khi được sử dụng với các polygon navigation mesh có dạng tile rõ ràng, tất cả có kích thước đồng đều và việc đi theo path dự kiến cũng bị giới hạn ở tâm các cell, chẳng hạn game dạng grid điển hình với chuyển động bị giới hạn ở tâm các cell của grid.

- Hậu xử lý ``PATH_POSTPROCESSING_NONE`` trả về path đúng như cách pathfinding đã di chuyển **bên trong polygon corridor hiện có**.

  Hậu xử lý này rất hữu ích khi debug vì nó cho thấy quá trình tìm path đã di chuyển từ điểm cạnh gần nhất này đến điểm cạnh gần nhất khác như thế nào và đã chọn những polygon nào. Nhiều kết quả path bất ngờ hoặc chưa tối ưu có thể được giải thích ngay bằng cách xem path thô và polygon corridor này.

Đơn giản hóa path
-----------------

.. tip::

    Đơn giản hóa path có thể hỗ trợ các agent điều hướng hoặc các agent bị rung giật trên những cạnh polygon mỏng.

.. figure:: img/path_simplification_diff.webp
   :align: center
   :alt: Path point difference with or without path simplification

   Path point difference with or without path simplification.

Nếu ``simplify_path`` được bật, một biến thể của thuật toán đơn giản hóa path Ramer-Douglas-Peucker sẽ được áp dụng cho path. Thuật toán này làm thẳng path bằng cách loại bỏ các điểm path ít quan trọng hơn, tùy thuộc vào ``simplify_epsilon`` được sử dụng.

Đơn giản hóa path giúp giải quyết nhiều vấn đề chuyển động của agent trong "open fields" do có quá nhiều cạnh polygon không cần thiết. Ví dụ, một terrain mesh khi được bake thành navigation mesh có thể tạo ra số lượng polygon quá lớn do tất cả các biến thiên độ cao nhỏ (nhưng hầu như không có ý nghĩa đối với việc tìm path) trên terrain.

Đơn giản hóa path cũng hỗ trợ các agent "steering" vì chúng chỉ cần hướng đến những điểm path ở góc quan trọng hơn.

.. Warning::

    Đơn giản hóa path là một bước hậu xử lý cuối bổ sung cho path. Nó làm tăng chi phí hiệu năng của query, vì vậy chỉ bật khi thực sự cần.

.. note::

    Đơn giản hóa path được cung cấp trên NavigationServer dưới dạng một function generic. Nó cũng có thể được sử dụng bên ngoài các navigation query cho mọi loại mảng vị trí.

Metadata của path
-----------------

.. tip::

    Tắt các tùy chọn metadata path không cần thiết có thể cải thiện hiệu năng và giảm mức tiêu thụ bộ nhớ.

Một path query có thể trả về metadata bổ sung cho mỗi điểm path.

- Flag ``PATH_METADATA_INCLUDE_TYPES`` thu thập một array chứa thông tin primitive về các owner của điểm, chẳng hạn điểm đó thuộc về region hay link. - Flag ``PATH_METADATA_INCLUDE_RIDS`` thu thập một array chứa :ref:`RIDs<class_RID>` của các owner điểm. Tùy thuộc vào primitive của owner điểm, các RID này có thể được sử dụng với nhiều function NavigationServer liên quan đến region hoặc link. - Flag ``PATH_METADATA_INCLUDE_OWNERS`` thu thập một array chứa ``ObjectIDs`` của các owner điểm. Các object ID này có thể được sử dụng với :ref:`@GlobalScope.instance_from_id()<class_@GlobalScope_method_instance_from_id>` để lấy node đứng sau instance object đó, chẳng hạn node NavigationRegion hoặc NavigationLink.

Theo mặc định, tất cả metadata của path đều được thu thập vì metadata này có thể rất cần thiết cho gameplay điều hướng nâng cao hơn.

- Ví dụ, để biết điểm path nào tương ứng với owner object hoặc node nào bên trong SceneTree. - Ví dụ, để biết một điểm path có phải là điểm bắt đầu hoặc kết thúc của một navigation link yêu cầu takeover bằng script hay không.

Đối với các trường hợp sử dụng path cơ bản nhất, metadata không phải lúc nào cũng cần thiết. Có thể tắt có chọn lọc việc thu thập metadata path để đạt thêm hiệu năng và giảm mức tiêu thụ bộ nhớ.

Loại trừ hoặc bao gồm các region
--------------------------------

.. tip::

    Region filter có thể hỗ trợ đáng kể về hiệu năng trên các navigation map lớn được phân vùng theo region.

Các tham số query cho phép giới hạn việc tìm path vào những navigation mesh của region cụ thể.

Nếu một navigation map lớn được phân vùng hợp lý thành các region nhỏ hơn, điều này có thể hỗ trợ đáng kể về hiệu năng vì query có thể bỏ qua một số lượng lớn polygon ngay trong một trong những bước kiểm tra sớm nhất của quá trình tìm path.

- Theo mặc định và khi để trống, tất cả region của navigation map được query đều được bao gồm. - Nếu một region :ref:`RID<class_RID>` được thêm vào array ``excluded_regions``, navigation mesh của region đó sẽ bị bỏ qua trong quá trình tìm path. - Nếu một region :ref:`RID<class_RID>` được thêm vào array ``included_regions``, navigation mesh của region đó sẽ được xét trong quá trình tìm path, đồng thời tất cả region khác không được đưa vào cũng sẽ bị bỏ qua. - Nếu một region vừa được bao gồm vừa bị loại trừ thì nó được xem là bị loại trừ.

Region filter rất hiệu quả về hiệu năng khi kết hợp với các chunk của navigation region được căn chỉnh theo grid. Theo cách này, filter có thể được thiết lập để chỉ bao gồm chunk chứa vị trí bắt đầu và các chunk xung quanh, thay vì toàn bộ navigation map.

Ngay cả khi target nằm bên ngoài các chunk xung quanh này (có thể luôn thêm các "ring" khác), pathfinding sẽ cố gắng tạo path đến polygon gần target nhất. Điều này thường tạo ra các nửa path đi theo hướng tổng quát phù hợp, với chỉ một phần chi phí hiệu năng so với việc tìm kiếm trên toàn bộ map.

Phần bổ sung sau đây cho script path query cơ bản minh họa cách tích hợp việc ánh xạ region chunk với các region filter. Đây không phải là một ví dụ hoàn chỉnh có thể chạy.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    # ...

    var chunk_id_to_region_rid: Dictionary[Vector2i, RID] = {}

    func query_path(p_start_position: Vector2, p_target_position: Vector2, p_navigation_layers: int = 1) -> PackedVector2Array:

        # ...

        var regions_around_start_position: Array[RID] = []

        var chunk_rings: int = 1 # Tăng giá trị này đối với các region rất nhỏ hoặc để có chất lượng cao hơn.
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

        var chunk_rings: int = 1 # Tăng giá trị này đối với các region rất nhỏ hoặc để có chất lượng cao hơn.
        var start_chunk_id: Vector3i = floor(p_start_position / float(chunk_size))
        var y: int = 0 # Giả định một navigation map phẳng để đơn giản hóa.

        for z: int in range(start_chunk_id.z - chunk_rings, start_chunk_id.z + chunk_rings):
            for x: int in range(start_chunk_id.x - chunk_rings, start_chunk_id.x + chunk_rings):
                var chunk_id: Vector3i = Vector3i(x, y, z)
                if chunk_id_to_region_rid.has(chunk_id):
                    var region: RID = chunk_id_to_region_rid[chunk_id]
                    regions_around_start_position.push_back(region)

        query_parameters.included_regions = regions_around_start_position

        # ...

Cắt và giới hạn path
--------------------

.. tip::

    Việc thiết lập giới hạn hợp lý có thể hỗ trợ đáng kể về hiệu năng trên các navigation map lớn, đặc biệt khi target không thể tiếp cận.

.. figure:: img/path_clip_and_limits.gif
   :align: center
   :alt: Clipping returned paths to specific distances

   Clipping returned paths to specific distances.

Các tham số query cho phép cắt path được trả về theo độ dài cụ thể. Những tùy chọn này cắt path như một phần của hậu xử lý. Path vẫn được tìm như thể có độ dài đầy đủ, vì vậy chất lượng sẽ không đổi. Cắt độ dài path có thể hữu ích khi tạo các path phù hợp hơn với gameplay bị giới hạn, chẳng hạn game chiến thuật có phạm vi di chuyển giới hạn.

- Property ``path_return_max_length`` có thể được sử dụng để cắt path được trả về theo một độ dài tối đa cụ thể. - Property ``path_return_max_radius`` có thể được sử dụng để cắt path được trả về bên trong bán kính hình tròn (2D) hoặc hình cầu (3D) quanh vị trí bắt đầu.

Các tham số truy vấn cho phép giới hạn việc tìm kiếm path để chỉ tìm kiếm trong một khoảng cách cụ thể hoặc một số lượng polygon cụ thể. Những tùy chọn này nhằm cải thiện hiệu suất và ảnh hưởng trực tiếp đến quá trình tìm kiếm path.

- Thuộc tính ``path_search_max_distance`` có thể được dùng để dừng quá trình tìm kiếm path khi vượt quá khoảng cách này tính từ vị trí bắt đầu. - Thuộc tính ``path_search_max_polygons`` có thể được dùng để dừng quá trình tìm kiếm path khi vượt quá số lượng polygon đã tìm kiếm này.

Khi quá trình tìm kiếm path bị dừng do đạt đến một giới hạn, path sẽ được đặt lại và tạo từ polygon tại vị trí bắt đầu đến polygon được tìm thấy cho đến thời điểm đó gần với vị trí đích nhất.

.. warning::

    Mặc dù có lợi cho hiệu suất, nếu các giá trị giới hạn tìm kiếm path được đặt quá thấp, chúng có thể ảnh hưởng rất tiêu cực đến chất lượng path. Tùy thuộc vào cách bố trí polygon và mẫu tìm kiếm, các path được trả về có thể đi theo những hướng hoàn toàn sai thay vì hướng đến đích.
