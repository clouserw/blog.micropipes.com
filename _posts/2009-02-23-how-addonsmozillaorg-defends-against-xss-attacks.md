---
layout: post
title: How addons.mozilla.org defends against XSS attacks
tags:
- Mozilla
- software
---
One of the things that gets a lot of news time these days is <abbr title="Cross
Site Scripting">XSS</abbr>.  There are a lot of places that explain what it is
and how to prevent it but most are oversimplified or don't provide real world
examples.  I thought I'd explain a couple of the ways <a
href="https://addons.mozilla.org/"><abbr
title="addons.mozilla.org">AMO</abbr></a> attempts to prevent it.

I'm not trying to invite attackers by posting this.  My goal is to provide a
(hopefully) working example from a real world, high-traffic site.  I think the
people exploiting XSS have a fairly good idea what they are doing and, too
often, the people attempting to secure their sites don't.  Since AMO is open
source I'm not sharing anything that isn't available already anyway (side note:
please don't depend on security by obscurity).

Firstly, this chunk of code sits in CakePHP's <a
href="http://svn.mozilla.org/addons/trunk/site/app/config/bootstrap.php">bootstrap.php</a>
and runs very close to the start of every request:

{% highlight php %}
<?
if (array_key_exists('url',$_GET) &&
    !preg_match('/\/api\//', $_GET['url']) &&
    preg_match('/[^\w\d\/\.\-_!: ]/u',$_GET['url'])) {
    header("HTTP/1.1 400 Bad Request");
    exit;
}
?>
{% endhighlight %}

Since a lot of XSS attacks are launched from the URL we implemented this simple
white list of characters we'll allow.  If anything outside of that white-list is
in the URL we return an invalid request header and die.  This isn't a lot of
protection but it does narrow the field of what our application expects and has
to deal with (particularly with control characters, high level ASCII, etc.).

The second, and more important section of code is in our <a
href="http://svn.mozilla.org/addons/trunk/site/app/app_controller.php">app_controller
class</a>.  We wrote a custom sanitize() function that any string going into one
of our views gets run through:

{% highlight php %}
<?
$sanitize_patterns = array(
    'patterns'      => array("/%/u", "/\(/u", "/\)/u", "//u", "/-/u"),
    'replacements'  => array("&amp;#37;", "&amp;#40;", "&amp;#41;", "&amp;#43;", "&amp;#45;")
    );

........

$data = iconv('UTF-8', 'UTF-8//IGNORE', $data);
$data = htmlspecialchars($data, ENT_QUOTES, 'UTF-8');
$data = preg_replace($sanitize_patterns['patterns'], $sanitize_patterns['replacements'], $data);
?>
{% endhighlight %}

This code has several important parts and I'll start with the functions.  The
first function that modifies the actual data is <a
href="http://php.oregonstate.edu/manual/en/function.iconv.php">iconv()</a>.  We
ask it to convert our data from UTF-8 to UTF-8 which seems unnecessary but the
"//IGNORE" part is important - that means it will throw out any characters it
can't represent appropriately.  This was added to prevent a proof of concept
attack that exploited a <a
href="http://en.wikipedia.org/wiki/C0_and_C1_control_codes">C0 ASCII control
code</a> character to break the output (discovered on the <a
href="http://sla.ckers.org/forum/">sla.ckers.org forums</a>).

The next function, <a
href="http://php.oregonstate.edu/htmlspecialchars">htmlspecialchars()</a>, is a
pretty well known function and converts special characters to their ASCII
equivalents.  The second parameter specifically asks it to encode single quotes.

Lastly we use the array of patterns and replacements declared at the beginning
to encode a few final symbols, like parenthesis and the percentage sign, into
HTML entities.

This system has worked fairly well for a few years now and as issues are
discovered we make changes to it.  If you're looking for the latest code please
be sure to check <a href="http://svn.mozilla.org/addons/trunk/">our
repository</a>.  And, as always, if you find any kind of exploit on AMO please
let me know! :)
