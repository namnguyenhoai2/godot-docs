.. _doc_general_optimization:

Các mẹo tối ưu hóa chung
========================

Giới thiệu
----------

Trong một thế giới lý tưởng, máy tính sẽ chạy với tốc độ vô hạn. Giới hạn duy nhất đối với những gì chúng ta có thể đạt được sẽ là trí tưởng tượng của chúng ta. Tuy nhiên, trong thế giới thực, việc tạo ra phần mềm khiến ngay cả máy tính nhanh nhất cũng phải chậm lại đến mức gần như không thể hoạt động là điều quá dễ xảy ra.

Vì vậy, việc thiết kế game và các phần mềm khác là sự thỏa hiệp giữa những gì chúng ta muốn có thể thực hiện được và những gì chúng ta có thể thực tế đạt được trong khi vẫn duy trì hiệu năng tốt.

Để đạt được kết quả tốt nhất, chúng ta có hai cách tiếp cận:

- Làm việc nhanh hơn. - Làm việc thông minh hơn.

Và tốt nhất là chúng ta sẽ kết hợp cả hai.

Đánh lạc hướng và tạo ảo giác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một phần của việc làm việc thông minh hơn là nhận ra rằng trong game, chúng ta thường có thể khiến người chơi tin rằng họ đang ở trong một thế giới phức tạp, tương tác và thú vị về mặt đồ họa hơn rất nhiều so với thực tế. Một programmer giỏi là một ảo thuật gia, và nên cố gắng học hỏi các mánh khóe trong nghề, đồng thời tìm cách sáng tạo ra những mánh khóe mới.

Bản chất của sự chậm chạp
~~~~~~~~~~~~~~~~~~~~~~~~~

Đối với người quan sát bên ngoài, các vấn đề về hiệu năng thường bị gộp chung với nhau. Nhưng trên thực tế, có một số loại vấn đề về hiệu năng khác nhau:

- Một quy trình chậm diễn ra ở mỗi frame, dẫn đến frame rate liên tục thấp. - Một quy trình diễn ra không liên tục gây ra các "spike" chậm, dẫn đến tình trạng đình trệ. - Một quy trình chậm diễn ra bên ngoài gameplay thông thường, chẳng hạn như khi tải một level.

Mỗi vấn đề này đều gây khó chịu cho người dùng, nhưng theo những cách khác nhau.

Đo lường hiệu năng
------------------

Có lẽ công cụ quan trọng nhất để tối ưu hóa là khả năng đo lường hiệu năng — xác định vị trí của các bottleneck và đo lường mức độ thành công của những nỗ lực tăng tốc chúng ta thực hiện.

Có một số phương pháp đo lường hiệu năng, bao gồm:

- Đặt bộ đếm thời gian bắt đầu/dừng xung quanh đoạn code cần quan tâm. - Sử dụng :ref:`Godot profiler <doc_the_profiler>`. - Sử dụng :ref:`external CPU profilers <doc_using_cpp_profilers>`. - Sử dụng các GPU profiler/debugger bên ngoài như `NVIDIA Nsight Graphics <https://developer.nvidia.com/nsight-graphics>`__, `Radeon GPU Profiler <https://gpuopen.com/rgp/>`__, `PIX <https://devblogs.microsoft.com/pix/download/>`__ (chỉ dành cho Direct3D 12), `Xcode <https://developer.apple.com/documentation/xcode/optimizing-gpu-performance>`__ (chỉ dành cho Metal) hoặc `Arm Performance Studio <https://developer.arm.com/Tools%20and%20Software/Arm%20Performance%20Studio>`__. - Kiểm tra frame rate (khi đã tắt V-Sync). Các tiện ích bên thứ ba như `RivaTuner Statistics Server <https://www.guru3d.com/files-details/rtss-rivatuner-statistics-server-download.html>`__ (Windows), `Special K <https://www.special-k.info/>`__ (Windows) hoặc `MangoHud <https://github.com/flightlessmango/MangoHud>`__ (Linux) cũng có thể hữu ích trong trường hợp này. - Sử dụng một `debug menu add-on <https://github.com/godot-extended-libraries/godot-debug-menu>`__ không chính thức.

