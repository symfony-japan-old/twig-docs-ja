``json_encode``
===============

``json_encode`` フィルタは、文字列の JSON 表現を返します:

.. code-block:: jinja

    {{ data|json_encode() }}

.. note::

    内部的には、Twigは、PHPの `json_encode`_ 関数を使います。

.. _`json_encode`: http://php.net/json_encode

.. 2012/08/09 goohib 22ef32e5eb2e04d860daa025c5303d4ef8bbfdc7
