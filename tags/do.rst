``do``
======

.. versionadded:: 1.5
    do タグは、Twig 1.5 で追加されました。

``do`` タグは、通常の変数式 (``{{ ... }}``) 
とまったく同様に動作するものですが、何も出力しません:

.. code-block:: jinja

    {% do 1 + 2 %}

-- 2012/08/08 goohib 4b8a0e5e7a002afe273d2fa67df1facd04195ea3
