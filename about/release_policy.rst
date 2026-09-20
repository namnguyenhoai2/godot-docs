:allow_comments: False

.. _doc_release_policy:

Chính sách phát hành Godot
==========================

Chính sách phát hành của Godot không ngừng được hoàn thiện. Phần mô tả dưới đây cung cấp một ý tưởng tổng quát về những điều có thể mong đợi, nhưng điều thực sự xảy ra còn phụ thuộc vào lựa chọn của các cộng tác viên cốt lõi và nhu cầu của cộng đồng tại từng thời điểm.

Đánh số phiên bản Godot
-----------------------

Godot tuân theo `Semantic Versioning <https://semver.org/>`__ ở mức tương đối, với hệ thống đánh số phiên bản ``major.minor.patch``, dù cách diễn giải từng thuật ngữ được điều chỉnh cho phù hợp với độ phức tạp của một game engine:

- Phiên bản ``major`` được tăng lên khi xảy ra những thay đổi lớn làm phá vỡ tính tương thích, đòi hỏi công sức chuyển đổi đáng kể để chuyển các dự án từ phiên bản chính này sang phiên bản chính khác.

  Ví dụ, việc chuyển các dự án Godot từ Godot 3.x sang Godot 4.x yêu cầu chạy dự án qua một công cụ chuyển đổi, sau đó thực hiện thủ công một số điều chỉnh bổ sung đối với những phần mà công cụ không thể tự động xử lý.

- Phiên bản ``minor`` được tăng lên cho các bản phát hành tính năng không phá vỡ tính tương thích theo cách nghiêm trọng. Các phiên bản nhỏ *có thể* gây ra những thay đổi nhỏ làm phá vỡ tính tương thích trong các lĩnh vực rất cụ thể, nhưng phần lớn dự án sẽ không bị ảnh hưởng hoặc không cần nhiều công sức chuyển đổi.

  Điều này là do Godot, với tư cách là một game engine, bao quát nhiều lĩnh vực như kết xuất, vật lý và lập trình kịch bản. Việc sửa lỗi hoặc triển khai tính năng mới trong một lĩnh vực đôi khi có thể yêu cầu thay đổi cách hoạt động của một tính năng hoặc sửa đổi giao diện của một lớp, ngay cả khi phần còn lại của API engine vẫn tương thích ngược.

.. tip::

    Tất cả người dùng đều được khuyến nghị nâng cấp lên phiên bản nhỏ mới, nhưng cần tiến hành một số kiểm thử để đảm bảo dự án vẫn hoạt động như mong đợi.

- Phiên bản ``patch`` được tăng lên cho các bản phát hành bảo trì, tập trung vào việc sửa lỗi và các vấn đề bảo mật, triển khai các yêu cầu mới để hỗ trợ nền tảng, và đưa ngược các cải tiến khả dụng an toàn. Các bản vá tương thích ngược.

  Các phiên bản vá có thể bao gồm những tính năng mới nhỏ không ảnh hưởng đến API hiện có, do đó không có nguy cơ ảnh hưởng đến các dự án hiện tại.

.. tip::

    Vì vậy, việc cập nhật lên các phiên bản vá mới được xem là an toàn và được đặc biệt khuyến nghị cho tất cả người dùng của một nhánh ổn định nhất định.

Chúng tôi gọi các tổ hợp ``major.minor`` là *nhánh ổn định*. Mỗi nhánh ổn định bắt đầu bằng một bản phát hành ``major.minor`` (không có ``0`` cho ``patch``) và tiếp tục được phát triển cho các bản phát hành bảo trì trong một nhánh Git cùng tên (ví dụ: các bản cập nhật vá cho nhánh ổn định 4.0 được phát triển trong nhánh Git ``4.0``).

Lộ trình hỗ trợ bản phát hành
-----------------------------

.. UPDATE: Bảng thay đổi sau mỗi phiên bản nhỏ. Chính sách hỗ trợ có thể thay đổi.

