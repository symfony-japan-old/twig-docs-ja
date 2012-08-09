``url_encode``
==============

``url_encode`` フィルタは、与えられた文字を URLエンコードします:

.. code-block:: jinja

    {{ data|url_encode() }}

.. note::

    内部的には、Twig は、PHPの `urlencode`_ 関数を使います。

.. _`urlencode`: http://php.net/urlencode

.. 2012/08/09 goohib 22ef32e5eb2e04d860daa025c5303d4ef8bbfdc7
