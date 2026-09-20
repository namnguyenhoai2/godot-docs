.. _doc_c_sharp_differences:

Các khác biệt về API giữa C# và GDScript
========================================

Đây là danh sách (chưa đầy đủ) các khác biệt về API giữa C# và GDScript.

Các khác biệt chung
-------------------

Như đã giải thích trong :ref:`doc_c_sharp_general_differences`, ``PascalCase`` được dùng để truy cập các API của Godot trong C# thay cho ``snake_case`` được GDScript và C++ sử dụng. Khi có thể, các field và getter/setter đã được chuyển đổi thành property. Nhìn chung, C# Godot API hướng tới việc tuân theo phong cách tự nhiên nhất có thể. Hãy xem :ref:`doc_c_sharp_styleguide`, chúng tôi cũng khuyến khích bạn sử dụng cho code C# của mình.

Trong GDScript, setter/getter của một property có thể được gọi trực tiếp, mặc dù không được khuyến khích. Trong C#, chỉ property được định nghĩa. Ví dụ, để chuyển code GDScript ``x.set_name("Friend")`` sang C#, hãy viết ``x.Name = "Friend";``.

Một C# IDE sẽ cung cấp tính năng intellisense, cực kỳ hữu ích khi xác định các C# API đã được đổi tên. Trình soạn thảo script tích hợp của Godot không hỗ trợ C# intellisense và cũng không cung cấp nhiều công cụ phát triển C# khác vốn được xem là thiết yếu. Hãy xem :ref:`doc_c_sharp_setup_external_editor`.

Phạm vi toàn cục
----------------

Các hàm toàn cục và một số hằng số phải được chuyển vào các class, vì C# không cho phép khai báo chúng trong namespace. Hầu hết hằng số toàn cục đã được chuyển vào các enum riêng.

Hằng số
~~~~~~~

Trong C#, chỉ các kiểu nguyên thủy mới có thể là hằng số. Ví dụ, hằng số ``TAU`` được thay thế bằng hằng số ``Mathf.Tau``, nhưng hằng số ``Vector2.RIGHT`` được thay thế bằng read-only property ``Vector2.Right``. Property này hoạt động tương tự một hằng số, nhưng không thể được dùng trong một số ngữ cảnh như các câu lệnh ``switch``.

Các hằng số enum toàn cục đã được chuyển vào các enum riêng. Ví dụ, các hằng số ``ERR_*`` được chuyển vào enum ``Error``.

Các trường hợp đặc biệt:

=======================  ===========================================================
GDScript                 C#
=======================  ===========================================================
``TYPE_*``               ``Variant.Type`` enum
``OP_*``                 ``Variant.Operator`` enum
=======================  ===========================================================

Các hàm toán học
~~~~~~~~~~~~~~~~

Các hàm toán học toàn cục, như ``abs``, ``acos``, ``asin``, ``atan`` và ``atan2``, nằm dưới ``Mathf`` với tên lần lượt là ``Abs``, ``Acos``, ``Asin``, ``Atan`` và ``Atan2``. Hằng số ``PI`` có thể được tìm thấy dưới dạng ``Mathf.Pi``.

C# cũng cung cấp các class static `System.Math`_ và `System.MathF`_, có thể chứa những phép toán toán học hữu ích khác.

.. _System.Math: https://learn.microsoft.com/en-us/dotnet/api/system.math
.. _System.MathF: https://learn.microsoft.com/en-us/dotnet/api/system.mathf

Các hàm ngẫu nhiên
~~~~~~~~~~~~~~~~~~

Các hàm ngẫu nhiên toàn cục, như ``rand_range`` và ``rand_seed``, nằm dưới ``GD``. Ví dụ: ``GD.RandRange`` và ``GD.RandSeed``.

Hãy cân nhắc sử dụng `System.Random`_ hoặc, nếu bạn cần tính ngẫu nhiên mạnh về mặt mật mã, `System.Security.Cryptography.RandomNumberGenerator`_.

.. _System.Random: https://learn.microsoft.com/en-us/dotnet/api/system.random
.. _System.Security.Cryptography.RandomNumberGenerator: https://learn.microsoft.com/en-us/dotnet/api/system.security.cryptography.randomnumbergenerator

Các hàm khác
~~~~~~~~~~~~

Nhiều hàm toàn cục khác như ``print`` và ``var_to_str`` nằm dưới ``GD``. Ví dụ: ``GD.Print`` và ``GD.VarToStr``.

Ngoại lệ:

============================  =======================================================
GDScript                      C#
============================  =======================================================
``weakref(obj)``              ``GodotObject.WeakRef(obj)``
``instance_from_id(id)``      ``GodotObject.InstanceFromId(id)``
``is_instance_id_valid(id)``  ``GodotObject.IsInstanceIdValid(id)``
``is_instance_valid(obj)``    ``GodotObject.IsInstanceValid(obj)``
============================  =======================================================

Mẹo
~~~

Đôi khi việc sử dụng directive ``using static`` có thể hữu ích. Directive này cho phép truy cập các member và nested type của một class mà không cần chỉ định tên class.

Ví dụ:

.. code-block:: csharp

    using static Godot.GD;

    public class Test
    {
        static Test()
        {
            Print("Hello"); // Thay vì GD.Print("Hello");
        }
    }

