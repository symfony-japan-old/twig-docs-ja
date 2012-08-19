``constant``
============

``constant`` は、指定した文字列に対応する定数値を返します:

.. code-block:: jinja

    {{ some_date|date(constant('DATE_W3C')) }}
    {{ constant('Namespace\\Classname::CONSTANT_NAME') }}

.. 2012/08/20 goohib cf03a65e8b13d8b4c492e92bb1c13df350920b3c
