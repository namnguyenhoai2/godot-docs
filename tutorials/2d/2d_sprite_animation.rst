.. _doc_2d_sprite_animation:

Hoạt ảnh sprite 2D
==================

Giới thiệu
----------

Trong hướng dẫn này, bạn sẽ học cách tạo các nhân vật 2D có hoạt ảnh bằng lớp AnimatedSprite2D và AnimationPlayer. Thông thường, khi tạo hoặc tải xuống một nhân vật có hoạt ảnh, bạn sẽ nhận được một trong hai dạng: các hình ảnh riêng lẻ hoặc một sprite sheet duy nhất chứa tất cả các khung hình của hoạt ảnh. Cả hai dạng đều có thể được tạo hoạt ảnh trong Godot bằng lớp AnimatedSprite2D.

Trước tiên, chúng ta sẽ sử dụng :ref:`AnimatedSprite2D <class_AnimatedSprite2D>` để tạo hoạt ảnh cho một tập hợp các hình ảnh riêng lẻ. Sau đó, chúng ta sẽ tạo hoạt ảnh cho một sprite sheet bằng lớp này. Cuối cùng, chúng ta sẽ tìm hiểu một cách khác để tạo hoạt ảnh cho sprite sheet bằng :ref:`AnimationPlayer <class_AnimationPlayer>` và thuộc tính *Animation* của :ref:`Sprite2D <class_Sprite2D>`.

.. note:: Art for the following examples by https://opengameart.org/users/ansimuz and tgfcoder.

Các hình ảnh riêng lẻ với AnimatedSprite2D
------------------------------------------

Trong trường hợp này, bạn có một tập hợp các hình ảnh, mỗi hình ảnh chứa một khung hình hoạt ảnh của nhân vật. Trong ví dụ này, chúng ta sẽ sử dụng hoạt ảnh sau:

.. image:: img/2d_animation_run_preview.gif

Bạn có thể tải xuống các hình ảnh tại đây: `2d_sprite_animation_assets.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/2d_sprite_animation_assets.zip>`_

Giải nén các hình ảnh và đặt chúng vào thư mục dự án của bạn. Thiết lập cây cảnh với các nút sau:

.. image:: img/2d_animation_tree1.webp

.. note:: The root node could also be :ref:`Area2D <class_Area2D>` or
          :ref:`RigidBody2D <class_RigidBody2D>`. The animation will still be
          được tạo theo cách tương tự. Sau khi hoàn tất hoạt ảnh, bạn có thể gán một hình dạng cho CollisionShape2D. Xem
          :ref:`Physics Introduction <doc_physics_introduction>` for more
          thông tin.

Bây giờ chọn ``AnimatedSprite2D`` và trong thuộc tính *SpriteFrames* của nó, chọn "New SpriteFrames".

.. image:: img/2d_animation_new_spriteframes.webp

Nhấp vào tài nguyên SpriteFrames mới và bạn sẽ thấy một bảng điều khiển mới xuất hiện ở cuối cửa sổ trình chỉnh sửa:

.. image:: img/2d_animation_spriteframes.webp

Từ dock FileSystem ở bên trái, kéo 8 hình ảnh riêng lẻ vào phần trung tâm của bảng SpriteFrames. Ở bên trái, đổi tên hoạt ảnh từ "default" thành "run".

.. image:: img/2d_animation_spriteframes_done.webp

Sử dụng các nút "Play" ở phía trên bên phải của ô nhập *Filter Animations* để xem trước hoạt ảnh. Bây giờ bạn sẽ thấy hoạt ảnh đang chạy trong khung nhìn. Tuy nhiên, hoạt ảnh hơi chậm. Để khắc phục, hãy thay đổi thiết lập *Speed (FPS)* trong bảng SpriteFrames thành 10.

Bạn có thể thêm các hoạt ảnh khác bằng cách nhấp vào nút "Add Animation" và thêm các hình ảnh khác.

Điều khiển hoạt ảnh
~~~~~~~~~~~~~~~~~~~

