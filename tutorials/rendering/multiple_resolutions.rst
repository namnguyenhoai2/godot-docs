.. _doc_multiple_resolutions:

Nhiều độ phân giải
==================

Vấn đề về nhiều độ phân giải
----------------------------

Các nhà phát triển thường gặp khó khăn trong việc tìm ra cách hỗ trợ nhiều độ phân giải tốt nhất cho game của mình. Đối với game trên máy tính và console, việc này tương đối đơn giản, vì hầu hết tỷ lệ khung hình của màn hình là 16:9 và độ phân giải đều theo các chuẩn phổ biến (720p, 1080p, 1440p, 4K, …).

Đối với game di động, ban đầu mọi việc khá dễ dàng. Trong nhiều năm, iPhone và iPad sử dụng cùng một độ phân giải. Khi *Retina* được triển khai, mật độ pixel chỉ được tăng gấp đôi; hầu hết nhà phát triển chỉ cần cung cấp asset ở độ phân giải mặc định và độ phân giải gấp đôi.

Ngày nay, điều này không còn đúng nữa, vì có rất nhiều kích thước màn hình, mật độ pixel và tỷ lệ khung hình khác nhau. Các kích thước không theo chuẩn cũng ngày càng phổ biến, chẳng hạn như màn hình ultrawide.

Đối với việc render 3D, không cần thiết phải hỗ trợ nhiều độ phân giải. Nhờ đặc tính dựa trên vector, hình học 3D sẽ tự lấp đầy màn hình dựa trên kích thước viewport. Với 2D và UI của game thì lại khác, vì artwork cần được tạo bằng các kích thước pixel cụ thể trong những phần mềm như Photoshop, GIMP hoặc Krita.

Vì layout, tỷ lệ khung hình, độ phân giải và mật độ pixel có thể thay đổi rất nhiều, việc thiết kế UI cho từng màn hình cụ thể không còn khả thi. Cần sử dụng một phương pháp khác.

Một kích thước phù hợp cho tất cả
---------------------------------

Cách tiếp cận phổ biến nhất là sử dụng một độ phân giải *cơ sở* duy nhất, sau đó điều chỉnh nó cho mọi trường hợp khác. Đây là độ phân giải mà phần lớn người chơi được dự đoán sẽ sử dụng để chơi game (dựa trên phần cứng của họ). Đối với thiết bị di động, Google có `stats <https://developer.android.com/about/dashboards>`_ hữu ích trên mạng, còn đối với máy tính để bàn, Steam `also does <https://store.steampowered.com/hwsurvey/>`_.

Ví dụ, Steam cho thấy *độ phân giải màn hình chính* phổ biến nhất là 1920×1080, vì vậy một cách tiếp cận hợp lý là phát triển game ở độ phân giải này, sau đó xử lý việc scale cho các kích thước và tỷ lệ khung hình khác nhau.

Godot cung cấp một số công cụ hữu ích để thực hiện việc này một cách dễ dàng.

.. seealso::

    Bạn có thể xem cách Godot hỗ trợ nhiều độ phân giải hoạt động trên thực tế bằng cách sử dụng `Multiple Resolutions and Aspect Ratios demo project <https://github.com/godotengine/godot-demo-projects/tree/master/gui/multiple_resolutions>`__.

Kích thước cơ sở
----------------

Có thể chỉ định kích thước cơ sở cho cửa sổ trong Project Settings tại **Display → Window**.

.. image:: img/screenres.webp

Tuy nhiên, tác dụng của nó không hoàn toàn rõ ràng; engine sẽ *không* cố gắng chuyển màn hình sang độ phân giải này. Thay vào đó, hãy xem thiết lập này là "kích thước thiết kế", tức kích thước của khu vực mà bạn làm việc trong editor. Thiết lập này tương ứng trực tiếp với kích thước của hình chữ nhật màu xanh trong 2D editor.

Thông thường, cần hỗ trợ các thiết bị có kích thước màn hình và cửa sổ khác với kích thước cơ sở này. Godot cung cấp nhiều cách để kiểm soát cách viewport được resize và stretch theo các kích thước màn hình khác nhau.

.. note::

   Trong trang này, *window* đề cập đến khu vực màn hình mà hệ thống dành cho game của bạn, còn *viewport* đề cập đến object gốc (có thể truy cập từ ``get_tree().root``) mà game kiểm soát để lấp đầy khu vực màn hình này. Viewport này là một instance :ref:`Window <class_Window>`. Hãy nhớ lại từ
   :ref:`introduction <doc_viewports>` that *all* Window objects are viewports.

Để cấu hình kích thước cơ sở của stretch trong runtime từ một script, hãy sử dụng property ``get_tree().root.content_scale_size`` (xem
:ref:`Window.content_scale_size <class_Window_property_content_scale_size>`).
Việc thay đổi giá trị này có thể gián tiếp thay đổi kích thước của các phần tử 2D. Tuy nhiên, để cung cấp tùy chọn scale mà người dùng có thể truy cập, hãy sử dụng
:ref:`doc_multiple_resolutions_stretch_scale` is recommended as it's easier to
adjust.

