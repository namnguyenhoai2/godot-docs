.. _doc_custom_audiostreams:

AudioStreams tùy chỉnh
======================

Giới thiệu
----------

AudioStream là lớp cơ sở của mọi đối tượng phát âm thanh. AudioStreamPlayer liên kết với một AudioStream để phát dữ liệu PCM vào AudioServer, nơi quản lý các audio driver.

Mọi audio resource đều cần hai lớp dựa trên audio: AudioStream và AudioStreamPlayback. Với vai trò là một bộ chứa dữ liệu, AudioStream chứa resource và cung cấp nó cho GDScript. AudioStream tham chiếu đến AudioStreamPlayback tùy chỉnh nội bộ của chính nó, lớp này chuyển AudioStream thành dữ liệu PCM.

Hướng dẫn này giả định rằng bạn biết cách tạo các C++ module. Nếu không, hãy tham khảo hướng dẫn này
:ref:`doc_custom_modules_in_cpp`.

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `servers/audio/audio_stream.h <https://github.com/godotengine/godot/blob/master/servers/audio/audio_stream.h>`__
-  `scene/audio/audio_stream_player.cpp <https://github.com/godotengine/godot/blob/master/scene/audio/audio_stream_player.cpp>`__

Dùng để làm gì?
---------------

- Liên kết các thư viện bên ngoài (chẳng hạn như Wwise, FMOD, v.v.).
- Thêm các audio queue tùy chỉnh
- Thêm hỗ trợ cho nhiều audio format hơn

Tạo một AudioStream
-------------------

Một AudioStream gồm ba thành phần: bộ chứa dữ liệu, tên stream và trình tạo lớp friend AudioStreamPlayback. Dữ liệu audio có thể được tải theo nhiều cách, chẳng hạn như dùng bộ đếm nội bộ cho tone generator, buffer nội bộ/bên ngoài hoặc tham chiếu đến một tệp.

Một số AudioStream cần phải stateless, chẳng hạn như các đối tượng được tải từ ResourceLoader. ResourceLoader chỉ tải một lần và tham chiếu đến cùng một đối tượng bất kể ``load`` được gọi bao nhiêu lần trên một resource cụ thể. Do đó, trạng thái phát phải được tự chứa trong AudioStreamPlayback.

.. code-block:: cpp
    :caption: audiostream_mytone.h

    #include "core/reference.h"
    #include "core/resource.h"
    #include "servers/audio/audio_stream.h"

    class AudioStreamMyTone : public AudioStream {
        GDCLASS(AudioStreamMyTone, AudioStream)

    private:
        friend class AudioStreamPlaybackMyTone;
        uint64_t pos;
        int mix_rate;
        bool stereo;
        int hz;

    public:
        void reset();
        void set_position(uint64_t pos);
        virtual Ref<AudioStreamPlayback> instance_playback();
        virtual String get_stream_name() const;
        void gen_tone(int16_t *pcm_buf, int size);
        virtual float get_length() const { return 0; } // nếu được hỗ trợ, nếu không thì trả về 0
        AudioStreamMyTone();

    protected:
        static void _bind_methods();
    };

.. code-block:: cpp
    :caption: audiostream_mytone.cpp

    #include "audiostream_mytone.h"

    AudioStreamMyTone::AudioStreamMyTone()
            : mix_rate(44100), stereo(false), hz(639) {
    }

    Ref<AudioStreamPlayback> AudioStreamMyTone::instance_playback() {
        Ref<AudioStreamPlaybackMyTone> talking_tree;
        talking_tree.instantiate();
        talking_tree->base = Ref<AudioStreamMyTone>(this);
        return talking_tree;
    }

    String AudioStreamMyTone::get_stream_name() const {
        return "MyTone";
    }
    void AudioStreamMyTone::reset() {
        set_position(0);
    }
    void AudioStreamMyTone::set_position(uint64_t p) {
        pos = p;
    }
    void AudioStreamMyTone::gen_tone(int16_t *pcm_buf, int size) {
        for (int i = 0; i < size; i++) {
            pcm_buf[i] = 32767.0 * sin(2.0 * Math_PI * double(pos + i) / (double(mix_rate) / double(hz)));
        }
        pos += size;
    }
    void AudioStreamMyTone::_bind_methods() {
        ClassDB::bind_method(D_METHOD("reset"), &AudioStreamMyTone::reset);
        ClassDB::bind_method(D_METHOD("get_stream_name"), &AudioStreamMyTone::get_stream_name);
    }

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `servers/audio/audio_stream.h <https://github.com/godotengine/godot/blob/master/servers/audio/audio_stream.h>`__


