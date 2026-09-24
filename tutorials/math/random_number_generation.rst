.. _doc_random_number_generation:

Tạo số ngẫu nhiên
=================

Nhiều trò chơi dựa vào tính ngẫu nhiên để triển khai các cơ chế cốt lõi của trò chơi. Trang này hướng dẫn bạn về các kiểu ngẫu nhiên phổ biến và cách triển khai chúng trong Godot.

Sau khi giới thiệu ngắn gọn về các hàm hữu ích để tạo số ngẫu nhiên, bạn sẽ học cách lấy các phần tử ngẫu nhiên từ mảng, dictionary và cách sử dụng trình tạo nhiễu trong GDScript. Cuối cùng, chúng ta sẽ tìm hiểu về việc tạo số ngẫu nhiên an toàn về mặt mật mã và sự khác biệt của nó so với cách tạo số ngẫu nhiên thông thường.

.. note::

    Máy tính không thể tạo ra các số ngẫu nhiên "thực sự". Thay vào đó, chúng dựa vào `bộ tạo số giả ngẫu nhiên <https://en.wikipedia.org/wiki/Pseudorandom_number_generator>`__ (PRNG).

    Godot sử dụng nội bộ `PCG Family <https://www.pcg-random.org/>`__ của các bộ tạo số giả ngẫu nhiên.

Global scope so với lớp RandomNumberGenerator
---------------------------------------------

Godot cung cấp hai cách để tạo số ngẫu nhiên: thông qua các phương thức của *global scope* hoặc sử dụng :ref:`class_RandomNumberGenerator`.

Các phương thức global scope dễ thiết lập hơn, nhưng không cung cấp nhiều quyền kiểm soát.

RandomNumberGenerator cần nhiều mã hơn để sử dụng, nhưng cho phép tạo nhiều instance, mỗi instance có seed và state riêng. Điều này hữu ích trong một số tình huống như multiplayer qua mạng, hệ thống replay, trò chơi có cơ chế tua lại và nhiều trường hợp khác.

Tutorial này sử dụng các phương thức global scope, ngoại trừ khi phương thức đó chỉ tồn tại trong lớp RandomNumberGenerator.

Seed ngẫu nhiên và state nội bộ
-------------------------------

Theo mặc định, Godot sử dụng một seed ngẫu nhiên được thiết lập theo giờ địa phương của thiết bị. Điều này có nghĩa là kết quả sẽ khác nhau trong mỗi lần chạy. Để nhận được kết quả xác định, bạn có thể đặt một seed cố định bằng cách sử dụng
:ref:`seed() <class_@GlobalScope_method_seed>` method. *seed* là một số nguyên khởi tạo state của bộ tạo số ngẫu nhiên. Nếu sử dụng cùng một seed, bạn sẽ nhận được cùng một chuỗi số ngẫu nhiên trong mỗi lần chạy.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        seed(12345)
        # Để sử dụng chuỗi làm seed, bạn có thể băm chuỗi đó thành một số.
        seed("Hello world".hash())

 .. code-tab:: csharp

    public override void _Ready()
    {
        GD.Seed(12345);
        // Để sử dụng chuỗi làm seed, bạn có thể băm chuỗi đó thành một số.
        GD.Seed("Hello world".Hash());
    }

Khi sử dụng lớp RandomNumberGenerator, bạn có thể đặt
:ref:`RandomNumberGenerator.seed <class_RandomNumberGenerator_property_seed>` property trên từng instance:

.. tabs::
 .. code-tab:: gdscript GDScript

    var random = RandomNumberGenerator.new()
    random.seed = 12345

 .. code-tab:: csharp

    var random = new RandomNumberGenerator();
    random.Seed = 12345;

Bạn có thể đặt lại seed về một giá trị được tạo ngẫu nhiên bằng cách sử dụng
:ref:`randomize() <class_@GlobalScope_method_randomize>` global scope method. Phương thức này cũng có sẵn dưới dạng
:ref:`RandomNumberGenerator.randomize() <class_RandomNumberGenerator_method_randomize>` method trên các instance của RandomNumberGenerator.

Các bộ tạo số ngẫu nhiên cũng có một *state* nội bộ, thay đổi mỗi khi một số ngẫu nhiên được tạo. State này được dùng để tạo số ngẫu nhiên tiếp theo trong chuỗi.