.. note::

   Godot áp dụng một cách tiếp cận hiện đại đối với nhiều độ phân giải. Engine sẽ không bao giờ tự thay đổi độ phân giải của màn hình. Mặc dù thay đổi độ phân giải màn hình là cách hiệu quả nhất, đây cũng là cách kém đáng tin cậy nhất vì có thể khiến màn hình bị kẹt ở độ phân giải thấp nếu game bị crash. Điều này đặc biệt thường xảy ra trên macOS hoặc Linux, những hệ điều hành xử lý việc thay đổi độ phân giải không tốt bằng Windows.

   Việc thay đổi độ phân giải màn hình cũng khiến nhà phát triển game mất quyền kiểm soát đối với filtering và việc stretch tỷ lệ khung hình, những yếu tố có thể rất quan trọng để đảm bảo hiển thị chính xác cho game pixel art.

   Ngoài ra, việc thay đổi độ phân giải màn hình khiến thao tác alt-tab ra vào game chậm hơn nhiều, vì màn hình phải thay đổi độ phân giải mỗi lần thực hiện thao tác này.

Resize
------

Có nhiều loại thiết bị với nhiều loại màn hình khác nhau, và mỗi loại lại có mật độ pixel và độ phân giải khác nhau. Xử lý tất cả chúng có thể tốn rất nhiều công sức, vì vậy Godot cố gắng giúp cuộc sống của nhà phát triển dễ dàng hơn một chút. Node :ref:`Viewport <class_Viewport>` có một số function để xử lý việc resize, và node gốc của scene tree luôn là một viewport (các scene được load sẽ được instance làm node con của nó, và luôn có thể truy cập bằng cách gọi ``get_tree().root`` hoặc ``get_node("/root")``).

Trong mọi trường hợp, mặc dù thay đổi các tham số của root Viewport có lẽ là cách linh hoạt nhất để xử lý vấn đề này, việc đó có thể đòi hỏi rất nhiều công sức, code và phỏng đoán, vì vậy Godot cung cấp một tập hợp tham số trong project settings để xử lý nhiều độ phân giải.

.. tip::

    To render 3D at a lower resolution than 2D elements (without needing separate viewports), you can use Godot's
    :ref:`resolution scaling <doc_resolution_scaling>` support. This is a good way
    để cải thiện đáng kể hiệu năng trong các trường hợp bị giới hạn bởi GPU. Cách này hoạt động với mọi kết hợp giữa stretch mode và stretch aspect.

Thiết lập Stretch
-----------------

.. note::

    Khi thử nghiệm các stretch mode và thiết lập stretch aspect khác nhau, hãy đảm bảo
    :ref:`game embedding <doc_game_embedding>` is configured to use the :ui:`Stretch to Fit`
    tùy chọn scale:

    .. figure:: img/multiple_resolutions_game_embedding_size_dropdown.webp
      :align: center

    Điều này đảm bảo kích thước viewport luôn khớp với kích thước cửa sổ, chẳng hạn khi tính năng nhúng game bị tắt.

Các thiết lập Stretch nằm trong project settings và cung cấp một số tùy chọn:

.. image:: img/stretchsettings.webp

Stretch Mode
~~~~~~~~~~~~

Thiết lập **Stretch Mode** xác định cách kích thước cơ sở được stretch để vừa với độ phân giải của cửa sổ hoặc màn hình. Các animation bên dưới sử dụng "kích thước cơ sở" chỉ 16×9 pixel để minh họa hiệu ứng của các stretch mode khác nhau. Một sprite duy nhất, cũng có kích thước 16×9 pixel, phủ toàn bộ viewport, và một :ref:`Line2D <class_Line2D>` chéo được thêm lên trên nó:

.. image:: img/stretch_demo_scene.png

.. Animated GIF được tạo từ: .. https://github.com/ttencate/godot_scaling_mode

-  **Stretch Mode = Disabled** (mặc định): Không xảy ra việc stretch. Một unit trong scene tương ứng với một pixel trên màn hình. Ở mode này, thiết lập **Stretch Aspect** không có tác dụng.

   .. image:: img/stretch_disabled_expand.gif

-  **Stretch Mode = Canvas Items**: Ở mode này, kích thước cơ sở được chỉ định bằng chiều rộng và chiều cao trong project settings sẽ được stretch để phủ toàn bộ màn hình (có tính đến thiết lập **Stretch Aspect**). Điều này có nghĩa là mọi thứ được render trực tiếp ở độ phân giải đích. 3D không bị ảnh hưởng, còn trong 2D, không còn sự tương ứng 1:1 giữa pixel của sprite và pixel trên màn hình, điều này có thể gây ra các artifact do scale.

   .. image:: img/stretch_2d_expand.gif

