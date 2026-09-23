.. _doc_animation_tree:

Sử dụng AnimationTree
=====================

Giới thiệu
----------

Với :ref:`AnimationPlayer <class_AnimationPlayer>`, Godot có một trong những hệ thống animation linh hoạt nhất mà bạn có thể tìm thấy ở bất kỳ game engine nào. Hệ thống này gần như độc nhất ở khả năng tạo animation cho hầu hết mọi thuộc tính trong bất kỳ node hoặc resource nào, cùng các track transform, bezier, gọi hàm, audio và sub-animation chuyên dụng.

Tuy nhiên, khả năng blend các animation đó thông qua ``AnimationPlayer`` còn hạn chế, vì bạn chỉ có thể đặt một khoảng thời gian chuyển tiếp cross-fade cố định.

:ref:`AnimationTree <class_AnimationTree>` là một node được thiết kế để xử lý các chuyển tiếp nâng cao.

AnimationTree và AnimationPlayer
--------------------------------

Trước khi bắt đầu, hãy lưu ý rằng node ``AnimationTree`` không chứa các animation riêng. Thay vào đó, nó sử dụng các animation được chứa trong node ``AnimationPlayer``. Bạn tạo, chỉnh sửa hoặc import animation trong một ``AnimationPlayer``, sau đó dùng ``AnimationTree`` để điều khiển việc phát.

``AnimationPlayer`` và ``AnimationTree`` có thể được sử dụng trong cả scene 2D và 3D. Khi import các scene 3D cùng animation của chúng, bạn có thể sử dụng `name suffixes <https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/node_type_customization.html#animation-loop-loop-cycle>`_ để đơn giản hóa quy trình và import với các thuộc tính chính xác. Cuối cùng, scene Godot được import sẽ chứa các animation trong một node ``AnimationPlayer``. Vì bạn hiếm khi sử dụng trực tiếp các scene đã import trong Godot (chúng либо được instantiate hoặc kế thừa), bạn có thể đặt node ``AnimationTree`` vào scene mới chứa scene đã import. Sau đó, trỏ node ``AnimationTree`` đến ``AnimationPlayer`` được tạo trong scene đã import.

Sau đây là cách thực hiện trong `Third Person Shooter demo <https://godotengine.org/asset-library/asset/2710>`_, để bạn tham khảo:

.. image:: img/animtree_treeandplayersetup.png

Một scene mới được tạo cho player với ``CharacterBody3D`` làm root. Bên trong scene này, file ``.dae`` (Collada) ban đầu được instantiate và một node ``AnimationTree`` được tạo.

Tạo một cây
-----------

Để sử dụng ``AnimationTree``, bạn phải đặt một root node. Root node của animation là một class chứa và đánh giá các sub-node rồi xuất ra một animation. Có 3 loại sub-node:

1. Animation node, tham chiếu đến một animation từ ``AnimationPlayer`` được liên kết.
2. Animation Root node, được dùng để blend các sub-node và có thể được lồng nhau.
3. Animation Blend node, được sử dụng trong một ``AnimationNodeBlendTree``, một graph node 2D. Blend node nhận nhiều input port và cung cấp một output port.

Có một số loại root node:

.. image:: img/animtree_rootnodes.png

* ``AnimationNodeAnimation``: Chọn một animation từ danh sách và phát animation đó. Đây là root node đơn giản nhất và thường không được dùng làm root.
* ``AnimationNodeBlendTree``: Chứa nhiều node con trong một graph. Có nhiều blend node, chẳng hạn như mix, blend2, blend3, one shot, v.v.
* ``AnimationNodeBlendSpace1D``: Cho phép blend tuyến tính giữa hai animation node. Điều khiển vị trí blend trong blend space 1D để trộn giữa các animation.
* ``AnimationNodeBlendSpace2D``: Cho phép blend tuyến tính giữa ba animation node. Điều khiển vị trí blend trong blend space 2D để trộn giữa các animation.
* ``AnimationNodeStateMachine``: Chứa nhiều node con trong một graph. Mỗi node được sử dụng như một state, với nhiều hàm dùng để chuyển đổi giữa các state.

Blend tree
----------

