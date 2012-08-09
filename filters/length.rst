``length``
==========

``length`` フィルタは、シーケンスまたはマッピングの要素の数、あるいは、
文字列の長さを返します:

.. code-block:: jinja

    {% if users|length > 10 %}
        ...
    {% endif %}

.. 2012/08/09 goohib b096e21daa6647cd23063c3a4e4280ad81df8f84
