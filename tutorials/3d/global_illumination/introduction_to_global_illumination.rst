.. _doc_introduction_to_global_illumination:

Giới thiệu về global illumination
=================================

Global illumination là gì?
--------------------------

*Global illumination* là thuật ngữ tổng quát dùng để mô tả một hệ thống chiếu sáng sử dụng cả ánh sáng trực tiếp (ánh sáng đến trực tiếp từ nguồn sáng) và ánh sáng gián tiếp (ánh sáng phản xạ từ một bề mặt). Trong một công cụ kết xuất 3D, global illumination là một trong những yếu tố quan trọng nhất để đạt được ánh sáng chân thực. Global illumination nhằm mô phỏng cách ánh sáng hoạt động trong thực tế, chẳng hạn như ánh sáng phản xạ trên các bề mặt và ánh sáng phát ra từ các vật liệu phát sáng.

Trong ví dụ dưới đây, toàn bộ cảnh được chiếu sáng bởi một vật liệu phát sáng (hình vuông màu trắng ở phía trên). Bức tường và trần nhà màu trắng ở phía sau được phủ sắc đỏ và xanh lá khi ở gần các bức tường, vì ánh sáng phản xạ trên những bức tường có màu được phản xạ trở lại phần còn lại của cảnh.

.. image:: img/global_illumination_example.webp

Global illumination bao gồm một số khái niệm chính:

Chiếu sáng khuếch tán gián tiếp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đây là kiểu chiếu sáng không thay đổi tùy theo góc nhìn của camera. Có hai nguồn chính của chiếu sáng khuếch tán gián tiếp:

- Ánh sáng *phản xạ* trên các bề mặt. Ánh sáng phản xạ này được nhân với màu albedo của vật liệu. Sau đó, ánh sáng phản xạ có thể được các bề mặt khác phản xạ tiếp, với mức ảnh hưởng giảm dần do suy hao ánh sáng. Trong thực tế, ánh sáng phản xạ vô số lần. Tuy nhiên, vì lý do hiệu năng, điều này không thể được mô phỏng trong game engine. Thay vào đó, số lần phản xạ thường được giới hạn ở 1 hoặc 2 lần (hoặc tối đa 16 lần khi baking lightmap). Số lần phản xạ lớn hơn sẽ giúp ánh sáng giảm dần trong các vùng đổ bóng trông chân thực hơn, nhưng phải đánh đổi bằng hiệu năng thấp hơn hoặc thời gian bake lâu hơn. - Vật liệu phát sáng cũng có thể phát ra ánh sáng và ánh sáng này có thể phản xạ trên các bề mặt. Đây là một dạng *area lighting*. Thay vì để một điểm có kích thước vô hạn nhỏ phát ra ánh sáng bằng node OmniLight3D hoặc SpotLight3D, một vùng có kích thước xác định sẽ phát ra ánh sáng bằng chính bề mặt của nó.

Chiếu sáng khuếch tán trực tiếp đã được các light node tự xử lý, nghĩa là các thuật toán global illumination chỉ cố gắng biểu diễn ánh sáng gián tiếp.

Các kỹ thuật global illumination khác nhau cung cấp những mức độ chính xác khác nhau để biểu diễn chiếu sáng khuếch tán gián tiếp. Xem bảng so sánh ở cuối trang này để biết thêm thông tin.

Để cung cấp ambient occlusion chính xác hơn cho các vật thể nhỏ, có thể bật screen-space ambient occlusion (SSAO) trong phần cài đặt :ref:`environment <doc_environment_and_post_processing>`. SSAO tiêu tốn hiệu năng đáng kể, vì vậy hãy đảm bảo tắt nó khi nhắm đến phần cứng cấp thấp.

.. note::

    Chiếu sáng khuếch tán gián tiếp có thể là nguyên nhân gây ra hiện tượng color banding trong các cảnh không có texture chi tiết. Điều này khiến các gradient ánh sáng không mượt mà mà thay vào đó có hiệu ứng "bậc thang" rõ rệt. Xem tài liệu
    :ref:`doc_3d_rendering_limitations_color_banding` section in the 3D rendering
    về các giới hạn để biết cách giảm hiệu ứng này.

