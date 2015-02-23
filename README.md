## Udacity Project 4: Website Performance Optimization
In this project, the students were required to study the fundamentals of the CRP, critical rendering path according to which we had to figure out how to make a few optimizations as follows:
-1 PageSpeed Insights on index.html has to score 90 or more
-2 pizzeria.html needs to perform at least at 60 FPS and have a responsive design to it that would not allow the text to flow out of the container when downsizing the screen estate.

For the first part, the main aspect was to async JS that doesn't have any influence on the DOM rendering, to adjust the media tag of print.css to 'print' and to inline style.css directly into the HTML. This last one provided a huge improvement in performance on PageSpeed Insights as the css would not increase the HTML beyond the 14KB treshhold and thus would save on an extra roundtrip. I also minified the images used, especially pizzeria.jpg which was succesfully reduced to 125KB. I also made the judgement call to opt for a resized thumbnail version of the same file by the name pizzeria-tiny.jpg which further reduced the size to 10KB. I achieved this using GimpShop.

For the second part, my 'aha-erlebnis' manifested itself after reading this article: http://www.nczonline.net/blog/2009/02/03/speed-up-your-javascript-part-4/ which made me understand that DOM is extremely slow and should be avoided to be read from and written to unless absolutely necessary, as is clear from following extract:

    Since the DOM is so slow at pretty much everything, it’s very important to cache results that you retrieve from the DOM. This is important for property access that causes reflow, such as offsetWidth, but also important in general. The following, for example, is incredibly inefficient:

    document.getElementById("myDiv").style.left = document.getElementById("myDiv").offsetLeft +
        document.getElementById("myDiv").offsetWidth + "px";
    The three calls to getElementById() here are the problem. Accessing the DOM is expensive, and this is three DOM calls to access the exact same element. The code would better be written as such:

    var myDiv = document.getElementById("myDiv");
    myDiv.style.left = myDiv.offsetLeft + myDiv.offsetWidth + "px";
    Now the number of total DOM operations has been minimized by removing the redundant calls. Always cache DOM values that are used more than once to avoid a performance penalty.

Thereafter, for the sake of further optimization, I inlined the CSS directly into the HTML and added flex-box to .container so that all it's children will end up stacking on one and another in case of shortage of space due to screen estate. Without doing this, the text ended up flowing out of the container making it appear to be cut off at the black background on the side.

My insight and efficiency of Chrome Dev-Tools after the Udacity Course further improved by watching the following presentation by the same instructor:
https://www.youtube.com/watch?v=BaneWEqNcpE
The slides of which are at:
https://www.igvita.com/slides/2012/devtools-tips-and-tricks/#1

I really liked the cool feature of how the PageSpeeds Insights plugin can not only help you understand the bulky size of an image, but also provides you with an immediate link to the optimized image which would have saved me some work if I werre to have known this earlier.

The general instructions of the project by Udacity follow below:

## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository, inspect the code,

### Getting started

####Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

####Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js.

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
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

### Sample Portfolios

Feeling uninspired by the portfolio? Here's a list of cool portfolios I found after a few minutes of Googling.

* <a href="http://www.reddit.com/r/webdev/comments/280qkr/would_anybody_like_to_post_their_portfolio_site/">A great discussion about portfolios on reddit</a>
* <a href="http://ianlunn.co.uk/">http://ianlunn.co.uk/</a>
* <a href="http://www.adhamdannaway.com/portfolio">http://www.adhamdannaway.com/portfolio</a>
* <a href="http://www.timboelaars.nl/">http://www.timboelaars.nl/</a>
* <a href="http://futoryan.prosite.com/">http://futoryan.prosite.com/</a>
* <a href="http://playonpixels.prosite.com/21591/projects">http://playonpixels.prosite.com/21591/projects</a>
* <a href="http://colintrenter.prosite.com/">http://colintrenter.prosite.com/</a>
* <a href="http://calebmorris.prosite.com/">http://calebmorris.prosite.com/</a>
* <a href="http://www.cullywright.com/">http://www.cullywright.com/</a>
* <a href="http://yourjustlucky.com/">http://yourjustlucky.com/</a>
* <a href="http://nicoledominguez.com/portfolio/">http://nicoledominguez.com/portfolio/</a>
* <a href="http://www.roxannecook.com/">http://www.roxannecook.com/</a>
* <a href="http://www.84colors.com/portfolio.html">http://www.84colors.com/portfolio.html</a>
