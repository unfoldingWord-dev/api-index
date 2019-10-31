.. _door43:

Door43 Resource Catalog (v3)
============================

Quick Links
-----------

* API Endpoint: https://api.door43.org/v3/catalog.json
* Subjects List Endpoint: https://api.door43.org/v3/subjects/index.json
* Subjects API Endpoint: https://api.door43.org/v3/subjects/pivoted.json
* Browser Endpoint: https://git.door43.org/Door43-Catalog


Description
-----------

The Door43 Resource Catalog provides access to all of our published content.  The catalog is provided in ``JSON`` format and it is a structured hierarchy of resources organized by language and project. Resources may be available in a number of different formats from `Resource Containers <http://resource-container.readthedocs.io/>`_ (which are highly structured translation modules), to binary outputs such as ``pdf``.

.. warning:: The key names in the catalog *will not* change, but new ones may be added without changing the API version.

Please report any issues you may find into our `Door43 Catalog Issue Queue <https://github.com/unfoldingWord-dev/d43-catalog/issues>`_.


For Translation Apps
~~~~~~~~~~~~~~~~~~~~

Translation applications should use the `Resource Containers <http://resource-container.readthedocs.io/>`_ formats (e.g. ``application/zip; type=bundle content=text/usfm conformsto=rc2.0``), which provides access to USFM and Markdown projects in a structured manner.. Other formats may also be used.


For Consumption/Use Apps
~~~~~~~~~~~~~~~~~~~~~~~~

The ``formats`` array will provide various media types that the resource is available in.  These types include (but are not limited to): USFM, Markdown, PDF, DOCX, HTML, MP3, MP4.  Note that not all media types will be available for any given resource.


Design
------

* The catalog is available at https://api.door43.org/v3/catalog.json, where v3 is the API version. Initially this will be the sole endpoint.  A dynamic endpoint that returns only requested information may be built later.
* All timestamps follow the encoding scheme defined in the `W3CDTF profile of ISO 8601 <https://www.w3.org/TR/NOTE-datetime>`_.
* Content linked to within the catalog will be available predominantly (though not exclusively) from https://cdn.door43.org.
* Keys must always be represented even when the value is optional. If the key is not needed/available the value may be empty.
* Values that indicate file size are given in bytes.

.. _door43-definitions:

Definitions
-----------

Much of the catalog (see :ref:`door43-example` below) should be self explanatory. Below are further details about less obvious terms.

* ``identifiers`` must be composed of lowercase alphanumeric characters and hyphens. Additionally: the first character must be a letter and the last character must **not** be a hyphen.

* ``languages`` → ``resources`` → ``projects`` → ``categories`` indicates the hierarchy under which the project is to be displayed. For example: the project ``gen`` would be nested under the ``bible-ot`` category when viewed in an application. Localized titles for each category are available in ``languages`` → ``category_labels``.

* ``languages`` → ``resources`` [→ ``projects``] → ``formats`` provides links to content in various media types. Formats may be presented at the ``resource`` level when containing content for all projects or the ``project`` level when containing a single project.

  * The ``format`` field indicates the type of content that is available for download. This is most commonly a zip archive with additional flags indicating the type of content within the archive:

    * ``type`` this flag indicates the type of `Resource Container <http://resource-container.readthedocs.io/en/v0.2/container_types.html>`_ (RC) represented. RCs are most often used by translation apps such as `translationStudio <http://ufw.io/ts>`_.
    * ``content`` this flag gives the format of the content inside the RC.
    * ``conformsto`` this flag gives the version of the RC specification this RC is built on.

* ``catalogs``: provides links to other supporting content.

* version numbers in the urls such as ``v7`` indicate the version of the resource or asset. This is not the same as the api version seen in the catalog url.

* ``languages`` → ``versification_labels``: provides human readable labels to the different versification systems available in the catalog. These labels may be used, for example, when a user imports raw content such as USFM and are given the opportunity to select the appropriate versification system.

* ``languages`` → ``resources`` → ``modified``: gives the date the resource was last modified according to the translator.

