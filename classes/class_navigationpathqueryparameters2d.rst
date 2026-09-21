:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationPathQueryParameters2D.xml.

.. _class_NavigationPathQueryParameters2D:

NavigationPathQueryParameters2D
===============================

**Thử nghiệm:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho các truy vấn đường dẫn điều hướng 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi nhiều thuộc tính khác nhau của đối tượng này, chẳng hạn như vị trí bắt đầu và vị trí đích, bạn có thể cấu hình các truy vấn đường dẫn cho :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationPathQueryObjects <../tutorials/navigation/navigation_using_navigationpathqueryobjects>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]                                             | :ref:`excluded_regions<class_NavigationPathQueryParameters2D_property_excluded_regions>`                 | ``[]``            |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]                                             | :ref:`included_regions<class_NavigationPathQueryParameters2D_property_included_regions>`                 | ``[]``            |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`RID<class_RID>`                                                                          | :ref:`map<class_NavigationPathQueryParameters2D_property_map>`                                           | ``RID()``         |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\] | :ref:`metadata_flags<class_NavigationPathQueryParameters2D_property_metadata_flags>`                     | ``7``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`navigation_layers<class_NavigationPathQueryParameters2D_property_navigation_layers>`               | ``1``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>`             | :ref:`path_postprocessing<class_NavigationPathQueryParameters2D_property_path_postprocessing>`           | ``0``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_length<class_NavigationPathQueryParameters2D_property_path_return_max_length>`     | ``0.0``           |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_radius<class_NavigationPathQueryParameters2D_property_path_return_max_radius>`     | ``0.0``           |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_search_max_distance<class_NavigationPathQueryParameters2D_property_path_search_max_distance>` | ``0.0``           |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`path_search_max_polygons<class_NavigationPathQueryParameters2D_property_path_search_max_polygons>` | ``4096``          |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>`         | :ref:`pathfinding_algorithm<class_NavigationPathQueryParameters2D_property_pathfinding_algorithm>`       | ``0``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`simplify_epsilon<class_NavigationPathQueryParameters2D_property_simplify_epsilon>`                 | ``0.0``           |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`simplify_path<class_NavigationPathQueryParameters2D_property_simplify_path>`                       | ``false``         |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                                                                  | :ref:`start_position<class_NavigationPathQueryParameters2D_property_start_position>`                     | ``Vector2(0, 0)`` |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                                                                  | :ref:`target_position<class_NavigationPathQueryParameters2D_property_target_position>`                   | ``Vector2(0, 0)`` |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_NavigationPathQueryParameters2D_PathfindingAlgorithm:

.. rst-class:: classref-enumeration

enum **PathfindingAlgorithm**: :ref:`🔗<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>`

.. _class_NavigationPathQueryParameters2D_constant_PATHFINDING_ALGORITHM_ASTAR:

.. rst-class:: classref-enumeration-constant

:ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>` **PATHFINDING_ALGORITHM_ASTAR** = ``0``

Truy vấn đường dẫn sử dụng thuật toán tìm đường A\* mặc định.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationPathQueryParameters2D_PathPostProcessing:

.. rst-class:: classref-enumeration

enum **PathPostProcessing**: :ref:`🔗<enum_NavigationPathQueryParameters2D_PathPostProcessing>`

.. _class_NavigationPathQueryParameters2D_constant_PATH_POSTPROCESSING_CORRIDORFUNNEL:

.. rst-class:: classref-enumeration-constant

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>` **PATH_POSTPROCESSING_CORRIDORFUNNEL** = ``0``

Áp dụng thuật toán funnel cho corridor đường dẫn thô được thuật toán tìm đường tìm thấy. Kết quả là đường dẫn ngắn nhất có thể bên trong corridor đường dẫn. Quá trình hậu xử lý này phụ thuộc rất nhiều vào bố cục polygon của navigation mesh và corridor được tạo. Đặc biệt, các bố cục dựa trên tile hoặc grid có thể gặp các góc nhân tạo khi di chuyển theo đường chéo do corridor đường dẫn gồ ghề bị hình dạng của các cell áp đặt.

.. _class_NavigationPathQueryParameters2D_constant_PATH_POSTPROCESSING_EDGECENTERED:

.. rst-class:: classref-enumeration-constant

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>` **PATH_POSTPROCESSING_EDGECENTERED** = ``1``

Đưa mọi vị trí trên đường dẫn vào giữa cạnh polygon của navigation mesh đã đi qua. Điều này tạo ra các đường dẫn tốt hơn cho các bố cục dựa trên tile hoặc grid, vốn giới hạn chuyển động vào tâm của các cell.

