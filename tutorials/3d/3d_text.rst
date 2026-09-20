.. _doc_3d_text:

Văn bản 3D
==========

Giới thiệu
----------

Trong một project, đôi khi bạn cần tạo văn bản như một phần của cảnh 3D thay vì chỉ hiển thị trong HUD. Godot cung cấp 2 phương pháp để thực hiện việc này: node Label3D và *resource* TextMesh cho node MeshInstance3D.

Ngoài ra, Godot cho phép định vị các node Control theo vị trí của một điểm 3D trên camera. Bạn có thể dùng cách này thay cho văn bản 3D "thực" trong những trường hợp Label3D và TextMesh không đủ linh hoạt.

.. seealso::

    Bạn có thể xem văn bản 3D hoạt động như thế nào trong `project demo 3D Labels and Texts <https://github.com/godotengine/godot-demo-projects/tree/master/3d/labels_and_texts>`__.

    Trang này **không** đề cập đến cách hiển thị một cảnh GUI trong môi trường 3D. Để biết cách thực hiện, hãy xem `project demo GUI in 3D <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/gui_in_3d>`__.

Label3D
-------

.. image:: img/label_3d.png

Label3D hoạt động giống như node Label, nhưng trong không gian 3D. Không giống node Label, node Label3D này **không** kế thừa các thuộc tính của GUI theme. Tuy nhiên, giao diện của nó vẫn có thể tùy chỉnh và sử dụng cùng font subresource như các node Control (bao gồm hỗ trợ :abbr:`MSDF (Multi-channel Signed Distance Font)` font rendering).

Ưu điểm
~~~~~~~

- Label3D tạo nhanh hơn TextMesh. Mặc dù cả hai đều sử dụng cơ chế caching để chỉ render các glyph mới một lần, Label3D vẫn tạo (hoặc tạo lại) nhanh hơn, đặc biệt với văn bản dài. Điều này có thể tránh hiện tượng giật trong khi chơi game trên CPU cấp thấp hoặc thiết bị di động. - Label3D có thể sử dụng bitmap font và dynamic font (có và không có
  :abbr:`MSDF (Multi-channel Signed Distance Font)` or mipmaps). This makes it
  linh hoạt hơn về khía cạnh đó so với TextMesh, đặc biệt khi render font có đường viền tự giao nhau hoặc font có màu (emoji).

.. seealso::

    Xem :ref:`doc_gui_using_fonts` để biết hướng dẫn về cách cấu hình quá trình import font.

Hạn chế
~~~~~~~

Theo mặc định, Label3D có tương tác hạn chế với môi trường 3D. Nó có thể bị che khuất bởi hình học và được chiếu sáng bởi các nguồn sáng nếu bật cờ **Shaded**. Tuy nhiên, nó sẽ không đổ bóng ngay cả khi **Cast Shadow** được đặt thành **On** trong các thuộc tính GeometryInstance3D của Label3D. Điều này là do node này tạo nội bộ một quad mesh (mỗi glyph tương ứng với một quad) cùng các texture trong suốt và có những hạn chế giống như Sprite3D. Các vấn đề về sắp xếp transparency cũng có thể xuất hiện khi nhiều Label3D chồng lên nhau, đặc biệt nếu chúng có đường viền.

Bạn có thể giảm thiểu vấn đề này bằng cách đặt transparency mode của Label3D thành **Alpha Cut**, đổi lại chất lượng render văn bản sẽ kém mượt hơn. Transparency mode **Opaque Pre-Pass** có thể duy trì độ mượt của văn bản đồng thời cho phép Label3D đổ bóng, nhưng một số vấn đề về sắp xếp transparency vẫn sẽ còn tồn tại.

Xem phần :ref:`Transparency sorting <doc_3d_rendering_limitations_transparency_sorting>` trong trang về các hạn chế của 3D rendering để biết thêm thông tin.

Chất lượng rendering văn bản cũng có thể bị ảnh hưởng khi Label3D được nhìn từ xa. Để cải thiện chất lượng rendering văn bản, :ref:`enable mipmaps on the font <doc_using_fonts_mipmaps>` hoặc
:ref:`switch the font to use MSDF rendering <doc_using_fonts_msdf>`.

TextMesh
--------

.. image:: img/text_mesh.png

TextMesh resource có một số điểm tương đồng với Label3D. Cả hai đều hiển thị văn bản trong một cảnh 3D và sử dụng cùng font subresource. Tuy nhiên, thay vì tạo các quad trong suốt, TextMesh tạo hình học 3D biểu diễn các đường bao của glyph và có các thuộc tính của một mesh. Do đó, TextMesh được shaded theo mặc định và tự động đổ bóng lên môi trường. TextMesh cũng có thể được áp dụng material (bao gồm custom shader).

