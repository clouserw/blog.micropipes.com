---
layout: post
title: Ten Tips for Website Localization
tags:
- Mozilla
---
This post has some general tips that I'd recommend to anyone wanting to write
a multilingual web application.  The majority of my code these days is <abbr
title="PHP: Hypertext Preprocessor">PHP</abbr>, but I think these tips are
applicable to most web programming languages.  In no particular order:

### <abbr title="Universal Transformation Format">UTF</abbr>-8 is your friend.  Use it.

The big step from <abbr title="American Standard Code for Information
Interchange">ASCII</abbr> to Unicode was the potential to use multiple bytes to
represent a single character.  With ASCII, each character was given a number
between 0 and 255 and that's all the programmer could use.  If another character
needed to be shown, the numbers were reused and a different font was loaded.  If
people didn't have the same fonts, they got errors or undefined results.

Enter Unicode and UTF-8.  With the creation of UTF-8, characters from all
over the world are assigned numbers between 0 and 1,114,111.  This is fantastic
news, because you can store text in many different languages without having to
worry about specific encodings.  This also means you can support language fall
back for sections of your web page.  If you have 80% of your page translated for
a specific language, you can fall back to an alternative, all while using the
same encoding.  <em>(an aside: Be sure to use lang="" attributes in your HTML
tags if you're changing the language mid-stream).</em>

### Don't concatenate strings

Code like this makes me sad, and will make your localizers cry (or quit):

{% highlight PHP %}
  <?
    $item = "toast";

    // Example one - This is bad
    echo _("Sometimes I eat")." {$item} "._("and sometimes I don't.");

    // Example two - This is better
    echo sprintf(_("Sometimes I eat %s and sometimes I don't."), $item);
?>
{% endhighlight %}

In the first example, chances are good the localizer will get the list of
strings to translate and the two separate calls to _() will look like two
different sentences with no context around them.  Firstly, the phrases by
themselves make no sense, and secondly, a localizer needs to be able to look at
an entire sentence (and sometimes more) to understand how to translate it most
effectively.

The second example uses the printf() standard %s to let the localizer know
you'll be substituting a string into the middle of the sentence.  This is the
current best practice for creating sentences with variables.  Depending on what
the string is, they may still be upset, but that's out of scope for this tip (<a
href="http://en.wikipedia.org/wiki/Declension">here's a hint though</a>).

### Don't use machine translation
In recent years great progress has been made towards programmatically
translating documents from language to language.  That said, it is <em>far</em>
from being an acceptable replacement for a fluent translator.  The edge cases
and "what ifs" on the technical/logical side of the translation are enough for
me to say that, but when you start talking about potentially offensive
translations (that's the next tip) this is a definite requirement.  Just look at
an example of <a href="http://translate.google.com/translate?u=http%3A%2F%2Fwww.germnews.de%2F&langpair=de%7Cen&hl=EN&safe=off&ie=UTF-8&oe=UTF-8&prev=%2Flanguage_tools">an
automated German to English translation</a>.  It's readable but it's far from
polished - not something you want as a first impression to your site.

### Be culturally sensitive
If you're not very familiar with your target culture ask for an opinion from
someone who is (or hire a localizer who is).  Seemingly innocent words, phrases,
and images could be misunderstood by another culture.  If you use terminology
that is only understood in your region or culture, the best case you can hope
for is that a visitor to your site just won't understand and will ignore it, but
it really reduces your credibility and the overall enjoyment of visiting your
site.

### Use multi-byte functions
This may be a little PHP specific, but it's good to be aware of it in any
language.  PHP has <a
href="http://php.oregonstate.edu/manual/en/ref.strings.php">string functions</a>
and <a href="http://php.oregonstate.edu/manual/en/ref.mbstring.php">multibyte
string functions</a>.  The latter functions support characters that fill up more
than one byte (ie. UTF-8 characters).  This is essential when manipulating
strings with letters outside of the Latin alphabet.  If you're not using PHP, at
the least, verify your programming language will manipulate multi-byte strings
correctly.

### Separate your views from  your logic
I'm a fan of <abbr title="Model View Controller">MVC</abbr> separation, but
there are plenty of <a
href="http://en.wikipedia.org/wiki/Architectural_pattern_%28computer_science%29">other
architectural patterns</a>.  Depending on what process and software you use for
localization you may be giving template files to localizers.  If that's the
case, the simpler the better - you don't need a bunch of complex code around the
strings waiting to be translated.  Even if you're using a method that doesn't
require giving template files to localizers, updating strings is easier, and
whoever does maintenance on your software in the future will thank you.

### Use (meaningful) placeholder text
This one might be a little controversial and is <a
href="http://www.gnu.org/software/gettext/">gettext</a> specific.  The
documented and recommended way to use gettext is to pass an English string to
the gettext() function.  This serves two purposes:  It lets the localizer see
the complete English string when they are translating, and it let's gettext fall
back to English if a translation isn't available.

I'm suggesting using a substitute string in place of the English string.  For
example, instead of `_("Error: Your cart is full!")` I would use
`_("error_cart_full")`.  English translations are done in the .po file, just like
every other locale.  By following this rule, it's possible to change the English
text, without affecting the other translations.  Using the documented method
means that even adding a comma means changing every locale's .po file and then
recompiling them all.  If you've got localizers watching for changes on their
files (through a shared repository) this means they have to check and verify any
changes - it's a hassle and it's time consuming for everyone involved.

The first purpose I mentioned, seeing English strings, can be duplicated by
running `msgattrib --set-fuzzy $file1 | msgmerge -NUs $file2` where
$file1 is the updated en-US .po file, and $file2 is the outdated .po file from
another locale.  This will merge the English strings into the other locale, but
will mark them as fuzzy, so gettext will ignore them until they are
translated.

The second purpose can be addressed just by making sure the strings you're
trying to use are available.  If you need to use a new English string on the
site, and the localizer is unavailable, you can temporarily move the fall back
logic into your code:

{% highlight php %}
  <?
    // This is a temporary fix!
    if (_("string_to_translate") == "string_to_translate") {
      // Print the English string
    } else {
      // Print the translated string
    }
?>
{% endhighlight %}

While we're on the subject of .po files, useful comments should be added to the
file wherever appropriate to help provide context and hints for localizers.

### Be aware of word length
Words in different languages have different lengths - words in Asian languages
generally have fewer characters than English, and German words, more.  When
designing the layout for your site, bear this in mind.  Don't hard code widths
to elements holding text - the words should be able to flow and expand as
necessary.  This can be tough with today's complex sites, but <abbr
title="Cascading Style Sheets">CSS</abbr> will go a long way to help.  Also,
when accepting user input, don't put unneeded arbitrary length restrictions on
the input.

### Don't use graphics as text
This is just a good idea in general, but it makes even more sense when
localizing pages.  Creating images is time consuming and has more potential for
error.  Using an appropriate encoding and employing CSS should get close to the
same effect (with an extra point for accessibility).  If you need to use an
image, be prepared to accept localized strings and make the image yourself -
localizers may not have the time, skills, or software they need to create the
images.

### Be aware of how changing the locale can affect strings
Setting the LC_ALL variable doesn't just change the formatting of strings -
it also changes currency formatting, time/date formatting, how things are
sorted, and what symbols represent numbers/lettters/etc.  Some Examples:

{% highlight php %}
  <?
    setlocale(LC_ALL, 'fr_FR');
    $num = 1.5;
    var_dump($num); // Prints 1.5
    echo $num; // Prints 1,5
?>
{% endhighlight %}

Internally, the decimal is represented by a period, and all the php functions
will recognize that (eg. <em>/[0-9.]+/</em> matches, whereas <em>/[0-9,]+/</em>
does not).  However, if you need to print the string to pass it to another
library or page (into a mysql query, passing to javascript, etc.) it's going to
become a comma.  Another example:

{% highlight php %}
  <?
    preg_match('/\w/', 'ホーム'); // Will never match, regardless of LC_ALL
?>
{% endhighlight %}

Using regular expressions on UTF-8 data can be risky.  The \w and [[:alpha:]]
character escapes only ever match single byte values (ie. characters with values
up to 256) with the <a
href="http://php.oregonstate.edu/manual/en/ref.pcre.php">preg functions</a>.
The <a href="http://www.pcre.org/pcre.txt"><abbr title="Perl-Compatible Regular
Expressions">PCRE</abbr> Documentation</a> says:

> "This remains true even when PCRE includes Unicode property support, because to
> do otherwise would slow down PCRE in many common cases. If you really want to
> test for a  wider sense  of,  say,  "digit",  you must use Unicode property
> tests such as \p{Nd}."

If we need to match UTF-8 strings with regular expressions in PHP, we can use:

{% highlight php %}
  <?
    mb_regex_encoding('UTF-8');
    mb_ereg('\w+', 'ホーム', $match);
    print_r($match); // Prints: Array ( [0] => ホーム  )
?>
{% endhighlight %}

By setting the internal regular expression encoding to UTF-8, and using the <a
href="http://us2.php.net/manual/en/function.mb-ereg.php">mb_ereg()</a> function,
we can match multibyte characters with regular expressions.  Realize though,
that this has the performance issues the PCRE documentation mentioned.