Không giống như việc tạo số ngẫu nhiên trong global scope, RandomNumberGenerator có một
:ref:`state <class_RandomNumberGenerator_property_state>` property. Điều này hữu ích khi bạn thực hiện nhiều thao tác với số ngẫu nhiên và muốn quay lại state trước đó của bộ tạo số ngẫu nhiên mà không thay đổi seed. Để làm vậy, hãy lưu state hiện tại vào một biến, sau đó đặt property state về biến đó khi cần:

.. tabs::
 .. code-tab:: gdscript GDScript

    var random = RandomNumberGenerator.new()
    # Thay đổi seed sẽ đặt lại state, vì vậy hãy nhớ đặt seed trước.
    random.seed = 12345
    var previous_random_state = random.state
    # Mỗi lần gọi một hàm ngẫu nhiên trên instance này sẽ làm thay đổi state của nó.
    print(random.randi())

    random.state = previous_random_state
    # Lệnh này sẽ trả về cùng giá trị như lần gọi trước,
    # mặc dù chúng ta không thay đổi seed.
    print(random.randi())

 .. code-tab:: csharp

    var random = new RandomNumberGenerator();
    // Thay đổi seed sẽ đặt lại state, vì vậy hãy nhớ đặt seed trước.
    random.Seed = 12345;
    int previousRandomState = random.State;
    // Mỗi lần gọi một hàm ngẫu nhiên trên instance này sẽ làm thay đổi state của nó.
    GD.Print(random.Randi());

    random.State = previousRandomState;
    // Lệnh này sẽ trả về cùng giá trị như lần gọi trước,
    // mặc dù chúng ta không thay đổi seed.
    GD.Print(random.Randi());

Lấy một số ngẫu nhiên
---------------------

Hãy cùng xem một số hàm và phương thức thường được sử dụng nhất để tạo số ngẫu nhiên trong Godot.

Hàm :ref:`randi() <class_@GlobalScope_method_randi>` trả về một số ngẫu nhiên nằm giữa ``0`` và ``2^32 - 1``. Vì giá trị tối đa rất lớn, nhiều khả năng bạn sẽ muốn sử dụng toán tử modulo (``%``) để giới hạn kết quả trong khoảng từ 0 đến mẫu số:

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

:ref:`randf() <class_@GlobalScope_method_randf>` trả về một số thực ngẫu nhiên trong khoảng từ 0 đến 1. Điều này hữu ích để triển khai một
:ref:`doc_random_number_generation_weighted_random_probability` system, cùng nhiều mục đích khác.

:ref:`randfn() <class_@GlobalScope_method_randfn>` trả về một số thực ngẫu nhiên tuân theo `phân phối chuẩn <https://en.wikipedia.org/wiki/Normal_distribution>`__. Điều này có nghĩa là giá trị trả về có khả năng nằm quanh giá trị trung bình cao hơn (mặc định là 0.0), với độ lệch thay đổi (mặc định là 1.0):

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một số thực ngẫu nhiên từ phân phối chuẩn với giá trị trung bình 0.0 và độ lệch 1.0.
    print(randfn(0.0, 1.0))

 .. code-tab:: csharp

    // In ra một số thực ngẫu nhiên từ phân phối chuẩn với giá trị trung bình 0.0 và độ lệch 1.0.
    GD.Print(GD.Randfn(0.0, 1.0));

:ref:`randf_range() <class_@GlobalScope_method_randf_range>` nhận hai đối số ``from`` và ``to``, rồi trả về một số thực ngẫu nhiên nằm giữa ``from`` và ``to``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một số thực ngẫu nhiên từ -4 đến 6.5.
    print(randf_range(-4, 6.5))

 .. code-tab:: csharp

    // In ra một số thực ngẫu nhiên từ -4 đến 6.5.
    GD.Print(GD.RandRange(-4.0, 6.5));

:ref:`randi_range() <class_@GlobalScope_method_randi_range>` nhận hai đối số ``from`` và ``to``, rồi trả về một số nguyên ngẫu nhiên nằm giữa ``from`` và ``to``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một số nguyên ngẫu nhiên nằm giữa -10 và 10.
    print(randi_range(-10, 10))

 .. code-tab:: csharp

    // In ra một số nguyên ngẫu nhiên nằm giữa -10 và 10.
    GD.Print(GD.RandRange(-10, 10));

