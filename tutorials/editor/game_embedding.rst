.. _doc_game_embedding:

Nhúng game
==========

Godot tùy chọn hỗ trợ chạy game ngay trong editor. Tính năng này được bật theo mặc định.

.. note::

    Game luôn chạy trong một tiến trình riêng, bất kể sử dụng chế độ nhúng nào. Điều này có nghĩa là nếu game bị crash, editor sẽ không bị crash theo.

Cấu hình tính năng nhúng game
-----------------------------

Tính năng nhúng game có thể ở một trong 3 trạng thái:

- **Floating window** *(mặc định)*: Game chạy trong một cửa sổ riêng, với Game bar ở phía trên, cho phép bạn điều chỉnh các thiết lập và chọn các node trong game được nhúng. Nhấp vào nút :button:`Game` main screen sẽ đưa cửa sổ nổi lên trước.
- **Main window:** Game chạy trong editor, với Game bar ở phía trên, cho phép bạn điều chỉnh các thiết lập và chọn các node trong game được nhúng. Nhấp vào nút :button:`Game` main screen sẽ chuyển sang tab chứa project đang chạy.
- **Disabled:** Game chạy trong một cửa sổ riêng, như khi đó là một project đã được export. Game bar ở phía trên không xuất hiện; không thể chọn các node trong game được nhúng.

Để cấu hình chức năng này, hãy nhấp vào Game main screen ở phía trên editor:

.. figure:: img/game_embedding_main_screen.webp
   :align: center
   :alt: Truy cập Game embedding main screen

   Truy cập Game embedding main screen

Khi ở Game main screen, hãy nhấp vào menu thả xuống ở góc trên bên phải của Game bar:

.. figure:: img/game_embedding_mode_dropdown.webp
   :align: center
   :alt: Menu thả xuống chế độ nhúng game

   Menu thả xuống chế độ nhúng game

Có hai tùy chọn để cấu hình chế độ nhúng game:

- **Embed Game on Next Play:** Nếu được bật, tính năng nhúng game sẽ được bật và Game bar sẽ khả dụng khi game đang chạy.
- **Make Window Floating on Next Play:** Nếu được bật, game sẽ chạy trong một cửa sổ nổi. Nếu bị tắt, game sẽ chạy trong cửa sổ editor chính.

Điều chỉnh kích thước cửa sổ được nhúng
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Như bạn thấy trong menu thả xuống ở bên phải Game bar, có một số lựa chọn để cấu hình cách xử lý kích thước cửa sổ được nhúng. Điều này ảnh hưởng đến cả chế độ nhúng cửa sổ nổi và cửa sổ chính:

- **Fixed Size** *(mặc định)*: Đặt kích thước viewport thành một độ phân giải cố định, như được cấu hình trong Project Settings. Nếu cả :ref:`display/window/size/window_width_override <class_ProjectSettings_property_display/window/size/window_width_override>` và :ref:`display/window/size/window_height_override <class_ProjectSettings_property_display/window/size/window_height_override>` đều được đặt lớn hơn ``0``, giá trị ghi đè này sẽ được sử dụng thay thế.
- **Keep Aspect Ratio:** Kích thước viewport được kéo giãn để khớp với kích thước cửa sổ game, nhưng luôn tuân theo tỷ lệ khung hình được định nghĩa bởi ``width / height`` như đã cấu hình trong Project Settings.
- **Stretch to Fit**: Kích thước viewport được kéo giãn để khớp với kích thước cửa sổ game và có thể sử dụng tỷ lệ khung hình khác với tỷ lệ được định nghĩa bởi ``width / height`` như đã cấu hình trong Project Settings. Cách này giống với hành vi khi tính năng nhúng game bị tắt.

Các tùy chọn này không có tác dụng khi tính năng nhúng game bị tắt.

Tính năng
---------

Khi tính năng nhúng game được bật, bạn có thể điều chỉnh một số tính năng trong khi project đang chạy bằng Game bar ở phía trên.

.. figure:: img/game_embedding_game_bar.webp
   :align: center
   :alt: Game bar ở phía trên cửa sổ game được nhúng

   Game bar ở phía trên cửa sổ game được nhúng

Theo thứ tự từ trái sang phải:

Tạm dừng (F9)
^^^^^^^^^^^^^

Tạm dừng/tiếp tục game. Khi bị tạm dừng, game sẽ ngừng xử lý physics và các frame nhàn rỗi, nhưng vẫn render và xử lý input. Điều này cho phép bạn
:ref:`chọn các node trong scene <doc_game_embedding_interaction_mode>` và kiểm tra các thuộc tính của chúng trong inspector của editor khi game đang chạy.

Tiến từng frame (F10)
^^^^^^^^^^^^^^^^^^^^^

Chỉ khả dụng khi game đang tạm dừng. Tiến game thêm một frame, cho phép bạn kiểm tra trạng thái của game tại một thời điểm cụ thể. Bạn có thể dùng tính năng này để chẩn đoán các tương tác diễn ra trong thời gian ngắn (chẳng hạn như va chạm), vốn khó kiểm tra khi game chạy ở tốc độ tối đa.

