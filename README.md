---
layout: side_nav
title: unfoldingWord - API Documentation
side_nav: index_side_nav.html
---
# API Documentation

Following are a list of API's we offer to share our content.  Simply make a GET request to the following URL's to receive the content.

###translationKeyboard (v1)

Official specification for translationKeyboard API, version 1:

####Keyboard Layout Catalog

The translationKeyboard app has a unified API endpoint.

**URL:** http://tk.unfoldingword.org/api/v1/keyboard/

**Example:** [http://tk.unfoldingword.org/api/v1/keyboard/](http://tk.unfoldingword.org/api/v1/keyboard/)

~~~~~~~~
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
~~~~~~~~

####Keyboard Layout Endpoint

Keyboard layouts may be accessed via their id (from the above catalog), like this:

**URL:** http://tk.unfoldingword.org/api/v1/keyboard/[id]

**Example:** [http://tk.unfoldingword.org/api/v1/keyboard/5](http://tk.unfoldingword.org/api/v1/keyboard/5)

~~~~~~~~
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
~~~~~~~~

* * * * *

###translationStudio (v2)

In the following examples each catalog reference (i.e. the url) could be generated dynamically in order to slim down the apisize.

####Audio

It has not been determined if a new api will be developed for audio files. This is partly due to the fact that audio has not been incorporated into the app yet. Please refer to the [unfoldingWord API](#unfoldingword-api-v2) instead.

####Images

It has not been determined if a new api will be developed for images. Please refer to the [unfoldingWord API](#unfoldingword-api-v2) instead.

####Languages Catalog

The language catalog contains the translated project name and description along with necessary information regarding the language. Optional meta in the project provides the ability to create soft/virtual categories when viewed in the app. e.g. Bible→New Testament→Luke. NOTE: if the project specifies meta slugs the language must also provide the translated meta names. The date_modified field in the language gets it's value from the most recent date_modified value in the resources catalog. Once again this allows the app to determine if updates are available for a particular language.

**URL:** http://api.unfoldingword.org/ts/txt/2/[book_id]/languages.json

**Example:** [http://api.unfoldingword.org/ts/txt/2/luk/languages.json](http://api.unfoldingword.org/ts/txt/2/luk/languages.json)

~~~~~~~~
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
~~~~~~~~

####Projects Catalog

The main catalog records resources available for translation in translationStudio. This file will always be downloaded first by the app in order to identify available updates. Please note: the date_modified field within this catalog gets it's value from the most recent date_modified value found in the languages catalog. This allows the app to determine if updates are available. You may optionally specify meta categories on a project. See the notes on the language catalog for more details. The sort field allows projects to be displayed in a sorted manner within the app. The sort value MUST be a numeric value. That is, it should be able to be parsed as an int.

**URL:** http://api.unfoldingword.org/ts/txt/2/catalog.json

**Example:** [http://api.unfoldingword.org/ts/txt/2/catalog.json](http://api.unfoldingword.org/ts/txt/2/catalog.json)

~~~~~~~~
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
~~~~~~~~

####Resources Catalog

The resource catalog contains the different types of resources available for translation. When multiple resources are present the app will supply ui controls to switch between resources. The date_modified field is updated any time the source, terms, or notes catalogs are updated. Included in each resource is status which indicates (among other things) the checking level of the resource. The app uses this to determine whether or not the resource is ready for use in the app. If there is only one resource it should be given the slug value “default” and the name can be left as an empty string.

**URL:** http://api.unfoldingword.org/ts/txt/2/[book_id]/[language_code]/resources.json

**Example:** [http://api.unfoldingword.org/ts/txt/2/luk/en/resources.json](http://api.unfoldingword.org/ts/txt/2/luk/en/resources.json)

~~~~~~~~
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
  ...
]
~~~~~~~~

####Source Catalog

The source catalog contains all the chapters and frames of the project. The ref and title are optional. If left blank they will not be available for translation within the app. The img field is likewise optional. There is a new format field that allows you to specify the format of the frame text. For example Bible translation projects are in the usx format. Valid options for format are currently usx and txt.

**URL:** http://api.unfoldingword.org/ts/txt/2/[book_id]/[language_code]/[bible_id]/source.json

**Example:** [http://api.unfoldingword.org/ts/txt/2/luk/en/udb/source.json](http://api.unfoldingword.org/ts/txt/2/luk/en/udb/source.json)

~~~~~~~~
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
         ...
       ],
    },
    ...
  ],
  "date_modified": "20141207",
  "direction": "ltr",
  "language": "en"
}
~~~~~~~~

####Target Languages Catalog

Pull language information.

**URL:** http://td.unfoldingword.org/exports/langnames.json

**Example:** [http://td.unfoldingword.org/exports/langnames.json](http://td.unfoldingword.org/exports/langnames.json)

~~~~~~~~
[
    {
        "gw": false,
        "ld": "ltr",
        "lc": "aa",
        "ln": "Afaraf",
        "cc": ["ET"],
        "lr": "Africa",
        "pk": 6
    }
    ...
]
~~~~~~~~

* * * * *

###unfoldingWord API (v2)

Official specification for unfoldingWord API, version 2:

####Catalog

The unfoldingWord app now has a unified API endpoint.

**URL:** http://api.unfoldingword.org/uw/txt/2/catalog.json

**Example:** [http://api.unfoldingword.org/uw/txt/2/catalog.json](http://api.unfoldingword.org/uw/txt/2/catalog.json)

~~~~~~~~
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
    ...
  ],
  "mod": 1430171270
}
~~~~~~~~

* * * * *

###unfoldingWord API (v1)

Official specification for unfoldingWord API, version 1:

####App Catalog

**URL:** http://api.unfoldingword.org/obs/txt/1/obs-catalog.json

**Example:** [http://api.unfoldingword.org/obs/txt/1/obs-catalog.json](http://api.unfoldingword.org/obs/txt/1/obs-catalog.json)

~~~~~~~~
[
    {
        "date_modified": "20141208",
        "direction": "ltr",
        "language": "fr",
        "status": {
            "checking_entity": "translation team",
            "checking_level": "1",
            "comments": "",
            "contributors": "francoise39;grace-duval;morendo",
            "publish_date": "2014-12-08",
            "source_text": "en",
            "source_text_version": "3.1",
            "version": "3.2.1"
        },
        "string": "Français"
    },
    ...
]
~~~~~~~~

For languages that are currently in progress (from door43.org's perspective).

**URL:** http://api.unfoldingword.org/obs/txt/1/obs-in-progress.json

**Example:** [http://api.unfoldingword.org/obs/txt/1/obs-in-progress.json](http://api.unfoldingword.org/obs/txt/1/obs-in-progress.json)

~~~~~~~~
[
    {
        "lc": "zmz",
        "ln": "Mbandja"
    },
    ...
    {
        "date_modified": "20150903"
    }
]
~~~~~~~~

####JSON Text

**URL:** http://api.unfoldingword.org/obs/txt/1/[language_code]/obs-[language_code].json

**Example:** [http://api.unfoldingword.org/obs/txt/1/en/obs-en.json](http://api.unfoldingword.org/obs/txt/1/en/obs-en.json)

~~~~~~~~
{
    "app_words": {
        "cancel": "Cancel",
        "chapters": "Chapters",
        "languages": "Languages",
        "next_chapter": "Next Chapter",
        "ok": "OK",
        "remove_locally": "Remove Locally",
        "remove_this_string": "Remove this language from offline storage. You will need an internet connection to view it in the future.",
        "save_locally": "Save Locally",
        "save_this_string": "Save this language locally for offline use.",
        "select_a_language": "Select a Language"
    },
    "chapters": [
        {
            "frames": [
                {
                    "id": "01-01",
                    "img": "https://api.unfoldingword.org/obs/jpg/1/en/360px/obs-en-01-01.jpg",
                    "text": "This is how the beginning of everything happened. God created the universe and everything in it in six days. After God created the earth it was dark and empty, and nothing had been formed in it. But God’s Spirit was there over the water."
                }
                ...
            ],
            "number": "01",
            "ref": "A Bible story from: Genesis 1-2",
            "title": "1. The Creation"
        }
        ...
    ],
    "date_modified": "20150826",
    "direction": "ltr",
    "language": "en"
}
~~~~~~~~

####OBS Audio

**URL:** http://api.unfoldingword.org/obs/mp3/1/[language_code]/[language_code]-obs-v[version_number]/[language_code]\_obs\_[frame].mp3

**Example:** [https://api.unfoldingword.org/obs/mp3/1/en/en-obs-v4/en_obs_01.mp3](https://api.unfoldingword.org/obs/mp3/1/en/en-obs-v4/en_obs_01.mp3)

####OBS Images

Current supported height: 2160 pixels & 360 pixels.

**URL:** http://api.unfoldingword.org/obs/jpg/1/[language_code]/[height_pixels]/obs-[langcode]-[chapter]-[frame].jpg

**Example:** [http://api.unfoldingword.org/obs/jpg/1/en/2160px/obs-en-01-01.jpg](http://api.unfoldingword.org/obs/jpg/1/en/2160px/obs-en-01-01.jpg)

* * * * *

###Mirroring the API

Depending on your location, you may mirror the unfoldingWord API docroot with any of the following commands:

~~~~~~~~
rsync -havP rsync://us.door43.org/api/ /path/to/your/docroot/

rsync -havP rsync://uk.door43.org/api/ /path/to/your/docroot/

rsync -havP rsync://jp.door43.org/api/ /path/to/your/docroot/
~~~~~~~~
