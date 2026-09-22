.. _doc_what_is_assetlib:

Giới thiệu về Asset Library
===========================

Godot Asset Library, còn được gọi là AssetLib, là một repository chứa các addon, script, tool và tài nguyên khác do người dùng đóng góp cho Godot, gọi chung là asset. Tất cả người dùng Godot đều có thể tải chúng xuống trực tiếp từ engine, nhưng bạn cũng có thể truy cập Asset Library tại `trang web chính thức <https://godotengine.org/asset-library/asset>`_ của Godot.

Thoạt nhìn, Asset Library có thể trông giống và hoạt động tương tự các cửa hàng asset dành cho những engine khác, chẳng hạn như Asset Store của Unity hoặc Marketplace của Unreal Engine, nơi bạn có thể gửi cả asset miễn phí lẫn asset thương mại có tính phí. Ngoài ra, những asset như vậy thường được phân phối theo các giấy phép độc quyền, không miễn phí, giới hạn những gì bạn có thể làm với chúng.

Asset Library thì khác - tất cả asset đều được phân phối miễn phí và theo nhiều giấy phép nguồn mở, chẳng hạn như giấy phép MIT, GPL và Boost Software License. Vì vậy, AssetLib gần với các repository phần mềm của một bản phân phối Linux hơn.

Nhóm trang này sẽ hướng dẫn cách sử dụng AssetLib (cả bên trong Godot lẫn trên trang web), cách bạn có thể gửi asset của riêng mình và các nguyên tắc gửi asset.

Xin lưu ý rằng AssetLib còn tương đối mới - có thể vẫn tồn tại nhiều điểm bất tiện, bug và vấn đề về khả năng sử dụng. Cũng như mọi dự án Godot, repository mã nguồn có sẵn trên `GitHub <https://github.com/godotengine/godot-asset-library>`_, nơi bạn có thể gửi pull request và issue, vì vậy đừng ngần ngại truy cập repository này!

Các loại asset
--------------

Hãy lưu ý rằng nhìn chung có hai loại asset khác nhau mà bạn có thể đăng.

* Các asset được gắn nhãn "Templates", "Projects" hoặc "Demos" sẽ xuất hiện trong tab "Asset Library" của Godot Project Manager. Đây là những project Godot độc lập và có thể tự chạy.

* Các asset khác sẽ xuất hiện bên trong Godot editor, trong tab màn hình chính "Asset Library", cạnh "2D", "3D" và "Script". Những asset này được thiết kế để tải xuống và đặt vào một project Godot hiện có.

Câu hỏi thường gặp
------------------

Có thể tải asset có tính phí lên asset library không?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Không phải asset library chính thức, mặc dù trong tương lai có thể sẽ có các asset library khác cho phép điều này. Tuy vậy, bạn được phép kiếm tiền và bán asset Godot bên ngoài Asset Library.

.. _`official website`: https://godotengine.org/asset-library/asset
.. _`GitHub`: https://github.com/godotengine/godot-asset-library
