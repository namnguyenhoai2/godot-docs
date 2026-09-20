.. _doc_c_sharp_collections:

Các collection trong C#
=======================

Thư viện lớp cơ sở .NET chứa nhiều loại collection có thể được sử dụng để lưu trữ và thao tác với dữ liệu. Godot cũng cung cấp một số loại collection được tích hợp chặt chẽ với phần còn lại của engine.

Chọn một collection
-------------------

Điểm khác biệt chính giữa `.NET collections <https://learn.microsoft.com/en-us/dotnet/standard/collections/>`_ và các collection của Godot là các collection .NET được triển khai bằng C#, trong khi các collection của Godot được triển khai bằng C++ và C# API của Godot chỉ là một wrapper cho chúng. Đây là một điểm khác biệt quan trọng, vì điều đó có nghĩa là mọi thao tác trên collection của Godot đều yêu cầu marshaling, việc này có thể tốn kém, đặc biệt là bên trong một vòng lặp.

Do những ảnh hưởng đến hiệu năng, chỉ nên sử dụng các collection của Godot khi thực sự cần thiết (chẳng hạn như khi tương tác với Godot API). Godot chỉ hiểu các loại collection của riêng nó, vì vậy bắt buộc phải sử dụng chúng khi giao tiếp với engine.

Nếu bạn có một collection các phần tử không cần truyền vào Godot API, việc sử dụng collection .NET sẽ có hiệu năng tốt hơn.

.. tip::

    Bạn cũng có thể chuyển đổi giữa các collection .NET và các collection của Godot. Các collection của Godot có các constructor nhận các generic .NET collection interface và sao chép các phần tử của chúng, đồng thời các collection của Godot có thể được sử dụng với các phương thức `LINQ <https://learn.microsoft.com/en-us/dotnet/standard/linq>`_ ``ToList``, ``ToArray`` và ``ToDictionary``. Tuy nhiên, hãy nhớ rằng việc chuyển đổi này yêu cầu marshaling mọi phần tử trong collection và sao chép chúng vào một collection mới, nên có thể tốn kém.

Mặc dù vậy, các collection của Godot được tối ưu hóa để cố gắng tránh marshaling không cần thiết, vì vậy các phương thức như ``Sort`` hoặc ``Reverse`` được triển khai bằng một interop call duy nhất và không cần marshal từng phần tử. Hãy chú ý đến các generic API nhận các collection interface như `LINQ <https://learn.microsoft.com/en-us/dotnet/standard/linq>`_, vì mọi phương thức đều yêu cầu lặp qua collection và do đó marshaling từng phần tử. Khi có thể, hãy ưu tiên sử dụng các instance method của collection Godot.

Để chọn loại collection sẽ sử dụng trong từng trường hợp, hãy cân nhắc các câu hỏi sau:

* Collection của bạn có cần tương tác với Godot engine không? (ví dụ: kiểu của một exported property, gọi một phương thức Godot).

   * Nếu có, vì Godot chỉ hỗ trợ :ref:`c_sharp_variant_compatible_types`, hãy sử dụng một collection Godot. * Nếu không, hãy cân nhắc `choosing an appropriate .NET collection <https://learn.microsoft.com/en-us/dotnet/standard/collections/selecting-a-collection-class>`_.

* Bạn có cần một collection Godot biểu diễn một danh sách hoặc một tập dữ liệu tuần tự không?

   * :ref:`arrays <doc_c_sharp_collections_array>` của Godot tương tự như collection C# ``List<T>``. * :ref:`packed arrays <doc_c_sharp_collections_packedarray>` của Godot là các mảng tiết kiệm bộ nhớ hơn; trong C#, hãy sử dụng một trong các loại ``System.Array`` được hỗ trợ.

* Bạn có cần một collection Godot ánh xạ một tập khóa với một tập giá trị không?

   * :ref:`dictionaries <doc_c_sharp_collections_dictionary>` của Godot lưu trữ các cặp khóa và giá trị, đồng thời cho phép dễ dàng truy cập các giá trị thông qua khóa tương ứng của chúng.

Các collection của Godot
------------------------

.. _doc_c_sharp_collections_packedarray:

PackedArray
~~~~~~~~~~~

Các packed array của Godot được triển khai dưới dạng một mảng chứa một kiểu cụ thể, cho phép đóng gói chặt chẽ hơn vì mỗi phần tử có kích thước của kiểu cụ thể đó, thay vì ``Variant``.

Trong C#, packed array được thay thế bằng ``System.Array``:

======================  ==============================================================
GDScript                C#
======================  ==============================================================
``PackedByteArray``     ``byte[]``
``PackedInt32Array``    ``int[]``
``PackedInt64Array``    ``long[]``
``PackedFloat32Array``  ``float[]``
``PackedFloat64Array``  ``double[]``
``PackedStringArray``   ``string[]``
``PackedVector2Array``  ``Vector2[]``
``PackedVector3Array``  ``Vector3[]``
``PackedVector4Array``  ``Vector4[]``
``PackedColorArray``    ``Color[]``
======================  ==============================================================

Các mảng C# khác không được Godot C# API hỗ trợ vì không tồn tại kiểu tương đương với packed array. Xem danh sách :ref:`c_sharp_variant_compatible_types`.

.. _doc_c_sharp_collections_array:

Array
~~~~~

Các array của Godot được triển khai dưới dạng một mảng gồm ``Variant`` và có thể chứa nhiều phần tử thuộc bất kỳ kiểu nào. Trong C#, kiểu tương đương là ``Godot.Collections.Array``.

