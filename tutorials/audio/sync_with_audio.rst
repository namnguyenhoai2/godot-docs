:article_outdated: True

.. _doc_sync_with_audio:

Đồng bộ gameplay với âm thanh và nhạc
=====================================

Giới thiệu
----------

Trong bất kỳ ứng dụng hoặc trò chơi nào, việc phát âm thanh và nhạc sẽ có một độ trễ nhỏ. Đối với trò chơi, độ trễ này thường nhỏ đến mức không đáng kể. Hiệu ứng âm thanh sẽ phát ra sau vài mili giây kể từ khi gọi bất kỳ hàm play() nào. Đối với nhạc, điều này không quan trọng vì trong hầu hết trò chơi, nhạc không tương tác với gameplay.

Tuy vậy, đối với một số trò chơi (chủ yếu là trò chơi rhythm), có thể cần đồng bộ hành động của người chơi với một sự kiện xảy ra trong bài hát (thường đồng bộ theo BPM). Để làm được điều này, thông tin thời gian chính xác hơn về vị trí phát hiện tại sẽ rất hữu ích.

Việc đạt được độ chính xác thời gian phát rất cao là khó. Điều này là do có nhiều yếu tố ảnh hưởng trong quá trình phát âm thanh:

* Âm thanh được trộn theo từng khối (không liên tục), tùy thuộc vào kích thước của các audio buffer được sử dụng (hãy kiểm tra latency trong cài đặt project). * Các khối âm thanh đã trộn không được phát ngay lập tức. * Graphics API hiển thị trễ hai hoặc ba frame. * Khi phát trên TV, độ trễ có thể tăng thêm do quá trình xử lý hình ảnh.

Cách phổ biến nhất để giảm latency là thu nhỏ audio buffer (một lần nữa, bằng cách chỉnh cài đặt latency trong cài đặt project). Vấn đề là khi latency quá nhỏ, việc trộn âm thanh sẽ cần nhiều CPU hơn đáng kể. Điều này làm tăng nguy cơ bị ngắt quãng (âm thanh bị rè do một mix callback bị mất).

Đây là một sự đánh đổi phổ biến, vì vậy Godot đi kèm các giá trị mặc định hợp lý và thường không cần thay đổi.

Cuối cùng, vấn đề không nằm ở độ trễ nhỏ này mà là ở việc đồng bộ graphics và audio cho những trò chơi cần điều đó. Có một số helper giúp lấy thông tin thời gian phát chính xác hơn.

Sử dụng system clock để đồng bộ
-------------------------------

Như đã đề cập trước đó, nếu bạn gọi :ref:`AudioStreamPlayer.play()<class_AudioStreamPlayer_method_play>`, âm thanh sẽ không bắt đầu ngay lập tức mà chỉ bắt đầu khi audio thread xử lý khối tiếp theo.

Không thể tránh được độ trễ này, nhưng có thể ước tính nó bằng cách gọi :ref:`AudioServer.get_time_to_next_mix()<class_AudioServer_method_get_time_to_next_mix>`.

Output latency (những gì xảy ra sau khi trộn) cũng có thể được ước tính bằng cách gọi :ref:`AudioServer.get_output_latency()<class_AudioServer_method_get_output_latency>`.

Cộng hai giá trị này lại, ta có thể đoán gần như chính xác thời điểm âm thanh hoặc nhạc bắt đầu phát ra từ loa trong *_process()*:

.. tabs::
 .. code-tab:: gdscript GDScript

    var time_begin
    var time_delay


    func _ready():
        time_begin = Time.get_ticks_usec()
        time_delay = AudioServer.get_time_to_next_mix() + AudioServer.get_output_latency()
        $Player.play()


    func _process(delta):
        # Lấy từ ticks.
        var time = (Time.get_ticks_usec() - time_begin) / 1000000.0
        # Bù cho latency.
        time -= time_delay
        # Có thể nhỏ hơn 0 (chưa bắt đầu).
        time = max(0, time)
        print("Time is: ", time)

 .. code-tab:: csharp

    private double _timeBegin;
    private double _timeDelay;

    public override void _Ready()
    {
        _timeBegin = Time.GetTicksUsec();
        _timeDelay = AudioServer.GetTimeToNextMix() + AudioServer.GetOutputLatency();
        GetNode<AudioStreamPlayer>("Player").Play();
    }

    public override void _Process(double delta)
    {
        double time = (Time.GetTicksUsec() - _timeBegin) / 1000000.0d;
        time = Math.Max(0.0d, time - _timeDelay);
        GD.Print(string.Format("Time is: {0}", time));
    }


