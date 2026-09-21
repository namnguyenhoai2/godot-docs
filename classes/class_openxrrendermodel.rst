:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRRenderModel.xml.

.. _class_OpenXRRenderModel:

OpenXRRenderModel
=================

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node này sẽ hiển thị một render model OpenXR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này sẽ hiển thị một render model OpenXR bằng cách truy cập GLTF liên kết và xử lý tất cả dữ liệu animation (nếu được XR runtime hỗ trợ).

Render model được giới thiệu để cho phép hiển thị model chính xác của controller (hoặc thiết bị khác) mà người dùng đang cầm trên tay, vì OpenXR action map không cung cấp thông tin về phần cứng mà người dùng đang sử dụng. Lưu ý rằng mặc dù có thể suy ra phần nào controller (hoặc thiết bị) thông qua action map profile được liên kết, đây là một cách tiếp cận nguy hiểm vì người dùng có thể đang sử dụng phần cứng chưa được biết đến tại thời điểm phát triển, và OpenXR sẽ chỉ mô phỏng một interaction profile có sẵn.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------------+-----------+
   | :ref:`RID<class_RID>` | :ref:`render_model<class_OpenXRRenderModel_property_render_model>` | ``RID()`` |
   +-----------------------+--------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_top_level_path<class_OpenXRRenderModel_method_get_top_level_path>`\ (\ ) |const| |
   +-----------------------------+--------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_OpenXRRenderModel_signal_render_model_top_level_path_changed:

.. rst-class:: classref-signal

**render_model_top_level_path_changed**\ (\ ) :ref:`🔗<class_OpenXRRenderModel_signal_render_model_top_level_path_changed>`

Được phát ra khi top level path của render model này thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRRenderModel_property_render_model:

.. rst-class:: classref-property

:ref:`RID<class_RID>` **render_model** = ``RID()`` :ref:`🔗<class_OpenXRRenderModel_property_render_model>`

.. rst-class:: classref-property-setget

- |void| **set_render_model**\ (\ value\: :ref:`RID<class_RID>`\ ) - :ref:`RID<class_RID>` **get_render_model**\ (\ )

RID của render model cần tải, được trả về bởi :ref:`OpenXRRenderModelExtension.render_model_create()<class_OpenXRRenderModelExtension_method_render_model_create>` hoặc :ref:`OpenXRRenderModelExtension.render_model_get_all()<class_OpenXRRenderModelExtension_method_render_model_get_all>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRRenderModel_method_get_top_level_path:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_top_level_path**\ (\ ) |const| :ref:`🔗<class_OpenXRRenderModel_method_get_top_level_path>`

Trả về top level path liên quan đến render model này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
