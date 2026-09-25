.. _doc_gpu_optimization:

Tối ưu hóa GPU
==============

Giới thiệu
----------

Nhu cầu về các tính năng đồ họa mới và sự tiến bộ gần như chắc chắn sẽ khiến bạn gặp phải các nút thắt đồ họa. Một số nút thắt có thể nằm ở phía CPU, chẳng hạn như trong các phép tính bên trong Godot engine để chuẩn bị các đối tượng cho việc kết xuất. Nút thắt cũng có thể xảy ra ở CPU trong graphics driver, nơi sắp xếp các chỉ dẫn để chuyển cho GPU, cũng như trong quá trình truyền các chỉ dẫn này. Cuối cùng, nút thắt cũng có thể xảy ra ngay trên GPU.

Vị trí xảy ra nút thắt trong quá trình kết xuất phụ thuộc rất nhiều vào phần cứng. Đặc biệt, GPU trên thiết bị di động có thể gặp khó khăn với những scene chạy dễ dàng trên máy tính để bàn.

Việc hiểu và điều tra các nút thắt GPU hơi khác so với tình huống trên CPU. Đó là vì thường thì bạn chỉ có thể thay đổi hiệu năng một cách gián tiếp bằng cách thay đổi các chỉ dẫn gửi cho GPU. Ngoài ra, việc đo lường cũng có thể khó khăn hơn. Trong nhiều trường hợp, cách duy nhất để đo hiệu năng là kiểm tra những thay đổi trong thời gian dành cho việc kết xuất từng frame.

Draw call, thay đổi trạng thái và API
-------------------------------------

.. note:: Phần sau đây không liên quan đến người dùng cuối, nhưng hữu ích để cung cấp thông tin nền tảng liên quan đến các phần sau.

Godot gửi các chỉ dẫn đến GPU thông qua graphics API (Vulkan, OpenGL, OpenGL ES hoặc WebGL). Hoạt động giao tiếp và driver liên quan có thể khá tốn kém, đặc biệt là trong OpenGL, OpenGL ES và WebGL. Nếu có thể cung cấp các chỉ dẫn này theo cách được driver và GPU ưu tiên, chúng ta có thể tăng hiệu năng đáng kể.

Gần như mọi lệnh API trong OpenGL đều yêu cầu một mức độ xác thực nhất định để đảm bảo GPU đang ở đúng trạng thái. Ngay cả những lệnh có vẻ đơn giản cũng có thể dẫn đến hàng loạt hoạt động dọn dẹp phía sau. Vì vậy, mục tiêu là giảm các chỉ dẫn này xuống mức tối thiểu và nhóm các đối tượng tương tự lại với nhau nhiều nhất có thể để chúng có thể được kết xuất cùng nhau, hoặc với số lần thay đổi trạng thái tốn kém này ở mức tối thiểu.

Batching 2D
~~~~~~~~~~~

Trong 2D, chi phí xử lý từng item riêng lẻ có thể cao đến mức không thể chấp nhận được - trên màn hình dễ dàng có đến hàng nghìn item. Đây là lý do *batching* 2D được sử dụng. Nhiều item tương tự được nhóm lại và kết xuất theo batch thông qua một draw call duy nhất, thay vì thực hiện một draw call riêng cho từng item. Ngoài ra, điều này giúp giảm thiểu các thay đổi trạng thái, thay đổi material và texture.

Batching 3D
~~~~~~~~~~~

Trong 3D, chúng ta vẫn hướng đến việc giảm thiểu draw call và thay đổi trạng thái. Tuy nhiên, việc gộp nhiều đối tượng vào một draw call duy nhất có thể khó khăn hơn. Mesh 3D thường bao gồm hàng trăm hoặc hàng nghìn tam giác, và việc kết hợp các mesh lớn theo thời gian thực có chi phí quá cao. Khi số lượng tam giác trên mỗi mesh tăng lên, chi phí nối chúng nhanh chóng vượt xa mọi lợi ích. Một giải pháp thay thế tốt hơn nhiều là **nối các mesh từ trước** (các mesh tĩnh tương quan với nhau). Việc này có thể do artist thực hiện hoặc được lập trình trong Godot bằng một add-on.

Việc batching các đối tượng trong 3D cũng có chi phí. Một số đối tượng được kết xuất như một đối tượng duy nhất không thể được culling riêng lẻ. Toàn bộ một thành phố nằm ngoài màn hình vẫn sẽ được kết xuất nếu nó được nối với một ngọn cỏ duy nhất đang ở trên màn hình. Vì vậy, khi cố gắng batching các đối tượng 3D với nhau, bạn luôn phải tính đến vị trí và việc culling các đối tượng. Mặc dù vậy, lợi ích của việc nối các đối tượng tĩnh thường lớn hơn những cân nhắc khác, đặc biệt là với số lượng lớn các đối tượng ở xa hoặc có ít polygon.

