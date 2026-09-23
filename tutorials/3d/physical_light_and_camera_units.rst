.. _doc_physical_light_and_camera_units:

Đơn vị vật lý của đèn và camera
===============================

Tại sao nên sử dụng đơn vị vật lý của đèn và camera?
----------------------------------------------------

Godot sử dụng các đơn vị tùy ý cho nhiều thuộc tính vật lý áp dụng cho đèn, chẳng hạn như màu sắc, năng lượng, trường nhìn của camera và độ phơi sáng. Theo mặc định, các thuộc tính này sử dụng đơn vị tùy ý, vì việc sử dụng đơn vị vật lý chính xác đi kèm một số đánh đổi không đáng kể đối với nhiều game. Vì Godot ưu tiên tính dễ sử dụng theo mặc định, đơn vị vật lý của đèn bị tắt theo mặc định.

Ưu điểm của đơn vị vật lý
~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu hướng đến tính chân thực như ảnh trong dự án, việc sử dụng đơn vị thế giới thực làm cơ sở có thể giúp bạn dễ dàng điều chỉnh hơn. Các tài liệu tham khảo về vật liệu, đèn và độ sáng của cảnh trong thế giới thực có rất nhiều trên các trang web như `Physically Based <https://physicallybased.info/>`__.

Việc sử dụng đơn vị thế giới thực trong Godot cũng hữu ích khi chuyển một cảnh từ phần mềm 3D khác có sử dụng đơn vị vật lý của đèn, chẳng hạn như Blender.

Nhược điểm của đơn vị vật lý
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nhược điểm lớn nhất của việc sử dụng đơn vị vật lý của đèn là bạn sẽ phải chú ý sát sao đến dải động đang được sử dụng tại một thời điểm cụ thể. Bạn có thể gặp lỗi độ chính xác dấu phẩy động khi kết hợp cường độ đèn rất cao với cường độ đèn rất thấp.

Trên thực tế, điều này có nghĩa là bạn sẽ phải quản lý thủ công các thiết lập độ phơi sáng để bảo đảm cảnh không bị phơi sáng quá mức hoặc thiếu sáng quá nhiều. Tự động phơi sáng có thể giúp bạn cân bằng ánh sáng trong cảnh để đưa ánh sáng về phạm vi bình thường, nhưng không thể khôi phục độ chính xác đã mất do dải động quá cao.

Việc sử dụng đơn vị vật lý của đèn và camera sẽ không tự động khiến dự án của bạn trông *better*. Đôi khi, việc rời xa tính chân thực thực sự có thể khiến cảnh trông đẹp hơn đối với mắt người. Ngoài ra, việc sử dụng đơn vị vật lý đòi hỏi mức độ nghiêm ngặt cao hơn so với đơn vị phi vật lý. Hầu hết lợi ích của đơn vị vật lý chỉ có thể đạt được nếu các đơn vị được thiết lập chính xác để khớp với tài liệu tham khảo trong thế giới thực.

.. note::

    Đơn vị vật lý của đèn chỉ khả dụng trong kết xuất 3D, không khả dụng trong 2D.

Thiết lập đơn vị vật lý của đèn
-------------------------------

Có thể bật riêng đơn vị vật lý của đèn và đơn vị vật lý của camera.

Để bật chính xác đơn vị vật lý của đèn, cần thực hiện 4 bước:

1. Bật thiết lập dự án.
2. Cấu hình camera.
3. Cấu hình môi trường.
4. Cấu hình các node Light3D.

Vì đơn vị vật lý của đèn và camera chỉ yêu cầu một vài phép tính để xử lý việc chuyển đổi đơn vị, việc bật chúng không gây ảnh hưởng hiệu suất đáng kể nào trên CPU. Tuy nhiên, ở phía GPU, đơn vị vật lý của camera hiện buộc phải sử dụng độ sâu trường ảnh. Điều này gây ảnh hưởng hiệu suất ở mức vừa phải. Để giảm ảnh hưởng hiệu suất này, có thể giảm chất lượng độ sâu trường ảnh trong Project Settings nâng cao.

Bật thiết lập dự án
~~~~~~~~~~~~~~~~~~~

Mở Project Settings, bật nút chuyển **Advanced**, sau đó bật **Rendering > Lights And Shadows > Use Physical Light Units**. Khởi động lại editor.

Cấu hình camera
~~~~~~~~~~~~~~~

.. warning::

    Khi đơn vị vật lý của đèn được bật và cảnh của bạn có một node WorldEnvironment (tức là Environment của editor bị tắt), bạn **must** gán một tài nguyên :ref:`class_CameraAttributes` cho node WorldEnvironment. Nếu không, viewport của trình chỉnh sửa 3D sẽ trông cực kỳ sáng nếu bạn có một node DirectionalLight3D hiển thị.

