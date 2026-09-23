.. _doc_one-click_deploy:

Triển khai bằng một cú nhấp
===========================

Triển khai bằng một cú nhấp là gì?
----------------------------------

Triển khai bằng một cú nhấp là một tính năng khả dụng sau khi một platform được cấu hình đúng cách và một thiết bị được hỗ trợ được kết nối với máy tính. Vì có nhiều cấp độ có thể xảy ra sự cố (platform có thể chưa được cấu hình đúng, SDK có thể được cài đặt không chính xác, thiết bị có thể được cấu hình không đúng, v.v.), nên việc cho người dùng biết tính năng này tồn tại là điều hữu ích.

Sau khi thêm một Android export preset được đánh dấu là Runnable, Godot có thể phát hiện khi một thiết bị USB được kết nối với máy tính và đề xuất tự động export, install và run project (ở debug mode) trên thiết bị. Tính năng này được gọi là *triển khai bằng một cú nhấp*.

.. note::

   Triển khai bằng một cú nhấp chỉ khả dụng sau khi bạn đã thêm một export template được đánh dấu là **Runnable** trong hộp thoại Export. Bạn có thể đánh dấu nhiều export preset là runnable, nhưng mỗi platform chỉ có thể có một preset được đánh dấu là runnable. Nếu bạn đánh dấu preset thứ hai trong một platform nhất định là runnable, preset còn lại sẽ không còn được đánh dấu là runnable.

Các platform được hỗ trợ
------------------------

- **Android:** Export project với debugging được bật và chạy project trên thiết bị đã kết nối.

   - Hãy đảm bảo làm theo các bước được mô tả trong :ref:`doc_exporting_for_android`. Nếu không, nút triển khai bằng một cú nhấp sẽ không xuất hiện.

   - Nếu bạn có nhiều hơn một thiết bị được kết nối, Godot sẽ hỏi bạn muốn export project sang thiết bị nào.

- **iOS:** Export project với debugging được bật và chạy project trên thiết bị đã kết nối.

   - Hãy đảm bảo làm theo các bước được mô tả trong :ref:`doc_exporting_for_ios`. Nếu không, nút triển khai bằng một cú nhấp sẽ không xuất hiện.

   - Với mỗi bundle identifier mới, hãy export project, mở project trong Xcode và build ít nhất một lần để tạo provisioning profile mới, hoặc tạo provisioning profile trong dashboard tài khoản Apple Developer.

   - Nếu bạn có nhiều hơn một thiết bị được kết nối, Godot sẽ hỏi bạn muốn export project sang thiết bị nào.

- **Desktop platforms:** Export project với debugging được bật và chạy project trên máy tính từ xa qua SSH.

- **Web:** Khởi động một web server cục bộ và chạy project đã export bằng cách mở trình duyệt web mặc định. Theo mặc định, tính năng này chỉ có thể truy cập trên ``localhost``. Xem :ref:`Troubleshooting <doc_one-click_deploy_troubleshooting_web>` để cho phép các thiết bị từ xa truy cập project đã export.

Sử dụng triển khai bằng một cú nhấp
-----------------------------------

- **Android:**
   - Bật developer mode trên thiết bị di động, sau đó bật USB debugging trong phần cài đặt của thiết bị.
   - Sau khi bật USB debugging, hãy kết nối thiết bị với PC bằng cáp USB.
   - Bạn cũng có thể triển khai bằng một cú nhấp qua wireless ADB thay vì cáp USB. Để thực hiện việc này, cần:
        - Bật wireless debugging trên thiết bị: :menu:`Settings > Developer options > Debugging`
        - Kết nối thiết bị di động và PC vào cùng một mạng Wi-Fi.
        - Nhấp vào :button:`Pair device with pairing code` (có thể truy cập bằng cách nhấn giữ wireless debugging) để hiển thị IP, port và pairing code.
        - Trên PC, nhập command ``adb pair <ip address>:<port>`` và cung cấp pairing code khi được yêu cầu. Nếu không nhận diện được ``adb``, bạn có thể cần thêm thư mục platform-tools của android-sdk vào ``PATH`` hoặc thực thi command này từ thư mục đó.
        - Bạn có thể xác minh thiết bị ADB đã được kết nối thành công bằng cách nhập ``adb devices`` trong terminal.

- **iOS:**
   - Cài đặt Xcode, chấp nhận license của Xcode và đăng nhập bằng tài khoản Apple Developer của bạn.
   - Nếu bạn đang sử dụng Xcode 14 hoặc phiên bản cũ hơn, hãy cài đặt `ios-deploy <https://github.com/ios-control/ios-deploy>`__ và đặt path thành `ios-deploy` trong Editor Settings (xem `Export ⇾ iOS ⇾ iOS Deploy`).
   - Để chạy trên thiết bị:
      - Pair thiết bị di động với máy Mac.
      - Bật developer mode trên thiết bị.
      - Thiết bị có thể được kết nối qua USB hoặc mạng cục bộ.
      - Hãy đảm bảo thiết bị sử dụng cùng mạng cục bộ và một network interface chính xác được chọn trong editor settings (xem `Network ⇾ Debug ⇾ Remote Host`). Theo mặc định, editor chỉ lắng nghe các kết nối `localhost`.
   - Màn hình thiết bị phải được mở khóa.

