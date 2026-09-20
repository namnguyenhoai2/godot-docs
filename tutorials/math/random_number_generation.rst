.. _doc_random_number_generation:

Tạo số ngẫu nhiên
=================

Nhiều trò chơi dựa vào tính ngẫu nhiên để triển khai các cơ chế cốt lõi của trò chơi. Trang này hướng dẫn bạn về các loại tính ngẫu nhiên phổ biến và cách triển khai chúng trong Godot.

Sau khi cung cấp cho bạn phần tổng quan ngắn gọn về các hàm hữu ích để tạo số ngẫu nhiên, bạn sẽ học cách lấy các phần tử ngẫu nhiên từ array, dictionary và cách sử dụng trình tạo nhiễu trong GDScript. Cuối cùng, chúng ta sẽ tìm hiểu về việc tạo số ngẫu nhiên an toàn về mặt mật mã và điểm khác biệt của nó so với việc tạo số ngẫu nhiên thông thường.

.. note::

    Máy tính không thể tạo ra các số ngẫu nhiên "thực sự". Thay vào đó, chúng dựa vào `pseudorandom number generators <https://en.wikipedia.org/wiki/Pseudorandom_number_generator>`__ (PRNG).

    Godot sử dụng nội bộ `PCG Family <https://www.pcg-random.org/>`__ của các trình tạo số giả ngẫu nhiên.

Global scope so với class RandomNumberGenerator
-----------------------------------------------

Godot cung cấp hai cách để tạo số ngẫu nhiên: thông qua các phương thức *global scope* hoặc sử dụng class :ref:`class_RandomNumberGenerator`.

Các phương thức global scope dễ thiết lập hơn, nhưng không cung cấp nhiều quyền kiểm soát.

RandomNumberGenerator cần nhiều code hơn để sử dụng, nhưng cho phép tạo nhiều instance, mỗi instance có seed và state riêng. Điều này hữu ích trong một số trường hợp như multiplayer qua mạng, hệ thống replay, trò chơi có cơ chế tua ngược và nhiều trường hợp khác.

Tutorial này sử dụng các phương thức global scope, ngoại trừ khi phương thức đó chỉ tồn tại trong class RandomNumberGenerator.

Seed ngẫu nhiên và state nội bộ
-------------------------------

Theo mặc định, Godot sử dụng seed ngẫu nhiên được thiết lập theo thời gian cục bộ của thiết bị. Điều này có nghĩa là kết quả sẽ khác nhau ở mỗi lần chạy. Để nhận được kết quả xác định, bạn có thể thiết lập seed cố định bằng cách sử dụng
:ref:`seed() <class_@GlobalScope_method_seed>` method. The *seed* is an integer
khởi tạo state của trình tạo số ngẫu nhiên. Nếu sử dụng cùng một seed, bạn sẽ nhận được cùng một chuỗi số ngẫu nhiên ở mỗi lần chạy.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        seed(12345)
        # Để sử dụng một chuỗi làm seed, bạn có thể băm chuỗi đó thành một số.
        seed("Hello world".hash())

 .. code-tab:: csharp

    public override void _Ready()
    {
        GD.Seed(12345);
        // Để sử dụng một chuỗi làm seed, bạn có thể băm chuỗi đó thành một số.
        GD.Seed("Hello world".Hash());
    }

Khi sử dụng class RandomNumberGenerator, bạn có thể thiết lập
:ref:`RandomNumberGenerator.seed <class_RandomNumberGenerator_property_seed>`
property trên từng instance:

.. tabs::
 .. code-tab:: gdscript GDScript

    var random = RandomNumberGenerator.new()
    random.seed = 12345

 .. code-tab:: csharp

    var random = new RandomNumberGenerator();
    random.Seed = 12345;