Trên node Camera3D, bạn có thể thêm một tài nguyên :ref:`class_CameraAttributes` vào thuộc tính **Attributes** của node. Tài nguyên này được dùng để điều khiển độ sâu trường ảnh và độ phơi sáng của camera. Khi sử dụng
:ref:`class_CameraAttributesPhysical`, thuộc tính tiêu cự của nó cũng được dùng để điều chỉnh trường nhìn của camera.

Khi đơn vị vật lý của đèn được bật, các thuộc tính bổ sung sau đây sẽ khả dụng trong phần **Exposure** của CameraAttributesPhysical:

- **Aperture:** Kích thước khẩu độ của camera, được đo bằng f-stop. F-stop là một tỷ lệ không có đơn vị giữa tiêu cự của camera và đường kính khẩu độ. Thiết lập khẩu độ cao sẽ tạo ra khẩu độ nhỏ hơn, dẫn đến hình ảnh tối hơn và lấy nét sắc nét hơn. Khẩu độ thấp tạo ra khẩu độ rộng, cho nhiều ánh sáng đi vào hơn, dẫn đến hình ảnh sáng hơn và kém nét hơn.
- **Shutter Speed:** Thời gian màn trập mở và đóng, được đo bằng *inverse seconds* (``1/N``). Giá trị thấp hơn sẽ cho nhiều ánh sáng đi vào hơn, dẫn đến hình ảnh sáng hơn, trong khi giá trị cao hơn sẽ cho ít ánh sáng đi vào hơn, dẫn đến hình ảnh tối hơn. *Khi lấy hoặc thiết lập thuộc tính này bằng script, đơn vị là giây thay vì giây nghịch đảo.*
- **Sensitivity:** Độ nhạy của cảm biến camera, được đo bằng ISO. Độ nhạy cao hơn tạo ra hình ảnh sáng hơn. Khi bật tự động phơi sáng, thuộc tính này có thể được dùng như một phương pháp bù phơi sáng. Tăng gấp đôi giá trị sẽ tăng giá trị phơi sáng (được đo bằng EV100) thêm 1 stop.
- **Multiplier:** Hệ số nhân phơi sáng *non-physical*. Giá trị cao hơn sẽ tăng độ sáng của cảnh. Có thể dùng thuộc tính này để điều chỉnh hậu kỳ hoặc phục vụ mục đích animation.

Giá trị **Aperture** mặc định là 16 f-stop, phù hợp với môi trường ngoài trời vào ban ngày (tức là khi sử dụng DirectionalLight3D mặc định). Đối với ánh sáng trong nhà, giá trị từ 2 đến 4 phù hợp hơn.

Tốc độ màn trập thường được sử dụng trong nhiếp ảnh và sản xuất phim là 1/50 (0.02 giây). Nhiếp ảnh ban đêm thường sử dụng màn trập khoảng 1/10 (0.1 giây), trong khi nhiếp ảnh thể thao sử dụng tốc độ màn trập từ 1/250 (0.004 giây) đến 1/1000 (0.001 giây) để giảm nhòe chuyển động.

Trong đời thực, độ nhạy thường được đặt trong khoảng từ 50 ISO đến 400 ISO khi chụp ảnh ngoài trời ban ngày, tùy thuộc vào điều kiện thời tiết. Các giá trị cao hơn được sử dụng khi chụp ảnh trong nhà hoặc vào ban đêm.

.. note::

    Không giống camera đời thực, Godot không mô phỏng các hiệu ứng bất lợi của việc tăng độ nhạy ISO hoặc giảm tốc độ màn trập, chẳng hạn như nhiễu hạt nhìn thấy được hoặc vệt sáng.

Xem :ref:`doc_physical_light_and_camera_units_setting_up_physical_camera_units` để biết mô tả về các thuộc tính CameraAttributesPhysical cũng khả dụng khi **not** sử dụng đơn vị vật lý của đèn.

Cấu hình môi trường
~~~~~~~~~~~~~~~~~~~

.. warning::

    Cấu hình mặc định được thiết kế cho các cảnh ngoài trời vào ban ngày. Cảnh ban đêm và trong nhà sẽ cần điều chỉnh cường độ nền của DirectionalLight3D và WorldEnvironment để hiển thị chính xác. Nếu không, các đèn vị trí sẽ gần như không nhìn thấy ở cường độ mặc định.

