``cycle``
=========

``cycle`` 関数は、配列の値を循環させます:

.. code-block:: jinja

    {% for i in 0..10 %}
        {{ cycle(['odd', 'even'], i) }}
    {% endfor %}

配列には、値がいくつ含まれていても構いません:

.. code-block:: jinja

    {% set fruits = ['apple', 'orange', 'citrus'] %}

    {% for i in 0..10 %}
        {{ cycle(fruits, i) }}
    {% endfor %}

.. 2012/08/20 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
