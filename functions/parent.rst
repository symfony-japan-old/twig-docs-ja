``parent``
==========

テンプレート継承を使っているとき、``parent`` 関数を使えば、
オーバーライドしているブロックの親ブロックをレンダリングできます:

.. code-block:: jinja

    {% extends "base.html" %}

    {% block sidebar %}
        <h3>目次</h3>
        ...
        {{ parent() }}
    {% endblock %}

``parent()`` を呼び出すと、``base.html`` テンプレートで定義されている``sidebar`` ブロック
のコンテンツが返ります。

.. seealso:: :doc:`extends<../tags/extends>`, :doc:`block<../functions/block>`, :doc:`block<../tags/block>`

.. 2012/08/20 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
