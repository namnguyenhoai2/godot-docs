:article_outdated: Đúng

.. _doc_2d_skeletons:

Skeleton 2D
===========

Giới thiệu
----------

Khi làm việc với 3D, biến dạng bằng skeleton thường được dùng cho nhân vật và sinh vật, và hầu hết các ứng dụng modeling 3D đều hỗ trợ tính năng này. Với 2D, do chức năng này không được sử dụng thường xuyên, rất khó tìm thấy phần mềm phổ biến hướng đến mục đích này.

Một lựa chọn là tạo animation trong phần mềm bên thứ ba như Spine hoặc Dragonbones. Chức năng này cũng được hỗ trợ tích hợp sẵn.

Tại sao bạn muốn thực hiện animation bằng skeleton trực tiếp trong Godot? Câu trả lời là tính năng này có nhiều ưu điểm:

* Tích hợp tốt hơn với engine, giúp giảm phiền phức khi import và chỉnh sửa từ một công cụ bên ngoài.
* Có khả năng điều khiển particle system, shader, âm thanh, gọi script, màu sắc, độ trong suốt, v.v. trong animation.
* Hệ thống skeleton tích hợp sẵn trong Godot rất hiệu quả và được thiết kế để đạt hiệu năng cao.

Vì vậy, tutorial sau đây sẽ giải thích về biến dạng bằng skeleton 2D.

Thiết lập
---------

.. seealso::

   Trước khi bắt đầu, chúng tôi khuyên bạn nên xem qua
   :ref:`doc_cutout_animation` tutorial để có hiểu biết tổng quan về việc tạo animation trong Godot.

Trong tutorial này, chúng ta sẽ sử dụng một hình ảnh duy nhất để tạo nhân vật. Hãy tải xuống từ :download:`gBot_pieces.png <img/gBot_pieces.png>` hoặc lưu hình ảnh bên dưới.

.. image:: img/gBot_pieces.png

Bạn cũng nên tải xuống hình ảnh nhân vật hoàn chỉnh
:download:`gBot_complete.png <img/gBot_complete.png>` để có tài liệu tham khảo tốt khi ghép các mảnh khác nhau lại với nhau.

.. image:: img/gBot_complete.png

Tạo các polygon
---------------

Tạo một scene mới cho model của bạn (nếu đó là một nhân vật animated, bạn có thể muốn sử dụng một ``CharacterBody2D``). Để dễ sử dụng, một node 2D trống được tạo làm root cho các polygon.

Bắt đầu với một node ``Polygon2D``. Hiện tại không cần đặt nó ở vị trí nào trong scene, vì vậy chỉ cần tạo node như sau:

.. image:: img/skel2d1.png

Chọn node đó và gán texture chứa các mảnh nhân vật mà bạn đã tải xuống trước đó:

.. image:: img/skel2d2.png

Không nên vẽ polygon trực tiếp. Thay vào đó, hãy mở hộp thoại "UV" cho polygon:

.. image:: img/skel2d3.png

Chuyển sang chế độ *Points*, chọn bút chì và vẽ một polygon xung quanh mảnh mong muốn:

.. image:: img/skel2d4.png

Nhân bản polygon node và đặt cho nó một tên phù hợp. Sau đó, mở lại hộp thoại "UV" và thay polygon cũ bằng một polygon khác trong mảnh mới mong muốn.

Khi nhân bản các node và mảnh tiếp theo có hình dạng tương tự, bạn có thể chỉnh sửa polygon trước đó thay vì vẽ một polygon mới.

Sau khi di chuyển polygon, hãy nhớ cập nhật UV bằng cách chọn **Edit > Copy Polygon to UV** trong Polygon 2D UV Editor.

.. image:: img/skel2d5.png

Tiếp tục làm như vậy cho đến khi bạn ánh xạ tất cả các mảnh.

.. image:: img/skel2d6.png

Bạn sẽ nhận thấy các mảnh của các node xuất hiện theo cùng bố cục như trong texture gốc. Điều này là vì theo mặc định, khi bạn vẽ một polygon, UV và các điểm là giống nhau.

Sắp xếp lại các mảnh và tạo nhân vật. Việc này sẽ khá nhanh. Không cần thay đổi các pivot, vì vậy đừng bận tâm kiểm tra xem pivot xoay của từng mảnh đã đúng chưa; hiện tại bạn có thể giữ nguyên chúng.

.. image:: img/skel2d7.png

À, thứ tự hiển thị của các mảnh vẫn chưa đúng, vì một số mảnh đang che sai mảnh khác. Hãy sắp xếp lại thứ tự của các node để khắc phục điều này:

.. image:: img/skel2d8.png

Vậy là xong! Cách này chắc chắn dễ hơn nhiều so với tutorial về cutout.

Tạo skeleton
------------

Tạo một node ``Skeleton2D`` làm node con của root node. Đây sẽ là phần nền của skeleton:

.. image:: img/skel2d9.png

Tạo một node ``Bone2D`` làm node con của skeleton. Đặt nó ở hông (skeleton thường bắt đầu từ đây). Bone sẽ hướng sang phải, nhưng hiện tại bạn có thể bỏ qua điều này.

.. image:: img/skel2d10.png

Tiếp tục tạo các bone theo hệ phân cấp và đặt tên tương ứng.

.. image:: img/skel2d11.png