Nếu bạn vẫn chưa thêm một node :ref:`class_WorldEnvironment` và một node :ref:`class_Camera3D` vào scene hiện tại, hãy thực hiện ngay bằng cách nhấp vào 3 dấu chấm dọc ở đầu khung nhìn của trình chỉnh sửa 3D. Nhấp vào **Add Sun to Scene**, mở lại hộp thoại rồi nhấp vào **Add Environment to Scene**.

Sau khi bật đơn vị ánh sáng vật lý, một thuộc tính mới sẽ có thể chỉnh sửa trong resource :ref:`class_Environment`:

- **Background Intensity:** Cường độ của bầu trời nền, tính bằng `nits <https://en.wikipedia.org/wiki/Candela_per_square_metre>`__ (candela trên mét vuông). Giá trị này cũng ảnh hưởng đến ánh sáng môi trường và ánh sáng phản chiếu nếu các mode tương ứng được đặt thành **Background**. Nếu đặt **Background Energy** tùy chỉnh, năng lượng này sẽ được nhân với cường độ.

Cấu hình các node ánh sáng
~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi bật đơn vị ánh sáng vật lý, 2 thuộc tính mới sẽ có trong các node Light3D:

- **Intensity:** Cường độ ánh sáng, tính bằng `lux <https://en.wikipedia.org/wiki/Lux>`__ (DirectionalLight3D) hoặc `lumens <https://en.wikipedia.org/wiki/Lumen_(unit)>`__ (OmniLight3D/SpotLight3D/AreaLight3D). Nếu đặt **Energy** tùy chỉnh, năng lượng này sẽ được nhân với cường độ.
- **Temperature:** *color temperature* của ánh sáng, được xác định theo Kelvin. Nếu đặt **Color** tùy chỉnh, màu này sẽ được nhân với nhiệt độ màu.

**Cường độ OmniLight3D/SpotLight3D/AreaLight3D**

Lumen là đơn vị đo quang thông, tức tổng lượng ánh sáng nhìn thấy được phát ra từ một nguồn sáng trong một đơn vị thời gian.

Đối với SpotLight3D, chúng tôi giả định rằng khu vực bên ngoài hình nón nhìn thấy được bao quanh bởi một vật liệu hấp thụ ánh sáng hoàn hảo. Vì vậy, độ sáng biểu kiến của vùng hình nón *không* thay đổi khi kích thước hình nón tăng hoặc giảm.

Một bóng đèn gia dụng thông thường có thể có cường độ từ khoảng 600 đến 1200 lumen. Một ngọn nến có khoảng 13 lumen, trong khi đèn đường có thể đạt khoảng 60000 lumen.

**Cường độ DirectionalLight3D**

Lux là đơn vị đo quang thông trên một đơn vị diện tích, bằng một lumen trên một mét vuông. Lux đo lượng ánh sáng chiếu tới một bề mặt tại một thời điểm nhất định.

Với DirectionalLight3D, vào một ngày nắng quang mây, một bề mặt dưới ánh nắng trực tiếp có thể nhận khoảng 100000 lux. Một căn phòng thông thường trong nhà có thể nhận khoảng 50 lux, trong khi mặt đất dưới ánh trăng có thể nhận khoảng 0.1 lux.

**Nhiệt độ màu**

6500 Kelvin là màu trắng. Giá trị cao hơn tạo ra màu lạnh hơn (xanh hơn), trong khi giá trị thấp hơn tạo ra màu ấm hơn (cam hơn).

Mặt trời vào ngày nhiều mây có nhiệt độ khoảng 6500 Kelvin. Vào ngày quang mây, nhiệt độ của mặt trời nằm trong khoảng 5500 đến 6000 Kelvin. Vào lúc bình minh hoặc hoàng hôn trong ngày quang mây, nhiệt độ của mặt trời có thể giảm xuống khoảng 1850 Kelvin.

.. figure:: img/physical_light_units_color_temperature_chart.webp
   :align: center
   :alt: Biểu đồ nhiệt độ màu từ 1,000 Kelvin (bên trái) đến 12,500 Kelvin (bên phải)

   Biểu đồ nhiệt độ màu từ 1,000 Kelvin (bên trái) đến 12,500 Kelvin (bên phải)

Các thuộc tính Light3D khác như **Energy** và **Color** vẫn có thể chỉnh sửa cho mục đích animation, cũng như khi thỉnh thoảng bạn cần tạo ánh sáng với các thuộc tính không thực tế.

.. _doc_physical_light_and_camera_units_setting_up_physical_camera_units:

Thiết lập đơn vị camera vật lý
------------------------------

Có thể bật đơn vị camera vật lý độc lập với đơn vị ánh sáng vật lý.

