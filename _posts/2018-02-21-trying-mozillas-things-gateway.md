---
layout: post
title: Trying Mozilla's Things Gateway
tags:
- Mozilla
---

*Spoiler: It doesn't yet support my hardware and I didn't get it working, but
I'm posting anyway because it's ok to fail. :)*

Last weekend I was inspired by [Lars's posts on IoT][1] to try [Mozilla's Things
Gateway][2].

I have an old Raspberry Pi 1 Model B with a [RaZberry Z-Wave Daughterboard][3]
which I had soldered a larger external antenna on to last year.  I used to run
OpenHAB on it to control some z-wave devices before I moved last year and since
then it's just been in a box.  Let's fire it up!

This original Raspberry Pi is a single core 700mhz CPU, so I'm planning on
running it headless and doing everything remotely over SSH to save on GUI
resources.

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/public/img/2018.raspberry.pi.1.jpg" />

Firstly, since I hadn't plugged this in forever, I booted it up, uninstalled
OpenHAB and the RaZberry software and [upgraded Raspbian to the latest
version](https://www.raspberrypi.org/blog/raspbian-stretch/).  It's still as
easy as it should be, just edit the sources.list and:

```bash
# apt-get update
# apt-get dist-upgrade
```

I left the upgrade running over night because it was taking so long -- a
foreshadowing of things to come! 😩

On the suggestion of the page I linked to above, I removed `pulseaudio` since I
don't use it.

```bash
# sudo apt-get purge "pulseaudio*"
```

[The instructions for installing the Gateway][4] are great and easy to follow.

I installed `nvm` as recommended, although so far I'm regretting it.  It takes
12 seconds to start a new login shell now while nvm executes the stuff it put
in `.bashrc`.  If I end up logging in very often I'll get rid of it.

On the other hand, the Node world does do permissions well.  Most tools can
install in a users home directory without any root permissions, which I was
happy to do:

```bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
$ nvm install --lts
$ nvm use --lts
$ npm --version
5.6.0
$ node --version
v8.9.4
$ npm install --global yarn
```

Next up was OpenZWave.  Their documentation mentions supporting the Razberry
card, so I felt good about things working.  When you get to the `make` command,
go grab some lunch -- this also took plenty of time.

```bash
$ git clone https://github.com/OpenZWave/open-zwave.git
$ cd open-zwave
$ make && sudo make install
$ sudo ldconfig
```

Finally, I'm ready to install the Things Gateway.  For a project that is still
new and moving quickly I like to install directly out of Git which makes
testing patches and upgrading to new versions easy (I hope!).

```bash
$ git clone https://github.com/mozilla-iot/gateway.git
$ cd gateway
$ yarn  # Yarn actually prints how long it takes to execute.  This took 6070.32 seconds! 💤
```

I don't want to use Mozilla's tunneling service, so I faked some SSL:

```bash
$ mkdir -p ssl
$ openssl genrsa -out ssl/privatekey.pem 2048
$ openssl req -new -sha256 -key ssl/privatekey.pem -out ssl/csr.pem
$ openssl x509 -req -in ssl/csr.pem -signkey ssl/privatekey.pem -out ssl/certificate.pem
```

And then start the web server.

```bash
$ npm start  # This takes around 4 minutes to finish starting :(
```

Loading the site in my browser works!   I click `settings` -> `add-ons` and
install `z-wave device support`.  However, watching the console I can see it
fail to find the z-wave interface.

I dug around in the code and [found the findZWavePort() code][5] that does the
detection, and confrimed that it's looking at USB ports which won't work for
the Razberry which comes in on `/dev/ttyAMA0`.

<div class="aside">
<p>I'm just going to stick in a little aside here...</p>

<p>I modified the <code>zwave-adapter.js</code> file to add some logging and
make sure that was as far as it was getting and restarted the server (which,
took 4 minutes...) and then saw the module failed to load because the checksum
didn't match.  I deleted the checksum file (4 minutes...), and it failed again,
so I finally just removed the one line from the checksum file.</p>

<p>The checksum is a great idea and I assume there is some kind of flag I can pass
to the server to ignore it, but I haven't found it yet.</p>
</div>

One last thing I wanted to verify before I dug too far into the Gateway was to
make sure OpenZWave was working.  They include a program with their code called
`MinOZW`.  I didn't see documentation for it, but it takes the port to monitor
as it's first parameter:

```bash
$ MinOZW /dev/ttyAMA0
```

That command gave me a flood of Z-wave data, so I knew it was seeing the
controller properly.

Searching the open Mozilla IOT issues revealed that the request to [support the Razberry
board was filed a couple weeks ago][6].  So, I CC'd myself to keep an eye on
it, and that's as far as I got.  So far:

* I have really high hopes for the Mozilla IoT Gateway
* A first generation Raspberry Pi might be too slow for these shenanigans 😞

[1]: http://www.twobraids.com/2018/02/lars-and-real-internet-of-things-part-1.html
[2]: https://iot.mozilla.org/gateway/
[3]: https://razberry.z-wave.me/
[4]: https://github.com/mozilla-iot/gateway/blob/master/README.md
[5]: https://github.com/mozilla-iot/zwave-adapter/blob/master/zwave-adapter.js#L368
[6]: https://github.com/mozilla-iot/zwave-adapter/issues/8
