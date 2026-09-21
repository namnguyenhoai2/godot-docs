:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NodePath.xml.

.. _class_NodePath:

NodePath
========

Đường dẫn cây cảnh đã được phân tích cú pháp trước.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểu dựng sẵn **NodePath** :ref:`Variant<class_Variant>` biểu diễn đường dẫn đến một node hoặc thuộc tính trong một hệ thống phân cấp các node. Kiểu này được thiết kế để truyền hiệu quả vào nhiều phương thức dựng sẵn (chẳng hạn như :ref:`Node.get_node()<class_Node_method_get_node>`, :ref:`Object.set_indexed()<class_Object_method_set_indexed>`, :ref:`Tween.tween_property()<class_Tween_method_tween_property>`, v.v.) mà không phụ thuộc cứng vào node hoặc thuộc tính mà chúng trỏ đến.

Đường dẫn node được biểu diễn dưới dạng một :ref:`String<class_String>` bao gồm các tên node phân tách bằng dấu gạch chéo (``/``) và các tên thuộc tính phân tách bằng dấu hai chấm (``:``) (còn được gọi là "subname"). Tương tự đường dẫn hệ thống tệp, ``".."`` và ``"."`` là các tên node đặc biệt. Chúng lần lượt tham chiếu đến node cha và node hiện tại.

Các ví dụ sau là những đường dẫn tương đối so với node hiện tại:

::

    ^"A"     # Trỏ đến node con trực tiếp A.
    ^"A/B"   # Trỏ đến node con B của A.
    ^"."     # Trỏ đến node hiện tại.
    ^".."    # Trỏ đến node cha.
    ^"../C"  # Trỏ đến node anh em C.
    ^"../.." # Trỏ đến node ông bà.

Dấu gạch chéo ở đầu có nghĩa là đường dẫn là tuyệt đối và bắt đầu từ :ref:`SceneTree<class_SceneTree>`:

::

    ^"/root"            # Trỏ đến Window gốc của SceneTree.
    ^"/root/Title"      # Có thể trỏ đến node gốc của scene chính có tên là "Title".
    ^"/root/Global"     # Có thể trỏ đến node hoặc scene autoload có tên là "Global".

Mặc dù có tên như vậy, đường dẫn node cũng có thể trỏ đến một thuộc tính:

::

    ^":position"           # Trỏ đến vị trí của đối tượng này.
    ^":position:x"         # Trỏ đến vị trí của đối tượng này trên trục x.
    ^"Camera3D:rotation:y" # Trỏ đến Camera3D con và phép xoay y của nó.
    ^"/root:size:x"        # Trỏ đến Window gốc và chiều rộng của nó.

Trong một số tình huống, có thể bỏ qua ``:`` ở đầu khi trỏ đến thuộc tính của một đối tượng. Ví dụ, trường hợp này xảy ra với :ref:`Object.set_indexed()<class_Object_method_set_indexed>` và :ref:`Tween.tween_property()<class_Tween_method_tween_property>`, vì các phương thức đó gọi :ref:`get_as_property_path()<class_NodePath_method_get_as_property_path>` ở bên dưới. Tuy nhiên, nhìn chung nên giữ tiền tố ``:``.

Đường dẫn node không thể kiểm tra xem chúng có hợp lệ hay không và có thể trỏ đến các node hoặc thuộc tính không tồn tại. Ý nghĩa của chúng hoàn toàn phụ thuộc vào ngữ cảnh sử dụng.

Thông thường bạn không cần lo lắng về kiểu **NodePath**, vì các chuỗi sẽ được tự động chuyển đổi sang kiểu này khi cần. Tuy vậy, vẫn có những lúc việc định nghĩa đường dẫn node rất hữu ích. Ví dụ, các thuộc tính **NodePath** được export cho phép bạn dễ dàng chọn bất kỳ node nào trong scene đang được chỉnh sửa. Chúng cũng được tự động cập nhật khi di chuyển, đổi tên hoặc xóa node trong trình chỉnh sửa cây scene. Xem thêm :ref:`@GDScript.@export_node_path<class_@GDScript_annotation_@export_node_path>`.

