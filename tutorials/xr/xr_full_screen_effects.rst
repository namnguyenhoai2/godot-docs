.. _doc_xr_full_screen_effects:

Các hiệu ứng toàn màn hình XR
=============================

Khi thêm các hiệu ứng toàn màn hình tùy chỉnh vào ứng dụng XR, một cách tiếp cận là sử dụng một full screen quad và áp dụng các hiệu ứng vào shader của quad đó. Thêm một node :ref:`MeshInstance3D <class_MeshInstance3D>` vào scene dưới dạng node con của :ref:`XRCamera3D <class_XRCamera3D>`, rồi đặt thuộc tính ``mesh`` thành một :ref:`QuadMesh <class_QuadMesh>`. Đặt chiều rộng và chiều cao của quad thành ``2``.

.. image:: img/xr_full_screen_effects_starting_quad.webp

Sau đó, bạn có thể thêm một shader vào quad để làm cho nó bao phủ màn hình. Thực hiện việc này bằng cách đặt built-in ``POSITION`` của vertex shader thành ``vec4(VERTEX.xy, 1.0, 1.0)``. Tuy nhiên, khi tạo một hiệu ứng được căn giữa thẳng phía trước trong tầm nhìn của người dùng (chẳng hạn như hiệu ứng vignette), kết quả cuối cùng có thể trông không chính xác trong XR.

Bên dưới là các ảnh chụp chế độ xem mắt phải với shader vignette, lần lượt từ headset và chính render target. Các ảnh bên trái sử dụng shader chưa được sửa đổi; các ảnh bên phải điều chỉnh full screen quad bằng projection matrix. Mặc dù ảnh chụp bên trái được căn giữa trong render target, nó lại lệch tâm trong chế độ xem của headset. Nhưng sau khi áp dụng projection matrix, chúng ta thấy hiệu ứng được căn giữa ngay trong headset.

.. image:: img/xr_full_screen_effects_vignette_before_after.webp

Áp dụng projection matrix
-------------------------

Để căn giữa hiệu ứng một cách chính xác, ``POSITION`` của full screen quad cần tính đến trường nhìn bất đối xứng. Để thực hiện việc này đồng thời bảo đảm quad bao phủ toàn bộ render target, chúng ta có thể chia nhỏ quad và áp dụng projection matrix vào các đỉnh bên trong. Hãy tăng chiều rộng và chiều sâu subdivision của quad.

.. image:: img/xr_full_screen_effects_ending_quad.webp

Sau đó, trong vertex function của shader, chúng ta áp dụng một offset từ projection matrix vào các đỉnh bên trong. Dưới đây là ví dụ về cách bạn có thể thực hiện việc này với shader vignette đơn giản ở trên:

.. code-block:: glsl

  shader_type spatial;
  render_mode depth_test_disabled, skip_vertex_transform, unshaded, cull_disabled;

  // Sửa đổi VERTEX.xy bằng projection matrix để căn giữa hiệu ứng một cách chính xác.
  void vertex() {
	  vec2 vert_pos = VERTEX.xy;

	  if (length(vert_pos) < 0.99) {
		  vec4 offset = PROJECTION_MATRIX * vec4(0.0, 0.0, 1.0, 1.0);
		  vert_pos += (offset.xy / offset.w);
	  }

	  POSITION = vec4(vert_pos, 1.0, 1.0);
  }

  void fragment() {
	  ALBEDO = vec3(0.0);
	  ALPHA = dot(UV * 2.0 - 1.0, UV * 2.0 - 1.0) * 2.0;
  }


.. note:: For more info on asymmetric FOV and its purpose, see this
          `Meta Asymmetric Field of View FAQ <https://developers.meta.com/horizon/documentation/unity/unity-asymmetric-fov-faq/>`_.

Giới hạn
--------

Phương pháp hiệu ứng toàn màn hình này không gây lo ngại về hiệu năng đối với các hiệu ứng theo từng pixel như shader vignette ở trên. Tuy nhiên, không nên đọc từ screen texture khi sử dụng kỹ thuật này. Các hiệu ứng toàn màn hình yêu cầu đọc từ screen texture sẽ vô hiệu hóa hiệu quả tất cả các tối ưu hóa hiệu năng rendering trong XR. Điều này là do khi đọc từ screen texture, Godot tạo một bản sao đầy đủ của render buffer; việc này làm tăng đáng kể khối lượng công việc của GPU và có thể gây ra các vấn đề về hiệu năng.
