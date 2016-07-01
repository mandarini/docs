---
$title: amp-analytics
$order: 3
$category: Reference
$parent: /content/docs/extended.md
$path: /docs/reference/extended/amp-analytics.html
$localization:
  path: /{locale}/docs/reference/extended/amp-analytics.html
  locales:
---

<!---
Copyright 2015 The AMP HTML Authors. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS-IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->



<table>
  <tr>
    <td class="col-fourty"><strong>Description</strong></td>
    <td>Capture analytics data from an AMP document.</td>
  </tr>
  <tr>
    <td class="col-fourty"><strong>Availability</strong></td>
    <td>Stable</td>
  </tr>
  <tr>
    <td class="col-fourty"><strong>Required Script</strong></td>
    <td><code>&lt;script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js">&lt;/script></code></td>
  </tr>
  <tr>
    <td class="col-fourty"><strong>Examples</strong></td>
    <td><a href="https://github.com/ampproject/amphtml/blob/master/examples/analytics.amp.html">analytics.amp.html</a></td>
  </tr>
</table>

## <a name="behavior"></a>Behavior

The `<amp-analytics>` element is used to measure activity on an AMP document. The details concerning what is measured and how that data is sent to an analytics server is specified in a JSON configuration object. It comes pre-configured to support many [analytics vendors](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/#analytics-vendors) out of the box.

For example, the following `<amp-analytics>` element is configured to send a request to `https://example.com/analytics`
when the document is first loaded, and each time an `<a>` tag is clicked:

[sourcecode:html]
<amp-analytics>
<script type="application/json">
{
  "requests": {
    "pageview": "https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}",
    "event": "https://example.com/analytics?eid=${eventId}&elab=${eventLabel}&acct=${account}"
  },
  "vars": {
    "account": "ABC123"
  },
  "triggers": {
    "trackPageview": {
      "on": "visible",
      "request": "pageview"
    },
    "trackAnchorClicks": {
      "on": "click",
      "selector": "a",
      "request": "event",
      "vars": {
        "eventId": "42",
        "eventLabel": "clicked on a link"
      }
    }
  }
}
</script>
</amp-analytics>
[/sourcecode]

## Analytics vendors

By specifying the name of an analytics vendor with the `type` attribute you can quickly configure `amp-analytics` to use the respective product. Additional configuration (such as your user id) may still be necessary.

Here's an example of usage of `type` for a provider called XYZ:

[sourcecode:html]
<amp-analytics type="XYZ"> ... </amp-analytics>
[/sourcecode]

### Adobe Analytics

Type attribute value: `adobeanalytics`

Adds support for Adobe Analytics. More details for adding Adobe Analytics support can be found at [marketing.adobe.com](https://marketing.adobe.com/resources/help/en_US/sc/implement/accelerated-mobile-pages.html).

### AT Internet

Type attribute value: `atinternet`

Adds support for AT Internet. More details for adding AT Internet support can be found at [developers.atinternet-solutions.com](http://developers.atinternet-solutions.com/javascript-en/advanced-features-javascript-en/accelerated-mobile-pages-amp-javascript-en/).

### Burt

Type attribute value: `burt`

Adds support for Burt. Additionally, the `trackingKey` variable must be specified. It's also possible to specify the optional variables `category` and `subCategory`.

### Chartbeat

Type attribute value: `chartbeat`

Adds support for Chartbeat. More details for adding Chartbeat support can be found at [support.chartbeat.com](http://support.chartbeat.com/docs/integrations.html#amp).

### ColAnalytics

Type attribute value: `colanalytics`

Adds support for ColAnalytics. Additionally, need the value for `id`.

### Clicky Web Analytics

Type attribute value: `clicky`

Adds support for Clicky Web Analytics. More details for adding Clicky support can be found at [clicky.com](https://clicky.com/help/apps-plugins).

### comScore

Type attribute value: `comscore`

Adds support for comScore Unified Digital Measurement™ pageview analytics. Requires defining *var* `c2` with comScore-provided *c2 id*.

### Google Analytics

Type attribute value: `googleanalytics`

Adds support for Google Analytics. More details for adding Google Analytics support can be found at [developers.google.com](https://developers.google.com/analytics/devguides/collection/amp-analytics/).

### INFOnline / IVW

Type attribute value: `infonline`

Adds support for [INFOnline](https://www.infonline.de) / [IVW](http://www.ivw.de). Requires a copy of [amp-analytics-infonline.html](https://3p.ampproject.net/custom/amp-analytics-infonline.html) on a different subdomain than the including AMP file ([why?](https://github.com/ampproject/amphtml/blob/master/spec/amp-iframe-origin-policy.md)). The file must be served via HTTPS. Example: if your AMP files are hosted on `www.example.com`, then `amp-analytics-infonline.html` needs to be on another subdomain such as `iframe.example.com` or `assets.example.com`.

Additionally, the following variables must be defined:

* `st`: Angebotskennung
* `co`: comment
* `cp`: code
* `url`: HTTPS location of `amp-analytics-infonline.html`

More details for adding INFOnline / IVW support can be found at [www.infonline.de](https://www.infonline.de/downloads/web-mew-und-ctv/).

### Krux

Type attribute value: `krux`

Adds support for Krux.  Configuration details can be found at [help.krux.com](https://konsole.zendesk.com/hc/en-us/articles/216596608).

### Linkpulse

Type attribute value: `linkpulse`

Adds support for Linkpulse. Configuration details can be found at [docs.linkpulse.com](http://docs.linkpulse.com)

### Lotame

Type attribute value: `lotame`

Adds support for Lotame.  More information and configuration details can be found at [mylotame.force.com](https://mylotame.force.com/s/article/Google-AMP).

### Médiamétrie

Type attribute value: `mediametrie`

Adds support for Médiamétrie tracking pages. Requires defining *var* `serial`. Vars `level1` to `level4` are optional.

### OEWA

Type attribute value: `oewa`

There is a variation called `oewadirect` wich does not use iframe-ping solution - and has a better client detection, by using AMP CLIENT_ID, this is currently EXPERIMENTAL,
and as of today (01.07.2015) prohibited by the OEWA - as it does not use `oewa2.js`

Adds support for [OEWA](https://www.oewa.at). Requires a copy of [amp-analytics-oewa.html](http://www.oewa.at/fileadmin/downloads/amp-analytics-oewa.html) on a different subdomain than the including AMP file ([why?](https://github.com/ampproject/amphtml/blob/master/spec/amp-iframe-origin-policy.md)). The file must be served via HTTPS. Example: if your AMP files are hosted on `www.example.com`, then `amp-analytics-oewa.html` needs to be on another subdomain such as `oewa-amp.example.com`.

Additionally, the following variables must be defined:

in vars-section:

* `s`: offer
* `cp`: categorypath

in requests-section:

* `url`: HTTPS location of `amp-analytics-oewa.html`

More details for adding ÖWA, support can be found [here](http://www.oewa.at/basic/implementierung).

### Parsely

Type attribute value: `parsely`

Adds support for Parsely. Configuration details can be found at [parsely.com/docs](http://parsely.com/docs/integration/tracking/google-amp.html).

##### Piano

Type attribute value: `piano`

Adds support for Piano.  Configuration details can be found at [vx.piano.io](http://vx.piano.io/javascript-tracking-amp).

### Quantcast Measurement

Type attribute value: `quantcast`

Adds support for Quantcast Measurement. More details for adding Quantcast Measurement can be found at [quantcast.com](https://www.quantcast.com/help/guides/)

### SOASTA mPulse

Type attribute value: `mpulse`

Adds support for [SOASTA mPulse](https://www.soasta.com/mPulse). Configuration details can be found at [docs.soasta.com](http://docs.soasta.com/).

### SimpleReach

Type attribute value: `simplereach`

Adds support for SimpleReach.  Configuration details can be found at [simplereach.com/docs](http://docs.simplereach.com/dev-guide/implementation/google-amp-implementation)

### Snowplow Analytics

Type attribute value: `snowplow`

Adds support for Snowplow Analytics. More details for adding Snowplow Analytics support can be found at [github.com/snowplow/snowplow/wiki](https://github.com/snowplow/snowplow/wiki/Google-AMP-Tracker).

### Webtrekk

Type attribute value: `webtrekk`

Adds support for Webtrekk. Configuration details can be found at [supportcenter.webtrekk.com](https://supportcenter.webtrekk.com/en/public/amp-analytics.html).

## <a name="attributes"></a>Attributes

  - `type` See [Analytics vendors](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/#analytics-vendors)
  - `config` Optional attribute. This attribute can be used to load a configuration from a specified remote URL. The URL specified here should use https scheme. See also `data-include-credentials` attribute below. The URL may include [AMP URL vars](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/../../spec/amp-var-substitutions.md).

    [sourcecode]
    <amp-analytics config="https://example.com/analytics.config.json"></amp-analytics>
    [/sourcecode]
    The response must follow the [AMP CORS security guidelines](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/../../spec/amp-cors-requests.md).

  - `data-credentials` Optional attribute. If set to `include` turns on the ability to read and write cookies on the request specified via `config` above.
  - `data-consent-notification-id` Optional attribute. If provided, the page will not process analytics requests until an [amp-user-notification](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/../../extensions/amp-user-notification/amp-user-notification.md) with
    the given HTML element id is confirmed (accepted) by the user.

## Configuration

Configuration may be specified inline (as shown in the example above) or fetched remotely by specifying a URL in the
`config` attribute. Additionally, built-in configuration for popular analytics vendors can be selected using
the `type` attribute.

If configuration data from more than one of these sources is used, the configuration objects (vars, requests and triggers) will
be merged together such that **(i) remote configuration takes precedence over inline configuration and (ii) inline configuration
takes precedence over vendor configuration**.

The `<amp-analytics>` configuration object uses the following format:

[sourcecode:javascript]
{
  "requests": {
    request-name: request-value,
    ...
  },
  "vars": {
    var-name: var-value,
    ...
  },
  "triggers": {
    trigger-name: trigger-object,
    ...
  },
  "transport": {
    "beacon": *boolean*,
    "xhrpost": *boolean*,
    "image": *boolean*
  }
}
[/sourcecode]
### Requests
The `requests` attribute specifies the URLs used to transmit data to an analytics platform. The `request-name` is used
in the trigger configuration to specify what request should be sent in response to a pariticular event. The `request-value`
is an https URL. These values may include placeholder tokens that can reference other requests or variables.

[sourcecode:javascript]
"requests": {
  "base": "https://example.com/analytics?a=${account}&u=${canonicalUrl}&t=${title}",
  "pageview": "${base}&type=pageview",
  "event": "${base}&type=event&eventId=${eventId}"
}
[/sourcecode]

### Vars

`amp-analytics` defines many basic variables that can be used in requests. A list of all such variables is available in the  [`amp-analytics` Variables Guide](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/./analytics-vars.md). In addition, all of the variables supported by [AMP HTML Substitutions Guide](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/../../spec/amp-var-substitutions.md) are also supported.

The `vars` attribute in the configuration can be used to define new key-value pairs or override existing variables that can be referenced in `request` values. New variables are commonly used to specify publisher specific information.  Arrays can be used to specify a list of values that should be URL encoded separately while preserving the comma delimiter.

[sourcecode:javascript]
"vars": {
  "account": "ABC123",
  "countryCode": "tr",
  "tags": ["Swift,Jonathan", "Gulliver's Travels"]
}
[/sourcecode]

### Triggers
The `triggers` attribute describes when an analytics request should be sent. It contains a key-value pair of trigger-name and
 trigger-configuration. Trigger name can be any string comprised of alphanumeric characters (a-zA-Z0-9). Triggers from a
 configuration with lower precedence are overridden by triggers with the same names from a configuration with higher precedence.

  - `on` (required) The event to listener for. Valid values are `click`, `scroll`, `timer`, and `visible`.
  - `request` (required) Name of the request to send (as specified in the `requests` section).
  - `vars` An object containing key-value pairs used to override `vars` defined in the top level config, or to specify
    vars unique to this trigger.

  - `selector` (required when `on` is set to `click`) This configuration is used on conjunction with the `click` trigger. Please see below for details.
  - `scrollSpec` (required when `on` is set to `scroll`) This configuration is used on conjunction with the `scroll` trigger. Please see below for details.
  - `timerSpec` (required when `on` is set to `timer`) This configuration is used on conjunction with the `timer` trigger. Please see below for details.

#### Page visible trigger (`"on": "visible"`)
Use this configuration to fire a request when the page becomes visible. No further configuration is required.

[sourcecode:javascript]
"triggers": {
  "defaultPageview": {
    "on": "visible",
    "request": "pageview"
  }
}
[/sourcecode]

#### Click trigger (`"on": "click"`)
Use this configuration to fire a request when a specified element is clicked. Use `selector` to control which elements will cause this request to fire:

  - `selector` A CSS selector used to refine which elements should be tracked. Use value `*` to track all elements.

    [sourcecode:javascript]
    "triggers": {
      "anchorClicks": {
        "on": "click",
        "selector": "a",
        "request": "event",
        "vars": {
          "eventId": 128
        }
      }
    }
    [/sourcecode]

#### Scroll trigger (`"on": "scroll"`)
Use this configuration to fire a request under certain conditions when the page is scrolled. Use `scrollSpec` to control when this will fire:

  - `scrollSpec` This object can contain `verticalBoundaries` and `horizontalBoundaries`. At least one of the two properties is required for a scroll event to fire. The values for both of the properties should be arrays of numbers containing the boundaries on which a scroll event is generated. For instance, in the following code snippet, the scroll event will be fired when page is scrolled vertically by 25%, 50% and 90%. Additionally, the event will also fire when the page is horizontally scrolled to 90% of scroll width. To keep the page performant, the scroll boundaries are rounded to the nearest multiple of `5`.


    [sourcecode:javascript]
    "triggers": {
      "scrollPings": {
        "on": "scroll",
        "scrollSpec": {
          "verticalBoundaries": [25, 50, 90],
          "horizontalBoundaries": [90]
        },
        "request": "event"
      }
    }
    [/sourcecode]

#### Timer trigger (`"on": "timer"`)
Use this configuration to fire a request on a regular time interval. Use `timerSpec` to control when this will fire:

  - `timerSpec` Specification for triggers of type `timer`. The timer will trigger immediately and then at a specified interval thereafter.
    - `interval` Length of the timer interval, in seconds.
    - `maxTimerLength` Maximum duration for which the timer will fire, in seconds.

    [sourcecode:javascript]
    "triggers": {
      "pageTimer": {
        "on": "timer",
        "timerSpec": {
          "interval": 10,
          "maxTimerLength": 600
        },
        "request": "pagetime"
      }
    }
    [/sourcecode]

#### Access triggers (`"on": "amp-access-*"`)

AMP Access system issues numerous events for different states in the access flow. See [amp-access-analytics.md](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/../amp-access/amp-access-analytics.md) for details.

### Transport
The `transport` attribute specifies how to send a request. The value is an object with fields that
indicate which transport methods are acceptable.

  - `beacon` Indicates [`navigator.sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)
     can be used to transmit the request. This will send a POST request, with credentials, and an empty body.

  - `xhrpost` Indicates `XMLHttpRequest` can be used to transmit the request. This will send a POST
     request, with credentials, and an empty body.

  - `image` Indicates the request can be sent by generating an `Image` tag. This will send a GET request.

If more than one of the above transport methods are enabled, the precedence is `beacon` > `xhrpost` > `image`. Only one transport method will be used, and it will be the highest precedence one that is permitted and available. If the client's user agent does not support a method, the next highest precedence method enabled will be used. By default, all three methods above are enabled.

In the example below, `beacon` and `xhrpost` are set to `false`, so they will not be used even though they have higher precedence than `image`. `image` would be set `true` by default, but it is explicitly declared here. If the client's user agent supports the `image` method, then it will be used; otherwise, no request would be sent.

[sourcecode:javascript]
"transport": {
  "beacon": false,
  "xhrpost": false,
  "image": true
}
[/sourcecode]


### Extra URL Params

The `extraUrlParams` attribute specifies additional parameters to append to the query string of a request URL via the usual "&foo=baz" convention.

Here's an example that would append `&a=1&b=2&c=3` to a request:

[sourcecode:javascript]
"extraUrlParams": {
  "a": "1",
  "b": "2",
  "c": "3"
}
[/sourcecode]

The `extraUrlParamsReplaceMap` attribute specifies a map of keys and values that act as parameters to String.replace() to preprocess keys in the extraUrlParams configuration. For example, if an `extraUrlParams` configuration defines `"page.title": "The title of my page"` and the `extraUrlParamsReplaceMap` defines `"page.": "_p_"`, then `&_p_title=The%20title%20of%20my%20page%20` will be appended to the request.

`extraUrlParamsReplaceMap` is not required to use `extraUrlParams`. If `extraUrlParamsReplaceMap` is not defined, then no string substitution will happens and the strings defined in `extraUrlParams` are used as-is.

## Validation

See [amp-analytics rules](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/0.1/validator-amp-analytics.protoascii) in the AMP validator specification.