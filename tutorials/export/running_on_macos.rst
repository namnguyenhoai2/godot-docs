.. _doc_running_on_macos:

Chạy ứng dụng Godot trên macOS
==============================

.. seealso::

    Trang này hướng dẫn cách chạy các dự án Godot trên macOS. Nếu bạn chưa export dự án, trước tiên hãy đọc :ref:`doc_exporting_for_macos`.

Theo mặc định, macOS chỉ chạy các ứng dụng đã được ký và notarize.

.. note::

    Khi chạy ứng dụng từ thư mục Downloads hoặc khi ứng dụng vẫn đang trong trạng thái cách ly, Gatekeeper sẽ thực hiện *ngẫu nhiên hóa đường dẫn* như một biện pháp bảo mật. Điều này làm mất khả năng truy cập các đường dẫn tương đối từ ứng dụng, trong khi ứng dụng cần chúng để hoạt động. Để khắc phục vấn đề này, hãy di chuyển ứng dụng vào thư mục ``/Applications``.

    Nhìn chung, các ứng dụng macOS nên tránh phụ thuộc vào các đường dẫn tương đối từ thư mục ứng dụng.

Tùy thuộc vào cách ứng dụng macOS được ký và phân phối, có thể xảy ra các trường hợp sau:

Ứng dụng được ký, notarize và phân phối qua App Store
-----------------------------------------------------

.. note::

    Nhà phát triển ứng dụng cần tham gia Apple Developer Program và cấu hình các tùy chọn signing và notarization trong quá trình export, sau đó tải ứng dụng lên App Store.

Ứng dụng sẽ chạy ngay mà không cần người dùng thực hiện thêm thao tác nào.

Ứng dụng được ký, notarize và phân phối bên ngoài App Store
-----------------------------------------------------------

.. note::

    Nhà phát triển ứng dụng cần tham gia Apple Developer Program và cấu hình các tùy chọn signing và notarization trong quá trình export, sau đó phân phối ứng dụng dưới dạng tệp lưu trữ ".DMG" hoặc ".ZIP".

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ hiển thị:

.. image:: img/signed_and_notarized_0.png

Nhấp vào ``Open`` để khởi động ứng dụng.

Nếu bạn thấy hộp thoại cảnh báo sau, máy Mac của bạn được thiết lập để chỉ cho phép các ứng dụng từ App Store.

.. image:: img/signed_and_notarized_1.png

Để cho phép các ứng dụng của bên thứ ba, hãy mở ``System Preferences``, nhấp vào ``Security & Privacy``, sau đó nhấp vào ``General``, mở khóa các cài đặt và chọn ``App Store and identified developers``.

.. image:: img/sys_pref_0.png

Ứng dụng được ký (bao gồm chữ ký ad-hoc) nhưng chưa được notarize
-----------------------------------------------------------------

.. note::

    Nhà phát triển ứng dụng đã sử dụng chứng chỉ tự ký hoặc signing ad-hoc (hành vi mặc định của Godot đối với dự án đã export).

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ hiển thị:

.. image:: img/signed_0.png

Để chạy ứng dụng này, bạn có thể tạm thời bỏ qua Gatekeeper:

* Hoặc mở ``System Preferences``, nhấp vào ``Security & Privacy``, sau đó nhấp vào ``General`` và nhấp vào ``Open Anyway``.

  .. image:: img/sys_pref_1.png

* Hoặc nhấp chuột phải (Control-click) vào biểu tượng ứng dụng trong cửa sổ Finder và chọn ``Open`` từ menu.

  .. image:: img/signed_1.png

* Sau đó nhấp vào ``Open`` trong hộp thoại xác nhận.

  .. image:: img/signed_2.png

* Nhập mật khẩu nếu được yêu cầu.

Một tùy chọn khác là tắt hoàn toàn Gatekeeper. Lưu ý rằng việc này làm giảm mức độ bảo mật của máy tính, vì cho phép bạn chạy bất kỳ phần mềm nào. Để thực hiện, hãy chạy ``sudo spctl --master-disable`` trong Terminal, nhập mật khẩu, rồi tùy chọn **Anywhere** sẽ khả dụng:

  .. image:: img/macos_allow_from_anywhere.png

Lưu ý rằng Gatekeeper sẽ tự bật lại khi macOS cập nhật.

Ứng dụng chưa được ký, tệp thực thi được linker ký
--------------------------------------------------

.. note::

    Ứng dụng được xây dựng bằng các export template chính thức nhưng chưa được ký.

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ hiển thị:

.. image:: img/linker_signed_1.png

Để chạy ứng dụng này, bạn nên tự xóa thuộc tính tệp mở rộng quarantine:

* Mở ``Terminal.app`` (nhấn :kbd:`Cmd + Space` và nhập ``Terminal``).

* Đi đến thư mục chứa ứng dụng đích.

  Sử dụng lệnh ``cd path_to_the_app_folder``, chẳng hạn như ``cd ~/Downloads/`` nếu ứng dụng nằm trong thư mục ``Downloads``.

* Chạy lệnh ``xattr -dr com.apple.quarantine "Unsigned Game.app"`` (bao gồm dấu ngoặc kép và phần mở rộng ``.app``).

Cả ứng dụng lẫn tệp thực thi đều chưa được ký (chỉ áp dụng cho máy Mac Apple Silicon)
-------------------------------------------------------------------------------------

.. note::

    Ứng dụng được xây dựng bằng các export template tùy chỉnh, biên dịch bằng OSXCross và hoàn toàn chưa được ký.

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ hiển thị:

.. image:: img/unsigned_1.png

Để chạy ứng dụng này, bạn có thể tự ký ad-hoc cho ứng dụng:

* Cài đặt ``Xcode`` dành cho App Store, khởi động ứng dụng và xác nhận cài đặt các công cụ dòng lệnh.

* Mở ``Terminal.app`` (nhấn :kbd:`Cmd + Space` và nhập ``Terminal``).

* Đi đến thư mục chứa ứng dụng đích.

  Sử dụng lệnh ``cd path_to_the_app_folder``, chẳng hạn như ``cd ~/Downloads/`` nếu ứng dụng nằm trong thư mục ``Downloads``.

* Chạy các lệnh sau:

  ``xattr -dr com.apple.quarantine "Unsigned Game.app"`` (bao gồm dấu ngoặc kép và phần mở rộng ".app").

  ``codesign -s - --force --deep "Unsigned Game.app"`` (bao gồm dấu ngoặc kép và phần mở rộng ".app").