Danh sách đầy đủ các tương đương
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Danh sách các hàm trong phạm vi toàn cục của Godot và tương đương của chúng trong C#:

===============================  ==============================================================
GDScript                         C#
===============================  ==============================================================
abs                              Mathf.Abs
absf                             Mathf.Abs
absi                             Mathf.Abs
acos                             Mathf.Acos
acosh                            Mathf.Acosh
angle_difference                 Mathf.AngleDifference
asin                             Mathf.Asin
asinh                            Mathf.Asinh
atan                             Mathf.Atan
atan2                            Mathf.Atan2
atanh                            Mathf.Atanh
bezier_derivative                Mathf.BezierDerivative
bezier_interpolate               Mathf.BezierInterpolate
bytes_to_var                     GD.BytesToVar
bytes_to_var_with_objects        GD.BytesToVarWithObjects
ceil                             Mathf.Ceil
ceilf                            Mathf.Ceil
ceili                            Mathf.CeilToInt
clamp                            Mathf.Clamp
clampf                           Mathf.Clamp
clampi                           Mathf.Clamp
cos                              Mathf.Cos
cosh                             Mathf.Cosh
cubic_interpolate                Mathf.CubicInterpolate
cubic_interpolate_angle          Mathf.CubicInterpolateAngle
cubic_interpolate_angle_in_time  Mathf.CubicInterpolateInTime
cubic_interpolate_in_time        Mathf.CubicInterpolateAngleInTime
db_to_linear                     Mathf.DbToLinear
deg_to_rad                       Mathf.DegToRad
ease                             Mathf.Ease
error_string                     Error.ToString
exp                              Mathf.Exp
floor                            Mathf.Floor
floorf                           Mathf.Floor
floori                           Mathf.FloorToInt
fmod                             operator %
fposmod                          Mathf.PosMod
hash                             GD.Hash
instance_from_id                 GodotObject.InstanceFromId
inverse_lerp                     Mathf.InverseLerp
is_equal_approx                  Mathf.IsEqualApprox
is_finite                        Mathf.IsFinite or `float.IsFinite`_ or `double.IsFinite`_
is_inf                           Mathf.IsInf or `float.IsInfinity`_ or `double.IsInfinity`_
is_instance_id_valid             GodotObject.IsInstanceIdValid
is_instance_valid                GodotObject.IsInstanceValid
is_nan                           Mathf.IsNaN or `float.IsNaN`_ or `double.IsNaN`_
is_same                          operator == or `object.ReferenceEquals`_
is_zero_approx                   Mathf.IsZeroApprox
lerp                             Mathf.Lerp
lerp_angle                       Mathf.LerpAngle
lerpf                            Mathf.Lerp
linear_to_db                     Mathf.LinearToDb
log                              Mathf.Log
max                              Mathf.Max
maxf                             Mathf.Max
maxi                             Mathf.Max
min                              Mathf.Min
minf                             Mathf.Min
mini                             Mathf.Min
move_toward                      Mathf.MoveToward
nearest_po2                      Mathf.NearestPo2
pingpong                         Mathf.PingPong
posmod                           Mathf.PosMod
pow                              Mathf.Pow
print                            GD.Print
print_rich                       GD.PrintRich
print_verbose                    Use OS.IsStdoutVerbose and GD.Print
printerr                         GD.PrintErr
printraw                         GD.PrintRaw
prints                           GD.PrintS
printt                           GD.PrintT
push_error                       GD.PushError
push_warning                     GD.PushWarning
rad_to_deg                       Mathf.RadToDeg
rand_from_seed                   GD.RandFromSeed
randf                            GD.Randf
randf_range                      GD.RandRange
randfn                           GD.Randfn
randi                            GD.Randi
randi_range                      GD.RandRange
randomize                        GD.Randomize
remap                            Mathf.Remap
rid_allocate_id                  N/A
rid_from_int64                   N/A
rotate_toward                    Mathf.RotateToward
round                            Mathf.Round
roundf                           Mathf.Round
roundi                           Mathf.RoundToInt
seed                             GD.Seed
sign                             Mathf.Sign
signf                            Mathf.Sign
signi                            Mathf.Sign
sin                              Mathf.Sin
sinh                             Mathf.Sinh
smoothstep                       Mathf.SmoothStep
snapped                          Mathf.Snapped
snappedf                         Mathf.Snapped
snappedi                         Mathf.Snapped
sqrt                             Mathf.Sqrt
step_decimals                    Mathf.StepDecimals
str                              Use `$ string interpolation`_
str_to_var                       GD.StrToVar
tan                              Mathf.Tan
tanh                             Mathf.Tanh
type_convert                     Variant.As<T> or GD.Convert
type_string                      Variant.Type.ToString
typeof                           Variant.VariantType
var_to_bytes                     GD.VarToBytes
var_to_bytes_with_objects        GD.VarToBytesWithObjects
var_to_str                       GD.VarToStr
weakref                          GodotObject.WeakRef
wrap                             Mathf.Wrap
wrapf                            Mathf.Wrap
wrapi                            Mathf.Wrap
===============================  ==============================================================

