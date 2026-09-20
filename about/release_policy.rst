:allow_comments: False

.. _doc_release_policy:

Chính sách phát hành Godot
==========================

Chính sách phát hành của Godot không ngừng phát triển. Phần mô tả dưới đây cung cấp một hình dung tổng quát về những gì có thể mong đợi, nhưng điều thực sự xảy ra sẽ phụ thuộc vào các lựa chọn của những người đóng góp cốt lõi và nhu cầu của cộng đồng tại từng thời điểm.

Quản lý phiên bản Godot
-----------------------

Godot phần nào tuân theo `Semantic Versioning <https://semver.org/>`__ với hệ thống quản lý phiên bản ``major.minor.patch``, mặc dù cách diễn giải từng thuật ngữ được điều chỉnh cho phù hợp với độ phức tạp của một game engine:

- Phiên bản ``major`` được tăng lên khi xảy ra những thay đổi lớn làm phá vỡ tính tương thích, đòi hỏi nhiều công việc chuyển đổi để chuyển các project từ phiên bản lớn này sang phiên bản lớn khác.

  Ví dụ, việc chuyển các project Godot từ Godot 3.x sang Godot 4.x yêu cầu chạy project qua một công cụ chuyển đổi, sau đó thực hiện thủ công một số điều chỉnh khác đối với những phần mà công cụ không thể tự động xử lý.

- Phiên bản ``minor`` được tăng lên đối với các bản phát hành tính năng không phá vỡ tính tương thích theo cách nghiêm trọng. Các phiên bản minor *có thể* gây ra những thay đổi nhỏ làm phá vỡ tính tương thích trong một số lĩnh vực rất cụ thể, nhưng phần lớn project sẽ không bị ảnh hưởng hoặc không cần nhiều công việc chuyển đổi.

  Điều này là do Godot, với tư cách là một game engine, bao quát nhiều lĩnh vực như rendering, physics và scripting. Việc sửa lỗi hoặc triển khai tính năng mới trong một lĩnh vực đôi khi có thể yêu cầu thay đổi hành vi của một tính năng hoặc sửa đổi interface của một class, ngay cả khi API của phần còn lại của engine vẫn tương thích ngược.

.. tip::

    Tất cả người dùng đều được khuyến nghị nâng cấp lên phiên bản minor mới, nhưng cần thực hiện một số kiểm thử để đảm bảo project vẫn hoạt động như mong đợi.

- Phiên bản ``patch`` được tăng lên đối với các bản phát hành bảo trì, tập trung vào việc sửa lỗi và vấn đề bảo mật, triển khai các yêu cầu mới để hỗ trợ nền tảng, cũng như backport các cải tiến an toàn về khả năng sử dụng. Các bản phát hành patch tương thích ngược.

  Các phiên bản patch có thể bao gồm những tính năng mới nhỏ không ảnh hưởng đến API hiện có, do đó không có nguy cơ ảnh hưởng đến các project hiện có.

.. tip::

    Vì vậy, việc cập nhật lên các phiên bản patch mới được xem là an toàn và được đặc biệt khuyến nghị cho tất cả người dùng của một stable branch nhất định.

Chúng tôi gọi các tổ hợp ``major.minor`` là *stable branch*. Mỗi stable branch bắt đầu bằng một bản phát hành ``major.minor`` (không có ``0`` cho ``patch``) và tiếp tục được phát triển cho các bản phát hành bảo trì trong một Git branch có cùng tên (ví dụ: các bản cập nhật patch cho stable branch 4.0 được phát triển trong Git branch ``4.0``).

Lộ trình hỗ trợ các bản phát hành
---------------------------------

.. UPDATE: Bảng thay đổi sau mỗi phiên bản minor. Chính sách hỗ trợ có thể thay đổi.

Các stable branch được hỗ trợ *ít nhất* cho đến khi stable branch tiếp theo được phát hành và nhận bản cập nhật patch đầu tiên. Trên thực tế, chúng tôi hỗ trợ các stable branch trên cơ sở *nỗ lực tốt nhất* trong chừng nào vẫn còn người dùng đang hoạt động cần các bản cập nhật bảo trì.

Mỗi khi một phiên bản major mới được phát hành, chúng tôi biến stable branch trước đó thành một bản phát hành được hỗ trợ dài hạn và cố gắng hết sức để cung cấp các bản sửa lỗi cho những vấn đề mà người dùng của branch đó gặp phải nhưng không thể chuyển các project phức tạp sang phiên bản major mới. Đây là trường hợp của branch 2.1 và cũng là trường hợp của branch 3.x.

