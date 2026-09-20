.. _doc_running_on_macos:

Chạy ứng dụng Godot trên macOS
==============================

.. seealso::

    Trang này hướng dẫn cách chạy các project Godot trên macOS. Nếu bạn chưa export project, trước tiên hãy đọc :ref:`doc_exporting_for_macos`.

Theo mặc định, macOS chỉ chạy các ứng dụng đã được ký và notarize.

.. note::

    Khi chạy một ứng dụng từ thư mục Downloads hoặc khi ứng dụng vẫn đang trong trạng thái quarantine, Gatekeeper sẽ thực hiện *path randomization* như một biện pháp bảo mật. Điều này khiến ứng dụng không thể truy cập các đường dẫn tương đối, vốn cần thiết để ứng dụng hoạt động. Để giải quyết vấn đề này, hãy chuyển ứng dụng vào thư mục ``/Applications``.

    Nhìn chung, các ứng dụng macOS nên tránh phụ thuộc vào các đường dẫn tương đối từ thư mục ứng dụng.

Tùy thuộc vào cách ứng dụng macOS được ký và phân phối, có thể xảy ra các trường hợp sau:

Ứng dụng được ký, notarize và phân phối qua App Store
-----------------------------------------------------

.. note::

    Nhà phát triển ứng dụng cần tham gia Apple Developer Program và cấu hình các tùy chọn ký và notarize trong quá trình export, sau đó upload ứng dụng lên App Store.

Ứng dụng sẽ chạy ngay mà không cần người dùng tương tác thêm.

Ứng dụng được ký, notarize và phân phối bên ngoài App Store
-----------------------------------------------------------

.. note::

    Nhà phát triển ứng dụng cần tham gia Apple Developer Program và cấu hình các tùy chọn ký và notarize trong quá trình export, sau đó phân phối ứng dụng dưới dạng tệp lưu trữ ".DMG" hoặc ".ZIP".

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ được hiển thị:

.. image:: img/signed_and_notarized_0.png

Nhấp vào ``Open`` để khởi động ứng dụng.

Nếu bạn thấy hộp thoại cảnh báo sau, máy Mac của bạn được thiết lập để chỉ cho phép các ứng dụng từ App Store.

.. image:: img/signed_and_notarized_1.png

Để cho phép các ứng dụng của bên thứ ba, hãy mở ``System Preferences``, nhấp vào ``Security & Privacy``, sau đó nhấp vào ``General``, mở khóa các cài đặt và chọn ``App Store and identified developers``.

.. image:: img/sys_pref_0.png

Ứng dụng được ký (bao gồm chữ ký ad-hoc) nhưng chưa được notarize
-----------------------------------------------------------------

.. note::

    Nhà phát triển ứng dụng đã sử dụng chứng chỉ tự ký hoặc ký ad-hoc (hành vi mặc định của Godot đối với project đã export).

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ được hiển thị:

.. image:: img/signed_0.png

Để chạy ứng dụng này, bạn có thể tạm thời ghi đè Gatekeeper:

* Hoặc mở ``System Preferences``, nhấp vào ``Security & Privacy``, sau đó nhấp vào ``General`` và nhấp vào ``Open Anyway``.

  .. image:: img/sys_pref_1.png

* Hoặc nhấp chuột phải (Control-click) vào biểu tượng ứng dụng trong cửa sổ Finder và chọn ``Open`` từ menu.

  .. image:: img/signed_1.png

* Sau đó nhấp vào ``Open`` trong hộp thoại xác nhận.

  .. image:: img/signed_2.png

* Nhập mật khẩu nếu được yêu cầu.

Một tùy chọn khác là tắt hoàn toàn Gatekeeper. Lưu ý rằng việc này làm giảm độ bảo mật của máy tính, vì cho phép bạn chạy bất kỳ phần mềm nào mình muốn. Để thực hiện việc này, hãy chạy ``sudo spctl --master-disable`` trong Terminal, nhập mật khẩu, sau đó tùy chọn **Anywhere** sẽ khả dụng:

  .. image:: img/macos_allow_from_anywhere.png

Lưu ý rằng Gatekeeper sẽ tự bật lại khi macOS được cập nhật.

Ứng dụng chưa được ký, tệp thực thi được linker ký
--------------------------------------------------

.. note::

    Ứng dụng được build bằng các export template chính thức nhưng chưa được ký.

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ được hiển thị:

.. image:: img/linker_signed_1.png

Để chạy ứng dụng này, bạn nên tự xóa thuộc tính tệp mở rộng quarantine:

* Mở ``Terminal.app`` (nhấn :kbd:`Cmd + Space` và nhập ``Terminal``).

* Điều hướng đến thư mục chứa ứng dụng đích.

  Sử dụng lệnh ``cd path_to_the_app_folder``, chẳng hạn ``cd ~/Downloads/`` nếu ứng dụng nằm trong thư mục ``Downloads``.

* Chạy lệnh ``xattr -dr com.apple.quarantine "Unsigned Game.app"`` (bao gồm dấu ngoặc kép và phần mở rộng ``.app``).

Cả ứng dụng lẫn tệp thực thi đều chưa được ký (chỉ liên quan đến máy Mac Apple Silicon)
---------------------------------------------------------------------------------------

.. note::

    Ứng dụng được build bằng các export template tùy chỉnh, được biên dịch bằng OSXCross và hoàn toàn chưa được ký.

Khi bạn chạy ứng dụng lần đầu, hộp thoại sau sẽ được hiển thị:

.. image:: img/unsigned_1.png

Để chạy ứng dụng này, bạn có thể tự ký ad-hoc cho ứng dụng:

* Cài đặt ``Xcode`` cho App Store, khởi động ứng dụng và xác nhận cài đặt command line tools.

* Mở ``Terminal.app`` (nhấn :kbd:`Cmd + Space` và nhập ``Terminal``).

* Điều hướng đến thư mục chứa ứng dụng đích.

  Sử dụng lệnh ``cd path_to_the_app_folder``, chẳng hạn ``cd ~/Downloads/`` nếu ứng dụng nằm trong thư mục ``Downloads``.

* Chạy các lệnh sau:

  ``xattr -dr com.apple.quarantine "Unsigned Game.app"`` (bao gồm dấu ngoặc kép và phần mở rộng ".app").

  ``codesign -s - --force --deep "Unsigned Game.app"`` (bao gồm dấu ngoặc kép và phần mở rộng ".app").