Khi tạo một ``AnimationNodeBlendTree``, bạn sẽ nhận được một graph 2D trống ở panel dưới, bên dưới tab AnimationTree. Theo mặc định, graph chỉ chứa một node ``Output``.

.. image:: img/animtree_emptyblendtree.webp

Để animation phát, một node phải được kết nối với output. Bạn có thể thêm node từ menu **Add Node..** hoặc nhấp chuột phải vào vùng trống:

.. image:: img/animtree_blendnodes.webp

Kết nối đơn giản nhất là kết nối trực tiếp một node ``Animation`` với output, khi đó animation sẽ chỉ được phát.

.. image:: img/animtree_animtooutput.png

Sau đây là mô tả về các node khả dụng khác:

Blend2 / Blend3
~~~~~~~~~~~~~~~

Các node này sẽ blend giữa hai hoặc ba input bằng một giá trị blend do người dùng chỉ định:

.. image:: img/animtree_blend2.gif

Blending có thể sử dụng **filters** để kiểm soát riêng track nào được blend và track nào không. Điều này hữu ích khi xếp chồng các animation lên nhau.

.. image:: img/animtree_filtering.png

Đối với blending phức tạp hơn, bạn nên sử dụng blend space.

OneShot
~~~~~~~

Node này sẽ thực thi một animation một lần rồi trả về khi animation kết thúc. Bạn có thể tùy chỉnh thời gian blend khi fade in và fade out, cũng như các filter.

.. image:: img/animtree_oneshot.gif

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phát animation con được kết nối với port "shot".
    animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE

    # Hủy animation con được kết nối với port "shot".
    animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT

    # Lấy trạng thái hiện tại (chỉ đọc).
    animation_tree.get("parameters/OneShot/active"))
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/OneShot/active"]

 .. code-tab:: csharp

    // Phát animation con được kết nối với port "shot".
    animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Fire);

    // Hủy animation con được kết nối với port "shot".
    animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Abort);

    // Lấy trạng thái hiện tại (chỉ đọc).
    animationTree.Get("parameters/OneShot/active");

TimeSeek
~~~~~~~~

Node này cho phép bạn seek đến một thời điểm trong animation được kết nối với input `in` của nó. Sử dụng node này để phát một ``Animation`` bắt đầu từ một vị trí phát nhất định. Lưu ý rằng giá trị seek request được đo bằng giây, vì vậy nếu muốn phát animation từ đầu, hãy đặt giá trị là ``0.0``, hoặc nếu muốn phát animation từ giây thứ 3, hãy đặt giá trị là ``3.0``.

.. image:: img/animtree_timeseek.webp

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phát animation con từ đầu.
    animation_tree.set("parameters/TimeSeek/seek_request", 0.0)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/TimeSeek/seek_request"] = 0.0

    # Phát animation con từ mốc thời gian 12 giây.
    animation_tree.set("parameters/TimeSeek/seek_request", 12.0)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/TimeSeek/seek_request"] = 12.0

 .. code-tab:: csharp

    // Phát animation con từ đầu.
    animationTree.Set("parameters/TimeSeek/seek_request", 0.0);

    // Phát animation con từ mốc thời gian 12 giây.
    animationTree.Set("parameters/TimeSeek/seek_request", 12.0);

TimeScale
~~~~~~~~~

Node này cho phép bạn điều chỉnh tốc độ của animation được kết nối với đầu vào `in`. Tốc độ của animation sẽ được nhân với số trong tham số `scale`. Đặt scale thành 0 sẽ tạm dừng animation. Đặt scale thành một số âm sẽ phát animation ngược lại.

.. image:: img/animtree_timescale.webp

Transition
~~~~~~~~~~

Node này là một phiên bản đơn giản hóa của StateMachine. Bạn kết nối các animation với các đầu vào, và chỉ số trạng thái hiện tại sẽ xác định animation nào được phát. Bạn có thể chỉ định thời gian crossfade. Trong Inspector, bạn có thể thay đổi số lượng cổng đầu vào, sắp xếp lại các đầu vào hoặc xóa các đầu vào.

