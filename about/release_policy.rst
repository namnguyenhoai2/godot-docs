:allow_comments: False

.. _doc_release_policy:

Chính sách phát hành Godot
==========================

Chính sách phát hành của Godot không ngừng được hoàn thiện. Phần mô tả dưới đây cung cấp ý tưởng khái quát về những gì có thể mong đợi, nhưng điều thực sự diễn ra sẽ phụ thuộc vào các quyết định của những người đóng góp cốt lõi và nhu cầu của cộng đồng tại từng thời điểm.

Đánh số phiên bản Godot
-----------------------

Godot tuân theo `Semantic Versioning <https://semver.org/>`__ ở mức tương đối, với hệ thống đánh số phiên bản ``major.minor.patch``, dù cách diễn giải từng thuật ngữ được điều chỉnh cho phù hợp với độ phức tạp của một game engine:

- Phiên bản ``major`` được tăng lên khi xảy ra những thay đổi lớn làm phá vỡ khả năng tương thích, đòi hỏi nhiều công việc chuyển đổi để chuyển dự án từ phiên bản chính này sang phiên bản chính khác.

  Ví dụ, để chuyển các dự án Godot từ Godot 3.x sang Godot 4.x, bạn cần chạy dự án qua một công cụ chuyển đổi, sau đó thực hiện thủ công một số điều chỉnh bổ sung đối với những việc mà công cụ không thể tự động thực hiện.

- Phiên bản ``minor`` được tăng lên đối với các bản phát hành tính năng không phá vỡ khả năng tương thích theo cách nghiêm trọng. Những phá vỡ nhỏ về khả năng tương thích trong các lĩnh vực rất cụ thể *có thể* xảy ra ở các phiên bản phụ, nhưng phần lớn dự án sẽ không bị ảnh hưởng hoặc không cần thực hiện nhiều công việc chuyển đổi.

  Điều này là do Godot, với vai trò là một game engine, bao quát nhiều lĩnh vực như kết xuất, vật lý và scripting. Việc sửa lỗi hoặc triển khai tính năng mới trong một lĩnh vực đôi khi có thể yêu cầu thay đổi hành vi của một tính năng hoặc sửa đổi interface của một class, ngay cả khi API của phần còn lại của engine vẫn tương thích ngược.

.. tip::

    Tất cả người dùng đều nên nâng cấp lên phiên bản phụ mới, nhưng cần thực hiện một số kiểm thử để đảm bảo dự án vẫn hoạt động như mong đợi.

- Phiên bản ``patch`` được tăng lên đối với các bản phát hành bảo trì, tập trung vào việc sửa lỗi và vấn đề bảo mật, triển khai các yêu cầu mới để hỗ trợ nền tảng, cũng như backport các cải tiến an toàn về khả năng sử dụng. Các bản phát hành patch tương thích ngược.

  Các phiên bản patch có thể bao gồm những tính năng mới nhỏ không ảnh hưởng đến API hiện có, do đó không có nguy cơ ảnh hưởng đến các dự án hiện có.

.. tip::

    Vì vậy, việc cập nhật lên các phiên bản patch mới được xem là an toàn và được đặc biệt khuyến nghị cho tất cả người dùng của một stable branch nhất định.

Chúng tôi gọi các tổ hợp ``major.minor`` phiên bản *nhánh ổn định*. Mỗi nhánh ổn định bắt đầu bằng một bản phát hành ``major.minor`` (không có ``0`` đối với ``patch``) và tiếp tục được phát triển cho các bản phát hành bảo trì trong một Git branch cùng tên (ví dụ: các bản cập nhật patch cho stable branch 4.0 được phát triển trong ``4.0`` Git branch).

Lộ trình hỗ trợ các bản phát hành
---------------------------------

.. UPDATE: Table changes every minor version. Support policy may change.

Các stable branch được hỗ trợ *ít nhất* cho đến khi stable branch tiếp theo được phát hành và nhận bản cập nhật patch đầu tiên. Trên thực tế, chúng tôi hỗ trợ các stable branch theo nguyên tắc *cố gắng hết sức* miễn là vẫn có người dùng đang hoạt động cần các bản cập nhật bảo trì.

Mỗi khi một phiên bản chính mới được phát hành, chúng tôi biến stable branch trước đó thành một bản phát hành được hỗ trợ dài hạn và cố gắng hết sức để cung cấp bản sửa lỗi cho các vấn đề mà người dùng của nhánh đó gặp phải nhưng không thể chuyển các dự án phức tạp sang phiên bản chính mới. Điều này đã xảy ra với branch 2.1 và cũng đang xảy ra với branch 3.x.

