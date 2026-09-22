.. _doc_custom_resource_format_loaders:

Trình nạp định dạng tài nguyên tùy chỉnh
========================================

Giới thiệu
----------

ResourceFormatLoader là một giao diện factory để nạp các asset dạng tệp. Resource là các container chính. Khi gọi load lại trên cùng một đường dẫn tệp, Resource đã được nạp trước đó sẽ được tham chiếu. Do đó, các resource đã nạp phải không có trạng thái.

Hướng dẫn này giả định người đọc biết cách tạo các module C++ và kiểu dữ liệu Godot. Nếu không, hãy tham khảo hướng dẫn này: :ref:`doc_custom_modules_in_cpp`

Tham khảo
~~~~~~~~~

- :ref:`ResourceLoader<class_resourceloader>`
- `core/io/resource_loader.cpp <https://github.com/godotengine/godot/blob/master/core/io/resource_loader.cpp>`_

Dùng để làm gì?
---------------

- Bổ sung hỗ trợ cho nhiều định dạng tệp
- Các định dạng âm thanh
- Các định dạng video
- Các model machine learning

Không dùng cho việc gì?
-----------------------

- Ảnh raster

Nên sử dụng ImageFormatLoader để nạp ảnh.

Tham khảo
~~~~~~~~~

- `core/io/image_loader.h <https://github.com/godotengine/godot/blob/master/core/io/image_loader.h>`_


Tạo một ResourceFormatLoader
----------------------------

Mỗi định dạng tệp gồm một container dữ liệu và một ``ResourceFormatLoader``.

ResourceFormatLoader là các class trả về toàn bộ metadata cần thiết để hỗ trợ các extension mới trong Godot. Class này phải trả về tên định dạng và chuỗi extension.

Ngoài ra, ResourceFormatLoader phải chuyển đổi đường dẫn tệp thành resource bằng hàm ``load``. Để nạp một resource, ``load`` phải đọc và xử lý việc serialization dữ liệu.


.. code-block:: cpp
    :caption: resource_loader_json.h

    #pragma once

    #include "core/io/resource_loader.h"

    class ResourceFormatLoaderJson : public ResourceFormatLoader {
        GDCLASS(ResourceFormatLoaderJson, ResourceFormatLoader);
    public:
        virtual RES load(const String &p_path, const String &p_original_path, Error *r_error = NULL);
        virtual void get_recognized_extensions(List<String> *r_extensions) const;
        virtual bool handles_type(const String &p_type) const;
        virtual String get_resource_type(const String &p_path) const;
    };

.. code-block:: cpp
    :caption: resource_loader_json.cpp

    #include "resource_loader_json.h"

    #include "resource_json.h"

    RES ResourceFormatLoaderJson::load(const String &p_path, const String &p_original_path, Error *r_error) {
    Ref<JsonResource> json = memnew(JsonResource);
        if (r_error) {
            *r_error = OK;
        }
        Error err = json->load_file(p_path);
        return json;
    }

    void ResourceFormatLoaderJson::get_recognized_extensions(List<String> *r_extensions) const {
        if (!r_extensions->find("json")) {
            r_extensions->push_back("json");
        }
    }

    String ResourceFormatLoaderJson::get_resource_type(const String &p_path) const {
        return "Resource";
    }

    bool ResourceFormatLoaderJson::handles_type(const String &p_type) const {
        return ClassDB::is_parent_class(p_type, "Resource");
    }

Tạo một ResourceFormatSaver
---------------------------

Nếu bạn muốn có thể chỉnh sửa và lưu một resource, bạn có thể triển khai một ``ResourceFormatSaver``:

.. code-block:: cpp
    :caption: resource_saver_json.h

    #pragma once

    #include "core/io/resource_saver.h"

    class ResourceFormatSaverJson : public ResourceFormatSaver {
        GDCLASS(ResourceFormatSaverJson, ResourceFormatSaver);
    public:
        virtual Error save(const String &p_path, const RES &p_resource, uint32_t p_flags = 0);
        virtual bool recognize(const RES &p_resource) const;
        virtual void get_recognized_extensions(const RES &p_resource, List<String> *r_extensions) const;
    };

.. code-block:: cpp
    :caption: resource_saver_json.cpp

    #include "resource_saver_json.h"

    #include "resource_json.h"
    #include "scene/resources/resource_format_text.h"

    Error ResourceFormatSaverJson::save(const String &p_path, const RES &p_resource, uint32_t p_flags) {
        Ref<JsonResource> json = memnew(JsonResource);
        Error error = json->save_file(p_path, p_resource);
        return error;
    }

    bool ResourceFormatSaverJson::recognize(const RES &p_resource) const {
        return Object::cast_to<JsonResource>(*p_resource) != NULL;
    }

    void ResourceFormatSaverJson::get_recognized_extensions(const RES &p_resource, List<String> *r_extensions) const {
        if (Object::cast_to<JsonResource>(*p_resource)) {
            r_extensions->push_back("json");
        }
    }

Tạo kiểu dữ liệu tùy chỉnh
--------------------------

Godot có thể không có một thành phần thay thế phù hợp trong :ref:`doc_core_types` hoặc các resource được quản lý. Godot cần một kiểu dữ liệu mới được đăng ký để hiểu các định dạng nhị phân bổ sung, chẳng hạn như các model machine learning.

Sau đây là ví dụ về cách tạo một kiểu dữ liệu tùy chỉnh:

.. code-block:: cpp
    :caption: resource_json.h

    #pragma once

    #include "core/io/json.h"
    #include "core/variant_parser.h"

    class JsonResource : public Resource {
        GDCLASS(JsonResource, Resource);

    protected:
        static void _bind_methods() {
            ClassDB::bind_method(D_METHOD("set_dict", "dict"), &JsonResource::set_dict);
            ClassDB::bind_method(D_METHOD("get_dict"), &JsonResource::get_dict);

            ADD_PROPERTY(PropertyInfo(Variant::DICTIONARY, "content"), "set_dict", "get_dict");
        }

    private:
        Dictionary content;

    public:
        Error load_file(const String &p_path);
        Error save_file(const String &p_path, const RES &p_resource);

        void set_dict(const Dictionary &p_dict);
        Dictionary get_dict();
    };

.. code-block:: cpp
    :caption: resource_json.cpp

    #include "resource_json.h"

    Error JsonResource::load_file(const String &p_path) {
        Error error;
        FileAccess *file = FileAccess::open(p_path, FileAccess::READ, &error);
        if (error != OK) {
            if (file) {
                file->close();
            }
            return error;
        }

        String json_string = String("");
        while (!file->eof_reached()) {
            json_string += file->get_line();
        }
        file->close();

        String error_string;
        int error_line;
        JSON json;
        Variant result;
        error = json.parse(json_string, result, error_string, error_line);
        if (error != OK) {
            file->close();
            return error;
        }

        content = Dictionary(result);
        return OK;
    }

    Error JsonResource::save_file(const String &p_path, const RES &p_resource) {
        Error error;
        FileAccess *file = FileAccess::open(p_path, FileAccess::WRITE, &error);
        if (error != OK) {
            if (file) {
                file->close();
            }
            return error;
        }

        Ref<JsonResource> json_ref = p_resource.get_ref_ptr();
        JSON json;

        file->store_string(json.print(json_ref->get_dict(), "    "));
        file->close();
        return OK;
    }

    void JsonResource::set_dict(const Dictionary &p_dict) {
        content = p_dict;
    }

    Dictionary JsonResource::get_dict() {
        return content;
    }

Các điểm cần lưu ý
~~~~~~~~~~~~~~~~~~

Một số thư viện có thể không định nghĩa một số routine phổ biến, chẳng hạn như xử lý IO. Vì vậy, cần chuyển đổi các lời gọi của Godot.

Ví dụ, sau đây là code để chuyển đổi các lời gọi ``FileAccess`` thành ``std::istream``.

.. code-block:: cpp

    #include "core/io/file_access.h"

    #include <istream>
    #include <streambuf>

    class GodotFileInStreamBuf : public std::streambuf {

    public:
        GodotFileInStreamBuf(FileAccess *fa) {
            _file = fa;
        }
        int underflow() {
            if (_file->eof_reached()) {
                return EOF;
            } else {
                size_t pos = _file->get_position();
                uint8_t ret = _file->get_8();
                _file->seek(pos); // Cần thiết vì get_8() tiến con trỏ đọc.
                return ret;
            }
        }
        int uflow() {
            return _file->eof_reached() ? EOF : _file->get_8();
        }

    private:
        FileAccess *_file;
    };


Tham khảo
~~~~~~~~~

- `istream <https://cplusplus.com/reference/istream/istream/>`_
- `streambuf <https://cplusplus.com/reference/streambuf/streambuf/?kw=streambuf>`_
- `core/io/file_access.h <https://github.com/godotengine/godot/blob/master/core/io/file_access.h>`_

Đăng ký định dạng tệp mới
-------------------------

Godot đăng ký ``ResourcesFormatLoader`` với một handler ``ResourceLoader``. Handler này tự động chọn loader phù hợp khi gọi ``load``.

.. code-block:: cpp
    :caption: register_types.h

    void register_json_types();
    void unregister_json_types();

.. code-block:: cpp
    :caption: register_types.cpp

    #include "register_types.h"

    #include "core/class_db.h"
    #include "resource_loader_json.h"
    #include "resource_saver_json.h"
    #include "resource_json.h"

    static Ref<ResourceFormatLoaderJson> json_loader;
    static Ref<ResourceFormatSaverJson> json_saver;

    void register_json_types() {
        ClassDB::register_class<JsonResource>();

        json_loader.instantiate();
        ResourceLoader::add_resource_format_loader(json_loader);

        json_saver.instantiate();
        ResourceSaver::add_resource_format_saver(json_saver);
    }

    void unregister_json_types() {
        ResourceLoader::remove_resource_format_loader(json_loader);
        json_loader.unref();

        ResourceSaver::remove_resource_format_saver(json_saver);
        json_saver.unref();
    }

Tham khảo
~~~~~~~~~

- `core/io/resource_loader.cpp <https://github.com/godotengine/godot/blob/master/core/io/resource_loader.cpp>`_

Nạp bằng GDScript
-----------------

Lưu một tệp có tên ``demo.json`` với nội dung sau và đặt tệp đó vào thư mục gốc của project:

.. code-block:: json

    {
      "savefilename": "demo.json",
      "demo": [
        "welcome",
        "to",
        "godot",
        "resource",
        "loaders"
      ]
    }

Sau đó, gắn script sau vào bất kỳ node nào:

::

    extends Node

    @onready var json_resource = load("res://demo.json")

    func _ready():
        print(json_resource.get_dict())

.. _`core/io/resource_loader.cpp`: https://github.com/godotengine/godot/blob/master/core/io/resource_loader.cpp
.. _`core/io/image_loader.h`: https://github.com/godotengine/godot/blob/master/core/io/image_loader.h
.. _`istream`: https://cplusplus.com/reference/istream/istream/
.. _`streambuf`: https://cplusplus.com/reference/streambuf/streambuf/?kw=streambuf
.. _`core/io/file_access.h`: https://github.com/godotengine/godot/blob/master/core/io/file_access.h
