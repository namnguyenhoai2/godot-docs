:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/fbx/doc_classes/FBXState.xml.

.. _class_FBXState:

FBXState
========

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`GLTFState<class_GLTFState>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

.. rst-class:: classref-introduction-group

Mô tả
-----

FBXState xử lý dữ liệu trạng thái được import từ các tệp FBX.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`allow_geometry_helper_nodes<class_FBXState_property_allow_geometry_helper_nodes>` | ``false`` |
   +-------------------------+-----------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FBXState_property_allow_geometry_helper_nodes:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **allow_geometry_helper_nodes** = ``false`` :ref:`🔗<class_FBXState_property_allow_geometry_helper_nodes>`

.. rst-class:: classref-property-setget

- |void| **set_allow_geometry_helper_nodes**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_allow_geometry_helper_nodes**\ (\ )

Nếu ``true``, quy trình import sẽ sử dụng các node phụ được gọi là geometry helper nodes. Các node này giúp bảo toàn các pivot và phép biến đổi của model 3D gốc trong quá trình import.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