Chiếu sáng specular
~~~~~~~~~~~~~~~~~~~

Chiếu sáng specular còn được gọi là *phản xạ*. Đây là kiểu chiếu sáng thay đổi cường độ tùy theo góc nhìn của camera. Kiểu chiếu sáng specular này có thể là *trực tiếp* hoặc *gián tiếp*.

Hầu hết các kỹ thuật global illumination đều cung cấp cách kết xuất chiếu sáng specular. Tuy nhiên, độ chính xác khi kết xuất chiếu sáng specular thay đổi rất lớn tùy theo từng kỹ thuật. Xem bảng so sánh ở cuối trang này để biết thêm thông tin.

Để cung cấp phản xạ chính xác hơn cho các vật thể nhỏ, có thể bật screen-space reflections (SSR) trong phần cài đặt :ref:`environment <doc_environment_and_post_processing>`. SSR tiêu tốn hiệu năng đáng kể (thậm chí còn nhiều hơn SSAO), vì vậy hãy đảm bảo tắt nó khi nhắm đến phần cứng cấp thấp.

.. _doc_introduction_to_global_illumination_comparison:

Tôi nên sử dụng kỹ thuật global illumination nào?
-------------------------------------------------

Khi xác định kỹ thuật global illumination (GI) cần sử dụng, có một số tiêu chí cần lưu ý:

- **Hiệu năng.** Các kỹ thuật GI real-time thường tốn kém hơn so với các kỹ thuật semi-real-time hoặc baked. Lưu ý rằng phần lớn chi phí khi kết xuất GI được dành cho GPU thay vì CPU. - **Hình ảnh.** Ngoài việc không đạt hiệu năng tốt nhất, các kỹ thuật GI real-time nhìn chung cũng không tạo ra hình ảnh đẹp nhất. Điều này đặc biệt đúng trong một cảnh phần lớn là tĩnh, nơi tính động của GI real-time không dễ nhận thấy. Nếu mục tiêu của bạn là tối đa hóa chất lượng hình ảnh, các kỹ thuật baked thường sẽ trông đẹp hơn và tạo ra ít light leak hơn. - **Khả năng real-time.** Một số kỹ thuật GI hoàn toàn real-time, trong khi những kỹ thuật khác chỉ semi-real-time hoặc hoàn toàn không real-time. Các kỹ thuật semi-real-time có những hạn chế mà các kỹ thuật hoàn toàn real-time không có. Ví dụ, các vật thể động có thể không đóng góp ánh sáng phát xạ cho cảnh. Các kỹ thuật không real-time không hỗ trợ *bất kỳ* dạng GI động nào, vì vậy nếu cần, phải giả lập bằng các kỹ thuật khác (chẳng hạn như đặt các positional light gần các bề mặt phát sáng). Khả năng real-time cũng ảnh hưởng đến tính phù hợp của kỹ thuật GI trong các level được tạo theo thủ tục. - **Công sức cần thiết từ người dùng.** Một số kỹ thuật GI hoàn toàn tự động, trong khi những kỹ thuật khác đòi hỏi người dùng phải lập kế hoạch cẩn thận và thực hiện công việc thủ công. Tùy vào quỹ thời gian, một số kỹ thuật GI có thể phù hợp hơn những kỹ thuật khác.

Dưới đây là bảng so sánh tất cả các kỹ thuật global illumination có trong Godot:

Hiệu năng
~~~~~~~~~

Theo thứ tự hiệu năng từ nhanh nhất đến chậm nhất:

- **ReflectionProbe:**

  - ReflectionProbe với chế độ cập nhật được đặt thành **Always** tốn kém hơn nhiều so với probe có chế độ cập nhật được đặt thành **Once** (mặc định). Phù hợp với đồ họa tích hợp khi sử dụng chế độ cập nhật **Once**. *Có trong tất cả renderer.*