Hãy đặc biệt lưu ý rằng hiệu năng tương đối của các khu vực khác nhau có thể thay đổi tùy theo phần cứng. Thường thì đo thời gian trên nhiều thiết bị là một ý hay. Điều này đặc biệt đúng nếu bạn nhắm đến các thiết bị di động.

Các giới hạn
~~~~~~~~~~~~

CPU profiler thường là phương pháp được sử dụng đầu tiên để đo lường hiệu năng. Tuy nhiên, chúng không phải lúc nào cũng cho bạn biết toàn bộ câu chuyện.

- Các bottleneck thường nằm ở GPU, "do" những instruction mà CPU đưa ra. - Các spike có thể xảy ra trong các process của hệ điều hành (bên ngoài Godot) "do" những instruction được sử dụng trong Godot (ví dụ: cấp phát bộ nhớ động). - Bạn có thể không phải lúc nào cũng profile được các thiết bị cụ thể như điện thoại di động do yêu cầu thiết lập ban đầu. - Bạn có thể phải giải quyết các vấn đề về hiệu năng xảy ra trên phần cứng mà bạn không có quyền truy cập.

Do những giới hạn này, bạn thường cần sử dụng công việc điều tra để tìm ra vị trí của các bottleneck.

Công việc điều tra
------------------

Công việc điều tra là một kỹ năng then chốt đối với developer (cả về hiệu năng lẫn sửa lỗi). Công việc này có thể bao gồm kiểm thử giả thuyết và tìm kiếm nhị phân.

Kiểm thử giả thuyết
~~~~~~~~~~~~~~~~~~~

Ví dụ, giả sử bạn tin rằng các sprite đang làm game chậm đi. Bạn có thể kiểm thử giả thuyết này bằng cách:

- Đo lường hiệu năng khi bạn thêm hoặc bớt một số sprite.

Điều này có thể dẫn đến một giả thuyết tiếp theo: kích thước của sprite có quyết định mức sụt giảm hiệu năng hay không?

- Bạn có thể kiểm thử điều này bằng cách giữ nguyên mọi thứ, chỉ thay đổi kích thước sprite và đo lường hiệu năng.

Tìm kiếm nhị phân
~~~~~~~~~~~~~~~~~

Nếu bạn biết rằng các frame mất nhiều thời gian hơn đáng lẽ, nhưng không chắc bottleneck nằm ở đâu, bạn có thể bắt đầu bằng cách comment out khoảng một nửa số routine diễn ra trong một frame bình thường. Hiệu năng đã cải thiện nhiều hơn hay ít hơn so với dự kiến?

Khi biết nửa nào trong hai nửa chứa bottleneck, bạn có thể lặp lại quy trình này cho đến khi xác định chính xác khu vực có vấn đề.

Profiler
--------

Profiler cho phép bạn đo thời gian chạy của chương trình. Sau đó, profiler cung cấp các kết quả cho biết bao nhiêu phần trăm thời gian được dành cho các function và khu vực khác nhau, cũng như tần suất các function được gọi.

Điều này có thể rất hữu ích, cả để xác định bottleneck lẫn đo lường kết quả của những cải tiến bạn thực hiện. Đôi khi, các nỗ lực cải thiện hiệu năng có thể phản tác dụng và dẫn đến hiệu năng chậm hơn. **Luôn sử dụng profiling và đo thời gian để định hướng nỗ lực của bạn.**

Để biết thêm thông tin về cách sử dụng profiler tích hợp sẵn của Godot, hãy xem :ref:`doc_the_profiler`.

Các nguyên tắc
--------------

`Donald Knuth <https://en.wikipedia.org/wiki/Donald_Knuth>`__ đã nói:

    *Các programmer lãng phí một lượng thời gian khổng lồ để suy nghĩ hoặc lo lắng về tốc độ của những phần không quan trọng trong chương trình, và những nỗ lực nhằm đạt hiệu quả này thực sự gây ảnh hưởng tiêu cực lớn khi xét đến việc debug và bảo trì. Chúng ta nên quên đi những tối ưu hóa nhỏ, có thể nói là trong khoảng 97% thời gian: tối ưu hóa quá sớm là cội nguồn của mọi điều xấu. Tuy nhiên, chúng ta không nên bỏ qua những cơ hội trong 3% quan trọng đó.*

