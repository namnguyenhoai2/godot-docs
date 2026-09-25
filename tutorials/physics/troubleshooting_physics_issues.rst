.. _doc_troubleshooting_physics_issues:

Khắc phục sự cố vật lý
======================

Khi làm việc với physics engine, bạn có thể gặp phải những kết quả không mong muốn.

Mặc dù nhiều vấn đề trong số này có thể được giải quyết thông qua cấu hình, một số lại là do lỗi của engine. Để xem các vấn đề đã biết liên quan đến physics engine, hãy xem `các vấn đề liên quan đến vật lý đang mở trên GitHub <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Atopic%3Aphysics>`__. Xem qua `các vấn đề đã đóng <https://github.com/godotengine/godot/issues?q=+is%3Aclosed+is%3Aissue+label%3Atopic%3Aphysics>`__ cũng có thể giúp trả lời các câu hỏi liên quan đến hành vi của physics engine.

Các đối tượng đi xuyên qua nhau ở tốc độ cao
--------------------------------------------

Hiện tượng này được gọi là *tunneling*. Bật **Continuous CD** (Continuous Collision Detection) trong các thuộc tính của RigidBody đôi khi có thể giải quyết vấn đề này. Nếu cách này không hiệu quả, bạn có thể thử các giải pháp khác:

- Làm cho các collision shape tĩnh dày hơn. Ví dụ, nếu bạn có một sàn mỏng mà người chơi không thể đi xuống bên dưới vì một lý do nào đó, bạn có thể làm collider dày hơn phần hiển thị trực quan của sàn.
- Điều chỉnh collision shape của đối tượng di chuyển nhanh tùy theo tốc độ di chuyển của nó. Đối tượng di chuyển càng nhanh thì collision shape càng nên mở rộng ra ngoài đối tượng để đảm bảo nó có thể va chạm với các bức tường mỏng đáng tin cậy hơn.
- Tăng :ref:`Physics Ticks per Second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>` trong Project Settings nâng cao. Mặc dù việc này mang lại các lợi ích khác (chẳng hạn như mô phỏng ổn định hơn và giảm input lag), nó làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các bội số của giá trị mặc định là ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để hình ảnh hiển thị mượt mà trên hầu hết các màn hình.

Các đối tượng xếp chồng không ổn định và bị rung lắc
----------------------------------------------------

Dù có vẻ là một vấn đề đơn giản, việc triển khai mô phỏng RigidBody ổn định với các đối tượng xếp chồng là rất khó trong physics engine. Nguyên nhân là do việc tích hợp các lực tác động ngược chiều nhau. Càng có nhiều đối tượng xếp chồng, các lực tác động ngược chiều nhau càng mạnh. Điều này cuối cùng khiến mô phỏng trở nên rung lắc, làm cho các đối tượng không thể nằm yên trên nhau mà không chuyển động.

Tăng tốc độ mô phỏng vật lý có thể giúp giảm bớt vấn đề này. Để thực hiện, hãy tăng :ref:`Physics Ticks per Second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>` trong Project Settings nâng cao. Lưu ý rằng việc này làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các bội số của giá trị mặc định là ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để hình ảnh hiển thị mượt mà trên hầu hết các màn hình.

Trong 3D, chuyển physics engine từ GodotPhysics mặc định sang Jolt cũng có thể cải thiện độ ổn định. Xem :ref:`doc_using_jolt_physics` để biết thêm thông tin.

Các physics body hoặc collision shape đã scale không va chạm chính xác
----------------------------------------------------------------------

Hiện tại Godot không hỗ trợ scale physics body hoặc collision shape. Để khắc phục tạm thời, hãy thay đổi độ rộng của collision shape thay vì thay đổi scale của nó. Nếu bạn cũng muốn thay đổi scale của phần hiển thị trực quan, hãy thay đổi scale của phần hiển thị trực quan bên dưới (Sprite2D, MeshInstance3D, …) và thay đổi riêng độ rộng của collision shape. Trong trường hợp này, hãy đảm bảo collision shape không phải là node con của phần hiển thị trực quan.

Vì các resource được chia sẻ theo mặc định, bạn sẽ phải làm cho resource của collision shape trở nên duy nhất nếu không muốn thay đổi này được áp dụng cho tất cả các node sử dụng cùng một resource collision shape trong scene. Có thể thực hiện việc này theo hai cách:

- Trong editor, bằng cách nhấp vào :menu:`Make Unique` trong trình đơn thả xuống resource CollisionShape ở inspector, sau đó thay đổi kích thước của nó.
- Trong một script, bằng cách gọi ``duplicate()`` trong một script trên resource collision shape *trước khi* thay đổi kích thước của nó.

Các đối tượng mỏng bị rung lắc khi nằm trên sàn
-----------------------------------------------

Điều này có thể do một trong hai nguyên nhân:

- Collision shape của sàn quá mỏng.
- Collision shape của RigidBody quá mỏng.

Trong trường hợp đầu tiên, có thể giảm bớt vấn đề này bằng cách làm collision shape của sàn dày hơn. Ví dụ, nếu bạn có một sàn mỏng mà người chơi không thể đi xuống bên dưới vì một lý do nào đó, bạn có thể làm collider dày hơn phần hiển thị trực quan của sàn.

Trong trường hợp thứ hai, vấn đề này thường chỉ có thể được giải quyết bằng cách tăng tốc độ mô phỏng vật lý (vì việc làm collision shape dày hơn sẽ gây ra sự không đồng nhất giữa phần hiển thị trực quan và va chạm của RigidBody).

Trong cả hai trường hợp, tăng tốc độ mô phỏng vật lý cũng có thể giúp giảm bớt vấn đề này. Để thực hiện, hãy tăng
:ref:`Physics Ticks per Second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>` trong Project Settings nâng cao. Lưu ý rằng việc này làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các bội số của giá trị mặc định là ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để hình ảnh hiển thị mượt mà trên hầu hết các màn hình.

Collision shape hình trụ không ổn định
--------------------------------------

Chuyển physics engine từ GodotPhysics mặc định sang Jolt sẽ giúp collision shape hình trụ đáng tin cậy hơn. Xem :ref:`doc_using_jolt_physics` để biết thêm thông tin.

Trong quá trình chuyển từ Bullet sang GodotPhysics ở Godot 4, collision shape hình trụ phải được triển khai lại từ đầu. Tuy nhiên, collision shape hình trụ là một trong những shape khó hỗ trợ nhất, đó là lý do nhiều physics engine khác không cung cấp hỗ trợ cho chúng. Hiện có một số lỗi đã biết liên quan đến collision shape hình trụ.

Nếu vẫn sử dụng GodotPhysics, hiện tại chúng tôi khuyên bạn nên dùng collision shape dạng hộp hoặc capsule cho nhân vật. Hộp thường mang lại độ tin cậy tốt nhất, nhưng có nhược điểm là khiến nhân vật chiếm nhiều không gian hơn theo đường chéo. Collision shape dạng capsule không có nhược điểm này, nhưng hình dạng của chúng có thể khiến việc platforming chính xác trở nên khó khăn hơn.

Mô phỏng VehicleBody không ổn định, đặc biệt ở tốc độ cao
---------------------------------------------------------

Khi một physics body di chuyển ở tốc độ cao, nó đi được một quãng đường lớn giữa mỗi physics step. Chẳng hạn, khi sử dụng quy ước 1 unit = 1 meter trong 3D, một phương tiện di chuyển ở tốc độ 360 km/h sẽ đi được 100 unit mỗi giây. Với tốc độ mô phỏng vật lý mặc định là 60 Hz, phương tiện di chuyển khoảng 1.67 unit mỗi physics tick. Điều này có nghĩa là các đối tượng nhỏ có thể bị phương tiện hoàn toàn bỏ qua (do tunneling), đồng thời mô phỏng nói chung cũng có rất ít dữ liệu để xử lý ở tốc độ cao như vậy.

Các phương tiện di chuyển nhanh có thể hưởng lợi đáng kể từ việc tăng tốc độ mô phỏng vật lý. Để thực hiện, hãy tăng
:ref:`Physics Ticks per Second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>` trong Project Settings nâng cao. Lưu ý rằng điều này làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các hệ số nhân của giá trị mặc định là ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để hình ảnh hiển thị mượt mà trên hầu hết màn hình.

Va chạm gây ra các chỗ gồ ghề khi một đối tượng di chuyển qua các tile
----------------------------------------------------------------------

