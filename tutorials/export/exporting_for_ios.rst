.. _doc_exporting_for_ios:

Export cho iOS
==============

.. seealso::

    Trang này mô tả cách export một project Godot sang iOS. Nếu bạn muốn compile các binary của export template từ source thay vào đó, hãy đọc :ref:`doc_compiling_for_ios`.

Sau đây là các bước để load một project Godot trong Xcode. Việc này cho phép bạn build và deploy lên thiết bị iOS, build bản release cho App Store và thực hiện mọi thao tác khác mà bạn thường có thể làm với Xcode.

.. attention::

    Các project được viết bằng C# có thể được export sang iOS kể từ Godot 4.2, nhưng tính năng này vẫn đang ở trạng thái experimental và :ref:`some limitations apply <doc_c_sharp_platforms>`.

Yêu cầu
-------

-  Bạn phải export cho iOS từ một máy tính chạy macOS có cài Xcode. - Tải các export template của Godot. Sử dụng menu Godot: Editor > Manage Export Templates

Export một project Godot sang Xcode
-----------------------------------

Trong Godot editor, mở cửa sổ **Export** từ menu **Project**. Khi cửa sổ Export mở ra, nhấp vào **Add..** và chọn **iOS**.

Các tùy chọn **App Store Team ID** và (Bundle) **Identifier** trong danh mục **Application** là bắt buộc. Để trống chúng sẽ khiến exporter báo lỗi. Bundle ID phải là duy nhất.

.. note::

    Một bundle ID hợp lệ chỉ có thể chứa các ký tự chữ và số, dấu gạch ngang và dấu chấm (``A-Z``, ``a-z``, ``0-9``, ``-`` và ``.``). Apple khuyến nghị sử dụng định dạng reverse-DNS (ví dụ: ``com.example.your-game``) của một domain mà bạn sở hữu, để đảm bảo bundle ID của bạn là duy nhất. Bundle ID không phân biệt chữ hoa chữ thường. Xem `CFBundleIdentifier <https://developer.apple.com/documentation/bundleresources/information-property-list/cfbundleidentifier>`__.

.. note:: | If you encounter an error during export similar to
          | ``JSON text did not start with array or object and option to allow fragments not set`` | thì có thể nguyên nhân là do **App Store Team ID** bị sai định dạng! | The exporter expects a (10 characters long) code like ``ABCDE12XYZ`` and not, e.g., your name as Xcode likes to display in the *Signing & Capabilities* tab. | Bạn có thể tìm thấy mã này tại `developer.apple.com <https://developer.apple.com/account/resources/certificates/list>`_, bên cạnh tên của bạn ở góc trên bên phải.

Sau khi bạn nhấp vào **Export Project**, vẫn còn hai tùy chọn quan trọng:

  * **Path** là một thư mục trống sẽ chứa các file project Xcode đã export. * **File** sẽ là tên của project Xcode cùng một số file và thư mục riêng của project.

.. image:: img/ios_export_file.webp

.. note:: This tutorial uses **exported_xcode_project_name**, but you will use your
          tên của project. Khi thấy **exported_xcode_project_name** trong các bước sau, hãy thay thế bằng tên bạn đã sử dụng.

.. note:: Avoid using spaces when you choose your **exported_xcode_project_name** as
          điều này có thể khiến file project XCode bị hỏng.

Khi quá trình export hoàn tất, thư mục output sẽ có dạng như sau:

.. image:: img/ios_export_output.webp


.. warning::

    iOS simulator chỉ hỗ trợ renderer ``Compatibility``.

    Các máy Mac Apple Silicon có thể chạy ứng dụng iOS native, vì vậy bạn có thể chạy trực tiếp các project iOS đã export trên máy Mac Apple Silicon mà không bị giới hạn của iOS simulator.

Mở **exported_xcode_project_name.xcodeproj** cho phép bạn build và deploy như bất kỳ ứng dụng iOS nào khác.

Các lưu ý khi phát triển chủ động
---------------------------------

Phương pháp trên tạo một project đã export mà bạn có thể build cho bản release, nhưng bạn phải export lại mỗi khi thực hiện thay đổi trong Godot.

Trong quá trình phát triển, bạn có thể tăng tốc quy trình này bằng cách liên kết trực tiếp các file project Godot vào ứng dụng của mình.

