# Website Performance Optimization portfolio project

Challenge accepted, performance optimized!

## How to run
1. Extract the .zip archive
2. Start a local server in the new directory [eg. if python available run `python -m SimpleHTTPServer 3030` (Python 2.x) or `python -m http.server 3030` (Python 3.x)] using either Command Prompt or bash.
3. Start your favourite browser and visit localhost:3030

## List of optimizations

### Optimizations to `index.html` to achieve a PageSpeed score > 90 for Mobile and Desktop (live test using this [link] (https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fevblance.github.io%2Ffend-optimization%2F&tab=mobile))
- `media=print` attribute added to `print.css` head link.
- Resized, reduced quality (85%), changed chroma to 4:2:0 and discarded EXIF data on `pizzeria.jpg` to give `pizzeria-thumb.jpg`.
- Reduced quality (85%), changed chroma to 4:2:0 and discarded EXIF data on `profilepic.jpg`.
- Reduced number of critical resource requests by using a resized local image of `mobilewebdev.jpg` -> `mobilewebdev-thumb.jpg` instead of `src`'ing one of these monsters: https://lh6.ggpht.com/f_0W8h__3G99CWTjnMjD8BUKm7yp2-wJyApLtTwFoFtlal2ULf_JgHIsOQq2NiYfKOdMlXlMHDKNo5XVZLs=s100
- Removed Google Fonts request
- Inlined base and mobile styles from `css/style.css` into `index.html`.
- Eliminated Google Analytics code (sorry Paul...)
- Moved `perfmatters.js` script request to end of html `body`.


### Optimizations to `views/pizza.html` and `views/js/main.js` to achieve 60FPS
#### 1. `pizza.html`
 -  `pizzeria.jpg`-src'ing `img` tag replaced by `picture` and `srcset`s using reduced-size and 85% quality images.

#### 2. `main.js`
 - Wasteful `determineDx` renamed to `determineWidth` and simplified down to only the `switch` statement to return a percentage integer.
 - The new width of the pizza is determined just once before the for-loop of `changePizzaSizes` by `var newwidth = determineWidth(size) + '%';`.
 - Call to `updatePositions` from window scroll listener wrapped in a `requestAnimationFrame`. Complementary call to self using `requestAnimationFrame` added to end of `updatePositions`.
 - Insane layout thrashing via looped querying of `document.body.scrollTop` prevented by moving this call to a single variable assignment outside for-loop (`scrollToTop`).

### Other
- Similar optimizations that were applied to `index.html` in root folder also applied to the other linked html pages.
<!-- - Only one request of Google Fonts (root `index.html`) kept as these will automatically be cached for other page views. -->
- Although unrelated to optimization, other small changes were made to bring the pages up to best standards, improve semantics, and achieve a rating of 100% for both Performance and Accessibility in Lighthouse 2.0.0 audit for at least `index.html`.


##### #perfmatters and lovin' it.
