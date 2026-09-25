.. _doc_using_physics_interpolation:

Sử dụng nội suy vật lý
======================

Làm thế nào để tích hợp nội suy vật lý vào một game Godot? Có điều gì cần lưu ý không?

Chúng tôi đã cố gắng làm cho hệ thống dễ sử dụng nhất có thể, và nhiều game hiện có sẽ hoạt động với rất ít thay đổi. Tuy vậy, có một số tình huống cần được xử lý đặc biệt, và chúng sẽ được mô tả dưới đây.

Bật thiết lập nội suy vật lý
----------------------------

Bước đầu tiên là bật nội suy vật lý trong
:ref:`Project Settings > Physics > Common > Physics Interpolation <class_ProjectSettings_property_physics/common/physics_interpolation>` Bây giờ bạn có thể chạy game.

Có khả năng là bạn sẽ không nhận thấy khác biệt quá lớn, đặc biệt nếu bạn chạy vật lý ở mức 60 TPS hoặc một bội số của mức này. Tuy nhiên, có khá nhiều hoạt động diễn ra phía sau.

.. tip::

    Để chuyển một game hiện có sang sử dụng nội suy, bạn rất nên tạm thời đặt
    :ref:`Project Settings > Physics > Common > Physics Tick per Second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>` thành một giá trị thấp như ``10``, để các vấn đề về nội suy trở nên dễ nhận thấy hơn.

Chuyển (gần như) toàn bộ logic game từ _process sang _physics_process
---------------------------------------------------------------------

Yêu cầu cơ bản nhất đối với nội suy vật lý (có thể bạn đã thực hiện điều này) là bạn nên di chuyển các đối tượng và thực hiện logic game trên chúng trong ``_physics_process`` (chạy theo mỗi physics tick), thay vì ``_process`` (chạy theo mỗi frame được render). Điều này có nghĩa là các script của bạn thường nên thực hiện phần lớn quá trình xử lý trong ``_physics_process``, bao gồm cả việc phản hồi input và AI.

Chỉ thiết lập transform của các đối tượng trong các physics tick cho phép cơ chế nội suy tự động xử lý các transform *between* physics tick, đồng thời đảm bảo game chạy giống nhau trên mọi máy. Ngoài ra, cách này còn giảm mức sử dụng CPU nếu game render ở FPS cao, vì logic AI (chẳng hạn) sẽ không còn chạy ở mỗi frame được render.

.. note:: Nếu bạn cố gắng thiết lập transform của các đối tượng được nội suy *outside* physics tick, phép tính vị trí nội suy sẽ không chính xác và bạn sẽ thấy hiện tượng giật. Hiện tượng giật này có thể không nhìn thấy trên máy của bạn, nhưng *will* xảy ra với một số người chơi. Vì lý do này, nên tránh thiết lập transform của các đối tượng được nội suy bên ngoài physics tick. Godot sẽ cố gắng đưa ra cảnh báo trong editor nếu phát hiện trường hợp này.

.. tip:: Đây chỉ là một *soft rule*. Có một số trường hợp bạn có thể muốn dịch chuyển đối tượng bên ngoài physics tick (chẳng hạn khi bắt đầu một level hoặc hồi sinh các đối tượng). Tuy nhiên, nhìn chung, bạn nên áp dụng các transform từ physics tick.


Đảm bảo mọi chuyển động gián tiếp diễn ra trong các physics tick
----------------------------------------------------------------

Hãy lưu ý rằng trong Godot, các node không chỉ có thể được di chuyển trực tiếp trong các script của bạn mà còn bằng những phương thức tự động như tweening, animation và navigation. Tất cả các phương thức này cũng nên được thiết lập thời gian hoạt động theo physics tick thay vì mỗi frame ("idle"), **if** bạn sử dụng chúng để di chuyển các đối tượng (*these methods can also be used to control properties that are not interpolated*).

.. note:: Cũng cần lưu ý rằng các node không chỉ có thể được di chuyển bằng cách tự di chuyển chúng, mà còn bằng cách di chuyển các node cha trong :ref:`SceneTree<class_SceneTree>`. Vì vậy, chuyển động của các node cha cũng chỉ nên diễn ra trong các physics tick.

Chọn tốc độ physics tick
------------------------

Khi sử dụng nội suy vật lý, việc render được tách khỏi vật lý và bạn có thể chọn bất kỳ giá trị nào phù hợp với game của mình. Bạn không còn bị giới hạn ở các giá trị là bội số của tốc độ làm mới màn hình của người dùng (để gameplay không bị giật nếu đạt FPS mục tiêu).

Hướng dẫn chung:

.. csv-table::
    :header: "Low tick rates (10-30)", "Medium tick rates (30-60)", "High tick rates (60+)"
    :widths: 20, 20, 20

    "Better CPU performance","Good physics behavior in complex scenes","Good with fast physics"
    "Add some delay to input","Good for first person games","Good for racing games"
    "Simple physics behaviour"

