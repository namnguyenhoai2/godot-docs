.. _doc_using_area_2d:

Sử dụng Area2D
==============

Giới thiệu
----------

Godot cung cấp một số đối tượng collision để thực hiện cả việc phát hiện và phản hồi collision. Việc quyết định nên sử dụng loại nào cho dự án có thể gây khó hiểu. Bạn có thể tránh được các vấn đề và đơn giản hóa quá trình phát triển nếu hiểu cách mỗi loại hoạt động cũng như ưu và nhược điểm của chúng. Trong tutorial này, chúng ta sẽ xem xét
:ref:`Area2D <class_Area2D>` node and show some examples of how it can be used.

.. note:: This document assumes you're familiar with Godot's various physics
          các body. Trước tiên, hãy đọc :ref:`doc_physics_introduction`.

Area là gì?
-----------

Area2D xác định một vùng trong không gian 2D. Trong không gian này, bạn có thể phát hiện các
:ref:`CollisionObject2D <class_CollisionObject2D>` nodes overlapping, entering,
và rời khỏi vùng. Area cũng cho phép ghi đè các thuộc tính physics cục bộ. Chúng ta sẽ khám phá từng chức năng này bên dưới.

Các thuộc tính của Area
-----------------------

Area có nhiều thuộc tính mà bạn có thể sử dụng để tùy chỉnh hành vi của chúng.

.. image:: img/area2d_properties.webp

Các phần ``Gravity``, ``Linear Damp`` và ``Angular Damp`` được dùng để cấu hình hành vi ghi đè physics của area. Chúng ta sẽ xem cách sử dụng chúng trong phần *Ảnh hưởng của Area* bên dưới.

``Monitoring`` và ``Monitorable`` được dùng để bật và tắt area.

Phần ``Audio Bus`` cho phép bạn ghi đè âm thanh trong area, chẳng hạn như áp dụng một hiệu ứng âm thanh khi người chơi di chuyển qua đó.

Lưu ý rằng Area2D kế thừa từ :ref:`CollisionObject2D <class_CollisionObject2D>`, vì vậy nó cũng cung cấp các thuộc tính được kế thừa từ class đó. Phần ``Collision`` của ``CollisionObject2D`` là nơi bạn cấu hình collision layer và mask của area.

Phát hiện chồng lấp
-------------------

Có lẽ cách sử dụng phổ biến nhất của các node Area2D là phát hiện tiếp xúc và chồng lấp. Khi cần biết hai object đã chạm vào nhau nhưng không cần collision vật lý, bạn có thể sử dụng một area để thông báo cho bạn về lần tiếp xúc đó.

Ví dụ, giả sử chúng ta đang tạo một đồng xu để người chơi nhặt. Đồng xu không phải là một object rắn - người chơi không thể đứng lên hoặc đẩy nó - chúng ta chỉ muốn nó biến mất khi người chơi chạm vào.

Đây là thiết lập node cho đồng xu:

.. image:: img/area2d_coin_nodes.webp

Để phát hiện chồng lấp, chúng ta sẽ kết nối signal thích hợp trên Area2D. Signal cần sử dụng phụ thuộc vào loại node của người chơi. Nếu người chơi là một area khác, hãy sử dụng ``area_entered``. Tuy nhiên, hãy giả sử người chơi của chúng ta là một ``CharacterBody2D`` (và do đó thuộc loại ``CollisionObject2D``), vì vậy chúng ta sẽ kết nối signal ``body_entered``.

.. note:: If you're not familiar with using signals, see :ref:`doc_signals` for
          một phần giới thiệu.

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

Giờ đây người chơi của chúng ta có thể thu thập các đồng xu!

Một số ví dụ sử dụng khác:

- Area rất phù hợp cho đạn và các projectile khác có va chạm và gây sát thương nhưng không cần physics nào khác, chẳng hạn như nảy. - Sử dụng một area hình tròn lớn quanh kẻ địch để xác định bán kính "phát hiện" của nó. Khi người chơi ở bên ngoài area, kẻ địch không thể "nhìn thấy" người chơi. - "Camera an ninh" - Trong một level lớn có nhiều camera, gắn area vào mỗi camera và kích hoạt chúng khi người chơi đi vào.

Xem :ref:`doc_your_first_2d_game` để biết ví dụ về việc sử dụng Area2D trong một game.

Ảnh hưởng của Area
------------------

Cách sử dụng chính thứ hai của các node area là thay đổi physics. Theo mặc định, area sẽ không làm điều này, nhưng bạn có thể bật chức năng này bằng thuộc tính ``Space Override``. Khi các area chồng lấp, chúng được xử lý theo thứ tự ``Priority`` (các area có priority cao hơn được xử lý trước). Có bốn tùy chọn ghi đè:

- *Combine* - Area cộng các giá trị của nó vào kết quả đã được tính cho đến thời điểm hiện tại. - *Replace* - Area thay thế các thuộc tính physics và các area có priority thấp hơn sẽ bị bỏ qua. - *Combine-Replace* - Area cộng các giá trị gravity/damping của nó vào kết quả đã được tính cho đến thời điểm hiện tại (theo thứ tự priority), đồng thời bỏ qua mọi area có priority thấp hơn. - *Replace-Combine* - Area thay thế mọi giá trị gravity/damping đã được tính cho đến thời điểm hiện tại nhưng vẫn tiếp tục tính toán các area còn lại.

Bằng cách sử dụng các thuộc tính này, bạn có thể tạo ra hành vi rất phức tạp với nhiều area chồng lấp.

Các thuộc tính physics có thể được ghi đè là:

- *Gravity* - Độ mạnh của gravity bên trong area. - *Gravity Direction* - Vector này không cần được chuẩn hóa. - *Linear Damp* - Tốc độ các object dừng chuyển động - vận tốc tuyến tính mất đi mỗi giây. - *Angular Damp* - Tốc độ các object dừng quay - vận tốc góc mất đi mỗi giây.

Gravity điểm
~~~~~~~~~~~~

Thuộc tính ``Gravity Point`` cho phép bạn tạo một "attractor". Gravity trong area sẽ được tính hướng về một điểm, được xác định bởi thuộc tính ``Point Center``. Các giá trị tương đối với Area2D, vì vậy chẳng hạn sử dụng ``(0, 0)`` sẽ hút các object về tâm của area.

Ví dụ
~~~~~

Project mẫu đính kèm bên dưới có ba area minh họa việc ghi đè physics.

.. image:: img/area2d_override.gif

Bạn có thể tải project này tại đây: `area_2d_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/area_2d_starter.zip>`_
