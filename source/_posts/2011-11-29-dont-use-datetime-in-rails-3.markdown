---
layout: post
title: Don't Use DateTime in Rails 3
categories: blog
---
Rails 3 has good TimeZone support built in, but you have to use the right Date and Time classes to get full support.

If you have this set in your application.rb <code>config.active_record.default_timezone = :local</code>, then you really need to use Time so that it properly identifies itself as being in the local timezone and not in UTC when passing to the database insert.

``` ruby
ree-1.8.7-2011.03 :001 > DateTime.parse('2011-11-27 12:00:00 +0000')
=> Sun, 27 Nov 2011 12:00:00 +0000
ree-1.8.7-2011.03 :002 > DateTime.parse('2011-11-27 12:00:00')
=> Sun, 27 Nov 2011 12:00:00 +0000
ree-1.8.7-2011.03 :003 > Time.parse('2011-11-27 12:00:00 +0000')
=> Sun Nov 27 06:00:00 -0600 2011
ree-1.8.7-2011.03 :004 > Time.parse('2011-11-27 12:00:00')
=> Sun Nov 27 12:00:00 -0600 2011
```

So basically, Time.parse always returns the value in the local timezone, DateTime.parse always returns the value in UTC.  To get complete compatibility, always use Time.parse.  Trust me, I learned the hard way :)
