.. _doc_introduction_to_global_illumination:

Giới thiệu về chiếu sáng toàn cục
=================================

Chiếu sáng toàn cục là gì?
--------------------------

*Chiếu sáng toàn cục* là thuật ngữ chung dùng để mô tả một hệ thống chiếu sáng sử dụng cả ánh sáng trực tiếp (ánh sáng đi thẳng từ nguồn sáng) và ánh sáng gián tiếp (ánh sáng dội lại từ một bề mặt). Trong một công cụ kết xuất 3D, chiếu sáng toàn cục là một trong những yếu tố quan trọng nhất để đạt được ánh sáng chân thực. Chiếu sáng toàn cục nhằm mô phỏng cách ánh sáng hoạt động trong đời thực, chẳng hạn như ánh sáng dội trên các bề mặt và ánh sáng phát ra từ các vật liệu phát sáng.

Trong ví dụ bên dưới, toàn bộ cảnh được chiếu sáng bởi một vật liệu phát sáng (hình vuông màu trắng ở phía trên). Bức tường trắng và trần nhà ở phía sau được nhuộm màu đỏ và xanh lục khi ở gần các bức tường, vì ánh sáng dội trên những bức tường có màu được phản xạ trở lại phần còn lại của cảnh.

.. image:: img/global_illumination_example.webp

Chiếu sáng toàn cục bao gồm một số khái niệm chính:

Chiếu sáng khuếch tán gián tiếp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đây là loại ánh sáng không thay đổi tùy theo góc nhìn của camera. Có hai nguồn chính của chiếu sáng khuếch tán gián tiếp:

- Ánh sáng *dội* trên các bề mặt. Ánh sáng dội này được nhân với màu albedo của vật liệu. Sau đó, ánh sáng dội có thể được các bề mặt khác phản xạ, với mức ảnh hưởng giảm dần do sự suy hao ánh sáng. Trong đời thực, ánh sáng dội lại vô số lần. Tuy nhiên, vì lý do hiệu năng, điều này không thể được mô phỏng trong game engine. Thay vào đó, số lần dội thường được giới hạn ở 1 hoặc 2 lần (hoặc tối đa 16 lần khi baking lightmap). Số lần dội lớn hơn sẽ tạo ra sự suy giảm ánh sáng chân thực hơn trong các vùng đổ bóng, nhưng phải đánh đổi bằng hiệu năng thấp hơn hoặc thời gian baking lâu hơn.
- Vật liệu phát sáng cũng có thể phát ra ánh sáng và ánh sáng đó có thể dội trên các bề mặt. Đây là một dạng *area lighting*. Thay vì để một điểm có kích thước vô hạn nhỏ phát ra ánh sáng bằng node OmniLight3D hoặc SpotLight3D, một vùng có kích thước xác định sẽ phát ra ánh sáng bằng chính bề mặt của nó.

Chiếu sáng khuếch tán trực tiếp đã được chính các node ánh sáng xử lý, nghĩa là các thuật toán chiếu sáng toàn cục chỉ cố gắng mô phỏng ánh sáng gián tiếp.

Các kỹ thuật chiếu sáng toàn cục khác nhau cung cấp mức độ chính xác khác nhau để mô phỏng chiếu sáng khuếch tán gián tiếp. Xem bảng so sánh ở cuối trang này để biết thêm thông tin.

Để cung cấp ambient occlusion chính xác hơn cho các vật thể nhỏ, có thể bật screen-space ambient occlusion (SSAO) trong phần cài đặt :ref:`environment <doc_environment_and_post_processing>`. SSAO gây tốn hiệu năng đáng kể, vì vậy hãy nhớ tắt nó khi nhắm đến phần cứng cấp thấp.

.. note::

    Chiếu sáng khuếch tán gián tiếp có thể là nguồn gây ra hiện tượng color banding trong các cảnh không có texture chi tiết. Điều này khiến các dải chuyển màu của ánh sáng không mượt mà mà xuất hiện hiệu ứng "bậc thang" rõ rệt. Xem
    :ref:`doc_3d_rendering_limitations_color_banding` phần trong tài liệu về các giới hạn của kết xuất 3D để biết cách giảm hiệu ứng này.

Chiếu sáng specular
~~~~~~~~~~~~~~~~~~~

