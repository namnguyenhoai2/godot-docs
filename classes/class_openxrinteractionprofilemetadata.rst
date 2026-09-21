:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRInteractionProfileMetadata.xml.

.. _class_OpenXRInteractionProfileMetadata:

OpenXRInteractionProfileMetadata
================================

**Kế thừa:** :ref:`Object<class_Object>`

Lớp meta đăng ký các thiết bị được hỗ trợ trong OpenXR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này cho phép OpenXR core và các extension đăng ký metadata liên quan đến những thiết bị tương tác được hỗ trợ, chẳng hạn như controller, tracker, thiết bị haptic, v.v. Lớp này chủ yếu được action map editor sử dụng và dùng để làm sạch action map bằng cách loại bỏ các mục phụ thuộc vào extension khi thích hợp.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`register_interaction_profile<class_OpenXRInteractionProfileMetadata_method_register_interaction_profile>`\ (\ display_name\: :ref:`String<class_String>`, openxr_path\: :ref:`String<class_String>`, openxr_extension_names\: :ref:`String<class_String>`\ )                                                                                                                                        |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`register_io_path<class_OpenXRInteractionProfileMetadata_method_register_io_path>`\ (\ interaction_profile\: :ref:`String<class_String>`, display_name\: :ref:`String<class_String>`, toplevel_path\: :ref:`String<class_String>`, openxr_path\: :ref:`String<class_String>`, openxr_extension_names\: :ref:`String<class_String>`, action_type\: :ref:`ActionType<enum_OpenXRAction_ActionType>`\ ) |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`register_path_rename<class_OpenXRInteractionProfileMetadata_method_register_path_rename>`\ (\ old_name\: :ref:`String<class_String>`, new_name\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                     |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`register_profile_rename<class_OpenXRInteractionProfileMetadata_method_register_profile_rename>`\ (\ old_name\: :ref:`String<class_String>`, new_name\: :ref:`String<class_String>`\ )                                                                                                                                                                                                               |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`register_top_level_path<class_OpenXRInteractionProfileMetadata_method_register_top_level_path>`\ (\ display_name\: :ref:`String<class_String>`, openxr_path\: :ref:`String<class_String>`, openxr_extension_names\: :ref:`String<class_String>`\ )                                                                                                                                                  |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRInteractionProfileMetadata_method_register_interaction_profile:

.. rst-class:: classref-method

|void| **register_interaction_profile**\ (\ display_name\: :ref:`String<class_String>`, openxr_path\: :ref:`String<class_String>`, openxr_extension_names\: :ref:`String<class_String>`\ ) :ref:`🔗<class_OpenXRInteractionProfileMetadata_method_register_interaction_profile>`

Đăng ký một interaction profile bằng định danh OpenXR của nó (ví dụ: ``/interaction_profiles/khr/simple_controller`` là profile dành cho simple controller profile của OpenXR).

\ ``display_name`` là phần mô tả hiển thị cho người dùng. ``openxr_path`` là interaction profile path đang được đăng ký. ``openxr_extension_names`` tùy chọn giới hạn profile này cho extension đã được bật/có sẵn cụ thể. Nếu extension không có sẵn, profile và tất cả mục liên quan được sử dụng trong action map sẽ bị lọc bỏ.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInteractionProfileMetadata_method_register_io_path:

.. rst-class:: classref-method

|void| **register_io_path**\ (\ interaction_profile\: :ref:`String<class_String>`, display_name\: :ref:`String<class_String>`, toplevel_path\: :ref:`String<class_String>`, openxr_path\: :ref:`String<class_String>`, openxr_extension_names\: :ref:`String<class_String>`, action_type\: :ref:`ActionType<enum_OpenXRAction_ActionType>`\ ) :ref:`🔗<class_OpenXRInteractionProfileMetadata_method_register_io_path>`

Đăng ký một input/output path cho ``interaction_profile`` đã cho. Profile này trước đó phải được đăng ký bằng :ref:`register_interaction_profile()<class_OpenXRInteractionProfileMetadata_method_register_interaction_profile>`. ``display_name`` là phần mô tả hiển thị cho người dùng. ``toplevel_path`` chỉ định bind path mà input/output này có thể được bind vào (ví dụ: ``/user/hand/left`` hoặc ``/user/hand/right``). ``openxr_path`` là action input/output đang được đăng ký (ví dụ: ``/user/hand/left/input/aim/pose``). ``openxr_extension_names`` giới hạn input/output này cho một extension đã được bật/có sẵn; không cần lặp lại extension trong profile, nhưng liên quan đến extension chồng lấp (ví dụ: ``XR_EXT_palm_pose``) giới thiệu các input path ``…/input/palm_ext/pose``. ``action_type`` xác định loại input hoặc output do OpenXR cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInteractionProfileMetadata_method_register_path_rename:

.. rst-class:: classref-method

|void| **register_path_rename**\ (\ old_name\: :ref:`String<class_String>`, new_name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_OpenXRInteractionProfileMetadata_method_register_path_rename>`

Cho phép đổi tên các input/output path cũ thành path mới để tải và xử lý các action map cũ hơn.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInteractionProfileMetadata_method_register_profile_rename:

.. rst-class:: classref-method

|void| **register_profile_rename**\ (\ old_name\: :ref:`String<class_String>`, new_name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_OpenXRInteractionProfileMetadata_method_register_profile_rename>`

Cho phép đổi tên các interaction profile path cũ thành path mới để tải và xử lý các action map cũ hơn.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInteractionProfileMetadata_method_register_top_level_path:

.. rst-class:: classref-method

|void| **register_top_level_path**\ (\ display_name\: :ref:`String<class_String>`, openxr_path\: :ref:`String<class_String>`, openxr_extension_names\: :ref:`String<class_String>`\ ) :ref:`🔗<class_OpenXRInteractionProfileMetadata_method_register_top_level_path>`

Đăng ký một top level path mà các profile có thể được bind vào. Ví dụ, ``/user/hand/left`` tham chiếu đến bind point dành cho tay trái của người chơi. Các extension có thể đăng ký thêm top level path, chẳng hạn extension cho áo vest haptic có thể đăng ký ``/user/body/vest``.

\ ``display_name`` là tên hiển thị cho người dùng. ``openxr_path`` là top level path đang được đăng ký. ``openxr_extension_names`` là tùy chọn và đảm bảo top level path chỉ được sử dụng khi extension được chỉ định có sẵn/được bật.

Khi một top level path cuối cùng được OpenXR bind, một :ref:`XRPositionalTracker<class_XRPositionalTracker>` sẽ được khởi tạo để quản lý trạng thái của thiết bị.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
