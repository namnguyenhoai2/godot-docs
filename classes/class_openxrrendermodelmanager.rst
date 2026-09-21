:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRRenderModelManager.xml.

.. _class_OpenXRRenderModelManager:

OpenXRRenderModelManager
========================

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node trợ giúp sẽ tự động quản lý việc hiển thị các render model.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node trợ giúp này sẽ tự động quản lý việc hiển thị các render model. Node sẽ tạo các node :ref:`OpenXRRenderModel<class_OpenXRRenderModel>` mới khi phát hiện controller và các thiết bị cầm tay khác, đồng thời xóa các node đó khi chúng bị vô hiệu hóa.

\ **Lưu ý:** Nếu muốn kiểm soát logic này tốt hơn, bạn có thể gọi :ref:`OpenXRRenderModelExtension.render_model_get_all()<class_OpenXRRenderModelExtension_method_render_model_get_all>` để lấy danh sách các render model id đang hoạt động và tạo các instance :ref:`OpenXRRenderModel<class_OpenXRRenderModel>` cho từng render model id được cung cấp.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------------+---------------------------------------------------------------------------------------+--------+
   | :ref:`String<class_String>`                                                 | :ref:`make_local_to_pose<class_OpenXRRenderModelManager_property_make_local_to_pose>` | ``""`` |
   +-----------------------------------------------------------------------------+---------------------------------------------------------------------------------------+--------+
   | :ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>` | :ref:`tracker<class_OpenXRRenderModelManager_property_tracker>`                       | ``0``  |
   +-----------------------------------------------------------------------------+---------------------------------------------------------------------------------------+--------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_OpenXRRenderModelManager_signal_render_model_added:

.. rst-class:: classref-signal

**render_model_added**\ (\ render_model\: :ref:`OpenXRRenderModel<class_OpenXRRenderModel>`\ ) :ref:`🔗<class_OpenXRRenderModelManager_signal_render_model_added>`

Được phát ra khi một node render model được thêm làm node con của node này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRRenderModelManager_signal_render_model_removed:

.. rst-class:: classref-signal

**render_model_removed**\ (\ render_model\: :ref:`OpenXRRenderModel<class_OpenXRRenderModel>`\ ) :ref:`🔗<class_OpenXRRenderModelManager_signal_render_model_removed>`

Được phát ra ngay trước khi một node con render model bị xóa khỏi node này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_OpenXRRenderModelManager_RenderModelTracker:

.. rst-class:: classref-enumeration

enum **RenderModelTracker**: :ref:`🔗<enum_OpenXRRenderModelManager_RenderModelTracker>`

.. _class_OpenXRRenderModelManager_constant_RENDER_MODEL_TRACKER_ANY:

.. rst-class:: classref-enumeration-constant

:ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>` **RENDER_MODEL_TRACKER_ANY** = ``0``

Hiển thị tất cả các render model đang hoạt động, bất kể chúng liên quan đến tracker nào.

.. _class_OpenXRRenderModelManager_constant_RENDER_MODEL_TRACKER_NONE_SET:

.. rst-class:: classref-enumeration-constant

:ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>` **RENDER_MODEL_TRACKER_NONE_SET** = ``1``

Chỉ hiển thị các render model đang hoạt động không liên quan đến bất kỳ tracker nào do chúng ta quản lý.

.. _class_OpenXRRenderModelManager_constant_RENDER_MODEL_TRACKER_LEFT_HAND:

.. rst-class:: classref-enumeration-constant

:ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>` **RENDER_MODEL_TRACKER_LEFT_HAND** = ``2``

Chỉ hiển thị các render model đang hoạt động liên quan đến tracker tay trái.

.. _class_OpenXRRenderModelManager_constant_RENDER_MODEL_TRACKER_RIGHT_HAND:

.. rst-class:: classref-enumeration-constant

:ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>` **RENDER_MODEL_TRACKER_RIGHT_HAND** = ``3``

Chỉ hiển thị các render model đang hoạt động liên quan đến tracker tay phải.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRRenderModelManager_property_make_local_to_pose:

.. rst-class:: classref-property

:ref:`String<class_String>` **make_local_to_pose** = ``""`` :ref:`🔗<class_OpenXRRenderModelManager_property_make_local_to_pose>`

.. rst-class:: classref-property-setget

- |void| **set_make_local_to_pose**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_make_local_to_pose**\ (\ )

Đặt các render model theo hệ tọa độ cục bộ của pose này (điều này sẽ điều chỉnh vị trí của node container chứa các render model).

.. rst-class:: classref-item-separator

----

.. _class_OpenXRRenderModelManager_property_tracker:

.. rst-class:: classref-property

:ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>` **tracker** = ``0`` :ref:`🔗<class_OpenXRRenderModelManager_property_tracker>`

.. rst-class:: classref-property-setget

- |void| **set_tracker**\ (\ value\: :ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>`\ ) - :ref:`RenderModelTracker<enum_OpenXRRenderModelManager_RenderModelTracker>` **get_tracker**\ (\ )

Giới hạn các render model theo tracker được chỉ định. Bao gồm: 0 = Tất cả render model, 1 = Các render model không liên quan đến tracker, 2 = Các render model liên quan đến tracker tay trái, 3 = Các render model liên quan đến tracker tay phải.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
