.. _doc_gui_skinning:

Giới thiệu về skinning GUI
==========================

Điều thiết yếu đối với một game là cung cấp cho người chơi giao diện người dùng rõ ràng, đầy đủ thông tin nhưng vẫn đẹp mắt. Mặc dù các node :ref:`Control <class_Control>` có giao diện khá đầy đủ chức năng ngay từ đầu, vẫn luôn có chỗ để tạo sự độc đáo và tinh chỉnh theo từng trường hợp cụ thể. Vì mục đích này, Godot engine tích hợp một hệ thống skinning GUI (hay theming), cho phép bạn tùy chỉnh giao diện của mọi control trong giao diện người dùng, bao gồm cả các control tùy chỉnh của bạn.

Dưới đây là một ví dụ về hệ thống này khi hoạt động — một game có GUI hoàn toàn khác với UI theme mặc định của engine:

.. figure:: img/tank-kings-by-winterpixel-games.png
   :align: center

   A "Gear Up!" screen in Tank Kings, courtesy of Winterpixel Games

Ngoài việc tạo ra diện mạo độc đáo cho game, hệ thống này còn cho phép các developer cung cấp tùy chọn tùy chỉnh cho người dùng cuối, bao gồm cả các cài đặt hỗ trợ khả năng tiếp cận. UI theme được áp dụng theo kiểu phân tầng (tức là lan truyền từ các control cha xuống các control con), nghĩa là các cài đặt font hoặc điều chỉnh màu sắc cho người dùng mù màu có thể được áp dụng tại một nơi duy nhất và ảnh hưởng đến toàn bộ cây UI. Tất nhiên, hệ thống này cũng có thể được dùng cho mục đích gameplay: game dựa trên các hero của bạn có thể thay đổi style theo nhân vật người chơi được chọn, hoặc bạn có thể tạo các sắc thái khác nhau cho các phe trong project đấu đội của mình.

Kiến thức cơ bản về theme
-------------------------

Hệ thống skinning được điều khiển bởi resource :ref:`Theme <class_Theme>`. Mọi project Godot đều có một theme mặc định vốn có, chứa các cài đặt được sử dụng bởi những control node tích hợp sẵn. Đây là thứ tạo nên diện mạo đặc trưng cho các control ngay từ đầu. Tuy nhiên, theme chỉ mô tả cấu hình, còn việc mỗi control riêng lẻ sử dụng cấu hình đó theo cách cần thiết để hiển thị chính nó vẫn thuộc về control đó. Điều này rất quan trọng cần ghi nhớ khi triển khai
:ref:`your own custom controls <doc_custom_gui_controls>`.

.. note::
   Ngay cả Godot editor cũng dựa trên theme mặc định. Tuy nhiên, nó không có giao diện giống một project Godot, vì nó áp dụng theme được tùy chỉnh rất nhiều của riêng mình lên trên theme mặc định. Về nguyên tắc, điều này hoạt động chính xác như trong game của bạn, như đã giải thích :ref:`below <doc_gui_theme_in_project>`.

Các mục của theme
~~~~~~~~~~~~~~~~~

Cấu hình được lưu trong một theme bao gồm các mục theme. Mỗi mục có một tên duy nhất và phải thuộc một trong các kiểu dữ liệu sau:

-  **Color**

   Một giá trị :ref:`color <class_Color>`, thường được dùng cho font và background. Color cũng có thể được dùng để điều chỉnh màu (modulation) của control và icon.

-  **Constant**

   Một giá trị integer, có thể được dùng cho các thuộc tính số của control (chẳng hạn như khoảng cách giữa các mục trong một :ref:`BoxContainer <class_BoxContainer>`), hoặc cho các cờ boolean (chẳng hạn như việc vẽ các đường liên kết trong một :ref:`Tree <class_Tree>`).

