.. _doc_3d_text:

Văn bản 3D
==========

Giới thiệu
----------

Trong một project, đôi khi cần tạo văn bản như một phần của scene 3D thay vì chỉ trong HUD. Godot cung cấp 2 phương pháp để thực hiện việc này: node Label3D và *resource* TextMesh cho node MeshInstance3D.

Ngoài ra, Godot cho phép định vị các node Control dựa trên vị trí của một điểm 3D trên camera. Có thể dùng cách này thay thế cho văn bản 3D "thực" trong những trường hợp Label3D và TextMesh không đủ linh hoạt.

.. seealso::

    Bạn có thể xem văn bản 3D hoạt động như thế nào trong `project demo 3D Labels and Texts <https://github.com/godotengine/godot-demo-projects/tree/master/3d/labels_and_texts>`__.

    Trang này **không** đề cập đến cách hiển thị một scene GUI trong môi trường 3D. Để biết cách thực hiện, hãy xem project demo `GUI in 3D <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/gui_in_3d>`__.

Label3D
-------

.. image:: img/label_3d.png

Label3D hoạt động giống như một node Label, nhưng trong không gian 3D. Không giống node Label, node Label3D này **không** kế thừa các thuộc tính của GUI theme. Tuy nhiên, giao diện của nó vẫn có thể tùy chỉnh và sử dụng cùng font subresource như các node Control (bao gồm hỗ trợ render font :abbr:`MSDF (Multi-channel Signed Distance Font)`).

Ưu điểm
~~~~~~~

- Label3D được tạo nhanh hơn TextMesh. Mặc dù cả hai đều sử dụng cơ chế caching để chỉ render các glyph mới một lần, Label3D vẫn được (tái) tạo nhanh hơn, đặc biệt với văn bản dài. Điều này có thể tránh hiện tượng giật trong khi chơi game trên CPU cấp thấp hoặc thiết bị di động.
- Label3D có thể sử dụng bitmap font và dynamic font (có hoặc không có
  :abbr:`MSDF (Multi-channel Signed Distance Font)` hoặc mipmap). Điều này giúp Label3D linh hoạt hơn TextMesh ở khía cạnh đó, đặc biệt khi render các font có đường viền tự giao nhau hoặc font màu (emoji).

.. seealso::

    Xem :ref:`doc_gui_using_fonts` để biết hướng dẫn cấu hình việc import font.

Hạn chế
~~~~~~~

Theo mặc định, Label3D có tương tác hạn chế với môi trường 3D. Nó có thể bị che bởi hình học và được chiếu sáng bởi các nguồn sáng nếu bật cờ **Shaded**. Tuy nhiên, nó sẽ không đổ bóng ngay cả khi **Cast Shadow** được đặt thành **On** trong các thuộc tính GeometryInstance3D của Label3D. Lý do là node này tạo nội bộ một quad mesh (mỗi glyph tương ứng với một quad) sử dụng texture trong suốt và có cùng hạn chế như Sprite3D. Các vấn đề sắp xếp độ trong suốt cũng có thể xuất hiện khi nhiều Label3D chồng lên nhau, đặc biệt nếu chúng có đường viền.

Có thể giảm thiểu vấn đề này bằng cách đặt chế độ trong suốt của Label3D thành **Alpha Cut**, nhưng văn bản sẽ kém mượt hơn. Chế độ trong suốt **Opaque Pre-Pass** có thể giữ độ mượt của văn bản đồng thời cho phép Label3D đổ bóng, nhưng một số vấn đề sắp xếp độ trong suốt vẫn sẽ còn.

Xem phần :ref:`Transparency sorting <doc_3d_rendering_limitations_transparency_sorting>` trong trang về các hạn chế khi render 3D để biết thêm thông tin.

Chất lượng render văn bản cũng có thể giảm khi Label3D được nhìn từ xa. Để cải thiện chất lượng render văn bản, :ref:`hãy bật mipmap cho font <doc_using_fonts_mipmaps>` hoặc
:ref:`chuyển font sang sử dụng rendering MSDF <doc_using_fonts_msdf>`.

TextMesh
--------

.. image:: img/text_mesh.png

Resource TextMesh có một số điểm tương đồng với Label3D. Cả hai đều hiển thị văn bản trong scene 3D và sử dụng cùng font subresource. Tuy nhiên, thay vì tạo các quad trong suốt, TextMesh tạo hình học 3D biểu diễn đường viền của các glyph và có các thuộc tính của một mesh. Vì vậy, TextMesh được chiếu sáng theo mặc định và tự động đổ bóng lên môi trường. TextMesh cũng có thể được áp dụng material (bao gồm cả custom shader).