Tuy nhiên, về lâu dài, vì clock của phần cứng âm thanh không bao giờ hoàn toàn đồng bộ với system clock, thông tin thời gian sẽ dần bị lệch.

Đối với một rhythm game trong đó bài hát bắt đầu và kết thúc sau vài phút, cách tiếp cận này là phù hợp (và đây là cách tiếp cận được khuyến nghị). Đối với một trò chơi có thời lượng phát dài hơn nhiều, trò chơi cuối cùng sẽ bị mất đồng bộ và cần một cách tiếp cận khác.

Sử dụng sound hardware clock để đồng bộ
---------------------------------------

Sử dụng :ref:`AudioStreamPlayer.get_playback_position()<class_AudioStreamPlayer_method_get_playback_position>` để lấy vị trí hiện tại của bài hát có vẻ lý tưởng, nhưng bản thân giá trị này không hữu ích lắm. Giá trị sẽ tăng theo từng khối (mỗi khi audio callback trộn xong một khối âm thanh), vì vậy nhiều lần gọi có thể trả về cùng một giá trị. Ngoài ra, giá trị này cũng sẽ không đồng bộ với loa vì những lý do đã đề cập trước đó.

Để bù cho đầu ra theo "khối", có một hàm có thể hỗ trợ: :ref:`AudioServer.get_time_since_last_mix()<class_AudioServer_method_get_time_since_last_mix>`.


Cộng giá trị trả về từ hàm này vào *get_playback_position()* sẽ tăng độ chính xác:

.. tabs::
 .. code-tab:: gdscript GDScript

    var time = $Player.get_playback_position() + AudioServer.get_time_since_last_mix()

 .. code-tab:: csharp

    double time = GetNode<AudioStreamPlayer>("Player").GetPlaybackPosition() + AudioServer.GetTimeSinceLastMix();


Để tăng độ chính xác, hãy trừ thông tin latency (thời gian cần thiết để nghe được âm thanh sau khi âm thanh đã được trộn):

.. tabs::
 .. code-tab:: gdscript GDScript

    var time = $Player.get_playback_position() + AudioServer.get_time_since_last_mix() - AudioServer.get_output_latency()

 .. code-tab:: csharp

    double time = GetNode<AudioStreamPlayer>("Player").GetPlaybackPosition() + AudioServer.GetTimeSinceLastMix() - AudioServer.GetOutputLatency();

Kết quả có thể hơi giật do cách nhiều thread hoạt động. Chỉ cần kiểm tra để bảo đảm giá trị không nhỏ hơn giá trị ở frame trước (nếu nhỏ hơn thì loại bỏ). Đây cũng là cách tiếp cận kém chính xác hơn cách trước, nhưng sẽ hoạt động với các bài hát có độ dài bất kỳ hoặc khi đồng bộ bất kỳ thứ gì (chẳng hạn như hiệu ứng âm thanh) với nhạc.

Dưới đây là đoạn code trước đó sử dụng cách tiếp cận này:

.. tabs::
 .. code-tab:: gdscript GDScript


    func _ready():
        $Player.play()


    func _process(delta):
        var time = $Player.get_playback_position() + AudioServer.get_time_since_last_mix()
        # Bù cho output latency.
        time -= AudioServer.get_output_latency()
        print("Time is: ", time)

 .. code-tab:: csharp

    public override void _Ready()
    {
        GetNode<AudioStreamPlayer>("Player").Play();
    }

    public override void _Process(double delta)
    {
        double time = GetNode<AudioStreamPlayer>("Player").GetPlaybackPosition() + AudioServer.GetTimeSinceLastMix();
        // Bù cho output latency.
        time -= AudioServer.GetOutputLatency();
        GD.Print(string.Format("Time is: {0}", time));
    }
