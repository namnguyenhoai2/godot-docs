.. _doc_introduction_to_godot:

Giới thiệu về Godot
===================

Bài viết này sẽ giúp bạn xác định liệu Godot có phù hợp với mình hay không. Chúng tôi sẽ giới thiệu một số tính năng tổng quan của engine để giúp bạn hình dung những gì có thể đạt được với Godot, đồng thời trả lời các câu hỏi như "tôi cần biết gì để bắt đầu?".

Đây hoàn toàn không phải là phần tổng quan đầy đủ. Chúng tôi sẽ giới thiệu thêm nhiều tính năng trong loạt bài hướng dẫn bắt đầu này.

Godot là gì?
------------

Godot là một game engine 2D và 3D đa dụng, được thiết kế để hỗ trợ mọi loại dự án. Bạn có thể dùng nó để tạo game hoặc ứng dụng, sau đó phát hành trên máy tính để bàn, thiết bị di động cũng như trên web.

Bạn cũng có thể tạo game cho console bằng Godot, mặc dù bạn cần có kỹ năng lập trình vững hoặc cần một developer port game giúp mình.

.. note:: Để biết thông tin về việc hỗ trợ console, hãy xem `website Godot <https://godotengine.org/consoles/>`_.

Engine có thể làm được gì?
--------------------------

Godot ban đầu được một studio game Argentina phát triển nội bộ. Quá trình phát triển bắt đầu vào năm 2001, và engine đã được viết lại cũng như cải tiến đáng kể kể từ khi được phát hành dưới dạng mã nguồn mở vào năm 2014.

Một số game được tạo bằng Godot gồm Cassette Beasts, PVKK và Usagi Shima. Về ứng dụng, chương trình vẽ pixel art mã nguồn mở Pixelorama được xây dựng trên Godot, cũng như công cụ tạo RPG voxel RPG in a Box. Bạn có thể tìm thêm nhiều ví dụ trong `Showcase chính thức <https://godotengine.org/showcase/>`_.

.. figure:: img/introduction_usagi_shima.webp
   :align: center

   Usagi Shima

.. figure:: img/introduction_cassette_beasts.webp
   :align: center

   Cassette Beasts

.. figure:: img/introduction_pvkk.webp
   :align: center

   PVKK: Planetenverteidigungskanonenkommandant

.. figure:: img/introduction_rpg_in_a_box.webp
   :align: center

   RPG in a Box

Godot hoạt động và có giao diện như thế nào?
--------------------------------------------

Godot đi kèm một game editor hoàn chỉnh với các công cụ tích hợp nhằm đáp ứng những nhu cầu phổ biến nhất. Editor bao gồm code editor, animation editor, tilemap editor, shader editor, debugger, profiler và nhiều công cụ khác.

.. image:: img/introduction_editor.webp

Đội ngũ phát triển nỗ lực cung cấp một game editor giàu tính năng với trải nghiệm người dùng nhất quán. Mặc dù luôn còn chỗ để cải thiện, giao diện người dùng vẫn không ngừng được tinh chỉnh.

Tất nhiên, nếu muốn, bạn có thể làm việc với các chương trình bên ngoài. Chúng tôi chính thức hỗ trợ nhập các scene 3D được thiết kế trong Blender_ và duy trì các plugin để viết code bằng VSCode_ và Emacs_ cho GDScript và C#. Chúng tôi cũng hỗ trợ Visual Studio cho C# trên Windows.

.. image:: img/introduction_vscode.png

Ngôn ngữ lập trình
------------------

Hãy cùng tìm hiểu các ngôn ngữ lập trình hiện có.

Bạn có thể lập trình game bằng :ref:`GDScript <doc_gdscript>`, một ngôn ngữ riêng của Godot được tích hợp chặt chẽ với cú pháp nhẹ nhàng, hoặc
:ref:`C# <doc_c_sharp>`, ngôn ngữ phổ biến trong ngành game. Đây là hai ngôn ngữ scripting chính được chúng tôi hỗ trợ.

Với công nghệ :ref:`GDExtension <doc_what_is_gdextension>`, bạn cũng có thể viết gameplay hoặc các thuật toán hiệu năng cao bằng :ref:`C++ <doc_godot_cpp>` hoặc
:ref:`các ngôn ngữ khác <doc_scripting_languages>` mà không cần biên dịch lại engine. Bạn có thể sử dụng công nghệ này để tích hợp các thư viện bên thứ ba và những Software Development Kit (SDK) khác vào engine.

Tất nhiên, bạn cũng có thể trực tiếp thêm các module và tính năng vào engine, vì engine hoàn toàn miễn phí và mã nguồn mở.

.. _doc_introduction_learning_programming:

Tôi cần biết gì để sử dụng Godot?
---------------------------------

Godot là một game engine đầy đủ tính năng. Với hàng nghìn tính năng, có rất nhiều điều cần học. Để tận dụng tối đa engine, bạn cần có nền tảng lập trình tốt. Mặc dù chúng tôi cố gắng làm cho engine dễ tiếp cận, bạn sẽ nhận được nhiều lợi ích nếu trước tiên biết cách tư duy như một programmer.

Godot dựa trên mô hình lập trình hướng đối tượng. Nắm vững các khái niệm như class và object sẽ giúp bạn viết code hiệu quả trong Godot.

Nếu hoàn toàn mới với lập trình, *Learn GDScript From Zero* của GDQuest là một tutorial tương tác miễn phí và mã nguồn mở dành cho người mới bắt đầu, giúp học lập trình bằng ngôn ngữ GDScript của Godot. Tutorial này có sẵn dưới dạng `ứng dụng máy tính để bàn <https://gdquest.itch.io/learn-godot-gdscript>`__ hoặc `trên trình duyệt <https://gdquest.github.io/learn-gdscript>`__.

Chúng tôi sẽ cung cấp thêm cho bạn các tài nguyên học Godot chuyên biệt trong
:ref:`doc_learning_new_features`.

Trong phần tiếp theo, bạn sẽ được tìm hiểu tổng quan về các khái niệm cốt lõi của engine.

.. _Blender: https://www.blender.org/
.. _VSCode: https://github.com/godotengine/godot-vscode-plugin
.. _Emacs: https://github.com/godotengine/emacs-gdscript-mode
.. _official showcase videos: https://www.youtube.com/playlist?list=PLeG_dAglpVo6EpaO9A1nkwJZOwrfiLdQ8

.. _`Godot website`: https://godotengine.org/consoles/
.. _`Official Showcase`: https://godotengine.org/showcase/
