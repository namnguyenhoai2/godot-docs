:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Expression.xml.

.. _class_Expression:

Biểu thức
=========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một class lưu trữ một biểu thức mà bạn có thể thực thi.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một biểu thức có thể bao gồm bất kỳ phép toán số học nào, lệnh gọi hàm toán học tích hợp, lệnh gọi method của một instance được truyền vào hoặc lệnh gọi khởi tạo kiểu tích hợp.

Một ví dụ về văn bản biểu thức sử dụng các hàm toán học tích hợp có thể là ``sqrt(pow(3, 2) + pow(4, 2))``.

Trong ví dụ sau, chúng ta sử dụng node :ref:`LineEdit<class_LineEdit>` để viết biểu thức và hiển thị kết quả.


.. tabs::

 .. code-tab:: gdscript

    var expression = Expression.new()

    func _ready():
        $LineEdit.text_submitted.connect(self._on_text_submitted)

    func _on_text_submitted(command):
        var error = expression.parse(command)
        if error != OK:
            print(expression.get_error_text())
            return
        var result = expression.execute()
        if not expression.has_execute_failed():
            $LineEdit.text = str(result)

 .. code-tab:: csharp

    private Expression _expression = new Expression();

    public override void _Ready()
    {
        GetNode<LineEdit>("LineEdit").TextSubmitted += OnTextEntered;
    }

    private void OnTextEntered(string command)
    {
        Error error = _expression.Parse(command);
        if (error != Error.Ok)
        {
            GD.Print(_expression.GetErrorText());
            return;
        }
        Variant result = _expression.Execute();
        if (!_expression.HasExecuteFailed())
        {
            GetNode<LineEdit>("LineEdit").Text = result.ToString();
        }
    }



.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Đánh giá biểu thức <../tutorials/scripting/evaluating_expressions>`

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`         | :ref:`execute<class_Expression_method_execute>`\ (\ inputs\: :ref:`Array<class_Array>` = [], base_instance\: :ref:`Object<class_Object>` = null, show_error\: :ref:`bool<class_bool>` = true, const_calls_only\: :ref:`bool<class_bool>` = false\ ) |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`get_error_text<class_Expression_method_get_error_text>`\ (\ ) |const|                                                                                                                                                                         |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`has_execute_failed<class_Expression_method_has_execute_failed>`\ (\ ) |const|                                                                                                                                                                 |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`parse<class_Expression_method_parse>`\ (\ expression\: :ref:`String<class_String>`, input_names\: :ref:`PackedStringArray<class_PackedStringArray>` = PackedStringArray()\ )                                                                  |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_Expression_method_execute:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **execute**\ (\ inputs\: :ref:`Array<class_Array>` = [], base_instance\: :ref:`Object<class_Object>` = null, show_error\: :ref:`bool<class_bool>` = true, const_calls_only\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Expression_method_execute>`

Thực thi biểu thức đã được phân tích cú pháp trước đó bởi :ref:`parse()<class_Expression_method_parse>` và trả về kết quả. Trước khi sử dụng object được trả về, bạn nên kiểm tra xem method có thất bại hay không bằng cách gọi :ref:`has_execute_failed()<class_Expression_method_has_execute_failed>`.

Nếu bạn đã định nghĩa các biến đầu vào trong :ref:`parse()<class_Expression_method_parse>`, bạn có thể chỉ định giá trị của chúng trong mảng inputs, theo cùng thứ tự.

.. rst-class:: classref-item-separator

----

.. _class_Expression_method_get_error_text:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_error_text**\ (\ ) |const| :ref:`🔗<class_Expression_method_get_error_text>`

Trả về nội dung lỗi nếu :ref:`parse()<class_Expression_method_parse>` hoặc :ref:`execute()<class_Expression_method_execute>` đã thất bại.

.. rst-class:: classref-item-separator

----

.. _class_Expression_method_has_execute_failed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_execute_failed**\ (\ ) |const| :ref:`🔗<class_Expression_method_has_execute_failed>`

Trả về ``true`` nếu :ref:`execute()<class_Expression_method_execute>` đã thất bại.

.. rst-class:: classref-item-separator

----

.. _class_Expression_method_parse:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **parse**\ (\ expression\: :ref:`String<class_String>`, input_names\: :ref:`PackedStringArray<class_PackedStringArray>` = PackedStringArray()\ ) :ref:`🔗<class_Expression_method_parse>`

Phân tích cú pháp biểu thức và trả về mã :ref:`Error<enum_@GlobalScope_Error>`.

Bạn có thể tùy chọn chỉ định tên của các biến có thể xuất hiện trong biểu thức bằng ``input_names``, để có thể liên kết chúng khi biểu thức được thực thi.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