- **LightmapGI:**

  - Có thể bake light chỉ với ánh sáng gián tiếp, hoặc bake hoàn toàn theo từng light để cải thiện hiệu năng hơn nữa. Có thể sử dụng các thiết lập hybrid (chẳng hạn như có một directional light real-time và các positional light được bake hoàn toàn). Có thể bật thông tin hướng trước khi bake để cải thiện hình ảnh với một chi phí hiệu năng nhỏ (và phải đánh đổi bằng kích thước tệp lớn hơn). Phù hợp với đồ họa tích hợp. *Có trong tất cả renderer. Tuy nhiên, baking lightmap yêu cầu phần cứng hỗ trợ RenderingDevice.*

- **VoxelGI:**

  - Có thể điều chỉnh số lượng subdivision của quá trình bake để cân bằng giữa hiệu năng và chất lượng. Có thể điều chỉnh chất lượng kết xuất VoxelGI trong Project Settings. Tùy chọn kết xuất ở một nửa độ phân giải (sau đó scale tuyến tính) để cải thiện đáng kể hiệu năng. **Không khả dụng** *khi sử dụng Mobile hoặc Compatibility renderer.*

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):**

  - Có thể điều chỉnh chất lượng SSIL và số lần blur pass trong Project Settings. Theo mặc định, quá trình kết xuất SSIL được thực hiện ở một nửa độ phân giải (sau đó scale tuyến tính) để đảm bảo mức hiệu năng hợp lý. **Không khả dụng** *khi sử dụng Mobile hoặc Compatibility renderer.*

- **SDFGI:**

  - Có thể điều chỉnh số lượng cascade để cân bằng giữa hiệu năng và chất lượng. Có thể điều chỉnh số lượng ray được phát mỗi frame trong Project Settings. Tùy chọn kết xuất ở một nửa độ phân giải (sau đó scale tuyến tính) để cải thiện đáng kể hiệu năng. **Không khả dụng** *khi sử dụng Mobile hoặc Compatibility renderer.*

Hình ảnh
~~~~~~~~

Để so sánh, đây là một cảnh 3D không sử dụng tùy chọn global illumination nào:

.. figure:: img/gi_none.webp
   :alt: A 3D scene without any form of global illumination (only constant environment lighting). The box and sphere near the camera are both dynamic objects.

   A 3D scene without any form of global illumination (only constant environment lighting). The box and sphere near the camera are both dynamic objects.

Dưới đây là cách các kỹ thuật global illumination khác nhau của Godot so sánh với nhau:

- **VoxelGI:** |average| Phản xạ và ánh sáng gián tiếp tốt, nhưng hãy cẩn thận với light leak.

  - Do bản chất dựa trên voxel, VoxelGI sẽ xuất hiện light leak nếu tường và sàn quá mỏng. Bạn nên đảm bảo tất cả các bề mặt đặc có độ dày ít nhất bằng một voxel.

    Các lỗi dạng vệt cũng có thể xuất hiện trên những bề mặt dốc. Trong trường hợp này, điều chỉnh các thuộc tính bias hoặc xoay node VoxelGI có thể giúp khắc phục.

    .. figure:: img/gi_voxel_gi.webp
       :alt: VoxelGI in action.

       VoxelGI in action.

