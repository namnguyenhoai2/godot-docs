.. _doc_using_sdfgi:

Global illumination bằng trường khoảng cách có dấu (SDFGI)
==========================================================

Global illumination bằng trường khoảng cách có dấu (SDFGI) là một kỹ thuật mới có trong Godot. Kỹ thuật này cung cấp global illumination gần thời gian thực, có thể mở rộng đến mọi kích thước thế giới và hoạt động với các level được tạo theo quy trình.

SDFGI hỗ trợ đèn động, nhưng *not* các vật cản động hoặc bề mặt phát sáng động. Vì vậy, SDFGI có khả năng xử lý theo thời gian thực tốt hơn
:ref:`baked lightmaps <doc_using_lightmap_gi>`, nhưng khả năng xử lý theo thời gian thực kém hơn
:ref:`VoxelGI <doc_using_voxel_gi>`.

Xét về hiệu năng, SDFGI là một trong những kỹ thuật global illumination đòi hỏi nhiều tài nguyên nhất trong Godot. Giống như với VoxelGI, vẫn có nhiều thiết lập cho phép điều chỉnh yêu cầu hiệu năng để đánh đổi chất lượng.

.. important::

    SDFGI chỉ được hỗ trợ khi sử dụng Forward+, không được hỗ trợ với các renderer Mobile hoặc Compatibility.

.. seealso::

    Không chắc SDFGI có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI có trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :alt: Đã tắt SDFGI.

   Đã tắt SDFGI.

.. figure:: img/gi_sdfgi.webp
   :alt: Đã bật SDFGI.

   Đã bật SDFGI.

Thiết lập SDFGI
---------------

Trong Godot, SDFGI là kỹ thuật global illumination cần ít bước nhất để bật:

1. Đảm bảo thuộc tính **Global Illumination > Mode** của các node MeshInstance được đặt thành **Static** trong inspector.

  - Đối với các scene 3D đã import, có thể cấu hình chế độ bake trong dock Import sau khi chọn tệp scene 3D trong dock FileSystem.

2. Thêm một node WorldEnvironment và tạo một resource Environment cho node đó.
3. Chỉnh sửa resource Environment, cuộn xuống phần **SDFGI** rồi mở rộng phần này.
4. Bật **SDFGI > Enabled**. SDFGI sẽ tự động đi theo camera khi camera di chuyển, vì vậy bạn không cần cấu hình phạm vi (khác với VoxelGI).

Các thuộc tính SDFGI của Environment
------------------------------------

Trong resource Environment, có một số thuộc tính cho phép điều chỉnh diện mạo và chất lượng của SDFGI:

- **Use Occlusion:** Nếu bật, SDFGI sẽ phát thêm các tia để tìm và giảm hiện tượng rò rỉ ánh sáng. Việc này làm giảm hiệu năng, vì vậy chỉ bật thuộc tính này khi thực sự cần.
- **Read Sky Light:** Nếu bật, ánh sáng môi trường sẽ được thể hiện trong global illumination. Nên bật tùy chọn này trong các scene ngoài trời và tắt trong các scene hoàn toàn trong nhà.
- **Bounce Feedback:** Theo mặc định, ánh sáng gián tiếp chỉ dội một lần khi sử dụng SDFGI. Đặt giá trị này cao hơn ``0.0`` sẽ khiến SDFGI dội nhiều hơn một lần, cung cấp ánh sáng gián tiếp chân thực hơn với một chi phí hiệu năng nhỏ. Các giá trị hợp lý thường nằm giữa ``0.3`` và ``1.0`` tùy theo scene. Lưu ý rằng trong một số scene, các giá trị cao hơn ``0.5`` có thể gây ra vòng lặp feedback vô hạn, khiến scene trở nên cực kỳ sáng chỉ trong vài giây. Nếu ánh sáng gián tiếp trông "lốm đốm", hãy cân nhắc tăng giá trị này cao hơn ``0.0`` để ánh sáng trông đồng đều hơn. Nếu kết quả là ánh sáng trở nên quá sáng, hãy giảm **Energy** để bù lại.
- **Cascades:** Giá trị cao hơn tạo ra thông tin GI chi tiết hơn (và/hoặc khoảng cách tối đa lớn hơn), nhưng tiêu tốn CPU và GPU nhiều hơn đáng kể. Chi phí hiệu năng do có nhiều cascade hơn đặc biệt tăng khi camera di chuyển nhanh, vì vậy hãy cân nhắc giảm giá trị này xuống ``4`` hoặc thấp hơn nếu camera của bạn di chuyển nhanh.
- **Min Cell Size:** Kích thước ô SDFGI tối thiểu được sử dụng cho cascade gần nhất và chi tiết nhất. Giá trị thấp hơn cho ánh sáng gián tiếp và phản chiếu chính xác hơn, nhưng làm giảm hiệu năng. Điều chỉnh thiết lập này cũng tự động ảnh hưởng đến **Cascade 0 Distance** và **Max Distance**.
- **Cascade 0 Distance:** Khoảng cách tại đó cascade gần nhất và chi tiết nhất kết thúc. Giá trị lớn hơn khiến quá trình chuyển tiếp của cascade gần nhất ít nhận thấy hơn, nhưng làm giảm mức độ chi tiết trong cascade gần nhất. Điều chỉnh thiết lập này cũng tự động ảnh hưởng đến **Min Cell Size** và **Max Distance**.
- **Max Distance:** Kiểm soát khoảng cách tính toán trường khoảng cách có dấu (đối với cascade ít chi tiết nhất). SDFGI sẽ không có tác dụng ngoài khoảng cách này. Giá trị này luôn phải được đặt thấp hơn giá trị Far của Camera, vì không có lợi ích nào khi tính SDFGI vượt quá khoảng cách quan sát. Điều chỉnh thiết lập này cũng tự động ảnh hưởng đến **Min Cell Size** và **Cascade 0 Distance**.
- **Y Scale:** Kiểm soát khoảng cách phân bố các probe SDFGI *vertically*. Theo mặc định, khoảng phân bố theo chiều dọc giống với chiều ngang. Tuy nhiên, vì hầu hết scene game không có độ cao lớn, đặt Y Scale thành ``75%`` hoặc thậm chí ``50%`` có thể mang lại chất lượng tốt hơn và giảm rò rỉ ánh sáng mà không ảnh hưởng đến hiệu năng.
- **Energy:** Hệ số độ sáng cho ánh sáng gián tiếp của SDFGI.
- **Normal Bias:** Độ lệch pháp tuyến được sử dụng cho các lần dội tia probe của SDFGI. Khác với **Probe Bias**, thuộc tính này chỉ tăng giá trị theo pháp tuyến của mesh. Điều này giúp việc điều chỉnh độ lệch tinh tế hơn và tránh tăng độ lệch quá mức mà không có lý do. Hãy tăng giá trị này nếu bạn nhận thấy các nhiễu dạng sọc trong ánh sáng gián tiếp hoặc phản chiếu.
- **Probe Bias:** Độ lệch được sử dụng cho các lần dội tia probe của SDFGI. Hãy tăng giá trị này nếu bạn nhận thấy các nhiễu dạng sọc trong ánh sáng gián tiếp hoặc phản chiếu.

Tương tác của SDFGI với đèn và vật thể
--------------------------------------

Lượng năng lượng gián tiếp do một đèn phát ra được xác định bởi màu sắc, năng lượng *and* các thuộc tính năng lượng gián tiếp của đèn. Để khiến một đèn cụ thể phát ra nhiều hoặc ít năng lượng gián tiếp hơn mà không ảnh hưởng đến lượng ánh sáng trực tiếp do đèn phát ra, hãy điều chỉnh thuộc tính **Indirect Energy** trong inspector của Light3D.

Để đảm bảo hình ảnh chính xác khi sử dụng SDFGI, bạn phải cấu hình các thuộc tính global illumination của mesh và đèn theo *purpose* của chúng trong scene (tĩnh hoặc động).

Có 3 chế độ global illumination dành cho mesh:

- **Đã tắt:** Mesh sẽ không được tính đến khi tạo SDFGI. Mesh sẽ nhận ánh sáng gián tiếp từ cảnh, nhưng sẽ không đóng góp ánh sáng gián tiếp cho cảnh.
- **Tĩnh (mặc định):** Mesh sẽ được tính đến khi tạo SDFGI. Mesh sẽ vừa nhận *vừa* đóng góp ánh sáng gián tiếp cho cảnh. Nếu mesh bị thay đổi theo bất kỳ cách nào sau khi SDFGI được tạo, camera phải di chuyển ra xa đối tượng rồi di chuyển lại gần để SDFGI được tạo lại. Ngoài ra, có thể tắt rồi bật lại SDFGI. Nếu không thực hiện một trong hai cách này, ánh sáng gián tiếp sẽ hiển thị không chính xác.
- **Động (không được SDFGI hỗ trợ):** Mesh sẽ không được tính đến khi tạo SDFGI. Mesh sẽ nhận ánh sáng gián tiếp từ cảnh, nhưng sẽ không đóng góp ánh sáng gián tiếp cho cảnh. Chế độ này hoạt động giống hệt chế độ bake **Đã tắt** khi sử dụng SDFGI.

Ngoài ra, có 3 chế độ bake khả dụng cho các đèn (DirectionalLight3D, OmniLight3D, SpotLight3D và AreaLight3D):

- **Đã tắt:** Đèn sẽ không được tính đến khi bake SDFGI. Đèn sẽ không đóng góp ánh sáng gián tiếp cho cảnh.
- **Tĩnh:** Đèn sẽ được tính đến khi bake SDFGI. Đèn sẽ đóng góp ánh sáng gián tiếp cho cảnh. Nếu đèn bị thay đổi theo bất kỳ cách nào sau khi bake, ánh sáng gián tiếp sẽ hiển thị không chính xác cho đến khi camera di chuyển ra xa đèn rồi quay lại (việc này khiến SDFGI được bake lại). Nếu không chắc chắn, hãy sử dụng chế độ này cho ánh sáng của level.
- **Động (mặc định):** Đèn sẽ không được tính đến khi bake SDFGI, nhưng vẫn đóng góp ánh sáng gián tiếp cho cảnh theo thời gian thực. Tùy chọn này chậm hơn so với **Tĩnh**. Chỉ sử dụng chế độ global illumination **Động** trên những đèn sẽ thay đổi đáng kể trong khi chơi.

.. note::

    Lượng năng lượng gián tiếp do đèn phát ra phụ thuộc vào màu sắc, năng lượng *và* các thuộc tính năng lượng gián tiếp của đèn. Để khiến một đèn cụ thể phát ra nhiều hơn hoặc ít hơn năng lượng gián tiếp mà không ảnh hưởng đến lượng ánh sáng trực tiếp do đèn phát ra, hãy điều chỉnh thuộc tính **Năng lượng gián tiếp** trong inspector của Light3D.

.. seealso::

    Xem :ref:`doc_introduction_to_global_illumination_gi_mode_recommendations` để biết các khuyến nghị sử dụng chung.

Điều chỉnh hiệu năng và chất lượng SDFGI
----------------------------------------

Vì SDFGI tương đối nặng, tính năng này sẽ hoạt động tốt nhất trên các hệ thống có GPU chuyên dụng đời mới. Trên các GPU chuyên dụng đời cũ và đồ họa tích hợp, cần tinh chỉnh các thiết lập để đạt hiệu năng hợp lý.

Trong phần **Rendering > Global Illumination** của Project Settings, chất lượng SDFGI cũng có thể được điều chỉnh theo một số cách:

- **Sdfgi > Probe Ray Count:** Giá trị cao hơn cho chất lượng tốt hơn, nhưng sử dụng GPU nhiều hơn. Nếu đặt giá trị này quá thấp, các bề mặt có thể xuất hiện những "đốm" ánh sáng gián tiếp rõ rệt do số lượng tia được phóng ra quá ít.
- **Sdfgi > Frames To Converge:** Giá trị cao hơn cho chất lượng tốt hơn, nhưng GI sẽ mất nhiều thời gian hơn để hội tụ hoàn toàn. Tác động của thiết lập này đặc biệt dễ nhận thấy khi lần đầu tải một cảnh hoặc khi các đèn có chế độ bake khác **Đã tắt** di chuyển nhanh. Nếu đặt giá trị này quá thấp, các bề mặt có thể xuất hiện những "đốm" ánh sáng gián tiếp rõ rệt do số lượng tia được phóng ra quá ít. Nếu ánh sáng trong cảnh của bạn không có các đèn di chuyển nhanh và đóng góp vào GI, hãy cân nhắc đặt giá trị này thành ``30`` để cải thiện chất lượng mà không ảnh hưởng đến hiệu năng.
- **Sdfgi > Frames To Update Light:** Giá trị thấp hơn giúp phản ánh các đèn đang di chuyển nhanh hơn, nhưng sử dụng GPU nhiều hơn. Nếu ánh sáng trong cảnh của bạn không có các đèn di chuyển nhanh và đóng góp vào GI, hãy cân nhắc đặt giá trị này thành ``16`` để cải thiện hiệu năng.
- **Gi > Use Half Resolution:** Nếu bật, cả SDFGI và VoxelGI sẽ kết xuất bộ đệm GI ở độ phân giải giảm một nửa. Ví dụ, khi kết xuất ở 3840×2160, bộ đệm GI sẽ được tính toán ở độ phân giải 1920×1080. Bật tùy chọn này giúp tiết kiệm đáng kể thời gian GPU, nhưng có thể tạo ra hiện tượng aliasing rõ rệt xung quanh các chi tiết mảnh.

Hiệu năng kết xuất SDFGI cũng phụ thuộc vào số lượng cascade và kích thước ô được chọn trong tài nguyên Environment (xem phần trên).

Các hạn chế của SDFGI
---------------------

SDFGI có một số nhược điểm do bản chất phân tầng của nó. Khi camera di chuyển, có thể nhìn thấy sự dịch chuyển của cascade trong ánh sáng gián tiếp. Có thể giảm hiện tượng này bằng cách điều chỉnh kích thước cascade, cũng như thêm sương mù (giúp các dịch chuyển của cascade ở xa khó nhận thấy hơn).

Ngoài ra, hiệu năng sẽ giảm nếu camera di chuyển quá nhanh. Có thể khắc phục điều này bằng hai cách:

- Đảm bảo camera không di chuyển quá nhanh trong bất kỳ tình huống nào.
- Tạm thời tắt SDFGI trong tài nguyên Environment nếu cần di chuyển camera với tốc độ cao, sau đó bật lại SDFGI khi tốc độ camera chậm xuống.

Khi SDFGI được bật, global illumination cũng cần một khoảng thời gian để hội tụ hoàn toàn (mặc định là 30 khung hình). Điều này có thể tạo ra hiệu ứng chuyển tiếp dễ nhận thấy trong khi GI vẫn đang hội tụ. Để ẩn hiệu ứng này, bạn có thể sử dụng một node ColorRect phủ toàn bộ viewport và làm mờ nó khi chuyển cảnh bằng node AnimationPlayer.

Signed distance field chỉ được cập nhật khi camera di chuyển vào hoặc ra khỏi một cascade. Điều này có nghĩa là nếu hình học bị thay đổi ở xa, hình thức của global illumination sẽ chính xác khi camera đến gần hơn. Tuy nhiên, nếu một đối tượng ở gần có chế độ bake được đặt thành **Tĩnh** hoặc **Động** bị di chuyển (chẳng hạn như một cánh cửa), global illumination sẽ hiển thị không chính xác cho đến khi camera di chuyển ra xa đối tượng.

Các phản xạ sắc nét của SDFGI chỉ hiển thị trên vật liệu opaque. Vật liệu trong suốt sẽ chỉ sử dụng phản xạ thô, ngay cả khi roughness của vật liệu thấp hơn 0.2.