- **Desktop platforms:**
   - Bật `SSH Remote Deploy` và cấu hình connection settings trong project export setting.

- Hãy đảm bảo có một export preset được đánh dấu là **Runnable** cho platform đích (Android, iOS hoặc Web).
- Nếu mọi thứ được cấu hình chính xác và không có lỗi, các biểu tượng dành riêng cho từng platform sẽ xuất hiện ở góc trên bên phải của editor.
- Nhấp vào nút để export sang platform mong muốn bằng một cú nhấp.

.. image:: img/remote_debug.webp

.. _doc_one-click_deploy_troubleshooting:

Khắc phục sự cố
---------------

Android
~~~~~~~

Nếu bạn không thấy thiết bị trong danh sách thiết bị khi chạy command ``adb devices`` trong terminal, Godot cũng sẽ không hiển thị thiết bị đó. Để giải quyết vấn đề này:

- Kiểm tra xem USB debugging đã được bật *và được cấp quyền trên thiết bị* hay chưa. Hãy thử mở khóa thiết bị và chấp nhận lời nhắc cấp quyền nếu lời nhắc xuất hiện. Nếu không thấy lời nhắc này, chạy ``adb devices`` trên PC sẽ khiến lời nhắc cấp quyền xuất hiện trên thiết bị.
- Hãy thử `thu hồi quyền cấp cho debugging <https://stackoverflow.com/questions/23081263/adb-android-device-unauthorized>`__ trong developer settings của thiết bị, sau đó thực hiện lại các bước.
- Hãy thử sử dụng USB debugging thay vì wireless debugging hoặc ngược lại. Đôi khi một trong hai cách có thể hoạt động tốt hơn cách kia.
- Trên Linux, có thể bạn đang thiếu `udev rules <https://github.com/M0Rf30/android-udev-rules>`__ cần thiết để thiết bị được nhận diện.

.. _doc_one-click_deploy_troubleshooting_web:

Web
~~~

Theo mặc định, web server được editor khởi động chỉ có thể truy cập từ ``localhost``. Điều này có nghĩa là các thiết bị khác trong mạng cục bộ hoặc trên Internet không thể truy cập web server (nếu router đã được thiết lập port forwarding). Cách này được thực hiện vì lý do bảo mật, vì bạn có thể không muốn các thiết bị khác truy cập project đã export trong khi đang kiểm thử. Việc bind vào ``localhost`` cũng ngăn không cho cửa sổ bật lên của firewall xuất hiện khi bạn sử dụng triển khai bằng một cú nhấp cho web platform.

Để máy chủ web cục bộ có thể truy cập được qua mạng cục bộ, bạn cần thay đổi thiết lập trình chỉnh sửa **Export > Web > HTTP Host** thành ``0.0.0.0``. Bạn cũng cần bật **Export > Web > Use TLS** vì SharedArrayBuffer yêu cầu kết nối bảo mật để hoạt động, *trừ khi* kết nối đến ``localhost``. Tuy nhiên, vì các client khác sẽ kết nối đến một thiết bị từ xa, việc sử dụng TLS ở đây là bắt buộc tuyệt đối.

Để máy chủ web cục bộ có thể truy cập được qua Internet, bạn cũng cần chuyển tiếp cổng **Export > Web > HTTP Port** được chỉ định trong Editor Settings (``8060`` theo mặc định) bằng TCP trên router của bạn. Thông thường, bạn thực hiện việc này bằng cách truy cập giao diện web của router rồi thêm quy tắc NAT cho cổng tương ứng. Đối với kết nối IPv6, thay vào đó, bạn nên cho phép cổng này trong tường lửa IPv6 của router. Cũng như đối với các thiết bị trong mạng cục bộ, bạn cần bật **Export > Web > Use TLS**.

.. note::

    Khi bật **Use TLS**, trình duyệt web sẽ hiển thị cảnh báo vì Godot sẽ sử dụng chứng chỉ tự ký tạm thời. Bạn có thể an toàn bỏ qua cảnh báo này bằng cách nhấp vào **Advanced** rồi nhấp vào **Proceed to (address)**.

    Nếu bạn có chứng chỉ SSL/TLS được các trình duyệt tin cậy, bạn có thể chỉ định đường dẫn đến các tệp khóa và chứng chỉ trong **Export > Web > TLS Key** và **Export > Web > TLS Certificate**. Điều này chỉ hoạt động nếu dự án được truy cập thông qua một tên miền thuộc chứng chỉ TLS.

.. warning::

    Khi sử dụng triển khai một cú nhấp chuột trên các dự án khác nhau, có thể dự án được chỉnh sửa trước đó lại đang được hiển thị. Nguyên nhân là bộ nhớ đệm của service worker không được tự động xóa. Xem
    :ref:`doc_exporting_for_web_troubleshooting` để biết hướng dẫn hủy đăng ký service worker; thao tác này sẽ xóa bộ nhớ đệm và giải quyết vấn đề.