Đây là một vấn đề đã biết trong physics engine, xảy ra do đối tượng va vào các cạnh của một shape, mặc dù cạnh đó đã được một shape khác che phủ. Vấn đề này có thể xảy ra cả trong 2D lẫn 3D.

Cách tốt nhất để khắc phục vấn đề này là tạo một collider "composite". Điều này có nghĩa là thay vì để từng tile có collision riêng, bạn tạo một collision shape duy nhất đại diện cho collision của một nhóm tile. Thông thường, bạn nên chia các composite collider theo từng đảo (island), nghĩa là mỗi nhóm tile tiếp xúc với nhau sẽ có collider riêng.

Sử dụng composite collider cũng có thể cải thiện hiệu năng mô phỏng physics trong một số trường hợp. Tuy nhiên, vì composite collision shape phức tạp hơn nhiều, điều này không phải lúc nào cũng mang lại hiệu năng tổng thể tốt hơn.

.. tip::

    Trong Godot 4.5 trở lên, composite collider sẽ được tự động tạo khi sử dụng node TileMapLayer. Kích thước chunk (``16`` tile trên mỗi trục theo mặc định) có thể được thiết lập bằng thuộc tính **Physics Quadrant Size** trong inspector của TileMapLayer. Giá trị lớn hơn giúp collision đáng tin cậy hơn, nhưng phải đánh đổi bằng thời gian cập nhật lâu hơn khi TileMap thay đổi.

Framerate giảm khi một đối tượng chạm vào đối tượng khác
--------------------------------------------------------

Nguyên nhân có thể là một trong các đối tượng đang sử dụng collision shape quá phức tạp. Vì lý do hiệu năng, convex collision shape nên sử dụng số lượng shape ít nhất có thể. Khi dựa vào tính năng tự động tạo của Godot, bạn có thể đã gặp trường hợp một collision resource cho convex shape duy nhất tạo ra hàng chục, thậm chí hàng trăm shape.

Trong một số trường hợp, thay thế convex collider bằng một vài primitive collision shape (box, sphere hoặc capsule) có thể mang lại hiệu năng tốt hơn.

Vấn đề này cũng có thể xảy ra với StaticBody sử dụng collision trimesh (concave) rất chi tiết. Trong trường hợp này, hãy sử dụng một biểu diễn đơn giản hóa của hình học level làm collider. Điều này không chỉ cải thiện đáng kể hiệu năng mô phỏng physics mà còn có thể tăng độ ổn định bằng cách loại bỏ các chi tiết nhỏ và khe hẹp khỏi quá trình xét collision.

Trong 3D, chuyển physics engine từ GodotPhysics mặc định sang Jolt cũng có thể cải thiện hiệu năng. Xem :ref:`doc_using_jolt_physics` để biết thêm thông tin.

Framerate đột ngột giảm xuống mức rất thấp khi vượt quá một lượng mô phỏng physics nhất định
--------------------------------------------------------------------------------------------

Điều này xảy ra vì physics engine không thể theo kịp tốc độ mô phỏng dự kiến. Trong trường hợp này, framerate sẽ bắt đầu giảm, nhưng engine chỉ được phép mô phỏng một số lượng physics step nhất định trong mỗi frame được render. Tình trạng này tạo thành một vòng xoáy khiến framerate liên tục giảm cho đến khi đạt mức rất thấp (thường là 1-2 FPS), và được gọi là *physics spiral of death*.

Để tránh điều này, bạn nên kiểm tra các tình huống trong project có thể khiến số lượng physics simulation diễn ra đồng thời quá lớn (hoặc sử dụng collision shape quá phức tạp). Nếu không thể tránh các tình huống này, bạn có thể tăng project setting **Max Physics Steps per Frame** và/hoặc giảm **Physics Ticks per Second** để giảm nhẹ vấn đề.

Mô phỏng physics không đáng tin cậy khi ở quá xa gốc tọa độ của thế giới
------------------------------------------------------------------------

Nguyên nhân là các lỗi về độ chính xác của số dấu phẩy động, trở nên rõ rệt hơn khi mô phỏng physics diễn ra càng xa gốc tọa độ của thế giới. Vấn đề này cũng ảnh hưởng đến việc render, khiến camera chuyển động rung lắc khi ở quá xa gốc tọa độ của thế giới. Xem :ref:`doc_large_world_coordinates` để biết thêm thông tin.