Các nhánh ổn định được hỗ trợ *ít nhất* cho đến khi nhánh ổn định tiếp theo được phát hành và nhận bản cập nhật vá đầu tiên. Trên thực tế, chúng tôi hỗ trợ các nhánh ổn định trên cơ sở *nỗ lực tốt nhất* miễn là vẫn có người dùng đang hoạt động cần các bản cập nhật bảo trì.

Mỗi khi một phiên bản chính mới được phát hành, chúng tôi biến nhánh ổn định trước đó thành một bản phát hành được hỗ trợ dài hạn và cố gắng hết sức để cung cấp bản sửa lỗi cho các vấn đề mà người dùng của nhánh đó gặp phải nhưng không thể chuyển đổi các dự án phức tạp sang phiên bản chính mới. Đây là trường hợp của nhánh 2.1 và cũng là trường hợp của nhánh 3.x.

Trong một chuỗi bản phát hành nhỏ nhất định, chỉ bản phát hành vá mới nhất nhận được hỗ trợ. Nếu gặp vấn đề khi sử dụng một bản phát hành vá cũ hơn, hãy nâng cấp lên bản phát hành vá mới nhất của chuỗi đó và kiểm tra lại trước khi báo cáo vấn đề trên GitHub.

+--------------+----------------------+--------------------------------------------------------------------------+
| **Phiên bản** | **Ngày phát hành** | **Mức hỗ trợ** |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.8 | Quý 4 năm 2026 (ước tính) | |unstable| *Đang phát triển.* Nhận các tính năng mới, cải tiến khả dụng và |
| (`master`) | | cải tiến hiệu năng, cũng như bản sửa lỗi trong thời gian phát triển. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.7 | Tháng 6 năm 2026 | |supported| Nhận các bản sửa lỗi và vấn đề bảo mật, cũng như |
| | | các bản vá cho phép hỗ trợ nền tảng. |
++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.6 | Tháng 1 năm 2026 | |supported| Nhận các bản sửa lỗi và vấn đề bảo mật, cũng như |
| | | các bản vá cho phép hỗ trợ nền tảng. |
++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.5 | Tháng 9 năm 2025 | |partial| Chỉ nhận các bản sửa lỗi liên quan đến bảo mật và hỗ trợ nền tảng. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.4 | Tháng 3 năm 2025 | |eol| Không còn được hỗ trợ (cập nhật cuối: 4.4.1). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.3 | Tháng 8 năm 2024 | |eol| Không còn được hỗ trợ (cập nhật cuối: 4.3). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.2 | Tháng 11 năm 2023 | |eol| Không còn được hỗ trợ (cập nhật cuối: 4.2.2). |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.1 | Tháng 7 năm 2023 | |eol| Không còn được hỗ trợ (cập nhật cuối: 4.1.4). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 4.0 | Tháng 3 năm 2023 | |eol| Không còn được hỗ trợ (cập nhật cuối: 4.0.4). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.7 | Hiện chưa có thời gian dự kiến | |supported| *Beta.* Nhận các tính năng mới, cải tiến khả dụng và hiệu năng |
| (`3.x`) | | cũng như bản sửa lỗi trong thời gian phát triển. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.6 | Tháng 9 năm 2024 | |supported| Nhận các bản sửa lỗi và vấn đề bảo mật, cũng như |
| | | các bản vá cho phép hỗ trợ nền tảng. |
++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.5 | Tháng 8 năm 2022 | |eol| Không còn được hỗ trợ (cập nhật cuối: 3.5.3). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.4 | Tháng 11 năm 2021 | |eol| Không còn được hỗ trợ (cập nhật cuối: 3.4.5). |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.3 | Tháng 4 năm 2021 | |eol| Không còn được hỗ trợ (cập nhật cuối: 3.3.4). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.2 | Tháng 1 năm 2020 | |eol| Không còn được hỗ trợ (cập nhật cuối: 3.2.3). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.1 | Tháng 3 năm 2019 | |eol| Không còn được hỗ trợ (cập nhật cuối: 3.1.2). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 3.0 | Tháng 1 năm 2018 | |eol| Không còn được hỗ trợ (cập nhật cuối: 3.0.6). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 2.1 | Tháng 7 năm 2016 | |eol| Không còn được hỗ trợ (cập nhật cuối: 2.1.6). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 2.0 | Tháng 2 năm 2016 | |eol| Không còn được hỗ trợ (cập nhật cuối: 2.0.4.1). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 1.1 | Tháng 5 năm 2015 | |eol| Không còn được hỗ trợ. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| Godot 1.0 | Tháng 12 năm 2014 | |eol| Không còn được hỗ trợ. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. |supported| image:: img/supported.png
.. |partial| image:: img/partial.png
.. |eol| image:: img/eol.png
.. |unstable| image:: img/unstable.png

