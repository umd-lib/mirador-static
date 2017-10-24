# mirador-static

Current Mirador version: [v2.1.2-umd-1.3](https://github.com/umd-lib/mirador/releases/tag/v2.1.2-umd-1.3).

## Quick Start

To prevent cross-origin request errors, please clone this repo to a local web server and run via HTTP.

### Running with Browsersync

[Browsersync](https://www.browsersync.io/) is a simple web server for front-end development. It requires NodeJS to run.

```
# install Browsersync
npm install -g browser-sync

# clone mirador-static and start Browsersync
git clone git@github.com:umd-lib/mirador-static.git
cd mirador-static
browser-sync start --server
```

Mirador Static will be running at <http://localhost:3000/mirador.html>.

**Note:** If you have another process (e.g., a Rails app) already listening on localhost port 3000, Browsersync will try ports 3001, 3002, etc., until it finds an open one.

## Query Parameters

Mirador Static accepts the following query parameters:

* manifest
* iiifURLPrefix
* q

If **manifest** is an IIIF ID only, then **iiifURLPrefix** should also be provided. In this case, the manifest URI will be `{iiifURLPrefix}{manifest}/manifest`. (Note the appended `/manifest`; this is only added if **iiifURLPrefix** is set.)

The **q** parameter, if present, is appended as-is to the manifest URI. This is to enable the IIIF Presentation API backend to support returning hit highlight annotation lists or other dynamic content based on a user query.

## Annotation Styles

`annotationTypeStyles` supports multiple annotation styles, hovering styles, and ability to show or hide annotation tooltips.  

Annotations with the types `umd:Hits`, `umd:Article`, `umd:ArticleSelected`, and `umd:Line` will each have a different appearance according to the settings of `'annotationTypeStyles'` in [site.js](js/site.js):

```js
'annotationTypeStyles': {
  'umd:Article': {
    'strokeColor': 'rgba(255, 255, 255, 0)',
    'fillColor': 'green',
    'fillColorAlpha': 0.08,
    'hoverColor': 'rgba(255, 255, 255, 0.2)',
    'hoverFillColor': 'green',
    'hoverFillColorAlpha': 0.4,
    'hideTooltip': true
  },
  ...
}
```

## Annotations

[Web Annotations](https://www.w3.org/TR/annotation-model/) are used to implement both the full-text blocks and the search hit highlights.

An example Web Annotation, in JSON-LD:

```json
{
  "@id": "P1_TL00160",
  "@type": [
    "oa:Annotation",
    "umd:Hits"
  ],
  "resource": [
    {
      "@type": "cnt:ContentAsText",
      "format": "text/plain",
      "chars": "College Park"
    }
  ],
  "on": {
    "@type": "oa:SpecificResource",
    "selector": {
      "@type": "oa:FragmentSelector",
      "value": "xywh=1536,5408,260,33"
    },
    "full": "0002.xml"
  },
  "motivation": "sc:painting"
},
```

## License

See the [LICENSE](LICENSE.md) file for license rights and limitations (Apache 2.0).