-  **Font**

   Một resource :ref:`font <class_Font>`, được các control hiển thị văn bản sử dụng. Font chứa hầu hết cài đặt kết xuất văn bản, ngoại trừ kích thước và màu sắc của nó. Ngoài ra, việc căn chỉnh và hướng văn bản được các control riêng lẻ điều khiển.

-  **Font size**

   Một giá trị integer, được sử dụng cùng với font để xác định kích thước hiển thị của văn bản.

-  **Icon**

   Một resource :ref:`texture <class_Texture2D>`, thường được dùng để hiển thị một icon (chẳng hạn trên một :ref:`Button <class_Button>`).

-  **StyleBox**

   Một resource :ref:`StyleBox <class_StyleBox>`, là tập hợp các tùy chọn cấu hình xác định cách hiển thị một panel UI. Điều này không chỉ giới hạn ở control :ref:`Panel <class_Panel>`, vì stylebox được nhiều control sử dụng cho background và lớp phủ của chúng.

   Các control khác nhau sẽ áp dụng StyleBox theo những cách khác nhau. Đáng chú ý nhất, stylebox ``focus`` được vẽ như một *lớp phủ* lên các stylebox khác (chẳng hạn như ``normal`` hoặc ``pressed``) để stylebox cơ sở vẫn hiển thị. Điều này có nghĩa là stylebox focus nên được thiết kế dưới dạng đường viền hoặc một box bán trong suốt, để background của nó vẫn nhìn thấy được.

Các kiểu theme
~~~~~~~~~~~~~~

Để giúp tổ chức các mục, mỗi theme được chia thành các kiểu, và mỗi mục phải thuộc về một kiểu duy nhất. Nói cách khác, mỗi mục theme được xác định bởi tên, kiểu dữ liệu và kiểu theme của nó. Tổ hợp này phải là duy nhất trong theme. Ví dụ, không thể có hai mục color tên là ``font_color`` trong một kiểu có tên ``Label``, nhưng có thể có một mục ``font_color`` khác trong kiểu ``LineEdit``.

Theme Godot mặc định đi kèm với nhiều kiểu theme đã được định nghĩa sẵn, mỗi kiểu tương ứng với một control node tích hợp sử dụng skinning UI. Ví dụ trên chứa các mục theme thực tế có trong theme mặc định. Bạn có thể tham khảo phần **Theme Properties** trong class reference của từng control để xem những mục nào khả dụng cho control đó và các class con của nó.

.. note::
   Các class con có thể sử dụng những mục theme được định nghĩa cho class cha của chúng (``Button`` và các class dẫn xuất của nó là một ví dụ điển hình). Trên thực tế, mọi control đều có thể sử dụng mọi mục theme của bất kỳ kiểu theme nào nếu cần (nhưng để đảm bảo tính rõ ràng và dễ dự đoán, chúng tôi cố gắng tránh điều đó trong engine).

   Điều quan trọng cần nhớ là đối với các class con, quy trình đó được tự động hóa. Bất cứ khi nào một control tích hợp yêu cầu một mục theme từ theme, nó có thể bỏ qua kiểu theme, và tên class của nó sẽ được sử dụng thay thế. Ngoài ra, tên class của các class cha của nó cũng sẽ lần lượt được sử dụng. Điều này cho phép các thay đổi đối với class cha, chẳng hạn như ``Button``, ảnh hưởng đến tất cả class dẫn xuất mà không cần tùy chỉnh từng class.

Bạn cũng có thể định nghĩa các kiểu theme của riêng mình, đồng thời tùy chỉnh cả control tích hợp lẫn control của riêng bạn. Vì các control tích hợp không biết về các kiểu theme tùy chỉnh của bạn, bạn phải sử dụng script để truy cập các mục đó. Tất cả control node đều có một số method cho phép bạn lấy các mục theme từ theme được áp dụng cho chúng. Các method đó nhận kiểu theme làm một trong các argument.

