:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventMIDI.xml.

.. _class_InputEventMIDI:

InputEventMIDI
==============

**Kế thừa:** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một thông điệp MIDI từ thiết bị MIDI, chẳng hạn như bàn phím nhạc.

.. rst-class:: classref-introduction-group

Mô tả
-----

InputEventMIDI lưu trữ thông tin về các thông điệp từ thiết bị `MIDI <https://en.wikipedia.org/wiki/MIDI>`__ (Musical Instrument Digital Interface). Các thiết bị này có thể bao gồm bàn phím nhạc, synthesizer và máy trống.

Thông điệp MIDI có thể được nhận qua đầu nối MIDI 5 chân hoặc qua USB. Nếu thiết bị của bạn hỗ trợ cả hai, hãy nhớ kiểm tra các cài đặt trên thiết bị để biết thiết bị đang sử dụng đầu ra nào.

Theo mặc định, Godot không phát hiện các thiết bị MIDI. Trước tiên, bạn cần gọi :ref:`OS.open_midi_inputs()<class_OS_method_open_midi_inputs>`. Bạn có thể kiểm tra những thiết bị nào đã được phát hiện bằng :ref:`OS.get_connected_midi_inputs()<class_OS_method_get_connected_midi_inputs>`, và đóng kết nối bằng :ref:`OS.close_midi_inputs()<class_OS_method_close_midi_inputs>`.


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        OS.open_midi_inputs()
        print(OS.get_connected_midi_inputs())

    func _input(input_event):
        if input_event is InputEventMIDI:
            _print_midi_info(input_event)

    func _print_midi_info(midi_event):
        print(midi_event)
        print("Channel ", midi_event.channel)
        print("Message ", midi_event.message)
        print("Pitch ", midi_event.pitch)
        print("Velocity ", midi_event.velocity)
        print("Instrument ", midi_event.instrument)
        print("Pressure ", midi_event.pressure)
        print("Controller number: ", midi_event.controller_number)
        print("Controller value: ", midi_event.controller_value)

 .. code-tab:: csharp

    public override void _Ready()
    {
        OS.OpenMidiInputs();
        GD.Print(OS.GetConnectedMidiInputs());
    }

    public override void _Input(InputEvent inputEvent)
    {
        if (inputEvent is InputEventMidi midiEvent)
        {
            PrintMIDIInfo(midiEvent);
        }
    }

    private void PrintMIDIInfo(InputEventMidi midiEvent)
    {
        GD.Print(midiEvent);
        GD.Print($"Channel {midiEvent.Channel}");
        GD.Print($"Message {midiEvent.Message}");
        GD.Print($"Pitch {midiEvent.Pitch}");
        GD.Print($"Velocity {midiEvent.Velocity}");
        GD.Print($"Instrument {midiEvent.Instrument}");
        GD.Print($"Pressure {midiEvent.Pressure}");
        GD.Print($"Controller number: {midiEvent.ControllerNumber}");
        GD.Print($"Controller value: {midiEvent.ControllerValue}");
    }



\ **Lưu ý:** Godot không hỗ trợ đầu ra MIDI, vì vậy không có cách nào để phát các thông điệp MIDI từ Godot. Chỉ hỗ trợ đầu vào MIDI.

\ **Lưu ý:** Trên nền tảng Web, việc sử dụng đầu vào MIDI trước tiên yêu cầu được trình duyệt cấp quyền. Yêu cầu cấp quyền này được thực hiện khi gọi :ref:`OS.open_midi_inputs()<class_OS_method_open_midi_inputs>`. Đầu vào MIDI sẽ không hoạt động cho đến khi người dùng chấp nhận yêu cầu cấp quyền.

.. rst-class:: classref-introduction-group

Tutorial
--------

- `MIDI Message Status Byte List <https://www.midi.org/specifications-old/item/table-2-expanded-messages-list-status-bytes>`__

