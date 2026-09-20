.. _doc_animation_tree:

Sử dụng AnimationTree
=====================

Giới thiệu
----------

Với :ref:`AnimationPlayer <class_AnimationPlayer>`, Godot có một trong những hệ thống animation linh hoạt nhất mà bạn có thể tìm thấy ở bất kỳ game engine nào. Khả năng animate gần như mọi thuộc tính trong bất kỳ node hoặc resource nào, cùng các track transform, bezier, gọi hàm, audio và sub-animation chuyên dụng, khiến hệ thống này gần như độc nhất.

Tuy nhiên, khả năng blend các animation đó thông qua ``AnimationPlayer`` còn hạn chế, vì bạn chỉ có thể đặt một khoảng thời gian chuyển tiếp cross-fade cố định.

:ref:`AnimationTree <class_AnimationTree>` is a node designed to deal with advanced transitions.

AnimationTree và AnimationPlayer
--------------------------------

Trước khi bắt đầu, hãy biết rằng node ``AnimationTree`` không chứa animation riêng. Thay vào đó, nó sử dụng các animation được chứa trong node ``AnimationPlayer``. Bạn tạo, chỉnh sửa hoặc import animation trong một ``AnimationPlayer``, sau đó dùng một ``AnimationTree`` để điều khiển việc phát.

``AnimationPlayer`` và ``AnimationTree`` có thể được sử dụng trong cả scene 2D và 3D. Khi import scene 3D cùng các animation của chúng, bạn có thể dùng `name suffixes <https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/node_type_customization.html#animation-loop-loop-cycle>`_ để đơn giản hóa quy trình và import với các thuộc tính chính xác. Cuối cùng, scene Godot đã import sẽ chứa các animation trong một node ``AnimationPlayer``. Vì bạn hiếm khi sử dụng trực tiếp các scene đã import trong Godot (chúng thường được instantiate hoặc kế thừa), bạn có thể đặt node ``AnimationTree`` vào scene mới của mình, node này chứa scene đã import. Sau đó, trỏ node ``AnimationTree`` đến ``AnimationPlayer`` đã được tạo trong scene đã import.

Đây là cách thực hiện trong `Third Person Shooter demo <https://godotengine.org/asset-library/asset/2710>`_, để bạn tham khảo:

.. image:: img/animtree_treeandplayersetup.png

Một scene mới đã được tạo cho player với ``CharacterBody3D`` làm root. Bên trong scene này, file ``.dae`` (Collada) ban đầu được instantiate và một node ``AnimationTree`` được tạo.

Tạo một tree
------------

Để sử dụng ``AnimationTree``, bạn phải đặt một root node. Animation root node là một class chứa và đánh giá các sub-node rồi xuất ra một animation. Có 3 loại sub-node:

1. Animation node, tham chiếu đến một animation từ ``AnimationPlayer`` được liên kết. 2. Animation Root node, được dùng để blend các sub-node và có thể được lồng nhau. 3. Animation Blend node, được dùng trong một ``AnimationNodeBlendTree``, một graph node 2D. Blend node nhận nhiều input port và cung cấp một output port.

Có một số loại root node:

.. image:: img/animtree_rootnodes.png

* ``AnimationNodeAnimation``: Chọn một animation từ danh sách và phát animation đó. Đây là root node đơn giản nhất và thường không được dùng làm root. * ``AnimationNodeBlendTree``: Chứa nhiều node con trong một graph. Có nhiều blend node, chẳng hạn như mix, blend2, blend3, one shot, v.v. * ``AnimationNodeBlendSpace1D``: Cho phép blend tuyến tính giữa hai animation node. Điều khiển vị trí blend trong blend space 1D để trộn giữa các animation. * ``AnimationNodeBlendSpace2D``: Cho phép blend tuyến tính giữa ba animation node. Điều khiển vị trí blend trong blend space 2D để trộn giữa các animation. * ``AnimationNodeStateMachine``: Chứa nhiều node con trong một graph. Mỗi node được dùng như một state, với nhiều hàm được sử dụng để chuyển đổi giữa các state.

