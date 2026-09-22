.. _doc_handling_compatibility_breakages:

Xử lý các lỗi tương thích
=========================

.. TODO: Elaborate on types of compatibility and procedure.

Bạn đã thêm một tham số mới vào một phương thức, thay đổi kiểu trả về, thay đổi kiểu của một tham số hoặc thay đổi giá trị mặc định của tham số đó, và giờ các bài kiểm thử tự động đang báo lỗi tương thích?

Nên tránh phá vỡ tính tương thích, nhưng khi cần thiết, đã có các cơ chế để xử lý việc này theo cách giúp quá trình chuyển đổi diễn ra suôn sẻ nhất có thể.

Một ví dụ thực tế
-----------------

.. TODO: Add example that showcases more details like original default arguments etc.

Các thay đổi này được lấy từ `pull request #88047 <https://github.com/godotengine/godot/pull/88047>`_, trong đó bổ sung các tùy chọn định tuyến mới cho ``AStarGrid2D`` và các lớp AStar khác. Trong số những thay đổi đó, các phương thức sau đã được chỉnh sửa trong ``core/math/a_star_grid_2d.h``:

.. code-block:: cpp

    Vector<Vector2> get_point_path(const Vector2i &p_from, const Vector2i &p_to);
    TypedArray<Vector2i> get_id_path(const Vector2i &p_from, const Vector2i &p_to);

Thành:

.. code-block:: cpp

    Vector<Vector2> get_point_path(const Vector2i &p_from, const Vector2i &p_to, bool p_allow_partial_path = false);
    TypedArray<Vector2i> get_id_path(const Vector2i &p_from, const Vector2i &p_to, bool p_allow_partial_path = false);

Điều này có nghĩa là phải thêm các liên kết phương thức tương thích mới vào tệp, nằm trong phần ``protected`` của mã, thường được đặt cạnh ``_bind_methods()``:

.. code-block:: cpp

    #ifndef DISABLE_DEPRECATED
        TypedArray<Vector2i> _get_id_path_bind_compat_88047(const Vector2i &p_from, const Vector2i &p_to);
        Vector<Vector2> _get_point_path_bind_compat_88047(const Vector2i &p_from, const Vector2i &p_to);
        static void _bind_compatibility_methods();
    #endif

Chúng phải bắt đầu bằng ``_`` để cho biết rằng chúng là nội bộ và kết thúc bằng ``_bind_compat_`` theo sau là số PR đã giới thiệu thay đổi (``88047`` trong ví dụ này). Các phương thức tương thích này cần được triển khai trong một tệp riêng, như ``core/math/a_star_grid_2d.compat.inc`` trong trường hợp này:

.. code-block:: cpp
    :caption: core/math/a_star_grid_2d.compat.inc

	/**************************************************************************/
	/*  a_star_grid_2d.compat.inc                                             */
	/**************************************************************************/
	/*                         Tệp này là một phần của:                       */
	/*                             GODOT ENGINE                               */
	/*                        https://godotengine.org                         */
	/**************************************************************************/
	/* Bản quyền (c) 2014-hiện tại, các cộng tác viên của Godot Engine (xem AUTHORS.md). */
	/* Bản quyền (c) 2007-2014 Juan Linietsky, Ariel Manzur.                  */
	/*                                                                        */
	/* Theo đây, mọi người được cấp quyền miễn phí để nhận một bản sao của   */
	/* phần mềm này và các tệp tài liệu đi kèm (gọi là "Phần mềm"), được     */
	/* sử dụng Phần mềm không hạn chế, bao gồm không giới hạn quyền sử dụng,  */
	/* sao chép, sửa đổi, hợp nhất, xuất bản, phân phối, cấp phép lại và/hoặc */
	/* bán các bản sao của Phần mềm, cũng như cho phép những người được cung  */
	/* cấp Phần mềm thực hiện các việc đó, theo các điều kiện sau:            */
	/*                                                                        */
	/* Thông báo bản quyền nêu trên và thông báo cho phép này phải được       */
	/* đưa vào tất cả các bản sao hoặc phần đáng kể của Phần mềm.             */
	/*                                                                        */
	/* PHẦN MỀM ĐƯỢC CUNG CẤP "NGUYÊN TRẠNG", KHÔNG CÓ BẤT KỲ BẢO ĐẢM NÀO,  */
	/* DÙ RÕ RÀNG HAY NGỤ Ý, BAO GỒM NHƯNG KHÔNG GIỚI HẠN Ở CÁC BẢO ĐẢM VỀ   */
	/* KHẢ NĂNG THƯƠNG MẠI, SỰ PHÙ HỢP CHO MỘT MỤC ĐÍCH CỤ THỂ VÀ KHÔNG     */
	/* XÂM PHẠM.                                                             */
	/* TRONG MỌI TRƯỜNG HỢP, CÁC TÁC GIẢ HOẶC CHỦ SỞ HỮU BẢN QUYỀN SẼ KHÔNG  */
	/* CHỊU TRÁCH NHIỆM VỀ BẤT KỲ KHIẾU NẠI, THIỆT HẠI HOẶC TRÁCH NHIỆM NÀO  */
	/* KHÁC, DÙ PHÁT SINH TỪ HỢP ĐỒNG, HÀNH VI GÂY THIỆT HẠI HOẶC CÁCH KHÁC, */
	/* PHÁT SINH TỪ, DO HOẶC LIÊN QUAN ĐẾN PHẦN MỀM HOẶC VIỆC SỬ DỤNG HAY    */
	/* CÁC GIAO DỊCH KHÁC ĐỐI VỚI PHẦN MỀM.                                  */
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