Tốc độ game
^^^^^^^^^^^

Tùy chọn này là một menu cho phép điều chỉnh tốc độ game. Nếu game thiết lập
:ref:`Engine.time_scale <class_Engine_property_time_scale>` trong runtime, giá trị đó sẽ được nhân với giá trị được đặt tại đây.

.. figure:: img/game_embedding_game_speed_dropdown.webp
   :align: center
   :alt: Menu thả xuống tốc độ game ở bên trái Game bar

   Menu thả xuống tốc độ game ở bên trái Game bar

Bạn có thể dùng tính năng này để xem các tương tác ở chế độ slow motion hoặc tăng tốc game đáng kể nhằm kiểm thử những cơ chế thường mất nhiều thời gian mới xảy ra.

Nút đặt lại ở bên phải menu thả xuống sẽ đặt lại tốc độ game về mức bình thường (1.0×).

.. tip::

    Khi điều chỉnh tốc độ game bằng cơ chế này, tốc độ tick của physics (được xác định bởi
    :ref:`physics/common/physics_ticks_per_second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>` project setting) sẽ tự động được nhân với tốc độ game. Điều này cho phép logic game chạy ở tốc độ khác mà không ảnh hưởng đến mô phỏng physics. Ví dụ:

    - Nếu đặt tốc độ game là 0.5, tốc độ tick của physics sẽ giảm một nửa.
    - Nếu đặt tốc độ game là 4.0, tốc độ tick của physics sẽ tăng gấp bốn.

    :ref:`số bước physics tối đa mỗi frame <class_ProjectSettings_property_physics/common/max_physics_steps_per_frame>` cũng được tăng lên để khớp với tốc độ tick physics mới, nhưng sẽ không giảm xuống dưới giá trị mặc định khi chạy ở chế độ slow motion.

.. _doc_game_embedding_interaction_mode:

Chế độ tương tác
^^^^^^^^^^^^^^^^

Tùy chọn này kiểm soát hành vi khi nhấp chuột hoặc nhấn phím trong lúc cửa sổ game được nhúng đang được focus.

- **Input** *(mặc định)*: Cho phép input của game như bình thường.
- **2D:** Tắt input của game và cho phép chọn Node2Ds, Controls cũng như thao tác với camera 2D.
- **3D:** Tắt input của game và cho phép chọn Node3Ds cũng như thao tác với camera 3D.

Các node được chọn trong chế độ 2D và 3D có thể được kiểm tra trong inspector của editor, giống như khi chúng được chọn trong editor. Điều này cho phép bạn kiểm tra và sửa đổi các thuộc tính của node trong game đang chạy.

.. warning::

    Giống như trong cây scene Remote, các thay đổi được thực hiện với game đang chạy theo cách này sẽ không được lưu lại khi game dừng.

    Để thực hiện các thay đổi vẫn được giữ lại sau khi dừng game, bạn cần chọn các node trong cây scene Local của editor và sửa đổi chúng từ đó trong khi game đang chạy. Hãy đảm bảo :menu:`Debug > Synchronize Scene Changes` được bật khi thực hiện việc này.

Select mode
^^^^^^^^^^^

*Chỉ có hiệu lực nếu interaction mode là 2D hoặc 3D, không phải Input.*

Khi bật tùy chọn này, chế độ "show list of selectable nodes at position clicked" sẽ bị tắt. Tuy nhiên, bạn vẫn có thể thực hiện thao tác này trong select mode bằng cách sử dụng :kbd:`Ctrl + Alt + Right mouse button` tại vị trí mong muốn.

Show list of selectable nodes at position clicked
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Chỉ có hiệu lực nếu interaction mode là 2D hoặc 3D, không phải Input.*

Giống như trong editor, tùy chọn này hiển thị danh sách các node có thể chọn tại vị trí được nhấp. Tùy chọn này hữu ích khi nhiều node chồng lên nhau và bạn muốn chọn một node cụ thể. Khi bật tùy chọn này, select mode sẽ bị tắt.

Toggle selection visibility
^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Chỉ có hiệu lực nếu interaction mode là 2D hoặc 3D, không phải Input.*

Theo mặc định, node được chọn trong interaction mode 2D hoặc 3D sẽ được đánh dấu bằng hình chữ nhật hoặc hộp màu cam (giống như trong editor).

Khi bật tùy chọn này, biểu tượng con mắt đóng sẽ xuất hiện. Các lựa chọn trong tương lai sẽ không được đánh dấu trong chế độ xem game, nhưng vẫn được chọn để kiểm tra trong inspector. Tùy chọn này hữu ích để tránh giao diện bị rối.

Selection advanced options
^^^^^^^^^^^^^^^^^^^^^^^^^^

Có hai tùy chọn nâng cao trong menu thả xuống bên cạnh các biểu tượng select mode:

- **Don't Select Locked Nodes:** Khi bật, các node bị khóa trong editor không thể được chọn. Tùy chọn này mô phỏng hành vi của editor.
- **Select Group over Children:** Khi bật, các node được nhóm sẽ được chọn thay vì từng node con của chúng. Tùy chọn này mô phỏng hành vi của editor.

Mute game audio
^^^^^^^^^^^^^^^

Tùy chọn này tắt âm thanh game khi được bật mà không ảnh hưởng đến editor hoặc các ứng dụng khác. Tùy chọn này đặc biệt hữu ích trên macOS và Android, vì hai nền tảng này không có sẵn thanh trượt âm lượng riêng cho từng ứng dụng.

Camera override
^^^^^^^^^^^^^^^

Khi được bật, camera sẽ ngừng đi theo camera của game. Sau đó, bạn có thể tự do di chuyển camera 2D/3D bằng cách chuyển sang interaction mode 2D/3D và sử dụng các điều khiển điều hướng thông thường:

- Trong interaction mode 2D, sử dụng nút chuột giữa (hoặc
  :kbd:`Space + Left mouse button`) để di chuyển khung nhìn và con lăn chuột để thu phóng.
- Trong interaction mode 3D, giữ nút chuột phải và nhấn :kbd:`W`,
  :kbd:`A`, :kbd:`S`, và :kbd:`D` để sử dụng freelook. Sử dụng nút chuột giữa để xoay quanh, :kbd:`Shift + Middle mouse button` để di chuyển khung nhìn, và con lăn chuột để thu phóng. Ngoài ra, bạn có thể sử dụng :kbd:`Ctrl + Minus`, :kbd:`Ctrl + Plus`, và :kbd:`Ctrl + 0` để điều khiển trường nhìn (field of view) so với FOV của camera riêng của game.

Tính năng này hữu ích để kiểm tra các phần của scene không hiển thị từ góc nhìn của camera game, hoặc để kiểm tra chính camera game. Khi camera override bị tắt, camera sẽ trở về ngay góc nhìn của camera game.

Khi tắt camera override, vị trí và góc xoay của camera bị override sẽ không được đặt lại. Điều này cho phép bạn nhanh chóng chuyển đổi qua lại giữa camera game và camera bị override.

.. note::

    Nếu camera override có vẻ không tương tác được, hãy đảm bảo bạn đang ở interaction mode 2D hoặc 3D. Camera override vẫn tiếp tục hoạt động trong interaction mode Input, nhưng bạn sẽ không thể di chuyển camera bị override trong chế độ đó (trừ khi sử dụng chế độ camera override **Manipulate From Editors** như mô tả bên dưới).

    Khi override camera 2D/3D, các script của project không nhận biết được camera override này. Hãy lưu ý điều này khi kiểm tra các thuộc tính phụ thuộc vào vị trí camera, vì chúng sẽ sử dụng vị trí camera ban đầu thay thế.

Camera override options
^^^^^^^^^^^^^^^^^^^^^^^

- **Reset 2D/3D Camera:** Đặt lại camera 2D/3D về vị trí và góc xoay do game xác định. Lưu ý rằng camera vẫn sẽ bị cố định tại chỗ cho đến khi bạn tắt camera override.
- **Manipulate In-Game** *(default)*: Camera override được điều khiển từ cửa sổ game. Điều này cho phép điều khiển camera mà không cần chuyển lại editor.
- **Manipulate From Editors:** Camera override được điều khiển từ cửa sổ editor. Tùy chọn này có thể hữu ích khi sử dụng nhiều màn hình, trong đó editor có thể được hiển thị cạnh project đang chạy. Ngoài ra, khi sử dụng tùy chọn này, vị trí camera override có thể được ghi nhớ qua các lần chạy project, vì tùy chọn này sẽ trực tiếp sử dụng vị trí camera của editor khi được bật.

.. note::

    Camera override có thể kém mượt hơn khi sử dụng chế độ camera override **Manipulate From Editors**, do sử dụng giao tiếp mạng cục bộ giữa editor và game để cập nhật vị trí camera.

Limitations
-----------

Game embedding có một số giới hạn cần lưu ý:

- Trong editor Android, game embedding luôn sử dụng cửa sổ nổi. Theo mặc định, cửa sổ nổi được giữ ở trên editor bằng chức năng picture-in-picture của Android. Bạn có thể tắt hành vi này trong Game bar bằng cách bỏ chọn :menu:`Keep on Top using PiP` trong menu ở bên phải Game bar.
- Không hỗ trợ thay đổi chế độ cửa sổ (ví dụ: toàn màn hình) khi sử dụng game embedding.
- Khi sử dụng :menu:`Debug > Customize Run Instances...` để bật chạy với nhiều instance, chỉ instance đầu tiên sử dụng game embedding. Các instance khác sẽ mở trong cửa sổ riêng, không có Game bar ở phía trên.