* \* → ``formats`` → ``modified``: gives the date of the most recent commit in `DCS <https://git.door43.org/>`_.
* \* → ``formats`` → ``quality``: if appropriate this specifies the quality of the media such as bitrate or dpi.
* \* → ``formats`` → ``chapters``: lists additional files for download broken up by chapter.
* \* → ``formats`` → ``chapters`` → ``length``: if applicable, the length of the media file in seconds.
* \* → ``formats`` → ``chapters`` → ``identifier``: the chapter identifier.


.. _door43-example:

Example
-------

.. include:: /includes/json_snippet.txt
.. warning:: The following ``JSON`` snippet has several parts removed so that it can be more concise.
.. code-block:: json

    {
      "catalogs": [
        {
          "identifier": "langnames",
          "modified": "2016-10-03",
          "url": "https://td.unfoldingword.org/exports/langnames.json"
        },
        {
          "identifier": "temp-langnames",
          "modified": "2016-10-03",
          "url": "https://td.unfoldingword.org/api/templanguages/"
        },
        {
          "identifier": "approved-temp-langnames",
          "modified": "2016-10-03",
          "url": "https://td.unfoldingword.org/api/templanguages/assignment/changed/"
        },
        {
          "identifier": "new-language-questions",
          "modified": "2016-10-03",
          "url": "https://td.unfoldingword.org/api/questionnaire/"
        }
      ],
      "languages": [
        {
          "category_labels": {
            "bible-nt": "Bible: NT",
            "bible-ot": "Bible: OT",
            "ta": "translationAcademy"
          },
          "direction": "ltr",
          "identifier": "en",
          "resources": [
            {
              "checking": {
                "checking_entity": [
                  "unfoldingWord"
                ],
                "checking_level": "3"
              },
              "comment": "",
              "contributor": [
                "unfoldingWord"
              ],
              "creator": "Door43 World Missions Community",
              "description": "",
              "formats": [
                {
                  "format": "application/zip; type=man content=text/markdown conformsto=rc0.2",
                  "modified": "2017-07-06T15:16:59+00:00",
                  "signature": "https://cdn.door43.org/en/ta/v7/ta.zip.sig",
                  "size": 479004,
                  "url": "https://cdn.door43.org/en/ta/v7/ta.zip"
                }
              ],
              "identifier": "ta",
              "issued": "2017-07-06T00:00:00+00:00",
              "modified": "2017-07-06T00:00:00+00:00",
              "projects": [
                {
                  "categories": [
                    "ta"
                  ],
                  "identifier": "intro",
                  "sort": 0,
                  "title": "Introduction to translationAcademy",
                  "versification": null
                },
                {
                  "categories": [
                    "ta"
                  ],
                  "identifier": "process",
                  "sort": 1,
                  "title": "Process Manual",
                  "versification": null
                },
                {
                  "categories": [
                    "ta"
                  ],
                  "identifier": "translate",
                  "sort": 2,
                  "title": "Translation Manual",
                  "versification": null
                },
                {
                  "categories": [
                    "ta"
                  ],
                  "identifier": "checking",
                  "sort": 3,
                  "title": "Checking Manual",
                  "versification": null
                }
              ],
              "publisher": "unfoldingWord",
              "relation": [],
              "rights": "CC BY-SA 4.0",
              "source": [
                {
                  "identifier": "ta",
                  "language": "en",
                  "version": "7"
                }
              ],
              "subject": "",
              "title": "translationAcademy",
              "version": "7"
            },
            {
              "checking": {
                "checking_entity": [
                  "Distant Shores Media"
                ],
                "checking_level": "3"
              },
              "comment": "",
              "contributor": [
                "Distant Shores Media",
                "unfoldingWord"
              ],
              "creator": "Distant Shores Media",
              "description": "50 key stories of the Bible, from Creation to Revelation, for evangelism & discipleship, in text, audio, and video, on any mobile phone, in any language, for free. It increases understanding of the historical and redemptive narrative of the entire Bible.",
              "identifier": "obs",
              "issued": "2015-08-26T00:00:00+00:00",
              "modified": "2017-01-10T00:00:00+00:00",
              "projects": [
                {
                  "categories": [],
                  "formats": [
                    {
                      "format": "application/zip; type=book content=text/markdown conformsto=rc0.2",
                      "modified": "2017-08-02T18:42:44+00:00",
                      "signature": "https://cdn.door43.org/en/obs/v4/obs.zip.sig",
                      "size": 81845,
                      "url": "https://cdn.door43.org/en/obs/v4/obs.zip"
                    },
                    {
                      "chapters": [
                        {
                          "format": "audio/mp3",
                          "identifier": "08",
                          "length": 212.072,
                          "modified": "2016-05-26T16:28:18+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_08_64kbps.mp3.sig",
                          "size": 1714636,
                          "url": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_08_64kbps.mp3"
                        },
                        {
                          "format": "audio/mp3",
                          "identifier": "30",
                          "length": 133.448,
                          "modified": "2016-05-26T16:28:15+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_30_64kbps.mp3.sig",
                          "size": 1083639,
                          "url": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_30_64kbps.mp3"
                        },
                        {
                          "format": "audio/mp3",
                          "identifier": "12",
                          "length": 221.328,
                          "modified": "2016-05-26T16:28:17+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_12_64kbps.mp3.sig",
                          "size": 1788226,
                          "url": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_12_64kbps.mp3"
                        }
                      ],
                      "contributor": [
                        "Narrator: Steve Lossing",
                        "Checker: Brad Harrington",
                        "Engineer: Brad Harrington"
                      ],
                      "format": "application/zip; content=audio/mp3",
                      "modified": "2016-06-03T21:19:52+00:00",
                      "quality": "64kbps",
                      "signature": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_64kbps.zip.sig",
                      "size": 81732032,
                      "source_version": "4",
                      "url": "https://cdn.door43.org/en/obs/v4/64kbps/en_obs_64kbps.zip",
                      "version": "1"
                    },
                    {
                      "chapters": [
                        {
                          "format": "audio/mp3",
                          "identifier": "08",
                          "length": 212.114,
                          "modified": "2016-05-26T16:27:54+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_08_32kbps.mp3.sig",
                          "size": 866598,
                          "url": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_08_32kbps.mp3"
                        },
                        {
                          "format": "audio/mp3",
                          "identifier": "30",
                          "length": 133.49,
                          "modified": "2016-05-26T16:27:52+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_30_32kbps.mp3.sig",
                          "size": 550062,
                          "url": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_30_32kbps.mp3"
                        },
                        {
                          "format": "audio/mp3",
                          "identifier": "12",
                          "length": 221.37,
                          "modified": "2016-05-26T16:27:53+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_12_32kbps.mp3.sig",
                          "size": 903158,
                          "url": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_12_32kbps.mp3"
                        }
                      ],
                      "contributor": [
                        "Narrator: Steve Lossing",
                        "Checker: Brad Harrington",
                        "Engineer: Brad Harrington"
                      ],
                      "format": "application/zip; content=audio/mp3",
                      "modified": "2016-06-03T21:19:31+00:00",
                      "quality": "32kbps",
                      "signature": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_32kbps.zip.sig",
                      "size": 40456543,
                      "source_version": "4",
                      "url": "https://cdn.door43.org/en/obs/v4/32kbps/en_obs_32kbps.zip",
                      "version": "1"
                    },
                    {
                      "chapters": [
                        {
                          "format": "video/mp4",
                          "identifier": "08",
                          "length": 214.016,
                          "modified": "2016-05-26T16:28:48+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/720p/en_obs_08_720p.mp4.sig",
                          "size": 58156957,
                          "url": "https://cdn.door43.org/en/obs/v4/720p/en_obs_08_720p.mp4"
                        },
                        {
                          "format": "video/mp4",
                          "identifier": "30",
                          "length": 135.04,
                          "modified": "2016-05-26T16:28:33+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/720p/en_obs_30_720p.mp4.sig",
                          "size": 36589625,
                          "url": "https://cdn.door43.org/en/obs/v4/720p/en_obs_30_720p.mp4"
                        },
                        {
                          "format": "video/mp4",
                          "identifier": "12",
                          "length": 223.33866666666665,
                          "modified": "2016-05-26T16:28:45+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/720p/en_obs_12_720p.mp4.sig",
                          "size": 60021756,
                          "url": "https://cdn.door43.org/en/obs/v4/720p/en_obs_12_720p.mp4"
                        }
                      ],
                      "contributor": [],
                      "format": "application/zip; content=video/mp4",
                      "modified": "2017-08-15T21:05:41.995214+00:00",
                      "quality": "720p",
                      "signature": "https://cdn.door43.org/en/obs/v4/720p/en_obs_720p.zip.sig",
                      "size": 2748880681,
                      "source_version": "4",
                      "url": "https://cdn.door43.org/en/obs/v4/720p/en_obs_720p.zip",
                      "version": "1"
                    },
                    {
                      "chapters": [
                        {
                          "format": "video/mp4",
                          "identifier": "08",
                          "length": 214.01832199546485,
                          "modified": "2016-05-26T16:28:08+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/360p/en_obs_08_360p.mp4.sig",
                          "size": 23848949,
                          "url": "https://cdn.door43.org/en/obs/v4/360p/en_obs_08_360p.mp4"
                        },
                        {
                          "format": "video/mp4",
                          "identifier": "30",
                          "length": 135.04725623582766,
                          "modified": "2016-05-26T16:28:00+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/360p/en_obs_30_360p.mp4.sig",
                          "size": 14833310,
                          "url": "https://cdn.door43.org/en/obs/v4/360p/en_obs_30_360p.mp4"
                        },
                        {
                          "format": "video/mp4",
                          "identifier": "39",
                          "length": 211.06938775510204,
                          "modified": "2016-05-26T16:27:58+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/360p/en_obs_39_360p.mp4.sig",
                          "size": 23116536,
                          "url": "https://cdn.door43.org/en/obs/v4/360p/en_obs_39_360p.mp4"
                        },
                        {
                          "format": "video/mp4",
                          "identifier": "12",
                          "length": 223.3295238095238,
                          "modified": "2016-05-26T16:28:07+00:00",
                          "signature": "https://cdn.door43.org/en/obs/v4/360p/en_obs_12_360p.mp4.sig",
                          "size": 24531836,
                          "url": "https://cdn.door43.org/en/obs/v4/360p/en_obs_12_360p.mp4"
                        }
                      ],
                      "contributor": [],
                      "format": "application/zip; content=video/mp4",
                      "modified": "2017-08-15T21:08:34.645965+00:00",
                      "quality": "360p",
                      "signature": "https://cdn.door43.org/en/obs/v4/360p/en_obs_360p.zip.sig",
                      "size": 1135776951,
                      "source_version": "4",
                      "url": "https://cdn.door43.org/en/obs/v4/360p/en_obs_360p.zip",
                      "version": "1"
                    }
                  ],
                  "identifier": "obs",
                  "sort": 0,
                  "title": "Open Bible Stories",
                  "versification": null
                }
              ],
              "publisher": "unfoldingWord",
              "relation": [
                "en/tw",
                "en/obs-tq",
                "en/obs-tn"
              ],
              "rights": "CC BY-SA 4.0",
              "source": [
                {
                  "identifier": "obs",
                  "language": "en",
                  "version": "4"
                }
              ],
              "subject": "Bible stories",
              "title": "Open Bible Stories",
              "version": "4"
            },
            {
              "checking": {
                "checking_entity": [
                  "unfoldingWord"
                ],
                "checking_level": "3"
              },
              "comment": "",
              "contributor": [
                "Jesse Griffin",
                "Jim Pohlig",
                "Larry Sallee",
                "Perry Oakes",
                "Tom Warren",
                "Dave Statezni",
                "Bram van den Heuvel",
                "C. Harry Harriss",
                "Hendrik \"Henry\" de Vries"
              ],
              "creator": "Door43 World Missions Community",
              "description": "An unrestricted literal Bible",
              "formats": [
                {
                  "format": "application/zip; type=bundle content=text/usfm conformsto=rc0.2",
                  "modified": "2017-08-09T23:56:12+00:00",
                  "signature": "https://cdn.door43.org/en/ulb/v10/ulb.zip.sig",
                  "size": 1439121,
                  "url": "https://cdn.door43.org/en/ulb/v10/ulb.zip"
                }
              ],
              "identifier": "ulb",
              "issued": "2017-07-05T00:00:00+00:00",
              "modified": "2017-07-05T00:00:00+00:00",
              "projects": [
                {
                  "categories": [
                    "bible-ot"
                  ],
                  "formats": [
                    {
                      "format": "text/usfm",
                      "modified": "2017-07-05T00:00:00+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/gen.usfm.sig",
                      "size": 204009,
                      "url": "https://cdn.door43.org/en/ulb/v10/gen.usfm"
                    },
                    {
                      "contributor": [],
                      "format": "application/pdf",
                      "modified": "2017-07-21T12:37:08+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/pdf/01-GEN.pdf.sig",
                      "size": 306278,
                      "source_version": "10",
                      "url": "https://cdn.door43.org/en/ulb/v10/pdf/01-GEN.pdf",
                      "version": "10"
                    }
                  ],
                  "identifier": "gen",
                  "sort": 1,
                  "title": "Genesis",
                  "versification": "ufw"
                },
                {
                  "categories": [
                    "bible-ot"
                  ],
                  "formats": [
                    {
                      "format": "text/usfm",
                      "modified": "2017-07-05T00:00:00+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/exo.usfm.sig",
                      "size": 172290,
                      "url": "https://cdn.door43.org/en/ulb/v10/exo.usfm"
                    },
                    {
                      "contributor": [],
                      "format": "application/pdf",
                      "modified": "2017-07-21T12:37:09+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/pdf/02-EXO.pdf.sig",
                      "size": 260802,
                      "source_version": "10",
                      "url": "https://cdn.door43.org/en/ulb/v10/pdf/02-EXO.pdf",
                      "version": "10"
                    }
                  ],
                  "identifier": "exo",
                  "sort": 2,
                  "title": "Exodus",
                  "versification": "ufw"
                },
                {
                  "categories": [
                    "bible-ot"
                  ],
                  "formats": [
                    {
                      "format": "text/usfm",
                      "modified": "2017-07-05T00:00:00+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/mal.usfm.sig",
                      "size": 10425,
                      "url": "https://cdn.door43.org/en/ulb/v10/mal.usfm"
                    },
                    {
                      "contributor": [],
                      "format": "application/pdf",
                      "modified": "2017-07-21T12:37:17+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/pdf/39-MAL.pdf.sig",
                      "size": 69016,
                      "source_version": "10",
                      "url": "https://cdn.door43.org/en/ulb/v10/pdf/39-MAL.pdf",
                      "version": "10"
                    }
                  ],
                  "identifier": "mal",
                  "sort": 39,
                  "title": "Malachi",
                  "versification": "ufw"
                },
                {
                  "categories": [
                    "bible-nt"
                  ],
                  "formats": [
                    {
                      "format": "text/usfm",
                      "modified": "2017-07-05T00:00:00+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/mat.usfm.sig",
                      "size": 132963,
                      "url": "https://cdn.door43.org/en/ulb/v10/mat.usfm"
                    },
                    {
                      "contributor": [],
                      "format": "application/pdf",
                      "modified": "2017-07-21T12:37:17+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/pdf/41-MAT.pdf.sig",
                      "size": 224432,
                      "source_version": "10",
                      "url": "https://cdn.door43.org/en/ulb/v10/pdf/41-MAT.pdf",
                      "version": "10"
                    }
                  ],
                  "identifier": "mat",
                  "sort": 40,
                  "title": "Matthew",
                  "versification": "ufw"
                },
                {
                  "categories": [
                    "bible-nt"
                  ],
                  "formats": [
                    {
                      "format": "text/usfm",
                      "modified": "2017-07-05T00:00:00+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/mrk.usfm.sig",
                      "size": 82963,
                      "url": "https://cdn.door43.org/en/ulb/v10/mrk.usfm"
                    },
                    {
                      "contributor": [],
                      "format": "application/pdf",
                      "modified": "2017-07-21T12:37:18+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/pdf/42-MRK.pdf.sig",
                      "size": 164274,
                      "source_version": "10",
                      "url": "https://cdn.door43.org/en/ulb/v10/pdf/42-MRK.pdf",
                      "version": "10"
                    }
                  ],
                  "identifier": "mrk",
                  "sort": 41,
                  "title": "Mark",
                  "versification": "ufw"
                },
                {
                  "categories": [
                    "bible-nt"
                  ],
                  "formats": [
                    {
                      "format": "text/usfm",
                      "modified": "2017-07-05T00:00:00+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/luk.usfm.sig",
                      "size": 143906,
                      "url": "https://cdn.door43.org/en/ulb/v10/luk.usfm"
                    },
                    {
                      "contributor": [],
                      "format": "application/pdf",
                      "modified": "2017-07-21T12:37:18+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/pdf/43-LUK.pdf.sig",
                      "size": 237635,
                      "source_version": "10",
                      "url": "https://cdn.door43.org/en/ulb/v10/pdf/43-LUK.pdf",
                      "version": "10"
                    }
                  ],
                  "identifier": "luk",
                  "sort": 42,
                  "title": "Luke",
                  "versification": "ufw"
                },
                {
                  "categories": [
                    "bible-nt"
                  ],
                  "formats": [
                    {
                      "format": "text/usfm",
                      "modified": "2017-07-05T00:00:00+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/rev.usfm.sig",
                      "size": 66681,
                      "url": "https://cdn.door43.org/en/ulb/v10/rev.usfm"
                    },
                    {
                      "contributor": [],
                      "format": "application/pdf",
                      "modified": "2017-07-21T12:37:24+00:00",
                      "signature": "https://cdn.door43.org/en/ulb/v10/pdf/67-REV.pdf.sig",
                      "size": 140369,
                      "source_version": "10",
                      "url": "https://cdn.door43.org/en/ulb/v10/pdf/67-REV.pdf",
                      "version": "10"
                    }
                  ],
                  "identifier": "rev",
                  "sort": 66,
                  "title": "Revelation",
                  "versification": "ufw"
                }
              ],
              "publisher": "unfoldingWord",
              "relation": [
                "en/tw",
                "en/tq",
                "en/tn"
              ],
              "rights": "CC BY-SA 4.0",
              "source": [
                {
                  "identifier": "asv",
                  "language": "en",
                  "version": "1901"
                }
              ],
              "subject": "Bible",
              "title": "Unlocked Literal Bible",
              "version": "10"
            }
          ],
          "title": "English",
          "versification_labels": {
            "kjv": "King James Version",
            "mt": "Masoretic Text (Hebrew Bible)"
          }
        }
      ]
    }