-  **Stretch Mode = Viewport**: Viewport scaling có nghĩa là kích thước của :ref:`Viewport <class_Viewport>` gốc được đặt chính xác bằng kích thước cơ sở được chỉ định trong mục **Display** của Project Settings. Scene trước tiên được render vào viewport này. Cuối cùng, viewport này được scale để vừa với màn hình (có tính đến thiết lập **Stretch Aspect**).

   .. image:: img/stretch_viewport_expand.gif

Để cấu hình stretch mode trong runtime từ một script, hãy sử dụng property ``get_tree().root.content_scale_mode`` (xem
:ref:`Window.content_scale_mode <class_Window_property_content_scale_mode>`
và enum :ref:`ContentScaleMode <enum_Window_ContentScaleMode>`).

Stretch Aspect
~~~~~~~~~~~~~~

Thiết lập thứ hai là stretch aspect. Lưu ý rằng thiết lập này chỉ có hiệu lực nếu **Stretch Mode** được đặt thành giá trị khác **Disabled**.

Trong các animation bên dưới, bạn sẽ thấy những vùng màu xám và màu đen. Các vùng màu đen được engine thêm vào và không thể vẽ lên đó. Các vùng màu xám là một phần của scene và có thể vẽ lên đó. Các vùng màu xám tương ứng với khu vực nằm ngoài khung màu xanh mà bạn thấy trong 2D editor.

-  **Stretch Aspect = Ignore**: Bỏ qua tỷ lệ khung hình khi stretch màn hình. Điều này có nghĩa là độ phân giải ban đầu sẽ được stretch để lấp đầy chính xác màn hình, ngay cả khi màn hình rộng hơn hoặc hẹp hơn. Điều này có thể dẫn đến việc stretch không đồng đều: các vật thể trông rộng hơn hoặc cao hơn so với thiết kế.

   .. image:: img/stretch_viewport_ignore.gif

-  **Stretch Aspect = Keep**: Giữ nguyên tỷ lệ khung hình khi stretch màn hình. Điều này có nghĩa là viewport giữ nguyên kích thước ban đầu bất kể độ phân giải màn hình, và các dải màu đen sẽ được thêm vào phía trên/phía dưới màn hình ("letterboxing") hoặc hai bên ("pillarboxing").

   Đây là một lựa chọn tốt nếu bạn biết trước tỷ lệ khung hình của các thiết bị mục tiêu, hoặc nếu bạn không muốn xử lý các tỷ lệ khung hình khác nhau.

   .. image:: img/stretch_viewport_keep.gif

-  **Stretch Aspect = Keep Width**: Giữ nguyên tỷ lệ khung hình khi stretch màn hình. Nếu màn hình rộng hơn kích thước cơ sở, các dải màu đen sẽ được thêm vào bên trái và bên phải (pillarboxing). Nhưng nếu màn hình cao hơn độ phân giải cơ sở, viewport sẽ được mở rộng theo hướng dọc (và sẽ hiển thị thêm nội dung ở phía dưới). Bạn cũng có thể hiểu tùy chọn này là "Expand Vertically".

   Đây thường là lựa chọn tốt nhất để tạo GUI hoặc HUD có thể scale, nhờ đó một số control có thể được anchor vào phía dưới (:ref:`doc_size_and_anchors`).

   .. image:: img/stretch_viewport_keep_width.gif

-  **Stretch Aspect = Keep Height**: Giữ nguyên tỷ lệ khung hình khi stretch màn hình. Nếu màn hình cao hơn kích thước cơ sở, các dải màu đen sẽ được thêm vào phía trên và phía dưới (letterboxing). Nhưng nếu màn hình rộng hơn độ phân giải cơ sở, viewport sẽ được mở rộng theo hướng ngang (và sẽ hiển thị thêm nội dung ở bên phải). Bạn cũng có thể hiểu tùy chọn này là "Expand Horizontally".

   Đây thường là lựa chọn tốt nhất cho game 2D cuộn theo chiều ngang (chẳng hạn như game runner hoặc platformer).

   .. image:: img/stretch_viewport_keep_height.gif

-  **Stretch Aspect = Expand**: Giữ nguyên tỷ lệ khung hình khi kéo giãn màn hình, nhưng không giữ nguyên chiều rộng hoặc chiều cao cơ sở. Tùy thuộc vào tỷ lệ khung hình của màn hình, viewport sẽ lớn hơn theo chiều ngang (nếu màn hình rộng hơn kích thước cơ sở) hoặc theo chiều dọc (nếu màn hình cao hơn kích thước ban đầu).

   .. image:: img/stretch_viewport_expand.gif

.. tip::

    Để hỗ trợ cả chế độ dọc và ngang với hệ số scale được tự động xác định tương tự nhau, hãy đặt độ phân giải cơ sở của project thành *hình vuông* (tỷ lệ khung hình 1:1) thay vì hình chữ nhật. Ví dụ: nếu bạn muốn thiết kế với độ phân giải cơ sở là 1280×720 nhưng muốn hỗ trợ cả chế độ dọc và ngang, hãy sử dụng kích thước cửa sổ cơ sở 720×720 cho project trong Project Settings.

    Để cho phép người dùng chọn hướng màn hình ưa thích khi runtime, hãy nhớ đặt **Display > Window > Handheld > Orientation** thành ``sensor``.

