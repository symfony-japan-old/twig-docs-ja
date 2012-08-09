``date``
========

.. versionadded:: 1.1
    タイムゾーンのサポートは、Twig 1.1 から追加されています。

.. versionadded:: 1.5
    デフォルトの日付書式のサポートは、Twig 1.5 から追加されています。

.. versionadded:: 1.6.1
    デフォルトのタイムゾーンのサポートは、Twig 1.6.1 から追加されています。

``date`` フィルタは、指定した書式で日付をフォーマットします:

.. code-block:: jinja

    {{ post.published_at|date("m/d/Y") }}

``date`` フィルタが受け取れるものは、文字列 (`strtotime`_ 関数でサポートされている
書式でなければなりません)、`DateTime`_ インスタンス、または、`DateInterval`_ インスタンスです。 
例えば、現在の日付を表示するには、単語 "now" をフィルタにかけます:

.. code-block:: jinja

    {{ "now"|date("m/d/Y") }}

日付書式の中の文字や単語をエスケープするには、``\\`` をそれぞれの文字の前に使います:

.. code-block:: jinja

    {{ post.published_at|date("F jS \\a\\t g:ia") }}

タイムゾーンを指定することも可能です:

.. code-block:: jinja

    {{ post.published_at|date("m/d/Y", "Europe/Paris") }}

書式が指定されないときは、Twigは、デフォルトの書式を使います: ``F j, Y H:i``。 この
デフォルトは、簡単に変更できますが、それには、``core`` エクステンションのインスタンスの ``setDateFormat()``
メソッドを呼びます。 第1引数は、日付の、第2引数は、日付間隔の
デフォルトの書式になります:

.. code-block:: php

    $twig = new Twig_Environment($loader);
    $twig->getExtension('core')->setDateFormat('d/m/Y', '%d days');

デフォルトのタイムゾーンもグローバルにセットでき、これには、``setTimezone()`` を呼びます:

.. code-block:: php

    $twig = new Twig_Environment($loader);
    $twig->getExtension('core')->setTimezone('Europe/Paris');

.. _`strtotime`:    http://www.php.net/strtotime
.. _`DateTime`:     http://www.php.net/DateTime
.. _`DateInterval`: http://www.php.net/DateInterval

``date`` フィルタに渡された値が null のときは、デフォルトでは、現在の日時が返ります。
現在日時の代わりに、空の文字が必要でしたら、3項演算子を使ってください:

.. code-block:: jinja

    {{ post.published_at is empty ? "" : post.published_at|date("m/d/Y") }}

.. 2012/08/09 goohib 0366cf6185ce575e8cbd8354880a1f95743505b3
