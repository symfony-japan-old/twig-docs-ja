``random``
==========

.. versionadded:: 1.5
    random 関数は、Twig 1.5 で追加されました。

.. versionadded:: 1.6
    Twig 1.6で、文字列と整数の処理に対応しました。

``random`` 関数は、渡されたパラメータの型に応じて、
ランダムな値を返します:

* シーケンスから取り出したランダムな要素;
* 文字列の中から取り出したランダムな文字;
* 0から整数の引数（この値も含みます）の間の中のランダムな整数。

.. code-block:: jinja

    {{ random(['apple', 'orange', 'citrus']) }} {# 出力例: orange #}
    {{ random('ABC') }}                         {# 出力例: C #}
    {{ random() }}                              {# 出力例: 15386094 (PHPネイティブの `mt_rand`_ 関数として動作します) #}
    {{ random(5) }}                             {# 出力例: 3 #}

.. _`mt_rand`: http://php.net/mt_rand

.. 2012/08/20 goohib cbadac91cde2e47cf5a22f1c1670630c0aeaa399