Để cấu hình stretch aspect khi runtime từ một script, hãy sử dụng thuộc tính ``get_tree().root.content_scale_aspect`` (xem
:ref:`Window.content_scale_aspect <class_Window_property_content_scale_aspect>`
và enum :ref:`ContentScaleAspect <enum_Window_ContentScaleAspect>`).

.. _doc_multiple_resolutions_stretch_scale:

Stretch Scale
~~~~~~~~~~~~~

Thiết lập **Scale** cho phép bạn thêm một hệ số scale bổ sung bên trên những gì các tùy chọn **Stretch** ở trên đã cung cấp. Giá trị mặc định là ``1.0``, có nghĩa là không diễn ra scale bổ sung.

Ví dụ: nếu bạn đặt **Scale** thành ``2.0`` và giữ **Stretch Mode** ở **Disabled**, mỗi unit trong scene sẽ tương ứng với 2×2 pixel trên màn hình. Đây là một cách tốt để cung cấp các tùy chọn scale cho những ứng dụng không phải game.

Nếu **Stretch Mode** được đặt thành **canvas_items**, các phần tử 2D sẽ được scale tương đối so với kích thước cửa sổ cơ sở, sau đó được nhân với thiết lập **Scale**. Bạn có thể cung cấp tùy chọn này cho người chơi để họ điều chỉnh scale được tự động xác định theo ý muốn, nhằm cải thiện khả năng tiếp cận.

Nếu **Stretch Mode** được đặt thành **viewport**, độ phân giải của viewport sẽ được chia cho **Scale**. Điều này làm cho pixel trông lớn hơn và giảm độ phân giải rendering (với một kích thước cửa sổ nhất định), từ đó có thể cải thiện hiệu năng.

Để cấu hình stretch scale khi runtime từ một script, hãy sử dụng thuộc tính ``get_tree().root.content_scale_factor`` (xem
:ref:`Window.content_scale_factor <class_Window_property_content_scale_factor>`).

Bạn cũng có thể điều chỉnh scale mà default project theme được tạo bằng thiết lập project **GUI > Theme > Default Theme Scale**. Thiết lập này có thể được dùng để tạo các UI có kích thước hợp lý hơn ở những độ phân giải cơ sở cao hơn hoặc thấp hơn đáng kể so với mặc định. Tuy nhiên, không thể thay đổi thiết lập project này khi runtime, vì giá trị của nó chỉ được đọc một lần khi project khởi chạy.

.. _doc_multiple_resolutions_stretch_scale_mode:

Stretch Scale Mode
~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.2, thiết lập **Stretch Scale Mode** cho phép bạn giới hạn hệ số scale được tự động xác định (cũng như thiết lập **Stretch Scale** được chỉ định thủ công) ở các giá trị nguyên. Theo mặc định, thiết lập này được đặt thành ``fractional``, cho phép áp dụng mọi hệ số scale (bao gồm các giá trị phân số như ``2.5``). Khi đặt thành ``integer``, giá trị sẽ được làm tròn xuống số nguyên gần nhất. Ví dụ: thay vì sử dụng hệ số scale ``2.5``, giá trị sẽ được làm tròn xuống thành ``2.0``. Điều này hữu ích để tránh biến dạng khi hiển thị pixel art.

Hãy so sánh pixel art này, được hiển thị bằng stretch mode ``viewport``, với stretch scale mode được đặt thành ``fractional``:

.. figure:: img/multiple_resolutions_pixel_art_fractional_scaling.webp
   :align: center
   :alt: Fractional scaling example (incorrect pixel art appearance)

   Checkerboard doesn't look "even". Line widths in the logo and text varies wildly.

Pixel art này cũng được hiển thị bằng stretch mode ``viewport``, nhưng lần này stretch scale mode được đặt thành ``integer``:

.. figure:: img/multiple_resolutions_pixel_art_integer_scaling.webp
   :align: center
   :alt: Integer scaling example (correct pixel art appearance)

   Checkerboard looks perfectly even. Line widths are consistent.

Ví dụ: nếu kích thước cơ sở của viewport là 640×360 và kích thước cửa sổ là 1366×768:

- Khi sử dụng ``fractional``, viewport được hiển thị ở độ phân giải 1366×768 (hệ số scale xấp xỉ 2.133×). Toàn bộ không gian cửa sổ được sử dụng. Mỗi pixel trong viewport tương ứng với 2.133×2.133 pixel trong vùng hiển thị. Tuy nhiên, vì màn hình chỉ có thể hiển thị các pixel "nguyên", điều này sẽ dẫn đến việc scale pixel không đồng đều, khiến pixel art hiển thị không chính xác. - Khi sử dụng ``integer``, viewport được hiển thị ở độ phân giải 1280×720 (hệ số scale là 2×). Phần không gian còn lại được lấp đầy bằng các dải đen ở cả bốn phía, để mỗi pixel trong viewport tương ứng với 2×2 pixel trong vùng hiển thị.

