.. _doc_physics_interpolation_introduction:

Giới thiệu
==========

Các nhịp physics và frame được kết xuất
---------------------------------------

Một khái niệm quan trọng cần hiểu trong Godot là sự khác biệt giữa các nhịp physics (đôi khi được gọi là các lần lặp hoặc frame physics) và các frame được kết xuất. Physics hoạt động ở một tần suất nhịp cố định (được đặt trong :ref:`Project Settings > Physics > Common > Physics Tick per Second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>`), mặc định là 60 nhịp mỗi giây.

Tuy nhiên, engine không nhất thiết phải **kết xuất** ở cùng tần suất đó. Mặc dù nhiều màn hình làm mới ở 60 Hz (chu kỳ mỗi giây), nhiều màn hình khác lại làm mới ở các tần số hoàn toàn khác (ví dụ: 75 Hz, 144 Hz, 240 Hz hoặc cao hơn). Dù một màn hình có thể hiển thị một frame mới, chẳng hạn 60 lần mỗi giây, không có gì đảm bảo CPU và GPU sẽ có thể *cung cấp* frame ở tần suất này. Ví dụ, khi chạy với V-Sync, máy tính có thể quá chậm để đạt 60 và chỉ kịp các thời hạn cho 30 FPS, trong trường hợp đó các frame bạn thấy sẽ thay đổi ở 30 FPS (dẫn đến hiện tượng giật hình).

Nhưng ở đây có một vấn đề. Điều gì xảy ra nếu các nhịp physics không trùng với các frame? Điều gì xảy ra nếu tần suất nhịp physics lệch pha với tần suất frame? Hoặc tệ hơn, điều gì xảy ra nếu tần suất nhịp physics *thấp hơn* tần suất frame được kết xuất?

Vấn đề này sẽ dễ hiểu hơn nếu ta xét một tình huống cực đoan. Giả sử bạn đặt tần suất nhịp physics là 10 nhịp mỗi giây trong một game đơn giản có tần suất frame được kết xuất là 60 FPS. Nếu vẽ biểu đồ vị trí của một đối tượng theo các frame được kết xuất, bạn sẽ thấy các vị trí dường như "nhảy" mỗi 1/10 giây, thay vì tạo ra chuyển động mượt mà. Khi physics tính toán một vị trí mới cho một đối tượng, vị trí này không chỉ được kết xuất trong một frame mà trong 6 frame.

.. image:: img/fti_graph_fixed_ticks.webp

Hiện tượng nhảy này cũng có thể xuất hiện trong các tổ hợp tần suất nhịp / frame khác dưới dạng glitch hoặc jitter, do hiệu ứng bậc thang gây ra bởi sự chênh lệch giữa thời gian của nhịp physics và thời gian của frame được kết xuất.

Chúng ta có thể làm gì khi các frame và nhịp không đồng bộ?
-----------------------------------------------------------

Đồng bộ tần suất nhịp / frame?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Giải pháp rõ ràng nhất là loại bỏ vấn đề bằng cách đảm bảo có một nhịp physics trùng với mỗi frame. Đây từng là cách tiếp cận trên các console cũ và máy tính có phần cứng cố định. Nếu biết mọi người chơi sẽ sử dụng cùng một phần cứng, bạn có thể đảm bảo phần cứng đó đủ nhanh để tính toán các nhịp và frame ở, chẳng hạn, 50 FPS, và bạn có thể chắc chắn rằng mọi người đều sẽ có trải nghiệm tốt.

Tuy nhiên, các game hiện đại thường không còn được tạo ra cho phần cứng cố định. Bạn thường sẽ dự định phát hành game trên máy tính để bàn, thiết bị di động và nhiều nền tảng khác. Tất cả các thiết bị này có hiệu năng khác nhau rất nhiều, cũng như có tần suất làm mới màn hình khác nhau. Chúng ta cần tìm ra một cách tốt hơn để xử lý vấn đề này.

Điều chỉnh tần suất nhịp?
~~~~~~~~~~~~~~~~~~~~~~~~~

Thay vì thiết kế game với một tần suất nhịp physics cố định, chúng ta có thể cho phép tần suất nhịp thay đổi theo phần cứng của người dùng cuối. Ví dụ, chúng ta có thể sử dụng một tần suất nhịp cố định phù hợp với phần cứng đó, hoặc thậm chí thay đổi thời lượng của từng nhịp physics để khớp với thời lượng của một frame cụ thể.

Cách này có hiệu quả, nhưng vẫn có một vấn đề. Physics (*và logic game*, thường cũng được chạy trong ``_physics_process``) hoạt động tốt nhất và nhất quán nhất khi chạy ở một tần suất nhịp **cố định**, được xác định trước. Nếu cố chạy physics của một game đua xe được thiết kế cho 60 TPS (nhịp mỗi giây) ở mức, chẳng hạn, 10 TPS, physics sẽ hoạt động hoàn toàn khác. Điều khiển có thể kém phản hồi hơn, các va chạm / quỹ đạo có thể hoàn toàn khác. Bạn có thể kiểm thử game kỹ lưỡng ở 60 TPS, rồi phát hiện game bị lỗi trên máy của người dùng cuối khi chạy ở một tần suất nhịp khác.

