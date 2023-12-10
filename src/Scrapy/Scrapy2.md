:::

It returns [`None`{.docutils .literal .notranslate}]{.pre} if no element
was found:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//div[@id="not-exists"]/text()').get() is None
    True
:::
:::

A default return value can be provided as an argument, to be used
instead of [`None`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//div[@id="not-exists"]/text()').get(default="not-found")
    'not-found'
:::
:::

Instead of using e.g. [`'@src'`{.docutils .literal .notranslate}]{.pre}
XPath it is possible to query for attributes using [`.attrib`{.docutils
.literal .notranslate}]{.pre} property of a [`Selector`{.xref .py
.py-class .docutils .literal .notranslate}]{.pre}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> [img.attrib["src"] for img in response.css("img")]
    ['image1_thumb.jpg',
    'image2_thumb.jpg',
    'image3_thumb.jpg',
    'image4_thumb.jpg',
    'image5_thumb.jpg']
:::
:::

As a shortcut, [`.attrib`{.docutils .literal .notranslate}]{.pre} is
also available on SelectorList directly; it returns attributes for the
first matching element:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("img").attrib["src"]
    'image1_thumb.jpg'
:::
:::

This is most useful when only a single result is expected, e.g. when
selecting by id, or selecting unique elements on a web page:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("base").attrib["href"]
    'http://example.com/'
:::
:::

Now we're going to get the base URL and some image links:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//base/@href").get()
    'http://example.com/'

    >>> response.css("base::attr(href)").get()
    'http://example.com/'

    >>> response.css("base").attrib["href"]
    'http://example.com/'

    >>> response.xpath('//a[contains(@href, "image")]/@href').getall()
    ['image1.html',
    'image2.html',
    'image3.html',
    'image4.html',
    'image5.html']

    >>> response.css("a[href*=image]::attr(href)").getall()
    ['image1.html',
    'image2.html',
    'image3.html',
    'image4.html',
    'image5.html']

    >>> response.xpath('//a[contains(@href, "image")]/img/@src').getall()
    ['image1_thumb.jpg',
    'image2_thumb.jpg',
    'image3_thumb.jpg',
    'image4_thumb.jpg',
    'image5_thumb.jpg']

    >>> response.css("a[href*=image] img::attr(src)").getall()
    ['image1_thumb.jpg',
    'image2_thumb.jpg',
    'image3_thumb.jpg',
    'image4_thumb.jpg',
    'image5_thumb.jpg']
:::
:::
:::

::: {#extensions-to-css-selectors .section}
[]{#topics-selectors-css-extensions}

##### Extensions to CSS Selectors[¶](#extensions-to-css-selectors "Permalink to this heading"){.headerlink}

Per W3C standards, [CSS
selectors](https://www.w3.org/TR/selectors-3/#selectors){.reference
.external} do not support selecting text nodes or attribute values. But
selecting these is so essential in a web scraping context that Scrapy
(parsel) implements a couple of **non-standard pseudo-elements**:

-   to select text nodes, use [`::text`{.docutils .literal
    .notranslate}]{.pre}

-   to select attribute values, use [`::attr(name)`{.docutils .literal
    .notranslate}]{.pre} where *name* is the name of the attribute that
    you want the value of

::: {.admonition .warning}
Warning

These pseudo-elements are Scrapy-/Parsel-specific. They will most
probably not work with other libraries like
[lxml](https://lxml.de/){.reference .external} or
[PyQuery](https://pypi.org/project/pyquery/){.reference .external}.
:::

Examples:

-   [`title::text`{.docutils .literal .notranslate}]{.pre} selects
    children text nodes of a descendant [`<title>`{.docutils .literal
    .notranslate}]{.pre} element:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title::text").get()
    'Example website'
:::
:::

-   [`*::text`{.docutils .literal .notranslate}]{.pre} selects all
    descendant text nodes of the current selector context:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("#images *::text").getall()
    ['\n   ',
    'Name: My image 1 ',
    '\n   ',
    'Name: My image 2 ',
    '\n   ',
    'Name: My image 3 ',
    '\n   ',
    'Name: My image 4 ',
    '\n   ',
    'Name: My image 5 ',
    '\n  ']
:::
:::

-   [`foo::text`{.docutils .literal .notranslate}]{.pre} returns no
    results if [`foo`{.docutils .literal .notranslate}]{.pre} element
    exists, but contains no text (i.e. text is empty):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("img::text").getall()
    []

    This means ``.css('foo::text').get()`` could return None even if an element
    exists. Use ``default=''`` if you always want a string:
:::
:::

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("img::text").get()
    >>> response.css("img::text").get(default="")
    ''
:::
:::

-   [`a::attr(href)`{.docutils .literal .notranslate}]{.pre} selects the
    *href* attribute value of descendant links:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("a::attr(href)").getall()
    ['image1.html',
    'image2.html',
    'image3.html',
    'image4.html',
    'image5.html']
:::
:::

::: {.admonition .note}
Note

See also: [[Selecting element attributes]{.std
.std-ref}](#selecting-attributes){.hoverxref .tooltip .reference
.internal}.
:::

::: {.admonition .note}
Note

You cannot chain these pseudo-elements. But in practice it would not
make much sense: text nodes do not have attributes, and attribute values
are string values already and do not have children nodes.
:::
:::

::: {#nesting-selectors .section}
[]{#topics-selectors-nesting-selectors}

##### Nesting selectors[¶](#nesting-selectors "Permalink to this heading"){.headerlink}

The selection methods ([`.xpath()`{.docutils .literal
.notranslate}]{.pre} or [`.css()`{.docutils .literal
.notranslate}]{.pre}) return a list of selectors of the same type, so
you can call the selection methods for those selectors too. Here's an
example:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> links = response.xpath('//a[contains(@href, "image")]')
    >>> links.getall()
    ['<a href="image1.html">Name: My image 1 <br><img src="image1_thumb.jpg" alt="image1"></a>',
    '<a href="image2.html">Name: My image 2 <br><img src="image2_thumb.jpg" alt="image2"></a>',
    '<a href="image3.html">Name: My image 3 <br><img src="image3_thumb.jpg" alt="image3"></a>',
    '<a href="image4.html">Name: My image 4 <br><img src="image4_thumb.jpg" alt="image4"></a>',
    '<a href="image5.html">Name: My image 5 <br><img src="image5_thumb.jpg" alt="image5"></a>']

    >>> for index, link in enumerate(links):
    ...     href_xpath = link.xpath("@href").get()
    ...     img_xpath = link.xpath("img/@src").get()
    ...     print(f"Link number {index} points to url {href_xpath!r} and image {img_xpath!r}")
    ...
    Link number 0 points to url 'image1.html' and image 'image1_thumb.jpg'
    Link number 1 points to url 'image2.html' and image 'image2_thumb.jpg'
    Link number 2 points to url 'image3.html' and image 'image3_thumb.jpg'
    Link number 3 points to url 'image4.html' and image 'image4_thumb.jpg'
    Link number 4 points to url 'image5.html' and image 'image5_thumb.jpg'
:::
:::
:::

::: {#selecting-element-attributes .section}
[]{#selecting-attributes}

##### Selecting element attributes[¶](#selecting-element-attributes "Permalink to this heading"){.headerlink}

There are several ways to get a value of an attribute. First, one can
use XPath syntax:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//a/@href").getall()
    ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']
:::
:::

XPath syntax has a few advantages: it is a standard XPath feature, and
[`@attributes`{.docutils .literal .notranslate}]{.pre} can be used in
other parts of an XPath expression - e.g. it is possible to filter by
attribute value.

Scrapy also provides an extension to CSS selectors
([`::attr(...)`{.docutils .literal .notranslate}]{.pre}) which allows to
get attribute values:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("a::attr(href)").getall()
    ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']
:::
:::

In addition to that, there is a [`.attrib`{.docutils .literal
.notranslate}]{.pre} property of Selector. You can use it if you prefer
to lookup attributes in Python code, without using XPaths or CSS
extensions:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> [a.attrib["href"] for a in response.css("a")]
    ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']
:::
:::

This property is also available on SelectorList; it returns a dictionary
with attributes of a first matching element. It is convenient to use
when a selector is expected to give a single result (e.g. when selecting
by element ID, or when selecting an unique element on a page):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("base").attrib
    {'href': 'http://example.com/'}
    >>> response.css("base").attrib["href"]
    'http://example.com/'
:::
:::

[`.attrib`{.docutils .literal .notranslate}]{.pre} property of an empty
SelectorList is empty:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("foo").attrib
    {}
:::
:::
:::

::: {#using-selectors-with-regular-expressions .section}
##### Using selectors with regular expressions[¶](#using-selectors-with-regular-expressions "Permalink to this heading"){.headerlink}

[`Selector`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
also has a [`.re()`{.docutils .literal .notranslate}]{.pre} method for
extracting data using regular expressions. However, unlike using
[`.xpath()`{.docutils .literal .notranslate}]{.pre} or
[`.css()`{.docutils .literal .notranslate}]{.pre} methods,
[`.re()`{.docutils .literal .notranslate}]{.pre} returns a list of
strings. So you can't construct nested [`.re()`{.docutils .literal
.notranslate}]{.pre} calls.

Here's an example used to extract image names from the [[HTML code]{.std
.std-ref}](#topics-selectors-htmlcode){.hoverxref .tooltip .reference
.internal} above:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//a[contains(@href, "image")]/text()').re(r"Name:\s*(.*)")
    ['My image 1 ',
    'My image 2 ',
    'My image 3 ',
    'My image 4 ',
    'My image 5 ']
:::
:::

There's an additional helper reciprocating [`.get()`{.docutils .literal
.notranslate}]{.pre} (and its alias [`.extract_first()`{.docutils
.literal .notranslate}]{.pre}) for [`.re()`{.docutils .literal
.notranslate}]{.pre}, named [`.re_first()`{.docutils .literal
.notranslate}]{.pre}. Use it to extract just the first matching string:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//a[contains(@href, "image")]/text()').re_first(r"Name:\s*(.*)")
    'My image 1 '
:::
:::
:::

::: {#extract-and-extract-first .section}
[]{#old-extraction-api}

##### extract() and extract_first()[¶](#extract-and-extract-first "Permalink to this heading"){.headerlink}

If you're a long-time Scrapy user, you're probably familiar with
[`.extract()`{.docutils .literal .notranslate}]{.pre} and
[`.extract_first()`{.docutils .literal .notranslate}]{.pre} selector
methods. Many blog posts and tutorials are using them as well. These
methods are still supported by Scrapy, there are **no plans** to
deprecate them.

However, Scrapy usage docs are now written using [`.get()`{.docutils
.literal .notranslate}]{.pre} and [`.getall()`{.docutils .literal
.notranslate}]{.pre} methods. We feel that these new methods result in a
more concise and readable code.

The following examples show how these methods map to each other.

1.  [`SelectorList.get()`{.docutils .literal .notranslate}]{.pre} is the
    same as [`SelectorList.extract_first()`{.docutils .literal
    .notranslate}]{.pre}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("a::attr(href)").get()
    'image1.html'
    >>> response.css("a::attr(href)").extract_first()
    'image1.html'
:::
:::

2.  [`SelectorList.getall()`{.docutils .literal .notranslate}]{.pre} is
    the same as [`SelectorList.extract()`{.docutils .literal
    .notranslate}]{.pre}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("a::attr(href)").getall()
    ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']
    >>> response.css("a::attr(href)").extract()
    ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']
:::
:::

3.  [`Selector.get()`{.docutils .literal .notranslate}]{.pre} is the
    same as [`Selector.extract()`{.docutils .literal
    .notranslate}]{.pre}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("a::attr(href)")[0].get()
    'image1.html'
    >>> response.css("a::attr(href)")[0].extract()
    'image1.html'
:::
:::

4.  For consistency, there is also [`Selector.getall()`{.docutils
    .literal .notranslate}]{.pre}, which returns a list:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("a::attr(href)")[0].getall()
    ['image1.html']
:::
:::

So, the main difference is that output of [`.get()`{.docutils .literal
.notranslate}]{.pre} and [`.getall()`{.docutils .literal
.notranslate}]{.pre} methods is more predictable: [`.get()`{.docutils
.literal .notranslate}]{.pre} always returns a single result,
[`.getall()`{.docutils .literal .notranslate}]{.pre} always returns a
list of all extracted results. With [`.extract()`{.docutils .literal
.notranslate}]{.pre} method it was not always obvious if a result is a
list or not; to get a single result either [`.extract()`{.docutils
.literal .notranslate}]{.pre} or [`.extract_first()`{.docutils .literal
.notranslate}]{.pre} should be called.
:::
:::

::: {#working-with-xpaths .section}
[]{#topics-selectors-xpaths}

#### Working with XPaths[¶](#working-with-xpaths "Permalink to this heading"){.headerlink}

Here are some tips which may help you to use XPath with Scrapy selectors
effectively. If you are not much familiar with XPath yet, you may want
to take a look first at this [XPath
tutorial](http://www.zvon.org/comp/r/tut-XPath_1.html){.reference
.external}.

::: {.admonition .note}
Note

Some of the tips are based on [this post from Zyte's
blog](https://www.zyte.com/blog/xpath-tips-from-the-web-scraping-trenches/){.reference
.external}.
:::

::: {#working-with-relative-xpaths .section}
[]{#topics-selectors-relative-xpaths}

##### Working with relative XPaths[¶](#working-with-relative-xpaths "Permalink to this heading"){.headerlink}

Keep in mind that if you are nesting selectors and use an XPath that
starts with [`/`{.docutils .literal .notranslate}]{.pre}, that XPath
will be absolute to the document and not relative to the
[`Selector`{.docutils .literal .notranslate}]{.pre} you're calling it
from.

For example, suppose you want to extract all [`<p>`{.docutils .literal
.notranslate}]{.pre} elements inside [`<div>`{.docutils .literal
.notranslate}]{.pre} elements. First, you would get all
[`<div>`{.docutils .literal .notranslate}]{.pre} elements:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> divs = response.xpath("//div")
:::
:::

At first, you may be tempted to use the following approach, which is
wrong, as it actually extracts all [`<p>`{.docutils .literal
.notranslate}]{.pre} elements from the document, not only those inside
[`<div>`{.docutils .literal .notranslate}]{.pre} elements:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> for p in divs.xpath("//p"):  # this is wrong - gets all <p> from the whole document
    ...     print(p.get())
    ...
:::
:::

This is the proper way to do it (note the dot prefixing the
[`.//p`{.docutils .literal .notranslate}]{.pre} XPath):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> for p in divs.xpath(".//p"):  # extracts all <p> inside
    ...     print(p.get())
    ...
:::
:::

Another common case would be to extract all direct [`<p>`{.docutils
.literal .notranslate}]{.pre} children:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> for p in divs.xpath("p"):
    ...     print(p.get())
    ...
:::
:::

For more details about relative XPaths see the [Location
Paths](https://www.w3.org/TR/xpath/all/#location-paths){.reference
.external} section in the XPath specification.
:::

::: {#when-querying-by-class-consider-using-css .section}
##### When querying by class, consider using CSS[¶](#when-querying-by-class-consider-using-css "Permalink to this heading"){.headerlink}

Because an element can contain multiple CSS classes, the XPath way to
select elements by class is the rather verbose:

::: {.highlight-python .notranslate}
::: highlight
    *[contains(concat(' ', normalize-space(@class), ' '), ' someclass ')]
:::
:::

If you use [`@class='someclass'`{.docutils .literal .notranslate}]{.pre}
you may end up missing elements that have other classes, and if you just
use [`contains(@class,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`'someclass')`{.docutils .literal .notranslate}]{.pre} to
make up for that you may end up with more elements that you want, if
they have a different class name that shares the string
[`someclass`{.docutils .literal .notranslate}]{.pre}.

As it turns out, Scrapy selectors allow you to chain selectors, so most
of the time you can just select by class using CSS and then switch to
XPath when needed:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy import Selector
    >>> sel = Selector(
    ...     text='<div class="hero shout"><time datetime="2014-07-23 19:00">Special date</time></div>'
    ... )
    >>> sel.css(".shout").xpath("./time/@datetime").getall()
    ['2014-07-23 19:00']
:::
:::

This is cleaner than using the verbose XPath trick shown above. Just
remember to use the [`.`{.docutils .literal .notranslate}]{.pre} in the
XPath expressions that will follow.
:::

::: {#beware-of-the-difference-between-node-1-and-node-1 .section}
##### Beware of the difference between //node\[1\] and (//node)\[1\][¶](#beware-of-the-difference-between-node-1-and-node-1 "Permalink to this heading"){.headerlink}

[`//node[1]`{.docutils .literal .notranslate}]{.pre} selects all the
nodes occurring first under their respective parents.

[`(//node)[1]`{.docutils .literal .notranslate}]{.pre} selects all the
nodes in the document, and then gets only the first of them.

Example:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy import Selector
    >>> sel = Selector(
    ...     text="""
    ...     <ul class="list">
    ...         <li>1</li>
    ...         <li>2</li>
    ...         <li>3</li>
    ...     </ul>
    ...     <ul class="list">
    ...         <li>4</li>
    ...         <li>5</li>
    ...         <li>6</li>
    ...     </ul>"""
    ... )
    >>> xp = lambda x: sel.xpath(x).getall()
:::
:::

This gets all first [`<li>`{.docutils .literal .notranslate}]{.pre}
elements under whatever it is its parent:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> xp("//li[1]")
    ['<li>1</li>', '<li>4</li>']
:::
:::

And this gets the first [`<li>`{.docutils .literal .notranslate}]{.pre}
element in the whole document:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> xp("(//li)[1]")
    ['<li>1</li>']
:::
:::

This gets all first [`<li>`{.docutils .literal .notranslate}]{.pre}
elements under an [`<ul>`{.docutils .literal .notranslate}]{.pre}
parent:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> xp("//ul/li[1]")
    ['<li>1</li>', '<li>4</li>']
:::
:::

And this gets the first [`<li>`{.docutils .literal .notranslate}]{.pre}
element under an [`<ul>`{.docutils .literal .notranslate}]{.pre} parent
in the whole document:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> xp("(//ul/li)[1]")
    ['<li>1</li>']
:::
:::
:::

::: {#using-text-nodes-in-a-condition .section}
##### Using text nodes in a condition[¶](#using-text-nodes-in-a-condition "Permalink to this heading"){.headerlink}

When you need to use the text content as argument to an [XPath string
function](https://www.w3.org/TR/xpath/all/#section-String-Functions){.reference
.external}, avoid using [`.//text()`{.docutils .literal
.notranslate}]{.pre} and use just [`.`{.docutils .literal
.notranslate}]{.pre} instead.

This is because the expression [`.//text()`{.docutils .literal
.notranslate}]{.pre} yields a collection of text elements -- a
*node-set*. And when a node-set is converted to a string, which happens
when it is passed as argument to a string function like
[`contains()`{.docutils .literal .notranslate}]{.pre} or
[`starts-with()`{.docutils .literal .notranslate}]{.pre}, it results in
the text for the first element only.

Example:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy import Selector
    >>> sel = Selector(
    ...     text='<a href="#">Click here to go to the <strong>Next Page</strong></a>'
    ... )
:::
:::

Converting a *node-set* to string:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> sel.xpath("//a//text()").getall()  # take a peek at the node-set
    ['Click here to go to the ', 'Next Page']
    >>> sel.xpath("string(//a[1]//text())").getall()  # convert it to string
    ['Click here to go to the ']
:::
:::

A *node* converted to a string, however, puts together the text of
itself plus of all its descendants:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> sel.xpath("//a[1]").getall()  # select the first node
    ['<a href="#">Click here to go to the <strong>Next Page</strong></a>']
    >>> sel.xpath("string(//a[1])").getall()  # convert it to string
    ['Click here to go to the Next Page']
:::
:::

So, using the [`.//text()`{.docutils .literal .notranslate}]{.pre}
node-set won't select anything in this case:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> sel.xpath("//a[contains(.//text(), 'Next Page')]").getall()
    []
:::
:::

But using the [`.`{.docutils .literal .notranslate}]{.pre} to mean the
node, works:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> sel.xpath("//a[contains(., 'Next Page')]").getall()
    ['<a href="#">Click here to go to the <strong>Next Page</strong></a>']
:::
:::
:::

::: {#variables-in-xpath-expressions .section}
[]{#topics-selectors-xpath-variables}

##### Variables in XPath expressions[¶](#variables-in-xpath-expressions "Permalink to this heading"){.headerlink}

XPath allows you to reference variables in your XPath expressions, using
the [`$somevariable`{.docutils .literal .notranslate}]{.pre} syntax.
This is somewhat similar to parameterized queries or prepared statements
in the SQL world where you replace some arguments in your queries with
placeholders like [`?`{.docutils .literal .notranslate}]{.pre}, which
are then substituted with values passed with the query.

Here's an example to match an element based on its "id" attribute value,
without hard-coding it (that was shown previously):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> # `$val` used in the expression, a `val` argument needs to be passed
    >>> response.xpath("//div[@id=$val]/a/text()", val="images").get()
    'Name: My image 1 '
:::
:::

Here's another example, to find the "id" attribute of a
[`<div>`{.docutils .literal .notranslate}]{.pre} tag containing five
[`<a>`{.docutils .literal .notranslate}]{.pre} children (here we pass
the value [`5`{.docutils .literal .notranslate}]{.pre} as an integer):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//div[count(a)=$cnt]/@id", cnt=5).get()
    'images'
:::
:::

All variable references must have a binding value when calling
[`.xpath()`{.docutils .literal .notranslate}]{.pre} (otherwise you'll
get a [`ValueError:`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`XPath`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`error:`{.docutils .literal .notranslate}]{.pre}
exception). This is done by passing as many named arguments as
necessary.

[parsel](https://parsel.readthedocs.io/en/latest/){.reference
.external}, the library powering Scrapy selectors, has more details and
examples on [XPath
variables](https://parsel.readthedocs.io/en/latest/usage.html#variables-in-xpath-expressions){.reference
.external}.
:::

::: {#removing-namespaces .section}
[]{#id2}

##### Removing namespaces[¶](#removing-namespaces "Permalink to this heading"){.headerlink}

When dealing with scraping projects, it is often quite convenient to get
rid of namespaces altogether and just work with element names, to write
more simple/convenient XPaths. You can use the
[`Selector.remove_namespaces()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre} method for that.

Let's show an example that illustrates this with the Python Insider blog
atom feed.

First, we open the shell with the url we want to scrape:

::: {.highlight-sh .notranslate}
::: highlight
    $ scrapy shell https://feeds.feedburner.com/PythonInsider
:::
:::

This is how the file starts:

::: {.highlight-sh .notranslate}
::: highlight
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-stylesheet ...
    <feed xmlns="http://www.w3.org/2005/Atom"
          xmlns:openSearch="http://a9.com/-/spec/opensearchrss/1.0/"
          xmlns:blogger="http://schemas.google.com/blogger/2008"
          xmlns:georss="http://www.georss.org/georss"
          xmlns:gd="http://schemas.google.com/g/2005"
          xmlns:thr="http://purl.org/syndication/thread/1.0"
          xmlns:feedburner="http://rssnamespace.org/feedburner/ext/1.0">
      ...
:::
:::

You can see several namespace declarations including a default
"[http://www.w3.org/2005/Atom](http://www.w3.org/2005/Atom){.reference
.external}" and another one using the "gd:" prefix for
"[http://schemas.google.com/g/2005](http://schemas.google.com/g/2005){.reference
.external}".

Once in the shell we can try selecting all [`<link>`{.docutils .literal
.notranslate}]{.pre} objects and see that it doesn't work (because the
Atom XML namespace is obfuscating those nodes):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//link")
    []
:::
:::

But once we call the [`Selector.remove_namespaces()`{.xref .py .py-meth
.docutils .literal .notranslate}]{.pre} method, all nodes can be
accessed directly by their names:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.selector.remove_namespaces()
    >>> response.xpath("//link")
    [<Selector query='//link' data='<link rel="alternate" type="text/html" h'>,
        <Selector query='//link' data='<link rel="next" type="application/atom+'>,
        ...
:::
:::

If you wonder why the namespace removal procedure isn't always called by
default instead of having to call it manually, this is because of two
reasons, which, in order of relevance, are:

1.  Removing namespaces requires to iterate and modify all nodes in the
    document, which is a reasonably expensive operation to perform by
    default for all documents crawled by Scrapy

2.  There could be some cases where using namespaces is actually
    required, in case some element names clash between namespaces. These
    cases are very rare though.
:::

::: {#using-exslt-extensions .section}
##### Using EXSLT extensions[¶](#using-exslt-extensions "Permalink to this heading"){.headerlink}

Being built atop [lxml](https://lxml.de/){.reference .external}, Scrapy
selectors support some [EXSLT](http://exslt.org/){.reference .external}
extensions and come with these pre-registered namespaces to use in XPath
expressions:

+-----+---------------------------------------+------------------------+
| pre | namespace                             | usage                  |
| fix |                                       |                        |
+=====+=======================================+========================+
| re  | http://exslt.org/regular-expressions  | [regular               |
|     |                                       | expressions](ht        |
|     |                                       | tp://exslt.org/regexp/ |
|     |                                       | index.html){.reference |
|     |                                       | .external}             |
+-----+---------------------------------------+------------------------+
| set | http://exslt.org/sets                 | [set                   |
|     |                                       | manipulation]          |
|     |                                       | (http://exslt.org/set/ |
|     |                                       | index.html){.reference |
|     |                                       | .external}             |
+-----+---------------------------------------+------------------------+

::: {#regular-expressions .section}
###### Regular expressions[¶](#regular-expressions "Permalink to this heading"){.headerlink}

The [`test()`{.docutils .literal .notranslate}]{.pre} function, for
example, can prove quite useful when XPath's [`starts-with()`{.docutils
.literal .notranslate}]{.pre} or [`contains()`{.docutils .literal
.notranslate}]{.pre} are not sufficient.

Example selecting links in list item with a "class" attribute ending
with a digit:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy import Selector
    >>> doc = """
    ... <div>
    ...     <ul>
    ...         <li class="item-0"><a href="link1.html">first item</a></li>
    ...         <li class="item-1"><a href="link2.html">second item</a></li>
    ...         <li class="item-inactive"><a href="link3.html">third item</a></li>
    ...         <li class="item-1"><a href="link4.html">fourth item</a></li>
    ...         <li class="item-0"><a href="link5.html">fifth item</a></li>
    ...     </ul>
    ... </div>
    ... """
    >>> sel = Selector(text=doc, type="html")
    >>> sel.xpath("//li//@href").getall()
    ['link1.html', 'link2.html', 'link3.html', 'link4.html', 'link5.html']
    >>> sel.xpath('//li[re:test(@class, "item-\d$")]//@href').getall()
    ['link1.html', 'link2.html', 'link4.html', 'link5.html']
:::
:::

::: {.admonition .warning}
Warning

C library [`libxslt`{.docutils .literal .notranslate}]{.pre} doesn't
natively support EXSLT regular expressions so
[lxml](https://lxml.de/){.reference .external}'s implementation uses
hooks to Python's [`re`{.docutils .literal .notranslate}]{.pre} module.
Thus, using regexp functions in your XPath expressions may add a small
performance penalty.
:::
:::

::: {#set-operations .section}
###### Set operations[¶](#set-operations "Permalink to this heading"){.headerlink}

These can be handy for excluding parts of a document tree before
extracting text elements for example.

Example extracting microdata (sample content taken from
[https://schema.org/Product](https://schema.org/Product){.reference
.external}) with groups of itemscopes and corresponding itemprops:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> doc = """
    ... <div itemscope itemtype="http://schema.org/Product">
    ...   <span itemprop="name">Kenmore White 17" Microwave</span>
    ...   <img src="kenmore-microwave-17in.jpg" alt='Kenmore 17" Microwave' />
    ...   <div itemprop="aggregateRating"
    ...     itemscope itemtype="http://schema.org/AggregateRating">
    ...    Rated <span itemprop="ratingValue">3.5</span>/5
    ...    based on <span itemprop="reviewCount">11</span> customer reviews
    ...   </div>
    ...   <div itemprop="offers" itemscope itemtype="http://schema.org/Offer">
    ...     <span itemprop="price">$55.00</span>
    ...     <link itemprop="availability" href="http://schema.org/InStock" />In stock
    ...   </div>
    ...   Product description:
    ...   <span itemprop="description">0.7 cubic feet countertop microwave.
    ...   Has six preset cooking categories and convenience features like
    ...   Add-A-Minute and Child Lock.</span>
    ...   Customer reviews:
    ...   <div itemprop="review" itemscope itemtype="http://schema.org/Review">
    ...     <span itemprop="name">Not a happy camper</span> -
    ...     by <span itemprop="author">Ellie</span>,
    ...     <meta itemprop="datePublished" content="2011-04-01">April 1, 2011
    ...     <div itemprop="reviewRating" itemscope itemtype="http://schema.org/Rating">
    ...       <meta itemprop="worstRating" content = "1">
    ...       <span itemprop="ratingValue">1</span>/
    ...       <span itemprop="bestRating">5</span>stars
    ...     </div>
    ...     <span itemprop="description">The lamp burned out and now I have to replace
    ...     it. </span>
    ...   </div>
    ...   <div itemprop="review" itemscope itemtype="http://schema.org/Review">
    ...     <span itemprop="name">Value purchase</span> -
    ...     by <span itemprop="author">Lucas</span>,
    ...     <meta itemprop="datePublished" content="2011-03-25">March 25, 2011
    ...     <div itemprop="reviewRating" itemscope itemtype="http://schema.org/Rating">
    ...       <meta itemprop="worstRating" content = "1"/>
    ...       <span itemprop="ratingValue">4</span>/
    ...       <span itemprop="bestRating">5</span>stars
    ...     </div>
    ...     <span itemprop="description">Great microwave for the price. It is small and
    ...     fits in my apartment.</span>
    ...   </div>
    ...   ...
    ... </div>
    ... """
    >>> sel = Selector(text=doc, type="html")
    >>> for scope in sel.xpath("//div[@itemscope]"):
    ...     print("current scope:", scope.xpath("@itemtype").getall())
    ...     props = scope.xpath(
    ...         """
    ...                 set:difference(./descendant::*/@itemprop,
    ...                                .//*[@itemscope]/*/@itemprop)"""
    ...     )
    ...     print(f"    properties: {props.getall()}")
    ...     print("")
    ...

    current scope: ['http://schema.org/Product']
        properties: ['name', 'aggregateRating', 'offers', 'description', 'review', 'review']

    current scope: ['http://schema.org/AggregateRating']
        properties: ['ratingValue', 'reviewCount']

    current scope: ['http://schema.org/Offer']
        properties: ['price', 'availability']

    current scope: ['http://schema.org/Review']
        properties: ['name', 'author', 'datePublished', 'reviewRating', 'description']

    current scope: ['http://schema.org/Rating']
        properties: ['worstRating', 'ratingValue', 'bestRating']

    current scope: ['http://schema.org/Review']
        properties: ['name', 'author', 'datePublished', 'reviewRating', 'description']

    current scope: ['http://schema.org/Rating']
        properties: ['worstRating', 'ratingValue', 'bestRating']
:::
:::

Here we first iterate over [`itemscope`{.docutils .literal
.notranslate}]{.pre} elements, and for each one, we look for all
[`itemprops`{.docutils .literal .notranslate}]{.pre} elements and
exclude those that are themselves inside another [`itemscope`{.docutils
.literal .notranslate}]{.pre}.
:::
:::

::: {#other-xpath-extensions .section}
##### Other XPath extensions[¶](#other-xpath-extensions "Permalink to this heading"){.headerlink}

Scrapy selectors also provide a sorely missed XPath extension function
[`has-class`{.docutils .literal .notranslate}]{.pre} that returns
[`True`{.docutils .literal .notranslate}]{.pre} for nodes that have all
of the specified HTML classes.

For the following HTML:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy.http import HtmlResponse
    >>> response = HtmlResponse(
    ...     url="http://example.com",
    ...     body="""
    ... <html>
    ...     <body>
    ...         <p class="foo bar-baz">First</p>
    ...         <p class="foo">Second</p>
    ...         <p class="bar">Third</p>
    ...         <p>Fourth</p>
    ...     </body>
    ... </html>
    ... """,
    ...     encoding="utf-8",
    ... )
:::
:::

You can use it like this:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//p[has-class("foo")]')
    [<Selector query='//p[has-class("foo")]' data='<p class="foo bar-baz">First</p>'>,
    <Selector query='//p[has-class("foo")]' data='<p class="foo">Second</p>'>]
    >>> response.xpath('//p[has-class("foo", "bar-baz")]')
    [<Selector query='//p[has-class("foo", "bar-baz")]' data='<p class="foo bar-baz">First</p>'>]
    >>> response.xpath('//p[has-class("foo", "bar")]')
    []
:::
:::

So XPath [`//p[has-class("foo",`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`"bar-baz")]`{.docutils .literal .notranslate}]{.pre} is
roughly equivalent to CSS [`p.foo.bar-baz`{.docutils .literal
.notranslate}]{.pre}. Please note, that it is slower in most of the
cases, because it's a pure-Python function that's invoked for every node
in question whereas the CSS lookup is translated into XPath and thus
runs more efficiently, so performance-wise its uses are limited to
situations that are not easily described with CSS selectors.

Parsel also simplifies adding your own XPath extensions.

[[parsel.xpathfuncs.]{.pre}]{.sig-prename .descclassname}[[set_xpathfunc]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[fname]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[func]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/xpathfuncs.html#set_xpathfunc){.reference .internal}[¶](#parsel.xpathfuncs.set_xpathfunc "Permalink to this definition"){.headerlink}

:   Register a custom extension function to use in XPath expressions.

    The function [`func`{.docutils .literal .notranslate}]{.pre}
    registered under [`fname`{.docutils .literal .notranslate}]{.pre}
    identifier will be called for every matching node, being passed a
    [`context`{.docutils .literal .notranslate}]{.pre} parameter as well
    as any parameters passed from the corresponding XPath expression.

    If [`func`{.docutils .literal .notranslate}]{.pre} is
    [`None`{.docutils .literal .notranslate}]{.pre}, the extension
    function will be removed.

    See more [in lxml
    documentation](https://lxml.de/extensions.html#xpath-extension-functions){.reference
    .external}.
:::
:::

::: {#module-scrapy.selector .section}
[]{#built-in-selectors-reference}[]{#topics-selectors-ref}

#### Built-in Selectors reference[¶](#module-scrapy.selector "Permalink to this heading"){.headerlink}

::: {#selector-objects .section}
##### Selector objects[¶](#selector-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.selector.]{.pre}]{.sig-prename .descclassname}[[Selector]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[\*]{.pre}]{.o}[[args]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/selector/unified.html#Selector){.reference .internal}[¶](#scrapy.selector.Selector "Permalink to this definition"){.headerlink}

:   An instance of [[`Selector`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
    .internal} is a wrapper over response to select certain parts of its
    content.

    [`response`{.docutils .literal .notranslate}]{.pre} is an
    [[`HtmlResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.HtmlResponse "scrapy.http.HtmlResponse"){.reference
    .internal} or an [[`XmlResponse`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.XmlResponse "scrapy.http.XmlResponse"){.reference
    .internal} object that will be used for selecting and extracting
    data.

    [`text`{.docutils .literal .notranslate}]{.pre} is a unicode string
    or utf-8 encoded text for cases when a [`response`{.docutils
    .literal .notranslate}]{.pre} isn't available. Using
    [`text`{.docutils .literal .notranslate}]{.pre} and
    [`response`{.docutils .literal .notranslate}]{.pre} together is
    undefined behavior.

    [`type`{.docutils .literal .notranslate}]{.pre} defines the selector
    type, it can be [`"html"`{.docutils .literal .notranslate}]{.pre},
    [`"xml"`{.docutils .literal .notranslate}]{.pre} or
    [`None`{.docutils .literal .notranslate}]{.pre} (default).

    If [`type`{.docutils .literal .notranslate}]{.pre} is
    [`None`{.docutils .literal .notranslate}]{.pre}, the selector
    automatically chooses the best type based on [`response`{.docutils
    .literal .notranslate}]{.pre} type (see below), or defaults to
    [`"html"`{.docutils .literal .notranslate}]{.pre} in case it is used
    together with [`text`{.docutils .literal .notranslate}]{.pre}.

    If [`type`{.docutils .literal .notranslate}]{.pre} is
    [`None`{.docutils .literal .notranslate}]{.pre} and a
    [`response`{.docutils .literal .notranslate}]{.pre} is passed, the
    selector type is inferred from the response type as follows:

    -   [`"html"`{.docutils .literal .notranslate}]{.pre} for
        [[`HtmlResponse`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.HtmlResponse "scrapy.http.HtmlResponse"){.reference
        .internal} type

    -   [`"xml"`{.docutils .literal .notranslate}]{.pre} for
        [[`XmlResponse`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.XmlResponse "scrapy.http.XmlResponse"){.reference
        .internal} type

    -   [`"html"`{.docutils .literal .notranslate}]{.pre} for anything
        else

    Otherwise, if [`type`{.docutils .literal .notranslate}]{.pre} is
    set, the selector type will be forced and no detection will occur.

    [[xpath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[query]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[namespaces]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Mapping]{.pre}](https://docs.python.org/3/library/typing.html#typing.Mapping "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[SelectorList]{.pre}[[\[]{.pre}]{.p}[\_SelectorType]{.pre}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.xpath){.reference .internal}[¶](#scrapy.selector.Selector.xpath "Permalink to this definition"){.headerlink}

    :   Find nodes matching the xpath [`query`{.docutils .literal
        .notranslate}]{.pre} and return the result as a
        [[`SelectorList`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
        .internal} instance with all elements flattened. List elements
        implement [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal} interface too.

        [`query`{.docutils .literal .notranslate}]{.pre} is a string
        containing the XPATH query to apply.

        [`namespaces`{.docutils .literal .notranslate}]{.pre} is an
        optional [`prefix:`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`namespace-uri`{.docutils .literal
        .notranslate}]{.pre} mapping (dict) for additional prefixes to
        those registered with [`register_namespace(prefix,`{.docutils
        .literal .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`uri)`{.docutils .literal .notranslate}]{.pre}.
        Contrary to [`register_namespace()`{.docutils .literal
        .notranslate}]{.pre}, these prefixes are not saved for future
        calls.

        Any additional named arguments can be used to pass values for
        XPath variables in the XPath expression, e.g.:

        ::: {.highlight-python .notranslate}
        ::: highlight
            selector.xpath('//a[href=$url]', url="http://www.example.com")
        :::
        :::

        ::: {.admonition .note}
        Note

        For convenience, this method can be called as
        [`response.xpath()`{.docutils .literal .notranslate}]{.pre}
        :::

    [[css]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[query]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[SelectorList]{.pre}[[\[]{.pre}]{.p}[\_SelectorType]{.pre}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.css){.reference .internal}[¶](#scrapy.selector.Selector.css "Permalink to this definition"){.headerlink}

    :   Apply the given CSS selector and return a [[`SelectorList`{.xref
        .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
        .internal} instance.

        [`query`{.docutils .literal .notranslate}]{.pre} is a string
        containing the CSS selector to apply.

        In the background, CSS queries are translated into XPath queries
        using
        [cssselect](https://pypi.python.org/pypi/cssselect/){.reference
        .external} library and run [`.xpath()`{.docutils .literal
        .notranslate}]{.pre} method.

        ::: {.admonition .note}
        Note

        For convenience, this method can be called as
        [`response.css()`{.docutils .literal .notranslate}]{.pre}
        :::

    [[get]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.get){.reference .internal}[¶](#scrapy.selector.Selector.get "Permalink to this definition"){.headerlink}

    :   Serialize and return the matched nodes in a single string.
        Percent encoded content is unquoted.

        See also: [[extract() and extract_first()]{.std
        .std-ref}](#old-extraction-api){.hoverxref .tooltip .reference
        .internal}

    [[attrib]{.pre}]{.sig-name .descname}[¶](#scrapy.selector.Selector.attrib "Permalink to this definition"){.headerlink}

    :   Return the attributes dictionary for underlying element.

        See also: [[Selecting element attributes]{.std
        .std-ref}](#selecting-attributes){.hoverxref .tooltip .reference
        .internal}.

    [[re]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[regex]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Pattern]{.pre}](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[replace_entities]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.re){.reference .internal}[¶](#scrapy.selector.Selector.re "Permalink to this definition"){.headerlink}

    :   Apply the given regex and return a list of strings with the
        matches.

        [`regex`{.docutils .literal .notranslate}]{.pre} can be either a
        compiled regular expression or a string which will be compiled
        to a regular expression using [`re.compile(regex)`{.docutils
        .literal .notranslate}]{.pre}.

        By default, character entity references are replaced by their
        corresponding character (except for [`&amp;`{.docutils .literal
        .notranslate}]{.pre} and [`&lt;`{.docutils .literal
        .notranslate}]{.pre}). Passing [`replace_entities`{.docutils
        .literal .notranslate}]{.pre} as [`False`{.docutils .literal
        .notranslate}]{.pre} switches off these replacements.

    [[re_first]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[regex]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Pattern]{.pre}](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[replace_entities]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.re_first){.reference .internal}[¶](#scrapy.selector.Selector.re_first "Permalink to this definition"){.headerlink}\
    [[re_first]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[regex]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Pattern]{.pre}](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[replace_entities]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}

    :   Apply the given regex and return the first string which matches.
        If there is no match, return the default value
        ([`None`{.docutils .literal .notranslate}]{.pre} if the argument
        is not provided).

        By default, character entity references are replaced by their
        corresponding character (except for [`&amp;`{.docutils .literal
        .notranslate}]{.pre} and [`&lt;`{.docutils .literal
        .notranslate}]{.pre}). Passing [`replace_entities`{.docutils
        .literal .notranslate}]{.pre} as [`False`{.docutils .literal
        .notranslate}]{.pre} switches off these replacements.

    [[register_namespace]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[prefix]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[uri]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.register_namespace){.reference .internal}[¶](#scrapy.selector.Selector.register_namespace "Permalink to this definition"){.headerlink}

    :   Register the given namespace to be used in this
        [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal}. Without registering namespaces you can't select or
        extract data from non-standard namespaces. See [[Selector
        examples on XML response]{.std
        .std-ref}](#selector-examples-xml){.hoverxref .tooltip
        .reference .internal}.

    [[remove_namespaces]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.remove_namespaces){.reference .internal}[¶](#scrapy.selector.Selector.remove_namespaces "Permalink to this definition"){.headerlink}

    :   Remove all namespaces, allowing to traverse the document using
        namespace-less xpaths. See [[Removing namespaces]{.std
        .std-ref}](#removing-namespaces){.hoverxref .tooltip .reference
        .internal}.

    [[\_\_bool\_\_]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.__bool__){.reference .internal}[¶](#scrapy.selector.Selector.__bool__ "Permalink to this definition"){.headerlink}

    :   Return [`True`{.docutils .literal .notranslate}]{.pre} if there
        is any real content selected or [`False`{.docutils .literal
        .notranslate}]{.pre} otherwise. In other words, the boolean
        value of a [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal} is given by the contents it selects.

    [[getall]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#Selector.getall){.reference .internal}[¶](#scrapy.selector.Selector.getall "Permalink to this definition"){.headerlink}

    :   Serialize and return the matched node in a 1-element list of
        strings.

        This method is added to Selector for consistency; it is more
        useful with SelectorList. See also: [[extract() and
        extract_first()]{.std .std-ref}](#old-extraction-api){.hoverxref
        .tooltip .reference .internal}
:::

::: {#selectorlist-objects .section}
##### SelectorList objects[¶](#selectorlist-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.selector.]{.pre}]{.sig-prename .descclassname}[[SelectorList]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[iterable]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[/]{.pre}]{.o}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/selector/unified.html#SelectorList){.reference .internal}[¶](#scrapy.selector.SelectorList "Permalink to this definition"){.headerlink}

:   The [[`SelectorList`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
    .internal} class is a subclass of the builtin [`list`{.docutils
    .literal .notranslate}]{.pre} class, which provides a few additional
    methods.

    [[xpath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[xpath]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[namespaces]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Mapping]{.pre}](https://docs.python.org/3/library/typing.html#typing.Mapping "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[SelectorList]{.pre}[[\[]{.pre}]{.p}[\_SelectorType]{.pre}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#SelectorList.xpath){.reference .internal}[¶](#scrapy.selector.SelectorList.xpath "Permalink to this definition"){.headerlink}

    :   Call the [`.xpath()`{.docutils .literal .notranslate}]{.pre}
        method for each element in this list and return their results
        flattened as another [[`SelectorList`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
        .internal}.

        [`xpath`{.docutils .literal .notranslate}]{.pre} is the same
        argument as the one in [[`Selector.xpath()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.Selector.xpath "scrapy.selector.Selector.xpath"){.reference
        .internal}

        [`namespaces`{.docutils .literal .notranslate}]{.pre} is an
        optional [`prefix:`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`namespace-uri`{.docutils .literal
        .notranslate}]{.pre} mapping (dict) for additional prefixes to
        those registered with [`register_namespace(prefix,`{.docutils
        .literal .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`uri)`{.docutils .literal .notranslate}]{.pre}.
        Contrary to [`register_namespace()`{.docutils .literal
        .notranslate}]{.pre}, these prefixes are not saved for future
        calls.

        Any additional named arguments can be used to pass values for
        XPath variables in the XPath expression, e.g.:

        ::: {.highlight-python .notranslate}
        ::: highlight
            selector.xpath('//a[href=$url]', url="http://www.example.com")
        :::
        :::

    [[css]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[query]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[SelectorList]{.pre}[[\[]{.pre}]{.p}[\_SelectorType]{.pre}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#SelectorList.css){.reference .internal}[¶](#scrapy.selector.SelectorList.css "Permalink to this definition"){.headerlink}

    :   Call the [`.css()`{.docutils .literal .notranslate}]{.pre}
        method for each element in this list and return their results
        flattened as another [[`SelectorList`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
        .internal}.

        [`query`{.docutils .literal .notranslate}]{.pre} is the same
        argument as the one in [[`Selector.css()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.selector.Selector.css "scrapy.selector.Selector.css"){.reference
        .internal}

    [[getall]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#SelectorList.getall){.reference .internal}[¶](#scrapy.selector.SelectorList.getall "Permalink to this definition"){.headerlink}

    :   Call the [`.get()`{.docutils .literal .notranslate}]{.pre}
        method for each element is this list and return their results
        flattened, as a list of strings.

        See also: [[extract() and extract_first()]{.std
        .std-ref}](#old-extraction-api){.hoverxref .tooltip .reference
        .internal}

    [[get]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#SelectorList.get){.reference .internal}[¶](#scrapy.selector.SelectorList.get "Permalink to this definition"){.headerlink}\
    [[get]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}

    :   Return the result of [`.get()`{.docutils .literal
        .notranslate}]{.pre} for the first element in this list. If the
        list is empty, return the default value.

        See also: [[extract() and extract_first()]{.std
        .std-ref}](#old-extraction-api){.hoverxref .tooltip .reference
        .internal}

    [[re]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[regex]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Pattern]{.pre}](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[replace_entities]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#SelectorList.re){.reference .internal}[¶](#scrapy.selector.SelectorList.re "Permalink to this definition"){.headerlink}

    :   Call the [`.re()`{.docutils .literal .notranslate}]{.pre} method
        for each element in this list and return their results
        flattened, as a list of strings.

        By default, character entity references are replaced by their
        corresponding character (except for [`&amp;`{.docutils .literal
        .notranslate}]{.pre} and [`&lt;`{.docutils .literal
        .notranslate}]{.pre}. Passing [`replace_entities`{.docutils
        .literal .notranslate}]{.pre} as [`False`{.docutils .literal
        .notranslate}]{.pre} switches off these replacements.

    [[re_first]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[regex]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Pattern]{.pre}](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[replace_entities]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/parsel/selector.html#SelectorList.re_first){.reference .internal}[¶](#scrapy.selector.SelectorList.re_first "Permalink to this definition"){.headerlink}\
    [[re_first]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[regex]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Pattern]{.pre}](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[replace_entities]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}

    :   Call the [`.re()`{.docutils .literal .notranslate}]{.pre} method
        for the first element in this list and return the result in an
        string. If the list is empty or the regex doesn't match
        anything, return the default value ([`None`{.docutils .literal
        .notranslate}]{.pre} if the argument is not provided).

        By default, character entity references are replaced by their
        corresponding character (except for [`&amp;`{.docutils .literal
        .notranslate}]{.pre} and [`&lt;`{.docutils .literal
        .notranslate}]{.pre}. Passing [`replace_entities`{.docutils
        .literal .notranslate}]{.pre} as [`False`{.docutils .literal
        .notranslate}]{.pre} switches off these replacements.

    [[attrib]{.pre}]{.sig-name .descname}[¶](#scrapy.selector.SelectorList.attrib "Permalink to this definition"){.headerlink}

    :   Return the attributes dictionary for the first element. If the
        list is empty, return an empty dict.

        See also: [[Selecting element attributes]{.std
        .std-ref}](#selecting-attributes){.hoverxref .tooltip .reference
        .internal}.
:::
:::

::: {#examples .section}
[]{#selector-examples}

#### Examples[¶](#examples "Permalink to this heading"){.headerlink}

::: {#selector-examples-on-html-response .section}
[]{#selector-examples-html}

##### Selector examples on HTML response[¶](#selector-examples-on-html-response "Permalink to this heading"){.headerlink}

Here are some [[`Selector`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
.internal} examples to illustrate several concepts. In all cases, we
assume there is already a [[`Selector`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
.internal} instantiated with a [[`HtmlResponse`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.HtmlResponse "scrapy.http.HtmlResponse"){.reference
.internal} object like this:

::: {.highlight-python .notranslate}
::: highlight
    sel = Selector(html_response)
:::
:::

1.  Select all [`<h1>`{.docutils .literal .notranslate}]{.pre} elements
    from an HTML response body, returning a list of [[`Selector`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
    .internal} objects (i.e. a [[`SelectorList`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
    .internal} object):

    ::: {.highlight-python .notranslate}
    ::: highlight
        sel.xpath("//h1")
    :::
    :::

2.  Extract the text of all [`<h1>`{.docutils .literal
    .notranslate}]{.pre} elements from an HTML response body, returning
    a list of strings:

    ::: {.highlight-python .notranslate}
    ::: highlight
        sel.xpath("//h1").getall()  # this includes the h1 tag
        sel.xpath("//h1/text()").getall()  # this excludes the h1 tag
    :::
    :::

3.  Iterate over all [`<p>`{.docutils .literal .notranslate}]{.pre} tags
    and print their class attribute:

    ::: {.highlight-python .notranslate}
    ::: highlight
        for node in sel.xpath("//p"):
            print(node.attrib["class"])
    :::
    :::
:::

::: {#selector-examples-on-xml-response .section}
[]{#selector-examples-xml}

##### Selector examples on XML response[¶](#selector-examples-on-xml-response "Permalink to this heading"){.headerlink}

Here are some examples to illustrate concepts for [[`Selector`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
.internal} objects instantiated with an [[`XmlResponse`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.XmlResponse "scrapy.http.XmlResponse"){.reference
.internal} object:

::: {.highlight-python .notranslate}
::: highlight
    sel = Selector(xml_response)
:::
:::

1.  Select all [`<product>`{.docutils .literal .notranslate}]{.pre}
    elements from an XML response body, returning a list of
    [[`Selector`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
    .internal} objects (i.e. a [[`SelectorList`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
    .internal} object):

    ::: {.highlight-python .notranslate}
    ::: highlight
        sel.xpath("//product")
    :::
    :::

2.  Extract all prices from a [Google Base XML
    feed](https://support.google.com/merchants/answer/160589?hl=en&ref_topic=2473799){.reference
    .external} which requires registering a namespace:

    ::: {.highlight-python .notranslate}
    ::: highlight
        sel.register_namespace("g", "http://base.google.com/ns/1.0")
        sel.xpath("//g:price").getall()
    :::
    :::
:::
:::
:::

[]{#document-topics/items}

::: {#module-scrapy.item .section}
[]{#items}[]{#topics-items}

### Items[¶](#module-scrapy.item "Permalink to this heading"){.headerlink}

The main goal in scraping is to extract structured data from
unstructured sources, typically, web pages. [[Spiders]{.std
.std-ref}](index.html#topics-spiders){.hoverxref .tooltip .reference
.internal} may return the extracted data as items, Python objects that
define key-value pairs.

Scrapy supports [[multiple types of items]{.std
.std-ref}](#item-types){.hoverxref .tooltip .reference .internal}. When
you create an item, you may use whichever type of item you want. When
you write code that receives an item, your code should [[work for any
item type]{.std .std-ref}](#supporting-item-types){.hoverxref .tooltip
.reference .internal}.

::: {#item-types .section}
[]{#id1}

#### Item Types[¶](#item-types "Permalink to this heading"){.headerlink}

Scrapy supports the following types of items, via the
[itemadapter](https://github.com/scrapy/itemadapter){.reference
.external} library: [[dictionaries]{.std
.std-ref}](#dict-items){.hoverxref .tooltip .reference .internal},
[[Item objects]{.std .std-ref}](#item-objects){.hoverxref .tooltip
.reference .internal}, [[dataclass objects]{.std
.std-ref}](#dataclass-items){.hoverxref .tooltip .reference .internal},
and [[attrs objects]{.std .std-ref}](#attrs-items){.hoverxref .tooltip
.reference .internal}.

::: {#dictionaries .section}
[]{#dict-items}

##### Dictionaries[¶](#dictionaries "Permalink to this heading"){.headerlink}

As an item type, [[`dict`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
.external} is convenient and familiar.
:::

::: {#item-objects .section}
[]{#id2}

##### Item objects[¶](#item-objects "Permalink to this heading"){.headerlink}

[`Item`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
provides a [[`dict`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
.external}-like API plus additional features that make it the most
feature-complete item type:

*[class]{.pre}[ ]{.w}*[[scrapy.item.]{.pre}]{.sig-prename .descclassname}[[Item]{.pre}]{.sig-name .descname}[(]{.sig-paren}[\[]{.optional}*[[arg]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[¶](#scrapy.item.scrapy.item.Item "Permalink to this definition"){.headerlink}

:   

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.]{.pre}]{.sig-prename .descclassname}[[Item]{.pre}]{.sig-name .descname}[(]{.sig-paren}[\[]{.optional}*[[arg]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[¶](#scrapy.item.scrapy.Item "Permalink to this definition"){.headerlink}

:   [`Item`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
    objects replicate the standard [[`dict`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
    .external} API, including its [`__init__`{.docutils .literal
    .notranslate}]{.pre} method.

    [`Item`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
    allows defining field names, so that:

    -   [[`KeyError`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#KeyError "(in Python v3.12)"){.reference
        .external} is raised when using undefined field names (i.e.
        prevents typos going unnoticed)

    -   [[Item exporters]{.std
        .std-ref}](index.html#topics-exporters){.hoverxref .tooltip
        .reference .internal} can export all fields by default even if
        the first scraped object does not have values for all of them

    [`Item`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
    also allows defining field metadata, which can be used to
    [[customize serialization]{.std
    .std-ref}](index.html#topics-exporters-field-serialization){.hoverxref
    .tooltip .reference .internal}.

    [`trackref`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre} tracks [`Item`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre} objects to help find memory leaks (see
    [[Debugging memory leaks with trackref]{.std
    .std-ref}](index.html#topics-leaks-trackrefs){.hoverxref .tooltip
    .reference .internal}).

    [`Item`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
    objects also provide the following additional API members:

    [[Item.]{.pre}]{.sig-prename .descclassname}[[copy]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[¶](#scrapy.scrapy.Item.Item.copy "Permalink to this definition"){.headerlink}

    :   

    [[Item.]{.pre}]{.sig-prename .descclassname}[[deepcopy]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[¶](#scrapy.scrapy.Item.Item.deepcopy "Permalink to this definition"){.headerlink}

    :   Return a [[`deepcopy()`{.xref .py .py-func .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/copy.html#copy.deepcopy "(in Python v3.12)"){.reference
        .external} of this item.

    [[fields]{.pre}]{.sig-name .descname}[¶](#scrapy.item.scrapy.Item.fields "Permalink to this definition"){.headerlink}

    :   A dictionary containing *all declared fields* for this Item, not
        only those populated. The keys are the field names and the
        values are the [`Field`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre} objects used in the [[Item
        declaration]{.std .std-ref}](#topics-items-declaring){.hoverxref
        .tooltip .reference .internal}.

Example:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.item import Item, Field


    class CustomItem(Item):
        one_field = Field()
        another_field = Field()
:::
:::
:::

::: {#dataclass-objects .section}
[]{#dataclass-items}

##### Dataclass objects[¶](#dataclass-objects "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.2.]{.versionmodified .added}
:::

[[`dataclass()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/dataclasses.html#dataclasses.dataclass "(in Python v3.12)"){.reference
.external} allows defining item classes with field names, so that [[item
exporters]{.std .std-ref}](index.html#topics-exporters){.hoverxref
.tooltip .reference .internal} can export all fields by default even if
the first scraped object does not have values for all of them.

Additionally, [`dataclass`{.docutils .literal .notranslate}]{.pre} items
also allow to:

-   define the type and default value of each defined field.

-   define custom field metadata through [[`dataclasses.field()`{.xref
    .py .py-func .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/dataclasses.html#dataclasses.field "(in Python v3.12)"){.reference
    .external}, which can be used to [[customize serialization]{.std
    .std-ref}](index.html#topics-exporters-field-serialization){.hoverxref
    .tooltip .reference .internal}.

Example:

::: {.highlight-python .notranslate}
::: highlight
    from dataclasses import dataclass


    @dataclass
    class CustomItem:
        one_field: str
        another_field: int
:::
:::

::: {.admonition .note}
Note

Field types are not enforced at run time.
:::
:::

::: {#attr-s-objects .section}
[]{#attrs-items}

##### attr.s objects[¶](#attr-s-objects "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.2.]{.versionmodified .added}
:::

[[`attr.s()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](https://www.attrs.org/en/stable/api-attr.html#attr.s "(in attrs v23.1)"){.reference
.external} allows defining item classes with field names, so that [[item
exporters]{.std .std-ref}](index.html#topics-exporters){.hoverxref
.tooltip .reference .internal} can export all fields by default even if
the first scraped object does not have values for all of them.

Additionally, [`attr.s`{.docutils .literal .notranslate}]{.pre} items
also allow to:

-   define the type and default value of each defined field.

-   define custom field [[metadata]{.xref .std
    .std-ref}](https://www.attrs.org/en/stable/examples.html#metadata "(in attrs v23.1)"){.reference
    .external}, which can be used to [[customize serialization]{.std
    .std-ref}](index.html#topics-exporters-field-serialization){.hoverxref
    .tooltip .reference .internal}.

In order to use this type, the [[attrs package]{.xref .std
.std-doc}](https://www.attrs.org/en/stable/index.html "(in attrs v23.1)"){.reference
.external} needs to be installed.

Example:

::: {.highlight-python .notranslate}
::: highlight
    import attr


    @attr.s
    class CustomItem:
        one_field = attr.ib()
        another_field = attr.ib()
:::
:::
:::
:::

::: {#working-with-item-objects .section}
#### Working with Item objects[¶](#working-with-item-objects "Permalink to this heading"){.headerlink}

::: {#declaring-item-subclasses .section}
[]{#topics-items-declaring}

##### Declaring Item subclasses[¶](#declaring-item-subclasses "Permalink to this heading"){.headerlink}

Item subclasses are declared using a simple class definition syntax and
[`Field`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
objects. Here is an example:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class Product(scrapy.Item):
        name = scrapy.Field()
        price = scrapy.Field()
        stock = scrapy.Field()
        tags = scrapy.Field()
        last_updated = scrapy.Field(serializer=str)
:::
:::

::: {.admonition .note}
Note

Those familiar with [Django](https://www.djangoproject.com/){.reference
.external} will notice that Scrapy Items are declared similar to [Django
Models](https://docs.djangoproject.com/en/dev/topics/db/models/){.reference
.external}, except that Scrapy Items are much simpler as there is no
concept of different field types.
:::
:::

::: {#declaring-fields .section}
[]{#topics-items-fields}

##### Declaring fields[¶](#declaring-fields "Permalink to this heading"){.headerlink}

[`Field`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
objects are used to specify metadata for each field. For example, the
serializer function for the [`last_updated`{.docutils .literal
.notranslate}]{.pre} field illustrated in the example above.

You can specify any kind of metadata for each field. There is no
restriction on the values accepted by [`Field`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre} objects. For this same reason,
there is no reference list of all available metadata keys. Each key
defined in [`Field`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} objects could be used by a different component, and
only those components know about it. You can also define and use any
other [`Field`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} key in your project too, for your own needs. The
main goal of [`Field`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} objects is to provide a way to define all field
metadata in one place. Typically, those components whose behaviour
depends on each field use certain field keys to configure that
behaviour. You must refer to their documentation to see which metadata
keys are used by each component.

It's important to note that the [`Field`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre} objects used to declare the item do not
stay assigned as class attributes. Instead, they can be accessed through
the [`Item.fields`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} attribute.

*[class]{.pre}[ ]{.w}*[[scrapy.item.]{.pre}]{.sig-prename .descclassname}[[Field]{.pre}]{.sig-name .descname}[(]{.sig-paren}[\[]{.optional}*[[arg]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[¶](#scrapy.item.scrapy.item.Field "Permalink to this definition"){.headerlink}

:   

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.]{.pre}]{.sig-prename .descclassname}[[Field]{.pre}]{.sig-name .descname}[(]{.sig-paren}[\[]{.optional}*[[arg]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[¶](#scrapy.item.scrapy.Field "Permalink to this definition"){.headerlink}

:   The [`Field`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} class is just an alias to the built-in
    [[`dict`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
    .external} class and doesn't provide any extra functionality or
    attributes. In other words, [`Field`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre} objects are plain-old Python dicts. A
    separate class is used to support the [[item declaration
    syntax]{.std .std-ref}](#topics-items-declaring){.hoverxref .tooltip
    .reference .internal} based on class attributes.

::: {.admonition .note}
Note

Field metadata can also be declared for [`dataclass`{.docutils .literal
.notranslate}]{.pre} and [`attrs`{.docutils .literal
.notranslate}]{.pre} items. Please refer to the documentation for
[dataclasses.field](https://docs.python.org/3/library/dataclasses.html#dataclasses.field){.reference
.external} and
[attr.ib](https://www.attrs.org/en/stable/api.html#attr.ib){.reference
.external} for additional information.
:::
:::

::: {#id3 .section}
##### Working with Item objects[¶](#id3 "Permalink to this heading"){.headerlink}

Here are some examples of common tasks performed with items, using the
[`Product`{.docutils .literal .notranslate}]{.pre} item [[declared
above]{.std .std-ref}](#topics-items-declaring){.hoverxref .tooltip
.reference .internal}. You will notice the API is very similar to the
[[`dict`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
.external} API.

::: {#creating-items .section}
###### Creating items[¶](#creating-items "Permalink to this heading"){.headerlink}

::: {.highlight-pycon .notranslate}
::: highlight
    >>> product = Product(name="Desktop PC", price=1000)
    >>> print(product)
    Product(name='Desktop PC', price=1000)
:::
:::
:::

::: {#getting-field-values .section}
###### Getting field values[¶](#getting-field-values "Permalink to this heading"){.headerlink}

::: {.highlight-pycon .notranslate}
::: highlight
    >>> product["name"]
    Desktop PC
    >>> product.get("name")
    Desktop PC

    >>> product["price"]
    1000

    >>> product["last_updated"]
    Traceback (most recent call last):
        ...
    KeyError: 'last_updated'

    >>> product.get("last_updated", "not set")
    not set

    >>> product["lala"]  # getting unknown field
    Traceback (most recent call last):
        ...
    KeyError: 'lala'

    >>> product.get("lala", "unknown field")
    'unknown field'

    >>> "name" in product  # is name field populated?
    True

    >>> "last_updated" in product  # is last_updated populated?
    False

    >>> "last_updated" in product.fields  # is last_updated a declared field?
    True

    >>> "lala" in product.fields  # is lala a declared field?
    False
:::
:::
:::

::: {#setting-field-values .section}
###### Setting field values[¶](#setting-field-values "Permalink to this heading"){.headerlink}

::: {.highlight-pycon .notranslate}
::: highlight
    >>> product["last_updated"] = "today"
    >>> product["last_updated"]
    today

    >>> product["lala"] = "test"  # setting unknown field
    Traceback (most recent call last):
        ...
    KeyError: 'Product does not support field: lala'
:::
:::
:::

::: {#accessing-all-populated-values .section}
###### Accessing all populated values[¶](#accessing-all-populated-values "Permalink to this heading"){.headerlink}

To access all populated values, just use the typical [[`dict`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
.external} API:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> product.keys()
    ['price', 'name']

    >>> product.items()
    [('price', 1000), ('name', 'Desktop PC')]
:::
:::
:::

::: {#copying-items .section}
[]{#id4}

###### Copying items[¶](#copying-items "Permalink to this heading"){.headerlink}

To copy an item, you must first decide whether you want a shallow copy
or a deep copy.

If your item contains [[mutable]{.xref .std
.std-term}](https://docs.python.org/3/glossary.html#term-mutable "(in Python v3.12)"){.reference
.external} values like lists or dictionaries, a shallow copy will keep
references to the same mutable values across all different copies.

For example, if you have an item with a list of tags, and you create a
shallow copy of that item, both the original item and the copy have the
same list of tags. Adding a tag to the list of one of the items will add
the tag to the other item as well.

If that is not the desired behavior, use a deep copy instead.

See [[`copy`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/copy.html#module-copy "(in Python v3.12)"){.reference
.external} for more information.

To create a shallow copy of an item, you can either call [`copy()`{.xref
.py .py-meth .docutils .literal .notranslate}]{.pre} on an existing item
([`product2`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`=`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`product.copy()`{.docutils .literal .notranslate}]{.pre})
or instantiate your item class from an existing item
([`product2`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`=`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`Product(product)`{.docutils .literal
.notranslate}]{.pre}).

To create a deep copy, call [`deepcopy()`{.xref .py .py-meth .docutils
.literal .notranslate}]{.pre} instead ([`product2`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`=`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`product.deepcopy()`{.docutils .literal
.notranslate}]{.pre}).
:::

::: {#other-common-tasks .section}
###### Other common tasks[¶](#other-common-tasks "Permalink to this heading"){.headerlink}

Creating dicts from items:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> dict(product)  # create a dict from all populated values
    {'price': 1000, 'name': 'Desktop PC'}

    Creating items from dicts:

    >>> Product({"name": "Laptop PC", "price": 1500})
    Product(price=1500, name='Laptop PC')

    >>> Product({"name": "Laptop PC", "lala": 1500})  # warning: unknown field in dict
    Traceback (most recent call last):
        ...
    KeyError: 'Product does not support field: lala'
:::
:::
:::
:::

::: {#extending-item-subclasses .section}
##### Extending Item subclasses[¶](#extending-item-subclasses "Permalink to this heading"){.headerlink}

You can extend Items (to add more fields or to change some metadata for
some fields) by declaring a subclass of your original Item.

For example:

::: {.highlight-python .notranslate}
::: highlight
    class DiscountedProduct(Product):
        discount_percent = scrapy.Field(serializer=str)
        discount_expiration_date = scrapy.Field()
:::
:::

You can also extend field metadata by using the previous field metadata
and appending more values, or changing existing values, like this:

::: {.highlight-python .notranslate}
::: highlight
    class SpecificProduct(Product):
        name = scrapy.Field(Product.fields["name"], serializer=my_serializer)
:::
:::

That adds (or replaces) the [`serializer`{.docutils .literal
.notranslate}]{.pre} metadata key for the [`name`{.docutils .literal
.notranslate}]{.pre} field, keeping all the previously existing metadata
values.
:::
:::

::: {#supporting-all-item-types .section}
[]{#supporting-item-types}

#### Supporting All Item Types[¶](#supporting-all-item-types "Permalink to this heading"){.headerlink}

In code that receives an item, such as methods of [[item pipelines]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal} or [[spider middlewares]{.std
.std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
.reference .internal}, it is a good practice to use the
[[`ItemAdapter`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#itemadapter.ItemAdapter "itemadapter.ItemAdapter"){.reference
.internal} class and the [[`is_item()`{.xref .py .py-func .docutils
.literal
.notranslate}]{.pre}](#itemadapter.is_item "itemadapter.is_item"){.reference
.internal} function to write code that works for any [[supported item
type]{.std .std-ref}](#item-types){.hoverxref .tooltip .reference
.internal}:

*[class]{.pre}[ ]{.w}*[[itemadapter.]{.pre}]{.sig-prename .descclassname}[[ItemAdapter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemadapter/adapter.html#ItemAdapter){.reference .internal}[¶](#itemadapter.ItemAdapter "Permalink to this definition"){.headerlink}

:   Wrapper class to interact with data container objects. It provides a
    common interface to extract and set data without having to take the
    object's type into account.

```{=html}
<!-- -->
```

[[itemadapter.]{.pre}]{.sig-prename .descclassname}[[is_item]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[obj]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemadapter/utils.html#is_item){.reference .internal}[¶](#itemadapter.is_item "Permalink to this definition"){.headerlink}

:   Return True if the given object belongs to one of the supported
    types, False otherwise.

    Alias for ItemAdapter.is_item
:::

::: {#other-classes-related-to-items .section}
#### Other classes related to items[¶](#other-classes-related-to-items "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.item.]{.pre}]{.sig-prename .descclassname}[[ItemMeta]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[class_name]{.pre}]{.n}*, *[[bases]{.pre}]{.n}*, *[[attrs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/item.html#ItemMeta){.reference .internal}[¶](#scrapy.item.ItemMeta "Permalink to this definition"){.headerlink}

:   [Metaclass](https://realpython.com/python-metaclasses){.reference
    .external} of [`Item`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} that handles field definitions.
:::
:::

[]{#document-topics/loaders}

::: {#module-scrapy.loader .section}
[]{#item-loaders}[]{#topics-loaders}

### Item Loaders[¶](#module-scrapy.loader "Permalink to this heading"){.headerlink}

Item Loaders provide a convenient mechanism for populating scraped
[[items]{.std .std-ref}](index.html#topics-items){.hoverxref .tooltip
.reference .internal}. Even though items can be populated directly, Item
Loaders provide a much more convenient API for populating them from a
scraping process, by automating some common tasks like parsing the raw
extracted data before assigning it.

In other words, [[items]{.std
.std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
.internal} provide the *container* of scraped data, while Item Loaders
provide the mechanism for *populating* that container.

Item Loaders are designed to provide a flexible, efficient and easy
mechanism for extending and overriding different field parsing rules,
either by spider, or by source format (HTML, XML, etc) without becoming
a nightmare to maintain.

::: {.admonition .note}
Note

Item Loaders are an extension of the
[itemloaders](https://itemloaders.readthedocs.io/en/latest/){.reference
.external} library that make it easier to work with Scrapy by adding
support for [[responses]{.std
.std-ref}](index.html#topics-request-response){.hoverxref .tooltip
.reference .internal}.
:::

::: {#using-item-loaders-to-populate-items .section}
#### Using Item Loaders to populate items[¶](#using-item-loaders-to-populate-items "Permalink to this heading"){.headerlink}

To use an Item Loader, you must first instantiate it. You can either
instantiate it with an [[item object]{.std
.std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
.internal} or without one, in which case an [[item object]{.std
.std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
.internal} is automatically created in the Item Loader
[`__init__`{.docutils .literal .notranslate}]{.pre} method using the
[[item]{.std .std-ref}](index.html#topics-items){.hoverxref .tooltip
.reference .internal} class specified in the
[[`ItemLoader.default_item_class`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_item_class "scrapy.loader.ItemLoader.default_item_class"){.reference
.internal} attribute.

Then, you start collecting values into the Item Loader, typically using
[[Selectors]{.std .std-ref}](index.html#topics-selectors){.hoverxref
.tooltip .reference .internal}. You can add more than one value to the
same item field; the Item Loader will know how to "join" those values
later using a proper processing function.

::: {.admonition .note}
Note

Collected data is internally stored as lists, allowing to add several
values to the same field. If an [`item`{.docutils .literal
.notranslate}]{.pre} argument is passed when creating a loader, each of
the item's values will be stored as-is if it's already an iterable, or
wrapped with a list if it's a single value.
:::

Here is a typical Item Loader usage in a [[Spider]{.std
.std-ref}](index.html#topics-spiders){.hoverxref .tooltip .reference
.internal}, using the [[Product item]{.std
.std-ref}](index.html#topics-items-declaring){.hoverxref .tooltip
.reference .internal} declared in the [[Items chapter]{.std
.std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
.internal}:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.loader import ItemLoader
    from myproject.items import Product


    def parse(self, response):
        l = ItemLoader(item=Product(), response=response)
        l.add_xpath("name", '//div[@class="product_name"]')
        l.add_xpath("name", '//div[@class="product_title"]')
        l.add_xpath("price", '//p[@id="price"]')
        l.add_css("stock", "p#stock")
        l.add_value("last_updated", "today")  # you can also use literal values
        return l.load_item()
:::
:::

By quickly looking at that code, we can see the [`name`{.docutils
.literal .notranslate}]{.pre} field is being extracted from two
different XPath locations in the page:

1.  [`//div[@class="product_name"]`{.docutils .literal
    .notranslate}]{.pre}

2.  [`//div[@class="product_title"]`{.docutils .literal
    .notranslate}]{.pre}

In other words, data is being collected by extracting it from two XPath
locations, using the [[`add_xpath()`{.xref .py .py-meth .docutils
.literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
.internal} method. This is the data that will be assigned to the
[`name`{.docutils .literal .notranslate}]{.pre} field later.

Afterwards, similar calls are used for [`price`{.docutils .literal
.notranslate}]{.pre} and [`stock`{.docutils .literal
.notranslate}]{.pre} fields (the latter using a CSS selector with the
[[`add_css()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_css "scrapy.loader.ItemLoader.add_css"){.reference
.internal} method), and finally the [`last_update`{.docutils .literal
.notranslate}]{.pre} field is populated directly with a literal value
([`today`{.docutils .literal .notranslate}]{.pre}) using a different
method: [[`add_value()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
.internal}.

Finally, when all data is collected, the
[[`ItemLoader.load_item()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
.internal} method is called which actually returns the item populated
with the data previously extracted and collected with the
[[`add_xpath()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
.internal}, [[`add_css()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_css "scrapy.loader.ItemLoader.add_css"){.reference
.internal}, and [[`add_value()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
.internal} calls.
:::

::: {#working-with-dataclass-items .section}
[]{#topics-loaders-dataclass}

#### Working with dataclass items[¶](#working-with-dataclass-items "Permalink to this heading"){.headerlink}

By default, [[dataclass items]{.std
.std-ref}](index.html#dataclass-items){.hoverxref .tooltip .reference
.internal} require all fields to be passed when created. This could be
an issue when using dataclass items with item loaders: unless a
pre-populated item is passed to the loader, fields will be populated
incrementally using the loader's [[`add_xpath()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
.internal}, [[`add_css()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_css "scrapy.loader.ItemLoader.add_css"){.reference
.internal} and [[`add_value()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
.internal} methods.

One approach to overcome this is to define items using the
[[`field()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/dataclasses.html#dataclasses.field "(in Python v3.12)"){.reference
.external} function, with a [`default`{.docutils .literal
.notranslate}]{.pre} argument:

::: {.highlight-python .notranslate}
::: highlight
    from dataclasses import dataclass, field
    from typing import Optional


    @dataclass
    class InventoryItem:
        name: Optional[str] = field(default=None)
        price: Optional[float] = field(default=None)
        stock: Optional[int] = field(default=None)
:::
:::
:::

::: {#input-and-output-processors .section}
[]{#topics-loaders-processors}

#### Input and Output processors[¶](#input-and-output-processors "Permalink to this heading"){.headerlink}

An Item Loader contains one input processor and one output processor for
each (item) field. The input processor processes the extracted data as
soon as it's received (through the [[`add_xpath()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
.internal}, [[`add_css()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_css "scrapy.loader.ItemLoader.add_css"){.reference
.internal} or [[`add_value()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
.internal} methods) and the result of the input processor is collected
and kept inside the ItemLoader. After collecting all data, the
[[`ItemLoader.load_item()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
.internal} method is called to populate and get the populated [[item
object]{.std .std-ref}](index.html#topics-items){.hoverxref .tooltip
.reference .internal}. That's when the output processor is called with
the data previously collected (and processed using the input processor).
The result of the output processor is the final value that gets assigned
to the item.

Let's see an example to illustrate how the input and output processors
are called for a particular field (the same applies for any other
field):

::: {.highlight-python .notranslate}
::: highlight
    l = ItemLoader(Product(), some_selector)
    l.add_xpath("name", xpath1)  # (1)
    l.add_xpath("name", xpath2)  # (2)
    l.add_css("name", css)  # (3)
    l.add_value("name", "test")  # (4)
    return l.load_item()  # (5)
:::
:::

So what happens is:

1.  Data from [`xpath1`{.docutils .literal .notranslate}]{.pre} is
    extracted, and passed through the *input processor* of the
    [`name`{.docutils .literal .notranslate}]{.pre} field. The result of
    the input processor is collected and kept in the Item Loader (but
    not yet assigned to the item).

2.  Data from [`xpath2`{.docutils .literal .notranslate}]{.pre} is
    extracted, and passed through the same *input processor* used in
    (1). The result of the input processor is appended to the data
    collected in (1) (if any).

3.  This case is similar to the previous ones, except that the data is
    extracted from the [`css`{.docutils .literal .notranslate}]{.pre}
    CSS selector, and passed through the same *input processor* used
    in (1) and (2). The result of the input processor is appended to the
    data collected in (1) and (2) (if any).

4.  This case is also similar to the previous ones, except that the
    value to be collected is assigned directly, instead of being
    extracted from a XPath expression or a CSS selector. However, the
    value is still passed through the input processors. In this case,
    since the value is not iterable it is converted to an iterable of a
    single element before passing it to the input processor, because
    input processor always receive iterables.

5.  The data collected in steps (1), (2), (3) and (4) is passed through
    the *output processor* of the [`name`{.docutils .literal
    .notranslate}]{.pre} field. The result of the output processor is
    the value assigned to the [`name`{.docutils .literal
    .notranslate}]{.pre} field in the item.

It's worth noticing that processors are just callable objects, which are
called with the data to be parsed, and return a parsed value. So you can
use any function as input or output processor. The only requirement is
that they must accept one (and only one) positional argument, which will
be an iterable.

::: versionchanged
[Changed in version 2.0: ]{.versionmodified .changed}Processors no
longer need to be methods.
:::

::: {.admonition .note}
Note

Both input and output processors must receive an iterable as their first
argument. The output of those functions can be anything. The result of
input processors will be appended to an internal list (in the Loader)
containing the collected values (for that field). The result of the
output processors is the value that will be finally assigned to the
item.
:::

The other thing you need to keep in mind is that the values returned by
input processors are collected internally (in lists) and then passed to
output processors to populate the fields.

Last, but not least,
[itemloaders](https://itemloaders.readthedocs.io/en/latest/){.reference
.external} comes with some [[commonly used processors]{.xref .std
.std-ref}](https://itemloaders.readthedocs.io/en/latest/built-in-processors.html#built-in-processors "(in itemloaders)"){.reference
.external} built-in for convenience.
:::

::: {#declaring-item-loaders .section}
#### Declaring Item Loaders[¶](#declaring-item-loaders "Permalink to this heading"){.headerlink}

Item Loaders are declared using a class definition syntax. Here is an
example:

::: {.highlight-python .notranslate}
::: highlight
    from itemloaders.processors import TakeFirst, MapCompose, Join
    from scrapy.loader import ItemLoader


    class ProductLoader(ItemLoader):
        default_output_processor = TakeFirst()

        name_in = MapCompose(str.title)
        name_out = Join()

        price_in = MapCompose(str.strip)

        # ...
:::
:::

As you can see, input processors are declared using the [`_in`{.docutils
.literal .notranslate}]{.pre} suffix while output processors are
declared using the [`_out`{.docutils .literal .notranslate}]{.pre}
suffix. And you can also declare a default input/output processors using
the [[`ItemLoader.default_input_processor`{.xref .py .py-attr .docutils
.literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_input_processor "scrapy.loader.ItemLoader.default_input_processor"){.reference
.internal} and [[`ItemLoader.default_output_processor`{.xref .py
.py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_output_processor "scrapy.loader.ItemLoader.default_output_processor"){.reference
.internal} attributes.
:::

::: {#declaring-input-and-output-processors .section}
[]{#topics-loaders-processors-declaring}

#### Declaring Input and Output Processors[¶](#declaring-input-and-output-processors "Permalink to this heading"){.headerlink}

As seen in the previous section, input and output processors can be
declared in the Item Loader definition, and it's very common to declare
input processors this way. However, there is one more place where you
can specify the input and output processors to use: in the [[Item
Field]{.std .std-ref}](index.html#topics-items-fields){.hoverxref
.tooltip .reference .internal} metadata. Here is an example:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from itemloaders.processors import Join, MapCompose, TakeFirst
    from w3lib.html import remove_tags


    def filter_price(value):
        if value.isdigit():
            return value


    class Product(scrapy.Item):
        name = scrapy.Field(
            input_processor=MapCompose(remove_tags),
            output_processor=Join(),
        )
        price = scrapy.Field(
            input_processor=MapCompose(remove_tags, filter_price),
            output_processor=TakeFirst(),
        )
:::
:::

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy.loader import ItemLoader
    >>> il = ItemLoader(item=Product())
    >>> il.add_value("name", ["Welcome to my", "<strong>website</strong>"])
    >>> il.add_value("price", ["&euro;", "<span>1000</span>"])
    >>> il.load_item()
    {'name': 'Welcome to my website', 'price': '1000'}
:::
:::

The precedence order, for both input and output processors, is as
follows:

1.  Item Loader field-specific attributes: [`field_in`{.docutils
    .literal .notranslate}]{.pre} and [`field_out`{.docutils .literal
    .notranslate}]{.pre} (most precedence)

2.  Field metadata ([`input_processor`{.docutils .literal
    .notranslate}]{.pre} and [`output_processor`{.docutils .literal
    .notranslate}]{.pre} key)

3.  Item Loader defaults: [[`ItemLoader.default_input_processor()`{.xref
    .py .py-meth .docutils .literal
    .notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_input_processor "scrapy.loader.ItemLoader.default_input_processor"){.reference
    .internal} and [[`ItemLoader.default_output_processor()`{.xref .py
    .py-meth .docutils .literal
    .notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_output_processor "scrapy.loader.ItemLoader.default_output_processor"){.reference
    .internal} (least precedence)

See also: [[Reusing and extending Item Loaders]{.std
.std-ref}](#topics-loaders-extending){.hoverxref .tooltip .reference
.internal}.
:::

::: {#item-loader-context .section}
[]{#topics-loaders-context}

#### Item Loader Context[¶](#item-loader-context "Permalink to this heading"){.headerlink}

The Item Loader Context is a dict of arbitrary key/values which is
shared among all input and output processors in the Item Loader. It can
be passed when declaring, instantiating or using Item Loader. They are
used to modify the behaviour of the input/output processors.

For example, suppose you have a function [`parse_length`{.docutils
.literal .notranslate}]{.pre} which receives a text value and extracts a
length from it:

::: {.highlight-python .notranslate}
::: highlight
    def parse_length(text, loader_context):
        unit = loader_context.get("unit", "m")
        # ... length parsing code goes here ...
        return parsed_length
:::
:::

By accepting a [`loader_context`{.docutils .literal .notranslate}]{.pre}
argument the function is explicitly telling the Item Loader that it's
able to receive an Item Loader context, so the Item Loader passes the
currently active context when calling it, and the processor function
([`parse_length`{.docutils .literal .notranslate}]{.pre} in this case)
can thus use them.

There are several ways to modify Item Loader context values:

1.  By modifying the currently active Item Loader context
    ([[`context`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.loader.ItemLoader.context "scrapy.loader.ItemLoader.context"){.reference
    .internal} attribute):

    ::: {.highlight-python .notranslate}
    ::: highlight
        loader = ItemLoader(product)
        loader.context["unit"] = "cm"
    :::
    :::

2.  On Item Loader instantiation (the keyword arguments of Item Loader
    [`__init__`{.docutils .literal .notranslate}]{.pre} method are
    stored in the Item Loader context):

    ::: {.highlight-python .notranslate}
    ::: highlight
        loader = ItemLoader(product, unit="cm")
    :::
    :::

3.  On Item Loader declaration, for those input/output processors that
    support instantiating them with an Item Loader context.
    [`MapCompose`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} is one of them:

    ::: {.highlight-python .notranslate}
    ::: highlight
        class ProductLoader(ItemLoader):
            length_out = MapCompose(parse_length, unit="cm")
    :::
    :::
:::

::: {#itemloader-objects .section}
#### ItemLoader objects[¶](#itemloader-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.loader.]{.pre}]{.sig-prename .descclassname}[[ItemLoader]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[selector]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[response]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[parent]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[context]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/loader.html#ItemLoader){.reference .internal}[¶](#scrapy.loader.ItemLoader "Permalink to this definition"){.headerlink}

:   A user-friendly abstraction to populate an [[item]{.std
    .std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
    .internal} with data by applying [[field processors]{.std
    .std-ref}](#topics-loaders-processors){.hoverxref .tooltip
    .reference .internal} to scraped data. When instantiated with a
    [`selector`{.docutils .literal .notranslate}]{.pre} or a
    [`response`{.docutils .literal .notranslate}]{.pre} it supports data
    extraction from web pages using [[selectors]{.std
    .std-ref}](index.html#topics-selectors){.hoverxref .tooltip
    .reference .internal}.

    Parameters

    :   -   **item**
            ([*scrapy.item.Item*](index.html#scrapy.item.scrapy.item.Item "scrapy.item.scrapy.item.Item"){.reference
            .internal}) -- The item instance to populate using
            subsequent calls to [[`add_xpath()`{.xref .py .py-meth
            .docutils .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
            .internal}, [[`add_css()`{.xref .py .py-meth .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_css "scrapy.loader.ItemLoader.add_css"){.reference
            .internal}, or [[`add_value()`{.xref .py .py-meth .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
            .internal}.

        -   **selector** ([[`Selector`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
            .internal} object) -- The selector to extract data from,
            when using the [[`add_xpath()`{.xref .py .py-meth .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
            .internal}, [[`add_css()`{.xref .py .py-meth .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_css "scrapy.loader.ItemLoader.add_css"){.reference
            .internal}, [[`replace_xpath()`{.xref .py .py-meth .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.replace_xpath "scrapy.loader.ItemLoader.replace_xpath"){.reference
            .internal}, or [[`replace_css()`{.xref .py .py-meth
            .docutils .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.replace_css "scrapy.loader.ItemLoader.replace_css"){.reference
            .internal} method.

        -   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal} object) -- The response used to construct the
            selector using the [[`default_selector_class`{.xref .py
            .py-attr .docutils .literal
            .notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_selector_class "scrapy.loader.ItemLoader.default_selector_class"){.reference
            .internal}, unless the selector argument is given, in which
            case this argument is ignored.

    If no item is given, one is instantiated automatically using the
    class in [[`default_item_class`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_item_class "scrapy.loader.ItemLoader.default_item_class"){.reference
    .internal}.

    The item, selector, response and remaining keyword arguments are
    assigned to the Loader context (accessible through the
    [[`context`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.loader.ItemLoader.context "scrapy.loader.ItemLoader.context"){.reference
    .internal} attribute).

    [[item]{.pre}]{.sig-name .descname}[¶](#scrapy.loader.ItemLoader.item "Permalink to this definition"){.headerlink}

    :   The item object being parsed by this Item Loader. This is mostly
        used as a property so, when attempting to override this value,
        you may want to check out [[`default_item_class`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_item_class "scrapy.loader.ItemLoader.default_item_class"){.reference
        .internal} first.

    [[context]{.pre}]{.sig-name .descname}[¶](#scrapy.loader.ItemLoader.context "Permalink to this definition"){.headerlink}

    :   The currently active [[Context]{.xref .std
        .std-ref}](https://itemloaders.readthedocs.io/en/latest/loaders-context.html#loaders-context "(in itemloaders)"){.reference
        .external} of this Item Loader.

    [[default_item_class]{.pre}]{.sig-name .descname}[¶](#scrapy.loader.ItemLoader.default_item_class "Permalink to this definition"){.headerlink}

    :   An [[item]{.std .std-ref}](index.html#topics-items){.hoverxref
        .tooltip .reference .internal} class (or factory), used to
        instantiate items when not given in the [`__init__`{.docutils
        .literal .notranslate}]{.pre} method.

    [[default_input_processor]{.pre}]{.sig-name .descname}[¶](#scrapy.loader.ItemLoader.default_input_processor "Permalink to this definition"){.headerlink}

    :   The default input processor to use for those fields which don't
        specify one.

    [[default_output_processor]{.pre}]{.sig-name .descname}[¶](#scrapy.loader.ItemLoader.default_output_processor "Permalink to this definition"){.headerlink}

    :   The default output processor to use for those fields which don't
        specify one.

    [[default_selector_class]{.pre}]{.sig-name .descname}[¶](#scrapy.loader.ItemLoader.default_selector_class "Permalink to this definition"){.headerlink}

    :   The class used to construct the [[`selector`{.xref .py .py-attr
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.selector "scrapy.loader.ItemLoader.selector"){.reference
        .internal} of this [[`ItemLoader`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}, if only a response is given in the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method. If a
        selector is given in the [`__init__`{.docutils .literal
        .notranslate}]{.pre} method this attribute is ignored. This
        attribute is sometimes overridden in subclasses.

    [[selector]{.pre}]{.sig-name .descname}[¶](#scrapy.loader.ItemLoader.selector "Permalink to this definition"){.headerlink}

    :   The [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal} object to extract data from. It's either the selector
        given in the [`__init__`{.docutils .literal .notranslate}]{.pre}
        method or one created from the response given in the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method using
        the [[`default_selector_class`{.xref .py .py-attr .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.default_selector_class "scrapy.loader.ItemLoader.default_selector_class"){.reference
        .internal}. This attribute is meant to be read-only.

    [[add_css]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[css]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.add_css){.reference .internal}[¶](#scrapy.loader.ItemLoader.add_css "Permalink to this definition"){.headerlink}

    :   Similar to [[`ItemLoader.add_value()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
        .internal} but receives a CSS selector instead of a value, which
        is used to extract a list of unicode strings from the selector
        associated with this [[`ItemLoader`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}.

        See [[`get_css()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.get_css "scrapy.loader.ItemLoader.get_css"){.reference
        .internal} for [`kwargs`{.docutils .literal
        .notranslate}]{.pre}.

        Parameters

        :   **css**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the CSS selector to extract data from

        Examples:

        ::: {.highlight-default .notranslate}
        ::: highlight
            # HTML snippet: <p class="product-name">Color TV</p>
            loader.add_css('name', 'p.product-name')
            # HTML snippet: <p id="price">the price is $1200</p>
            loader.add_css('price', 'p#price', re='the price is (.*)')
        :::
        :::

    [[add_jmes]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[jmes]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.add_jmes){.reference .internal}[¶](#scrapy.loader.ItemLoader.add_jmes "Permalink to this definition"){.headerlink}

    :   Similar to [[`ItemLoader.add_value()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
        .internal} but receives a JMESPath selector instead of a value,
        which is used to extract a list of unicode strings from the
        selector associated with this [[`ItemLoader`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}.

        See [[`get_jmes()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.get_jmes "scrapy.loader.ItemLoader.get_jmes"){.reference
        .internal} for [`kwargs`{.docutils .literal
        .notranslate}]{.pre}.

        Parameters

        :   **jmes**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the JMESPath selector to extract data from

        Examples:

        ::: {.highlight-default .notranslate}
        ::: highlight
            # HTML snippet: {"name": "Color TV"}
            loader.add_jmes('name')
            # HTML snippet: {"price": the price is $1200"}
            loader.add_jmes('price', TakeFirst(), re='the price is (.*)')
        :::
        :::

    [[add_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[value]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.add_value){.reference .internal}[¶](#scrapy.loader.ItemLoader.add_value "Permalink to this definition"){.headerlink}

    :   Process and then add the given [`value`{.docutils .literal
        .notranslate}]{.pre} for the given field.

        The value is first passed through [[`get_value()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.get_value "scrapy.loader.ItemLoader.get_value"){.reference
        .internal} by giving the [`processors`{.docutils .literal
        .notranslate}]{.pre} and [`kwargs`{.docutils .literal
        .notranslate}]{.pre}, and then passed through the [[field input
        processor]{.xref .std
        .std-ref}](https://itemloaders.readthedocs.io/en/latest/processors.html#processors "(in itemloaders)"){.reference
        .external} and its result appended to the data collected for
        that field. If the field already contains collected data, the
        new data is added.

        The given [`field_name`{.docutils .literal .notranslate}]{.pre}
        can be [`None`{.docutils .literal .notranslate}]{.pre}, in which
        case values for multiple fields may be added. And the processed
        value should be a dict with field_name mapped to values.

        Examples:

        ::: {.highlight-default .notranslate}
        ::: highlight
            loader.add_value('name', 'Color TV')
            loader.add_value('colours', ['white', 'blue'])
            loader.add_value('length', '100')
            loader.add_value('name', 'name: foo', TakeFirst(), re='name: (.+)')
            loader.add_value(None, {'name': 'foo', 'sex': 'male'})
        :::
        :::

    [[add_xpath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[xpath]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.add_xpath){.reference .internal}[¶](#scrapy.loader.ItemLoader.add_xpath "Permalink to this definition"){.headerlink}

    :   Similar to [[`ItemLoader.add_value()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
        .internal} but receives an XPath instead of a value, which is
        used to extract a list of strings from the selector associated
        with this [[`ItemLoader`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}.

        See [[`get_xpath()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.get_xpath "scrapy.loader.ItemLoader.get_xpath"){.reference
        .internal} for [`kwargs`{.docutils .literal
        .notranslate}]{.pre}.

        Parameters

        :   **xpath**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the XPath to extract data from

        Examples:

        ::: {.highlight-default .notranslate}
        ::: highlight
            # HTML snippet: <p class="product-name">Color TV</p>
            loader.add_xpath('name', '//p[@class="product-name"]')
            # HTML snippet: <p id="price">the price is $1200</p>
            loader.add_xpath('price', '//p[@id="price"]', re='the price is (.*)')
        :::
        :::

    [[get_collected_values]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.get_collected_values){.reference .internal}[¶](#scrapy.loader.ItemLoader.get_collected_values "Permalink to this definition"){.headerlink}

    :   Return the collected values for the given field.

    [[get_css]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[css]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.get_css){.reference .internal}[¶](#scrapy.loader.ItemLoader.get_css "Permalink to this definition"){.headerlink}

    :   Similar to [[`ItemLoader.get_value()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.get_value "scrapy.loader.ItemLoader.get_value"){.reference
        .internal} but receives a CSS selector instead of a value, which
        is used to extract a list of unicode strings from the selector
        associated with this [[`ItemLoader`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}.

        Parameters

        :   -   **css**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the CSS selector to extract data from

            -   **re**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*Pattern*](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference
                .external}) -- a regular expression to use for
                extracting data from the selected CSS region

        Examples:

        ::: {.highlight-default .notranslate}
        ::: highlight
            # HTML snippet: <p class="product-name">Color TV</p>
            loader.get_css('p.product-name')
            # HTML snippet: <p id="price">the price is $1200</p>
            loader.get_css('p#price', TakeFirst(), re='the price is (.*)')
        :::
        :::

    [[get_jmes]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[jmes]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.get_jmes){.reference .internal}[¶](#scrapy.loader.ItemLoader.get_jmes "Permalink to this definition"){.headerlink}

    :   Similar to [[`ItemLoader.get_value()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.get_value "scrapy.loader.ItemLoader.get_value"){.reference
        .internal} but receives a JMESPath selector instead of a value,
        which is used to extract a list of unicode strings from the
        selector associated with this [[`ItemLoader`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}.

        Parameters

        :   -   **jmes**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the JMESPath selector to extract data
                from

            -   **re**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*Pattern*](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference
                .external}) -- a regular expression to use for
                extracting data from the selected JMESPath

        Examples:

        ::: {.highlight-default .notranslate}
        ::: highlight
            # HTML snippet: {"name": "Color TV"}
            loader.get_jmes('name')
            # HTML snippet: {"price": the price is $1200"}
            loader.get_jmes('price', TakeFirst(), re='the price is (.*)')
        :::
        :::

    [[get_output_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.get_output_value){.reference .internal}[¶](#scrapy.loader.ItemLoader.get_output_value "Permalink to this definition"){.headerlink}

    :   Return the collected values parsed using the output processor,
        for the given field. This method doesn't populate or modify the
        item at all.

    [[get_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[value]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.get_value){.reference .internal}[¶](#scrapy.loader.ItemLoader.get_value "Permalink to this definition"){.headerlink}

    :   Process the given [`value`{.docutils .literal
        .notranslate}]{.pre} by the given [`processors`{.docutils
        .literal .notranslate}]{.pre} and keyword arguments.

        Available keyword arguments:

        Parameters

        :   **re**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*Pattern*](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference
            .external}) -- a regular expression to use for extracting
            data from the given value using [`extract_regex()`{.xref .py
            .py-func .docutils .literal .notranslate}]{.pre} method,
            applied before processors

        Examples:

        ::: {.doctest .highlight-default .notranslate}
        ::: highlight
            >>> from itemloaders import ItemLoader
            >>> from itemloaders.processors import TakeFirst
            >>> loader = ItemLoader()
            >>> loader.get_value('name: foo', TakeFirst(), str.upper, re='name: (.+)')
            'FOO'
        :::
        :::

    [[get_xpath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[xpath]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.get_xpath){.reference .internal}[¶](#scrapy.loader.ItemLoader.get_xpath "Permalink to this definition"){.headerlink}

    :   Similar to [[`ItemLoader.get_value()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.get_value "scrapy.loader.ItemLoader.get_value"){.reference
        .internal} but receives an XPath instead of a value, which is
        used to extract a list of unicode strings from the selector
        associated with this [[`ItemLoader`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}.

        Parameters

        :   -   **xpath**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the XPath to extract data from

            -   **re**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*Pattern*](https://docs.python.org/3/library/typing.html#typing.Pattern "(in Python v3.12)"){.reference
                .external}) -- a regular expression to use for
                extracting data from the selected XPath region

        Examples:

        ::: {.highlight-default .notranslate}
        ::: highlight
            # HTML snippet: <p class="product-name">Color TV</p>
            loader.get_xpath('//p[@class="product-name"]')
            # HTML snippet: <p id="price">the price is $1200</p>
            loader.get_xpath('//p[@id="price"]', TakeFirst(), re='the price is (.*)')
        :::
        :::

    [[load_item]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.load_item){.reference .internal}[¶](#scrapy.loader.ItemLoader.load_item "Permalink to this definition"){.headerlink}

    :   Populate the item with the data collected so far, and return it.
        The data collected is first passed through the [[output
        processors]{.xref .std
        .std-ref}](https://itemloaders.readthedocs.io/en/latest/processors.html#processors "(in itemloaders)"){.reference
        .external} to get the final value to assign to each item field.

    [[nested_css]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[css]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[context]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.nested_css){.reference .internal}[¶](#scrapy.loader.ItemLoader.nested_css "Permalink to this definition"){.headerlink}

    :   Create a nested loader with a css selector. The supplied
        selector is applied relative to selector associated with this
        [[`ItemLoader`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}. The nested loader shares the item with the parent
        [[`ItemLoader`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal} so calls to [[`add_xpath()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
        .internal}, [[`add_value()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
        .internal}, [[`replace_value()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.replace_value "scrapy.loader.ItemLoader.replace_value"){.reference
        .internal}, etc. will behave as expected.

    [[nested_xpath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[xpath]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[context]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.nested_xpath){.reference .internal}[¶](#scrapy.loader.ItemLoader.nested_xpath "Permalink to this definition"){.headerlink}

    :   Create a nested loader with an xpath selector. The supplied
        selector is applied relative to selector associated with this
        [[`ItemLoader`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal}. The nested loader shares the item with the parent
        [[`ItemLoader`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
        .internal} so calls to [[`add_xpath()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
        .internal}, [[`add_value()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
        .internal}, [[`replace_value()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.replace_value "scrapy.loader.ItemLoader.replace_value"){.reference
        .internal}, etc. will behave as expected.

    [[replace_css]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[css]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.replace_css){.reference .internal}[¶](#scrapy.loader.ItemLoader.replace_css "Permalink to this definition"){.headerlink}

    :   Similar to [[`add_css()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_css "scrapy.loader.ItemLoader.add_css"){.reference
        .internal} but replaces collected data instead of adding it.

    [[replace_jmes]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[jmes]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.replace_jmes){.reference .internal}[¶](#scrapy.loader.ItemLoader.replace_jmes "Permalink to this definition"){.headerlink}

    :   Similar to [[`add_jmes()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_jmes "scrapy.loader.ItemLoader.add_jmes"){.reference
        .internal} but replaces collected data instead of adding it.

    [[replace_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[value]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.replace_value){.reference .internal}[¶](#scrapy.loader.ItemLoader.replace_value "Permalink to this definition"){.headerlink}

    :   Similar to [[`add_value()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_value "scrapy.loader.ItemLoader.add_value"){.reference
        .internal} but replaces the collected data with the new value
        instead of adding it.

    [[replace_xpath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field_name]{.pre}]{.n}*, *[[xpath]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[processors]{.pre}]{.n}*, *[[re]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kw]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/itemloaders.html#ItemLoader.replace_xpath){.reference .internal}[¶](#scrapy.loader.ItemLoader.replace_xpath "Permalink to this definition"){.headerlink}

    :   Similar to [[`add_xpath()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.loader.ItemLoader.add_xpath "scrapy.loader.ItemLoader.add_xpath"){.reference
        .internal} but replaces collected data instead of adding it.
:::

::: {#nested-loaders .section}
[]{#topics-loaders-nested}

#### Nested Loaders[¶](#nested-loaders "Permalink to this heading"){.headerlink}

When parsing related values from a subsection of a document, it can be
useful to create nested loaders. Imagine you're extracting details from
a footer of a page that looks something like:

Example:

::: {.highlight-default .notranslate}
::: highlight
    <footer>
        <a class="social" href="https://facebook.com/whatever">Like Us</a>
        <a class="social" href="https://twitter.com/whatever">Follow Us</a>
        <a class="email" href="mailto:whatever@example.com">Email Us</a>
    </footer>
:::
:::

Without nested loaders, you need to specify the full xpath (or css) for
each value that you wish to extract.

Example:

::: {.highlight-python .notranslate}
::: highlight
    loader = ItemLoader(item=Item())
    # load stuff not in the footer
    loader.add_xpath("social", '//footer/a[@class = "social"]/@href')
    loader.add_xpath("email", '//footer/a[@class = "email"]/@href')
    loader.load_item()
:::
:::

Instead, you can create a nested loader with the footer selector and add
values relative to the footer. The functionality is the same but you
avoid repeating the footer selector.

Example:

::: {.highlight-python .notranslate}
::: highlight
    loader = ItemLoader(item=Item())
    # load stuff not in the footer
    footer_loader = loader.nested_xpath("//footer")
    footer_loader.add_xpath("social", 'a[@class = "social"]/@href')
    footer_loader.add_xpath("email", 'a[@class = "email"]/@href')
    # no need to call footer_loader.load_item()
    loader.load_item()
:::
:::

You can nest loaders arbitrarily and they work with either xpath or css
selectors. As a general guideline, use nested loaders when they make
your code simpler but do not go overboard with nesting or your parser
can become difficult to read.
:::

::: {#reusing-and-extending-item-loaders .section}
[]{#topics-loaders-extending}

#### Reusing and extending Item Loaders[¶](#reusing-and-extending-item-loaders "Permalink to this heading"){.headerlink}

As your project grows bigger and acquires more and more spiders,
maintenance becomes a fundamental problem, especially when you have to
deal with many different parsing rules for each spider, having a lot of
exceptions, but also wanting to reuse the common processors.

Item Loaders are designed to ease the maintenance burden of parsing
rules, without losing flexibility and, at the same time, providing a
convenient mechanism for extending and overriding them. For this reason
Item Loaders support traditional Python class inheritance for dealing
with differences of specific spiders (or groups of spiders).

Suppose, for example, that some particular site encloses their product
names in three dashes (e.g. [`---Plasma`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`TV---`{.docutils .literal .notranslate}]{.pre}) and you
don't want to end up scraping those dashes in the final product names.

Here's how you can remove those dashes by reusing and extending the
default Product Item Loader ([`ProductLoader`{.docutils .literal
.notranslate}]{.pre}):

::: {.highlight-python .notranslate}
::: highlight
    from itemloaders.processors import MapCompose
    from myproject.ItemLoaders import ProductLoader


    def strip_dashes(x):
        return x.strip("-")


    class SiteSpecificLoader(ProductLoader):
        name_in = MapCompose(strip_dashes, ProductLoader.name_in)
:::
:::

Another case where extending Item Loaders can be very helpful is when
you have multiple source formats, for example XML and HTML. In the XML
version you may want to remove [`CDATA`{.docutils .literal
.notranslate}]{.pre} occurrences. Here's an example of how to do it:

::: {.highlight-python .notranslate}
::: highlight
    from itemloaders.processors import MapCompose
    from myproject.ItemLoaders import ProductLoader
    from myproject.utils.xml import remove_cdata


    class XmlProductLoader(ProductLoader):
        name_in = MapCompose(remove_cdata, ProductLoader.name_in)
:::
:::

And that's how you typically extend input processors.

As for output processors, it is more common to declare them in the field
metadata, as they usually depend only on the field and not on each
specific site parsing rule (as input processors do). See also:
[[Declaring Input and Output Processors]{.std
.std-ref}](#topics-loaders-processors-declaring){.hoverxref .tooltip
.reference .internal}.

There are many other possible ways to extend, inherit and override your
Item Loaders, and different Item Loaders hierarchies may fit better for
different projects. Scrapy only provides the mechanism; it doesn't
impose any specific organization of your Loaders collection - that's up
to you and your project's needs.
:::
:::

[]{#document-topics/shell}

::: {#scrapy-shell .section}
[]{#topics-shell}

### Scrapy shell[¶](#scrapy-shell "Permalink to this heading"){.headerlink}

The Scrapy shell is an interactive shell where you can try and debug
your scraping code very quickly, without having to run the spider. It's
meant to be used for testing data extraction code, but you can actually
use it for testing any kind of code as it is also a regular Python
shell.

The shell is used for testing XPath or CSS expressions and see how they
work and what data they extract from the web pages you're trying to
scrape. It allows you to interactively test your expressions while
you're writing your spider, without having to run the spider to test
every change.

Once you get familiarized with the Scrapy shell, you'll see that it's an
invaluable tool for developing and debugging your spiders.

::: {#configuring-the-shell .section}
#### Configuring the shell[¶](#configuring-the-shell "Permalink to this heading"){.headerlink}

If you have [IPython](https://ipython.org/){.reference .external}
installed, the Scrapy shell will use it (instead of the standard Python
console). The [IPython](https://ipython.org/){.reference .external}
console is much more powerful and provides smart auto-completion and
colorized output, among other things.

We highly recommend you install
[IPython](https://ipython.org/){.reference .external}, specially if
you're working on Unix systems (where
[IPython](https://ipython.org/){.reference .external} excels). See the
[IPython installation
guide](https://ipython.org/install.html){.reference .external} for more
info.

Scrapy also has support for
[bpython](https://bpython-interpreter.org/){.reference .external}, and
will try to use it where [IPython](https://ipython.org/){.reference
.external} is unavailable.

Through Scrapy's settings you can configure it to use any one of
[`ipython`{.docutils .literal .notranslate}]{.pre}, [`bpython`{.docutils
.literal .notranslate}]{.pre} or the standard [`python`{.docutils
.literal .notranslate}]{.pre} shell, regardless of which are installed.
This is done by setting the [`SCRAPY_PYTHON_SHELL`{.docutils .literal
.notranslate}]{.pre} environment variable; or by defining it in your
[[scrapy.cfg]{.std
.std-ref}](index.html#topics-config-settings){.hoverxref .tooltip
.reference .internal}:

::: {.highlight-default .notranslate}
::: highlight
    [settings]
    shell = bpython
:::
:::
:::

::: {#launch-the-shell .section}
#### Launch the shell[¶](#launch-the-shell "Permalink to this heading"){.headerlink}

To launch the Scrapy shell you can use the [[`shell`{.xref .std
.std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-shell){.hoverxref .tooltip
.reference .internal} command like this:

::: {.highlight-default .notranslate}
::: highlight
    scrapy shell <url>
:::
:::

Where the [`<url>`{.docutils .literal .notranslate}]{.pre} is the URL
you want to scrape.

[[`shell`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-shell){.hoverxref .tooltip
.reference .internal} also works for local files. This can be handy if
you want to play around with a local copy of a web page. [[`shell`{.xref
.std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-shell){.hoverxref .tooltip
.reference .internal} understands the following syntaxes for local
files:

::: {.highlight-default .notranslate}
::: highlight
    # UNIX-style
    scrapy shell ./path/to/file.html
    scrapy shell ../other/path/to/file.html
    scrapy shell /absolute/path/to/file.html

    # File URI
    scrapy shell file:///absolute/path/to/file.html
:::
:::

::: {.admonition .note}
Note

When using relative file paths, be explicit and prepend them with
[`./`{.docutils .literal .notranslate}]{.pre} (or [`../`{.docutils
.literal .notranslate}]{.pre} when relevant). [`scrapy`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`shell`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`index.html`{.docutils .literal .notranslate}]{.pre} will
not work as one might expect (and this is by design, not a bug).

Because [[`shell`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-shell){.hoverxref .tooltip
.reference .internal} favors HTTP URLs over File URIs, and
[`index.html`{.docutils .literal .notranslate}]{.pre} being
syntactically similar to [`example.com`{.docutils .literal
.notranslate}]{.pre}, [[`shell`{.xref .std .std-command .docutils
.literal .notranslate}]{.pre}](index.html#std-command-shell){.hoverxref
.tooltip .reference .internal} will treat [`index.html`{.docutils
.literal .notranslate}]{.pre} as a domain name and trigger a DNS lookup
error:

::: {.highlight-default .notranslate}
::: highlight
    $ scrapy shell index.html
    [ ... scrapy shell starts ... ]
    [ ... traceback ... ]
    twisted.internet.error.DNSLookupError: DNS lookup failed:
    address 'index.html' not found: [Errno -5] No address associated with hostname.
:::
:::

[[`shell`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-shell){.hoverxref .tooltip
.reference .internal} will not test beforehand if a file called
[`index.html`{.docutils .literal .notranslate}]{.pre} exists in the
current directory. Again, be explicit.
:::
:::

::: {#using-the-shell .section}
#### Using the shell[¶](#using-the-shell "Permalink to this heading"){.headerlink}

The Scrapy shell is just a regular Python console (or
[IPython](https://ipython.org/){.reference .external} console if you
have it available) which provides some additional shortcut functions for
convenience.

::: {#available-shortcuts .section}
##### Available Shortcuts[¶](#available-shortcuts "Permalink to this heading"){.headerlink}

-   [`shelp()`{.docutils .literal .notranslate}]{.pre} - print a help
    with the list of available objects and shortcuts

-   [`fetch(url[,`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`redirect=True])`{.docutils .literal
    .notranslate}]{.pre} - fetch a new response from the given URL and
    update all related objects accordingly. You can optionally ask for
    HTTP 3xx redirections to not be followed by passing
    [`redirect=False`{.docutils .literal .notranslate}]{.pre}

-   [`fetch(request)`{.docutils .literal .notranslate}]{.pre} - fetch a
    new response from the given request and update all related objects
    accordingly.

-   [`view(response)`{.docutils .literal .notranslate}]{.pre} - open the
    given response in your local web browser, for inspection. This will
    add a [\<base\>
    tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base){.reference
    .external} to the response body in order for external links (such as
    images and style sheets) to display properly. Note, however, that
    this will create a temporary file in your computer, which won't be
    removed automatically.
:::

::: {#available-scrapy-objects .section}
##### Available Scrapy objects[¶](#available-scrapy-objects "Permalink to this heading"){.headerlink}

The Scrapy shell automatically creates some convenient objects from the
downloaded page, like the [[`Response`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} object and the [`Selector`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre} objects (for both HTML and XML content).

Those objects are:

-   [`crawler`{.docutils .literal .notranslate}]{.pre} - the current
    [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal} object.

-   [`spider`{.docutils .literal .notranslate}]{.pre} - the Spider which
    is known to handle the URL, or a [[`Spider`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
    .internal} object if there is no spider found for the current URL

-   [`request`{.docutils .literal .notranslate}]{.pre} - a
    [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} object of the last fetched page. You can modify
    this request using [`replace()`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre} or fetch a new request (without
    leaving the shell) using the [`fetch`{.docutils .literal
    .notranslate}]{.pre} shortcut.

-   [`response`{.docutils .literal .notranslate}]{.pre} - a
    [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} object containing the last fetched page

-   [`settings`{.docutils .literal .notranslate}]{.pre} - the current
    [[Scrapy settings]{.std
    .std-ref}](index.html#topics-settings){.hoverxref .tooltip
    .reference .internal}
:::
:::

::: {#example-of-shell-session .section}
#### Example of shell session[¶](#example-of-shell-session "Permalink to this heading"){.headerlink}

Here's an example of a typical shell session where we start by scraping
the [https://scrapy.org](https://scrapy.org){.reference .external} page,
and then proceed to scrape the
[https://old.reddit.com/](https://old.reddit.com/){.reference .external}
page. Finally, we modify the (Reddit) request method to POST and
re-fetch it getting an error. We end the session by typing Ctrl-D (in
Unix systems) or Ctrl-Z in Windows.

Keep in mind that the data extracted here may not be the same when you
try it, as those pages are not static and could have changed by the time
you test this. The only purpose of this example is to get you
familiarized with how the Scrapy shell works.

First, we launch the shell:

::: {.highlight-default .notranslate}
::: highlight
    scrapy shell 'https://scrapy.org' --nolog
:::
:::

::: {.admonition .note}
Note

Remember to always enclose URLs in quotes when running the Scrapy shell
from the command line, otherwise URLs containing arguments (i.e. the
[`&`{.docutils .literal .notranslate}]{.pre} character) will not work.

On Windows, use double quotes instead:

::: {.highlight-default .notranslate}
::: highlight
    scrapy shell "https://scrapy.org" --nolog
:::
:::
:::

Then, the shell fetches the URL (using the Scrapy downloader) and prints
the list of available objects and useful shortcuts (you'll notice that
these lines all start with the [`[s]`{.docutils .literal
.notranslate}]{.pre} prefix):

::: {.highlight-default .notranslate}
::: highlight
    [s] Available Scrapy objects:
    [s]   scrapy     scrapy module (contains scrapy.Request, scrapy.Selector, etc)
    [s]   crawler    <scrapy.crawler.Crawler object at 0x7f07395dd690>
    [s]   item       {}
    [s]   request    <GET https://scrapy.org>
    [s]   response   <200 https://scrapy.org/>
    [s]   settings   <scrapy.settings.Settings object at 0x7f07395dd710>
    [s]   spider     <DefaultSpider 'default' at 0x7f0735891690>
    [s] Useful shortcuts:
    [s]   fetch(url[, redirect=True]) Fetch URL and update local objects (by default, redirects are followed)
    [s]   fetch(req)                  Fetch a scrapy.Request and update local objects
    [s]   shelp()           Shell help (print this help)
    [s]   view(response)    View response in a browser

    >>>
:::
:::

After that, we can start playing with the objects:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//title/text()").get()
    'Scrapy | A Fast and Powerful Scraping and Web Crawling Framework'

    >>> fetch("https://old.reddit.com/")

    >>> response.xpath("//title/text()").get()
    'reddit: the front page of the internet'

    >>> request = request.replace(method="POST")

    >>> fetch(request)

    >>> response.status
    404

    >>> from pprint import pprint

    >>> pprint(response.headers)
    {'Accept-Ranges': ['bytes'],
    'Cache-Control': ['max-age=0, must-revalidate'],
    'Content-Type': ['text/html; charset=UTF-8'],
    'Date': ['Thu, 08 Dec 2016 16:21:19 GMT'],
    'Server': ['snooserv'],
    'Set-Cookie': ['loid=KqNLou0V9SKMX4qb4n; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure',
                    'loidcreated=2016-12-08T16%3A21%3A19.445Z; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure',
                    'loid=vi0ZVe4NkxNWdlH7r7; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure',
                    'loidcreated=2016-12-08T16%3A21%3A19.459Z; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure'],
    'Vary': ['accept-encoding'],
    'Via': ['1.1 varnish'],
    'X-Cache': ['MISS'],
    'X-Cache-Hits': ['0'],
    'X-Content-Type-Options': ['nosniff'],
    'X-Frame-Options': ['SAMEORIGIN'],
    'X-Moose': ['majestic'],
    'X-Served-By': ['cache-cdg8730-CDG'],
    'X-Timer': ['S1481214079.394283,VS0,VE159'],
    'X-Ua-Compatible': ['IE=edge'],
    'X-Xss-Protection': ['1; mode=block']}
:::
:::
:::

::: {#invoking-the-shell-from-spiders-to-inspect-responses .section}
[]{#topics-shell-inspect-response}

#### Invoking the shell from spiders to inspect responses[¶](#invoking-the-shell-from-spiders-to-inspect-responses "Permalink to this heading"){.headerlink}

Sometimes you want to inspect the responses that are being processed in
a certain point of your spider, if only to check that response you
expect is getting there.

This can be achieved by using the
[`scrapy.shell.inspect_response`{.docutils .literal .notranslate}]{.pre}
function.

Here's an example of how you would call it from your spider:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "myspider"
        start_urls = [
            "http://example.com",
            "http://example.org",
            "http://example.net",
        ]

        def parse(self, response):
            # We want to inspect one specific response.
            if ".org" in response.url:
                from scrapy.shell import inspect_response

                inspect_response(response, self)

            # Rest of parsing code.
:::
:::

When you run the spider, you will get something similar to this:

::: {.highlight-default .notranslate}
::: highlight
    2014-01-23 17:48:31-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.com> (referer: None)
    2014-01-23 17:48:31-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.org> (referer: None)
    [s] Available Scrapy objects:
    [s]   crawler    <scrapy.crawler.Crawler object at 0x1e16b50>
    ...

    >>> response.url
    'http://example.org'
:::
:::

Then, you can check if the extraction code is working:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//h1[@class="fn"]')
    []
:::
:::

Nope, it doesn't. So you can open the response in your web browser and
see if it's the response you were expecting:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> view(response)
    True
:::
:::

Finally you hit Ctrl-D (or Ctrl-Z in Windows) to exit the shell and
resume the crawling:

::: {.highlight-default .notranslate}
::: highlight
    >>> ^D
    2014-01-23 17:50:03-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.net> (referer: None)
    ...
:::
:::

Note that you can't use the [`fetch`{.docutils .literal
.notranslate}]{.pre} shortcut here since the Scrapy engine is blocked by
the shell. However, after you leave the shell, the spider will continue
crawling where it stopped, as shown above.
:::
:::

[]{#document-topics/item-pipeline}

::: {#item-pipeline .section}
[]{#topics-item-pipeline}

### Item Pipeline[¶](#item-pipeline "Permalink to this heading"){.headerlink}

After an item has been scraped by a spider, it is sent to the Item
Pipeline which processes it through several components that are executed
sequentially.

Each item pipeline component (sometimes referred as just "Item
Pipeline") is a Python class that implements a simple method. They
receive an item and perform an action over it, also deciding if the item
should continue through the pipeline or be dropped and no longer
processed.

Typical uses of item pipelines are:

-   cleansing HTML data

-   validating scraped data (checking that the items contain certain
    fields)

-   checking for duplicates (and dropping them)

-   storing the scraped item in a database

::: {#writing-your-own-item-pipeline .section}
#### Writing your own item pipeline[¶](#writing-your-own-item-pipeline "Permalink to this heading"){.headerlink}

Each item pipeline component is a Python class that must implement the
following method:

[[process_item]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[item]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#process_item "Permalink to this definition"){.headerlink}

:   This method is called for every item pipeline component.

    item is an [[item object]{.std
    .std-ref}](index.html#item-types){.hoverxref .tooltip .reference
    .internal}, see [[Supporting All Item Types]{.std
    .std-ref}](index.html#supporting-item-types){.hoverxref .tooltip
    .reference .internal}.

    [[`process_item()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](#process_item "process_item"){.reference
    .internal} must either: return an [[item object]{.std
    .std-ref}](index.html#item-types){.hoverxref .tooltip .reference
    .internal}, return a [[`Deferred`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
    .external} or raise a [[`DropItem`{.xref .py .py-exc .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.DropItem "scrapy.exceptions.DropItem"){.reference
    .internal} exception.

    Dropped items are no longer processed by further pipeline
    components.

    Parameters

    :   -   **item** ([[item object]{.std
            .std-ref}](index.html#item-types){.hoverxref .tooltip
            .reference .internal}) -- the scraped item

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which scraped the item

Additionally, they may also implement the following methods:

[[open_spider]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#open_spider "Permalink to this definition"){.headerlink}

:   This method is called when the spider is opened.

    Parameters

    :   **spider** ([[`Spider`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
        .internal} object) -- the spider which was opened

```{=html}
<!-- -->
```

[[close_spider]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#close_spider "Permalink to this definition"){.headerlink}

:   This method is called when the spider is closed.

    Parameters

    :   **spider** ([[`Spider`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
        .internal} object) -- the spider which was closed

```{=html}
<!-- -->
```

*[classmethod]{.pre}[ ]{.w}*[[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[cls]{.pre}]{.n}*, *[[crawler]{.pre}]{.n}*[)]{.sig-paren}[¶](#from_crawler "Permalink to this definition"){.headerlink}

:   If present, this class method is called to create a pipeline
    instance from a [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal}. It must return a new instance of the pipeline. Crawler
    object provides access to all Scrapy core components like settings
    and signals; it is a way for pipeline to access them and hook its
    functionality into Scrapy.

    Parameters

    :   **crawler** ([[`Crawler`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} object) -- crawler that uses this pipeline
:::

::: {#item-pipeline-example .section}
#### Item pipeline example[¶](#item-pipeline-example "Permalink to this heading"){.headerlink}

::: {#price-validation-and-dropping-items-with-no-prices .section}
##### Price validation and dropping items with no prices[¶](#price-validation-and-dropping-items-with-no-prices "Permalink to this heading"){.headerlink}

Let's take a look at the following hypothetical pipeline that adjusts
the [`price`{.docutils .literal .notranslate}]{.pre} attribute for those
items that do not include VAT ([`price_excludes_vat`{.docutils .literal
.notranslate}]{.pre} attribute), and drops those items which don't
contain a price:

::: {.highlight-python .notranslate}
::: highlight
    from itemadapter import ItemAdapter
    from scrapy.exceptions import DropItem


    class PricePipeline:
        vat_factor = 1.15

        def process_item(self, item, spider):
            adapter = ItemAdapter(item)
            if adapter.get("price"):
                if adapter.get("price_excludes_vat"):
                    adapter["price"] = adapter["price"] * self.vat_factor
                return item
            else:
                raise DropItem(f"Missing price in {item}")
:::
:::
:::

::: {#write-items-to-a-json-lines-file .section}
##### Write items to a JSON lines file[¶](#write-items-to-a-json-lines-file "Permalink to this heading"){.headerlink}

The following pipeline stores all scraped items (from all spiders) into
a single [`items.jsonl`{.docutils .literal .notranslate}]{.pre} file,
containing one item per line serialized in JSON format:

::: {.highlight-python .notranslate}
::: highlight
    import json

    from itemadapter import ItemAdapter


    class JsonWriterPipeline:
        def open_spider(self, spider):
            self.file = open("items.jsonl", "w")

        def close_spider(self, spider):
            self.file.close()

        def process_item(self, item, spider):
            line = json.dumps(ItemAdapter(item).asdict()) + "\n"
            self.file.write(line)
            return item
:::
:::

::: {.admonition .note}
Note

The purpose of JsonWriterPipeline is just to introduce how to write item
pipelines. If you really want to store all scraped items into a JSON
file you should use the [[Feed exports]{.std
.std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
.reference .internal}.
:::
:::

::: {#write-items-to-mongodb .section}
##### Write items to MongoDB[¶](#write-items-to-mongodb "Permalink to this heading"){.headerlink}

In this example we'll write items to
[MongoDB](https://www.mongodb.com/){.reference .external} using
[pymongo](https://api.mongodb.com/python/current/){.reference
.external}. MongoDB address and database name are specified in Scrapy
settings; MongoDB collection is named after item class.

The main point of this example is to show how to use
[[`from_crawler()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#from_crawler "from_crawler"){.reference
.internal} method and how to clean up the resources properly.

::: {.highlight-python .notranslate}
::: highlight
    import pymongo
    from itemadapter import ItemAdapter


    class MongoPipeline:
        collection_name = "scrapy_items"

        def __init__(self, mongo_uri, mongo_db):
            self.mongo_uri = mongo_uri
            self.mongo_db = mongo_db

        @classmethod
        def from_crawler(cls, crawler):
            return cls(
                mongo_uri=crawler.settings.get("MONGO_URI"),
                mongo_db=crawler.settings.get("MONGO_DATABASE", "items"),
            )

        def open_spider(self, spider):
            self.client = pymongo.MongoClient(self.mongo_uri)
            self.db = self.client[self.mongo_db]

        def close_spider(self, spider):
            self.client.close()

        def process_item(self, item, spider):
            self.db[self.collection_name].insert_one(ItemAdapter(item).asdict())
            return item
:::
:::
:::

::: {#take-screenshot-of-item .section}
[]{#screenshotpipeline}

##### Take screenshot of item[¶](#take-screenshot-of-item "Permalink to this heading"){.headerlink}

This example demonstrates how to use [[coroutine
syntax]{.doc}](index.html#document-topics/coroutines){.reference
.internal} in the [[`process_item()`{.xref .py .py-meth .docutils
.literal .notranslate}]{.pre}](#process_item "process_item"){.reference
.internal} method.

This item pipeline makes a request to a locally-running instance of
[Splash](https://splash.readthedocs.io/en/stable/){.reference .external}
to render a screenshot of the item URL. After the request response is
downloaded, the item pipeline saves the screenshot to a file and adds
the filename to the item.

::: {.highlight-python .notranslate}
::: highlight
    import hashlib
    from pathlib import Path
    from urllib.parse import quote

    import scrapy
    from itemadapter import ItemAdapter
    from scrapy.http.request import NO_CALLBACK
    from scrapy.utils.defer import maybe_deferred_to_future


    class ScreenshotPipeline:
        """Pipeline that uses Splash to render screenshot of
        every Scrapy item."""

        SPLASH_URL = "http://localhost:8050/render.png?url={}"

        async def process_item(self, item, spider):
            adapter = ItemAdapter(item)
            encoded_item_url = quote(adapter["url"])
            screenshot_url = self.SPLASH_URL.format(encoded_item_url)
            request = scrapy.Request(screenshot_url, callback=NO_CALLBACK)
            response = await maybe_deferred_to_future(
                spider.crawler.engine.download(request)
            )

            if response.status != 200:
                # Error happened, return item.
                return item

            # Save screenshot to file, filename will be hash of url.
            url = adapter["url"]
            url_hash = hashlib.md5(url.encode("utf8")).hexdigest()
            filename = f"{url_hash}.png"
            Path(filename).write_bytes(response.body)

            # Store filename in item.
            adapter["screenshot_filename"] = filename
            return item
:::
:::
:::

::: {#duplicates-filter .section}
##### Duplicates filter[¶](#duplicates-filter "Permalink to this heading"){.headerlink}

A filter that looks for duplicate items, and drops those items that were
already processed. Let's say that our items have a unique id, but our
spider returns multiples items with the same id:

::: {.highlight-python .notranslate}
::: highlight
    from itemadapter import ItemAdapter
    from scrapy.exceptions import DropItem


    class DuplicatesPipeline:
        def __init__(self):
            self.ids_seen = set()

        def process_item(self, item, spider):
            adapter = ItemAdapter(item)
            if adapter["id"] in self.ids_seen:
                raise DropItem(f"Duplicate item found: {item!r}")
            else:
                self.ids_seen.add(adapter["id"])
                return item
:::
:::
:::
:::

::: {#activating-an-item-pipeline-component .section}
#### Activating an Item Pipeline component[¶](#activating-an-item-pipeline-component "Permalink to this heading"){.headerlink}

To activate an Item Pipeline component you must add its class to the
[[`ITEM_PIPELINES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
.tooltip .reference .internal} setting, like in the following example:

::: {.highlight-python .notranslate}
::: highlight
    ITEM_PIPELINES = {
        "myproject.pipelines.PricePipeline": 300,
        "myproject.pipelines.JsonWriterPipeline": 800,
    }
:::
:::

The integer values you assign to classes in this setting determine the
order in which they run: items go through from lower valued to higher
valued classes. It's customary to define these numbers in the 0-1000
range.
:::
:::

[]{#document-topics/feed-exports}

::: {#feed-exports .section}
[]{#topics-feed-exports}

### Feed exports[¶](#feed-exports "Permalink to this heading"){.headerlink}

One of the most frequently required features when implementing scrapers
is being able to store the scraped data properly and, quite often, that
means generating an "export file" with the scraped data (commonly called
"export feed") to be consumed by other systems.

Scrapy provides this functionality out of the box with the Feed Exports,
which allows you to generate feeds with the scraped items, using
multiple serialization formats and storage backends.

::: {#serialization-formats .section}
[]{#topics-feed-format}

#### Serialization formats[¶](#serialization-formats "Permalink to this heading"){.headerlink}

For serializing the scraped data, the feed exports use the [[Item
exporters]{.std .std-ref}](index.html#topics-exporters){.hoverxref
.tooltip .reference .internal}. These formats are supported out of the
box:

-   [[JSON]{.std .std-ref}](#topics-feed-format-json){.hoverxref
    .tooltip .reference .internal}

-   [[JSON lines]{.std
    .std-ref}](#topics-feed-format-jsonlines){.hoverxref .tooltip
    .reference .internal}

-   [[CSV]{.std .std-ref}](#topics-feed-format-csv){.hoverxref .tooltip
    .reference .internal}

-   [[XML]{.std .std-ref}](#topics-feed-format-xml){.hoverxref .tooltip
    .reference .internal}

But you can also extend the supported format through the
[[`FEED_EXPORTERS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FEED_EXPORTERS){.hoverxref .tooltip
.reference .internal} setting.

::: {#json .section}
[]{#topics-feed-format-json}

##### JSON[¶](#json "Permalink to this heading"){.headerlink}

-   Value for the [`format`{.docutils .literal .notranslate}]{.pre} key
    in the [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
    .reference .internal} setting: [`json`{.docutils .literal
    .notranslate}]{.pre}

-   Exporter used: [[`JsonItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.JsonItemExporter "scrapy.exporters.JsonItemExporter"){.reference
    .internal}

-   See [[this warning]{.std
    .std-ref}](index.html#json-with-large-data){.hoverxref .tooltip
    .reference .internal} if you're using JSON with large feeds.
:::

::: {#json-lines .section}
[]{#topics-feed-format-jsonlines}

##### JSON lines[¶](#json-lines "Permalink to this heading"){.headerlink}

-   Value for the [`format`{.docutils .literal .notranslate}]{.pre} key
    in the [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
    .reference .internal} setting: [`jsonlines`{.docutils .literal
    .notranslate}]{.pre}

-   Exporter used: [[`JsonLinesItemExporter`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.JsonLinesItemExporter "scrapy.exporters.JsonLinesItemExporter"){.reference
    .internal}
:::

::: {#csv .section}
[]{#topics-feed-format-csv}

##### CSV[¶](#csv "Permalink to this heading"){.headerlink}

-   Value for the [`format`{.docutils .literal .notranslate}]{.pre} key
    in the [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
    .reference .internal} setting: [`csv`{.docutils .literal
    .notranslate}]{.pre}

-   Exporter used: [[`CsvItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.CsvItemExporter "scrapy.exporters.CsvItemExporter"){.reference
    .internal}

-   To specify columns to export, their order and their column names,
    use [[`FEED_EXPORT_FIELDS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_FIELDS){.hoverxref
    .tooltip .reference .internal}. Other feed exporters can also use
    this option, but it is important for CSV because unlike many other
    export formats CSV uses a fixed header.
:::

::: {#xml .section}
[]{#topics-feed-format-xml}

##### XML[¶](#xml "Permalink to this heading"){.headerlink}

-   Value for the [`format`{.docutils .literal .notranslate}]{.pre} key
    in the [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
    .reference .internal} setting: [`xml`{.docutils .literal
    .notranslate}]{.pre}

-   Exporter used: [[`XmlItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.XmlItemExporter "scrapy.exporters.XmlItemExporter"){.reference
    .internal}
:::

::: {#pickle .section}
[]{#topics-feed-format-pickle}

##### Pickle[¶](#pickle "Permalink to this heading"){.headerlink}

-   Value for the [`format`{.docutils .literal .notranslate}]{.pre} key
    in the [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
    .reference .internal} setting: [`pickle`{.docutils .literal
    .notranslate}]{.pre}

-   Exporter used: [[`PickleItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.PickleItemExporter "scrapy.exporters.PickleItemExporter"){.reference
    .internal}
:::

::: {#marshal .section}
[]{#topics-feed-format-marshal}

##### Marshal[¶](#marshal "Permalink to this heading"){.headerlink}

-   Value for the [`format`{.docutils .literal .notranslate}]{.pre} key
    in the [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
    .reference .internal} setting: [`marshal`{.docutils .literal
    .notranslate}]{.pre}

-   Exporter used: [[`MarshalItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.MarshalItemExporter "scrapy.exporters.MarshalItemExporter"){.reference
    .internal}
:::
:::

::: {#storages .section}
[]{#topics-feed-storage}

#### Storages[¶](#storages "Permalink to this heading"){.headerlink}

When using the feed exports you define where to store the feed using one
or multiple
[URIs](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier){.reference
.external} (through the [[`FEEDS`{.xref .std .std-setting .docutils
.literal .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
.reference .internal} setting). The feed exports supports multiple
storage backend types which are defined by the URI scheme.

The storages backends supported out of the box are:

-   [[Local filesystem]{.std
    .std-ref}](#topics-feed-storage-fs){.hoverxref .tooltip .reference
    .internal}

-   [[FTP]{.std .std-ref}](#topics-feed-storage-ftp){.hoverxref .tooltip
    .reference .internal}

-   [[S3]{.std .std-ref}](#topics-feed-storage-s3){.hoverxref .tooltip
    .reference .internal} (requires
    [boto3](https://github.com/boto/boto3){.reference .external})

-   [[Google Cloud Storage (GCS)]{.std
    .std-ref}](#topics-feed-storage-gcs){.hoverxref .tooltip .reference
    .internal} (requires
    [google-cloud-storage](https://cloud.google.com/storage/docs/reference/libraries#client-libraries-install-python){.reference
    .external})

-   [[Standard output]{.std
    .std-ref}](#topics-feed-storage-stdout){.hoverxref .tooltip
    .reference .internal}

Some storage backends may be unavailable if the required external
libraries are not available. For example, the S3 backend is only
available if the [boto3](https://github.com/boto/boto3){.reference
.external} library is installed.
:::

::: {#storage-uri-parameters .section}
[]{#topics-feed-uri-params}

#### Storage URI parameters[¶](#storage-uri-parameters "Permalink to this heading"){.headerlink}

The storage URI can also contain parameters that get replaced when the
feed is being created. These parameters are:

-   [`%(time)s`{.docutils .literal .notranslate}]{.pre} - gets replaced
    by a timestamp when the feed is being created

-   [`%(name)s`{.docutils .literal .notranslate}]{.pre} - gets replaced
    by the spider name

Any other named parameter gets replaced by the spider attribute of the
same name. For example, [`%(site_id)s`{.docutils .literal
.notranslate}]{.pre} would get replaced by the
[`spider.site_id`{.docutils .literal .notranslate}]{.pre} attribute the
moment the feed is being created.

Here are some examples to illustrate:

-   Store in FTP using one directory per spider:

    -   [`ftp://user:password@ftp.example.com/scraping/feeds/%(name)s/%(time)s.json`{.docutils
        .literal .notranslate}]{.pre}

-   Store in S3 using one directory per spider:

    -   [`s3://mybucket/scraping/feeds/%(name)s/%(time)s.json`{.docutils
        .literal .notranslate}]{.pre}

::: {.admonition .note}
Note

[[Spider arguments]{.std .std-ref}](index.html#spiderargs){.hoverxref
.tooltip .reference .internal} become spider attributes, hence they can
also be used as storage URI parameters.
:::
:::

::: {#storage-backends .section}
[]{#topics-feed-storage-backends}

#### Storage backends[¶](#storage-backends "Permalink to this heading"){.headerlink}

::: {#local-filesystem .section}
[]{#topics-feed-storage-fs}

##### Local filesystem[¶](#local-filesystem "Permalink to this heading"){.headerlink}

The feeds are stored in the local filesystem.

-   URI scheme: [`file`{.docutils .literal .notranslate}]{.pre}

-   Example URI: [`file:///tmp/export.csv`{.docutils .literal
    .notranslate}]{.pre}

-   Required external libraries: none

Note that for the local filesystem storage (only) you can omit the
scheme if you specify an absolute path like [`/tmp/export.csv`{.docutils
.literal .notranslate}]{.pre} (Unix systems only). Alternatively you can
also use a [[`pathlib.Path`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.12)"){.reference
.external} object.
:::

::: {#ftp .section}
[]{#topics-feed-storage-ftp}

##### FTP[¶](#ftp "Permalink to this heading"){.headerlink}

The feeds are stored in a FTP server.

-   URI scheme: [`ftp`{.docutils .literal .notranslate}]{.pre}

-   Example URI:
    [`ftp://user:pass@ftp.example.com/path/to/export.csv`{.docutils
    .literal .notranslate}]{.pre}

-   Required external libraries: none

FTP supports two different connection modes: [active or
passive](https://stackoverflow.com/a/1699163){.reference .external}.
Scrapy uses the passive connection mode by default. To use the active
connection mode instead, set the [[`FEED_STORAGE_FTP_ACTIVE`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FEED_STORAGE_FTP_ACTIVE){.hoverxref
.tooltip .reference .internal} setting to [`True`{.docutils .literal
.notranslate}]{.pre}.

The default value for the [`overwrite`{.docutils .literal
.notranslate}]{.pre} key in the [[`FEEDS`{.xref .std .std-setting
.docutils .literal .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref
.tooltip .reference .internal} for this storage backend is:
[`True`{.docutils .literal .notranslate}]{.pre}.

::: {.admonition .caution}
Caution

The value [`True`{.docutils .literal .notranslate}]{.pre} in
[`overwrite`{.docutils .literal .notranslate}]{.pre} will cause you to
lose the previous version of your data.
:::

This storage backend uses [[delayed file delivery]{.std
.std-ref}](#delayed-file-delivery){.hoverxref .tooltip .reference
.internal}.
:::

::: {#s3 .section}
[]{#topics-feed-storage-s3}

##### S3[¶](#s3 "Permalink to this heading"){.headerlink}

The feeds are stored on [Amazon
S3](https://aws.amazon.com/s3/){.reference .external}.

-   URI scheme: [`s3`{.docutils .literal .notranslate}]{.pre}

-   Example URIs:

    -   [`s3://mybucket/path/to/export.csv`{.docutils .literal
        .notranslate}]{.pre}

    -   [`s3://aws_key:aws_secret@mybucket/path/to/export.csv`{.docutils
        .literal .notranslate}]{.pre}

-   Required external libraries:
    [boto3](https://github.com/boto/boto3){.reference .external} \>=
    1.20.0

The AWS credentials can be passed as user/password in the URI, or they
can be passed through the following settings:

-   [[`AWS_ACCESS_KEY_ID`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_ACCESS_KEY_ID){.hoverxref
    .tooltip .reference .internal}

-   [[`AWS_SECRET_ACCESS_KEY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_SECRET_ACCESS_KEY){.hoverxref
    .tooltip .reference .internal}

-   [[`AWS_SESSION_TOKEN`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_SESSION_TOKEN){.hoverxref
    .tooltip .reference .internal} (only needed for [temporary security
    credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#temporary-access-keys){.reference
    .external})

You can also define a custom ACL, custom endpoint, and region name for
exported feeds using these settings:

-   [[`FEED_STORAGE_S3_ACL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_STORAGE_S3_ACL){.hoverxref
    .tooltip .reference .internal}

-   [[`AWS_ENDPOINT_URL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_ENDPOINT_URL){.hoverxref
    .tooltip .reference .internal}

-   [[`AWS_REGION_NAME`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_REGION_NAME){.hoverxref
    .tooltip .reference .internal}

The default value for the [`overwrite`{.docutils .literal
.notranslate}]{.pre} key in the [[`FEEDS`{.xref .std .std-setting
.docutils .literal .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref
.tooltip .reference .internal} for this storage backend is:
[`True`{.docutils .literal .notranslate}]{.pre}.

::: {.admonition .caution}
Caution

The value [`True`{.docutils .literal .notranslate}]{.pre} in
[`overwrite`{.docutils .literal .notranslate}]{.pre} will cause you to
lose the previous version of your data.
:::

This storage backend uses [[delayed file delivery]{.std
.std-ref}](#delayed-file-delivery){.hoverxref .tooltip .reference
.internal}.
:::

::: {#google-cloud-storage-gcs .section}
[]{#topics-feed-storage-gcs}

##### Google Cloud Storage (GCS)[¶](#google-cloud-storage-gcs "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.3.]{.versionmodified .added}
:::

The feeds are stored on [Google Cloud
Storage](https://cloud.google.com/storage/){.reference .external}.

-   URI scheme: [`gs`{.docutils .literal .notranslate}]{.pre}

-   Example URIs:

    -   [`gs://mybucket/path/to/export.csv`{.docutils .literal
        .notranslate}]{.pre}

-   Required external libraries:
    [google-cloud-storage](https://cloud.google.com/storage/docs/reference/libraries#client-libraries-install-python){.reference
    .external}.

For more information about authentication, please refer to [Google Cloud
documentation](https://cloud.google.com/docs/authentication/production){.reference
.external}.

You can set a *Project ID* and *Access Control List (ACL)* through the
following settings:

-   [[`FEED_STORAGE_GCS_ACL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_STORAGE_GCS_ACL){.hoverxref
    .tooltip .reference .internal}

-   [[`GCS_PROJECT_ID`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-GCS_PROJECT_ID){.hoverxref
    .tooltip .reference .internal}

The default value for the [`overwrite`{.docutils .literal
.notranslate}]{.pre} key in the [[`FEEDS`{.xref .std .std-setting
.docutils .literal .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref
.tooltip .reference .internal} for this storage backend is:
[`True`{.docutils .literal .notranslate}]{.pre}.

::: {.admonition .caution}
Caution

The value [`True`{.docutils .literal .notranslate}]{.pre} in
[`overwrite`{.docutils .literal .notranslate}]{.pre} will cause you to
lose the previous version of your data.
:::

This storage backend uses [[delayed file delivery]{.std
.std-ref}](#delayed-file-delivery){.hoverxref .tooltip .reference
.internal}.
:::

::: {#standard-output .section}
[]{#topics-feed-storage-stdout}

##### Standard output[¶](#standard-output "Permalink to this heading"){.headerlink}

The feeds are written to the standard output of the Scrapy process.

-   URI scheme: [`stdout`{.docutils .literal .notranslate}]{.pre}

-   Example URI: [`stdout:`{.docutils .literal .notranslate}]{.pre}

-   Required external libraries: none
:::

::: {#delayed-file-delivery .section}
[]{#id1}

##### Delayed file delivery[¶](#delayed-file-delivery "Permalink to this heading"){.headerlink}

As indicated above, some of the described storage backends use delayed
file delivery.

These storage backends do not upload items to the feed URI as those
items are scraped. Instead, Scrapy writes items into a temporary local
file, and only once all the file contents have been written (i.e. at the
end of the crawl) is that file uploaded to the feed URI.

If you want item delivery to start earlier when using one of these
storage backends, use [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
.tooltip .reference .internal} to split the output items in multiple
files, with the specified maximum item count per file. That way, as soon
as a file reaches the maximum item count, that file is delivered to the
feed URI, allowing item delivery to start way before the end of the
crawl.
:::
:::

::: {#item-filtering .section}
[]{#item-filter}

#### Item filtering[¶](#item-filtering "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.6.0.]{.versionmodified .added}
:::

You can filter items that you want to allow for a particular feed by
using the [`item_classes`{.docutils .literal .notranslate}]{.pre} option
in [[feeds options]{.std .std-ref}](#feed-options){.hoverxref .tooltip
.reference .internal}. Only items of the specified types will be added
to the feed.

The [`item_classes`{.docutils .literal .notranslate}]{.pre} option is
implemented by the [[`ItemFilter`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.extensions.feedexport.ItemFilter "scrapy.extensions.feedexport.ItemFilter"){.reference
.internal} class, which is the default value of the
[`item_filter`{.docutils .literal .notranslate}]{.pre} [[feed
option]{.std .std-ref}](#feed-options){.hoverxref .tooltip .reference
.internal}.

You can create your own custom filtering class by implementing
[[`ItemFilter`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.extensions.feedexport.ItemFilter "scrapy.extensions.feedexport.ItemFilter"){.reference
.internal}'s method [`accepts`{.docutils .literal .notranslate}]{.pre}
and taking [`feed_options`{.docutils .literal .notranslate}]{.pre} as an
argument.

For instance:

::: {.highlight-python .notranslate}
::: highlight
    class MyCustomFilter:
        def __init__(self, feed_options):
            self.feed_options = feed_options

        def accepts(self, item):
            if "field1" in item and item["field1"] == "expected_data":
                return True
            return False
:::
:::

You can assign your custom filtering class to the
[`item_filter`{.docutils .literal .notranslate}]{.pre} [[option of a
feed]{.std .std-ref}](#feed-options){.hoverxref .tooltip .reference
.internal}. See [[`FEEDS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip .reference
.internal} for examples.

::: {#itemfilter .section}
##### ItemFilter[¶](#itemfilter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.feedexport.]{.pre}]{.sig-prename .descclassname}[[ItemFilter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[feed_options]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/feedexport.html#ItemFilter){.reference .internal}[¶](#scrapy.extensions.feedexport.ItemFilter "Permalink to this definition"){.headerlink}

:   This will be used by FeedExporter to decide if an item should be
    allowed to be exported to a particular feed.

    Parameters

    :   **feed_options**
        ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
        .external}) -- feed specific options passed from FeedExporter

    [[accepts]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/feedexport.html#ItemFilter.accepts){.reference .internal}[¶](#scrapy.extensions.feedexport.ItemFilter.accepts "Permalink to this definition"){.headerlink}

    :   Return [`True`{.docutils .literal .notranslate}]{.pre} if item
        should be exported or [`False`{.docutils .literal
        .notranslate}]{.pre} otherwise.

        Parameters

        :   **item** ([[Scrapy items]{.std
            .std-ref}](index.html#topics-items){.hoverxref .tooltip
            .reference .internal}) -- scraped item which user wants to
            check if is acceptable

        Returns

        :   True if accepted, False otherwise

        Return type