Xem thêm :ref:`StringName<class_StringName>`, một kiểu tương tự được thiết kế cho các chuỗi được tối ưu hóa.

\ **Lưu ý:** Trong ngữ cảnh boolean, **NodePath** sẽ được đánh giá là ``false`` nếu nó rỗng (``NodePath("")``). Nếu không, **NodePath** luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Tutorials
---------

- `2D Role Playing Game (RPG) Demo <https://godotengine.org/asset-library/asset/2729>`__

.. rst-class:: classref-reftable-group

Constructors
------------

.. table::
   :widths: auto

   +---------------------------------+----------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`NodePath<class_NodePath_constructor_NodePath>`\ (\ )                                         |
   +---------------------------------+----------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`NodePath<class_NodePath_constructor_NodePath>`\ (\ from\: :ref:`NodePath<class_NodePath>`\ ) |
   +---------------------------------+----------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`NodePath<class_NodePath_constructor_NodePath>`\ (\ from\: :ref:`String<class_String>`\ )     |
   +---------------------------------+----------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`     | :ref:`get_as_property_path<class_NodePath_method_get_as_property_path>`\ (\ ) |const|                                            |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_concatenated_names<class_NodePath_method_get_concatenated_names>`\ (\ ) |const|                                        |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_concatenated_subnames<class_NodePath_method_get_concatenated_subnames>`\ (\ ) |const|                                  |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_name<class_NodePath_method_get_name>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                       |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_name_count<class_NodePath_method_get_name_count>`\ (\ ) |const|                                                        |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_subname<class_NodePath_method_get_subname>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                 |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_subname_count<class_NodePath_method_get_subname_count>`\ (\ ) |const|                                                  |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`hash<class_NodePath_method_hash>`\ (\ ) |const|                                                                            |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_absolute<class_NodePath_method_is_absolute>`\ (\ ) |const|                                                              |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_empty<class_NodePath_method_is_empty>`\ (\ ) |const|                                                                    |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`     | :ref:`slice<class_NodePath_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Operators
---------

.. table::
   :widths: auto

   +-------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator !=<class_NodePath_operator_neq_NodePath>`\ (\ right\: :ref:`NodePath<class_NodePath>`\ ) |
   +-------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator ==<class_NodePath_operator_eq_NodePath>`\ (\ right\: :ref:`NodePath<class_NodePath>`\ )  |
   +-------------------------+---------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Constructor
-----------------

.. _class_NodePath_constructor_NodePath:

.. rst-class:: classref-constructor

:ref:`NodePath<class_NodePath>` **NodePath**\ (\ ) :ref:`🔗<class_NodePath_constructor_NodePath>`

Tạo một **NodePath** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`NodePath<class_NodePath>` **NodePath**\ (\ from\: :ref:`NodePath<class_NodePath>`\ )

Tạo một **NodePath** dưới dạng bản sao của **NodePath** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`NodePath<class_NodePath>` **NodePath**\ (\ from\: :ref:`String<class_String>`\ )

Tạo một **NodePath** từ :ref:`String<class_String>`. Đường dẫn được tạo là tuyệt đối nếu có tiền tố là dấu gạch chéo (xem :ref:`is_absolute()<class_NodePath_method_is_absolute>`).

Các "subname" được thêm tùy chọn sau đường dẫn đến node đích có thể trỏ đến các thuộc tính và cũng có thể được lồng vào nhau.

Các chuỗi sau có thể là những đường dẫn node hợp lệ:

::

    # Trỏ đến node Sprite2D.
    "Level/RigidBody2D/Sprite2D"

    # Trỏ đến node Sprite2D và resource "texture" của nó.
    # get_node() sẽ lấy Sprite2D, còn get_node_and_resource()
    # sẽ lấy cả node Sprite2D và resource "texture".
    "Level/RigidBody2D/Sprite2D:texture"

    # Trỏ đến node Sprite2D và thuộc tính "position" của nó.
    "Level/RigidBody2D/Sprite2D:position"

    # Trỏ đến node Sprite2D và thành phần "x" của thuộc tính "position" của nó.
    "Level/RigidBody2D/Sprite2D:position:x"

    # Trỏ đến node RigidBody2D dưới dạng đường dẫn tuyệt đối bắt đầu từ SceneTree.
    "/root/Level/RigidBody2D"

\ **Lưu ý:** Trong GDScript, cũng có thể chuyển đổi một chuỗi hằng thành đường dẫn node bằng cách thêm tiền tố ``^`` vào chuỗi. ``^"path/to/node"`` tương đương với ``NodePath("path/to/node")``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_NodePath_method_get_as_property_path:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_as_property_path**\ (\ ) |const| :ref:`🔗<class_NodePath_method_get_as_property_path>`

Trả về một bản sao của đường dẫn node này với ký tự dấu hai chấm (``:``) được thêm vào trước, chuyển đổi nó thành một đường dẫn thuộc tính thuần túy không có tên node (tương đối so với node hiện tại).


.. tabs::

 .. code-tab:: gdscript

    # node_path trỏ đến thuộc tính "x" của node con có tên là "position".
    var node_path = ^"position:x"

    # property_path trỏ đến "position" trên trục "x" của node này.
    var property_path = node_path.get_as_property_path()
    print(property_path) # In ra ":position:x"

 .. code-tab:: csharp

    // nodePath trỏ đến thuộc tính "x" của node con có tên là "position".
    var nodePath = new NodePath("position:x");

    // propertyPath trỏ đến "position" trên trục "x" của node này.
    NodePath propertyPath = nodePath.GetAsPropertyPath();
    GD.Print(propertyPath); // In ra ":position:x"



.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_get_concatenated_names:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_concatenated_names**\ (\ ) |const| :ref:`🔗<class_NodePath_method_get_concatenated_names>`

Trả về tất cả tên node được nối bằng một ký tự gạch chéo (``/``) dưới dạng một :ref:`StringName<class_StringName>` duy nhất.

.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_get_concatenated_subnames:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_concatenated_subnames**\ (\ ) |const| :ref:`🔗<class_NodePath_method_get_concatenated_subnames>`

Trả về tất cả subname thuộc tính được nối bằng một ký tự dấu hai chấm (``:``) dưới dạng một :ref:`StringName<class_StringName>` duy nhất.


.. tabs::

 .. code-tab:: gdscript

    var node_path = ^"Sprite2D:texture:resource_name"
    print(node_path.get_concatenated_subnames()) # In ra "texture:resource_name"

 .. code-tab:: csharp

    var nodePath = new NodePath("Sprite2D:texture:resource_name");
    GD.Print(nodePath.GetConcatenatedSubnames()); // In ra "texture:resource_name"



.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_get_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_name**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NodePath_method_get_name>`

