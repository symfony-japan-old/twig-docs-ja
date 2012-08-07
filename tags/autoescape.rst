``autoescape``
==============

自動エスケープが有効か否かにかかわらず、テンプレートの領域をマークして、
その領域をエスケープする、あるいはエスケープしないようにできます。これには、``autoescape`` タグを使用します:

.. code-block:: jinja

    {# 次の構文は、Twig 1.8 から動作します -- 過去のバージョンの場合は、下記のnoteをご覧ください #}

    {% autoescape %}
        このブロックでは、どんなものも自動でエスケープされます。
        エスケープには、HTMLストラテジ（エスケープの方法）が使用されます。
    {% endautoescape %}

    {% autoescape 'html' %}
        このブロックでは、どんなものも自動でエスケープされます。
        エスケープには、HTMLストラテジが使用されます。
    {% endautoescape %}

    {% autoescape 'js' %}
        このブロックでは、どんなものも自動でエスケープされます。
        エスケープには、js エスケープ・ストラテジが使用されます。
    {% endautoescape %}

    {% autoescape false %}
        このブロックでは、何でもそのまま出力されます。
    {% endautoescape %}

.. note::

    Twig 1.8 より前では、構文が異なります:

    .. code-block:: jinja

        {% autoescape true %}
            このブロックでは、どんなものも自動でエスケープされます。
            エスケープには、HTMLストラテジが使用されます。
        {% endautoescape %}

        {% autoescape false %}
            このブロックでは、何でもそのまま出力されます。
        {% endautoescape %}

        {% autoescape true js %}
            このブロックでは、どんなものも自動でエスケープされます。
            エスケープには、js エスケープ・ストラテジが使用されます。
        {% endautoescape %}

自動エスケープが有効な場合は、デフォルトですべてエスケープされます。ただし、例外として、
安全であると明示的にマークされたものは除きます。テンプレートで、:doc:`raw<../filters/raw>` フィルタを使って、
その安全な部分をマークすることができます:

.. code-block:: jinja

    {% autoescape %}
        {{ safe_value|raw }}
    {% endautoescape %}

テンプレートのデータを返す関数 (:doc:`macros<macro>` や
:doc:`parent<../functions/parent>` のような関数) は、常に安全なマークアップを返します。

.. note::

    :doc:`escape<../filters/escape>` フィルタで既にエスケープされた値については、
    Twigでうまく判断されるので、さらにエスケープされることはありません。

.. note::

    :doc:`開発者のためのTwig<../api>` の章では、自動エスケープが適用される仕組みについて、
    さらに詳しい情報をご覧いただけます。

.. 2012/08/08 goohib 75d97b4a275b90956df554fd7d8d7bc6e3d4ae73