Catalog Subjects Endpoint
~~~~~~~~~~~~~~~~~~~~~~~~~

Subjects layouts may be accessed via their ``subject`` (from the above catalog), like this: ``https://api.door43.org/v3/subjects/[subject].json``.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    [
      {
        "subject": "Greek_New_Testament",
        "identifier": "Greek_New_Testament",
        "language": "el-x-koine",
        "resources": [
          {
            "checking": {
              "checking_entity": [
                "unfoldingWord"
              ],
              "checking_level": "2"
            },
            "comment": "",
            "contributor": [
              ...
            ],
            "creator": "unfoldingWord",
            "description": "An open-licensed, lexically tagged, morphologically parsed critical Greek New Testament with full apparatus. It enables the global Church to have access to the original texts of the New Testament.",
            "formats": [
              {
                "format": "application/zip; type=bundle content=text/usfm3 conformsto=rc0.2",
                "modified": "2018-08-02T17:46:25+00:00",
                "signature": "https://cdn.door43.org/el-x-koine/ugnt/v0.2/ugnt.zip.sig",
                "size": 1465124,
                "url": "https://cdn.door43.org/el-x-koine/ugnt/v0.2/ugnt.zip"
              }
            ],
            "identifier": "ugnt",
            "issued": "2018-08-02T00:00:00+00:00",
            "modified": "2018-08-02T00:00:00+00:00",
            "projects": [
              {
                "categories": [
                  "bible-nt"
                ],
                "identifier": "mat",
                "sort": 40,
                "title": "Matthew",
                "versification": "ufw"
              }
              ...
            ],
            "subject": "Greek New Testament",
            "title": "unfoldingWord Greek New Testament",
            "version": "0.2"
          }
        ],
        "direction": "ltr",
        "title": "Koine Greek"
      }
    ]