.. image:: img/animtree_transition.webp

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phát animation con được kết nối với cổng "state_2".
    animation_tree.set("parameters/Transition/transition_request", "state_2")
    # Cú pháp thay thế (kết quả tương tự).
    animation_tree["parameters/Transition/transition_request"] = "state_2"

    # Lấy tên trạng thái hiện tại (chỉ đọc).
    animation_tree.get("parameters/Transition/current_state")
    # Cú pháp thay thế (kết quả tương tự).
    animation_tree["parameters/Transition/current_state"]

    # Lấy chỉ số trạng thái hiện tại (chỉ đọc).
    animation_tree.get("parameters/Transition/current_index"))
    # Cú pháp thay thế (kết quả tương tự).
    animation_tree["parameters/Transition/current_index"]

 .. code-tab:: csharp

    // Phát animation con được kết nối với cổng "state_2".
    animationTree.Set("parameters/Transition/transition_request", "state_2");

    // Lấy tên trạng thái hiện tại (chỉ đọc).
    animationTree.Get("parameters/Transition/current_state");

    // Lấy chỉ số trạng thái hiện tại (chỉ đọc).
    animationTree.Get("parameters/Transition/current_index");


StateMachine
~~~~~~~~~~~~

Khi tạo một ``AnimationNodeStateMachine``, bạn sẽ nhận được một đồ thị 2D trống trong bảng điều khiển phía dưới, bên dưới tab AnimationTree. Theo mặc định, đồ thị này chứa một trạng thái ``Start`` và ``End``.

.. image:: img/animtree_emptystatemachine.webp

Để thêm trạng thái, hãy nhấp chuột phải hoặc sử dụng nút **create new nodes**, có biểu tượng dấu cộng trong một hình hộp. Bạn có thể thêm animation, blendspace, blendtree hoặc thậm chí một StateMachine khác. Để chỉnh sửa một trong các sub-node phức tạp hơn này, hãy nhấp vào biểu tượng bút chì ở bên phải trạng thái. Để quay lại StateMachine ban đầu, hãy nhấp vào **Root** ở góc trên bên trái của bảng điều khiển.

Trước khi StateMachine có thể thực hiện điều gì đó hữu ích, các trạng thái phải được kết nối bằng các transition. Để thêm một transition, hãy nhấp vào nút **connect nodes**, có biểu tượng là một đường thẳng với mũi tên hướng sang phải, rồi kéo giữa hai trạng thái. Bạn có thể tạo 2 transition giữa các trạng thái, mỗi transition theo một hướng.

.. image:: img/animtree_connections.gif

Có 3 loại transition:

.. image:: img/animtree_transitiontypes.png

* *Immediate*: Chuyển sang trạng thái tiếp theo ngay lập tức.
* *Sync*: Chuyển sang trạng thái tiếp theo ngay lập tức, nhưng đưa trạng thái mới đến vị trí phát lại của trạng thái cũ.
* *At End*: Chờ đến khi việc phát trạng thái hiện tại kết thúc, sau đó chuyển đến đầu animation của trạng thái tiếp theo.

Transition cũng có một số thuộc tính. Hãy nhấp vào một transition, thuộc tính của transition sẽ được hiển thị trong inspector:

.. image:: img/animtree_statemachinetransitionproperties.webp

* *Xfade Time* là thời gian cross-fade giữa trạng thái này và trạng thái tiếp theo.
* *Xfade Curve* là kiểu cross-fade theo một đường cong thay vì blend tuyến tính.
* *Reset* xác định liệu trạng thái mà bạn chuyển đến có phát từ đầu (true) hay không (false).
* *Priority* được sử dụng cùng với hàm ``travel()`` trong code (sẽ nói thêm về điều này sau). Các transition có độ ưu tiên thấp hơn sẽ được ưu tiên khi di chuyển qua cây.
* *Switch Mode* là loại transition (xem ở trên). Bạn có thể thay đổi loại này sau khi tạo tại đây.
* *Advance Mode* xác định chế độ chuyển tiếp. Nếu là ``Disabled``, transition sẽ không được sử dụng. Nếu là ``Enabled``, transition chỉ được sử dụng trong ``travel()``. Nếu là ``Auto``, transition sẽ được sử dụng khi điều kiện và biểu thức chuyển tiếp là true, hoặc khi không có điều kiện/biểu thức chuyển tiếp.