- **SDFGI:** |average| Phản xạ và ánh sáng gián tiếp tốt, nhưng hãy cẩn thận với light leak và hiện tượng cascade dịch chuyển rõ rệt.

  - Mức độ chi tiết của GI thay đổi tùy theo khoảng cách giữa camera và bề mặt.

    Có thể giảm đáng kể light leak bằng cách bật thuộc tính **Use Occlusion**. Tính năng này tiêu tốn một lượng nhỏ hiệu năng, nhưng thường tạo ra ít light leak hơn so với VoxelGI.

    Cascade dịch chuyển có thể nhìn thấy khi camera di chuyển nhanh. Có thể làm hiện tượng này ít rõ rệt hơn bằng cách điều chỉnh kích thước cascade hoặc sử dụng fog.

    .. figure:: img/gi_sdfgi.webp
       :alt: SDFGI in action.

       SDFGI in action.

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):** |average| Nguồn chiếu sáng gián tiếp *thứ cấp* tốt, nhưng không có phản xạ.

  - SSIL được thiết kế để sử dụng bổ trợ cho một kỹ thuật GI khác như VoxelGI, SDFGI hoặc LightmapGI. SSIL hoạt động tốt nhất với các chi tiết quy mô nhỏ, vì bản thân nó không thể cung cấp ánh sáng gián tiếp chính xác cho các cấu trúc lớn. SSIL có thể cung cấp ánh sáng gián tiếp real-time trong những tình huống mà các kỹ thuật GI khác không thể nắm bắt các chi tiết quy mô nhỏ hoặc các vật thể động. Bản chất trong không gian màn hình của nó sẽ tạo ra một số lỗi, đặc biệt khi các vật thể đi vào hoặc rời khỏi màn hình. SSIL hoạt động bằng màu của frame trước (trước bước post-processing), nghĩa là các decal phát sáng và shader tùy chỉnh cũng được bao gồm (miễn là chúng xuất hiện trên màn hình).

    .. figure:: img/gi_ssil_only.webp
       :alt: SSIL in action (without any other GI technique). Notice the emissive lighting around the yellow box.

       SSIL in action (without any other GI technique). Notice the emissive lighting around the yellow box.

- **LightmapGI:** |good| Ánh sáng gián tiếp tuyệt vời, phản xạ khá tốt (tùy chọn).

  - Đây là kỹ thuật duy nhất cho phép tăng số lần ánh sáng nảy lên trên 2 (tối đa 16). Khi bật thông tin định hướng, spherical harmonics (SH) được sử dụng để tạo ra các phản xạ mờ.

    .. figure:: img/gi_lightmap_gi_indirect_only.webp
       :alt: LightmapGI in action. Only indirect lighting is baked here, but direct light can also be baked.

       LightmapGI in action. Only indirect lighting is baked here, but direct light can also be baked.

- **ReflectionProbe:** |average| Phản xạ tốt nhưng chiếu sáng gián tiếp kém.

  - Có thể tắt chiếu sáng gián tiếp, đặt thành một màu cố định lan tỏa khắp probe hoặc tự động đọc từ môi trường của probe (và áp dụng dưới dạng cubemap). Về cơ bản, cơ chế này hoạt động như ánh sáng môi trường cục bộ. Phản xạ và chiếu sáng gián tiếp được hòa trộn với các probe lân cận khác.

    .. figure:: img/gi_none_reflection_probe.webp
       :alt: ReflectionProbe in action (without any other GI technique). Notice the reflective sphere.

       ReflectionProbe in action (without any other GI technique). Notice the reflective sphere.

Khả năng hoạt động theo thời gian thực
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **VoxelGI:** |good| Hoàn toàn theo thời gian thực.

  - Chiếu sáng gián tiếp và phản xạ hoàn toàn theo thời gian thực. Các đối tượng động có thể nhận GI *và* đóng góp vào GI thông qua các bề mặt phát sáng của chúng. Shader tùy chỉnh cũng có thể phát ra ánh sáng riêng, và ánh sáng đó sẽ được phát ra một cách chính xác.

    Phù hợp với các level được tạo theo thủ tục *nếu chúng được tạo trước* (không phải trong lúc chơi). Quá trình baking cần vài giây trở lên để hoàn tất, nhưng có thể thực hiện từ cả editor lẫn project đã export.

