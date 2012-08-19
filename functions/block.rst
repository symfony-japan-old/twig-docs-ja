``block``
=========

テンプレートで継承を利用しており、ブロックを複数回出力するときは
``block`` 関数を使います:

.. code-block:: jinja

    <title>{% block title %}{% endblock %}</title>

    <h1>{{ block('title') }}</h1>

    {% block body %}{% endblock %}

.. seealso:: :doc:`extends<../tags/extends>`, :doc:`parent<../functions/parent>`

.. 2012/08/20 goohib fc016bd281690879a0c61516de4310e885ec9472
