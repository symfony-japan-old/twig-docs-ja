``escape``
==========

.. versionadded:: 1.9.0
    Twig 1.9.0 で、``css`` 、``url`` 、``html_attr`` ストラテジが
    追加されました。
    

``escape`` フィルタは、文字列を最終出力に安全に挿入できるようにエスケープします。
テンプレートのコンテキストに応じて、異なるエスケープストラテジが
利用できます。

デフォルトでは、HTMLエスケープストラテジが使用されます:

.. code-block:: jinja

    {{ user.username|escape }}

利便性のために、``e`` フィルタが、別名として定義されています:

.. code-block:: jinja

    {{ user.username|e }}

``escape`` フィルタは、利用するエスケープストラテジを定義するオプションの引数があるので、
HTML以外のコンテキストでも利用することができます:

.. code-block:: jinja

    {{ user.username|e }}
    {# is equivalent to #}
    {{ user.username|e('html') }}

それから、下記は、JavaScript コードの中の変数をエスケープする方法です:

.. code-block:: jinja

    {{ user.username|escape('js') }}
    {{ user.username|e('js') }}

``escape`` フィルタでは、次のエスケープストラテジが利用できます:

* ``html``: **HTML 本文** コンテキストで文字列をエスケープします。

* ``js``: **JavaScript コンテキスト** で文字列をエスケープします。

* ``css``: **CSS コンテキスト** で、文字列をエスケープします。 CSS エスケープは、
  CSS に挿入されるどんな文字列にも適用でき、
  英数字以外をすべてエスケープします。

* ``url``: **URI または パラメータコンテキスト** で文字列をエスケープします。 これは、URI
  全体に使用すべきではありません。挿入された部分にのみ使用すべきです。

* ``html_attr``: **HTML 属性** コンテキストで、文字列をエスケープします。

.. note::

    内部的には、``escape`` は、HTMLのエスケープに、PHP ネイティブの `htmlspecialchars`_ 関数を
    使います。

.. _`htmlspecialchars`: http://php.net/htmlspecialchars

.. 2012/08/09 goohib 7657c01e65695a9a53cf63e0d8e4b872ce00451b