.. _class_NavigationPathQueryParameters2D_constant_PATH_POSTPROCESSING_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>` **PATH_POSTPROCESSING_NONE** = ``2``

Không áp dụng hậu xử lý và trả về corridor đường dẫn thô như được thuật toán tìm đường tìm thấy.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationPathQueryParameters2D_PathMetadataFlags:

.. rst-class:: classref-enumeration

flags **PathMetadataFlags**: :ref:`🔗<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`

.. _class_NavigationPathQueryParameters2D_constant_PATH_METADATA_INCLUDE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_NONE** = ``0``

Không bao gồm bất kỳ metadata bổ sung nào về đường dẫn được trả về.

.. _class_NavigationPathQueryParameters2D_constant_PATH_METADATA_INCLUDE_TYPES:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_TYPES** = ``1``

Bao gồm kiểu primitive điều hướng (region hoặc link) mà mỗi điểm trên đường dẫn đi qua.

.. _class_NavigationPathQueryParameters2D_constant_PATH_METADATA_INCLUDE_RIDS:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_RIDS** = ``2``

Bao gồm các :ref:`RID<class_RID>`\ của các region và link mà mỗi điểm trên đường dẫn đi qua.

.. _class_NavigationPathQueryParameters2D_constant_PATH_METADATA_INCLUDE_OWNERS:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_OWNERS** = ``4``

Bao gồm các ``ObjectID``\ của các :ref:`Object<class_Object>`\ quản lý các region và link mà mỗi điểm trên đường dẫn đi qua.

.. _class_NavigationPathQueryParameters2D_constant_PATH_METADATA_INCLUDE_ALL:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_ALL** = ``7``

Bao gồm toàn bộ metadata hiện có về đường dẫn được trả về.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationPathQueryParameters2D_property_excluded_regions:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **excluded_regions** = ``[]`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_excluded_regions>`

.. rst-class:: classref-property-setget

- |void| **set_excluded_regions**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_excluded_regions**\ (\ )

Danh sách các :ref:`RID<class_RID>`\ của region sẽ bị loại trừ khỏi truy vấn đường dẫn. Sử dụng :ref:`NavigationRegion2D.get_rid()<class_NavigationRegion2D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node :ref:`NavigationRegion2D<class_NavigationRegion2D>`.

\ **Lưu ý:** Mảng được trả về là một bản sao và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về, sau đó gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_included_regions:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **included_regions** = ``[]`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_included_regions>`

.. rst-class:: classref-property-setget

- |void| **set_included_regions**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_included_regions**\ (\ )

Danh sách các :ref:`RID<class_RID>`\ của region sẽ được truy vấn đường dẫn bao gồm. Sử dụng :ref:`NavigationRegion2D.get_rid()<class_NavigationRegion2D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node :ref:`NavigationRegion2D<class_NavigationRegion2D>`. Nếu để trống, tất cả region sẽ được bao gồm. Nếu một region đồng thời được bao gồm và loại trừ, region đó sẽ bị loại trừ.

\ **Lưu ý:** Mảng được trả về là một bản sao và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về, sau đó gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_map:

.. rst-class:: classref-property

:ref:`RID<class_RID>` **map** = ``RID()`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_map>`

.. rst-class:: classref-property-setget

- |void| **set_map**\ (\ value\: :ref:`RID<class_RID>`\ ) - :ref:`RID<class_RID>` **get_map**\ (\ )

Navigation map :ref:`RID<class_RID>` được sử dụng trong truy vấn đường dẫn.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_metadata_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\] **metadata_flags** = ``7`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_metadata_flags>`

.. rst-class:: classref-property-setget

- |void| **set_metadata_flags**\ (\ value\: |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\]\ ) - |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\] **get_metadata_flags**\ (\ )

Thông tin bổ sung cần bao gồm cùng với đường dẫn điều hướng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_navigation_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **navigation_layers** = ``1`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_navigation_layers>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_navigation_layers**\ (\ )

Các navigation layer mà truy vấn sẽ sử dụng (dưới dạng bitmask).

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_path_postprocessing:

.. rst-class:: classref-property

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>` **path_postprocessing** = ``0`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_path_postprocessing>`

.. rst-class:: classref-property-setget

- |void| **set_path_postprocessing**\ (\ value\: :ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>`\ ) - :ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>` **get_path_postprocessing**\ (\ )

Hậu xử lý đường dẫn được áp dụng cho corridor đường dẫn thô do :ref:`pathfinding_algorithm<class_NavigationPathQueryParameters2D_property_pathfinding_algorithm>` tìm thấy.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_path_return_max_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_length** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_path_return_max_length>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_length**\ (\ )

Độ dài tối đa được phép của đường dẫn được trả về, tính theo đơn vị thế giới. Đường dẫn sẽ bị cắt khi vượt quá độ dài này. Giá trị ``0`` trở xuống được xem là đã tắt.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_path_return_max_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_radius** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_path_return_max_radius>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_radius**\ (\ )

Bán kính tối đa được phép, tính theo đơn vị thế giới, mà đường dẫn được trả về có thể cách điểm bắt đầu của đường dẫn. Đường dẫn sẽ bị cắt khi vượt quá bán kính này. Giá trị ``0`` trở xuống được xem là đã tắt.

\ **Lưu ý:** Thao tác này sẽ thực hiện việc cắt theo hình tròn trên đường dẫn, với vị trí đầu tiên của đường dẫn là tâm của hình tròn.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_path_search_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_search_max_distance** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_path_search_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_search_max_distance**\ (\ )

Khoảng cách tối đa mà một polygon đang được tìm kiếm có thể cách polygon bắt đầu trước khi thuật toán tìm đường hủy việc tìm đường đến polygon vị trí đích (có thể không thể đến được hoặc ở rất xa). Trong trường hợp này, thuật toán tìm đường sẽ đặt lại và xây dựng đường dẫn từ polygon bắt đầu đến polygon gần vị trí đích nhất được tìm thấy cho đến thời điểm đó. Giá trị ``0`` trở xuống được xem là không giới hạn. Khi không giới hạn, thuật toán tìm đường sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí đích hoặc đã dùng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_path_search_max_polygons:

.. rst-class:: classref-property

:ref:`int<class_int>` **path_search_max_polygons** = ``4096`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_path_search_max_polygons>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_polygons**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_path_search_max_polygons**\ (\ )

Số polygon tối đa được tìm kiếm trước khi thuật toán tìm đường hủy việc tìm đường đến polygon vị trí đích (có thể không thể đến được hoặc ở rất xa). Trong trường hợp này, thuật toán tìm đường sẽ đặt lại và xây dựng đường dẫn từ polygon bắt đầu đến polygon gần vị trí đích nhất được tìm thấy cho đến thời điểm đó. Giá trị ``0`` trở xuống được xem là không giới hạn. Khi không giới hạn, thuật toán tìm đường sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí đích hoặc đã dùng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_pathfinding_algorithm:

.. rst-class:: classref-property

:ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>` **pathfinding_algorithm** = ``0`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_pathfinding_algorithm>`

.. rst-class:: classref-property-setget

- |void| **set_pathfinding_algorithm**\ (\ value\: :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>`\ ) - :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>` **get_pathfinding_algorithm**\ (\ )

Thuật toán tìm đường được sử dụng trong truy vấn đường dẫn.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_simplify_epsilon:

.. rst-class:: classref-property

:ref:`float<class_float>` **simplify_epsilon** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_simplify_epsilon>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_epsilon**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_simplify_epsilon**\ (\ )

Mức độ đơn giản hóa đường dẫn, tính theo đơn vị thế giới.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_simplify_path:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **simplify_path** = ``false`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_simplify_path>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_path**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_simplify_path**\ (\ )

Nếu ``true``, một phiên bản đơn giản hóa của đường đi sẽ được trả về, trong đó các điểm ít quan trọng hơn trên đường đi đã được loại bỏ. Mức độ đơn giản hóa được kiểm soát bởi :ref:`simplify_epsilon<class_NavigationPathQueryParameters2D_property_simplify_epsilon>`. Việc đơn giản hóa sử dụng một biến thể của thuật toán Ramer-Douglas-Peucker để giảm số lượng điểm của đường cong.

Việc đơn giản hóa đường đi có thể giúp giảm thiểu nhiều vấn đề khi bám theo đường đi, vốn có thể phát sinh với một số loại agent và hành vi của script. Ví dụ: các agent "steering" hoặc cơ chế tránh vật cản trong "open fields".

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_start_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **start_position** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_start_position>`

.. rst-class:: classref-property-setget

- |void| **set_start_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_start_position**\ (\ )

Vị trí bắt đầu tìm đường trong hệ tọa độ global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters2D_property_target_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **target_position** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationPathQueryParameters2D_property_target_position>`

.. rst-class:: classref-property-setget

- |void| **set_target_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_target_position**\ (\ )

Vị trí đích tìm đường trong hệ tọa độ global.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