Blend tree
----------

Khi tạo một ``AnimationNodeBlendTree``, bạn sẽ nhận được một graph 2D trống trong bottom panel, bên dưới tab AnimationTree. Theo mặc định, graph chỉ chứa một node ``Output``.

.. image:: img/animtree_emptyblendtree.webp

Để animation phát, một node phải được kết nối với output. Bạn có thể thêm node từ menu **Add Node..** hoặc nhấp chuột phải vào một vùng trống:

.. image:: img/animtree_blendnodes.webp

Kết nối đơn giản nhất là kết nối trực tiếp một node ``Animation`` với output; node này sẽ chỉ phát animation.

.. image:: img/animtree_animtooutput.png

Sau đây là mô tả về các node khả dụng khác:

Blend2 / Blend3
~~~~~~~~~~~~~~~

Các node này sẽ blend giữa hai hoặc ba input bằng một giá trị blend do người dùng chỉ định:

.. image:: img/animtree_blend2.gif

Blending có thể sử dụng **filters** để kiểm soát riêng từng track nào được blend và track nào không. Điều này hữu ích khi xếp chồng các animation lên nhau.

.. image:: img/animtree_filtering.png

Đối với blending phức tạp hơn, bạn nên sử dụng blend space.

OneShot
~~~~~~~

Node này sẽ thực thi một animation một lần rồi kết thúc khi animation hoàn tất. Bạn có thể tùy chỉnh thời gian blend khi fade in và fade out, cũng như các filter.

.. image:: img/animtree_oneshot.gif

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phát child animation được kết nối với port "shot".
    animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE

    # Hủy child animation được kết nối với port "shot".
    animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT

    # Lấy state hiện tại (chỉ đọc).
    animation_tree.get("parameters/OneShot/active"))
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/OneShot/active"]

 .. code-tab:: csharp

    // Phát child animation được kết nối với port "shot".
    animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Fire);

    // Hủy child animation được kết nối với port "shot".
    animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Abort);

    // Lấy state hiện tại (chỉ đọc).
    animationTree.Get("parameters/OneShot/active");

TimeSeek
~~~~~~~~

Node này cho phép bạn seek đến một thời điểm trong animation được kết nối với input `in` của nó. Sử dụng node này để phát một ``Animation`` bắt đầu từ một vị trí phát nhất định. Lưu ý rằng giá trị seek request được tính bằng giây, vì vậy nếu muốn phát animation từ đầu, hãy đặt giá trị là ``0.0``, hoặc nếu muốn phát animation từ giây thứ 3, hãy đặt giá trị là ``3.0``.

.. image:: img/animtree_timeseek.webp

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phát child animation từ đầu.
    animation_tree.set("parameters/TimeSeek/seek_request", 0.0)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/TimeSeek/seek_request"] = 0.0

    # Phát child animation từ mốc thời gian 12 giây.
    animation_tree.set("parameters/TimeSeek/seek_request", 12.0)
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/TimeSeek/seek_request"] = 12.0

 .. code-tab:: csharp

    // Phát child animation từ đầu.
    animationTree.Set("parameters/TimeSeek/seek_request", 0.0);

    // Phát child animation từ mốc thời gian 12 giây.
    animationTree.Set("parameters/TimeSeek/seek_request", 12.0);

TimeScale
~~~~~~~~~

Node này cho phép bạn điều chỉnh tốc độ của animation được kết nối với input `in` của nó. Tốc độ animation sẽ được nhân với số trong tham số `scale`. Đặt scale bằng 0 sẽ tạm dừng animation. Đặt scale thành một số âm sẽ phát animation theo chiều ngược lại.

.. image:: img/animtree_timescale.webp

Transition
~~~~~~~~~~

Node này là một phiên bản đơn giản hóa của StateMachine. Bạn kết nối các animation với các input, và state index hiện tại sẽ quyết định animation nào được phát. Bạn có thể chỉ định thời gian chuyển tiếp crossfade. Trong Inspector, bạn có thể thay đổi số lượng input port, sắp xếp lại các input hoặc xóa input.

