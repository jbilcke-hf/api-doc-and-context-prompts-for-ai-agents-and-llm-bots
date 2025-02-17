seo 0.0.10 ![copy "seo: ^0.0.10" to clipboard](/static/hash-emgk9in0/img/content-copy-icon.svg "Copy "seo: ^0.0.10" to clipboard")

seo: ^0.0.10 copied to clipboard


======================================================================================================================================================================

Published 15 days ago Dart 3 compatible

SDK[Flutter](/packages?q=sdk%3Aflutter "Packages compatible with Flutter SDK")

Platform[Android](/packages?q=platform%3Aandroid "Packages compatible with Android platform")[iOS](/packages?q=platform%3Aios "Packages compatible with iOS platform")[Linux](/packages?q=platform%3Alinux "Packages compatible with Linux platform")[macOS](/packages?q=platform%3Amacos "Packages compatible with macOS platform")[web](/packages?q=platform%3Aweb "Packages compatible with Web platform")[Windows](/packages?q=platform%3Awindows "Packages compatible with Windows platform")

![liked status: inactive](/static/hash-emgk9in0/img/like-inactive.svg)![liked status: active](/static/hash-emgk9in0/img/like-active.svg)116

→

### Metadata

Flutter package for enabling SEO (meta, body tag) support on Web.

More...

*   Readme
*   [Changelog](/packages/seo/changelog)
*   [Example](/packages/seo/example)
*   [Installing](/packages/seo/install)
*   [Versions](/packages/seo/versions)
*   [Scores](/packages/seo/score)