Dưới đây là một ví dụ về texture và cách áp dụng texture đó lên mesh. Bạn có thể sử dụng texture bên dưới làm tham chiếu cho UV map của mesh được tạo:

.. image:: img/text_mesh_texture.png

.. image:: img/text_mesh_textured.png

Ưu điểm
~~~~~~~

TextMesh có một số ưu điểm so với Label3D:

- TextMesh có thể sử dụng texture để thay đổi màu văn bản theo từng mặt.
- Hình học TextMesh có thể có độ sâu thực, tạo cho các glyph diện mạo 3D.
- TextMesh có thể sử dụng custom shader, không giống Label3D.

Hạn chế
~~~~~~~

TextMesh có một số hạn chế:

- Không tích hợp hỗ trợ đường viền, không giống Label3D. Tuy nhiên, có thể mô phỏng tính năng này bằng custom shader.
- Chỉ hỗ trợ dynamic font (``.ttf``, ``.otf``, ``.woff``, ``.woff2``). Bitmap font ở các định dạng ``.fnt`` hoặc ``.font`` **không** được hỗ trợ.
- Font có đường viền tự giao nhau sẽ không được render chính xác. Nếu nhận thấy vấn đề render với các font tải xuống từ những website như Google Fonts, hãy thử tải font từ website chính thức của tác giả font.
- Để khử răng cưa khi render văn bản, cần bật một phương pháp khử răng cưa toàn scene như MSAA, FXAA và temporal antialiasing (TAA). Nếu không bật phương pháp khử răng cưa nào, văn bản sẽ có vẻ nhiễu hạt, đặc biệt khi nhìn từ xa. Xem :ref:`doc_3d_antialiasing` để biết thêm thông tin.

Node Label được chiếu (hoặc bất kỳ Control nào khác)
----------------------------------------------------

Có một giải pháp cuối cùng phức tạp hơn khi thiết lập nhưng linh hoạt nhất: chiếu một node 2D vào không gian 3D. Có thể thực hiện việc này bằng giá trị trả về của phương thức :ref:`unproject_position<class_Camera3D_method_unproject_position>` trên node Camera3D trong hàm ``_process()`` của script. Sau đó, dùng giá trị trả về này để đặt thuộc tính ``position`` của một node Control.

Xem demo `3D waypoints <https://github.com/godotengine/godot-demo-projects/tree/master/3d/waypoints>`__ để biết ví dụ về cách này.

Ưu điểm
~~~~~~~

- Có thể sử dụng bất kỳ node Control nào, bao gồm Label, RichTextLabel hoặc thậm chí các node như Button. Điều này cho phép định dạng mạnh mẽ và tương tác GUI.
- Cách tiếp cận dựa trên script cho phép tự do hoàn toàn trong việc định vị. Ví dụ, cách này giúp ghim Control vào các cạnh màn hình dễ dàng hơn đáng kể khi chúng đi ra ngoài màn hình (dùng cho các marker 3D trong game).
- Tuân theo Control theming. Điều này giúp tùy chỉnh dễ dàng hơn và áp dụng trên toàn project.

Hạn chế
~~~~~~~

- Projected Control không thể bị che bởi hình học 3D theo bất kỳ cách nào. Bạn có thể dùng RayCast để ẩn hoàn toàn control nếu vị trí đích của nó bị collider che khuất, nhưng cách này không cho phép ẩn một phần control phía sau tường.
- Có thể thay đổi kích thước văn bản tùy theo khoảng cách bằng cách điều chỉnh thuộc tính ``scale`` của Control, nhưng cần thực hiện thủ công. Label3D và TextMesh tự động xử lý việc này, đổi lại là độ linh hoạt thấp hơn (không thể đặt kích thước văn bản tối thiểu/tối đa theo pixel).
- Script phải xử lý việc thay đổi resolution và aspect ratio, điều này có thể khó khăn.

Nên sử dụng Label3D, TextMesh hay một Control được chiếu?
---------------------------------------------------------

Trong hầu hết các trường hợp, bạn nên dùng Label3D vì nó dễ thiết lập hơn và cho chất lượng kết xuất cao hơn (đặc biệt khi tính năng khử răng cưa 3D bị tắt).

Đối với các trường hợp sử dụng nâng cao, TextMesh linh hoạt hơn vì cho phép tạo kiểu cho văn bản bằng custom shader. Custom shader cho phép sửa đổi hình học cuối cùng, chẳng hạn như uốn cong văn bản theo một bề mặt. Vì văn bản thực sự là hình học 3D, bạn có thể tùy chọn tạo chiều sâu cho văn bản và cũng có thể để văn bản đóng góp vào global illumination.

Nếu cần các tính năng như hỗ trợ BBCode hoặc theming của Control, thì sử dụng node RichTextLabel được chiếu là lựa chọn duy nhất.
