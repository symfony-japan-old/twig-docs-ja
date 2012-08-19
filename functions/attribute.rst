``attribute``
=============

.. versionadded:: 1.2
    ``attribute`` 関数は、Twig 1.2 で追加されました。

``attribute`` は、変数の "動的な" 属性にアクセスするために使えます:

.. code-block:: jinja

    {{ attribute(object, method) }}
    {{ attribute(object, method, arguments) }}
    {{ attribute(array, item) }}

.. note::

    導出アルゴリズムは、``.`` 記法で使われているものと同じものですが、
    要素は、有効な式であれば、いずれも取りうるところが違います。

.. 2012/08/20 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
