.. _doc_faking_global_illumination:

Giả lập chiếu sáng toàn cục
===========================

Tại sao phải giả lập chiếu sáng toàn cục?
-----------------------------------------

Godot cung cấp một số kỹ thuật chiếu sáng toàn cục (GI), mỗi kỹ thuật đều có ưu điểm và nhược điểm riêng. Tuy vậy, bạn vẫn có thể tránh sử dụng bất kỳ kỹ thuật GI nào và thay vào đó dùng một phương pháp thủ công. Có một vài lý do để sử dụng phương pháp "thủ công" cho chiếu sáng toàn cục thay vì VoxelGI, SDFGI hoặc lightmap được bake:

- Bạn cần hiệu năng rendering tốt nhưng không thể thực hiện quy trình bake lightmap có thể khá phức tạp.
- Bạn cần một phương pháp GI hoàn toàn theo thời gian thực *and* hoạt động với các level được tạo theo quy trình.
- Bạn cần một phương pháp GI hoàn toàn theo thời gian thực *and* không gặp phải hiện tượng rò rỉ ánh sáng đáng kể.

Các phương pháp được mô tả dưới đây chỉ xử lý ánh sáng khuếch tán gián tiếp, không xử lý ánh sáng specular. Đối với ánh sáng specular, hãy cân nhắc sử dụng ReflectionProbes, vốn thường đủ nhẹ để dùng kết hợp với phương pháp GI giả lập này.

.. seealso::

    Không chắc việc giả lập chiếu sáng toàn cục bằng các nguồn sáng có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI hiện có trong Godot 4.

Giả lập chiếu sáng toàn cục của DirectionalLight3D
--------------------------------------------------

Mặc dù bầu trời cung cấp ánh sáng định hướng riêng, node DirectionalLight3D chính của scene thường phát ra một lượng ánh sáng lớn. Khi sử dụng kỹ thuật GI, ánh sáng này sẽ phản xạ trên các bề mặt rắn và dội lại trên hầu hết các bề mặt ngoài trời đang trong vùng bóng.

Ta có thể giả lập điều này bằng cách thêm một node DirectionalLight3D thứ hai với các thay đổi sau:

- Xoay nguồn sáng 180 độ. Điều này cho phép nó biểu diễn ánh sáng dội lại từ node DirectionalLight3D chính.
- Đặt **Shadows** thành **Off**. Điều này làm giảm tải hiệu năng của nguồn sáng phụ, đồng thời cho phép các khu vực trong bóng nhận được *some* ánh sáng (đúng với mục đích của chúng ta ở đây).
- Đặt **Energy** bằng 10-40% giá trị ban đầu. Không có giá trị "hoàn hảo", vì vậy hãy thử nghiệm với nhiều giá trị energy khác nhau tùy theo nguồn sáng và màu vật liệu thường dùng của bạn.
- Đặt **Specular** thành ``0.0``. Ánh sáng gián tiếp không nên tạo ra các vùng specular có thể nhìn thấy, vì vậy chúng ta cần tắt hoàn toàn ánh sáng specular cho nguồn sáng phụ.

.. note::

    Phương pháp này hiệu quả nhất trong các scene chủ yếu ở ngoài trời. Khi đi vào trong nhà, ánh sáng của DirectionalLight3D phụ vẫn sẽ nhìn thấy vì nguồn sáng này đã tắt bóng.

    Có thể khắc phục điều này bằng cách giảm dần energy của DirectionalLight3D phụ khi đi vào khu vực trong nhà (và thực hiện ngược lại khi rời khỏi khu vực trong nhà). Chẳng hạn, bạn có thể đạt được điều này bằng node Area3D và AnimationPlayer.

Giả lập chiếu sáng toàn cục của nguồn sáng theo vị trí
------------------------------------------------------

Có thể áp dụng cùng phương pháp như với DirectionalLight3D cho các nguồn sáng theo vị trí (OmniLight3D và SpotLight3D). Tuy nhiên, việc này đòi hỏi nhiều thao tác thủ công hơn vì cần lặp lại cho từng node nguồn sáng theo vị trí trong scene để có kết quả tốt.

Trong trường hợp lý tưởng, nên thêm các OmniLight3D bổ sung tại mọi vị trí mà một lượng ánh sáng đáng kể chiếu vào một bề mặt đủ sáng. Tuy nhiên, do giới hạn thời gian, điều này không phải lúc nào cũng khả thi một cách dễ dàng (đặc biệt khi tạo level theo quy trình).

Nếu đang vội, bạn có thể đặt một node OmniLight3D phụ tại cùng vị trí với node OmniLight3D chính. Bạn có thể thêm node này làm node con của OmniLight3D chính để dễ dàng di chuyển và ẩn cả hai node cùng lúc.

Trong node OmniLight3D phụ, hãy thực hiện các thay đổi sau:

- Tăng **Range** của nguồn sáng lên 25-50%. Điều này cho phép nguồn sáng phụ làm sáng những khu vực trước đó không được nguồn sáng ban đầu chiếu tới.
- Đặt **Shadows** thành **Off**. Điều này làm giảm tải hiệu năng của nguồn sáng phụ, đồng thời cho phép các khu vực trong bóng nhận được *some* ánh sáng (đúng với mục đích của chúng ta ở đây).
- Đặt **Energy** bằng 10-40% giá trị ban đầu. Không có giá trị "hoàn hảo", vì vậy hãy thử nghiệm với nhiều giá trị energy khác nhau tùy theo nguồn sáng và môi trường xung quanh.
- Đặt **Specular** thành 0. Ánh sáng gián tiếp không nên tạo ra các vùng specular có thể nhìn thấy, vì vậy chúng ta cần tắt hoàn toàn ánh sáng specular cho nguồn sáng phụ.

Đối với SpotLight3D, có thể sử dụng cùng mẹo này. Trong trường hợp này, OmniLight3D phụ nên được đặt sao cho phản ánh vị trí mà *most* ánh sáng sẽ dội tới. Vị trí này thường gần với vị trí tác động chính của SpotLight3D.

Trong ví dụ bên dưới, một node SpotLight3D được dùng để chiếu sáng sàn phòng. Tuy nhiên, vì không có ánh sáng gián tiếp nên phần còn lại của căn phòng hoàn toàn tối. Trong thực tế, tường và trần phòng sẽ được chiếu sáng bởi ánh sáng dội qua lại. Sử dụng một node OmniLight3D được đặt giữa gốc của SpotLight3D và sàn nhà cho phép mô phỏng hiệu ứng này:

.. image:: img/faking_global_illumination_comparison.webp
