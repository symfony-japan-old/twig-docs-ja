Twig の内部
==============

Twig はとても拡張性があり、かんたんにハックできます。コアをハックする前にエクステンションをつくることを念頭に置くべきでしょう。たいていのフィーチャと強化はエクステンションによって実現できるからです。この章は Twig の内部がどのように動くのか理解したい人にも役立ちます。

Twig はどのように動くのか？
----------------------------

Twig テンプレートのレンダリングは 4 つのキーステップに要約できますs:

 * テンプレートを **ロードします**: テンプレートがすでにコンパイル済みである場合、これをロードして*評価*ステップに向かいます。そうでなければ:

   * 最初に、**レキサー**はテンプレートコードをより簡単に処理できる小さなピースにトークン化します;

   * それから、**パーサー**はトークンストリームをノードの意味あるツリーに変換します (Abstract Syntax Tree);

   * 最後に、*コンパイラー*は AST を PHP コードに変換します;

 * テンプレートを**評価します**: このことは基本的にコンパイル済みテンプレートの `display()` メソッドを呼び出しこれにコンテキストを渡すことを意味します。

レキサー
----------

レキサーはテンプレートのソースコードをトークンのストリームにトークン化します (それぞれのトークンは ``Twig_Token`` のインスタンスであり、ストリームは ``Twig_TokenStream`` のインスタンスです)。デフォルトのレキサーは13のトークンのタイプを認識します。

* ``Twig_Token::BLOCK_START_TYPE``, ``Twig_Token::BLOCK_END_TYPE``: ブロックのデリミッタ (``{% %}``)
* ``Twig_Token::VAR_START_TYPE``, ``Twig_Token::VAR_END_TYPE``: 変数のデリミッタ (``{{ }}``)
* ``Twig_Token::TEXT_TYPE``: 式の外のテキスト;
* ``Twig_Token::NAME_TYPE``: 式の中の名前;
* ``Twig_Token::NUMBER_TYPE``: 式の中の数値;
* ``Twig_Token::STRING_TYPE``: 式の中の文字列;
* ``Twig_Token::OPERATOR_TYPE``: 演算子;
* ``Twig_Token::PUNCTUATION_TYPE``: 約物;
* ``Twig_Token::INTERPOLATION_START_TYPE``, ``Twig_Token::INTERPOLATION_END_TYPE`` (Twig 1.5 以降): 文字列補完のデリミッタ;
* ``Twig_Token::EOF_TYPE``: テンプレートの末端


環境の ``tokenize()`` を呼び出すことで手動でソースコードをトークンストリームに変換することができます。 ::

    $stream = $twig->tokenize($source, $identifier);

ストリームには ``__toString()`` メソッドが用意されており、echo によるオブジェクトのテキスト表現を表示することができます。::

    echo $stream."\n";

``Hello {{ name }}`` テンプレートの出力は次のようになります。

.. code-block:: text

    TEXT_TYPE(Hello )
    VAR_START_TYPE()
    NAME_TYPE(name)
    VAR_END_TYPE()
    EOF_TYPE()

.. note::

    ``setLexer()`` メソッドを呼び出すことで Twig (``Twig_Lexer``) のデフォルトのレキサーを変更できます。::

        $twig->setLexer($lexer);

パーサー
----------

パーサーはトークンのストリームを AST (Abstract Syntax Tree)、もしくはノードツリー (``Twig_Node_Module`` のインスタンス) に変換します。コアエクステンションは ``for`` 、 ``if`` のような基本ノードと式ノードを定義します。

環境の ``parse()`` メソッドを呼び出すことでトークンストリームをノードツリーに手動で変換できます。::

    $nodes = $twig->parse($stream);

ノードオブジェクトを echo するとツリーのすばらしい表現が得られます。::

    echo $nodes."\n";

Here is the output for the ``Hello {{ name }}`` template:

.. code-block:: text

    Twig_Node_Module(
      Twig_Node_Text(Hello )
      Twig_Node_Print(
        Twig_Node_Expression_Name(name)
      )
    )

.. note::

    デフォルトのパーサー (``Twig_TokenParser``) は
    ``setParser()`` メソッドを呼び出すことでも変更できます。method::

        $twig->setParser($parser);

コンパイラ
------------

最後のステップはコンパイラによって行われます。これはノードツリーを入力としてとり、テンプレートの実行時に利用する PHP コードを生成します。

環境の ``compile()`` メソッドによって手動でコンパイラを呼び出すことができます。::

    $php = $twig->compile($nodes);

``compile()`` メソッドはノードをあらわす PHP ソースコードを返します。

``Hello {{ name }}`` テンプレートに対して生成されたテンプレートは次のようになります
(実際の出力は Twig のバージョンによって異なる場合があります)::

    /* Hello {{ name }} */
    class __TwigTemplate_1121b6f109fe93ebe8c6e22e3712bceb extends Twig_Template
    {
        protected function doDisplay(array $context, array $blocks = array())
        {
            // line 1
            echo "Hello ";
            echo twig_escape_filter($this->env, $this->getContext($context, "name"), "ndex", null, true);
        }

        // some more code
    }

.. note::

    レキサーとパーサーに関して、デフォルトのコンパイラ (``Twig_Compiler``)
    は ``setCompiler()`` メソッドを呼び出すことで変更できます。::

        $twig->setCompiler($compiler);