Thiết lập này có hiệu lực với mọi stretch mode. Tuy nhiên, khi sử dụng stretch mode ``disabled``, thiết lập này chỉ ảnh hưởng đến thiết lập **Stretch Scale** bằng cách làm tròn nó *xuống* giá trị nguyên gần nhất. Bạn có thể sử dụng cách này cho các game 3D có UI pixel art, để vùng hiển thị trong viewport 3D không bị giảm kích thước (điều xảy ra khi sử dụng stretch mode ``canvas_items`` hoặc ``viewport`` cùng scale mode ``integer``).

.. tip::

    Game nên sử dụng window mode **Exclusive Fullscreen**, thay vì **Fullscreen**, vốn được thiết kế để ngăn Windows tự động xử lý cửa sổ như thể đó là exclusive fullscreen.

    **Fullscreen** dành cho các ứng dụng GUI muốn sử dụng độ trong suốt theo từng pixel mà không có nguy cơ bị OS vô hiệu hóa. Chế độ này thực hiện điều đó bằng cách chừa lại một đường rộng 1 pixel ở cuối màn hình. Ngược lại, **Exclusive Fullscreen** sử dụng kích thước màn hình thực tế và cho phép Windows giảm hiện tượng giật hình cũng như độ trễ input cho các game fullscreen.

    Điều này đặc biệt quan trọng khi sử dụng integer scaling, vì việc giảm 1 pixel chiều cao trong chế độ **Fullscreen** có thể khiến integer scaling sử dụng hệ số scale nhỏ hơn dự kiến.

Các trường hợp sử dụng phổ biến
-------------------------------

Các thiết lập sau được khuyến nghị để hỗ trợ tốt nhiều độ phân giải và tỷ lệ khung hình.

Game desktop
~~~~~~~~~~~~

**Không phải pixel art:**

- Đặt chiều rộng cửa sổ cơ sở thành ``1920`` và chiều cao cửa sổ thành ``1080``. Nếu bạn có màn hình nhỏ hơn 1920×1080, hãy đặt **Window Width Override** và **Window Height Override** thành các giá trị thấp hơn để cửa sổ nhỏ hơn khi project khởi chạy. - Ngoài ra, nếu chủ yếu nhắm đến các thiết bị cao cấp, hãy đặt chiều rộng cửa sổ cơ sở thành ``3840`` và chiều cao cửa sổ thành ``2160``. Điều này cho phép bạn cung cấp các asset 2D có độ phân giải cao hơn, tạo hình ảnh sắc nét hơn nhưng phải đánh đổi bằng mức sử dụng bộ nhớ và kích thước file lớn hơn. Bạn cũng nên tăng **GUI > Theme > Default Theme Scale** lên một giá trị trong khoảng từ ``2.0`` đến ``3.0`` để đảm bảo các phần tử UI vẫn dễ đọc.

  - Lưu ý rằng điều này sẽ khiến các texture không có mipmap bị nhiễu hạt trên các thiết bị có độ phân giải thấp, vì vậy hãy đảm bảo làm theo hướng dẫn được mô tả trong
    :ref:`doc_multiple_resolutions_reducing_aliasing_on_downsampling`.

- Đặt stretch mode thành ``canvas_items``. - Đặt stretch aspect thành ``expand``. Điều này cho phép hỗ trợ nhiều tỷ lệ khung hình và tận dụng tốt hơn màn hình smartphone cao (chẳng hạn như tỷ lệ 18:9 hoặc 19:9). - Cấu hình anchor của các node Control để chúng bám vào đúng các góc bằng menu **Layout**. - Đối với game 3D, hãy cân nhắc cung cấp :ref:`doc_resolution_scaling` trong menu tùy chọn của game để người chơi có thể điều chỉnh riêng độ phân giải rendering 3D với các phần tử UI. Điều này hữu ích cho việc tinh chỉnh hiệu năng, đặc biệt trên phần cứng cấp thấp.

**Pixel art:**

- Đặt kích thước cửa sổ cơ sở thành kích thước viewport mà bạn dự định sử dụng. Hầu hết game pixel art sử dụng kích thước viewport trong khoảng từ 256×224 đến 640×480. 640×360 là một mốc cơ sở tốt, vì nó scale thành 1280×720, 1920×1080, 2560×1440 và 3840×2160 mà không có dải đen khi sử dụng integer scaling. Các kích thước viewport cao hơn sẽ yêu cầu artwork có độ phân giải cao hơn, trừ khi bạn dự định hiển thị nhiều hơn về thế giới game tại một thời điểm. - Đặt stretch mode thành ``viewport``. - Đặt stretch aspect thành ``keep`` để áp dụng một tỷ lệ khung hình duy nhất (có dải đen). Ngoài ra, bạn có thể đặt stretch aspect thành ``expand`` để hỗ trợ nhiều tỷ lệ khung hình. - Nếu sử dụng stretch aspect ``expand``, hãy cấu hình anchor của các node Control để chúng bám vào đúng các góc bằng menu **Layout**. - Đặt stretch scale mode thành ``integer``. Điều này ngăn việc scale pixel không đồng đều xảy ra, vốn khiến pixel art không được hiển thị như dự định.