.. tabs::
 .. code-tab:: gdscript

   var accent_color = get_theme_color("accent_color", "MyType")
   label.add_theme_color_override("font_color", accent_color)

 .. code-tab:: csharp

   Color accentColor = GetThemeColor("accent_color", "MyType");
   label.AddThemeColorOverride("font_color", accentColor);

Để có thêm nhiều cơ hội tùy chỉnh, các kiểu cũng có thể được liên kết với nhau dưới dạng các biến thể kiểu. Đây là một cách sử dụng khác của các kiểu theme tùy chỉnh. Ví dụ, một theme có thể chứa một kiểu ``Header``, được đánh dấu là biến thể của kiểu cơ sở ``Label``. Sau đó, một control ``Label`` riêng lẻ có thể được đặt để sử dụng biến thể ``Header`` cho kiểu của nó, và mỗi khi một mục theme được yêu cầu từ theme, biến thể này sẽ được sử dụng trước mọi kiểu khác. Điều này cho phép lưu trữ nhiều preset mục theme khác nhau cho cùng một class control node trong một resource ``Theme`` duy nhất.

.. warning::
   Chỉ những biến thể có trong theme mặc định hoặc được định nghĩa trong custom theme của project mới được hiển thị dưới dạng tùy chọn trong dock Inspector. Bạn vẫn có thể nhập thủ công tên của một biến thể được định nghĩa bên ngoài hai nơi đó, nhưng nên giữ tất cả biến thể trong theme của project.

Bạn có thể tìm hiểu thêm về cách tạo và sử dụng các biến thể kiểu theme trong một
:ref:`dedicated article <doc_gui_theme_type_variations>`.

Tùy chỉnh một control
---------------------

Mỗi control node có thể được tùy chỉnh trực tiếp mà không cần dùng theme. Đây được gọi là local override. Mọi thuộc tính theme trong class reference của control đều có thể được ghi đè trực tiếp trên chính control đó, bằng dock Inspector hoặc script. Điều này cho phép thực hiện các thay đổi chi tiết đối với một phần cụ thể của UI mà không ảnh hưởng đến bất kỳ thứ gì khác trong project, bao gồm cả các control con của control này.

.. figure:: img/themecheck.webp
   :align: center

Local override ít hữu ích hơn đối với việc tạo điểm nhấn trực quan cho giao diện người dùng, đặc biệt nếu bạn hướng đến tính nhất quán. Tuy nhiên, đối với các layout node, chúng lại rất cần thiết. Các node như :ref:`BoxContainer <class_BoxContainer>` và
:ref:`GridContainer <class_GridContainer>` use theme constants for defining
khoảng cách giữa các node con, còn :ref:`MarginContainer <class_MarginContainer>` lưu các margin có thể tùy chỉnh trong các mục theme của nó.

Bất cứ khi nào một control có local theme item override, nó sẽ sử dụng giá trị này. Các giá trị do theme cung cấp sẽ bị bỏ qua.

.. _doc_gui_theme_in_project:

Tùy chỉnh một project
---------------------

Ngay từ đầu, mỗi project sử dụng theme project mặc định do Godot cung cấp. Bản thân theme mặc định là cố định và không thể thay đổi, nhưng các mục của nó có thể được ghi đè bằng custom theme. Custom theme có thể được áp dụng theo hai cách: dưới dạng một project setting và dưới dạng thuộc tính node xuyên suốt cây control node.

Có hai project setting có thể được điều chỉnh để ảnh hưởng đến toàn bộ project của bạn:
:ref:`GUI > Theme > Custom<class_ProjectSettings_property_gui/theme/custom>` allows you to
đặt một theme tùy chỉnh áp dụng trên toàn project, và :ref:`GUI > Theme > Custom Font<class_ProjectSettings_property_gui/theme/custom_font>` thực hiện điều tương tự với fallback font mặc định. Khi một control node yêu cầu một mục theme, custom theme của project, nếu có, sẽ được kiểm tra trước. Chỉ khi nó không có mục đó thì theme mặc định mới được kiểm tra.

