:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/fbx/doc_classes/FBXDocument.xml.

.. _class_FBXDocument:

FBXDocument
===========

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`GLTFDocument<class_GLTFDocument>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Xử lý các tài liệu FBX.

.. rst-class:: classref-introduction-group

Mô tả
-----

FBXDocument xử lý các tài liệu FBX. Nó cung cấp các phương thức để thêm dữ liệu từ các buffer hoặc tệp, tạo scene, cũng như đăng ký/hủy đăng ký các phần mở rộng của tài liệu.

Khi export FBX từ Blender, hãy sử dụng tùy chọn "FBX Units Scale". Tùy chọn "FBX Units Scale" thiết lập hệ số scale chính xác và tránh phải điều chỉnh thủ công khi import lại vào Blender, chẳng hạn như thông qua quá trình export glTF.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