.. _$ string interpolation: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated
.. _double.IsFinite: https://learn.microsoft.com/en-us/dotnet/api/system.double.isfinite
.. _double.IsInfinity: https://learn.microsoft.com/en-us/dotnet/api/system.double.isinfinity
.. _double.IsNaN: https://learn.microsoft.com/en-us/dotnet/api/system.double.isnan
.. _float.IsFinite: https://learn.microsoft.com/en-us/dotnet/api/system.single.isfinite
.. _float.IsInfinity: https://learn.microsoft.com/en-us/dotnet/api/system.single.isinfinity
.. _float.IsNaN: https://learn.microsoft.com/en-us/dotnet/api/system.single.isnan
.. _object.ReferenceEquals: https://learn.microsoft.com/en-us/dotnet/api/system.object.referenceequals

Danh sách các hàm tiện ích của GDScript và tương đương của chúng trong C#:

=======================  ==============================================================
GDScript                 C#
=======================  ==============================================================
assert                   `System.Diagnostics.Debug.Assert`_
char                     Use explicit conversion: ``(char)65``
convert                  GD.Convert
dict_to_inst             N/A
get_stack                `System.Environment.StackTrace`_
inst_to_dict             N/A
len                      N/A
load                     GD.Load
preload                  N/A
print_debug              N/A
print_stack              GD.Print(`System.Environment.StackTrace`_)
range                    GD.Range or `System.Linq.Enumerable.Range`_
type_exists              ClassDB.ClassExists(type)
=======================  ==============================================================

.. _System.Diagnostics.Debug.Assert: https://learn.microsoft.com/en-us/dotnet/api/system.diagnostics.debug.assert
.. _System.Environment.StackTrace: https://learn.microsoft.com/en-us/dotnet/api/system.environment.stacktrace
.. _System.Linq.Enumerable.Range: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.range

``preload``, với cách hoạt động như trong GDScript, không khả dụng trong C#. Thay vào đó, hãy sử dụng ``GD.Load`` hoặc ``ResourceLoader.Load``.

Annotation ``@export``
----------------------

