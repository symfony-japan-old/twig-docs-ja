``number_format``
=================

.. versionadded:: 1.5
    number_format フィルタは、Twig 1.5 で追加されました

``number_format`` フィルタは、数値をフォーマットします。 このフィルタは、PHP の
`number_format`_ 関数のラッパーです:

.. code-block:: jinja

    {{ 200.35|number_format }}

小数位の桁数、小数点記号、千の位の区切り文字を
追加の引数でコントロールできます:

.. code-block:: jinja

    {{ 9800.333|number_format(2, '.', ',') }}

書式が指定されないときは、Twigでは、次のようなデフォルトの書式を
使用します:

- 少数桁は 0。
- ``.`` を小数点の記号として使用する。
- ``,`` を千の位の区切り文字として使用する。

コアエクステンションを通じて、このデフォルトは簡単に変更できます:

.. code-block:: php

    $twig = new Twig_Environment($loader);
    $twig->getExtension('core')->setNumberFormat(3, '.', ',');

``number_format`` にセットするデフォルトは、呼び出しの際に上書きすることができ、
これには、追加のパラメータを使用します。

.. _`number_format`: http://php.net/number_format

.. 2012/08/09 goohib 1d1b949150ec93cf400b9cd562cb4f0068d33cc2
