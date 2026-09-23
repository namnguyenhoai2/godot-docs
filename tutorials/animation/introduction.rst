.. _doc_introduction_animation:

Giới thiệu về các tính năng animation
=====================================

Node :ref:`class_AnimationPlayer` cho phép bạn tạo mọi loại animation, từ đơn giản đến phức tạp.

Trong hướng dẫn này, bạn sẽ học cách:

-  Làm việc với Animation Panel
-  Tạo animation cho bất kỳ thuộc tính nào của bất kỳ node nào
-  Tạo một animation đơn giản

Trong Godot, bạn có thể tạo animation cho mọi thứ có trong Inspector, chẳng hạn như các phép biến đổi của Node, sprite, phần tử UI, particle, khả năng hiển thị và màu sắc của material, v.v. Bạn cũng có thể thay đổi giá trị của các biến script và thậm chí gọi các hàm.

Tạo node AnimationPlayer
------------------------

Để sử dụng các công cụ animation, trước tiên chúng ta phải tạo một
node :ref:`class_AnimationPlayer`.

Loại node AnimationPlayer là nơi chứa dữ liệu cho các animation của bạn. Một node AnimationPlayer có thể chứa nhiều animation, và các animation này có thể tự động chuyển tiếp sang nhau.

.. figure:: img/animation_create_animationplayer.webp
   :alt: Node AnimationPlayer

   Node AnimationPlayer

Sau khi tạo node AnimationPlayer, hãy nhấp vào node đó để mở Animation Panel ở phía dưới viewport.

.. figure:: img/animation_animation_panel.webp
   :alt: Vị trí của animation panel

   Vị trí của animation panel

Animation panel gồm bốn phần:

.. figure:: img/animation_animation_panel_overview.webp
   :alt: Animation panel

   Animation panel

-  Các điều khiển animation (chẳng hạn như thêm, tải, lưu và xóa animation)
-  Danh sách track
-  Timeline với các keyframe
-  Các điều khiển timeline và track, nơi bạn có thể phóng to timeline và chỉnh sửa track, chẳng hạn như vậy.

Animation trên máy tính dựa vào keyframe
----------------------------------------

Một keyframe xác định giá trị của một thuộc tính tại một thời điểm.

Các hình thoi biểu thị keyframe trên timeline. Một đường thẳng giữa hai keyframe cho biết giá trị không thay đổi giữa chúng.

.. figure:: img/animation_keyframes.webp
   :alt: Các keyframe trong Godot

   Các keyframe trong Godot

Bạn thiết lập giá trị cho các thuộc tính của một node và tạo các keyframe animation cho chúng. Khi animation chạy, engine sẽ nội suy các giá trị giữa các keyframe, khiến chúng dần thay đổi theo thời gian.

.. figure:: img/animation_illustration.webp
   :alt: Chỉ cần hai keyframe là đủ để tạo chuyển động mượt mà

   Chỉ cần hai keyframe là đủ để tạo chuyển động mượt mà

Timeline xác định thời lượng của animation. Bạn có thể chèn keyframe tại nhiều thời điểm khác nhau và thay đổi thời gian của chúng.

.. figure:: img/animation_timeline.webp
   :alt: Timeline trong animation panel

   Timeline trong animation panel

Mỗi dòng trong Animation Panel là một animation track tham chiếu đến thuộc tính Normal hoặc Transform của một node. Mỗi track lưu một đường dẫn đến node và thuộc tính chịu ảnh hưởng của node đó. Ví dụ, track position trong hình minh họa tham chiếu đến thuộc tính ``position`` của node Sprite2D.

.. figure:: img/animation_normal_track.webp
   :alt: Ví dụ về các animation track Normal

   Ví dụ về các animation track Normal

.. tip::

   Nếu bạn tạo animation cho sai thuộc tính, bạn có thể chỉnh sửa đường dẫn của track bất cứ lúc nào bằng cách nhấp đúp vào track và nhập đường dẫn mới. Chạy animation bằng nút "Play from beginning" |Play from beginning| (hoặc nhấn
   :kbd:`Shift + D` trên bàn phím) để xem ngay các thay đổi.

Hướng dẫn: Tạo một animation đơn giản
-------------------------------------

Thiết lập scene
~~~~~~~~~~~~~~~

Trong hướng dẫn này, chúng ta sẽ tạo một node Sprite với AnimationPlayer làm node con. Chúng ta sẽ tạo animation để sprite di chuyển giữa hai điểm trên màn hình.

.. figure:: img/animation_animation_player_tree.webp
   :alt: Scene của chúng ta sau khi thiết lập

   Scene của chúng ta sau khi thiết lập