.. image:: img/animtree_transition.webp

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phát child animation được kết nối với port "state_2".
    animation_tree.set("parameters/Transition/transition_request", "state_2")
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/Transition/transition_request"] = "state_2"

    # Lấy tên state hiện tại (chỉ đọc).
    animation_tree.get("parameters/Transition/current_state")
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/Transition/current_state"]

    # Lấy state index hiện tại (chỉ đọc).
    animation_tree.get("parameters/Transition/current_index"))
    # Cú pháp thay thế (cùng kết quả).
    animation_tree["parameters/Transition/current_index"]

 .. code-tab:: csharp

    // Phát child animation được kết nối với port "state_2".
    animationTree.Set("parameters/Transition/transition_request", "state_2");

    // Lấy tên state hiện tại (chỉ đọc).
    animationTree.Get("parameters/Transition/current_state");

    // Lấy state index hiện tại (chỉ đọc).
    animationTree.Get("parameters/Transition/current_index");


StateMachine
~~~~~~~~~~~~

Khi tạo một ``AnimationNodeStateMachine``, bạn sẽ nhận được một graph 2D trống trong bottom panel, bên dưới tab AnimationTree. Theo mặc định, graph chứa một state ``Start`` và ``End``.

.. image:: img/animtree_emptystatemachine.webp

Để thêm state, hãy nhấp chuột phải hoặc sử dụng nút **create new nodes**, có biểu tượng dấu cộng trong một ô vuông. Bạn có thể thêm animation, blendspace, blendtree hoặc thậm chí một StateMachine khác. Để chỉnh sửa một trong các sub-node phức tạp hơn này, hãy nhấp vào biểu tượng bút chì ở bên phải state. Để quay lại StateMachine ban đầu, hãy nhấp vào **Root** ở phía trên bên trái của panel.

Trước khi StateMachine có thể thực hiện điều gì đó hữu ích, các state phải được kết nối bằng transition. Để thêm transition, hãy nhấp vào nút **connect nodes**, có biểu tượng một đường thẳng với mũi tên hướng sang phải, rồi kéo giữa hai state. Bạn có thể tạo 2 transition giữa các state, mỗi transition theo một hướng.

.. image:: img/animtree_connections.gif

Có 3 loại transition:

.. image:: img/animtree_transitiontypes.png

* *Immediate*: Chuyển sang state tiếp theo ngay lập tức. * *Sync*: Chuyển sang state tiếp theo ngay lập tức, nhưng seek state mới đến vị trí phát của state cũ. * *At End*: Chờ việc phát state hiện tại kết thúc, sau đó chuyển đến đầu animation của state tiếp theo.

Transition cũng có một số thuộc tính. Hãy nhấp vào một transition, thuộc tính của nó sẽ được hiển thị trong inspector:

.. image:: img/animtree_statemachinetransitionproperties.webp

* *Xfade Time* là thời gian cross-fade giữa state này và state tiếp theo. * *Xfade Curve* là cross-fade đi theo một curve thay vì blend tuyến tính. * *Reset* xác định state mà bạn chuyển vào có phát từ đầu hay không (true hoặc false). * *Priority* được sử dụng cùng với hàm ``travel()`` trong code (sẽ nói thêm về hàm này sau). Các transition có priority thấp hơn được ưu tiên khi di chuyển qua tree. * *Switch Mode* là loại transition (xem ở trên). Bạn có thể thay đổi loại này sau khi tạo tại đây. * *Advance Mode* xác định chế độ advance. Nếu là ``Disabled``, transition sẽ không được sử dụng. Nếu là ``Enabled``, transition chỉ được sử dụng trong ``travel()``. Nếu là ``Auto``, transition sẽ được sử dụng nếu advance condition và expression là true, hoặc nếu không có advance condition/expression.

