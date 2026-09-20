Gỡ lỗi trên macOS
=================

Gỡ lỗi trình chỉnh sửa Godot
----------------------------

Việc đính kèm trình gỡ lỗi vào tiến trình macOS đã ký yêu cầu entitlement "com.apple.security.get-task-allow", vốn không được bật theo mặc định vì ứng dụng không thể được công chứng nếu entitlement này được bật. Nếu bạn muốn gỡ lỗi bản dựng chính thức của trình chỉnh sửa, bạn nên ký lại bản dựng đó với các entitlement thích hợp.

Tạo một tệp văn bản ``editor.entitlements`` với nội dung sau:

.. code-block:: xml

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
        <dict>
            <key>com.apple.security.cs.allow-dyld-environment-variables</key>
            <true/>
            <key>com.apple.security.cs.allow-jit</key>
            <true/>
            <key>com.apple.security.cs.allow-unsigned-executable-memory</key>
            <true/>
            <key>com.apple.security.cs.disable-executable-page-protection</key>
            <true/>
            <key>com.apple.security.cs.disable-library-validation</key>
            <true/>
            <key>com.apple.security.device.audio-input</key>
            <true/>
            <key>com.apple.security.device.camera</key>
            <true/>
            <key>com.apple.security.get-task-allow</key>
            <true/>
        </dict>
    </plist>

Sau đó, sử dụng lệnh sau để ký lại trình chỉnh sửa:

::

    codesign -s - --deep --force --options=runtime --entitlements ./editor.entitlements ./path/to/Godot.app

Gỡ lỗi dự án đã xuất
--------------------

Để cho phép gỡ lỗi, hãy chọn entitlement ``codesign\debugging`` (``com.apple.security.get-task-allow``) trong quá trình xuất. Khi được chọn, tính năng công chứng không được hỗ trợ và nên bị tắt.
