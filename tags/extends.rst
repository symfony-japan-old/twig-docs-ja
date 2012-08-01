``extends``
===========

``extends`` は、テンプレートを別のテンプレートから継承するために使用できます。

.. note::

    PHPと同様、Twigでは、多重継承はサポートされません。 ですから、レンダリングにつき、
    ひとつのextendsタグのみ利用可能です。 しかしながら、Twigでは、水平方向の再利用 ( horizontal
    :doc:`reuse<use>` ) であれば利用可能です。

ベースになるテンプレート、 ``base.html`` を定義してみましょう。このテンプレートは、単純なHTMLの
骨組みのドキュメントを定義するものです:

.. code-block:: html+jinja

    <!DOCTYPE html>
    <html>
        <head>
            {% block head %}
                <link rel="stylesheet" href="style.css" />
                <title>{% block title %}{% endblock %} - MY ウェブページ</title>
            {% endblock %}
        </head>
        <body>
            <div id="content">{% block content %}{% endblock %}</div>
            <div id="footer">
                {% block footer %}
                    &copy; Copyright 2011 by <a href="http://domain.invalid/">you</a>.
                {% endblock %}
            </div>
        </body>
    </html>

この例では、:doc:`block<tags/block>` タグで、4つのブロックが定義されていますが、
このブロックの内容は、子テンプレートで埋めることができます。 ``block`` タグが行うことのすべては、
テンプレートエンジンに、子テンプレートが、各部分をオーバーライドできるのだということを教えるだけなのです。

子テンプレート
--------------

子テンプレートは、大体このようになっています:

.. code-block:: jinja

    {% extends "base.html" %}

    {% block title %}Index{% endblock %}
    {% block head %}
        {{ parent() }}
        <style type="text/css">
            .important { color: #336699; }
        </style>
    {% endblock %}
    {% block content %}
        <h1>Index</h1>
        <p class="important">
            素晴らしいホームページへようこそ。
        </p>
    {% endblock %}

:doc:`extends<tags/extends>` タグがここでのキーです。 extendsタグは、テンプレートエンジンに、
このテンプレートは、別のテンプレートを"extends (継承/拡張)" しているのだと伝えるものです。テンプレートシステムが、
このテンプレートを評価するときには、まず、親の場所を特定します。 extendsタグは、
テンプレートの最初のタグでなければならないというわけです。

ここでは、子テンプレートで、``footer`` ブロックを定義していないので、
親テンプレートの値が代わりに使用されているのにご注意ください。

``block`` タグを同じテンプレートの中で、同じ名前で複数定義することは、
できません。 blockタグは、「双方向」に動作するので、こういった制限があるのです。
つまり、blockタグは、埋めるべき穴を提供するだけでなく― 同時に、*親で* この穴を埋める
コンテンツを定義するものでもある、ということです。 仮に、同じ名前がつけられた、
2つの ``block`` タグが1つのテンプレートの中にあったとするなら、このテンプレートの親では、
どちらのブロックのコンテンツを使用すべきかわからないというわけです。

しかしながら、あるブロックを複数回表示したいときには、``block`` 関数を使うことが
できます:

.. code-block:: jinja

    <title>{% block title %}{% endblock %}</title>
    <h1>{{ block('title') }}</h1>
    {% block body %}{% endblock %}

親ブロック
------------

:doc:`parent<../functions/parent>` 関数を使えば、親ブロックの内容を
レンダリングすることもできます。 この関数により、親ブロックの処理結果が
返されます:

.. code-block:: jinja

    {% block sidebar %}
        <h3>目次</h3>
        ...
        {{ parent() }}
    {% endblock %}

名前付きのBlock閉じタグ
-----------------------

可読性を高めるため、Twigでは、閉じタグの後に、ブロックの名前を
書くこともできます:

.. code-block:: jinja

    {% block sidebar %}
        {% block inner_sidebar %}
            ...
        {% endblock inner_sidebar %}
    {% endblock sidebar %}

当然のことながら、``endblock`` の後の名前は、ブロックの名前と一致していなければなりません。

ブロックのネストとスコープ
--------------------------

ブロックは入れ子にして、さらに複雑なレイアウトにすることもできます。 デフォルトでは、ブロックは、
外のスコープの変数にアクセスすることもできます:

.. code-block:: jinja

    {% for item in seq %}
        <li>{% block loop_item %}{{ item }}{% endblock %}</li>
    {% endfor %}

ブロック・ショートカット
------------------------

内容が少ないブロックのために、ショートカットの構文を使用することができます。 次に挙げる構成は、
どちらも同じものです:

.. code-block:: jinja

    {% block title %}
        {{ page_title|title }}
    {% endblock %}

.. code-block:: jinja

    {% block title page_title|title %}

動的継承
------------

Twigでは、動的継承を利用することができますが、これは、変数をベースのテンプレートとして使用することで可能になります:

.. code-block:: jinja

    {% extends some_var %}

変数が ``Twig_Template`` オブジェクトとして評価できれば、Twigでは、それを親のテンプレートとして
使います::

    // {% extends layout %}

    $layout = $twig->loadTemplate('some_layout_template.twig');

    $twig->display('template.twig', array('layout' => $layout));

.. versionadded:: 1.2
    テンプレートの配列を渡すことができる機能は、Twig 1.2 で追加されました。

テンプレートのリストを渡すこともでき、渡されたテンプレートは、それぞれ存在するかチェックされて使用されます。 最初の
テンプレートが存在する場合、それが親として利用されます:

.. code-block:: jinja

    {% extends ['layout.html', 'base_layout.html'] %}

条件付き継承
------------

親テンプレートの名前には、有効などんな Twig の式でも使うこともできます。 これにより、
継承のメカニズムを条件付きにすることができます:

.. code-block:: jinja

    {% extends standalone ? "minimum.html" : "base.html" %}

この例では、``standalone`` 変数が ``true`` と評価される場合は、
このテンプレートは、"minimum.html" レイアウトテンプレートを継承し、さもなくば、"base.html"を
継承します。

.. seealso:: :doc:`block<../functions/block>`, :doc:`block<../tags/block>`, :doc:`parent<../functions/parent>`, :doc:`use<../tags/use>`
