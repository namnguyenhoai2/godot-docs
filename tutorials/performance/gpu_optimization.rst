.. _doc_gpu_optimization:

Tối ưu hóa GPU
==============

Giới thiệu
----------

Nhu cầu về các tính năng đồ họa mới và những tiến bộ trong lĩnh vực này gần như chắc chắn sẽ khiến bạn gặp phải các nút thắt đồ họa. Một số nút thắt có thể nằm ở phía CPU, chẳng hạn như trong các phép tính bên trong engine Godot để chuẩn bị đối tượng cho việc render. Nút thắt cũng có thể xảy ra trên CPU trong graphics driver, nơi sắp xếp các instruction để gửi đến GPU, cũng như trong quá trình truyền các instruction này. Và cuối cùng, nút thắt cũng có thể xảy ra ngay trên GPU.

Nút thắt xảy ra ở đâu trong quá trình render phụ thuộc rất nhiều vào phần cứng cụ thể. Đặc biệt, GPU trên thiết bị di động có thể gặp khó khăn với những scene chạy dễ dàng trên desktop.

Việc tìm hiểu và điều tra các nút thắt GPU hơi khác so với tình huống trên CPU. Điều này là vì thường thì bạn chỉ có thể thay đổi hiệu năng một cách gián tiếp bằng cách thay đổi các instruction gửi cho GPU. Ngoài ra, việc đo lường cũng có thể khó hơn. Trong nhiều trường hợp, cách duy nhất để đo hiệu năng là xem xét những thay đổi trong thời gian render từng frame.

Draw call, state change và API
------------------------------

.. note:: The following section is not relevant to end-users, but is useful to
          cung cấp thông tin nền tảng phù hợp cho các phần sau.

Godot gửi instruction đến GPU thông qua một graphics API (Vulkan, OpenGL, OpenGL ES hoặc WebGL). Hoạt động giao tiếp và hoạt động của driver liên quan có thể khá tốn kém, đặc biệt là trong OpenGL, OpenGL ES và WebGL. Nếu có thể cung cấp các instruction này theo cách được driver và GPU ưu tiên, chúng ta có thể tăng hiệu năng đáng kể.

Gần như mọi lệnh API trong OpenGL đều yêu cầu một lượng validation nhất định để đảm bảo GPU đang ở đúng state. Ngay cả những lệnh có vẻ đơn giản cũng có thể dẫn đến hàng loạt công việc housekeeping diễn ra phía sau. Vì vậy, mục tiêu là giảm các instruction này xuống mức tối thiểu và nhóm các đối tượng tương tự lại với nhau nhiều nhất có thể để chúng có thể được render cùng nhau, hoặc chỉ cần số lượng state change tốn kém tối thiểu.

Batching 2D
~~~~~~~~~~~

Trong 2D, chi phí xử lý riêng từng item có thể cao đến mức không thể chấp nhận được - trên màn hình rất dễ có hàng nghìn item. Đây là lý do sử dụng *batching* 2D. Nhiều item tương tự được nhóm lại và render theo một batch, thông qua một draw call duy nhất, thay vì thực hiện một draw call riêng cho từng item. Ngoài ra, điều này giúp giữ state change, thay đổi material và texture ở mức tối thiểu.

Batching 3D
~~~~~~~~~~~

Trong 3D, chúng ta vẫn hướng đến việc giảm thiểu draw call và state change. Tuy nhiên, việc batch nhiều đối tượng vào một draw call duy nhất có thể khó hơn. Mesh 3D thường bao gồm hàng trăm hoặc hàng nghìn triangle, và việc kết hợp các mesh lớn trong thời gian thực có chi phí quá cao. Khi số lượng triangle trên mỗi mesh tăng lên, chi phí kết hợp chúng nhanh chóng vượt qua mọi lợi ích. Một giải pháp thay thế tốt hơn nhiều là **join mesh trước thời điểm chạy** (các static mesh có quan hệ với nhau). Việc này có thể do artist thực hiện hoặc được thực hiện bằng code trong Godot באמצעות add-on.

Việc batch các đối tượng trong 3D cũng có chi phí. Một số đối tượng được render như một đối tượng duy nhất sẽ không thể được cull riêng lẻ. Toàn bộ một thành phố nằm ngoài màn hình vẫn sẽ được render nếu nó được join với một ngọn cỏ duy nhất đang nằm trong màn hình. Vì vậy, bạn luôn nên tính đến vị trí và việc culling của các đối tượng khi cố gắng batch các đối tượng 3D với nhau. Dù vậy, lợi ích của việc join các đối tượng tĩnh thường lớn hơn những cân nhắc khác, đặc biệt với số lượng lớn các đối tượng ở xa hoặc có ít polygon.

