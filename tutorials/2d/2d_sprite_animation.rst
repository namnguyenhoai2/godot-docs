.. _doc_2d_sprite_animation:

Hoạt ảnh sprite 2D
==================

Giới thiệu
----------

Trong hướng dẫn này, bạn sẽ học cách tạo các nhân vật hoạt ảnh 2D bằng lớp AnimatedSprite2D và AnimationPlayer. Thông thường, khi tạo hoặc tải xuống một nhân vật hoạt ảnh, bạn sẽ nhận được nhân vật đó theo một trong hai dạng: các hình ảnh riêng lẻ hoặc một sprite sheet duy nhất chứa tất cả các khung hình của hoạt ảnh. Cả hai dạng đều có thể được tạo hoạt ảnh trong Godot bằng lớp AnimatedSprite2D.

Trước tiên, chúng ta sẽ sử dụng :ref:`AnimatedSprite2D <class_AnimatedSprite2D>` để tạo hoạt ảnh cho một tập hợp các hình ảnh riêng lẻ. Sau đó, chúng ta sẽ tạo hoạt ảnh cho một sprite sheet bằng lớp này. Cuối cùng, chúng ta sẽ tìm hiểu một cách khác để tạo hoạt ảnh cho sprite sheet bằng :ref:`AnimationPlayer <class_AnimationPlayer>` và thuộc tính *Animation* của :ref:`Sprite2D <class_Sprite2D>`.

.. note:: Hình minh họa cho các ví dụ sau do https://opengameart.org/users/ansimuz và tgfcoder thực hiện.

Hình ảnh riêng lẻ với AnimatedSprite2D
--------------------------------------

Trong trường hợp này, bạn có một tập hợp các hình ảnh, mỗi hình chứa một khung hình hoạt ảnh của nhân vật. Trong ví dụ này, chúng ta sẽ sử dụng hoạt ảnh sau:

.. image:: img/2d_animation_run_preview.gif

Bạn có thể tải các hình ảnh tại đây: `2d_sprite_animation_assets.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/2d_sprite_animation_assets.zip>`_

Giải nén các hình ảnh và đặt chúng vào thư mục dự án của bạn. Thiết lập cây cảnh với các node sau:

.. image:: img/2d_animation_tree1.webp

.. note:: Node gốc cũng có thể là :ref:`Area2D <class_Area2D>` hoặc
          :ref:`RigidBody2D <class_RigidBody2D>`. The animation will still be
          được tạo theo cách tương tự. Sau khi hoàn tất hoạt ảnh, bạn có thể gán một hình dạng cho CollisionShape2D. Xem
          :ref:`Physics Introduction <doc_physics_introduction>` để biết thêm thông tin.

Bây giờ hãy chọn ``AnimatedSprite2D`` và trong thuộc tính *SpriteFrames* của nó, chọn "New SpriteFrames".

.. image:: img/2d_animation_new_spriteframes.webp

Nhấp vào resource SpriteFrames mới và bạn sẽ thấy một panel mới xuất hiện ở cuối cửa sổ trình chỉnh sửa:

.. image:: img/2d_animation_spriteframes.webp

Từ dock FileSystem ở bên trái, kéo 8 hình ảnh riêng lẻ vào phần giữa của panel SpriteFrames. Ở bên trái, đổi tên hoạt ảnh từ "default" thành "run".

.. image:: img/2d_animation_spriteframes_done.webp

Sử dụng các nút "Play" ở phía trên bên phải của ô nhập *Filter Animations* để xem trước hoạt ảnh. Bây giờ bạn sẽ thấy hoạt ảnh đang chạy trong viewport. Tuy nhiên, hoạt ảnh hơi chậm. Để khắc phục, hãy thay đổi thiết lập *Speed (FPS)* trong panel SpriteFrames thành 10.

Bạn có thể thêm các hoạt ảnh khác bằng cách nhấp vào nút "Add Animation" và thêm các hình ảnh khác.

Điều khiển hoạt ảnh
~~~~~~~~~~~~~~~~~~~