Chiếu sáng specular còn được gọi là *phản xạ*. Đây là loại ánh sáng thay đổi cường độ tùy theo góc nhìn của camera. Chiếu sáng specular này có thể là *trực tiếp* hoặc *gián tiếp*.

Hầu hết các kỹ thuật chiếu sáng toàn cục đều cung cấp cách kết xuất chiếu sáng specular. Tuy nhiên, mức độ chính xác khi kết xuất chiếu sáng specular thay đổi rất lớn giữa các kỹ thuật. Xem bảng so sánh ở cuối trang này để biết thêm thông tin.

Để cung cấp phản xạ chính xác hơn cho các vật thể nhỏ, có thể bật screen-space reflections (SSR) trong phần cài đặt :ref:`environment <doc_environment_and_post_processing>`. SSR gây tốn hiệu năng đáng kể (thậm chí còn nhiều hơn SSAO), vì vậy hãy nhớ tắt nó khi nhắm đến phần cứng cấp thấp.

.. _doc_introduction_to_global_illumination_comparison:

Nên sử dụng kỹ thuật chiếu sáng toàn cục nào?
---------------------------------------------

Khi xác định kỹ thuật chiếu sáng toàn cục (GI) cần sử dụng, có một số tiêu chí cần lưu ý:

- **Hiệu năng.** Các kỹ thuật GI theo thời gian thực thường tốn kém hơn so với các kỹ thuật bán thời gian thực hoặc đã baking. Lưu ý rằng phần lớn chi phí kết xuất GI nằm ở GPU thay vì CPU.
- **Hình ảnh.** Ngoài việc không có hiệu năng tốt nhất, các kỹ thuật GI theo thời gian thực thường cũng không cung cấp đầu ra hình ảnh tốt nhất. Điều này đặc biệt đúng với các cảnh phần lớn tĩnh, trong đó tính động của GI theo thời gian thực khó nhận thấy. Nếu mục tiêu của bạn là tối đa hóa chất lượng hình ảnh, các kỹ thuật đã baking thường sẽ trông đẹp hơn và tạo ra ít light leak hơn.
- **Khả năng theo thời gian thực.** Một số kỹ thuật GI hoàn toàn theo thời gian thực, trong khi các kỹ thuật khác chỉ bán thời gian thực hoặc hoàn toàn không theo thời gian thực. Các kỹ thuật bán thời gian thực có những hạn chế mà các kỹ thuật hoàn toàn theo thời gian thực không có. Chẳng hạn, các vật thể động có thể không đóng góp ánh sáng phát ra cho cảnh. Các kỹ thuật không theo thời gian thực không hỗ trợ bất kỳ dạng GI động *nào*, vì vậy nếu cần, phải giả lập bằng các kỹ thuật khác (chẳng hạn như đặt các đèn định vị gần các bề mặt phát sáng). Khả năng theo thời gian thực cũng ảnh hưởng đến tính khả thi của kỹ thuật GI trong các level được tạo theo thủ tục.
- **Công việc người dùng cần thực hiện.** Một số kỹ thuật GI hoàn toàn tự động, trong khi các kỹ thuật khác yêu cầu người dùng lên kế hoạch cẩn thận và thực hiện thủ công. Tùy thuộc vào quỹ thời gian của bạn, một số kỹ thuật GI có thể phù hợp hơn các kỹ thuật khác.

Dưới đây là phần so sánh tất cả các kỹ thuật chiếu sáng toàn cục có trong Godot:

Hiệu năng
~~~~~~~~~

Theo thứ tự hiệu năng từ nhanh nhất đến chậm nhất:

- **ReflectionProbe:**

  - ReflectionProbes có chế độ cập nhật được đặt thành **Always** tốn kém hơn nhiều so với các probe có chế độ cập nhật được đặt thành **Once** (mặc định). Phù hợp với đồ họa tích hợp khi sử dụng chế độ cập nhật **Once**. *Có trong tất cả các renderer.*

