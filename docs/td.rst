.. _tD:

translationDatabase API
=======================

Quick Links
-----------

* API Endpoint: http://td.unfoldingword.org/exports/langnames.json
* API Endpoint: http://td.unfoldingword.org/exports/langnames_short.json
* Browser Endpoint: https://td.unfoldingword.org

Description
-----------



Example
-------

.. _tD-langnames:

Language Names Endpoint
~~~~~~~~~~~~~~~~~~~~~~~

* API Endpoint: http://td.unfoldingword.org/exports/langnames.json

The :ref:`tD-langnames` provides access to basic language information for all languages in the world.  The ``lc`` field provides a unique language code for each language, based on the IETF standard (see our `IETF page on the unfoldingWord website <https://unfoldingword.org/ietf>`_ for a simple introduction).

.. include:: /includes/json_snippet.txt
.. code-block:: json

    {
      "pk": 6,
      "alt": [
        "Afaraf",
        "Danakil",
        "Denkel",
        "Adal",
        "Afar Af",
        "Qafar",
        "Baadu (Ba'adu)"
      ],
      "lr": "Africa",
      "gw": false,
      "ang": "Afar",
      "ld": "ltr",
      "lc": "aa",
      "ln": "Afaraf",
      "hc": "ET",
      "cc": [
        "DJ",
        "ER",
        "ET",
        "US",
        "CA"
      ]
    }

The field names are described as follows:

* ``pk``: database key id, for internal use only
* ``alt``: list of alternate names for the language
* ``lr``: specifies the region of the world where the language is predominantly used
* ``gw``: specifies whether or not this is a `Gateway Language <https://unfoldingword.org/gateway/>`_
* ``ang``: an anglicized version of the language name
* ``ld``: specifies the usual text direction, either "ltr" or "rtl"
* ``lc``: specifies language code of this resource following the `IETF standard <https://unfoldingword.org/ietf/>`_
* ``ln``: specifies the name of the language as its speakers refer to it (localized name)
* ``hc``: specifies the country code for the home country of this language
* ``cc``: list of country codes where the language is spoken


.. _tD-langnames-short:

Language Names Short Endpoint
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* API Endpoint: http://td.unfoldingword.org/exports/langnames_short.json

The :ref:`tD-langnames-short` provides access to abbreviated language information for all languages in the world.  The ``lc`` field provides a unique language code for each language, based on the IETF standard (see our `IETF page on the unfoldingWord website <https://unfoldingword.org/ietf>`_ for a simple introduction).

.. include:: /includes/json_snippet.txt
.. code-block:: json

    {
      "pk": 6,
      "lr": "Africa",
      "ang": "Afar",
      "lc": "aa",
      "ln": "Afaraf",
      "hc": "ET"
    }

The field names are described as follows:

* ``pk``: database key id, for internal use only
* ``lr``: specifies the region of the world where the language is predominantly used
* ``ang``: an anglicized version of the language name
* ``lc``: specifies language code of this resource following the `IETF standard <https://unfoldingword.org/ietf/>`_
* ``ln``: specifies the name of the language as its speakers refer to it (localized name)
* ``hc``: specifies the country code for the home country of this language