Lấy một phần tử ngẫu nhiên trong mảng
-------------------------------------

Chúng ta có thể sử dụng tính năng tạo số nguyên ngẫu nhiên để lấy một phần tử ngẫu nhiên từ một mảng, hoặc sử dụng phương thức :ref:`Array.pick_random<class_Array_method_pick_random>` để thực hiện việc đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _fruits = ["apple", "orange", "pear", "banana"]

    func _ready():
        for i in range(100):
            # Chọn ngẫu nhiên 100 loại trái cây.
            print(get_fruit())

        for i in range(100):
            # Chọn ngẫu nhiên 100 loại trái cây, lần này sử dụng `Array.pick_random()`
            # phương thức helper. Phương thức này có hành vi giống `get_fruit()`.
            print(_fruits.pick_random())

    func get_fruit():
        var random_fruit = _fruits[randi() % _fruits.size()]
        # Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi mã chạy.
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
            // phương thức helper. Phương thức này có hành vi giống `GetFruit()`.
            GD.Print(_fruits.PickRandom());
        }
    }

    public string GetFruit()
    {
        string randomFruit = _fruits[GD.Randi() % _fruits.Size()];
        // Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi mã chạy.
        // Chúng ta có thể nhận cùng một loại trái cây nhiều lần liên tiếp.
        return randomFruit;
    }

Để ngăn không cho cùng một loại trái cây được chọn nhiều hơn một lần liên tiếp, chúng ta có thể thêm logic vào phương thức ở trên. Trong trường hợp này, chúng ta không thể sử dụng
:ref:`Array.pick_random<class_Array_method_pick_random>` vì nó không có cách ngăn việc lặp lại:

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
            # Loại trái cây cuối cùng đã được chọn. Thử lại cho đến khi nhận được một loại trái cây khác.
            random_fruit = _fruits[randi() % _fruits.size()]

        # Lưu ý: nếu phần tử ngẫu nhiên cần chọn được truyền theo tham chiếu,
        # chẳng hạn như một mảng hoặc dictionary,
        # hãy sử dụng `_last_fruit = random_fruit.duplicate()` thay thế.
        _last_fruit = random_fruit

        # Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi mã chạy.
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
            // Loại trái cây cuối cùng đã được chọn. Thử lại cho đến khi nhận được một loại trái cây khác.
            randomFruit = _fruits[GD.Randi() % _fruits.Length];
        }

        _lastFruit = randomFruit;

        // Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi mã chạy.
        // Hàm sẽ không bao giờ trả về cùng một loại trái cây nhiều hơn một lần liên tiếp.
        return randomFruit;
    }

Cách tiếp cận này có thể hữu ích để khiến việc tạo số ngẫu nhiên có cảm giác ít lặp lại hơn. Tuy nhiên, nó không ngăn các kết quả "ping-pong" giữa một tập hợp giá trị giới hạn. Để ngăn điều này, hãy sử dụng mẫu :ref:`shuffle bag <doc_random_number_generation_shuffle_bags>` thay thế.

Lấy một giá trị ngẫu nhiên từ dictionary
----------------------------------------

Chúng ta cũng có thể áp dụng logic tương tự từ mảng cho dictionary:

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
        # Trả về một dictionary giá trị kim loại ngẫu nhiên mỗi khi mã chạy.
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
        // Trả về một dictionary giá trị kim loại ngẫu nhiên mỗi khi mã chạy.
        // Cùng một kim loại có thể được chọn nhiều lần liên tiếp.
        return randomMetal;
    }

.. _doc_random_number_generation_weighted_random_probability:

Xác suất ngẫu nhiên có trọng số
-------------------------------

Phương thức :ref:`randf() <class_@GlobalScope_method_randf>` trả về một số dấu phẩy động nằm giữa 0.0 và 1.0. Chúng ta có thể sử dụng phương thức này để tạo một xác suất "có trọng số", trong đó các kết quả khác nhau có khả năng xảy ra khác nhau:

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

Bạn cũng có thể lấy *index* ngẫu nhiên có trọng số bằng cách sử dụng
phương thức :ref:`RandomNumberGenerator.rand_weighted() <class_RandomNumberGenerator_method_rand_weighted>` trên một instance RandomNumberGenerator. Phương thức này trả về một số nguyên ngẫu nhiên từ 0 đến kích thước của mảng được truyền làm tham số. Mỗi giá trị trong mảng là một số dấu phẩy động biểu thị khả năng *relative* mà giá trị đó được trả về dưới dạng index. Giá trị càng cao thì khả năng giá trị đó được trả về dưới dạng index càng lớn, trong khi giá trị ``0`` có nghĩa là giá trị đó sẽ không bao giờ được trả về dưới dạng index.