.. note::

    Stretch mode ``viewport`` cung cấp rendering độ phân giải thấp, sau đó được kéo giãn đến kích thước cửa sổ cuối cùng. Nếu bạn không ngại sprite có thể di chuyển hoặc xoay ở các vị trí "sub-pixel", hoặc muốn có viewport 3D độ phân giải cao, bạn nên sử dụng stretch mode ``canvas_items`` thay cho stretch mode ``viewport``.

Game mobile ở chế độ ngang
~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot được cấu hình để sử dụng chế độ ngang theo mặc định. Điều này có nghĩa là bạn không cần thay đổi thiết lập hướng màn hình của project.

- Đặt chiều rộng cửa sổ cơ sở thành ``1280`` và chiều cao cửa sổ thành ``720``. - Ngoài ra, nếu chủ yếu nhắm đến các thiết bị cao cấp, hãy đặt chiều rộng cửa sổ cơ sở thành ``1920`` và chiều cao cửa sổ thành ``1080``. Điều này cho phép bạn cung cấp các asset 2D có độ phân giải cao hơn, tạo hình ảnh sắc nét hơn nhưng phải đánh đổi bằng mức sử dụng bộ nhớ và kích thước file lớn hơn. Nhiều thiết bị có màn hình độ phân giải còn cao hơn (1440p), nhưng sự khác biệt so với 1080p hầu như không đáng kể do kích thước màn hình smartphone nhỏ. Bạn cũng nên tăng **GUI > Theme > Default Theme Scale** lên một giá trị trong khoảng từ ``1.5`` đến ``2.0`` để đảm bảo các phần tử UI vẫn dễ đọc.

  - Lưu ý rằng điều này sẽ khiến các texture không có mipmap bị nhiễu hạt trên các thiết bị có độ phân giải thấp, vì vậy hãy đảm bảo làm theo hướng dẫn được mô tả trong
    :ref:`doc_multiple_resolutions_reducing_aliasing_on_downsampling`.

- Đặt chế độ stretch thành ``canvas_items``. - Đặt stretch aspect thành ``expand``. Điều này cho phép hỗ trợ nhiều tỷ lệ khung hình và tận dụng tốt hơn màn hình smartphone cao (chẳng hạn tỷ lệ khung hình 18:9 hoặc 19:9). - Cấu hình anchor của các node Control để neo vào đúng các góc bằng menu **Layout**.

.. tip::

    Để hỗ trợ tốt hơn cho tablet và điện thoại gập (thường có màn hình với tỷ lệ khung hình gần 4:3), hãy cân nhắc sử dụng độ phân giải cơ sở có tỷ lệ khung hình 4:3, đồng thời làm theo các hướng dẫn còn lại ở đây. Chẳng hạn, bạn có thể đặt chiều rộng cửa sổ cơ sở thành ``1280`` và chiều cao cửa sổ cơ sở thành ``960``.

Game mobile ở chế độ dọc
~~~~~~~~~~~~~~~~~~~~~~~~

- Đặt chiều rộng cửa sổ cơ sở thành ``720`` và chiều cao cửa sổ thành ``1280``. - Ngoài ra, nếu chủ yếu nhắm đến các thiết bị cao cấp, hãy đặt chiều rộng cửa sổ cơ sở thành ``1080`` và chiều cao cửa sổ thành ``1920``. Điều này cho phép bạn cung cấp các asset 2D có độ phân giải cao hơn, tạo hình ảnh sắc nét hơn nhưng làm tăng mức sử dụng bộ nhớ và kích thước tệp. Nhiều thiết bị còn có màn hình độ phân giải cao hơn (1440p), nhưng sự khác biệt so với 1080p hầu như không thể nhận thấy do kích thước màn hình smartphone nhỏ. Bạn cũng nên tăng **GUI > Theme > Default Theme Scale** lên một giá trị trong khoảng từ ``1.5`` đến ``2.0`` để đảm bảo các phần tử UI vẫn dễ đọc.

  - Lưu ý rằng điều này sẽ khiến các texture không có mipmap bị nhiễu hạt trên các thiết bị độ phân giải thấp, vì vậy hãy đảm bảo làm theo hướng dẫn được mô tả trong
    :ref:`doc_multiple_resolutions_reducing_aliasing_on_downsampling`.

- Đặt **Display > Window > Handheld > Orientation** thành ``portrait``. - Đặt chế độ stretch thành ``canvas_items``. - Đặt stretch aspect thành ``expand``. Điều này cho phép hỗ trợ nhiều tỷ lệ khung hình và tận dụng tốt hơn màn hình smartphone cao (chẳng hạn tỷ lệ khung hình 18:9 hoặc 19:9). - Cấu hình anchor của các node Control để neo vào đúng các góc bằng menu **Layout**.

