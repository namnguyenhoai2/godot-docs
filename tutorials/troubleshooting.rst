.. _doc_troubleshooting:

Xử lý sự cố
===========

Trang này liệt kê các vấn đề thường gặp khi sử dụng Godot và các giải pháp khả thi.

.. seealso::

    Xem :ref:`doc_using_the_web_editor` để biết các lưu ý riêng của phiên bản Web của trình chỉnh sửa Godot.

Trình chỉnh sửa chạy chậm và sử dụng toàn bộ tài nguyên CPU và GPU, khiến máy tính của tôi phát ra nhiều tiếng ồn
-----------------------------------------------------------------------------------------------------------------

Đây là một vấn đề đã biết, đặc biệt là trên macOS vì hầu hết máy Mac đều có màn hình Retina. Do màn hình Retina có mật độ điểm ảnh cao hơn, mọi thứ phải được kết xuất ở độ phân giải cao hơn. Điều này làm tăng tải cho GPU và làm giảm hiệu năng cảm nhận được.

Có một số cách để cải thiện hiệu năng và thời lượng pin:

- Trong 3D, hãy nhấp vào nút **Perspective** ở góc trên bên trái và bật **Half Resolution**. Khi đó, khung nhìn 3D sẽ được kết xuất ở một nửa độ phân giải, có thể nhanh hơn tới 4 lần.
- Mở Editor Settings và tăng giá trị **Low Processor Mode Sleep (µsec)** lên ``33000`` (30 FPS). Giá trị này xác định khoảng thời gian *microseconds* giữa các khung hình cần kết xuất. Giá trị cao hơn sẽ khiến trình chỉnh sửa kém phản hồi hơn, nhưng giúp giảm đáng kể mức sử dụng CPU và GPU.
- Nếu bạn có một node khiến trình chỉnh sửa liên tục vẽ lại (chẳng hạn như particle), hãy ẩn node đó và hiển thị nó bằng một script trong phương thức ``_ready()``. Bằng cách này, node sẽ bị ẩn trong trình chỉnh sửa nhưng vẫn hiển thị trong project đang chạy.

Trình chỉnh sửa bị giật và nhấp nháy trên màn hình có tần số quét biến thiên (G-Sync/FreeSync)
----------------------------------------------------------------------------------------------

Đây là một `known issue <https://github.com/godotengine/godot/issues/38219>`__. Màn hình có tần số quét biến thiên cần liên tục điều chỉnh các đường cong gamma để phát ra lượng ánh sáng nhất quán theo thời gian. Điều này có thể khiến hiện tượng nhấp nháy xuất hiện ở các vùng tối của hình ảnh khi tần số quét thay đổi nhiều, điều xảy ra vì trình chỉnh sửa Godot chỉ vẽ lại khi cần thiết.

Có một số cách khắc phục tạm thời cho vấn đề này:

- Bật **Interface > Editor > Update Continuously** trong Editor Settings. Lưu ý rằng việc này sẽ làm tăng mức tiêu thụ điện năng và lượng nhiệt/tiếng ồn phát ra vì trình chỉnh sửa sẽ liên tục kết xuất, ngay cả khi không có gì thay đổi trên màn hình. Để giảm bớt điều này, bạn có thể tăng **Low Processor Mode Sleep (µsec)** lên ``33000`` (30 FPS) trong Editor Settings. Giá trị này xác định khoảng thời gian *microseconds* giữa các khung hình cần kết xuất. Giá trị cao hơn sẽ khiến trình chỉnh sửa kém phản hồi hơn, nhưng giúp giảm đáng kể mức sử dụng CPU và GPU.
- Ngoài ra, hãy tắt tần số quét biến thiên trên màn hình hoặc trong driver đồ họa.
- Có thể giảm hiện tượng nhấp nháy VRR trên một số màn hình bằng các tùy chọn **VRR Control** hoặc **Fine Tune Dark Areas** trong OSD của màn hình. Các tùy chọn này có thể làm tăng độ trễ đầu vào hoặc khiến màu đen bị mất chi tiết.
- Nếu sử dụng màn hình OLED, hãy dùng preset giao diện **Black (OLED)** của trình chỉnh sửa trong Editor Settings. Preset này che hiện tượng nhấp nháy VRR nhờ mức màu đen hoàn hảo của OLED.

