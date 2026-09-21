:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationPathQueryParameters3D.xml.

.. _class_NavigationPathQueryParameters3D:

NavigationPathQueryParameters3D
===============================

**Thử nghiệm:** Lớp này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho các truy vấn đường dẫn điều hướng 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi nhiều thuộc tính khác nhau của đối tượng này, chẳng hạn như vị trí bắt đầu và vị trí đích, bạn có thể cấu hình các truy vấn đường dẫn tới :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationPathQueryObjects <../tutorials/navigation/navigation_using_navigationpathqueryobjects>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]                                             | :ref:`excluded_regions<class_NavigationPathQueryParameters3D_property_excluded_regions>`                 | ``[]``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]                                             | :ref:`included_regions<class_NavigationPathQueryParameters3D_property_included_regions>`                 | ``[]``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`RID<class_RID>`                                                                          | :ref:`map<class_NavigationPathQueryParameters3D_property_map>`                                           | ``RID()``            |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\] | :ref:`metadata_flags<class_NavigationPathQueryParameters3D_property_metadata_flags>`                     | ``7``                |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`navigation_layers<class_NavigationPathQueryParameters3D_property_navigation_layers>`               | ``1``                |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>`             | :ref:`path_postprocessing<class_NavigationPathQueryParameters3D_property_path_postprocessing>`           | ``0``                |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_length<class_NavigationPathQueryParameters3D_property_path_return_max_length>`     | ``0.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_radius<class_NavigationPathQueryParameters3D_property_path_return_max_radius>`     | ``0.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_search_max_distance<class_NavigationPathQueryParameters3D_property_path_search_max_distance>` | ``0.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`path_search_max_polygons<class_NavigationPathQueryParameters3D_property_path_search_max_polygons>` | ``4096``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>`         | :ref:`pathfinding_algorithm<class_NavigationPathQueryParameters3D_property_pathfinding_algorithm>`       | ``0``                |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`simplify_epsilon<class_NavigationPathQueryParameters3D_property_simplify_epsilon>`                 | ``0.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`simplify_path<class_NavigationPathQueryParameters3D_property_simplify_path>`                       | ``false``            |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                                                                  | :ref:`start_position<class_NavigationPathQueryParameters3D_property_start_position>`                     | ``Vector3(0, 0, 0)`` |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                                                                  | :ref:`target_position<class_NavigationPathQueryParameters3D_property_target_position>`                   | ``Vector3(0, 0, 0)`` |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_NavigationPathQueryParameters3D_PathfindingAlgorithm:

.. rst-class:: classref-enumeration

enum **PathfindingAlgorithm**: :ref:`🔗<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>`

.. _class_NavigationPathQueryParameters3D_constant_PATHFINDING_ALGORITHM_ASTAR:

.. rst-class:: classref-enumeration-constant

:ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>` **PATHFINDING_ALGORITHM_ASTAR** = ``0``

Truy vấn đường dẫn sử dụng thuật toán tìm đường A\* mặc định.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationPathQueryParameters3D_PathPostProcessing:

.. rst-class:: classref-enumeration

enum **PathPostProcessing**: :ref:`🔗<enum_NavigationPathQueryParameters3D_PathPostProcessing>`

.. _class_NavigationPathQueryParameters3D_constant_PATH_POSTPROCESSING_CORRIDORFUNNEL:

.. rst-class:: classref-enumeration-constant

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>` **PATH_POSTPROCESSING_CORRIDORFUNNEL** = ``0``

Áp dụng thuật toán funnel cho corridor đường dẫn thô được thuật toán tìm đường phát hiện. Kết quả sẽ là đường dẫn ngắn nhất có thể bên trong corridor đường dẫn. Việc hậu xử lý này phụ thuộc rất nhiều vào bố cục polygon của navigation mesh và corridor được tạo. Đặc biệt, các bố cục dựa trên tile hoặc grid có thể gặp các góc nhân tạo khi di chuyển theo đường chéo do corridor đường dẫn lởm chởm bị hình dạng của các ô áp đặt.

.. _class_NavigationPathQueryParameters3D_constant_PATH_POSTPROCESSING_EDGECENTERED:

.. rst-class:: classref-enumeration-constant

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>` **PATH_POSTPROCESSING_EDGECENTERED** = ``1``

Đưa mọi vị trí trên đường dẫn vào chính giữa cạnh polygon của navigation mesh đã đi qua. Điều này tạo ra các đường dẫn tốt hơn cho các bố cục dựa trên tile hoặc grid vốn giới hạn việc di chuyển ở tâm các ô.

