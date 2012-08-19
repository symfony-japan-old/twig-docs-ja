``date``
========

.. versionadded:: 1.6
    date 関数は、Twig 1.6 から追加されています。

.. versionadded:: 1.6.1
    デフォルトのタイムゾーンは、Twig 1.6.1 から利用できます。

日付の比較ができるよう、引数を日付に変換します:

.. code-block:: jinja

    {% if date(user.created_at) < date('+2days') %}
        {# 何かを実行 #}
    {% endif %}

引数は、`date`_ 関数でサポートされている書式でなければなりません。

タイムゾーンを第2引数で渡すことができます:

.. code-block:: jinja

    {% if date(user.created_at) < date('+2days', 'Europe/Paris') %}
        {# 何かを実行 #}
    {% endif %}

引数が何も渡されないときは、この関数は現在の日付を返します:

.. code-block:: jinja

    {% if date(user.created_at) < date() %}
        {# 常に! #}
    {% endif %}

.. note::

    デフォルトのタイムゾーンをグローバルに設定することもでき、それには、
    ``core`` エクステンションのインスタンスで、``setTimezone()`` を呼び出します:

    .. code-block:: php

        $twig = new Twig_Environment($loader);
        $twig->getExtension('core')->setTimezone('Europe/Paris');

.. _`date`: http://www.php.net/date

.. 2012/08/20 goohib e9cfd2ec8555f237a5a2dcc66d61065f9c1c4566
