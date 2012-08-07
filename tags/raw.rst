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

-- 2012/08/08 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
