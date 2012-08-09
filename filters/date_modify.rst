``date_modify``
===============

.. versionadded:: 1.9.0
    date_modify フィルタは、Twig 1.9.0 より追加されています。

``date_modify`` フィルタは、指定された修飾子文字列で日付を変更します:

.. code-block:: jinja

    {{ post.published_at|date_modify("+1 day")|date("m/d/Y") }}

``date_modify`` フィルタが受け取れるものは、文字列 (`strtotime`_ 関数でサポートされている書式
でなければなりません)、または、`DateTime`_ インスタンスです。 フォーマットには、`date`_
フィルタを簡単に組わせて使えます。

.. _`strtotime`:    http://www.php.net/strtotime
.. _`DateTime`:     http://www.php.net/DateTime

.. 2012/08/09 goohib 7657c01e65695a9a53cf63e0d8e4b872ce00451b
