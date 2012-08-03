``include``
===========

``include`` ステートメントは、テンプレートをインクルードし、インクルードしたファイルの内容をレンダリングしたものを
現在の名前空間に返します:

.. code-block:: jinja

    {% include 'header.html' %}
        本文
    {% include 'footer.html' %}

インクルードされたテンプレートは、現在有効なコンテキストの変数へのアクセスが可能です。

ファイルシステムローダーを使っている場合は、テンプレートは、ローダーで定義されているパスの中を
探します。

追加の変数を加えることもできますが、こうするには、``with`` キーワードの後に変数を渡します:

.. code-block:: jinja

    {# テンプレート foo は、現在のコンテキストの変数と、変数 foo にアクセスできます #}
    {% include 'foo' with {'foo': 'bar'} %}

    {% set vars = {'foo': 'bar'} %}
    {% include 'foo' with vars %}

現在のコンテキストへのアクセスを無効にすることもでき、``only`` キーワードを加えることで、これができます:

.. code-block:: jinja

    {# 変数 foo のみアクセスできます #}
    {% include 'foo' with {'foo': 'bar'} only %}

.. code-block:: jinja

    {# どの変数もアクセスできません #}
    {% include 'foo' only %}

.. tip::

    エンドユーザーが作成したテンプレートをインクルードするときには、これをサンドボックス化する
    ことを考慮すべきです。 :doc:`開発者のための Twig<../api>` の章、
    それから、:doc:`sandbox<../tags/sandbox>` タグ のドキュメントで、これについてのさらに詳しい情報をご覧いただけます。

テンプレートの名前には、有効な Twig の式であれば、どれも使えます:

.. code-block:: jinja

    {% include some_var %}
    {% include ajax ? 'ajax.html' : 'not_ajax.html' %}

式が ``Twig_Template`` オブジェクトとして評価された場合は、Twig はそれを
直接使います::

    // {% include template %}

    $template = $twig->loadTemplate('some_template.twig');

    $twig->loadTemplate('template.twig')->display(array('template' => $template));

.. versionadded:: 1.2
    ``ignore missing`` の機能は、Twig 1.2から追加されています。

include を ``ignore missing`` でマークすると、テンプレートが見つからない場合には、
Twigがステートメントを無視するようにできます。 これは、テンプレート名の
すぐ後に記述しなければなりません。 有効な例を下記にいくつか挙げます:

.. code-block:: jinja

    {% include "sidebar.html" ignore missing %}
    {% include "sidebar.html" ignore missing with {'foo': 'bar} %}
    {% include "sidebar.html" ignore missing only %}

.. versionadded:: 1.2
    Twig 1.2 よりテンプレートの配列を渡すことが可能になっています。

また、テンプレートのリストを渡すこともでき、リストのテンプレートがインクルードされる前に、
存在するか確認されます。 最初に存在したテンプレートがインクルードされます:

.. code-block:: jinja

    {% include ['page_detailed.html', 'page.html'] %}

``ignore missing`` が指定されたときで、テンプレートが一つも見つからない場合には、
フォールバックして何もレンダリングされません、指定されていない場合は、例外がスローされます。
