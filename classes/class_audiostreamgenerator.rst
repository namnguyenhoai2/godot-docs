:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamGenerator.xml.

.. _class_AudioStreamGenerator:

AudioStreamGenerator
====================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một audio stream với các tiện ích để tạo âm thanh theo quy trình.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AudioStreamGenerator** là một loại audio stream không tự phát lại âm thanh; thay vào đó, nó yêu cầu một script tạo dữ liệu âm thanh cho nó. Xem thêm :ref:`AudioStreamGeneratorPlayback<class_AudioStreamGeneratorPlayback>`.

Sau đây là một ví dụ về cách sử dụng nó để tạo sóng hình sin:


.. tabs::

 .. code-tab:: gdscript

    var playback # Sẽ chứa AudioStreamGeneratorPlayback.
    @onready var sample_hz = $AudioStreamPlayer.stream.mix_rate
    var pulse_hz = 440.0 # Tần số của sóng âm thanh.
    var phase = 0.0

    func _ready():
        $AudioStreamPlayer.play()
        playback = $AudioStreamPlayer.get_stream_playback()
        fill_buffer()

    func fill_buffer():
        var increment = pulse_hz / sample_hz
        var frames_available = playback.get_frames_available()

        for i in range(frames_available):
            playback.push_frame(Vector2.ONE * sin(phase * TAU))
            phase = fmod(phase + increment, 1.0)

 .. code-tab:: csharp

    [Export] public AudioStreamPlayer Player { get; set; }

    private AudioStreamGeneratorPlayback _playback; // Sẽ chứa AudioStreamGeneratorPlayback.
    private float _sampleHz;
    private float _pulseHz = 440.0f; // Tần số của sóng âm thanh.
    private double phase = 0.0;

    public override void _Ready()
    {
        if (Player.Stream is AudioStreamGenerator generator) // Ép kiểu thành generator để truy cập MixRate.
        {
            _sampleHz = generator.MixRate;
            Player.Play();
            _playback = (AudioStreamGeneratorPlayback)Player.GetStreamPlayback();
            FillBuffer();
        }
    }

    public void FillBuffer()
    {
        float increment = _pulseHz / _sampleHz;
        int framesAvailable = _playback.GetFramesAvailable();

        for (int i = 0; i < framesAvailable; i++)
        {
            _playback.PushFrame(Vector2.One * (float)Mathf.Sin(phase * Mathf.Tau));
            phase = Mathf.PosMod(phase + increment, 1.0);
        }
    }



Trong ví dụ trên, node "AudioStreamPlayer" phải sử dụng **AudioStreamGenerator** làm stream của nó. Hàm ``fill_buffer`` cung cấp dữ liệu âm thanh để xấp xỉ một sóng hình sin.

Xem thêm :ref:`AudioEffectSpectrumAnalyzer<class_AudioEffectSpectrumAnalyzer>` để thực hiện phân tích phổ âm thanh theo thời gian thực.

\ **Lưu ý:** Do các giới hạn về hiệu năng, class này nên được sử dụng từ C# hoặc từ một ngôn ngữ đã biên dịch thông qua GDExtension. Nếu bạn vẫn muốn sử dụng class này từ GDScript, hãy cân nhắc sử dụng :ref:`mix_rate<class_AudioStreamGenerator_property_mix_rate>` thấp hơn, chẳng hạn như 11,025 Hz hoặc 22,050 Hz.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

- `Audio Generator Demo <https://godotengine.org/asset-library/asset/2759>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                                                                 | :ref:`buffer_length<class_AudioStreamGenerator_property_buffer_length>` | ``0.5``     |
   +-------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                                                                 | :ref:`mix_rate<class_AudioStreamGenerator_property_mix_rate>`           | ``44100.0`` |
   +-------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+-------------+
   | :ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>` | :ref:`mix_rate_mode<class_AudioStreamGenerator_property_mix_rate_mode>` | ``2``       |
   +-------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+-------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_AudioStreamGenerator_AudioStreamGeneratorMixRate:

.. rst-class:: classref-enumeration

enum **AudioStreamGeneratorMixRate**: :ref:`🔗<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>`

.. _class_AudioStreamGenerator_constant_MIX_RATE_OUTPUT:

.. rst-class:: classref-enumeration-constant

:ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>` **MIX_RATE_OUTPUT** = ``0``

Tốc độ trộn đầu ra :ref:`AudioServer<class_AudioServer>` hiện tại.

.. _class_AudioStreamGenerator_constant_MIX_RATE_INPUT:

.. rst-class:: classref-enumeration-constant

:ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>` **MIX_RATE_INPUT** = ``1``