Sau khi thêm một resource :ref:`class_CameraAttributesPhysical` vào thuộc tính **Camera Attributes** của node Camera3D, một số thuộc tính như **FOV** sẽ không còn có thể chỉnh sửa. Thay vào đó, các thuộc tính này giờ được điều khiển bởi các thuộc tính của CameraAttributesPhysical, chẳng hạn như tiêu cự và khẩu độ.

CameraAttributesPhysical cung cấp các thuộc tính sau trong phần **Frustum**:

- **Focus Distance:** Khoảng cách từ camera đến đối tượng sẽ được lấy nét, tính bằng mét. Về mặt nội bộ, giá trị này sẽ được giới hạn để luôn lớn hơn **Focal Length** ít nhất 1 milimét.
- **Focal Length:** Khoảng cách giữa ống kính camera và khẩu độ camera, tính bằng milimét. Điều khiển trường nhìn và độ sâu trường ảnh. Tiêu cự lớn hơn sẽ tạo ra trường nhìn nhỏ hơn và độ sâu trường ảnh hẹp hơn, nghĩa là sẽ có ít đối tượng được lấy nét hơn. Tiêu cự nhỏ hơn sẽ tạo ra trường nhìn rộng hơn và độ sâu trường ảnh lớn hơn, nghĩa là sẽ có nhiều đối tượng được lấy nét hơn. Thuộc tính này ghi đè các thuộc tính **FOV** và **Keep Aspect** của Camera3D, khiến chúng ở trạng thái chỉ đọc trong inspector.
- **Near/Far:** Khoảng cách cắt gần và xa, tính bằng mét. Các giá trị này hoạt động giống như các thuộc tính cùng tên của Camera3D. Giá trị **Near** thấp hơn cho phép camera hiển thị các đối tượng ở rất gần, nhưng có thể gây ra các vấn đề về độ chính xác (Z-fighting) ở khoảng cách xa. Giá trị **Far** cao hơn cho phép camera nhìn xa hơn, nhưng cũng có thể gây ra các vấn đề về độ chính xác (Z-fighting) ở khoảng cách xa.

Tiêu cự mặc định 35 mm tương ứng với một ống kính góc rộng. Tuy nhiên, nó vẫn tạo ra trường nhìn hẹp hơn đáng kể so với FOV dọc "thực dụng" mặc định là 75 độ. Điều này là do các trường hợp sử dụng không liên quan đến game, chẳng hạn như làm phim và nhiếp ảnh, thường ưu tiên trường nhìn hẹp hơn để tạo vẻ điện ảnh.

Các giá trị tiêu cự phổ biến được sử dụng trong làm phim và nhiếp ảnh là:

- **Fisheye (ultrawide angle):** Dưới 15 mm. Hầu như không nhìn thấy độ sâu trường ảnh.
- **Wide angle:** Từ 15 mm đến 50 mm. Độ sâu trường ảnh giảm.
- **Standard:** Từ 50 mm đến 100 mm. Độ sâu trường ảnh tiêu chuẩn.
- **Telephoto:** Lớn hơn 100 mm. Độ sâu trường ảnh tăng.

Tương tự khi sử dụng mode tỷ lệ **Keep Height**, trường nhìn hiệu dụng phụ thuộc vào tỷ lệ khung hình của viewport; tỷ lệ khung hình rộng hơn sẽ tự động tạo ra trường nhìn *ngang* rộng hơn.

Bạn cũng có thể bật điều chỉnh phơi sáng tự động dựa trên mức độ sáng trung bình của camera trong phần **Auto Exposure**, với các thuộc tính sau:

- **Min Sensitivity:** Mức độ sáng tối thiểu mà camera được phép đạt tới, tính bằng EV100.
- **Max Sensitivity:** Độ sáng tối đa mà camera được phép đạt tới, được đo bằng EV100.
- **Speed:** Tốc độ của hiệu ứng auto exposure. Ảnh hưởng đến thời gian camera cần để thực hiện auto exposure. Giá trị cao hơn cho phép chuyển tiếp nhanh hơn, nhưng các điều chỉnh tạo ra có thể trông gây mất tập trung tùy thuộc vào cảnh.
- **Scale:** Tỷ lệ của hiệu ứng auto exposure. Ảnh hưởng đến cường độ của auto exposure.

EV100 là một giá trị phơi sáng (EV) được đo ở độ nhạy ISO 100. Xem `bảng này <https://en.wikipedia.org/wiki/Exposure_value#Tabulated_exposure_values>`__ để biết các giá trị EV100 phổ biến trong thực tế.
