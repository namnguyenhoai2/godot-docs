:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/OptimizedTranslation.xml.

.. _class_OptimizedTranslation:

OptimizedTranslation
====================

**Kế thừa:** :ref:`Translation<class_Translation>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một bản dịch được tối ưu hóa.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một bản dịch được tối ưu hóa. Sử dụng các bản dịch được nén theo thời gian thực, tạo ra các từ điển có kích thước rất nhỏ.

Lớp này không lưu trữ các chuỗi chưa dịch vì mục đích tối ưu hóa. Do đó, :ref:`Translation.get_message_list()<class_Translation_method_get_message_list>` luôn trả về một mảng rỗng, còn :ref:`Translation.get_message_count()<class_Translation_method_get_message_count>` luôn trả về ``0``.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`generate<class_OptimizedTranslation_method_generate>`\ (\ from\: :ref:`Translation<class_Translation>`\ ) |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OptimizedTranslation_method_generate:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **generate**\ (\ from\: :ref:`Translation<class_Translation>`\ ) :ref:`🔗<class_OptimizedTranslation_method_generate>`

Tạo và thiết lập một bản dịch được tối ưu hóa từ resource :ref:`Translation<class_Translation>` đã cho. Trả về ``true`` nếu thành công.

\ **Lưu ý:** Các message trong ``from`` không nên sử dụng context hoặc dạng số nhiều.

\ **Lưu ý:** Phương thức này предназначен để sử dụng trong editor. Phương thức không thực hiện gì khi được gọi từ một project đã export.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