Để biết thêm thông tin về các tối ưu hóa dành riêng cho 3D, hãy xem
:ref:`doc_optimizing_3d_performance`.

Tái sử dụng shader và material
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot renderer hơi khác so với những renderer khác hiện có. Nó được thiết kế để giảm state change của GPU nhiều nhất có thể. :ref:`StandardMaterial3D <class_StandardMaterial3D>` làm tốt việc tái sử dụng các material cần những shader tương tự. Nếu sử dụng custom shader, hãy đảm bảo tái sử dụng chúng nhiều nhất có thể. Các ưu tiên của Godot là:

-  **Tái sử dụng Material:** Càng có ít material khác nhau trong scene thì việc render càng nhanh. Nếu một scene có số lượng đối tượng rất lớn (hàng trăm hoặc hàng nghìn), hãy thử tái sử dụng các material. Trong trường hợp xấu nhất, hãy sử dụng atlas để giảm số lần thay đổi texture. - **Tái sử dụng Shader:** Nếu không thể tái sử dụng material, ít nhất hãy cố gắng tái sử dụng shader. Lưu ý: shader được tự động tái sử dụng giữa các StandardMaterial3D dùng chung một cấu hình (các feature được bật hoặc tắt bằng checkbox), ngay cả khi chúng có các parameter khác nhau.

Nếu một scene có, chẳng hạn, 20.000 đối tượng với 20.000 material khác nhau, việc render sẽ chậm. Nếu cùng scene đó có 20.000 đối tượng nhưng chỉ sử dụng 100 material, việc render sẽ nhanh hơn nhiều.

Chi phí pixel so với chi phí vertex
-----------------------------------

Có thể bạn đã nghe nói rằng số polygon trong một model càng thấp thì model đó sẽ được render càng nhanh. Điều này *thực sự* mang tính tương đối và phụ thuộc vào nhiều yếu tố.

Trên PC và console hiện đại, chi phí vertex thấp. Ban đầu, GPU chỉ render triangle. Điều này có nghĩa là trong mỗi frame:

1. Tất cả vertex phải được CPU transform (bao gồm clipping). 2. Tất cả vertex phải được gửi từ RAM chính đến memory của GPU.

Ngày nay, tất cả việc này đều được xử lý bên trong GPU, giúp tăng hiệu năng đáng kể. Các artist 3D thường có cảm nhận sai về hiệu năng theo polycount vì phần mềm modeling 3D (chẳng hạn như Blender, 3ds Max, v.v.) cần giữ geometry trong memory của CPU để có thể chỉnh sửa, làm giảm hiệu năng thực tế. Game engine dựa vào GPU nhiều hơn, vì vậy có thể render nhiều triangle hiệu quả hơn rất nhiều.

Trên thiết bị di động, tình hình lại khác. GPU của PC và console là những cỗ máy brute-force có thể lấy lượng điện tùy ý từ lưới điện. GPU di động bị giới hạn bởi một viên pin rất nhỏ, nên cần tiết kiệm năng lượng hơn rất nhiều.

Để hiệu quả hơn, GPU di động cố gắng tránh *overdraw*. Overdraw xảy ra khi cùng một pixel trên màn hình được render nhiều hơn một lần. Hãy tưởng tượng một thị trấn có vài tòa nhà. GPU không biết phần nào hiển thị và phần nào bị che khuất cho đến khi render chúng. Ví dụ, một ngôi nhà có thể được render trước, sau đó là một ngôi nhà khác ở phía trước nó (điều này có nghĩa là cùng một pixel đã được render hai lần). GPU của PC thường không quá quan tâm đến việc này mà chỉ thêm nhiều pixel processor hơn vào phần cứng để tăng hiệu năng (điều này cũng làm tăng mức tiêu thụ điện năng).

Việc sử dụng nhiều điện năng hơn không phải là lựa chọn trên thiết bị di động, vì vậy các thiết bị di động sử dụng một kỹ thuật gọi là *tile-based rendering*, chia màn hình thành một grid. Mỗi cell lưu danh sách các triangle được vẽ vào đó và sắp xếp chúng theo depth để giảm thiểu *overdraw*. Kỹ thuật này cải thiện hiệu năng và giảm mức tiêu thụ điện năng, nhưng phải đánh đổi hiệu năng vertex. Do đó, có thể xử lý ít vertex và triangle hơn để vẽ.

