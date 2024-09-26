# Fundamentals of Web Performance, v2

With [Todd Gardner](https://toddhgardner.com/). :)

GitHub repository: <https://github.com/toddhgardner/fundametals-of-web-performance>
Slides part 1: <https://static.frontendmasters.com/resources/2024-09-26-web-perf-v2/web-perf-v2-slides_part1.pdf>
Slides part 2: <https://static.frontendmasters.com/resources/2024-09-26-web-perf-v2/web-perf-v2-slides_part2.pdf>

Web performance definition:

> The **speed** and **efficiency** with wh ich a website loads, renders, and
> responds to interactions from the visitors.

What does slow feel like?

- Waiting for the page to load
- Elements jump around
- Delays to click input
- Slow images/videos
- Laggy scrolls/animations

## Why is web perf important?

- UX
- SEO
- Advertising

### UX

> So your users don't try to strangle you.

> The key to happiness is to _lower expectations_.

IEEE response times: need some sort of response within 2s of request.

- Instant: <= .01s (100ms)
- Uninterrupted flow: <= 1s
- Break flow & feel frustration: 10s

- 40% abandon site at 3s
- 75% that experience "slow" will _not_ return

### SEO

Helping search engines understand and _rank_ your content.

> Search ranking change that incorporates _page experience metrics_. We will
> introduce a new signal in addition to Core Web Vitals.
> <br> &mdash; Google, 2020

tl;dr You need to be _fast_ to _rank well_.

### (Online) Advertising

> 65% perf improvement reduced bounce rate 20% and 200% time on page.

### Revenue

> 100ms improvement up to 1% incremental sales/revenue.

Author's note: I've seen this before on [instant.page](https://instant.page/).

## Measuring web perf

- Legacy metrics
- Core Web Vitals (CWT)
- more metrics
- how to capture metrics
- browser supports
- waterfall charts & flame charts

How do we measure "fast"?

### Waterfall charts

Measures time, usually milliseconds or microseconds.

- Blue: HTML
- Purple: CSS
- Yellow: JS
- Green: Images

### Legacy metrics

`DOMContentLoaded`: the HTML downloaded and deferred scripts have executed.

The structure of the page is done, but images/media may not be displayed.

`Load`: the HTML and all **known** resources have been downloaded and rendered,
_except_ those that are lazy-loaded.

The document is _ready_ and update and reporting tasks can begin.

The **problem** with legacy metrics:

- What `load` _originally_ meant: the document is ready e.g. `$(document).ready()`
- In 2010 client-side rendering happened: Backbone.js, Knockout, jQuery UI
- Users are more likely to stay on a fast website &mdash; Google
- How do compare foo.com to bar.com in terms of fastness?

### Core Web Vitals

Google's Core Web Vitals:

1. Largest Contentful Paint (LCP): how fast your site visibly loads
2. Cumulative Layout Shift (CLS): how smooth things load
3. Interaction to Next Paint (INP): how quickly users can interact

> "Search ranking incorporates the \[CWV] page experience metrics"

#### Largest Contentful Paint (LCP)

How fast our site visibly loads _the most important_ element.

Google doesn't trust you.

What is the largest?

- `<img>`
- `<video>`
- CSS `background-image`
- text elements

Rules:

- opacity > 0 (cannot be invisible)
- size < 100% (cannot be whole page)
- low entropy images < 0.05

WTF is entropy?

Bits per pixel shown. "How much data density are we showing in this image?"

Unencoded size / pixel size => entropy

Calculate in JS:

```js
console.table(
  [...document.images].map((img) => {
    const entry = performance.getEntriesByName(img.currentSrc)[0];
    const bytes = (entry?.encodedBodySize * 8);
    const pixels = (img.width * img.height);
    return { src: img.currentSrc, bytes, pixels, entropy: (bytes / pixels) };
  })
)
```

LCP considerations:

- Stops after first user interaction
- Good: <= 2.5s
- Needs improvement: <= 4s
- Poor: > 4s

#### Cumulative Layout Shift (CLS)

How smooth & _predictably_ elements load into the page.

Layout shift value: impact fraction * distance fraction

The score is dependent on the _size of the user's viewport_ i.e. mobile devices
are typically much taller with mostly vertical layouts.

And the keyword here is _cumulative_ i.e. the sum of all layout shifts.

CLS considerations:

If a layout shift happens within 500s of a user interaction it _doesn't count_.

- Good: < 0.1
- Needs improvement: < 0.25
- Poor: > .25

#### Flame charts (needed to understand INP)

Still measuring time in milliseconds and microseconds of the browser execution.

- Gray: browser tasks
- Blue: parse HTML
- Pink: layout & paint events
- Yellow: top-level JS eval & compile (passthrough)
- White: JS execution (working)
- Green: extensions

The main thread: the single thread of work the browser has for handling user
events, layout, paint, and running JavaScript.

#### Interaction to Next Paint (INP)

How quickly users can _interact_.

Interactions are everything _except_ a scroll.

What's the "next paint"?

INP considerations:

- There might not be an interaction
- We don't know the worst until it's over
- Heavily influenced by device capability

- Good: < 200ms
- Needs improvement: < 500ms
- Poor: > 500ms

#### First Input Delay (FID)

In memory 2020&ndash;2024 (replaced by INP).

Essentially, measure the _first_ INP.

Problems with FID:

- Emphasized _blocking time_ over _processing time_
- Users interact _many_ times

### More (performance) metrics

**Time to First Byte (TTFB)**: how quickly your _host_ responds.

- Good: < 800ms
- Needs improvement: < 1800ms
- Poor: > 1800ms

TTFB _will_ impact LCP: if server delays are felt on the client too.

**First Contentful Paint (FCP)**: how fast your site visibly loads _something_.

- Good: < 1.8s
- Needs improvement: < 3s
- Poor: > 3s

### Capturing metrics

Performance API & PerformanceObserver API.

Performance API:

- `performance.now()` (also `performance.timeOrigin`)
- `performance.getEntries()` (timing info)
- `performance.mark()`
- `performance.measure()`

Observer effect: disturbance of observed system by the act of observation.

Google's `web-vitals` JS package.

### Browser support

More specifically, browser engines:

Blink:

- Chrome
- Edge
- Opera
- Samsung
- Brave
- Arc

Webkit:

- Safari
- Mobile Safari
- (Chrome \[or anything, really] on iOS)

Gecko:

- Firefox

WebKit supports no CWV. Gecko only supports LCP.

## Tests & tools

Lab test: close to host (maybe even same network).

Synthetic test: lives in the cloud, still automated.

Field test: real user data reported back.

Lab is easier, field is more accurate.

Lab is diagnostic, field is experience.

Improve lab data:

- Mobile vs desktop
- Network conditions
- Processing power

Devtool tips:

- Small laptop (1366 x 768) custom device
- Coffee shop WiFi: 10Mb/s down, 4Mb/s up, 50ms latency

### Chrome User Experience Report (CrUX)

- field data
- logged in Chrome users
- top 1M public sites
- anonymous & public
- 28 day rolling average

Request Metrics tool to check CrUX data: <https://requestmetrics.com/resources/tools/crux/>

### Real User Monitoring (RUM)

Request Metrics. :)

## Setting goals

How fast is fast enough? _Fast_ is subjective user perception.

Perceived performance:

1. People want to _start_
2. Bored waits feel slower
3. Anxious waits feel slower
4. Unexplained waits feel slower
5. Uncertain waits feel slower
6. People will wait for _value_

Who gets to decide? Not you.

1. User experience
2. Competitors
3. SEO page rank

Follow the business metrics:

- Bounce rate
- Session time
- Add to cart rate
- Cart abandonment
- Conversion rate

Compared to competitors, you need to be _20% faster_ because generally that's
what it takes to be noticeable.

Author note: interesting to see the general smallest mobile width is 360px these
days: <https://gs.statcounter.com/screen-resolution-stats/mobile/worldwide>

## Improving

This is where part 2 of slides start.

Focus on the _easiest_ fixes for your _worst_ metrics from _real user data_.

You shouldn't try to do everything. Sometimes it's fast enough.

Do. Fewer. Things.

### Time to First Byte (TTFB)

> How quickly the _host_ responds.

Testing a Minneapolis -> Amsterdam connection w/ devtools handicapping too.

Tactics:

1. Compress HTTP resources
2. Efficient protocols
3. Host capacity
4. Host proximity (location)

#### Compress HTTP resources

TIL Gzip is an order of magnitude worse than Brotli when compressing HTML. The
results for CSS & JS are comparable though. I'm curious why.

#### Efficient protocols

HTTP/1.1 vs HTTP/2 vs HTTP/3.

HTTP/3 uses QUIC which is UDP vs TCP.

TCP has SYN -> SYN/ACK -> ACK. UDP doesn't have that builtin reliability.

HTTP/3 drawbacks

- requires HTTPS (so does HTTP/2)
- UDP networking
- difficult to debug e.g. curl can't make a HTTP/3 request

#### Host capacity

Right-size your host for your workload.

#### Host proximity

Put your hosts close to your users.

Minneapolis -> Amsterdam is ~117ms for network hops.

Completely on the ops side. [Bunny](https://bunny.net/) is the rec.

### First Contentful Paint (FCP)

> How fast your site visibly loads _something_.

Tactics:

1. Remove sequence chains
2. Preload resources
3. Lazy load resources

#### Remove sequence chains

Collapse dependencies

CSS and fonts are **render blocking**. They prevent the page from rendering
until complete.

CSS `@import` and `@font-face` no bueno.

Easy fix: concat & minify CSS.

#### Preload resources

e.g. Google Fonts `<link rel="preconnect">` or `<link rel="preload" as="font">`

You can preload

- style
- script
- image
- font
- fetch

Fonts & fetch requires CORS e.g. `crossorigin` attribute.

#### Lazy load resources

Remove resources that _aren't_ on the **critical path**.

JS is **parser blocking**. It prevents parsing content, rendering, and main
execution.

`defer` vs `async`: async downloads lazy but executes blocking while defer
downloads lazy but executes _before_ `DOMContentLoaded`.

You almost _never_ want `async`. Multiple `defer` scripts will execute in the
order they appear.

`type="module"` is _always_ deferred.

`<script>` placement? `<head>` vs `<body>`? It _probably_ doesn't matter anymore.

### Largest Contentful Paint (LCP)

> How fast your site visibly loads the **most important** element.

Tactics:

1. (More) lazy loading
2. Eager loader
3. Optimize images

#### (More) lazy loading

Again, remove resources that _aren't_ on the **critical path**.

Via `loading="lazy"`.

#### Eager loading

Start loading **critical path** resources as soon as possible.

Similar to fonts:  `<link rel="preload" as="image">`

Very new: `fetchpriority="high` on `<img>`, `<script>`, and `<link>`s. No Gecko
support as of writing (2024SEPT).

#### Optimize images

Formats & responsive images. Plus, ensuring they're compressed.

Formats: JPEG, PNG, WebP, and AVIF. All are lossy except PNG.

Definitely prefer WebP & AVIF.

### Return User Experience (RUX???)

tl;dr caching.

### Cumulative Layout Shift (CLS)

> How _smooth_ elements load on to the page.

Tactics:

1. Layout hints

#### Layout hints

`width` and `height` for images which is used to calculate the aspect ratio.

Late content size: set explicit sizing if possible. Alteratively, paint _over_
existing content e.g. absolute positioning w/ z-index.

### Interaction to Next Paint (INP)

> How _quickly_ users can **interact**.

Tactics:

1. Yield the main thread

#### Yield the main thread

`setTimeout`:

- Schedule code to run in the future
- Allows other stuff to run

`requestAnimationFrame`:

- Schedules code to run just _before_ the next paint
- Useful for animations

## Performance Review

🙄

Why web perf important?

- UX
- SEO
- Advertising

Users will bounce and not come back on slow sites.

<https://bit.ly/speed-chex>

<https://bit.ly/sup-todd>