Sử dụng attribute ``[Export]`` thay cho annotation ``@export`` của GDScript. Attribute này cũng có thể được cung cấp cùng các tham số :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>` và ``hintString`` tùy chọn. Có thể thiết lập giá trị mặc định bằng cách gán một giá trị.

Ví dụ:

.. code-block:: csharp

    using Godot;

    public partial class MyNode : Node
    {
        [Export]
        private NodePath _nodePath;

        [Export]
        private string _name = "default";

        [Export(PropertyHint.Range, "0,100000,1000,or_greater")]
        private int _income;

        [Export(PropertyHint.File, "*.png,*.jpg")]
        private string _icon;
    }

Xem thêm: :ref:`doc_c_sharp_exports`.

Keyword ``signal``
------------------

Sử dụng attribute ``[Signal]`` để khai báo signal thay cho keyword ``signal`` của GDScript. Attribute này phải được sử dụng trên một ``delegate``, trong đó signature của tên sẽ được dùng để định nghĩa signal. ``delegate`` phải có hậu tố ``EventHandler``, một ``event`` sẽ được tạo trong class với cùng tên nhưng không có hậu tố; hãy sử dụng tên của event đó với ``EmitSignal``.

.. code-block:: csharp

    [Signal]
    delegate void MySignalEventHandler(string willSendAString);

Xem thêm: :ref:`doc_c_sharp_signals`.

Annotation ``@onready``
-----------------------

GDScript có khả năng trì hoãn việc khởi tạo member variable cho đến khi hàm ready được gọi bằng :ref:`@onready <doc_gdscript_onready_annotation>`. Ví dụ:

.. code-block:: gdscript

    @onready var my_label = get_node("MyLabel")

Tuy nhiên, C# không có khả năng này. Để đạt được hiệu ứng tương tự, bạn cần làm như sau.

.. code-block:: csharp

    private Label _myLabel;

    public override void _Ready()
    {
        _myLabel = GetNode<Label>("MyLabel");
    }

Singleton
---------

Singleton khả dụng dưới dạng static class thay vì sử dụng singleton pattern. Cách này giúp code ngắn gọn hơn so với khi sử dụng property ``Instance``.

Ví dụ:

.. code-block:: csharp

    Input.IsActionPressed("ui_down")

Tuy nhiên, trong một số trường hợp rất hiếm, cách này vẫn chưa đủ. Ví dụ, bạn có thể muốn truy cập một member từ base class ``GodotObject``, chẳng hạn như ``Connect``. Trong những trường hợp như vậy, chúng tôi cung cấp một static property có tên ``Singleton``, trả về instance singleton. Kiểu của instance này là ``GodotObject``.

Ví dụ:

.. code-block:: csharp

    Input.Singleton.JoyConnectionChanged += Input_JoyConnectionChanged;

Nếu bạn đang phát triển main screen plugin, điều cần thiết là phải lưu ý rằng ``EditorInterface`` không phải là static class trong C#, không giống như trong GDScript. Vì vậy, bạn phải sử dụng singleton pattern để lấy một instance của ``EditorInterface``:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``EditorInterface``        ``EditorInterface.Singleton``
====================  ==============================================================

String
------

Sử dụng ``System.String`` (``string``). Hầu hết các method String của Godot đều có tương đương trong ``System.String`` hoặc được class ``StringExtensions`` cung cấp dưới dạng extension method.

Lưu ý rằng string trong C# sử dụng encoding UTF-16, trong khi String của Godot sử dụng encoding UTF-32.

Ví dụ:

.. code-block:: csharp

    string text = "Get up!";
    string[] bigrams = text.Bigrams(); // ["Ge", "et", "t ", " u", "up", "p!"]

String là immutable trong .NET, vì vậy tất cả method thao tác với một string đều không sửa đổi string ban đầu mà trả về một string mới được tạo với các thay đổi đã áp dụng. Để tránh tạo nhiều allocation cho string, hãy cân nhắc sử dụng `StringBuilder`_.

Danh sách các method String của Godot và tương đương của chúng trong C#:

=======================  ==============================================================
GDScript                 C#
=======================  ==============================================================
begins_with              `string.StartsWith`_
bigrams                  StringExtensions.Bigrams
bin_to_int               StringExtensions.BinToInt
c_escape                 StringExtensions.CEscape
c_unescape               StringExtensions.CUnescape
capitalize               StringExtensions.Capitalize
casecmp_to               StringExtensions.CasecmpTo or StringExtensions.CompareTo (Consider using `string.Equals`_ or `string.Compare`_)
chr                      N/A
contains                 `string.Contains`_
count                    StringExtensions.Count (Consider using `RegEx`_)
countn                   StringExtensions.CountN (Consider using `RegEx`_)
dedent                   StringExtensions.Dedent
ends_with                `string.EndsWith`_
erase                    `string.Remove`_ (Consider using `StringBuilder`_ to manipulate strings)
find                     StringExtensions.Find (Consider using `string.IndexOf`_ or `string.IndexOfAny`_)
findn                    StringExtensions.FindN (Consider using `string.IndexOf`_ or `string.IndexOfAny`_)
format                   Use `$ string interpolation`_
get_base_dir             StringExtensions.GetBaseDir
get_basename             StringExtensions.GetBaseName
get_extension            StringExtensions.GetExtension
get_file                 StringExtensions.GetFile
get_slice                N/A
get_slice_count          N/A
get_slicec               N/A
hash                     StringExtensions.Hash (Consider using `object.GetHashCode`_ unless you need to guarantee the same behavior as in GDScript)
hex_decode               StringExtensions.HexDecode (Consider using `System.Convert.FromHexString`_)
hex_to_int               StringExtensions.HexToInt (Consider using `int.Parse`_ or `long.Parse`_ with `System.Globalization.NumberStyles.HexNumber`_)
humanize_size            N/A
indent                   StringExtensions.Indent
insert                   `string.Insert`_ (Consider using `StringBuilder`_ to manipulate strings)
is_absolute_path         StringExtensions.IsAbsolutePath
is_empty                 `string.IsNullOrEmpty`_ or `string.IsNullOrWhiteSpace`_
is_relative_path         StringExtensions.IsRelativePath
is_subsequence_of        StringExtensions.IsSubsequenceOf
is_subsequence_ofn       StringExtensions.IsSubsequenceOfN
is_valid_filename        StringExtensions.IsValidFileName
is_valid_float           StringExtensions.IsValidFloat (Consider using `float.TryParse`_ or `double.TryParse`_)
is_valid_hex_number      StringExtensions.IsValidHexNumber
is_valid_html_color      StringExtensions.IsValidHtmlColor
is_valid_identifier      StringExtensions.IsValidIdentifier
is_valid_int             StringExtensions.IsValidInt (Consider using `int.TryParse`_ or `long.TryParse`_)
is_valid_ip_address      StringExtensions.IsValidIPAddress
join                     `string.Join`_
json_escape              StringExtensions.JSONEscape
left                     StringExtensions.Left (Consider using `string.Substring`_ or `string.AsSpan`_)
length                   `string.Length`_
lpad                     `string.PadLeft`_
lstrip                   `string.TrimStart`_
match                    StringExtensions.Match (Consider using `RegEx`_)
matchn                   StringExtensions.MatchN (Consider using `RegEx`_)
md5_buffer               StringExtensions.Md5Buffer (Consider using `System.Security.Cryptography.MD5.HashData`_)
md5_text                 StringExtensions.Md5Text (Consider using `System.Security.Cryptography.MD5.HashData`_ with StringExtensions.HexEncode)
naturalnocasecmp_to      N/A (Consider using `string.Equals`_ or `string.Compare`_)
nocasecmp_to             StringExtensions.NocasecmpTo or StringExtensions.CompareTo (Consider using `string.Equals`_ or `string.Compare`_)
num                      `float.ToString`_ or `double.ToString`_
num_int64                `int.ToString`_ or `long.ToString`_
num_scientific           `float.ToString`_ or `double.ToString`_
num_uint64               `uint.ToString`_ or `ulong.ToString`_
pad_decimals             StringExtensions.PadDecimals
pad_zeros                StringExtensions.PadZeros
path_join                StringExtensions.PathJoin
repeat                   Use `string constructor`_ or a `StringBuilder`_
replace                  `string.Replace`_ or `RegEx`_
replacen                 StringExtensions.ReplaceN (Consider using `string.Replace`_ or `RegEx`_)
reverse                  N/A
rfind                    StringExtensions.RFind (Consider using `string.LastIndexOf`_ or `string.LastIndexOfAny`_)
rfindn                   StringExtensions.RFindN (Consider using `string.LastIndexOf`_ or `string.LastIndexOfAny`_)
right                    StringExtensions.Right (Consider using `string.Substring`_ or `string.AsSpan`_)
rpad                     `string.PadRight`_
rsplit                   N/A
rstrip                   `string.TrimEnd`_
sha1_buffer              StringExtensions.Sha1Buffer (Consider using `System.Security.Cryptography.SHA1.HashData`_)
sha1_text                StringExtensions.Sha1Text (Consider using `System.Security.Cryptography.SHA1.HashData`_ with StringExtensions.HexEncode)
sha256_buffer            StringExtensions.Sha256Buffer (Consider using `System.Security.Cryptography.SHA256.HashData`_)
sha256_text              StringExtensions.Sha256Text (Consider using `System.Security.Cryptography.SHA256.HashData`_ with StringExtensions.HexEncode)
similarity               StringExtensions.Similarity
simplify_path            StringExtensions.SimplifyPath
split                    StringExtensions.Split (Consider using `string.Split`_)
split_floats             StringExtensions.SplitFloat
strip_edges              StringExtensions.StripEdges (Consider using `string.Trim`_, `string.TrimStart`_ or `string.TrimEnd`_)
strip_escapes            StringExtensions.StripEscapes
substr                   StringExtensions.Substr (Consider using `string.Substring`_ or `string.AsSpan`_)
to_ascii_buffer          StringExtensions.ToAsciiBuffer (Consider using `System.Text.Encoding.ASCII.GetBytes`_)
to_camel_case            StringExtensions.ToCamelCase
to_float                 StringExtensions.ToFloat (Consider using `float.TryParse`_ or `double.TryParse`_)
to_int                   StringExtensions.ToInt (Consider using `int.TryParse`_ or `long.TryParse`_)
to_lower                 `string.ToLower`_
to_pascal_case           StringExtensions.ToPascalCase
to_snake_case            StringExtensions.ToSnakeCase
to_upper                 `string.ToUpper`_
to_utf16_buffer          StringExtensions.ToUtf16Buffer (Consider using `System.Text.Encoding.UTF16.GetBytes`_)
to_utf32_buffer          StringExtensions.ToUtf32Buffer (Consider using `System.Text.Encoding.UTF32.GetBytes`_)
to_utf8_buffer           StringExtensions.ToUtf8Buffer (Consider using `System.Text.Encoding.UTF8.GetBytes`_)
to_wchar_buffer          StringExtensions.ToUtf16Buffer in Windows and StringExtensions.ToUtf32Buffer in other platforms
trim_prefix              StringExtensions.TrimPrefix
trim_suffix              StringExtensions.TrimSuffix
unicode_at               `string[int]`_ indexer
uri_decode               StringExtensions.URIDecode (Consider using `System.Uri.UnescapeDataString`_)
uri_encode               StringExtensions.URIEncode (Consider using `System.Uri.EscapeDataString`_)
validate_node_name       StringExtensions.ValidateNodeName
xml_escape               StringExtensions.XMLEscape
xml_unescape             StringExtensions.XMLUnescape
=======================  ==============================================================

Danh sách các method PackedByteArray của Godot tạo String và tương đương của chúng trong C#:

=========================  ==============================================================
GDScript                   C#
=========================  ==============================================================
get_string_from_ascii      StringExtensions.GetStringFromAscii (Consider using `System.Text.Encoding.ASCII.GetString`_)
get_string_from_utf16      StringExtensions.GetStringFromUtf16 (Consider using `System.Text.Encoding.UTF16.GetString`_)
get_string_from_utf32      StringExtensions.GetStringFromUtf32 (Consider using `System.Text.Encoding.UTF32.GetString`_)
get_string_from_utf8       StringExtensions.GetStringFromUtf8 (Consider using `System.Text.Encoding.UTF8.GetString`_)
hex_encode                 StringExtensions.HexEncode (Consider using `System.Convert.ToHexString`_)
=========================  ==============================================================

.. note::

    .NET cung cấp các method tiện ích xử lý path trong class `System.IO.Path`_. Chúng chỉ có thể được sử dụng với path gốc của OS, không phải path của Godot (các path bắt đầu bằng ``res://`` hoặc ``user://``). Xem :ref:`doc_data_paths`.

.. _$ string interpolation: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated
.. _double.ToString: https://learn.microsoft.com/en-us/dotnet/api/system.double.tostring
.. _double.TryParse: https://learn.microsoft.com/en-us/dotnet/api/system.double.tryparse
.. _float.ToString: https://learn.microsoft.com/en-us/dotnet/api/system.single.tostring
.. _float.TryParse: https://learn.microsoft.com/en-us/dotnet/api/system.single.tryparse
.. _int.Parse: https://learn.microsoft.com/en-us/dotnet/api/system.int32.parse
.. _int.ToString: https://learn.microsoft.com/en-us/dotnet/api/system.int32.tostring
.. _int.TryParse: https://learn.microsoft.com/en-us/dotnet/api/system.int32.tryparse
.. _long.Parse: https://learn.microsoft.com/en-us/dotnet/api/system.int64.parse
.. _long.ToString: https://learn.microsoft.com/en-us/dotnet/api/system.int64.tostring
.. _long.TryParse: https://learn.microsoft.com/en-us/dotnet/api/system.int64.tryparse
.. _uint.ToString: https://learn.microsoft.com/en-us/dotnet/api/system.uint32.tostring
.. _ulong.ToString: https://learn.microsoft.com/en-us/dotnet/api/system.uint64.tostring
.. _object.GetHashCode: https://learn.microsoft.com/en-us/dotnet/api/system.object.gethashcode
.. _RegEx: https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions
.. _string constructor: https://learn.microsoft.com/en-us/dotnet/api/system.string.-ctor
.. _string[int]: https://learn.microsoft.com/en-us/dotnet/api/system.string.chars
.. _string.AsSpan: https://learn.microsoft.com/en-us/dotnet/api/system.memoryextensions.asspan
.. _string.Compare: https://learn.microsoft.com/en-us/dotnet/api/system.string.compare
.. _string.Contains: https://learn.microsoft.com/en-us/dotnet/api/system.string.contains
.. _string.EndsWith: https://learn.microsoft.com/en-us/dotnet/api/system.string.endswith
.. _string.Equals: https://learn.microsoft.com/en-us/dotnet/api/system.string.equals
.. _string.IndexOf: https://learn.microsoft.com/en-us/dotnet/api/system.string.indexof
.. _string.IndexOfAny: https://learn.microsoft.com/en-us/dotnet/api/system.string.indexofany
.. _string.Insert: https://learn.microsoft.com/en-us/dotnet/api/system.string.insert
.. _string.IsNullOrEmpty: https://learn.microsoft.com/en-us/dotnet/api/system.string.isnullorempty
.. _string.IsNullOrWhiteSpace: https://learn.microsoft.com/en-us/dotnet/api/system.string.isnullorwhitespace
.. _string.Join: https://learn.microsoft.com/en-us/dotnet/api/system.string.join
.. _string.LastIndexOf: https://learn.microsoft.com/en-us/dotnet/api/system.string.lastindexof
.. _string.LastIndexOfAny: https://learn.microsoft.com/en-us/dotnet/api/system.string.lastindexofany
.. _string.Length: https://learn.microsoft.com/en-us/dotnet/api/system.string.length
.. _string.PadLeft: https://learn.microsoft.com/en-us/dotnet/api/system.string.padleft
.. _string.PadRight: https://learn.microsoft.com/en-us/dotnet/api/system.string.padright
.. _string.Remove: https://learn.microsoft.com/en-us/dotnet/api/system.string.remove
.. _string.Replace: https://learn.microsoft.com/en-us/dotnet/api/system.string.replace
.. _string.Split: https://learn.microsoft.com/en-us/dotnet/api/system.string.split
.. _string.StartsWith: https://learn.microsoft.com/en-us/dotnet/api/system.string.startswith
.. _string.Substring: https://learn.microsoft.com/en-us/dotnet/api/system.string.substring
.. _string.Trim: https://learn.microsoft.com/en-us/dotnet/api/system.string.trim
.. _string.TrimEnd: https://learn.microsoft.com/en-us/dotnet/api/system.string.trimend
.. _string.TrimStart: https://learn.microsoft.com/en-us/dotnet/api/system.string.trimstart
.. _string.ToLower: https://learn.microsoft.com/en-us/dotnet/api/system.string.tolower
.. _string.ToUpper: https://learn.microsoft.com/en-us/dotnet/api/system.string.toupper
.. _StringBuilder: https://learn.microsoft.com/en-us/dotnet/api/system.text.stringbuilder
.. _System.Convert.FromHexString: https://learn.microsoft.com/en-us/dotnet/api/system.convert.fromhexstring
.. _System.Convert.ToHexString: https://learn.microsoft.com/en-us/dotnet/api/system.convert.tohexstring
.. _System.Globalization.NumberStyles.HexNumber: https://learn.microsoft.com/en-us/dotnet/api/system.globalization.numberstyles#system-globalization-numberstyles-hexnumber
.. _System.IO.Path: https://learn.microsoft.com/en-us/dotnet/api/system.io.path
.. _System.Security.Cryptography.MD5.HashData: https://learn.microsoft.com/en-us/dotnet/api/system.security.cryptography.md5.hashdata
.. _System.Security.Cryptography.SHA1.HashData: https://learn.microsoft.com/en-us/dotnet/api/system.security.cryptography.sha1.hashdata
.. _System.Security.Cryptography.SHA256.HashData: https://learn.microsoft.com/en-us/dotnet/api/system.security.cryptography.sha256.hashdata
.. _System.Text.Encoding.ASCII.GetBytes: https://learn.microsoft.com/en-us/dotnet/api/system.text.asciiencoding.getbytes
.. _System.Text.Encoding.ASCII.GetString: https://learn.microsoft.com/en-us/dotnet/api/system.text.asciiencoding.getstring
.. _System.Text.Encoding.UTF16.GetBytes: https://learn.microsoft.com/en-us/dotnet/api/system.text.unicodeencoding.getbytes
.. _System.Text.Encoding.UTF16.GetString: https://learn.microsoft.com/en-us/dotnet/api/system.text.unicodeencoding.getstring
.. _System.Text.Encoding.UTF32.GetBytes: https://learn.microsoft.com/en-us/dotnet/api/system.text.utf32encoding.getbytes
.. _System.Text.Encoding.UTF32.GetString: https://learn.microsoft.com/en-us/dotnet/api/system.text.utf32encoding.getstring
.. _System.Text.Encoding.UTF8.GetBytes: https://learn.microsoft.com/en-us/dotnet/api/system.text.utf8encoding.getbytes
.. _System.Text.Encoding.UTF8.GetString: https://learn.microsoft.com/en-us/dotnet/api/system.text.utf8encoding.getstring
.. _System.Uri.EscapeDataString: https://learn.microsoft.com/en-us/dotnet/api/system.uri.escapedatastring
.. _System.Uri.UnescapeDataString: https://learn.microsoft.com/en-us/dotnet/api/system.uri.unescapedatastring

NodePath
--------

Method sau đây đã được chuyển thành property với tên khác:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``is_empty()``        ``IsEmpty``
====================  ==============================================================

Signal
------

Các method sau đây đã được chuyển thành property với tên tương ứng được thay đổi:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``get_name()``        ``Name``
``get_object()``      ``Owner``
====================  ==============================================================

Kiểu ``Signal`` triển khai awaitable pattern, nghĩa là có thể được sử dụng với keyword ``await``. Xem :ref:`doc_c_sharp_differences_await`.

Thay vì sử dụng kiểu ``Signal``, cách được khuyến nghị để sử dụng signal của Godot trong C# là dùng các C# event được tạo tự động. Xem :ref:`doc_c_sharp_signals`.

Callable
--------

Các method sau đây đã được chuyển thành property với tên tương ứng được thay đổi:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``get_object()``      ``Target``
``get_method()``      ``Method``
====================  ==============================================================

Hiện tại C# hỗ trợ ``Callable`` nếu một trong các điều kiện sau đúng:

* ``Callable`` được tạo bằng kiểu C# ``Callable``. * ``Callable`` là phiên bản cơ bản của ``Callable`` của engine. Các ``Callable`` tùy chỉnh không được hỗ trợ. Một ``Callable`` là tùy chỉnh khi có bất kỳ điều kiện nào sau đây:

  * ``Callable`` has bound information (``Callable``\ s created with ``bind``/``unbind`` are unsupported). * ``Callable`` was created from other languages through the GDExtension API.

Một số method như ``bind`` và ``unbind`` chưa được triển khai; thay vào đó, hãy sử dụng lambda:

.. code-block:: csharp

    string name = "John Doe";
    Callable callable = Callable.From(() => SayHello(name));

    void SayHello(string name)
    {
        GD.Print($"Hello {name}");
    }

Lambda capture biến ``name`` để có thể bind biến này vào method ``SayHello``.

RID
---

Kiểu này có tên là ``Rid`` trong C# để tuân theo quy ước đặt tên của .NET.

Các method sau đây đã được chuyển thành property với tên tương ứng được thay đổi:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``get_id()``          ``Id``
``is_valid()``        ``IsValid``
====================  ==============================================================

Basis
-----

Struct không thể có constructor không tham số trong C#. Vì vậy, ``new Basis()`` khởi tạo tất cả member nguyên thủy về giá trị mặc định của chúng. Hãy sử dụng ``Basis.Identity`` để có tương đương với ``Basis()`` trong GDScript và C++.

Method sau đây đã được chuyển thành property với tên khác:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``get_scale()``       ``Scale``
====================  ==============================================================

Transform2D
-----------

Struct không thể có constructor không tham số trong C#. Vì vậy, ``new Transform2D()`` khởi tạo tất cả member nguyên thủy về giá trị mặc định của chúng. Hãy sử dụng ``Transform2D.Identity`` để có tương đương với ``Transform2D()`` trong GDScript và C++.

Các method sau đây đã được chuyển thành property với tên tương ứng được thay đổi:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``get_rotation()``    ``Rotation``
``get_scale()``       ``Scale``
``get_skew()``        ``Skew``
====================  ==============================================================

Transform3D
-----------

Struct không thể có constructor không tham số trong C#. Vì vậy, ``new Transform3D()`` khởi tạo tất cả member nguyên thủy về giá trị mặc định của chúng. Hãy sử dụng ``Transform3D.Identity`` để có tương đương với ``Transform3D()`` trong GDScript và C++.

Các method sau đây đã được chuyển thành property với tên tương ứng được thay đổi:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``get_rotation()``    ``Rotation``
``get_scale()``       ``Scale``
====================  ==============================================================

Rect2
-----

Field sau đây đã được chuyển thành property với tên *hơi* khác:

================  ==================================================================
GDScript          C#
================  ==================================================================
``end``           ``End``
================  ==================================================================

Method sau đây đã được chuyển thành property với tên khác:

================  ==================================================================
GDScript          C#
================  ==================================================================
``get_area()``    ``Area``
================  ==================================================================

Rect2i
------

Kiểu này được đặt tên là ``Rect2I`` trong C# để tuân theo quy ước đặt tên của .NET.

Trường sau đây đã được chuyển đổi thành một property với tên *hơi* khác:

================  ==================================================================
GDScript          C#
================  ==================================================================
``end``           ``End``
================  ==================================================================

Method sau đây đã được chuyển đổi thành một property với tên khác:

================  ==================================================================
GDScript          C#
================  ==================================================================
``get_area()``    ``Area``
================  ==================================================================

AABB
----

Kiểu này được đặt tên là ``Aabb`` trong C# để tuân theo quy ước đặt tên của .NET.

Method sau đây đã được chuyển đổi thành một property với tên khác:

================  ==================================================================
GDScript          C#
================  ==================================================================
``get_volume()``  ``Volume``
================  ==================================================================

Quaternion
----------

Struct không thể có constructor không tham số trong C#. Do đó, ``new Quaternion()`` khởi tạo tất cả member nguyên thủy về giá trị mặc định của chúng. Vui lòng sử dụng ``Quaternion.Identity`` để có được phiên bản tương đương với ``Quaternion()`` trong GDScript và C++.

Projection
----------

Struct không thể có constructor không tham số trong C#. Do đó, ``new Projection()`` khởi tạo tất cả member nguyên thủy về giá trị mặc định của chúng. Vui lòng sử dụng ``Projection.Identity`` để có được phiên bản tương đương với ``Projection()`` trong GDScript và C++.

Color
-----

Struct không thể có constructor không tham số trong C#. Do đó, ``new Color()`` khởi tạo tất cả member nguyên thủy về giá trị mặc định của chúng (đại diện cho màu đen trong suốt). Vui lòng sử dụng ``Colors.Black`` để có được phiên bản tương đương với ``Color()`` trong GDScript và C++.

Method toàn cục ``Color8`` để tạo một Color từ các byte được cung cấp dưới dạng static method trong kiểu Color.

Các hằng số Color được cung cấp dưới dạng readonly property trong static class ``Colors``.

Method sau đây đã được chuyển đổi thành một property với tên khác:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``get_luminance()``   ``Luminance``
====================  ==============================================================

Method sau đây đã được chuyển đổi thành một method với tên khác:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``html(String)``      ``FromHtml(ReadOnlySpan<char>)``
====================  ==============================================================

Các method sau đây được cung cấp dưới dạng constructor:

====================  ==============================================================
GDScript              C#
====================  ==============================================================
``hex(int)``          ``Color(uint)``
``hex64(int)``        ``Color(ulong)``
====================  ==============================================================

Array
-----

Tương đương với packed array là ``System.Array``.

Xem thêm :ref:`PackedArray in C# <doc_c_sharp_collections_packedarray>`.

