.. _doc_your_second_spatial_shader:

Shader 3D thứ hai của bạn
=========================

Ở cấp độ tổng quát, Godot cung cấp cho người dùng một loạt tham số có thể được tùy chọn thiết lập (``AO``, ``SSS_Strength``, ``RIM``, v.v.). Các tham số này tương ứng với những hiệu ứng phức tạp khác nhau (Ambient Occlusion, SubSurface Scattering, Rim Lighting, v.v.). Khi không được ghi giá trị, đoạn mã sẽ bị loại bỏ trước khi biên dịch, vì vậy shader không phải chịu chi phí của tính năng bổ sung đó. Điều này giúp người dùng dễ dàng có được shading đúng theo PBR phức tạp mà không cần viết các shader phức tạp. Tất nhiên, Godot cũng cho phép bạn bỏ qua tất cả các tham số này và viết một shader được tùy chỉnh hoàn toàn.

Để xem danh sách đầy đủ các tham số này, hãy xem tài liệu tham chiếu :ref:`spatial shader <doc_spatial_shader>`.

Một điểm khác biệt giữa hàm vertex và hàm fragment là hàm vertex chạy trên từng vertex và thiết lập các thuộc tính như ``VERTEX`` (vị trí) và ``NORMAL``, trong khi fragment shader chạy trên từng pixel và quan trọng nhất là thiết lập màu ``ALBEDO`` của :ref:`MeshInstance3D<class_MeshInstance3D>`.

Hàm fragment spatial đầu tiên của bạn
-------------------------------------

Như đã đề cập trong phần trước của tutorial này, cách sử dụng tiêu chuẩn của hàm fragment trong Godot là thiết lập các thuộc tính vật liệu khác nhau và để Godot xử lý phần còn lại. Để mang lại nhiều tính linh hoạt hơn nữa, Godot cũng cung cấp các tùy chọn gọi là render mode. Render mode được thiết lập ở đầu shader, ngay bên dưới ``shader_type``, và chúng chỉ định loại chức năng mà bạn muốn các khía cạnh tích hợp sẵn của shader có.

Ví dụ, nếu bạn không muốn ánh sáng ảnh hưởng đến một đối tượng, hãy đặt render mode thành ``unshaded``:

.. code-block:: glsl

  render_mode unshaded;

Bạn cũng có thể kết hợp nhiều render mode với nhau. Ví dụ, nếu muốn sử dụng toon shading thay vì PBR shading chân thực hơn, hãy đặt diffuse mode và specular mode thành toon:

.. code-block:: glsl

  render_mode diffuse_toon, specular_toon;

Mô hình chức năng tích hợp sẵn này cho phép bạn viết các shader tùy chỉnh phức tạp chỉ bằng cách thay đổi một vài tham số.

Để xem danh sách đầy đủ các render mode, hãy xem tài liệu tham chiếu :ref:`Spatial shader reference <doc_spatial_shader>`.

Trong phần này của tutorial, chúng ta sẽ tìm hiểu cách biến địa hình gồ ghề từ phần trước thành một đại dương.

Trước tiên, hãy thiết lập màu của nước. Chúng ta thực hiện điều đó bằng cách thiết lập ``ALBEDO``.

``ALBEDO`` là một ``vec3`` chứa màu của đối tượng.

Hãy đặt nó thành một sắc xanh lam đẹp mắt.

.. code-block:: glsl

  void fragment() {
    ALBEDO = vec3(0.1, 0.3, 0.5);
  }

.. image:: img/albedo.png

Chúng ta đặt nó thành một sắc xanh lam rất tối vì phần lớn sắc xanh của nước sẽ đến từ các phản chiếu của bầu trời.

Mô hình PBR mà Godot sử dụng dựa trên hai tham số chính: ``METALLIC`` và ``ROUGHNESS``.

``ROUGHNESS`` chỉ định bề mặt của vật liệu mịn hay thô đến mức nào. ``ROUGHNESS`` thấp sẽ khiến vật liệu trông giống nhựa bóng, trong khi độ roughness cao khiến vật liệu có màu sắc đồng nhất hơn.

