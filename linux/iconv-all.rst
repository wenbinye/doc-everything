批量替换文件编码
==============================

.. code-block:: bash

    for file in `find src -name '*.java'`
    do
        iconv -f gbk -t utf8 -o "$file.new" "$file" &&
        mv -f "$file.new" "$file"
    done
