.. _doc_animation_track_types:

Các loại Animation Track
========================

Trang này tổng quan về các loại track có sẵn cho node animation player của Godot, bên cạnh các property track mặc định.

.. seealso::

   Chúng tôi giả định rằng bạn đã đọc :ref:`doc_introduction_animation`, trong đó trình bày các kiến thức cơ bản, bao gồm cả property track.

.. image:: img/track_types.webp

Property Track
--------------

Đây là loại track cơ bản nhất. Xem :ref:`doc_introduction_animation`.

Position 3D / Rotation 3D / Scale 3D Track
------------------------------------------

Các track biến đổi 3D này điều khiển vị trí, phép xoay và tỷ lệ của một đối tượng 3D. Chúng giúp việc tạo animation cho phép biến đổi của đối tượng 3D dễ dàng hơn so với việc sử dụng các property track thông thường.

Loại track này được thiết kế cho các animation được nhập từ model 3D bên ngoài và có thể giảm dung lượng tài nguyên nhờ compression.

Blend Shape Track
-----------------

Blend shape track được tối ưu hóa để tạo animation cho blend shape trong :ref:`MeshInstance3D <class_MeshInstance3D>`.

Loại track này được thiết kế cho các animation được nhập từ model 3D bên ngoài và có thể giảm dung lượng tài nguyên nhờ compression.

Call Method Track
-----------------

Call method track cho phép bạn gọi một function tại một thời điểm chính xác trong animation. Ví dụ, bạn có thể gọi ``queue_free()`` để xóa một node khi animation chết kết thúc.

.. note:: Các event được đặt trên call method track sẽ không được thực thi khi animation được xem trước trong editor vì lý do an toàn.

Để tạo track như vậy trong editor, hãy nhấp vào "Add Track -> Call Method Track." Sau đó, một cửa sổ sẽ mở ra và cho phép bạn chọn node liên kết với track. Để gọi một trong các method của node, hãy nhấp chuột phải vào timeline và chọn "Insert Key". Một cửa sổ sẽ mở ra với danh sách các method có sẵn. Nhấp đúp vào một method để hoàn tất việc tạo keyframe.

.. image:: img/node_methods.webp

Để thay đổi lời gọi method hoặc các đối số của nó, hãy nhấp vào key rồi chuyển đến inspector dock. Tại đó, bạn có thể thay đổi method cần gọi. Nếu mở rộng phần "Args", bạn sẽ thấy danh sách các đối số có thể chỉnh sửa.

.. image:: img/node_method_args.webp

Để tạo track như vậy bằng code, hãy truyền một dictionary chứa tên và các tham số của method đích dưới dạng Variant cho ``key`` trong ``Animation.track_insert_key()``. Các key và giá trị tương ứng được yêu cầu như sau:

+--------------+----------------------------------------------------+
| **Key**      | **Value**                                          |
+==============+====================================================+
| ``"method"`` | Tên của method dưới dạng ``String``                |
+--------------+----------------------------------------------------+
| ``"args"``   | Các đối số truyền cho function dưới dạng ``Array`` |
+--------------+----------------------------------------------------+

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tạo call method track.
    func create_method_animation_track():
        # Lấy hoặc tạo animation mà từ đó method đích sẽ được gọi.
        var animation = $AnimationPlayer.get_animation("idle")
        # Lấy hoặc tạo animation track của method đích.
        var track_index = animation.add_track(Animation.TYPE_METHOD)
        # Tạo các đối số cho method đích jump().
        var jump_velocity = -400.0
        var multiplier = randf_range(.8, 1.2)
        # Lấy hoặc tạo một dictionary chứa tên và các đối số của method đích.
        var method_dictionary = {
            "method": "jump",
            "args": [jump_velocity, multiplier],
        }

        # Đặt scene-tree path đến node chứa method đích.
        animation.track_set_path(track_index, ".")
        # Thêm dictionary làm key cho animation method track.
        animation.track_insert_key(track_index, 0.6, method_dictionary, 0)


    # Method đích sẽ được gọi từ animation.
    func jump(jump_velocity, multiplier):
        velocity.y = jump_velocity * multiplier

 .. code-tab:: csharp

    // Tạo call method track.
    public void CreateAnimationTrack()
    {
        // Lấy reference đến AnimationPlayer.
        var animationPlayer = GetNode<AnimationPlayer>("AnimationPlayer");
        // Lấy hoặc tạo animation mà từ đó method đích sẽ được gọi.
        var animation = animationPlayer.GetAnimation("idle");
        // Lấy hoặc tạo animation track của method đích.
        var trackIndex = animation.AddTrack(Animation.TrackType.Method);
        // Tạo các đối số cho method đích Jump().
        var jumpVelocity = -400.0;
        var multiplier = GD.RandRange(.8, 1.2);
        // Lấy hoặc tạo một dictionary chứa tên và các đối số của method đích.
        var methodDictionary = new Godot.Collections.Dictionary
        {
            { "method", MethodName.Jump },
            { "args", new Godot.Collections.Array { jumpVelocity, multiplier } }
        };

        // Đặt scene-tree path đến node chứa method đích.
        animation.TrackSetPath(trackIndex, ".");
        // Thêm dictionary làm key cho animation method track.
        animation.TrackInsertKey(trackIndex, 0.6, methodDictionary, 0);
    }


    // Method đích sẽ được gọi từ animation.
    private void Jump(float jumpVelocity, float multiplier)
    {
        Velocity = new Vector2(Velocity.X, jumpVelocity * multiplier);
    }