Ngoài ra, tile-based rendering gặp khó khăn khi có các đối tượng nhỏ với nhiều geometry nằm trong một phần nhỏ của màn hình. Điều này buộc GPU di động phải dồn nhiều tải lên một tile màn hình duy nhất, khiến hiệu năng giảm đáng kể vì tất cả cell khác phải chờ tile đó hoàn tất trước khi hiển thị frame.

Tóm lại, đừng lo lắng về số lượng vertex trên thiết bị di động, nhưng **hãy tránh tập trung vertex vào các phần nhỏ của màn hình**. Nếu một character, NPC, vehicle, v.v. ở xa (nghĩa là trông rất nhỏ), hãy sử dụng model có level of detail (LOD) thấp hơn. Ngay cả trên GPU desktop, tốt nhất cũng nên tránh có các triangle nhỏ hơn kích thước của một pixel trên màn hình.

Hãy chú ý đến việc xử lý vertex bổ sung cần thiết khi sử dụng:

-  Skinning (skeletal animation) - Morph (shape key) - Đối tượng được chiếu sáng bằng vertex (thường dùng trên thiết bị di động)

Pixel/fragment shader và fill rate
----------------------------------

Trái ngược với xử lý vertex, chi phí shading fragment (theo từng pixel) đã tăng mạnh qua nhiều năm. Độ phân giải màn hình đã tăng: diện tích của màn hình 4K là 8.294.400 pixel, so với 307.200 pixel của màn hình VGA 640×480 cũ. Diện tích lớn hơn 27 lần! Ngoài ra, độ phức tạp của fragment shader cũng tăng vọt. Physically-based rendering yêu cầu các phép tính phức tạp cho mỗi fragment.

Bạn có thể kiểm tra khá dễ dàng xem một project có bị giới hạn bởi fill rate hay không. Tắt V-Sync để tránh giới hạn số frame trên giây, sau đó so sánh số frame trên giây khi chạy với một cửa sổ lớn và khi chạy với một cửa sổ rất nhỏ. Bạn cũng có thể đạt được lợi ích tương tự bằng cách giảm kích thước shadow map nếu đang sử dụng shadow. Thông thường, bạn sẽ thấy FPS tăng khá nhiều khi dùng cửa sổ nhỏ, cho thấy ở một mức độ nào đó bạn bị giới hạn bởi fill rate. Mặt khác, nếu FPS tăng rất ít hoặc không tăng, thì nút thắt của bạn nằm ở nơi khác.

Bạn có thể tăng hiệu năng trong một project bị giới hạn bởi fill rate bằng cách giảm lượng công việc GPU phải thực hiện. Bạn có thể làm điều này bằng cách đơn giản hóa shader (có thể tắt các tùy chọn tốn kém nếu bạn đang sử dụng một :ref:`StandardMaterial3D <class_StandardMaterial3D>`), hoặc giảm số lượng và kích thước texture được sử dụng. Ngoài ra, khi sử dụng shaded particle, hãy cân nhắc ép buộc vertex shading trong material của chúng để giảm chi phí shading.

.. seealso::

    Trên phần cứng được hỗ trợ, :ref:`doc_variable_rate_shading` có thể được sử dụng để giảm chi phí xử lý shading mà không ảnh hưởng đến độ sắc nét của các cạnh trong hình ảnh cuối cùng.

**Khi nhắm đến các thiết bị di động, hãy cân nhắc sử dụng các shader đơn giản nhất mà bạn có thể sử dụng một cách hợp lý.**

Đọc texture
~~~~~~~~~~~

Yếu tố còn lại trong fragment shader là chi phí đọc texture. Đọc texture là một thao tác tốn kém, đặc biệt khi đọc từ nhiều texture trong cùng một fragment shader. Ngoài ra, hãy lưu ý rằng việc filtering có thể làm thao tác này chậm hơn nữa (trilinear filtering giữa các mipmap và việc tính trung bình). Đọc texture cũng tốn nhiều điện năng, đây là một vấn đề lớn trên thiết bị di động.

**Nếu bạn sử dụng shader của bên thứ ba hoặc tự viết shader, hãy cố gắng sử dụng các thuật toán yêu cầu ít thao tác đọc texture nhất có thể.**

Nén texture
~~~~~~~~~~~

Theo mặc định, Godot nén texture của các model 3D khi import bằng phương pháp nén video RAM (VRAM). Nén video RAM không hiệu quả về kích thước bằng PNG hoặc JPG khi lưu trữ, nhưng cải thiện hiệu năng đáng kể khi vẽ các texture đủ lớn.

Đó là vì mục tiêu chính của việc nén texture là giảm băng thông giữa bộ nhớ và GPU.

