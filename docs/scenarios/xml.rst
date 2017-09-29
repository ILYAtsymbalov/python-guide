XML разбор
===========

.. image:: https://farm3.staticflickr.com/2808/33888714601_a1f7d020a2_k_d.jpg

untangle
--------

`untangle <https://github.com/stchris/untangle>`_ простая библиотека, 
которая берет XML-документ и возвращает объект Python, который отражает 
узлы и атрибуты в его структуре.

Например, для XML файла:

.. code-block:: xml

    <?xml version="1.0"?>
    <root>
        <child name="child1">
    </root>

можно загрузить следующим образом:

.. code-block:: python

    import untangle
    obj = untangle.parse('path/to/file.xml')

и затем вы можете получить имя дочерних элементов следующим образом:

.. code-block:: python

    obj.root.child['name']

untangle акже поддерживает загрузку XML из строки или URL-адреса.

xmltodict
---------

`xmltodict <http://github.com/martinblech/xmltodict>`_ еще одна простая 
библиотека, цель которой - заставить XML работать с JSON.

XML файл:

.. code-block:: xml

    <mydocument has="an attribute">
      <and>
        <many>elements</many>
        <many>more elements</many>
      </and>
      <plus a="complex">
        element as well
      </plus>
    </mydocument>

могут быть загружены в Python dict следующим образом:

.. code-block:: python

    import xmltodict

    with open('path/to/file.xml') as fd:
        doc = xmltodict.parse(fd.read())

а затем вы можете получить доступ к элементам, атрибутам и значениям
следующим образом:

.. code-block:: python

    doc['mydocument']['@has'] # == u'an attribute'
    doc['mydocument']['and']['many'] # == [u'elements', u'more elements']
    doc['mydocument']['plus']['@a'] # == u'complex'
    doc['mydocument']['plus']['#text'] # == u'element as well'

xmltodict также позволяет вам вернуться в XML с помощью функции unparse, 
иметь режим потоковой передачи, подходящий для обработки файлов, которые 
не вписываются в память и поддерживать пространства имен.
