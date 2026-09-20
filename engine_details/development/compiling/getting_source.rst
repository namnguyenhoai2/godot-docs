.. _doc_getting_source:

Lấy mã nguồn
============

.. highlight:: shell

Tải mã nguồn Godot
------------------

Trước khi :ref:`getting into the SCons build system <doc_introduction_to_the_buildsystem>` và biên dịch Godot, bạn cần thực sự tải mã nguồn Godot xuống.

Mã nguồn có sẵn trên `GitHub <https://github.com/godotengine/godot>`__ và mặc dù bạn có thể tải xuống thủ công thông qua trang web, nhìn chung bạn nên thực hiện việc này thông qua hệ thống kiểm soát phiên bản ``git``.

Nếu bạn biên dịch để đóng góp hoặc tạo pull request, bạn nên làm theo hướng dẫn trên trang `Quy trình pull request <https://contributing.godotengine.org/en/latest/organization/pull_requests/creating_pull_requests.html>`__.

Nếu bạn chưa biết nhiều về ``git``, có rất nhiều `hướng dẫn <https://git-scm.com/book>`__ trên nhiều trang web khác nhau.

Nhìn chung, bạn cần cài đặt ``git`` và/hoặc một trong nhiều ứng dụng GUI client.

Sau đó, để lấy phiên bản phát triển mới nhất của mã nguồn Godot (nhánh ``master`` không ổn định), bạn có thể sử dụng ``git clone``.

Nếu bạn đang sử dụng ứng dụng dòng lệnh ``git``, hãy nhập nội dung sau trong terminal:

::

    git clone https://github.com/godotengine/godot.git
    # You can add the --depth 1 argument to omit the commit history (shallow clone).
    # A shallow clone is faster, but not all Git operations (like blame) will work.

Đối với bất kỳ bản phát hành ổn định nào, hãy truy cập `trang bản phát hành <https://github.com/godotengine/godot/releases>`__ và nhấp vào liên kết của bản phát hành bạn muốn. Sau đó, bạn có thể tải xuống và giải nén mã nguồn từ liên kết tải xuống trên trang đó.

Với ``git``, bạn cũng có thể sao chép một bản phát hành ổn định bằng cách chỉ định nhánh hoặc thẻ của bản phát hành đó sau đối số ``--branch`` (hoặc chỉ ``-b``):

::

    # Clone the continuously maintained stable branch (`4.7` as of writing).
    git clone https://github.com/godotengine/godot.git -b 4.7

    # Clone the `4.7-stable` tag. This is a fixed revision that will never change.
    git clone https://github.com/godotengine/godot.git -b 4.7-stable

    # After cloning, optionally go to a specific commit.
    # This can be used to access the source code at a specific point in time,
    # e.g. for development snapshots, betas and release candidates.
    cd godot
    git checkout f4af8201bac157b9d47e336203d3e8a8ef729de2

Các `nhánh bảo trì <https://github.com/godotengine/godot/branches/all>`__ được sử dụng để phát hành các bản vá tiếp theo cho từng phiên bản phụ.

Bạn có thể lấy mã nguồn của từng bản phát hành và bản phát hành thử ở định dạng ``.tar.xz`` từ `godotengine/godot-builds trên GitHub <https://github.com/godotengine/godot-builds/releases>`__. Các tệp này không chứa thông tin kiểm soát phiên bản nhưng có dung lượng tải xuống nhỏ hơn một chút.

Sau khi tải mã nguồn Godot xuống, bạn có thể :ref:`continue to compiling Godot <doc_introduction_to_the_buildsystem>`.