Ví dụ: nếu truyền ``[0.5, 1, 1, 2]`` làm tham số, phương thức sẽ có khả năng trả về ``3`` (index của giá trị ``2``) cao gấp đôi và khả năng trả về ``0`` (index của giá trị ``0.5``) thấp bằng một nửa so với các index ``1`` và ``2``.

Vì giá trị được trả về tương ứng với kích thước của mảng, bạn có thể sử dụng nó làm index để lấy một giá trị từ mảng khác như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    # In ra một phần tử ngẫu nhiên bằng cách sử dụng index có trọng số được trả về bởi `rand_weighted()`.
    # Ở đây, "apple" sẽ được trả về ít hơn "orange" và "pear" hai lần.
    # "banana" phổ biến gấp đôi "orange" và "pear", và phổ biến gấp bốn lần "apple".
    var fruits = ["apple", "orange", "pear", "banana"]
    var probabilities = [0.5, 1, 1, 2];

    var random = RandomNumberGenerator.new()
    print(fruits[random.rand_weighted(probabilities)])

 .. code-tab:: csharp

    // In một phần tử ngẫu nhiên bằng chỉ mục có trọng số được `RandWeighted()` trả về.
    // Ở đây, "apple" sẽ được trả về ít hơn "orange" và "pear" hai lần.
    // "banana" phổ biến gấp đôi "orange" và "pear", và phổ biến gấp bốn lần "apple".
    string[] fruits = ["apple", "orange", "pear", "banana"];
    float[] probabilities = [0.5f, 1, 1, 2];

    var random = new RandomNumberGenerator();
    GD.Print(fruits[random.RandWeighted(probabilities)]);

.. _doc_random_number_generation_shuffle_bags:

Tính ngẫu nhiên "tốt hơn" bằng shuffle bag
------------------------------------------

Lấy cùng ví dụ như trên, chúng ta muốn chọn trái cây một cách ngẫu nhiên. Tuy nhiên, việc dựa vào quá trình tạo số ngẫu nhiên mỗi lần chọn một loại trái cây có thể dẫn đến phân phối *không* đồng đều hơn. Nếu người chơi may mắn (hoặc không may), họ có thể nhận cùng một loại trái cây ba lần liên tiếp hoặc nhiều hơn.

Bạn có thể thực hiện điều này bằng mẫu *shuffle bag*. Mẫu này hoạt động bằng cách xóa một phần tử khỏi mảng sau khi chọn phần tử đó. Sau nhiều lần chọn, mảng sẽ trở nên rỗng. Khi đó, bạn khởi tạo lại mảng về giá trị mặc định của nó:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _fruits = ["apple", "orange", "pear", "banana"]
    # Một bản sao của mảng fruits để chúng ta có thể khôi phục giá trị ban đầu vào `fruits`.
    var _fruits_full = []


    func _ready():
        _fruits_full = _fruits.duplicate()
        _fruits.shuffle()

        for i in 100:
            print(get_fruit())


    func get_fruit():
        if _fruits.is_empty():
            # Điền lại mảng fruits và xáo trộn nó.
            _fruits = _fruits_full.duplicate()
            _fruits.shuffle()

        # Lấy một loại trái cây ngẫu nhiên vì chúng ta đã xáo trộn mảng,
        # và xóa nó khỏi mảng `_fruits`.
        var random_fruit = _fruits.pop_front()
        # Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi mã chạy, đồng thời xóa phần tử đó khỏi mảng.
        # Khi tất cả trái cây đã bị xóa, mảng sẽ được điền lại.
        return random_fruit

 .. code-tab:: csharp

    private Godot.Collections.Array<string> _fruits = ["apple", "orange", "pear", "banana"];
    // Một bản sao của mảng fruits để chúng ta có thể khôi phục giá trị ban đầu vào `fruits`.
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
            // Điền lại mảng fruits và xáo trộn nó.
            _fruits = _fruitsFull.Duplicate();
            _fruits.Shuffle();
        }

        // Lấy một loại trái cây ngẫu nhiên vì chúng ta đã xáo trộn mảng,
        string randomFruit = _fruits[0];
        // và xóa nó khỏi mảng `_fruits`.
        _fruits.RemoveAt(0);
        // Trả về "apple", "orange", "pear" hoặc "banana" mỗi khi mã chạy, đồng thời xóa phần tử đó khỏi mảng.
        // Khi tất cả trái cây đã bị xóa, mảng sẽ được điền lại.
        return randomFruit;
    }

