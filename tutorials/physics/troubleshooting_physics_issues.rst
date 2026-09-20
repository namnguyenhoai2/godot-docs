.. _doc_troubleshooting_physics_issues:

Khắc phục sự cố vật lý
======================

Khi làm việc với physics engine, bạn có thể gặp phải những kết quả ngoài dự kiến.

Mặc dù nhiều vấn đề trong số này có thể được giải quyết thông qua cấu hình, một số lại là kết quả của các lỗi trong engine. Để xem các vấn đề đã biết liên quan đến physics engine, hãy xem `open physics-related issues on GitHub <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Atopic%3Aphysics>`__. Xem qua `closed issues <https://github.com/godotengine/godot/issues?q=+is%3Aclosed+is%3Aissue+label%3Atopic%3Aphysics>`__ cũng có thể giúp giải đáp các câu hỏi liên quan đến cách physics engine hoạt động.

Các object đi xuyên qua nhau khi di chuyển ở tốc độ cao
-------------------------------------------------------

Hiện tượng này được gọi là *tunneling*. Việc bật **Continuous CD** (Continuous Collision Detection) trong các thuộc tính của RigidBody đôi khi có thể giải quyết vấn đề này. Nếu cách này không hiệu quả, bạn có thể thử các giải pháp khác sau:

- Làm cho các collision shape tĩnh dày hơn. Ví dụ: nếu bạn có một sàn mỏng mà player không thể rơi xuống dưới vì một lý do nào đó, bạn có thể làm collider dày hơn phần hiển thị trực quan của sàn. - Điều chỉnh collision shape của object di chuyển nhanh tùy theo tốc độ di chuyển của nó. Object di chuyển càng nhanh thì collision shape càng phải nhô ra ngoài object nhiều hơn để đảm bảo nó có thể va chạm với các bức tường mỏng đáng tin cậy hơn. - Tăng :ref:`Physics Ticks per Second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>` trong Project Settings nâng cao. Mặc dù điều này mang lại các lợi ích khác (chẳng hạn như mô phỏng ổn định hơn và giảm độ trễ input), nó làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các hệ số nhân của giá trị mặc định ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để có hình ảnh mượt mà trên hầu hết màn hình.

Các object xếp chồng không ổn định và bị rung lắc
-------------------------------------------------

Mặc dù có vẻ là một vấn đề đơn giản, việc triển khai mô phỏng RigidBody ổn định với các object xếp chồng là rất khó trong physics engine. Nguyên nhân là do việc tích hợp các lực tác động ngược chiều nhau. Càng có nhiều object xếp chồng, các lực tác động ngược chiều nhau càng mạnh. Cuối cùng, điều này khiến mô phỏng trở nên rung lắc, làm cho các object không thể nằm yên trên nhau mà không di chuyển.

Tăng tần suất mô phỏng vật lý có thể giúp giảm bớt vấn đề này. Để thực hiện, hãy tăng :ref:`Physics Ticks per Second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>` trong Project Settings nâng cao. Lưu ý rằng việc này làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các hệ số nhân của giá trị mặc định ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để có hình ảnh mượt mà trên hầu hết màn hình.

Trong 3D, chuyển physics engine từ GodotPhysics mặc định sang Jolt cũng có thể cải thiện độ ổn định. Xem :ref:`doc_using_jolt_physics` để biết thêm thông tin.

Các physics body hoặc collision shape được scale không va chạm chính xác
------------------------------------------------------------------------

Godot hiện chưa hỗ trợ scale physics body hoặc collision shape. Để khắc phục tạm thời, hãy thay đổi extents của collision shape thay vì thay đổi scale của nó. Nếu bạn cũng muốn thay đổi scale của phần hiển thị trực quan, hãy thay đổi scale của phần hiển thị trực quan bên dưới (Sprite2D, MeshInstance3D, …) và thay đổi riêng extents của collision shape. Trong trường hợp này, hãy đảm bảo collision shape không phải là node con của phần hiển thị trực quan.

Vì các resource được chia sẻ theo mặc định, bạn sẽ phải làm cho resource của collision shape trở nên duy nhất nếu không muốn thay đổi này được áp dụng cho tất cả các node sử dụng cùng resource collision shape trong scene. Có thể thực hiện việc này theo hai cách:

- Trong editor, bằng cách nhấp vào :menu:`Make Unique` trong menu thả xuống resource CollisionShape ở inspector, sau đó thay đổi kích thước của nó. - Trong một script, bằng cách gọi ``duplicate()`` trong một script trên resource collision shape *trước khi* thay đổi kích thước của nó.

Các object mỏng bị rung lắc khi nằm trên sàn
--------------------------------------------

Điều này có thể do một trong hai nguyên nhân:

- Collision shape của sàn quá mỏng. - Collision shape của RigidBody quá mỏng.

Trong trường hợp đầu tiên, có thể giảm bớt vấn đề bằng cách làm collision shape của sàn dày hơn. Ví dụ: nếu bạn có một sàn mỏng mà player không thể rơi xuống dưới vì một lý do nào đó, bạn có thể làm collider dày hơn phần hiển thị trực quan của sàn.

Trong trường hợp thứ hai, vấn đề này thường chỉ có thể được giải quyết bằng cách tăng tần suất mô phỏng vật lý (vì việc làm collision shape dày hơn sẽ gây ra sự không khớp giữa phần hiển thị trực quan của RigidBody và va chạm của nó).

Trong cả hai trường hợp, việc tăng tần suất mô phỏng vật lý cũng có thể giúp giảm bớt vấn đề này. Để thực hiện, hãy tăng
:ref:`Physics Ticks per Second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>`
trong Project Settings nâng cao. Lưu ý rằng việc này làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các hệ số nhân của giá trị mặc định ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để có hình ảnh mượt mà trên hầu hết màn hình.

Các collision shape dạng cylinder không ổn định
-----------------------------------------------

Chuyển physics engine từ GodotPhysics mặc định sang Jolt sẽ giúp collision shape dạng cylinder đáng tin cậy hơn. Xem :ref:`doc_using_jolt_physics` để biết thêm thông tin.

Trong quá trình chuyển từ Bullet sang GodotPhysics ở Godot 4, collision shape dạng cylinder phải được triển khai lại từ đầu. Tuy nhiên, collision shape dạng cylinder là một trong những shape khó hỗ trợ nhất, đó là lý do nhiều physics engine khác không cung cấp bất kỳ hỗ trợ nào cho chúng. Hiện vẫn còn một số lỗi đã biết với collision shape dạng cylinder.

Nếu vẫn sử dụng GodotPhysics, hiện tại chúng tôi khuyến nghị dùng collision shape dạng box hoặc capsule cho character. Box thường mang lại độ tin cậy tốt nhất, nhưng có nhược điểm là khiến character chiếm nhiều không gian hơn theo đường chéo. Collision shape dạng capsule không có nhược điểm này, nhưng hình dạng của chúng có thể khiến việc platforming chính xác trở nên khó khăn hơn.

Mô phỏng VehicleBody không ổn định, đặc biệt ở tốc độ cao
---------------------------------------------------------

Khi một physics body di chuyển ở tốc độ cao, nó đi được một quãng đường lớn giữa mỗi physics step. Ví dụ, khi sử dụng quy ước 1 unit = 1 meter trong 3D, một phương tiện di chuyển với tốc độ 360 km/h sẽ đi được 100 unit mỗi giây. Với tần suất mô phỏng vật lý mặc định là 60 Hz, phương tiện di chuyển khoảng ~1.67 unit trong mỗi physics tick. Điều này có nghĩa là các object nhỏ có thể bị phương tiện bỏ qua hoàn toàn (do tunneling), đồng thời mô phỏng nói chung cũng có rất ít dữ liệu để xử lý ở tốc độ cao như vậy.

Các phương tiện di chuyển nhanh có thể hưởng lợi đáng kể từ việc tăng tần suất mô phỏng vật lý. Để thực hiện, hãy tăng
:ref:`Physics Ticks per Second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>`
trong Project Settings nâng cao. Lưu ý rằng việc này làm tăng mức sử dụng CPU và có thể không phù hợp với các nền tảng mobile/web. Nên ưu tiên các hệ số nhân của giá trị mặc định ``60`` (chẳng hạn như ``120``, ``180`` hoặc ``240``) để có hình ảnh mượt mà trên hầu hết màn hình.

Va chạm gây ra hiện tượng nảy khi object di chuyển qua các tile
---------------------------------------------------------------