Sử dụng ``Godot.Collections.Array`` cho một array ``Variant`` không định kiểu. ``Godot.Collections.Array<T>`` là một wrapper type-safe cho ``Godot.Collections.Array``.

Xem thêm :ref:`Array in C# <doc_c_sharp_collections_array>`.

Dictionary
----------

Sử dụng ``Godot.Collections.Dictionary`` cho một dictionary ``Variant`` không định kiểu. ``Godot.Collections.Dictionary<TKey, TValue>`` là một wrapper type-safe cho ``Godot.Collections.Dictionary``.

Xem thêm :ref:`Dictionary in C# <doc_c_sharp_collections_dictionary>`.

Variant
-------

``Godot.Variant`` được dùng để biểu diễn kiểu :ref:`Variant <class_Variant>` gốc của Godot. Bất kỳ :ref:`Variant-compatible type <c_sharp_variant_compatible_types>` nào cũng có thể được chuyển đổi từ hoặc sang kiểu này.

Xem thêm: :ref:`doc_c_sharp_variant`.

Giao tiếp với các ngôn ngữ scripting khác
-----------------------------------------

Nội dung này được giải thích đầy đủ trong :ref:`doc_cross_language_scripting`.

.. _doc_c_sharp_differences_await:

Từ khóa ``await``
-----------------