Advance Condition and Advance Expression
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2 thuộc tính cuối cùng trong một transition của StateMachine là ``Advance Condition`` và ``Advance Expression.``. Khi Advance Mode được đặt thành *Auto*, các thuộc tính này xác định transition có chuyển tiếp hay không.

Advance Condition là một phép kiểm tra true/false. Bạn có thể nhập tên biến tùy chỉnh vào trường văn bản; khi StateMachine đến transition này, nó sẽ kiểm tra xem biến của bạn có phải là *true* hay không. Nếu đúng, transition sẽ tiếp tục. Lưu ý rằng Advance Condition **chỉ** kiểm tra xem một biến có phải là *true* hay không và không thể kiểm tra giá trị false.

Điều này khiến Advance Condition có khả năng rất hạn chế. Nếu muốn tạo một transition qua lại dựa trên một thuộc tính, bạn sẽ cần tạo 2 biến có giá trị đối lập và kiểm tra xem một trong hai biến có true hay không. Đây là lý do Advance Expression được thêm vào Godot 4.

Advance Expression hoạt động tương tự Advance Condition, nhưng thay vì kiểm tra xem một biến có true hay không, nó đánh giá bất kỳ expression nào. Expression là bất kỳ thứ gì bạn có thể đặt trong một câu lệnh ``if``. Sau đây là các ví dụ về expression có thể hoạt động trong Advance Expression:

* ``is_walking``
* ``is_walking == true`` (hoạt động giống như ví dụ ở trên)
* ``is_walking && !is_idle``
* ``velocity > 0``
* ``player.is_on_floor()``

.. warning::

      Expression **phân biệt chữ hoa chữ thường**. Nếu tham chiếu đến các thuộc tính của engine, chẳng hạn như ``velocity`` trên một node :ref:`class_CharacterBody3D`, bạn nên sử dụng quy ước đặt tên ``snake_case``. Nếu tham chiếu đến các thuộc tính của script, bạn nên tuân theo phong cách được sử dụng trong script, thường là ``snake_case`` trong GDScript và ``PascalCase`` trong C#.

Sau đây là ví dụ về một transition của StateMachine được thiết lập không đúng bằng Advance Condition:

.. image:: img/animtree_badanimcondition.webp
.. image:: img/animtree_badanimcondition.gif

Ví dụ này không hoạt động vì có một biến ``!`` trong Advance Condition, và biến đó không thể được kiểm tra.

Sau đây là cùng ví dụ đó, được thiết lập đúng cách bằng hai biến đối lập:

.. image:: img/animtree_goodanimcondition.webp
.. image:: img/animtree_goodanimcondition.gif

Sau đây là cùng ví dụ đó, nhưng sử dụng Advance Expression thay vì Advance Condition, nhờ đó không cần hai biến:

.. image:: img/animtree_goodanimexpression.webp
.. image:: img/animtree_goodanimexpression2.webp
.. image:: img/animtree_goodanimexpression.gif

Để sử dụng Advance Expression, phải thiết lập Advance Expression Base Node trong Inspector của node AnimationTree. Theo mặc định, nó được đặt thành chính node AnimationTree, nhưng cần trỏ đến node chứa script với các biến animation của bạn.

.. seealso::

   Advance Expression được đánh giá bằng class :ref:`class_expression` của Godot. Xem :ref:`doc_evaluating_expressions` để biết thêm thông tin về cách viết expression.

StateMachine travel
^^^^^^^^^^^^^^^^^^^

Một trong những tính năng thú vị của triển khai ``StateMachine`` trong Godot là khả năng di chuyển. Bạn có thể hướng dẫn graph đi từ trạng thái hiện tại đến một trạng thái khác, đồng thời đi qua tất cả các trạng thái trung gian. Việc này được thực hiện bằng thuật toán A\*. Nếu không có đường chuyển tiếp nào bắt đầu từ trạng thái hiện tại và kết thúc ở trạng thái đích, graph sẽ dịch chuyển tức thời đến trạng thái đích.

Để sử dụng khả năng di chuyển, trước tiên bạn nên lấy đối tượng :ref:`AnimationNodeStateMachinePlayback <class_AnimationNodeStateMachinePlayback>` từ node ``AnimationTree`` (đối tượng này được export dưới dạng một property), sau đó gọi một trong nhiều hàm của nó:

.. tabs::
 .. code-tab:: gdscript GDScript

    var state_machine = animation_tree["parameters/playback"]
    state_machine.travel("SomeState")

 .. code-tab:: csharp

    AnimationNodeStateMachinePlayback stateMachine = (AnimationNodeStateMachinePlayback)animationTree.Get("parameters/playback");
    stateMachine.Travel("SomeState");

StateMachine phải đang chạy trước khi bạn có thể di chuyển. Hãy đảm bảo bạn gọi ``start()`` hoặc kết nối một node với **Start**.

BlendSpace2D và BlendSpace1D
----------------------------

``BlendSpace2D`` là một node dùng để thực hiện blending nâng cao trong không gian hai chiều. Các điểm biểu diễn animation được thêm vào không gian 2D, sau đó một vị trí giữa chúng được điều khiển để xác định quá trình blending:

.. image:: img/animtree_blendspace2d.gif

Bạn có thể chèn các điểm này ở bất kỳ vị trí nào trên graph bằng cách nhấp chuột phải hoặc sử dụng nút **add point** trên toolbar. Khi được tạo, một điểm sẽ nhận tên từ animation hoặc loại :ref:`AnimationRootNode<class_AnimationRootNode>` đã chọn. Sau đó, bạn có thể đổi tên điểm bằng cách nhấp vào tên của điểm, hoặc định vị lại điểm bằng cách nhấp và kéo tên hoặc điểm đó. Nếu bật **Auto Triangles**, một tam giác blend giữa các điểm đã chèn sẽ được tự động tạo bằng `Delaunay triangulation <https://en.wikipedia.org/wiki/Delaunay_triangulation>`__.

.. image:: img/animtree_blendspacepoints.webp

Bạn có thể điều khiển blend target của animation trong node này bằng cách giữ Shift trong khi kéo bằng nút chuột trái trong editor, hoặc sử dụng công cụ chuyên dụng.

``BlendSpace1D`` hoạt động giống hệt ``BlendSpace2D``, nhưng trong một chiều duy nhất (một đường nằm ngang). Vì không sử dụng các tam giác, nó có thể hoạt động với ít hơn ba điểm blend.

.. image:: img/animtree_blendspace1d.webp

Chế độ đồng bộ
~~~~~~~~~~~~~~

Cả ``BlendSpace1D`` và ``BlendSpace2D`` đều có property **Sync Mode** để điều khiển cách các animation tiến triển khi được blend. Property này thay thế property boolean ``sync`` cũ và cung cấp khả năng kiểm soát chính xác hơn.

.. image:: img/animtree_syncmode_mutable.webp

Có bốn chế độ:

* **None** (mặc định): Các animation không hoạt động sẽ bị đóng băng và không tiến triển. Chỉ animation đang hoạt động (có weight cao nhất) tiếp tục tiến về phía trước.
* **Independent**: Các animation không hoạt động vẫn tiến triển với weight bằng ``0``. Chế độ này khớp với hành vi của thiết lập ``sync = true`` cũ.
* **Cyclic Mutable**: Tất cả animation được scale theo thời gian để các phase của chúng luôn đồng bộ. Độ dài cycle dùng chung được tính toán động dựa trên các blend weight đang hoạt động, nghĩa là một animation duy nhất không được blend sẽ phát ở tốc độ bình thường. Chế độ này hữu ích khi tất cả animation của bạn có cùng một cycle logic (ví dụ: các loop locomotion), nhưng có thể có độ dài hơi khác nhau.
* **Cyclic Constant**: Tất cả animation được scale theo thời gian để hoàn thành một cycle đầy đủ trong đúng **Cyclic Length** giây, bất kể độ dài riêng của chúng. Đặt property ``cyclic_length`` thành thời lượng cycle mong muốn (phải lớn hơn ``0``).

.. warning::

   Các chế độ đồng bộ cyclic yêu cầu tất cả điểm blend sử dụng :ref:`AnimationNodeAnimation <class_AnimationNodeAnimation>` với độ dài hữu hạn, bất biến. Nếu bất kỳ điểm blend nào sử dụng loại node khác, một cảnh báo sẽ hiển thị và đồng bộ cyclic sẽ không có hiệu lực:

   .. image:: img/animtree_syncmode_warning.webp