Sau khi hoàn tất hoạt ảnh, bạn có thể điều khiển hoạt ảnh thông qua mã bằng các phương thức ``play()`` và ``stop()``. Dưới đây là một ví dụ ngắn để phát hoạt ảnh khi phím mũi tên phải được nhấn giữ và dừng khi thả phím.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @onready var _animated_sprite = $AnimatedSprite2D

    func _process(_delta): if Input.is_action_pressed("ui_right"): _animated_sprite.play("run") else: _animated_sprite.stop()

 .. code-tab:: csharp

    using Godot;

    public partial class Character : CharacterBody2D { private AnimatedSprite2D _animatedSprite;

        public override void _Ready() { _animatedSprite = GetNode<AnimatedSprite2D>("AnimatedSprite2D"); }

        public override void _Process(double delta) { if (Input.IsActionPressed("ui_right")) { _animatedSprite.Play("run"); } else { _animatedSprite.Stop(); } } }


Sprite sheet với AnimatedSprite2D
---------------------------------

Bạn cũng có thể dễ dàng tạo hoạt ảnh từ một sprite sheet bằng lớp ``AnimatedSprite2D``. Chúng ta sẽ sử dụng sprite sheet thuộc phạm vi công cộng sau:

.. image:: img/2d_animation_frog_spritesheet.png

Nhấp chuột phải vào hình ảnh và chọn "Save Image As" để tải xuống, sau đó sao chép hình ảnh vào thư mục dự án của bạn.

Thiết lập cây cảnh giống như trước đây khi sử dụng các hình ảnh riêng lẻ. Chọn ``AnimatedSprite2D`` và trong thuộc tính *SpriteFrames* của nó, chọn "New SpriteFrames".

Nhấp vào tài nguyên SpriteFrames mới. Lần này, khi bảng điều khiển phía dưới xuất hiện, hãy chọn "Add frames from a Sprite Sheet".

.. image:: img/2d_animation_add_from_spritesheet.webp

Bạn sẽ được nhắc mở một tệp. Hãy chọn sprite sheet của bạn.

Một cửa sổ mới sẽ mở ra, hiển thị sprite sheet của bạn. Việc đầu tiên bạn cần làm là thay đổi số lượng hình ảnh theo chiều dọc và chiều ngang trong sprite sheet. Trong sprite sheet này, chúng ta có bốn hình ảnh theo chiều ngang và hai hình ảnh theo chiều dọc.

.. image:: img/2d_animation_spritesheet_select_rows.webp

Tiếp theo, chọn các khung hình trong sprite sheet mà bạn muốn đưa vào hoạt ảnh. Chúng ta sẽ chọn bốn khung hình trên cùng, sau đó nhấp vào "Add 4 frames" để tạo hoạt ảnh.

.. image:: img/2d_animation_spritesheet_selectframes.webp

Bây giờ bạn sẽ thấy hoạt ảnh của mình trong danh sách các hoạt ảnh ở bảng điều khiển phía dưới. Nhấp đúp vào default để đổi tên hoạt ảnh thành jump.

.. image:: img/2d_animation_spritesheet_animation.webp

Cuối cùng, nhấp vào nút phát trong trình chỉnh sửa SpriteFrames để xem chú ếch của bạn nhảy!

.. image:: img/2d_animation_play_spritesheet_animation.webp


Sprite sheet với AnimationPlayer
--------------------------------

Một cách khác để tạo hoạt ảnh khi sử dụng sprite sheet là dùng một
:ref:`Sprite2D <class_Sprite2D>` node to display the texture, and then animating the
cách chuyển từ texture này sang texture khác với :ref:`AnimationPlayer <class_AnimationPlayer>`.

Hãy xem xét sprite sheet này, chứa 6 khung hình hoạt ảnh:

.. image:: img/2d_animation_player-run.png

Nhấp chuột phải vào hình ảnh và chọn "Save Image As" để tải xuống, sau đó sao chép hình ảnh vào thư mục dự án của bạn.

Mục tiêu của chúng ta là lần lượt hiển thị các hình ảnh này theo một vòng lặp. Hãy bắt đầu bằng cách thiết lập cây cảnh:

.. image:: img/2d_animation_tree2.webp

.. note:: The root node could also be :ref:`Area2D <class_Area2D>` or
          :ref:`RigidBody2D <class_RigidBody2D>`. The animation will still be
          được tạo theo cách tương tự. Sau khi hoàn tất hoạt ảnh, bạn có thể gán một hình dạng cho CollisionShape2D. Xem
          :ref:`Physics Introduction <doc_physics_introduction>` for more
          thông tin.

