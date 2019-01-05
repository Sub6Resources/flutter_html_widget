# flutter_html
[![pub package](https://img.shields.io/pub/v/flutter_html.svg)](https://pub.dartlang.org/packages/flutter_html)

A Flutter widget for rendering static html tags as Flutter widgets. (Will render over 70 different html tags!)

## Installing:

Add the following to your `pubspec.yaml` file:

    dependencies:
      flutter_html: ^0.8.2

## Currently Supported HTML Tags:
`a`, `abbr`, `acronym`, `address`, `article`, `aside`, `b`, `bdi`, `bdo`, `big`, `blockquote`, `body`, `br`, `caption`, `cite`, `code`, `data`, `dd`, `del`, `dfn`, `div`, `dl`, `dt`, `em`, `figcaption`, `figure`, `footer`, `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `header`, `hr`, `i`, `img`, `ins`, `kbd`, `li`, `main`, `mark`, `nav`, `noscript`, `ol`, `p`, `pre`, `q`, `rp`, `rt`, `ruby`, `s`, `samp`, `section`, `small`, `span`, `strike`, `strong`, `table`, `tbody`, `td`, `template`, `tfoot`, `th`, `thead`, `time`, `tr`, `tt`, `u`, `ul`, `var`
 
### Partially supported elements:
> These are common elements that aren't yet fully supported, but won't be ignored and will still render somewhat correctly.

`center`
 
### List of _planned_ supported elements:
> These are elements that are planned, but present a specific challenge that makes them somewhat difficult to implement.

`audio`, `details`, `source`, `sub`, `summary`, `sup`, `svg`, `track`, `video`, `wbr`

### List of elements that I don't plan on implementing:

> Feel free to open an issue if you have a good reason and feel like you can convince me to implement
 them. A _well written_ and _complete_ pull request implementing one of these is always welcome,
 though I cannot promise I will merge them.

> Note: These unsupported tags will just be ignored.

`applet`, `area`, `base`, `basefont`, `button`, `canvas`, `col`, `colgroup`, `datalist`, `dialog`, `dir`, `embed`, `font`, `fieldset`, `form`, `frame`, `frameset`, `head`, `iframe`, `input`, `label`, `legend`, `link`, `map`, `meta`, `meter`, `noframe`, `object`, `optgroup`, `option`, `output`, `param`, `picture`, `progress`, `script`, `select`, `style`, `textarea`, `title`
 

## Why this package?

This package is designed with simplicity in mind. Flutter currently does not support rendering of web content
into the widget tree. This package is designed to be a reasonable alternative for rendering static web content
until official support is added.

## Example Usage:

    Html(
      data: """
        <!--For a much more extensive example, look at example/main.dart-->
        <div>
          <h1>Demo Page</h1>
          <p>This is a fantastic nonexistent product that you should buy!</p>
          <h2>Pricing</h2>
          <p>Lorem ipsum <b>dolor</b> sit amet.</p>
          <h2>The Team</h2>
          <p>There isn't <i>really</i> a team...</p>
          <h2>Installation</h2>
          <p>You <u>cannot</u> install a nonexistent product!</p>
          <!--You can pretty much put any html in here!-->
        </div>
      """,
      //Optional parameters:
      padding: EdgeInsets.all(8.0),
      backgroundColor: Colors.white70,
      defaultTextStyle: TextStyle(fontFamily: 'serif'),
      onLinkTap: (url) {
        // open url in a webview
      },
      customRender: (node, children) {
        if(node is dom.Element) {
          switch(node.localName) {
            case "video": return Chewie(...);
            case "custom_tag": return CustomWidget(...);
            // You can also pass node children to another Html widget
            case "another_custom_tag": 
                return AnotherCustomWidget(child: Html.fromNodeList(nodeList: node.nodes));
          }
        }
      },
    )