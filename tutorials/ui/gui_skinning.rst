.. _doc_gui_skinning:

Giới thiệu về skinning GUI
==========================

Điều thiết yếu đối với một game là cung cấp cho người chơi giao diện người dùng rõ ràng, giàu thông tin nhưng vẫn đẹp mắt. Mặc dù các node :ref:`Control <class_Control>` có giao diện đủ chức năng ngay từ đầu, vẫn luôn có chỗ để tạo sự độc đáo và tinh chỉnh theo từng trường hợp cụ thể. Vì mục đích này, engine Godot tích hợp một hệ thống skinning GUI (hay theming), cho phép bạn tùy chỉnh giao diện của mọi control trong giao diện người dùng, bao gồm cả các control tùy chỉnh của bạn.

Sau đây là một ví dụ về hệ thống này đang hoạt động — một game có GUI hoàn toàn khác với theme UI mặc định của engine:

.. figure:: img/tank-kings-by-winterpixel-games.png
   :align: center

   Màn hình "Gear Up!" trong Tank Kings, do Winterpixel Games cung cấp

Ngoài việc tạo ra diện mạo độc đáo cho game, hệ thống này còn cho phép nhà phát triển cung cấp các tùy chọn tùy chỉnh cho người dùng cuối, bao gồm cả các thiết lập trợ năng. Các theme UI được áp dụng theo dạng phân tầng (tức là lan truyền từ các control cha đến các control con), nghĩa là các thiết lập font hoặc điều chỉnh dành cho người dùng mù màu có thể được áp dụng tại một nơi duy nhất và ảnh hưởng đến toàn bộ cây UI. Tất nhiên, hệ thống này cũng có thể được dùng cho mục đích gameplay: game dựa trên hero của bạn có thể thay đổi phong cách theo nhân vật người chơi được chọn, hoặc bạn có thể tạo diện mạo khác nhau cho các phe trong dự án theo đội của mình.

Kiến thức cơ bản về theme
-------------------------

Hệ thống skinning được điều khiển bởi resource :ref:`Theme <class_Theme>`. Mọi project Godot đều có một theme mặc định vốn có, chứa các thiết lập được sử dụng bởi các control node tích hợp sẵn. Đây là yếu tố tạo nên diện mạo riêng của các control ngay từ đầu. Tuy nhiên, theme chỉ mô tả cấu hình, còn việc sử dụng cấu hình đó theo cách cần thiết để hiển thị chính mình vẫn thuộc về từng control riêng lẻ. Điều này rất quan trọng cần ghi nhớ khi triển khai
:ref:`các control tùy chỉnh của riêng bạn <doc_custom_gui_controls>`.

.. note::
   Ngay cả chính editor Godot cũng dựa vào theme mặc định. Tuy nhiên, nó không có giao diện giống một project Godot, vì nó áp dụng theme được tùy chỉnh rất nhiều của riêng mình lên trên theme mặc định. Về nguyên tắc, cơ chế này hoạt động chính xác như trong game của bạn, như được giải thích :ref:`bên dưới <doc_gui_theme_in_project>`.

Các mục của theme
~~~~~~~~~~~~~~~~~

Cấu hình được lưu trong một theme bao gồm các mục của theme. Mỗi mục có một tên duy nhất và phải thuộc một trong các kiểu dữ liệu sau:

-  **Color**

   Một giá trị :ref:`color <class_Color>`, thường được dùng cho font và background. Color cũng có thể được dùng để điều chỉnh màu của control và icon.

-  **Constant**

   Một giá trị số nguyên, có thể được dùng cho các thuộc tính số của control (chẳng hạn như khoảng cách giữa các item trong một :ref:`BoxContainer <class_BoxContainer>`), hoặc cho các cờ boolean (chẳng hạn như việc vẽ các đường liên kết trong một :ref:`Tree <class_Tree>`).