Bạn có thể đặt lại seed về một giá trị được tạo ngẫu nhiên bằng cách sử dụng
:ref:`randomize() <class_@GlobalScope_method_randomize>` global scope method.
Điều này cũng khả dụng dưới dạng
:ref:`RandomNumberGenerator.randomize() <class_RandomNumberGenerator_method_randomize>`
method trên các instance của RandomNumberGenerator.

Các trình tạo số ngẫu nhiên cũng có *state* nội bộ, state này thay đổi mỗi khi một số ngẫu nhiên được tạo. State này được sử dụng để tạo số ngẫu nhiên tiếp theo trong chuỗi.

Không giống việc tạo số ngẫu nhiên trong global scope, RandomNumberGenerator có
:ref:`state <class_RandomNumberGenerator_property_state>` property. This is
hữu ích nếu bạn thực hiện nhiều thao tác ngẫu nhiên và muốn quay lại state trước đó của trình tạo số ngẫu nhiên mà không thay đổi seed. Để thực hiện việc này, hãy lưu state hiện tại vào một biến, sau đó đặt property state về biến đó khi cần:

.. tabs::
 .. code-tab:: gdscript GDScript

    var random = RandomNumberGenerator.new()
    # Thay đổi seed sẽ đặt lại state, vì vậy hãy đảm bảo thiết lập seed trước.
    random.seed = 12345
    var previous_random_state = random.state
    # Mỗi lần gọi một hàm ngẫu nhiên trên instance này sẽ thay đổi state của nó.
    print(random.randi())

    random.state = previous_random_state
    # Lệnh này sẽ trả về cùng giá trị với lần gọi trước,
    # mặc dù chúng ta không thay đổi seed.
    print(random.randi())

 .. code-tab:: csharp

    var random = new RandomNumberGenerator();
    // Thay đổi seed sẽ đặt lại state, vì vậy hãy đảm bảo thiết lập seed trước.
    random.Seed = 12345;
    int previousRandomState = random.State;
    // Mỗi lần gọi một hàm ngẫu nhiên trên instance này sẽ thay đổi state của nó.
    GD.Print(random.Randi());

    random.State = previousRandomState;
    // Lệnh này sẽ trả về cùng giá trị với lần gọi trước,
    // mặc dù chúng ta không thay đổi seed.
    GD.Print(random.Randi());

Lấy số ngẫu nhiên
-----------------

Hãy cùng xem một số hàm và method thường được sử dụng nhất để tạo số ngẫu nhiên trong Godot.

Hàm :ref:`randi() <class_@GlobalScope_method_randi>` trả về một số ngẫu nhiên giữa ``0`` và ``2^32 - 1``. Vì giá trị tối đa rất lớn, nhiều khả năng bạn sẽ muốn sử dụng toán tử modulo (``%``) để giới hạn kết quả trong khoảng từ 0 đến mẫu số:

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một số nguyên ngẫu nhiên từ 0 đến 49.
    print(randi() % 50)

    # In ra một số nguyên ngẫu nhiên từ 10 đến 60.
    print(randi() % 51 + 10)

 .. code-tab:: csharp

    // In ra một số nguyên ngẫu nhiên từ 0 đến 49.
    GD.Print(GD.Randi() % 50);

    // In ra một số nguyên ngẫu nhiên từ 10 đến 60.
    GD.Print(GD.Randi() % 51 + 10);

:ref:`randf() <class_@GlobalScope_method_randf>` returns a random floating-point
một số trong khoảng từ 0 đến 1. Điều này hữu ích để triển khai một
:ref:`doc_random_number_generation_weighted_random_probability` system, among
và những thứ khác.

:ref:`randfn() <class_@GlobalScope_method_randfn>` returns a random
số thực dấu phẩy động tuân theo `normal distribution <https://en.wikipedia.org/wiki/Normal_distribution>`__. Điều này có nghĩa là giá trị được trả về có khả năng nằm quanh giá trị trung bình cao hơn (mặc định là 0.0), với độ dao động theo độ lệch (mặc định là 1.0):

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một số thực dấu phẩy động ngẫu nhiên từ phân phối chuẩn với giá trị trung bình 0.0 và độ lệch 1.0.
    print(randfn(0.0, 1.0))

 .. code-tab:: csharp

    // In ra một số thực dấu phẩy động ngẫu nhiên từ phân phối chuẩn với giá trị trung bình 0.0 và độ lệch 1.0.
    GD.Print(GD.Randfn(0.0, 1.0));