flutter\_seo [#](#flutter_seo)
==============================

[![pub package](https://img.shields.io/pub/v/seo.svg)](https://pub.dartlang.org/packages/seo)

Flutter package for enabling SEO (meta, body tag) support on Web. The package listens to widget tree changes and converts `Seo.text(...)`, `Seo.image(...)`, `Seo.link(...)`, `Seo.head(...)` widgets into html document tree. [View Demo](#demo)

Getting Started [#](#getting-started)
-------------------------------------

To use this plugin, add `seo` as a [dependency in your pubspec.yaml file](https://flutter.io/platform-plugins/).

    dependencies:
      seo: ^0.0.10
    

copied to clipboard

Use `usePathUrlStrategy()` to ensure that Google recognizes each URL as a distinct page. Failure to do so may result in Google perceiving all URLs as the same page. For additional details, refer to [this video](https://www.youtube.com/watch?v=vow-m6R-YHo).

    void main() {
      usePathUrlStrategy();
      runApp(App());
    }
    

copied to clipboard

  
Wrap your app within `SeoController` which will handle listening to widget tree changes and updating the html document tree. In case your app has authorization and user is logged in you can disable the controller by `enabled: false` as it's redundant to update the html document tree at that state.

    import 'package:seo/seo.dart';
    
    void main() {
      usePathUrlStrategy();
      runApp(const App());
    }
    
    class App extends StatelessWidget {
      const App({super.key});
    
      @override
      Widget build(BuildContext context) {
        return SeoController(
          enabled: true,
          tree: WidgetTree(context: context),
          child: MaterialApp(...),
        );
      }
    }
    

copied to clipboard

  
There's two available SeoTree implementations:

*   **WidgetTree (recommended)** - based on traversing widget tree, while it's bit slower than SemanticsTree it's production ready and doesn't have any blocking Flutter SDK issues.
*   **SemanticsTree (`experimental`)** - based on traversing semantic data node tree. Does traverse the tree faster but doesn't support `Seo.head(...)`, `Seo.text(style: ...)`, `Seo.link(rel: ...)`, `Seo.html(html: ...)`

Sample Usage [#](#sample-usage)
-------------------------------

You should wrap all your SEO required widgets accordingly within `Seo.text(...)`, `Seo.image(...)`, `Seo.link(...)` and SEO required pages within `Seo.head(...)`. From personal experience it's more comfortable to create custom [AppText](https://github.com/krokyze/flutter_seo/blob/main/example/lib/widgets/app_text.dart), [AppImage](https://github.com/krokyze/flutter_seo/blob/main/example/lib/widgets/app_image.dart), [AppLink](https://github.com/krokyze/flutter_seo/blob/main/example/lib/widgets/app_link.dart), [AppHead](https://github.com/krokyze/flutter_seo/blob/main/example/lib/widgets/app_head.dart) base widgets and use those in the project.

#### Text

    Seo.text(
      text: 'Some text',
      child: ...,
    ); // converts to: <p>Some text</p>
    
    Seo.text(
      text: 'Some text',
      style: TextTagStyle.h1,
      child: ...,
    ); // converts to: <h1>Some text</h1>
    

copied to clipboard

#### Image

    Seo.image(
      src: 'http://www.example.com/image.jpg',
      alt: 'Some example image',
      child: ...,
    ); // converts to: <img src="http://www.example.com/image.jpg" alt="Some example image"/>
    

copied to clipboard

#### Link

    Seo.link(
      href: 'http://www.example.com',
      anchor: 'Some example',
      rel: 'nofollow', (optional)
      child: ...,
    ); // converts to: <a href="http://www.example.com" rel="nofollow"><p>Some example</p></a>
    

copied to clipboard

#### Html

    Seo.html(
      html: '<div>Some raw html</div>',
      child: ...,
    ); // converts to: <div>Some raw html</div>
    

copied to clipboard

#### Head

    Seo.head(
      tags: [
        MetaTag(name: 'title', content: 'Flutter SEO Example'),
        LinkTag(rel: 'canonical', href: 'http://www.example.com'),
      ],
      child: ...,
    ); // converts to: <meta name="title" content="Flutter SEO Example"><link rel="canonical" href="http://www.example.com" />
    

copied to clipboard

> **Warning**: Open Graph (og:title, og:description, etc.) and Twitter Card (twitter:title, twitter:description, etc.) will not work. [Read more](#supporting-open-graph-twitter-card-tags).

Tips [#](#tips)
---------------

#### Supporting Open Graph, Twitter Card tags

Facebook, Twitter, etc. simply load index.html and don't execute any JavaScript that webpage contains so we're not able to change meta tags within Dart code. The proposed solution is to create simple Server-Side Rendering which would add Open Graph, Twitter Card tags within `index.html` before returning it to Client.

Demo [#](#demo)
---------------

View demo here: [https://flutter-seo.netlify.app](https://flutter-seo.netlify.app)

#### PageSpeed Insights

[![Mobile](https://img.shields.io/badge/Mobile-lightgray?style=flat-square)![Performance ≈56](https://img.shields.io/badge/Performance-%E2%89%8855-important?style=flat-square)![Accessibility 87](https://img.shields.io/badge/Accessibility-87-important?style=flat-square)![Best Practices 100](https://img.shields.io/badge/Best_Practices-100-success?style=flat-square)![SEO 100](https://img.shields.io/badge/SEO-100-success?style=flat-square)  
![Desktop](https://img.shields.io/badge/Desktop-lightgray?style=flat-square)![Performance ≈85](https://img.shields.io/badge/Performance-%E2%89%8885-important?style=flat-square)![Accessibility 88](https://img.shields.io/badge/Accessibility-88-important?style=flat-square)![Best Practices 100](https://img.shields.io/badge/Best_Practices-100-success?style=flat-square)![SEO 100](https://img.shields.io/badge/SEO-100-success?style=flat-square)](https://pagespeed.web.dev/report?url=https://flutter-seo.netlify.app)

#### Google Search

Landing page has been indexed and does appear in [Search](https://www.google.com/search?q=flutter+seo+green+papaya+salad)

Remaining pages have `Discovered - currently not indexed` status. I am investigating why.

[

116

likes

140

points

18.5k

downloads



](/packages/seo/score)

### Publisher

unverified uploader

### Weekly Downloads

2024.07.28 - 2025.02.09

### Metadata

Flutter package for enabling SEO (meta, body tag) support on Web.

[Repository (GitHub)](https://github.com/krokyze/flutter_seo)  

### Documentation

[API reference](/documentation/seo/latest/)  

### License

![](/static/hash-emgk9in0/img/material-icon-balance.svg)MIT ([license](/packages/seo/license))

### Dependencies

[flutter](https://api.flutter.dev/), [rxdart](/packages/rxdart ">=0.27.5 <0.29.0"), [web](/packages/web "^1.1.0")

### More

[Packages that depend on seo](/packages?q=dependency%3Aseo)

{"@context":"http\\u003a\\u002f\\u002fschema.org","@type":"SoftwareSourceCode","name":"seo","version":"0.0.10","description":"seo - Flutter package for enabling SEO \\u0028meta, body tag\\u0029 support on Web.","url":"https\\u003a\\u002f\\u002fpub.dev\\u002fpackages\\u002fseo","dateCreated":"2022-11-14T00\\u003a02\\u003a08.422549Z","dateModified":"2025-01-26T13\\u003a08\\u003a23.762626Z","programmingLanguage":"Dart","image":"https\\u003a\\u002f\\u002fpub.dev\\u002fstatic\\u002fimg\\u002fpub-dev-icon-cover-image.png","license":"https\\u003a\\u002f\\u002fpub.dev\\u002fpackages\\u002fseo\\u002flicense"}