- **LightmapGI:**

  - Có thể baking ánh sáng chỉ với ánh sáng gián tiếp, hoặc baking hoàn toàn theo từng đèn để cải thiện hiệu năng hơn nữa. Có thể sử dụng các thiết lập kết hợp (chẳng hạn như một đèn directional theo thời gian thực và các đèn positional được baking hoàn toàn). Có thể bật thông tin directional trước khi baking để cải thiện hình ảnh với một mức đánh đổi nhỏ về hiệu năng (và làm tăng kích thước tệp). Phù hợp với đồ họa tích hợp. *Có trong tất cả các renderer. Tuy nhiên, việc baking lightmap yêu cầu phần cứng hỗ trợ RenderingDevice.*

- **VoxelGI:**

  - Có thể điều chỉnh số lần subdivision khi baking để cân bằng giữa hiệu năng và chất lượng. Có thể điều chỉnh chất lượng kết xuất VoxelGI trong Project Settings. Có thể tùy chọn thực hiện kết xuất ở một nửa độ phân giải (sau đó scale tuyến tính) để cải thiện đáng kể hiệu năng. **Không khả dụng** *khi sử dụng renderer Mobile hoặc Compatibility.*

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):**

  - Có thể điều chỉnh chất lượng SSIL và số lượt làm mờ trong Project Settings. Theo mặc định, việc kết xuất SSIL được thực hiện ở một nửa độ phân giải (sau đó được thu phóng tuyến tính) để đảm bảo hiệu năng ở mức hợp lý. **Không khả dụng** *khi sử dụng các renderer Mobile hoặc Compatibility.*

- **SDFGI:**

  - Có thể điều chỉnh số cascade để cân bằng hiệu năng và chất lượng. Có thể điều chỉnh số tia được phát trong mỗi khung hình trong Project Settings. Có thể tùy chọn thực hiện việc kết xuất ở một nửa độ phân giải (sau đó được thu phóng tuyến tính) để cải thiện đáng kể hiệu năng. **Không khả dụng** *khi sử dụng các renderer Mobile hoặc Compatibility.*

Hình ảnh
~~~~~~~~

Để so sánh, dưới đây là một cảnh 3D không sử dụng tùy chọn global illumination nào:

.. figure:: img/gi_none.webp
   :alt: Một cảnh 3D không có bất kỳ dạng global illumination nào (chỉ có ánh sáng môi trường cố định). Hộp và hình cầu gần camera đều là các đối tượng động.

   Một cảnh 3D không có bất kỳ dạng global illumination nào (chỉ có ánh sáng môi trường cố định). Hộp và hình cầu gần camera đều là các đối tượng động.

Dưới đây là so sánh giữa các kỹ thuật global illumination khác nhau của Godot:

- **VoxelGI:** |average| Phản xạ và ánh sáng gián tiếp tốt, nhưng cần đề phòng hiện tượng rò sáng.

  - Do bản chất dựa trên voxel, VoxelGI sẽ xuất hiện hiện tượng rò rỉ ánh sáng nếu tường và sàn quá mỏng. Bạn nên đảm bảo tất cả các bề mặt đặc có độ dày ít nhất bằng một voxel.

    Các hiện tượng nhiễu dạng vệt cũng có thể nhìn thấy trên các bề mặt nghiêng. Trong trường hợp này, điều chỉnh các thuộc tính bias hoặc xoay node VoxelGI có thể giúp khắc phục hiện tượng này.

    .. figure:: img/gi_voxel_gi.webp
       :alt: VoxelGI đang hoạt động.

       VoxelGI đang hoạt động.

