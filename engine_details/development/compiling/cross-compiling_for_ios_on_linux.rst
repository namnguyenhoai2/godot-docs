.. _doc_cross-compiling_for_ios_on_linux:

Biên dịch chéo cho iOS trên Linux
=================================

.. highlight:: shell

Quy trình này tương đối phức tạp và yêu cầu thực hiện nhiều bước, nhưng một khi đã cấu hình môi trường đúng cách, bạn có thể biên dịch Godot cho iOS bất cứ khi nào muốn.

Tuyên bố miễn trừ trách nhiệm
-----------------------------

Mặc dù có thể biên dịch cho iOS trong môi trường Linux, Apple rất hạn chế về các công cụ được phép sử dụng (đặc biệt là về phần cứng), gần như chỉ cho phép sử dụng các sản phẩm của họ để phát triển. Vì vậy, đây **không phải là quy trình chính thức**. Tuy nhiên, vào năm 2010, Apple cho biết họ đã nới lỏng một số `App Store review guidelines <https://developer.apple.com/app-store/review/guidelines/>`__ để cho phép sử dụng bất kỳ công cụ nào, miễn là tệp nhị phân tạo ra không tải xuống bất kỳ mã nào, điều đó có nghĩa là việc sử dụng quy trình được mô tả ở đây và biên dịch chéo tệp nhị phân sẽ không có vấn đề gì.

Yêu cầu
-------

- `XCode with the iOS SDK <https://developer.apple.com/download/all/?q=Xcode>`__ (bạn phải đăng nhập vào Apple ID để tải Xcode). - `Clang >= 3.5 <https://clang.llvm.org>`__ cho máy phát triển của bạn, được cài đặt trong ``PATH``. Phiên bản này phải là >= 3.5 để nhắm đến kiến trúc ``arm64``. - `xar <https://mackyle.github.io/xar/>`__ và `pbzx <https://github.com/NiklasRosenstein/pbzx>`__ (cần thiết để giải nén kho lưu trữ ``.xip`` đi kèm với Xcode).

  - Để xây dựng xar và pbzx, bạn có thể làm theo `this guide <https://gist.github.com/phracker/1944ce190e01963c550566b749bd2b54>`__.

- `cctools-port <https://github.com/tpoechtrager/cctools-port>`__ để có các công cụ xây dựng cần thiết. Quy trình xây dựng khá đặc thù và được mô tả bên dưới.

  - Quy trình này cũng có một số dependency bổ sung: automake, autogen, libtool.

Cấu hình môi trường
-------------------

Chuẩn bị SDK
~~~~~~~~~~~~

Giải nén tệp ``.xip`` của Xcode mà bạn đã tải xuống từ trang web dành cho nhà phát triển của Apple:

::

    mkdir xcode
    xar -xf /path/to/Xcode_X.x.xip -C xcode
    pbzx -n Content | cpio -i

    [...]
    ######### Blocks

Lưu ý rằng đối với các lệnh bên dưới, bạn sẽ cần thay thế phiên bản (``x.x``) bằng phiên bản iOS SDK mà bạn đang sử dụng. Nếu không biết phiên bản iPhone SDK của mình, bạn có thể xem tệp JSON bên trong ``Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs``.

Giải nén iOS SDK:

::

    export IOS_SDK_VERSION="x.x"
    mkdir -p iPhoneSDK/iPhoneOS${IOS_SDK_VERSION}.sdk
    cp -r xcode/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/* iPhoneSDK/iPhoneOS${IOS_SDK_VERSION}.sdk
    cp -r xcode/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include/c++/* iPhoneSDK/iPhoneOS${IOS_SDK_VERSION}.sdk/usr/include/c++
    fusermount -u xcode

Đóng gói SDK để cctools có thể sử dụng:

::

    cd iPhoneSDK
    tar -cf - * | xz -9 -c - > iPhoneOS${IOS_SDK_VERSION}.sdk.tar.xz

Toolchain
~~~~~~~~~

Xây dựng cctools:

::

    git clone https://github.com/tpoechtrager/cctools-port.git
    cd cctools-port/usage_examples/ios_toolchain
    ./build.sh /path/iPhoneOS${IOS_SDK_VERSION}.sdk.tar.xz arm64

Sao chép các công cụ vào một vị trí dễ quản lý hơn. Lưu ý rằng các tập lệnh SCons dùng để xây dựng sẽ tìm trong ``usr/bin`` bên trong thư mục bạn cung cấp cho các tệp nhị phân của toolchain, vì vậy bạn phải sao chép vào thư mục con đó, tương tự như các lệnh sau:

::

    mkdir -p "$HOME/iostoolchain/usr"
    cp -r target/bin "$HOME/iostoolchain/usr/"

Bây giờ bạn sẽ có các tệp nhị phân của toolchain iOS trong ``$HOME/iostoolchain/usr/bin``.

Biên dịch Godot cho iPhone
--------------------------

Sau khi hoàn tất các bước trên, trong môi trường của bạn sẽ cần có hai thứ: toolchain đã xây dựng và thư mục iPhoneOS SDK. Bạn có thể đặt chúng ở bất kỳ đâu vì phải cung cấp đường dẫn đến chúng cho lệnh xây dựng SCons.

Để nền tảng iPhone được nhận diện, bạn cần định nghĩa biến môi trường ``OSXCROSS_IOS`` với bất kỳ giá trị nào.

::

    export OSXCROSS_IOS="anything"

Bây giờ bạn có thể biên dịch cho iPhone bằng SCons theo cách tiêu chuẩn của Godot, với một số đối số bổ sung để cung cấp các đường dẫn chính xác:

::

    scons platform=ios arch=arm64 target=template_release IOS_SDK_PATH="/path/to/iPhoneSDK" IOS_TOOLCHAIN_PATH="/path/to/iostoolchain" ios_triple="arm-apple-darwin11-"