Advance Condition và Advance Expression
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2 thuộc tính cuối cùng trong một transition của StateMachine là ``Advance Condition`` và ``Advance Expression.``. Khi Advance Mode được đặt thành *Auto*, chúng sẽ xác định transition có advance hay không.

Advance Condition là một phép kiểm tra true/false. Bạn có thể nhập tên biến tùy chỉnh vào trường văn bản; khi StateMachine đến transition này, nó sẽ kiểm tra xem biến của bạn có phải là *true* hay không. Nếu đúng, transition sẽ tiếp tục. Lưu ý rằng advance condition **chỉ** kiểm tra xem một biến có phải là *true* hay không và không thể kiểm tra giá trị false.

Điều này khiến Advance Condition chỉ có khả năng rất hạn chế. Nếu bạn muốn thực hiện chuyển tiếp qua lại dựa trên một thuộc tính, bạn sẽ cần tạo 2 biến có các giá trị đối lập nhau và kiểm tra xem một trong hai biến có giá trị true hay không. Đây là lý do trong Godot 4, Advance Expression đã được bổ sung.

Advance Expression hoạt động tương tự Advance Condition, nhưng thay vì kiểm tra xem một biến có giá trị true hay không, nó sẽ đánh giá bất kỳ expression nào. Expression là bất kỳ thứ gì bạn có thể đặt trong câu lệnh ``if``. Sau đây là một số ví dụ về expression có thể hoạt động trong Advance Expression:

* ``is_walking`` * ``is_walking == true`` (hoạt động giống như ví dụ bên trên) * ``is_walking && !is_idle`` * ``velocity > 0`` * ``player.is_on_floor()``

.. warning::

      Expression có phân biệt **chữ hoa chữ thường**. Nếu bạn tham chiếu đến các thuộc tính của engine, chẳng hạn như ``velocity`` trên node :ref:`class_CharacterBody3D`, bạn nên sử dụng quy ước đặt tên ``snake_case``. Nếu bạn tham chiếu đến các thuộc tính của script, hãy tuân theo kiểu được sử dụng trong script đó, thường là ``snake_case`` trong GDScript và ``PascalCase`` trong C#.

Sau đây là một ví dụ về transition StateMachine được thiết lập không đúng bằng Advance Condition:

.. image:: img/animtree_badanimcondition.webp
.. image:: img/animtree_badanimcondition.gif

Ví dụ này không hoạt động vì có một biến ``!`` trong Advance Condition, vốn không thể được kiểm tra.

Sau đây là cùng ví dụ đó, được thiết lập đúng cách bằng cách sử dụng hai biến đối lập nhau:

.. image:: img/animtree_goodanimcondition.webp
.. image:: img/animtree_goodanimcondition.gif

Sau đây là cùng ví dụ đó, nhưng sử dụng Advance Expression thay vì Advance Condition, nhờ đó không cần đến hai biến:

.. image:: img/animtree_goodanimexpression.webp
.. image:: img/animtree_goodanimexpression2.webp
.. image:: img/animtree_goodanimexpression.gif

Để sử dụng Advance Expression, Advance Expression Base Node phải được thiết lập trong Inspector của node AnimationTree. Mặc định, nó được đặt thành chính node AnimationTree, nhưng cần trỏ đến node chứa script có các biến animation của bạn.

.. seealso::

   Advance Expression được đánh giá bằng class :ref:`class_expression` của Godot. Xem :ref:`doc_evaluating_expressions` để biết thêm thông tin về cách viết expression.

Di chuyển trong StateMachine
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Một trong những tính năng hữu ích của implementation ``StateMachine`` trong Godot là khả năng di chuyển. Bạn có thể yêu cầu graph đi từ state hiện tại đến một state khác, đồng thời đi qua tất cả các state trung gian. Việc này được thực hiện bằng thuật toán A\*. Nếu không có path transition nào bắt đầu từ state hiện tại và kết thúc tại state đích, graph sẽ dịch chuyển tức thời đến state đích.

