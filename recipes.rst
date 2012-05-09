レシピ
=======

レイアウトの条件分岐を作る
---------------------------

Ajax と連携させることは同じコンテンツがときにそのまま表示されたり、レイアウトによってデコレートされることを意味します。Twig のレイアウトテンプレート名は任意の有効な式になるので、Ajax を通じてリクエストが行われるときに `true` に評価される式を渡し、それにしたがってレイアウトを選ぶことができます。

.. code-block:: jinja

    {% extends request.ajax ? "base_ajax.html" : "base.html" %}

    {% block content %}
        This is the content to be displayed.
    {% endblock %}

インクルードを動的に行う
-------------------------

テンプレートをインクルードするとき、名前は文字列である必要はありません。たとえば、名前は可変変数の値に依存することができます。

.. code-block:: jinja

    {% include var ~ '_foo.html' %}

``var`` は ``index`` に評価され、 ``index_foo.html`` テンプレートはレンダリングされます。

当然のことながら、テンプレートの名前は次のような任意の有効な式になります。

.. code-block:: jinja

    {% include var|default('index') ~ '_foo.html' %}

自分自身も継承するテンプレートをオーバーライドする
----------------------------------------------

テンプレートは2つの異なる方法でカスタマイズできます。

* *継承*: テンプレートは親テンプレートを *拡張し* ブロックをオーバーライドします;

* *置き換え*: ファイルシステムのローダーを使う場合、Twig は指定されたディレクトリのリストで見つかる最初のテンプレートをロードします;
  ディレクトリで見つかるテンプレートはさらにリストで見つかるディレクトリから 別のものに *置き換えます* 。

しかし両方を組み合わせる: 自分自身も拡張するテンプレートを *置き換える* にはどうしたらよいでしょうか？ (言い換えるとさらにリストで見つかるディレクトリのテンプレート)?

テンプレートは ``.../templates/mysite``
と ``.../templates/default`` の両方からこの順番でロードされるとします。 ``.../templates/default`` に保存される ``page.twig`` テンプレートは次のようになります。