Để biết thêm thông tin về các tối ưu hóa dành riêng cho 3D, hãy xem
:ref:`doc_optimizing_3d_performance`.

Tái sử dụng shader và material
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot renderer hơi khác so với những gì hiện có. Nó được thiết kế để giảm thiểu tối đa các thay đổi trạng thái GPU. :ref:`StandardMaterial3D <class_StandardMaterial3D>` thực hiện tốt việc tái sử dụng các material cần những shader tương tự. Nếu sử dụng custom shader, hãy đảm bảo tái sử dụng chúng nhiều nhất có thể. Các ưu tiên của Godot là:

-  **Tái sử dụng Material:** Càng có ít material khác nhau trong scene thì việc kết xuất càng nhanh. Nếu scene có số lượng đối tượng rất lớn (hàng trăm hoặc hàng nghìn), hãy cố gắng tái sử dụng material. Trong trường hợp xấu nhất, hãy sử dụng atlas để giảm số lần thay đổi texture.
-  **Tái sử dụng Shader:** Nếu không thể tái sử dụng material, ít nhất hãy cố gắng tái sử dụng shader. Lưu ý: shader được tự động tái sử dụng giữa các StandardMaterial3D có cùng cấu hình (các tính năng được bật hoặc tắt bằng hộp kiểm), ngay cả khi chúng có các tham số khác nhau.

Ví dụ, nếu một scene có 20.000 đối tượng với 20.000 material khác nhau, việc kết xuất sẽ chậm. Nếu cùng scene đó có 20.000 đối tượng nhưng chỉ sử dụng 100 material, việc kết xuất sẽ nhanh hơn nhiều.

Chi phí pixel so với chi phí vertex
-----------------------------------

Có thể bạn đã nghe nói rằng số polygon trong model càng thấp thì model sẽ được kết xuất càng nhanh. Điều này *thực sự* mang tính tương đối và phụ thuộc vào nhiều yếu tố.

Trên máy tính và console hiện đại, chi phí vertex thấp. Ban đầu, GPU chỉ kết xuất các tam giác. Điều này có nghĩa là trong mỗi frame:

1. Tất cả vertex phải được CPU biến đổi (bao gồm cả clipping).
2. Tất cả vertex phải được gửi từ RAM chính đến bộ nhớ GPU.

Ngày nay, tất cả những việc này được xử lý bên trong GPU, giúp tăng hiệu năng đáng kể. Các artist 3D thường có nhận định sai về hiệu năng của polycount vì phần mềm modeling 3D (chẳng hạn như Blender, 3ds Max, v.v.) cần giữ geometry trong bộ nhớ CPU để có thể chỉnh sửa, làm giảm hiệu năng thực tế. Game engine phụ thuộc vào GPU nhiều hơn, nên có thể kết xuất nhiều tam giác hiệu quả hơn nhiều.

Trên thiết bị di động, tình hình lại khác. GPU của máy tính và console là những cỗ máy brute-force có thể lấy lượng điện cần thiết từ lưới điện. GPU di động bị giới hạn bởi một viên pin nhỏ, nên cần tiết kiệm điện hơn nhiều.

Để hiệu quả hơn, GPU di động cố gắng tránh *overdraw*. Overdraw xảy ra khi cùng một pixel trên màn hình được kết xuất nhiều hơn một lần. Hãy hình dung một thị trấn có nhiều tòa nhà. GPU không biết phần nào hiển thị và phần nào bị che khuất cho đến khi chúng được vẽ. Ví dụ, một ngôi nhà có thể được vẽ rồi sau đó một ngôi nhà khác ở phía trước nó được vẽ (có nghĩa là cùng một pixel đã được kết xuất hai lần). GPU của máy tính thường không quá quan tâm đến điều này mà chỉ bổ sung thêm nhiều bộ xử lý pixel vào phần cứng để tăng hiệu năng (điều này cũng làm tăng mức tiêu thụ điện).

Việc sử dụng nhiều điện hơn không phải là một lựa chọn trên thiết bị di động, vì vậy thiết bị di động sử dụng một kỹ thuật gọi là *tile-based rendering*, chia màn hình thành một lưới. Mỗi ô lưu danh sách các tam giác được vẽ trên đó và sắp xếp chúng theo độ sâu để giảm thiểu *overdraw*. Kỹ thuật này cải thiện hiệu năng và giảm mức tiêu thụ điện, nhưng phải đánh đổi bằng hiệu năng vertex. Do đó, có thể xử lý ít vertex và tam giác hơn để vẽ.