Kéo spritesheet vào thuộc tính *Texture* của Sprite, và bạn sẽ thấy toàn bộ sheet được hiển thị trên màn hình. Để cắt nó thành các khung hình riêng lẻ, hãy mở rộng phần *Animation* trong Inspector và đặt *Hframes* thành ``6``. *Hframes* và *Vframes* là số lượng khung hình theo chiều ngang và chiều dọc trong sprite sheet của bạn.

.. image:: img/2d_animation_setframes.webp

Bây giờ hãy thử thay đổi giá trị của thuộc tính *Frame*. Bạn sẽ thấy giá trị này nằm trong khoảng từ ``0`` đến ``5``, và hình ảnh được Sprite2D hiển thị cũng thay đổi tương ứng. Đây là thuộc tính mà chúng ta sẽ tạo hoạt ảnh.

Chọn ``AnimationPlayer`` và nhấp vào nút "Animation", sau đó chọn "New". Đặt tên cho hoạt ảnh mới là "walk". Đặt độ dài hoạt ảnh thành ``0.6`` và nhấp vào nút "Loop" để hoạt ảnh của chúng ta lặp lại.

.. image:: img/2d_animation_new_animation.webp

Bây giờ chọn nút ``Sprite2D`` và nhấp vào biểu tượng khóa để thêm một track mới.

.. image:: img/2d_animation_new_track.webp

Tiếp tục thêm các khung hình tại mỗi điểm trên dòng thời gian (mặc định là ``0.1`` giây), cho đến khi bạn có tất cả các khung hình từ 0 đến 5. Bạn sẽ thấy các khung hình thực sự xuất hiện trên track hoạt ảnh:

.. image:: img/2d_animation_full_animation.webp

Nhấn "Play" trên hoạt ảnh để xem nó trông như thế nào.

.. image:: img/2d_animation_running.gif

Điều khiển hoạt ảnh AnimationPlayer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tương tự như với AnimatedSprite2D, bạn có thể điều khiển hoạt ảnh thông qua mã bằng các phương thức ``play()`` và ``stop()``. Một lần nữa, dưới đây là ví dụ để phát hoạt ảnh khi phím mũi tên phải được nhấn giữ và dừng khi thả phím.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @onready var _animation_player = $AnimationPlayer

    func _process(_delta): if Input.is_action_pressed("ui_right"): _animation_player.play("walk") else: _animation_player.stop()

 .. code-tab:: csharp

    using Godot;

    public partial class Character : CharacterBody2D { private AnimationPlayer _animationPlayer;

        public override void _Ready() { _animationPlayer = GetNode<AnimationPlayer>("AnimationPlayer"); }

        public override void _Process(double delta) { if (Input.IsActionPressed("ui_right")) { _animationPlayer.Play("walk"); } else { _animationPlayer.Stop(); } } }

.. note:: If updating both an animation and a separate property at once
          (ví dụ, một trò chơi platformer có thể cập nhật các thuộc tính ``h_flip``/``v_flip`` của sprite khi nhân vật xoay người trong lúc bắt đầu một hoạt ảnh 'turning'), điều quan trọng cần lưu ý là ``play()`` không được áp dụng ngay lập tức. Thay vào đó, nó được áp dụng vào lần tiếp theo :ref:`AnimationPlayer <class_AnimationPlayer>` được xử lý. Điều này có thể xảy ra ở khung hình tiếp theo, gây ra một khung hình 'glitch', trong đó thay đổi thuộc tính đã được áp dụng nhưng hoạt ảnh thì chưa. Nếu đây trở thành vấn đề, sau khi gọi ``play()``, bạn có thể gọi ``advance(0)`` để cập nhật hoạt ảnh ngay lập tức.

Tóm tắt
-------

Các ví dụ này minh họa hai lớp mà bạn có thể sử dụng trong Godot để tạo hoạt ảnh 2D. ``AnimationPlayer`` phức tạp hơn một chút so với ``AnimatedSprite2D``, nhưng cung cấp thêm chức năng, vì bạn cũng có thể tạo hoạt ảnh cho các thuộc tính khác như vị trí hoặc tỷ lệ. Lớp ``AnimationPlayer`` cũng có thể được sử dụng với một ``AnimatedSprite2D``. Hãy thử nghiệm để xem cách nào phù hợp nhất với nhu cầu của bạn.