Trong một chuỗi bản phát hành minor nhất định, chỉ bản phát hành patch mới nhất nhận được hỗ trợ. Nếu gặp vấn đề khi sử dụng một bản phát hành patch cũ hơn, vui lòng nâng cấp lên bản phát hành patch mới nhất của chuỗi đó và kiểm thử lại trước khi báo cáo vấn đề trên GitHub.

+--------------+----------------------+--------------------------------------------------------------------------+
| **Version**  | **Release date**     | **Support level**                                                        |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.8    | Q4 2026 (estimate)   | |unstable| *Development.* Receives new features, usability and           |
| (`master`)   |                      | performance improvements, as well as bug fixes, while under development. |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.7    | June 2026            | |supported| Receives fixes for bugs and security issues, as well as      |
|              |                      | patches that enable platform support.                                    |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.6    | January 2026         | |supported| Receives fixes for bugs and security issues, as well as      |
|              |                      | patches that enable platform support.                                    |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.5    | September 2025       | |partial| Receives fixes for security and platform support issues only.  |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.4    | March 2025           | |eol| No longer supported (last update: 4.4.1).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.3    | August 2024          | |eol| No longer supported (last update: 4.3).                            |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.2    | November 2023        | |eol| No longer supported (last update: 4.2.2).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.1    | July 2023            | |eol| No longer supported (last update: 4.1.4).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 4.0    | March 2023           | |eol| No longer supported (last update: 4.0.4).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.7    | No ETA for now       | |supported| *Beta.* Receives new features, usability and performance     |
| (`3.x`)      |                      | improvements, as well as bug fixes, while under development.             |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.6    | September 2024       | |supported| Receives fixes for bugs and security issues, as well as      |
|              |                      | patches that enable platform support.                                    |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.5    | August 2022          | |eol| No longer supported (last update: 3.5.3).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.4    | November 2021        | |eol| No longer supported (last update: 3.4.5).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.3    | April 2021           | |eol| No longer supported (last update: 3.3.4).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.2    | January 2020         | |eol| No longer supported (last update: 3.2.3).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.1    | March 2019           | |eol| No longer supported (last update: 3.1.2).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 3.0    | January 2018         | |eol| No longer supported (last update: 3.0.6).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 2.1    | July 2016            | |eol| No longer supported (last update: 2.1.6).                          |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 2.0    | February 2016        | |eol| No longer supported (last update: 2.0.4.1).                        |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 1.1    | May 2015             | |eol| No longer supported.                                               |
+--------------+----------------------+--------------------------------------------------------------------------+
| Godot 1.0    | December 2014        | |eol| No longer supported.                                               |
+--------------+----------------------+--------------------------------------------------------------------------+

.. |supported| image:: img/supported.png
.. |partial| image:: img/partial.png
.. |eol| image:: img/eol.png
.. |unstable| image:: img/unstable.png

**Chú giải:** |supported| Hỗ trợ đầy đủ – |partial| Hỗ trợ một phần – |eol| Không hỗ trợ (end of life) – |unstable| Phiên bản đang phát triển

Các phiên bản Godot pre-release không nhằm mục đích sử dụng trong môi trường production và chỉ được cung cấp cho mục đích kiểm thử.

.. seealso::

    Xem :ref:`doc_upgrading_to_godot_4` để biết hướng dẫn chuyển một project từ Godot 3.x sang 4.x.

.. _doc_release_policy_which_version_should_i_use:

Tôi nên sử dụng phiên bản nào cho một project mới?
--------------------------------------------------

Chúng tôi khuyến nghị sử dụng Godot 4.x cho các project mới, vì chuỗi Godot 4.x sẽ được hỗ trợ lâu dài sau khi 3.x ngừng nhận các bản cập nhật trong tương lai. Một điểm cần lưu ý là nhiều tài liệu của bên thứ ba vẫn chưa được cập nhật cho Godot 4.x. Nếu phải làm theo một tutorial được thiết kế cho Godot 3.x, chúng tôi khuyến nghị tiếp tục
:ref:`doc_upgrading_to_godot_4` open in a separate tab to check which methods
đã được đổi tên (nếu bạn gặp lỗi script khi cố sử dụng một node hoặc method cụ thể đã được đổi tên trong Godot 4.x).

