.. _doc_general_optimization:

Mẹo tối ưu hóa chung
====================

Giới thiệu
----------

Trong một thế giới lý tưởng, máy tính sẽ chạy với tốc độ vô hạn. Giới hạn duy nhất đối với những gì chúng ta có thể đạt được sẽ là trí tưởng tượng của mình. Tuy nhiên, trong thế giới thực, việc tạo ra phần mềm khiến ngay cả chiếc máy tính nhanh nhất cũng phải hoạt động hết công suất là điều quá dễ dàng.

Vì vậy, việc thiết kế game và các phần mềm khác là sự thỏa hiệp giữa những gì chúng ta muốn có thể thực hiện được và những gì chúng ta có thể đạt được một cách thực tế mà vẫn duy trì hiệu năng tốt.

Để đạt được kết quả tốt nhất, chúng ta có hai cách tiếp cận:

- Làm việc nhanh hơn.
- Làm việc thông minh hơn.

Và tốt nhất là chúng ta sẽ kết hợp cả hai cách.

Màn khói và đánh lạc hướng
~~~~~~~~~~~~~~~~~~~~~~~~~~

Một phần của việc làm việc thông minh hơn là nhận ra rằng trong game, chúng ta thường có thể khiến người chơi tin rằng họ đang ở trong một thế giới phức tạp, tương tác và hấp dẫn về mặt đồ họa hơn rất nhiều so với thực tế. Một lập trình viên giỏi giống như một ảo thuật gia, và nên cố gắng học các mánh khóe trong nghề đồng thời tìm cách sáng tạo ra những mánh khóe mới.

Bản chất của sự chậm chạp
~~~~~~~~~~~~~~~~~~~~~~~~~

Đối với người quan sát bên ngoài, các vấn đề về hiệu năng thường bị gộp chung với nhau. Nhưng trên thực tế, có một số loại vấn đề hiệu năng khác nhau:

- Một tiến trình chậm diễn ra ở mỗi frame, dẫn đến frame rate luôn thấp.
- Một tiến trình diễn ra không liên tục, gây ra các "đợt tăng vọt" về độ chậm, dẫn đến tình trạng đình trệ.
- Một tiến trình chậm diễn ra bên ngoài gameplay thông thường, chẳng hạn như khi tải một level.

Mỗi vấn đề trong số này đều gây khó chịu cho người dùng, nhưng theo những cách khác nhau.

Đo hiệu năng
------------

Có lẽ công cụ quan trọng nhất để tối ưu hóa là khả năng đo hiệu năng — xác định các điểm nghẽn và đo lường mức độ thành công của những nỗ lực tăng tốc chúng ta thực hiện.

Có một số phương pháp đo hiệu năng, bao gồm:

- Đặt một bộ hẹn giờ bắt đầu/dừng xung quanh đoạn code cần quan tâm.
- Sử dụng :ref:`Godot profiler <doc_the_profiler>`.
- Sử dụng :ref:`external CPU profilers <doc_using_cpp_profilers>`.
- Sử dụng các profiler/debugger GPU bên ngoài như `NVIDIA Nsight Graphics <https://developer.nvidia.com/nsight-graphics>`__, `Radeon GPU Profiler <https://gpuopen.com/rgp/>`__, `PIX <https://devblogs.microsoft.com/pix/download/>`__ (chỉ Direct3D 12), `Xcode <https://developer.apple.com/documentation/xcode/optimizing-gpu-performance>`__ (chỉ Metal) hoặc `Arm Performance Studio <https://developer.arm.com/Tools%20and%20Software/Arm%20Performance%20Studio>`__.
- Kiểm tra frame rate (khi tắt V-Sync). Các tiện ích của bên thứ ba như `RivaTuner Statistics Server <https://www.guru3d.com/files-details/rtss-rivatuner-statistics-server-download.html>`__ (Windows), `Special K <https://www.special-k.info/>`__ (Windows) hoặc `MangoHud <https://github.com/flightlessmango/MangoHud>`__ (Linux) cũng có thể hữu ích trong trường hợp này.
- Sử dụng `debug menu add-on <https://github.com/godot-extended-libraries/godot-debug-menu>`__ không chính thức.

