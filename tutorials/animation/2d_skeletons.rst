:article_outdated: True

.. _doc_2d_skeletons:

Skeleton 2D
===========

Giới thiệu
----------

Khi làm việc với 3D, biến dạng bằng skeleton rất phổ biến đối với nhân vật và sinh vật, và hầu hết các ứng dụng modeling 3D đều hỗ trợ tính năng này. Với 2D, vì chức năng này không được sử dụng thường xuyên, nên rất khó tìm được phần mềm phổ biến hướng đến mục đích này.

Một lựa chọn là tạo animation trong phần mềm bên thứ ba như Spine hoặc Dragonbones. Chức năng này cũng được tích hợp sẵn.

Tại sao bạn lại muốn thực hiện skeletal animation trực tiếp trong Godot? Câu trả lời là tính năng này có nhiều ưu điểm:

* Tích hợp tốt hơn với engine, nhờ đó việc import và chỉnh sửa từ một công cụ bên ngoài sẽ bớt rắc rối hơn. * Khả năng điều khiển particle system, shader, âm thanh, gọi script, màu sắc, độ trong suốt, v.v. trong animation. * Hệ thống skeleton tích hợp sẵn trong Godot rất hiệu quả và được thiết kế để đạt hiệu năng cao.

Vì vậy, tutorial sau đây sẽ giải thích về các biến dạng bằng skeleton trong 2D.

Thiết lập
---------

.. seealso::

   Trước khi bắt đầu, chúng tôi khuyên bạn nên xem qua
   :ref:`doc_cutout_animation` tutorial to gain a general understanding of
   tạo animation trong Godot.

Trong tutorial này, chúng ta sẽ sử dụng một hình ảnh duy nhất để tạo nhân vật. Hãy tải hình ảnh từ :download:`gBot_pieces.png <img/gBot_pieces.png>` hoặc lưu hình ảnh bên dưới.

.. image:: img/gBot_pieces.png

Bạn cũng nên tải xuống hình ảnh nhân vật hoàn chỉnh
:download:`gBot_complete.png <img/gBot_complete.png>` to have a good reference
để ghép các mảnh khác nhau lại với nhau.

.. image:: img/gBot_complete.png

Tạo polygon
-----------

Tạo một scene mới cho model của bạn (nếu đó sẽ là một nhân vật được animate, bạn có thể muốn sử dụng một ``CharacterBody2D``). Để dễ sử dụng, một node 2D trống được tạo làm root cho các polygon.

Bắt đầu với một node ``Polygon2D``. Hiện tại không cần đặt nó ở đâu trong scene, vì vậy chỉ cần tạo node như sau:

.. image:: img/skel2d1.png

Chọn node đó và gán texture chứa các mảnh của nhân vật mà bạn đã tải xuống trước đó:

.. image:: img/skel2d2.png

Không nên vẽ polygon trực tiếp. Thay vào đó, hãy mở hộp thoại "UV" cho polygon:

.. image:: img/skel2d3.png

Chuyển sang chế độ *Points*, chọn bút chì và vẽ một polygon quanh mảnh mong muốn:

.. image:: img/skel2d4.png

Nhân bản polygon node và đặt cho nó một tên phù hợp. Sau đó, mở lại hộp thoại "UV" và thay polygon cũ bằng một polygon khác trong mảnh mong muốn mới.

Khi bạn nhân bản các node và mảnh tiếp theo có hình dạng tương tự, bạn có thể chỉnh sửa polygon trước đó thay vì vẽ một polygon mới.

Sau khi di chuyển polygon, hãy nhớ cập nhật UV bằng cách chọn **Edit > Copy Polygon to UV** trong Polygon 2D UV Editor.

.. image:: img/skel2d5.png

Tiếp tục thực hiện như vậy cho đến khi bạn map xong tất cả các mảnh.

.. image:: img/skel2d6.png

Bạn sẽ nhận thấy các mảnh của node xuất hiện theo cùng bố cục như trong texture gốc. Đó là vì theo mặc định, khi bạn vẽ một polygon, UV và các điểm có cùng vị trí.

Sắp xếp lại các mảnh và tạo nhân vật. Việc này sẽ khá nhanh. Không cần thay đổi pivot, vì vậy đừng mất công đảm bảo rằng các rotation pivot của từng mảnh đều chính xác; hiện tại bạn có thể giữ nguyên chúng.

.. image:: img/skel2d7.png

Ồ, thứ tự hiển thị của các mảnh vẫn chưa đúng, vì một số mảnh đang che nhầm mảnh khác. Hãy sắp xếp lại thứ tự của các node để sửa lỗi này:

.. image:: img/skel2d8.png

Vậy là xong! Cách này chắc chắn dễ hơn nhiều so với tutorial về cutout.

Tạo skeleton
------------

Tạo một node ``Skeleton2D`` làm node con của root node. Đây sẽ là phần gốc của skeleton:

.. image:: img/skel2d9.png

Tạo một node ``Bone2D`` làm node con của skeleton. Đặt nó ở hông (skeleton thường bắt đầu từ đây). Bone sẽ hướng sang phải, nhưng hiện tại bạn có thể bỏ qua điều này.

.. image:: img/skel2d10.png

Tiếp tục tạo các bone theo dạng hierarchy và đặt tên tương ứng.

.. image:: img/skel2d11.png