.. warning::

   AnimationPlayer kế thừa từ Node thay vì Node2D hoặc Node3D, điều này có nghĩa là các node con sẽ không kế thừa phép biến đổi từ các node cha do có một Node thuần túy trong hệ thống phân cấp.

   Do đó, không nên thêm các node có phép biến đổi 2D/3D làm node con của node AnimationPlayer.

Sprite chứa một image texture. Trong hướng dẫn này, hãy chọn node Sprite2D, nhấp vào Texture trong Inspector, rồi nhấp vào Load. Chọn biểu tượng Godot mặc định làm texture cho sprite.

Thêm một animation
~~~~~~~~~~~~~~~~~~

Chọn node AnimationPlayer và nhấp vào nút "Animation" trong animation editor. Từ danh sách, chọn "New" (|Add Animation|) để thêm một animation mới. Nhập tên cho animation vào hộp thoại.

.. figure:: img/animation_create_new_animation.webp
   :alt: Thêm một animation mới

   Thêm một animation mới

Quản lý các animation library
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để có thể tái sử dụng, animation được đăng ký trong một danh sách thuộc resource animation library. Nếu bạn thêm animation vào AnimationPlayer mà không chỉ định bất kỳ thiết lập cụ thể nào, animation sẽ được đăng ký trong animation library [Global] mà AnimationPlayer có sẵn theo mặc định.

.. figure:: img/animation_library.webp
   :alt: Quản lý animation

   Quản lý animation

Nếu có nhiều animation library và bạn cố gắng thêm một animation, một hộp thoại sẽ xuất hiện với các tùy chọn.

.. figure:: img/animation_library_dialog.webp
   :alt: Thêm một animation mới với tùy chọn library

   Thêm một animation mới với tùy chọn library

Thêm một track
~~~~~~~~~~~~~~

Để thêm một track mới cho sprite của chúng ta, hãy chọn sprite và quan sát toolbar:

.. figure:: img/animation_convenience_buttons.webp
   :alt: Các nút tiện ích

   Các nút tiện ích

Các công tắc và nút này cho phép bạn thêm keyframe cho vị trí, góc xoay và tỷ lệ của node đã chọn. Vì chúng ta chỉ tạo animation cho vị trí của sprite, hãy đảm bảo chỉ công tắc vị trí được chọn. Các công tắc được chọn có màu xanh dương.

Nhấp vào nút key để tạo keyframe đầu tiên. Vì chúng ta chưa thiết lập track cho thuộc tính Position, Godot sẽ đề nghị tạo track đó cho chúng ta. Nhấp vào **Create**.

Godot sẽ tạo một track mới và chèn keyframe đầu tiên vào đầu timeline:

.. figure:: img/animation_track.webp
   :alt: Track của sprite

   Track của sprite

Keyframe thứ hai
~~~~~~~~~~~~~~~~

Chúng ta cần đặt vị trí cuối của sprite và thời gian để nó đi đến đó.

Giả sử chúng ta muốn sprite mất hai giây để di chuyển giữa hai điểm. Theo mặc định, animation chỉ kéo dài một giây, vì vậy hãy đổi thời lượng animation thành 2 trong các điều khiển ở bên phải tiêu đề timeline của bảng animation.

.. figure:: img/animation_set_length.webp
   :alt: Thời lượng animation

   Thời lượng animation

Bây giờ, di chuyển sprite sang phải đến vị trí cuối cùng. Bạn có thể sử dụng *Move tool* trên thanh công cụ hoặc đặt giá trị X của *Position* trong *Inspector*.

Nhấp vào tiêu đề timeline gần mốc hai giây trong bảng animation, sau đó nhấp vào nút key trên thanh công cụ để tạo keyframe thứ hai.

Chạy animation
~~~~~~~~~~~~~~

Nhấp vào nút "Play from beginning" (|Play from beginning|).

Tuyệt! Animation của chúng ta chạy rồi:

.. figure:: img/animation_simple.gif
   :alt: Animation

   Animation

Tự động phát khi tải
~~~~~~~~~~~~~~~~~~~~

Bạn có thể đặt để animation tự động phát khi scene của node AnimationPlayer bắt đầu hoặc được thêm vào một scene khác. Để làm vậy, hãy nhấp vào nút "Autoplay on load" trong trình chỉnh sửa animation; nút này nằm ngay cạnh nút edit.

.. image:: img/autoplay_on_load.webp

Biểu tượng của nó cũng sẽ xuất hiện phía trước tên animation, giúp bạn dễ dàng nhận biết animation nào được tự động phát.

Qua lại
~~~~~~~

Godot có một tính năng thú vị mà chúng ta có thể sử dụng trong animation. Khi Animation Looping được bật nhưng không có keyframe nào được chỉ định ở cuối animation, keyframe đầu tiên cũng sẽ là keyframe cuối cùng.