Điều này cho phép bạn cấu hình diện mạo mặc định của mọi Godot control chỉ bằng một theme resource, nhưng bạn có thể thực hiện chi tiết hơn thế. Mỗi control node cũng có một thuộc tính :ref:`theme <class_Control_property_theme>`, cho phép bạn đặt một custom theme cho nhánh node bắt đầu từ control đó. Điều này có nghĩa là control đó cùng tất cả control con của nó, và các control con của chúng, trước tiên sẽ kiểm tra custom theme resource đó trước khi fallback về theme của project và theme mặc định.

.. note::
   Thay vì thay đổi project setting, bạn có thể đặt custom theme resource cho control node ở gốc của toàn bộ nhánh UI để đạt được hiệu ứng gần như tương tự. Khi project đang chạy, nó sẽ hoạt động như mong đợi, nhưng các scene riêng lẻ vẫn hiển thị bằng theme mặc định khi được preview hoặc chạy trực tiếp. Để khắc phục điều đó, bạn có thể đặt cùng theme resource cho control gốc của từng scene riêng lẻ.

Ví dụ, bạn có thể sử dụng một kiểu nhất định cho các button trong theme của dự án, nhưng lại muốn các button bên trong một popup dialog có giao diện khác. Bạn có thể đặt một theme resource tùy chỉnh cho control gốc của popup và định nghĩa một kiểu khác cho các button trong resource đó. Miễn là chuỗi control node giữa gốc của popup và các button không bị gián đoạn, các button đó sẽ sử dụng những kiểu được định nghĩa trong theme resource gần chúng nhất. Tất cả control khác vẫn sẽ được tạo kiểu bằng theme cấp dự án và các kiểu theme mặc định.

Tóm lại, với một control bất kỳ, việc tra cứu theme item sẽ diễn ra đại khái như sau:

#. Kiểm tra các ghi đè cục bộ có cùng kiểu dữ liệu và tên. #. Sử dụng type variation, tên class và tên các class cha của control:

   a. Kiểm tra từng control, bắt đầu từ chính nó, và xem nó có được thiết lập thuộc tính theme hay không; b. Nếu có, kiểm tra theme đó để tìm item khớp có cùng tên, dữ liệu và theme type; c. Nếu không có theme tùy chỉnh hoặc theme đó không có item này, chuyển đến control cha; d. Lặp lại các bước a-c. cho đến khi đến gốc của cây hoặc gặp một node không phải control.

#. Sử dụng type variation, tên class và tên các class cha của control để kiểm tra theme cấp dự án, nếu theme này tồn tại. #. Sử dụng type variation, tên class và tên các class cha của control để kiểm tra theme mặc định.

Ngay cả khi item không tồn tại trong bất kỳ theme nào, một giá trị mặc định tương ứng với kiểu dữ liệu đó vẫn sẽ được trả về.

Ngoài các control
-----------------

Đương nhiên, theme là một loại resource lý tưởng để lưu trữ cấu hình cho bất cứ thứ gì mang tính trực quan. Mặc dù khả năng hỗ trợ theming được tích hợp trong các control node, những node khác cũng có thể sử dụng theme, giống như bất kỳ resource nào khác.

Một ví dụ về việc sử dụng theme cho mục đích ngoài các control là điều chỉnh màu (modulation) của các sprite đại diện cho cùng một loại unit thuộc những đội khác nhau trong một game chiến thuật. Một theme resource có thể định nghĩa một tập hợp màu, còn các sprite (với sự hỗ trợ của script) có thể sử dụng những màu đó để vẽ texture. Lợi ích chính là bạn có thể tạo các theme khác nhau bằng cách sử dụng cùng những theme item cho đội đỏ, xanh dương và xanh lá, rồi chuyển đổi giữa chúng chỉ bằng một thay đổi resource.
