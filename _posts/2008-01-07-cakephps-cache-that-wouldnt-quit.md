---
layout: post
title: CakePHP's cache that wouldn't quit
tags:
- Mozilla
- software
---
I had the joy of debugging some unit tests the other day on [<abbr
title="addons.mozilla.org">AMO</abbr>][1] and ran into caching trouble.  Turns
out the [bug for this][2] was filed over a year ago, but I tested it in the
latest build of Cake (1.1.18.5850) and it's still not fixed.

Cake's models have a Boolean variable called $cacheQueries which I misplaced my
faith in early on.  Turns out this does disable query caching...sometimes.

The test I was writing was pretty straight forward: Look in the database for
some information to make sure it wasn't there, add the info, look in the
database to make sure it was there.  You can [see the actual code][3], but this
example is simplified:

{% highlight php linenos %}
<?
   $this->Addon->cacheQueries = false; // Disable the built-in caching.
   $ret = $this->Addon->query("SELECT addon_id FROM `addons_tags` WHERE addon_id={$this->testdata['addonid']}");
   $this->assertEmpty($ret, 'Data exists!'); // this should be empty
   $this->Addon->doSomething($this->testdata['addonid']);
   $ret = $this->Addon->query("SELECT addon_id FROM `addons_tags` WHERE addon_id={$this->testdata['addonid']}");
   $this->assertNotEmpty($ret, 'Data exists!'); // The array should have info in it
?>
{% endhighlight %}

The problem is, line 6 always returned an empty array.  I turned the DEBUG
mode to 2 so Cake would print out all the queries it was doing and discovered it
never actually made the second SELECT call.  I smell query caching!

Let's dig through some CakePHP code to figure out what's up:

`$this->Addon->query()` is passed through `AppModel::query()` to
[Model::query()][4]</a> and eventually works it's way down to
[DboSource::query()][5] with the same arguments.  This is where things go south.
Near the top of that function you'll see:

{% highlight php %}
<?
    if (count($args) == 1) {
        return $this->fetchAll($args[0]);
?>
{% endhighlight %}

The function signature for [DboSource::fetchAll()][6] looks like:

{% highlight php %}
<?
    function fetchAll($sql, $cache = true, $modelName = null)
?>
{% endhighlight %}

You can see the second parameter is a Boolean for caching and by default it's
on.  That's the fly in my clam chowder!

So, two ways around it:

The first way is to scroll up about 20 lines and look at the end of
`DboSource::query()`.  There is a handler there for a second parameter to your
original query() function.  Pass in false and voila, things just work.  Of
course, I didn't realize this until I was writing this post. I'm pretty sure
it's not documented anywhere unless you look at the code.

The second way is to use execute() instead of query().  If you look at
[DboSource::execute()][7] you'll see it suffers no caching and is as close to a
direct SQL call as you can get.

The [CakePHP manual][8] has this to say about query() and execute():

> Custom SQL calls can be made using the model's query() and execute() methods.
> The difference between the two is that query() is used to make custom SQL
> queries (the results of which are returned), and execute() is used to make
> custom SQL commands (which require no return value).

Apparently there are some other differences as well.  (The fact that execute()
returns results seems counter to what the manual suggests in the paragraph above
but I may just be misinterpreting what they mean.)  Regardless, if your tests
are failing double check that you're not fighting the cache and save yourself
some time.

[1]: http://addons.mozilla.org
[2]: https://trac.cakephp.org/ticket/1915
[3]: http://svn.mozilla.org/addons/trunk/site/app/tests/controllers/editors_controller.test.php
[4]: http://api.cakephp.org/model__php4_8php-source.html#l01334
[5]: http://api.cakephp.org/dbo__source_8php-source.html#l00177
[6]: http://api.cakephp.org/dbo__source_8php-source.html#l00290
[7]: http://api.cakephp.org/dbo__source_8php-source.html#l00153
[8]: http://manual.cakephp.org/chapter/models