:ref:`randf_range() <class_@GlobalScope_method_randf_range>` takes two arguments
``from`` và ``to``, rồi trả về một số thực dấu phẩy động ngẫu nhiên giữa ``from`` và ``to``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một số thực dấu phẩy động ngẫu nhiên từ -4 đến 6.5.
    print(randf_range(-4, 6.5))

 .. code-tab:: csharp

    // In ra một số thực dấu phẩy động ngẫu nhiên từ -4 đến 6.5.
    GD.Print(GD.RandRange(-4.0, 6.5));

:ref:`randi_range() <class_@GlobalScope_method_randi_range>` takes two arguments ``from``
và ``to``, rồi trả về một số nguyên ngẫu nhiên giữa ``from`` và ``to``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một số nguyên ngẫu nhiên từ -10 đến 10.
    print(randi_range(-10, 10))

 .. code-tab:: csharp

    // In ra một số nguyên ngẫu nhiên từ -10 đến 10.
    GD.Print(GD.RandRange(-10, 10));

Lấy một phần tử ngẫu nhiên trong array
--------------------------------------

Chúng ta có thể sử dụng việc tạo số nguyên ngẫu nhiên để lấy một phần tử ngẫu nhiên từ array, hoặc sử dụng method :ref:`Array.pick_random<class_Array_method_pick_random>` để thực hiện việc này thay chúng ta:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _fruits = ["apple", "orange", "pear", "banana"]

    func _ready():
        for i in range(100):
            # Chọn ngẫu nhiên 100 loại trái cây.
            print(get_fruit())

        for i in range(100):
            # Chọn ngẫu nhiên 100 loại trái cây, lần này sử dụng
            # method hỗ trợ. Method này có cùng hành vi với `get_fruit()`.
            print(_fruits.pick_random())

    func get_fruit():
        var random_fruit = _fruits[randi() % _fruits.size()]
        # Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi code chạy.
        # Chúng ta có thể nhận cùng một loại trái cây nhiều lần liên tiếp.
        return random_fruit

 .. code-tab:: csharp

    // Sử dụng kiểu Array của Godot thay vì kiểu BCL để chúng ta có thể sử dụng `PickRandom()` trên đó.
    private Godot.Collections.Array<string> _fruits = ["apple", "orange", "pear", "banana"];

    public override void _Ready()
    {
        for (int i = 0; i < 100; i++)
        {
            // Chọn ngẫu nhiên 100 loại trái cây.
            GD.Print(GetFruit());
        }

        for (int i = 0; i < 100; i++)
        {
            // Chọn ngẫu nhiên 100 loại trái cây, lần này sử dụng `Array.PickRandom()`
            // method hỗ trợ. Method này có cùng hành vi với `GetFruit()`.
            GD.Print(_fruits.PickRandom());
        }
    }

    public string GetFruit()
    {
        string randomFruit = _fruits[GD.Randi() % _fruits.Size()];
        // Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi code chạy.
        // Chúng ta có thể nhận cùng một loại trái cây nhiều lần liên tiếp.
        return randomFruit;
    }

