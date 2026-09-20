.. _doc_gui_containers:

Sử dụng Container
=================

:ref:`Anchors <doc_size_and_anchors>` are an efficient way to handle
các tỷ lệ khung hình khác nhau để xử lý cơ bản nhiều độ phân giải trong GUI.

Đối với các giao diện người dùng phức tạp hơn, chúng có thể trở nên khó sử dụng.

Điều này thường xảy ra với các game như RPG, trò chuyện trực tuyến, game tycoon hoặc game mô phỏng. Một trường hợp phổ biến khác cần đến các tính năng layout nâng cao hơn là các công cụ trong game (hoặc đơn giản là các công cụ).

Tất cả những tình huống này đều cần một giao diện người dùng giống hệ điều hành mạnh mẽ hơn, với layout và formatting nâng cao. Để làm được điều đó, :ref:`Containers <class_container>` hữu ích hơn.

Layout của Container
--------------------

Container cung cấp khả năng layout rất mạnh mẽ (ví dụ: toàn bộ giao diện người dùng của trình chỉnh sửa Godot đều được tạo bằng chúng):

   .. image:: img/godot_containers.png

Khi một node bắt nguồn từ :ref:`Container <class_Container>` được sử dụng, tất cả các node con :ref:`Control <class_Control>` sẽ mất khả năng tự định vị. Điều này có nghĩa là *Container* sẽ kiểm soát vị trí của chúng, và mọi nỗ lực thay đổi thủ công các node này sẽ bị bỏ qua hoặc bị vô hiệu hóa vào lần tiếp theo node cha được resize.

Tương tự, khi một node bắt nguồn từ *Container* được resize, tất cả node con của nó sẽ được định vị lại theo node đó, với hành vi phụ thuộc vào loại container được sử dụng:

   .. image:: img/container_example.gif

Ví dụ về *HBoxContainer* resize các button con.

Điểm mạnh thực sự của container là chúng có thể được lồng vào nhau (dưới dạng các node), cho phép tạo ra những layout rất phức tạp và có thể resize dễ dàng.

Các tùy chọn kích thước
-----------------------

Khi thêm một node vào container, cách container xử lý từng node con phụ thuộc chủ yếu vào *container sizing options* của chúng. Bạn có thể tìm thấy các tùy chọn này bằng cách kiểm tra layout của bất kỳ *Control* nào là node con của một *Container*.

   .. image:: img/container_sizing_options.webp

Các tùy chọn kích thước hoạt động độc lập đối với kích thước dọc và ngang, và không phải container nào cũng sử dụng chúng (nhưng phần lớn có sử dụng):

* **Fill**: Đảm bảo control *lấp đầy* khu vực được chỉ định bên trong container. Dù control có *mở rộng* hay không (xem bên dưới), nó chỉ *lấp đầy* khu vực được chỉ định khi tùy chọn này được bật (mặc định là bật). * **Expand**: Cố gắng sử dụng nhiều không gian nhất có thể trong container cha (trên từng trục). Các control không mở rộng sẽ bị đẩy ra bởi những control có mở rộng. Giữa các control đang mở rộng, lượng không gian chúng chiếm từ nhau được xác định bởi *Stretch Ratio* (xem bên dưới). Tùy chọn này chỉ khả dụng khi Container cha thuộc đúng loại; ví dụ, *HBoxContainer* có tùy chọn này cho kích thước ngang. * **Shrink Begin** Khi mở rộng, cố gắng giữ ở bên trái hoặc phía trên của khu vực được mở rộng. * **Shrink Center** Khi mở rộng, cố gắng giữ ở chính giữa khu vực được mở rộng. * **Shrink End** Khi mở rộng, cố gắng giữ ở bên phải hoặc phía dưới của khu vực được mở rộng. * **Stretch Ratio**: Tỷ lệ xác định lượng không gian khả dụng mà các control đã mở rộng chiếm so với nhau. Một control có giá trị "2" sẽ chiếm lượng không gian khả dụng gấp đôi control có giá trị "1".