Trình chỉnh sửa hoặc project mất rất nhiều thời gian để khởi động
-----------------------------------------------------------------

Khi sử dụng một trong các renderer dựa trên RenderingDevice (Forward+ hoặc Mobile), lần khởi động đầu tiên dự kiến sẽ tương đối lâu. Đó là vì shader cần được biên dịch trước khi có thể lưu vào bộ nhớ đệm. Shader cũng cần được lưu vào bộ nhớ đệm lại sau khi cập nhật Godot, cập nhật driver đồ họa hoặc chuyển đổi card đồ họa.

Nếu vấn đề vẫn tiếp diễn sau lần khởi động đầu tiên, đây là một `known bug <https://github.com/godotengine/godot/issues/20566>`__ trên Windows khi bạn kết nối một số thiết bị ngoại vi USB nhất định. Cụ thể, phần mềm iCUE của Corsair có vẻ gây ra lỗi này. Hãy thử cập nhật driver của các thiết bị ngoại vi USB lên phiên bản mới nhất. Nếu lỗi vẫn tiếp diễn, bạn cần ngắt kết nối thiết bị ngoại vi cụ thể đó trước khi mở trình chỉnh sửa. Sau đó, bạn có thể kết nối lại thiết bị.

Phần mềm tường lửa như Portmaster cũng có thể khiến cổng debug bị chặn. Điều này khiến project mất nhiều thời gian để khởi động, đồng thời không thể sử dụng các tính năng debug trong trình chỉnh sửa (chẳng hạn như xem ``print()`` output). Bạn có thể khắc phục bằng cách thay đổi cổng debug mà project sử dụng trong Editor Settings (**Network > Debug > Remote Port**). Giá trị mặc định là ``6007``; hãy thử một giá trị khác lớn hơn ``1024``, chẳng hạn như ``7007``.

Trên Windows, khi tải project lần đầu tiên sau khi bật PC, Windows Defender sẽ khiến quá trình xác thực bộ nhớ đệm filesystem lúc khởi động project mất nhiều thời gian hơn đáng kể. Điều này đặc biệt dễ nhận thấy ở các project có số lượng tệp lớn. Hãy cân nhắc thêm thư mục project vào danh sách loại trừ bằng cách đi tới Virus & threat protection > Virus & threat protection settings > Add or remove exclusions.

Trình chỉnh sửa Godot có vẻ bị treo sau khi nhấp vào system console
-------------------------------------------------------------------

Khi chạy Godot trên Windows với system console được bật, bạn có thể vô tình bật *selection mode* bằng cách nhấp vào bên trong cửa sổ lệnh. Hành vi riêng của Windows này sẽ tạm dừng ứng dụng để cho phép bạn chọn văn bản bên trong system console. Godot không thể ghi đè hành vi đặc thù của hệ thống này.

Để giải quyết vấn đề này, hãy chọn cửa sổ system console và nhấn Enter để thoát khỏi selection mode.

Biểu tượng Godot editor trên dock của macOS bị nhân bản mỗi khi được di chuyển thủ công
---------------------------------------------------------------------------------------

Nếu bạn mở trình chỉnh sửa Godot và thay đổi thủ công vị trí của biểu tượng trên dock, sau đó khởi động lại trình chỉnh sửa, một biểu tượng dock trùng lặp sẽ xuất hiện ở ngoài cùng bên phải của dock.

Điều này là do một hạn chế trong thiết kế của dock trên macOS. Cách duy nhất đã biết để giải quyết vấn đề này là hợp nhất project manager và trình chỉnh sửa thành một process duy nhất, nghĩa là project manager sẽ không còn tạo một process riêng khi khởi động trình chỉnh sửa. Mặc dù việc sử dụng một instance process duy nhất mang lại một số lợi ích, điều này chưa được lên kế hoạch thực hiện trong tương lai gần do độ phức tạp của nhiệm vụ.

Để tránh vấn đề này, hãy giữ biểu tượng Godot editor trên dock ở vị trí mặc định do macOS tạo.

