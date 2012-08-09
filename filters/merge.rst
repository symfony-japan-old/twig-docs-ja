``merge``
=========

``merge`` フィルタは、ある配列を別の配列にマージします:

.. code-block:: jinja

    {% set values = [1, 2] %}

    {% set values = values|merge(['apple', 'orange']) %}

    {# values now contains [1, 2, 'apple', 'orange'] #}

新しい値が、既存の値の末尾に追加されます。

``merge`` フィルタは、ハッシュでも動作します:

.. code-block:: jinja

    {% set items = { 'apple': 'fruit', 'orange': 'fruit', 'peugeot': 'unknown' } %}

    {% set items = items|merge({ 'peugeot': 'car', 'renault': 'car' }) %}

    {# items now contains { 'apple': 'fruit', 'orange': 'fruit', 'peugeot': 'car', 'renault': 'car' } #}

ハッシュでは、マージの処理は、キーに対して行われます: もしキーが存在しないときには
追加されますが、キーが既に存在するときは、
値が上書きされます。

.. tip::

    配列の中のいずれかの値を（デフォルト値を指定して）確実に定義する場合は、
    呼び出しのときに、2つのマージ対象の要素を逆にしてください:

    .. code-block:: jinja

        {% set items = { 'apple': 'fruit', 'orange': 'fruit' } %}

        {% set items = { 'apple': 'unknown' }|merge(items) %}

        {# items now contains { 'apple': 'fruit', 'orange': 'fruit' } #}

.. 2012/08/09 goohib d95db40838d9d78751f670a5f0050f66efe0fa50