Bạn nên thử nghiệm với các cờ này và những container khác nhau để hiểu rõ hơn cách chúng hoạt động.

Các loại Container
------------------

Godot cung cấp sẵn một số loại container vì mỗi loại phục vụ những mục đích khác nhau:

Box Container
~~~~~~~~~~~~~

Sắp xếp các control con theo chiều dọc hoặc chiều ngang (thông qua :ref:`HBoxContainer <class_HBoxContainer>` và
:ref:`VBoxContainer <class_VBoxContainer>`). In the opposite of the designated direction
(tức là theo chiều dọc đối với container ngang), nó chỉ mở rộng các node con.

   .. image:: img/containers_box.png

Các container này sử dụng thuộc tính *Stretch Ratio* cho những node con được bật cờ *Expand*.

Grid Container
~~~~~~~~~~~~~~

Sắp xếp các control con theo layout dạng lưới (thông qua :ref:`GridContainer <class_GridContainer>`, phải chỉ định số lượng cột). Sử dụng cả cờ mở rộng theo chiều dọc và chiều ngang.

   .. image:: img/containers_grid.png

Margin Container
~~~~~~~~~~~~~~~~

Các control con được mở rộng về phía các biên của control này (thông qua
:ref:`MarginContainer <class_MarginContainer>`). Padding will be added on the margins
tùy thuộc vào cấu hình theme.

   .. image:: img/containers_margin.png

Một lần nữa, hãy nhớ rằng các margin là một giá trị *Theme*, vì vậy chúng cần được chỉnh sửa trong phần constants overrides của từng control:

   .. image:: img/containers_margin_constants.png

Tab Container
~~~~~~~~~~~~~

Cho phép bạn đặt nhiều control con chồng lên nhau (thông qua
:ref:`TabContainer <class_TabContainer>`), with only the *current* one visible.

   .. image:: img/containers_tab.png

Bạn có thể thay đổi node *current* bằng các tab ở phía trên container thông qua thao tác nhấp chuột:

   .. image:: img/containers_tab_click.gif

Theo mặc định, tiêu đề được tạo từ tên node (mặc dù có thể ghi đè chúng thông qua API của *TabContainer*).

Các cài đặt như vị trí tab và *StyleBox* có thể được sửa đổi trong phần theme overrides của *TabContainer*.

Split Container
~~~~~~~~~~~~~~~

Sắp xếp các control con theo chiều dọc hoặc chiều ngang và tạo các thanh kéo giữa chúng (thông qua :ref:`HSplitContainer <class_HSplitContainer>` và :ref:`VSplitContainer <class_VSplitContainer>`). Tuân theo cả cờ mở rộng theo chiều ngang và chiều dọc, cũng như *Stretch Ratio*.

   .. image:: img/containers_split.png

Có thể kéo các thanh kéo để thay đổi tương quan kích thước giữa các node con:

   .. image:: img/containers_split_drag.gif


PanelContainer
~~~~~~~~~~~~~~

Một container vẽ một *StyleBox*, sau đó mở rộng các node con để phủ toàn bộ khu vực của nó (thông qua :ref:`PanelContainer <class_PanelContainer>`, tuân theo các margin của *StyleBox*). Nó tuân theo cả các tùy chọn kích thước ngang và dọc.

   .. image:: img/containers_panel.png

Container này hữu ích khi làm control cấp cao nhất, hoặc chỉ đơn giản là thêm background tùy chỉnh cho các phần của một layout.

FoldableContainer
~~~~~~~~~~~~~~~~~

Một container có thể được mở rộng/thu gọn (thông qua :ref:`FoldableContainer <class_FoldableContainer>`). Các control con sẽ bị ẩn khi container được thu gọn.

ScrollContainer
~~~~~~~~~~~~~~~

Chấp nhận một node con duy nhất. Nếu node con lớn hơn container, các thanh cuộn sẽ được thêm vào để cho phép pan node (thông qua :ref:`ScrollContainer <class_ScrollContainer>`). Cả tùy chọn kích thước dọc và ngang đều được tuân theo, và hành vi này có thể được bật hoặc tắt riêng cho từng trục trong phần properties.

   .. image:: img/containers_scroll.png