Đây là một vấn đề đã biết trong physics engine, xảy ra do object va vào các cạnh của một shape, mặc dù cạnh đó được một shape khác che phủ. Điều này có thể xảy ra cả trong 2D lẫn 3D.

Cách tốt nhất để khắc phục tạm thời vấn đề này là tạo một collider "composite". Điều này có nghĩa là thay vì mỗi tile có collision riêng, bạn tạo một collision shape duy nhất đại diện cho collision của một nhóm tile. Thông thường, bạn nên chia các collider composite theo từng island (nghĩa là mỗi nhóm tile tiếp xúc với nhau sẽ có collider riêng).

Việc sử dụng collider composite cũng có thể cải thiện hiệu năng mô phỏng vật lý trong một số trường hợp. Tuy nhiên, vì collision shape composite phức tạp hơn nhiều, điều này không phải lúc nào cũng mang lại hiệu năng tổng thể tốt hơn.

.. tip::

    Trong Godot 4.5 trở lên, collider composite sẽ tự động được tạo khi sử dụng node TileMapLayer. Kích thước chunk (``16`` tile trên mỗi trục theo mặc định) có thể được thiết lập bằng thuộc tính **Physics Quadrant Size** trong inspector của TileMapLayer. Giá trị lớn hơn mang lại collision đáng tin cậy hơn, nhưng phải đánh đổi bằng tốc độ cập nhật chậm hơn khi TileMap được thay đổi.

Framerate giảm khi một object chạm vào object khác
--------------------------------------------------

Điều này có thể là do một trong các object đang sử dụng collision shape quá phức tạp. Collision shape lồi nên sử dụng số lượng shape ít nhất có thể vì lý do hiệu năng. Khi dựa vào việc tự động tạo của Godot, có thể bạn đã tạo ra hàng chục, thậm chí hàng trăm shape cho một collision resource dạng lồi duy nhất.

Trong một số trường hợp, thay collider lồi bằng một vài collision shape nguyên thủy (box, sphere hoặc capsule) có thể mang lại hiệu năng tốt hơn.

Vấn đề này cũng có thể xảy ra với StaticBody sử dụng collision trimesh (concave) rất chi tiết. Trong trường hợp này, hãy sử dụng một phần hình học của level được đơn giản hóa làm collider. Điều này không chỉ cải thiện đáng kể hiệu năng mô phỏng vật lý, mà còn có thể cải thiện độ ổn định bằng cách loại bỏ các chi tiết nhỏ và khe hẹp khỏi quá trình xét va chạm.

Trong 3D, chuyển physics engine từ GodotPhysics mặc định sang Jolt cũng có thể cải thiện hiệu năng. Xem :ref:`doc_using_jolt_physics` để biết thêm thông tin.

Framerate đột ngột giảm xuống mức rất thấp khi vượt quá một lượng mô phỏng vật lý nhất định
-------------------------------------------------------------------------------------------

Điều này xảy ra vì physics engine không thể theo kịp tần suất mô phỏng dự kiến. Trong trường hợp này, framerate sẽ bắt đầu giảm, nhưng engine chỉ được phép mô phỏng một số lượng physics step nhất định trong mỗi frame được render. Tình trạng này tiếp diễn khiến framerate không ngừng giảm cho đến khi đạt mức rất thấp (thường là 1-2 FPS) và được gọi là *physics spiral of death*.

Để tránh điều này, bạn nên kiểm tra các tình huống trong dự án có thể khiến quá nhiều mô phỏng vật lý diễn ra đồng thời (hoặc sử dụng các hình dạng va chạm quá phức tạp). Nếu không thể tránh những tình huống này, bạn có thể tăng thiết lập dự án **Max Physics Steps per Frame** và/hoặc giảm **Physics Ticks per Second** để giảm nhẹ vấn đề.

Mô phỏng vật lý trở nên không đáng tin cậy khi ở xa gốc tọa độ thế giới
-----------------------------------------------------------------------

Nguyên nhân là do lỗi độ chính xác dấu phẩy động, trở nên rõ rệt hơn khi mô phỏng vật lý diễn ra càng xa gốc tọa độ thế giới. Vấn đề này cũng ảnh hưởng đến quá trình rendering, dẫn đến chuyển động camera bị rung lắc khi ở xa gốc tọa độ thế giới. Xem :ref:`doc_large_world_coordinates` để biết thêm thông tin.
