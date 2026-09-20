.. _doc_using_sdfgi:

Chiếu sáng toàn cục bằng trường khoảng cách có dấu (SDFGI)
==========================================================

Chiếu sáng toàn cục bằng trường khoảng cách có dấu (SDFGI) là một kỹ thuật mới có trong Godot. Kỹ thuật này cung cấp khả năng chiếu sáng toàn cục bán thời gian thực, có thể mở rộng cho mọi kích thước thế giới và hoạt động với các level được tạo theo thủ tục.

SDFGI hỗ trợ đèn động, nhưng *không* hỗ trợ vật cản động hoặc bề mặt phát sáng động. Do đó, SDFGI cung cấp khả năng theo thời gian thực tốt hơn
:ref:`baked lightmaps <doc_using_lightmap_gi>`, but worse real-time ability than
:ref:`VoxelGI <doc_using_voxel_gi>`.

Xét về hiệu năng, SDFGI là một trong những kỹ thuật chiếu sáng toàn cục đòi hỏi nhiều tài nguyên nhất trong Godot. Tương tự VoxelGI, vẫn có nhiều thiết lập để tinh chỉnh yêu cầu hiệu năng, đánh đổi bằng chất lượng.

.. important::

    SDFGI chỉ được hỗ trợ khi sử dụng trình kết xuất Forward+, không hỗ trợ trình kết xuất Mobile hoặc Compatibility.

.. seealso::

    Không chắc SDFGI có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI có trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :alt: SDFGI disabled.

   SDFGI disabled.

.. figure:: img/gi_sdfgi.webp
   :alt: SDFGI enabled.

   SDFGI enabled.

Thiết lập SDFGI
---------------

Trong Godot, SDFGI là kỹ thuật chiếu sáng toàn cục yêu cầu ít bước bật nhất:

1. Đảm bảo các node MeshInstance của bạn có thuộc tính **Global Illumination > Mode** được đặt thành **Static** trong inspector.

  - Đối với các scene 3D đã import, có thể cấu hình chế độ bake trong dock Import sau khi chọn tệp scene 3D trong dock FileSystem.

2. Thêm một node WorldEnvironment và tạo một resource Environment cho node đó. 3. Chỉnh sửa resource Environment, cuộn xuống phần **SDFGI** và mở rộng phần này. 4. Bật **SDFGI > Enabled**. SDFGI sẽ tự động đi theo camera khi camera di chuyển, vì vậy bạn không cần cấu hình phạm vi (khác với VoxelGI).

Các thuộc tính SDFGI của Environment
------------------------------------

Trong resource Environment, có một số thuộc tính để điều chỉnh giao diện và chất lượng của SDFGI:

- **Use Occlusion:** Nếu được bật, SDFGI sẽ phóng thêm các tia để tìm và giảm hiện tượng rò rỉ ánh sáng. Việc này làm tăng chi phí hiệu năng, vì vậy chỉ bật thuộc tính này nếu bạn thực sự cần. - **Read Sky Light:** Nếu được bật, ánh sáng môi trường sẽ được thể hiện trong phần chiếu sáng toàn cục. Nên bật tùy chọn này trong các scene ngoài trời và tắt trong các scene hoàn toàn trong nhà. - **Bounce Feedback:** Theo mặc định, ánh sáng gián tiếp chỉ nảy một lần khi sử dụng SDFGI. Đặt giá trị này lớn hơn ``0.0`` sẽ khiến SDFGI nảy nhiều hơn một lần, tạo ra ánh sáng gián tiếp chân thực hơn với chi phí hiệu năng nhỏ. Các giá trị hợp lý thường nằm trong khoảng từ ``0.3`` đến ``1.0``, tùy thuộc vào scene. Lưu ý rằng trong một số scene, các giá trị lớn hơn ``0.5`` có thể gây ra vòng lặp phản hồi vô hạn, khiến scene trở nên cực kỳ sáng chỉ trong vài giây. Nếu ánh sáng gián tiếp trông "lốm đốm", hãy cân nhắc tăng giá trị này lên trên ``0.0`` để ánh sáng trông đồng đều hơn. Nếu ánh sáng trở nên quá sáng do đó, hãy giảm **Energy** để bù lại. - **Cascades:** Giá trị cao hơn tạo ra thông tin GI chi tiết hơn (và/hoặc khoảng cách tối đa lớn hơn), nhưng có chi phí cao hơn đáng kể trên CPU và GPU. Chi phí hiệu năng của việc có nhiều cascade đặc biệt tăng khi camera di chuyển nhanh, vì vậy hãy cân nhắc giảm giá trị này xuống ``4`` hoặc thấp hơn nếu camera của bạn di chuyển nhanh. - **Min Cell Size:** Kích thước cell SDFGI tối thiểu được sử dụng cho cascade gần nhất và chi tiết nhất. Giá trị thấp hơn tạo ra ánh sáng gián tiếp và phản xạ chính xác hơn, đánh đổi bằng hiệu năng thấp hơn. Việc điều chỉnh thiết lập này cũng tự động ảnh hưởng đến **Cascade 0 Distance** và **Max Distance**. - **Cascade 0 Distance:** Khoảng cách tại đó cascade gần nhất và chi tiết nhất kết thúc. Giá trị lớn hơn làm cho quá trình chuyển tiếp của cascade gần nhất ít noticeable hơn, đánh đổi bằng mức độ chi tiết thấp hơn trong cascade gần nhất. Việc điều chỉnh thiết lập này cũng tự động ảnh hưởng đến **Min Cell Size** và **Max Distance**. - **Max Distance:** Kiểm soát khoảng cách mà trường khoảng cách có dấu sẽ được tính toán (cho cascade ít chi tiết nhất). SDFGI sẽ không có tác dụng vượt quá khoảng cách này. Giá trị này luôn phải được đặt thấp hơn giá trị Far của Camera, vì không có lợi ích gì khi tính toán SDFGI vượt quá khoảng cách nhìn thấy. Việc điều chỉnh thiết lập này cũng tự động ảnh hưởng đến **Min Cell Size** và **Cascade 0 Distance**. - **Y Scale:** Kiểm soát khoảng cách phân bố *theo chiều dọc* giữa các probe SDFGI. Theo mặc định, độ phân bố theo chiều dọc giống với chiều ngang. Tuy nhiên, vì hầu hết scene game không quá cao theo chiều dọc, đặt Y Scale thành ``75%`` hoặc thậm chí ``50%`` có thể mang lại chất lượng tốt hơn và giảm rò rỉ ánh sáng mà không ảnh hưởng đến hiệu năng. - **Energy:** Hệ số nhân độ sáng cho ánh sáng gián tiếp của SDFGI. - **Normal Bias:** Độ lệch pháp tuyến được sử dụng cho các lần nảy tia của probe SDFGI. Không giống **Probe Bias**, giá trị này chỉ tăng theo hướng liên quan đến các pháp tuyến của mesh. Điều này giúp việc điều chỉnh độ lệch trở nên tinh tế hơn và tránh tăng độ lệch quá mức mà không có lý do. Hãy tăng giá trị này nếu bạn nhận thấy các hiện tượng sọc trong ánh sáng gián tiếp hoặc phản xạ. - **Probe Bias:** Độ lệch được sử dụng cho các lần nảy tia của probe SDFGI. Hãy tăng giá trị này nếu bạn nhận thấy các hiện tượng sọc trong ánh sáng gián tiếp hoặc phản xạ.

Tương tác của SDFGI với đèn và đối tượng
----------------------------------------

Lượng năng lượng gián tiếp do một đèn phát ra được xác định bởi các thuộc tính màu sắc, năng lượng *và* năng lượng gián tiếp của đèn. Để khiến một đèn cụ thể phát ra nhiều hoặc ít năng lượng gián tiếp hơn mà không ảnh hưởng đến lượng ánh sáng trực tiếp do đèn phát ra, hãy điều chỉnh thuộc tính **Indirect Energy** trong inspector của Light3D.

Để đảm bảo hình ảnh chính xác khi sử dụng SDFGI, bạn phải cấu hình các thuộc tính chiếu sáng toàn cục của mesh và đèn theo *mục đích* của chúng trong scene (tĩnh hoặc động).

