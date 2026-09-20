.. _doc_custom_audiostreams:

AudioStream tùy chỉnh
=====================

Giới thiệu
----------

AudioStream là lớp cơ sở của tất cả các đối tượng phát âm thanh. AudioStreamPlayer liên kết với một AudioStream để phát dữ liệu PCM vào AudioServer, nơi quản lý các trình điều khiển âm thanh.

Tất cả tài nguyên âm thanh đều cần hai lớp liên quan đến âm thanh: AudioStream và AudioStreamPlayback. Với vai trò là một vùng chứa dữ liệu, AudioStream chứa tài nguyên và cung cấp chính nó cho GDScript. AudioStream tham chiếu đến AudioStreamPlayback tùy chỉnh nội bộ của chính nó, lớp này chuyển đổi AudioStream thành dữ liệu PCM.

Hướng dẫn này giả định rằng người đọc biết cách tạo các module C++. Nếu không, hãy tham khảo hướng dẫn này
:ref:`doc_custom_modules_in_cpp`.

Tài liệu tham khảo:
~~~~~~~~~~~~~~~~~~~

-  `servers/audio/audio_stream.h <https://github.com/godotengine/godot/blob/master/servers/audio/audio_stream.h>`__ - `scene/audio/audio_stream_player.cpp <https://github.com/godotengine/godot/blob/master/scene/audio/audio_stream_player.cpp>`__

Dùng để làm gì?
---------------

- Liên kết với các thư viện bên ngoài (chẳng hạn như Wwise, FMOD, v.v.). - Thêm các hàng đợi âm thanh tùy chỉnh - Thêm hỗ trợ cho nhiều định dạng âm thanh hơn

Tạo một AudioStream
-------------------

Một AudioStream gồm có ba thành phần: vùng chứa dữ liệu, tên stream và bộ sinh lớp bạn AudioStreamPlayback. Dữ liệu âm thanh có thể được tải theo nhiều cách, chẳng hạn như bằng một bộ đếm nội bộ cho trình tạo âm, một bộ đệm nội bộ/bên ngoài hoặc một tham chiếu tệp.

Một số AudioStream cần không có trạng thái, chẳng hạn như các đối tượng được tải từ ResourceLoader. ResourceLoader chỉ tải một lần và tham chiếu đến cùng một đối tượng bất kể ``load`` được gọi bao nhiêu lần trên một tài nguyên cụ thể. Vì vậy, trạng thái phát phải được tự chứa trong AudioStreamPlayback.

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
        virtual float get_length() const { return 0; } // if supported, otherwise return 0
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

AudioStreamPlayer sử dụng lệnh gọi lại ``mix`` để lấy dữ liệu PCM. Lệnh gọi lại phải khớp với tần số lấy mẫu và điền vào bộ đệm.

Vì AudioStreamPlayback được luồng âm thanh điều khiển, các thao tác I/O và việc cấp phát bộ nhớ động đều bị cấm.

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
        virtual int get_loop_count() const; // times it looped
        virtual float get_playback_position() const;
        virtual void seek(float p_time);
        virtual void mix(AudioFrame *p_buffer, float p_rate_scale, int p_frames);
        virtual float get_length() const; // if supported, otherwise return 0
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

Tái lấy mẫu
~~~~~~~~~~~

AudioServer của Godot hiện sử dụng tần số lấy mẫu 44100 Hz. Khi cần các tần số lấy mẫu khác, chẳng hạn như 48000, hãy tự cung cấp một lớp hoặc sử dụng AudioStreamPlaybackResampled. Godot cung cấp phép nội suy bậc ba để tái lấy mẫu âm thanh.

Thay vì nạp chồng ``mix``, AudioStreamPlaybackResampled sử dụng ``_mix_internal`` để truy vấn AudioFrames và ``get_stream_sampling_rate`` để truy vấn tần số trộn hiện tại.

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
        virtual int get_loop_count() const; // times it looped
        virtual float get_playback_position() const;
        virtual void seek(float p_time);
        virtual float get_length() const; // if supported, otherwise return 0
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
-  `core/math/audio_frame.h <https://github.com/godotengine/godot/blob/master/core/math/audio_frame.h>`__ - `servers/audio/audio_stream.h <https://github.com/godotengine/godot/blob/master/servers/audio/audio_stream.h>`__ - `scene/audio/audio_stream_player.cpp <https://github.com/godotengine/godot/blob/master/scene/audio/audio_stream_player.cpp>`__