Trong một chuỗi phát hành phiên bản phụ nhất định, chỉ bản phát hành patch mới nhất nhận được hỗ trợ. Nếu bạn gặp sự cố khi sử dụng bản phát hành patch cũ hơn, hãy nâng cấp lên bản phát hành patch mới nhất của chuỗi đó và kiểm thử lại trước khi báo cáo sự cố trên GitHub.

+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| **Phiên bản**        | **Ngày phát hành**             | **Mức độ hỗ trợ**                                                                                                                                 |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.8 (`master`) | Quý 4 năm 2026 (ước tính)      | |unstable| *Đang phát triển.* Nhận các tính năng mới, cải tiến về khả năng sử dụng và hiệu năng, cũng như bản sửa lỗi trong thời gian phát triển. |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.7            | Tháng 6 năm 2026               | |supported| Nhận bản sửa lỗi và vấn đề bảo mật, cũng như các bản vá cho phép hỗ trợ nền tảng.                                                     |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.6            | Tháng 1 năm 2026               | |supported| Nhận bản sửa lỗi và vấn đề bảo mật, cũng như các bản vá cho phép hỗ trợ nền tảng.                                                     |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.5            | Tháng 9 năm 2025               | |partial| Chỉ nhận bản sửa lỗi cho các vấn đề bảo mật và hỗ trợ nền tảng.                                                                         |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.4            | Tháng 3 năm 2025               | |eol| Không còn được hỗ trợ (bản cập nhật cuối: 4.4.1).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.3            | Tháng 8 năm 2024               | |eol| Không còn được hỗ trợ (bản cập nhật cuối: 4.3).                                                                                             |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.2            | Tháng 11 năm 2023              | |eol| Không còn được hỗ trợ (bản cập nhật cuối: 4.2.2).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.1            | Tháng 7 năm 2023               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 4.1.4).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 4.0            | Tháng 3 năm 2023               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 4.0.4).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.7 (`3.x`)    | Hiện chưa có thời gian dự kiến | |supported| *Beta.* Nhận các tính năng mới, cải thiện khả năng sử dụng và hiệu suất, cũng như các bản sửa lỗi trong quá trình phát triển.         |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.6            | Tháng 9 năm 2024               | |supported| Nhận các bản sửa lỗi và bản vá cho vấn đề bảo mật, cũng như các bản vá cho phép hỗ trợ nền tảng.                                      |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.5            | Tháng 8 năm 2022               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 3.5.3).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.4            | Tháng 11 năm 2021              | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 3.4.5).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.3            | Tháng 4 năm 2021               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 3.3.4).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.2            | Tháng 1 năm 2020               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 3.2.3).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.1            | Tháng 3 năm 2019               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 3.1.2).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 3.0            | Tháng 1 năm 2018               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 3.0.6).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 2.1            | Tháng 7 năm 2016               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 2.1.6).                                                                                           |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 2.0            | Tháng 2 năm 2016               | |eol| Không còn được hỗ trợ (cập nhật lần cuối: 2.0.4.1).                                                                                         |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 1.1            | Tháng 5 năm 2015               | |eol| Không còn được hỗ trợ.                                                                                                                      |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Godot 1.0            | Tháng 12 năm 2014              | |eol| Không còn được hỗ trợ.                                                                                                                      |
+----------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. |supported| image:: img/supported.png
.. |partial| image:: img/partial.png
.. |eol| image:: img/eol.png
.. |unstable| image:: img/unstable.png

**Chú giải:** |supported| Hỗ trợ đầy đủ – |partial| Hỗ trợ một phần – |eol| Không hỗ trợ (đã hết vòng đời) – |unstable| Phiên bản đang phát triển

Các phiên bản Godot tiền phát hành không nhằm mục đích sử dụng trong môi trường production và chỉ được cung cấp cho mục đích kiểm thử.

.. seealso::

    Xem :ref:`doc_upgrading_to_godot_4` để biết hướng dẫn di chuyển một project từ Godot 3.x sang 4.x.

.. _doc_release_policy_which_version_should_i_use:

Tôi nên sử dụng phiên bản nào cho một project mới?
--------------------------------------------------

Chúng tôi khuyến nghị sử dụng Godot 4.x cho các project mới, vì dòng Godot 4.x sẽ tiếp tục được hỗ trợ trong thời gian dài sau khi 3.x ngừng nhận các bản cập nhật trong tương lai. Một điểm cần lưu ý là nhiều tài liệu của bên thứ ba vẫn chưa được cập nhật cho Godot 4.x. Nếu phải làm theo một tutorial được thiết kế cho Godot 3.x, chúng tôi khuyến nghị giữ
:ref:`doc_upgrading_to_godot_4` mở trong một tab riêng để kiểm tra những method nào đã được đổi tên (nếu bạn gặp lỗi script khi cố sử dụng một node hoặc method cụ thể đã được đổi tên trong Godot 4.x).