Điều này có nghĩa là giờ đây chúng ta có thể kéo dài thời lượng animation lên bốn giây, và Godot cũng sẽ tính toán các frame từ keyframe cuối đến keyframe đầu, khiến sprite di chuyển qua lại.

.. figure:: img/animation_loop.webp
   :alt: Lặp animation

   Lặp animation

Bạn có thể thay đổi hành vi này bằng cách thay đổi chế độ lặp của track. Nội dung này được trình bày trong chương tiếp theo.

Thiết lập track
~~~~~~~~~~~~~~~

Mỗi track thuộc tính có một bảng thiết lập ở cuối, nơi bạn có thể đặt chế độ cập nhật, nội suy track và chế độ lặp của track.

.. figure:: img/animation_track_settings.webp
   :alt: Thiết lập track

   Thiết lập track

Chế độ cập nhật của track cho Godot biết khi nào cần cập nhật các giá trị thuộc tính. Các chế độ này gồm:

-  **Continuous:** Cập nhật thuộc tính ở mỗi frame
-  **Discrete:** Chỉ cập nhật thuộc tính tại các keyframe
-  **Capture:** nếu thời điểm của keyframe đầu tiên lớn hơn ``0.0``, giá trị hiện tại của thuộc tính sẽ được ghi nhớ và được trộn với key đầu tiên của animation. Ví dụ, bạn có thể sử dụng chế độ Capture để di chuyển một node đang ở bất kỳ vị trí nào đến một vị trí cụ thể.

.. figure:: img/animation_track_rate.webp
   :alt: Chế độ track

   Chế độ track

Thông thường, bạn sẽ sử dụng chế độ "Continuous". Các loại còn lại được dùng để tạo các animation phức tạp bằng script.

Nội suy track cho Godot biết cách tính các giá trị frame giữa các keyframe. Các chế độ nội suy được hỗ trợ gồm:

-  Nearest: Đặt giá trị của keyframe gần nhất
-  Linear: Đặt giá trị dựa trên phép tính hàm tuyến tính giữa hai keyframe
-  Cubic: Đặt giá trị dựa trên phép tính hàm bậc ba giữa hai keyframe
-  Linear Angle (Chỉ xuất hiện trong thuộc tính rotation): Chế độ Linear với góc xoay theo đường đi ngắn nhất
-  Cubic Angle (Chỉ xuất hiện trong thuộc tính rotation): Chế độ Cubic với góc xoay theo đường đi ngắn nhất

.. figure:: img/animation_track_interpolation.webp
   :alt: Nội suy track

   Nội suy track

Với nội suy Cubic, animation chậm hơn tại các keyframe và nhanh hơn ở giữa chúng, tạo ra chuyển động tự nhiên hơn. Nội suy Cubic thường được sử dụng cho animation nhân vật. Nội suy Linear thay đổi với tốc độ cố định, tạo ra hiệu ứng giống robot hơn.

Godot hỗ trợ hai chế độ lặp, ảnh hưởng đến animation khi animation được đặt ở chế độ lặp:

.. figure:: img/animation_track_loop_modes.webp
   :alt: Chế độ lặp

   Chế độ lặp

-  Clamp loop interpolation: Khi được chọn, animation sẽ dừng sau keyframe cuối cùng của track này. Khi keyframe đầu tiên được lặp lại, animation sẽ đặt lại về các giá trị của nó.
-  Wrap loop interpolation: Khi được chọn, Godot sẽ tính animation sau keyframe cuối cùng để đạt đến các giá trị của keyframe đầu tiên một lần nữa.

Keyframe cho các thuộc tính khác
--------------------------------

Hệ thống animation của Godot không bị giới hạn ở vị trí, góc xoay và tỷ lệ. Bạn có thể tạo animation cho bất kỳ thuộc tính nào.

Nếu bạn chọn sprite khi bảng animation đang hiển thị, Godot sẽ hiển thị một nút keyframe nhỏ trong *Inspector* cho từng thuộc tính của sprite. Nhấp vào một trong các nút này để thêm track và keyframe vào animation hiện tại.

.. figure:: img/animation_properties_keyframe.webp
   :alt: Keyframe cho các thuộc tính khác

   Keyframe cho các thuộc tính khác

Chỉnh sửa keyframe
------------------

Bạn có thể nhấp vào một keyframe trong timeline animation để hiển thị và chỉnh sửa giá trị của nó trong *Inspector*.

.. figure:: img/animation_keyframe_editor_key.webp
   :alt: Trình chỉnh sửa keyframe đang chỉnh sửa một key

   Trình chỉnh sửa keyframe đang chỉnh sửa một key