- **SDFGI:** |average| Phản xạ và ánh sáng gián tiếp tốt, nhưng cần đề phòng hiện tượng rò sáng và dịch chuyển cascade dễ thấy.

  - Mức độ chi tiết của GI thay đổi tùy theo khoảng cách giữa camera và bề mặt.

    Có thể giảm đáng kể hiện tượng rò rỉ bằng cách bật thuộc tính **Use Occlusion**. Tính năng này làm giảm nhẹ hiệu năng, nhưng thường cho ít rò rỉ hơn so với VoxelGI.

    Có thể nhìn thấy hiện tượng dịch chuyển cascade khi camera di chuyển nhanh. Có thể làm cho hiện tượng này khó nhận thấy hơn bằng cách điều chỉnh kích thước cascade hoặc sử dụng sương mù.

    .. figure:: img/gi_sdfgi.webp
       :alt: SDFGI đang hoạt động.

       SDFGI đang hoạt động.

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):** |average| Nguồn *thứ cấp* tốt cho ánh sáng gián tiếp, nhưng không có phản xạ.

  - SSIL được thiết kế để sử dụng bổ trợ cho một kỹ thuật GI khác như VoxelGI, SDFGI hoặc LightmapGI. SSIL hoạt động tốt nhất với các chi tiết quy mô nhỏ, vì tự nó không thể cung cấp chiếu sáng gián tiếp chính xác cho các cấu trúc lớn. SSIL có thể cung cấp chiếu sáng gián tiếp theo thời gian thực trong những tình huống các kỹ thuật GI khác không thể thu nhận các chi tiết quy mô nhỏ hoặc các đối tượng động. Bản chất trong không gian màn hình của SSIL sẽ tạo ra một số hiện tượng nhiễu, đặc biệt khi các đối tượng đi vào hoặc rời khỏi màn hình. SSIL sử dụng màu của khung hình trước (trước bước hậu kỳ), điều đó có nghĩa là các decal phát sáng và shader tùy chỉnh cũng được tính đến (miễn là chúng xuất hiện trên màn hình).

    .. figure:: img/gi_ssil_only.webp
       :alt: SSIL đang hoạt động (không sử dụng kỹ thuật GI nào khác). Hãy chú ý đến ánh sáng phát ra xung quanh chiếc hộp màu vàng.

       SSIL đang hoạt động (không sử dụng kỹ thuật GI nào khác). Hãy chú ý đến ánh sáng phát ra xung quanh chiếc hộp màu vàng.

- **LightmapGI:** |good| Ánh sáng gián tiếp xuất sắc, phản xạ khá tốt (tùy chọn).

  - Đây là kỹ thuật duy nhất cho phép tăng số lần ánh sáng dội lên trên 2 (tối đa 16). Khi bật thông tin định hướng, spherical harmonics (SH) được sử dụng để tạo ra phản chiếu mờ.

    .. figure:: img/gi_lightmap_gi_indirect_only.webp
       :alt: LightmapGI đang hoạt động. Ở đây chỉ có chiếu sáng gián tiếp được bake, nhưng ánh sáng trực tiếp cũng có thể được bake.

       LightmapGI đang hoạt động. Ở đây chỉ có chiếu sáng gián tiếp được bake, nhưng ánh sáng trực tiếp cũng có thể được bake.

- **ReflectionProbe:** |average| Phản xạ tốt, nhưng ánh sáng gián tiếp kém.

  - Có thể tắt chiếu sáng gián tiếp, đặt thành một màu cố định trải đều trong probe hoặc tự động đọc từ môi trường của probe (và áp dụng dưới dạng cubemap). Về cơ bản, tính năng này hoạt động như ánh sáng môi trường cục bộ. Phản chiếu và chiếu sáng gián tiếp được hòa trộn với các probe lân cận khác.

    .. figure:: img/gi_none_reflection_probe.webp
       :alt: ReflectionProbe đang hoạt động (không sử dụng kỹ thuật GI nào khác). Hãy chú ý đến hình cầu phản chiếu.

       ReflectionProbe đang hoạt động (không sử dụng kỹ thuật GI nào khác). Hãy chú ý đến hình cầu phản chiếu.

Khả năng hoạt động theo thời gian thực
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **VoxelGI:** |good| Hoàn toàn theo thời gian thực.

  - Chiếu sáng gián tiếp và phản chiếu hoàn toàn theo thời gian thực. Các đối tượng động có thể nhận GI *và* đóng góp vào GI đó thông qua các bề mặt phát sáng của chúng. Shader tùy chỉnh cũng có thể phát ra ánh sáng riêng, và ánh sáng đó sẽ được phát ra một cách chính xác.

    Phù hợp với các level được tạo bằng quy trình *nếu chúng được tạo trước* (không phải trong khi chơi). Quá trình baking cần vài giây hoặc lâu hơn để hoàn tất, nhưng có thể được thực hiện từ cả editor lẫn project đã export.

