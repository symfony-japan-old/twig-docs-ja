``abs``
=======

``abs`` フィルタは、値の絶対値を返します。

.. code-block:: jinja

    {# number = -5 #}
    
    {{ number|abs }}
    
    {# outputs 5 #}

.. note::

    内部的には、Twigは、PHPの `abs`_ 関数を使います。

.. _`abs`: http://php.net/abs

.. 2012/08/09 goohib f0a00368924c385a0c55bba53e0fc1098fb4eab4