.. note:: Bạn luôn có thể thay đổi tốc độ tick trong quá trình phát triển; việc này đơn giản như thay đổi thiết lập của project.

Gọi ``reset_physics_interpolation()`` khi dịch chuyển các đối tượng
-------------------------------------------------------------------

Trong hầu hết thời gian, nội suy là điều bạn muốn giữa hai physics tick. Tuy nhiên, có một tình huống mà nó *not* phải là điều bạn muốn. Đó là khi bạn đặt các đối tượng lần đầu hoặc di chuyển chúng đến một vị trí mới. Trong trường hợp này, bạn không muốn chuyển động mượt mà giữa vị trí đối tượng từng ở (ví dụ: origin) và vị trí ban đầu; bạn muốn di chuyển tức thời.

Giải pháp là gọi hàm :ref:`Node.reset_physics_interpolation<class_Node_method_reset_physics_interpolation>`. Về bản chất, hàm này thiết lập *previous transform* được lưu trữ nội bộ của đối tượng bằng với *current transform*. Điều này đảm bảo rằng khi nội suy giữa hai transform giống nhau này, sẽ không có chuyển động nào xảy ra.

Ngay cả khi bạn quên gọi hàm này, trong hầu hết tình huống thường cũng không có vấn đề gì (đặc biệt ở tốc độ tick cao). Đây là việc bạn có thể dễ dàng để dành cho giai đoạn hoàn thiện game. Điều tệ nhất có thể xảy ra là bạn thấy chuyển động kéo dài trong khoảng một frame khi di chuyển chúng; bạn sẽ biết khi nào mình cần hàm này!

Thực tế có hai cách sử dụng ``reset_physics_interpolation()``:

*Bắt đầu đứng yên (ví dụ: người chơi)*

1) Thiết lập transform ban đầu
2) Gọi ``reset_physics_interpolation()``

Transform trước đó và transform hiện tại sẽ giống hệt nhau, nên không có chuyển động ban đầu.

*Bắt đầu chuyển động (ví dụ: đạn)*

1) Thiết lập transform ban đầu
2) Gọi ``reset_physics_interpolation()``
3) Ngay lập tức thiết lập transform dự kiến sau tick chuyển động đầu tiên

Transform trước đó sẽ là vị trí bắt đầu, còn transform hiện tại sẽ hoạt động như thể một tick mô phỏng đã diễn ra. Điều này sẽ khiến đối tượng bắt đầu chuyển động ngay lập tức, thay vì đứng yên trong một tick.

.. important:: Hãy đảm bảo bạn thiết lập transform và gọi ``reset_physics_interpolation()`` theo đúng thứ tự như trên, nếu không bạn sẽ thấy hiện tượng "kéo dài" không mong muốn.

Mẹo kiểm thử và gỡ lỗi
----------------------

Ngay cả khi bạn dự định chạy physics ở 60 TPS, để kiểm thử kỹ lưỡng interpolation và có gameplay mượt mà nhất, bạn rất nên tạm thời đặt tần số tick của physics ở một giá trị thấp như 10 TPS.

Gameplay có thể không hoạt động hoàn hảo, nhưng điều này sẽ giúp bạn dễ nhận thấy hơn những trường hợp cần gọi :ref:`Node.reset_physics_interpolation<class_Node_method_reset_physics_interpolation>`, hoặc những trường hợp cần sử dụng interpolation tùy chỉnh của riêng bạn trên, chẳng hạn, một
:ref:`Camera3D<class_Camera3D>`. Sau khi đã khắc phục những trường hợp này, bạn có thể đặt lại tần số tick của physics về mức mong muốn.

Một lợi ích lớn khác của việc kiểm thử ở tần số tick thấp là bạn thường có thể nhận ra các hệ thống khác của game được đồng bộ theo tick của physics và gây ra lỗi hiển thị mà bạn có thể muốn xử lý tránh. Các ví dụ điển hình bao gồm việc đặt các giá trị blend của animation, vốn có thể được bạn quyết định đặt trong ``_process()`` và tự thực hiện interpolation.

.. note::

    Trong 2D, vị trí của các hình dạng collision hiển thị được hiển thị bởi
    tùy chọn :menu:`Debug > Visible Collision Shapes` **sẽ** tính đến physics interpolation.

    Ngược lại, trong 3D, vị trí của các hình dạng collision hiển thị **sẽ không** tính đến physics interpolation. Điều này có nghĩa là các hình dạng collision hiển thị có thể trông kém mượt hơn và hơi ở phía trước phần hiển thị của đối tượng khi đối tượng đang di chuyển. Đây không phải là lỗi, mà là hệ quả của cách physics interpolation được triển khai trong 3D.