.. _class_NavigationPathQueryParameters3D_constant_PATH_POSTPROCESSING_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>` **PATH_POSTPROCESSING_NONE** = ``2``

Không áp dụng hậu xử lý và trả về corridor đường dẫn thô do thuật toán tìm đường phát hiện.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationPathQueryParameters3D_PathMetadataFlags:

.. rst-class:: classref-enumeration

flags **PathMetadataFlags**: :ref:`🔗<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`

.. _class_NavigationPathQueryParameters3D_constant_PATH_METADATA_INCLUDE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_NONE** = ``0``

Không đưa thêm metadata nào về đường dẫn được trả về.

.. _class_NavigationPathQueryParameters3D_constant_PATH_METADATA_INCLUDE_TYPES:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_TYPES** = ``1``

Đưa vào kiểu của navigation primitive (region hoặc link) mà mỗi điểm trên đường dẫn đi qua.

.. _class_NavigationPathQueryParameters3D_constant_PATH_METADATA_INCLUDE_RIDS:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_RIDS** = ``2``

Đưa vào các :ref:`RID<class_RID>`\ s của những region và link mà mỗi điểm trên đường dẫn đi qua.

.. _class_NavigationPathQueryParameters3D_constant_PATH_METADATA_INCLUDE_OWNERS:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_OWNERS** = ``4``

Đưa vào các ``ObjectID``\ s của những :ref:`Object<class_Object>`\ s quản lý các region và link mà mỗi điểm trên đường dẫn đi qua.

.. _class_NavigationPathQueryParameters3D_constant_PATH_METADATA_INCLUDE_ALL:

.. rst-class:: classref-enumeration-constant

:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>` **PATH_METADATA_INCLUDE_ALL** = ``7``

Đưa vào tất cả metadata hiện có về đường dẫn được trả về.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationPathQueryParameters3D_property_excluded_regions:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **excluded_regions** = ``[]`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_excluded_regions>`

.. rst-class:: classref-property-setget

- |void| **set_excluded_regions**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_excluded_regions**\ (\ )

Danh sách các :ref:`RID<class_RID>`\ s của region sẽ bị loại trừ khỏi truy vấn đường dẫn. Sử dụng :ref:`NavigationRegion3D.get_rid()<class_NavigationRegion3D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node :ref:`NavigationRegion3D<class_NavigationRegion3D>`.

\ **Lưu ý:** Mảng được trả về là bản sao và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính gốc. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về rồi gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_included_regions:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **included_regions** = ``[]`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_included_regions>`

.. rst-class:: classref-property-setget

- |void| **set_included_regions**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_included_regions**\ (\ )

Danh sách các :ref:`RID<class_RID>`\ s của region sẽ được truy vấn đường dẫn đưa vào. Sử dụng :ref:`NavigationRegion3D.get_rid()<class_NavigationRegion3D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node :ref:`NavigationRegion3D<class_NavigationRegion3D>`. Nếu để trống, tất cả region đều được đưa vào. Nếu một region đồng thời được đưa vào và loại trừ, nó sẽ bị loại trừ.

\ **Lưu ý:** Mảng được trả về là bản sao và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính gốc. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về rồi gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_map:

.. rst-class:: classref-property

:ref:`RID<class_RID>` **map** = ``RID()`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_map>`

.. rst-class:: classref-property-setget

- |void| **set_map**\ (\ value\: :ref:`RID<class_RID>`\ ) - :ref:`RID<class_RID>` **get_map**\ (\ )

Navigation map :ref:`RID<class_RID>` được sử dụng trong truy vấn đường dẫn.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_metadata_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\] **metadata_flags** = ``7`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_metadata_flags>`

.. rst-class:: classref-property-setget

- |void| **set_metadata_flags**\ (\ value\: |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\]\ ) - |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\] **get_metadata_flags**\ (\ )

Thông tin bổ sung cần đưa vào đường dẫn điều hướng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_navigation_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **navigation_layers** = ``1`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_navigation_layers>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_navigation_layers**\ (\ )

Các navigation layer mà truy vấn sẽ sử dụng (dưới dạng bitmask).

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_path_postprocessing:

.. rst-class:: classref-property

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>` **path_postprocessing** = ``0`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_path_postprocessing>`

.. rst-class:: classref-property-setget