- **SDFGI:** |average| Bán thời gian thực.

  - Các cascade được tạo theo thời gian thực, khiến SDFGI phù hợp với các level được tạo theo thủ tục (kể cả khi cấu trúc được tạo trong lúc chơi).

    Các đối tượng động có thể *nhận* GI nhưng không thể *đóng góp* vào GI. Ánh sáng phát xạ chỉ cập nhật khi một đối tượng đi vào một cascade, vì vậy cơ chế này vẫn có thể hoạt động với các đối tượng di chuyển chậm.

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):** |good| Hoàn toàn theo thời gian thực.

  - SSIL hoạt động với cả ánh sáng tĩnh và động. Nó cũng hoạt động với cả các vật chắn tĩnh và động (bao gồm cả vật liệu phát sáng).

- **LightmapGI:** |bad| Được bake và do đó không hoạt động theo thời gian thực.

  - Cả chiếu sáng gián tiếp và phản xạ SH đều được bake và không thể thay đổi trong runtime. GI theo thời gian thực phải được
    :ref:`simulated via other means <doc_faking_global_illumination>`,
    chẳng hạn như các đèn định vị theo thời gian thực. Các đối tượng động nhận chiếu sáng gián tiếp thông qua light probe, có thể được tự động đặt hoặc do người dùng đặt thủ công (node LightmapProbe). Không phù hợp với các level được tạo theo thủ tục, vì chỉ có thể bake lightmap từ editor.

- **ReflectionProbe:** |average| Tùy chọn theo thời gian thực.

  - Theo mặc định, phản xạ được cập nhật khi probe được di chuyển. Chúng được cập nhật thường xuyên nhất có thể nếu chế độ cập nhật được đặt thành **Always** (tốn nhiều tài nguyên).

  - Người dùng phải cấu hình thủ công chiếu sáng gián tiếp, nhưng có thể thay đổi trong runtime mà không gây ra phép tính tốn kém nào chạy ngầm. Điều này khiến ReflectionProbe phù hợp với các level được tạo theo thủ tục.

Công việc cần thực hiện
~~~~~~~~~~~~~~~~~~~~~~~

- **VoxelGI:** Cần tạo và bake một hoặc nhiều node VoxelGI.

  - Cần điều chỉnh đúng phạm vi để đạt kết quả tốt. Ngoài ra, xoay node rồi bake lại có thể giúp khắc phục hiện tượng rò rỉ hoặc các artifact dạng vệt trong một số trường hợp. Thời gian bake nhanh – thường dưới 10 giây đối với một scene có độ phức tạp trung bình.

- **SDFGI:** Rất ít.

  - SDFGI hoàn toàn tự động; chỉ cần bật nó trong resource Environment. Công việc thủ công duy nhất cần thực hiện là đặt đúng thuộc tính bake mode của MeshInstances. Không cần tạo node và cũng không cần bake.

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):** Rất ít.

  - SSIL hoàn toàn tự động; chỉ cần bật nó trong resource Environment. Không cần tạo node và cũng không cần bake.

- **LightmapGI:** Cần thiết lập UV2 và bake.

  - Các mesh tĩnh phải được reimport với UV2 và bật tính năng tạo lightmap. Trên GPU chuyên dụng, thời gian bake tương đối nhanh nhờ tính năng baking lightmap dựa trên GPU – thường dưới 1 phút đối với một scene có độ phức tạp trung bình.

- **ReflectionProbe:** Do người dùng đặt thủ công.

.. |good| image:: img/score_good.webp

.. |average| image:: img/score_average.webp

.. |bad| image:: img/score_bad.webp

Tóm tắt
~~~~~~~

Nếu bạn không chắc nên sử dụng kỹ thuật GI nào:

- Đối với game desktop, bạn nên bắt đầu với :ref:`SDFGI <doc_using_sdfgi>` trước vì kỹ thuật này yêu cầu ít công đoạn thiết lập nhất. Sau đó chuyển sang các kỹ thuật GI khác nếu cần. Để cải thiện hiệu năng trên GPU cấp thấp và đồ họa tích hợp, hãy cân nhắc thêm tùy chọn tắt SDFGI hoặc :ref:`VoxelGI <doc_using_voxel_gi>` trong phần cài đặt game. Có thể tắt SDFGI trong resource Environment và tắt VoxelGI bằng cách ẩn các node VoxelGI. Để cải thiện hình ảnh hơn nữa trên các cấu hình cao cấp, hãy thêm tùy chọn bật SSIL trong phần cài đặt game. - Đối với game mobile, :ref:`LightmapGI <doc_using_lightmap_gi>` và
  :ref:`ReflectionProbes <doc_reflection_probes>` are the only supported options.
  Xem thêm :ref:`doc_introduction_to_global_illumination_alternatives`.