Sau khi hoàn tất hoạt ảnh, bạn có thể điều khiển hoạt ảnh bằng code sử dụng các phương thức ``play()`` và ``stop()``. Dưới đây là một ví dụ ngắn để phát hoạt ảnh khi giữ phím mũi tên phải và dừng hoạt ảnh khi nhả phím.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @onready var _animated_sprite = $AnimatedSprite2D

    func _process(_delta):
        if Input.is_action_pressed("ui_right"):
            _animated_sprite.play("run")
        else:
            _animated_sprite.stop()

 .. code-tab:: csharp

    using Godot;

    public partial class Character : CharacterBody2D
    {
        private AnimatedSprite2D _animatedSprite;

        public override void _Ready()
        {
            _animatedSprite = GetNode<AnimatedSprite2D>("AnimatedSprite2D");
        }

        public override void _Process(double delta)
        {
            if (Input.IsActionPressed("ui_right"))
            {
                _animatedSprite.Play("run");
            }
            else
            {
                _animatedSprite.Stop();
            }
        }
    }


Sprite sheet với AnimatedSprite2D
---------------------------------

Bạn cũng có thể dễ dàng tạo hoạt ảnh từ một sprite sheet bằng lớp ``AnimatedSprite2D``. Chúng ta sẽ sử dụng sprite sheet thuộc phạm vi công cộng sau đây:

.. image:: img/2d_animation_frog_spritesheet.png

Nhấp chuột phải vào hình ảnh và chọn "Save Image As" để tải xuống, sau đó sao chép hình ảnh vào thư mục dự án của bạn.

Thiết lập cây cảnh giống như trước đây khi sử dụng các hình ảnh riêng lẻ. Chọn ``AnimatedSprite2D`` và trong thuộc tính *SpriteFrames* của nó, chọn "New SpriteFrames".

Nhấp vào resource SpriteFrames mới. Lần này, khi panel bên dưới xuất hiện, hãy chọn "Add frames from a Sprite Sheet".

.. image:: img/2d_animation_add_from_spritesheet.webp

Bạn sẽ được yêu cầu mở một tệp. Hãy chọn sprite sheet của bạn.

Một cửa sổ mới sẽ mở ra và hiển thị sprite sheet của bạn. Việc đầu tiên bạn cần làm là thay đổi số lượng hình ảnh theo chiều dọc và chiều ngang trong sprite sheet. Trong sprite sheet này, chúng ta có bốn hình ảnh theo chiều ngang và hai hình ảnh theo chiều dọc.

.. image:: img/2d_animation_spritesheet_select_rows.webp

Tiếp theo, hãy chọn các khung hình từ sprite sheet mà bạn muốn đưa vào hoạt ảnh. Chúng ta sẽ chọn bốn khung hình ở trên cùng, sau đó nhấp vào "Add 4 frames" để tạo hoạt ảnh.

.. image:: img/2d_animation_spritesheet_selectframes.webp

Bây giờ bạn sẽ thấy hoạt ảnh của mình trong danh sách các hoạt ảnh ở panel bên dưới. Nhấp đúp vào default để đổi tên hoạt ảnh thành jump.

.. image:: img/2d_animation_spritesheet_animation.webp

Cuối cùng, hãy nhấp vào nút phát trong trình chỉnh sửa SpriteFrames để xem chú ếch của bạn nhảy!

.. image:: img/2d_animation_play_spritesheet_animation.webp


Sprite sheet với AnimationPlayer
--------------------------------

Một cách khác để tạo hoạt ảnh khi sử dụng sprite sheet là dùng một
:ref:`Sprite2D <class_Sprite2D>` node tiêu chuẩn để hiển thị texture, sau đó tạo hoạt ảnh cho việc thay đổi từ texture này sang texture khác bằng :ref:`AnimationPlayer <class_AnimationPlayer>`.

Hãy xem xét sprite sheet này, chứa 6 khung hình hoạt ảnh:

.. image:: img/2d_animation_player-run.png

Nhấp chuột phải vào hình ảnh và chọn "Save Image As" để tải xuống, sau đó sao chép hình ảnh vào thư mục dự án của bạn.

Mục tiêu của chúng ta là hiển thị lần lượt các hình ảnh này trong một vòng lặp. Bắt đầu bằng cách thiết lập cây cảnh:

.. image:: img/2d_animation_tree2.webp

.. note:: Node gốc cũng có thể là :ref:`Area2D <class_Area2D>` hoặc
          :ref:`RigidBody2D <class_RigidBody2D>`. The animation will still be
          được tạo theo cách tương tự. Sau khi hoàn tất hoạt ảnh, bạn có thể gán một hình dạng cho CollisionShape2D. Xem
          :ref:`Physics Introduction <doc_physics_introduction>` để biết thêm thông tin.