Khi chạy đoạn mã trên, có khả năng nhận cùng một loại trái cây hai lần liên tiếp. Sau khi chúng ta chọn một loại trái cây, nó sẽ không còn là giá trị có thể được trả về, trừ khi mảng hiện đã rỗng. Khi mảng rỗng, chúng ta đặt lại mảng về giá trị mặc định, khiến việc nhận lại cùng loại trái cây là có thể, nhưng chỉ một lần.

Nhiễu ngẫu nhiên
----------------

Quá trình tạo số ngẫu nhiên được trình bày ở trên có thể bộc lộ giới hạn khi bạn cần một giá trị *thay đổi từ từ* tùy thuộc vào đầu vào. Đầu vào có thể là một vị trí, thời gian hoặc bất kỳ thứ gì khác.

Để đạt được điều này, bạn có thể sử dụng các hàm *nhiễu* ngẫu nhiên. Các hàm nhiễu đặc biệt phổ biến trong việc tạo sinh theo quy trình để tạo địa hình trông chân thực. Godot cung cấp :ref:`class_fastnoiselite` cho mục đích này, hỗ trợ nhiễu 1D, 2D và 3D. Sau đây là một ví dụ với nhiễu 1D:

.. tabs::
 .. code-tab:: gdscript GDScript

    var _noise = FastNoiseLite.new()

    func _ready():
        # Cấu hình thực thể FastNoiseLite.
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
        // Cấu hình thực thể FastNoiseLite.
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

Cho đến nay, các phương pháp được đề cập ở trên **không** phù hợp để tạo số giả ngẫu nhiên *an toàn về mặt mật mã* (CSPRNG). Điều này phù hợp với trò chơi, nhưng không đủ cho các tình huống liên quan đến mã hóa, xác thực hoặc ký.

Godot cung cấp một :ref:`class_Crypto` class cho mục đích này. Class này có thể thực hiện mã hóa/giải mã khóa bất đối xứng, ký/xác minh, đồng thời tạo các byte ngẫu nhiên an toàn về mặt mật mã, khóa RSA, thông báo HMAC và các :ref:`class_X509Certificate`\  tự ký.

Nhược điểm của :abbr:`CSPRNG (Tạo số giả ngẫu nhiên an toàn về mặt mật mã)` là nó chậm hơn nhiều so với việc tạo số giả ngẫu nhiên tiêu chuẩn. API của nó cũng kém thuận tiện hơn khi sử dụng. Vì vậy,
:abbr:`CSPRNG (Tạo số giả ngẫu nhiên an toàn về mặt mật mã)` nên được tránh dùng cho các thành phần gameplay.

Ví dụ sử dụng class Crypto để tạo 2 số nguyên ngẫu nhiên trong khoảng từ ``0`` đến ``2^32 - 1`` (bao gồm cả hai đầu mút):

::

    var crypto := Crypto.new()
    # Request as many bytes as you need, but try to minimize the amount
    # of separate requests to improve performance.
    # Each 32-bit integer requires 4 bytes, so we request 8 bytes.
    var byte_array := crypto.generate_random_bytes(8)

    # Use the ``decode_u32()`` method from PackedByteArray to decode a 32-bit unsigned integer
    # from the beginning of `byte_array`. This method doesn't modify `byte_array`.
    var random_int_1 := byte_array.decode_u32(0)
    # Do the same as above, but with an offset of 4 bytes since we've already decoded
    # the first 4 bytes previously.
    var random_int_2 := byte_array.decode_u32(4)

    prints("Random integers:", random_int_1, random_int_2)

.. seealso::

    Xem tài liệu của :ref:`class_PackedByteArray` để biết các phương thức khác mà bạn có thể sử dụng để giải mã các byte đã tạo thành nhiều kiểu dữ liệu khác nhau, chẳng hạn như số nguyên hoặc số thực.
