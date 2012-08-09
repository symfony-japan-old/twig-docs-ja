``nl2br``
=========

.. versionadded:: 1.5
    nl2br フィルタは、Twig 1.5 で追加されました。

``nl2br`` フィルタは、改行文字の前に HTML の改行タグを挿入します:

.. code-block:: jinja

    {{ "Twigが好き。\nあなたもきっと好きになる。"|nl2br }}
    {# 出力結果

        Twigが好き。<br />
        あなたもきっと好きになる。

    #}

.. note::

    ``nl2br`` フィルタは、変換する前に、入力を
    事前エスケープ (pre-escape) します。

.. 2012/08/09 goohib 7194b1adaad92a16d6461c5a6fdfa42829df1dfe
