# Mediumish-Pagebundles Theme for Hugo

Hugo is a static site generator, see https://gohugo.io

This theme for gohugo is a modified version of [lgaida's customized port](https://github.com/lgaida/mediumish-gohugo-theme) based on the [Mediumish Jekyll-Theme](//github.com/wowthemesnet/mediumish-theme-jekyll) by [WowThemesNet](//github.com/wowthemesnet). It uses **page bundles**, automatic **image processing** done by Hugo, and is more **lightweight** for better GDPR-compliance and **excellent performance** ratings in Google Page Speed Insights Lighthouse. A **print style**, a **RSS-feed** and **better control of search engine indexing** was added. The theme is **localized in German**, but you can change this easily.

![screenshot](https://raw.githubusercontent.com/mplatten/mediumish-pagebundles-gohugo-theme/master/images/screenshot.png)


## Features of the original gohugo-theme port by lgaida

+ Landingpage
+ 404-Page
+ Posts
    + tags can be used
    + shareable via socialmedia
+ Custom pagination
+ Prev/Next-Links
+ Tag-Overview in Jumbotron
+ Integrations:
    + Disqus Comments
    + Google Analytics
    + Mailchimp


## Added/modified features by mplatten

This is a modified version of lgaida's port to Hugo. Changes to that are:

+ use with **page bundles** instead of assets in `/static` (works also)—keep content and its assets together
+ **Automatic image resizing** (done by Hugo)--feel free to save Markdown-text and your original images of any size for future use and other assets in a subfolder of `/content` (i. e. page bundles), Hugo will resize the *published* images for a great performance and strip EXIF-data (please be advised: Hugo publishes a copy of the unaltered original file with its original filename in `/public` too, EXIF not altered! This is a Hugo problem which might be an issue with security.)
+ **Improved overall performance**: Google Pagespeed Insights/Lighthouse >90, pages usually at peek performance
+ **Print-Style**: Site title and page-URL are printed on top before `title`, Hyperlink-URLs will be displayed in brackets behind each link in print so anyone can resolve them even on paper, `<video>` won't show in print, no other webpage-elements on paper
+ Full-text **RSS-Feed** at `<baseurl>/index.xml` (Thanks to code taken from funkydan2, <https://github.com/funkydan2/alpha-church>)
+ Image titles will be shown as a caption, e. g. `![Alt text wont't show, use it anyway, always](image.jpg This title shows as a caption below the image)`. The file `image.jpg` should be placed in the same folder, text-file must be named `index.md`.
+ Subtitles with `subtitle: "Text"` in frontmatter on each page (if set, can be omited)
+ Control search engine indexing with `robots: "value"` in frontmatter on each page individually (if it is used, it will override the values in config.toml for that page) if you dont use `/static/robots.txt`
+ All frameworks served locally, no CDNs, thus better GDPR/DSGVO-compliancy due to no third-parties
+ no embedded fonts -- Google Pagespeed Insights' Lighthouse likes few chains
+ FontAwesome social-media icons replaced by small local SVGs
+ Twitter Cards and Facebook Open Graph


## Installation

Inside the folder of your Hugo site run:

    $ cd themes
    $ git clone https://github.com/mplatten/mediumish-pagebundles-gohugo-theme mediumish-pagebundles

You can--this is a good idea--move the contents of the folder `exampleSite` to the root folder next to `themes` to get a working configuration and example content.


## Preface

Each page/article should have its own folder under `content`, e. g. `content/2020-11-28-demo-page`. In this folder there *must* be an `index.md` (no other filename) which has frontmatter and the page's content. Put assets like images in this folder too, not in `static`.

Other assets can be placed somewhere within the `static` folder of your gohugo website. This allows them to be easily referenced from the config.toml. You may structure the files and folders within `static` however you'd like, with one exception: There must be a file named `jumbotron.jpg` present under the path `static/images` as it is referenced in the .css.


## Post Example

To create a simple post use the hugo new command as usual.
```
hugo new blog/2020-11-28-demo-page/index.md
```

An example `index.md` – the folder's name should be distinct.

```
---
title: "The title"
subtitle: "Some more information about this content"
summary: "This is a demo page. Search engines like this field."
date: 2020-11-28T00:00:00+01:00
publishdate: 2020-11-28T00:00:00+01:00
image: "/blog/2020-11-28-demo-page/2007-schwarzewueste.jpg"
type: post
tags: ["Tag 1","Tag 2"]
comments: false
robots: "noindex, nofollow, noarchive"
---
This is some Text with an image below. Hugo will resize images to a long side size of 800 Pixels automatically with this theme--the original file is untouched, so you can simply use images without any worries on optimization, Hugo does that for you:

![Schwarze Wüste](2007-schwarzewueste.jpg "Schwarze Wüste, Ägypten.")

As you can see, the image's title is shown as a caption.

## Structure

The page bundle feature requires a folder with a distinct name (here: `2020-11-28-demo-page`).

The main article in that folder *must* be named `index.md`.

Assets are put into that folder too. For list pages to show thumbnails it is necessary that the post's main image is linked in frontmatter with *full path*, see above in this page's frotmatter: `image: "/blog/test/2007-schwarzewueste.jpg"`. This image will only show on list pages--if you want a copy in single view, you must link it like in the examle above. This gives you control over where images show and the possibility to have an explicit thumbnail for each article in list view. Twitter Cards and Facebook will use this image too.

## Hugo's Shortcodes

Shortcodes are an easy way to inlude content from e.g. Twitter or Youtube:

**Example Twitter**:

{{</* tweet 877500564405444608 */>}} renders as:

{{< tweet 877500564405444608 >}}

**Example Youtube**:

{{</* youtube w7Ft2ymGmfc */>}} renders as:

{{< youtube w7Ft2ymGmfc >}}

Now try to print this page so you can see the print style in action.

By the way: launch hugo with `hugo --gc --minify` for automatic clean up and smaller files.
```

`publishdate`: is displayed at the top of the single-view\
`image`: is displayed in the list- and single-view\
`tags`: are used as usual, just add the tags you want to use. They are displayed in the jumbotron on the list-view, and on the bottom of each single-view\
`comments`: true/false to turn on/off disqus-comments
`robots`: use standard robots.txt commands. If this field is present, it will override a  the general settings in config.toml. To use these, omit this fiel in a page.


## Configuration

You should at least specify the following default params in your config.toml
```toml
baseURL = "https://example.com" # No slash (/) in the end of site address!
languageCode = "de-DE"
title = "<title of this site>"
theme = "mediumish-pagebundles"
summaryLength = 25
rssLimit = 5
copyright = "<your name here>"
enableEmoji = true
publishDir = "public"
#disqusShortname = "your-shortname-here"
#googleAnalytics = "UA-1XXXXXXX1-1"
pluralizelisttitles = false

defaultMarkdownHandler = "goldmark"

[markup.goldmark]
  [markup.goldmark.extensions]
    definitionList = true
    footnote = true
    linkify = true
    strikethrough = true
    table = true
    taskList = true
    typographer = true
  [markup.goldmark.parser]
    attribute = true
    autoHeadingID = true
  [markup.goldmark.renderer]
    hardWraps = false
    unsafe = true # Allows HTML-tags in MD, e.g. the HTML5 video-tag so that video can play in a page.
    xHTML = false
  [markup.highlight]
    codeFences = true
    hl_Lines = ""
    lineNoStart = 1
    lineNos = false
    lineNumbersInTable = true
    noClasses = true
    style = "monokai"
    tabWidth = 4
  [markup.tableOfContents]
    endLevel = 3
    startLevel = 2

[params]
#  logo = "/images/logo.png"
  description ="Welcome!"
  #mailchimp = "you can provide a mailchimp-link here"
  robots = "noarchive"

[params.author]
  name = "<your name>"
#  thumbnail = "/images/author.jpg"
  description = ""

[params.index]
  picture = "/images/welcome.jpg"
  title = "Welcome!"
  subtitle = ""
  mdtext = '''
  **Read My [Blog](/blog/) first**,\
  \
and then read another post.
'''
  alertbar = false

[params.social]
#  github = "<username>"
#  facebook = "<username>"
#  facebookmessenger = "<username>"
#  twitter = "<username>"
  rssfeed = "/index.xml"

## Main Menu
[[menu.main]]
    name = "Blog"
    weight = 100
    identifier = "blog"
    url = "/blog/"
# [[menu.main]]
#    name = "Other"
#    weight = 200
#    identifier = "other"
#    url = "/other/"
# [[menu.main]]
#    name = "About Me"
#    identifier = "about"
#    weight = 400
#    url = "/"
[[menu.main]]
    name = "Datenschutzerklärung"
    identifier = "datenschutz"
    weight = 500
    url = "/datenschutz/"
[[menu.main]]
    name = "Impressum"
    identifier = "imprint"
    weight = 600
    url = "/impressum/"

[sitemap]
    changefreq = "monthly"
    priority = 0.5
    filename = "sitemap.xml"

[imaging.exif]
    # This will strip EXIF-Data from *processed* images.
    # PLEASE BE AWARE: **Hugo copies the *original file* (original
    # filenname) unaltered into the `publish`-folder** too—this
    # might be an issue with security due to unaltered EXIF-
    # Data in the original. This is a Hugo problem, at the
    # time (Nov 2020) there ist no way to prevent Hugo
    # from doing so.
    #
     # Regexp matching the fields you want to Exclude from the (massive) set of Exif info
    # available. As we cache this info to disk, this is for performance and
    # disk space reasons more than anything.
    # If you want it all, put ".*" in this config setting.
    # Note that if neither this or ExcludeFields is set, Hugo will return a small
    # default set.
    includeFields = ""

    # Regexp matching the Exif fields you want to exclude. This may be easier to use
    # than IncludeFields above, depending on what you want.
    excludeFields = ".*"

    # Hugo extracts the "photo taken" date/time into .Date by default.
    # Set this to true to turn it off.
    disableDate = true

    # Hugo extracts the "photo taken where" (GPS latitude and longitude) into
    # .Long and .Lat. Set this to true to turn it off.
    disableLatLong = true
```

`disqusShortname`: provide your disqusShortname\
`googleAnalytics`: provide your googleAnalytics-Code


## License

Like the original jekyll-theme and lgaida's port to gohugo this modified theme is released under the MIT License. Read more at the [License](//github.com/mplatten/mediumish-pagebundles-gohugo-theme/blob/master/LICENSE) itself.