Để sử dụng khả năng di chuyển, trước tiên bạn nên lấy object :ref:`AnimationNodeStateMachinePlayback <class_AnimationNodeStateMachinePlayback>` từ node ``AnimationTree`` (nó được export dưới dạng một property), sau đó gọi một trong nhiều function của object này:

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

``BlendSpace2D`` là một node dùng để blend nâng cao trong không gian hai chiều. Các point đại diện cho animation được thêm vào một không gian 2D, sau đó một vị trí giữa chúng được điều khiển để xác định việc blend:

.. image:: img/animtree_blendspace2d.gif

Bạn có thể chèn các point này ở bất kỳ đâu trên graph bằng cách nhấp chuột phải hoặc sử dụng nút **add point** trên toolbar. Khi được tạo, một point sẽ lấy tên từ animation hoặc type :ref:`AnimationRootNode<class_AnimationRootNode>` đã chọn. Sau đó, bạn có thể đổi tên point bằng cách nhấp vào tên của nó, hoặc thay đổi vị trí bằng cách nhấp và kéo tên hay point đó. Nếu **Auto Triangles** được bật, một blend triangle giữa các point đã chèn sẽ tự động được tạo bằng cách sử dụng `Delaunay triangulation <https://en.wikipedia.org/wiki/Delaunay_triangulation>`__.

.. image:: img/animtree_blendspacepoints.webp

Blend target của animation trong node này có thể được điều chỉnh trong editor bằng cách nhấn Shift trong khi kéo bằng nút chuột trái, hoặc sử dụng tool chuyên dụng.

``BlendSpace1D`` hoạt động giống hệt ``BlendSpace2D``, nhưng trong một chiều duy nhất (một đường ngang). Vì không sử dụng triangle nên nó có thể hoạt động với ít hơn ba blend point.

.. image:: img/animtree_blendspace1d.webp

Chế độ đồng bộ
~~~~~~~~~~~~~~

Cả ``BlendSpace1D`` và ``BlendSpace2D`` đều có property **Sync Mode**, dùng để kiểm soát cách các animation tiến triển khi được blend. Property này thay thế property boolean ``sync`` cũ và cung cấp khả năng kiểm soát chính xác hơn.

.. image:: img/animtree_syncmode_mutable.webp

Có bốn mode khả dụng:

* **None** (mặc định): Các animation không hoạt động sẽ bị đóng băng và không tiến triển. Chỉ animation hiện đang hoạt động (có weight cao nhất) mới tiến về phía trước. * **Independent**: Các animation không hoạt động tiến triển với weight ``0``. Chế độ này phù hợp với hành vi của thiết lập ``sync = true`` cũ. * **Cyclic Mutable**: Tất cả animation được time-scale để các phase của chúng luôn thẳng hàng. Độ dài cycle dùng chung được tính động dựa trên các blend weight đang hoạt động, nghĩa là một animation duy nhất không được blend sẽ phát ở tốc độ bình thường. Chế độ này hữu ích khi tất cả animation của bạn có cùng một cycle logic (ví dụ: các loop locomotion) nhưng có thể hơi khác nhau về độ dài. * **Cyclic Constant**: Tất cả animation được time-scale để hoàn thành một cycle đầy đủ trong đúng **Cyclic Length** giây, bất kể độ dài riêng của chúng. Đặt property ``cyclic_length`` thành khoảng thời gian cycle mong muốn (phải lớn hơn ``0``).

.. warning::

   Các mode cyclic sync yêu cầu tất cả blend point sử dụng :ref:`AnimationNodeAnimation <class_AnimationNodeAnimation>` với độ dài hữu hạn, không thay đổi. Nếu bất kỳ blend point nào sử dụng type node khác, một cảnh báo sẽ được hiển thị và cyclic sync sẽ không có hiệu lực:

   .. image:: img/animtree_syncmode_warning.webp