Điều này có thể khiến việc đảm bảo chất lượng trở nên khó khăn do các lỗi khó tái hiện, đặc biệt là trong các game AAA, nơi những vấn đề kiểu này có thể gây tốn kém rất nhiều. Điều này cũng có thể gây vấn đề cho các game multiplayer về tính công bằng trong thi đấu, vì chạy game ở một số tần suất nhịp nhất định có thể mang lại lợi thế hơn so với các tần suất khác.

Cố định tần suất nhịp, nhưng dùng interpolation để làm mượt các frame nằm giữa các nhịp physics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đây đã trở thành một trong những cách tiếp cận phổ biến nhất để xử lý vấn đề này, mặc dù đây là tùy chọn và mặc định bị tắt.

Chúng ta đã xác định rằng cách sắp xếp physics / logic game đáng mong muốn nhất về tính nhất quán và khả năng dự đoán là tần suất nhịp physics được cố định từ lúc thiết kế. Vấn đề nằm ở sự chênh lệch giữa vị trí physics được ghi lại và vị trí mà chúng ta "muốn" hiển thị một đối tượng physics trong một frame để tạo ra chuyển động mượt mà.

Hóa ra câu trả lời rất đơn giản, nhưng ban đầu có thể hơi khó hình dung.

Thay vì chỉ theo dõi vị trí hiện tại của một đối tượng physics trong engine, chúng ta theo dõi *cả vị trí hiện tại của đối tượng và vị trí trước đó* ở nhịp physics trước.

Tại sao chúng ta cần vị trí trước đó *(thực tế là toàn bộ transform, bao gồm cả phép xoay và tỷ lệ)*? Bằng một chút phép màu toán học, chúng ta có thể dùng **interpolation** để tính toán transform của đối tượng sẽ như thế nào giữa hai điểm đó, trong thế giới lý tưởng với chuyển động liên tục, mượt mà.

.. image:: img/fti_graph_interpolated.webp

Interpolation tuyến tính
~~~~~~~~~~~~~~~~~~~~~~~~

Cách đơn giản nhất để đạt được điều này là interpolation tuyến tính, hay lerp, có thể bạn đã từng sử dụng.

Hãy chỉ xét vị trí và một tình huống trong đó ta biết tọa độ X của nhịp physics trước là 10 đơn vị, còn tọa độ X của nhịp physics hiện tại là 30 đơn vị.

.. note:: Mặc dù phần toán học được giải thích ở đây, bạn không cần lo về các chi tiết, vì bước này sẽ được thực hiện thay cho bạn. Bên dưới, Godot có thể sử dụng các dạng interpolation phức tạp hơn, nhưng interpolation tuyến tính là dạng dễ giải thích nhất.

Phân số interpolation physics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu các nhịp physics của chúng ta diễn ra 10 lần mỗi giây (trong ví dụ này), điều gì xảy ra nếu frame được kết xuất diễn ra tại thời điểm 0.12 giây? Chúng ta có thể thực hiện một số phép tính để xác định vị trí của đối tượng, qua đó tạo ra chuyển động mượt mà giữa hai nhịp.

Trước hết, chúng ta phải tính xem đối tượng cần đi được bao xa trong nhịp physics. Nếu nhịp physics cuối cùng diễn ra tại 0.1 giây, chúng ta đã đi qua 0.02 giây *(0.12 - 0.1)* trong một nhịp mà ta biết sẽ kéo dài 0.1 giây (10 nhịp mỗi giây). Do đó, phân số đã đi qua trong nhịp là:

.. code-block:: gdscript

	fraction = 0.02 / 0.10
	fraction = 0.2

Đây được gọi là **phân số interpolation physics**, và Godot sẽ tiện thể tính toán nó cho bạn. Bạn có thể lấy giá trị này ở bất kỳ frame nào bằng cách gọi :ref:`Engine.get_physics_interpolation_fraction<class_Engine_method_get_physics_interpolation_fraction>`.

Tính toán vị trí được nội suy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi đã có phân số interpolation, chúng ta có thể đưa nó vào phương trình interpolation tuyến tính tiêu chuẩn. Do đó, tọa độ X sẽ là:

.. code-block:: gdscript

	x_interpolated = x_prev + ((x_curr - x_prev) * 0.2)

Vậy khi thay ``x_prev`` bằng 10 và ``x_curr`` bằng 30:

.. code-block:: gdscript

	x_interpolated = 10 + ((30 - 10) * 0.2)
	x_interpolated = 10 + 4
	x_interpolated = 14