Một số văn bản như "NO DC" xuất hiện ở góc trên bên trái của cửa sổ Project Manager và trình chỉnh sửa
------------------------------------------------------------------------------------------------------

Nguyên nhân là driver đồ họa NVIDIA chèn một lớp phủ để hiển thị thông tin.

Để tắt lớp phủ này trên Windows, hãy khôi phục cài đặt driver đồ họa về giá trị mặc định trong NVIDIA Control Panel.

Để tắt lớp phủ này trên Linux, hãy mở ``nvidia-settings``, đi đến **X Screen 0 > OpenGL Settings** rồi bỏ chọn **Enable Graphics API Visual Indicator**.

Một biểu tượng micrô hoặc "refresh" xuất hiện ở góc dưới bên phải của cửa sổ Project Manager và trình chỉnh sửa
---------------------------------------------------------------------------------------------------------------

Nguyên nhân là driver đồ họa NVIDIA chèn một lớp phủ để hiển thị thông tin instant replay khi ghi bằng ShadowPlay. Lớp phủ này chỉ hiển thị trên Windows, vì Linux không hỗ trợ ShadowPlay.

Để tắt lớp phủ này, hãy nhấn :kbd:`Alt + Z` (phím tắt mặc định cho lớp phủ NVIDIA) và tắt **Settings > HUD Layout > Status Indicator** trong lớp phủ NVIDIA.

Ngoài ra, bạn có thể cài đặt `new NVIDIA app <https://www.nvidia.com/en-us/software/nvidia-app/>`, ứng dụng thay thế GeForce Experience và không gặp vấn đề này. Không giống GeForce Experience, ứng dụng NVIDIA hiển thị chỉ báo replay ở góc màn hình thay vì góc của từng cửa sổ.

Trình chỉnh sửa hoặc project hiển thị quá sắc nét hoặc quá mờ
-------------------------------------------------------------

.. figure:: img/troubleshooting_graphics_driver_sharpening.webp
   :align: center
   :alt: Hiển thị chính xác (bên trái), hiển thị quá sắc nét do tính năng làm sắc nét của driver đồ họa (bên phải)

   Hiển thị chính xác (bên trái), hiển thị quá sắc nét do tính năng làm sắc nét của driver đồ họa (bên phải)

Nếu trình chỉnh sửa hoặc project hiển thị quá sắc nét, nguyên nhân có thể là tính năng làm sắc nét hình ảnh bị driver đồ họa buộc bật cho tất cả ứng dụng Vulkan hoặc OpenGL. Bạn có thể tắt hành vi này trong control panel của driver đồ họa:

- **NVIDIA (Windows):** Mở start menu và chọn **NVIDIA Control Panel**. Mở thẻ **Manage 3D settings** ở bên trái. Trong danh sách ở giữa, cuộn đến **Image Sharpening** và đặt thành **Sharpening Off**.
- **AMD (Windows):** Mở start menu và chọn **AMD Software**. Nhấp vào biểu tượng "cog" cài đặt ở góc trên bên phải. Chuyển đến thẻ **Graphics** rồi tắt **Radeon Image Sharpening**.

Nếu trình chỉnh sửa hoặc project hiển thị quá mờ, nguyên nhân có thể là
:abbr:`FXAA (Fast Approximate AntiAliasing)` bị driver đồ họa buộc bật cho tất cả ứng dụng Vulkan hoặc OpenGL.

- **NVIDIA (Windows):** Mở start menu và chọn **NVIDIA Control Panel**. Mở thẻ **Manage 3D settings** ở bên trái. Trong danh sách ở giữa, cuộn đến **Fast Approximate Antialiasing** và đặt thành **Application Controlled**.
- **NVIDIA (Linux):** Mở menu ứng dụng và chọn **NVIDIA X Server Settings**. Ở bên trái, chọn **Antialiasing Settings**, sau đó bỏ chọn **Enable FXAA**.
- **AMD (Windows):** Mở start menu và chọn **AMD Software**. Nhấp vào biểu tượng "cog" cài đặt ở góc trên bên phải. Chuyển đến thẻ **Graphics**, cuộn xuống dưới cùng và nhấp vào **Advanced** để mở rộng các cài đặt. Tắt **Morphological Antialiasing**.