-  **Font**

   Một resource :ref:`font <class_Font>`, được sử dụng bởi các control hiển thị văn bản. Font chứa hầu hết các thiết lập kết xuất văn bản, ngoại trừ kích thước và màu của văn bản. Ngoài ra, việc căn chỉnh và hướng văn bản được điều khiển bởi từng control riêng lẻ.

-  **Font size**

   Một giá trị số nguyên, được dùng cùng với font để xác định kích thước hiển thị của văn bản.

-  **Icon**

   Một resource :ref:`texture <class_Texture2D>`, thường được dùng để hiển thị icon (ví dụ trên một :ref:`Button <class_Button>`).

-  **StyleBox**

   Một resource :ref:`StyleBox <class_StyleBox>`, là tập hợp các tùy chọn cấu hình xác định cách hiển thị một panel UI. Điều này không chỉ giới hạn ở control :ref:`Panel <class_Panel>`, vì stylebox được nhiều control sử dụng cho background và overlay của chúng.

   Các control khác nhau sẽ áp dụng StyleBox theo những cách khác nhau. Đáng chú ý nhất, các stylebox ``focus`` được vẽ dưới dạng *overlay* lên các stylebox khác (chẳng hạn như ``normal`` hoặc ``pressed``) để stylebox cơ sở vẫn hiển thị. Điều này có nghĩa là stylebox focus nên được thiết kế dưới dạng đường viền hoặc một box trong suốt, để background của nó vẫn có thể nhìn thấy.

Các kiểu theme
~~~~~~~~~~~~~~

Để hỗ trợ việc tổ chức các mục, mỗi theme được chia thành các kiểu và mỗi mục phải thuộc về một kiểu duy nhất. Nói cách khác, mỗi mục của theme được xác định bởi tên, kiểu dữ liệu và kiểu theme của nó. Tổ hợp này phải là duy nhất trong theme. Ví dụ, không thể có hai mục color cùng tên ``font_color`` trong một kiểu có tên ``Label``, nhưng có thể có một mục ``font_color`` khác trong kiểu ``LineEdit``.

Theme Godot mặc định đã định nghĩa sẵn nhiều kiểu theme, mỗi kiểu tương ứng với một control node tích hợp sẵn sử dụng skinning UI. Ví dụ trên chứa các mục theme thực tế có trong theme mặc định. Bạn có thể tham khảo phần **Theme Properties** trong tài liệu tham chiếu class của từng control để xem những mục nào có sẵn cho control đó và các class con của nó.

.. note::
   Các class con có thể sử dụng những mục theme được định nghĩa cho class cha của chúng (``Button`` và các class dẫn xuất của nó là một ví dụ điển hình). Trên thực tế, mọi control đều có thể sử dụng mọi mục theme thuộc bất kỳ kiểu theme nào nếu cần (nhưng để đảm bảo tính rõ ràng và dễ dự đoán, chúng tôi cố gắng tránh điều đó trong engine).

   Điều quan trọng cần ghi nhớ là đối với các class con, quy trình này được tự động hóa. Bất cứ khi nào một control tích hợp sẵn yêu cầu một mục theme từ theme, nó có thể bỏ qua kiểu theme, và tên class của nó sẽ được sử dụng thay thế. Ngoài ra, tên class của các class cha của nó cũng lần lượt được sử dụng. Điều này cho phép các thay đổi đối với class cha, chẳng hạn như ``Button``, ảnh hưởng đến mọi class dẫn xuất mà không cần tùy chỉnh từng class.

Bạn cũng có thể định nghĩa các kiểu theme của riêng mình, đồng thời tùy chỉnh cả control tích hợp sẵn lẫn control của riêng bạn. Vì các control tích hợp sẵn không biết về những kiểu theme tùy chỉnh của bạn, bạn phải sử dụng script để truy cập các mục đó. Tất cả control node đều có một số method cho phép bạn lấy các mục theme từ theme được áp dụng cho chúng. Những method đó nhận kiểu theme làm một trong các đối số.

