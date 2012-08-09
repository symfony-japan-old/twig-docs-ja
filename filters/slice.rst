``slice``
===========

.. versionadded:: 1.6
    slice フィルタは、Twig 1.6 で追加されました。

``slice`` フィルタは、シーケンス、マッピングまたは、文字列の一部を展開します:

.. code-block:: jinja

    {% for i in [1, 2, 3, 4]|slice(1, 2) %}
        {# 2 と 3 に対して反復処理されます #}
    {% endfor %}

    {{ '1234'|slice(1, 2) }}

    {# 23 が出力されます #}

開始位置と長さの引数には、正しい式であれば、いずれも使えます:

.. code-block:: jinja

    {% for i in [1, 2, 3, 4]|slice(start, length) %}
        {# ... #}
    {% endfor %}

シンタックスシュガーとして、``[]`` 記法も使えます:

.. code-block:: jinja

    {% for i in [1, 2, 3, 4][start:length] %}
        {# ... #}
    {% endfor %}

    {{ '1234'[1:2] }}

``slice`` フィルタは、配列に対しては、`array_slice`_ PHP 関数として動作し、
文字列に対しては、`substr`_ として動作します。

開始位置が負の数でない場合は、結果のシーケンスは、フィルタ対象の変数の指定された開始位置から
始まります。 開始位置が負の数の場合は、シーケンスは、変数の最後を起点とした位置
から始まります。

長さが指定されていて、正の数の場合は、結果のシーケンスは、最大で、
その要素の数になります。 フィルタ対象の変数が、指定された長さよりも短い場合は、その変数の中で利用可能な
要素のみが現れることになります。 長さが指定されていて、負の数の場合は、
シーケンスは、その変数の最後を起点としたその長さだけ
になります。 省略された場合は、シーケンスは、その変数の開始位置から最後までの
全部になります。

.. note::

    It also works with objects implementing the `Traversable`_ interface.

.. _`Traversable`: http://php.net/manual/en/class.traversable.php
.. _`array_slice`: http://php.net/array_slice
.. _`substr`:      http://php.net/substr

.. 2012/08/09 goohib d9dc813dfd64119815edc4ec533528de2ef4c3d6
