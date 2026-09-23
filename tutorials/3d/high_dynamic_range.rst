:article_outdated: Đúng

.. _doc_high_dynamic_range:

Chiếu sáng dải động cao
=======================

Giới thiệu
----------

Thông thường, nghệ sĩ sẽ hoàn thành toàn bộ việc dựng hình 3D, sau đó hoàn thành toàn bộ việc tạo texture, xem model có vẻ ngoài tuyệt đẹp của mình trong phần mềm dựng hình 3D và nói "trông tuyệt vời, sẵn sàng để tích hợp!", rồi chuyển sang game, thiết lập ánh sáng và chạy game.

Vậy toàn bộ vấn đề "HDR" này bắt đầu xuất hiện ở thời điểm nào? Để hiểu câu trả lời, chúng ta cần xem xét cách các màn hình hoạt động.

Màn hình của bạn xuất ra các tỷ lệ ánh sáng tuyến tính từ một cường độ tối đa đến một cường độ tối thiểu. Các game engine hiện đại thực hiện những phép toán phức tạp trên các giá trị ánh sáng tuyến tính trong những scene tương ứng. Vậy vấn đề là gì?

Màn hình có dải cường độ giới hạn, tùy thuộc vào loại màn hình. Tuy nhiên, game engine render đến một dải giá trị cường độ không giới hạn. Mặc dù "cường độ tối đa" có ý nghĩa đối với màn hình sRGB, nó không có ảnh hưởng gì trong game engine; ở đó chỉ có một dải giá trị cường độ có khả năng rộng vô hạn được tạo ra trong mỗi frame render.

Điều này có nghĩa là một số phép biến đổi đối với cường độ ánh sáng của scene, còn được gọi là các tỷ lệ ánh sáng *scene-referred*, cần được biến đổi và ánh xạ để nằm trong dải đầu ra cụ thể của màn hình được chọn. Cách dễ hiểu nhất là hình dung chúng ta đang chụp ảnh scene của game engine thông qua một camera ảo. Khi đó, camera ảo sẽ áp dụng một phép biến đổi render camera cụ thể cho dữ liệu scene, và đầu ra sẽ sẵn sàng để hiển thị trên một loại màn hình cụ thể.

.. note::

    Godot hỗ trợ *output* dải động cao. Bạn có thể đọc thêm về vấn đề này trên trang :ref:`doc_hdr_output`.

    Đối với người dùng nâng cao, có thể lấy hình ảnh viewport chưa qua tonemapping với đầy đủ dữ liệu HDR, sau đó lưu hình ảnh này vào tệp OpenEXR.

Màn hình máy tính
-----------------

Hầu hết mọi màn hình đều yêu cầu mã hóa phi tuyến cho các giá trị mã được gửi đến chúng. Sau đó, màn hình sử dụng đặc tính truyền riêng của mình để "giải mã" giá trị mã thành các tỷ lệ ánh sáng tuyến tính đầu ra, rồi chiếu các tỷ lệ đó từ những nguồn sáng có màu sắc riêng biệt tại mỗi vị trí phát xạ đỏ, lục và lam.

Đối với phần lớn màn hình máy tính, thông số kỹ thuật của màn hình được xác định theo IEC 61966-2-1, còn được gọi là đặc tả sRGB năm 1996. Đặc tả này mô tả cách một màn hình sRGB phải hoạt động, bao gồm màu của các nguồn sáng trong pixel LED cũng như các đặc tính truyền của đầu vào (OETF) và đầu ra (EOTF).

Không phải mọi màn hình đều sử dụng OETF và EOTF giống như màn hình máy tính. Ví dụ, màn hình phát sóng truyền hình sử dụng EOTF BT.1886. Tuy nhiên, Godot chỉ hỗ trợ màn hình sRGB và HDR.

Tiêu chuẩn sRGB dựa trên mối quan hệ phi tuyến giữa dòng điện và đầu ra ánh sáng của các màn hình CRT máy tính để bàn thông dụng.

.. image:: img/hdr_gamma.png

Phép toán của một model scene-referred yêu cầu chúng ta nhân scene với các giá trị khác nhau để điều chỉnh cường độ và độ phơi sáng theo các dải ánh sáng khác nhau. Hàm truyền của màn hình không thể render phù hợp dải động rộng hơn của đầu ra scene từ game engine chỉ bằng hàm truyền đơn giản của màn hình. Cần có một phương pháp mã hóa phức tạp hơn.

Scene tuyến tính & pipeline asset
---------------------------------

Làm việc với sRGB tuyến tính theo scene phức tạp hơn việc nhấn một công tắc duy nhất. Trước tiên, các asset hình ảnh được import phải được chuyển đổi thành các tỷ lệ ánh sáng tuyến tính trong quá trình import. Ngay cả khi đã được tuyến tính hóa, các asset đó có thể vẫn không hoàn toàn phù hợp để sử dụng làm texture, tùy thuộc vào cách chúng được tạo ra.

Có hai cách để thực hiện việc này:

Hàm truyền sRGB để hiển thị các tỷ lệ tuyến tính trong quá trình import hình ảnh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đây là phương pháp dễ nhất để sử dụng asset sRGB, nhưng không phải là phương pháp lý tưởng nhất. Một vấn đề của phương pháp này là làm giảm chất lượng. Việc sử dụng 8 bit cho mỗi kênh để biểu diễn các tỷ lệ ánh sáng tuyến tính không đủ để lượng tử hóa chính xác các giá trị. Những texture này cũng có thể bị nén về sau, khiến vấn đề trở nên nghiêm trọng hơn.

Hàm truyền sRGB phần cứng để chuyển đổi tuyến tính hiển thị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

GPU sẽ thực hiện việc chuyển đổi sau khi đọc texel bằng số dấu phẩy động. Cách này hoạt động tốt trên PC và console, nhưng hầu hết thiết bị di động không hỗ trợ, hoặc không hỗ trợ trên các định dạng texture nén (ví dụ như iOS).

Từ scene tuyến tính sang phi tuyến theo màn hình
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi hoàn tất toàn bộ quá trình render, kết quả render tuyến tính của scene cần được biến đổi thành đầu ra phù hợp, chẳng hạn như màn hình sRGB. Để thực hiện việc này, hãy bật chuyển đổi sRGB trong :ref:`Environment <class_Environment>` hiện tại (sẽ nói thêm về vấn đề này bên dưới).

Hãy nhớ rằng các phép chuyển đổi **sRGB -> Display Linear** và **Display Linear -> sRGB** luôn phải được bật **cả hai**. Nếu không bật một trong hai, hình ảnh sẽ trở nên tệ hại, chỉ phù hợp với các game indie thử nghiệm avant-garde.

Các tham số của HDR
-------------------

Bạn có thể tìm thấy các thiết lập HDR trong resource :ref:`Environment <class_Environment>`. Hầu hết thời gian, chúng nằm bên trong một
node :ref:`WorldEnvironment <class_WorldEnvironment>` hoặc được thiết lập trong một Camera node. Để biết thêm thông tin, hãy xem
:ref:`doc_environment_and_post_processing`.
