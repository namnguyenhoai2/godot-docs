.. _doc_faking_global_illumination:

Giả lập chiếu sáng toàn cục
===========================

Tại sao phải giả lập chiếu sáng toàn cục?
-----------------------------------------

Godot cung cấp một số kỹ thuật chiếu sáng toàn cục (GI), mỗi kỹ thuật đều có ưu điểm và nhược điểm riêng. Tuy vậy, bạn vẫn có thể không sử dụng bất kỳ kỹ thuật GI nào mà thay vào đó dùng một phương pháp tự xây dựng. Có một số lý do để sử dụng phương pháp "tự xây dựng" cho chiếu sáng toàn cục thay vì VoxelGI, SDFGI hoặc lightmap được bake:

- Bạn cần hiệu năng rendering tốt nhưng không thể thực hiện quy trình bake lightmap vốn có thể khá rườm rà. - Bạn cần một phương pháp GI hoàn toàn real-time *và* hoạt động trong các level được tạo theo thủ tục. - Bạn cần một phương pháp GI hoàn toàn real-time *và* không bị rò rỉ ánh sáng đáng kể.

Các phương pháp được mô tả dưới đây chỉ bao quát ánh sáng khuếch tán gián tiếp, không bao gồm ánh sáng specular. Đối với ánh sáng specular, hãy cân nhắc sử dụng ReflectionProbes, vốn thường đủ nhẹ để dùng kết hợp với phương pháp GI giả lập này.

.. seealso::

    Không chắc việc giả lập chiếu sáng toàn cục bằng các light có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI có trong Godot 4.

Giả lập chiếu sáng toàn cục bằng DirectionalLight3D
---------------------------------------------------

Mặc dù sky cung cấp ánh sáng định hướng riêng, node DirectionalLight3D chính của scene thường phát ra một lượng ánh sáng lớn. Khi sử dụng một kỹ thuật GI, ánh sáng này sẽ được phản xạ trên các bề mặt đặc và dội lại trên hầu hết các bề mặt ngoài trời có bóng.

Chúng ta có thể giả lập điều này bằng cách thêm một node DirectionalLight3D thứ hai với các thay đổi sau:

- Xoay light 180 độ. Điều này cho phép nó đại diện cho ánh sáng dội lại từ node DirectionalLight3D chính. - Đặt **Shadows** thành **Off**. Điều này làm giảm chi phí hiệu năng của light thứ cấp, đồng thời cho phép các khu vực có bóng nhận được *một phần* ánh sáng (đây chính là điều chúng ta muốn ở đây). - Đặt **Energy** bằng 10-40% giá trị ban đầu. Không có giá trị nào là "hoàn hảo", vì vậy hãy thử nghiệm với nhiều giá trị energy khác nhau tùy theo light và màu vật liệu thường dùng của bạn. - Đặt **Specular** thành ``0.0``. Ánh sáng gián tiếp không nên phát ra các vùng specular có thể nhìn thấy, vì vậy chúng ta cần tắt hoàn toàn ánh sáng specular cho light thứ cấp.

.. note::

    Phương pháp này hiệu quả nhất trong các scene chủ yếu ở ngoài trời. Khi đi vào trong nhà, ánh sáng của DirectionalLight3D thứ cấp vẫn sẽ nhìn thấy được vì light này đã tắt shadow.

    Có thể khắc phục điều này bằng cách giảm dần Energy của DirectionalLight3D thứ cấp khi đi vào khu vực trong nhà (và thực hiện ngược lại khi rời khỏi khu vực trong nhà). Chẳng hạn, bạn có thể thực hiện việc này bằng node Area3D và AnimationPlayer.

Giả lập chiếu sáng toàn cục bằng positional light
-------------------------------------------------

Có thể áp dụng cùng phương pháp như với DirectionalLight3D cho các positional light (OmniLight3D và SpotLight3D). Tuy nhiên, việc này đòi hỏi nhiều thao tác thủ công hơn, vì cần lặp lại quy trình cho từng positional light node trong scene để đạt kết quả tốt.

Trong trường hợp lý tưởng, nên thêm các OmniLight3D bổ sung tại mọi vị trí mà một lượng ánh sáng đáng kể chiếu lên một bề mặt đủ sáng. Tuy nhiên, do hạn chế về thời gian, điều này không phải lúc nào cũng dễ thực hiện (đặc biệt khi tạo level theo thủ tục).

Nếu đang vội, bạn có thể đặt một node OmniLight3D thứ cấp tại cùng vị trí với node OmniLight3D chính. Bạn có thể thêm node này làm child của node OmniLight3D chính để dễ dàng di chuyển và ẩn cả hai node cùng lúc.

Trong node OmniLight3D thứ cấp, hãy thực hiện các thay đổi sau:

- Tăng **Range** của light lên 25-50%. Điều này cho phép light thứ cấp chiếu sáng những khu vực trước đó không được light ban đầu chiếu tới. - Đặt **Shadows** thành **Off**. Điều này làm giảm chi phí hiệu năng của light thứ cấp, đồng thời cho phép các khu vực có bóng nhận được *một phần* ánh sáng (đây chính là điều chúng ta muốn ở đây). - Đặt **Energy** bằng 10-40% giá trị ban đầu. Không có giá trị nào là "hoàn hảo", vì vậy hãy thử nghiệm với nhiều giá trị energy khác nhau tùy theo light và môi trường xung quanh. - Đặt **Specular** thành 0. Ánh sáng gián tiếp không nên phát ra các vùng specular có thể nhìn thấy, vì vậy chúng ta cần tắt hoàn toàn ánh sáng specular cho light thứ cấp.

Có thể sử dụng thủ thuật tương tự cho SpotLight3D. Trong trường hợp này, OmniLight3D thứ cấp nên được đặt sao cho phản ánh vị trí mà *phần lớn* ánh sáng sẽ dội tới. Vị trí này thường ở gần vị trí tác động chính của SpotLight3D.

Trong ví dụ dưới đây, một node SpotLight3D được dùng để chiếu sáng sàn của căn phòng. Tuy nhiên, vì không có ánh sáng gián tiếp nên phần còn lại của căn phòng vẫn hoàn toàn tối. Trong thực tế, tường và trần phòng sẽ được chiếu sáng nhờ ánh sáng dội qua lại. Sử dụng một node OmniLight3D được đặt giữa điểm gốc của SpotLight3D và sàn cho phép mô phỏng hiệu ứng này:

.. image:: img/faking_global_illumination_comparison.webp
