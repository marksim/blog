---
layout: post
title: "Easy way to limit the length of a list"
date: 2012-06-15 13:33
comments: true
categories: jquery blog code 
---

I have lots of lists on my new site that we want to show 'only the first 5' items on, but allow people to expand to see them all if they want.  It's common enough that I'd like to have an easy way to do it.  Bonus points if it's non-obtrusive.

``` coffeescript
jQuery ->
  $('ul.show-more').each ->
    if $(this).find('li').length > 5
      $(this).find('li:gt(4)').hide().end().append(
        $('<li><a href="#">Show More...</a></li>').click ->
          $(this).siblings(':hidden').show().end().remove()
        )
```

Now all I have to do is drop into my favorite haml template and bang out a list

``` haml
%ul.show-more
  - items.each do |item|
    %li= item
```

And as long as I'm using the <code>show-more</code> class, I get it for free.  Beautiful.