- |void| **set_path_postprocessing**\ (\ value\: :ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>`\ ) - :ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>` **get_path_postprocessing**\ (\ )

Hậu xử lý đường dẫn được áp dụng cho corridor đường dẫn thô do :ref:`pathfinding_algorithm<class_NavigationPathQueryParameters3D_property_pathfinding_algorithm>` phát hiện.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_path_return_max_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_length** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_path_return_max_length>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_length**\ (\ )

Độ dài tối đa được phép của đường dẫn được trả về, tính theo đơn vị thế giới. Đường dẫn sẽ bị cắt khi vượt quá độ dài này. Giá trị ``0`` trở xuống được xem là đã tắt.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_path_return_max_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_radius** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_path_return_max_radius>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_radius**\ (\ )

Bán kính tối đa được phép, tính theo đơn vị thế giới, mà đường dẫn được trả về có thể cách điểm bắt đầu của đường dẫn. Đường dẫn sẽ bị cắt khi vượt quá bán kính này. Giá trị ``0`` trở xuống được xem là đã tắt.

\ **Lưu ý:** Thao tác này sẽ cắt đường dẫn theo hình cầu, với vị trí đầu tiên trên đường dẫn là tâm của hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_path_search_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_search_max_distance** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_path_search_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_search_max_distance**\ (\ )

Khoảng cách tối đa mà một polygon được tìm kiếm có thể cách polygon bắt đầu trước khi thuật toán tìm đường hủy việc tìm đường tới polygon vị trí đích (có thể không thể tiếp cận hoặc ở rất xa). Trong trường hợp này, thuật toán tìm đường đặt lại và xây dựng đường dẫn từ polygon bắt đầu tới polygon được phát hiện là gần vị trí đích nhất cho đến thời điểm đó. Giá trị ``0`` trở xuống được xem là không giới hạn. Khi không giới hạn, thuật toán tìm đường sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí đích hoặc đã sử dụng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_path_search_max_polygons:

.. rst-class:: classref-property

:ref:`int<class_int>` **path_search_max_polygons** = ``4096`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_path_search_max_polygons>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_polygons**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_path_search_max_polygons**\ (\ )

Số lượng polygon tối đa được tìm kiếm trước khi thuật toán tìm đường hủy việc tìm đường tới polygon vị trí đích (có thể không thể tiếp cận hoặc ở rất xa). Trong trường hợp này, thuật toán tìm đường đặt lại và xây dựng đường dẫn từ polygon bắt đầu tới polygon được phát hiện là gần vị trí đích nhất cho đến thời điểm đó. Giá trị ``0`` trở xuống được xem là không giới hạn. Khi không giới hạn, thuật toán tìm đường sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí đích hoặc đã sử dụng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_pathfinding_algorithm:

.. rst-class:: classref-property

:ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>` **pathfinding_algorithm** = ``0`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_pathfinding_algorithm>`

.. rst-class:: classref-property-setget

- |void| **set_pathfinding_algorithm**\ (\ value\: :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>`\ ) - :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>` **get_pathfinding_algorithm**\ (\ )

Thuật toán tìm đường được sử dụng trong truy vấn đường dẫn.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_simplify_epsilon:

.. rst-class:: classref-property

:ref:`float<class_float>` **simplify_epsilon** = ``0.0`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_simplify_epsilon>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_epsilon**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_simplify_epsilon**\ (\ )

Mức độ đơn giản hóa đường dẫn, tính theo đơn vị thế giới.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_simplify_path:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **simplify_path** = ``false`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_simplify_path>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_path**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_simplify_path**\ (\ )

Nếu ``true``, một phiên bản được đơn giản hóa của path sẽ được trả về, trong đó các điểm path ít quan trọng hơn đã bị loại bỏ. Mức độ đơn giản hóa được điều khiển bởi :ref:`simplify_epsilon<class_NavigationPathQueryParameters3D_property_simplify_epsilon>`. Việc đơn giản hóa sử dụng một biến thể của thuật toán Ramer-Douglas-Peucker để giảm số lượng điểm trên đường cong.

Việc đơn giản hóa path có thể hữu ích để giảm thiểu nhiều vấn đề khi đi theo path có thể phát sinh với một số loại agent và hành vi của script. Ví dụ: các agent "steering" hoặc cơ chế tránh né trong "open fields".

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_start_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **start_position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_start_position>`

.. rst-class:: classref-property-setget

- |void| **set_start_position**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_start_position**\ (\ )

Vị trí bắt đầu tìm path trong tọa độ global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryParameters3D_property_target_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **target_position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_NavigationPathQueryParameters3D_property_target_position>`

.. rst-class:: classref-property-setget

- |void| **set_target_position**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_target_position**\ (\ )

Vị trí đích tìm path trong tọa độ global.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