**Chú giải:** |supported| Hỗ trợ đầy đủ – |partial| Hỗ trợ một phần – |eol| Không hỗ trợ (đã hết vòng đời) – |unstable| Phiên bản đang phát triển

Các phiên bản Godot tiền phát hành không nhằm mục đích sử dụng trong môi trường production và chỉ được cung cấp cho mục đích kiểm thử.

.. seealso::

    Xem :ref:`doc_upgrading_to_godot_4` để biết hướng dẫn chuyển một dự án từ Godot 3.x sang 4.x.

.. _doc_release_policy_which_version_should_i_use:

Nên sử dụng phiên bản nào cho dự án mới?
----------------------------------------

Chúng tôi khuyến nghị sử dụng Godot 4.x cho các dự án mới, vì chuỗi Godot 4.x sẽ được hỗ trợ lâu dài sau khi 3.x ngừng nhận cập nhật trong tương lai. Một điểm cần lưu ý là nhiều tài liệu của bên thứ ba vẫn chưa được cập nhật cho Godot 4.x. Nếu phải làm theo một hướng dẫn được thiết kế cho Godot 3.x, chúng tôi khuyến nghị tiếp tục giữ
:ref:`doc_upgrading_to_godot_4` open in a separate tab to check which methods
đã được đổi tên (nếu bạn gặp lỗi tập lệnh khi cố gắng sử dụng một node hoặc phương thức cụ thể đã được đổi tên trong Godot 4.x).

Nếu dự án của bạn yêu cầu một tính năng không có trong 4.x (chẳng hạn như GLES2/WebGL 1.0), bạn nên sử dụng Godot 3.x thay thế cho dự án mới.

.. _doc_release_policy_should_i_upgrade_my_project:

Có nên nâng cấp dự án để sử dụng các phiên bản engine mới không?
----------------------------------------------------------------

.. note::

    Nâng cấp phần mềm trong khi đang thực hiện một dự án vốn tiềm ẩn rủi ro, vì vậy hãy cân nhắc liệu đó có phải là lựa chọn phù hợp cho dự án của bạn hay không trước khi thử nâng cấp. Ngoài ra, hãy sao lưu dự án hoặc sử dụng hệ thống quản lý phiên bản để tránh mất dữ liệu nếu quá trình nâng cấp gặp sự cố.

    Dù vậy, chúng tôi luôn cố gắng giữ cho các bản phát hành nhỏ và đặc biệt là các bản phát hành vá tương thích với những dự án hiện có.

Khuyến nghị chung là nâng cấp dự án để theo kịp các bản phát hành *vá* mới, chẳng hạn như nâng cấp từ 4.0.2 lên 4.0.3. Điều này đảm bảo bạn nhận được các bản sửa lỗi, cập nhật bảo mật và cập nhật hỗ trợ nền tảng (điều đặc biệt quan trọng đối với các nền tảng di động). Bạn cũng tiếp tục nhận được hỗ trợ, vì chỉ bản phát hành vá mới nhất được hỗ trợ trên các nền tảng cộng đồng chính thức.

