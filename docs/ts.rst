.. _tS:

translationStudio API (v2)
==========================

.. include:: /includes/deprecated.txt


Quick Links
-----------

* API Endpoint: https://api.unfoldingword.org/ts/txt/2/catalog.json
* Browser Endpoint: https://git.door43.org/Door43-Catalog

.. note:: The Browser Endpoint above will contain more data than the tS API (2). Please update your software to use :ref:`door43` if you need all the data shown there.


Description
-----------

The translationStudio version 2 API is comprised of several cascading catalogs, starting with the :ref:`tS-projects`.

.. warning:: Please update your software to use :ref:`door43` if you experience issues with this endpoint.


Example
-------

.. _tS-projects:

Projects Catalog
~~~~~~~~~~~~~~~~

* API Endpoint: http://api.unfoldingword.org/ts/txt/2/catalog.json

The :ref:`tS-projects` records resources available for translation in translationStudio. This file will always be downloaded first by the app in order to identify available updates.

Please note: the ``date_modified`` field within this catalog gets it's value from the most recent ``date_modified`` value found in the :ref:`tS-langs`. This allows the app to determine if updates are available.

You may optionally specify meta categories on a project. See the notes on the :ref:`tS-langs` for more details.

The sort field allows projects to be displayed in a sorted manner within the app. The sort value MUST be a numeric value. That is, it should be able to be parsed as an integer.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    [
      {
        "slug": "obs",
        "sort": "01",
        "date_modified": "20141207",
        "lang_catalog": "https://api.unfoldingword.org/ts/txt/2/obs/languages.json?date_modified=20141207"
      },
      {
        "slug": "luk",
        "sort": "42",
        "meta": ["bible", "nt"],
        "date_modified": "20141207",
        "lang_catalog": "https://api.unfoldingword.org/ts/txt/2/luk/languages.json?date_modified=20141207"
      }
    ]


.. _tS-langs:

Languages Catalog
~~~~~~~~~~~~~~~~~

* API Endpoint: http://api.unfoldingword.org/ts/txt/2/[book_id]/languages.json
* Example: http://api.unfoldingword.org/ts/txt/2/luk/languages.json

The :ref:`tS-langs` contains the translated project name and description along with necessary information regarding the language.

Optional meta in the project provides the ability to create soft/virtual categories when viewed in the app. e.g. Bible→New Testament→Luke.

.. note:: If the project specifies meta slugs the language must also provide the translated meta names.

The ``date_modified`` field in the language gets it's value from the most recent ``date_modified`` value in the :ref:`tS-resources`. Once again this allows the app to determine if updates are available for a particular language.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    [
      {
        "project": {
          "name": "Luke",
          "desc": "Gospel",
          "meta": ["Bible", "New Testament"]
        },
        "language": {
          "slug": "en",
          "name": "English",
          "direction": "ltr",
          "date_modified": "20141207"
        },
        "res_catalog": "https://api.unfoldingword.org/ts/txt/2/luk/en/resources.json?date_modified=20141207"
      },
      {
        "project": {
          "name": "Lucas",
          "desc": "evangelio",
          "meta": ["Biblia", "Nuevo Testamento"]
        },
        "language": {
          "slug": "es",
          "name": "español",
          "direction": "ltr",
          "date_modified": "20141207"
        },
        "res_catalog": "https://api.unfoldingword.org/ts/txt/2/luk/es/resources.json?date_modified=20141207"
      }
    ]


.. _tS-resources:

Resources Catalog
~~~~~~~~~~~~~~~~~

* API Endpoint: http://api.unfoldingword.org/ts/txt/2/[book_id]/[language_code]/resources.json
* Example: http://api.unfoldingword.org/ts/txt/2/luk/en/resources.json

The :ref:`tS-resources` contains the different types of resources available for translation. When multiple resources are present the app will supply ui controls to switch between resources.

The ``date_modified`` field is updated any time the source, terms, or notes catalogs are updated.

Included in each resource is status which indicates (among other things) the checking level of the resource. The app uses this to determine whether or not the resource is ready for use in the app. If there is only one resource it should be given the slug value “default” and the name can be left as an empty string.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    [
      {
        "slug": "ulb",
        "name": "unfoldingWord Literal Bible",
        "date_modified": "20141207",
        "status": {
          "checking_entity": "Distant Shores Media; Wycliffe Associates",
          "checking_level": "3",
          "comments": "Original source text.",
          "contributors": "Wycliffe Associates",
          "publish_date": "2014-12-07",
          "source_text": "en",
          "source_text_version": "3.1.1",
          "version": "3.1.1"
        },
        "source": "https://api.unfoldingword.org/ts/txt/2/luk/en/ulb/source.json?date_modified=20150409",
        "terms": "https://api.unfoldingword.org/ts/txt/2/luk/en/ulb/terms.json?date_modified=20150409",
        "notes": "https://api.unfoldingword.org/ts/txt/2/luk/en/ulb/notes.json?date_modified=20150409",
        "checking_questions":"https://api.unfoldingword.org/ts/txt/2/luk/en/ulb/CQ-en.json?date_modified=20150409"
      }
    ]


.. _tS-source:

Source Catalog
~~~~~~~~~~~~~~

* API Endpoint: http://api.unfoldingword.org/ts/txt/2/[book_id]/[language_code]/[bible_id]/source.json
* Example: http://api.unfoldingword.org/ts/txt/2/luk/en/udb/source.json

The :ref:`tS-source` contains all the chapters and frames of the project.

The ``ref`` and ``title`` fields are optional. If left blank they will not be available for translation within the app. The ``img`` field is likewise optional.

There is a new format field that allows you to specify the format of the frame text. For example Bible translation projects are in the usx format. Valid options for format are currently usx and txt.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    {
      "chapters": [
        {
          "number": "01",
          "ref": "",
          "title": "",
          "frames": [
            {
              "id": "01-01",
              "img": "",
              "format": "usx",
              "text": "<para style=\"p\"><verse number=\"1\" style=\"v\" />Now in those days, it came about that Caesar Augustus sent out a decree ordering that a census be taken of all the people living in the Roman world.<verse number=\"2\" style=\"v\" />This was the first census made while Quirinius was governor of Syria.<verse number=\"3\" style=\"v\" />So everyone went to his own town to be registered for the census.</para>"
             },
           ],
        },
      ],
      "date_modified": "20141207",
      "direction": "ltr",
      "language": "en"
    }


Target Languages Catalog
~~~~~~~~~~~~~~~~~~~~~~~~

The list of languages used in translationStudio is pulled from :ref:`td`.
