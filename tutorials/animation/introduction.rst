.. _doc_introduction_animation:

Giới thiệu về các tính năng animation
=====================================

Node :ref:`class_AnimationPlayer` cho phép bạn tạo mọi loại animation, từ đơn giản đến phức tạp.

Trong hướng dẫn này, bạn sẽ học cách:

-  Làm việc với Animation Panel - Animate mọi thuộc tính của mọi node - Tạo một animation đơn giản

Trong Godot, bạn có thể animate mọi thứ có trong Inspector, chẳng hạn như transform của Node, sprite, phần tử UI, particle, khả năng hiển thị và màu của material, v.v. Bạn cũng có thể sửa đổi giá trị của các biến script và thậm chí gọi các function.

Tạo một node AnimationPlayer
----------------------------

Để sử dụng các công cụ animation, trước tiên chúng ta phải tạo một
:ref:`class_AnimationPlayer` node.

Loại node AnimationPlayer là nơi chứa dữ liệu cho các animation của bạn. Một node AnimationPlayer có thể chứa nhiều animation, và các animation này có thể tự động chuyển tiếp sang nhau.

.. figure:: img/animation_create_animationplayer.webp
   :alt: The AnimationPlayer node

   The AnimationPlayer node

Sau khi tạo node AnimationPlayer, hãy nhấp vào node đó để mở Animation Panel ở phía dưới viewport.

.. figure:: img/animation_animation_panel.webp
   :alt: The animation panel position

   The animation panel position

Animation panel gồm bốn phần:

.. figure:: img/animation_animation_panel_overview.webp
   :alt: The animation panel

   The animation panel

-  Các điều khiển animation (chẳng hạn như thêm, tải, lưu và xóa animation) - Danh sách track - Timeline với các keyframe - Các điều khiển timeline và track, nơi bạn có thể phóng to timeline và chỉnh sửa track, chẳng hạn.

Computer animation dựa trên keyframe
------------------------------------

Một keyframe xác định giá trị của một thuộc tính tại một thời điểm.

Các hình thoi biểu thị keyframe trên timeline. Một đường nối giữa hai keyframe cho biết giá trị không thay đổi giữa chúng.

.. figure:: img/animation_keyframes.webp
   :alt: Keyframes in Godot

   Keyframes in Godot

Bạn thiết lập giá trị cho các thuộc tính của một node và tạo các keyframe animation cho chúng. Khi animation chạy, engine sẽ nội suy các giá trị giữa các keyframe, khiến chúng dần thay đổi theo thời gian.

.. figure:: img/animation_illustration.webp
   :alt: Two keyframes are all it takes to obtain a smooth motion

   Two keyframes are all it takes to obtain a smooth motion

Timeline xác định thời lượng của animation. Bạn có thể chèn keyframe tại nhiều thời điểm khác nhau và thay đổi thời gian của chúng.

.. figure:: img/animation_timeline.webp
   :alt: The timeline in the animation panel

   The timeline in the animation panel

Mỗi dòng trong Animation Panel là một animation track tham chiếu đến thuộc tính Normal hoặc Transform của một node. Mỗi track lưu một path đến node và thuộc tính chịu ảnh hưởng của node đó. Ví dụ, position track trong hình minh họa tham chiếu đến thuộc tính ``position`` của node Sprite2D.

.. figure:: img/animation_normal_track.webp
   :alt: Example of Normal animation tracks

   Example of Normal animation tracks

.. tip::

   Nếu animate nhầm thuộc tính, bạn có thể chỉnh sửa path của track bất kỳ lúc nào bằng cách nhấp đúp vào path đó và nhập path mới. Chạy animation bằng nút "Play from beginning" |Play from beginning| (hoặc nhấn
   :kbd:`Shift + D` on keyboard) to see the changes instantly.

Tutorial: Tạo một animation đơn giản
------------------------------------

Thiết lập scene
~~~~~~~~~~~~~~~

Trong tutorial này, chúng ta sẽ tạo một node Sprite với AnimationPlayer làm node con. Chúng ta sẽ animate sprite để di chuyển giữa hai điểm trên màn hình.

.. figure:: img/animation_animation_player_tree.webp
   :alt: Our scene setup

   Our scene setup

.. warning::

   AnimationPlayer kế thừa từ Node thay vì Node2D hoặc Node3D, điều này có nghĩa là các node con sẽ không kế thừa transform từ các node cha do có một Node thuần túy trong hierarchy.

   Do đó, bạn không nên thêm các node có transform 2D/3D làm node con của node AnimationPlayer.

