:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeExtension.xml.

.. _class_AnimationNodeExtension:

AnimationNodeExtension
======================

**Thử nghiệm:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Base class for extending :ref:`AnimationRootNode<class_AnimationRootNode>`\ s from GDScript, C#, or C++.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AnimationNodeExtension** cung cấp các API của :ref:`AnimationRootNode<class_AnimationRootNode>` để cho phép người dùng mở rộng nó từ GDScript, C# hoặc C++. Lớp này không предназнач để sử dụng trực tiếp mà để được các lớp khác mở rộng. Lớp này được dùng để tạo các node tùy chỉnh cho hệ thống :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`_process_animation_node<class_AnimationNodeExtension_private_method__process_animation_node>`\ (\ playback_info\: :ref:`PackedFloat64Array<class_PackedFloat64Array>`, test_only\: :ref:`bool<class_bool>`\ ) |virtual| |required| |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get_remaining_time<class_AnimationNodeExtension_method_get_remaining_time>`\ (\ node_info\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`, break_loop\: :ref:`bool<class_bool>`\ ) |static|                                  |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`is_looping<class_AnimationNodeExtension_method_is_looping>`\ (\ node_info\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) |static|                                                                                        |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationNodeExtension_private_method__process_animation_node:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **_process_animation_node**\ (\ playback_info\: :ref:`PackedFloat64Array<class_PackedFloat64Array>`, test_only\: :ref:`bool<class_bool>`\ ) |virtual| |required| :ref:`🔗<class_AnimationNodeExtension_private_method__process_animation_node>`

Một phiên bản của phương thức :ref:`AnimationNode._process()<class_AnimationNode_private_method__process>` được thiết kế để các node tùy chỉnh ghi đè. Phương thức này trả về một :ref:`PackedFloat32Array<class_PackedFloat32Array>` chứa dữ liệu animation đã được xử lý.

Tham số :ref:`PackedFloat64Array<class_PackedFloat64Array>` chứa thông tin phát lại, bao gồm các giá trị sau được mã hóa dưới dạng số thực (theo thứ tự): thời gian phát lại và delta, thời gian bắt đầu và kết thúc, liệu có yêu cầu seek hay không (được mã hóa dưới dạng số thực lớn hơn ``0``), liệu yêu cầu seek có được thực hiện từ bên ngoài hay không (được mã hóa dưới dạng số thực lớn hơn ``0``), :ref:`LoopedFlag<enum_Animation_LoopedFlag>` hiện tại (được mã hóa dưới dạng số thực) và blend weight hiện tại.

Hàm phải trả về một :ref:`PackedFloat32Array<class_PackedFloat32Array>` chứa thông tin thời gian của node, bao gồm các giá trị sau (theo thứ tự): độ dài animation, vị trí thời gian, delta, :ref:`LoopMode<enum_Animation_LoopMode>` (được mã hóa dưới dạng số thực), liệu animation sắp kết thúc hay không (được mã hóa dưới dạng số thực lớn hơn ``0``) và liệu animation có vô hạn hay không (được mã hóa dưới dạng số thực lớn hơn ``0``). Tất cả các giá trị phải được đưa vào mảng trả về.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeExtension_method_get_remaining_time:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_remaining_time**\ (\ node_info\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`, break_loop\: :ref:`bool<class_bool>`\ ) |static| :ref:`🔗<class_AnimationNodeExtension_method_get_remaining_time>`

Trả về thời gian còn lại của animation cho thông tin node đã cho. Đối với animation lặp, phương thức chỉ trả về thời gian còn lại nếu ``break_loop`` là ``true``; nếu không, một giá trị số nguyên lớn sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeExtension_method_is_looping:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_looping**\ (\ node_info\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) |static| :ref:`🔗<class_AnimationNodeExtension_method_is_looping>`

Trả về ``true`` nếu animation của ``node_info`` đã cho đang lặp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