Đối với các bản phát hành *nhỏ*, bạn nên xác định từng trường hợp xem việc nâng cấp có phải là lựa chọn phù hợp hay không. Chúng tôi đã nỗ lực rất nhiều để quy trình nâng cấp liền mạch nhất có thể, nhưng các bản phát hành nhỏ có thể chứa một số thay đổi làm phá vỡ tính tương thích, cùng với nguy cơ hồi quy cao hơn. Một số bản sửa lỗi trong các bản phát hành nhỏ cũng có thể thay đổi cách hoạt động dự kiến của một lớp, như một yêu cầu để sửa một số lỗi. Điều này đặc biệt đúng với các lớp được đánh dấu là *experimental* trong tài liệu.

Các bản phát hành *chính* mang đến nhiều chức năng mới, nhưng cũng loại bỏ những chức năng từng tồn tại và có thể nâng yêu cầu phần cứng. So với các bản phát hành nhỏ, chúng cũng đòi hỏi nhiều công sức hơn để nâng cấp. Do đó, nếu hài lòng với cách dự án hiện đang hoạt động, chúng tôi khuyến nghị tiếp tục sử dụng bản phát hành chính mà bạn đã bắt đầu dự án. Ví dụ, nếu dự án được bắt đầu với 3.5, chúng tôi khuyến nghị nâng cấp lên 3.5.2 và có thể lên 3.6 trong tương lai, nhưng không nâng cấp lên 4.0+, trừ khi dự án của bạn thực sự cần các tính năng mới đi kèm 4.0+.

.. _doc_release_policy_when_is_next_release_out:

Khi nào bản phát hành tiếp theo sẽ ra mắt?
------------------------------------------

.. UPDATE: Đề cập đến các phiên bản nhỏ hiện tại cụ thể là 3.6 và 3.7.

Mặc dù các cộng tác viên Godot không làm việc theo bất kỳ thời hạn nào, chúng tôi cố gắng phát hành các phiên bản nhỏ tương đối thường xuyên.

Cụ thể, sau chu kỳ phát hành rất dài cho 4.0, chúng tôi đang chuyển sang quy trình phát triển với nhịp độ nhanh hơn: 4.1 được phát hành 4 tháng sau 4.0 và 4.2 được phát hành 4 tháng sau 4.1.

Các bản phát hành nhỏ thường xuyên sẽ cho phép chúng tôi phát hành các tính năng mới nhanh hơn (có thể dưới dạng thử nghiệm), nhanh chóng tiếp nhận phản hồi của người dùng và lặp lại để cải thiện các tính năng cũng như khả năng sử dụng của chúng. Tương tự, trải nghiệm người dùng nói chung sẽ được cải thiện ổn định hơn nhờ con đường nhanh hơn đến tay người dùng cuối.

Các bản phát hành bảo trì (bản vá) được phát hành khi cần, với chu kỳ phát triển có thể rất ngắn, nhằm cung cấp cho người dùng nhánh ổn định hiện tại các bản sửa lỗi mới nhất phục vụ nhu cầu sản xuất của họ.

Hiện chưa có ngày phát hành dự kiến cho phiên bản nhỏ tiếp theo của 3.x là 3.7. Bản phát hành ổn định hiện tại, 3.6, có thể là nhánh ổn định cuối cùng của Godot 3.x. Godot 3.x được hỗ trợ trên cơ sở nỗ lực tốt nhất, miễn là các cộng tác viên tiếp tục duy trì nó.

Các tiêu chí để đảm bảo tính tương thích giữa các phiên bản của engine là gì?
-----------------------------------------------------------------------------

.. note::

    Phần này dành cho các cộng tác viên sử dụng để xác định những thay đổi nào là an toàn đối với một bản phát hành nhất định. Danh sách này không đầy đủ; nó chỉ nêu những tình huống phổ biến nhất gặp phải trong quá trình phát triển Godot.

