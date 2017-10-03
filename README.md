# ASS-tools
Simple tool untuk mengconvert ass2json/json2ass dan auto translate dengan API


Installing
----------

To install the dependencies, run:

    cpanm --installdeps .

Use
---


- ass2json.pl - converts the ASS file in JSON with the possibility of translating subtitles via Google Translate API
- json2ass.pl - converts the generated file in JSON by ass2json.pl tool in ASS file

ass2json.pl
-----------

This tool accepts the following parameters:
- `-f` -- **required** -- ASS file
- `-c` -- *optional* -- Counts the number of characters used in the subtitles. (Useful for measuring the Google Translate API use)
- `-v` -- *optional* -- Print progress during execution (There are two levels: (-v) prints information about the progress and (-v -v) prints the contents of the previous level with the JSON result.)
- `-t` -- *optional* -- Translate subtitles using Google Translate API (You must set the environment variable GOOGLE_TRANSLATE_API_KEY)
- `-i` -- **required if -t is set** -- Subtitle language in the file (input language)
- `-p` -- **required if -t is set** -- Output language

**Important**: `-c` and `-t` are mutually exclusive. Use one at a time.

For a complete list of parameters used for each language, see [here](https://cloud.google.com/translate/v2/using_rest#language-params)

The file produced by the tool has the name of the input file, increased by the extension `.json`.

json2ass.pl
-----------

This tool accepts the following parameters:
- `-f` -- **required** -- ass file

The file produced by the tool has the name of the input file, increased by the extension `.ass`.



## Translate ASS file (with verbose)


    export GOOGLE_TRANSLATE_API_KEY='example-api-key'
    ./ass2json.pl -f sub.ass -t -i pt -o en -v
    -> Checking file permissions (sub.ass)
    -> Translating 1 of 5
    -> Translating 2 of 5
    -> Translating 3 of 5
    -> Translating 4 of 5
    -> Translating 5 of 5
    -> Write results file (sub.ass.json)

    > cat sub.srt.json (pretty printed)
    [
        {
            "end_time": "00:00:05,752",
            "original": "\u00c3\u0089 preciso sofrer depois de ter sofrido,",
            "start_time": "00:00:03,084",
            "subtitle": "You need to suffer after having suffered,"
        },
        {
            "end_time": "00:00:07,887",
            "original": "e amar, e mais amar, depois de ter amado.",
            "start_time": "00:00:05,754",
            "subtitle": "and love, and more love, having loved."
        },
        {
            "end_time": "00:00:12,325",
            "original": "Se todo animal inspira ternura,",
            "start_time": "00:00:07,889",
            "subtitle": "If every animal inspires tenderness,"
        },
        {
            "end_time": "00:00:14,894",
            "original": "que houve, ent\u00c3\u00a3o, com os homens?",
            "start_time": "00:00:12,327",
            "subtitle": "What happened, then, with men?"
        },
        {
            "end_time": "00:00:16,696",
            "original": "Guimar\u00c3\u00a3es Rosa",
            "start_time": "00:00:14,896",
            "subtitle": "Guimar\u00c3\u00a3es Rosa"
        }
    ]

## Translate ASS file (with super verbose)


    export GOOGLE_TRANSLATE_API_KEY='example-api-key'
    ./ass2json.pl -f sub.ass -t -i pt -o en -v -v
    -> Checking file permissions (sub.ass)
    -> Translating 1 of 5
    -> Translating 2 of 5
    -> Translating 3 of 5
    -> Translating 4 of 5
    -> Translating 5 of 5
    -> Write results file (sub.ass.json)
    
    [{"start_time":"00:00:03,084","end_time":"00:00:05,752","subtitle":"You need to suffer after having suffered,","original":"Ã preciso sofrer depois de ter sofrido,"},{"subtitle":"and love, and more love, having loved.","original":"e amar, e mais amar, depois de ter amado.","end_time":"00:00:07,887","start_time":"00:00:05,754"},{"start_time":"00:00:07,889","subtitle":"If every animal inspires tenderness,","original":"Se todo animal inspira ternura,","end_time":"00:00:12,325"},{"start_time":"00:00:12,327","end_time":"00:00:14,894","subtitle":"What happened, then, with men?","original":"que houve, entÃ£o, com os homens?"},{"end_time":"00:00:16,696","original":"GuimarÃ£es Rosa","subtitle":"GuimarÃ£es Rosa","start_time":"00:00:14,896"}]


The generated file is the same as the previous example.

Contributing
------------

If you have any questions that this documentation does not resolve, or want a feature, open an issue.

If you want to contribute code, please send a pull-request.
