.. _doc_exporting_for_ios:

Xuất cho iOS
============

.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang iOS. Nếu bạn muốn biên dịch các tệp nhị phân export template từ mã nguồn thay vào đó, hãy đọc :ref:`doc_compiling_for_ios`.

Đây là các bước để tải một dự án Godot vào Xcode. Việc này cho phép bạn build và deploy lên thiết bị iOS, build bản phát hành cho App Store và thực hiện mọi việc khác mà bạn thường có thể làm với Xcode.

.. attention::

    Các dự án viết bằng C# có thể được xuất sang iOS kể từ Godot 4.2, nhưng tính năng này đang ở trạng thái thử nghiệm và :ref:`áp dụng một số giới hạn <doc_c_sharp_platforms>`.

Yêu cầu
-------

-  Bạn phải xuất cho iOS từ một máy tính chạy macOS đã cài Xcode.
-  Tải các export template của Godot. Sử dụng menu Godot: Editor > Manage Export Templates

Xuất một dự án Godot sang Xcode
-------------------------------

Trong trình chỉnh sửa Godot, mở cửa sổ **Export** từ menu **Project**. Khi cửa sổ Export mở ra, nhấp vào **Add..** và chọn **iOS**.

Các tùy chọn **App Store Team ID** và (Bundle) **Identifier** trong danh mục **Application** là bắt buộc. Để trống chúng sẽ khiến trình xuất gây ra lỗi. Bundle ID phải là duy nhất.

.. note::

    Bundle ID hợp lệ chỉ có thể chứa các ký tự chữ và số, dấu gạch nối và dấu chấm (``A-Z``, ``a-z``, ``0-9``, ``-`` và ``.``). Apple khuyến nghị sử dụng định dạng reverse-DNS (ví dụ: ``com.example.your-game``) của một miền mà bạn sở hữu, để đảm bảo bundle ID của bạn là duy nhất. Bundle ID không phân biệt chữ hoa chữ thường. Xem `CFBundleIdentifier <https://developer.apple.com/documentation/bundleresources/information-property-list/cfbundleidentifier>`__.

.. note:: | Nếu bạn gặp lỗi trong quá trình xuất tương tự như
          | ``JSON text did not start with array or object and option to allow fragments not set``
          | thì có thể là do **App Store Team ID** không đúng định dạng!
          | Trình xuất yêu cầu một mã (dài 10 ký tự) như ``ABCDE12XYZ`` chứ không phải, chẳng hạn, tên của bạn như cách Xcode hiển thị trong tab *Signing & Capabilities*.
          | Bạn có thể tìm mã này tại `developer.apple.com <https://developer.apple.com/account/resources/certificates/list>`_, bên cạnh tên của bạn ở góc trên bên phải.

Sau khi bạn nhấp vào **Export Project**, vẫn còn hai tùy chọn quan trọng:

  * **Path** là một thư mục trống, nơi sẽ chứa các tệp dự án Xcode đã xuất.
  * **File** sẽ là tên của dự án Xcode cùng một số tệp và thư mục dành riêng cho dự án.

.. image:: img/ios_export_file.webp

.. note:: Hướng dẫn này sử dụng **exported_xcode_project_name**, nhưng bạn sẽ sử dụng tên dự án của mình. Khi thấy **exported_xcode_project_name** trong các bước sau, hãy thay thế bằng tên bạn đã sử dụng.

.. note:: Tránh sử dụng khoảng trắng khi chọn **exported_xcode_project_name** vì điều này có thể dẫn đến hỏng tệp dự án XCode của bạn.

Khi quá trình xuất hoàn tất, thư mục đầu ra sẽ trông như sau:

.. image:: img/ios_export_output.webp


.. warning::

    Trình mô phỏng iOS chỉ hỗ trợ ``Compatibility`` renderer.

    Máy Mac Apple Silicon có thể chạy ứng dụng iOS nguyên bản, vì vậy bạn có thể chạy trực tiếp các dự án iOS đã xuất trên máy Mac Apple Silicon mà không gặp các giới hạn của trình mô phỏng iOS.

Mở **exported_xcode_project_name.xcodeproj** cho phép bạn build và deploy giống như bất kỳ ứng dụng iOS nào khác.

Các lưu ý khi phát triển tích cực
---------------------------------

Phương pháp trên tạo ra một dự án đã xuất mà bạn có thể build để phát hành, nhưng bạn phải xuất lại mỗi khi thực hiện thay đổi trong Godot.

Trong quá trình phát triển, bạn có thể tăng tốc quy trình này bằng cách liên kết trực tiếp các tệp dự án Godot với ứng dụng của mình.

