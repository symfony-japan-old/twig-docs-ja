``dump``
========

.. versionadded:: 1.5
    dump 関数は、Twig 1.5 で追加されました。

``dump`` 関数は、テンプレート変数についての情報をダンプします。 これは、テンプレートが
期待した振る舞いにならないときに、その変数の中身を見てみることで、
テンプレートをデバッグするのに主に役立ちます:

.. code-block:: jinja

    {{ dump(user) }}

.. note::

    ``dump`` 関数は、デフォルトでは利用できません。 Twig環境を生成する際に、
    ``Twig_Extension_Debug`` エクステンションを明示的に追加する
    必要があります::

        $twig = new Twig_Environment($loader, array(
            'debug' => true,
            // ...
        ));
        $twig->addExtension(new Twig_Extension_Debug());

    エクステンションが有効になっていたとしても、環境の ``debug`` オプションが
    有効になっていなければ、``dump`` 関数は、何も表示しません
    (プロダクションサーバーでデバッグ情報が
    漏れてしまうのを防ぐためです)。

HTMLのコンテキストでは、読みやすくするために、出力を
``pre`` タグで囲みます:

.. code-block:: jinja

    <pre>
        {{ dump(user) }}
    </pre>

.. tip::

    `XDebug`_ が有効で、``html_errors`` が ``on`` になっているときは、
    ``pre`` タグの使用は不要です; XDebugが有効な場合は、さらに、
    出力がより見やすいものにもなります。

複数の変数をデバッグすることもでき、それには、追加の引数でそれらを指定します:

.. code-block:: jinja

    {{ dump(user, categories) }}

何も渡さないときは、現在のコンテキストのすべての変数が
ダンプされます:

.. code-block:: jinja

    {{ dump() }}

.. note::

    内部的には、Twigは、PHPの `var_dump`_ 関数を使います。

.. _`XDebug`:   http://xdebug.org/docs/display
.. _`var_dump`: http://php.net/var_dump

.. 2012/08/20 goohib 4cd98e62d052a77375adee3e287cfe11857dc996