Có 3 chế độ chiếu sáng toàn cục dành cho mesh:

- **Disabled:** Mesh sẽ không được tính đến khi tạo SDFGI. Mesh sẽ nhận ánh sáng gián tiếp từ scene, nhưng không đóng góp ánh sáng gián tiếp cho scene. - **Static (default):** Mesh sẽ được tính đến khi tạo SDFGI. Mesh vừa nhận *vừa* đóng góp ánh sáng gián tiếp cho scene. Nếu mesh bị thay đổi theo bất kỳ cách nào sau khi SDFGI được tạo, camera phải di chuyển ra xa đối tượng rồi di chuyển lại gần để SDFGI tạo lại. Ngoài ra, có thể tắt rồi bật lại SDFGI. Nếu không thực hiện một trong hai cách này, ánh sáng gián tiếp sẽ hiển thị không chính xác. - **Dynamic (not supported with SDFGI):** Mesh sẽ không được tính đến khi tạo SDFGI. Mesh sẽ nhận ánh sáng gián tiếp từ scene, nhưng không đóng góp ánh sáng gián tiếp cho scene. Chế độ này hoạt động giống hệt chế độ bake **Disabled** khi sử dụng SDFGI.

Ngoài ra, có 3 chế độ bake dành cho đèn (DirectionalLight3D, OmniLight3D, SpotLight3D và AreaLight3D):

- **Disabled:** Đèn sẽ không được tính đến khi bake SDFGI. Đèn sẽ không đóng góp ánh sáng gián tiếp cho scene. - **Static:** Đèn sẽ được tính đến khi bake SDFGI. Đèn sẽ đóng góp ánh sáng gián tiếp cho scene. Nếu đèn bị thay đổi theo bất kỳ cách nào sau khi bake, ánh sáng gián tiếp sẽ hiển thị không chính xác cho đến khi camera di chuyển ra xa đèn rồi quay lại (việc này khiến SDFGI được bake lại). Nếu không chắc chắn, hãy sử dụng chế độ này cho ánh sáng của level. - **Dynamic (default):** Đèn sẽ không được tính đến khi bake SDFGI, nhưng vẫn đóng góp ánh sáng gián tiếp cho scene theo thời gian thực. Tùy chọn này chậm hơn so với **Static**. Chỉ sử dụng chế độ chiếu sáng toàn cục **Dynamic** cho các đèn sẽ thay đổi đáng kể trong quá trình chơi.

.. note::

    Lượng năng lượng gián tiếp do một đèn phát ra phụ thuộc vào các thuộc tính màu sắc, năng lượng *và* năng lượng gián tiếp của đèn. Để khiến một đèn cụ thể phát ra nhiều hoặc ít năng lượng gián tiếp hơn mà không ảnh hưởng đến lượng ánh sáng trực tiếp do đèn phát ra, hãy điều chỉnh thuộc tính **Indirect Energy** trong inspector của Light3D.

.. seealso::

    Xem :ref:`doc_introduction_to_global_illumination_gi_mode_recommendations` để biết các khuyến nghị sử dụng chung.

Điều chỉnh hiệu năng và chất lượng SDFGI
----------------------------------------

Vì SDFGI tương đối đòi hỏi nhiều tài nguyên, kỹ thuật này hoạt động tốt nhất trên các hệ thống có GPU rời đời mới. Trên các GPU rời đời cũ và đồ họa tích hợp, cần tinh chỉnh các thiết lập để đạt hiệu năng hợp lý.

Trong phần **Rendering > Global Illumination** của Project Settings, chất lượng SDFGI cũng có thể được điều chỉnh theo một số cách:

