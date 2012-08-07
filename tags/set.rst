``set``
=======

コードブロックの中で、変数に値を代入することもできます。 代入には
``set`` タグを使用し、これは、複数の対象への代入も可能です:

.. code-block:: jinja

    {% set foo = 'foo' %}

    {% set foo = [1, 2] %}

    {% set foo = {'foo': 'bar'} %}

    {% set foo = 'foo' ~ 'bar' %}

    {% set foo, bar = 'foo', 'bar' %}

``set`` タグは、テキストの塊を 'キャプチャ' するためにも使用できます:

.. code-block:: jinja

    {% set foo %}
      <div id="pagination">
        ...
      </div>
    {% endset %}

.. caution::

    自動エスケープを有効にしている場合、Twigでは、テキストの塊を
    キャプチャする時にのみ、内容を安全にするよう考慮されます。

-- 2012/08/08 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