Ngoài ra, tile-based rendering gặp khó khăn khi có các đối tượng nhỏ với nhiều geometry nằm trong một phần nhỏ của màn hình. Điều này buộc GPU di động phải chịu nhiều tải trên một tile màn hình duy nhất, làm giảm hiệu năng đáng kể vì tất cả các ô khác phải chờ tile đó hoàn tất trước khi hiển thị frame.

Tóm lại, đừng lo về số lượng đỉnh trên thiết bị di động, nhưng **hãy tránh tập trung các đỉnh vào những phần nhỏ của màn hình**. Nếu một nhân vật, NPC, phương tiện, v.v. ở xa (nghĩa là trông rất nhỏ), hãy sử dụng mô hình có mức độ chi tiết (LOD) thấp hơn. Ngay cả trên GPU máy tính để bàn, tốt hơn hết là tránh có các tam giác nhỏ hơn kích thước một pixel trên màn hình.

Hãy chú ý đến phần xử lý đỉnh bổ sung cần thiết khi sử dụng:

-  Skinning (hoạt ảnh khung xương)
-  Morphs (shape keys)
-  Đối tượng được chiếu sáng theo đỉnh (phổ biến trên thiết bị di động)

Pixel/fragment shader và fill rate
----------------------------------

Trái ngược với việc xử lý đỉnh, chi phí shading fragment (theo từng pixel) đã tăng đáng kể qua nhiều năm. Độ phân giải màn hình đã tăng: diện tích của màn hình 4K là 8.294.400 pixel, so với 307.200 pixel của màn hình VGA 640×480 cũ. Diện tích lớn hơn 27 lần! Ngoài ra, độ phức tạp của fragment shader cũng tăng vọt. Việc render dựa trên vật lý đòi hỏi các phép tính phức tạp cho từng fragment.

Bạn có thể khá dễ dàng kiểm tra xem một project có bị giới hạn bởi fill rate hay không. Tắt V-Sync để tránh giới hạn số khung hình mỗi giây, sau đó so sánh số khung hình mỗi giây khi chạy với cửa sổ lớn và khi chạy với cửa sổ rất nhỏ. Nếu sử dụng shadow, bạn cũng có thể giảm kích thước shadow map tương tự. Thông thường, bạn sẽ thấy FPS tăng khá nhiều khi sử dụng cửa sổ nhỏ, cho biết bạn đang bị giới hạn bởi fill rate ở một mức độ nào đó. Ngược lại, nếu FPS tăng rất ít hoặc không tăng, thì nút thắt cổ chai của bạn nằm ở nơi khác.

Bạn có thể tăng hiệu năng trong một project bị giới hạn bởi fill rate bằng cách giảm lượng công việc GPU phải thực hiện. Bạn có thể làm điều này bằng cách đơn giản hóa shader (có thể tắt các tùy chọn tốn kém nếu bạn đang sử dụng :ref:`StandardMaterial3D <class_StandardMaterial3D>`), hoặc giảm số lượng và kích thước texture được sử dụng. Ngoài ra, khi sử dụng particle có shading, hãy cân nhắc buộc material của chúng sử dụng vertex shading để giảm chi phí shading.

.. seealso::

    Trên phần cứng được hỗ trợ, :ref:`doc_variable_rate_shading` có thể được sử dụng để giảm chi phí xử lý shading mà không ảnh hưởng đến độ sắc nét của các cạnh trong hình ảnh cuối cùng.

**Khi nhắm đến các thiết bị di động, hãy cân nhắc sử dụng những shader đơn giản nhất có thể mà bạn vẫn có thể chấp nhận được.**

Đọc texture
~~~~~~~~~~~

Yếu tố khác trong fragment shader là chi phí đọc texture. Đọc texture là một thao tác tốn kém, đặc biệt khi đọc từ nhiều texture trong cùng một fragment shader. Ngoài ra, hãy lưu ý rằng việc filtering có thể khiến thao tác này chậm hơn nữa (trilinear filtering giữa các mipmap và tính trung bình). Đọc texture cũng tốn năng lượng, đây là một vấn đề lớn trên thiết bị di động.

**Nếu bạn sử dụng shader của bên thứ ba hoặc tự viết shader, hãy cố gắng sử dụng các thuật toán yêu cầu ít thao tác đọc texture nhất có thể.**

Nén texture
~~~~~~~~~~~

Theo mặc định, Godot nén texture của các model 3D khi import bằng phương pháp nén video RAM (VRAM). Nén video RAM không hiệu quả về kích thước như PNG hoặc JPG khi lưu trữ, nhưng giúp tăng hiệu năng đáng kể khi vẽ các texture đủ lớn.

Đó là vì mục tiêu chính của việc nén texture là giảm băng thông giữa bộ nhớ và GPU.

