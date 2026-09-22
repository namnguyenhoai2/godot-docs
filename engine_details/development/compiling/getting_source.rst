.. _doc_getting_source:

Lấy mã nguồn
============

.. highlight:: shell

Tải xuống mã nguồn Godot
------------------------

Trước khi :ref:`bắt đầu tìm hiểu hệ thống build SCons <doc_introduction_to_the_buildsystem>` và biên dịch Godot, bạn cần thực sự tải xuống mã nguồn Godot.

Mã nguồn có trên `GitHub <https://github.com/godotengine/godot>`__ và mặc dù bạn có thể tải xuống thủ công qua trang web, nhìn chung bạn nên thực hiện việc này thông qua ``git`` hệ thống quản lý phiên bản.

Nếu bạn biên dịch để đóng góp hoặc tạo pull request, hãy làm theo hướng dẫn trên trang `Quy trình pull request <https://contributing.godotengine.org/en/latest/organization/pull_requests/creating_pull_requests.html>`__.

Nếu bạn chưa biết nhiều về ``git``, có rất nhiều `hướng dẫn <https://git-scm.com/book>`__ trên nhiều trang web khác nhau.

Nhìn chung, bạn cần cài đặt ``git`` và/hoặc một trong các GUI client khác nhau.

Sau đó, để lấy phiên bản phát triển mới nhất của mã nguồn Godot (nhánh ``master`` không ổn định), bạn có thể sử dụng ``git clone``.

Nếu bạn sử dụng ``git`` command line client, hãy nhập lệnh sau vào terminal:

::

    git clone https://github.com/godotengine/godot.git # Bạn có thể thêm đối số --depth 1 để bỏ qua lịch sử commit (shallow clone). # Shallow clone nhanh hơn, nhưng không phải mọi thao tác Git (chẳng hạn như blame) đều hoạt động.

Đối với bất kỳ bản phát hành ổn định nào, hãy truy cập `trang phát hành <https://github.com/godotengine/godot/releases>`__ và nhấp vào liên kết của bản phát hành bạn muốn. Sau đó, bạn có thể tải xuống và giải nén mã nguồn từ liên kết tải xuống trên trang đó.

Với ``git``, bạn cũng có thể clone một bản phát hành ổn định bằng cách chỉ định branch hoặc tag của bản đó sau đối số ``--branch`` (hoặc chỉ cần đối số ``-b``):

::

    # Clone stable branch được duy trì liên tục (`4.7` tại thời điểm viết tài liệu). git clone https://github.com/godotengine/godot.git -b 4.7

    # Clone tag `4.7-stable`. Đây là một revision cố định và sẽ không bao giờ thay đổi. git clone https://github.com/godotengine/godot.git -b 4.7-stable

    # Sau khi clone, bạn có thể chuyển đến một commit cụ thể nếu muốn. # Có thể dùng cách này để truy cập mã nguồn tại một thời điểm cụ thể, # chẳng hạn như đối với development snapshot, beta và release candidate. cd godot git checkout f4af8201bac157b9d47e336203d3e8a8ef729de2

Các `nhánh bảo trì <https://github.com/godotengine/godot/branches/all>`__ được dùng để phát hành các bản vá tiếp theo cho từng phiên bản minor.

Bạn có thể lấy mã nguồn của từng bản phát hành và bản phát hành trước ở định dạng ``.tar.xz`` từ `godotengine/godot-builds trên GitHub <https://github.com/godotengine/godot-builds/releases>`__. Bản này không có thông tin quản lý phiên bản nhưng có dung lượng tải xuống nhỏ hơn một chút.

Sau khi tải xuống mã nguồn Godot, bạn có thể :ref:`tiếp tục biên dịch Godot <doc_introduction_to_the_buildsystem>`.