You may also get a list of ``subject`` endpoints available from the index like this: ``https://api.door43.org/v3/subjects/index.json``.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    [
      "https://api.door43.org/v3/subjects/Bible.json",
      "https://api.door43.org/v3/subjects/Translation_Words.json",
      "https://api.door43.org/v3/subjects/OBS_Translation_Questions.json",
      "https://api.door43.org/v3/subjects/Open_Bible_Stories.json",
      "https://api.door43.org/v3/subjects/Translation_Notes.json",
      "https://api.door43.org/v3/subjects/Translation_Questions.json",
      "https://api.door43.org/v3/subjects/OBS_Translation_Notes.json",
      "https://api.door43.org/v3/subjects/Translation_Academy.json",
      "https://api.door43.org/v3/subjects/Translation_Questions'.json",
      "https://api.door43.org/v3/subjects/Greek_New_Testament.json"
    ]

For some applications it is more efficient to retrieve all the subject entries at once and parse them
on the client. You can do receive the entire object at once here: ``https://api.door43.org/v3/subjects/pivoted.json``.

.. include:: /includes/json_snippet.txt
.. code-block:: json

    {
      "catalogs": [
        {
          "identifier": "langnames",
          "modified": "2016-10-03",
          "url": "https://td.unfoldingword.org/exports/langnames.json"
        }
        ...
      ],
      "subjects": [
        {
          "subject": "Bible",
          "identifier": "Bible",
          "language": "hi",
          "resources": [
            {
              "checking": {
                "checking_entity": [
                  "John Smith"
                ],
                "checking_level": "3"
              },
              "comment": "",
              "contributor": [
                "John Smith",
                ...
              ],
              "creator": "BCS",
              "description": "A basic Bible lexicon that provides translators with clear, concise definitions and translation suggestions for every important word in the Bible. It provides translators and checkers with essential lexical information to help them make the best possible translation decisions.",
              "identifier": "tw",
              "issued": "2018-02-23T00:00:00+00:00",
              "modified": "2018-06-08T00:00:00+00:00",
              "projects": [
                {
                  "categories": [],
                  "formats": [
                    {
                      "format": "application/zip; type=dict content=text/markdown conformsto=rc0.2",
                      "modified": "2018-06-08T19:49:08+00:00",
                      "signature": "https://cdn.door43.org/hi/tw/v8.1/bible.zip.sig",
                      "size": 1196446,
                      "url": "https://cdn.door43.org/hi/tw/v8.1/bible.zip"
                    }
                  ],
                  "identifier": "bible",
                  "sort": 0,
                  "title": "translationWords",
                  "versification": null
                }
              ],
              "publisher": "BCS",
              "relation": [
                "hi/ulb",
                "hi/tn",
                "hi/tq"
              ],
              "rights": "CC BY-SA 4.0",
              "source": [
                {
                  "identifier": "tw",
                  "language": "en",
                  "version": "8"
                }
              ],
              "subject": "Translation Words",
              "title": "translationWords",
              "version": "8.1"
            }
          ],
          "direction": "ltr",
          "title": "हिन्दी"
        }
      ]
    }
