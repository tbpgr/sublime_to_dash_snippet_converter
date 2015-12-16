Dash Snippet Converter(Sublime Text to Dash)

## Setup
```
$ git clone https://github.com/tbpgr/sublime_to_dash_snippet_converter.git
```

## Structure

```
$ cd %git%/sublime_to_dash_snippet_converter
$ tree
.
├── Gemfile
├── LICENSE.txt
├── README.md
├── Rakefile
├── dash
└── sublime
    ├── fa-500px.sublime-snippet
    └── ... snippet files
```

## Settings
### Move to work dir
```
$ cd %git%/sublime_to_dash_snippet_converter

# check rake task
$ rake -T
rake dash:sublime_convert  # convert sublime snippets to dash snippets
```

### .env Setting(Sample)
```
$ cd 
$ touch .env
```

```
LOG_LEVEL=DEBUG
```

### Sublime Snippet(Sample)
* fa-500px.sublime-setting

```xml
<snippet>
  <content><![CDATA[
<i class="fa fa-500px" style="font-size:1em;"></i>
]]></content>
  <tabTrigger>fa-500px</tabTrigger>
  <scope>text.html.markdown</scope>
  <description>fontawesome fa fa-500px</description>
</snippet>
```

## Usage
### Build
```bash
$ rake dash:sublime_convert
2015/12/16 22:39:57 - DEBUG - start convert snippets
2015/12/16 22:39:57 - DEBUG -    complete output ./dash/fa-500px.toml
2015/12/16 22:39:57 - DEBUG - finish convert snippets
```

### Check Dash Snippet
```bash
$ cat dash/fa-500px.toml
[snippet]
body = "<i class=\"fa fa-500px\" style=\"font-size:1em;\"></i>"
syntax = "None"
tag = "FontAwesome"
title = "fa-500px;;"
```

## Relation
https://github.com/tbpgr/dash_snippets_builder
https://github.com/tbpgr/dash-snippets

