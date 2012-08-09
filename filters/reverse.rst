``reverse``
===========

.. versionadded:: 1.6
    文字列のサポートは、Twig 1.6 から追加されました。

``reverse`` フィルタは、シーケンス、マッピング、または文字列を逆順にします:

.. code-block:: jinja

    {% for use in users|reverse %}
        ...
    {% endfor %}

    {{ '1234'|reverse }}

    {# 4321 が出力 #}

.. note::

    これは、`Traversable`_ インターフェースを実装したオブジェクトでも動作します。

.. _`Traversable`: http://php.net/Traversable

.. 2012/08/09 goohib 4578c176e59910f3ebb3b56d7c8d9e9808a511be