- **SDFGI:** |average| Bán thời gian thực.

  - Các cascade được tạo theo thời gian thực, khiến SDFGI phù hợp với các level được tạo bằng quy trình (bao gồm cả khi các cấu trúc được tạo trong khi chơi).

    Các đối tượng động có thể *nhận* GI, nhưng không thể *đóng góp* vào GI đó. Ánh sáng phát ra chỉ được cập nhật khi một đối tượng đi vào cascade, vì vậy tính năng này vẫn có thể hoạt động với các đối tượng di chuyển chậm.

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):** |good| Hoàn toàn theo thời gian thực.

  - SSIL hoạt động với cả ánh sáng tĩnh và động. Tính năng này cũng hoạt động với cả các vật cản tĩnh và động (bao gồm vật liệu phát sáng).

- **LightmapGI:** |bad| Được bake, vì vậy không theo thời gian thực.

  - Cả chiếu sáng gián tiếp và phản chiếu SH đều được bake và không thể thay đổi trong runtime. GI theo thời gian thực phải được
    :ref:`mô phỏng bằng các phương tiện khác <doc_faking_global_illumination>`, chẳng hạn như các đèn vị trí theo thời gian thực. Các đối tượng động nhận chiếu sáng gián tiếp thông qua light probe, có thể được người dùng đặt tự động hoặc thủ công (node LightmapProbe). Không phù hợp với các level được tạo bằng quy trình, vì lightmap chỉ có thể được bake từ editor.

- **ReflectionProbe:** |average| Có thể hoạt động theo thời gian thực tùy chọn.

  - Theo mặc định, phản chiếu được cập nhật khi probe được di chuyển. Phản chiếu được cập nhật thường xuyên nhất có thể nếu chế độ cập nhật được đặt thành **Always** (tốn nhiều tài nguyên).

  - Chiếu sáng gián tiếp phải được người dùng cấu hình thủ công, nhưng có thể thay đổi trong runtime mà không gây ra phép tính tốn kém nào diễn ra ngầm. Điều này khiến ReflectionProbes phù hợp với các level được tạo theo thủ tục.

Công việc cần thực hiện
~~~~~~~~~~~~~~~~~~~~~~~

- **VoxelGI:** Cần tạo và bake một hoặc nhiều node VoxelGI.

  - Cần điều chỉnh đúng phạm vi để đạt kết quả tốt. Ngoài ra, xoay node rồi bake lại có thể giúp khắc phục hiện tượng rò rỉ hoặc các lỗi sọc trong một số trường hợp. Thời gian bake nhanh – thường dưới 10 giây đối với một scene có độ phức tạp trung bình.

- **SDFGI:** Rất ít.

  - SDFGI hoàn toàn tự động; chỉ cần bật trong resource Environment. Công việc thủ công duy nhất cần thực hiện là đặt đúng thuộc tính bake mode của MeshInstances. Không cần tạo node và cũng không cần bake.

- **Chiếu sáng gián tiếp trong không gian màn hình (SSIL):** Rất ít.

  - SSIL hoàn toàn tự động; chỉ cần bật trong resource Environment. Không cần tạo node và cũng không cần bake.

- **LightmapGI:** Yêu cầu thiết lập UV2 và bake.

  - Các mesh tĩnh phải được reimport với UV2 và bật tính năng tạo lightmap. Trên GPU chuyên dụng, thời gian bake tương đối nhanh nhờ quá trình bake lightmap dựa trên GPU – thường dưới 1 phút đối với một scene có độ phức tạp trung bình.

- **ReflectionProbe:** Được người dùng đặt thủ công.

.. |good| image:: img/score_good.webp

.. |average| image:: img/score_average.webp

.. |bad| image:: img/score_bad.webp

Tóm tắt
~~~~~~~

Nếu bạn không chắc nên sử dụng kỹ thuật GI nào:

- Đối với game trên desktop, bạn nên bắt đầu với :ref:`SDFGI <doc_using_sdfgi>` vì kỹ thuật này yêu cầu ít thiết lập nhất. Sau đó, nếu cần, hãy chuyển sang các kỹ thuật GI khác. Để cải thiện hiệu năng trên GPU cấp thấp và đồ họa tích hợp, hãy cân nhắc thêm tùy chọn tắt SDFGI hoặc :ref:`VoxelGI <doc_using_voxel_gi>` trong phần cài đặt game. Có thể tắt SDFGI trong resource Environment, còn VoxelGI có thể được tắt bằng cách ẩn các node VoxelGI. Để tiếp tục cải thiện hình ảnh trên các hệ thống cao cấp, hãy thêm tùy chọn bật SSIL trong phần cài đặt game.
- Đối với game trên thiết bị di động, :ref:`LightmapGI <doc_using_lightmap_gi>` và
  :ref:`ReflectionProbes <doc_reflection_probes>` là những tùy chọn duy nhất được hỗ trợ. Xem thêm :ref:`doc_introduction_to_global_illumination_alternatives`.

