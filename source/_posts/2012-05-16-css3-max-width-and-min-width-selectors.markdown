---
layout: post
title: "CSS3 max-width and min-width selectors"
date: 2012-05-16 08:20
comments: true
categories: blog, css
---

I learned recently about min-width and max-width css selectors that allow you to specify certain properties that are applied under a maximum width and above a minimum width.  This can enable a flexible layout that works on many different screens without multiple distinct layouts (instead, just CSS).  This also makes it relatively easy to spot-test by simply resizing your browser to get an idea of how it will look on different size devices.

This example shows a 'Watch the Video' button on screens smaller than 480px wide.  Perfect for phones.

``` css

.video-alternative {
  display: none;
}

@media (max-width: 480px) {
  .video {
    display: none;
  }
  .video-alternative {
    display: block;
  }
}

```

``` html
<body>
  <div class='video'>
    <!-- embedded youtube video -->
  </div>
  <div class='video-alternative'>
    <div class='btn'>
      <a href="http://youtu.be/linkylink">Watch the Video</a>
    </div>
  </div>
</body>
```

Nifty for a dev guy like me who doesn't know much about design/CSS :)