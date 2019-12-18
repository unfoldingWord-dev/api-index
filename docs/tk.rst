.. _tk:

translationKeyboard API
=======================

.. warning:: This API endpoint is no longer available.  Please try `Keyman <https://keyman.com/>`_ instead.

Quick Links
-----------

* API Endpoint: http://tk.unfoldingword.org/api/v1/keyboard/
* Browser Endpoint: http://tk.unfoldingword.org/

Description
-----------

The web component of translationKeyboard allows people to create and modify keyboard layouts that can then be downloaded to Android devices using the translationKeyboard mobile app.  Once downloaded, these layouts can be used on the device or shared with others.

The tK API endpoint provides access to these keyboard layouts and is used by the `tK mobile app <https://github.com/unfoldingWord-dev/translationKeyboard>`_.

Please report any issues you may find into our `translationKeyboardWeb Issue Queue <https://github.com/unfoldingWord-dev/translationKeyboardWeb/issues>`_.


Example
-------

tK Catalog Endpoint
~~~~~~~~~~~~~~~~~~~

The translationKeyboard app has a unified API endpoint at http://tk.unfoldingword.org/api/v1/keyboard/.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    {
      "keyboards": [
        {
          "id": 5,
          "iso_language": "ne",
          "iso_region": "NP",
          "language_name": "नेपाली",
          "updated_at": 1414783592.712652
        },
        ...
      ],
      "updated_at": 1427386363.6908412
    }



tK Keyboard Endpoint
~~~~~~~~~~~~~~~~~~~~

Keyboard layouts may be accessed via their ``id`` (from the above catalog), like this: ``http://tk.unfoldingword.org/api/v1/keyboard/[id]``.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    {
      "keyboard_id": 5,
      "keyboard_name": "Devanagari",
      "created_at": 1414783592.712652,
      "updated_at": 1414783592.712652,
      "iso_region": "NP",
      "iso_language": "ne",
      "keyboard_variants": [
        {
          "name": "Devanagari Android 4 Row",
          "created_at": 1414783739.552225,
          "updated_at": 1414783739.552225,
          "key_position_rows": [
            {
              "key_position_columns": [
                {
                  "percent_width": 1.0,
                  "characters": [
                    {
                      "modmask": 0,
                      "unicode": 2378
                    },
                    {
                      "modmask": 1,
                      "unicode": 2322
                    }
                  ]
                }
              ...
              ]
            ...
            ]
          ...
          ]
      ]
    }