``METALLIC`` chỉ định đối tượng giống kim loại đến mức nào. Tốt nhất nên đặt nó gần ``0`` hoặc ``1``. Hãy xem ``METALLIC`` như việc thay đổi sự cân bằng giữa màu phản chiếu và màu ``ALBEDO``. ``METALLIC`` cao gần như hoàn toàn bỏ qua ``ALBEDO``, và trông giống như một tấm gương phản chiếu bầu trời. Trong khi đó, ``METALLIC`` thấp thể hiện màu bầu trời và màu ``ALBEDO`` cân bằng hơn.

``ROUGHNESS`` tăng từ ``0`` đến ``1`` từ trái sang phải, trong khi ``METALLIC`` tăng từ ``0`` đến ``1`` từ trên xuống dưới.

.. image:: img/PBR.png

.. note:: ``METALLIC`` nên gần với ``0`` hoặc ``1`` để có shading PBR phù hợp. Chỉ đặt nó nằm giữa hai giá trị này khi chuyển đổi giữa các vật liệu.

Nước không phải kim loại, vì vậy chúng ta sẽ đặt thuộc tính ``METALLIC`` của nó thành ``0.0``. Nước cũng có độ phản chiếu cao, vì vậy chúng ta cũng sẽ đặt thuộc tính ``ROUGHNESS`` của nó ở mức khá thấp.

.. code-block:: glsl

  void fragment() {
    METALLIC = 0.0;
    ROUGHNESS = 0.01;
    ALBEDO = vec3(0.1, 0.3, 0.5);
  }

.. image:: img/plastic.png

Bây giờ chúng ta có một bề mặt trông như nhựa mịn. Đã đến lúc nghĩ về một số thuộc tính cụ thể của nước mà chúng ta muốn mô phỏng. Có hai thuộc tính chính sẽ biến bề mặt nhựa kỳ quặc này thành mặt nước cách điệu đẹp mắt. Đầu tiên là specular reflections. Specular reflections là những điểm sáng bạn thấy ở nơi ánh nắng phản chiếu trực tiếp vào mắt. Thứ hai là fresnel reflectance. Fresnel reflectance là thuộc tính khiến các đối tượng phản chiếu nhiều hơn ở những góc nhìn nông. Đây là lý do bạn có thể nhìn thấy phần nước bên dưới mình, nhưng ở xa hơn, nước lại phản chiếu bầu trời.

Để tăng specular reflections, chúng ta sẽ làm hai việc. Trước tiên, chúng ta sẽ thay đổi render mode cho specular thành toon vì toon render mode có các điểm nổi bật specular lớn hơn.

.. code-block:: glsl

  render_mode specular_toon;

.. image:: img/specular-toon.png

Thứ hai, chúng ta sẽ thêm rim lighting. Rim lighting tăng hiệu ứng của ánh sáng ở các góc nhìn lướt. Thông thường, nó được dùng để mô phỏng cách ánh sáng xuyên qua vải ở các cạnh của một đối tượng, nhưng ở đây chúng ta sẽ dùng nó để tạo hiệu ứng mặt nước đẹp mắt.

.. code-block:: glsl

  void fragment() {
    RIM = 0.2;
    METALLIC = 0.0;
    ROUGHNESS = 0.01;
    ALBEDO = vec3(0.1, 0.3, 0.5);
  }

.. image:: img/rim.png

Để thêm fresnel reflectance, chúng ta sẽ tính một fresnel term trong fragment shader. Ở đây, vì lý do hiệu năng, chúng ta sẽ không sử dụng fresnel term thực. Thay vào đó, chúng ta sẽ xấp xỉ nó bằng dot product của các vector ``NORMAL`` và ``VIEW``. Vector ``NORMAL`` hướng ra khỏi bề mặt của mesh, trong khi vector ``VIEW`` là hướng từ mắt bạn đến điểm đó trên bề mặt. Dot product giữa chúng là một cách thuận tiện để xác định khi bạn nhìn thẳng vào bề mặt hay nhìn ở một góc lướt.

.. code-block:: glsl

  float fresnel = sqrt(1.0 - dot(NORMAL, VIEW));

Và trộn nó vào cả ``ROUGHNESS`` lẫn ``ALBEDO``. Đây là lợi ích của ShaderMaterials so với StandardMaterial3Ds. Với StandardMaterial3D, chúng ta có thể thiết lập các thuộc tính này bằng texture hoặc một số cố định. Nhưng với shader, chúng ta có thể thiết lập chúng dựa trên bất kỳ hàm toán học nào mà mình nghĩ ra.