Nếu project của bạn yêu cầu một tính năng bị thiếu trong 4.x (chẳng hạn như GLES2/WebGL 1.0), bạn nên sử dụng Godot 3.x cho project mới.

.. _doc_release_policy_should_i_upgrade_my_project:

Tôi có nên nâng cấp project để sử dụng các phiên bản engine mới không?
----------------------------------------------------------------------

.. note::

    Việc nâng cấp software trong khi đang thực hiện một project vốn tiềm ẩn rủi ro, vì vậy hãy cân nhắc xem đó có phải là lựa chọn phù hợp cho project của bạn hay không trước khi bắt đầu nâng cấp. Ngoài ra, hãy sao lưu project hoặc sử dụng version control để tránh mất dữ liệu nếu quá trình nâng cấp gặp lỗi.

    Tuy vậy, chúng tôi cố gắng hết sức để giữ cho các bản phát hành minor và đặc biệt là patch tương thích với các project hiện có.

Khuyến nghị chung là nâng cấp project để theo kịp các bản phát hành *patch* mới, chẳng hạn như nâng cấp từ 4.0.2 lên 4.0.3. Điều này đảm bảo bạn nhận được các bản sửa lỗi, cập nhật bảo mật và cập nhật hỗ trợ nền tảng (điều đặc biệt quan trọng đối với các nền tảng mobile). Bạn cũng tiếp tục nhận được hỗ trợ, vì chỉ bản phát hành patch mới nhất nhận được hỗ trợ trên các nền tảng cộng đồng chính thức.

Đối với các bản phát hành *minor*, bạn nên quyết định có nên nâng cấp hay không tùy từng trường hợp. Chúng tôi đã nỗ lực rất nhiều để quá trình nâng cấp liền mạch nhất có thể, nhưng các bản phát hành minor có thể chứa một số thay đổi làm phá vỡ tính tương thích, đồng thời có nguy cơ regression cao hơn. Một số bản sửa lỗi được đưa vào các bản phát hành minor cũng có thể thay đổi hành vi dự kiến của một class để sửa một số lỗi nhất định. Điều này đặc biệt đúng với các class được đánh dấu là *experimental* trong tài liệu.

Các bản phát hành *major* mang đến nhiều chức năng mới, nhưng cũng loại bỏ những chức năng đã tồn tại trước đó và có thể nâng yêu cầu phần cứng. So với các bản phát hành minor, chúng cũng đòi hỏi nhiều công sức hơn để nâng cấp. Do đó, nếu hài lòng với cách project hiện đang hoạt động, chúng tôi khuyến nghị tiếp tục sử dụng bản phát hành major mà bạn đã bắt đầu project cùng. Ví dụ, nếu project của bạn bắt đầu với 3.5, chúng tôi khuyến nghị nâng cấp lên 3.5.2 và có thể lên 3.6 trong tương lai, nhưng không nên nâng cấp lên 4.0+, trừ khi project thực sự cần các tính năng mới đi kèm với 4.0+.

.. _doc_release_policy_when_is_next_release_out:

Khi nào bản phát hành tiếp theo sẽ ra mắt?
------------------------------------------

.. UPDATE: Đề cập đến các phiên bản minor hiện tại cụ thể là 3.6 và 3.7.

Mặc dù những người đóng góp cho Godot không làm việc theo bất kỳ thời hạn nào, chúng tôi cố gắng phát hành các bản phát hành minor tương đối thường xuyên.

Cụ thể, sau chu kỳ phát hành rất dài của 4.0, chúng tôi đang chuyển sang quy trình phát triển với nhịp độ nhanh hơn: 4.1 được phát hành 4 tháng sau 4.0 và 4.2 được phát hành 4 tháng sau 4.1.

Các bản phát hành minor thường xuyên sẽ giúp chúng tôi phát hành tính năng mới nhanh hơn (có thể dưới dạng experimental), nhanh chóng nhận phản hồi từ người dùng và lặp lại để cải thiện các tính năng cũng như khả năng sử dụng của chúng. Tương tự, trải nghiệm người dùng nói chung sẽ được cải thiện đều đặn hơn nhờ con đường nhanh hơn đến tay người dùng cuối.

Các bản phát hành bảo trì (patch) được phát hành khi cần, với chu kỳ phát triển có thể rất ngắn, nhằm cung cấp cho người dùng của stable branch hiện tại những bản sửa lỗi mới nhất phục vụ nhu cầu production của họ.

