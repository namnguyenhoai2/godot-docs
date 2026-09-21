:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeTimeSeek.xml.

.. _class_AnimationNodeTimeSeek:

AnimationNodeTimeSeek
=====================

**Kế thừa:** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một node animation tìm kiếm theo thời gian được sử dụng trong :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node animation này có thể được sử dụng để khiến mọi node con trong animation graph thực hiện lệnh tìm kiếm. Dùng để phát một :ref:`Animation<class_Animation>` từ đầu hoặc từ một vị trí phát nhất định bên trong :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

Sau khi đặt thời gian và thay đổi quá trình phát animation, node tìm kiếm theo thời gian sẽ tự động chuyển sang chế độ ngủ ở frame process tiếp theo bằng cách đặt giá trị ``seek_request`` thành ``-1.0``.


.. tabs::

 .. code-tab:: gdscript

    # Phát animation con từ đầu.
    animation_tree.set("parameters/TimeSeek/seek_request", 0.0)
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/TimeSeek/seek_request"] = 0.0

    # Phát animation con từ mốc thời gian 12 giây.
    animation_tree.set("parameters/TimeSeek/seek_request", 12.0)
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/TimeSeek/seek_request"] = 12.0

 .. code-tab:: csharp

    // Phát animation con từ đầu.
    animationTree.Set("parameters/TimeSeek/seek_request", 0.0);

    // Phát animation con từ mốc thời gian 12 giây.
    animationTree.Set("parameters/TimeSeek/seek_request", 12.0);



.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>` | :ref:`explicit_elapse<class_AnimationNodeTimeSeek_property_explicit_elapse>` | ``true`` |
   +-------------------------+------------------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeTimeSeek_property_explicit_elapse:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **explicit_elapse** = ``true`` :ref:`🔗<class_AnimationNodeTimeSeek_property_explicit_elapse>`

.. rst-class:: classref-property-setget

- |void| **set_explicit_elapse**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_explicit_elapse**\ (\ )

Nếu ``true``, một số quy trình sẽ được thực thi để xử lý các key nằm giữa những lần tìm kiếm, chẳng hạn như tính toán root motion và tìm key rời rạc gần nhất.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
