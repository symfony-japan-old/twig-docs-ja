``if``
======

Twigの ``if`` ステートメントは、PHPのifステートメントと互換性があります。

ifを利用するための最も単純な形は、式が ``true`` と評価されるかどうか検査する
ために使うというものです:

.. code-block:: jinja

    {% if online == false %}
        <p>Webサイトは、メンテナンスモードになっています。後ほどお越しください。</p>
    {% endif %}

配列が空でないか検査することもできます:

.. code-block:: jinja

    {% if users %}
        <ul>
            {% for user in users %}
                <li>{{ user.username|e }}</li>
            {% endfor %}
        </ul>
    {% endif %}

.. note::

    変数が定義されているかどうか検査したい場合は、``if users is
    defined`` を代わりに使うことができます。

複数の分岐には、``elseif`` と ``else`` がPHPと同様に利用できます。 ここでは、他と同様に、もっと複雑な ``式`` を
使うこともできます:

.. code-block:: jinja

    {% if kenny.sick %}
        ケニーは病気です。
    {% elseif kenny.dead %}
        ケニーを殺してしまいました！ なんてこった!!!
    {% else %}
        ケニーは、元気なようです --- いまのところは
    {% endif %}