.. seealso::

    Bạn có thể so sánh các kỹ thuật global illumination trong thực tế bằng `Global Illumination demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/global_illumination>`__.

.. _doc_introduction_to_global_illumination_gi_mode_recommendations:

Tôi nên sử dụng chế độ global illumination nào trên mesh và đèn?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bất kể bạn sử dụng kỹ thuật global illumination nào, không có chế độ global illumination nào "tốt hơn" một cách tuyệt đối. Tuy vậy, dưới đây là một số khuyến nghị cho mesh:

- Đối với hình học tĩnh của level, hãy sử dụng chế độ global illumination **Static** *(mặc định)*. - Đối với hình học động nhỏ và người chơi/kẻ địch, hãy sử dụng chế độ global illumination **Disabled**. Hình học động nhỏ sẽ không thể đóng góp một lượng chiếu sáng gián tiếp đáng kể vì hình học này nhỏ hơn một voxel. Nếu cần chiếu sáng gián tiếp cho các đối tượng động nhỏ, bạn có thể mô phỏng bằng node OmniLight3D hoặc SpotLight3D được làm node cha của đối tượng. - Đối với hình học động *lớn* của level (chẳng hạn như một đoàn tàu đang di chuyển), hãy sử dụng chế độ global illumination **Dynamic**. Lưu ý rằng chế độ này chỉ có tác dụng với VoxelGI, vì SDFGI và LightmapGI không hỗ trợ global illumination với các đối tượng động.

Dưới đây là một số khuyến nghị cho các chế độ light bake:

- Đối với ánh sáng tĩnh của level, hãy sử dụng chế độ bake **Static**. Chế độ **Static** cũng phù hợp với các đèn động không thay đổi nhiều trong lúc chơi, chẳng hạn như ngọn đuốc nhấp nháy. - Đối với các hiệu ứng động có thời gian tồn tại ngắn (chẳng hạn như vũ khí), hãy sử dụng chế độ bake **Disabled** để cải thiện hiệu năng. - Đối với các hiệu ứng động có thời gian tồn tại dài (chẳng hạn như đèn cảnh báo xoay), hãy sử dụng chế độ bake **Dynamic** để cải thiện chất lượng *(mặc định)*. Lưu ý rằng chế độ này chỉ có tác dụng với VoxelGI và SDFGI, vì LightmapGI không hỗ trợ global illumination với các đèn động.

.. _doc_introduction_to_global_illumination_alternatives:

Các lựa chọn thay thế cho kỹ thuật GI
-------------------------------------

Nếu không kỹ thuật GI nào được đề cập ở trên phù hợp, bạn vẫn có thể
:ref:`simulate GI by placing additional lights manually <doc_faking_global_illumination>`.
Cách tiếp cận này cần nhiều công việc thủ công hơn, nhưng có thể mang lại hiệu năng *và* hình ảnh tốt nếu được thực hiện đúng cách. Cho đến nay, cách tiếp cận này vẫn được sử dụng trong nhiều game hiện đại.

Khi nhắm đến phần cứng cấp thấp trong các trường hợp không thể sử dụng LightmapGI (chẳng hạn như các level được tạo theo thủ tục), chỉ dựa vào ánh sáng môi trường hoặc một hệ số ánh sáng môi trường cố định có thể là điều cần thiết. Điều này có thể khiến hình ảnh phẳng hơn, nhưng việc điều chỉnh màu ánh sáng môi trường và mức đóng góp của bầu trời vẫn cho phép đạt được kết quả chấp nhận được trong hầu hết trường hợp.