.. code-block:: glsl

  void fragment() {
    float fresnel = sqrt(1.0 - dot(NORMAL, VIEW));
    RIM = 0.2;
    METALLIC = 0.0;
    ROUGHNESS = 0.01 * (1.0 - fresnel);
    ALBEDO = vec3(0.1, 0.3, 0.5) + (0.1 * fresnel);
  }

.. image:: img/fresnel.png

Và giờ đây, chỉ với 5 dòng mã, bạn đã có thể tạo ra mặt nước trông phức tạp. Bây giờ chúng ta đã có ánh sáng, mặt nước này trông quá sáng. Hãy làm nó tối hơn. Việc này rất dễ thực hiện bằng cách giảm các giá trị của ``vec3`` mà chúng ta truyền vào ``ALBEDO``. Hãy đặt chúng thành ``vec3(0.01, 0.03, 0.05)``.

.. image:: img/dark-water.png

Tạo hoạt ảnh với ``TIME``
-------------------------

Quay lại hàm vertex, chúng ta có thể tạo hoạt ảnh cho các con sóng bằng biến tích hợp sẵn ``TIME``.

``TIME`` là một biến tích hợp sẵn, có thể được truy cập từ các hàm vertex và fragment.


Trong tutorial trước, chúng ta đã tính chiều cao bằng cách đọc từ heightmap. Trong tutorial này, chúng ta cũng sẽ làm tương tự. Đặt mã heightmap vào một hàm có tên ``height()``.

.. code-block:: glsl

  float height(vec2 position) {
    return texture(noise, position / 10.0).x; // Hệ số tỷ lệ dựa trên kích thước mesh (PlaneMesh này có kích thước 10×10).
  }

Để sử dụng ``TIME`` trong hàm ``height()``, chúng ta cần truyền nó vào.

.. code-block:: glsl

  float height(vec2 position, float time) {
  }

Và hãy đảm bảo truyền nó vào đúng cách bên trong hàm vertex.

.. code-block:: glsl

  void vertex() {
    vec2 pos = VERTEX.xz;
    float k = height(pos, TIME);
    VERTEX.y = k;
  }

Thay vì sử dụng normal map để tính các normal, chúng ta sẽ tự tính chúng trong hàm ``vertex()``. Để làm vậy, hãy sử dụng dòng mã sau.

.. code-block:: glsl

  NORMAL = normalize(vec3(k - height(pos + vec2(0.1, 0.0), TIME), 0.1, k - height(pos + vec2(0.0, 0.1), TIME)));

Chúng ta cần tự tính ``NORMAL`` vì trong phần tiếp theo, chúng ta sẽ sử dụng toán học để tạo ra những con sóng trông phức tạp.

Bây giờ, chúng ta sẽ làm cho hàm ``height()`` phức tạp hơn một chút bằng cách offset ``position`` theo cosine của ``TIME``.

.. code-block:: glsl

  float height(vec2 position, float time) {
    vec2 offset = 0.01 * cos(position + time);
    return texture(noise, (position / 10.0) - offset).x;
  }

Kết quả là những con sóng chuyển động chậm, nhưng không thật tự nhiên. Phần tiếp theo sẽ tìm hiểu sâu hơn về việc sử dụng shader để tạo ra các hiệu ứng phức tạp hơn, trong trường hợp này là những con sóng chân thực, bằng cách thêm một vài hàm toán học.

Các hiệu ứng nâng cao: sóng
---------------------------

Điều làm cho shader trở nên mạnh mẽ là bạn có thể đạt được các hiệu ứng phức tạp bằng cách sử dụng toán học. Để minh họa điều này, chúng ta sẽ đưa những con sóng lên một cấp độ mới bằng cách sửa đổi hàm ``height()`` và giới thiệu một hàm mới có tên là ``wave()``.

``wave()`` có một tham số là ``position``, giống với tham số trong ``height()``.

Chúng ta sẽ gọi ``wave()`` nhiều lần trong ``height()`` để mô phỏng hình dạng của những con sóng.