Hiện chưa có ngày phát hành dự kiến cho phiên bản minor 3.x tiếp theo, 3.7. Bản phát hành stable hiện tại, 3.6, có thể là stable branch cuối cùng của Godot 3.x. Godot 3.x được hỗ trợ trên cơ sở nỗ lực tốt nhất, chừng nào những người đóng góp vẫn tiếp tục duy trì nó.

Tiêu chí tương thích giữa các phiên bản engine là gì?
-----------------------------------------------------

.. note::

    Phần này dành cho những người đóng góp, nhằm xác định những thay đổi nào là an toàn đối với một bản phát hành nhất định. Danh sách này không đầy đủ; nó chỉ nêu những tình huống phổ biến nhất gặp phải trong quá trình phát triển Godot.

Các thay đổi sau đây được chấp nhận trong các bản phát hành patch:

- Sửa lỗi theo cách không gây tác động tiêu cực nghiêm trọng đến phần lớn project, chẳng hạn như lỗi hình ảnh hoặc physics. Physics engine của Godot không mang tính deterministic, vì vậy các bản sửa lỗi physics không được xem là phá vỡ tính tương thích. Nếu việc sửa lỗi gây ra tác động tiêu cực có thể ảnh hưởng đến nhiều project, thay đổi đó nên được đặt thành tùy chọn (ví dụ: sử dụng project setting hoặc method riêng). - Thêm một parameter tùy chọn mới vào một method. - Những điều chỉnh nhỏ về khả năng sử dụng của editor.

Lưu ý rằng chúng tôi có xu hướng thận trọng hơn với các bản sửa lỗi được cho phép trong mỗi bản phát hành patch tiếp theo. Chẳng hạn, 4.0.1 có thể nhận các bản sửa lỗi có tác động lớn hơn so với 4.0.4.

Các thay đổi sau đây được chấp nhận trong các bản phát hành minor nhưng không được chấp nhận trong các bản phát hành patch:

- Các tính năng mới quan trọng. - Đổi tên một tham số của method. Trong C#, các tham số của method có thể được truyền theo tên (nhưng không thể làm vậy trong GDScript). Do đó, việc này có thể làm hỏng một số project sử dụng C#. - Đánh dấu một method, member variable hoặc class là deprecated. Việc này được thực hiện bằng cách thêm cờ deprecated vào tham chiếu class của nó, và cờ này sẽ hiển thị trong editor. Khi một method được đánh dấu là deprecated, method đó dự kiến sẽ bị xóa trong bản phát hành *major* tiếp theo. - Các thay đổi ảnh hưởng đến giao diện trực quan của theme project mặc định. - Các bản sửa lỗi làm thay đổi đáng kể hành vi hoặc đầu ra, nhằm đáp ứng tốt hơn kỳ vọng của người dùng. Ngược lại, trong các bản phát hành patch, chúng tôi có thể ưu tiên giữ nguyên hành vi có lỗi để không làm hỏng các project hiện có, vốn có thể đã phụ thuộc vào lỗi đó hoặc sử dụng một workaround. - Các tối ưu hóa hiệu năng dẫn đến thay đổi về mặt hình ảnh.

Các thay đổi sau đây được xem là **phá vỡ khả năng tương thích** và chỉ có thể được thực hiện trong một bản phát hành major mới:

- Đổi tên hoặc xóa một method, member variable hoặc class. - Sửa đổi cây kế thừa của một node bằng cách cho node đó kế thừa từ một class khác. - Thay đổi giá trị mặc định của một project setting theo cách ảnh hưởng đến các project hiện có. Để chỉ ảnh hưởng đến các project mới, project manager nên ghi một ``project.godot`` đã sửa đổi thay thế.

Vì Godot 5.0 vẫn chưa được tách thành một branch, hiện tại chúng tôi không khuyến khích thực hiện các thay đổi phá vỡ khả năng tương thích thuộc loại này.

.. note::

      Khi sửa đổi signature của một method theo bất kỳ cách nào (bao gồm cả việc thêm một parameter tùy chọn), phải tạo một method tương thích với GDExtension. Điều này đảm bảo các GDExtension hiện có tiếp tục hoạt động giữa các bản phát hành patch và minor, để người dùng không phải biên dịch lại chúng. Xem :ref:`doc_handling_compatibility_breakages` để biết thêm thông tin.
