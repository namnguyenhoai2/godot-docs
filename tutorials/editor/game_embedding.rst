.. _doc_game_embedding:

Nhúng game
==========

Godot tùy chọn hỗ trợ chạy game ngay trong editor. Tính năng này được bật theo mặc định.

.. note::

    Game luôn chạy trong một process riêng, bất kể sử dụng chế độ nhúng nào. Điều này có nghĩa là nếu game bị crash, editor sẽ không bị crash theo.

Cấu hình tính năng nhúng game
-----------------------------

Tính năng nhúng game có thể ở một trong 3 trạng thái:

- **Cửa sổ nổi** *(mặc định)*: Game chạy trong một cửa sổ riêng, với Game bar ở phía trên cho phép bạn điều chỉnh các thiết lập và chọn node trong game được nhúng. Nhấp vào nút màn hình chính :button:`Game` sẽ đưa cửa sổ nổi lên trước. - **Cửa sổ chính:** Game chạy trong editor, với Game bar ở phía trên cho phép bạn điều chỉnh các thiết lập và chọn node trong game được nhúng. Nhấp vào nút màn hình chính :button:`Game` sẽ chuyển sang tab chứa project đang chạy. - **Đã tắt:** Game chạy trong một cửa sổ riêng, như thể đó là một project đã export. Game bar ở phía trên không xuất hiện; không thể chọn node trong game được nhúng.

Để cấu hình chức năng này, hãy nhấp vào Game main screen ở phía trên editor:

.. figure:: img/game_embedding_main_screen.webp
   :align: center
   :alt: Accessing the Game embedding main screen

   Accessing the Game embedding main screen

Trong Game main screen, hãy nhấp vào menu dropdown ở góc trên bên phải của Game bar:

.. figure:: img/game_embedding_mode_dropdown.webp
   :align: center
   :alt: Game embedding mode dropdown

   Game embedding mode dropdown

Có hai tùy chọn để cấu hình chế độ nhúng game:

- **Embed Game on Next Play:** Nếu được bật, tính năng nhúng game sẽ được bật và Game bar sẽ khả dụng để sử dụng trên game đang chạy. - **Make Window Floating on Next Play:** Nếu được bật, game sẽ chạy trong một cửa sổ nổi. Nếu bị tắt, game sẽ chạy trong cửa sổ editor chính.

Định cỡ cửa sổ được nhúng
^^^^^^^^^^^^^^^^^^^^^^^^^

Như bạn thấy trong menu dropdown ở bên phải Game bar, có một số lựa chọn để cấu hình cách hoạt động của kích thước cửa sổ được nhúng. Các lựa chọn này ảnh hưởng đến cả chế độ nhúng cửa sổ nổi và cửa sổ chính:

- **Kích thước cố định** *(mặc định)*: Đặt kích thước viewport thành một độ phân giải cố định, như được cấu hình trong Project Settings. Nếu cả :ref:`display/window/size/window_width_override<class_ProjectSettings_property_display/window/size/window_width_override>` và :ref:`display/window/size/window_height_override<class_ProjectSettings_property_display/window/size/window_height_override>` đều được đặt lớn hơn ``0``, chế độ ghi đè này sẽ được sử dụng thay thế. - **Giữ tỷ lệ khung hình:** Kích thước viewport được kéo giãn để khớp với kích thước cửa sổ game, nhưng luôn tuân theo tỷ lệ khung hình do ``width / height`` xác định, như được cấu hình trong Project Settings. - **Kéo giãn để vừa:** Kích thước viewport được kéo giãn để khớp với kích thước cửa sổ game và có thể sử dụng tỷ lệ khung hình khác với tỷ lệ do ``width / height`` xác định, như được cấu hình trong Project Settings. Cách này giống với hành vi khi tính năng nhúng game bị tắt.

Các tùy chọn này không có tác dụng khi tính năng nhúng game bị tắt.

Các tính năng
-------------

Khi tính năng nhúng game được bật, bạn có thể điều chỉnh một số tính năng trong lúc project đang chạy bằng Game bar ở phía trên.

.. figure:: img/game_embedding_game_bar.webp
   :align: center
   :alt: Game bar at the top of the embedded game window

   Game bar at the top of the embedded game window

Theo thứ tự từ trái sang phải:

Tạm dừng (F9)
^^^^^^^^^^^^^

Tạm dừng/tiếp tục game. Khi bị tạm dừng, game sẽ ngừng xử lý physics và các idle frame, nhưng vẫn render và xử lý input. Điều này cho phép bạn
:ref:`select nodes in the scene <doc_game_embedding_interaction_mode>` and
kiểm tra các thuộc tính của chúng trong inspector của editor khi game đang chạy.

Tiến một frame (F10)
^^^^^^^^^^^^^^^^^^^^

Chỉ khả dụng khi game đang tạm dừng. Tiến game thêm một frame, cho phép bạn kiểm tra trạng thái của game tại một thời điểm cụ thể. Tính năng này có thể được dùng để chẩn đoán các tương tác diễn ra trong thời gian ngắn (chẳng hạn như va chạm), vốn khó kiểm tra khi game chạy ở tốc độ tối đa.

