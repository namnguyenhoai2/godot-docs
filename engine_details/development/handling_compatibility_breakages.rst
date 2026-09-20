.. _doc_handling_compatibility_breakages:

Xử lý các vấn đề phá vỡ tính tương thích
========================================

.. TODO: Bổ sung chi tiết về các loại tính tương thích và quy trình.

Vậy là bạn đã thêm một tham số mới vào một phương thức, thay đổi kiểu trả về, thay đổi kiểu của một tham số hoặc thay đổi giá trị mặc định của tham số đó, và giờ hệ thống kiểm thử tự động đang báo lỗi về các vấn đề phá vỡ tính tương thích?

Nên tránh phá vỡ tính tương thích, nhưng khi cần thiết, đã có các hệ thống để xử lý việc này theo cách giúp quá trình chuyển đổi diễn ra suôn sẻ nhất có thể.

Một ví dụ thực tế
-----------------

.. TODO: Thêm ví dụ minh họa nhiều chi tiết hơn, chẳng hạn như các đối số mặc định ban đầu, v.v.

Những thay đổi này được lấy từ `pull request #88047 <https://github.com/godotengine/godot/pull/88047>`_, trong đó đã thêm các tùy chọn định tuyến mới vào ``AStarGrid2D`` và các lớp AStar khác. Trong số những thay đổi khác, các phương thức sau đã được sửa đổi trong ``core/math/a_star_grid_2d.h``:

.. code-block:: cpp

    Vector<Vector2> get_point_path(const Vector2i &p_from, const Vector2i &p_to);
    TypedArray<Vector2i> get_id_path(const Vector2i &p_from, const Vector2i &p_to);

Thành:

.. code-block:: cpp

    Vector<Vector2> get_point_path(const Vector2i &p_from, const Vector2i &p_to, bool p_allow_partial_path = false);
    TypedArray<Vector2i> get_id_path(const Vector2i &p_from, const Vector2i &p_to, bool p_allow_partial_path = false);

Điều này có nghĩa là phải thêm các liên kết phương thức tương thích mới vào tệp, nằm trong phần ``protected`` của mã, thường được đặt ngay bên cạnh ``_bind_methods()``:

.. code-block:: cpp

    #ifndef DISABLE_DEPRECATED
        TypedArray<Vector2i> _get_id_path_bind_compat_88047(const Vector2i &p_from, const Vector2i &p_to);
        Vector<Vector2> _get_point_path_bind_compat_88047(const Vector2i &p_from, const Vector2i &p_to);
        static void _bind_compatibility_methods();
    #endif

Chúng phải bắt đầu bằng ``_`` để cho biết rằng chúng là các thành phần nội bộ, và kết thúc bằng ``_bind_compat_`` theo sau là số PR đã giới thiệu thay đổi (``88047`` trong ví dụ này). Các phương thức tương thích này cần được triển khai trong một tệp riêng, chẳng hạn như ``core/math/a_star_grid_2d.compat.inc`` trong trường hợp này:

.. code-block:: cpp
    :caption: core/math/a_star_grid_2d.compat.inc

    /**************************************************************************/
    /*  a_star_grid_2d.compat.inc                                             */
    /**************************************************************************/
    /*                         This file is part of:                          */
    /*                             GODOT ENGINE                               */
    /*                        https://godotengine.org                         */
    /**************************************************************************/
    /* Copyright (c) 2014-present Godot Engine contributors (see AUTHORS.md). */
    /* Copyright (c) 2007-2014 Juan Linietsky, Ariel Manzur.                  */
    /*                                                                        */
    /* Permission is hereby granted, free of charge, to any person obtaining  */
    /* a copy of this software and associated documentation files (the        */
    /* "Software"), to deal in the Software without restriction, including    */
    /* without limitation the rights to use, copy, modify, merge, publish,    */
    /* distribute, sublicense, and/or sell copies of the Software, and to     */
    /* permit persons to whom the Software is furnished to do so, subject to  */
    /* the following conditions:                                              */
    /*                                                                        */
    /* The above copyright notice and this permission notice shall be         */
    /* included in all copies or substantial portions of the Software.        */
    /*                                                                        */
    /* THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,        */
    /* EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF     */
    /* MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. */
    /* IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY   */
    /* CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,   */
    /* TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE      */
    /* SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.                 */
    /**************************************************************************/

    #ifndef DISABLE_DEPRECATED

    #include "core/variant/typed_array.h"

    TypedArray<Vector2i> AStarGrid2D::_get_id_path_bind_compat_88047(const Vector2i &p_from_id, const Vector2i &p_to_id) {
        return get_id_path(p_from_id, p_to_id, false);
    }

    Vector<Vector2> AStarGrid2D::_get_point_path_bind_compat_88047(const Vector2i &p_from_id, const Vector2i &p_to_id) {
        return get_point_path(p_from_id, p_to_id, false);
    }

    void AStarGrid2D::_bind_compatibility_methods() {
        ClassDB::bind_compatibility_method(D_METHOD("get_id_path", "from_id", "to_id"), &AStarGrid2D::_get_id_path_bind_compat_88047);
        ClassDB::bind_compatibility_method(D_METHOD("get_point_path", "from_id", "to_id"), &AStarGrid2D::_get_point_path_bind_compat_88047);
    }

    #endif // DISABLE_DEPRECATED

