``use``
=======

.. versionadded:: 1.1
    水平方向の再利用(horizontal reuse) は、Twig 1.1で追加されました。

.. note::

    水平方向の再利用は、Twigの高度な機能で、通常のテンプレートで必要とされることは
    ほとんどありません。 この機能は、テンプレートブロックを継承を使わずに再利用可能にする必要がある
    プロジェクトで、主に使われるものです。

テンプレートの継承は、Twig のもっとも強力な機能の1つですが、これは、
単一継承に制限されています。テンプレートは、ほかの1つのテンプレートのみ継承できます。
この制限によって、テンプレートの継承は、簡単に理解でき、かつ、
デバッグしやすくもなるのです:

.. code-block:: jinja

    {% extends "base.html" %}

    {% block title %}{% endblock %}
    {% block content %}{% endblock %}

水平方向の再利用は、多重継承が目指すものと同じものを実現する方法ですが、
多重継承にともなう複雑さはありません:

.. code-block:: jinja

    {% extends "base.html" %}

    {% use "blocks.html" %}

    {% block title %}{% endblock %}
    {% block content %}{% endblock %}

``use`` ステートメントは、```blocks.html`` の中で定義されたブロックを
現在のテンプレートにインポートするよう Twig に指示します (マクロと同様ですが、これは、ブロックをインポートするためのものです):

.. code-block:: jinja

    # blocks.html
    {% block sidebar %}{% endblock %}

この例では、``use`` ステートメントにより、``sidebar`` ブロックがメインのテンプレートに
インポートされます。 このコードは、次のコードとほぼ同じものです (インポートされた
ブロックは自動的には出力されません):

.. code-block:: jinja

    {% extends "base.html" %}

    {% block sidebar %}{% endblock %}
    {% block title %}{% endblock %}
    {% block content %}{% endblock %}

.. note::

    ``use`` タグについては、対象のテンプレートが別のテンプレートを継承していない場合、マクロを定義していない場合、
    本体(body)が空である場合をとってみれば、ただテンプレートをインポートするだけのタグということになります。 しかし、そうでない場合は、これは、
    別のテンプレートを *使う（use）* ことができるものといえます。

.. note::

    ``use`` ステートメントは、テンプレートに渡されたコンテキストに依らずに
    解決されるので、テンプレートへの参照を式にすることはできません。

メインのテンプレートでは、インポートしたブロックをオーバーライドすることもできます。 テンプレートで、
``sidebar`` ブロックが既に定義されているなら、``blocks.html`` の中で定義されているものは、
無視されます。 名前の衝突を回避するために、インポートされたブロックをリネームすることができます:

.. code-block:: jinja

    {% extends "base.html" %}

    {% use "blocks.html" with sidebar as base_sidebar %}

    {% block sidebar %}{% endblock %}
    {% block title %}{% endblock %}
    {% block content %}{% endblock %}

.. versionadded:: 1.3
    ``parent()`` は、Twig 1.3 で利用できるようになりました。

``parent()`` 関数は、自動で正しい継承ツリーを決定するので、
この関数は、インポートしたテンプレートで定義されているブロックをオーバーライドしたときに
使うことができます:

.. code-block:: jinja

    {% extends "base.html" %}

    {% use "blocks.html" %}

    {% block sidebar %}
        {{ parent() }}
    {% endblock %}

    {% block title %}{% endblock %}
    {% block content %}{% endblock %}

上の例では、``parent()`` で、 ``blocks.html`` テンプレート
の中の ``sidebar`` ブロックが正しく呼び出されます。

.. tip::

    Twig 1.2では、リネームにより、"親" ブロックの呼び出しをすることで、
    継承のシミュレーションが可能です:

    .. code-block:: jinja

        {% extends "base.html" %}

        {% use "blocks.html" with sidebar as parent_sidebar %}

        {% block sidebar %}
            {{ block('parent_sidebar') }}
        {% endblock %}

.. note::

    どんなテンプレートであっても、何度でも ``use`` ステートメントを使うことができます。
    インポートした2つのテンプレートで、同じブロックが定義されている場合は、最後のものが有効になります。

-- 2012/08/08 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