Kiểu generic ``Godot.Collections.Array<T>`` cho phép giới hạn kiểu phần tử thành một :ref:`Variant-compatible type <c_sharp_variant_compatible_types>`.

Một ``Godot.Collections.Array`` không định kiểu có thể được chuyển đổi thành một array có kiểu bằng constructor ``Godot.Collections.Array<T>(Godot.Collections.Array)``.

.. note::

    Mặc dù có tên như vậy, các array của Godot tương tự với collection C# ``List<T>`` hơn là ``System.Array``. Kích thước của chúng không cố định và có thể tăng hoặc giảm khi các phần tử được thêm vào hoặc xóa khỏi collection.

Danh sách các phương thức Array của Godot và phương thức tương đương trong C#:

=======================  ==============================================================
GDScript                 C#
=======================  ==============================================================
all                      `System.Linq.Enumerable.All`_
any                      `System.Linq.Enumerable.Any`_
append                   Add
append_array             AddRange
assign                   Clear and AddRange
back                     ``Array[^1]`` or `System.Linq.Enumerable.Last`_ or `System.Linq.Enumerable.LastOrDefault`_
bsearch                  BinarySearch
bsearch_custom           N/A
clear                    Clear
count                    `System.Linq.Enumerable.Count`_
duplicate                Duplicate
erase                    Remove
fill                     Fill
filter                   Use `System.Linq.Enumerable.Where`_
find                     IndexOf
front                    ``Array[0]`` or `System.Linq.Enumerable.First`_ or `System.Linq.Enumerable.FirstOrDefault`_
get_typed_builtin        N/A
get_typed_class_name     N/A
get_typed_script         N/A
has                      Contains
hash                     GD.Hash
insert                   Insert
is_empty                 Use ``Count == 0``
is_read_only             IsReadOnly
is_same_typed            N/A
is_typed                 N/A
make_read_only           MakeReadOnly
map                      `System.Linq.Enumerable.Select`_
max                      Max
min                      Min
pick_random              PickRandom (Consider using `System.Random`_)
pop_at                   ``Array[i]`` with ``RemoveAt(i)``
pop_back                 ``Array[^1]`` with ``RemoveAt(Count - 1)``
pop_front                ``Array[0]`` with ``RemoveAt(0)``
push_back                ``Insert(Count, item)``
push_front               ``Insert(0, item)``
reduce                   `System.Linq.Enumerable.Aggregate`_
remove_at                RemoveAt
resize                   Resize
reverse                  Reverse
rfind                    LastIndexOf
shuffle                  Shuffle
size                     Count
slice                    Slice
sort                     Sort
sort_custom              `System.Linq.Enumerable.OrderBy`_
operator !=              !RecursiveEqual
operator +               operator +
operator <               N/A
operator <=              N/A
operator ==              RecursiveEqual
operator >               N/A
operator >=              N/A
operator []              Array[int] indexer
=======================  ==============================================================

.. _System.Random: https://learn.microsoft.com/en-us/dotnet/api/system.random
.. _System.Linq.Enumerable.Aggregate: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.aggregate
.. _System.Linq.Enumerable.All: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.all
.. _System.Linq.Enumerable.Any: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.any
.. _System.Linq.Enumerable.Count: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.count
.. _System.Linq.Enumerable.First: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.first
.. _System.Linq.Enumerable.FirstOrDefault: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.firstordefault
.. _System.Linq.Enumerable.Last: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.last
.. _System.Linq.Enumerable.LastOrDefault: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.lastordefault
.. _System.Linq.Enumerable.OrderBy: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderby
.. _System.Linq.Enumerable.Select: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.select
.. _System.Linq.Enumerable.Where: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.where

.. _doc_c_sharp_collections_dictionary:

Dictionary
~~~~~~~~~~

Các dictionary của Godot được triển khai dưới dạng một dictionary với các khóa và giá trị ``Variant``. Trong C#, kiểu tương đương là ``Godot.Collections.Dictionary``.

Kiểu generic ``Godot.Collections.Dictionary<TKey, TValue>`` cho phép giới hạn kiểu khóa và giá trị thành một :ref:`Variant-compatible type <c_sharp_variant_compatible_types>`.

Một ``Godot.Collections.Dictionary`` không định kiểu có thể được chuyển đổi thành một dictionary có kiểu bằng constructor ``Godot.Collections.Dictionary<TKey, TValue>(Godot.Collections.Dictionary)``.

.. tip::

    Nếu bạn cần một dictionary trong đó khóa có kiểu nhưng giá trị thì không, hãy sử dụng ``Variant`` làm tham số generic ``TValue`` của dictionary có kiểu.

    .. code-block:: csharp

        // Các khóa phải là string, nhưng các giá trị có thể là bất kỳ kiểu nào tương thích với Variant.
        var dictionary = new Godot.Collections.Dictionary<string, Variant>();

Danh sách các phương thức Dictionary của Godot và phương thức tương đương trong C#:

=======================  ==============================================================
GDScript                 C#
=======================  ==============================================================
clear                    Clear
duplicate                Duplicate
erase                    Remove
find_key                 N/A
get                      Dictionary[Variant] indexer or TryGetValue
has                      ContainsKey
has_all                  N/A
hash                     GD.Hash
is_empty                 Use ``Count == 0``
is_read_only             IsReadOnly
keys                     Keys
make_read_only           MakeReadOnly
merge                    Merge
size                     Count
values                   Values
operator !=              !RecursiveEqual
operator ==              RecursiveEqual
operator []              Dictionary[Variant] indexer, Add or TryGetValue
=======================  ==============================================================