.. tip::

    Để hỗ trợ tốt hơn cho tablet và điện thoại gập (thường có màn hình với tỷ lệ khung hình gần 4:3), hãy cân nhắc sử dụng độ phân giải cơ sở có tỷ lệ khung hình 3:4, đồng thời làm theo các hướng dẫn còn lại ở đây. Chẳng hạn, bạn có thể đặt chiều rộng cửa sổ cơ sở thành ``960`` và chiều cao cửa sổ cơ sở thành ``1280``.

.. _doc_multiple_resolutions_non_game_application:

Ứng dụng không phải game
~~~~~~~~~~~~~~~~~~~~~~~~

- Đặt chiều rộng và chiều cao cửa sổ cơ sở thành kích thước cửa sổ nhỏ nhất mà bạn dự định nhắm đến. Điều này không bắt buộc, nhưng giúp đảm bảo bạn thiết kế UI có tính đến các kích thước cửa sổ nhỏ. - Giữ chế độ stretch ở giá trị mặc định, ``disabled``. - Giữ stretch aspect ở giá trị mặc định, ``keep`` (giá trị này sẽ không được sử dụng vì chế độ stretch là ``disabled``). - Bạn có thể xác định kích thước cửa sổ tối thiểu bằng cách đặt ``get_window().min_size`` trong hàm ``_ready()`` của một script. Điều này ngăn người dùng thay đổi kích thước ứng dụng xuống dưới một kích thước nhất định, vốn có thể làm hỏng bố cục UI. - Thêm một tùy chọn trong phần cài đặt của ứng dụng để thay đổi viewport gốc của
  :ref:`stretch scale <doc_multiple_resolutions_stretch_scale>`,
  để có thể làm UI lớn hơn nhằm phù hợp với màn hình hiDPI. Xem thêm phần hỗ trợ hiDPI bên dưới.

hỗ trợ hiDPI
------------

Theo mặc định, các project Godot được hệ điều hành xem là có nhận biết DPI. Điều này được kiểm soát bởi project setting **Display > Window > DPI > Allow hiDPI**, và nên được bật bất cứ khi nào có thể. Việc tắt tính năng nhận biết DPI có thể làm hỏng hành vi toàn màn hình trên Windows.

Vì các project Godot có nhận biết DPI, chúng có thể hiển thị với kích thước cửa sổ rất nhỏ khi khởi chạy trên màn hình hiDPI (tỷ lệ theo độ phân giải màn hình). Đối với game, cách phổ biến nhất để khắc phục vấn đề này là đặt chế độ toàn màn hình theo mặc định. Ngoài ra, bạn có thể đặt kích thước cửa sổ trong một
:ref:`autoload <doc_singletons_autoload>`'s ``_ready()`` function according to
kích thước màn hình.

Để đảm bảo các phần tử 2D không hiển thị quá nhỏ trên màn hình hiDPI:

- Đối với game, hãy sử dụng chế độ stretch ``canvas_items`` hoặc ``viewport`` để các phần tử 2D được tự động thay đổi kích thước theo kích thước cửa sổ hiện tại. - Đối với các ứng dụng không phải game, hãy sử dụng chế độ stretch ``disabled`` và đặt stretch scale thành một giá trị tương ứng với hệ số scale của màn hình trong một
  :ref:`autoload <doc_singletons_autoload>`'s ``_ready()`` function.
  Hệ số scale của màn hình được đặt trong phần cài đặt của hệ điều hành và có thể được truy vấn bằng :ref:`screen_get_scale <class_DisplayServer_method_screen_get_scale>`. Phương thức này hiện được triển khai trên Android, iOS, Linux (chỉ Wayland), macOS và Web. Trên các nền tảng khác, bạn sẽ phải triển khai một phương thức để ước tính hệ số scale của màn hình dựa trên độ phân giải màn hình (kèm một tùy chọn cho phép người dùng ghi đè nếu cần). Đây là cách tiếp cận hiện đang được Godot editor sử dụng.

Thiết lập **Allow hiDPI** chỉ có hiệu lực trên Windows và macOS. Thiết lập này bị bỏ qua trên tất cả các nền tảng khác.

.. note::

    Bản thân Godot editor luôn được đánh dấu là có nhận biết DPI. Việc chạy project từ editor chỉ có nhận biết DPI nếu **Allow hiDPI** được bật trong Project Settings.

.. _doc_multiple_resolutions_font_and_image_oversampling:

Oversampling font và hình ảnh
-----------------------------

Godot hỗ trợ một quy trình gọi là *oversampling*, tức tự động render lại texture từ nguồn vector ban đầu khi hệ số scale của viewport thay đổi. Điều này đảm bảo texture font và hình ảnh vẫn sắc nét ở mọi độ phân giải.

Oversampling font được bật theo mặc định, nhưng có thể tắt bằng cách bỏ chọn **GUI > Fonts > Dynamic Fonts > Use Oversampling** trong Project Settings.