.. note::

   Khi sử dụng một trong hai chế độ cyclic với các animation có độ dài khác nhau, việc áp dụng một
   :ref:`AnimationNodeTimeSeek <class_AnimationNodeTimeSeek>` vào output sẽ phá vỡ sự đồng bộ. Trong trường hợp đó, hãy sử dụng :ref:`AnimationNodeAnimation.use_custom_timeline <class_AnimationNodeAnimation_property_use_custom_timeline>` để chuẩn hóa độ dài animation trước khi đồng bộ.

Chế độ blend
~~~~~~~~~~~~

Theo mặc định, blending diễn ra ở chế độ *Continuous*, bằng cách nội suy các điểm bên trong tam giác gần nhất trong ``BlendSpace2D``, hoặc trên đường thẳng giữa các điểm trong ``BlendSpace1D``. Tuy nhiên, đây không phải lúc nào cũng là lựa chọn tốt nhất. Ví dụ, khi làm việc với các animation 2D theo từng frame, bạn có thể muốn chuyển sang chế độ *Discrete*, trong đó các trạng thái trung gian của blend không xuất hiện trong kết quả. Ngoài ra, nếu muốn giữ nguyên vị trí phát hiện tại khi chuyển đổi giữa các animation discrete, chế độ *Carry* cho phép bạn thực hiện điều đó. Bạn có thể đặt các chế độ này bằng menu *Blend*.

.. image:: img/animtree_blendmode.webp

Để blending tốt hơn
-------------------

Để kết quả blending có tính xác định (có thể tái hiện và luôn nhất quán), các giá trị property được blend phải có một giá trị ban đầu cụ thể. Ví dụ, khi blend hai animation, nếu một animation có property track còn animation kia không có, animation được blend sẽ được tính như thể animation còn lại có một property track với giá trị ban đầu.

Khi sử dụng các track Position/Rotation/Scale 3D cho bone Skeleton3D, giá trị ban đầu là Bone Rest. Với các property khác, giá trị ban đầu là ``0``, và nếu track có trong animation ``RESET``, giá trị của keyframe đầu tiên của track sẽ được sử dụng thay thế.

Ví dụ sau đây, AnimationPlayer có hai animation, nhưng một animation không có Property track cho Position.

.. image:: img/blending1.webp

Điều này có nghĩa là animation thiếu track đó sẽ coi các Position đó là ``Vector2(0, 0)``.

.. image:: img/blending2.webp

Bạn có thể giải quyết vấn đề này bằng cách thêm một Property track cho Position làm giá trị ban đầu vào animation ``RESET``.

.. image:: img/blending3.webp

.. image:: img/blending4.webp

.. note:: Lưu ý rằng animation ``RESET`` tồn tại để xác định pose mặc định khi ban đầu tải một object. Animation này được giả định chỉ có một frame và không предназначено để phát bằng timeline.

Ngoài ra, hãy lưu ý rằng các track Rotation 3D và các Property track cho rotation 2D có Interpolation Type được đặt thành Linear Angle hoặc Cubic Angle sẽ ngăn rotation lớn hơn 180 độ so với giá trị ban đầu trong animation được blend.

Điều này có thể hữu ích cho Skeleton3D để ngăn các bone xuyên vào cơ thể khi blend animation. Do đó, các giá trị Bone Rest của Skeleton3D nên gần với trung điểm của phạm vi chuyển động nhất có thể. **Điều này có nghĩa là đối với các model hình người, tốt nhất nên import chúng ở tư thế chữ T**.

.. image:: img/blending5.webp

Bạn có thể thấy rằng đường xoay ngắn nhất từ các Bone Rest được ưu tiên thay vì đường xoay ngắn nhất giữa các animation.

Nếu cần xoay chính Skeleton3D hơn 180 độ bằng cách blend animation để tạo chuyển động, bạn có thể sử dụng Root Motion.

Root motion
-----------

Khi làm việc với animation 3D, một kỹ thuật phổ biến là animator sử dụng root bone của skeleton để tạo chuyển động cho phần còn lại của skeleton. Điều này cho phép tạo animation cho nhân vật theo cách mà bước chân thực sự khớp với mặt sàn bên dưới. Nó cũng cho phép tương tác chính xác với các object trong các cảnh cinematic.