.. note::

   Khi sử dụng một trong hai mode cyclic với các animation có độ dài khác nhau, việc áp dụng một
   :ref:`AnimationNodeTimeSeek <class_AnimationNodeTimeSeek>` to the output will break synchronization.
   Trong trường hợp đó, hãy sử dụng :ref:`AnimationNodeAnimation.use_custom_timeline <class_AnimationNodeAnimation_property_use_custom_timeline>` để chuẩn hóa độ dài animation trước khi đồng bộ.

Chế độ blend
~~~~~~~~~~~~

Theo mặc định, việc blend diễn ra ở mode *Continuous*, bằng cách nội suy các point bên trong triangle gần nhất trong ``BlendSpace2D``, hoặc trên đường thẳng giữa các point trong ``BlendSpace1D``. Tuy nhiên, đây không phải lúc nào cũng là lựa chọn tốt nhất. Ví dụ, khi xử lý các animation 2D theo từng frame, bạn có thể muốn chuyển sang mode *Discrete*, trong đó các state trung gian của blend không xuất hiện trong kết quả. Ngoài ra, nếu muốn giữ lại vị trí phát hiện tại khi chuyển đổi giữa các animation discrete, mode *Carry* cho phép bạn làm điều đó. Có thể thiết lập các mode này bằng menu *Blend*.

.. image:: img/animtree_blendmode.webp

Để blend tốt hơn
----------------

Để kết quả blend có tính deterministic (có thể tái tạo và luôn nhất quán), các giá trị property được blend phải có một giá trị ban đầu cụ thể. Ví dụ, trong trường hợp blend hai animation, nếu một animation có property track còn animation kia không có, animation sau sẽ được tính như thể nó có một property track với giá trị ban đầu.

Khi sử dụng các track Position/Rotation/Scale 3D cho bone của Skeleton3D, giá trị ban đầu là Bone Rest. Đối với các property khác, giá trị ban đầu là ``0``, và nếu track hiện diện trong animation ``RESET``, giá trị của keyframe đầu tiên sẽ được sử dụng thay thế.

Ví dụ, AnimationPlayer sau đây có hai animation, nhưng một trong số đó không có Property track cho Position.

.. image:: img/blending1.webp

Điều này có nghĩa là animation thiếu track đó sẽ coi các Position đó là ``Vector2(0, 0)``.

.. image:: img/blending2.webp

Có thể giải quyết vấn đề này bằng cách thêm một Property track cho Position làm giá trị ban đầu vào animation ``RESET``.

.. image:: img/blending3.webp

.. image:: img/blending4.webp

.. note:: Be aware that the ``RESET`` animation exists to define the default pose when loading an object originally.
          Nó được giả định là chỉ có một frame và không được kỳ vọng sẽ được phát bằng timeline.

Cũng cần lưu ý rằng các track Rotation 3D và các Property track cho rotation 2D có Interpolation Type được đặt thành Linear Angle hoặc Cubic Angle sẽ ngăn rotation lớn hơn 180 độ so với giá trị ban đầu khi animation được blend.

Điều này có thể hữu ích cho Skeleton3D để ngăn các bone xuyên vào cơ thể khi blend animation. Vì vậy, các giá trị Bone Rest của Skeleton3D nên gần với trung điểm của phạm vi chuyển động nhất có thể. **Điều này có nghĩa là đối với các model hình người, tốt nhất nên import chúng ở tư thế chữ T (T-pose)**.

.. image:: img/blending5.webp

Bạn có thể thấy path rotation ngắn nhất từ Bone Rest được ưu tiên, thay vì path rotation ngắn nhất giữa các animation.

Nếu cần xoay chính Skeleton3D hơn 180 độ bằng cách blend animation để di chuyển, bạn có thể sử dụng Root Motion.

Root motion
-----------

Khi làm việc với animation 3D, một kỹ thuật phổ biến là animator sử dụng root bone của skeleton để tạo chuyển động cho phần còn lại của skeleton. Điều này cho phép animate nhân vật theo cách mà các bước chân thực sự khớp với mặt sàn bên dưới. Nó cũng cho phép tương tác chính xác với các object trong những cảnh cinematic.