.. code-block:: glsl

  float wave(vec2 position){
    position += texture(noise, position / 10.0).x * 2.0 - 1.0;
    vec2 wv = 1.0 - abs(sin(position));
    return pow(1.0 - pow(wv.x * wv.y, 0.65), 4.0);
  }

Thoạt nhìn, đoạn này có vẻ phức tạp. Vì vậy, hãy cùng xem qua từng dòng.

.. code-block:: glsl

    position += texture(noise, position / 10.0).x * 2.0 - 1.0;

Offset vị trí theo texture ``noise``. Điều này sẽ làm cho các con sóng uốn cong, để chúng không còn là những đường thẳng hoàn toàn thẳng hàng với lưới.

.. code-block:: glsl

    vec2 wv = 1.0 - abs(sin(position));

Định nghĩa một hàm có dạng sóng bằng cách sử dụng ``sin()`` và ``position``. Thông thường, các sóng ``sin()`` rất tròn. Chúng ta sử dụng ``abs()`` để lấy giá trị tuyệt đối, tạo cho chúng một gờ sắc nét và giới hạn chúng trong khoảng 0-1. Sau đó, chúng ta trừ nó khỏi ``1.0`` để đưa đỉnh lên trên.

.. code-block:: glsl

    return pow(1.0 - pow(wv.x * wv.y, 0.65), 4.0);

Nhân sóng theo hướng x với sóng theo hướng y rồi nâng lên một lũy thừa để làm các đỉnh sắc nét hơn. Sau đó, trừ kết quả đó khỏi ``1.0`` để các gờ trở thành đỉnh, rồi nâng lên một lũy thừa để làm các gờ sắc nét hơn.

Bây giờ chúng ta có thể thay thế nội dung của hàm ``height()`` bằng ``wave()``.

.. code-block:: glsl

  float height(vec2 position, float time) {
    float h = wave(position);
    return h;
  }

Với cách này, bạn sẽ có:

.. image:: img/wave1.png

Hình dạng của sóng sin quá rõ ràng. Vì vậy, hãy làm các con sóng giãn ra một chút. Chúng ta thực hiện điều này bằng cách scale ``position``.

.. code-block:: glsl

  float height(vec2 position, float time) {
    float h = wave(position * 0.4);
    return h;
  }

Bây giờ trông đẹp hơn nhiều.

.. image:: img/wave2.png

Chúng ta còn có thể làm tốt hơn nữa nếu xếp chồng nhiều con sóng lên nhau với các tần số và biên độ khác nhau. Điều này có nghĩa là chúng ta sẽ scale vị trí của từng con sóng để làm chúng mảnh hơn hoặc rộng hơn (tần số). Đồng thời, chúng ta sẽ nhân đầu ra của sóng để làm chúng thấp hơn hoặc cao hơn (biên độ).

Dưới đây là một ví dụ về cách bạn có thể xếp chồng bốn con sóng để tạo ra những con sóng trông đẹp hơn.

.. code-block:: glsl

  float height(vec2 position, float time) {
    float d = wave((position + time) * 0.4) * 0.3;
    d += wave((position - time) * 0.3) * 0.3;
    d += wave((position + time) * 0.5) * 0.2;
    d += wave((position - time) * 0.6) * 0.2;
    return d;
  }

Lưu ý rằng chúng ta cộng thời gian vào hai con sóng và trừ nó khỏi hai con sóng còn lại. Điều này làm cho các con sóng chuyển động theo những hướng khác nhau, tạo ra một hiệu ứng phức tạp. Cũng lưu ý rằng tổng các biên độ (giá trị mà kết quả được nhân với) đều bằng ``1.0``. Điều này giữ cho sóng nằm trong khoảng 0-1.

Với đoạn mã này, bạn sẽ có được những con sóng trông phức tạp hơn, và tất cả những gì bạn cần làm là thêm một chút toán học!

.. image:: img/wave3.png

Để biết thêm thông tin về Spatial shader, hãy đọc tài liệu :ref:`Shading Language <doc_shading_language>` và tài liệu :ref:`Spatial Shaders <doc_spatial_shader>`. Ngoài ra, hãy xem các hướng dẫn nâng cao hơn trong các phần :ref:`Shading section <toc-learn-features-shading>` và :ref:`3D <toc-learn-features-3d>`.
