``filter``
==========

フィルタタグは、テンプレートデータの中のあるブロックに、標準の Twig フィルタを適用できる
というものです。 このために用意された、``filter`` タグで単にコードを囲んでください:

.. code-block:: jinja

    {% filter upper %}
        このテキストは大文字になります
    {% endfilter %}

フィルタを続けて呼び出すこともできます:

.. code-block:: jinja

    {% filter lower|escape %}
        <strong>何かのテキスト</strong>
    {% endfilter %}

    {# "&lt;strong&gt;何かのテキスト&lt;/strong&gt;" と出力されます #}
