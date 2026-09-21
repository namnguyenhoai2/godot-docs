:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/EditorSceneFormatImporterBlend.xml.

.. _class_EditorSceneFormatImporterBlend:

EditorSceneFormatImporterBlend
==============================

**Kế thừa:** :ref:`EditorSceneFormatImporter<class_EditorSceneFormatImporter>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Importer cho định dạng tệp scene ``.blend`` của Blender.

.. rst-class:: classref-introduction-group

Mô tả
-----

Nhập các scene Blender ở định dạng tệp ``.blend`` thông qua pipeline import 3D glTF 2.0. Importer này yêu cầu người dùng đã cài đặt Blender để có thể dùng Blender xuất scene sang glTF 2.0.

Vị trí của binary Blender được thiết lập thông qua setting :ref:`EditorSettings.filesystem/import/blender/blender_path<class_EditorSettings_property_filesystem/import/blender/blender_path>`.

Importer này chỉ được sử dụng khi :ref:`ProjectSettings.filesystem/import/blender/enabled<class_ProjectSettings_property_filesystem/import/blender/enabled>` được bật; nếu không, các tệp ``.blend`` có trong thư mục project sẽ không được import.

Việc import Blend yêu cầu Blender 3.0.

Về mặt nội bộ, EditorSceneFormatImporterBlend sử dụng chế độ "Use Original" của Blender glTF để tham chiếu đến các texture bên ngoài.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
