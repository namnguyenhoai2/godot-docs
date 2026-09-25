.. _doc_gui_containers:

Sử dụng Container
=================

:ref:`Anchors <doc_size_and_anchors>` là một cách hiệu quả để xử lý các tỷ lệ khung hình khác nhau nhằm hỗ trợ cơ bản cho nhiều độ phân giải trong GUI.

Đối với các giao diện người dùng phức tạp hơn, chúng có thể trở nên khó sử dụng.

Điều này thường xảy ra với các game như RPG, trò chuyện trực tuyến, game quản lý hoặc mô phỏng. Một trường hợp phổ biến khác có thể yêu cầu các tính năng bố cục nâng cao hơn là các công cụ trong game (hoặc đơn giản là các công cụ).

Tất cả những tình huống này đều yêu cầu một giao diện người dùng giống hệ điều hành có năng lực hơn, với bố cục và định dạng nâng cao. Trong trường hợp đó, :ref:`Containers <class_container>` hữu ích hơn.

Bố cục Container
----------------

Container cung cấp rất nhiều khả năng bố cục (ví dụ: toàn bộ giao diện người dùng của trình chỉnh sửa Godot được xây dựng bằng chúng):

   .. image:: img/godot_containers.png

Khi sử dụng một node dẫn xuất từ :ref:`Container <class_Container>`, tất cả các node :ref:`Control <class_Control>` con sẽ từ bỏ khả năng tự định vị của mình. Điều này có nghĩa là *Container* sẽ kiểm soát vị trí của chúng, và mọi nỗ lực thay đổi thủ công các node này sẽ bị bỏ qua hoặc bị vô hiệu hóa vào lần tiếp theo node cha được thay đổi kích thước.

Tương tự, khi một node dẫn xuất từ *Container* được thay đổi kích thước, tất cả các node con của nó sẽ được định vị lại theo nó, với hành vi phụ thuộc vào loại container được sử dụng:

   .. image:: img/container_example.gif

Ví dụ về việc *HBoxContainer* thay đổi kích thước các nút con.

Sức mạnh thực sự của container nằm ở việc chúng có thể được lồng nhau (dưới dạng các node), cho phép tạo ra những bố cục rất phức tạp và dễ dàng thay đổi kích thước.

Tùy chọn kích thước
-------------------

Khi thêm một node vào container, cách container xử lý từng node con chủ yếu phụ thuộc vào *tùy chọn kích thước của container* tương ứng. Bạn có thể tìm thấy các tùy chọn này khi kiểm tra bố cục của bất kỳ *Control* nào là node con của *Container*.

   .. image:: img/container_sizing_options.webp

Các tùy chọn kích thước độc lập đối với chiều dọc và chiều ngang, và không phải container nào cũng sử dụng chúng (nhưng phần lớn có sử dụng):

* **Fill**: Đảm bảo control *lấp đầy* vùng được chỉ định trong container. Cho dù control có *mở rộng* hay không (xem bên dưới), nó sẽ chỉ *lấp đầy* vùng được chỉ định khi tùy chọn này được bật (mặc định là bật).
* **Expand**: Cố gắng sử dụng nhiều không gian nhất có thể trong container cha (trên từng trục). Các control không mở rộng sẽ bị những control có mở rộng đẩy ra xa. Giữa các control đang mở rộng, lượng không gian mà chúng chiếm của nhau được xác định bởi *Stretch Ratio* (xem bên dưới). Tùy chọn này chỉ khả dụng khi Container cha thuộc loại phù hợp; ví dụ, *HBoxContainer* có tùy chọn này cho kích thước ngang.
* **Shrink Begin** Khi mở rộng, cố gắng giữ nguyên vị trí ở bên trái hoặc phía trên của vùng được mở rộng.
* **Shrink Center** Khi mở rộng, cố gắng giữ nguyên vị trí ở giữa vùng được mở rộng.
* **Shrink End** Khi mở rộng, cố gắng giữ nguyên vị trí ở bên phải hoặc phía dưới của vùng được mở rộng.
* **Stretch Ratio**: Tỷ lệ lượng không gian mà các control được mở rộng chiếm so với nhau. Một control có giá trị "2" sẽ chiếm lượng không gian khả dụng gấp đôi control có giá trị "1".

