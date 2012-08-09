``default``
===========

``default`` フィルタは、渡された値が未定義か空のときに、指定されたデフォルト値を
返し、そうでないときは、その変数の値を返します:

.. code-block:: jinja

    {{ var|default('varは、定義されていません') }}

    {{ var.foo|default('varのfoo要素は、定義されていません') }}

    {{ var['foo']|default('varのfoo要素は、定義されていません') }}

    {{ ''|default('渡された変数は空です')  }}

メソッド呼び出しの中で変数を使う式で ``default`` フィルタを使用するときは、
変数が未定義になる可能性のあるいずれの場合にも、確実に ``default`` フィルタを
使用するようにしてください:

.. code-block:: jinja

    {{ var.method(foo|default('foo'))|default('foo') }}

.. note::

    「未定義」や「空」の意味について詳しく理解するには、:doc:`defined<../tests/defined>` テストと
    :doc:`empty<../tests/empty>` テストのドキュメントをお読みください。

.. 2012/08/09 goohib 88dd4ac5797a4ffe702a5eb5a0e5f5f5bea187bf
