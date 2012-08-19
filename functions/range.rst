``range``
=========

整数の等差数列のリストを返します:

.. code-block:: jinja

    {% for i in range(0, 3) %}
        {{ i }},
    {% endfor %}

    {# returns 0, 1, 2, 3 #}

ステップ数が渡された場合（第3三引数で）、加算値 (または、
減算値) が指定されます:

.. code-block:: jinja

    {% for i in range(0, 6, 2) %}
        {{ i }},
    {% endfor %}

    {# returns 0, 2, 4, 6 #}

Twig のビルトインの ``..`` 演算子は、``range`` 関数の
シンタックスシュガーです (ステップ数は1になります):

.. code-block:: jinja

    {% for i in 0..3 %}
        {{ i }},
    {% endfor %}

.. tip::

    ``range`` 関数は、PHPネイティブの `range`_ 関数として動作します。

.. _`range`: http://php.net/range

.. 2012/08/20 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
