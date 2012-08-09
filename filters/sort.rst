``sort``
========

``sort`` フィルタは、配列を並べ替えます:

.. code-block:: jinja

    {% for use in users|sort %}
        ...
    {% endfor %}

.. note::

    内部的には、Twig は、インデックスとの関連を維持するために、
    PHPの `asort`_ 関数を使います。

.. _`asort`: http://php.net/asort

.. 2012/08/09 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
