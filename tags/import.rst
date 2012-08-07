``import``
==========

Twigでは、頻繁に使うコードを :doc:`macros<../tags/macro>` の中に配置することができます。 これらの
マクロは、異なるテンプレートに記述しておき、そこからインポートすることができます。

テンプレートをインポートする方法は2つあります。 まず、変数の中にテンプレートを全部インポートする方法、それから、
その中にあるマクロを指定して持ってくる方法です。

フォームを描画するヘルパーモジュールがあると考えてみてください (これは ``forms.html`` という名前になっています):

.. code-block:: jinja

    {% macro input(name, value, type, size) %}
        <input type="{{ type|default('text') }}" name="{{ name }}" value="{{ value|e }}" size="{{ size|default(20) }}" />
    {% endmacro %}

    {% macro textarea(name, value, rows) %}
        <textarea name="{{ name }}" rows="{{ rows|default(10) }}" cols="{{ cols|default(40) }}">{{ value|e }}</textarea>
    {% endmacro %}

もっとも簡単で柔軟なのは、変数の中に、モジュール全体をインポートすることです。
そのようにした場合、マクロを使うときには、その変数の属性にアクセスして利用できます:

.. code-block:: jinja

    {% import 'forms.html' as forms %}

    <dl>
        <dt>ユーザー名</dt>
        <dd>{{ forms.input('username') }}</dd>
        <dt>パスワード</dt>
        <dd>{{ forms.input('password', null, 'password') }}</dd>
    </dl>
    <p>{{ forms.textarea('comment') }}</p>

別の方法としては、テンプレートから名前を現在の名前空間に
インポートする方法があります:

.. code-block:: jinja

    {% from 'forms.html' import input as input_field, textarea %}

    <dl>
        <dt>ユーザー名</dt>
        <dd>{{ input_field('username') }}</dd>
        <dt>パスワード</dt>
        <dd>{{ input_field('password', '', 'password') }}</dd>
    </dl>
    <p>{{ textarea('comment') }}</p>

マクロとテンプレートが同じファイルの中に定義されている場合は、インポートは不要です。
そのかわり、特殊な ``_self`` 変数を使います:

.. code-block:: jinja

    {# index.html template #}

    {% macro textarea(name, value, rows) %}
        <textarea name="{{ name }}" rows="{{ rows|default(10) }}" cols="{{ cols|default(40) }}">{{ value|e }}</textarea>
    {% endmacro %}

    <p>{{ _self.textarea('comment') }}</p>

しかし、``_self`` 変数を使ってインポートすることにより、別名を作成することが、やはり可能です:

.. code-block:: jinja

    {# index.html template #}

    {% macro textarea(name, value, rows) %}
        <textarea name="{{ name }}" rows="{{ rows|default(10) }}" cols="{{ cols|default(40) }}">{{ value|e }}</textarea>
    {% endmacro %}

    {% import _self as forms %}

    <p>{{ forms.textarea('comment') }}</p>

.. seealso:: :doc:`macro<../tags/macro>`, :doc:`from<../tags/from>`

-- 2012/08/08 goohib ace74cc6a014b7004d3832e607342db84290dc7a