Bezier Curve Track
------------------

Bezier curve track tương tự property track, nhưng cho phép bạn tạo animation cho giá trị của một property bằng bezier curve.

.. note::

    Bezier curve track và property track không thể được blend trong :ref:`AnimationPlayer <class_AnimationPlayer>` và :ref:`AnimationTree <class_AnimationTree>`.

Để tạo một track, hãy nhấp vào "Add Track -> Bezier Curve Track". Giống như với property track, bạn cần chọn một node và một property để tạo animation. Để mở trình chỉnh sửa bezier curve, hãy nhấp vào biểu tượng curve ở bên phải animation track.

.. image:: img/bezier_curve_icon.webp

Trong editor, các key được biểu thị bằng những hình thoi đặc và các hình thoi viền nối với chúng bằng một đường thẳng sẽ điều khiển hình dạng của curve.

.. tip::

    Để có độ chính xác cao hơn khi thao tác thủ công với các curve, bạn có thể muốn thay đổi mức zoom của editor. Thanh trượt ở góc dưới bên phải editor có thể được dùng để phóng to và thu nhỏ theo trục thời gian; bạn cũng có thể làm vậy bằng :kbd:`Ctrl + Shift + Mouse wheel`. Sử dụng :kbd:`Ctrl + Alt + Mouse wheel` sẽ phóng to và thu nhỏ theo trục Y

.. image:: img/bezier_curves.webp

Khi một keyframe được chọn (không phải handle), bạn có thể chọn chế độ handle trong bảng mở bằng cách nhấp chuột phải của editor:

- Free: Cho phép bạn định hướng một manipulator theo bất kỳ hướng nào mà không ảnh hưởng đến vị trí của manipulator còn lại.
- Linear: Không cho phép xoay manipulator và vẽ một đồ thị tuyến tính.
- Balanced: Khiến các manipulator xoay cùng nhau, nhưng khoảng cách giữa key và một manipulator không được đối xứng.
- Mirrored: Khiến vị trí của một manipulator đối xứng hoàn hảo với manipulator còn lại, bao gồm cả khoảng cách của chúng đến key.

.. image:: img/manipulator_modes.webp

Audio Playback Track
--------------------

Nếu muốn tạo animation có âm thanh, bạn cần tạo một audio playback track. Để tạo track này, scene của bạn phải có một trong các node AudioStreamPlayer, AudioStreamPlayer2D hoặc AudioStreamPlayer3D. Khi tạo track, bạn phải chọn một trong các node đó.

Để phát âm thanh trong animation, hãy kéo và thả một tệp âm thanh từ dock hệ thống tệp vào track animation. Bạn sẽ thấy dạng sóng của tệp âm thanh trong track.

.. image:: img/audio_track.webp

Để xóa âm thanh khỏi animation, bạn có thể nhấp chuột phải vào âm thanh đó rồi chọn "Delete Key(s)", hoặc nhấp vào âm thanh đó và nhấn phím :kbd:`Del`.

Chế độ hòa trộn cho phép bạn chọn có điều chỉnh âm lượng âm thanh khi hòa trộn trong :ref:`AnimationTree <class_AnimationTree>` hay không.

.. image:: img/blend_mode.webp

Track phát animation
--------------------

Các track phát animation cho phép bạn sắp xếp trình tự animation của những node animation player khác trong một scene. Ví dụ, bạn có thể dùng chúng để tạo animation cho nhiều nhân vật trong một cut-scene.

Để tạo track phát animation, hãy chọn "New Track -> Animation Playback Track."

Sau đó, chọn animation player mà bạn muốn liên kết với track.

Để thêm một animation vào track, hãy nhấp chuột phải vào track và chèn một key. Chọn key vừa tạo để chọn một animation trong dock inspector.

.. image:: img/animation_player_animation.webp

Nếu một animation đang phát và bạn muốn dừng animation đó sớm, bạn có thể tạo một key và đặt key đó thành `[STOP]` trong inspector.

.. note:: Nếu bạn instance một scene chứa animation player vào scene của mình, bạn cần bật "Editable Children" trong scene tree để truy cập animation player của scene đó. Ngoài ra, một animation player không thể tham chiếu chính nó.