Trong ví dụ sau:

  * **exported_xcode_project_name** là tên của ứng dụng iOS đã xuất (như trên).
  * **godot_project_to_export** là tên của dự án Godot.

.. note:: **godot_project_to_export** không được trùng với **exported_xcode_project_name** để tránh các vấn đề về signing trong Xcode.

Các bước liên kết thư mục dự án Godot với Xcode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Bắt đầu từ một dự án iOS đã xuất (làm theo các bước trên).
2. Trong Finder, kéo thư mục dự án Godot vào trình duyệt tệp của Xcode.

.. image:: img/ios_export_add_dir.webp

3. Trong hộp thoại, hãy đảm bảo chọn Action: **Reference files in place** và Groups: **Create folders**. Bỏ chọn Targets: **exported_xcode_project_name**.

.. image:: img/ios_export_file_ref.webp

4. Xem thư mục **godot_project_to_export** trong trình duyệt tệp của Xcode.

5. Chọn dự án godot trong Project navigator. Sau đó, ở phía bên kia của cửa sổ XCode, trong File Inspector, hãy chọn các mục sau:

  * **Location**: Relative to Project
  * **Build Rules**: Apply Once to Folder
  * thêm dự án của bạn vào **Target Membership**

.. image:: img/ios_export_file_inspector.webp

.. image:: img/ios_export_target_membership.webp

7. Xóa **exported_xcode_project_name.pck** khỏi dự án Xcode trong project navigator.

.. image:: img/ios_export_delete_pck.webp

8. Mở **exported_xcode_project_name-Info.plist** và thêm một thuộc tính chuỗi có tên
**godot_path** (đây là tên key thực tế) với giá trị **godot_project_to_export** (đây là tên dự án của bạn)

.. image:: img/ios_export_set_path.webp

Vậy là xong! Giờ bạn có thể chỉnh sửa dự án trong trình chỉnh sửa Godot và build dự án trong Xcode khi muốn chạy nó trên thiết bị.

Plugin cho iOS
--------------

Bạn có thể sử dụng các plugin iOS đặc biệt trong Godot. Hãy xem
:ref:`doc_ios_plugin` page.

Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè các giá trị bạn đã đặt trong menu export.

.. list-table:: Các biến môi trường export iOS
   :header-rows: 1

   * - Export option
     - Environment variable
   * - Encryption / Encryption Key
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``
   * - Options / Application / Provisioning Profile UUID Debug
     - ``GODOT_IOS_PROVISIONING_PROFILE_UUID_DEBUG``
   * - Options / Application / Provisioning Profile UUID Release
     - ``GODOT_IOS_PROVISIONING_PROFILE_UUID_RELEASE``

Khắc phục sự cố
---------------

xcode-select trỏ đến vị trí SDK không đúng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

xcode-select là một công cụ đi kèm với Xcode và, cùng với những chức năng khác, trỏ đến các SDK iOS trên máy Mac của bạn. Nếu bạn đã cài đặt Xcode, mở Xcode, đồng ý với thỏa thuận cấp phép và cài đặt các công cụ dòng lệnh, xcode-select sẽ trỏ đến đúng vị trí của iPhone SDK. Nếu vì lý do nào đó công cụ này không trỏ đúng, Godot sẽ không thể export sang iOS và hiển thị lỗi có thể giống như sau:

::

    MSB3073: The command ""clang" <LOTS OF PATHS AND COMMAND LINE ARGUMENTS HERE>
    "/Library/Developer/CommandLineTools/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk"" exited with code 1.

Trong trường hợp này, Godot đang cố tìm thư mục ``Platforms`` chứa iPhone SDK bên trong thư mục ``/Library/Developer/CommandLineTools/``, nhưng thư mục ``Platforms`` chứa iPhone SDK thực tế lại nằm dưới ``/Applications/Xcode.app/Contents/Developer``. Để xác minh điều này, bạn có thể mở Terminal và chạy lệnh sau để xem xcode-select đang trỏ đến đâu:

::

    xcode-select -p

Để sửa lỗi xcode-select trỏ đến vị trí không đúng, hãy nhập lệnh này trong Terminal:

::

    sudo xcode-select -switch /Applications/Xcode.app

Sau khi chạy lệnh này, Godot sẽ có thể export sang iOS thành công.

Tùy chọn export
---------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có trong
tài liệu tham khảo lớp :ref:`class_EditorExportPlatformIOS`.

.. _`developer.apple.com`: https://developer.apple.com/account/resources/certificates/list
