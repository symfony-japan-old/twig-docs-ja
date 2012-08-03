``raw``
=======

``raw`` タグは、領域をパースされるべきでない生のテキストとしてマークします。
例えば、Twig の構文を、例としてテンプレートに記述する場合には、下記のスニペット
が使えます:

.. code-block:: jinja

    {% raw %}
        <ul>
        {% for item in seq %}
            <li>{{ item }}</li>
        {% endfor %}
        </ul>
    {% endraw %}