Để ngăn cùng một loại trái cây được chọn nhiều hơn một lần liên tiếp, chúng ta có thể bổ sung logic cho method bên trên. Trong trường hợp này, chúng ta không thể sử dụng
:ref:`Array.pick_random<class_Array_method_pick_random>` since it lacks a way to
để ngăn lặp lại:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _fruits = ["apple", "orange", "pear", "banana"]
    var _last_fruit = ""


    func _ready():
        # Chọn ngẫu nhiên 100 loại trái cây.
        for i in range(100):
            print(get_fruit())


    func get_fruit():
        var random_fruit = _fruits[randi() % _fruits.size()]
        while random_fruit == _last_fruit:
            # Loại trái cây vừa chọn là loại trước đó. Thử lại cho đến khi nhận được một loại trái cây khác.
            random_fruit = _fruits[randi() % _fruits.size()]

        # Note: if the random element to pick is passed by reference,
        # chẳng hạn như array hoặc dictionary,
        # hãy sử dụng `_last_fruit = random_fruit.duplicate()` thay thế.
        _last_fruit = random_fruit

        # Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi code chạy.
        # Hàm sẽ không bao giờ trả về cùng một loại trái cây nhiều hơn một lần liên tiếp.
        return random_fruit

 .. code-tab:: csharp

    private string[] _fruits = ["apple", "orange", "pear", "banana"];
    private string _lastFruit = "";

    public override void _Ready()
    {
        for (int i = 0; i < 100; i++)
        {
            // Chọn ngẫu nhiên 100 loại trái cây.
            GD.Print(GetFruit());
        }
    }

    public string GetFruit()
    {
        string randomFruit = _fruits[GD.Randi() % _fruits.Length];
        while (randomFruit == _lastFruit)
        {
            // Loại trái cây vừa chọn là loại trước đó. Thử lại cho đến khi nhận được một loại trái cây khác.
            randomFruit = _fruits[GD.Randi() % _fruits.Length];
        }

        _lastFruit = randomFruit;

        // Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi code chạy.
        // Hàm sẽ không bao giờ trả về cùng một loại trái cây nhiều hơn một lần liên tiếp.
        return randomFruit;
    }

Cách tiếp cận này có thể hữu ích để khiến việc tạo số ngẫu nhiên có cảm giác ít lặp lại hơn. Tuy vậy, nó không ngăn kết quả "ping-pong" giữa một tập giá trị giới hạn. Để ngăn điều này, hãy sử dụng pattern :ref:`shuffle bag <doc_random_number_generation_shuffle_bags>` thay thế.

Lấy một giá trị ngẫu nhiên trong dictionary
-------------------------------------------

Chúng ta cũng có thể áp dụng logic tương tự từ array cho dictionary:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _metals = {
        "copper": {"quantity": 50, "price": 50},
        "silver": {"quantity": 20, "price": 150},
        "gold": {"quantity": 3, "price": 500},
    }


    func _ready():
        for i in range(20):
            print(get_metal())


    func get_metal():
        var random_metal = _metals.values()[randi() % metals.size()]
        # Trả về một dictionary giá trị kim loại ngẫu nhiên mỗi khi code chạy.
        # Cùng một kim loại có thể được chọn nhiều lần liên tiếp.
        return random_metal

 .. code-tab:: csharp

    private Godot.Collections.Dictionary<string, Godot.Collections.Dictionary<string, int>> _metals = new()
    {
        {"copper", new Godot.Collections.Dictionary<string, int>{{"quantity", 50}, {"price", 50}}},
        {"silver", new Godot.Collections.Dictionary<string, int>{{"quantity", 20}, {"price", 150}}},
        {"gold", new Godot.Collections.Dictionary<string, int>{{"quantity", 3}, {"price", 500}}},
    };

    public override void _Ready()
    {
        for (int i = 0; i < 20; i++)
        {
            GD.Print(GetMetal());
        }
    }

    public Godot.Collections.Dictionary<string, int> GetMetal()
    {
        var (_, randomMetal) = _metals.ElementAt((int)(GD.Randi() % _metals.Count));
        // Trả về một dictionary giá trị kim loại ngẫu nhiên mỗi khi code chạy.
        // Cùng một kim loại có thể được chọn nhiều lần liên tiếp.
        return randomMetal;
    }

.. _doc_random_number_generation_weighted_random_probability:

Xác suất ngẫu nhiên có trọng số
-------------------------------

Method :ref:`randf() <class_@GlobalScope_method_randf>` trả về một số thực dấu phẩy động trong khoảng từ 0.0 đến 1.0. Chúng ta có thể sử dụng method này để tạo một xác suất "có trọng số", trong đó các kết quả khác nhau có khả năng xảy ra khác nhau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        for i in range(100):
            print(get_item_rarity())


    func get_item_rarity():
        var random_float = randf()

        if random_float < 0.8:
            # Có 80% khả năng được trả về.
            return "Common"
        elif random_float < 0.95:
            # Có 15% khả năng được trả về.
            return "Uncommon"
        else:
            # Có 5% khả năng được trả về.
            return "Rare"

 .. code-tab:: csharp

    public override void _Ready()
    {
        for (int i = 0; i < 100; i++)
        {
            GD.Print(GetItemRarity());
        }
    }

    public string GetItemRarity()
    {
        float randomFloat = GD.Randf();

        if (randomFloat < 0.8f)
        {
            // Có 80% khả năng được trả về.
            return "Common";
        }
        else if (randomFloat < 0.95f)
        {
            // Có 15% khả năng được trả về.
            return "Uncommon";
        }
        else
        {
            // Có 5% khả năng được trả về.
            return "Rare";
        }
    }

Bạn cũng có thể lấy một *index* ngẫu nhiên có trọng số bằng cách sử dụng
:ref:`RandomNumberGenerator.rand_weighted() <class_RandomNumberGenerator_method_rand_weighted>` method
trên một instance RandomNumberGenerator. Method này trả về một số nguyên ngẫu nhiên từ 0 đến kích thước của array được truyền vào dưới dạng tham số. Mỗi giá trị trong array là một số thực dấu phẩy động biểu thị khả năng *tương đối* để giá trị đó được trả về dưới dạng index. Giá trị càng cao thì khả năng giá trị đó được trả về dưới dạng index càng lớn, trong khi giá trị ``0`` có nghĩa là nó sẽ không bao giờ được trả về dưới dạng index.

Ví dụ: nếu ``[0.5, 1, 1, 2]`` được truyền vào dưới dạng tham số, method sẽ có khả năng trả về ``3`` (index của giá trị ``2``) cao gấp đôi và khả năng trả về ``0`` (index của giá trị ``0.5``) thấp hơn gấp đôi so với các index ``1`` và ``2``.

Vì giá trị được trả về tương ứng với kích thước của array, bạn có thể sử dụng nó làm index để lấy một giá trị từ array khác như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một phần tử ngẫu nhiên bằng cách sử dụng index có trọng số được trả về bởi `rand_weighted()`.
    # Ở đây, "apple" sẽ được trả về ít hơn hai lần so với "orange" và "pear".
    # "banana" phổ biến gấp đôi "orange" và "pear", và phổ biến gấp bốn lần "apple".
    var fruits = ["apple", "orange", "pear", "banana"]
    var probabilities = [0.5, 1, 1, 2];

    var random = RandomNumberGenerator.new()
    print(fruits[random.rand_weighted(probabilities)])

 .. code-tab:: csharp

    // In một phần tử ngẫu nhiên bằng chỉ số có trọng số được trả về bởi `RandWeighted()`.
    // Ở đây, "apple" sẽ được trả về với tần suất thấp hơn hai lần so với "orange" và "pear".
    // "banana" phổ biến gấp đôi "orange" và "pear", và phổ biến gấp bốn lần "apple".
    string[] fruits = ["apple", "orange", "pear", "banana"];
    float[] probabilities = [0.5f, 1, 1, 2];

    var random = new RandomNumberGenerator();
    GD.Print(fruits[random.RandWeighted(probabilities)]);

.. _doc_random_number_generation_shuffle_bags:

Tính ngẫu nhiên "tốt hơn" bằng shuffle bag
------------------------------------------

