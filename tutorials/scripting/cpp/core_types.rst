.. _doc_godot_cpp_core_types:

Các hàm và kiểu cốt lõi
=======================

API của godot-cpp được thiết kế để giống với API nội bộ của Godot nhất có thể.

Điều này có nghĩa là nhìn chung, bạn có thể sử dụng phần :ref:`Chi tiết về Engine <doc_engine_architecture>` để tìm hiểu cách làm việc với godot-cpp. Ngoài ra, việc xem qua `mã nguồn của engine <https://github.com/godotengine/godot>`__ thường rất hữu ích để tìm các ví dụ về cách làm việc với API của Godot.

Tuy vậy, có một số khác biệt bạn cần lưu ý, được ghi lại ở đây.

Các hàm và macro thông dụng
---------------------------

Vui lòng tham khảo :ref:`doc_common_engine_methods_and_macros` để biết thông tin về vấn đề này. Các hàm và macro được ghi lại ở đó cũng có trong godot-cpp.

Các kiểu cốt lõi
----------------

:ref:`Các kiểu cốt lõi <doc_core_types>` của Godot cũng có trong godot-cpp và các khuyến nghị tương tự như được mô tả trong bài viết đó cũng được áp dụng. Các kiểu này được đồng bộ thường xuyên với codebase của Godot.

Trong code của riêng bạn, bạn cũng có thể sử dụng `các kiểu STL của C++ <https://en.cppreference.com/w/cpp/container.html>`__, hoặc các kiểu từ bất kỳ thư viện nào bạn chọn, nhưng chúng sẽ không tương thích với các API của Godot.

Mảng packed
~~~~~~~~~~~

Trong Godot, các kiểu ``Packed*Array`` là bí danh của ``Vector``, còn trong godot-cpp, chúng là các kiểu riêng sử dụng các binding của Godot. Lý do là ``Packed*Array`` được expose cho Godot và chỉ giới hạn ở các kiểu của Godot, trong khi ``Vector`` có thể chứa bất kỳ kiểu C++ nào mà Godot có thể không hiểu được.

Nhìn chung, các kiểu ``Packed*Array`` hoạt động giống như các bí danh ``Vector`` tương ứng, tuy nhiên có một số khác biệt đáng chú ý.

Truy cập dữ liệu
++++++++++++++++

``Vector`` giữ dữ liệu hoàn toàn bên trong GDExtension, trong khi các kiểu ``Packed*Array`` giữ dữ liệu ở phía Godot. Điều này có nghĩa là mỗi khi truy cập một ``Packed*Array``, nó cần gọi vào Godot.

Để đọc hoặc ghi hiệu quả một lượng lớn dữ liệu vào ``Packed*Array``, bạn nên gọi ``.ptr()`` (để đọc) hoặc ``.ptrw()`` (để ghi) nhằm lấy trực tiếp con trỏ đến vùng nhớ của mảng:

.. code-block:: cpp

    // TỆ!
    void my_bad_function(const PackedByteArray &p_array) {
        for (int i = 0; i < p_array.size(); i++) {
            // Mỗi lần đoạn này chạy, nó cần gọi vào Godot.
            uint8_t byte = p_array[i];

            // .. thực hiện thao tác nào đó với byte.
        }
    }

    // TỐT :-)
    void my_good_function(const PackedByteArray &p_array) {
        const uint8_t *array_ptr = p_array.ptr();
        for (int i = 0; i < p_array.size(); i++) {
            // Thao tác này truy cập trực tiếp vào vùng nhớ!
            uint8_t byte = array_ptr[i];

            // .. thực hiện thao tác nào đó với byte.
        }
    }

Sao chép
++++++++

Các wrapper ``Variant`` cho ``Packed*Array`` xử lý chúng theo dạng truyền tham chiếu, trong khi bản thân các kiểu ``Packed*Array`` được truyền theo giá trị (được triển khai bằng copy-on-write).

Ngoài ra, bạn cũng nên biết rằng các lệnh gọi GDScript sử dụng interface gọi ``Variant``: mọi đối số ``Packed*Array`` truyền vào các hàm của bạn sẽ được truyền trong một ``Variant``, rồi được unpack từ đó. Việc này có thể tạo ra các bản sao của những kiểu này, vì vậy đối số bạn nhận được có thể là bản sao của đối số được dùng khi gọi hàm. Trên thực tế, điều này có nghĩa là bạn không thể dựa vào việc đối số được truyền cho mình có thể được sửa đổi tại vị trí của bên gọi.

Lớp Variant
-----------

Vui lòng tham khảo :ref:`doc_variant_class` để tìm hiểu cách làm việc với ``Variant``.

Quan trọng nhất, bạn cần biết rằng mọi hàm được expose thông qua API GDExtension đều phải tương thích với ``Variant``.

Lớp Object
----------

Vui lòng tham khảo :ref:`doc_object_class` để tìm hiểu cách đăng ký và làm việc với các kiểu ``Object`` của riêng bạn.

Chúng tôi không biết có khác biệt lớn nào giữa API ``Object`` của godot-cpp và API ``Object`` nội bộ của Godot, ngoại trừ việc một số phương thức có trong API nội bộ của Godot nhưng không có trong godot-cpp.

Bạn cần biết rằng con trỏ đến ``Object`` godot-cpp của bạn khác với con trỏ mà Godot sử dụng nội bộ. Lý do là phiên bản godot-cpp là một instance mở rộng, được cấp phát riêng với ``Object`` ban đầu. Tuy nhiên, trên thực tế, sự khác biệt này thường không đáng kể.