Tạo một AudioStreamPlayback
---------------------------

AudioStreamPlayer sử dụng ``mix`` callback để lấy dữ liệu PCM. Callback phải khớp với sample rate và điền đầy buffer.

Vì AudioStreamPlayback được audio thread điều khiển, không được phép thực hiện I/O và cấp phát bộ nhớ động.

.. code-block:: cpp
    :caption: audiostreamplayer_mytone.h

    #include "core/reference.h"
    #include "core/resource.h"
    #include "servers/audio/audio_stream.h"

    class AudioStreamPlaybackMyTone : public AudioStreamPlayback {
        GDCLASS(AudioStreamPlaybackMyTone, AudioStreamPlayback)
        friend class AudioStreamMyTone;

    private:
        enum {
            PCM_BUFFER_SIZE = 4096
        };
        enum {
            MIX_FRAC_BITS = 13,
            MIX_FRAC_LEN = (1 << MIX_FRAC_BITS),
            MIX_FRAC_MASK = MIX_FRAC_LEN - 1,
        };
        void *pcm_buffer;
        Ref<AudioStreamMyTone> base;
        bool active;

    public:
        virtual void start(float p_from_pos = 0.0);
        virtual void stop();
        virtual bool is_playing() const;
        virtual int get_loop_count() const; // số lần nó đã lặp
        virtual float get_playback_position() const;
        virtual void seek(float p_time);
        virtual void mix(AudioFrame *p_buffer, float p_rate_scale, int p_frames);
        virtual float get_length() const; // nếu được hỗ trợ, nếu không thì trả về 0
        AudioStreamPlaybackMyTone();
        ~AudioStreamPlaybackMyTone();
    };

.. code-block:: cpp
    :caption: audiostreamplayer_mytone.cpp

    #include "audiostreamplayer_mytone.h"

    #include "core/math/math_funcs.h"
    #include "core/print_string.h"

    AudioStreamPlaybackMyTone::AudioStreamPlaybackMyTone()
            : active(false) {
        AudioServer::get_singleton()->lock();
        pcm_buffer = AudioServer::get_singleton()->audio_data_alloc(PCM_BUFFER_SIZE);
        zeromem(pcm_buffer, PCM_BUFFER_SIZE);
        AudioServer::get_singleton()->unlock();
    }
    AudioStreamPlaybackMyTone::~AudioStreamPlaybackMyTone() {
        if(pcm_buffer) {
            AudioServer::get_singleton()->audio_data_free(pcm_buffer);
            pcm_buffer = NULL;
        }
    }
    void AudioStreamPlaybackMyTone::stop() {
        active = false;
        base->reset();
    }
    void AudioStreamPlaybackMyTone::start(float p_from_pos) {
        seek(p_from_pos);
        active = true;
    }
    void AudioStreamPlaybackMyTone::seek(float p_time) {
        float max = get_length();
        if (p_time < 0) {
                p_time = 0;
        }
        base->set_position(uint64_t(p_time * base->mix_rate) << MIX_FRAC_BITS);
    }
    void AudioStreamPlaybackMyTone::mix(AudioFrame *p_buffer, float p_rate, int p_frames) {
        ERR_FAIL_COND(!active);
        if (!active) {
                return;
        }
        zeromem(pcm_buffer, PCM_BUFFER_SIZE);
        int16_t *buf = (int16_t *)pcm_buffer;
        base->gen_tone(buf, p_frames);

        for(int i = 0; i < p_frames; i++) {
            float sample = float(buf[i]) / 32767.0;
            p_buffer[i] = AudioFrame(sample, sample);
        }
    }
    int AudioStreamPlaybackMyTone::get_loop_count() const {
        return 0;
    }
    float AudioStreamPlaybackMyTone::get_playback_position() const {
        return 0.0;
    }
    float AudioStreamPlaybackMyTone::get_length() const {
        return 0.0;
    }
    bool AudioStreamPlaybackMyTone::is_playing() const {
        return active;
    }

Resampling
~~~~~~~~~~

AudioServer của Godot hiện sử dụng sample rate 44100 Hz. Khi cần các sample rate khác, chẳng hạn như 48000, hãy cung cấp một sample rate hoặc sử dụng AudioStreamPlaybackResampled. Godot cung cấp phép nội suy cubic để resampling audio.

Thay vì overload ``mix``, AudioStreamPlaybackResampled sử dụng ``_mix_internal`` để truy vấn AudioFrames và ``get_stream_sampling_rate`` để truy vấn mix rate hiện tại.