Con lăn chuột và thao tác kéo bằng cảm ứng (khi có hỗ trợ cảm ứng) cũng là những cách hợp lệ để pan control con.

   .. image:: img/containers_center_pan.gif

Như trong ví dụ trên, một trong những cách phổ biến nhất để sử dụng container này là kết hợp nó với một *VBoxContainer* làm node con.

AspectRatioContainer
~~~~~~~~~~~~~~~~~~~~

Một loại container sắp xếp các control con theo cách tự động duy trì tỷ lệ của chúng khi container được resize. (thông qua :ref:`AspectRatioContainer <class_AspectRatioContainer>`). Nó có nhiều chế độ stretch, cung cấp các tùy chọn để điều chỉnh kích thước của các control con so với container: "fill", "width control height", "height control width" và "cover."

   .. image:: img/containers_aspectratio.webp

Nó hữu ích khi bạn có một container cần linh hoạt và responsive với nhiều kích thước màn hình khác nhau, đồng thời muốn các phần tử con được scale theo tỷ lệ mà không làm mất hình dạng dự kiến.

   .. image:: img/containers_aspectratio_drag.webp

FlowContainer
~~~~~~~~~~~~~

FlowContainer là một container sắp xếp các control con theo chiều ngang hoặc chiều dọc (thông qua :ref:`HFlowContainer <class_HFlowContainer>` và thông qua :ref:`VFlowContainer <class_VFlowContainer>`). Khi không gian khả dụng cạn, nó sẽ chuyển các node con sang dòng hoặc cột tiếp theo, tương tự cách văn bản xuống dòng trong một cuốn sách.


   .. image:: img/containers_hflow.webp

Nó hữu ích để tạo các layout linh hoạt, trong đó các control con tự động điều chỉnh theo không gian khả dụng mà không chồng lấn lên nhau.

   .. image:: img/containers_hflow_drag.webp

CenterContainer
~~~~~~~~~~~~~~~

CenterContainer là một container tự động giữ tất cả control con của nó ở chính giữa, tại kích thước tối thiểu của chúng. Nó đảm bảo các control con luôn được căn giữa, giúp dễ dàng tạo các layout căn giữa mà không cần định vị thủ công (thông qua :ref:`CenterContainer <class_CenterContainer>`).

   .. image:: img/containers_center.webp

   .. image:: img/containers_center_drag.webp

SubViewportContainer
~~~~~~~~~~~~~~~~~~~~

Đây là một control đặc biệt chỉ chấp nhận một node *Viewport* duy nhất làm node con, và sẽ hiển thị node đó như một hình ảnh (thông qua :ref:`SubViewportContainer <class_SubViewportContainer>`).

Tạo Container tùy chỉnh
-----------------------

Bạn có thể tạo một container tùy chỉnh bằng script. Dưới đây là ví dụ về một container điều chỉnh các node con vừa với kích thước của nó:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Container

    func _notification(what):
        if what == NOTIFICATION_SORT_CHILDREN:
            # Phải sắp xếp lại các node con
            for c in get_children():
                # Vừa với kích thước của chính nó
                fit_child_in_rect(c, Rect2(Vector2(), size))

    func set_some_setting():
        # Một số cài đặt đã thay đổi, yêu cầu sắp xếp lại các node con.
        queue_sort()

 .. code-tab:: csharp

    using Godot;

    public partial class CustomContainer : Container
    {
        public override void _Notification(int what)
        {
            if (what == NotificationSortChildren)
            {
                // Phải sắp xếp lại các node con
                foreach (Control c in GetChildren())
                {
                    // Vừa với kích thước của chính nó
                    FitChildInRect(c, new Rect2(new Vector2(), Size));
                }
            }
        }

        public void SetSomeSetting()
        {
            // Một số cài đặt đã thay đổi, yêu cầu sắp xếp lại các node con.
            QueueSort();
        }
    }