Khi phát animation trong Godot, bạn có thể chọn bone này làm *root motion track*. Làm vậy sẽ hủy biến đổi của bone về mặt trực quan (animation sẽ đứng yên tại chỗ).

.. image:: img/animtree_rootmotiontrack.webp

Sau đó, chuyển động thực tế có thể được lấy thông qua API :ref:`AnimationTree <class_AnimationTree>` dưới dạng một transform:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Lấy motion delta.
    animation_tree.get_root_motion_position()
    animation_tree.get_root_motion_rotation()
    animation_tree.get_root_motion_scale()

    # Lấy giá trị blended thực tế của animation.
    animation_tree.get_root_motion_position_accumulator()
    animation_tree.get_root_motion_rotation_accumulator()
    animation_tree.get_root_motion_scale_accumulator()

 .. code-tab:: csharp

    // Lấy motion delta.
    animationTree.GetRootMotionPosition();
    animationTree.GetRootMotionRotation();
    animationTree.GetRootMotionScale();

    // Lấy giá trị blended thực tế của animation.
    animationTree.GetRootMotionPositionAccumulator();
    animationTree.GetRootMotionRotationAccumulator();
    animationTree.GetRootMotionScaleAccumulator();

Giá trị này có thể được truyền vào các function như :ref:`CharacterBody3D.move_and_slide <class_CharacterBody3D_method_move_and_slide>` để điều khiển chuyển động của nhân vật.

Ngoài ra còn có một tool node, ``RootMotionView``, mà bạn có thể đặt vào một scene để hoạt động như một mặt sàn tùy chỉnh cho nhân vật và animation của mình (node này mặc định bị tắt trong khi game chạy).

.. image:: img/animtree15.gif

Điều khiển từ code
------------------

Sau khi xây dựng tree và xem trước, câu hỏi duy nhất còn lại là "Tất cả những thứ này được điều khiển từ code như thế nào?".

Hãy nhớ rằng các node animation chỉ là tài nguyên, vì vậy chúng được chia sẻ giữa tất cả các instance sử dụng chúng. Việc thiết lập giá trị trực tiếp trong các node sẽ ảnh hưởng đến tất cả các instance của scene sử dụng ``AnimationTree``. Điều này thường không được mong muốn, nhưng có một số trường hợp sử dụng thú vị, chẳng hạn như bạn có thể sao chép và dán các phần của cây animation, hoặc tái sử dụng các node có bố cục phức tạp (chẳng hạn như StateMachine hoặc blend space) trong các cây animation khác nhau.

Dữ liệu animation thực tế nằm trong node ``AnimationTree`` và được truy cập thông qua các thuộc tính. Hãy kiểm tra phần "Parameters" của node ``AnimationTree`` để xem tất cả các tham số có thể được sửa đổi trong thời gian thực:

.. image:: img/animtree_parameters.webp

Điều này rất hữu ích vì cho phép bạn animate chúng từ một ``AnimationPlayer``, hoặc thậm chí chính ``AnimationTree``, qua đó hỗ trợ logic animation rất phức tạp.

Để sửa đổi các giá trị này từ code, bạn phải lấy property path. Bạn có thể tìm thấy chúng bằng cách di chuột lên bất kỳ tham số nào:

.. image:: img/animtree_propertypath.webp

Sau đó, bạn có thể thiết lập hoặc đọc chúng:

.. tabs::
 .. code-tab:: gdscript GDScript

    animation_tree.set("parameters/eye_blend/blend_amount", 1.0)
    # Cú pháp thay thế (cùng kết quả)
    animation_tree["parameters/eye_blend/blend_amount"] = 1.0

 .. code-tab:: csharp

    animationTree.Set("parameters/eye_blend/blend_amount", 1.0);

.. note:: Advance Expressions from a StateMachine will not be found under the parameters. This is because they are held in another script rather than the
         Bản thân AnimationTree. Các `Conditions` nâng cao sẽ nằm trong phần parameters.