Trừ khi thay đổi về tính tương thích phức tạp, phương thức tương thích nên gọi trực tiếp phương thức đã sửa đổi thay vì sao chép phương thức đó. Hãy đảm bảo khớp với các đối số mặc định của phương thức đó (trong ví dụ trên, đây sẽ là ``false``).

Tệp này luôn phải được đặt cạnh tệp gốc và có ``.compat.inc`` ở cuối thay vì ``.cpp`` hoặc ``.h``. Tiếp theo, tệp này cần được include trong tệp ``.cpp`` mà chúng ta đang thêm các phương thức tương thích vào, vì vậy ``core/math/a_star_grid_2d.cpp``:

.. code-block:: cpp
    :caption: core/math/a_star_grid_2d.cpp

    #include "a_star_grid_2d.h"
    #include "a_star_grid_2d.compat.inc"

    #include "core/variant/typed_array.h"

Cuối cùng, các thay đổi API của GDExtension cần được ghi lại. Để thực hiện việc này, trước tiên hãy build Godot trên branch ``master``, sau đó chạy nó với flag ``--dump-extension-api``:

.. code-block:: shell

    git switch master
    scons
    godot --dump-extension-api

Thao tác này sẽ tạo một tệp có tên ``extension_api.json`` trong thư mục hiện tại. Chuyển sang feature branch, build lại Godot, sau đó chạy nó với flag ``--validate-extension-api`` theo sau là đường dẫn đến tệp ``extension_api.json`` vừa tạo:

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

    Nếu bạn nhận được lỗi ``Hash changed`` đối với một phương thức, điều đó có nghĩa là liên kết tương thích bị thiếu hoặc không chính xác. Không nên thêm các dòng như vậy vào tệp validation, mà cần sửa bằng cách liên kết đúng phương thức tương thích. Hãy kiểm tra kỹ những điều sau:

    - Đối với phương thức tương thích (phương thức có tên kết thúc bằng số PR), kiểu, tên và giá trị mặc định của các đối số phải giống hệt phiên bản phương thức trước khi bạn thay đổi.
    - Trong ``_bind_compatibility_methods()``, tên các đối số được cung cấp cho macro ``D_METHOD()`` trong ``ClassDB::bind_compatibility_method()`` phải giống hệt tên trong lời gọi ``ClassDB::bind_method()`` của phương thức gốc.

Thêm các dòng này, kèm theo một chú thích giải thích thay đổi API là gì và đã thực hiện những hành động nào để ngăn lỗi tương thích, vào một tệp validation được đặt tên theo ID pull request trên GitHub và đặt trong thư mục của phiên bản Godot mà thay đổi này sẽ làm mất tính tương thích.

Vì ví dụ này dành cho PR #88047 nên tên tệp sẽ là ``GH-88047.txt``, và vì việc này được thực hiện trong quá trình phát triển 4.3 (tức là thay đổi từ 4.2), tệp sẽ nằm trong thư mục ``misc/extension_api_validation/4.2-stable/``.

Xem bên dưới ví dụ hoàn chỉnh về một tệp như vậy cho PR này:

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

Vậy là xong! Bạn có thể gặp các trường hợp phức tạp hơn một chút, chẳng hạn như sắp xếp lại các đối số, thay đổi kiểu trả về, v.v., nhưng phần này đã trình bày những điều cơ bản về cách sử dụng hệ thống này.

Để biết thêm thông tin, hãy xem `pull request #76446 <https://github.com/godotengine/godot/pull/76446>`_.

.. _`pull request #88047`: https://github.com/godotengine/godot/pull/88047
.. _`pull request #76446`: https://github.com/godotengine/godot/pull/76446
