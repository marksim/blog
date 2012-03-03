---
layout: post
title: Installing memcached 1.4.4 on Mac OS X 10.6 Snow Leopard
categories: blog
---
<a href="https://wincent.com/wiki/Installing_memcached_1.4.1_on_Mac_OS_X_10.6_Snow_Leopard">Wincent.com has a great article on how to install memcached 1.4.1 on Mac OS X 10.6 Snow Leopard</a>.

Now that memcached 1.4.4 is out, I thought it would be nice to update it:

``` bash
curl -O http://www.monkey.org/~provos/libevent-1.4.13-stable.tar.gz
tar xzvf libevent-1.4.13-stable.tar.gz
cd libevent-1.4.13-stable
./configure
make
make verify
sudo make install
 
curl -O http://memcached.googlecode.com/files/memcached-1.4.4.tar.gz
tar xzvf memcached-1.4.4.tar.gz
cd memcached-1.4.4
./configure
make
make test
sudo make install
```

``` ruby
#!/usr/bin/env ruby
require 'pathname'
 
# memcached requires an absolute path for the -P switch
root = (Pathname.new(__FILE__).dirname + '..').realpath
pidfile = root + 'tmp' + 'memcached.pid'
 
if not pidfile.exist?
  puts "memcached not running: starting"
  system 'memcached', '-d', '-P', pidfile, '-l', '127.0.0.1'
else
  puts "memcached running: stopping"
  pid = pidfile.read.chomp
  system 'kill', pid
 
  # it appears that memcached doesn't clean up its pid file
  # unless you send it a QUIT signal (TERM, KILL, HUP don't)
  # unfortuantely, QUIT on Mac OS X causes memcached to crash
  pidfile.delete
end
```
