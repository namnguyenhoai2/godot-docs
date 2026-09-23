.. _doc_what_are_godot_classes:

Áp dụng các nguyên tắc lập trình hướng đối tượng trong Godot
============================================================

Engine cung cấp hai cách chính để tạo các object có thể tái sử dụng: script và scene. Về mặt kỹ thuật, không cách nào trong số này thực sự định nghĩa class ở bên dưới.

Tuy vậy, nhiều best practice khi sử dụng Godot liên quan đến việc áp dụng các nguyên tắc lập trình hướng đối tượng cho các script và scene cấu thành game của bạn. Vì vậy, việc hiểu cách chúng ta có thể xem chúng như các class là rất hữu ích.

Hướng dẫn này giải thích ngắn gọn cách script và scene hoạt động trong phần lõi của engine, giúp bạn hiểu cách chúng hoạt động ở bên dưới.

Cách script hoạt động trong engine
----------------------------------

Engine cung cấp các class tích hợp sẵn như :ref:`Node <class_Node>`. Bạn có thể mở rộng chúng để tạo các kiểu dẫn xuất bằng script.

Về mặt kỹ thuật, các script này không phải là class. Thay vào đó, chúng là các resource cho engine biết chuỗi thao tác khởi tạo cần thực hiện trên một trong các class tích hợp sẵn của engine.

Các class nội bộ của Godot có các method đăng ký dữ liệu của một class với :ref:`ClassDB <class_ClassDB>`. Cơ sở dữ liệu này cung cấp quyền truy cập thông tin về class trong runtime. ``ClassDB`` chứa thông tin về các class như:

- Property.
- Method.
- Hằng số.
- Signal.

``ClassDB`` này là thứ mà các object kiểm tra khi thực hiện một thao tác như truy cập property hoặc gọi method. Nó kiểm tra các bản ghi trong cơ sở dữ liệu và bản ghi của các kiểu cơ sở của object để xem object có hỗ trợ thao tác đó hay không.

Gắn một :ref:`Script <class_Script>` vào object của bạn sẽ mở rộng các method, property và signal có sẵn từ ``ClassDB``.

.. note::

    Ngay cả những script không sử dụng từ khóa ``extends`` cũng ngầm kế thừa từ lớp cơ sở của engine
    :ref:`RefCounted <class_RefCounted>`. Do đó, bạn có thể khởi tạo các script không có từ khóa ``extends`` từ code. Tuy nhiên, vì chúng mở rộng ``RefCounted``, bạn không thể gắn chúng vào một :ref:`Node <class_Node>`.

Scene
-----

Cách scene hoạt động có nhiều điểm tương đồng với class, vì vậy việc xem scene như một class là hợp lý. Scene là các nhóm node có thể tái sử dụng, khởi tạo và kế thừa. Việc tạo một scene tương tự như có một script tạo các node rồi thêm chúng làm node con bằng ``add_child()``.

Chúng ta thường ghép một scene với một node gốc có script sử dụng các node của scene. Vì vậy, script mở rộng scene bằng cách thêm behavior thông qua code mệnh lệnh.

Nội dung của một scene giúp xác định:

- Những node nào có sẵn cho script.
- Cách chúng được tổ chức.
- Cách chúng được khởi tạo.
- Các kết nối signal giữa chúng.

Tại sao tất cả những điều này lại quan trọng đối với việc tổ chức scene? Vì các instance của scene *là* object. Do đó, nhiều nguyên tắc hướng đối tượng áp dụng cho code viết cũng áp dụng cho scene: single responsibility, encapsulation và các nguyên tắc khác.

Scene *luôn là phần mở rộng của script được gắn vào node gốc của nó*, vì vậy bạn có thể xem nó là một phần của class.

Phần lớn các kỹ thuật được giải thích trong loạt bài best practice này đều dựa trên điểm này.