Các thay đổi sau đây được chấp nhận trong các bản phát hành bản vá:

- Sửa một lỗi theo cách không gây ảnh hưởng tiêu cực lớn đến hầu hết dự án, chẳng hạn như lỗi hiển thị hoặc lỗi vật lý. Engine vật lý của Godot không mang tính tất định, vì vậy các bản sửa lỗi vật lý không được xem là phá vỡ tính tương thích. Nếu việc sửa lỗi gây ảnh hưởng tiêu cực có thể tác động đến nhiều dự án, thì thay đổi đó nên được cung cấp dưới dạng tùy chọn (ví dụ: sử dụng thiết lập dự án hoặc phương thức riêng). - Thêm một tham số tùy chọn mới vào một phương thức. - Những tinh chỉnh nhỏ về khả năng sử dụng của trình chỉnh sửa.

Lưu ý rằng chúng tôi có xu hướng thận trọng hơn với các bản sửa lỗi được cho phép trong mỗi bản phát hành bản vá tiếp theo. Ví dụ, 4.0.1 có thể nhận các bản sửa lỗi có ảnh hưởng lớn hơn so với 4.0.4.

Các thay đổi sau đây được chấp nhận trong các bản phát hành nhỏ, nhưng không được chấp nhận trong các bản phát hành bản vá:

- Các tính năng mới đáng kể. - Đổi tên tham số của một phương thức. Trong C#, các tham số của phương thức có thể được truyền theo tên (nhưng không thể làm vậy trong GDScript). Do đó, điều này có thể phá vỡ một số dự án sử dụng C#. - Đánh dấu một phương thức, biến thành viên hoặc lớp là không còn được khuyến nghị. Việc này được thực hiện bằng cách thêm cờ deprecated vào tham chiếu lớp của nó; cờ này sẽ hiển thị trong trình chỉnh sửa. Khi một phương thức được đánh dấu là không còn được khuyến nghị, phương thức đó dự kiến sẽ bị xóa trong bản phát hành *chính* tiếp theo. - Các thay đổi ảnh hưởng đến hình ảnh của theme dự án mặc định. - Các bản sửa lỗi làm thay đổi đáng kể hành vi hoặc đầu ra, với mục tiêu đáp ứng tốt hơn kỳ vọng của người dùng. Ngược lại, trong các bản phát hành bản vá, chúng tôi có thể ưu tiên giữ lại hành vi bị lỗi để không phá vỡ các dự án hiện có vốn có thể đã phụ thuộc vào lỗi đó hoặc sử dụng một cách khắc phục tạm thời. - Các tối ưu hóa hiệu năng dẫn đến thay đổi về hình ảnh.

Các thay đổi sau đây được xem là **phá vỡ tính tương thích** và chỉ có thể được thực hiện trong một bản phát hành chính mới:

- Đổi tên hoặc xóa một phương thức, biến thành viên hoặc lớp. - Sửa đổi cây kế thừa của một node bằng cách cho node đó kế thừa từ một lớp khác. - Thay đổi giá trị mặc định của một giá trị thiết lập dự án theo cách ảnh hưởng đến các dự án hiện có. Để chỉ ảnh hưởng đến các dự án mới, trình quản lý dự án nên ghi một ``project.godot`` đã được sửa đổi thay vào đó.

Vì Godot 5.0 vẫn chưa được tách thành nhánh, hiện tại chúng tôi không khuyến khích thực hiện các thay đổi phá vỡ tính tương thích thuộc loại này.

.. note::

      Khi sửa đổi chữ ký của một phương thức theo bất kỳ cách nào (bao gồm thêm một tham số tùy chọn), phải tạo một phương thức tương thích GDExtension. Điều này đảm bảo các GDExtension hiện có tiếp tục hoạt động giữa các bản phát hành bản vá và bản phát hành nhỏ, để người dùng không phải biên dịch lại chúng. Xem :ref:`doc_handling_compatibility_breakages` để biết thêm thông tin.