Ở cuối chuỗi này sẽ có một node *jaw*. Một lần nữa, node này rất ngắn và hướng sang phải. Đây là điều bình thường đối với các bone không có node con. Độ dài của các bone *tip* có thể được thay đổi bằng một property trong inspector:

.. image:: img/skel2d12.png

Trong trường hợp này, chúng ta không cần xoay bone (tình cờ là jaw trong sprite đã hướng sang phải), nhưng nếu cần thì bạn cứ tự nhiên xoay nó. Một lần nữa, điều này thực sự chỉ cần thiết đối với các bone tip, vì các node có node con thường không cần độ dài hoặc rotation cụ thể.

Tiếp tục và tạo toàn bộ skeleton:

.. image:: img/skel2d13.png

Bạn sẽ nhận thấy tất cả các bone đều cảnh báo về việc thiếu rest pose. Rest pose là pose mặc định của một skeleton; bạn có thể quay lại pose này bất cứ lúc nào (rất tiện khi tạo animation). Để thiết lập rest pose, hãy nhấp vào node *skeleton* trong scene tree, sau đó nhấp vào nút :button:`Skeleton2D` trên toolbar và chọn ``Overwrite Rest Pose`` từ menu dropdown.

.. image:: img/skel2d14.webp

Các cảnh báo sẽ biến mất. Nếu bạn chỉnh sửa skeleton (thêm/xóa bone), bạn sẽ cần thiết lập lại rest pose.

Biến dạng polygon
-----------------

Chọn các polygon đã tạo trước đó và gán skeleton node vào property ``Skeleton`` của chúng. Điều này sẽ đảm bảo rằng sau này chúng có thể được biến dạng bởi skeleton.

.. image:: img/skel2d15.png

Nhấp vào property được đánh dấu ở trên và chọn skeleton node:

.. image:: img/skel2d16.png

Một lần nữa, hãy mở UV editor cho polygon và chuyển đến phần *Bones*.

.. image:: img/skel2d17.png

Bạn chưa thể paint weight. Để làm việc này, bạn cần đồng bộ danh sách bone từ skeleton với polygon. Bước này chỉ được thực hiện một lần và thủ công (trừ khi bạn chỉnh sửa skeleton bằng cách thêm/xóa/đổi tên bone). Bước này đảm bảo thông tin rigging của bạn được lưu trong polygon, ngay cả khi một skeleton node vô tình bị mất hoặc skeleton bị chỉnh sửa. Nhấn nút "Sync Bones to Polygon" để đồng bộ danh sách.

.. image:: img/skel2d18.png

Danh sách bone sẽ tự động xuất hiện. Theo mặc định, polygon của bạn chưa được gán weight cho bất kỳ bone nào. Chọn các bone mà bạn muốn gán weight rồi paint chúng:

.. image:: img/skel2d19.png

Các điểm màu trắng được gán weight đầy đủ, trong khi các điểm màu đen không chịu ảnh hưởng của bone. Nếu cùng một điểm được paint màu trắng cho nhiều bone, ảnh hưởng sẽ được phân bổ giữa các bone đó (vì vậy thường không cần dùng các sắc độ trung gian, trừ khi bạn muốn tinh chỉnh hiệu ứng uốn cong).

.. image:: img/skel2d20.gif

Sau khi paint weight, việc animate các bone (KHÔNG phải các polygon!) sẽ tạo ra hiệu ứng mong muốn, làm thay đổi và uốn cong các polygon tương ứng. Vì với cách tiếp cận này bạn chỉ cần animate các bone, công việc sẽ dễ dàng hơn nhiều!

Nhưng mọi chuyện không phải lúc nào cũng thuận lợi. Việc cố gắng animate các bone làm uốn cong polygon thường cho ra kết quả không như mong đợi:

.. image:: img/skel2d21.gif

Điều này xảy ra vì Godot tạo ra các tam giác bên trong để nối các điểm khi vẽ polygon. Chúng không phải lúc nào cũng uốn cong theo cách bạn mong đợi. Để giải quyết vấn đề này, bạn cần thiết lập các hint trong geometry nhằm chỉ rõ cách bạn muốn nó biến dạng.

Các vertex bên trong
--------------------

Mở lại menu UV cho từng bone và chuyển đến phần *Points*. Thêm một số vertex bên trong tại các vùng mà bạn mong geometry sẽ uốn cong:

.. image:: img/skel2d22.png

Bây giờ, hãy chuyển đến phần *Polygon* và vẽ lại các polygon của riêng bạn với nhiều chi tiết hơn. Hãy hình dung rằng khi polygon uốn cong, bạn cần đảm bảo chúng biến dạng ít nhất có thể, vì vậy hãy thử nghiệm một chút để tìm ra thiết lập phù hợp.

.. image:: img/skel2d23.png

Khi bắt đầu vẽ, polygon gốc sẽ biến mất và bạn có thể tự do tạo polygon của riêng mình:

.. image:: img/skel2d24.png

Mức độ chi tiết này thường là đủ, mặc dù bạn có thể muốn kiểm soát chi tiết hơn vị trí của các tam giác. Hãy tự thử nghiệm cho đến khi đạt được kết quả ưng ý.

**Lưu ý:** Đừng quên rằng các vertex bên trong mới được thêm vào cũng cần được paint weight! Hãy quay lại phần *Bones* để gán chúng cho đúng bone.

Sau khi hoàn tất, bạn sẽ có kết quả tốt hơn nhiều:

.. image:: img/skel2d25.gif