Tốc độ game
^^^^^^^^^^^

Tùy chọn này là một menu cho phép điều chỉnh tốc độ game. Nếu game đặt
:ref:`Engine.time_scale <class_Engine_property_time_scale>` at runtime, it will
sẽ được nhân với giá trị được đặt tại đây.

.. figure:: img/game_embedding_game_speed_dropdown.webp
   :align: center
   :alt: Game speed dropdown on the left of the Game bar

   Game speed dropdown on the left of the Game bar

Tính năng này có thể được dùng để xem các tương tác ở chế độ slow motion hoặc tăng đáng kể tốc độ game để kiểm thử các cơ chế thường mất nhiều thời gian mới xảy ra.

Nút reset ở bên phải dropdown sẽ đặt lại tốc độ game về mức bình thường (1.0×).

.. tip::

    Khi điều chỉnh tốc độ game bằng cơ chế này, tốc độ tick của physics (được xác định bởi
    :ref:`physics/common/physics_ticks_per_second <class_ProjectSettings_property_physics/common/physics_ticks_per_second>`
    project setting) sẽ tự động được nhân với tốc độ game. Điều này cho phép logic game chạy ở tốc độ khác mà không ảnh hưởng đến mô phỏng physics. Ví dụ:

    - Nếu đặt tốc độ game là 0.5, tốc độ tick của physics sẽ giảm một nửa. - Nếu đặt tốc độ game là 4.0, tốc độ tick của physics sẽ tăng gấp bốn.

    :ref:`maximum number of physics steps per frame <class_ProjectSettings_property_physics/common/max_physics_steps_per_frame>` cũng được tăng để khớp với tốc độ tick mới của physics, nhưng sẽ không giảm xuống dưới giá trị mặc định khi chạy ở chế độ slow motion.

.. _doc_game_embedding_interaction_mode:

Chế độ tương tác
^^^^^^^^^^^^^^^^

Tùy chọn này kiểm soát hành vi khi nhấp chuột hoặc nhấn phím trong lúc cửa sổ game được nhúng đang được focus.

- **Input** *(mặc định)*: Cho phép input của game như bình thường. - **2D:** Tắt input của game và cho phép chọn Node2D, Control cũng như thao tác với camera 2D. - **3D:** Tắt input của game và cho phép chọn Node3D cũng như thao tác với camera 3D.

Các node được chọn trong chế độ 2D và 3D có thể được kiểm tra trong inspector của editor, giống như khi chúng được chọn trong editor. Điều này cho phép bạn kiểm tra và sửa đổi các thuộc tính của node trong game đang chạy.

.. warning::

    Giống như trong Remote scene tree, các thay đổi được thực hiện với game đang chạy theo cách này sẽ không được giữ lại khi game dừng.

    Để thực hiện các thay đổi được giữ lại sau khi dừng game, thay vào đó bạn cần chọn các node trong Local scene tree của editor và sửa đổi chúng từ đó trong khi game đang chạy. Hãy đảm bảo :menu:`Debug > Synchronize Scene Changes` được bật khi thực hiện việc này.

Chế độ chọn
^^^^^^^^^^^

*Chỉ có hiệu lực nếu chế độ tương tác là 2D hoặc 3D, không phải Input.*

Khi bật tùy chọn này, chế độ "show list of selectable nodes at position clicked" sẽ bị tắt. Tuy nhiên, bạn vẫn có thể thực hiện thao tác này trong chế độ chọn bằng cách sử dụng :kbd:`Ctrl + Alt + Right mouse button` tại vị trí mong muốn.

Hiển thị danh sách node có thể chọn tại vị trí được nhấp
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Chỉ có hiệu lực nếu chế độ tương tác là 2D hoặc 3D, không phải Input.*

Giống như trong editor, tùy chọn này hiển thị danh sách các node có thể chọn tại vị trí được nhấp. Tính năng này hữu ích khi có nhiều node chồng lên nhau và bạn muốn chọn một node cụ thể. Khi bật tùy chọn này, chế độ chọn sẽ bị tắt.

Bật/tắt khả năng hiển thị lựa chọn
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Chỉ có hiệu lực nếu chế độ tương tác là 2D hoặc 3D, không phải Input.*

Theo mặc định, node được chọn trong chế độ tương tác 2D hoặc 3D sẽ được đánh dấu bằng một hình chữ nhật hoặc hình hộp màu cam (giống như trong editor).

Khi bật tùy chọn này, nó sẽ hiển thị dưới dạng biểu tượng con mắt đóng. Các lựa chọn trong tương lai sẽ không được đánh dấu trong game view, nhưng vẫn được chọn để kiểm tra trong inspector. Tính năng này hữu ích để tránh làm rối giao diện hình ảnh.

Tùy chọn nâng cao cho việc chọn
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Có hai tùy chọn nâng cao trong menu dropdown bên cạnh các biểu tượng của chế độ chọn:

- **Don't Select Locked Nodes:** Khi được bật, các node bị khóa trong editor sẽ không thể được chọn. Tùy chọn này mô phỏng hành vi của editor. - **Select Group over Children:** Khi được bật, các node được nhóm sẽ được chọn thay vì các node con riêng lẻ. Tùy chọn này mô phỏng hành vi của editor.

Tắt tiếng audio của game
^^^^^^^^^^^^^^^^^^^^^^^^

Khi được bật, tùy chọn này sẽ tắt audio của game mà không ảnh hưởng đến editor hoặc các ứng dụng khác. Tính năng này đặc biệt hữu ích trên macOS và Android, vốn không được tích hợp sẵn thanh trượt âm lượng riêng cho từng ứng dụng.

Ghi đè camera
^^^^^^^^^^^^^

Khi được bật, camera sẽ ngừng bám theo camera của game. Sau đó, bạn có thể tự do di chuyển camera 2D/3D bằng cách chuyển sang chế độ tương tác 2D/3D và sử dụng các điều khiển điều hướng thông thường:

- Trong chế độ tương tác 2D, sử dụng nút chuột giữa (hoặc
  :kbd:`Space + Left mouse button`) to pan around and the mouse wheel to zoom.
- Trong chế độ tương tác 3D, giữ nút chuột phải và nhấn :kbd:`W`,
  :kbd:`A`, :kbd:`S`, and :kbd:`D` to use freelook. Use the middle mouse button to
  orbit, :kbd:`Shift + Middle mouse button` để pan và con lăn chuột để zoom. Ngoài ra, bạn có thể sử dụng :kbd:`Ctrl + Minus`, :kbd:`Ctrl + Plus` và :kbd:`Ctrl + 0` để điều khiển field of view (so với FOV của camera riêng của game).

Tính năng này hữu ích để kiểm tra các phần của scene không hiển thị từ góc nhìn của camera game hoặc để kiểm tra chính camera game. Khi tắt ghi đè camera, camera sẽ quay về góc nhìn của camera game.

Khi tắt ghi đè camera, vị trí và góc xoay của camera bị ghi đè sẽ không được reset. Điều này cho phép bạn nhanh chóng chuyển đổi qua lại giữa camera game và camera bị ghi đè.

.. note::

    Nếu ghi đè camera có vẻ không hoạt động, hãy đảm bảo bạn đang ở chế độ tương tác 2D hoặc 3D. Ghi đè camera vẫn tiếp tục hoạt động trong chế độ tương tác Input, nhưng bạn sẽ không thể di chuyển camera bị ghi đè trong chế độ đó (trừ khi sử dụng chế độ ghi đè camera **Manipulate From Editors** như mô tả bên dưới).

    Khi ghi đè camera 2D/3D, các script của project không nhận biết được việc ghi đè camera này. Hãy lưu ý điều này khi kiểm tra các thuộc tính phụ thuộc vào vị trí camera, vì chúng sẽ tính theo vị trí camera ban đầu thay vì vị trí bị ghi đè.

Tùy chọn ghi đè camera
^^^^^^^^^^^^^^^^^^^^^^

- **Reset 2D/3D Camera:** Đặt lại camera 2D/3D về vị trí và góc xoay được game xác định. Lưu ý rằng camera vẫn sẽ bị cố định tại chỗ cho đến khi bạn tắt tính năng ghi đè camera. - **Manipulate In-Game** *(mặc định)*: Tính năng ghi đè camera được điều khiển từ cửa sổ game. Điều này cho phép điều khiển camera mà không cần chuyển lại về editor. - **Manipulate From Editors:** Tính năng ghi đè camera được điều khiển từ cửa sổ editor. Tùy chọn này có thể hữu ích khi sử dụng nhiều màn hình, trong đó editor có thể được hiển thị cạnh bên project đang chạy. Ngoài ra, khi sử dụng tùy chọn này, vị trí ghi đè camera có thể được ghi nhớ giữa các lần chạy project, vì vị trí camera của editor sẽ được sử dụng trực tiếp khi bật tùy chọn.

.. note::

    Tính năng ghi đè camera có thể kém mượt hơn khi sử dụng chế độ ghi đè camera **Manipulate From Editors**, do sử dụng giao tiếp mạng cục bộ giữa editor và game để cập nhật vị trí camera.

Các giới hạn
------------

Tính năng nhúng game có một số giới hạn mà bạn cần lưu ý:

- Trong editor Android, tính năng nhúng game luôn sử dụng cửa sổ nổi. Theo mặc định, cửa sổ nổi được giữ ở phía trên editor bằng chức năng picture-in-picture của Android. Bạn có thể tắt hành vi này trong Game bar bằng cách bỏ chọn :menu:`Keep on Top using PiP` trong menu ở bên phải Game bar. - Không hỗ trợ thay đổi chế độ cửa sổ (ví dụ: toàn màn hình) khi sử dụng tính năng nhúng game. - Khi sử dụng :menu:`Debug > Customize Run Instances...` để bật tính năng chạy nhiều instance, chỉ instance đầu tiên sử dụng tính năng nhúng game. Các instance khác sẽ mở trong cửa sổ riêng, không có Game bar ở phía trên.