Kéo spritesheet vào thuộc tính *Texture* của Sprite, và bạn sẽ thấy toàn bộ sheet được hiển thị trên màn hình. Để cắt nó thành các khung hình riêng lẻ, mở rộng phần *Animation* trong Inspector và đặt *Hframes* thành ``6``. *Hframes* và *Vframes* là số khung hình theo chiều ngang và chiều dọc trong sprite sheet của bạn.

.. image:: img/2d_animation_setframes.webp

Bây giờ hãy thử thay đổi giá trị của thuộc tính *Frame*. Bạn sẽ thấy giá trị này nằm trong khoảng từ ``0`` đến ``5`` và hình ảnh được Sprite2D hiển thị cũng thay đổi tương ứng. Đây là thuộc tính mà chúng ta sẽ tạo hoạt ảnh.

Chọn ``AnimationPlayer`` và nhấp vào nút "Animation", sau đó nhấp vào "New". Đặt tên cho hoạt ảnh mới là "walk". Đặt độ dài hoạt ảnh thành ``0.6`` và nhấp vào nút "Loop" để hoạt ảnh lặp lại.

.. image:: img/2d_animation_new_animation.webp

Bây giờ hãy chọn node ``Sprite2D`` và nhấp vào biểu tượng chìa khóa để thêm một track mới.

.. image:: img/2d_animation_new_track.webp

Tiếp tục thêm các khung hình tại từng điểm trên timeline (mặc định là ``0.1`` giây), cho đến khi bạn có tất cả các khung hình từ 0 đến 5. Bạn sẽ thấy các khung hình thực sự xuất hiện trong track hoạt ảnh:

.. image:: img/2d_animation_full_animation.webp

Nhấn "Play" trên animation để xem nó trông như thế nào.

.. image:: img/2d_animation_running.gif

Điều khiển animation của AnimationPlayer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tương tự như AnimatedSprite2D, bạn có thể điều khiển animation bằng code thông qua các phương thức ``play()`` và ``stop()``. Một lần nữa, dưới đây là ví dụ phát animation khi phím mũi tên phải được nhấn giữ và dừng animation khi nhả phím.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @onready var _animation_player = $AnimationPlayer

    func _process(_delta):
        if Input.is_action_pressed("ui_right"):
            _animation_player.play("walk")
        else:
            _animation_player.stop()

 .. code-tab:: csharp

    using Godot;

    public partial class Character : CharacterBody2D
    {
        private AnimationPlayer _animationPlayer;

        public override void _Ready()
        {
            _animationPlayer = GetNode<AnimationPlayer>("AnimationPlayer");
        }

        public override void _Process(double delta)
        {
            if (Input.IsActionPressed("ui_right"))
            {
                _animationPlayer.Play("walk");
            }
            else
            {
                _animationPlayer.Stop();
            }
        }
    }

.. note:: Nếu cập nhật cả một animation và một property riêng biệt cùng lúc (ví dụ: một platformer có thể cập nhật các property ``h_flip``/``v_flip`` của sprite khi nhân vật xoay người đồng thời bắt đầu animation 'turning'), bạn cần lưu ý rằng ``play()`` không được áp dụng ngay lập tức. Thay vào đó, nó được áp dụng vào lần tiếp theo :ref:`AnimationPlayer <class_AnimationPlayer>` được xử lý. Việc này có thể xảy ra ở frame tiếp theo, gây ra một frame 'glitch', trong đó thay đổi property đã được áp dụng nhưng animation thì chưa. Nếu đây trở thành vấn đề, sau khi gọi ``play()``, bạn có thể gọi ``advance(0)`` để cập nhật animation ngay lập tức.

Tóm tắt
-------

Các ví dụ này minh họa hai class mà bạn có thể sử dụng trong Godot cho animation 2D. ``AnimationPlayer`` phức tạp hơn một chút so với ``AnimatedSprite2D``, nhưng cung cấp thêm nhiều chức năng, vì bạn cũng có thể animate các property khác như vị trí hoặc scale. Class ``AnimationPlayer`` cũng có thể được sử dụng cùng với một ``AnimatedSprite2D``. Hãy thử nghiệm để xem cách nào phù hợp nhất với nhu cầu của bạn.

.. _`2d_sprite_animation_assets.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/2d_sprite_animation_assets.zip
