``replace``
===========

``replace`` フィルタは、指定された文字をプレースホルダを置き換えてフォーマットします
(プレースホルダは、何でも構いません):

.. code-block:: jinja

    {{ "%this% と %that% が好き。"|replace({'%this%': foo, '%that%': "bar"}) }}

    {# foo と bar が好き。 と返ります。
       このとき、パラメータ foo は、同じ foo という文字列であるとします。 #}

.. seealso:: :doc:`format<format>`

.. 2012/08/09 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