.. tabs::
 .. code-tab:: gdscript

   var accent_color = get_theme_color("accent_color", "MyType")
   label.add_theme_color_override("font_color", accent_color)

 .. code-tab:: csharp

   Color accentColor = GetThemeColor("accent_color", "MyType");
   label.AddThemeColorOverride("font_color", accentColor);

Để có thêm cơ hội tùy chỉnh, các kiểu cũng có thể được liên kết với nhau dưới dạng các biến thể kiểu. Đây là một trường hợp sử dụng khác của các kiểu theme tùy chỉnh. Ví dụ, một theme có thể chứa một kiểu ``Header``, được đánh dấu là biến thể của kiểu cơ sở ``Label``. Sau đó, một control ``Label`` riêng lẻ có thể được thiết lập để sử dụng biến thể ``Header`` cho kiểu của nó, và mỗi khi một mục theme được yêu cầu từ theme, biến thể này sẽ được sử dụng trước mọi kiểu khác. Điều này cho phép lưu trữ nhiều preset của các mục theme cho cùng một class control node trong một resource ``Theme`` duy nhất.

.. warning::
   Chỉ những biến thể có sẵn từ theme mặc định hoặc được định nghĩa trong theme tùy chỉnh của project mới được hiển thị dưới dạng các tùy chọn trong dock Inspector. Bạn vẫn có thể nhập thủ công tên của một biến thể được định nghĩa bên ngoài hai nơi này, nhưng nên giữ tất cả các biến thể trong theme của project.

Bạn có thể tìm hiểu thêm về cách tạo và sử dụng các biến thể kiểu theme trong một
:ref:`bài viết chuyên biệt <doc_gui_theme_type_variations>`.

Tùy chỉnh một control
---------------------

Mỗi control node có thể được tùy chỉnh trực tiếp mà không cần dùng theme. Đây được gọi là local override. Mọi thuộc tính theme trong tài liệu tham chiếu class của control đều có thể được ghi đè trực tiếp trên chính control đó, bằng dock Inspector hoặc script. Điều này cho phép thực hiện những thay đổi chi tiết đối với một phần cụ thể của UI mà không ảnh hưởng đến bất kỳ thành phần nào khác trong project, kể cả các control con của control này.

.. figure:: img/themecheck.webp
   :align: center

Các ghi đè cục bộ ít hữu ích hơn đối với việc tạo điểm nhấn trực quan cho giao diện người dùng, đặc biệt nếu bạn hướng đến tính nhất quán. Tuy nhiên, đối với các node bố cục, chúng lại rất cần thiết. Các node như :ref:`BoxContainer <class_BoxContainer>` và
:ref:`GridContainer <class_GridContainer>` sử dụng các hằng số của theme để xác định khoảng cách giữa các node con, còn :ref:`MarginContainer <class_MarginContainer>` lưu trữ các lề có thể tùy chỉnh trong các mục theme của nó.

Bất cứ khi nào một control có ghi đè mục theme cục bộ, nó sẽ sử dụng giá trị này. Các giá trị do theme cung cấp sẽ bị bỏ qua.

.. _doc_gui_theme_in_project:

Tùy chỉnh project
-----------------

Theo mặc định, mỗi project sử dụng project theme mặc định do Godot cung cấp. Bản thân theme mặc định là hằng số và không thể thay đổi, nhưng các mục của nó có thể được ghi đè bằng một theme tùy chỉnh. Theme tùy chỉnh có thể được áp dụng theo hai cách: dưới dạng cài đặt project và dưới dạng thuộc tính node trong toàn bộ cây các control node.

Có hai cài đặt project có thể điều chỉnh để ảnh hưởng đến toàn bộ project của bạn:
:ref:`GUI > Theme > Custom <class_ProjectSettings_property_gui/theme/custom>` cho phép bạn đặt theme tùy chỉnh trên toàn project, còn :ref:`GUI > Theme > Custom Font <class_ProjectSettings_property_gui/theme/custom_font>` thực hiện điều tương tự với font dự phòng mặc định. Khi một control node yêu cầu một mục theme, theme project tùy chỉnh, nếu có, sẽ được kiểm tra trước. Chỉ khi theme này không có mục đó thì theme mặc định mới được kiểm tra.

