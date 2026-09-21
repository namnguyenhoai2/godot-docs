.. _doc_what_is_assetlib:

Giới thiệu về Asset Library
===========================

Godot Asset Library, còn được gọi là AssetLib, là một kho chứa các addon, tập lệnh, công cụ và tài nguyên khác do người dùng Godot đóng góp, gọi chung là các asset. Tất cả người dùng Godot đều có thể tải chúng xuống trực tiếp từ bên trong engine, nhưng cũng có thể truy cập kho này tại `trang web chính thức <https://godotengine.org/asset-library/asset>`_ của Godot.

Nhìn bề ngoài, Asset Library có thể trông giống và hoạt động tương tự các cửa hàng asset dành cho những engine khác, chẳng hạn như Asset Store của Unity hoặc Marketplace của Unreal Engine, nơi bạn có thể gửi cả asset miễn phí lẫn asset thương mại có tính phí. Ngoài ra, các asset như vậy thường được phân phối theo những giấy phép độc quyền, không miễn phí, giới hạn những gì bạn có thể làm với chúng.

Asset Library thì khác — tất cả asset đều được phân phối miễn phí và theo nhiều giấy phép nguồn mở (chẳng hạn như giấy phép MIT, GPL và Boost Software License). Điều này khiến AssetLib giống với các kho phần mềm của một bản phân phối Linux hơn.

Nhóm trang này sẽ hướng dẫn cách sử dụng AssetLib (cả bên trong Godot lẫn trên trang web), cách bạn có thể gửi asset của riêng mình và các nguyên tắc gửi asset.

Xin lưu ý rằng AssetLib còn tương đối mới — có thể vẫn tồn tại nhiều điểm bất tiện, lỗi và vấn đề về khả năng sử dụng. Cũng như tất cả dự án Godot, kho mã nguồn có sẵn trên `GitHub <https://github.com/godotengine/godot-asset-library>`_, nơi bạn có thể gửi các pull request và issue, vì vậy đừng ngần ngại truy cập kho này!

Các loại asset
--------------

Hãy lưu ý rằng nhìn chung có hai loại asset khác nhau mà bạn có thể đăng.

* Các asset được gắn nhãn "Templates", "Projects" hoặc "Demos" sẽ xuất hiện trong thẻ "Asset Library" của Godot Project Manager. Đây là các dự án Godot độc lập có thể tự chạy.

* Các asset khác sẽ xuất hiện bên trong trình soạn thảo Godot, trong thẻ màn hình chính "Asset Library", bên cạnh "2D", "3D" và "Script". Những asset này có mục đích để tải xuống và đưa vào một dự án Godot hiện có.

Các câu hỏi thường gặp
----------------------

Có thể tải asset có tính phí lên asset library không?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Không thể tải lên asset library chính thức, mặc dù trong tương lai có thể sẽ có những asset library khác cho phép điều đó. Tuy vậy, bạn được phép kiếm tiền và bán asset Godot bên ngoài Asset Library.
