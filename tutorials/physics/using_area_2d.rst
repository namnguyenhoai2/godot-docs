.. _doc_using_area_2d:

Sử dụng Area2D
==============

Giới thiệu
----------

Godot cung cấp nhiều đối tượng va chạm để hỗ trợ cả việc phát hiện và phản hồi va chạm. Việc quyết định nên sử dụng đối tượng nào cho dự án có thể gây khó hiểu. Bạn có thể tránh được các vấn đề và đơn giản hóa quá trình phát triển nếu hiểu cách từng đối tượng hoạt động cũng như ưu, nhược điểm của chúng. Trong hướng dẫn này, chúng ta sẽ tìm hiểu về
:ref:`Area2D <class_Area2D>` node và xem một số ví dụ về cách sử dụng nó.

.. note:: Tài liệu này giả định rằng bạn đã quen thuộc với nhiều physics body khác nhau của Godot. Trước tiên, hãy đọc :ref:`doc_physics_introduction`.

Area là gì?
-----------

Một Area2D xác định một vùng trong không gian 2D. Trong không gian này, bạn có thể phát hiện các
:ref:`CollisionObject2D <class_CollisionObject2D>` node khác đang chồng lấp, đi vào và đi ra. Area cũng cho phép ghi đè các thuộc tính physics cục bộ. Chúng ta sẽ tìm hiểu từng chức năng này bên dưới.

Các thuộc tính của Area
-----------------------

Area có nhiều thuộc tính mà bạn có thể sử dụng để tùy chỉnh cách hoạt động của chúng.

.. image:: img/area2d_properties.webp

Các phần ``Gravity``, ``Linear Damp`` và ``Angular Damp`` được dùng để cấu hình cách ghi đè physics của Area. Chúng ta sẽ xem cách sử dụng các phần này trong phần *Area influence* bên dưới.

``Monitoring`` và ``Monitorable`` được dùng để bật và tắt Area.

Phần ``Audio Bus`` cho phép bạn ghi đè âm thanh trong Area, chẳng hạn để áp dụng hiệu ứng âm thanh khi người chơi di chuyển qua đó.

Lưu ý rằng Area2D kế thừa từ :ref:`CollisionObject2D <class_CollisionObject2D>`, vì vậy nó cũng cung cấp các thuộc tính kế thừa từ class đó. Phần ``Collision`` của ``CollisionObject2D`` là nơi bạn cấu hình các collision layer và mask của Area.

Phát hiện chồng lấp
-------------------

Có lẽ cách sử dụng phổ biến nhất của các node Area2D là phát hiện tiếp xúc và chồng lấp. Khi cần biết hai đối tượng đã chạm vào nhau nhưng không cần va chạm vật lý, bạn có thể sử dụng Area để nhận thông báo về tiếp xúc đó.

Ví dụ, giả sử chúng ta đang tạo một đồng xu để người chơi nhặt. Đồng xu không phải là một vật thể rắn - người chơi không thể đứng lên hoặc đẩy nó - chúng ta chỉ muốn nó biến mất khi người chơi chạm vào.

Sau đây là thiết lập node cho đồng xu:

.. image:: img/area2d_coin_nodes.webp

Để phát hiện chồng lấp, chúng ta sẽ kết nối signal thích hợp trên Area2D. Signal cần sử dụng phụ thuộc vào loại node của người chơi. Nếu người chơi là một Area khác, hãy sử dụng ``area_entered``. Tuy nhiên, hãy giả sử người chơi của chúng ta là một ``CharacterBody2D`` (và do đó thuộc loại ``CollisionObject2D``), vì vậy chúng ta sẽ kết nối signal ``body_entered``.

.. note:: Nếu bạn chưa quen với việc sử dụng signal, hãy xem :ref:`doc_signals` để biết phần giới thiệu.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Area2D

    func _on_coin_body_entered(body):
        queue_free()

 .. code-tab:: csharp

    using Godot;

    public partial class Coin : Area2D
    {
        private void OnCoinBodyEntered(PhysicsBody2D body)
        {
            QueueFree();
        }
    }

Bây giờ người chơi của chúng ta có thể thu thập các đồng xu!

Một số ví dụ sử dụng khác:

- Area rất phù hợp cho đạn và các projectile khác có khả năng va trúng và gây sát thương nhưng không cần bất kỳ physics nào khác, chẳng hạn như bật nảy.
- Sử dụng một Area hình tròn lớn xung quanh kẻ địch để xác định bán kính "phát hiện" của nó. Khi người chơi ở ngoài Area, kẻ địch không thể "nhìn thấy" người chơi.
- "Camera an ninh" - Trong một level lớn có nhiều camera, gắn Area vào mỗi camera và kích hoạt chúng khi người chơi đi vào.

Xem :ref:`doc_your_first_2d_game` để biết ví dụ về cách sử dụng Area2D trong một game.

Ảnh hưởng của Area
------------------

Cách sử dụng chính thứ hai của các node Area là thay đổi physics. Theo mặc định, Area sẽ không làm điều này, nhưng bạn có thể bật tính năng này bằng thuộc tính ``Space Override``. Khi các Area chồng lấp, chúng được xử lý theo thứ tự ``Priority`` (các Area có độ ưu tiên cao hơn được xử lý trước). Có bốn tùy chọn ghi đè:

- *Combine* - Area cộng các giá trị của nó vào kết quả đã được tính toán cho đến thời điểm hiện tại.
- *Replace* - Area thay thế các thuộc tính physics và các Area có độ ưu tiên thấp hơn sẽ bị bỏ qua.
- *Combine-Replace* - Area cộng các giá trị gravity/damping của nó vào kết quả đã được tính toán cho đến thời điểm hiện tại (theo thứ tự ưu tiên), đồng thời bỏ qua mọi Area có độ ưu tiên thấp hơn.
- *Replace-Combine* - Area thay thế mọi giá trị gravity/damping đã được tính toán cho đến thời điểm hiện tại, nhưng vẫn tiếp tục tính toán các Area còn lại.

Bằng cách sử dụng các thuộc tính này, bạn có thể tạo ra hành vi rất phức tạp với nhiều Area chồng lấp.

Các thuộc tính physics có thể được ghi đè là:

- *Gravity* - Độ mạnh của gravity bên trong Area.
- *Gravity Direction* - Vector này không cần được chuẩn hóa.
- *Linear Damp* - Tốc độ các đối tượng dừng chuyển động - vận tốc tuyến tính bị mất mỗi giây.
- *Angular Damp* - Tốc độ các đối tượng dừng quay - vận tốc góc bị mất mỗi giây.

Gravity điểm
~~~~~~~~~~~~

Thuộc tính ``Gravity Point`` cho phép bạn tạo một "attractor". Gravity trong Area sẽ được tính hướng về một điểm, được xác định bởi thuộc tính ``Point Center``. Các giá trị là tương đối so với Area2D, vì vậy chẳng hạn sử dụng ``(0, 0)`` sẽ hút các đối tượng về tâm của Area.

Ví dụ
~~~~~

Dự án mẫu đính kèm bên dưới có ba Area minh họa việc ghi đè physics.

.. image:: img/area2d_override.gif

Bạn có thể tải dự án này tại đây: `area_2d_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/area_2d_starter.zip>`_

.. _`area_2d_starter.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/area_2d_starter.zip