Trong 3D, hình dạng của các đối tượng phụ thuộc vào hình học nhiều hơn texture, vì vậy việc nén thường không dễ nhận thấy. Trong 2D, việc nén phụ thuộc nhiều hơn vào các hình dạng bên trong texture, nên các hiện tượng nhiễu do nén 2D tạo ra dễ nhận thấy hơn.

Xin lưu ý rằng hầu hết thiết bị Android không hỗ trợ nén texture có độ trong suốt (chỉ hỗ trợ texture opaque), vì vậy hãy ghi nhớ điều này.

.. note::

   Ngay cả trong 3D, texture "pixel art" cũng nên tắt nén VRAM, vì việc này sẽ ảnh hưởng tiêu cực đến hình thức của texture mà không cải thiện đáng kể hiệu năng do chúng có độ phân giải thấp.

Hậu xử lý và shadow
~~~~~~~~~~~~~~~~~~~

Các hiệu ứng hậu xử lý và shadow cũng có thể tốn kém về hoạt động shading fragment. Hãy luôn kiểm tra tác động của chúng trên nhiều loại phần cứng khác nhau.

**Giảm kích thước shadowmap có thể tăng hiệu năng**, cả khi ghi lẫn khi đọc shadowmap. Ngoài ra, cách tốt nhất để cải thiện hiệu năng của shadow là tắt shadow cho càng nhiều light và object càng tốt. Có thể thường tắt shadow của các OmniLight/SpotLight nhỏ hơn hoặc ở xa mà chỉ gây ảnh hưởng nhỏ đến hình ảnh.

Độ trong suốt và blending
-------------------------

Các đối tượng trong suốt gây ra những vấn đề đặc biệt đối với hiệu quả render. Các đối tượng opaque (đặc biệt trong 3D) về cơ bản có thể được render theo bất kỳ thứ tự nào, và Z-buffer sẽ đảm bảo chỉ các đối tượng ở phía trước được shading. Các đối tượng trong suốt hoặc được blend thì khác. Trong hầu hết trường hợp, chúng không thể dựa vào Z-buffer và phải được render theo "thứ tự họa sĩ" (tức là từ sau ra trước) để hiển thị chính xác.

Các đối tượng trong suốt cũng đặc biệt gây bất lợi cho fill rate, vì mọi đối tượng đều phải được vẽ ngay cả khi các đối tượng trong suốt khác sẽ được vẽ chồng lên sau đó.

Các đối tượng opaque không cần làm vậy. Thông thường, chúng có thể tận dụng Z-buffer bằng cách trước tiên chỉ ghi vào Z-buffer, sau đó chỉ thực hiện fragment shader trên fragment "chiến thắng", tức là đối tượng nằm ở phía trước tại một pixel cụ thể.

Độ trong suốt đặc biệt tốn kém khi nhiều đối tượng trong suốt chồng lên nhau. Thông thường, nên sử dụng các vùng trong suốt nhỏ nhất có thể để giảm thiểu yêu cầu về fill rate, đặc biệt trên thiết bị di động, nơi fill rate rất tốn kém. Thực tế, trong nhiều trường hợp, render hình học opaque phức tạp hơn có thể nhanh hơn việc sử dụng độ trong suốt để "đánh lừa".

Lời khuyên cho nhiều nền tảng
-----------------------------

Nếu bạn dự định phát hành trên nhiều nền tảng, hãy kiểm thử *sớm* và kiểm thử *thường xuyên* trên tất cả nền tảng, đặc biệt là thiết bị di động. Phát triển game trên máy tính để bàn nhưng đến phút cuối mới cố gắng chuyển sang thiết bị di động là công thức dẫn đến thảm họa.

Nhìn chung, bạn nên thiết kế game cho mẫu số chung thấp nhất, sau đó thêm các cải tiến tùy chọn cho những nền tảng mạnh hơn. Ví dụ: bạn có thể muốn sử dụng phương thức render Compatibility cho cả nền tảng máy tính để bàn và thiết bị di động nếu nhắm đến cả hai.

Trình render di động/tiled
--------------------------

Như đã mô tả ở trên, GPU trên thiết bị di động hoạt động khác biệt đáng kể so với GPU trên máy tính để bàn. Hầu hết thiết bị di động sử dụng tile renderer. Tile renderer chia màn hình thành các tile có kích thước cố định, vừa với bộ nhớ cache siêu nhanh, qua đó giảm số thao tác đọc/ghi vào bộ nhớ chính.

Tuy nhiên, cách này cũng có một số nhược điểm. Tiled rendering có thể khiến một số kỹ thuật trở nên phức tạp và tốn kém hơn nhiều khi thực hiện. Các tile phụ thuộc vào kết quả render ở những tile khác hoặc vào việc bảo toàn kết quả của các thao tác trước đó có thể rất chậm. Hãy hết sức cẩn thận khi kiểm tra hiệu năng của shader, texture viewport và hậu xử lý.