Các thông điệp này rất quan trọng:

- Thời gian của developer là có hạn. Thay vì mù quáng cố gắng tăng tốc mọi khía cạnh của một chương trình, chúng ta nên tập trung nỗ lực vào những khía cạnh thực sự quan trọng. - Những nỗ lực tối ưu hóa thường dẫn đến code khó đọc và debug hơn code chưa được tối ưu. Vì lợi ích của chính chúng ta, cần giới hạn điều này ở những khu vực thực sự được hưởng lợi.

Chỉ vì chúng ta *có thể* tối ưu hóa một phần code cụ thể không có nghĩa là chúng ta nhất thiết *nên* làm vậy. Biết khi nào nên và không nên tối ưu hóa là một kỹ năng tuyệt vời cần phát triển.

Một khía cạnh dễ gây hiểu lầm của câu trích dẫn này là mọi người có xu hướng tập trung vào phần trích dẫn phụ *"tối ưu hóa quá sớm là cội nguồn của mọi điều xấu"*. Mặc dù tối ưu hóa *quá sớm* (theo định nghĩa) là không mong muốn, phần mềm có hiệu năng tốt là kết quả của một thiết kế có hiệu năng tốt.

Thiết kế có hiệu năng tốt
~~~~~~~~~~~~~~~~~~~~~~~~~

Mối nguy hiểm của việc khuyến khích mọi người bỏ qua tối ưu hóa cho đến khi cần thiết là điều đó vô tình bỏ qua thời điểm quan trọng nhất để cân nhắc hiệu năng: giai đoạn thiết kế, trước cả khi một phím được nhấn trên bàn phím. Nếu thiết kế hoặc các thuật toán của một chương trình không hiệu quả, thì dù có trau chuốt các chi tiết về sau đến đâu cũng không thể khiến chương trình chạy nhanh. Nó có thể chạy *nhanh hơn*, nhưng sẽ không bao giờ nhanh bằng một chương trình được thiết kế để đạt hiệu năng cao.

Điều này thường quan trọng hơn nhiều trong lập trình game hoặc đồ họa so với lập trình nói chung. Một thiết kế có hiệu năng tốt, ngay cả khi không có tối ưu hóa cấp thấp, thường sẽ chạy nhanh hơn nhiều lần so với một thiết kế tầm thường có tối ưu hóa cấp thấp.

Thiết kế từng bước
~~~~~~~~~~~~~~~~~~

Tất nhiên, trên thực tế, trừ khi đã có kiến thức từ trước, bạn khó có thể đưa ra thiết kế tốt nhất ngay lần đầu. Thay vào đó, bạn thường sẽ tạo ra một loạt phiên bản của một khu vực code cụ thể, mỗi phiên bản tiếp cận vấn đề theo một cách khác nhau, cho đến khi tìm được giải pháp thỏa đáng. Ở giai đoạn này, điều quan trọng là không dành quá nhiều thời gian cho các chi tiết trước khi hoàn tất thiết kế tổng thể. Nếu không, phần lớn công việc của bạn sẽ bị loại bỏ.

Rất khó đưa ra các hướng dẫn chung cho thiết kế có hiệu năng tốt vì điều này phụ thuộc rất nhiều vào vấn đề cụ thể. Tuy nhiên, một điểm đáng đề cập ở phía CPU là các CPU hiện đại gần như luôn bị giới hạn bởi băng thông bộ nhớ. Điều này đã dẫn đến sự hồi sinh của thiết kế hướng dữ liệu, trong đó các cấu trúc dữ liệu và thuật toán được thiết kế để tối ưu *cache locality* của dữ liệu và truy cập tuyến tính, thay vì nhảy qua lại trong bộ nhớ.

Quy trình tối ưu hóa
~~~~~~~~~~~~~~~~~~~~

Giả sử chúng ta có một thiết kế hợp lý và rút ra bài học từ Knuth, bước đầu tiên trong quá trình tối ưu hóa nên là xác định các bottleneck lớn nhất — những function chậm nhất, những mục tiêu dễ đạt được nhất.