- **Sdfgi > Probe Ray Count:** Giá trị cao hơn sẽ cho chất lượng tốt hơn, nhưng sẽ tiêu tốn nhiều GPU hơn. Nếu đặt giá trị này quá thấp, các bề mặt có thể xuất hiện những "vệt loang" ánh sáng gián tiếp rõ rệt do số lượng tia được phát ra quá ít. - **Sdfgi > Frames To Converge:** Giá trị cao hơn sẽ cho chất lượng tốt hơn, nhưng GI sẽ cần nhiều thời gian hơn để hội tụ hoàn toàn. Ảnh hưởng của thiết lập này đặc biệt dễ nhận thấy khi mới tải một scene, hoặc khi các nguồn sáng có chế độ bake khác **Disabled** đang di chuyển nhanh. Nếu đặt giá trị này quá thấp, các bề mặt có thể xuất hiện những "vệt loang" ánh sáng gián tiếp rõ rệt do số lượng tia được phát ra quá ít. Nếu hệ thống chiếu sáng trong scene của bạn không có các nguồn sáng di chuyển nhanh và đóng góp vào GI, hãy cân nhắc đặt giá trị này thành ``30`` để cải thiện chất lượng mà không ảnh hưởng đến hiệu năng. - **Sdfgi > Frames To Update Light:** Giá trị thấp hơn sẽ giúp phản ánh các nguồn sáng đang di chuyển nhanh hơn, nhưng sẽ tiêu tốn nhiều GPU hơn. Nếu hệ thống chiếu sáng trong scene của bạn không có các nguồn sáng di chuyển nhanh và đóng góp vào GI, hãy cân nhắc đặt giá trị này thành ``16`` để cải thiện hiệu năng. - **Gi > Use Half Resolution:** Khi bật, cả SDFGI và VoxelGI sẽ kết xuất bộ đệm GI ở độ phân giải giảm một nửa. Ví dụ, khi kết xuất ở độ phân giải 3840×2160, bộ đệm GI sẽ được tính toán ở độ phân giải 1920×1080. Bật tùy chọn này giúp tiết kiệm nhiều thời gian GPU, nhưng có thể gây ra hiện tượng răng cưa rõ rệt quanh các chi tiết mảnh.

Hiệu năng kết xuất SDFGI cũng phụ thuộc vào số lượng cascade và kích thước ô được chọn trong tài nguyên Environment (xem ở trên).

Các hạn chế của SDFGI
---------------------

SDFGI có một số nhược điểm do bản chất sử dụng cascade. Khi camera di chuyển, các dịch chuyển của cascade có thể nhìn thấy trong ánh sáng gián tiếp. Có thể giảm bớt hiện tượng này bằng cách điều chỉnh kích thước cascade, cũng như thêm fog (giúp các dịch chuyển của cascade ở xa khó nhận thấy hơn).

Ngoài ra, hiệu năng sẽ bị ảnh hưởng nếu camera di chuyển quá nhanh. Có thể khắc phục điều này theo hai cách:

- Đảm bảo camera không di chuyển quá nhanh trong bất kỳ tình huống nào. - Tạm thời vô hiệu hóa SDFGI trong tài nguyên Environment nếu cần di chuyển camera ở tốc độ cao, sau đó bật lại SDFGI khi tốc độ camera giảm xuống.

Khi SDFGI được bật, hệ thống cũng sẽ cần một khoảng thời gian để global illumination hội tụ hoàn toàn (mặc định là 30 frame). Điều này có thể tạo ra hiệu ứng chuyển tiếp rõ rệt trong khi GI vẫn đang hội tụ. Để che giấu hiệu ứng này, bạn có thể sử dụng một node ColorRect phủ toàn bộ viewport và làm mờ nó khi chuyển scene bằng node AnimationPlayer.

Signed distance field chỉ được cập nhật khi camera di chuyển vào hoặc ra khỏi một cascade. Điều này có nghĩa là nếu hình học được thay đổi ở xa, diện mạo của global illumination sẽ chính xác khi camera đến gần hơn. Tuy nhiên, nếu một đối tượng ở gần có chế độ bake được đặt thành **Static** hoặc **Dynamic** bị di chuyển (chẳng hạn như một cánh cửa), global illumination sẽ hiển thị không chính xác cho đến khi camera di chuyển ra xa đối tượng đó.

Các phản chiếu sắc nét của SDFGI chỉ hiển thị trên vật liệu opaque. Vật liệu trong suốt sẽ chỉ sử dụng phản chiếu thô, ngay cả khi roughness của vật liệu thấp hơn 0.2.