Sprite chứa một image texture. Trong tutorial này, hãy chọn node Sprite2D, nhấp vào Texture trong Inspector, sau đó nhấp vào Load. Chọn icon Godot mặc định làm texture cho sprite.

Thêm một animation
~~~~~~~~~~~~~~~~~~

Chọn node AnimationPlayer và nhấp vào nút "Animation" trong animation editor. Từ danh sách, chọn "New" (|Add Animation|) để thêm animation mới. Nhập tên cho animation vào hộp thoại.

.. figure:: img/animation_create_new_animation.webp
   :alt: Add a new animation

   Add a new animation

Quản lý animation library
~~~~~~~~~~~~~~~~~~~~~~~~~

Để có thể tái sử dụng, animation được đăng ký trong một danh sách thuộc resource animation library. Nếu bạn thêm một animation vào AnimationPlayer mà không chỉ định bất kỳ thiết lập cụ thể nào, animation sẽ được đăng ký trong animation library [Global] mà AnimationPlayer có sẵn theo mặc định.

.. figure:: img/animation_library.webp
   :alt: Manage animations

   Manage animations

Nếu có nhiều animation library và bạn cố gắng thêm một animation, một hộp thoại sẽ xuất hiện cùng các tùy chọn.

.. figure:: img/animation_library_dialog.webp
   :alt: Add a new animation with library option

   Add a new animation with library option

Thêm một track
~~~~~~~~~~~~~~

Để thêm một track mới cho sprite, hãy chọn sprite và xem toolbar:

.. figure:: img/animation_convenience_buttons.webp
   :alt: Convenience buttons

   Convenience buttons

Các switch và nút này cho phép bạn thêm keyframe cho vị trí, rotation và scale của node được chọn. Vì chúng ta chỉ animate vị trí của sprite, hãy đảm bảo chỉ switch location được chọn. Các switch được chọn có màu xanh dương.

Nhấp vào nút key để tạo keyframe đầu tiên. Vì chúng ta chưa thiết lập track cho thuộc tính Position, Godot sẽ đề nghị tạo track đó cho chúng ta. Nhấp vào **Create**.

Godot sẽ tạo một track mới và chèn keyframe đầu tiên của chúng ta ở đầu timeline:

.. figure:: img/animation_track.webp
   :alt: The sprite track

   The sprite track

Keyframe thứ hai
~~~~~~~~~~~~~~~~

Chúng ta cần thiết lập vị trí cuối của sprite và khoảng thời gian để sprite đi đến đó.

Giả sử chúng ta muốn sprite mất hai giây để di chuyển giữa hai điểm. Theo mặc định, animation chỉ kéo dài một giây, vì vậy hãy đổi thời lượng animation thành 2 trong các điều khiển ở bên phải phần tiêu đề timeline của animation panel.

.. figure:: img/animation_set_length.webp
   :alt: Animation length

   Animation length

Bây giờ, hãy di chuyển sprite sang phải, đến vị trí cuối cùng. Bạn có thể sử dụng *Move tool* trong toolbar hoặc đặt giá trị X của *Position* trong *Inspector*.

Nhấp vào phần tiêu đề timeline gần mốc hai giây trong animation panel, sau đó nhấp vào nút key trên toolbar để tạo keyframe thứ hai.

Chạy animation
~~~~~~~~~~~~~~

Nhấp vào nút "Play from beginning" (|Play from beginning|).

Tuyệt! Animation của chúng ta chạy rồi:

.. figure:: img/animation_simple.gif
   :alt: The animation

   The animation

Tự động phát khi tải
~~~~~~~~~~~~~~~~~~~~

Bạn có thể thiết lập để animation tự động phát khi scene của node AnimationPlayer bắt đầu hoặc được thêm vào một scene khác. Để thực hiện việc này, hãy nhấp vào nút "Autoplay on load" trong animation editor; nút này nằm ngay bên cạnh nút edit.

.. image:: img/autoplay_on_load.webp

Icon của nó cũng sẽ xuất hiện phía trước tên animation, để bạn dễ dàng xác định animation nào là animation tự động phát.

Qua lại
~~~~~~~

Godot có một tính năng thú vị mà chúng ta có thể sử dụng trong animation. Khi Animation Looping được bật nhưng không có keyframe nào được chỉ định ở cuối animation, keyframe đầu tiên cũng sẽ là keyframe cuối cùng.