Trả về tên node được chỉ định bởi ``idx``, bắt đầu từ 0. Nếu ``idx`` nằm ngoài phạm vi, một lỗi sẽ được tạo ra. Xem thêm :ref:`get_subname_count()<class_NodePath_method_get_subname_count>` và :ref:`get_name_count()<class_NodePath_method_get_name_count>`.


.. tabs::

 .. code-tab:: gdscript

    var sprite_path = NodePath("../RigidBody2D/Sprite2D")
    print(sprite_path.get_name(0)) # In ra ".."
    print(sprite_path.get_name(1)) # In ra "RigidBody2D"
    print(sprite_path.get_name(2)) # In ra "Sprite"

 .. code-tab:: csharp

    var spritePath = new NodePath("../RigidBody2D/Sprite2D");
    GD.Print(spritePath.GetName(0)); // In ra ".."
    GD.Print(spritePath.GetName(1)); // In ra "PathFollow2D"
    GD.Print(spritePath.GetName(2)); // In ra "Sprite"



.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_get_name_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_name_count**\ (\ ) |const| :ref:`🔗<class_NodePath_method_get_name_count>`

Trả về số lượng tên node trong đường dẫn. Các subname thuộc tính không được tính.

Ví dụ, ``"../RigidBody2D/Sprite2D:texture"`` chứa 3 tên node.

