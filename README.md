# Website Performance Optimization portfolio project

Challenge accepted, performance optimized!

## How to run
1. Extract the .zip archive
2. Start a local server in the new directory [eg. if python available run `python -m SimpleHTTPServer 3030` (Python 2.x) or `python -m http.server 3030` (Python 3.x)] using either Command Prompt or bash.
3. Start your favourite browser and visit localhost:3030

## List of optimizations

### Optimizations to `index.html` to achive a PageSpeed score < 90 (<X>)
- `media=print` attribute added to `print.css` head link.
- Put portrait mobile styles from `style.css` into a new file `mobile.css` and linked with `media` attribute of `(max-width: 480px)`.
- Resized and reduced quality (85%) on `pizzeria.jpg` to give `pizzeria-thumb.jpg`.
- Reduced number of critical resource requests by using a resized local image of `mobilewebdev.jpg` -> `mobilewebdev-thumb.jpg` instead of `src`'ing one of these monsters: https://lh6.ggpht.com/f_0W8h__3G99CWTjnMjD8BUKm7yp2-wJyApLtTwFoFtlal2ULf_JgHIsOQq2NiYfKOdMlXlMHDKNo5XVZLs=s100
- Removed Google Fonts request
- Inlined base styles from `css/style.css` into `index.html`.
- Eliminated Google Analytics code (sorry Paul...)
- Moved `perfmatters.js` script request to end of html `body`.


### Optimizations to `views/pizza.html` and `views/js/main.js` to achieve 60FPS
#### 1. `pizza.html`
 -  `pizzeria.jpg` sourcing `img` tag replaced by `picture` and `srcset`s using differently sized and 85% quality images.

#### 2. `main.js`
 - Wasteful `determineDx` renamed to `determineWidth` and simplified down to only the `switch` statement to return a percentage integer.
 - The new width of the pizza is determined just once before the for-loop of `changePizzaSizes` by `var newwidth = determineWidth(size) + '%';`.
 - Call to `updatePositions` from window scroll listener wrapped in a `requestAnimationFrame`. Complementary call to self using `requestAnimationFrame` added to end of `updatePositions`.
 - Insane layout thrashing via looped querying of `document.body.scrollTop` prevented by moving this to a single variable assignment outside for-loop (`scrollToTop`).

### Other
- Similar optimizations that were applied to `index.html` in root folder also applied to the other linked html pages.
- Only one request of Google Fonts (root `index.html`) kept as these will automatically be cached for other page views.
- Although unrelated to optimization, other small changes were made to bring the pages up to best standards and achieve a rating of 100% for both Performance and Accessibility in Lighthouse 2.0.0 audit for at least `index.html`.


##### #perfmatters and lovin' it.


#### Tips

* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>