Có thể đạt được điều tương tự như từ khóa ``await`` của GDScript bằng `await keyword <https://docs.microsoft.com/en-US/dotnet/csharp/language-reference/keywords/await>`_ của C#.

Từ khóa ``await`` trong C# có thể được sử dụng với bất kỳ biểu thức awaitable nào. Từ khóa này thường được sử dụng với các toán hạng thuộc kiểu `Task`_, `Task<TResult>`_, `ValueTask`_ hoặc `ValueTask<TResult>`_.

Một biểu thức ``t`` là awaitable nếu thỏa mãn một trong các điều kiện sau:

* ``t`` có kiểu tại thời điểm biên dịch là ``dynamic``. * ``t`` có một instance method hoặc extension method có thể truy cập tên là ``GetAwaiter``, không có tham số và không có type parameter, với kiểu trả về ``A`` thỏa mãn tất cả các điều kiện sau:

  * ``A`` triển khai interface ``System.Runtime.CompilerServices.INotifyCompletion``. * ``A`` có một instance property ``IsCompleted`` có thể truy cập, có thể đọc, thuộc kiểu ``bool``. * ``A`` có một instance method ``GetResult`` có thể truy cập, không có tham số và không có type parameter.

.. _Task: https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.task
.. _Task<TResult>: https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1
.. _ValueTask: https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.valuetask
.. _ValueTask<TResult>: https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.valuetask-1

Có thể đạt được phiên bản tương đương với việc await một signal trong GDScript bằng từ khóa ``await`` và ``GodotObject.ToSignal``.

Ví dụ:

.. code-block:: csharp

  public async Task SomeFunction()
  {
      await ToSignal(timer, Timer.SignalName.Timeout);
      GD.Print("After timeout");
  }
