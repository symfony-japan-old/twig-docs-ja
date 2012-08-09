``trim``
========

.. versionadded:: 1.6.2
    trim フィルタは、Twig 1.6.2 で追加されました。

``trim`` フィルタは、空白文字 (または、他の文字) を文字列の最初と最後から
取り除きます:

.. code-block:: jinja

    {{ '  I like Twig.  '|trim }}

    {# 'I like Twig.' が出力されます #}

    {{ '  I like Twig.'|trim('.') }}

    {# '  I like Twig' が出力されます #}

.. note::

    内部的には、Twig は、PHPの `trim`_ 関数を使います。

.. _`trim`: http://php.net/trim

.. 2012/08/09 goohib a4fa6db03b70e679e0da3cd43309e22cc8d07d2a