Điều này có nghĩa là giờ đây chúng ta có thể kéo dài thời lượng animation lên bốn giây, và Godot cũng sẽ tính toán các frame từ keyframe cuối đến keyframe đầu tiên, khiến sprite di chuyển qua lại.

.. figure:: img/animation_loop.webp
   :alt: Animation loop

   Animation loop

Bạn có thể thay đổi hành vi này bằng cách thay đổi loop mode của track. Nội dung này sẽ được trình bày trong chương tiếp theo.

Thiết lập track
~~~~~~~~~~~~~~~

Mỗi property track có một settings panel ở cuối, nơi bạn có thể thiết lập update mode, track interpolation và loop mode của track.

.. figure:: img/animation_track_settings.webp
   :alt: Track settings

   Track settings

Update mode của một track cho Godot biết thời điểm cần cập nhật các giá trị thuộc tính. Các chế độ có thể là:

-  **Continuous:** Cập nhật thuộc tính ở mỗi frame - **Discrete:** Chỉ cập nhật thuộc tính tại các keyframe - **Capture:** nếu thời điểm của keyframe đầu tiên lớn hơn ``0.0``, giá trị hiện tại của thuộc tính sẽ được ghi nhớ và blend với animation key đầu tiên. Ví dụ, bạn có thể sử dụng Capture mode để di chuyển một node đang ở bất kỳ vị trí nào đến một vị trí cụ thể.

.. figure:: img/animation_track_rate.webp
   :alt: Track mode

   Track mode

Thông thường bạn sẽ sử dụng mode "Continuous". Các loại khác được dùng để viết script cho những animation phức tạp.

Track interpolation cho Godot biết cách tính các giá trị frame giữa các keyframe. Các interpolation mode được hỗ trợ là:

-  Nearest: Đặt giá trị của keyframe gần nhất - Linear: Đặt giá trị dựa trên phép tính hàm tuyến tính giữa hai keyframe - Cubic: Đặt giá trị dựa trên phép tính hàm bậc ba giữa hai keyframe - Linear Angle (Chỉ xuất hiện trong thuộc tính rotation): Mode Linear với rotation theo đường ngắn nhất - Cubic Angle (Chỉ xuất hiện trong thuộc tính rotation): Mode Cubic với rotation theo đường ngắn nhất

.. figure:: img/animation_track_interpolation.webp
   :alt: Track interpolation

   Track interpolation

Với interpolation Cubic, animation chậm hơn tại các keyframe và nhanh hơn ở giữa chúng, tạo ra chuyển động tự nhiên hơn. Interpolation Cubic thường được sử dụng cho character animation. Interpolation Linear animate các thay đổi với tốc độ cố định, tạo ra hiệu ứng giống robot hơn.

Godot hỗ trợ hai loop mode, ảnh hưởng đến animation khi animation được thiết lập lặp:

.. figure:: img/animation_track_loop_modes.webp
   :alt: Loop modes

   Loop modes

-  Clamp loop interpolation: Khi được chọn, animation sẽ dừng sau keyframe cuối cùng của track này. Khi keyframe đầu tiên được đạt tới lần nữa, animation sẽ đặt lại về các giá trị của nó. - Wrap loop interpolation: Khi được chọn, Godot sẽ tính toán animation sau keyframe cuối cùng để một lần nữa đạt đến các giá trị của keyframe đầu tiên.

Keyframe cho các thuộc tính khác
--------------------------------

Hệ thống animation của Godot không bị giới hạn ở position, rotation và scale. Bạn có thể animate bất kỳ thuộc tính nào.

Nếu bạn chọn sprite trong khi animation panel đang hiển thị, Godot sẽ hiển thị một nút keyframe nhỏ trong *Inspector* cho từng thuộc tính của sprite. Nhấp vào một trong các nút này để thêm track và keyframe vào animation hiện tại.

.. figure:: img/animation_properties_keyframe.webp
   :alt: Keyframes for other properties

   Keyframes for other properties

Chỉnh sửa keyframe
------------------

Bạn có thể nhấp vào một keyframe trên animation timeline để hiển thị và chỉnh sửa giá trị của nó trong *Inspector*.

.. figure:: img/animation_keyframe_editor_key.webp
   :alt: Keyframe editor editing a key

   Keyframe editor editing a key

