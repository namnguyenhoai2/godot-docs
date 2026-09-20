.. _doc_physics_interpolation_introduction:

Giới thiệu
==========

Physics tick và frame được render
---------------------------------

Một khái niệm quan trọng cần hiểu trong Godot là sự khác biệt giữa physics tick (đôi khi còn được gọi là iteration hoặc physics frame) và frame được render. Physics diễn ra ở một tick rate cố định (được thiết lập trong :ref:`Project Settings > Physics > Common > Physics Tick per Second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>`), mặc định là 60 tick mỗi giây.

Tuy nhiên, engine không nhất thiết **render** ở cùng tốc độ đó. Mặc dù nhiều màn hình refresh ở 60 Hz (chu kỳ mỗi giây), nhiều màn hình khác refresh ở các tần số hoàn toàn khác (ví dụ: 75 Hz, 144 Hz, 240 Hz hoặc cao hơn). Dù một màn hình có thể hiển thị frame mới, chẳng hạn, 60 lần mỗi giây, không có gì đảm bảo CPU và GPU có thể *cung cấp* frame ở tốc độ này. Ví dụ, khi chạy với V-Sync, máy tính có thể quá chậm để đạt 60 và chỉ kịp các deadline cho 30 FPS; khi đó, các frame bạn thấy sẽ thay đổi ở 30 FPS (dẫn đến hiện tượng giật hình).

Nhưng ở đây có một vấn đề. Điều gì xảy ra nếu các physics tick không trùng với các frame? Điều gì xảy ra nếu tick rate của physics lệch pha với frame rate? Hoặc tệ hơn, điều gì xảy ra nếu tick rate của physics *thấp hơn* frame rate được render?

Vấn đề này sẽ dễ hiểu hơn nếu ta xét một tình huống cực đoan. Nếu bạn đặt tick rate của physics là 10 tick mỗi giây, trong một game đơn giản có frame rate được render là 60 FPS. Nếu vẽ đồ thị vị trí của một object theo các frame được render, bạn sẽ thấy các vị trí dường như sẽ "nhảy" mỗi 1/10 giây, thay vì tạo ra chuyển động mượt mà. Khi physics tính toán vị trí mới cho một object, vị trí đó không chỉ được render trong một frame mà trong 6 frame.

.. image:: img/fti_graph_fixed_ticks.webp

Hiện tượng nhảy này có thể xuất hiện dưới dạng glitch hoặc jitter trong các tổ hợp tick / frame rate khác, do hiệu ứng bậc thang gây ra bởi sự chênh lệch giữa thời gian physics tick và thời gian frame được render.

Chúng ta có thể làm gì khi frame và tick không đồng bộ?
-------------------------------------------------------

Khóa tick / frame rate cùng nhau?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Giải pháp rõ ràng nhất là loại bỏ vấn đề bằng cách đảm bảo có một physics tick trùng với mỗi frame. Đây từng là cách tiếp cận trên các console cũ và máy tính có phần cứng cố định. Nếu biết mọi người chơi sẽ sử dụng cùng một phần cứng, bạn có thể đảm bảo phần cứng đó đủ nhanh để tính toán tick và frame ở, chẳng hạn, 50 FPS, và bạn sẽ chắc chắn rằng nó hoạt động tốt với tất cả mọi người.

Tuy nhiên, các game hiện đại thường không còn được tạo cho phần cứng cố định. Bạn thường sẽ dự định phát hành game trên máy tính desktop, thiết bị di động và nhiều nền tảng khác. Tất cả những nền tảng này có hiệu năng cũng như tần số refresh màn hình khác nhau rất lớn. Chúng ta cần tìm ra một cách tốt hơn để xử lý vấn đề này.

Điều chỉnh tick rate?
~~~~~~~~~~~~~~~~~~~~~

Thay vì thiết kế game với một tick rate cố định cho physics, chúng ta có thể cho phép tick rate thay đổi theo phần cứng của người dùng cuối. Chẳng hạn, chúng ta có thể sử dụng một tick rate cố định phù hợp với phần cứng đó, hoặc thậm chí thay đổi thời lượng của mỗi physics tick để khớp với thời lượng của một frame cụ thể.

Cách này hiệu quả, nhưng có một vấn đề. Physics (*và game logic*, vốn cũng thường chạy trong ``_physics_process``) hoạt động tốt nhất và nhất quán nhất khi chạy ở một tick rate **cố định**, được xác định trước. Nếu bạn cố chạy physics của một game đua xe được thiết kế cho 60 TPS (tick mỗi giây) ở mức, chẳng hạn, 10 TPS, physics sẽ hoạt động hoàn toàn khác. Điều khiển có thể kém phản hồi hơn, các va chạm / quỹ đạo có thể hoàn toàn khác. Bạn có thể kiểm thử game kỹ lưỡng ở 60 TPS, rồi phát hiện game bị hỏng trên máy của người dùng cuối khi chạy ở tick rate khác.