Lấy cùng ví dụ như trên, chúng ta muốn chọn trái cây một cách ngẫu nhiên. Tuy nhiên, việc dựa vào trình tạo số ngẫu nhiên mỗi lần chọn một loại trái cây có thể dẫn đến phân phối kém *đồng đều* hơn. Nếu người chơi may mắn (hoặc không may), họ có thể nhận cùng một loại trái cây ba lần trở lên liên tiếp.

Bạn có thể thực hiện điều này bằng pattern *shuffle bag*. Pattern này hoạt động bằng cách xóa một phần tử khỏi array sau khi chọn phần tử đó. Sau nhiều lần chọn, array sẽ trống. Khi đó, bạn khởi tạo lại nó về giá trị mặc định:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _fruits = ["apple", "orange", "pear", "banana"]
    # Một bản sao của array fruits để chúng ta có thể khôi phục giá trị ban đầu vào `fruits`.
    var _fruits_full = []


    func _ready():
        _fruits_full = _fruits.duplicate()
        _fruits.shuffle()

        for i in 100:
            print(get_fruit())


    func get_fruit():
        if _fruits.is_empty():
            # Điền lại array fruits và xáo trộn nó.
            _fruits = _fruits_full.duplicate()
            _fruits.shuffle()

        # Lấy một loại trái cây ngẫu nhiên vì chúng ta đã xáo trộn array,
        # và xóa nó khỏi array `_fruits`.
        var random_fruit = _fruits.pop_front()
        # Trả về "apple", "orange", "pear" hoặc "banana" mỗi lần code chạy, đồng thời xóa nó khỏi array.
        # Khi tất cả trái cây đã bị xóa, array sẽ được điền lại.
        return random_fruit

 .. code-tab:: csharp

    private Godot.Collections.Array<string> _fruits = ["apple", "orange", "pear", "banana"];
    // Một bản sao của array fruits để chúng ta có thể khôi phục giá trị ban đầu vào `fruits`.
    private Godot.Collections.Array<string> _fruitsFull;

    public override void _Ready()
    {
        _fruitsFull = _fruits.Duplicate();
        _fruits.Shuffle();

        for (int i = 0; i < 100; i++)
        {
            GD.Print(GetFruit());
        }
    }

    public string GetFruit()
    {
        if(_fruits.Count == 0)
        {
            // Điền lại array fruits và xáo trộn nó.
            _fruits = _fruitsFull.Duplicate();
            _fruits.Shuffle();
        }

        // Lấy một loại trái cây ngẫu nhiên vì chúng ta đã xáo trộn array,
        string randomFruit = _fruits[0];
        // và xóa nó khỏi array `_fruits`.
        _fruits.RemoveAt(0);
        // Trả về "apple", "orange", "pear" hoặc "banana" mỗi lần code chạy, đồng thời xóa nó khỏi array.
        // Khi tất cả trái cây đã bị xóa, array sẽ được điền lại.
        return randomFruit;
    }

Khi chạy code ở trên, có khả năng nhận cùng một loại trái cây hai lần liên tiếp. Sau khi chọn một loại trái cây, nó sẽ không còn là giá trị có thể được trả về nữa, trừ khi array hiện đã trống. Khi array trống, chúng ta đặt lại nó về giá trị mặc định, khiến cùng một loại trái cây có thể xuất hiện lại, nhưng chỉ một lần.

Nhiễu ngẫu nhiên
----------------

Việc tạo số ngẫu nhiên được trình bày ở trên có thể bộc lộ những hạn chế khi bạn cần một giá trị thay đổi *từ từ* tùy thuộc vào đầu vào. Đầu vào có thể là vị trí, thời gian hoặc bất kỳ thứ gì khác.