Bạn cũng có thể chỉnh sửa giá trị easing cho một keyframe tại đây bằng cách nhấp và kéo đường cong easing của keyframe. Điều này cho Godot biết cách nội suy thuộc tính được animate khi thuộc tính đạt đến keyframe này.

Bạn có thể điều chỉnh animation theo cách này cho đến khi chuyển động "trông đúng mắt".

.. |Play from beginning| image:: img/animation_play_from_beginning.png
.. |Add Animation| image:: img/animation_add.png

Sử dụng RESET track
-------------------

Bạn có thể thiết lập một animation *RESET* đặc biệt để chứa "default pose". Animation này được dùng để đảm bảo default pose được khôi phục khi bạn lưu scene và mở lại scene đó trong editor.

Đối với các track hiện có, bạn có thể thêm một animation có tên "RESET" (phân biệt chữ hoa chữ thường), sau đó thêm track cho từng property mà bạn muốn reset. Keyframe duy nhất phải ở thời điểm 0 và chứa giá trị mặc định mong muốn cho từng track.

Nếu property **Reset On Save** của AnimationPlayer được đặt thành ``true``, scene sẽ được lưu với các hiệu ứng của animation reset đã được áp dụng (như thể scene đã được seek đến thời điểm ``0.0``). Điều này chỉ ảnh hưởng đến file đã lưu – các property track trong editor vẫn giữ nguyên vị trí của chúng.

Nếu muốn reset các track trong editor, hãy chọn node AnimationPlayer, mở bottom panel **Animation**, sau đó chọn **Apply Reset** trong menu dropdown **Edit** của animation editor.

Khi sử dụng biểu tượng keyframe bên cạnh một property trong inspector, editor sẽ hỏi bạn có muốn tự động tạo một track RESET hay không.

.. note:: RESET tracks are also used as reference values for blending. See also `For better blending <../animation/animation_tree.html#for-better-blending>`__.

Onion Skinning
--------------

Animation editor của Godot cho phép bạn sử dụng onion skinning khi tạo animation. Để bật tính năng này, hãy nhấp vào biểu tượng onion ở góc trên bên phải của animation editor. Lúc này, các bản sao trong suốt màu đỏ của đối tượng đang được animate ở những vị trí trước đó trong animation sẽ xuất hiện.

.. image:: img/onion_skin.webp

Nút ba chấm bên cạnh nút onion skinning sẽ mở một menu dropdown, cho phép bạn điều chỉnh cách tính năng này hoạt động, bao gồm cả khả năng sử dụng onion skinning cho các frame trong tương lai.

Animation Markers
-----------------

Animation marker có thể được dùng để phát một phần cụ thể của animation thay vì toàn bộ animation. Ví dụ, một file animation có một character thực hiện hai hành động riêng biệt, và project yêu cầu cả toàn bộ animation lẫn từng hành động riêng lẻ. Thay vì tạo thêm hai animation, bạn có thể đặt marker trên timeline, sau đó phát riêng từng hành động.

Để thêm marker vào animation, hãy nhấp chuột phải vào khoảng trống phía trên timeline và chọn **Insert Marker...**.

.. image:: img/animation_marker_click_area.webp

Mọi marker đều yêu cầu một tên duy nhất trong animation. Bạn cũng có thể đặt màu cho các marker để sắp xếp dễ theo dõi hơn.

Để phát phần animation nằm giữa hai marker, hãy sử dụng các method :ref:`play_section_with_markers()<class_AnimationPlayer_method_play_section_with_markers>` và :ref:`play_section_with_markers_backwards()<class_AnimationPlayer_method_play_section_with_markers_backwards>`. Nếu không chỉ định marker bắt đầu, phần đầu của animation sẽ được sử dụng; nếu không chỉ định marker kết thúc, phần cuối của animation sẽ được sử dụng.

Nếu marker kết thúc nằm sau phần cuối của animation, ``AnimationPlayer`` sẽ giới hạn phần cuối của section để section không vượt quá phần cuối của animation.

Để xem trước animation giữa hai marker, hãy sử dụng :kbd:`Shift + Click` để chọn các marker. Khi hai marker được chọn, khoảng giữa chúng sẽ được tô sáng màu đỏ.

.. image:: img/animation_marker_selected.webp

Lúc này, tất cả các nút phát animation sẽ hoạt động như thể vùng đã chọn là toàn bộ animation. **Play Animation from Start** sẽ coi marker đầu tiên là điểm bắt đầu của animation, **Play Animation Backwards from End** sẽ coi marker thứ hai là điểm kết thúc, v.v.
