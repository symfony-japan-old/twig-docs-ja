``sandbox``
===========

``sandbox`` タグを使えば、インクルードしたテンプレートでサンドボックスモードが有効になります。
Twig の環境で、サンドボックス化がグローバルに有効化されていない場合に、これが利用できます:

.. code-block:: jinja

    {% sandbox %}
        {% include 'user.html' %}
    {% endsandbox %}

.. warning::

    ``sandbox`` タグは、sandbox エクステンションが有効になっているときのみ
    使用できます (:doc:`開発者のための Twig<../api>` の章をご覧ください)。

.. note::

    ``sandbox`` タグは、includeタグをサンドボックス化するときにのみ使用でき、
    テンプレートのどこかの領域をサンドボックス化するためには、使用できません。 次の例は、
    動作しない例です:

    .. code-block:: jinja

        {% sandbox %}
            {% for i in 1..2 %}
                {{ i }}
            {% endfor %}
        {% endsandbox %}

.. 2012/08/08 goohib 81807ea95b3a733ec237f1fcae9f944bfaadbdab