.. seealso::

    Bạn có thể so sánh các kỹ thuật chiếu sáng toàn cục đang hoạt động bằng cách sử dụng `dự án demo Global Illumination <https://github.com/godotengine/godot-demo-projects/tree/master/3d/global_illumination>`__.

.. _doc_introduction_to_global_illumination_gi_mode_recommendations:

Tôi nên sử dụng chế độ chiếu sáng toàn cục nào cho mesh và light?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bất kể bạn sử dụng kỹ thuật chiếu sáng toàn cục nào, không có chế độ chiếu sáng toàn cục nào "tốt hơn" một cách tuyệt đối. Tuy vậy, sau đây là một số khuyến nghị cho mesh:

- Đối với hình học tĩnh của level, hãy sử dụng chế độ chiếu sáng toàn cục **Static** *(mặc định)*.
- Đối với hình học động nhỏ và player/enemy, hãy sử dụng chế độ chiếu sáng toàn cục **Disabled**. Hình học động nhỏ sẽ không thể đóng góp một lượng chiếu sáng gián tiếp đáng kể vì hình học này nhỏ hơn một voxel. Nếu cần chiếu sáng gián tiếp cho các đối tượng động nhỏ, bạn có thể mô phỏng bằng node OmniLight3D hoặc SpotLight3D được làm node cha của đối tượng.
- Đối với hình học động *lớn* của level (chẳng hạn như một đoàn tàu đang di chuyển), hãy sử dụng chế độ chiếu sáng toàn cục **Dynamic**. Lưu ý rằng chế độ này chỉ có tác dụng với VoxelGI, vì SDFGI và LightmapGI không hỗ trợ chiếu sáng toàn cục với các đối tượng động.

Sau đây là một số khuyến nghị cho các chế độ light bake:

- Đối với lighting tĩnh của level, hãy sử dụng bake mode **Static**. Chế độ **Static** cũng phù hợp với các light động không thay đổi nhiều trong quá trình chơi, chẳng hạn như một ngọn đuốc chập chờn.
- Đối với các hiệu ứng động tồn tại trong thời gian ngắn (chẳng hạn như vũ khí), hãy sử dụng bake mode **Disabled** để cải thiện hiệu năng.
- Đối với các hiệu ứng động tồn tại trong thời gian dài (chẳng hạn như đèn báo động xoay), hãy sử dụng bake mode **Dynamic** để cải thiện chất lượng *(mặc định)*. Lưu ý rằng chế độ này chỉ có tác dụng với VoxelGI và SDFGI, vì LightmapGI không hỗ trợ chiếu sáng toàn cục với các light động.

.. _doc_introduction_to_global_illumination_alternatives:

Các phương án thay thế cho kỹ thuật GI
--------------------------------------

Nếu không kỹ thuật GI nào được đề cập ở trên phù hợp, bạn vẫn có thể
:ref:`mô phỏng GI bằng cách đặt thêm các light thủ công <doc_faking_global_illumination>`. Cách này đòi hỏi nhiều công việc thủ công hơn, nhưng có thể mang lại hiệu năng tốt *và* hình ảnh đẹp nếu được thực hiện đúng cách. Phương pháp này vẫn được sử dụng trong nhiều game hiện đại cho đến ngày nay.

Khi nhắm đến phần cứng cấp thấp trong các trường hợp không thể sử dụng LightmapGI (chẳng hạn như các level được tạo theo thủ tục), việc chỉ dựa vào lighting của môi trường hoặc một hệ số light môi trường cố định có thể là điều cần thiết. Điều này có thể khiến hình ảnh phẳng hơn, nhưng việc điều chỉnh màu light môi trường và mức đóng góp của bầu trời vẫn giúp đạt được kết quả chấp nhận được trong hầu hết trường hợp.