Điều này có thể khiến việc đảm bảo chất lượng trở nên khó khăn do các bug khó tái hiện, đặc biệt trong các game AAA, nơi những vấn đề kiểu này có thể gây tốn kém đáng kể. Đây cũng có thể là vấn đề đối với các game multiplayer xét về tính công bằng trong thi đấu, vì chạy game ở một số tick rate nhất định có thể có lợi hơn so với các tick rate khác.

Khóa tick rate, nhưng dùng interpolation để làm mượt các frame giữa các physics tick
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đây đã trở thành một trong những cách tiếp cận phổ biến nhất để xử lý vấn đề này, mặc dù đây là tùy chọn và mặc định bị tắt.

Chúng ta đã xác định rằng cách sắp xếp physics/game logic đáng mong muốn nhất xét về tính nhất quán và khả năng dự đoán là một physics tick rate được cố định tại thời điểm thiết kế. Vấn đề nằm ở sự chênh lệch giữa vị trí physics được ghi lại và vị trí mà chúng ta "muốn" một physics object được hiển thị trên frame để tạo ra chuyển động mượt mà.

Câu trả lời hóa ra khá đơn giản, nhưng lúc đầu có thể hơi khó nắm bắt.

Thay vì chỉ theo dõi vị trí hiện tại của một physics object trong engine, chúng ta theo dõi *cả vị trí hiện tại của object và vị trí trước đó* ở physics tick trước.

Tại sao chúng ta cần vị trí trước đó *(thực tế là toàn bộ transform, bao gồm rotation và scaling)*? Bằng một chút phép màu toán học, chúng ta có thể dùng **interpolation** để tính toán transform của object sẽ như thế nào giữa hai điểm đó, trong thế giới lý tưởng của chuyển động liên tục và mượt mà.

.. image:: img/fti_graph_interpolated.webp

Linear interpolation
~~~~~~~~~~~~~~~~~~~~

Cách đơn giản nhất để thực hiện việc này là linear interpolation, hay lerping, mà có thể bạn đã từng sử dụng.

Hãy chỉ xét vị trí và một tình huống trong đó ta biết tọa độ X của physics tick trước là 10 unit, còn tọa độ X của physics tick hiện tại là 30 unit.

.. note:: Although the maths is explained here, you do not have to worry about the
          chi tiết, vì bước này sẽ được thực hiện thay cho bạn. Bên dưới, Godot có thể sử dụng các dạng interpolation phức tạp hơn, nhưng linear interpolation là cách dễ giải thích nhất.

Phân số physics interpolation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu physics tick của chúng ta diễn ra 10 lần mỗi giây (trong ví dụ này), điều gì xảy ra nếu frame được render diễn ra tại thời điểm 0.12 giây? Chúng ta có thể thực hiện một số phép tính để tìm ra vị trí của object, từ đó tạo ra chuyển động mượt mà giữa hai tick.

Trước hết, chúng ta phải tính xem object cần đi được bao xa trong physics tick. Nếu physics tick cuối cùng diễn ra ở 0.1 giây, chúng ta đã đi qua 0.02 giây *(0.12 - 0.1)* của một tick mà ta biết sẽ kéo dài 0.1 giây (10 tick mỗi giây). Do đó, phân số thời gian đã đi qua trong tick là:

.. code-block:: gdscript

	fraction = 0.02 / 0.10
	fraction = 0.2

Giá trị này được gọi là **physics interpolation fraction** và được Godot tính sẵn cho bạn. Bạn có thể lấy giá trị này ở bất kỳ frame nào bằng cách gọi :ref:`Engine.get_physics_interpolation_fraction<class_Engine_method_get_physics_interpolation_fraction>`.

Tính toán vị trí được nội suy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi có interpolation fraction, chúng ta có thể đưa nó vào phương trình linear interpolation tiêu chuẩn. Khi đó, tọa độ X sẽ là:

.. code-block:: gdscript

	x_interpolated = x_prev + ((x_curr - x_prev) * 0.2)

Vậy thay ``x_prev`` bằng 10 và ``x_curr`` bằng 30:

.. code-block:: gdscript

	x_interpolated = 10 + ((30 - 10) * 0.2)
	x_interpolated = 10 + 4
	x_interpolated = 14

