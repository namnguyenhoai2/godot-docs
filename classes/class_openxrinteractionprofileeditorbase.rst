:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRInteractionProfileEditorBase.xml.

.. _class_OpenXRInteractionProfileEditorBase:

OpenXRInteractionProfileEditorBase
==================================

**Kế thừa:** :ref:`HBoxContainer<class_HBoxContainer>` **<** :ref:`BoxContainer<class_BoxContainer>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`OpenXRInteractionProfileEditor<class_OpenXRInteractionProfileEditor>`

Lớp cơ sở để chỉnh sửa các interaction profile.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là lớp cơ sở dành cho các trình chỉnh sửa interaction profile được trình chỉnh sửa action map của OpenXR sử dụng. Lớp này có thể được dùng để tạo các trình chỉnh sửa tùy chỉnh cho những interaction profile cụ thể.

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`setup<class_OpenXRInteractionProfileEditorBase_method_setup>`\ (\ action_map\: :ref:`OpenXRActionMap<class_OpenXRActionMap>`, interaction_profile\: :ref:`OpenXRInteractionProfile<class_OpenXRInteractionProfile>`\ ) |
   +--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRInteractionProfileEditorBase_method_setup:

.. rst-class:: classref-method

|void| **setup**\ (\ action_map\: :ref:`OpenXRActionMap<class_OpenXRActionMap>`, interaction_profile\: :ref:`OpenXRInteractionProfile<class_OpenXRInteractionProfile>`\ ) :ref:`🔗<class_OpenXRInteractionProfileEditorBase_method_setup>`

Thiết lập trình chỉnh sửa này cho ``action_map`` và ``interaction_profile`` được cung cấp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