Nếu project của bạn yêu cầu một tính năng chưa có trong 4.x (chẳng hạn như GLES2/WebGL 1.0), bạn nên sử dụng Godot 3.x cho project mới.

.. _doc_release_policy_should_i_upgrade_my_project:

Tôi có nên nâng cấp project để sử dụng các phiên bản engine mới không?
----------------------------------------------------------------------

.. note::

    Việc nâng cấp phần mềm trong khi đang làm việc trên một project vốn tiềm ẩn rủi ro, vì vậy hãy cân nhắc xem đó có phải là ý tưởng phù hợp cho project của bạn hay không trước khi thực hiện một
    upgrade. Ngoài ra, hãy tạo bản sao lưu cho project hoặc sử dụng version control để
    tránh mất dữ liệu trong trường hợp quá trình nâng cấp gặp lỗi.

    Tuy vậy, chúng tôi luôn cố gắng hết sức để giữ cho các bản phát hành minor và đặc biệt là patch tương thích với các project hiện có.

Khuyến nghị chung là nâng cấp project để sử dụng các bản phát hành *patch* mới, chẳng hạn như nâng cấp từ 4.0.2 lên 4.0.3. Điều này đảm bảo bạn nhận được các bản sửa lỗi, bản cập nhật bảo mật và bản cập nhật hỗ trợ nền tảng (điều đặc biệt quan trọng đối với các nền tảng di động). Bạn cũng tiếp tục nhận được hỗ trợ, vì chỉ bản phát hành patch mới nhất được hỗ trợ trên các nền tảng cộng đồng chính thức.

Đối với các bản phát hành *minor*, bạn nên xác định xem nâng cấp có phải là lựa chọn phù hợp hay không trong từng trường hợp cụ thể. Chúng tôi đã nỗ lực rất nhiều để quy trình nâng cấp diễn ra liền mạch nhất có thể, nhưng các bản phát hành minor có thể chứa một số thay đổi gây lỗi tương thích, cùng với nguy cơ hồi quy cao hơn. Một số bản sửa lỗi trong các bản phát hành minor cũng có thể thay đổi hành vi dự kiến của một class để sửa một số lỗi. Điều này đặc biệt đúng với các class được đánh dấu là *experimental* trong tài liệu.

Các bản phát hành *Major* mang đến nhiều chức năng mới, nhưng cũng loại bỏ các chức năng đã tồn tại trước đó và có thể làm tăng yêu cầu phần cứng. So với các bản phát hành minor, chúng cũng đòi hỏi nhiều công sức hơn để nâng cấp. Do đó, chúng tôi khuyến nghị bạn tiếp tục sử dụng bản phát hành major mà bạn đã bắt đầu project nếu hài lòng với cách project hiện hoạt động. Ví dụ: nếu project của bạn được bắt đầu với 3.5, chúng tôi khuyến nghị nâng cấp lên 3.5.2 và có thể lên 3.6 trong tương lai, nhưng không nên nâng cấp lên 4.0+, trừ khi project của bạn thực sự cần các tính năng mới đi kèm với 4.0+.

.. _doc_release_policy_when_is_next_release_out:

Bản phát hành tiếp theo sẽ ra mắt khi nào?
------------------------------------------

.. UPDATE: Refers to specific current minor versions 3.6 and 3.7.

Mặc dù những người đóng góp cho Godot không làm việc theo bất kỳ thời hạn nào, chúng tôi vẫn cố gắng phát hành các bản phát hành minor tương đối thường xuyên.

Cụ thể, sau chu kỳ phát hành rất dài của 4.0, chúng tôi đang chuyển sang quy trình phát triển với nhịp độ nhanh hơn: 4.1 được phát hành 4 tháng sau 4.0, và 4.2 được phát hành 4 tháng sau 4.1.

Các bản phát hành minor thường xuyên sẽ giúp chúng tôi phát hành tính năng mới nhanh hơn (có thể dưới dạng experimental), nhanh chóng nhận phản hồi từ người dùng và lặp lại để cải thiện các tính năng đó cũng như khả năng sử dụng của chúng. Tương tự, trải nghiệm người dùng nói chung sẽ được cải thiện ổn định hơn nhờ con đường nhanh hơn đến tay người dùng cuối.

