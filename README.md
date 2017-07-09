# Website Performance Optimization portfolio project

Challenge accepted, performance optimized!

## How to run
1. Extract the .zip archive
2. Start a local server in the new directory [eg. if python available run `python -m SimpleHTTPServer 3030` (Python 2.x) or `python -m http.server 3030` (Python 3.x)] using either Command Prompt or bash.
3. Start your favourite browser and visit localhost:3030

## List of optimizations

### Optimizations to `index.html` to achieve a PageSpeed score > 90 for Mobile and Desktop (live test using this [link](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fevblance.github.io%2Ffend-optimization%2F&tab=mobile))
- `media=print` attribute added to `print.css` head link.
- Resized, reduced quality (85%), changed chroma to 4:2:0 and discarded EXIF data on `pizzeria.jpg` to give `pizzeria-thumb.jpg`.
- Reduced quality (85%), changed chroma to 4:2:0 and discarded EXIF data on `profilepic.jpg`.
- Reduced number of critical resource requests by using a resized local image of `mobilewebdev.jpg` -> `mobilewebdev-thumb.jpg` instead of `src`'ing one of these monsters: https://lh6.ggpht.com/f_0W8h__3G99CWTjnMjD8BUKm7yp2-wJyApLtTwFoFtlal2ULf_JgHIsOQq2NiYfKOdMlXlMHDKNo5XVZLs=s100
- Removed Google Fonts request
- Inlined base and mobile styles from `css/style.css` into `index.html`.
- Eliminated Google Analytics code (sorry Paul...)
- Moved `perfmatters.js` script request to end of html `body`.


### Optimizations to achieve 60FPS in `pizzas.html` view
#### 1. `views/pizza.html`
 -  `pizzeria.jpg`-src'ing `img` tag replaced by `picture` and `srcset`s using reduced-size and 85% quality images.

#### 2. `views/js/main.js`
 - Wasteful `determineDx` function renamed to `determineWidth` and simplified down to only the `switch` statement to return a percentage integer.
 - The new width of the pizza is determined just once before the for-loop of `changePizzaSizes` by `var newWidth = determineWidth(size) + '%';`.
 - Call to `updatePositions` from window scroll listener wrapped in a `requestAnimationFrame`. Complementary call to self using `requestAnimationFrame` added to end of `updatePositions`.
 - Insane layout thrashing via looped querying of `document.body.scrollTop` prevented by moving it to a single variable assignment (`scrollToTop`) outside for-loop.
 - Changed a number of `document.querySelector` DOM queries throughout the script to use `document.getElementById` instead.
 - Changed a couple of `document.querySelectorAll` class parameter DOM queries in the script to use `document.getElementsByClassName` instead.
 - DOM queries in loop of `changePizzaSizes` function stored in local variables to avoid unnecessary re-querying.
 - `.mover` class pizza items array length query in `updatePositions` function moved from for-loop to a local function variable to prevent re-querying.
 - Stored `scrollToTop / 1250` argument from Math.sin() evaluation in `phase` variable in `updatePositions` in local variable `phaseArg` to prevent unnecessary re-calculation within for-loop body.
 - Reduced unnecessarily large number of pizzas being created on `DOMContentLoaded` by setting the rows and columns such that only 24 pizzas are created, and using the browser window resolution to dynamically derive a proper spacing to distribute the pizzas and center their appearance in the view.
 - Moved a variable declaration for `elem` out above the for-loop in `DOMContentLoaded` event listener to prevent unnecessary variable re-declaration inside loop body.
 - Moved a DOM query for `#movingPizzas1` outside for-loop in `DOMContentLoaded` event listener and stored result as variable to prevent re-querying inside loop body when appending new moving pizzas.

#### 3. `views/css/styles.css`
 - Forced hardware acceleration by adding `transform: translateZ(0)` and `backface-visibility: hidden` to `.mover` class.


### Other
- Similar optimizations that were applied to `index.html` in root folder also applied to the other linked html pages.
- Although unrelated to optimization, other small changes were made to bring the pages up to best standards, improve semantics, and achieve a rating of 100% for both Performance and Accessibility in Lighthouse 2.0.0 audit for at least `index.html`.
<!-- NOTE: If PageSpeed requirements were less strict, a single Google Fonts request would be kept in root `index.html`, as these would then be automatically be cached for other page views. -->


##### #perfmatters and lovin' it.
