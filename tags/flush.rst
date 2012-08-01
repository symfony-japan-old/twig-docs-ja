``flush``
=========

.. versionadded:: 1.5
    flushタグは、Twig 1.5 で追加されました。

``flush`` タグは、Twigに、出力バッファをフラッシュすることを伝えるためのものです:

.. code-block:: jinja

    {% flush %}

.. note::

    内部的には、Twigは、PHPの `flush`_ 関数を使用します。

.. _`flush`: http://php.net/flush
