``convert_encoding``
====================

.. versionadded:: 1.4
    ``convert_encoding`` フィルタは、Twig 1.4 で追加されました。

``convert_encoding`` フィルタは、文字列を、あるエンコーディングから
別のエンコーディングに変換します。 第1引数は、出力の文字セットを、第2引数は、
入力の文字セットを指定します:

.. code-block:: jinja

    {{ data|convert_encoding('UTF-8', 'iso-2022-jp') }}

.. note::

    このフィルタは、`iconv`_ または、`mbstring`_ エクステンションに依存しているので、
    どちらかがインストールされていなければなりません。 両方がインストールされている場合は、`mbstring`_ が
    デフォルトで使用されます (Twig 1.8.1 より前では、`iconv`_ がデフォルトで使用されます)。

.. _`iconv`:    http://php.net/iconv
.. _`mbstring`: http://php.net/mbstring

.. 2012/08/09 goohib 793660510f6424adc738ccd76be8e76ba827cee0
