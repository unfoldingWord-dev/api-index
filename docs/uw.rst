.. _uW:

unfoldingWord App Catalog (v2)
==============================

.. include:: /includes/deprecated.txt


Quick Links
-----------

* API Endpoint: https://api.unfoldingword.org/uw/txt/2/catalog.json
* Browser Endpoint: https://git.door43.org/Door43-Catalog

.. note:: The Browser Endpoint above will contain more data than the uW API (2). Please update your software to use :ref:`door43` if you need all the data shown there.


Description
-----------

The unfoldingWord app has a unified API endpoint that provides links to all the resources available.

.. warning:: Please update your software to use :ref:`door43` if you experience issues with this endpoint.


.. _uW-example:

Example
-------

* API Endpoint: https://api.unfoldingword.org/uw/txt/2/catalog.json

.. include:: /includes/json_snippet.txt
.. code-block:: json

    {
      "cat": [
        {
          "langs": [
            {
              "lc": "ar",
              "mod": "1427846400",
              "vers": [
                {
                  "mod": "1427846400",
                  "name": "\ufe8e\ufee0\ufedc\ufe97\ufe8e\ufe91 \ufe8e\ufee0\ufee4\ufed7\ufeaa\ufeb3 \ufe8f\ufe8e\ufee0\ufee0\ufecf\ufe93 \ufe8e\ufee0\ufecb\ufeae\ufe92\ufef3\ufe93\u060c \ufed1\ufe8e\ufee7 \ufea9\ufe8e\ufef4\ufedb",
                  "slug": "avd",
                  "status": {
                    "checking_entity": "Syrian Mission;American Bible Society;PNG Bible Translation Association",
                    "checking_level": "3",
                    "comments": "Original source text",
                    "contributors": "Eli Smith;Cornelius Van Allen Van Dyck;Nasif al Yaziji;Boutros al Bustani;Yusuf al-Asir",
                    "publish_date": "20150401",
                    "source_text": "ar",
                    "source_text_version": "2014-02-13",
                    "version": "2014-02-13"
                  },
                  "toc": [
                    {
                      "desc": "",
                      "mod": "1427846400",
                      "slug": "gen",
                      "src": "https://api.unfoldingword.org/avd/txt/1/avd-ar/01-GEN.usfm",
                      "src_sig": "https://api.unfoldingword.org/avd/txt/1/avd-ar/01-GEN.sig",
                      "title": "\u0627\u064e\u0644\u062a\u0651\u064e\u0643\u0652\u0648\u0650\u064a\u0646\u064f"
                    }
                  ]
                }
              ]
            }
          ],
          "slug": "bible",
          "title": "Bible"
        }
      ],
      "mod": 1430171270
    }
