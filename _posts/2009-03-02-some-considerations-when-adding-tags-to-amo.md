---
layout: post
title: Some considerations when adding Tags to AMO
tags:
- Mozilla
---
<p>Tags broke into the limelight around the time "Web 2.0" was becoming popularized.  They provided a simple but effective way to categorize objects and many sites are using them now.  Despite their proliferation, I haven't found any documentation on the internet regarding standards for implementing tags.  </p>
<p>A <a href="http://bakery.cakephp.org/articles/view/tag-cloud">tag library exists for CakePHP</a> but it, and many others, are too simplistic for what we want.</p>
<p>We've written our tagging goals into a plan but have some technical details we still need to figure out.  While reviewing what we have a couple questions arose that we thought people would have opinions on.</p>
<p>1) What should the range of allowed characters be?  Our first instinct was simplicity, something like <em>/[A-Za-z0-9-]/</em> (that is, all English letters and numbers and a dash).  This is easy to handle on our end but leaves out everyone that doesn't want to add tags using the English alphabet.  There is some debate how useful it would be to allow other Unicode characters, particularly when you think about #2 below.</p>
<p>2) Tags are most useful when they are normalized.  By allowing Unicode characters we run the risk of diluting our tag cloud.  For example, resume and résumé are close enough that for our purposes they are equivalent.  If we allow Unicode we'll have to deal with converting characters like é to e and vice versa for searches.  At that point we'll need a list of "equivalent" characters - not impossible but it will slow things down (both development and speed of a search).  The second question is:  Assuming you think we should allow Unicode characters, what characters are equivalents?  Here is a quick idea from <a href="http://php.oregonstate.edu/manual/en/function.strtr.php">php.net's strtr() documentation</a>:</p>

{% highlight php %}
<?
$a = 'ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖØÙÚÛÜÝÞßàáâãäåæçèéêëìíîïðñòóôõöøùúûýýþÿŔŕ';
$b = 'aaaaaaaceeeeiiiidnoooooouuuuybsaaaaaaaceeeeiiiidnoooooouuuyybyRr';
?>
{% endhighlight %}

<p>Some other aspects of our current plan are:</p>
<ul>
<li>Tags are not localizable in the same way as other strings on the site (like categories).  There isn't anything stopping someone from using "WebDev" as a tag or creating a new tag with "WebDev" translated in their language.  However, there won't be any relationship between the two translated tags.</li>
<li>Tags are separated by spaces.  Spaces within tags are allowed with quotes.</li>
<li>Spaces will be preserved when displaying a tag on the add-on's page, however, they will be removed for displaying the tag in a URL and for doing logical operations on the back end like searching.  This means searching for "Portland OR" will actually be collapsed to "PortlandOR" and will match either "Portland OR" or "PortlandOR" tags.  This is consistent with <a href="http://flickr.com/">flickr</a>.</li>
<li>If unicode is allowed we'll preserve characters as they are entered even if we are actually searching on their "equivalents."</li>
</ul>