Các bản phát hành bảo trì (patch) được phát hành khi cần, với các chu kỳ phát triển có thể rất ngắn, nhằm cung cấp cho người dùng của branch ổn định hiện tại những bản sửa lỗi mới nhất phục vụ nhu cầu production của họ.

Hiện chưa có ngày phát hành dự kiến cho phiên bản minor 3.x tiếp theo, 3.7. Bản phát hành ổn định hiện tại, 3.6, có thể là branch ổn định cuối cùng của Godot 3.x. Godot 3.x được hỗ trợ trên cơ sở nỗ lực tốt nhất, miễn là những người đóng góp vẫn tiếp tục duy trì nó.

Tiêu chí tương thích giữa các phiên bản engine là gì?
-----------------------------------------------------

.. note::

    Phần này dành cho những người đóng góp sử dụng để xác định thay đổi nào là an toàn đối với một bản phát hành nhất định. Danh sách này không đầy đủ; nó chỉ nêu ra những tình huống phổ biến nhất gặp phải trong quá trình phát triển Godot.

Các thay đổi sau đây được chấp nhận trong các bản phát hành patch:

- Sửa lỗi theo cách không gây ảnh hưởng tiêu cực đáng kể đến phần lớn project, chẳng hạn như lỗi hiển thị hoặc lỗi physics. Engine physics của Godot không mang tính deterministic, vì vậy các bản sửa lỗi physics không được xem là phá vỡ tính tương thích. Nếu việc sửa lỗi có ảnh hưởng tiêu cực đến nhiều project, thay đổi đó nên được đặt ở dạng tùy chọn (ví dụ: sử dụng project setting hoặc method riêng).
- Thêm một parameter tùy chọn mới vào một method.
- Các tinh chỉnh nhỏ về khả năng sử dụng của editor.

Lưu ý rằng chúng tôi có xu hướng thận trọng hơn với các bản sửa lỗi được cho phép trong mỗi bản phát hành patch tiếp theo. Chẳng hạn, 4.0.1 có thể nhận được các bản sửa lỗi có tác động lớn hơn so với 4.0.4.

Các thay đổi sau đây được chấp nhận trong các bản phát hành minor, nhưng không được chấp nhận trong các bản phát hành patch:

- Các tính năng mới đáng kể.
- Đổi tên parameter của một method. Trong C#, parameter của method có thể được truyền theo tên (nhưng không thể làm vậy trong GDScript). Do đó, điều này có thể làm hỏng một số project sử dụng C#.
- Đánh dấu một method, member variable hoặc class là deprecated. Việc này được thực hiện bằng cách thêm cờ deprecated vào class reference của nó; cờ này sẽ hiển thị trong editor. Khi một method được đánh dấu là deprecated, method đó dự kiến sẽ bị xóa trong bản phát hành *major* tiếp theo.
- Các thay đổi ảnh hưởng đến giao diện trực quan của theme project mặc định.
- Các bản sửa lỗi làm thay đổi đáng kể hành vi hoặc output, nhằm đáp ứng tốt hơn kỳ vọng của người dùng. Ngược lại, trong các bản phát hành patch, chúng tôi có thể ưu tiên giữ lại hành vi lỗi để không làm hỏng các project hiện có vốn có thể đã phụ thuộc vào lỗi đó hoặc sử dụng một workaround.
- Các tối ưu hóa hiệu năng dẫn đến thay đổi về hiển thị.

Các thay đổi sau đây được xem là **compatibility-breaking** và chỉ có thể được thực hiện trong một bản phát hành major mới:

- Đổi tên hoặc xóa một method, member variable hoặc class.
- Thay đổi cây kế thừa của một node bằng cách cho node đó kế thừa từ một class khác.
- Thay đổi giá trị mặc định của một project setting theo cách ảnh hưởng đến các project hiện có
  projects. Để chỉ ảnh hưởng đến các project mới, project manager nên ghi một
  modified ``project.godot`` thay thế.

Vì Godot 5.0 vẫn chưa được tách branch, hiện tại chúng tôi không khuyến khích thực hiện các thay đổi kiểu này làm phá vỡ tính tương thích.

.. note::

      Khi sửa signature của một method dưới bất kỳ hình thức nào (bao gồm cả việc thêm parameter tùy chọn), phải tạo một method tương thích GDExtension. Điều này đảm bảo các GDExtension hiện có tiếp tục hoạt động xuyên suốt các bản phát hành patch và minor, để người dùng không phải biên dịch lại chúng. Xem :ref:`doc_handling_compatibility_breakages` để biết thêm thông tin.
