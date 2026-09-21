:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Mutex.xml.

.. _class_Mutex:

Mutex
=====

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`Semaphore<class_Semaphore>` nhị phân để đồng bộ hóa nhiều :ref:`Thread<class_Thread>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mutex đồng bộ hóa (mutual exclusion). Mutex này được dùng để đồng bộ hóa nhiều :ref:`Thread<class_Thread>`\ s và tương đương với một :ref:`Semaphore<class_Semaphore>` nhị phân. Nó đảm bảo rằng tại một thời điểm chỉ có một thread có thể truy cập một vùng tới hạn.

Đây là một mutex có thể tái nhập (reentrant), nghĩa là một thread có thể khóa nó nhiều lần, miễn là thread đó cũng mở khóa nó với số lần tương ứng.

\ **Cảnh báo:** Để đảm bảo quá trình dọn dẹp diễn ra đúng cách mà không gây crash hoặc deadlock, phải đáp ứng các điều kiện sau:

- Khi số lượng tham chiếu của **Mutex** đạt đến 0 và do đó nó bị hủy, không thread nào (bao gồm cả thread thực hiện việc hủy) được phép đang khóa nó.

- Khi số lượng tham chiếu của :ref:`Thread<class_Thread>` đạt đến 0 và do đó nó bị hủy, nó không được khóa bất kỳ mutex nào.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng nhiều thread <../tutorials/performance/using_multiple_threads>`

- :doc:`Các API an toàn với thread <../tutorials/performance/thread_safe_apis>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------+
   | |void|                  | :ref:`lock<class_Mutex_method_lock>`\ (\ )         |
   +-------------------------+----------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`try_lock<class_Mutex_method_try_lock>`\ (\ ) |
   +-------------------------+----------------------------------------------------+
   | |void|                  | :ref:`unlock<class_Mutex_method_unlock>`\ (\ )     |
   +-------------------------+----------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Mutex_method_lock:

.. rst-class:: classref-method

|void| **lock**\ (\ ) :ref:`🔗<class_Mutex_method_lock>`

Khóa **Mutex** này và chặn cho đến khi chủ sở hữu hiện tại mở khóa nó.

\ **Lưu ý:** Hàm này trả về mà không chặn nếu thread đã sở hữu mutex.

.. rst-class:: classref-item-separator

----

.. _class_Mutex_method_try_lock:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **try_lock**\ (\ ) :ref:`🔗<class_Mutex_method_try_lock>`

Thử khóa **Mutex** này nhưng không chặn. Trả về ``true`` nếu thành công, nếu không thì trả về ``false``.

\ **Lưu ý:** Hàm này trả về ``true`` nếu thread đã sở hữu mutex.

.. rst-class:: classref-item-separator

----

.. _class_Mutex_method_unlock:

.. rst-class:: classref-method

|void| **unlock**\ (\ ) :ref:`🔗<class_Mutex_method_unlock>`

Mở khóa **Mutex** này, cho phép các thread khác sử dụng nó.

\ **Lưu ý:** Nếu một thread gọi :ref:`lock()<class_Mutex_method_lock>` hoặc :ref:`try_lock()<class_Mutex_method_try_lock>` nhiều lần trong khi đã sở hữu mutex, thread đó cũng phải gọi :ref:`unlock()<class_Mutex_method_unlock>` với cùng số lần để mở khóa nó đúng cách.

\ **Cảnh báo:** Gọi :ref:`unlock()<class_Mutex_method_unlock>` nhiều lần hơn :ref:`lock()<class_Mutex_method_lock>` trên một thread nhất định, dẫn đến việc cố mở khóa một mutex chưa được khóa, là sai và có thể gây crash hoặc deadlock.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
