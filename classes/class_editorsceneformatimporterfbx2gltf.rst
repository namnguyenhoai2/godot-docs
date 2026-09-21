:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/fbx/doc_classes/EditorSceneFormatImporterFBX2GLTF.xml.

.. _class_EditorSceneFormatImporterFBX2GLTF:

EditorSceneFormatImporterFBX2GLTF
=================================

**Kế thừa:** :ref:`EditorSceneFormatImporter<class_EditorSceneFormatImporter>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Importer cho định dạng tệp scene ``.fbx``.

.. rst-class:: classref-introduction-group

Mô tả
-----

Import các scene 3D Autodesk FBX bằng cách chuyển đổi chúng sang glTF 2.0 thông qua công cụ dòng lệnh FBX2glTF.

Vị trí của binary FBX2glTF được thiết lập thông qua thiết lập editor :ref:`EditorSettings.filesystem/import/fbx/fbx2gltf_path<class_EditorSettings_property_filesystem/import/fbx/fbx2gltf_path>`.

Importer này chỉ được sử dụng nếu :ref:`ProjectSettings.filesystem/import/fbx2gltf/enabled<class_ProjectSettings_property_filesystem/import/fbx2gltf/enabled>` được đặt thành ``true``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
