``striptags``
=============

``striptags`` フィルタは、 SGML/XML タグを除去し、タグと隣接する空白文字を
スペース一つに置換します:

.. code-block:: jinja

    {% some_html|striptags %}

.. note::

    内部的には、Twig は、PHPの `strip_tags`_ 関数を使います。

.. _`strip_tags`: http://php.net/strip_tags

.. 2012/08/09 goohib 22ef32e5eb2e04d860daa025c5303d4ef8bbfdc7