Dưới đây là một ví dụ về texture và cách texture đó được áp dụng vào mesh. Bạn có thể sử dụng texture bên dưới làm tham chiếu cho UV map của mesh được tạo:

.. image:: img/text_mesh_texture.png

.. image:: img/text_mesh_textured.png

Ưu điểm
~~~~~~~

TextMesh có một số ưu điểm so với Label3D:

- TextMesh có thể sử dụng texture để thay đổi màu văn bản theo từng mặt. - Hình học TextMesh có thể có độ sâu thực, tạo cho glyph giao diện 3D. - TextMesh có thể sử dụng custom shader, không giống Label3D.

Hạn chế
~~~~~~~

TextMesh có một số hạn chế:

- Không có hỗ trợ outline tích hợp sẵn, không giống Label3D. Tuy nhiên, bạn có thể mô phỏng điều này bằng custom shader. - Chỉ dynamic font được hỗ trợ (``.ttf``, ``.otf``, ``.woff``, ``.woff2``). Bitmap font ở định dạng ``.fnt`` hoặc ``.font`` **không** được hỗ trợ. - Font có đường viền tự giao nhau sẽ không được render chính xác. Nếu bạn nhận thấy vấn đề rendering với các font tải xuống từ những website như Google Fonts, hãy thử tải font từ website chính thức của tác giả font. - Để antialiasing cho việc rendering văn bản, cần bật một phương pháp antialiasing cho toàn cảnh, chẳng hạn như MSAA, FXAA và temporal antialiasing (TAA). Nếu không bật phương pháp antialiasing nào, văn bản sẽ có dạng nhiễu, đặc biệt khi nhìn từ xa. Xem :ref:`doc_3d_antialiasing` để biết thêm thông tin.

Node Label được chiếu (hoặc bất kỳ Control nào khác)
----------------------------------------------------

Có một giải pháp cuối cùng phức tạp hơn khi thiết lập nhưng mang lại nhiều tính linh hoạt nhất: chiếu một node 2D lên không gian 3D. Bạn có thể thực hiện việc này bằng cách sử dụng giá trị trả về của method :ref:`unproject_position<class_Camera3D_method_unproject_position>` trên node Camera3D trong hàm ``_process()`` của một script. Sau đó, dùng giá trị trả về này để đặt thuộc tính ``position`` của một node Control.

Xem demo `3D waypoints <https://github.com/godotengine/godot-demo-projects/tree/master/3d/waypoints>`__ để biết ví dụ về cách thực hiện.

Ưu điểm
~~~~~~~

- Có thể sử dụng bất kỳ node Control nào, bao gồm Label, RichTextLabel hoặc thậm chí các node như Button. Điều này cho phép định dạng mạnh mẽ và tương tác GUI. - Cách tiếp cận dựa trên script cho phép hoàn toàn tự do trong việc định vị. Ví dụ, cách này giúp ghim Control vào các cạnh màn hình dễ dàng hơn đáng kể khi chúng đi ra ngoài màn hình (dùng cho các marker 3D trong game). - Tuân theo Control theming. Điều này giúp tùy chỉnh dễ dàng hơn và áp dụng trên toàn project.

Hạn chế
~~~~~~~

- Projected Control không thể bị che khuất bởi hình học 3D theo bất kỳ cách nào. Bạn có thể dùng RayCast để ẩn hoàn toàn control nếu vị trí mục tiêu của nó bị collider che khuất, nhưng cách này không cho phép ẩn một phần control phía sau tường. - Có thể thay đổi kích thước văn bản theo khoảng cách bằng cách điều chỉnh thuộc tính ``scale`` của Control, nhưng bạn phải tự thực hiện. Label3D và TextMesh tự động xử lý việc này, đổi lại chúng kém linh hoạt hơn (không thể đặt kích thước văn bản tối thiểu/tối đa theo pixel). - Script cần xử lý các thay đổi về resolution và aspect ratio, điều này có thể gây khó khăn.

Nên sử dụng Label3D, TextMesh hay Control được chiếu?
-----------------------------------------------------

Trong hầu hết các trường hợp, Label3D được khuyến nghị vì dễ thiết lập hơn và cung cấp chất lượng rendering cao hơn (đặc biệt khi 3D antialiasing bị tắt).

Đối với các trường hợp sử dụng nâng cao, TextMesh linh hoạt hơn vì cho phép tạo kiểu cho văn bản bằng custom shader. Custom shader cho phép sửa đổi hình học cuối cùng, chẳng hạn như uốn cong văn bản dọc theo một bề mặt. Vì văn bản là hình học 3D thực, bạn có thể tùy chọn tạo độ sâu cho văn bản và văn bản cũng có thể đóng góp vào global illumination.

Nếu bạn cần các tính năng như hỗ trợ BBCode hoặc Control theming, thì sử dụng một node RichTextLabel được chiếu là lựa chọn duy nhất.