Hãy phân tích chi tiết:

- Chúng ta biết X bắt đầu từ tọa độ ở tick trước (``x_prev``), tức là 10 unit. - Chúng ta biết rằng sau toàn bộ tick, độ chênh lệch giữa tick hiện tại và tick trước sẽ được cộng vào (``x_curr - x_prev``) (tức là 20 unit). - Điều duy nhất chúng ta cần thay đổi là tỷ lệ của độ chênh lệch này được cộng vào, dựa trên việc chúng ta đã đi qua bao xa trong physics tick.

.. note:: Although this example interpolates the position, the same thing can be
          đã hoàn tất với rotation và scale của các object. Bạn không cần biết các chi tiết, vì Godot sẽ thực hiện tất cả việc này thay cho bạn.

Transform được làm mượt giữa các physics tick?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kết hợp tất cả lại, ta thấy rằng có thể tạo ra một ước tính mượt mà về transform của các object giữa physics tick hiện tại và physics tick trước.

Nhưng khoan, có thể bạn đã nhận thấy một điều. Nếu chúng ta nội suy giữa tick hiện tại và tick trước, chúng ta không ước tính vị trí của object *ngay lúc này*, mà đang ước tính vị trí của object trong quá khứ. Chính xác hơn, chúng ta đang ước tính vị trí của object *từ 1 đến 2 tick trước*.

Trong quá khứ
~~~~~~~~~~~~~

Điều này có nghĩa là gì? Cách này hoạt động, nhưng cũng có nghĩa là chúng ta thực chất đang tạo ra một độ trễ giữa những gì thấy trên màn hình và vị trí mà các object *đáng lẽ phải ở đó*.

Trên thực tế, hầu hết mọi người sẽ không nhận thấy độ trễ này, hay đúng hơn, nó thường không *gây khó chịu*. Game vốn đã có những độ trễ đáng kể, chỉ là chúng ta thường không nhận ra. Tác động đáng kể nhất là input có thể bị trễ nhẹ, điều này có thể trở thành yếu tố quan trọng trong các game cần phản xạ nhanh. Trong một số tình huống cần input nhanh này, bạn có thể muốn tắt physics interpolation và sử dụng một cách khác, hoặc dùng tick rate cao, giúp giảm các độ trễ này.

Tại sao lại nhìn vào quá khứ? Tại sao không dự đoán tương lai?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có một lựa chọn thay thế cho cách này: thay vì nội suy giữa tick trước và tick hiện tại, chúng ta dùng toán học để *ngoại suy* vào tương lai. Chúng ta cố dự đoán object *sẽ ở đâu*, thay vì hiển thị vị trí trước đó của nó. Điều này có thể thực hiện được và có thể sẽ được cung cấp như một tùy chọn trong tương lai, nhưng có một số nhược điểm đáng kể:

- Dự đoán có thể không chính xác, đặc biệt khi một object va chạm với object khác trong physics tick. - Khi dự đoán không chính xác, object có thể được ngoại suy đến một vị trí "bất khả thi", chẳng hạn như bên trong một bức tường. - Nếu tốc độ di chuyển chậm, những dự đoán không chính xác này có thể không gây ra vấn đề quá lớn. - Khi dự đoán không chính xác, object có thể phải nhảy hoặc snap trở lại đường đi đã được hiệu chỉnh. Điều này có thể gây khó chịu về mặt hình ảnh.

Interpolation với timestep cố định
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong Godot, toàn bộ hệ thống này được gọi là physics interpolation (nội suy vật lý), nhưng bạn cũng có thể nghe thấy nó được gọi là **"fixed timestep interpolation"**, vì nó thực hiện nội suy giữa các đối tượng được di chuyển với một fixed timestep (số lần physics tick mỗi giây). Xét trên một số phương diện, thuật ngữ thứ hai chính xác hơn, vì nó cũng có thể được dùng để nội suy các đối tượng không được điều khiển bởi physics.

.. tip:: Although physics interpolation is usually a good choice, there are
         các trường hợp ngoại lệ mà bạn có thể chọn không sử dụng physics interpolation tích hợp sẵn của Godot (hoặc chỉ sử dụng ở mức giới hạn). Một nhóm ví dụ là các game multiplayer qua internet. Các game multiplayer thường nhận thông tin dựa trên tick hoặc timing từ những người chơi khác hay từ server, và những thông tin này có thể không trùng với các physics tick cục bộ, vì vậy một kỹ thuật nội suy tùy chỉnh thường có thể phù hợp hơn.
