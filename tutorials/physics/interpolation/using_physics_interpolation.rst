.. _doc_using_physics_interpolation:

Sử dụng physics interpolation
=============================

Làm thế nào để tích hợp physics interpolation vào một game Godot? Có lưu ý nào không?

Chúng tôi đã cố gắng làm cho hệ thống dễ sử dụng nhất có thể, và nhiều game hiện có sẽ hoạt động mà chỉ cần thay đổi rất ít. Tuy vậy, có một số tình huống cần được xử lý đặc biệt, và chúng sẽ được mô tả dưới đây.

Bật thiết lập physics interpolation
-----------------------------------

Bước đầu tiên là bật physics interpolation trong
:ref:`Project Settings > Physics > Common > Physics Interpolation<class_ProjectSettings_property_physics/common/physics_interpolation>`
Bây giờ bạn có thể chạy game.

Có khả năng là mọi thứ trông không khác biệt quá nhiều, đặc biệt nếu bạn đang chạy physics ở mức 60 TPS hoặc bội số của mức này. Tuy nhiên, có khá nhiều việc hơn đang diễn ra ở phía sau.

.. tip::

    Để chuyển một game hiện có sang sử dụng interpolation, bạn rất nên tạm thời đặt
    :ref:`Project Settings > Physics > Common > Physics Tick per Second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>`
    thành một giá trị thấp như ``10``, điều này sẽ làm các vấn đề về interpolation dễ nhận thấy hơn.

Chuyển gần như toàn bộ logic game từ _process sang _physics_process
-------------------------------------------------------------------

Yêu cầu cơ bản nhất đối với physics interpolation (có thể bạn đã thực hiện điều này) là bạn nên di chuyển các object và thực hiện logic game trên chúng trong ``_physics_process`` (chạy ở một physics tick) thay vì ``_process`` (chạy trên một frame được render). Điều này có nghĩa là các script của bạn thường nên thực hiện phần lớn quá trình xử lý trong ``_physics_process``, bao gồm phản hồi input và AI.

Chỉ thiết lập transform của các object trong các physics tick cho phép interpolation tự động xử lý các transform *giữa* các physics tick, đồng thời đảm bảo game sẽ chạy giống nhau trên bất kỳ máy nào. Ngoài ra, điều này còn giảm mức sử dụng CPU nếu game render ở FPS cao, vì logic AI (chẳng hạn) sẽ không còn chạy trên mọi frame được render.

.. note:: If you attempt to set the transform of interpolated objects *outside* the
          physics tick, các phép tính cho vị trí đã được nội suy sẽ không chính xác và bạn sẽ gặp hiện tượng giật. Hiện tượng giật này có thể không xuất hiện trên máy của bạn, nhưng *sẽ* xảy ra với một số người chơi. Vì lý do này, nên tránh thiết lập transform của các object được nội suy bên ngoài physics tick. Godot sẽ cố gắng đưa ra cảnh báo trong editor nếu phát hiện trường hợp này.

.. tip:: This is only a *soft rule*. There are some occasions where you might want
         để dịch chuyển các object bên ngoài physics tick (chẳng hạn khi bắt đầu một level hoặc hồi sinh các object). Tuy vậy, nhìn chung, bạn nên áp dụng các transform từ physics tick.


Đảm bảo mọi chuyển động gián tiếp đều diễn ra trong các physics tick
--------------------------------------------------------------------

Hãy lưu ý rằng trong Godot, các node có thể được di chuyển không chỉ trực tiếp trong các script của bạn, mà còn bởi các phương thức tự động như tweening, animation và navigation. Tất cả các phương thức này cũng nên được thiết lập thời gian hoạt động theo physics tick thay vì theo từng frame ("idle"), **nếu** bạn đang dùng chúng để di chuyển các object (*các phương thức này cũng có thể được dùng để điều khiển những thuộc tính không được nội suy*).

.. note:: Also consider that nodes can be moved not just by moving themselves, but
          mà còn bằng cách di chuyển các node cha trong :ref:`SceneTree<class_SceneTree>`. Vì vậy, việc di chuyển các node cha cũng chỉ nên diễn ra trong các physics tick.

Chọn tốc độ physics tick
------------------------

Khi sử dụng physics interpolation, việc render được tách rời khỏi physics và bạn có thể chọn bất kỳ giá trị nào phù hợp với game của mình. Bạn không còn bị giới hạn ở các giá trị là bội số của tốc độ làm mới màn hình của người dùng (để gameplay không bị giật khi đạt FPS mục tiêu).

Hướng dẫn sơ bộ:

.. csv-table::
    :header: "Low tick rates (10-30)", "Medium tick rates (30-60)", "High tick rates (60+)"
    :widths: 20, 20, 20

    "Hiệu suất CPU tốt hơn","Hành vi physics tốt trong các scene phức tạp","Hoạt động tốt với physics nhanh" "Tăng một chút độ trễ input","Phù hợp cho game góc nhìn thứ nhất","Phù hợp cho game đua xe" "Hành vi physics đơn giản"

.. note:: You can always change the tick rate as you develop, it is as simple as
          thay đổi thiết lập project.

Gọi ``reset_physics_interpolation()`` khi dịch chuyển các object
----------------------------------------------------------------

Phần lớn thời gian, interpolation là điều bạn muốn giữa hai physics tick. Tuy nhiên, có một tình huống mà *có thể* bạn không muốn dùng nó. Đó là khi bạn đặt các object lần đầu hoặc di chuyển chúng đến một vị trí mới. Trong trường hợp này, bạn không muốn có chuyển động mượt giữa vị trí trước đó của object (ví dụ: origin) và vị trí ban đầu — bạn muốn di chuyển tức thời.

Giải pháp cho việc này là gọi hàm :ref:`Node.reset_physics_interpolation<class_Node_method_reset_physics_interpolation>`. Về bản chất, hàm này đặt *transform trước đó* được lưu trữ nội bộ của object bằng với *transform hiện tại*. Điều này đảm bảo rằng khi nội suy giữa hai transform giống hệt nhau này, sẽ không có chuyển động nào.

Ngay cả khi bạn quên gọi hàm này, trong hầu hết tình huống thường sẽ không có vấn đề gì (đặc biệt ở tốc độ tick cao). Đây là việc bạn có thể dễ dàng để dành cho giai đoạn hoàn thiện game. Điều tệ nhất có thể xảy ra là xuất hiện chuyển động kéo dài trong khoảng một frame khi bạn di chuyển chúng — bạn sẽ biết khi nào cần đến nó!

Thực tế có hai cách sử dụng ``reset_physics_interpolation()``:

*Bắt đầu đứng yên (ví dụ: player)*

1) Đặt transform ban đầu 2) Gọi ``reset_physics_interpolation()``

Các transform trước đó và hiện tại sẽ giống hệt nhau, do đó không có chuyển động ban đầu.

*Bắt đầu khi đang chuyển động (ví dụ: bullet)*

1) Đặt transform ban đầu 2) Gọi ``reset_physics_interpolation()`` 3) Ngay lập tức đặt transform dự kiến sau physics tick đầu tiên của chuyển động

Transform trước đó sẽ là vị trí bắt đầu, còn transform hiện tại sẽ hoạt động như thể một tick mô phỏng đã diễn ra. Điều này sẽ khiến object bắt đầu di chuyển ngay lập tức, thay vì đứng yên trong một tick rồi mới bắt đầu.

.. important:: Make sure you set the transform and call
               ``reset_physics_interpolation()`` theo đúng thứ tự như trên, nếu không bạn sẽ thấy hiện tượng "streaking" không mong muốn.

Mẹo kiểm thử và debug
---------------------

Ngay cả khi bạn định chạy physics ở mức 60 TPS, để kiểm thử interpolation kỹ lưỡng và đạt gameplay mượt nhất, bạn rất nên tạm thời đặt tốc độ physics tick ở một giá trị thấp như 10 TPS.

Gameplay có thể không hoạt động hoàn hảo, nhưng điều này sẽ giúp bạn dễ dàng nhận thấy hơn những trường hợp cần gọi :ref:`Node.reset_physics_interpolation<class_Node_method_reset_physics_interpolation>` hoặc những trường hợp cần sử dụng interpolation tùy chỉnh của riêng bạn trên, chẳng hạn, một
:ref:`Camera3D<class_Camera3D>`. Once you have these cases fixed, you can set the
đưa tốc độ physics tick trở lại thiết lập mong muốn.

Một lợi ích lớn khác của việc kiểm thử ở tốc độ tick thấp là bạn thường có thể nhận thấy các hệ thống game khác được đồng bộ theo physics tick và gây ra lỗi, từ đó tìm cách xử lý phù hợp. Các ví dụ điển hình bao gồm việc thiết lập các giá trị blend của animation, những giá trị mà bạn có thể quyết định đặt trong ``_process()`` rồi tự nội suy.

.. note::

    Trong 2D, vị trí của các collision shape hiển thị được thể hiện bởi tùy chọn
    :menu:`Debug > Visible Collision Shapes`
    **sẽ** tính đến physics interpolation.

    Ngược lại, trong 3D, vị trí của các collision shape hiển thị **sẽ không** tính đến physics interpolation. Điều này có nghĩa là các collision shape hiển thị có thể trông kém mượt hơn và hơi ở phía trước phần hiển thị của object khi object đang di chuyển. Đây không phải là lỗi, mà là hệ quả của cách physics interpolation được triển khai trong 3D.