Trong ví dụ sau:

  * **exported_xcode_project_name** là tên của ứng dụng iOS đã export (như trên). * **godot_project_to_export** là tên của project Godot.

.. note:: **godot_project_to_export** must not be the same as **exported_xcode_project_name**
          để tránh các vấn đề signing trong Xcode.

Các bước liên kết một thư mục project Godot với Xcode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Bắt đầu từ một project iOS đã export (làm theo các bước ở trên). 2. Trong Finder, kéo thư mục project Godot vào file browser của Xcode.

.. image:: img/ios_export_add_dir.webp

3. Trong hộp thoại, hãy đảm bảo chọn Action: **Reference files in place** và Groups: **Create folders**. Bỏ chọn Targets: **exported_xcode_project_name**.

.. image:: img/ios_export_file_ref.webp

4. Bạn sẽ thấy thư mục **godot_project_to_export** trong file browser của Xcode.

5. Chọn project Godot trong Project navigator. Sau đó, ở phía bên kia của cửa sổ XCode, trong File Inspector, hãy chọn các mục sau:

  * **Location**: Relative to Project * **Build Rules**: Apply Once to Folder * thêm project của bạn vào **Target Membership**

.. image:: img/ios_export_file_inspector.webp

.. image:: img/ios_export_target_membership.webp

7. Xóa **exported_xcode_project_name.pck** khỏi project Xcode trong project navigator.

.. image:: img/ios_export_delete_pck.webp

8. Mở **exported_xcode_project_name-Info.plist** và thêm một string property có tên **godot_path** (đây là tên key thực tế) với giá trị **godot_project_to_export** (đây là tên project của bạn)

.. image:: img/ios_export_set_path.webp

Vậy là xong! Giờ bạn có thể chỉnh sửa project trong Godot editor và build trong Xcode bất cứ khi nào muốn chạy project trên một thiết bị.

Các plugin cho iOS
------------------

Bạn có thể sử dụng các plugin iOS đặc biệt trong Godot. Hãy xem
:ref:`doc_ios_plugin` page.

Các biến môi trường
-------------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập các tùy chọn export bên ngoài editor. Trong quá trình export, chúng sẽ ghi đè các giá trị bạn đã đặt trong export menu.

.. list-table:: iOS export environment variables
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Encryption / Encryption Key
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``
   * - Options / Application / Provisioning Profile UUID Debug
     - ``GODOT_IOS_PROVISIONING_PROFILE_UUID_DEBUG``
   * - Options / Application / Provisioning Profile UUID Release
     - ``GODOT_IOS_PROVISIONING_PROFILE_UUID_RELEASE``

Khắc phục sự cố
---------------

xcode-select trỏ đến vị trí SDK không chính xác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

xcode-select là một công cụ đi kèm với Xcode và, cùng nhiều chức năng khác, dùng để trỏ đến các iOS SDK trên máy Mac của bạn. Nếu bạn đã cài Xcode, mở ứng dụng, đồng ý với thỏa thuận cấp phép và cài đặt các command line tools, xcode-select sẽ trỏ đến đúng vị trí của iPhone SDK. Nếu vì lý do nào đó công cụ không trỏ đúng, Godot sẽ không thể export sang iOS và hiển thị một lỗi có thể trông như sau:

::

    MSB3073: The command ""clang" <LOTS OF PATHS AND COMMAND LINE ARGUMENTS HERE>
    "/Library/Developer/CommandLineTools/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk"" exited with code 1.

Trong trường hợp này, Godot đang cố tìm thư mục ``Platforms`` chứa iPhone SDK bên trong thư mục ``/Library/Developer/CommandLineTools/``, nhưng thư mục ``Platforms`` chứa iPhone SDK thực tế lại nằm dưới ``/Applications/Xcode.app/Contents/Developer``. Để xác minh điều này, bạn có thể mở Terminal và chạy lệnh sau để xem xcode-select đang trỏ đến đâu:

::

    xcode-select -p

Để sửa lỗi xcode-select trỏ đến sai vị trí, hãy nhập lệnh này trong Terminal:

::

    sudo xcode-select -switch /Applications/Xcode.app

Sau khi chạy lệnh này, Godot sẽ có thể export thành công sang iOS.

Các tùy chọn export
-------------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export hiện có trong
:ref:`class_EditorExportPlatformIOS` class reference.
