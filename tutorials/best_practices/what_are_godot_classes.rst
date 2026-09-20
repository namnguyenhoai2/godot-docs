.. _doc_what_are_godot_classes:

Áp dụng các nguyên tắc lập trình hướng đối tượng trong Godot
============================================================

Engine cung cấp hai cách chính để tạo các đối tượng có thể tái sử dụng: scripts và scenes. Về mặt kỹ thuật, không cách nào trong số này thực sự định nghĩa các class ở bên dưới.

Tuy vậy, nhiều best practice khi sử dụng Godot liên quan đến việc áp dụng các nguyên tắc lập trình hướng đối tượng cho scripts và scenes cấu thành game của bạn. Vì vậy, việc hiểu cách chúng ta có thể xem chúng như các class là rất hữu ích.

Hướng dẫn này giải thích ngắn gọn cách scripts và scenes hoạt động trong core của engine, giúp bạn hiểu cách chúng hoạt động ở bên dưới.

Cách scripts hoạt động trong engine
-----------------------------------

Engine cung cấp các class dựng sẵn như :ref:`Node <class_Node>`. Bạn có thể mở rộng chúng để tạo các kiểu dẫn xuất bằng một script.

Về mặt kỹ thuật, các script này không phải là class. Thay vào đó, chúng là các resource cho engine biết một chuỗi thao tác khởi tạo cần thực hiện trên một trong các class dựng sẵn của engine.

Các class nội bộ của Godot có các method đăng ký dữ liệu của một class với :ref:`ClassDB <class_ClassDB>`. Cơ sở dữ liệu này cung cấp quyền truy cập thông tin về class trong runtime. ``ClassDB`` chứa thông tin về các class như:

- Properties. - Methods. - Constants. - Signals.

``ClassDB`` này là nơi các object đối chiếu khi thực hiện một thao tác như truy cập property hoặc gọi method. Nó kiểm tra các bản ghi trong cơ sở dữ liệu và các bản ghi về kiểu cơ sở của object để xem object có hỗ trợ thao tác đó hay không.

Gắn một :ref:`Script <class_Script>` vào object của bạn sẽ mở rộng các method, property và signal có sẵn từ ``ClassDB``.

.. note::

    Ngay cả các script không sử dụng từ khóa ``extends`` cũng ngầm kế thừa từ lớp cơ sở của engine
    :ref:`RefCounted <class_RefCounted>` class. As a result, you can instantiate scripts without the
    từ khóa ``extends`` trong mã nguồn. Tuy nhiên, vì chúng mở rộng ``RefCounted``, bạn không thể gắn chúng vào một :ref:`Node <class_Node>`.

Scenes
------

Hành vi của scenes có nhiều điểm tương đồng với classes, vì vậy việc xem một scene như một class là hợp lý. Scenes là các nhóm node có thể tái sử dụng, khởi tạo instance và kế thừa. Việc tạo một scene tương tự như viết một script tạo các node rồi thêm chúng làm node con bằng ``add_child()``.

Chúng ta thường kết hợp một scene với một node gốc có script, node này sử dụng các node của scene. Do đó, script mở rộng scene bằng cách thêm hành vi thông qua mã mệnh lệnh.

Nội dung của một scene giúp xác định:

- Các node có sẵn cho script. - Cách chúng được tổ chức. - Cách chúng được khởi tạo. - Các kết nối signal mà chúng có với nhau.

Tại sao tất cả những điều này lại quan trọng đối với việc tổ chức scene? Vì các instance của scene *chính là* các object. Do đó, nhiều nguyên tắc hướng đối tượng áp dụng cho code được viết cũng áp dụng cho scenes: single responsibility, encapsulation và các nguyên tắc khác.

Scene *luôn là phần mở rộng của script được gắn vào node gốc của nó*, vì vậy bạn có thể xem nó là một phần của class.

Hầu hết các kỹ thuật được giải thích trong loạt bài best practices này đều dựa trên điểm này.
