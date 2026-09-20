.. _doc_javaclasswrapper_and_androidruntimeplugin:

Tích hợp với các API Android
============================

Nền tảng Android có rất nhiều API, cùng một hệ sinh thái phong phú gồm các thư viện bên thứ ba với nhiều chức năng đa dạng, chẳng hạn như thông báo đẩy, phân tích, xác thực, quảng cáo, v.v...

Những tính năng này không phù hợp để tích hợp trực tiếp vào lõi Godot, vì vậy từ lâu Godot đã cung cấp một :ref:`Android plugin system <doc_android_plugin>`. :ref:`Android plugin system <doc_android_plugin>` cho phép các nhà phát triển tạo plugin Android cho Godot bằng mã Java hoặc Kotlin, cung cấp giao diện để truy cập và sử dụng các API Android hoặc thư viện bên thứ ba trong dự án Godot từ GDScript, C# hoặc GDExtension.

.. code-block:: kotlin

    class MyAndroidSingleton(godot: Godot?) : GodotPlugin(godot) {
	    @UsedByGodot
	    fun doSomething(value: String) {
		    // ...
	    }
    }


Tuy nhiên, việc viết một plugin Android đòi hỏi kiến thức về mã Java hoặc Kotlin, điều mà hầu hết nhà phát triển Godot không có. Vì vậy, có rất nhiều API Android và thư viện bên thứ ba không có plugin Godot để các nhà phát triển có thể tương tác. Trên thực tế, đây là một trong những lý do chính được các nhà phát triển đưa ra khi không thể chuyển sang Godot từ các game engine khác.

Để giải quyết vấn đề này, chúng tôi đã giới thiệu một vài công cụ trong **Godot 4.4** nhằm đơn giản hóa quy trình truy cập các API Android và thư viện bên thứ ba cho các nhà phát triển.

JavaClassWrapper (Godot singleton)
----------------------------------

``JavaClassWrapper`` là một :ref:`Godot singleton <class_JavaClassWrapper>` cho phép tạo các instance của lớp Java / Kotlin, triển khai các interface Java / Kotlin và gọi các phương thức của chúng chỉ bằng GDScript, C# hoặc GDExtension.

.. code-block:: gdscript

    var LocalDateTime = JavaClassWrapper.wrap("java.time.LocalDateTime")
    var DateTimeFormatter = JavaClassWrapper.wrap("java.time.format.DateTimeFormatter")

    var datetime = LocalDateTime.now()
    var formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")

    print(datetime.format(formatter))

Trong đoạn mã phía trên, ``JavaClassWrapper`` được sử dụng từ GDScript để truy cập các lớp Java ``LocalDateTime`` và ``DateTimeFormatter``. Thông qua ``JavaClassWrapper``, chúng ta có thể gọi trực tiếp các phương thức của lớp Java từ GDScript như thể chúng là các phương thức GDScript.

.. code-block:: gdscript

    class PrintProxy:
        func println(content: String) -> void:
            print(content)

    var print_proxy = PrintProxy.new()
    var printer_object = JavaClassWrapper.create_proxy(print_proxy, ["android.util.Printer"])
    printer_object.println("Hello Godot World!")

Trong đoạn mã phía trên, ``JavaClassWrapper`` được sử dụng để triển khai interface Java ``android.util.Printer`` từ GDScript bằng cách sử dụng một :ref:`Object<class_Object>` làm phần triển khai. Sau đó, proxy được khởi tạo có thể được truyền vào các phương thức Java nhận tham số ``android.util.Printer``.

Hãy xem :ref:`JavaClassWrapper documentation <class_JavaClassWrapper>` để tìm hiểu thêm về API của nó.

Plugin AndroidRuntime
---------------------

``JavaClassWrapper`` rất hữu ích, nhưng để thực hiện nhiều tác vụ trên Android, bạn cần truy cập vào nhiều đối tượng lifecycle / runtime khác nhau của Android. Plugin ``AndroidRuntime`` là một `built-in Godot Android plugin <https://javadoc.io/doc/org.godotengine/godot/latest/org/godotengine/godot/plugin/AndroidRuntimePlugin.html>`_ cho phép bạn thực hiện việc này.

Việc kết hợp plugin ``JavaClassWrapper`` và ``AndroidRuntime`` cho phép các nhà phát triển truy cập và sử dụng các API Android mà không cần rời khỏi GDScript hoặc sử dụng bất kỳ công cụ nào ngoài chính Godot. Điều này **rất quan trọng** đối với việc áp dụng Godot để phát triển Android:

- Nếu bạn cần thực hiện một việc đơn giản hoặc chỉ sử dụng một phần nhỏ của thư viện bên thứ ba, bạn không cần phải tạo plugin - Cho phép các nhà phát triển nhanh chóng tích hợp chức năng Android - Cho phép các nhà phát triển tạo addon Godot chỉ bằng GDScript và ``JavaClassWrapper`` (không cần Java hoặc Kotlin)

.. note::

    Đối với các bản export sử dụng ``gradle``, Godot sẽ tự động đưa vào các tệp ``.jar`` hoặc ``.aar`` mà nó tìm thấy trong thư mục ``addons`` của dự án. Vì vậy, để sử dụng một thư viện bên thứ ba, bạn chỉ cần thả tệp ``.jar`` hoặc ``.aar`` của thư viện đó vào thư mục ``addons``, rồi gọi trực tiếp phương thức của nó từ GDScript bằng ``JavaClassWrapper``.

Ví dụ: Hiển thị Android toast
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: gdscript

    # Lấy singleton AndroidRuntime.
    var android_runtime = Engine.get_singleton("AndroidRuntime")
    if android_runtime:
        # Lấy instance Android Activity.
        var activity = android_runtime.getActivity()

        # Tạo một Godot Callable để bọc logic hiển thị toast.
        var toast_callable = func():
            # Sử dụng JavaClassWrapper để lấy lớp android.widget.Toast, sau đó tạo và hiển thị toast bằng các API của lớp này.
            var ToastClass = JavaClassWrapper.wrap("android.widget.Toast")
            ToastClass.makeText(activity, "This is a test", ToastClass.LENGTH_LONG).show()

        # Bọc Callable trong một Java Runnable và chạy nó trên luồng UI của Android để hiển thị toast.
        activity.runOnUiThread(android_runtime.createRunnableFromGodotCallable(toast_callable))

Ví dụ: Làm rung thiết bị
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: gdscript

    # Lấy singleton AndroidRuntime.
    var android_runtime = Engine.get_singleton("AndroidRuntime")
    if android_runtime:
        # Lấy system service Android Vibrator và kiểm tra xem thiết bị có hỗ trợ hay không.
        var vibrator_service = android_runtime.getApplicationContext().getSystemService("vibrator")
        if vibrator_service and vibrator_service.hasVibrator():
            # Cấu hình và chạy một VibrationEffect.
            var VibrationEffect = JavaClassWrapper.wrap("android.os.VibrationEffect")
            var effect = VibrationEffect.createOneShot(500, VibrationEffect.DEFAULT_AMPLITUDE)
            vibrator_service.vibrate(effect)

Ví dụ: Truy cập các lớp bên trong
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể truy cập các lớp bên trong của Java bằng dấu ``Có thể truy cập các lớp bên trong của Java bằng dấu`` :

.. code-block:: gdscript

    # Truy cập lớp 'VERSION', là một lớp bên trong của lớp 'android.os.Build'.
    var version = JavaClassWrapper.wrap("android.os.Build$VERSION")
    var sdk_int = version.SDK_INT
    if sdk_int == 30:
        # Thực hiện một thao tác cụ thể trên các thiết bị android 11.
    else:
        # Tất cả thiết bị khác

Ví dụ: Gọi constructor
~~~~~~~~~~~~~~~~~~~~~~

Một constructor được gọi bằng cách gọi một phương thức có cùng tên với lớp.

Ví dụ này tạo một intent để gửi văn bản:

.. code-block:: gdscript

    # Lấy singleton AndroidRuntime.
    var android_runtime = Engine.get_singleton("AndroidRuntime")
    if android_runtime:
        var Intent = JavaClassWrapper.wrap("android.content.Intent")
        var activity = android_runtime.getActivity()
        var intent = Intent.Intent() # Gọi constructor.
        intent.setAction(Intent.ACTION_SEND)
        intent.putExtra(Intent.EXTRA_TEXT, "This is a test message.")
        intent.setType("text/plain")
        activity.startActivity(intent)

Ví dụ: Lưu hình ảnh vào thư viện Android
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: gdscript

    # Lấy singleton AndroidRuntime.
    var android_runtime = Engine.get_singleton("AndroidRuntime")
    if android_runtime:
        var Intent = JavaClassWrapper.wrap("android.content.Intent")
        var activity = android_runtime.getActivity()
        var intent = Intent.Intent()

        # Tạo File và Uri.
        var Uri = JavaClassWrapper.wrap("android.net.Uri")
        var File = JavaClassWrapper.wrap("java.io.File")
        var file = File.File(file_path_to_image_here)
        var uri = Uri.fromFile(file)

        # Thiết lập Action và Data của Intent.
        intent.setAction(Intent.ACTION_MEDIA_SCANNER_SCAN_FILE)
        intent.setData(uri)

        # Broadcast nó.
        activity.sendBroadcast(intent)