Tại đây, bạn cũng có thể chỉnh sửa giá trị easing của một keyframe bằng cách nhấp và kéo đường cong easing của nó. Điều này cho Godot biết cách nội suy thuộc tính được animate khi thuộc tính đó đến keyframe này.

Bạn có thể tinh chỉnh animation theo cách này cho đến khi chuyển động "trông đúng".

.. |Play from beginning| image:: img/animation_play_from_beginning.png
.. |Add Animation| image:: img/animation_add.png

Sử dụng các track RESET
-----------------------

Bạn có thể thiết lập một animation *RESET* đặc biệt để chứa "tư thế mặc định". Animation này được dùng để đảm bảo tư thế mặc định được khôi phục khi bạn lưu scene rồi mở lại scene đó trong editor.

Đối với các track hiện có, bạn có thể thêm một animation có tên "RESET" (phân biệt chữ hoa chữ thường), sau đó thêm các track cho từng thuộc tính mà bạn muốn reset. Keyframe duy nhất phải ở thời điểm 0 và bạn cần đặt giá trị mặc định mong muốn cho từng track.

Nếu thuộc tính **Reset On Save** của AnimationPlayer được đặt thành ``true``, scene sẽ được lưu với các hiệu ứng của animation reset đã được áp dụng (như thể animation đã được seek đến thời điểm ``0.0``). Điều này chỉ ảnh hưởng đến tệp đã lưu – các property track trong editor vẫn giữ nguyên vị trí.

Nếu muốn reset các track trong editor, hãy chọn node AnimationPlayer, mở panel bên dưới **Animation**, sau đó chọn **Apply Reset** trong menu thả xuống **Edit** của animation editor.

Khi sử dụng biểu tượng keyframe bên cạnh một thuộc tính trong inspector, editor sẽ hỏi bạn có muốn tự động tạo một track RESET hay không.

.. note:: Các track RESET cũng được dùng làm giá trị tham chiếu để blending. Xem thêm `Để blending tốt hơn <../animation/animation_tree.html#for-better-blending>`__.

Onion Skinning
--------------

Animation editor của Godot cho phép bạn sử dụng onion skinning khi tạo animation. Để bật tính năng này, hãy nhấp vào biểu tượng onion ở góc trên bên phải của animation editor. Lúc này, các bản sao trong suốt màu đỏ của đối tượng đang được animate sẽ xuất hiện tại những vị trí trước đó của đối tượng trong animation.

.. image:: img/onion_skin.webp

Nút ba chấm bên cạnh nút onion skinning sẽ mở menu thả xuống, cho phép bạn điều chỉnh cách hoạt động của tính năng này, bao gồm khả năng sử dụng onion skinning cho các frame trong tương lai.

Animation Markers
-----------------

Animation marker có thể được dùng để phát một phần cụ thể của animation thay vì phát toàn bộ animation. Ví dụ, một tệp animation có một nhân vật thực hiện hai hành động riêng biệt, và project cần cả animation hoàn chỉnh lẫn từng hành động riêng lẻ. Thay vì tạo thêm hai animation, bạn có thể đặt marker trên timeline để phát riêng từng hành động.

Để thêm marker vào animation, hãy nhấp chuột phải vào khoảng trống phía trên timeline và chọn **Insert Marker...**.

.. image:: img/animation_marker_click_area.webp

Mọi marker đều cần có một tên duy nhất trong animation. Bạn cũng có thể đặt màu cho các marker để tổ chức chúng dễ dàng hơn.

Để phát phần animation giữa hai marker, hãy sử dụng các phương thức :ref:`play_section_with_markers()<class_AnimationPlayer_method_play_section_with_markers>` và :ref:`play_section_with_markers_backwards()<class_AnimationPlayer_method_play_section_with_markers_backwards>`. Nếu không chỉ định marker bắt đầu, phần đầu của animation sẽ được sử dụng; nếu không chỉ định marker kết thúc, phần cuối của animation sẽ được sử dụng.

Nếu marker kết thúc nằm sau phần cuối của animation, ``AnimationPlayer`` sẽ giới hạn phần cuối của đoạn để đoạn đó không vượt quá phần cuối của animation.

Để xem trước animation giữa hai marker, hãy sử dụng :kbd:`Shift + Click` để chọn các marker. Khi đã chọn hai marker, khoảng giữa chúng sẽ được tô sáng màu đỏ.

.. image:: img/animation_marker_selected.webp

Lúc này, tất cả các nút phát animation sẽ hoạt động như thể vùng được chọn là toàn bộ animation. **Play Animation from Start** sẽ xem marker thứ nhất là phần bắt đầu của animation, **Play Animation Backwards from End** sẽ xem marker thứ hai là phần kết thúc, v.v.