- `Wikipedia General MIDI Instrument List <https://en.wikipedia.org/wiki/General_MIDI#Program_change_events>`__

- `Wikipedia Piano Key Frequencies List <https://en.wikipedia.org/wiki/Piano_key_frequencies#List>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>`                             | :ref:`channel<class_InputEventMIDI_property_channel>`                     | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>`                             | :ref:`controller_number<class_InputEventMIDI_property_controller_number>` | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>`                             | :ref:`controller_value<class_InputEventMIDI_property_controller_value>`   | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>`                             | :ref:`instrument<class_InputEventMIDI_property_instrument>`               | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`MIDIMessage<enum_@GlobalScope_MIDIMessage>` | :ref:`message<class_InputEventMIDI_property_message>`                     | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>`                             | :ref:`pitch<class_InputEventMIDI_property_pitch>`                         | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>`                             | :ref:`pressure<class_InputEventMIDI_property_pressure>`                   | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>`                             | :ref:`velocity<class_InputEventMIDI_property_velocity>`                   | ``0`` |
   +---------------------------------------------------+---------------------------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventMIDI_property_channel:

.. rst-class:: classref-property

:ref:`int<class_int>` **channel** = ``0`` :ref:`🔗<class_InputEventMIDI_property_channel>`

.. rst-class:: classref-property-setget

- |void| **set_channel**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_channel**\ (\ )

Kênh MIDI của thông điệp này, nằm trong khoảng từ ``0`` đến ``15``. Kênh MIDI ``9`` được dành riêng cho các nhạc cụ bộ gõ.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMIDI_property_controller_number:

.. rst-class:: classref-property

:ref:`int<class_int>` **controller_number** = ``0`` :ref:`🔗<class_InputEventMIDI_property_controller_number>`

.. rst-class:: classref-property-setget

- |void| **set_controller_number**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_controller_number**\ (\ )

Số duy nhất của controller, nếu :ref:`message<class_InputEventMIDI_property_message>` là :ref:`@GlobalScope.MIDI_MESSAGE_CONTROL_CHANGE<class_@GlobalScope_constant_MIDI_MESSAGE_CONTROL_CHANGE>`, nếu không thì đây là ``0``. Giá trị này có thể được dùng để xác định các thanh trượt điều chỉnh âm lượng, cân bằng và pan, cũng như các công tắc và bàn đạp trên thiết bị MIDI. Xem `General MIDI specification <https://en.wikipedia.org/wiki/General_MIDI#Controller_events>`__ để biết một danh sách ngắn.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMIDI_property_controller_value:

.. rst-class:: classref-property

:ref:`int<class_int>` **controller_value** = ``0`` :ref:`🔗<class_InputEventMIDI_property_controller_value>`

.. rst-class:: classref-property-setget

- |void| **set_controller_value**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_controller_value**\ (\ )

Giá trị được áp dụng cho controller. Nếu :ref:`message<class_InputEventMIDI_property_message>` là :ref:`@GlobalScope.MIDI_MESSAGE_CONTROL_CHANGE<class_@GlobalScope_constant_MIDI_MESSAGE_CONTROL_CHANGE>`, giá trị này nằm trong khoảng từ ``0`` đến ``127``, nếu không thì là ``0``. Xem thêm :ref:`controller_value<class_InputEventMIDI_property_controller_value>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMIDI_property_instrument:

.. rst-class:: classref-property

:ref:`int<class_int>` **instrument** = ``0`` :ref:`🔗<class_InputEventMIDI_property_instrument>`

.. rst-class:: classref-property-setget

- |void| **set_instrument**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_instrument**\ (\ )

Nhạc cụ (còn được gọi là *program* hoặc *preset*) được sử dụng trong thông điệp MIDI này. Giá trị này nằm trong khoảng từ ``0`` đến ``127``.

Để xem ý nghĩa của từng giá trị, hãy tham khảo `General MIDI's instrument list <https://en.wikipedia.org/wiki/General_MIDI#Program_change_events>`__. Hãy lưu ý rằng danh sách này lệch 1 vì không bắt đầu từ 0. Giá trị ``0`` tương ứng với piano đại dương cầm.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMIDI_property_message:

.. rst-class:: classref-property

:ref:`MIDIMessage<enum_@GlobalScope_MIDIMessage>` **message** = ``0`` :ref:`🔗<class_InputEventMIDI_property_message>`

.. rst-class:: classref-property-setget

- |void| **set_message**\ (\ value\: :ref:`MIDIMessage<enum_@GlobalScope_MIDIMessage>`\ ) - :ref:`MIDIMessage<enum_@GlobalScope_MIDIMessage>` **get_message**\ (\ )

Đại diện cho loại thông điệp MIDI (xem enum :ref:`MIDIMessage<enum_@GlobalScope_MIDIMessage>`).

Để biết thêm thông tin, hãy xem `MIDI message status byte list chart <https://www.midi.org/specifications-old/item/table-2-expanded-messages-list-status-bytes>`__.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMIDI_property_pitch:

.. rst-class:: classref-property

:ref:`int<class_int>` **pitch** = ``0`` :ref:`🔗<class_InputEventMIDI_property_pitch>`

.. rst-class:: classref-property-setget

- |void| **set_pitch**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_pitch**\ (\ )

Số chỉ mục cao độ của thông điệp MIDI này. Giá trị này nằm trong khoảng từ ``0`` đến ``127``.

Trên piano, **middle C** là ``60``, tiếp theo là **C-sharp** (``61``), rồi đến **D** (``62``), v.v. Mỗi quãng tám được chia thành các khoảng cách 12 đơn vị. Xem cột "MIDI note number" trong `piano key frequency chart <https://en.wikipedia.org/wiki/Piano_key_frequencies>`__ để biết danh sách đầy đủ.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMIDI_property_pressure:

.. rst-class:: classref-property

:ref:`int<class_int>` **pressure** = ``0`` :ref:`🔗<class_InputEventMIDI_property_pressure>`

.. rst-class:: classref-property-setget

- |void| **set_pressure**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_pressure**\ (\ )

Lực nhấn phím. Giá trị này nằm trong khoảng từ ``0`` đến ``127``.

\ **Lưu ý:** Đối với nhiều thiết bị, giá trị này luôn là ``0``. Các thiết bị khác, chẳng hạn như bàn phím nhạc, có thể mô phỏng lực nhấn bằng cách thay đổi :ref:`velocity<class_InputEventMIDI_property_velocity>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMIDI_property_velocity:

.. rst-class:: classref-property

:ref:`int<class_int>` **velocity** = ``0`` :ref:`🔗<class_InputEventMIDI_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_velocity**\ (\ )

Velocity của thông điệp MIDI. Giá trị này nằm trong khoảng từ ``0`` đến ``127``. Đối với bàn phím nhạc, giá trị này tương ứng với tốc độ nhấn phím và trong thực tế hiếm khi vượt quá ``110``.

\ **Lưu ý:** Một số thiết bị MIDI có thể gửi thông điệp :ref:`@GlobalScope.MIDI_MESSAGE_NOTE_ON<class_@GlobalScope_constant_MIDI_MESSAGE_NOTE_ON>` với velocity ``0`` và mong muốn thông điệp đó được xử lý giống như thông điệp :ref:`@GlobalScope.MIDI_MESSAGE_NOTE_OFF<class_@GlobalScope_constant_MIDI_MESSAGE_NOTE_OFF>`. Nếu cần, có thể xử lý việc này bằng một vài dòng mã:

::

    func _input(event):
        if event is InputEventMIDI:
            if event.message == MIDI_MESSAGE_NOTE_ON and event.velocity > 0:
                print("Note pressed!")

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