Trừ khi thay đổi về tính tương thích phức tạp, phương thức tương thích nên gọi trực tiếp phương thức đã sửa đổi thay vì sao chép phương thức đó. Hãy đảm bảo khớp các đối số mặc định của phương thức đó (trong ví dụ trên, giá trị này sẽ là ``false``).

Tệp này luôn phải được đặt cạnh tệp ban đầu và có ``.compat.inc`` ở cuối thay vì ``.cpp`` hoặc ``.h``. Tiếp theo, tệp này cần được đưa vào tệp ``.cpp`` mà chúng ta đang thêm các phương thức tương thích, do đó ``core/math/a_star_grid_2d.cpp``:

.. code-block:: cpp
    :caption: core/math/a_star_grid_2d.cpp

    #include "a_star_grid_2d.h"
    #include "a_star_grid_2d.compat.inc"

    #include "core/variant/typed_array.h"

Cuối cùng, các thay đổi đối với API GDExtension cần được ghi lại. Để thực hiện việc này, trước tiên hãy biên dịch Godot trên nhánh ``master``, sau đó chạy nó với cờ ``--dump-extension-api``:

.. code-block:: shell

    git switch master
    scons
    godot --dump-extension-api

Thao tác này sẽ tạo một tệp có tên ``extension_api.json`` trong thư mục hiện tại của bạn. Chuyển sang nhánh tính năng, biên dịch lại Godot, sau đó chạy nó với cờ ``--validate-extension-api`` theo sau là đường dẫn đến tệp ``extension_api.json`` mà bạn vừa tạo:

.. code-block:: shell

    git switch my-feature-branch
    scons
    godot --validate-extension-api /path/to/extension_api.json

Thao tác này sẽ tạo ra một số dòng bắt đầu bằng ``Validate extension JSON`` như sau:

.. code-block:: text

    Validate extension JSON: Error: Field 'classes/AStar2D/methods/get_id_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStar2D/methods/get_point_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStar3D/methods/get_id_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStar3D/methods/get_point_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStarGrid2D/methods/get_id_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStarGrid2D/methods/get_point_path/arguments': size changed value in new API, from 2 to 3.

.. attention::

    Nếu bạn nhận được lỗi ``Hash changed`` đối với một phương thức, điều đó có nghĩa là liên kết tương thích bị thiếu hoặc không chính xác. Không nên thêm những dòng như vậy vào tệp xác thực; thay vào đó, hãy sửa bằng cách liên kết đúng phương thức tương thích. Hãy đảm bảo kiểm tra kỹ những điều sau:

    - Đối với phương thức tương thích (phương thức có tên kết thúc bằng số PR), kiểu, tên và giá trị mặc định của các đối số phải giống hệt phiên bản phương thức trước khi bạn thay đổi. - Trong ``_bind_compatibility_methods()``, tên các đối số được cung cấp cho macro ``D_METHOD()`` trong ``ClassDB::bind_compatibility_method()`` phải giống hệt tên trong lệnh gọi ``ClassDB::bind_method()`` của phương thức ban đầu.

Thêm các dòng này, kèm theo một chú thích giải thích thay đổi API là gì và các hành động đã thực hiện để ngăn việc phá vỡ tính tương thích, vào một tệp xác thực được đặt tên theo ID pull request trên GitHub và đặt trong thư mục của phiên bản Godot mà thay đổi đó lẽ ra sẽ phá vỡ tính tương thích.

Vì ví dụ này dành cho PR #88047, tên tệp sẽ là ``GH-88047.txt``, và vì việc này được thực hiện trong quá trình phát triển phiên bản 4.3 (do đó thay đổi từ 4.2), tệp sẽ nằm trong thư mục ``misc/extension_api_validation/4.2-stable/``.

Xem bên dưới để biết ví dụ hoàn chỉnh về một tệp như vậy cho PR này:

.. code-block:: text
    :caption: misc/extension_api_validation/4.2-stable/GH-88047.txt

    GH-88047
    --------
    Validate extension JSON: Error: Field 'classes/AStar2D/methods/get_id_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStar2D/methods/get_point_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStar3D/methods/get_id_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStar3D/methods/get_point_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStarGrid2D/methods/get_id_path/arguments': size changed value in new API, from 2 to 3.
    Validate extension JSON: Error: Field 'classes/AStarGrid2D/methods/get_point_path/arguments': size changed value in new API, from 2 to 3.

    Added optional "allow_partial_path" argument to get_id_path and get_point_path methods in AStar classes.
    Compatibility methods registered.

Vậy là xong! Bạn có thể gặp những trường hợp phức tạp hơn một chút, chẳng hạn như sắp xếp lại các đối số, thay đổi kiểu trả về, v.v., nhưng phần này đã trình bày những điều cơ bản về cách sử dụng hệ thống này.

Để biết thêm thông tin, hãy xem `pull request #76446 <https://github.com/godotengine/godot/pull/76446>`_.
