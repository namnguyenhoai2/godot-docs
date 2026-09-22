.. _doc_cross-compiling_for_ios_on_linux:

Cross-compile cho iOS trên Linux
================================

.. highlight:: shell

Quy trình này khá phức tạp và yêu cầu nhiều bước, nhưng sau khi cấu hình môi trường đúng cách, bạn có thể compile Godot cho iOS bất cứ khi nào muốn.

Tuyên bố miễn trừ trách nhiệm
-----------------------------

Mặc dù có thể compile cho iOS trong môi trường Linux, Apple rất hạn chế các công cụ được phép sử dụng (đặc biệt là về phần cứng), gần như chỉ cho phép sử dụng sản phẩm của họ để phát triển. Vì vậy, quy trình này **không chính thức**. Tuy nhiên, vào năm 2010, Apple cho biết họ đã nới lỏng một số `hướng dẫn xét duyệt App Store <https://developer.apple.com/app-store/review/guidelines/>`__ để cho phép sử dụng bất kỳ công cụ nào, miễn là binary tạo ra không tải xuống bất kỳ code nào, nghĩa là việc sử dụng quy trình được mô tả ở đây và cross-compile binary sẽ không có vấn đề gì.

Yêu cầu
-------

- `XCode với iOS SDK <https://developer.apple.com/download/all/?q=Xcode>`__ (bạn phải đăng nhập vào Apple ID để tải Xcode).
- `Clang >= 3.5 <https://clang.llvm.org>`__ được cài đặt trên máy phát triển của bạn và nằm trong ``PATH``. Phiên bản này phải >= 3.5 để target kiến trúc ``arm64``.
- `xar <https://mackyle.github.io/xar/>`__ và `pbzx <https://github.com/NiklasRosenstein/pbzx>`__ (cần thiết để giải nén archive ``.xip`` chứa Xcode).

  - Để build xar và pbzx, bạn có thể làm theo `hướng dẫn này <https://gist.github.com/phracker/1944ce190e01963c550566b749bd2b54>`__.

- `cctools-port <https://github.com/tpoechtrager/cctools-port>`__ cho các build tool cần thiết. Quy trình build khá đặc thù và được mô tả bên dưới.

  - Công cụ này cũng có một số dependency bổ sung: automake, autogen, libtool.

Cấu hình môi trường
-------------------

Chuẩn bị SDK
~~~~~~~~~~~~

Giải nén file Xcode ``.xip`` mà bạn đã tải xuống từ trang web dành cho developer của Apple:

::

    mkdir xcode xar -xf /path/to/Xcode_X.x.xip -C xcode pbzx -n Content | cpio -i

    [...] ######### Blocks

Lưu ý rằng đối với các lệnh bên dưới, bạn sẽ cần thay thế phiên bản (``x.x``) bằng phiên bản iOS SDK bạn đang sử dụng. Nếu không biết phiên bản iPhone SDK của mình, bạn có thể xem file JSON bên trong ``Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs``.

Giải nén iOS SDK:

::

    export IOS_SDK_VERSION="x.x" mkdir -p iPhoneSDK/iPhoneOS${IOS_SDK_VERSION}.sdk cp -r xcode/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/* iPhoneSDK/iPhoneOS${IOS_SDK_VERSION}.sdk cp -r xcode/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include/c++/* iPhoneSDK/iPhoneOS${IOS_SDK_VERSION}.sdk/usr/include/c++ fusermount -u xcode

Đóng gói SDK để cctools có thể sử dụng:

::

    cd iPhoneSDK tar -cf - * | xz -9 -c - > iPhoneOS${IOS_SDK_VERSION}.sdk.tar.xz

Toolchain
~~~~~~~~~

Build cctools:

::

    git clone https://github.com/tpoechtrager/cctools-port.git cd cctools-port/usage_examples/ios_toolchain ./build.sh /path/iPhoneOS${IOS_SDK_VERSION}.sdk.tar.xz arm64

Sao chép các tool vào một vị trí dễ dùng hơn. Lưu ý rằng các script SCons để build sẽ tìm trong ``usr/bin`` bên dưới thư mục bạn cung cấp cho các binary của toolchain, vì vậy bạn phải sao chép chúng vào thư mục con đó, tương tự như các lệnh sau:

::

    mkdir -p "$HOME/iostoolchain/usr" cp -r target/bin "$HOME/iostoolchain/usr/"

Bây giờ các binary của iOS toolchain sẽ nằm trong ``$HOME/iostoolchain/usr/bin``.

Compile Godot cho iPhone
------------------------

Sau khi hoàn tất các bước trên, bạn cần giữ lại hai thứ trong môi trường của mình: toolchain đã build và thư mục iPhoneOS SDK. Bạn có thể đặt chúng ở bất kỳ đâu vì cần cung cấp đường dẫn của chúng cho lệnh build SCons.

Để phát hiện platform iPhone, bạn cần định nghĩa biến môi trường ``OSXCROSS_IOS`` với bất kỳ giá trị nào.

::

    export OSXCROSS_IOS="anything"

Bây giờ bạn có thể compile cho iPhone bằng SCons theo cách chuẩn của Godot, với một số đối số bổ sung để cung cấp đúng đường dẫn:

::

    scons platform=ios arch=arm64 target=template_release IOS_SDK_PATH="/path/to/iPhoneSDK" IOS_TOOLCHAIN_PATH="/path/to/iostoolchain" ios_triple="arm-apple-darwin11-"
