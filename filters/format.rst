``format``
==========

``format`` フィルタは、指定した文字列をプレースホルダを置換することによりフォーマットします
(プレースホルダは、`printf`_ の表記法に従います):

.. code-block:: jinja

    {{ "%s と %s が好きです。"|format(foo, "bar") }}

    {# パラメータ foo が、同じ文字列 foo であるとき、
       foo と bar が好きです。 が返ります。 #}

.. _`printf`: http://www.php.net/printf

.. seealso:: :doc:`replace<replace>`

.. 2012/08/09 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