Để đạt được điều này, bạn có thể sử dụng các hàm *nhiễu* ngẫu nhiên. Các hàm nhiễu đặc biệt phổ biến trong việc tạo nội dung theo quy trình để tạo địa hình trông chân thực. Godot cung cấp :ref:`class_fastnoiselite` cho mục đích này, hỗ trợ nhiễu 1D, 2D và 3D. Dưới đây là một ví dụ với nhiễu 1D:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _noise = FastNoiseLite.new()

    func _ready():
        # Cấu hình instance FastNoiseLite.
        _noise.noise_type = FastNoiseLite.NoiseType.TYPE_SIMPLEX_SMOOTH
        _noise.seed = randi()
        _noise.fractal_octaves = 4
        _noise.frequency = 1.0 / 20.0

        for i in 100:
            # In ra một chuỗi số dấu phẩy động thay đổi từ từ
            # trong khoảng từ -1.0 đến 1.0.
            print(_noise.get_noise_1d(i))

 .. code-tab:: csharp

    private FastNoiseLite _noise = new FastNoiseLite();

    public override void _Ready()
    {
        // Cấu hình instance FastNoiseLite.
        _noise.NoiseType = FastNoiseLite.NoiseTypeEnum.SimplexSmooth;
        _noise.Seed = (int)GD.Randi();
        _noise.FractalOctaves = 4;
        _noise.Frequency = 1.0f / 20.0f;

        for (int i = 0; i < 100; i++)
        {
            GD.Print(_noise.GetNoise1D(i));
        }
    }

Tạo số giả ngẫu nhiên an toàn về mặt mật mã
-------------------------------------------

Cho đến nay, các phương pháp được đề cập ở trên **không** phù hợp để tạo số giả ngẫu nhiên *an toàn về mặt mật mã* (CSPRNG). Điều này phù hợp với game, nhưng không đủ cho các trường hợp liên quan đến mã hóa, xác thực hoặc ký.

Godot offers a :ref:`class_Crypto` class for this. This class can perform asymmetric key encryption/decryption, signing/verification, while also generating cryptographically secure random bytes, RSA keys, HMAC digests, and self-signed :ref:`class_X509Certificate`\ s.

Nhược điểm của :abbr:`CSPRNG (Cryptographically secure pseudorandom number generation)` là nó chậm hơn nhiều so với việc tạo số giả ngẫu nhiên tiêu chuẩn. API của nó cũng kém thuận tiện hơn khi sử dụng. Do đó,
:abbr:`CSPRNG (Cryptographically secure pseudorandom number generation)`
nên tránh sử dụng nó cho các thành phần gameplay.

Ví dụ sử dụng class Crypto để tạo 2 số nguyên ngẫu nhiên trong khoảng từ ``0`` đến ``2^32 - 1`` (bao gồm cả hai đầu mút):

::

    var crypto := Crypto.new()
    # Yêu cầu số byte tùy theo nhu cầu, nhưng hãy cố gắng giảm thiểu số lượng
    # yêu cầu riêng lẻ để cải thiện hiệu năng.
    # Mỗi số nguyên 32-bit cần 4 byte, vì vậy chúng ta yêu cầu 8 byte.
    var byte_array := crypto.generate_random_bytes(8)

    # Sử dụng phương thức ``decode_u32()`` từ PackedByteArray để giải mã một số nguyên không dấu 32-bit
    # từ phần đầu của `byte_array`. Phương thức này không thay đổi `byte_array`.
    var random_int_1 := byte_array.decode_u32(0)
    # Thực hiện tương tự như trên, nhưng với offset 4 byte vì trước đó chúng ta đã giải mã
    # 4 byte đầu tiên.
    var random_int_2 := byte_array.decode_u32(4)

    prints("Random integers:", random_int_1, random_int_2)

.. seealso::

    Xem tài liệu của :ref:`class_PackedByteArray` để biết các phương thức khác mà bạn có thể sử dụng nhằm giải mã các byte đã tạo thành nhiều kiểu dữ liệu khác nhau, chẳng hạn như số nguyên hoặc số thực.