.. code-block:: cpp
    :caption: mytone_audiostream_resampled.h

    #include "core/reference.h"
    #include "core/resource.h"
    #include "servers/audio/audio_stream.h"

    class AudioStreamMyToneResampled;

    class AudioStreamPlaybackResampledMyTone : public AudioStreamPlaybackResampled {
        GDCLASS(AudioStreamPlaybackResampledMyTone, AudioStreamPlaybackResampled)
        friend class AudioStreamMyToneResampled;

    private:
        enum {
            PCM_BUFFER_SIZE = 4096
        };
        enum {
            MIX_FRAC_BITS = 13,
            MIX_FRAC_LEN = (1 << MIX_FRAC_BITS),
            MIX_FRAC_MASK = MIX_FRAC_LEN - 1,
        };
        void *pcm_buffer;
        Ref<AudioStreamMyToneResampled> base;
        bool active;

    protected:
        virtual void _mix_internal(AudioFrame *p_buffer, int p_frames);

    public:
        virtual void start(float p_from_pos = 0.0);
        virtual void stop();
        virtual bool is_playing() const;
        virtual int get_loop_count() const; // số lần nó đã lặp
        virtual float get_playback_position() const;
        virtual void seek(float p_time);
        virtual float get_length() const; // nếu được hỗ trợ, nếu không thì trả về 0
        virtual float get_stream_sampling_rate();
        AudioStreamPlaybackResampledMyTone();
        ~AudioStreamPlaybackResampledMyTone();
    };

.. code-block:: cpp
    :caption: mytone_audiostream_resampled.cpp

    #include "mytone_audiostream_resampled.h"

    #include "core/math/math_funcs.h"
    #include "core/print_string.h"

    AudioStreamPlaybackResampledMyTone::AudioStreamPlaybackResampledMyTone()
            : active(false) {
        AudioServer::get_singleton()->lock();
        pcm_buffer = AudioServer::get_singleton()->audio_data_alloc(PCM_BUFFER_SIZE);
        zeromem(pcm_buffer, PCM_BUFFER_SIZE);
        AudioServer::get_singleton()->unlock();
    }
    AudioStreamPlaybackResampledMyTone::~AudioStreamPlaybackResampledMyTone() {
        if (pcm_buffer) {
            AudioServer::get_singleton()->audio_data_free(pcm_buffer);
            pcm_buffer = NULL;
        }
    }
    void AudioStreamPlaybackResampledMyTone::stop() {
        active = false;
        base->reset();
    }
    void AudioStreamPlaybackResampledMyTone::start(float p_from_pos) {
        seek(p_from_pos);
        active = true;
    }
    void AudioStreamPlaybackResampledMyTone::seek(float p_time) {
        float max = get_length();
        if (p_time < 0) {
                p_time = 0;
        }
        base->set_position(uint64_t(p_time * base->mix_rate) << MIX_FRAC_BITS);
    }
    void AudioStreamPlaybackResampledMyTone::_mix_internal(AudioFrame *p_buffer, int p_frames) {
        ERR_FAIL_COND(!active);
        if (!active) {
            return;
        }
        zeromem(pcm_buffer, PCM_BUFFER_SIZE);
        int16_t *buf = (int16_t *)pcm_buffer;
        base->gen_tone(buf, p_frames);

        for(int i = 0;  i < p_frames; i++) {
            float sample = float(buf[i]) / 32767.0;
                p_buffer[i] = AudioFrame(sample, sample);
        }
    }
    float AudioStreamPlaybackResampledMyTone::get_stream_sampling_rate() {
        return float(base->mix_rate);
    }
    int AudioStreamPlaybackResampledMyTone::get_loop_count() const {
        return 0;
    }
    float AudioStreamPlaybackResampledMyTone::get_playback_position() const {
        return 0.0;
    }
    float AudioStreamPlaybackResampledMyTone::get_length() const {
        return 0.0;
    }
    bool AudioStreamPlaybackResampledMyTone::is_playing() const {
        return active;
    }

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~
-  `core/math/audio_frame.h <https://github.com/godotengine/godot/blob/master/core/math/audio_frame.h>`__
-  `servers/audio/audio_stream.h <https://github.com/godotengine/godot/blob/master/servers/audio/audio_stream.h>`__
-  `scene/audio/audio_stream_player.cpp <https://github.com/godotengine/godot/blob/master/scene/audio/audio_stream_player.cpp>`__