Hãy cùng phân tích:

- Ta biết X bắt đầu từ tọa độ ở tick trước (``x_prev``), tức là 10 đơn vị.
- Ta biết rằng sau toàn bộ một tick, hiệu giữa tick hiện tại và tick trước sẽ được cộng thêm (``x_curr - x_prev``) (tức là 20 đơn vị).
- Điều duy nhất cần thay đổi là tỷ lệ của hiệu này được cộng thêm, tùy theo mức độ tiến triển của ta trong tick vật lý.

.. note:: Mặc dù ví dụ này nội suy vị trí, ta cũng có thể thực hiện tương tự với rotation và scale của các đối tượng. Bạn không cần biết chi tiết vì Godot sẽ thực hiện tất cả việc này cho bạn.

Biến đổi mượt mà giữa các tick vật lý?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi kết hợp tất cả lại, ta thấy có thể ước tính khá mượt transform của các đối tượng giữa tick vật lý hiện tại và tick trước đó.

Nhưng khoan, có thể bạn đã nhận ra một điều. Nếu ta nội suy giữa tick hiện tại và tick trước đó, ta không ước tính vị trí của đối tượng *bây giờ*, mà đang ước tính vị trí của đối tượng trong quá khứ. Chính xác hơn, ta đang ước tính vị trí của đối tượng *từ 1 đến 2 tick* trước.

Trong quá khứ
~~~~~~~~~~~~~

Điều này có nghĩa là gì? Cơ chế này vẫn hoạt động, nhưng có nghĩa là trên thực tế ta đang tạo ra độ trễ giữa những gì nhìn thấy trên màn hình và vị trí mà các đối tượng *đáng lẽ* đang ở.

Trên thực tế, hầu hết mọi người sẽ không nhận thấy độ trễ này, hay đúng hơn là nó thường không *đáng kể*. Trò chơi vốn đã có những độ trễ đáng kể, chỉ là chúng ta thường không nhận ra. Tác động đáng kể nhất là đầu vào có thể bị trễ đôi chút, điều này có thể ảnh hưởng đến các trò chơi đòi hỏi phản xạ nhanh. Trong một số tình huống cần phản hồi đầu vào nhanh như vậy, bạn có thể muốn tắt nội suy vật lý và sử dụng một cơ chế khác, hoặc dùng tick rate cao để giảm thiểu những độ trễ này.

Tại sao lại xem xét quá khứ? Tại sao không dự đoán tương lai?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có một lựa chọn khác cho cơ chế này: thay vì nội suy giữa tick trước đó và tick hiện tại, ta dùng toán học để *ngoại suy* về tương lai. Ta cố gắng dự đoán vị trí mà đối tượng *sẽ ở*, thay vì hiển thị vị trí trước đó của nó. Điều này có thể thực hiện được và có thể sẽ được cung cấp dưới dạng một tùy chọn trong tương lai, nhưng có một số nhược điểm đáng kể:

- Dự đoán có thể không chính xác, đặc biệt khi một đối tượng va chạm với đối tượng khác trong tick vật lý.
- Khi dự đoán không chính xác, đối tượng có thể ngoại suy đến một vị trí "bất khả thi", chẳng hạn như bên trong một bức tường.
- Miễn là tốc độ di chuyển chậm, những dự đoán không chính xác này có thể không gây ra vấn đề quá lớn.
- Khi dự đoán không chính xác, đối tượng có thể phải nhảy hoặc snap trở lại quỹ đạo đã được hiệu chỉnh. Điều này có thể gây khó chịu về mặt hình ảnh.

Nội suy timestep cố định
~~~~~~~~~~~~~~~~~~~~~~~~

Trong Godot, toàn bộ hệ thống này được gọi là nội suy vật lý, nhưng bạn cũng có thể nghe thấy nó được gọi là **"nội suy timestep cố định"**, vì nó nội suy giữa các đối tượng được di chuyển bằng timestep cố định (số tick vật lý mỗi giây). Theo một số khía cạnh, thuật ngữ thứ hai chính xác hơn, vì nó cũng có thể được dùng để nội suy các đối tượng không được điều khiển bởi vật lý.

.. tip:: Mặc dù nội suy vật lý thường là một lựa chọn tốt, vẫn có những trường hợp ngoại lệ khiến bạn có thể chọn không sử dụng nội suy vật lý tích hợp của Godot (hoặc chỉ sử dụng ở mức hạn chế). Một ví dụ là các trò chơi multiplayer qua internet. Trò chơi multiplayer thường nhận thông tin dựa trên tick hoặc thời gian từ những người chơi khác hay từ máy chủ, và những thông tin này có thể không trùng với các tick vật lý cục bộ, vì vậy một kỹ thuật nội suy tùy chỉnh thường có thể phù hợp hơn.