Điều này cho phép bạn cấu hình giao diện mặc định của mọi control trong Godot bằng một resource theme duy nhất, nhưng bạn có thể tinh chỉnh chi tiết hơn. Mỗi control node cũng có thuộc tính :ref:`theme <class_Control_property_theme>`, cho phép bạn đặt một theme tùy chỉnh cho nhánh node bắt đầu từ control đó. Điều này có nghĩa là control đó cùng tất cả node con của nó, cũng như các node con của chúng, trước tiên sẽ kiểm tra resource theme tùy chỉnh đó trước khi chuyển sang theme project và theme mặc định.

.. note::
   Thay vì thay đổi cài đặt project, bạn có thể đặt resource theme tùy chỉnh cho control node ở gốc của toàn bộ nhánh UI để đạt được hiệu ứng gần như tương tự. Khi project đang chạy, nó sẽ hoạt động như mong đợi, nhưng các scene riêng lẻ vẫn hiển thị bằng theme mặc định khi xem trước hoặc chạy trực tiếp. Để khắc phục điều đó, bạn có thể đặt cùng resource theme cho control gốc của từng scene riêng lẻ.

Ví dụ, bạn có thể có một kiểu nhất định cho các button trong theme project, nhưng lại muốn các button bên trong một hộp thoại popup có giao diện khác. Bạn có thể đặt một resource theme tùy chỉnh cho control gốc của popup và định nghĩa một kiểu khác cho các button trong resource đó. Miễn là chuỗi control node giữa gốc của popup và các button không bị gián đoạn, các button đó sẽ sử dụng những kiểu được định nghĩa trong resource theme gần chúng nhất. Tất cả control khác vẫn sẽ được tạo kiểu bằng theme trên toàn project và các kiểu của theme mặc định.

Tóm lại, đối với một control bất kỳ, quá trình tra cứu mục theme sẽ tương tự như sau:

#. Kiểm tra các ghi đè cục bộ có cùng kiểu dữ liệu và tên.
#. Sử dụng biến thể kiểu của control, tên class và tên các class cha:

   a. Kiểm tra từng control, bắt đầu từ chính nó, và xem nó có được đặt thuộc tính theme hay không;
   b. Nếu có, kiểm tra theme đó để tìm mục khớp có cùng tên, dữ liệu và kiểu theme;
   c. Nếu không có theme tùy chỉnh hoặc theme đó không có mục này, chuyển đến control cha;
   d. Lặp lại các bước a-c. cho đến khi đến gốc của cây hoặc gặp một node không phải control.

#. Sử dụng biến thể kiểu của control, tên class và tên các class cha để kiểm tra theme trên toàn project, nếu theme đó tồn tại.
#. Sử dụng biến thể kiểu của control, tên class và tên các class cha để kiểm tra theme mặc định.

Ngay cả khi mục này không tồn tại trong bất kỳ theme nào, một giá trị mặc định tương ứng cho kiểu dữ liệu đó vẫn sẽ được trả về.

Ngoài các control
-----------------

Đương nhiên, theme là một loại resource lý tưởng để lưu trữ cấu hình cho các thành phần trực quan. Mặc dù chức năng hỗ trợ theme được tích hợp sẵn trong các control node, các node khác cũng có thể sử dụng chúng, giống như bất kỳ resource nào khác.

Một ví dụ về việc sử dụng theme cho những thứ ngoài control là điều chỉnh màu của các sprite đại diện cho cùng một đơn vị thuộc các phe khác nhau trong một game chiến thuật. Một resource theme có thể định nghĩa một tập hợp màu, còn các sprite (với sự hỗ trợ của script) có thể sử dụng những màu đó để vẽ texture. Lợi ích chính là bạn có thể tạo các theme khác nhau bằng cùng những mục theme cho phe đỏ, xanh dương và xanh lá, rồi chuyển đổi giữa chúng chỉ bằng một thay đổi resource.
