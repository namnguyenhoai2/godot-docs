.. _doc_importing_translations:

Nhập bản dịch
=============

Trò chơi và quốc tế hóa
-----------------------

Cộng đồng game không chỉ sử dụng một ngôn ngữ hay có một nền văn hóa duy nhất. Cộng đồng này bao gồm nhiều ngôn ngữ và nền văn hóa khác nhau — giống như cộng đồng Godot! Nếu muốn cho phép người chơi trải nghiệm game bằng ngôn ngữ của họ, một trong những điều bạn cần cung cấp là bản dịch văn bản, được Godot hỗ trợ thông qua văn bản quốc tế hóa.

Trong các ứng dụng desktop hoặc mobile thông thường, văn bản quốc tế hóa thường nằm trong các tệp tài nguyên (hoặc tệp .po đối với các phần mềm GNU). Tuy nhiên, game có thể sử dụng lượng văn bản lớn hơn các ứng dụng nhiều bậc độ lớn, vì vậy chúng phải hỗ trợ các phương pháp hiệu quả để xử lý khối lượng lớn văn bản đa ngôn ngữ.

Có hai cách tiếp cận để tạo game và ứng dụng đa ngôn ngữ. Cả hai đều dựa trên hệ thống key:value. Cách thứ nhất là sử dụng một trong các ngôn ngữ làm key (thường là tiếng Anh), cách thứ hai là sử dụng một identifier cụ thể. Cách thứ nhất có lẽ dễ hơn trong quá trình phát triển nếu game được phát hành trước bằng tiếng Anh rồi mới phát hành bằng các ngôn ngữ khác, nhưng sẽ trở thành một cơn ác mộng hoàn toàn nếu làm việc với nhiều ngôn ngữ cùng lúc.

Nhìn chung, game sử dụng cách tiếp cận thứ hai và một ID duy nhất được dùng cho mỗi chuỗi. Điều này cho phép bạn chỉnh sửa văn bản trong khi văn bản đang được dịch sang các ngôn ngữ khác. ID duy nhất có thể là một số, một chuỗi hoặc một chuỗi kèm theo một số (dù sao thì nó cũng chỉ là một chuỗi duy nhất).

Các định dạng được hỗ trợ
-------------------------

Để hoàn thiện quy trình và hỗ trợ bản dịch hiệu quả, Godot có một importer đặc biệt có thể đọc các tệp CSV. Hầu hết các trình chỉnh sửa bảng tính đều có thể xuất sang định dạng này, vì vậy yêu cầu duy nhất là các tệp phải được sắp xếp theo một cấu trúc đặc biệt. Xem
:ref:`doc_localization_using_spreadsheets` để biết thông tin chi tiết về cách định dạng và nhập CSV.

Nếu cần một định dạng tệp mạnh mẽ hơn, Godot cũng hỗ trợ tải các bản dịch được viết theo định dạng gettext ``.po``. Xem
:ref:`doc_localization_using_gettext` để biết chi tiết.