Tốc độ trộn đầu vào :ref:`AudioServer<class_AudioServer>` hiện tại.

.. _class_AudioStreamGenerator_constant_MIX_RATE_CUSTOM:

.. rst-class:: classref-enumeration-constant

:ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>` **MIX_RATE_CUSTOM** = ``2``

Tốc độ trộn tùy chỉnh, được chỉ định bởi :ref:`mix_rate<class_AudioStreamGenerator_property_mix_rate>`.

.. _class_AudioStreamGenerator_constant_MIX_RATE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>` **MIX_RATE_MAX** = ``3``

Giá trị tối đa cho enum chế độ tốc độ trộn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamGenerator_property_buffer_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **buffer_length** = ``0.5`` :ref:`🔗<class_AudioStreamGenerator_property_buffer_length>`

.. rst-class:: classref-property-setget

- |void| **set_buffer_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_buffer_length**\ (\ )

Độ dài của buffer cần tạo (tính bằng giây). Giá trị thấp hơn sẽ giúp giảm độ trễ, nhưng yêu cầu script tạo dữ liệu âm thanh nhanh hơn, dẫn đến mức sử dụng CPU cao hơn và nguy cơ âm thanh bị rè lớn hơn nếu CPU không theo kịp.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamGenerator_property_mix_rate:

.. rst-class:: classref-property

:ref:`float<class_float>` **mix_rate** = ``44100.0`` :ref:`🔗<class_AudioStreamGenerator_property_mix_rate>`

.. rst-class:: classref-property-setget

- |void| **set_mix_rate**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_mix_rate**\ (\ )

Tần số lấy mẫu cần sử dụng (tính bằng Hz). Giá trị cao hơn đòi hỏi CPU tạo âm thanh nhiều hơn, nhưng cho chất lượng tốt hơn.

Trong game, các tần số lấy mẫu thường được sử dụng là ``11025``, ``16000``, ``22050``, ``32000``, ``44100`` và ``48000``.

Theo `Nyquist-Shannon sampling theorem <https://en.wikipedia.org/wiki/Nyquist%E2%80%93Shannon_sampling_theorem>`__, thính giác của con người không nhận thấy sự khác biệt về chất lượng khi vượt quá 40.000 Hz (vì hầu hết con người chỉ có thể nghe đến khoảng ~20.000 Hz, thường là thấp hơn). Nếu bạn đang tạo các âm thanh có cao độ thấp hơn như giọng nói, các tần số lấy mẫu thấp hơn như ``32000`` hoặc ``22050`` có thể được sử dụng mà không làm giảm chất lượng.

\ **Lưu ý:** **AudioStreamGenerator** không tự động resample dữ liệu đầu vào, để tạo ra kết quả mong đợi thì :ref:`mix_rate_mode<class_AudioStreamGenerator_property_mix_rate_mode>` phải khớp với tần số lấy mẫu của dữ liệu đầu vào.

\ **Lưu ý:** Nếu bạn sử dụng :ref:`AudioEffectCapture<class_AudioEffectCapture>` làm nguồn dữ liệu, hãy đặt :ref:`mix_rate_mode<class_AudioStreamGenerator_property_mix_rate_mode>` thành :ref:`MIX_RATE_INPUT<class_AudioStreamGenerator_constant_MIX_RATE_INPUT>` hoặc :ref:`MIX_RATE_OUTPUT<class_AudioStreamGenerator_constant_MIX_RATE_OUTPUT>` để tự động khớp với tốc độ trộn :ref:`AudioServer<class_AudioServer>` hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamGenerator_property_mix_rate_mode:

.. rst-class:: classref-property

:ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>` **mix_rate_mode** = ``2`` :ref:`🔗<class_AudioStreamGenerator_property_mix_rate_mode>`

.. rst-class:: classref-property-setget

- |void| **set_mix_rate_mode**\ (\ value\: :ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>`\ ) - :ref:`AudioStreamGeneratorMixRate<enum_AudioStreamGenerator_AudioStreamGeneratorMixRate>` **get_mix_rate_mode**\ (\ )

Chế độ tốc độ trộn. Nếu được đặt thành :ref:`MIX_RATE_CUSTOM<class_AudioStreamGenerator_constant_MIX_RATE_CUSTOM>`, :ref:`mix_rate<class_AudioStreamGenerator_property_mix_rate>` sẽ được sử dụng; nếu không, tốc độ trộn :ref:`AudioServer<class_AudioServer>` hiện tại sẽ được sử dụng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