Hãy lưu ý rằng hiệu năng tương đối của các khu vực khác nhau có thể thay đổi tùy theo phần cứng. Thường thì nên đo thời gian trên nhiều thiết bị. Điều này đặc biệt đúng nếu bạn nhắm đến các thiết bị di động.

Giới hạn
~~~~~~~~

CPU profiler thường là phương pháp được sử dụng đầu tiên để đo hiệu năng. Tuy nhiên, chúng không phải lúc nào cũng cho thấy toàn bộ vấn đề.

- Các điểm nghẽn thường nằm trên GPU, "do" các instruction do CPU cung cấp.
- Các đợt tăng vọt có thể xảy ra trong các tiến trình của hệ điều hành (bên ngoài Godot) "do" các instruction được sử dụng trong Godot (ví dụ: cấp phát bộ nhớ động).
- Bạn có thể không phải lúc nào cũng profile được các thiết bị cụ thể như điện thoại di động do cần thực hiện bước thiết lập ban đầu.
- Bạn có thể phải giải quyết các vấn đề hiệu năng xảy ra trên phần cứng mà bạn không có quyền truy cập.

Do những giới hạn này, bạn thường cần điều tra như một thám tử để tìm ra các điểm nghẽn.

Điều tra như một thám tử
------------------------

Điều tra như một thám tử là một kỹ năng quan trọng đối với các nhà phát triển (cả về hiệu năng lẫn việc sửa lỗi). Việc này có thể bao gồm kiểm thử giả thuyết và tìm kiếm nhị phân.

Kiểm thử giả thuyết
~~~~~~~~~~~~~~~~~~~

Ví dụ, giả sử bạn cho rằng sprite đang làm game chậm đi. Bạn có thể kiểm tra giả thuyết này bằng cách:

- Đo hiệu năng khi thêm hoặc bớt một số sprite.

Điều này có thể dẫn đến một giả thuyết tiếp theo: kích thước của sprite có quyết định mức giảm hiệu năng hay không?

- Bạn có thể kiểm tra điều này bằng cách giữ nguyên mọi thứ, chỉ thay đổi kích thước sprite rồi đo hiệu năng.

Tìm kiếm nhị phân
~~~~~~~~~~~~~~~~~

Nếu bạn biết rằng các frame mất nhiều thời gian hơn đáng lẽ, nhưng không chắc điểm nghẽn nằm ở đâu, bạn có thể bắt đầu bằng cách comment khoảng một nửa số routine diễn ra trong một frame thông thường. Hiệu năng đã cải thiện nhiều hơn hay ít hơn so với dự kiến?

Khi biết nửa nào trong hai nửa chứa điểm nghẽn, bạn có thể lặp lại quy trình này cho đến khi xác định chính xác khu vực có vấn đề.

Profiler
--------

Profiler cho phép bạn tính thời gian chạy của chương trình. Sau đó, profiler cung cấp kết quả cho biết bao nhiêu phần trăm thời gian được dành cho các function và khu vực khác nhau, cũng như tần suất các function được gọi.

Điều này có thể rất hữu ích cả để xác định các điểm nghẽn lẫn đo lường kết quả của những cải tiến. Đôi khi, các nỗ lực cải thiện hiệu năng có thể phản tác dụng và khiến hiệu năng chậm hơn. **Luôn sử dụng profiling và đo thời gian để định hướng nỗ lực của bạn.**

Để biết thêm thông tin về cách sử dụng profiler tích hợp sẵn của Godot, hãy xem :ref:`doc_the_profiler`.

Nguyên tắc
----------

`Donald Knuth <https://en.wikipedia.org/wiki/Donald_Knuth>`__ từng nói:

    *Lập trình viên lãng phí một lượng thời gian khổng lồ để suy nghĩ hoặc lo lắng về tốc độ của những phần không quan trọng trong chương trình, và những nỗ lực nhằm đạt hiệu năng này thực sự gây ảnh hưởng tiêu cực nghiêm trọng khi xét đến việc debug và bảo trì. Chúng ta nên quên đi những tối ưu nhỏ, chẳng hạn trong khoảng 97% thời gian: tối ưu hóa sớm là cội rễ của mọi điều xấu. Tuy vậy, chúng ta không nên bỏ qua cơ hội trong 3% quan trọng đó.*

Những thông điệp này rất quan trọng:

- Thời gian của nhà phát triển là hữu hạn. Thay vì cố gắng một cách mù quáng để tăng tốc mọi khía cạnh của chương trình, chúng ta nên tập trung nỗ lực vào những khía cạnh thực sự quan trọng.
- Các nỗ lực tối ưu hóa thường dẫn đến code khó đọc và debug hơn code chưa được tối ưu. Vì lợi ích của chính mình, chúng ta nên giới hạn việc này ở những khu vực thực sự được hưởng lợi.

Chỉ vì chúng ta *có thể* tối ưu hóa một phần mã cụ thể không có nghĩa là chúng ta *nên* làm vậy. Biết khi nào nên và không nên tối ưu hóa là một kỹ năng tuyệt vời cần phát triển.

Một khía cạnh dễ gây hiểu lầm của câu trích dẫn này là mọi người có xu hướng tập trung vào câu trích dẫn phụ *"tối ưu hóa quá sớm là nguồn gốc của mọi điều xấu"*. Mặc dù việc tối ưu hóa *quá sớm* (theo định nghĩa) là không mong muốn, phần mềm có hiệu năng tốt là kết quả của một thiết kế có hiệu năng tốt.

Thiết kế có hiệu năng tốt
~~~~~~~~~~~~~~~~~~~~~~~~~

Mối nguy hiểm khi khuyến khích mọi người bỏ qua việc tối ưu hóa cho đến khi cần thiết là cách làm này thuận tiện bỏ qua thực tế rằng thời điểm quan trọng nhất để cân nhắc hiệu năng là ở giai đoạn thiết kế, trước cả khi một phím được nhấn trên bàn phím. Nếu thiết kế hoặc các thuật toán của một chương trình không hiệu quả, thì dù có trau chuốt các chi tiết về sau đến đâu cũng không khiến chương trình chạy nhanh. Chương trình có thể chạy *nhanh hơn*, nhưng sẽ không bao giờ chạy nhanh bằng một chương trình được thiết kế để có hiệu năng cao.

Điều này thường quan trọng hơn nhiều trong lập trình game hoặc đồ họa so với lập trình nói chung. Một thiết kế có hiệu năng tốt, ngay cả khi không được tối ưu hóa ở mức thấp, thường sẽ chạy nhanh hơn nhiều lần so với một thiết kế tầm thường có tối ưu hóa ở mức thấp.

Thiết kế tăng dần
~~~~~~~~~~~~~~~~~

Tất nhiên, trong thực tế, trừ khi đã có kiến thức từ trước, bạn khó có thể nghĩ ra thiết kế tốt nhất ngay lần đầu. Thay vào đó, bạn thường sẽ tạo ra một loạt phiên bản cho một khu vực mã cụ thể, mỗi phiên bản tiếp cận vấn đề theo một cách khác nhau, cho đến khi tìm được giải pháp thỏa đáng. Ở giai đoạn này, điều quan trọng là không dành quá nhiều thời gian cho các chi tiết trước khi hoàn thiện thiết kế tổng thể. Nếu không, phần lớn công sức của bạn sẽ bị loại bỏ.

Khó đưa ra các hướng dẫn chung cho một thiết kế có hiệu năng tốt vì điều này phụ thuộc rất nhiều vào vấn đề cần giải quyết. Tuy nhiên, có một điểm đáng đề cập ở phía CPU: các CPU hiện đại gần như luôn bị giới hạn bởi băng thông bộ nhớ. Điều này đã dẫn đến sự hồi sinh của thiết kế hướng dữ liệu, trong đó các cấu trúc dữ liệu và thuật toán được thiết kế để *tận dụng tính cục bộ của cache* dữ liệu và truy cập tuyến tính, thay vì nhảy qua lại trong bộ nhớ.

Quy trình tối ưu hóa
~~~~~~~~~~~~~~~~~~~~

Giả sử chúng ta có một thiết kế hợp lý và rút ra bài học từ Knuth, bước đầu tiên trong quá trình tối ưu hóa nên là xác định các nút thắt lớn nhất - những hàm chậm nhất, những điểm dễ cải thiện nhất.

Sau khi cải thiện thành công tốc độ của khu vực chậm nhất, khu vực đó có thể không còn là nút thắt nữa. Vì vậy, chúng ta nên kiểm tra/profile lại và tìm nút thắt tiếp theo để tập trung vào.

