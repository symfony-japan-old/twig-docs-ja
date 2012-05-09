イントロダクション
===================

これは柔軟で、速く、セキュアな PHP 言語のテンプレートである Twig のドキュメントです。

Smarty、Django もしくは Jinja などのほかのテキストベースのテンプレート言語に触れる機会があれば、Twig の扱いにすぐ慣れるでしょう。PHP の原則を忠実に守りテンプレート環境に役立つ機能性を追加することでこれはデザイナーと開発者の両方に親しみやすいものになっています。

キーフィーチャは次のとおりです...

 * *速い*: Twig はテンプレートをプレーンな最適化されたプレーンな PHP コードにコンパイルします。PHP コードと比べたオーバーヘッドは最小限に減りました。

 * *安全である*: Twig は信頼できないテンプレートコードを評価するサンドボックスモードを持ちます。このことによってユーザーがテンプレートデザインを修正することが許可されるアプリケーションのテンプレート言語で使えるようになっています。

 * *柔軟である*: Twig は柔軟なレクサーとパーサーによって支えられています。これによって開発者は独自のカスタムタグとフィルターを定義し、また独自の DSL を作ることができます。

前提要件
---------

Twig を実行するには少なくとも **PHP 5.2.4** が必要です。

インストール方法
------------------

Twig をインストールする方法は複数あります。何をやっているのかわからなければ、tarball のセクションをご覧ください。

tarball リリースからインストールする
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. `ダウンロードページ`_ から最新の tarball をダウンロードします
2. tarball を展開します
3. ファイルをプロジェクトのどこかに移動させます

開発バージョンをインストールする
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Subversion もしくは Git をインストールします。
2. Git の場合: ``git clone git://github.com/fabpot/Twig.git``
3. Subversion の場合: ``svn co http://svn.twig-project.org/trunk/ twig``

PEAR パッケージをインストールする
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. PEAR をインストールします
2. ``pear channel-discover pear.twig-project.org``
3. ``pear install twig/Twig`` (or ``pear install twig/Twig-beta``)

Composer 経由でインストールする
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Composer をプロジェクトにインストールします。

.. code-block:: bash

    curl -s http://getcomposer.org/installer | php

2. プロジェクトのルートで ``composer.json`` ファイルを作ります。

.. code-block:: javascript

    {
        "require": {
            "twig/twig": "1.6.0"
        }
    }

3. composer 経由でインストールします。

.. code-block:: bash

    php composer.phar install

C エクステンションのインストール方法
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. versionadded:: 1.4
    C エクステンションは Twig 1.4 で追加されました。

Twig には C エクステンションが用意されており、Twig 実行エンジンのパフォーマンスを強化してくれます。ほかの PHP エクステンションのようにインストールできます。

.. code-block:: bash

    $ cd ext/twig
    $ phpize
    $ ./configure
    $ make
    $ make install

最後に、 ``php.ini`` 設定ファイルでエクステンションを有効にします。

.. code-block:: ini

    extension=twig.so

これで、Twig は C エクステンションを使うようにあなたのテンプレートを自動的にコンパイルしてくれます。特筆することは PHP のコードを置き換えませんが、
``Twig_Template::getAttribute()`` メソッドの最適化されたバージョンだけを提供してくれます。

.. tip::

    Windowsにおいては、 `プレビルド DLL`_ をダウンロードしてインストールすることもできます。

API の基本的な使い方
---------------------

このセクションでは Twig の PHP API を手短に紹介します。

Twig を使う最初のステップはオートローダを登録することです。::

    require_once '/path/to/lib/Twig/Autoloader.php';
    Twig_Autoloader::register();

``/path/to/lib/`` パスを Twig がインストールされているパスに置き換えます。

.. note::

    Twig のクラス名は PEAR の慣習にしたがいます。
    このことは Twig のクラスのロードを独自のオートローダに統合することがかんたんであることを意味します。

.. code-block:: php

    $loader = new Twig_Loader_String();
    $twig = new Twig_Environment($loader);

    echo $twig->render('Hello {{ name }}!', array('name' => 'Fabien'));

Twig はテンプレートを割り出すのにローダー (``Twig_Loader_String``) を使い、コンフィギュレーションを保存するのに環境 (``Twig_Environment``) を使います。

``render()`` メソッドは第1引数として渡されたテンプレートをロードし、第2引数として渡された変数でそれをレンダリングします。

一般にテンプレートはファイルシステムに保存されるので、Twig にはファイルシステムのローダーが備わっています。::

    $loader = new Twig_Loader_Filesystem('/path/to/templates');
    $twig = new Twig_Environment($loader, array(
        'cache' => '/path/to/compilation_cache',
    ));

    echo $twig->render('index.html', array('name' => 'Fabien'));

.. _`ダウンロードページ`: https://github.com/fabpot/Twig/tags
.. _`プレビルド DLL`: https://github.com/stealth35/stealth35.github.com/downloads