.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_get_subname:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_subname**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NodePath_method_get_subname>`

Trả về tên thuộc tính được chỉ định bởi ``idx``, bắt đầu từ 0. Nếu ``idx`` nằm ngoài phạm vi, một lỗi sẽ được tạo ra. Xem thêm :ref:`get_subname_count()<class_NodePath_method_get_subname_count>`.


.. tabs::

 .. code-tab:: gdscript

    var path_to_name = NodePath("Sprite2D:texture:resource_name")
    print(path_to_name.get_subname(0)) # In ra "texture"
    print(path_to_name.get_subname(1)) # In ra "resource_name"

 .. code-tab:: csharp

    var pathToName = new NodePath("Sprite2D:texture:resource_name");
    GD.Print(pathToName.GetSubname(0)); // In ra "texture"
    GD.Print(pathToName.GetSubname(1)); // In ra "resource_name"



.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_get_subname_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_subname_count**\ (\ ) |const| :ref:`🔗<class_NodePath_method_get_subname_count>`

Trả về số lượng tên thuộc tính ("subname") trong đường dẫn. Mỗi subname trong đường dẫn node được liệt kê sau một ký tự dấu hai chấm (``:``).

Ví dụ, ``"Level/RigidBody2D/Sprite2D:texture:resource_name"`` chứa 2 subname.

.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_hash:

.. rst-class:: classref-method

:ref:`int<class_int>` **hash**\ (\ ) |const| :ref:`🔗<class_NodePath_method_hash>`

Trả về giá trị hash 32-bit đại diện cho nội dung của đường dẫn node.

\ **Lưu ý:** Các đường dẫn node có giá trị hash bằng nhau *không* được đảm bảo là giống nhau do xảy ra va chạm hash. Các đường dẫn node có giá trị hash khác nhau được đảm bảo là khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_is_absolute:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_absolute**\ (\ ) |const| :ref:`🔗<class_NodePath_method_is_absolute>`

Trả về ``true`` nếu đường dẫn node là tuyệt đối. Không giống đường dẫn tương đối, đường dẫn tuyệt đối được biểu diễn bằng một ký tự gạch chéo ở đầu (``/``) và luôn bắt đầu từ :ref:`SceneTree<class_SceneTree>`. Có thể dùng nó để truy cập đáng tin cậy các node từ node gốc (ví dụ: ``"/root/Global"`` nếu tồn tại một autoload có tên "Global").

.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_NodePath_method_is_empty>`

Trả về ``true`` nếu đường dẫn node được tạo từ một :ref:`String<class_String>` rỗng (``""``).

.. rst-class:: classref-item-separator

----

.. _class_NodePath_method_slice:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| :ref:`🔗<class_NodePath_method_slice>`

Trả về phần lát cắt của **NodePath**, từ ``begin`` (bao gồm) đến ``end`` (không bao gồm), dưới dạng một **NodePath** mới.

Giá trị tuyệt đối của ``begin`` và ``end`` sẽ được giới hạn ở tổng của :ref:`get_name_count()<class_NodePath_method_get_name_count>` và :ref:`get_subname_count()<class_NodePath_method_get_subname_count>`, vì vậy giá trị mặc định của ``end`` khiến nó mặc định cắt đến cuối **NodePath** (tức là ``path.slice(1)`` là cách viết tắt của ``path.slice(1, path.get_name_count() + path.get_subname_count())``).

Nếu ``begin`` hoặc ``end`` là số âm, chúng sẽ được tính tương đối từ cuối **NodePath** (tức là ``path.slice(0, -2)`` là cách viết tắt của ``path.slice(0, path.get_name_count() + path.get_subname_count() - 2)``).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_NodePath_operator_neq_NodePath:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`NodePath<class_NodePath>`\ ) :ref:`🔗<class_NodePath_operator_neq_NodePath>`

Trả về ``true`` nếu hai node path không bằng nhau.

.. rst-class:: classref-item-separator

----

.. _class_NodePath_operator_eq_NodePath:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`NodePath<class_NodePath>`\ ) :ref:`🔗<class_NodePath_operator_eq_NodePath>`

Trả về ``true`` nếu hai node path bằng nhau, nghĩa là chúng được tạo thành từ cùng các tên node và tên node con theo cùng một thứ tự.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