Ở cuối chuỗi này sẽ có một node *jaw*. Nó cũng rất ngắn và hướng sang phải. Đây là điều bình thường đối với các bone không có node con. Độ dài của các bone *tip* có thể được thay đổi bằng một property trong inspector:

.. image:: img/skel2d12.png

Trong trường hợp này, chúng ta không cần xoay bone (tình cờ là hàm của sprite cũng hướng sang phải), nhưng nếu cần, bạn cứ tự nhiên thực hiện. Một lần nữa, điều này thực sự chỉ cần thiết đối với các bone tip, vì các node có node con thường không cần độ dài hoặc góc xoay cụ thể.

Tiếp tục và tạo toàn bộ skeleton:

.. image:: img/skel2d13.png

Bạn sẽ nhận thấy tất cả các bone đều cảnh báo về việc thiếu rest pose. Rest pose là pose mặc định của skeleton, bạn có thể quay lại pose này bất cứ lúc nào (rất tiện cho việc tạo animation). Để thiết lập, hãy nhấp vào node *skeleton* trong scene tree, sau đó nhấp vào nút :button:`Skeleton2D` trên toolbar và chọn ``Overwrite Rest Pose`` từ menu thả xuống.

.. image:: img/skel2d14.webp

Các cảnh báo sẽ biến mất. Nếu bạn sửa đổi skeleton (thêm/xóa bone), bạn sẽ cần thiết lập lại rest pose.

Biến dạng các polygon
---------------------

Chọn các polygon đã tạo trước đó và gán skeleton node vào property ``Skeleton`` của chúng. Điều này sẽ đảm bảo rằng sau này chúng có thể được biến dạng bởi skeleton.

.. image:: img/skel2d15.png

Nhấp vào property được đánh dấu ở trên và chọn skeleton node:

.. image:: img/skel2d16.png

Một lần nữa, hãy mở UV editor cho polygon và chuyển đến phần *Bones*.

.. image:: img/skel2d17.png

Bạn chưa thể paint weight. Để làm việc này, bạn cần đồng bộ danh sách bone từ skeleton với polygon. Bước này chỉ được thực hiện một lần và thủ công (trừ khi bạn sửa đổi skeleton bằng cách thêm/xóa/đổi tên bone). Việc này đảm bảo thông tin rigging của bạn được lưu trong polygon, ngay cả khi một skeleton node vô tình bị mất hoặc skeleton bị sửa đổi. Nhấn nút "Sync Bones to Polygon" để đồng bộ danh sách.

.. image:: img/skel2d18.png

Danh sách bone sẽ tự động xuất hiện. Theo mặc định, polygon của bạn chưa được gán weight cho bone nào. Chọn các bone mà bạn muốn gán weight rồi paint chúng:

.. image:: img/skel2d19.png

Các điểm màu trắng được gán weight đầy đủ, trong khi các điểm màu đen không chịu ảnh hưởng của bone. Nếu cùng một điểm được paint màu trắng cho nhiều bone, ảnh hưởng sẽ được phân bổ giữa các bone đó (vì vậy thường không cần sử dụng các sắc độ trung gian, trừ khi bạn muốn tinh chỉnh hiệu ứng uốn cong).

.. image:: img/skel2d20.gif

Sau khi paint weight, việc tạo animation cho các bone (KHÔNG phải các polygon!) sẽ tạo ra hiệu ứng mong muốn là sửa đổi và uốn cong các polygon tương ứng. Vì trong cách tiếp cận này bạn chỉ cần tạo animation cho các bone nên công việc trở nên dễ dàng hơn nhiều!

Nhưng mọi chuyện không phải lúc nào cũng hoàn hảo. Việc cố gắng tạo animation cho các bone làm uốn cong polygon thường cho kết quả không mong đợi:

.. image:: img/skel2d21.gif

Điều này xảy ra vì Godot tạo các tam giác nội bộ để nối các điểm khi vẽ polygon. Chúng không phải lúc nào cũng uốn theo cách bạn mong đợi. Để khắc phục, bạn cần đặt các gợi ý trong hình học nhằm làm rõ cách bạn muốn nó biến dạng.

Đỉnh bên trong
--------------

Mở lại menu UV cho từng bone và đi đến mục *Points*. Thêm một số đỉnh bên trong vào các vùng mà bạn dự kiến hình học sẽ uốn:

.. image:: img/skel2d22.png

Bây giờ, đi đến mục *Polygon* và vẽ lại các polygon của riêng bạn với nhiều chi tiết hơn. Hãy hình dung rằng khi các polygon uốn, bạn cần đảm bảo chúng biến dạng ít nhất có thể, vì vậy hãy thử nghiệm một chút để tìm được thiết lập phù hợp.

.. image:: img/skel2d23.png

Khi bắt đầu vẽ, polygon ban đầu sẽ biến mất và bạn sẽ được tự do tạo polygon của riêng mình:

.. image:: img/skel2d24.png

Mức độ chi tiết này thường là đủ, mặc dù bạn có thể muốn kiểm soát chi tiết hơn vị trí của các tam giác. Hãy tự thử nghiệm cho đến khi đạt được kết quả ưng ý.

**Lưu ý:** Đừng quên rằng các đỉnh bên trong mới thêm cũng cần được tô trọng số! Hãy quay lại mục *Bones* để gán chúng cho đúng bone.

Sau khi hoàn tất, bạn sẽ có kết quả tốt hơn nhiều:

.. image:: img/skel2d25.gif
