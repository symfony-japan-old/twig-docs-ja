``macro``
=========

マクロは、通常のプログラム言語の関数と比較対比されるものです。 マクロは、
頻繁に使われるHTMLのイディオムを再利用可能な要素として配置するために使うことができ、これにより、
繰り返しの記述を避けることができます。

次は、マクロの簡単な例で、form 要素をレンダリングする例になります:

.. code-block:: jinja

    {% macro input(name, value, type, size) %}
        <input type="{{ type|default('text') }}" name="{{ name }}" value="{{ value|e }}" size="{{ size|default(20) }}" />
    {% endmacro %}

マクロは、PHPのネイティブの関数とは、何点かの違いがあります:

* 引数のデフォルト値は、マクロの本文で ``default`` フィルタを使用することにより
  定義します;

* マクロの引数は、常に、オプション引数(省略できる引数)になります。

一方で、PHPの関数と同じく、マクロは、現在のテンプレートの変数には、
アクセスできません。

.. tip::

    現在のコンテキスト全体を渡すことができ、これには、特殊な
    ``_context`` 変数を用います。

マクロは、どのテンプレートでも定義できます。使う前には、マクロを "インポート(import)する"
必要があります (詳しくは、:doc:`import<../tags/import>` タグのドキュメントを
ご覧ください):

.. code-block:: jinja

    {% import "forms.html" as forms %}

上の ``import`` の呼び出しにより、"forms.html" ファイル (マクロのみか、テンプレートと
マクロのみの内容が可能) がインポートされ、
``forms`` 変数の要素として、マクロの関数がインポートされます。

その後は、使いたいときにマクロを呼び出せます:

.. code-block:: jinja

    <p>{{ forms.input('username') }}</p>
    <p>{{ forms.input('password', null, 'password') }}</p>

同じテンプレートの中に定義されていているマクロを使う場合は、インポートせず、
特殊な ``_self`` 変数を使うことができます:

.. code-block:: jinja

    <p>{{ _self.input('username') }}</p>

マクロの中から同じファイルの別のマクロを使用したいときにも、この ``_self``
変数を使います:

.. code-block:: jinja

    {% macro input(name, value, type, size) %}
      <input type="{{ type|default('text') }}" name="{{ name }}" value="{{ value|e }}" size="{{ size|default(20) }}" />
    {% endmacro %}

    {% macro wrapped_input(name, value, type, size) %}
        <div class="field">
            {{ _self.input(name, value, type, size) }}
        </div>
    {% endmacro %}

マクロが別のファイルに定義されている時は、それをインポートする必要があります:

.. code-block:: jinja

    {# forms.html #}

    {% macro input(name, value, type, size) %}
      <input type="{{ type|default('text') }}" name="{{ name }}" value="{{ value|e }}" size="{{ size|default(20) }}" />
    {% endmacro %}

    {# shortcuts.html #}

    {% macro wrapped_input(name, value, type, size) %}
        {% import "forms.html" as forms %}
        <div class="field">
            {{ forms.input(name, value, type, size) }}
        </div>
    {% endmacro %}

.. seealso:: :doc:`from<../tags/from>`, :doc:`import<../tags/import>`

.. 2012/08/08 goohib 8d00b42e569f469e4e0934f87f82111560da8ac3
