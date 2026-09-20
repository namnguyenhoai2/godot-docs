:article_outdated: True

.. _doc_recording_with_microphone:

Ghi âm bằng microphone
======================

Godot hỗ trợ ghi âm trong game trên Windows, macOS, Linux, Android và iOS.

Một bản demo đơn giản được đưa vào các dự án demo chính thức và sẽ được dùng để hỗ trợ cho tutorial này: `<https://github.com/godotengine/godot-demo-projects/tree/master/audio/mic_record>`_.

Bạn cần bật audio input trong project setting :ref:`Audio > Driver > Enable Input<class_ProjectSettings_property_audio/driver/enable_input>`, nếu không bạn sẽ chỉ nhận được các tệp âm thanh rỗng.

Trên iOS và iPadOS, bạn cũng cần đặt setting nâng cao **Audio > General > iOS > Session Category** để bao gồm **Record** hoặc **Play and Record**.

Cấu trúc của bản demo
---------------------

Bản demo chỉ gồm một scene. Scene này có hai phần chính: GUI và audio.

Chúng ta sẽ tập trung vào phần audio. Trong bản demo này, một bus có tên ``Record`` cùng với effect ``Record`` được tạo để xử lý việc ghi âm. Một ``AudioStreamPlayer`` có tên ``AudioStreamRecord`` được dùng để ghi âm.

.. image:: img/record_bus.png

.. image:: img/record_stream_player.png

.. tabs::
 .. code-tab:: gdscript GDScript

    var effect
    var recording


    func _ready():
        # Chúng ta lấy index của bus "Record".
        var idx = AudioServer.get_bus_index("Record")
        # Sau đó dùng nó để lấy effect đầu tiên, vốn đã được định nghĩa
        # dưới dạng một resource "AudioEffectRecord".
        effect = AudioServer.get_bus_effect(idx, 0)

 .. code-tab:: csharp

    private AudioEffectRecord _effect;
    private AudioStreamSample _recording;

    public override void _Ready()
    {
        // Chúng ta lấy index của bus "Record".
        int idx = AudioServer.GetBusIndex("Record");
        // Sau đó dùng nó để lấy effect đầu tiên, vốn đã được định nghĩa
        // dưới dạng một resource "AudioEffectRecord".
        _effect = (AudioEffectRecord)AudioServer.GetBusEffect(idx, 0);
    }

Việc ghi âm được xử lý bởi resource :ref:`class_AudioEffectRecord`, trong đó có ba method:
:ref:`get_recording() <class_AudioEffectRecord_method_get_recording>`,
:ref:`is_recording_active() <class_AudioEffectRecord_method_is_recording_active>`,
và :ref:`set_recording_active() <class_AudioEffectRecord_method_set_recording_active>`.

.. tabs::
  .. code-tab:: gdscript GDScript

    func _on_record_button_pressed():
        if effect.is_recording_active():
            recording = effect.get_recording()
            $PlayButton.disabled = false
            $SaveButton.disabled = false
            effect.set_recording_active(false)
            $RecordButton.text = "Record"
            $Status.text = ""
        else:
            $PlayButton.disabled = true
            $SaveButton.disabled = true
            effect.set_recording_active(true)
            $RecordButton.text = "Stop"
            $Status.text = "Recording..."

  .. code-tab:: csharp

    private void OnRecordButtonPressed()
    {
        if (_effect.IsRecordingActive())
        {
            _recording = _effect.GetRecording();
            GetNode<Button>("PlayButton").Disabled = false;
            GetNode<Button>("SaveButton").Disabled = false;
            _effect.SetRecordingActive(false);
            GetNode<Button>("RecordButton").Text = "Record";
            GetNode<Label>("Status").Text = "";
        }
        else
        {
            GetNode<Button>("PlayButton").Disabled = true;
            GetNode<Button>("SaveButton").Disabled = true;
            _effect.SetRecordingActive(true);
            GetNode<Button>("RecordButton").Text = "Stop";
            GetNode<Label>("Status").Text = "Recording...";
        }
    }

Khi bắt đầu bản demo, effect ghi âm chưa hoạt động. Khi người dùng nhấn ``RecordButton``, effect được bật bằng ``set_recording_active(true)``.

Ở lần nhấn nút tiếp theo, vì ``effect.is_recording_active()`` là ``true``, stream đã ghi có thể được lưu vào biến ``recording`` bằng cách gọi ``effect.get_recording()``.

.. tabs::
  .. code-tab:: gdscript GDScript

    func _on_play_button_pressed():
        print(recording)
        print(recording.format)
        print(recording.mix_rate)
        print(recording.stereo)
        var data = recording.get_data()
        print(data.size())
        $AudioStreamPlayer.stream = recording
        $AudioStreamPlayer.play()

  .. code-tab:: csharp

    private void OnPlayButtonPressed()
    {
        GD.Print(_recording);
        GD.Print(_recording.Format);
        GD.Print(_recording.MixRate);
        GD.Print(_recording.Stereo);
        byte[] data = _recording.Data;
        GD.Print(data.Length);
        var audioStreamPlayer = GetNode<AudioStreamPlayer>("AudioStreamPlayer");
        audioStreamPlayer.Stream = _recording;
        audioStreamPlayer.Play();
    }

Để phát lại bản ghi, bạn gán bản ghi làm stream của ``AudioStreamPlayer`` rồi gọi ``play()``.

.. tabs::
  .. code-tab:: gdscript GDScript

    func _on_save_button_pressed():
        var save_path = $SaveButton/Filename.text
        recording.save_to_wav(save_path)
        $Status.text = "Saved WAV file to: %s\n(%s)" % [save_path, ProjectSettings.globalize_path(save_path)]

  .. code-tab:: csharp

    private void OnSaveButtonPressed()
    {
        string savePath = GetNode<LineEdit>("SaveButton/Filename").Text;
        _recording.SaveToWav(savePath);
        GetNode<Label>("Status").Text = string.Format("Saved WAV file to: {0}\n({1})", savePath, ProjectSettings.GlobalizePath(savePath));
    }

Để lưu bản ghi, bạn gọi ``save_to_wav()`` với đường dẫn đến một tệp. Trong bản demo này, đường dẫn được người dùng xác định thông qua một ô nhập ``LineEdit``.