Do đó, quy trình là:

1. Profile / Xác định nút thắt.
2. Tối ưu hóa nút thắt.
3. Quay lại bước 1.

Tối ưu hóa các nút thắt
~~~~~~~~~~~~~~~~~~~~~~~

Một số profiler thậm chí còn cho bạn biết phần nào của một hàm (những lần truy cập dữ liệu, phép tính nào) đang làm chậm chương trình.

Cũng như với thiết kế, trước tiên bạn nên tập trung nỗ lực để đảm bảo các thuật toán và cấu trúc dữ liệu đạt mức tốt nhất có thể. Việc truy cập dữ liệu nên mang tính cục bộ (để tận dụng tốt nhất cache của CPU), và thường nên sử dụng cách lưu trữ dữ liệu nhỏ gọn (một lần nữa, luôn profile để kiểm tra kết quả). Bạn thường tính toán trước các phép tính nặng. Việc này có thể được thực hiện bằng cách tiến hành tính toán khi tải một level, tải một tệp chứa dữ liệu đã được tính toán trước, hoặc lưu kết quả của các phép tính phức tạp vào một hằng số script rồi đọc giá trị của nó.

Khi các thuật toán và dữ liệu đã tốt, bạn thường có thể thực hiện những thay đổi nhỏ trong các routine để cải thiện hiệu năng. Chẳng hạn, bạn có thể đưa một số phép tính ra ngoài các vòng lặp hoặc chuyển đổi các ``for`` vòng lặp lồng nhau thành các vòng lặp không lồng nhau. (Điều này có thể thực hiện được nếu bạn biết trước chiều rộng hoặc chiều cao của một mảng 2D.)

Luôn kiểm tra lại thời gian/nút thắt sau mỗi thay đổi. Một số thay đổi sẽ tăng tốc độ, trong khi những thay đổi khác có thể gây tác động tiêu cực. Đôi khi, tác động tích cực nhỏ sẽ bị lấn át bởi tác động tiêu cực của mã phức tạp hơn, và bạn có thể chọn không đưa tối ưu hóa đó vào.

Phụ lục
-------

Tính toán nút thắt
~~~~~~~~~~~~~~~~~~

Câu tục ngữ *"một sợi xích chỉ mạnh bằng mắt xích yếu nhất"* áp dụng trực tiếp cho việc tối ưu hóa hiệu năng. Nếu dự án của bạn dành 90% thời gian trong hàm ``A``, thì việc tối ưu hóa ``A`` có thể tạo ra tác động rất lớn đến hiệu năng.

.. code-block:: none

    A: 9 ms
    Everything else: 1 ms
    Total frame time: 10 ms

.. code-block:: none

    A: 1 ms
    Everything else: 1ms
    Total frame time: 2 ms

Trong ví dụ này, việc cải thiện nút thắt này ``A`` lên 9 lần làm giảm 5 lần tổng thời gian của mỗi khung hình, đồng thời tăng 5 lần số khung hình trên giây.

Tuy nhiên, nếu có một thành phần khác cũng chạy chậm và đồng thời tạo thành nút thắt cho dự án của bạn, thì cùng một mức cải thiện có thể chỉ mang lại mức tăng ít đáng kể hơn:

.. code-block:: none

    A: 9 ms
    Everything else: 50 ms
    Total frame time: 59 ms

.. code-block:: none

    A: 1 ms
    Everything else: 50 ms
    Total frame time: 51 ms

Trong ví dụ này, mặc dù chúng ta đã tối ưu hóa rất nhiều cho hàm ``A``, mức tăng thực tế xét về tốc độ khung hình lại khá nhỏ.

Trong game, mọi thứ còn phức tạp hơn vì CPU và GPU chạy độc lập với nhau. Tổng thời gian mỗi khung hình được quyết định bởi thành phần chậm hơn trong hai thành phần này.

.. code-block:: none

    CPU: 9 ms
    GPU: 50 ms
    Total frame time: 50 ms

.. code-block:: none

    CPU: 1 ms
    GPU: 50 ms
    Total frame time: 50 ms

Trong ví dụ này, chúng ta lại tối ưu hóa CPU rất nhiều, nhưng thời gian khung hình không được cải thiện vì chúng ta bị giới hạn bởi GPU.