Bạn nên thử nghiệm với các cờ này và các container khác nhau để hiểu rõ hơn cách chúng hoạt động.

Các loại container
------------------

Godot cung cấp sẵn một số loại container vì mỗi loại phục vụ các mục đích khác nhau:

Box Container
~~~~~~~~~~~~~

Sắp xếp các control con theo chiều dọc hoặc chiều ngang (thông qua :ref:`HBoxContainer <class_HBoxContainer>` và
:ref:`VBoxContainer <class_VBoxContainer>`). Theo hướng ngược lại với hướng được chỉ định (tức là chiều dọc đối với container ngang), nó chỉ mở rộng các node con.

   .. image:: img/containers_box.png

Các container này sử dụng thuộc tính *Stretch Ratio* cho các node con được đặt cờ *Expand*.

Grid Container
~~~~~~~~~~~~~~

Sắp xếp các control con theo bố cục dạng lưới (thông qua :ref:`GridContainer <class_GridContainer>`, phải chỉ định số cột). Sử dụng cả cờ mở rộng theo chiều dọc và chiều ngang.

   .. image:: img/containers_grid.png

Margin Container
~~~~~~~~~~~~~~~~

Các control con được mở rộng về phía các biên của control này (thông qua
:ref:`MarginContainer <class_MarginContainer>`). Phần đệm sẽ được thêm vào các lề tùy theo cấu hình theme.

   .. image:: img/containers_margin.png

Một lần nữa, hãy nhớ rằng các lề là một giá trị *Theme*, vì vậy bạn cần chỉnh sửa chúng trong phần ghi đè hằng số của từng control:

   .. image:: img/containers_margin_constants.png

Tab Container
~~~~~~~~~~~~~

Cho phép bạn đặt nhiều control con chồng lên nhau (thông qua
:ref:`TabContainer <class_TabContainer>`), trong đó chỉ control *hiện tại* được hiển thị.

   .. image:: img/containers_tab.png

Bạn có thể thay đổi control *hiện tại* thông qua các tab ở đầu container bằng cách nhấp vào:

   .. image:: img/containers_tab_click.gif

Theo mặc định, tiêu đề được tạo từ tên node (mặc dù có thể ghi đè chúng thông qua API *TabContainer*).

Có thể sửa đổi các thiết lập như vị trí tab và *StyleBox* trong phần ghi đè theme của *TabContainer*.

Split Container
~~~~~~~~~~~~~~~

Sắp xếp các control con theo chiều dọc hoặc chiều ngang và tạo các thanh kéo giữa chúng (thông qua :ref:`HSplitContainer <class_HSplitContainer>` và :ref:`VSplitContainer <class_VSplitContainer>`). Tuân theo cả cờ mở rộng theo chiều ngang và chiều dọc, cũng như *Stretch Ratio*.

   .. image:: img/containers_split.png

Có thể kéo các thanh kéo để thay đổi tương quan kích thước giữa các node con:

   .. image:: img/containers_split_drag.gif


PanelContainer
~~~~~~~~~~~~~~

Một container vẽ *StyleBox*, sau đó mở rộng các node con để bao phủ toàn bộ vùng của nó (thông qua :ref:`PanelContainer <class_PanelContainer>`, tuân theo các lề của *StyleBox*). Tuân theo cả các tùy chọn kích thước theo chiều ngang và chiều dọc.

   .. image:: img/containers_panel.png

Container này hữu ích khi dùng làm control cấp cao nhất, hoặc đơn giản là để thêm nền tùy chỉnh vào các phần của bố cục.

FoldableContainer
~~~~~~~~~~~~~~~~~

Một container có thể mở rộng/thu gọn (thông qua :ref:`FoldableContainer <class_FoldableContainer>`). Các control con sẽ bị ẩn khi container được thu gọn.

ScrollContainer
~~~~~~~~~~~~~~~

Chấp nhận một node con duy nhất. Nếu node con lớn hơn container, các thanh cuộn sẽ được thêm vào để cho phép di chuyển node xung quanh (thông qua :ref:`ScrollContainer <class_ScrollContainer>`). Cả các tùy chọn kích thước theo chiều dọc và chiều ngang đều được tuân theo, và bạn có thể bật hoặc tắt hành vi này theo từng trục trong các thuộc tính.

   .. image:: img/containers_scroll.png