Sau khi cải thiện thành công tốc độ của khu vực chậm nhất, khu vực đó có thể không còn là bottleneck nữa. Vì vậy, chúng ta nên kiểm thử/profile lại và tìm bottleneck tiếp theo để tập trung vào đó.

Do đó, quy trình là:

1. Profile / Xác định bottleneck. 2. Tối ưu hóa bottleneck. 3. Quay lại bước 1.

Tối ưu hóa bottleneck
~~~~~~~~~~~~~~~~~~~~~

Một số profiler thậm chí còn cho bạn biết phần nào của một function (những lần truy cập dữ liệu, phép tính nào) đang làm chậm mọi thứ.

Cũng như với thiết kế, trước tiên bạn nên tập trung nỗ lực để bảo đảm các thuật toán và cấu trúc dữ liệu đạt mức tốt nhất có thể. Việc truy cập dữ liệu nên mang tính cục bộ (để tận dụng tốt nhất CPU cache), và thường thì sử dụng cách lưu trữ dữ liệu nhỏ gọn sẽ tốt hơn (một lần nữa, luôn profile để kiểm thử kết quả). Thông thường, bạn sẽ tính toán trước các phép tính nặng. Việc này có thể được thực hiện bằng cách thực hiện phép tính khi tải một level, tải một file chứa dữ liệu đã được tính toán trước, hoặc lưu kết quả của các phép tính phức tạp vào một hằng số của script rồi đọc giá trị của nó.

Khi các algorithm và data đã ổn, bạn thường có thể thực hiện những thay đổi nhỏ trong các routine để cải thiện performance. Chẳng hạn, bạn có thể đưa một số phép tính ra bên ngoài các vòng lặp hoặc chuyển các vòng lặp ``for`` lồng nhau thành các vòng lặp không lồng nhau. (Điều này sẽ khả thi nếu bạn biết trước width hoặc height của một mảng 2D.)

Luôn kiểm tra lại timing/bottleneck sau mỗi thay đổi. Một số thay đổi sẽ tăng speed, trong khi những thay đổi khác có thể gây tác động tiêu cực. Đôi khi, hiệu ứng tích cực nhỏ sẽ bị tác động tiêu cực của code phức tạp hơn lấn át, và bạn có thể chọn không đưa optimization đó vào.

Phụ lục
-------

Tính toán bottleneck
~~~~~~~~~~~~~~~~~~~~

Câu ngạn ngữ *"a chain is only as strong as its weakest link"* áp dụng trực tiếp vào việc tối ưu performance. Nếu project của bạn dành 90% thời gian trong hàm ``A``, thì việc tối ưu ``A`` có thể tạo ra ảnh hưởng rất lớn đến performance.

.. code-block:: none

    A: 9 ms
    Everything else: 1 ms
    Total frame time: 10 ms

.. code-block:: none

    A: 1 ms
    Everything else: 1ms
    Total frame time: 2 ms

Trong ví dụ này, việc cải thiện bottleneck ``A`` lên 9 lần làm giảm thời gian tổng thể của frame xuống 5 lần, đồng thời tăng số frames per second lên 5 lần.

Tuy nhiên, nếu một yếu tố khác cũng đang chạy chậm và đồng thời trở thành bottleneck của project, thì cùng một cải thiện đó có thể chỉ mang lại mức tăng ít đáng kể hơn:

.. code-block:: none

    A: 9 ms
    Everything else: 50 ms
    Total frame time: 59 ms

.. code-block:: none

    A: 1 ms
    Everything else: 50 ms
    Total frame time: 51 ms

Trong ví dụ này, mặc dù chúng ta đã tối ưu hàm ``A`` rất nhiều, mức tăng thực tế xét về frame rate lại khá nhỏ.

Trong game, mọi việc còn phức tạp hơn vì CPU và GPU chạy độc lập với nhau. Tổng thời gian của frame được quyết định bởi thành phần chậm hơn trong hai thành phần này.

.. code-block:: none

    CPU: 9 ms
    GPU: 50 ms
    Total frame time: 50 ms

.. code-block:: none

    CPU: 1 ms
    GPU: 50 ms
    Total frame time: 50 ms

Trong ví dụ này, một lần nữa chúng ta đã tối ưu CPU rất nhiều, nhưng thời gian của frame không được cải thiện vì bottleneck nằm ở GPU.
