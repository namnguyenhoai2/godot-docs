Debugging trên macOS
====================

Debugging trình soạn thảo Godot
-------------------------------

Việc đính kèm trình gỡ lỗi vào tiến trình macOS đã ký yêu cầu entitlement "com.apple.security.get-task-allow", vốn không được bật theo mặc định vì ứng dụng không thể được notarize khi entitlement này được bật. Nếu bạn muốn debug bản build chính thức của trình soạn thảo, bản build đó cần được ký lại với các entitlement phù hợp.

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

Sau đó, sử dụng lệnh sau để ký lại trình soạn thảo:

::

    codesign -s - --deep --force --options=runtime --entitlements ./editor.entitlements ./path/to/Godot.app

Debugging project đã export
---------------------------

Để cho phép debugging, hãy chọn entitlement ``codesign\debugging`` (``com.apple.security.get-task-allow``) trong quá trình export. Khi được chọn, notarization không được hỗ trợ và nên bị tắt.