.. code-block:: jinja

    {# page.twig #}
    {% extends "layout.twig" %}

    {% block content %}
    {% endblock %}

``.../templates/mysite`` において同じ名前のファイルを置くことでこのテンプレートを置き換えることができます。そしてオリジナルのテンプレートを拡張したいのであれば、次のように書きたいと思うかもしれません。

.. code-block:: jinja

    {# page.twig in .../templates/mysite #}
    {% extends "page.twig" %} {# from .../templates/default #}

もちろん、このコードは動きません。Twig は常に ``.../templates/mysite`` からテンプレートをロードするからです。

テンプレートディレクトリ、我々のケースではほかの親のすべてのディレクトリ: ``.../templates`` 、のすぐ後にディレクトリを追加することで、動かせることがすぐにわかります。 です。これによってシステムの範囲になるすべてのテンプレートファイルのアドレスを一意に指定できるようになる効果があります。大抵の場合、「通常の」パスを使うことになりますが、自分自身のバージョンをオーバーライドすることでテンプレートを拡張したい特別なケースの場合、extends タグの中で、親の完全で、完全ではないテンプレートパスを参照することができます。

.. code-block:: jinja

    {# page.twig in .../templates/mysite #}
    {% extends "default/page.twig" %} {# from .../templates #}

.. note::

    このレシピは Django の wiki ページにインスパイアされて書きました:
    http://code.djangoproject.com/wiki/ExtendingTemplates

構文をカスタマイズする
-----------------------

Twig はブロックの区切り文字の構文をカスタマイズすることを許可します。テンプレートがあなたのカスタム構文に結びつけられてしまうので、このフィーチャはおすすめしません。しかし特定のプロジェクトにおいて、デフォルトを変更するのに役立つことがあります。

ブロックの区切り文字を変更するために、レキサーオブジェクトをつくる必要があります。::

    $twig = new Twig_Environment();

    $lexer = new Twig_Lexer($twig, array(
        'tag_comment'  => array('{#', '#}'),
        'tag_block'    => array('{%', '%}'),
        'tag_variable' => array('{{', '}}'),
    ));
    $twig->setLexer($lexer);

ほかのテンプレートエンジンの構文をシミュレートするコンフィギュレーションのサンプルは次のとおりです。::

    // Ruby erb 構文
    $lexer = new Twig_Lexer($twig, array(
        'tag_comment'  => array('<%#', '%>'),
        'tag_block'    => array('<%', '%>'),
        'tag_variable' => array('<%=', '%>'),
    ));

    // SGML コメント構文
    $lexer = new Twig_Lexer($twig, array(
        'tag_comment'  => array('<!--#', '-->'),
        'tag_block'    => array('<!--', '-->'),
        'tag_variable' => array('${', '}'),
    ));

    // Smarty 形式
    $lexer = new Twig_Lexer($twig, array(
        'tag_comment'  => array('{*', '*}'),
        'tag_block'    => array('{', '}'),
        'tag_variable' => array('{$', '}'),
    ));

動的なオブジェクトプロパティを使う
-----------------------------------

Twig は ``article.title`` のような変数に遭遇すると、 `article` オブジェクトの中の `title` のパブリック変数を見つけようとします。

プロパティが存在しない場合でも  ``__get()`` マジックメソッドのおかげで、動的に定義されるので、これは機能します; 次のコードのスニペットで示される ``__isset()`` マジックメソッドを実装することだけが必要です。::

    class Article
    {
        public function __get($name)
        {
            if ('title' == $name) {
                return 'The title';
            }

            // 何らかのエラーを投げます
        }

        public function __isset($name)
        {
            if ('title' == $name) {
                return true;
            }

            return false;
        }
    }

入れ子ループの中で親のコンテキストにアクセスする
-------------------------------------------------

ときに、入れ子のループを使うとき、親のコンテキストにアクセスすることが必要になります。親のコンテキストは  ``loop.parent`` 変数を通じてアクセスできます。たとえば、次のテンプレートのデータがあるとします。::

    $data = array(
        'topics' => array(
            'topic1' => array('Message 1 of topic 1', 'Message 2 of topic 1'),
            'topic2' => array('Message 1 of topic 2', 'Message 2 of topic 2'),
        ),
    );

そして、すべてのトピックですべてのメッセージを表示するテンプレートは次のようになります。

.. code-block:: jinja

    {% for topic, messages in topics %}
        * {{ loop.index }}: {{ topic }}
      {% for message in messages %}
          - {{ loop.parent.loop.index }}.{{ loop.index }}: {{ message }}
      {% endfor %}
    {% endfor %}

出力は次のようになります。

.. code-block:: text

    * 1: topic1
      - 1.1: The message 1 of topic 1
      - 1.2: The message 2 of topic 1
    * 2: topic2
      - 2.1: The message 1 of topic 2
      - 2.2: The message 2 of topic 2

内側のループにおいて、 ``loop.parent`` 変数は外側のコンテキストにアクセスするために使われます。ですので、ループに対する外側で定義された現在の ``topic`` のインデックスは ``loop.parent.loop.index`` 変数を通じてアクセスできます。

未定義の関数とフィルタをその場で定義する
-----------------------------------------

関数 (もしくはフィルタ) が定義されていないとき、デフォルトでは Twig は ``Twig_Error_Syntax`` の例外を投げます。しかしながら、これは関数 (もしくはフィルタ) を返す `コールバック`_ (PHP の任意の有効な callable) も呼び出します。

フィルタに関しては、 ``registerUndefinedFilterCallback()`` でコールバックを登録します。
関数に関して、 ``registerUndefinedFunctionCallback()`` を使います。::

    // Twig 関数として PHP ネイティブの関数をすべて自動的に登録します。
    // まったくセキュアではないので手元で試さないでください！
    $twig->registerUndefinedFunctionCallback(function ($name) {
        if (function_exists($name)) {
            return new Twig_Function_Function($name);
        }

        return false;
    });

callable が有効な関数 (もしくはフィルタ) を返すことができなければ、 ``false`` を返さなければなりません。

複数のコールバックを登録すると、 ``false`` を返すものがあらわれるまで、それらを順番に呼び出します。

.. tip::

    関数とフィルタの解決はコンパイルのあいだに行われるので、
    これらのコールバックを登録するときにオーバーヘッドはありません。

テンプレート構文の妥当性を検証する
-----------------------------------

テンプレートのコードがサードパーティによって提供される場合 (たとえば Web　インターフェイス)、それを保存する前にテンプレート構文の妥当性を検証するとおもしろいかもしれません。テンプレートのコードが `$template` 変数に保存される場合、次のように書くことができます。::

    try {
        $twig->parse($twig->tokenize($template));

        // $template が妥当である
    } catch (Twig_Error_Syntax $e) {
        // $template に構文エラーが含まれる
    }

ファイルのセットをイテレートする場合、例外メッセージの中でファイルの名前を得るために
``tokenize()`` メソッドにファイルの名前を渡すことができます。::

    foreach ($files as $file) {
        try {
            $twig->parse($twig->tokenize($template, $file));

            // $template が妥当である
        } catch (Twig_Error_Syntax $e) {
            // $template に構文エラーが含まれる
        }
    }

.. note::

    このメソッドはサンドボックスポリシーの違反をキャッチしません。
    ポリシーが強制されるのはテンプレートレンダリングの合間だからです (オブジェクトの許可されたメソッドのようなチェックのために Twig はコンテキストを必要とするからです).

APC が有効で apc.stat = 0 のときに修正済みのテンプレートをリフレッシュする
---------------------------------------------------------------------------

``apc.stat`` に ``0`` の値がセットされており Twig キャッシュが有効な場合、テンプレートキャッシュをクリアしても APC キャッシュが更新されません。これを改善するには、 ``Twig_Environment`` を拡張して、Twig がキャッシュを書き換えるときに APC キャッシュの更新を強制します。::

    class Twig_Environment_APC extends Twig_Environment
    {
        protected function writeCacheFile($file, $content)
        {
            parent::writeCacheFile($file, $content);

            // キャッシュ済みのファイルをバイトコードキャッシュにコンパイルします
            apc_compile_file($file);
        }
    }

ステートフルなノード Visitor を再利用する
------------------------------------------

``Twig_Environment`` インスタンスに Visitor をアタッチするとき、Twig は コンパイルする *すべての* テンプレートに訪問するためにこれを使います。なんらかの状態の情報を保つ必要があれば、新しいテンプレートに訪問するときに、それをリセットするとよいでしょう。

これは次のコードによってかんたんに実現できます。::

    protected $someTemplateState = array();

    public function enterNode(Twig_NodeInterface $node, Twig_Environment $env)
    {
        if ($node instanceof Twig_Node_Module) {
            // 新しいテンプレートに入るので状態をリセットします
            $this->someTemplateState = array();
        }

        // ...

        return $node;
    }

デフォルトのエスケーピングストラテジーをセットすることでテンプレートの名前を使う
----------------------------------------------------------------------------------

.. versionadded:: 1.8
    このレシピは Twig 1.8 およびそれ以降を必要とします。

``autoescape`` オプションはエスケーピングが変数に適用されていない場合にデフォルトのエスケーピングストラテジーを決めます。Twig がおもに HTML ファイルを生成するために使われるとき、これに ``html`` をセットしておいて、``autoescape`` タグのおかげで動的な JavaScript がある場合に ``js`` に明示的に変更することができます。

.. code-block:: jinja

    {% autoescape js %}
        ... some JS ...
    {% endautoescape %}

しかし HTML と JS ファイルがたくさんある場合、そしてテンプレートの名前が何らかの慣習にしたがう場合、テンプレートの名前絵をもとに使うデフォルトエスケーピングストラテジーを決めることができます。テンプレートの名前は HTML ファイルの場合 ``.html`` で JavaScript の場合は ``.js`` で終わるとすると、Twig の設定方法は次のようになります。::

    function twig_escaping_guesser($filename)
    {
        // フォーマットの情報を得ます。
        $format = substr($filename, strrpos($filename, '.') + 1);

        switch ($format) {
            'js':
                return 'js';
            default:
                return 'html';
        }
    }

    $loader = new Twig_Loader_Filesystem('/path/to/templates');
    $twig = new Twig_Environment($loader, array(
        'autoescape' => 'twig_escaping_guesser',
    ));

オートエスケーピングはコンパイル時に行われるので、この動的なストラテジーは実行時にはオーバーヘッドはかかりません。

.. _`コールバック`: http://www.php.net/manual/function.is-callable.php