Oversampling hình ảnh bị tắt theo mặc định và có thể được bật cho các hình ảnh cụ thể ở định dạng SVG bằng cách đổi import type của chúng thành :ref:`class_DPITexture` trong Import dock. Các định dạng hình ảnh khác không hỗ trợ oversampling vì chúng lưu dữ liệu bitmap thay vì vector.

Editor tự động thực hiện oversampling khi phóng to trong 2D editor, cho phép bạn xem trước oversampling sẽ trông như thế nào ở các hệ số scale cụ thể. Bạn có thể tắt tính năng này bằng cách bỏ chọn **View > Auto Resample CanvasItems** ở phía trên viewport của 2D editor.

Oversampling cũng có thể được áp dụng theo thuộc tính Scale của Node2D hoặc Control. Hành vi *oversampling dựa trên scale* này bị tắt theo mặc định, nhưng có thể bật bằng cách đặt **Oversampling with Scale** thành **Enabled** trong inspector của node mong muốn. Điều này hữu ích cho các node có thể thay đổi scale khi runtime, chẳng hạn các hệ số scale tùy chỉnh cho một số phần tử UI như crosshair. Tuy nhiên, hãy lưu ý rằng tính năng này có thể gây tải cao cho CPU nếu scale thay đổi thường xuyên, vì texture phải được render lại mỗi lần.

Để có kết quả tốt nhất, node nên sử dụng scale đồng nhất. Scale không đồng nhất vẫn hoạt động, nhưng có thể gây aliasing trên trục ngắn hơn vì oversampling luôn được áp dụng đồng nhất.

.. note::

    Thuộc tính :ref:`offset_transform_enabled <class_Control_property_offset_transform_enabled>` của Control được tính đến bởi oversampling dựa trên scale, nhưng chỉ khi
    :ref:`offset_transform_visual_only <class_Control_property_offset_transform_visual_only>` is *disabled*.
    Khi :ref:`offset_transform_visual_only <class_Control_property_offset_transform_visual_only>` được bật, nó không ảnh hưởng đến scale thực tế của node (được sử dụng cho tọa độ đầu vào), mà chỉ ảnh hưởng đến phần hiển thị của node. Vì vậy, nó bị oversampling bỏ qua.

.. _doc_multiple_resolutions_reducing_aliasing_on_downsampling:

Giảm aliasing khi downsampling
------------------------------

Nếu game có độ phân giải cơ sở rất cao (ví dụ: 3840×2160), aliasing có thể xuất hiện khi downsampling xuống một độ phân giải thấp hơn đáng kể như 1280×720.

Để khắc phục, bạn có thể :ref:`enable mipmaps <doc_importing_images_mipmaps>` trên tất cả texture 2D. Tuy nhiên, việc bật mipmap sẽ làm tăng mức sử dụng bộ nhớ, có thể gây vấn đề trên các thiết bị mobile cấp thấp.

Đối với hình ảnh SVG, bạn cũng có thể đổi import type của chúng thành :ref:`class_DPITexture` trong Import dock để hưởng lợi từ oversampling tự động như mô tả ở trên. Điều này tránh aliasing bằng cách rasterize lại texture khi hệ số scale thay đổi.

Xử lý tỷ lệ khung hình
----------------------

Sau khi đã tính đến việc scale cho các độ phân giải khác nhau, hãy đảm bảo *giao diện người dùng* cũng scale theo các tỷ lệ khung hình khác nhau. Bạn có thể thực hiện việc này bằng :ref:`anchors <doc_size_and_anchors>` và/hoặc :ref:`containers <doc_gui_containers>`.

Scale trường nhìn
-----------------

Thuộc tính **Keep Aspect** của node 3D Camera mặc định sử dụng chế độ scale **Keep Height** (còn gọi là *Hor+*). Đây thường là giá trị tốt nhất cho game desktop và game mobile ở chế độ ngang, vì màn hình widescreen sẽ tự động sử dụng trường nhìn rộng hơn.

Tuy nhiên, nếu game 3D của bạn được thiết kế để chơi ở chế độ dọc, việc sử dụng **Keep Width** (còn gọi là *Vert-*) có thể hợp lý hơn. Nhờ đó, smartphone có tỷ lệ khung hình cao hơn 16:9 (ví dụ: 19:9) sẽ sử dụng trường nhìn *cao hơn*, phù hợp hơn trong trường hợp này.

Scale các phần tử 2D và 3D theo cách khác nhau
----------------------------------------------

Để render 3D ở độ phân giải khác với các phần tử 2D (chẳng hạn UI), hãy sử dụng
:ref:`resolution scaling <doc_resolution_scaling>` functionality. This allows you to
kiểm soát hệ số scale độ phân giải được sử dụng cho 3D mà không cần dùng một node Viewport riêng. Cách này có thể được sử dụng để cải thiện hiệu năng bằng cách render 3D ở độ phân giải thấp hơn, hoặc cải thiện chất lượng thông qua supersampling.