Khi phát animation trong Godot, bạn có thể chọn bone này làm *root motion track*. Khi đó, phép biến đổi của bone sẽ bị hủy về mặt hiển thị (animation sẽ đứng yên tại chỗ).

.. image:: img/animtree_rootmotiontrack.webp

Sau đó, bạn có thể lấy chuyển động thực tế thông qua API :ref:`AnimationTree <class_AnimationTree>` dưới dạng một transform:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Lấy delta chuyển động.
    animation_tree.get_root_motion_position()
    animation_tree.get_root_motion_rotation()
    animation_tree.get_root_motion_scale()

    # Lấy giá trị thực tế sau khi blend của animation.
    animation_tree.get_root_motion_position_accumulator()
    animation_tree.get_root_motion_rotation_accumulator()
    animation_tree.get_root_motion_scale_accumulator()

 .. code-tab:: csharp

    // Lấy delta chuyển động.
    animationTree.GetRootMotionPosition();
    animationTree.GetRootMotionRotation();
    animationTree.GetRootMotionScale();

    // Lấy giá trị thực tế sau khi blend của animation.
    animationTree.GetRootMotionPositionAccumulator();
    animationTree.GetRootMotionRotationAccumulator();
    animationTree.GetRootMotionScaleAccumulator();

Bạn có thể truyền giá trị này vào các hàm như :ref:`CharacterBody3D.move_and_slide <class_CharacterBody3D_method_move_and_slide>` để điều khiển chuyển động của nhân vật.

Ngoài ra còn có một tool node, ``RootMotionView``, cho phép bạn đặt một scene đóng vai trò là sàn tùy chỉnh cho nhân vật và các animation (node này mặc định bị vô hiệu hóa trong khi game chạy).

.. image:: img/animtree15.gif

Điều khiển từ code
------------------

Sau khi xây dựng tree và xem trước, câu hỏi duy nhất còn lại là "Tất cả những điều này được điều khiển từ code như thế nào?".

Hãy nhớ rằng các animation node chỉ là resource, vì vậy chúng được chia sẻ giữa mọi instance sử dụng chúng. Việc thiết lập các giá trị trực tiếp trong node sẽ ảnh hưởng đến tất cả instance của scene sử dụng ``AnimationTree``. Điều này thường không mong muốn, nhưng cũng có một số trường hợp sử dụng thú vị; chẳng hạn, bạn có thể sao chép và dán các phần của animation tree, hoặc tái sử dụng các node có bố cục phức tạp (chẳng hạn như StateMachine hoặc blend space) trong các animation tree khác nhau.

Dữ liệu animation thực tế nằm trong node ``AnimationTree`` và được truy cập thông qua các property. Hãy xem phần "Parameters" của node ``AnimationTree`` để biết tất cả các parameter có thể được thay đổi theo thời gian thực:

.. image:: img/animtree_parameters.webp

Điều này rất hữu ích vì cho phép bạn animate chúng từ một ``AnimationPlayer``, hoặc thậm chí chính ``AnimationTree``, nhờ đó có thể xây dựng logic animation rất phức tạp.

Để sửa các giá trị này từ code, bạn phải lấy property path. Bạn có thể tìm thấy chúng bằng cách di chuột lên bất kỳ parameter nào:

.. image:: img/animtree_propertypath.webp

Sau đó, bạn có thể thiết lập hoặc đọc chúng:

.. tabs::
 .. code-tab:: gdscript GDScript

    animation_tree.set("parameters/eye_blend/blend_amount", 1.0)
    # Tiến hành các Expression từ một StateMachine (cú pháp thay thế, cùng kết quả)
    animation_tree["parameters/eye_blend/blend_amount"] = 1.0

 .. code-tab:: csharp

    animationTree.Set("parameters/eye_blend/blend_amount", 1.0);

.. note:: Advance Expressions từ một StateMachine sẽ không được tìm thấy trong các parameter. Đó là vì chúng được lưu trong một script khác thay vì chính AnimationTree. Advance `Conditions` sẽ được tìm thấy trong các parameter.

.. _`name suffixes`: https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/node_type_customization.html#animation-loop-loop-cycle
.. _`Third Person Shooter demo`: https://godotengine.org/asset-library/asset/2710