Con lăn chuột và thao tác kéo bằng cảm ứng (khi có hỗ trợ cảm ứng) cũng là những cách hợp lệ để di chuyển điều khiển con.

   .. image:: img/containers_center_pan.gif

Như trong ví dụ trên, một trong những cách phổ biến nhất để sử dụng container này là đặt *VBoxContainer* làm con.

AspectRatioContainer
~~~~~~~~~~~~~~~~~~~~

Một loại container sắp xếp các điều khiển con theo cách tự động duy trì tỷ lệ của chúng khi container được thay đổi kích thước. (thông qua :ref:`AspectRatioContainer <class_AspectRatioContainer>`). Nó có nhiều chế độ co giãn, cung cấp các tùy chọn điều chỉnh kích thước của điều khiển con theo container: "fill", "width control height", "height control width" và "cover".

   .. image:: img/containers_aspectratio.webp

Nó hữu ích khi bạn có một container cần linh hoạt và đáp ứng với nhiều kích thước màn hình khác nhau, đồng thời muốn các phần tử con được масштаб theo tỷ lệ mà không làm mất hình dạng dự kiến.

   .. image:: img/containers_aspectratio_drag.webp

FlowContainer
~~~~~~~~~~~~~

FlowContainer là một container sắp xếp các điều khiển con theo chiều ngang hoặc chiều dọc (thông qua :ref:`HFlowContainer <class_HFlowContainer>` và thông qua :ref:`VFlowContainer <class_VFlowContainer>`). Khi không gian khả dụng đã hết, nó sẽ chuyển các phần tử con sang dòng hoặc cột tiếp theo, tương tự cách văn bản tự xuống dòng trong một cuốn sách.


   .. image:: img/containers_hflow.webp

Nó hữu ích để tạo các bố cục linh hoạt, trong đó các điều khiển con tự động điều chỉnh theo không gian khả dụng mà không chồng lấn lên nhau.

   .. image:: img/containers_hflow_drag.webp

CenterContainer
~~~~~~~~~~~~~~~

CenterContainer là một container tự động giữ tất cả điều khiển con ở chính giữa nó với kích thước tối thiểu của chúng. Nó đảm bảo các điều khiển con luôn được căn giữa, giúp tạo các bố cục căn giữa dễ dàng hơn mà không cần định vị thủ công (thông qua :ref:`CenterContainer <class_CenterContainer>`).

   .. image:: img/containers_center.webp

   .. image:: img/containers_center_drag.webp

SubViewportContainer
~~~~~~~~~~~~~~~~~~~~

Đây là một điều khiển đặc biệt chỉ chấp nhận một node *Viewport* duy nhất làm con và hiển thị node đó như thể nó là một hình ảnh (thông qua :ref:`SubViewportContainer <class_SubViewportContainer>`).

Tạo Containers tùy chỉnh
------------------------

Bạn có thể tạo một container tùy chỉnh bằng script. Dưới đây là ví dụ về một container điều chỉnh các phần tử con vừa với kích thước của nó:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Container

    func _notification(what):
        if what == NOTIFICATION_SORT_CHILDREN:
            # Cần sắp xếp lại các phần tử con
            for c in get_children():
                # Điều chỉnh vừa với kích thước của chính nó
                fit_child_in_rect(c, Rect2(Vector2(), size))

    func set_some_setting():
        # Một thiết lập đã thay đổi, yêu cầu sắp xếp lại các phần tử con.
        queue_sort()

 .. code-tab:: csharp

    using Godot;

    public partial class CustomContainer : Container
    {
        public override void _Notification(int what)
        {
            if (what == NotificationSortChildren)
            {
                // Cần sắp xếp lại các phần tử con
                foreach (Control c in GetChildren())
                {
                    // Điều chỉnh vừa với kích thước của chính nó
                    FitChildInRect(c, new Rect2(new Vector2(), Size));
                }
            }
        }

        public void SetSomeSetting()
        {
            // Một thiết lập đã thay đổi, yêu cầu sắp xếp lại các phần tử con.
            QueueSort();
        }
    }