Các tiện ích độc lập với nhà cung cấp bên thứ ba như vkBasalt cũng có thể buộc bật tính năng làm sắc nét hoặc FXAA cho tất cả ứng dụng Vulkan. Bạn cũng nên kiểm tra cấu hình của chúng.

Sau khi thay đổi các tùy chọn trong driver đồ họa hoặc tiện ích bên thứ ba, hãy khởi động lại Godot để các thay đổi có hiệu lực.

Nếu vẫn muốn buộc bật tính năng làm sắc nét hoặc FXAA cho các ứng dụng khác, bạn nên thực hiện theo từng ứng dụng bằng hệ thống application profile do control panel của driver đồ họa cung cấp.

Trình chỉnh sửa/project bị treo hoặc hiển thị hình ảnh bị lỗi sau khi đánh thức PC từ trạng thái tạm ngưng
----------------------------------------------------------------------------------------------------------

Đây là một vấn đề đã biết trên Linux với đồ họa NVIDIA khi sử dụng driver độc quyền. Hiện chưa có cách khắc phục dứt điểm, vì tính năng tạm ngưng trên Linux + NVIDIA thường bị lỗi khi có OpenGL hoặc Vulkan tham gia. Phương thức kết xuất Compatibility (sử dụng OpenGL) nhìn chung ít gặp vấn đề liên quan đến tạm ngưng hơn so với các renderer Forward+ và Mobile (sử dụng Vulkan).

Driver NVIDIA cung cấp một *experimental* `option to preserve video memory after suspend <https://wiki.archlinux.org/title/NVIDIA/Tips_and_tricks#Preserve_video_memory_after_suspend>`__, có thể khắc phục vấn đề này. Tùy chọn này được báo cáo là hoạt động tốt hơn với các phiên bản driver NVIDIA mới hơn.

Để tránh mất công việc, hãy lưu các scene trong trình chỉnh sửa trước khi đưa PC vào chế độ ngủ.

Project hoạt động khi chạy từ trình chỉnh sửa, nhưng không tải được một số tệp khi chạy từ bản sao đã export
------------------------------------------------------------------------------------------------------------

Nguyên nhân thường là bạn quên chỉ định bộ lọc cho các tệp không phải resource trong hộp thoại Export. Theo mặc định, Godot chỉ đưa các *resources* thực sự vào tệp PCK. Một số tệp thường được sử dụng, chẳng hạn như tệp JSON, không được xem là resource. Ví dụ: nếu tải ``test.json`` trong project đã export, bạn cần chỉ định ``*.json`` trong bộ lọc export non-resource. Xem
:ref:`doc_exporting_projects_export_mode` để biết thêm thông tin.

Ngoài ra, lưu ý rằng các tệp và thư mục có tên bắt đầu bằng dấu chấm sẽ không bao giờ được đưa vào project đã export. Điều này nhằm ngăn các thư mục kiểm soát phiên bản như ``.git`` được đưa vào tệp PCK đã export.

Trên Windows, nguyên nhân cũng có thể là do vấn đề :ref:`phân biệt chữ hoa chữ thường <doc_project_organization_case_sensitivity>`. Nếu bạn tham chiếu một tài nguyên trong script với kiểu chữ khác với kiểu chữ trên filesystem, việc tải sẽ thất bại sau khi bạn export project. Điều này là do filesystem PCK ảo phân biệt chữ hoa chữ thường, trong khi filesystem của Windows mặc định không phân biệt chữ hoa chữ thường.

Project thường xuyên bị crash hoặc bị crash ngay sau khi mở từ trình quản lý project
------------------------------------------------------------------------------------

Điều này có thể do nhiều nguyên nhân, chẳng hạn như editor plugin, GDExtension addon hoặc một nguyên nhân khác. Trong trường hợp này, bạn nên mở project ở recovery mode và cố gắng tìm cũng như khắc phục nguyên nhân gây ra các lần crash. Xem :ref:`trang Project Manager <doc_project_manager>` để biết thêm thông tin.