Trong 3D, hình dạng của các đối tượng phụ thuộc vào geometry nhiều hơn texture, vì vậy việc nén thường không dễ nhận thấy. Trong 2D, việc nén phụ thuộc nhiều hơn vào các hình dạng bên trong texture, nên các artifact do nén 2D tạo ra dễ nhận thấy hơn.

Cần lưu ý rằng hầu hết thiết bị Android không hỗ trợ nén texture có transparency (chỉ hỗ trợ texture opaque), vì vậy hãy ghi nhớ điều này.

.. note::

   Ngay cả trong 3D, các texture "pixel art" cũng nên tắt nén VRAM, vì nén sẽ ảnh hưởng tiêu cực đến hình thức của chúng mà không cải thiện đáng kể hiệu năng do độ phân giải thấp.

Hậu xử lý và shadow
~~~~~~~~~~~~~~~~~~~

Các hiệu ứng hậu xử lý và shadow cũng có thể tốn kém về mặt hoạt động fragment shading. Luôn kiểm tra ảnh hưởng của chúng trên nhiều loại phần cứng khác nhau.

**Giảm kích thước shadowmap có thể cải thiện hiệu năng**, cả khi ghi lẫn khi đọc shadowmap. Ngoài ra, cách tốt nhất để cải thiện hiệu năng của shadow là tắt shadow trên càng nhiều light và object càng tốt. Bạn thường có thể tắt shadow của các OmniLight/SpotLight nhỏ hơn hoặc ở xa mà chỉ gây ảnh hưởng nhỏ về mặt hình ảnh.

Transparency và blending
------------------------

Các object trong suốt gây ra những vấn đề đặc biệt đối với hiệu quả rendering. Các object opaque (đặc biệt trong 3D) về cơ bản có thể được render theo bất kỳ thứ tự nào, và Z-buffer sẽ đảm bảo rằng chỉ các object ở phía trước mới được shading. Các object transparent hoặc blended thì khác. Trong hầu hết trường hợp, chúng không thể dựa vào Z-buffer và phải được render theo "painter's order" (tức là từ sau ra trước) để hiển thị chính xác.

Các object transparent cũng đặc biệt gây ảnh hưởng xấu đến fill rate, vì mọi item đều phải được vẽ, ngay cả khi các object transparent khác sẽ được vẽ đè lên sau đó.

Các object opaque không cần làm vậy. Chúng thường có thể tận dụng Z-buffer bằng cách chỉ ghi vào Z-buffer trước, sau đó chỉ thực hiện fragment shader trên fragment "chiến thắng", tức object đang ở phía trước tại một pixel cụ thể.

Transparency đặc biệt tốn kém khi nhiều object transparent chồng lên nhau. Thông thường, tốt hơn là sử dụng các vùng transparent nhỏ nhất có thể để giảm thiểu yêu cầu về fill rate, đặc biệt trên thiết bị di động, nơi fill rate rất tốn kém. Thực tế, trong nhiều tình huống, render geometry opaque phức tạp hơn có thể nhanh hơn việc dùng transparency để "đánh lừa".

Lời khuyên cho nhiều nền tảng
-----------------------------

Nếu bạn dự định phát hành trên nhiều nền tảng, hãy kiểm thử *sớm* và *thường xuyên* trên tất cả nền tảng, đặc biệt là thiết bị di động. Phát triển game trên desktop nhưng đợi đến phút cuối mới cố gắng port sang mobile là công thức dẫn đến thảm họa.

Nhìn chung, bạn nên thiết kế game cho mẫu số chung thấp nhất, sau đó thêm các cải tiến tùy chọn cho những nền tảng mạnh hơn. Ví dụ, bạn có thể muốn sử dụng phương thức rendering Compatibility cho cả nền tảng desktop và mobile mà bạn nhắm đến.

Mobile/tiled renderer
---------------------

Như đã mô tả ở trên, GPU trên thiết bị di động hoạt động theo những cách khác biệt đáng kể so với GPU trên desktop. Hầu hết thiết bị di động sử dụng tile renderer. Tile renderer chia màn hình thành các tile có kích thước đồng đều, vừa với bộ nhớ cache siêu nhanh, nhờ đó giảm số lượng thao tác đọc/ghi vào bộ nhớ chính.

Tuy nhiên, cách này cũng có một số nhược điểm. Tiled rendering có thể khiến một số kỹ thuật trở nên phức tạp và tốn kém hơn nhiều khi thực hiện. Các tile phụ thuộc vào kết quả rendering ở những tile khác hoặc vào việc bảo toàn kết quả của các thao tác trước đó có thể rất chậm. Hãy đặc biệt cẩn thận khi kiểm tra hiệu năng của shader, viewport texture và post-processing.
