---
generator: "Docutils 0.17.1: http://docutils.sourceforge.net/"
lang: en
title: Scrapy 2.11.0 documentation
viewport: width=device-width, initial-scale=1.0
---

::: wy-grid-for-nav
::: wy-side-scroll
::: wy-side-nav-search
[Scrapy](#){.icon .icon-home}

::: version
master
:::
:::

::: {.wy-menu .wy-menu-vertical spy="affix" role="navigation" aria-label="Navigation menu"}
[First steps]{.caption-text}

-   [Scrapy at a glance](index.html#document-intro/overview){.reference
    .internal}
-   [Installation guide](index.html#document-intro/install){.reference
    .internal}
-   [Scrapy Tutorial](index.html#document-intro/tutorial){.reference
    .internal}
-   [Examples](index.html#document-intro/examples){.reference .internal}

[Basic concepts]{.caption-text}

-   [Command line tool](index.html#document-topics/commands){.reference
    .internal}
-   [Spiders](index.html#document-topics/spiders){.reference .internal}
-   [Selectors](index.html#document-topics/selectors){.reference
    .internal}
-   [Items](index.html#document-topics/items){.reference .internal}
-   [Item Loaders](index.html#document-topics/loaders){.reference
    .internal}
-   [Scrapy shell](index.html#document-topics/shell){.reference
    .internal}
-   [Item Pipeline](index.html#document-topics/item-pipeline){.reference
    .internal}
-   [Feed exports](index.html#document-topics/feed-exports){.reference
    .internal}
-   [Requests and
    Responses](index.html#document-topics/request-response){.reference
    .internal}
-   [Link
    Extractors](index.html#document-topics/link-extractors){.reference
    .internal}
-   [Settings](index.html#document-topics/settings){.reference
    .internal}
-   [Exceptions](index.html#document-topics/exceptions){.reference
    .internal}

[Built-in services]{.caption-text}

-   [Logging](index.html#document-topics/logging){.reference .internal}
-   [Stats Collection](index.html#document-topics/stats){.reference
    .internal}
-   [Sending e-mail](index.html#document-topics/email){.reference
    .internal}
-   [Telnet
    Console](index.html#document-topics/telnetconsole){.reference
    .internal}

[Solving specific problems]{.caption-text}

-   [Frequently Asked Questions](index.html#document-faq){.reference
    .internal}
-   [Debugging Spiders](index.html#document-topics/debug){.reference
    .internal}
-   [Spiders Contracts](index.html#document-topics/contracts){.reference
    .internal}
-   [Common Practices](index.html#document-topics/practices){.reference
    .internal}
-   [Broad Crawls](index.html#document-topics/broad-crawls){.reference
    .internal}
-   [Using your browser's Developer Tools for
    scraping](index.html#document-topics/developer-tools){.reference
    .internal}
-   [Selecting dynamically-loaded
    content](index.html#document-topics/dynamic-content){.reference
    .internal}
-   [Debugging memory
    leaks](index.html#document-topics/leaks){.reference .internal}
-   [Downloading and processing files and
    images](index.html#document-topics/media-pipeline){.reference
    .internal}
-   [Deploying Spiders](index.html#document-topics/deploy){.reference
    .internal}
-   [AutoThrottle
    extension](index.html#document-topics/autothrottle){.reference
    .internal}
-   [Benchmarking](index.html#document-topics/benchmarking){.reference
    .internal}
-   [Jobs: pausing and resuming
    crawls](index.html#document-topics/jobs){.reference .internal}
-   [Coroutines](index.html#document-topics/coroutines){.reference
    .internal}
-   [asyncio](index.html#document-topics/asyncio){.reference .internal}

[Extending Scrapy]{.caption-text}

-   [Architecture
    overview](index.html#document-topics/architecture){.reference
    .internal}
-   [Add-ons](index.html#document-topics/addons){.reference .internal}
-   [Downloader
    Middleware](index.html#document-topics/downloader-middleware){.reference
    .internal}
-   [Spider
    Middleware](index.html#document-topics/spider-middleware){.reference
    .internal}
-   [Extensions](index.html#document-topics/extensions){.reference
    .internal}
-   [Signals](index.html#document-topics/signals){.reference .internal}
-   [Scheduler](index.html#document-topics/scheduler){.reference
    .internal}
-   [Item Exporters](index.html#document-topics/exporters){.reference
    .internal}
-   [Components](index.html#document-topics/components){.reference
    .internal}
-   [Core API](index.html#document-topics/api){.reference .internal}

[All the rest]{.caption-text}

-   [Release notes](index.html#document-news){.reference .internal}
-   [Contributing to
    Scrapy](index.html#document-contributing){.reference .internal}
-   [Versioning and API
    stability](index.html#document-versioning){.reference .internal}
:::
:::

::: {.section .wy-nav-content-wrap toggle="wy-nav-shift"}
[Scrapy](#)

::: wy-nav-content
::: rst-content
::: {role="navigation" aria-label="Page navigation"}
-   [](#){.icon .icon-home} »
-   Scrapy 2.11.0 documentation
-   [Edit on
    GitHub](https://github.com/scrapy/scrapy/blob/master/docs/index){.fa
    .fa-github}

------------------------------------------------------------------------
:::

::: {.document role="main" itemscope="itemscope" itemtype="http://schema.org/Article"}
::: {itemprop="articleBody"}
::: {#scrapy-version-documentation .section}
[]{#topics-index}

# Scrapy 2.11 documentation[¶](#scrapy-version-documentation "Permalink to this heading"){.headerlink}

Scrapy is a fast high-level [web
crawling](https://en.wikipedia.org/wiki/Web_crawler){.reference
.external} and [web
scraping](https://en.wikipedia.org/wiki/Web_scraping){.reference
.external} framework, used to crawl websites and extract structured data
from their pages. It can be used for a wide range of purposes, from data
mining to monitoring and automated testing.

::: {#getting-help .section}
[]{#id1}

## Getting help[¶](#getting-help "Permalink to this heading"){.headerlink}

Having trouble? We'd like to help!

-   Try the [[FAQ]{.doc}](index.html#document-faq){.reference .internal}
    -- it's got answers to some common questions.

-   Looking for specific information? Try the [[Index]{.std
    .std-ref}](genindex.html){.reference .internal} or [[Module
    Index]{.std .std-ref}](py-modindex.html){.reference .internal}.

-   Ask or search questions in [StackOverflow using the scrapy
    tag](https://stackoverflow.com/tags/scrapy){.reference .external}.

-   Ask or search questions in the [Scrapy
    subreddit](https://www.reddit.com/r/scrapy/){.reference .external}.

-   Search for questions on the archives of the [scrapy-users mailing
    list](https://groups.google.com/forum/#!forum/scrapy-users){.reference
    .external}.

-   Ask a question in the [#scrapy IRC
    channel](irc://irc.freenode.net/scrapy){.reference .external},

-   Report bugs with Scrapy in our [issue
    tracker](https://github.com/scrapy/scrapy/issues){.reference
    .external}.

-   Join the Discord community [Scrapy
    Discord](https://discord.gg/mv3yErfpvq){.reference .external}.
:::

::: {#first-steps .section}
## First steps[¶](#first-steps "Permalink to this heading"){.headerlink}

::: {.toctree-wrapper .compound}
[]{#document-intro/overview}

::: {#scrapy-at-a-glance .section}
[]{#intro-overview}

### Scrapy at a glance[¶](#scrapy-at-a-glance "Permalink to this heading"){.headerlink}

Scrapy (/ˈskreɪpaɪ/) is an application framework for crawling web sites
and extracting structured data which can be used for a wide range of
useful applications, like data mining, information processing or
historical archival.

Even though Scrapy was originally designed for [web
scraping](https://en.wikipedia.org/wiki/Web_scraping){.reference
.external}, it can also be used to extract data using APIs (such as
[Amazon Associates Web
Services](https://affiliate-program.amazon.com/gp/advertising/api/detail/main.html){.reference
.external}) or as a general purpose web crawler.

::: {#walk-through-of-an-example-spider .section}
#### Walk-through of an example spider[¶](#walk-through-of-an-example-spider "Permalink to this heading"){.headerlink}

In order to show you what Scrapy brings to the table, we'll walk you
through an example of a Scrapy Spider using the simplest way to run a
spider.

Here's the code for a spider that scrapes famous quotes from website
[https://quotes.toscrape.com](https://quotes.toscrape.com){.reference
.external}, following the pagination:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"
        start_urls = [
            "https://quotes.toscrape.com/tag/humor/",
        ]

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {
                    "author": quote.xpath("span/small/text()").get(),
                    "text": quote.css("span.text::text").get(),
                }

            next_page = response.css('li.next a::attr("href")').get()
            if next_page is not None:
                yield response.follow(next_page, self.parse)
:::
:::

Put this in a text file, name it to something like
[`quotes_spider.py`{.docutils .literal .notranslate}]{.pre} and run the
spider using the [[`runspider`{.xref .std .std-command .docutils
.literal
.notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
.tooltip .reference .internal} command:

::: {.highlight-default .notranslate}
::: highlight
    scrapy runspider quotes_spider.py -o quotes.jsonl
:::
:::

When this finishes you will have in the [`quotes.jsonl`{.docutils
.literal .notranslate}]{.pre} file a list of the quotes in JSON Lines
format, containing text and author, looking like this:

::: {.highlight-default .notranslate}
::: highlight
    {"author": "Jane Austen", "text": "\u201cThe person, be it gentleman or lady, who has not pleasure in a good novel, must be intolerably stupid.\u201d"}
    {"author": "Steve Martin", "text": "\u201cA day without sunshine is like, you know, night.\u201d"}
    {"author": "Garrison Keillor", "text": "\u201cAnyone who thinks sitting in church can make you a Christian must also think that sitting in a garage can make you a car.\u201d"}
    ...
:::
:::

::: {#what-just-happened .section}
##### What just happened?[¶](#what-just-happened "Permalink to this heading"){.headerlink}

When you ran the command [`scrapy`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`runspider`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`quotes_spider.py`{.docutils .literal
.notranslate}]{.pre}, Scrapy looked for a Spider definition inside it
and ran it through its crawler engine.

The crawl started by making requests to the URLs defined in the
[`start_urls`{.docutils .literal .notranslate}]{.pre} attribute (in this
case, only the URL for quotes in *humor* category) and called the
default callback method [`parse`{.docutils .literal
.notranslate}]{.pre}, passing the response object as an argument. In the
[`parse`{.docutils .literal .notranslate}]{.pre} callback, we loop
through the quote elements using a CSS Selector, yield a Python dict
with the extracted quote text and author, look for a link to the next
page and schedule another request using the same [`parse`{.docutils
.literal .notranslate}]{.pre} method as callback.

Here you notice one of the main advantages about Scrapy: requests are
[[scheduled and processed asynchronously]{.std
.std-ref}](index.html#topics-architecture){.hoverxref .tooltip
.reference .internal}. This means that Scrapy doesn't need to wait for a
request to be finished and processed, it can send another request or do
other things in the meantime. This also means that other requests can
keep going even if some request fails or an error happens while handling
it.

While this enables you to do very fast crawls (sending multiple
concurrent requests at the same time, in a fault-tolerant way) Scrapy
also gives you control over the politeness of the crawl through [[a few
settings]{.std .std-ref}](index.html#topics-settings-ref){.hoverxref
.tooltip .reference .internal}. You can do things like setting a
download delay between each request, limiting amount of concurrent
requests per domain or per IP, and even [[using an auto-throttling
extension]{.std .std-ref}](index.html#topics-autothrottle){.hoverxref
.tooltip .reference .internal} that tries to figure out these
automatically.

::: {.admonition .note}
Note

This is using [[feed exports]{.std
.std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
.reference .internal} to generate the JSON file, you can easily change
the export format (XML or CSV, for example) or the storage backend (FTP
or [Amazon S3](https://aws.amazon.com/s3/){.reference .external}, for
example). You can also write an [[item pipeline]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal} to store the items in a database.
:::
:::
:::

::: {#what-else .section}
[]{#topics-whatelse}

#### What else?[¶](#what-else "Permalink to this heading"){.headerlink}

You've seen how to extract and store items from a website using Scrapy,
but this is just the surface. Scrapy provides a lot of powerful features
for making scraping easy and efficient, such as:

-   Built-in support for [[selecting and extracting]{.std
    .std-ref}](index.html#topics-selectors){.hoverxref .tooltip
    .reference .internal} data from HTML/XML sources using extended CSS
    selectors and XPath expressions, with helper methods to extract
    using regular expressions.

-   An [[interactive shell console]{.std
    .std-ref}](index.html#topics-shell){.hoverxref .tooltip .reference
    .internal} (IPython aware) for trying out the CSS and XPath
    expressions to scrape data, very useful when writing or debugging
    your spiders.

-   Built-in support for [[generating feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} in multiple formats (JSON, CSV, XML) and
    storing them in multiple backends (FTP, S3, local filesystem)

-   Robust encoding support and auto-detection, for dealing with
    foreign, non-standard and broken encoding declarations.

-   [[Strong extensibility support]{.std
    .std-ref}](index.html#extending-scrapy){.hoverxref .tooltip
    .reference .internal}, allowing you to plug in your own
    functionality using [[signals]{.std
    .std-ref}](index.html#topics-signals){.hoverxref .tooltip .reference
    .internal} and a well-defined API (middlewares, [[extensions]{.std
    .std-ref}](index.html#topics-extensions){.hoverxref .tooltip
    .reference .internal}, and [[pipelines]{.std
    .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
    .reference .internal}).

-   Wide range of built-in extensions and middlewares for handling:

    -   cookies and session handling

    -   HTTP features like compression, authentication, caching

    -   user-agent spoofing

    -   robots.txt

    -   crawl depth restriction

    -   and more

-   A [[Telnet console]{.std
    .std-ref}](index.html#topics-telnetconsole){.hoverxref .tooltip
    .reference .internal} for hooking into a Python console running
    inside your Scrapy process, to introspect and debug your crawler

-   Plus other goodies like reusable spiders to crawl sites from
    [Sitemaps](https://www.sitemaps.org/index.html){.reference
    .external} and XML/CSV feeds, a media pipeline for [[automatically
    downloading images]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal} (or any other media) associated with the
    scraped items, a caching DNS resolver, and much more!
:::

::: {#what-s-next .section}
#### What's next?[¶](#what-s-next "Permalink to this heading"){.headerlink}

The next steps for you are to [[install Scrapy]{.std
.std-ref}](index.html#intro-install){.hoverxref .tooltip .reference
.internal}, [[follow through the tutorial]{.std
.std-ref}](index.html#intro-tutorial){.hoverxref .tooltip .reference
.internal} to learn how to create a full-blown Scrapy project and [join
the community](https://scrapy.org/community/){.reference .external}.
Thanks for your interest!
:::
:::

[]{#document-intro/install}

::: {#installation-guide .section}
[]{#intro-install}

### Installation guide[¶](#installation-guide "Permalink to this heading"){.headerlink}

::: {#supported-python-versions .section}
[]{#faq-python-versions}

#### Supported Python versions[¶](#supported-python-versions "Permalink to this heading"){.headerlink}

Scrapy requires Python 3.8+, either the CPython implementation (default)
or the PyPy implementation (see [Alternate
Implementations](https://docs.python.org/3/reference/introduction.html#implementations "(in Python v3.12)"){.reference
.external}).
:::

::: {#installing-scrapy .section}
[]{#intro-install-scrapy}

#### Installing Scrapy[¶](#installing-scrapy "Permalink to this heading"){.headerlink}

If you're using
[Anaconda](https://docs.anaconda.com/anaconda/){.reference .external} or
[Miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html){.reference
.external}, you can install the package from the
[conda-forge](https://conda-forge.org/){.reference .external} channel,
which has up-to-date packages for Linux, Windows and macOS.

To install Scrapy using [`conda`{.docutils .literal
.notranslate}]{.pre}, run:

::: {.highlight-default .notranslate}
::: highlight
    conda install -c conda-forge scrapy
:::
:::

Alternatively, if you're already familiar with installation of Python
packages, you can install Scrapy and its dependencies from PyPI with:

::: {.highlight-default .notranslate}
::: highlight
    pip install Scrapy
:::
:::

We strongly recommend that you install Scrapy in [[a dedicated
virtualenv]{.std .std-ref}](#intro-using-virtualenv){.hoverxref .tooltip
.reference .internal}, to avoid conflicting with your system packages.

Note that sometimes this may require solving compilation issues for some
Scrapy dependencies depending on your operating system, so be sure to
check the [[Platform specific installation notes]{.std
.std-ref}](#intro-install-platform-notes){.hoverxref .tooltip .reference
.internal}.

For more detailed and platform specifics instructions, as well as
troubleshooting information, read on.

::: {#things-that-are-good-to-know .section}
##### Things that are good to know[¶](#things-that-are-good-to-know "Permalink to this heading"){.headerlink}

Scrapy is written in pure Python and depends on a few key Python
packages (among others):

-   [lxml](https://lxml.de/index.html){.reference .external}, an
    efficient XML and HTML parser

-   [parsel](https://pypi.org/project/parsel/){.reference .external}, an
    HTML/XML data extraction library written on top of lxml,

-   [w3lib](https://pypi.org/project/w3lib/){.reference .external}, a
    multi-purpose helper for dealing with URLs and web page encodings

-   [twisted](https://twistedmatrix.com/trac/){.reference .external}, an
    asynchronous networking framework

-   [cryptography](https://cryptography.io/en/latest/){.reference
    .external} and
    [pyOpenSSL](https://pypi.org/project/pyOpenSSL/){.reference
    .external}, to deal with various network-level security needs

Some of these packages themselves depend on non-Python packages that
might require additional installation steps depending on your platform.
Please check [[platform-specific guides below]{.std
.std-ref}](#intro-install-platform-notes){.hoverxref .tooltip .reference
.internal}.

In case of any trouble related to these dependencies, please refer to
their respective installation instructions:

-   [lxml installation](https://lxml.de/installation.html){.reference
    .external}

-   [[cryptography installation]{.xref .std
    .std-doc}](https://cryptography.io/en/latest/installation/ "(in Cryptography v42.0.0.dev1)"){.reference
    .external}
:::

::: {#using-a-virtual-environment-recommended .section}
[]{#intro-using-virtualenv}

##### Using a virtual environment (recommended)[¶](#using-a-virtual-environment-recommended "Permalink to this heading"){.headerlink}

TL;DR: We recommend installing Scrapy inside a virtual environment on
all platforms.

Python packages can be installed either globally (a.k.a system wide), or
in user-space. We do not recommend installing Scrapy system wide.

Instead, we recommend that you install Scrapy within a so-called
"virtual environment" ([[`venv`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/venv.html#module-venv "(in Python v3.12)"){.reference
.external}). Virtual environments allow you to not conflict with
already-installed Python system packages (which could break some of your
system tools and scripts), and still install packages normally with
[`pip`{.docutils .literal .notranslate}]{.pre} (without
[`sudo`{.docutils .literal .notranslate}]{.pre} and the likes).

See [Virtual Environments and
Packages](https://docs.python.org/3/tutorial/venv.html#tut-venv "(in Python v3.12)"){.reference
.external} on how to create your virtual environment.

Once you have created a virtual environment, you can install Scrapy
inside it with [`pip`{.docutils .literal .notranslate}]{.pre}, just like
any other Python package. (See [[platform-specific guides]{.std
.std-ref}](#intro-install-platform-notes){.hoverxref .tooltip .reference
.internal} below for non-Python dependencies that you may need to
install beforehand).
:::
:::

::: {#platform-specific-installation-notes .section}
[]{#intro-install-platform-notes}

#### Platform specific installation notes[¶](#platform-specific-installation-notes "Permalink to this heading"){.headerlink}

::: {#windows .section}
[]{#intro-install-windows}

##### Windows[¶](#windows "Permalink to this heading"){.headerlink}

Though it's possible to install Scrapy on Windows using pip, we
recommend you to install
[Anaconda](https://docs.anaconda.com/anaconda/){.reference .external} or
[Miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html){.reference
.external} and use the package from the
[conda-forge](https://conda-forge.org/){.reference .external} channel,
which will avoid most installation issues.

Once you've installed
[Anaconda](https://docs.anaconda.com/anaconda/){.reference .external} or
[Miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html){.reference
.external}, install Scrapy with:

::: {.highlight-default .notranslate}
::: highlight
    conda install -c conda-forge scrapy
:::
:::

To install Scrapy on Windows using [`pip`{.docutils .literal
.notranslate}]{.pre}:

::: {.admonition .warning}
Warning

This installation method requires "Microsoft Visual C++" for installing
some Scrapy dependencies, which demands significantly more disk space
than Anaconda.
:::

1.  Download and execute [Microsoft C++ Build
    Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/){.reference
    .external} to install the Visual Studio Installer.

2.  Run the Visual Studio Installer.

3.  Under the Workloads section, select **C++ build tools**.

4.  Check the installation details and make sure following packages are
    selected as optional components:

    > <div>
    >
    > -   **MSVC** (e.g MSVC v142 - VS 2019 C++ x64/x86 build tools
    >     (v14.23) )
    >
    > -   **Windows SDK** (e.g Windows 10 SDK (10.0.18362.0))
    >
    > </div>

5.  Install the Visual Studio Build Tools.

Now, you should be able to [[install Scrapy]{.std
.std-ref}](#intro-install-scrapy){.hoverxref .tooltip .reference
.internal} using [`pip`{.docutils .literal .notranslate}]{.pre}.
:::

::: {#ubuntu-14-04-or-above .section}
[]{#intro-install-ubuntu}

##### Ubuntu 14.04 or above[¶](#ubuntu-14-04-or-above "Permalink to this heading"){.headerlink}

Scrapy is currently tested with recent-enough versions of lxml, twisted
and pyOpenSSL, and is compatible with recent Ubuntu distributions. But
it should support older versions of Ubuntu too, like Ubuntu 14.04,
albeit with potential issues with TLS connections.

**Don't** use the [`python-scrapy`{.docutils .literal
.notranslate}]{.pre} package provided by Ubuntu, they are typically too
old and slow to catch up with latest Scrapy.

To install Scrapy on Ubuntu (or Ubuntu-based) systems, you need to
install these dependencies:

::: {.highlight-default .notranslate}
::: highlight
    sudo apt-get install python3 python3-dev python3-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev
:::
:::

-   [`python3-dev`{.docutils .literal .notranslate}]{.pre},
    [`zlib1g-dev`{.docutils .literal .notranslate}]{.pre},
    [`libxml2-dev`{.docutils .literal .notranslate}]{.pre} and
    [`libxslt1-dev`{.docutils .literal .notranslate}]{.pre} are required
    for [`lxml`{.docutils .literal .notranslate}]{.pre}

-   [`libssl-dev`{.docutils .literal .notranslate}]{.pre} and
    [`libffi-dev`{.docutils .literal .notranslate}]{.pre} are required
    for [`cryptography`{.docutils .literal .notranslate}]{.pre}

Inside a [[virtualenv]{.std
.std-ref}](#intro-using-virtualenv){.hoverxref .tooltip .reference
.internal}, you can install Scrapy with [`pip`{.docutils .literal
.notranslate}]{.pre} after that:

::: {.highlight-default .notranslate}
::: highlight
    pip install scrapy
:::
:::

::: {.admonition .note}
Note

The same non-Python dependencies can be used to install Scrapy in Debian
Jessie (8.0) and above.
:::
:::

::: {#macos .section}
[]{#intro-install-macos}

##### macOS[¶](#macos "Permalink to this heading"){.headerlink}

Building Scrapy's dependencies requires the presence of a C compiler and
development headers. On macOS this is typically provided by Apple's
Xcode development tools. To install the Xcode command line tools open a
terminal window and run:

::: {.highlight-default .notranslate}
::: highlight
    xcode-select --install
:::
:::

There's a [known
issue](https://github.com/pypa/pip/issues/2468){.reference .external}
that prevents [`pip`{.docutils .literal .notranslate}]{.pre} from
updating system packages. This has to be addressed to successfully
install Scrapy and its dependencies. Here are some proposed solutions:

-   *(Recommended)* **Don't** use system Python. Install a new, updated
    version that doesn't conflict with the rest of your system. Here's
    how to do it using the [homebrew](https://brew.sh/){.reference
    .external} package manager:

    -   Install [homebrew](https://brew.sh/){.reference .external}
        following the instructions in
        [https://brew.sh/](https://brew.sh/){.reference .external}

    -   Update your [`PATH`{.docutils .literal .notranslate}]{.pre}
        variable to state that homebrew packages should be used before
        system packages (Change [`.bashrc`{.docutils .literal
        .notranslate}]{.pre} to [`.zshrc`{.docutils .literal
        .notranslate}]{.pre} accordingly if you're using
        [zsh](https://www.zsh.org/){.reference .external} as default
        shell):

        ::: {.highlight-default .notranslate}
        ::: highlight
            echo "export PATH=/usr/local/bin:/usr/local/sbin:$PATH" >> ~/.bashrc
        :::
        :::

    -   Reload [`.bashrc`{.docutils .literal .notranslate}]{.pre} to
        ensure the changes have taken place:

        ::: {.highlight-default .notranslate}
        ::: highlight
            source ~/.bashrc
        :::
        :::

    -   Install python:

        ::: {.highlight-default .notranslate}
        ::: highlight
            brew install python
        :::
        :::

    -   Latest versions of python have [`pip`{.docutils .literal
        .notranslate}]{.pre} bundled with them so you won't need to
        install it separately. If this is not the case, upgrade python:

        ::: {.highlight-default .notranslate}
        ::: highlight
            brew update; brew upgrade python
        :::
        :::

-   *(Optional)* [[Install Scrapy inside a Python virtual
    environment]{.std .std-ref}](#intro-using-virtualenv){.hoverxref
    .tooltip .reference .internal}.

> <div>
>
> This method is a workaround for the above macOS issue, but it's an
> overall good practice for managing dependencies and can complement the
> first method.
>
> </div>

After any of these workarounds you should be able to install Scrapy:

::: {.highlight-default .notranslate}
::: highlight
    pip install Scrapy
:::
:::
:::

::: {#pypy .section}
##### PyPy[¶](#pypy "Permalink to this heading"){.headerlink}

We recommend using the latest PyPy version. For PyPy3, only Linux
installation was tested.

Most Scrapy dependencies now have binary wheels for CPython, but not for
PyPy. This means that these dependencies will be built during
installation. On macOS, you are likely to face an issue with building
the Cryptography dependency. The solution to this problem is described
[here](https://github.com/pyca/cryptography/issues/2692#issuecomment-272773481){.reference
.external}, that is to [`brew`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`install`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`openssl`{.docutils .literal .notranslate}]{.pre} and then
export the flags that this command recommends (only needed when
installing Scrapy). Installing on Linux has no special issues besides
installing build dependencies. Installing Scrapy with PyPy on Windows is
not tested.

You can check that Scrapy is installed correctly by running
[`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`bench`{.docutils .literal .notranslate}]{.pre}. If this
command gives errors such as [`TypeError:`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`...`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`got`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`2`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`unexpected`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`keyword`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`arguments`{.docutils .literal .notranslate}]{.pre}, this
means that setuptools was unable to pick up one PyPy-specific
dependency. To fix this issue, run [`pip`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`install`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`'PyPyDispatcher>=2.1.0'`{.docutils .literal
.notranslate}]{.pre}.
:::
:::

::: {#troubleshooting .section}
[]{#intro-install-troubleshooting}

#### Troubleshooting[¶](#troubleshooting "Permalink to this heading"){.headerlink}

::: {#attributeerror-module-object-has-no-attribute-op-no-tlsv1-1 .section}
##### AttributeError: 'module' object has no attribute 'OP_NO_TLSv1_1'[¶](#attributeerror-module-object-has-no-attribute-op-no-tlsv1-1 "Permalink to this heading"){.headerlink}

After you install or upgrade Scrapy, Twisted or pyOpenSSL, you may get
an exception with the following traceback:

::: {.highlight-default .notranslate}
::: highlight
    […]
      File "[…]/site-packages/twisted/protocols/tls.py", line 63, in <module>
        from twisted.internet._sslverify import _setAcceptableProtocols
      File "[…]/site-packages/twisted/internet/_sslverify.py", line 38, in <module>
        TLSVersion.TLSv1_1: SSL.OP_NO_TLSv1_1,
    AttributeError: 'module' object has no attribute 'OP_NO_TLSv1_1'
:::
:::

The reason you get this exception is that your system or virtual
environment has a version of pyOpenSSL that your version of Twisted does
not support.

To install a version of pyOpenSSL that your version of Twisted supports,
reinstall Twisted with the [`tls`{.code .docutils .literal
.notranslate}]{.pre} extra option:

::: {.highlight-default .notranslate}
::: highlight
    pip install twisted[tls]
:::
:::

For details, see [Issue
#2473](https://github.com/scrapy/scrapy/issues/2473){.reference
.external}.
:::
:::
:::

[]{#document-intro/tutorial}

::: {#scrapy-tutorial .section}
[]{#intro-tutorial}

### Scrapy Tutorial[¶](#scrapy-tutorial "Permalink to this heading"){.headerlink}

In this tutorial, we'll assume that Scrapy is already installed on your
system. If that's not the case, see [[Installation guide]{.std
.std-ref}](index.html#intro-install){.hoverxref .tooltip .reference
.internal}.

We are going to scrape
[quotes.toscrape.com](https://quotes.toscrape.com/){.reference
.external}, a website that lists quotes from famous authors.

This tutorial will walk you through these tasks:

1.  Creating a new Scrapy project

2.  Writing a [[spider]{.std
    .std-ref}](index.html#topics-spiders){.hoverxref .tooltip .reference
    .internal} to crawl a site and extract data

3.  Exporting the scraped data using the command line

4.  Changing spider to recursively follow links

5.  Using spider arguments

Scrapy is written in [Python](https://www.python.org/){.reference
.external}. If you're new to the language you might want to start by
getting an idea of what the language is like, to get the most out of
Scrapy.

If you're already familiar with other languages, and want to learn
Python quickly, the [Python
Tutorial](https://docs.python.org/3/tutorial){.reference .external} is a
good resource.

If you're new to programming and want to start with Python, the
following books may be useful to you:

-   [Automate the Boring Stuff With
    Python](https://automatetheboringstuff.com/){.reference .external}

-   [How To Think Like a Computer
    Scientist](http://openbookproject.net/thinkcs/python/english3e/){.reference
    .external}

-   [Learn Python 3 The Hard
    Way](https://learnpythonthehardway.org/python3/){.reference
    .external}

You can also take a look at [this list of Python resources for
non-programmers](https://wiki.python.org/moin/BeginnersGuide/NonProgrammers){.reference
.external}, as well as the [suggested resources in the
learnpython-subreddit](https://www.reddit.com/r/learnpython/wiki/index#wiki_new_to_python.3F){.reference
.external}.

::: {#creating-a-project .section}
#### Creating a project[¶](#creating-a-project "Permalink to this heading"){.headerlink}

Before you start scraping, you will have to set up a new Scrapy project.
Enter a directory where you'd like to store your code and run:

::: {.highlight-default .notranslate}
::: highlight
    scrapy startproject tutorial
:::
:::

This will create a [`tutorial`{.docutils .literal .notranslate}]{.pre}
directory with the following contents:

::: {.highlight-default .notranslate}
::: highlight
    tutorial/
        scrapy.cfg            # deploy configuration file

        tutorial/             # project's Python module, you'll import your code from here
            __init__.py

            items.py          # project items definition file

            middlewares.py    # project middlewares file

            pipelines.py      # project pipelines file

            settings.py       # project settings file

            spiders/          # a directory where you'll later put your spiders
                __init__.py
:::
:::
:::

::: {#our-first-spider .section}
#### Our first Spider[¶](#our-first-spider "Permalink to this heading"){.headerlink}

Spiders are classes that you define and that Scrapy uses to scrape
information from a website (or a group of websites). They must subclass
[[`Spider`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
.internal} and define the initial requests to make, optionally how to
follow links in the pages, and how to parse the downloaded page content
to extract data.

This is the code for our first Spider. Save it in a file named
[`quotes_spider.py`{.docutils .literal .notranslate}]{.pre} under the
[`tutorial/spiders`{.docutils .literal .notranslate}]{.pre} directory in
your project:

::: {.highlight-python .notranslate}
::: highlight
    from pathlib import Path

    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"

        def start_requests(self):
            urls = [
                "https://quotes.toscrape.com/page/1/",
                "https://quotes.toscrape.com/page/2/",
            ]
            for url in urls:
                yield scrapy.Request(url=url, callback=self.parse)

        def parse(self, response):
            page = response.url.split("/")[-2]
            filename = f"quotes-{page}.html"
            Path(filename).write_bytes(response.body)
            self.log(f"Saved file {filename}")
:::
:::

As you can see, our Spider subclasses [[`scrapy.Spider`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
.internal} and defines some attributes and methods:

-   [[`name`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.name "scrapy.Spider.name"){.reference
    .internal}: identifies the Spider. It must be unique within a
    project, that is, you can't set the same name for different Spiders.

-   [[`start_requests()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
    .internal}: must return an iterable of Requests (you can return a
    list of requests or write a generator function) which the Spider
    will begin to crawl from. Subsequent requests will be generated
    successively from these initial requests.

-   [[`parse()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
    .internal}: a method that will be called to handle the response
    downloaded for each of the requests made. The response parameter is
    an instance of [[`TextResponse`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} that holds the page content and has further helpful
    methods to handle it.

    The [[`parse()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
    .internal} method usually parses the response, extracting the
    scraped data as dicts and also finding new URLs to follow and
    creating new requests ([`Request`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre}) from them.

::: {#how-to-run-our-spider .section}
##### How to run our spider[¶](#how-to-run-our-spider "Permalink to this heading"){.headerlink}

To put our spider to work, go to the project's top level directory and
run:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl quotes
:::
:::

This command runs the spider with name [`quotes`{.docutils .literal
.notranslate}]{.pre} that we've just added, that will send some requests
for the [`quotes.toscrape.com`{.docutils .literal .notranslate}]{.pre}
domain. You will get an output similar to this:

::: {.highlight-default .notranslate}
::: highlight
    ... (omitted for brevity)
    2016-12-16 21:24:05 [scrapy.core.engine] INFO: Spider opened
    2016-12-16 21:24:05 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:24:05 [scrapy.extensions.telnet] DEBUG: Telnet console listening on 127.0.0.1:6023
    2016-12-16 21:24:05 [scrapy.core.engine] DEBUG: Crawled (404) <GET https://quotes.toscrape.com/robots.txt> (referer: None)
    2016-12-16 21:24:05 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://quotes.toscrape.com/page/1/> (referer: None)
    2016-12-16 21:24:05 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://quotes.toscrape.com/page/2/> (referer: None)
    2016-12-16 21:24:05 [quotes] DEBUG: Saved file quotes-1.html
    2016-12-16 21:24:05 [quotes] DEBUG: Saved file quotes-2.html
    2016-12-16 21:24:05 [scrapy.core.engine] INFO: Closing spider (finished)
    ...
:::
:::

Now, check the files in the current directory. You should notice that
two new files have been created: *quotes-1.html* and *quotes-2.html*,
with the content for the respective URLs, as our [`parse`{.docutils
.literal .notranslate}]{.pre} method instructs.

::: {.admonition .note}
Note

If you are wondering why we haven't parsed the HTML yet, hold on, we
will cover that soon.
:::

::: {#what-just-happened-under-the-hood .section}
###### What just happened under the hood?[¶](#what-just-happened-under-the-hood "Permalink to this heading"){.headerlink}

Scrapy schedules the [`scrapy.Request`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre} objects returned by the
[`start_requests`{.docutils .literal .notranslate}]{.pre} method of the
Spider. Upon receiving a response for each one, it instantiates
[[`Response`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} objects and calls the callback method associated with the
request (in this case, the [`parse`{.docutils .literal
.notranslate}]{.pre} method) passing the response as argument.
:::
:::

::: {#a-shortcut-to-the-start-requests-method .section}
##### A shortcut to the start_requests method[¶](#a-shortcut-to-the-start-requests-method "Permalink to this heading"){.headerlink}

Instead of implementing a [[`start_requests()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
.internal} method that generates [`scrapy.Request`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre} objects from URLs, you can just
define a [[`start_urls`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.start_urls "scrapy.Spider.start_urls"){.reference
.internal} class attribute with a list of URLs. This list will then be
used by the default implementation of [[`start_requests()`{.xref .py
.py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
.internal} to create the initial requests for your spider.

::: {.highlight-python .notranslate}
::: highlight
    from pathlib import Path

    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"
        start_urls = [
            "https://quotes.toscrape.com/page/1/",
            "https://quotes.toscrape.com/page/2/",
        ]

        def parse(self, response):
            page = response.url.split("/")[-2]
            filename = f"quotes-{page}.html"
            Path(filename).write_bytes(response.body)
:::
:::

The [[`parse()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
.internal} method will be called to handle each of the requests for
those URLs, even though we haven't explicitly told Scrapy to do so. This
happens because [[`parse()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
.internal} is Scrapy's default callback method, which is called for
requests without an explicitly assigned callback.
:::

::: {#extracting-data .section}
##### Extracting data[¶](#extracting-data "Permalink to this heading"){.headerlink}

The best way to learn how to extract data with Scrapy is trying
selectors using the [[Scrapy shell]{.std
.std-ref}](index.html#topics-shell){.hoverxref .tooltip .reference
.internal}. Run:

::: {.highlight-default .notranslate}
::: highlight
    scrapy shell 'https://quotes.toscrape.com/page/1/'
:::
:::

::: {.admonition .note}
Note

Remember to always enclose urls in quotes when running Scrapy shell from
command-line, otherwise urls containing arguments (i.e. [`&`{.docutils
.literal .notranslate}]{.pre} character) will not work.

On Windows, use double quotes instead:

::: {.highlight-default .notranslate}
::: highlight
    scrapy shell "https://quotes.toscrape.com/page/1/"
:::
:::
:::

You will see something like:

::: {.highlight-default .notranslate}
::: highlight
    [ ... Scrapy log here ... ]
    2016-09-19 12:09:27 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://quotes.toscrape.com/page/1/> (referer: None)
    [s] Available Scrapy objects:
    [s]   scrapy     scrapy module (contains scrapy.Request, scrapy.Selector, etc)
    [s]   crawler    <scrapy.crawler.Crawler object at 0x7fa91d888c90>
    [s]   item       {}
    [s]   request    <GET https://quotes.toscrape.com/page/1/>
    [s]   response   <200 https://quotes.toscrape.com/page/1/>
    [s]   settings   <scrapy.settings.Settings object at 0x7fa91d888c10>
    [s]   spider     <DefaultSpider 'default' at 0x7fa91c8af990>
    [s] Useful shortcuts:
    [s]   shelp()           Shell help (print this help)
    [s]   fetch(req_or_url) Fetch request (or URL) and update local objects
    [s]   view(response)    View response in a browser
:::
:::

Using the shell, you can try selecting elements using
[CSS](https://www.w3.org/TR/selectors){.reference .external} with the
response object:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title")
    [<Selector query='descendant-or-self::title' data='<title>Quotes to Scrape</title>'>]
:::
:::

The result of running [`response.css('title')`{.docutils .literal
.notranslate}]{.pre} is a list-like object called [[`SelectorList`{.xref
.py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
.internal}, which represents a list of [`Selector`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre} objects that wrap around
XML/HTML elements and allow you to run further queries to fine-grain the
selection or extract the data.

To extract the text from the title above, you can do:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title::text").getall()
    ['Quotes to Scrape']
:::
:::

There are two things to note here: one is that we've added
[`::text`{.docutils .literal .notranslate}]{.pre} to the CSS query, to
mean we want to select only the text elements directly inside
[`<title>`{.docutils .literal .notranslate}]{.pre} element. If we don't
specify [`::text`{.docutils .literal .notranslate}]{.pre}, we'd get the
full title element, including its tags:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title").getall()
    ['<title>Quotes to Scrape</title>']
:::
:::

The other thing is that the result of calling [`.getall()`{.docutils
.literal .notranslate}]{.pre} is a list: it is possible that a selector
returns more than one result, so we extract them all. When you know you
just want the first result, as in this case, you can do:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title::text").get()
    'Quotes to Scrape'
:::
:::

As an alternative, you could've written:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title::text")[0].get()
    'Quotes to Scrape'
:::
:::

Accessing an index on a [[`SelectorList`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
.internal} instance will raise an [[`IndexError`{.xref .py .py-exc
.docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#IndexError "(in Python v3.12)"){.reference
.external} exception if there are no results:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("noelement")[0].get()
    Traceback (most recent call last):
    ...
    IndexError: list index out of range
:::
:::

You might want to use [`.get()`{.docutils .literal .notranslate}]{.pre}
directly on the [[`SelectorList`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
.internal} instance instead, which returns [`None`{.docutils .literal
.notranslate}]{.pre} if there are no results:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("noelement").get()
:::
:::

There's a lesson here: for most scraping code, you want it to be
resilient to errors due to things not being found on a page, so that
even if some parts fail to be scraped, you can at least get **some**
data.

Besides the [[`getall()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.selector.SelectorList.getall "scrapy.selector.SelectorList.getall"){.reference
.internal} and [[`get()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.selector.SelectorList.get "scrapy.selector.SelectorList.get"){.reference
.internal} methods, you can also use the [[`re()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.selector.SelectorList.re "scrapy.selector.SelectorList.re"){.reference
.internal} method to extract using [[regular expressions]{.xref .std
.std-doc}](https://docs.python.org/3/library/re.html "(in Python v3.12)"){.reference
.external}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title::text").re(r"Quotes.*")
    ['Quotes to Scrape']
    >>> response.css("title::text").re(r"Q\w+")
    ['Quotes']
    >>> response.css("title::text").re(r"(\w+) to (\w+)")
    ['Quotes', 'Scrape']
:::
:::

In order to find the proper CSS selectors to use, you might find it
useful to open the response page from the shell in your web browser
using [`view(response)`{.docutils .literal .notranslate}]{.pre}. You can
use your browser's developer tools to inspect the HTML and come up with
a selector (see [[Using your browser's Developer Tools for
scraping]{.std .std-ref}](index.html#topics-developer-tools){.hoverxref
.tooltip .reference .internal}).

[Selector Gadget](https://selectorgadget.com/){.reference .external} is
also a nice tool to quickly find CSS selector for visually selected
elements, which works in many browsers.

::: {#xpath-a-brief-intro .section}
###### XPath: a brief intro[¶](#xpath-a-brief-intro "Permalink to this heading"){.headerlink}

Besides [CSS](https://www.w3.org/TR/selectors){.reference .external},
Scrapy selectors also support using
[XPath](https://www.w3.org/TR/xpath/all/){.reference .external}
expressions:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//title")
    [<Selector query='//title' data='<title>Quotes to Scrape</title>'>]
    >>> response.xpath("//title/text()").get()
    'Quotes to Scrape'
:::
:::

XPath expressions are very powerful, and are the foundation of Scrapy
Selectors. In fact, CSS selectors are converted to XPath under-the-hood.
You can see that if you read closely the text representation of the
selector objects in the shell.

While perhaps not as popular as CSS selectors, XPath expressions offer
more power because besides navigating the structure, it can also look at
the content. Using XPath, you're able to select things like: *select the
link that contains the text "Next Page"*. This makes XPath very fitting
to the task of scraping, and we encourage you to learn XPath even if you
already know how to construct CSS selectors, it will make scraping much
easier.

We won't cover much of XPath here, but you can read more about [[using
XPath with Scrapy Selectors here]{.std
.std-ref}](index.html#topics-selectors){.hoverxref .tooltip .reference
.internal}. To learn more about XPath, we recommend [this tutorial to
learn XPath through
examples](http://zvon.org/comp/r/tut-XPath_1.html){.reference
.external}, and [this tutorial to learn "how to think in
XPath"](http://plasmasturm.org/log/xpath101/){.reference .external}.
:::

::: {#extracting-quotes-and-authors .section}
###### Extracting quotes and authors[¶](#extracting-quotes-and-authors "Permalink to this heading"){.headerlink}

Now that you know a bit about selection and extraction, let's complete
our spider by writing the code to extract the quotes from the web page.

Each quote in
[https://quotes.toscrape.com](https://quotes.toscrape.com){.reference
.external} is represented by HTML elements that look like this:

::: {.highlight-html .notranslate}
::: highlight
    <div class="quote">
        <span class="text">“The world as we have created it is a process of our
        thinking. It cannot be changed without changing our thinking.”</span>
        <span>
            by <small class="author">Albert Einstein</small>
            <a href="/author/Albert-Einstein">(about)</a>
        </span>
        <div class="tags">
            Tags:
            <a class="tag" href="/tag/change/page/1/">change</a>
            <a class="tag" href="/tag/deep-thoughts/page/1/">deep-thoughts</a>
            <a class="tag" href="/tag/thinking/page/1/">thinking</a>
            <a class="tag" href="/tag/world/page/1/">world</a>
        </div>
    </div>
:::
:::

Let's open up scrapy shell and play a bit to find out how to extract the
data we want:

::: {.highlight-default .notranslate}
::: highlight
    scrapy shell 'https://quotes.toscrape.com'
:::
:::

We get a list of selectors for the quote HTML elements with:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("div.quote")
    [<Selector query="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' quote ')]" data='<div class="quote" itemscope itemtype...'>,
    <Selector query="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' quote ')]" data='<div class="quote" itemscope itemtype...'>,
    ...]
:::
:::

Each of the selectors returned by the query above allows us to run
further queries over their sub-elements. Let's assign the first selector
to a variable, so that we can run our CSS selectors directly on a
particular quote:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> quote = response.css("div.quote")[0]
:::
:::

Now, let's extract [`text`{.docutils .literal .notranslate}]{.pre},
[`author`{.docutils .literal .notranslate}]{.pre} and the
[`tags`{.docutils .literal .notranslate}]{.pre} from that quote using
the [`quote`{.docutils .literal .notranslate}]{.pre} object we just
created:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> text = quote.css("span.text::text").get()
    >>> text
    '“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”'
    >>> author = quote.css("small.author::text").get()
    >>> author
    'Albert Einstein'
:::
:::

Given that the tags are a list of strings, we can use the
[`.getall()`{.docutils .literal .notranslate}]{.pre} method to get all
of them:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> tags = quote.css("div.tags a.tag::text").getall()
    >>> tags
    ['change', 'deep-thoughts', 'thinking', 'world']
:::
:::

Having figured out how to extract each bit, we can now iterate over all
the quotes elements and put them together into a Python dictionary:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> for quote in response.css("div.quote"):
    ...     text = quote.css("span.text::text").get()
    ...     author = quote.css("small.author::text").get()
    ...     tags = quote.css("div.tags a.tag::text").getall()
    ...     print(dict(text=text, author=author, tags=tags))
    ...
    {'text': '“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”', 'author': 'Albert Einstein', 'tags': ['change', 'deep-thoughts', 'thinking', 'world']}
    {'text': '“It is our choices, Harry, that show what we truly are, far more than our abilities.”', 'author': 'J.K. Rowling', 'tags': ['abilities', 'choices']}
    ...
:::
:::
:::
:::

::: {#extracting-data-in-our-spider .section}
##### Extracting data in our spider[¶](#extracting-data-in-our-spider "Permalink to this heading"){.headerlink}

Let's get back to our spider. Until now, it doesn't extract any data in
particular, just saves the whole HTML page to a local file. Let's
integrate the extraction logic above into our spider.

A Scrapy spider typically generates many dictionaries containing the
data extracted from the page. To do that, we use the [`yield`{.docutils
.literal .notranslate}]{.pre} Python keyword in the callback, as you can
see below:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"
        start_urls = [
            "https://quotes.toscrape.com/page/1/",
            "https://quotes.toscrape.com/page/2/",
        ]

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {
                    "text": quote.css("span.text::text").get(),
                    "author": quote.css("small.author::text").get(),
                    "tags": quote.css("div.tags a.tag::text").getall(),
                }
:::
:::

To run this spider, exit the scrapy shell by entering:

::: {.highlight-default .notranslate}
::: highlight
    quit()
:::
:::

Then, run:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl quotes
:::
:::

Now, it should output the extracted data with the log:

::: {.highlight-default .notranslate}
::: highlight
    2016-09-19 18:57:19 [scrapy.core.scraper] DEBUG: Scraped from <200 https://quotes.toscrape.com/page/1/>
    {'tags': ['life', 'love'], 'author': 'André Gide', 'text': '“It is better to be hated for what you are than to be loved for what you are not.”'}
    2016-09-19 18:57:19 [scrapy.core.scraper] DEBUG: Scraped from <200 https://quotes.toscrape.com/page/1/>
    {'tags': ['edison', 'failure', 'inspirational', 'paraphrased'], 'author': 'Thomas A. Edison', 'text': "“I have not failed. I've just found 10,000 ways that won't work.”"}
:::
:::
:::
:::

::: {#storing-the-scraped-data .section}
[]{#storing-data}

#### Storing the scraped data[¶](#storing-the-scraped-data "Permalink to this heading"){.headerlink}

The simplest way to store the scraped data is by using [[Feed
exports]{.std .std-ref}](index.html#topics-feed-exports){.hoverxref
.tooltip .reference .internal}, with the following command:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl quotes -O quotes.json
:::
:::

That will generate a [`quotes.json`{.docutils .literal
.notranslate}]{.pre} file containing all scraped items, serialized in
[JSON](https://en.wikipedia.org/wiki/JSON){.reference .external}.

The [`-O`{.docutils .literal .notranslate}]{.pre} command-line switch
overwrites any existing file; use [`-o`{.docutils .literal
.notranslate}]{.pre} instead to append new content to any existing file.
However, appending to a JSON file makes the file contents invalid JSON.
When appending to a file, consider using a different serialization
format, such as [JSON Lines](http://jsonlines.org){.reference
.external}:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl quotes -o quotes.jsonl
:::
:::

The [JSON Lines](http://jsonlines.org){.reference .external} format is
useful because it's stream-like, you can easily append new records to
it. It doesn't have the same problem of JSON when you run twice. Also,
as each record is a separate line, you can process big files without
having to fit everything in memory, there are tools like
[JQ](https://stedolan.github.io/jq){.reference .external} to help do
that at the command-line.

In small projects (like the one in this tutorial), that should be
enough. However, if you want to perform more complex things with the
scraped items, you can write an [[Item Pipeline]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal}. A placeholder file for Item Pipelines has been
set up for you when the project is created, in
[`tutorial/pipelines.py`{.docutils .literal .notranslate}]{.pre}. Though
you don't need to implement any item pipelines if you just want to store
the scraped items.
:::

::: {#following-links .section}
#### Following links[¶](#following-links "Permalink to this heading"){.headerlink}

Let's say, instead of just scraping the stuff from the first two pages
from
[https://quotes.toscrape.com](https://quotes.toscrape.com){.reference
.external}, you want quotes from all the pages in the website.

Now that you know how to extract data from pages, let's see how to
follow links from them.

First thing is to extract the link to the page we want to follow.
Examining our page, we can see there is a link to the next page with the
following markup:

::: {.highlight-html .notranslate}
::: highlight
    <ul class="pager">
        <li class="next">
            <a href="/page/2/">Next <span aria-hidden="true">&rarr;</span></a>
        </li>
    </ul>
:::
:::

We can try extracting it in the shell:

::: {.doctest .highlight-default .notranslate}
::: highlight
    >>> response.css('li.next a').get()
    '<a href="/page/2/">Next <span aria-hidden="true">→</span></a>'
:::
:::

This gets the anchor element, but we want the attribute
[`href`{.docutils .literal .notranslate}]{.pre}. For that, Scrapy
supports a CSS extension that lets you select the attribute contents,
like this:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("li.next a::attr(href)").get()
    '/page/2/'
:::
:::

There is also an [`attrib`{.docutils .literal .notranslate}]{.pre}
property available (see [[Selecting element attributes]{.std
.std-ref}](index.html#selecting-attributes){.hoverxref .tooltip
.reference .internal} for more):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("li.next a").attrib["href"]
    '/page/2/'
:::
:::

Let's see now our spider modified to recursively follow the link to the
next page, extracting data from it:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"
        start_urls = [
            "https://quotes.toscrape.com/page/1/",
        ]

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {
                    "text": quote.css("span.text::text").get(),
                    "author": quote.css("small.author::text").get(),
                    "tags": quote.css("div.tags a.tag::text").getall(),
                }

            next_page = response.css("li.next a::attr(href)").get()
            if next_page is not None:
                next_page = response.urljoin(next_page)
                yield scrapy.Request(next_page, callback=self.parse)
:::
:::

Now, after extracting the data, the [`parse()`{.docutils .literal
.notranslate}]{.pre} method looks for the link to the next page, builds
a full absolute URL using the [[`urljoin()`{.xref .py .py-meth .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.http.Response.urljoin "scrapy.http.Response.urljoin"){.reference
.internal} method (since the links can be relative) and yields a new
request to the next page, registering itself as callback to handle the
data extraction for the next page and to keep the crawling going through
all the pages.

What you see here is Scrapy's mechanism of following links: when you
yield a Request in a callback method, Scrapy will schedule that request
to be sent and register a callback method to be executed when that
request finishes.

Using this, you can build complex crawlers that follow links according
to rules you define, and extract different kinds of data depending on
the page it's visiting.

In our example, it creates a sort of loop, following all the links to
the next page until it doesn't find one -- handy for crawling blogs,
forums and other sites with pagination.

::: {#a-shortcut-for-creating-requests .section}
[]{#response-follow-example}

##### A shortcut for creating Requests[¶](#a-shortcut-for-creating-requests "Permalink to this heading"){.headerlink}

As a shortcut for creating Request objects you can use
[[`response.follow`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.TextResponse.follow "scrapy.http.TextResponse.follow"){.reference
.internal}:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"
        start_urls = [
            "https://quotes.toscrape.com/page/1/",
        ]

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {
                    "text": quote.css("span.text::text").get(),
                    "author": quote.css("span small::text").get(),
                    "tags": quote.css("div.tags a.tag::text").getall(),
                }

            next_page = response.css("li.next a::attr(href)").get()
            if next_page is not None:
                yield response.follow(next_page, callback=self.parse)
:::
:::

Unlike scrapy.Request, [`response.follow`{.docutils .literal
.notranslate}]{.pre} supports relative URLs directly - no need to call
urljoin. Note that [`response.follow`{.docutils .literal
.notranslate}]{.pre} just returns a Request instance; you still have to
yield this Request.

You can also pass a selector to [`response.follow`{.docutils .literal
.notranslate}]{.pre} instead of a string; this selector should extract
necessary attributes:

::: {.highlight-python .notranslate}
::: highlight
    for href in response.css("ul.pager a::attr(href)"):
        yield response.follow(href, callback=self.parse)
:::
:::

For [`<a>`{.docutils .literal .notranslate}]{.pre} elements there is a
shortcut: [`response.follow`{.docutils .literal .notranslate}]{.pre}
uses their href attribute automatically. So the code can be shortened
further:

::: {.highlight-python .notranslate}
::: highlight
    for a in response.css("ul.pager a"):
        yield response.follow(a, callback=self.parse)
:::
:::

To create multiple requests from an iterable, you can use
[[`response.follow_all`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.TextResponse.follow_all "scrapy.http.TextResponse.follow_all"){.reference
.internal} instead:

::: {.highlight-python .notranslate}
::: highlight
    anchors = response.css("ul.pager a")
    yield from response.follow_all(anchors, callback=self.parse)
:::
:::

or, shortening it further:

::: {.highlight-python .notranslate}
::: highlight
    yield from response.follow_all(css="ul.pager a", callback=self.parse)
:::
:::
:::

::: {#more-examples-and-patterns .section}
##### More examples and patterns[¶](#more-examples-and-patterns "Permalink to this heading"){.headerlink}

Here is another spider that illustrates callbacks and following links,
this time for scraping author information:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class AuthorSpider(scrapy.Spider):
        name = "author"

        start_urls = ["https://quotes.toscrape.com/"]

        def parse(self, response):
            author_page_links = response.css(".author + a")
            yield from response.follow_all(author_page_links, self.parse_author)

            pagination_links = response.css("li.next a")
            yield from response.follow_all(pagination_links, self.parse)

        def parse_author(self, response):
            def extract_with_css(query):
                return response.css(query).get(default="").strip()

            yield {
                "name": extract_with_css("h3.author-title::text"),
                "birthdate": extract_with_css(".author-born-date::text"),
                "bio": extract_with_css(".author-description::text"),
            }
:::
:::

This spider will start from the main page, it will follow all the links
to the authors pages calling the [`parse_author`{.docutils .literal
.notranslate}]{.pre} callback for each of them, and also the pagination
links with the [`parse`{.docutils .literal .notranslate}]{.pre} callback
as we saw before.

Here we're passing callbacks to [[`response.follow_all`{.xref .py
.py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.TextResponse.follow_all "scrapy.http.TextResponse.follow_all"){.reference
.internal} as positional arguments to make the code shorter; it also
works for [`Request`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}.

The [`parse_author`{.docutils .literal .notranslate}]{.pre} callback
defines a helper function to extract and cleanup the data from a CSS
query and yields the Python dict with the author data.

Another interesting thing this spider demonstrates is that, even if
there are many quotes from the same author, we don't need to worry about
visiting the same author page multiple times. By default, Scrapy filters
out duplicated requests to URLs already visited, avoiding the problem of
hitting servers too much because of a programming mistake. This can be
configured by the setting [[`DUPEFILTER_CLASS`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DUPEFILTER_CLASS){.hoverxref
.tooltip .reference .internal}.

Hopefully by now you have a good understanding of how to use the
mechanism of following links and callbacks with Scrapy.

As yet another example spider that leverages the mechanism of following
links, check out the [[`CrawlSpider`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.spiders.CrawlSpider "scrapy.spiders.CrawlSpider"){.reference
.internal} class for a generic spider that implements a small rules
engine that you can use to write your crawlers on top of it.

Also, a common pattern is to build an item with data from more than one
page, using a [[trick to pass additional data to the callbacks]{.std
.std-ref}](index.html#topics-request-response-ref-request-callback-arguments){.hoverxref
.tooltip .reference .internal}.
:::
:::

::: {#using-spider-arguments .section}
#### Using spider arguments[¶](#using-spider-arguments "Permalink to this heading"){.headerlink}

You can provide command line arguments to your spiders by using the
[`-a`{.docutils .literal .notranslate}]{.pre} option when running them:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl quotes -O quotes-humor.json -a tag=humor
:::
:::

These arguments are passed to the Spider's [`__init__`{.docutils
.literal .notranslate}]{.pre} method and become spider attributes by
default.

In this example, the value provided for the [`tag`{.docutils .literal
.notranslate}]{.pre} argument will be available via
[`self.tag`{.docutils .literal .notranslate}]{.pre}. You can use this to
make your spider fetch only quotes with a specific tag, building the URL
based on the argument:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"

        def start_requests(self):
            url = "https://quotes.toscrape.com/"
            tag = getattr(self, "tag", None)
            if tag is not None:
                url = url + "tag/" + tag
            yield scrapy.Request(url, self.parse)

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {
                    "text": quote.css("span.text::text").get(),
                    "author": quote.css("small.author::text").get(),
                }

            next_page = response.css("li.next a::attr(href)").get()
            if next_page is not None:
                yield response.follow(next_page, self.parse)
:::
:::

If you pass the [`tag=humor`{.docutils .literal .notranslate}]{.pre}
argument to this spider, you'll notice that it will only visit URLs from
the [`humor`{.docutils .literal .notranslate}]{.pre} tag, such as
[`https://quotes.toscrape.com/tag/humor`{.docutils .literal
.notranslate}]{.pre}.

You can [[learn more about handling spider arguments here]{.std
.std-ref}](index.html#spiderargs){.hoverxref .tooltip .reference
.internal}.
:::

::: {#next-steps .section}
#### Next steps[¶](#next-steps "Permalink to this heading"){.headerlink}

This tutorial covered only the basics of Scrapy, but there's a lot of
other features not mentioned here. Check the [[What else?]{.std
.std-ref}](index.html#topics-whatelse){.hoverxref .tooltip .reference
.internal} section in [[Scrapy at a glance]{.std
.std-ref}](index.html#intro-overview){.hoverxref .tooltip .reference
.internal} chapter for a quick overview of the most important ones.

You can continue from the section [[Basic concepts]{.std
.std-ref}](index.html#section-basics){.hoverxref .tooltip .reference
.internal} to know more about the command-line tool, spiders, selectors
and other things the tutorial hasn't covered like modeling the scraped
data. If you prefer to play with an example project, check the
[[Examples]{.std .std-ref}](index.html#intro-examples){.hoverxref
.tooltip .reference .internal} section.
:::
:::

[]{#document-intro/examples}

::: {#examples .section}
[]{#intro-examples}

### Examples[¶](#examples "Permalink to this heading"){.headerlink}

The best way to learn is with examples, and Scrapy is no exception. For
this reason, there is an example Scrapy project named
[quotesbot](https://github.com/scrapy/quotesbot){.reference .external},
that you can use to play and learn more about Scrapy. It contains two
spiders for
[https://quotes.toscrape.com](https://quotes.toscrape.com){.reference
.external}, one using CSS selectors and another one using XPath
expressions.

The [quotesbot](https://github.com/scrapy/quotesbot){.reference
.external} project is available at:
[https://github.com/scrapy/quotesbot](https://github.com/scrapy/quotesbot){.reference
.external}. You can find more information about it in the project's
README.

If you're familiar with git, you can checkout the code. Otherwise you
can download the project as a zip file by clicking
[here](https://github.com/scrapy/quotesbot/archive/master.zip){.reference
.external}.
:::
:::

[[Scrapy at a glance]{.doc}](index.html#document-intro/overview){.reference .internal}

:   Understand what Scrapy is and how it can help you.

[[Installation guide]{.doc}](index.html#document-intro/install){.reference .internal}

:   Get Scrapy installed on your computer.

[[Scrapy Tutorial]{.doc}](index.html#document-intro/tutorial){.reference .internal}

:   Write your first Scrapy project.

[[Examples]{.doc}](index.html#document-intro/examples){.reference .internal}

:   Learn more by playing with a pre-made Scrapy project.
:::

::: {#basic-concepts .section}
[]{#section-basics}

## Basic concepts[¶](#basic-concepts "Permalink to this heading"){.headerlink}

::: {.toctree-wrapper .compound}
[]{#document-topics/commands}

::: {#command-line-tool .section}
[]{#topics-commands}

### Command line tool[¶](#command-line-tool "Permalink to this heading"){.headerlink}

Scrapy is controlled through the [`scrapy`{.docutils .literal
.notranslate}]{.pre} command-line tool, to be referred here as the
"Scrapy tool" to differentiate it from the sub-commands, which we just
call "commands" or "Scrapy commands".

The Scrapy tool provides several commands, for multiple purposes, and
each one accepts a different set of arguments and options.

(The [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`deploy`{.docutils .literal .notranslate}]{.pre}
command has been removed in 1.0 in favor of the standalone
[`scrapyd-deploy`{.docutils .literal .notranslate}]{.pre}. See
[Deploying your
project](https://scrapyd.readthedocs.io/en/latest/deploy.html){.reference
.external}.)

::: {#configuration-settings .section}
[]{#topics-config-settings}

#### Configuration settings[¶](#configuration-settings "Permalink to this heading"){.headerlink}

Scrapy will look for configuration parameters in ini-style
[`scrapy.cfg`{.docutils .literal .notranslate}]{.pre} files in standard
locations:

1.  [`/etc/scrapy.cfg`{.docutils .literal .notranslate}]{.pre} or
    [`c:\scrapy\scrapy.cfg`{.docutils .literal .notranslate}]{.pre}
    (system-wide),

2.  [`~/.config/scrapy.cfg`{.docutils .literal .notranslate}]{.pre}
    ([`$XDG_CONFIG_HOME`{.docutils .literal .notranslate}]{.pre}) and
    [`~/.scrapy.cfg`{.docutils .literal .notranslate}]{.pre}
    ([`$HOME`{.docutils .literal .notranslate}]{.pre}) for global
    (user-wide) settings, and

3.  [`scrapy.cfg`{.docutils .literal .notranslate}]{.pre} inside a
    Scrapy project's root (see next section).

Settings from these files are merged in the listed order of preference:
user-defined values have higher priority than system-wide defaults and
project-wide settings will override all others, when defined.

Scrapy also understands, and can be configured through, a number of
environment variables. Currently these are:

-   [`SCRAPY_SETTINGS_MODULE`{.docutils .literal .notranslate}]{.pre}
    (see [[Designating the settings]{.std
    .std-ref}](index.html#topics-settings-module-envvar){.hoverxref
    .tooltip .reference .internal})

-   [`SCRAPY_PROJECT`{.docutils .literal .notranslate}]{.pre} (see
    [[Sharing the root directory between projects]{.std
    .std-ref}](#topics-project-envvar){.hoverxref .tooltip .reference
    .internal})

-   [`SCRAPY_PYTHON_SHELL`{.docutils .literal .notranslate}]{.pre} (see
    [[Scrapy shell]{.std .std-ref}](index.html#topics-shell){.hoverxref
    .tooltip .reference .internal})
:::

::: {#default-structure-of-scrapy-projects .section}
[]{#topics-project-structure}

#### Default structure of Scrapy projects[¶](#default-structure-of-scrapy-projects "Permalink to this heading"){.headerlink}

Before delving into the command-line tool and its sub-commands, let's
first understand the directory structure of a Scrapy project.

Though it can be modified, all Scrapy projects have the same file
structure by default, similar to this:

::: {.highlight-none .notranslate}
::: highlight
    scrapy.cfg
    myproject/
        __init__.py
        items.py
        middlewares.py
        pipelines.py
        settings.py
        spiders/
            __init__.py
            spider1.py
            spider2.py
            ...
:::
:::

The directory where the [`scrapy.cfg`{.docutils .literal
.notranslate}]{.pre} file resides is known as the *project root
directory*. That file contains the name of the python module that
defines the project settings. Here is an example:

::: {.highlight-ini .notranslate}
::: highlight
    [settings]
    default = myproject.settings
:::
:::
:::

::: {#sharing-the-root-directory-between-projects .section}
[]{#topics-project-envvar}

#### Sharing the root directory between projects[¶](#sharing-the-root-directory-between-projects "Permalink to this heading"){.headerlink}

A project root directory, the one that contains the
[`scrapy.cfg`{.docutils .literal .notranslate}]{.pre}, may be shared by
multiple Scrapy projects, each with its own settings module.

In that case, you must define one or more aliases for those settings
modules under [`[settings]`{.docutils .literal .notranslate}]{.pre} in
your [`scrapy.cfg`{.docutils .literal .notranslate}]{.pre} file:

::: {.highlight-ini .notranslate}
::: highlight
    [settings]
    default = myproject1.settings
    project1 = myproject1.settings
    project2 = myproject2.settings
:::
:::

By default, the [`scrapy`{.docutils .literal .notranslate}]{.pre}
command-line tool will use the [`default`{.docutils .literal
.notranslate}]{.pre} settings. Use the [`SCRAPY_PROJECT`{.docutils
.literal .notranslate}]{.pre} environment variable to specify a
different project for [`scrapy`{.docutils .literal .notranslate}]{.pre}
to use:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy settings --get BOT_NAME
    Project 1 Bot
    $ export SCRAPY_PROJECT=project2
    $ scrapy settings --get BOT_NAME
    Project 2 Bot
:::
:::
:::

::: {#using-the-scrapy-tool .section}
#### Using the [`scrapy`{.docutils .literal .notranslate}]{.pre} tool[¶](#using-the-scrapy-tool "Permalink to this heading"){.headerlink}

You can start by running the Scrapy tool with no arguments and it will
print some usage help and the available commands:

::: {.highlight-none .notranslate}
::: highlight
    Scrapy X.Y - no active project

    Usage:
      scrapy <command> [options] [args]

    Available commands:
      crawl         Run a spider
      fetch         Fetch a URL using the Scrapy downloader
    [...]
:::
:::

The first line will print the currently active project if you're inside
a Scrapy project. In this example it was run from outside a project. If
run from inside a project it would have printed something like this:

::: {.highlight-none .notranslate}
::: highlight
    Scrapy X.Y - project: myproject

    Usage:
      scrapy <command> [options] [args]

    [...]
:::
:::

::: {#creating-projects .section}
##### Creating projects[¶](#creating-projects "Permalink to this heading"){.headerlink}

The first thing you typically do with the [`scrapy`{.docutils .literal
.notranslate}]{.pre} tool is create your Scrapy project:

::: {.highlight-none .notranslate}
::: highlight
    scrapy startproject myproject [project_dir]
:::
:::

That will create a Scrapy project under the [`project_dir`{.docutils
.literal .notranslate}]{.pre} directory. If [`project_dir`{.docutils
.literal .notranslate}]{.pre} wasn't specified, [`project_dir`{.docutils
.literal .notranslate}]{.pre} will be the same as [`myproject`{.docutils
.literal .notranslate}]{.pre}.

Next, you go inside the new project directory:

::: {.highlight-none .notranslate}
::: highlight
    cd project_dir
:::
:::

And you're ready to use the [`scrapy`{.docutils .literal
.notranslate}]{.pre} command to manage and control your project from
there.
:::

::: {#controlling-projects .section}
##### Controlling projects[¶](#controlling-projects "Permalink to this heading"){.headerlink}

You use the [`scrapy`{.docutils .literal .notranslate}]{.pre} tool from
inside your projects to control and manage them.

For example, to create a new spider:

::: {.highlight-none .notranslate}
::: highlight
    scrapy genspider mydomain mydomain.com
:::
:::

Some Scrapy commands (like [[`crawl`{.xref .std .std-command .docutils
.literal .notranslate}]{.pre}](#std-command-crawl){.hoverxref .tooltip
.reference .internal}) must be run from inside a Scrapy project. See the
[[commands reference]{.std .std-ref}](#topics-commands-ref){.hoverxref
.tooltip .reference .internal} below for more information on which
commands must be run from inside projects, and which not.

Also keep in mind that some commands may have slightly different
behaviours when running them from inside projects. For example, the
fetch command will use spider-overridden behaviours (such as the
[`user_agent`{.docutils .literal .notranslate}]{.pre} attribute to
override the user-agent) if the url being fetched is associated with
some specific spider. This is intentional, as the [`fetch`{.docutils
.literal .notranslate}]{.pre} command is meant to be used to check how
spiders are downloading pages.
:::
:::

::: {#available-tool-commands .section}
[]{#topics-commands-ref}

#### Available tool commands[¶](#available-tool-commands "Permalink to this heading"){.headerlink}

This section contains a list of the available built-in commands with a
description and some usage examples. Remember, you can always get more
info about each command by running:

::: {.highlight-none .notranslate}
::: highlight
    scrapy <command> -h
:::
:::

And you can see all available commands with:

::: {.highlight-none .notranslate}
::: highlight
    scrapy -h
:::
:::

There are two kinds of commands, those that only work from inside a
Scrapy project (Project-specific commands) and those that also work
without an active Scrapy project (Global commands), though they may
behave slightly different when running from inside a project (as they
would use the project overridden settings).

Global commands:

-   [[`startproject`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-startproject){.hoverxref .tooltip
    .reference .internal}

-   [[`genspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-genspider){.hoverxref .tooltip
    .reference .internal}

-   [[`settings`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-settings){.hoverxref .tooltip
    .reference .internal}

-   [[`runspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-runspider){.hoverxref .tooltip
    .reference .internal}

-   [[`shell`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-shell){.hoverxref .tooltip
    .reference .internal}

-   [[`fetch`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-fetch){.hoverxref .tooltip
    .reference .internal}

-   [[`view`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-view){.hoverxref .tooltip
    .reference .internal}

-   [[`version`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-version){.hoverxref .tooltip
    .reference .internal}

Project-only commands:

-   [[`crawl`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-crawl){.hoverxref .tooltip
    .reference .internal}

-   [[`check`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-check){.hoverxref .tooltip
    .reference .internal}

-   [[`list`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-list){.hoverxref .tooltip
    .reference .internal}

-   [[`edit`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-edit){.hoverxref .tooltip
    .reference .internal}

-   [[`parse`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-parse){.hoverxref .tooltip
    .reference .internal}

-   [[`bench`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](#std-command-bench){.hoverxref .tooltip
    .reference .internal}

::: {#startproject .section}
[]{#std-command-startproject}

##### startproject[¶](#startproject "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`startproject`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<project_name>`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`[project_dir]`{.docutils .literal
    .notranslate}]{.pre}

-   Requires project: *no*

Creates a new Scrapy project named [`project_name`{.docutils .literal
.notranslate}]{.pre}, under the [`project_dir`{.docutils .literal
.notranslate}]{.pre} directory. If [`project_dir`{.docutils .literal
.notranslate}]{.pre} wasn't specified, [`project_dir`{.docutils .literal
.notranslate}]{.pre} will be the same as [`project_name`{.docutils
.literal .notranslate}]{.pre}.

Usage example:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy startproject myproject
:::
:::
:::

::: {#genspider .section}
[]{#std-command-genspider}

##### genspider[¶](#genspider "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`genspider`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`[-t`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`template]`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<name>`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<domain`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`or`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`URL>`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *no*

::: versionadded
[New in version 2.6.0: ]{.versionmodified .added}The ability to pass a
URL instead of a domain.
:::

Create a new spider in the current folder or in the current project's
[`spiders`{.docutils .literal .notranslate}]{.pre} folder, if called
from inside a project. The [`<name>`{.docutils .literal
.notranslate}]{.pre} parameter is set as the spider's [`name`{.docutils
.literal .notranslate}]{.pre}, while [`<domain`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`or`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`URL>`{.docutils .literal .notranslate}]{.pre} is used to
generate the [`allowed_domains`{.docutils .literal .notranslate}]{.pre}
and [`start_urls`{.docutils .literal .notranslate}]{.pre} spider's
attributes.

Usage example:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy genspider -l
    Available templates:
      basic
      crawl
      csvfeed
      xmlfeed

    $ scrapy genspider example example.com
    Created spider 'example' using template 'basic'

    $ scrapy genspider -t crawl scrapyorg scrapy.org
    Created spider 'scrapyorg' using template 'crawl'
:::
:::

This is just a convenience shortcut command for creating spiders based
on pre-defined templates, but certainly not the only way to create
spiders. You can just create the spider source code files yourself,
instead of using this command.
:::

::: {#crawl .section}
[]{#std-command-crawl}

##### crawl[¶](#crawl "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`crawl`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<spider>`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *yes*

Start crawling using a spider.

Supported options:

-   [`-h,`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`--help`{.docutils .literal .notranslate}]{.pre}: show
    a help message and exit

-   [`-a`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`NAME=VALUE`{.docutils .literal .notranslate}]{.pre}:
    set a spider argument (may be repeated)

-   [`--output`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`FILE`{.docutils .literal
    .notranslate}]{.pre} or [`-o`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`FILE`{.docutils .literal .notranslate}]{.pre}: append
    scraped items to the end of FILE (use - for stdout), to define
    format set a colon at the end of the output URI (i.e.
    [`-o`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`FILE:FORMAT`{.docutils .literal .notranslate}]{.pre})

-   [`--overwrite-output`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`FILE`{.docutils .literal .notranslate}]{.pre} or
    [`-O`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`FILE`{.docutils .literal .notranslate}]{.pre}: dump
    scraped items into FILE, overwriting any existing file, to define
    format set a colon at the end of the output URI (i.e.
    [`-O`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`FILE:FORMAT`{.docutils .literal .notranslate}]{.pre})

-   [`--output-format`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`FORMAT`{.docutils .literal .notranslate}]{.pre} or
    [`-t`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`FORMAT`{.docutils .literal .notranslate}]{.pre}:
    deprecated way to define format to use for dumping items, does not
    work in combination with [`-O`{.docutils .literal
    .notranslate}]{.pre}

Usage examples:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy crawl myspider
    [ ... myspider starts crawling ... ]

    $ scrapy crawl -o myfile:csv myspider
    [ ... myspider starts crawling and appends the result to the file myfile in csv format ... ]

    $ scrapy crawl -O myfile:json myspider
    [ ... myspider starts crawling and saves the result in myfile in json format overwriting the original content... ]

    $ scrapy crawl -o myfile -t csv myspider
    [ ... myspider starts crawling and appends the result to the file myfile in csv format ... ]
:::
:::
:::

::: {#check .section}
[]{#std-command-check}

##### check[¶](#check "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`check`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`[-l]`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<spider>`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *yes*

Run contract checks.

Usage examples:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy check -l
    first_spider
      * parse
      * parse_item
    second_spider
      * parse
      * parse_item

    $ scrapy check
    [FAILED] first_spider:parse_item
    >>> 'RetailPricex' field is missing

    [FAILED] first_spider:parse
    >>> Returned 92 requests, expected 0..4
:::
:::
:::

::: {#list .section}
[]{#std-command-list}

##### list[¶](#list "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`list`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *yes*

List all available spiders in the current project. The output is one
spider per line.

Usage example:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy list
    spider1
    spider2
:::
:::
:::

::: {#edit .section}
[]{#std-command-edit}

##### edit[¶](#edit "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`edit`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<spider>`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *yes*

Edit the given spider using the editor defined in the
[`EDITOR`{.docutils .literal .notranslate}]{.pre} environment variable
or (if unset) the [[`EDITOR`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EDITOR){.hoverxref .tooltip
.reference .internal} setting.

This command is provided only as a convenience shortcut for the most
common case, the developer is of course free to choose any tool or IDE
to write and debug spiders.

Usage example:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy edit spider1
:::
:::
:::

::: {#fetch .section}
[]{#std-command-fetch}

##### fetch[¶](#fetch "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`fetch`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<url>`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *no*

Downloads the given URL using the Scrapy downloader and writes the
contents to standard output.

The interesting thing about this command is that it fetches the page how
the spider would download it. For example, if the spider has a
[`USER_AGENT`{.docutils .literal .notranslate}]{.pre} attribute which
overrides the User Agent, it will use that one.

So this command can be used to "see" how your spider would fetch a
certain page.

If used outside a project, no particular per-spider behaviour would be
applied and it will just use the default Scrapy downloader settings.

Supported options:

-   [`--spider=SPIDER`{.docutils .literal .notranslate}]{.pre}: bypass
    spider autodetection and force use of specific spider

-   [`--headers`{.docutils .literal .notranslate}]{.pre}: print the
    response's HTTP headers instead of the response's body

-   [`--no-redirect`{.docutils .literal .notranslate}]{.pre}: do not
    follow HTTP 3xx redirects (default is to follow them)

Usage examples:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy fetch --nolog http://www.example.com/some/page.html
    [ ... html content here ... ]

    $ scrapy fetch --nolog --headers http://www.example.com/
    {'Accept-Ranges': ['bytes'],
     'Age': ['1263   '],
     'Connection': ['close     '],
     'Content-Length': ['596'],
     'Content-Type': ['text/html; charset=UTF-8'],
     'Date': ['Wed, 18 Aug 2010 23:59:46 GMT'],
     'Etag': ['"573c1-254-48c9c87349680"'],
     'Last-Modified': ['Fri, 30 Jul 2010 15:30:18 GMT'],
     'Server': ['Apache/2.2.3 (CentOS)']}
:::
:::
:::

::: {#view .section}
[]{#std-command-view}

##### view[¶](#view "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`view`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<url>`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *no*

Opens the given URL in a browser, as your Scrapy spider would "see" it.
Sometimes spiders see pages differently from regular users, so this can
be used to check what the spider "sees" and confirm it's what you
expect.

Supported options:

-   [`--spider=SPIDER`{.docutils .literal .notranslate}]{.pre}: bypass
    spider autodetection and force use of specific spider

-   [`--no-redirect`{.docutils .literal .notranslate}]{.pre}: do not
    follow HTTP 3xx redirects (default is to follow them)

Usage example:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy view http://www.example.com/some/page.html
    [ ... browser starts ... ]
:::
:::
:::

::: {#shell .section}
[]{#std-command-shell}

##### shell[¶](#shell "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`shell`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`[url]`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *no*

Starts the Scrapy shell for the given URL (if given) or empty if no URL
is given. Also supports UNIX-style local file paths, either relative
with [`./`{.docutils .literal .notranslate}]{.pre} or [`../`{.docutils
.literal .notranslate}]{.pre} prefixes or absolute file paths. See
[[Scrapy shell]{.std .std-ref}](index.html#topics-shell){.hoverxref
.tooltip .reference .internal} for more info.

Supported options:

-   [`--spider=SPIDER`{.docutils .literal .notranslate}]{.pre}: bypass
    spider autodetection and force use of specific spider

-   [`-c`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`code`{.docutils .literal .notranslate}]{.pre}:
    evaluate the code in the shell, print the result and exit

-   [`--no-redirect`{.docutils .literal .notranslate}]{.pre}: do not
    follow HTTP 3xx redirects (default is to follow them); this only
    affects the URL you may pass as argument on the command line; once
    you are inside the shell, [`fetch(url)`{.docutils .literal
    .notranslate}]{.pre} will still follow HTTP redirects by default.

Usage example:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy shell http://www.example.com/some/page.html
    [ ... scrapy shell starts ... ]

    $ scrapy shell --nolog http://www.example.com/ -c '(response.status, response.url)'
    (200, 'http://www.example.com/')

    # shell follows HTTP redirects by default
    $ scrapy shell --nolog http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F -c '(response.status, response.url)'
    (200, 'http://example.com/')

    # you can disable this with --no-redirect
    # (only for the URL passed as command line argument)
    $ scrapy shell --no-redirect --nolog http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F -c '(response.status, response.url)'
    (302, 'http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F')
:::
:::
:::

::: {#parse .section}
[]{#std-command-parse}

##### parse[¶](#parse "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`parse`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<url>`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`[options]`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *yes*

Fetches the given URL and parses it with the spider that handles it,
using the method passed with the [`--callback`{.docutils .literal
.notranslate}]{.pre} option, or [`parse`{.docutils .literal
.notranslate}]{.pre} if not given.

Supported options:

-   [`--spider=SPIDER`{.docutils .literal .notranslate}]{.pre}: bypass
    spider autodetection and force use of specific spider

-   [`--a`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`NAME=VALUE`{.docutils .literal .notranslate}]{.pre}:
    set spider argument (may be repeated)

-   [`--callback`{.docutils .literal .notranslate}]{.pre} or
    [`-c`{.docutils .literal .notranslate}]{.pre}: spider method to use
    as callback for parsing the response

-   [`--meta`{.docutils .literal .notranslate}]{.pre} or [`-m`{.docutils
    .literal .notranslate}]{.pre}: additional request meta that will be
    passed to the callback request. This must be a valid json string.
    Example: --meta='{"foo" : "bar"}'

-   [`--cbkwargs`{.docutils .literal .notranslate}]{.pre}: additional
    keyword arguments that will be passed to the callback. This must be
    a valid json string. Example: --cbkwargs='{"foo" : "bar"}'

-   [`--pipelines`{.docutils .literal .notranslate}]{.pre}: process
    items through pipelines

-   [`--rules`{.docutils .literal .notranslate}]{.pre} or
    [`-r`{.docutils .literal .notranslate}]{.pre}: use
    [[`CrawlSpider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.CrawlSpider "scrapy.spiders.CrawlSpider"){.reference
    .internal} rules to discover the callback (i.e. spider method) to
    use for parsing the response

-   [`--noitems`{.docutils .literal .notranslate}]{.pre}: don't show
    scraped items

-   [`--nolinks`{.docutils .literal .notranslate}]{.pre}: don't show
    extracted links

-   [`--nocolour`{.docutils .literal .notranslate}]{.pre}: avoid using
    pygments to colorize the output

-   [`--depth`{.docutils .literal .notranslate}]{.pre} or
    [`-d`{.docutils .literal .notranslate}]{.pre}: depth level for which
    the requests should be followed recursively (default: 1)

-   [`--verbose`{.docutils .literal .notranslate}]{.pre} or
    [`-v`{.docutils .literal .notranslate}]{.pre}: display information
    for each depth level

-   [`--output`{.docutils .literal .notranslate}]{.pre} or
    [`-o`{.docutils .literal .notranslate}]{.pre}: dump scraped items to
    a file

    ::: versionadded
    [New in version 2.3.]{.versionmodified .added}
    :::

Usage example:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy parse http://www.example.com/ -c parse_item
    [ ... scrapy log lines crawling example.com spider ... ]

    >>> STATUS DEPTH LEVEL 1 <<<
    # Scraped Items  ------------------------------------------------------------
    [{'name': 'Example item',
     'category': 'Furniture',
     'length': '12 cm'}]

    # Requests  -----------------------------------------------------------------
    []
:::
:::
:::

::: {#settings .section}
[]{#std-command-settings}

##### settings[¶](#settings "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`settings`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`[options]`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *no*

Get the value of a Scrapy setting.

If used inside a project it'll show the project setting value, otherwise
it'll show the default Scrapy value for that setting.

Example usage:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy settings --get BOT_NAME
    scrapybot
    $ scrapy settings --get DOWNLOAD_DELAY
    0
:::
:::
:::

::: {#runspider .section}
[]{#std-command-runspider}

##### runspider[¶](#runspider "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`runspider`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`<spider_file.py>`{.docutils .literal
    .notranslate}]{.pre}

-   Requires project: *no*

Run a spider self-contained in a Python file, without having to create a
project.

Example usage:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy runspider myspider.py
    [ ... spider starts crawling ... ]
:::
:::
:::

::: {#version .section}
[]{#std-command-version}

##### version[¶](#version "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`version`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`[-v]`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *no*

Prints the Scrapy version. If used with [`-v`{.docutils .literal
.notranslate}]{.pre} it also prints Python, Twisted and Platform info,
which is useful for bug reports.
:::

::: {#bench .section}
[]{#std-command-bench}

##### bench[¶](#bench "Permalink to this heading"){.headerlink}

-   Syntax: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`bench`{.docutils .literal .notranslate}]{.pre}

-   Requires project: *no*

Run a quick benchmark test. [[Benchmarking]{.std
.std-ref}](index.html#benchmarking){.hoverxref .tooltip .reference
.internal}.
:::
:::

::: {#custom-project-commands .section}
#### Custom project commands[¶](#custom-project-commands "Permalink to this heading"){.headerlink}

You can also add your custom project commands by using the
[[`COMMANDS_MODULE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-COMMANDS_MODULE){.hoverxref .tooltip
.reference .internal} setting. See the Scrapy commands in
[scrapy/commands](https://github.com/scrapy/scrapy/tree/master/scrapy/commands){.reference
.external} for examples on how to implement your commands.

::: {#commands-module .section}
[]{#std-setting-COMMANDS_MODULE}

##### COMMANDS_MODULE[¶](#commands-module "Permalink to this heading"){.headerlink}

Default: [`''`{.docutils .literal .notranslate}]{.pre} (empty string)

A module to use for looking up custom Scrapy commands. This is used to
add custom commands for your Scrapy project.

Example:

::: {.highlight-python .notranslate}
::: highlight
    COMMANDS_MODULE = "mybot.commands"
:::
:::
:::

::: {#register-commands-via-setup-py-entry-points .section}
##### Register commands via setup.py entry points[¶](#register-commands-via-setup-py-entry-points "Permalink to this heading"){.headerlink}

You can also add Scrapy commands from an external library by adding a
[`scrapy.commands`{.docutils .literal .notranslate}]{.pre} section in
the entry points of the library [`setup.py`{.docutils .literal
.notranslate}]{.pre} file.

The following example adds [`my_command`{.docutils .literal
.notranslate}]{.pre} command:

::: {.highlight-python .notranslate}
::: highlight
    from setuptools import setup, find_packages

    setup(
        name="scrapy-mymodule",
        entry_points={
            "scrapy.commands": [
                "my_command=my_scrapy_module.commands:MyCommand",
            ],
        },
    )
:::
:::
:::
:::
:::

[]{#document-topics/spiders}

::: {#spiders .section}
[]{#topics-spiders}

### Spiders[¶](#spiders "Permalink to this heading"){.headerlink}

Spiders are classes which define how a certain site (or a group of
sites) will be scraped, including how to perform the crawl (i.e. follow
links) and how to extract structured data from their pages (i.e.
scraping items). In other words, Spiders are the place where you define
the custom behaviour for crawling and parsing pages for a particular
site (or, in some cases, a group of sites).

For spiders, the scraping cycle goes through something like this:

1.  You start by generating the initial Requests to crawl the first
    URLs, and specify a callback function to be called with the response
    downloaded from those requests.

    The first requests to perform are obtained by calling the
    [[`start_requests()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
    .internal} method which (by default) generates [`Request`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} for the URLs
    specified in the [[`start_urls`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.Spider.start_urls "scrapy.Spider.start_urls"){.reference
    .internal} and the [[`parse`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
    .internal} method as callback function for the Requests.

2.  In the callback function, you parse the response (web page) and
    return [[item objects]{.std
    .std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
    .internal}, [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} objects, or an iterable of these objects. Those
    Requests will also contain a callback (maybe the same) and will then
    be downloaded by Scrapy and then their response handled by the
    specified callback.

3.  In callback functions, you parse the page contents, typically using
    [[Selectors]{.std .std-ref}](index.html#topics-selectors){.hoverxref
    .tooltip .reference .internal} (but you can also use BeautifulSoup,
    lxml or whatever mechanism you prefer) and generate items with the
    parsed data.

4.  Finally, the items returned from the spider will be typically
    persisted to a database (in some [[Item Pipeline]{.std
    .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
    .reference .internal}) or written to a file using [[Feed
    exports]{.std .std-ref}](index.html#topics-feed-exports){.hoverxref
    .tooltip .reference .internal}.

Even though this cycle applies (more or less) to any kind of spider,
there are different kinds of default spiders bundled into Scrapy for
different purposes. We will talk about those types here.

::: {#scrapy-spider .section}
[]{#topics-spiders-ref}

#### scrapy.Spider[¶](#scrapy-spider "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spiders.]{.pre}]{.sig-prename .descclassname}[[Spider]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.Spider "Permalink to this definition"){.headerlink}

:   

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.]{.pre}]{.sig-prename .descclassname}[[Spider]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider "Permalink to this definition"){.headerlink}

:   This is the simplest spider, and the one from which every other
    spider must inherit (including spiders that come bundled with
    Scrapy, as well as spiders that you write yourself). It doesn't
    provide any special functionality. It just provides a default
    [[`start_requests()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
    .internal} implementation which sends requests from the
    [[`start_urls`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.Spider.start_urls "scrapy.Spider.start_urls"){.reference
    .internal} spider attribute and calls the spider's method
    [`parse`{.docutils .literal .notranslate}]{.pre} for each of the
    resulting responses.

    [[name]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.name "Permalink to this definition"){.headerlink}

    :   A string which defines the name for this spider. The spider name
        is how the spider is located (and instantiated) by Scrapy, so it
        must be unique. However, nothing prevents you from instantiating
        more than one instance of the same spider. This is the most
        important spider attribute and it's required.

        If the spider scrapes a single domain, a common practice is to
        name the spider after the domain, with or without the
        [TLD](https://en.wikipedia.org/wiki/Top-level_domain){.reference
        .external}. So, for example, a spider that crawls
        [`mywebsite.com`{.docutils .literal .notranslate}]{.pre} would
        often be called [`mywebsite`{.docutils .literal
        .notranslate}]{.pre}.

    [[allowed_domains]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.allowed_domains "Permalink to this definition"){.headerlink}

    :   An optional list of strings containing domains that this spider
        is allowed to crawl. Requests for URLs not belonging to the
        domain names specified in this list (or their subdomains) won't
        be followed if [[`OffsiteMiddleware`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.offsite.OffsiteMiddleware "scrapy.spidermiddlewares.offsite.OffsiteMiddleware"){.reference
        .internal} is enabled.

        Let's say your target url is
        [`https://www.example.com/1.html`{.docutils .literal
        .notranslate}]{.pre}, then add [`'example.com'`{.docutils
        .literal .notranslate}]{.pre} to the list.

    [[start_urls]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.start_urls "Permalink to this definition"){.headerlink}

    :   A list of URLs where the spider will begin to crawl from, when
        no particular URLs are specified. So, the first pages downloaded
        will be those listed here. The subsequent [`Request`{.xref .py
        .py-class .docutils .literal .notranslate}]{.pre} will be
        generated successively from data contained in the start URLs.

    [[custom_settings]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.custom_settings "Permalink to this definition"){.headerlink}

    :   A dictionary of settings that will be overridden from the
        project wide configuration when running this spider. It must be
        defined as a class attribute since the settings are updated
        before instantiation.

        For a list of available built-in settings see: [[Built-in
        settings reference]{.std
        .std-ref}](index.html#topics-settings-ref){.hoverxref .tooltip
        .reference .internal}.

    [[crawler]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.crawler "Permalink to this definition"){.headerlink}

    :   This attribute is set by the [[`from_crawler()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](index.html#from_crawler "from_crawler"){.reference
        .internal} class method after initializing the class, and links
        to the [[`Crawler`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} object to which this spider instance is bound.

        Crawlers encapsulate a lot of components in the project for
        their single entry access (such as extensions, middlewares,
        signals managers, etc). See [[Crawler API]{.std
        .std-ref}](index.html#topics-api-crawler){.hoverxref .tooltip
        .reference .internal} to know more about them.

    [[settings]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.settings "Permalink to this definition"){.headerlink}

    :   Configuration for running this spider. This is a
        [[`Settings`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
        .internal} instance, see the [[Settings]{.std
        .std-ref}](index.html#topics-settings){.hoverxref .tooltip
        .reference .internal} topic for a detailed introduction on this
        subject.

    [[logger]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.logger "Permalink to this definition"){.headerlink}

    :   Python logger created with the Spider's [[`name`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.Spider.name "scrapy.Spider.name"){.reference
        .internal}. You can use it to send log messages through it as
        described on [[Logging from Spiders]{.std
        .std-ref}](index.html#topics-logging-from-spiders){.hoverxref
        .tooltip .reference .internal}.

    [[state]{.pre}]{.sig-name .descname}[¶](#scrapy.Spider.state "Permalink to this definition"){.headerlink}

    :   A dict you can use to persist some spider state between batches.
        See [[Keeping persistent state between batches]{.std
        .std-ref}](index.html#topics-keeping-persistent-state-between-batches){.hoverxref
        .tooltip .reference .internal} to know more about it.

    [[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[args]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.Spider.from_crawler "Permalink to this definition"){.headerlink}

    :   This is the class method used by Scrapy to create your spiders.

        You probably won't need to override this directly because the
        default implementation acts as a proxy to the
        [[`__init__()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](index.html#init__ "__init__"){.reference
        .internal} method, calling it with the given arguments
        [`args`{.docutils .literal .notranslate}]{.pre} and named
        arguments [`kwargs`{.docutils .literal .notranslate}]{.pre}.

        Nonetheless, this method sets the [[`crawler`{.xref .py .py-attr
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.Spider.crawler "scrapy.Spider.crawler"){.reference
        .internal} and [[`settings`{.xref .py .py-attr .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.Spider.settings "scrapy.Spider.settings"){.reference
        .internal} attributes in the new instance so they can be
        accessed later inside the spider's code.

        ::: versionchanged
        [Changed in version 2.11: ]{.versionmodified .changed}The
        settings in [`crawler.settings`{.docutils .literal
        .notranslate}]{.pre} can now be modified in this method, which
        is handy if you want to modify them based on arguments. As a
        consequence, these settings aren't the final values as they can
        be modified later by e.g. [[add-ons]{.std
        .std-ref}](index.html#topics-addons){.hoverxref .tooltip
        .reference .internal}. For the same reason, most of the
        [[`Crawler`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} attributes aren't initialized at this point.

        The final settings and the initialized [[`Crawler`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} attributes are available in the
        [[`start_requests()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
        .internal} method, handlers of the [[`engine_started`{.xref .std
        .std-signal .docutils .literal
        .notranslate}]{.pre}](index.html#std-signal-engine_started){.hoverxref
        .tooltip .reference .internal} signal and later.
        :::

        Parameters

        :   -   **crawler** ([[`Crawler`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
                .internal} instance) -- crawler to which the spider will
                be bound

            -   **args**
                ([*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
                .external}) -- arguments passed to the
                [[`__init__()`{.xref .py .py-meth .docutils .literal
                .notranslate}]{.pre}](index.html#init__ "__init__"){.reference
                .internal} method

            -   **kwargs**
                ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
                .external}) -- keyword arguments passed to the
                [[`__init__()`{.xref .py .py-meth .docutils .literal
                .notranslate}]{.pre}](index.html#init__ "__init__"){.reference
                .internal} method

    *[classmethod]{.pre}[ ]{.w}*[[update_settings]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[settings]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.Spider.update_settings "Permalink to this definition"){.headerlink}

    :   The [`update_settings()`{.docutils .literal .notranslate}]{.pre}
        method is used to modify the spider's settings and is called
        during initialization of a spider instance.

        It takes a [[`Settings`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
        .internal} object as a parameter and can add or update the
        spider's configuration values. This method is a class method,
        meaning that it is called on the [[`Spider`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.Spider "scrapy.Spider"){.reference
        .internal} class and allows all instances of the spider to share
        the same configuration.

        While per-spider settings can be set in
        [[`custom_settings`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.Spider.custom_settings "scrapy.Spider.custom_settings"){.reference
        .internal}, using [`update_settings()`{.docutils .literal
        .notranslate}]{.pre} allows you to dynamically add, remove or
        change settings based on other settings, spider attributes or
        other factors and use setting priorities other than
        [`'spider'`{.docutils .literal .notranslate}]{.pre}. Also, it's
        easy to extend [`update_settings()`{.docutils .literal
        .notranslate}]{.pre} in a subclass by overriding it, while doing
        the same with [[`custom_settings`{.xref .py .py-attr .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.Spider.custom_settings "scrapy.Spider.custom_settings"){.reference
        .internal} can be hard.

        For example, suppose a spider needs to modify [[`FEEDS`{.xref
        .std .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
        .tooltip .reference .internal}:

        ::: {.highlight-python .notranslate}
        ::: highlight
            import scrapy


            class MySpider(scrapy.Spider):
                name = "myspider"
                custom_feed = {
                    "/home/user/documents/items.json": {
                        "format": "json",
                        "indent": 4,
                    }
                }

                @classmethod
                def update_settings(cls, settings):
                    super().update_settings(settings)
                    settings.setdefault("FEEDS", {}).update(cls.custom_feed)
        :::
        :::

    [[start_requests]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[¶](#scrapy.Spider.start_requests "Permalink to this definition"){.headerlink}

    :   This method must return an iterable with the first Requests to
        crawl for this spider. It is called by Scrapy when the spider is
        opened for scraping. Scrapy calls it only once, so it is safe to
        implement [[`start_requests()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
        .internal} as a generator.

        The default implementation generates [`Request(url,`{.docutils
        .literal .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`dont_filter=True)`{.docutils .literal
        .notranslate}]{.pre} for each url in [[`start_urls`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.Spider.start_urls "scrapy.Spider.start_urls"){.reference
        .internal}.

        If you want to change the Requests used to start scraping a
        domain, this is the method to override. For example, if you need
        to start by logging in using a POST request, you could do:

        ::: {.highlight-python .notranslate}
        ::: highlight
            import scrapy


            class MySpider(scrapy.Spider):
                name = "myspider"

                def start_requests(self):
                    return [
                        scrapy.FormRequest(
                            "http://www.example.com/login",
                            formdata={"user": "john", "pass": "secret"},
                            callback=self.logged_in,
                        )
                    ]

                def logged_in(self, response):
                    # here you would extract links to follow and return Requests for
                    # each of them, with another callback
                    pass
        :::
        :::

    [[parse]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.Spider.parse "Permalink to this definition"){.headerlink}

    :   This is the default callback used by Scrapy to process
        downloaded responses, when their requests don't specify a
        callback.

        The [`parse`{.docutils .literal .notranslate}]{.pre} method is
        in charge of processing the response and returning scraped data
        and/or more URLs to follow. Other Requests callbacks have the
        same requirements as the [`Spider`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} class.

        This method, as well as any other Request callback, must return
        a [`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre} object, an [[item object]{.std
        .std-ref}](index.html#topics-items){.hoverxref .tooltip
        .reference .internal}, an iterable of [`Request`{.xref .py
        .py-class .docutils .literal .notranslate}]{.pre} objects and/or
        [[item objects]{.std
        .std-ref}](index.html#topics-items){.hoverxref .tooltip
        .reference .internal}, or [`None`{.docutils .literal
        .notranslate}]{.pre}.

        Parameters

        :   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal}) -- the response to parse

    [[log]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[message]{.pre}]{.n}*[\[]{.optional}, *[[level]{.pre}]{.n}*, *[[component]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[¶](#scrapy.Spider.log "Permalink to this definition"){.headerlink}

    :   Wrapper that sends a log message through the Spider's
        [[`logger`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.Spider.logger "scrapy.Spider.logger"){.reference
        .internal}, kept for backward compatibility. For more
        information see [[Logging from Spiders]{.std
        .std-ref}](index.html#topics-logging-from-spiders){.hoverxref
        .tooltip .reference .internal}.

    [[closed]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[reason]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.Spider.closed "Permalink to this definition"){.headerlink}

    :   Called when the spider closes. This method provides a shortcut
        to signals.connect() for the [[`spider_closed`{.xref .std
        .std-signal .docutils .literal
        .notranslate}]{.pre}](index.html#std-signal-spider_closed){.hoverxref
        .tooltip .reference .internal} signal.

Let's see an example:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "example.com"
        allowed_domains = ["example.com"]
        start_urls = [
            "http://www.example.com/1.html",
            "http://www.example.com/2.html",
            "http://www.example.com/3.html",
        ]

        def parse(self, response):
            self.logger.info("A response from %s just arrived!", response.url)
:::
:::

Return multiple Requests and items from a single callback:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "example.com"
        allowed_domains = ["example.com"]
        start_urls = [
            "http://www.example.com/1.html",
            "http://www.example.com/2.html",
            "http://www.example.com/3.html",
        ]

        def parse(self, response):
            for h3 in response.xpath("//h3").getall():
                yield {"title": h3}

            for href in response.xpath("//a/@href").getall():
                yield scrapy.Request(response.urljoin(href), self.parse)
:::
:::

Instead of [[`start_urls`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.Spider.start_urls "scrapy.Spider.start_urls"){.reference
.internal} you can use [[`start_requests()`{.xref .py .py-meth .docutils
.literal
.notranslate}]{.pre}](#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
.internal} directly; to give data more structure you can use
[`Item`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
objects:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from myproject.items import MyItem


    class MySpider(scrapy.Spider):
        name = "example.com"
        allowed_domains = ["example.com"]

        def start_requests(self):
            yield scrapy.Request("http://www.example.com/1.html", self.parse)
            yield scrapy.Request("http://www.example.com/2.html", self.parse)
            yield scrapy.Request("http://www.example.com/3.html", self.parse)

        def parse(self, response):
            for h3 in response.xpath("//h3").getall():
                yield MyItem(title=h3)

            for href in response.xpath("//a/@href").getall():
                yield scrapy.Request(response.urljoin(href), self.parse)
:::
:::
:::

::: {#spider-arguments .section}
[]{#spiderargs}

#### Spider arguments[¶](#spider-arguments "Permalink to this heading"){.headerlink}

Spiders can receive arguments that modify their behaviour. Some common
uses for spider arguments are to define the start URLs or to restrict
the crawl to certain sections of the site, but they can be used to
configure any functionality of the spider.

Spider arguments are passed through the [[`crawl`{.xref .std
.std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref .tooltip
.reference .internal} command using the [`-a`{.docutils .literal
.notranslate}]{.pre} option. For example:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl myspider -a category=electronics
:::
:::

Spiders can access arguments in their \_\_init\_\_ methods:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "myspider"

        def __init__(self, category=None, *args, **kwargs):
            super(MySpider, self).__init__(*args, **kwargs)
            self.start_urls = [f"http://www.example.com/categories/{category}"]
            # ...
:::
:::

The default \_\_init\_\_ method will take any spider arguments and copy
them to the spider as attributes. The above example can also be written
as follows:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "myspider"

        def start_requests(self):
            yield scrapy.Request(f"http://www.example.com/categories/{self.category}")
:::
:::

If you are [[running Scrapy from a script]{.std
.std-ref}](index.html#run-from-script){.hoverxref .tooltip .reference
.internal}, you can specify spider arguments when calling
[[`CrawlerProcess.crawl`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess.crawl "scrapy.crawler.CrawlerProcess.crawl"){.reference
.internal} or [[`CrawlerRunner.crawl`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner.crawl "scrapy.crawler.CrawlerRunner.crawl"){.reference
.internal}:

::: {.highlight-python .notranslate}
::: highlight
    process = CrawlerProcess()
    process.crawl(MySpider, category="electronics")
:::
:::

Keep in mind that spider arguments are only strings. The spider will not
do any parsing on its own. If you were to set the
[`start_urls`{.docutils .literal .notranslate}]{.pre} attribute from the
command line, you would have to parse it on your own into a list using
something like [[`ast.literal_eval()`{.xref .py .py-func .docutils
.literal
.notranslate}]{.pre}](https://docs.python.org/3/library/ast.html#ast.literal_eval "(in Python v3.12)"){.reference
.external} or [[`json.loads()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.loads "(in Python v3.12)"){.reference
.external} and then set it as an attribute. Otherwise, you would cause
iteration over a [`start_urls`{.docutils .literal .notranslate}]{.pre}
string (a very common python pitfall) resulting in each character being
seen as a separate url.

A valid use case is to set the http auth credentials used by
[[`HttpAuthMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware "scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware"){.reference
.internal} or the user agent used by [[`UserAgentMiddleware`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.useragent.UserAgentMiddleware "scrapy.downloadermiddlewares.useragent.UserAgentMiddleware"){.reference
.internal}:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl myspider -a http_user=myuser -a http_pass=mypassword -a user_agent=mybot
:::
:::

Spider arguments can also be passed through the Scrapyd
[`schedule.json`{.docutils .literal .notranslate}]{.pre} API. See
[Scrapyd
documentation](https://scrapyd.readthedocs.io/en/latest/){.reference
.external}.
:::

::: {#generic-spiders .section}
[]{#builtin-spiders}

#### Generic Spiders[¶](#generic-spiders "Permalink to this heading"){.headerlink}

Scrapy comes with some useful generic spiders that you can use to
subclass your spiders from. Their aim is to provide convenient
functionality for a few common scraping cases, like following all links
on a site based on certain rules, crawling from
[Sitemaps](https://www.sitemaps.org/index.html){.reference .external},
or parsing an XML/CSV feed.

For the examples used in the following spiders, we'll assume you have a
project with a [`TestItem`{.docutils .literal .notranslate}]{.pre}
declared in a [`myproject.items`{.docutils .literal .notranslate}]{.pre}
module:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class TestItem(scrapy.Item):
        id = scrapy.Field()
        name = scrapy.Field()
        description = scrapy.Field()
:::
:::

::: {#crawlspider .section}
##### CrawlSpider[¶](#crawlspider "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spiders.]{.pre}]{.sig-prename .descclassname}[[CrawlSpider]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/crawl.html#CrawlSpider){.reference .internal}[¶](#scrapy.spiders.CrawlSpider "Permalink to this definition"){.headerlink}

:   This is the most commonly used spider for crawling regular websites,
    as it provides a convenient mechanism for following links by
    defining a set of rules. It may not be the best suited for your
    particular web sites or project, but it's generic enough for several
    cases, so you can start from it and override it as needed for more
    custom functionality, or just implement your own spider.

    Apart from the attributes inherited from Spider (that you must
    specify), this class supports a new attribute:

    [[rules]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.CrawlSpider.rules "Permalink to this definition"){.headerlink}

    :   Which is a list of one (or more) [[`Rule`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
        .internal} objects. Each [[`Rule`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
        .internal} defines a certain behaviour for crawling the site.
        Rules objects are described below. If multiple rules match the
        same link, the first one will be used, according to the order
        they're defined in this attribute.

    This spider also exposes an overridable method:

    [[parse_start_url]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/crawl.html#CrawlSpider.parse_start_url){.reference .internal}[¶](#scrapy.spiders.CrawlSpider.parse_start_url "Permalink to this definition"){.headerlink}

    :   This method is called for each response produced for the URLs in
        the spider's [`start_urls`{.docutils .literal
        .notranslate}]{.pre} attribute. It allows to parse the initial
        responses and must return either an [[item object]{.std
        .std-ref}](index.html#topics-items){.hoverxref .tooltip
        .reference .internal}, a [`Request`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre} object, or an iterable
        containing any of them.

::: {#crawling-rules .section}
###### Crawling rules[¶](#crawling-rules "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spiders.]{.pre}]{.sig-prename .descclassname}[[Rule]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[link_extractor]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[callback]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[cb_kwargs]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[follow]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[process_links]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[process_request]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[errback]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/crawl.html#Rule){.reference .internal}[¶](#scrapy.spiders.Rule "Permalink to this definition"){.headerlink}

:   [`link_extractor`{.docutils .literal .notranslate}]{.pre} is a
    [[Link Extractor]{.std
    .std-ref}](index.html#topics-link-extractors){.hoverxref .tooltip
    .reference .internal} object which defines how links will be
    extracted from each crawled page. Each produced link will be used to
    generate a [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} object, which will contain the link's text in
    its [`meta`{.docutils .literal .notranslate}]{.pre} dictionary
    (under the [`link_text`{.docutils .literal .notranslate}]{.pre}
    key). If omitted, a default link extractor created with no arguments
    will be used, resulting in all links being extracted.

    [`callback`{.docutils .literal .notranslate}]{.pre} is a callable or
    a string (in which case a method from the spider object with that
    name will be used) to be called for each link extracted with the
    specified link extractor. This callback receives a
    [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} as its first argument and must return either a single
    instance or an iterable of [[item objects]{.std
    .std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
    .internal} and/or [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} objects (or any subclass of them). As mentioned
    above, the received [[`Response`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} object will contain the text of the link that produced
    the [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} in its [`meta`{.docutils .literal
    .notranslate}]{.pre} dictionary (under the [`link_text`{.docutils
    .literal .notranslate}]{.pre} key)

    [`cb_kwargs`{.docutils .literal .notranslate}]{.pre} is a dict
    containing the keyword arguments to be passed to the callback
    function.

    [`follow`{.docutils .literal .notranslate}]{.pre} is a boolean which
    specifies if links should be followed from each response extracted
    with this rule. If [`callback`{.docutils .literal
    .notranslate}]{.pre} is None [`follow`{.docutils .literal
    .notranslate}]{.pre} defaults to [`True`{.docutils .literal
    .notranslate}]{.pre}, otherwise it defaults to [`False`{.docutils
    .literal .notranslate}]{.pre}.

    [`process_links`{.docutils .literal .notranslate}]{.pre} is a
    callable, or a string (in which case a method from the spider object
    with that name will be used) which will be called for each list of
    links extracted from each response using the specified
    [`link_extractor`{.docutils .literal .notranslate}]{.pre}. This is
    mainly used for filtering purposes.

    [`process_request`{.docutils .literal .notranslate}]{.pre} is a
    callable (or a string, in which case a method from the spider object
    with that name will be used) which will be called for every
    [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} extracted by this rule. This callable should
    take said request as first argument and the [[`Response`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} from which the request originated as second argument. It
    must return a [`Request`{.docutils .literal .notranslate}]{.pre}
    object or [`None`{.docutils .literal .notranslate}]{.pre} (to filter
    out the request).

    [`errback`{.docutils .literal .notranslate}]{.pre} is a callable or
    a string (in which case a method from the spider object with that
    name will be used) to be called if any exception is raised while
    processing a request generated by the rule. It receives a
    [[`Twisted`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}` `{.xref .py .py-class .docutils .literal
    .notranslate}[`Failure`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference
    .external} instance as first parameter.

    ::: {.admonition .warning}
    Warning

    Because of its internal implementation, you must explicitly set
    callbacks for new requests when writing [[`CrawlSpider`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.spiders.CrawlSpider "scrapy.spiders.CrawlSpider"){.reference
    .internal}-based spiders; unexpected behaviour can occur otherwise.
    :::

    ::: versionadded
    [New in version 2.0: ]{.versionmodified .added}The *errback*
    parameter.
    :::
:::

::: {#crawlspider-example .section}
###### CrawlSpider example[¶](#crawlspider-example "Permalink to this heading"){.headerlink}

Let's now take a look at an example CrawlSpider with rules:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from scrapy.spiders import CrawlSpider, Rule
    from scrapy.linkextractors import LinkExtractor


    class MySpider(CrawlSpider):
        name = "example.com"
        allowed_domains = ["example.com"]
        start_urls = ["http://www.example.com"]

        rules = (
            # Extract links matching 'category.php' (but not matching 'subsection.php')
            # and follow links from them (since no callback means follow=True by default).
            Rule(LinkExtractor(allow=(r"category\.php",), deny=(r"subsection\.php",))),
            # Extract links matching 'item.php' and parse them with the spider's method parse_item
            Rule(LinkExtractor(allow=(r"item\.php",)), callback="parse_item"),
        )

        def parse_item(self, response):
            self.logger.info("Hi, this is an item page! %s", response.url)
            item = scrapy.Item()
            item["id"] = response.xpath('//td[@id="item_id"]/text()').re(r"ID: (\d+)")
            item["name"] = response.xpath('//td[@id="item_name"]/text()').get()
            item["description"] = response.xpath(
                '//td[@id="item_description"]/text()'
            ).get()
            item["link_text"] = response.meta["link_text"]
            url = response.xpath('//td[@id="additional_data"]/@href').get()
            return response.follow(
                url, self.parse_additional_page, cb_kwargs=dict(item=item)
            )

        def parse_additional_page(self, response, item):
            item["additional_data"] = response.xpath(
                '//p[@id="additional_data"]/text()'
            ).get()
            return item
:::
:::

This spider would start crawling example.com's home page, collecting
category links, and item links, parsing the latter with the
[`parse_item`{.docutils .literal .notranslate}]{.pre} method. For each
item response, some data will be extracted from the HTML using XPath,
and an [`Item`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} will be filled with it.
:::
:::

::: {#xmlfeedspider .section}
##### XMLFeedSpider[¶](#xmlfeedspider "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spiders.]{.pre}]{.sig-prename .descclassname}[[XMLFeedSpider]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/feed.html#XMLFeedSpider){.reference .internal}[¶](#scrapy.spiders.XMLFeedSpider "Permalink to this definition"){.headerlink}

:   XMLFeedSpider is designed for parsing XML feeds by iterating through
    them by a certain node name. The iterator can be chosen from:
    [`iternodes`{.docutils .literal .notranslate}]{.pre},
    [`xml`{.docutils .literal .notranslate}]{.pre}, and
    [`html`{.docutils .literal .notranslate}]{.pre}. It's recommended to
    use the [`iternodes`{.docutils .literal .notranslate}]{.pre}
    iterator for performance reasons, since the [`xml`{.docutils
    .literal .notranslate}]{.pre} and [`html`{.docutils .literal
    .notranslate}]{.pre} iterators generate the whole DOM at once in
    order to parse it. However, using [`html`{.docutils .literal
    .notranslate}]{.pre} as the iterator may be useful when parsing XML
    with bad markup.

    To set the iterator and the tag name, you must define the following
    class attributes:

    [[iterator]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.XMLFeedSpider.iterator "Permalink to this definition"){.headerlink}

    :   A string which defines the iterator to use. It can be either:

        > <div>
        >
        > -   [`'iternodes'`{.docutils .literal .notranslate}]{.pre} - a
        >     fast iterator based on regular expressions
        >
        > -   [`'html'`{.docutils .literal .notranslate}]{.pre} - an
        >     iterator which uses [`Selector`{.xref .py .py-class
        >     .docutils .literal .notranslate}]{.pre}. Keep in mind this
        >     uses DOM parsing and must load all DOM in memory which
        >     could be a problem for big feeds
        >
        > -   [`'xml'`{.docutils .literal .notranslate}]{.pre} - an
        >     iterator which uses [`Selector`{.xref .py .py-class
        >     .docutils .literal .notranslate}]{.pre}. Keep in mind this
        >     uses DOM parsing and must load all DOM in memory which
        >     could be a problem for big feeds
        >
        > </div>

        It defaults to: [`'iternodes'`{.docutils .literal
        .notranslate}]{.pre}.

    [[itertag]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.XMLFeedSpider.itertag "Permalink to this definition"){.headerlink}

    :   A string with the name of the node (or element) to iterate in.
        Example:

        ::: {.highlight-default .notranslate}
        ::: highlight
            itertag = 'product'
        :::
        :::

    [[namespaces]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.XMLFeedSpider.namespaces "Permalink to this definition"){.headerlink}

    :   A list of [`(prefix,`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`uri)`{.docutils .literal .notranslate}]{.pre}
        tuples which define the namespaces available in that document
        that will be processed with this spider. The [`prefix`{.docutils
        .literal .notranslate}]{.pre} and [`uri`{.docutils .literal
        .notranslate}]{.pre} will be used to automatically register
        namespaces using the [`register_namespace()`{.xref .py .py-meth
        .docutils .literal .notranslate}]{.pre} method.

        You can then specify nodes with namespaces in the
        [[`itertag`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.spiders.XMLFeedSpider.itertag "scrapy.spiders.XMLFeedSpider.itertag"){.reference
        .internal} attribute.

        Example:

        ::: {.highlight-default .notranslate}
        ::: highlight
            class YourSpider(XMLFeedSpider):

                namespaces = [('n', 'http://www.sitemaps.org/schemas/sitemap/0.9')]
                itertag = 'n:url'
                # ...
        :::
        :::

    Apart from these new attributes, this spider has the following
    overridable methods too:

    [[adapt_response]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/feed.html#XMLFeedSpider.adapt_response){.reference .internal}[¶](#scrapy.spiders.XMLFeedSpider.adapt_response "Permalink to this definition"){.headerlink}

    :   A method that receives the response as soon as it arrives from
        the spider middleware, before the spider starts parsing it. It
        can be used to modify the response body before parsing it. This
        method receives a response and also returns a response (it could
        be the same or another one).

    [[parse_node]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[selector]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/feed.html#XMLFeedSpider.parse_node){.reference .internal}[¶](#scrapy.spiders.XMLFeedSpider.parse_node "Permalink to this definition"){.headerlink}

    :   This method is called for the nodes matching the provided tag
        name ([`itertag`{.docutils .literal .notranslate}]{.pre}).
        Receives the response and an [`Selector`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre} for each node.
        Overriding this method is mandatory. Otherwise, you spider won't
        work. This method must return an [[item object]{.std
        .std-ref}](index.html#topics-items){.hoverxref .tooltip
        .reference .internal}, a [`Request`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre} object, or an iterable
        containing any of them.

    [[process_results]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[results]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/feed.html#XMLFeedSpider.process_results){.reference .internal}[¶](#scrapy.spiders.XMLFeedSpider.process_results "Permalink to this definition"){.headerlink}

    :   This method is called for each result (item or request) returned
        by the spider, and it's intended to perform any last time
        processing required before returning the results to the
        framework core, for example setting the item IDs. It receives a
        list of results and the response which originated those results.
        It must return a list of results (items or requests).

    ::: {.admonition .warning}
    Warning

    Because of its internal implementation, you must explicitly set
    callbacks for new requests when writing [[`XMLFeedSpider`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.spiders.XMLFeedSpider "scrapy.spiders.XMLFeedSpider"){.reference
    .internal}-based spiders; unexpected behaviour can occur otherwise.
    :::

::: {#xmlfeedspider-example .section}
###### XMLFeedSpider example[¶](#xmlfeedspider-example "Permalink to this heading"){.headerlink}

These spiders are pretty easy to use, let's have a look at one example:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import XMLFeedSpider
    from myproject.items import TestItem


    class MySpider(XMLFeedSpider):
        name = "example.com"
        allowed_domains = ["example.com"]
        start_urls = ["http://www.example.com/feed.xml"]
        iterator = "iternodes"  # This is actually unnecessary, since it's the default value
        itertag = "item"

        def parse_node(self, response, node):
            self.logger.info(
                "Hi, this is a <%s> node!: %s", self.itertag, "".join(node.getall())
            )

            item = TestItem()
            item["id"] = node.xpath("@id").get()
            item["name"] = node.xpath("name").get()
            item["description"] = node.xpath("description").get()
            return item
:::
:::

Basically what we did up there was to create a spider that downloads a
feed from the given [`start_urls`{.docutils .literal
.notranslate}]{.pre}, and then iterates through each of its
[`item`{.docutils .literal .notranslate}]{.pre} tags, prints them out,
and stores some random data in an [`Item`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre}.
:::
:::

::: {#csvfeedspider .section}
##### CSVFeedSpider[¶](#csvfeedspider "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spiders.]{.pre}]{.sig-prename .descclassname}[[CSVFeedSpider]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/feed.html#CSVFeedSpider){.reference .internal}[¶](#scrapy.spiders.CSVFeedSpider "Permalink to this definition"){.headerlink}

:   This spider is very similar to the XMLFeedSpider, except that it
    iterates over rows, instead of nodes. The method that gets called in
    each iteration is [[`parse_row()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.spiders.CSVFeedSpider.parse_row "scrapy.spiders.CSVFeedSpider.parse_row"){.reference
    .internal}.

    [[delimiter]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.CSVFeedSpider.delimiter "Permalink to this definition"){.headerlink}

    :   A string with the separator character for each field in the CSV
        file Defaults to [`','`{.docutils .literal .notranslate}]{.pre}
        (comma).

    [[quotechar]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.CSVFeedSpider.quotechar "Permalink to this definition"){.headerlink}

    :   A string with the enclosure character for each field in the CSV
        file Defaults to [`'"'`{.docutils .literal .notranslate}]{.pre}
        (quotation mark).

    [[headers]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.CSVFeedSpider.headers "Permalink to this definition"){.headerlink}

    :   A list of the column names in the CSV file.

    [[parse_row]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[row]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/feed.html#CSVFeedSpider.parse_row){.reference .internal}[¶](#scrapy.spiders.CSVFeedSpider.parse_row "Permalink to this definition"){.headerlink}

    :   Receives a response and a dict (representing each row) with a
        key for each provided (or detected) header of the CSV file. This
        spider also gives the opportunity to override
        [`adapt_response`{.docutils .literal .notranslate}]{.pre} and
        [`process_results`{.docutils .literal .notranslate}]{.pre}
        methods for pre- and post-processing purposes.

::: {#csvfeedspider-example .section}
###### CSVFeedSpider example[¶](#csvfeedspider-example "Permalink to this heading"){.headerlink}

Let's see an example similar to the previous one, but using a
[[`CSVFeedSpider`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.spiders.CSVFeedSpider "scrapy.spiders.CSVFeedSpider"){.reference
.internal}:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import CSVFeedSpider
    from myproject.items import TestItem


    class MySpider(CSVFeedSpider):
        name = "example.com"
        allowed_domains = ["example.com"]
        start_urls = ["http://www.example.com/feed.csv"]
        delimiter = ";"
        quotechar = "'"
        headers = ["id", "name", "description"]

        def parse_row(self, response, row):
            self.logger.info("Hi, this is a row!: %r", row)

            item = TestItem()
            item["id"] = row["id"]
            item["name"] = row["name"]
            item["description"] = row["description"]
            return item
:::
:::
:::
:::

::: {#sitemapspider .section}
##### SitemapSpider[¶](#sitemapspider "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spiders.]{.pre}]{.sig-prename .descclassname}[[SitemapSpider]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/sitemap.html#SitemapSpider){.reference .internal}[¶](#scrapy.spiders.SitemapSpider "Permalink to this definition"){.headerlink}

:   SitemapSpider allows you to crawl a site by discovering the URLs
    using [Sitemaps](https://www.sitemaps.org/index.html){.reference
    .external}.

    It supports nested sitemaps and discovering sitemap urls from
    [robots.txt](https://www.robotstxt.org/){.reference .external}.

    [[sitemap_urls]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.SitemapSpider.sitemap_urls "Permalink to this definition"){.headerlink}

    :   A list of urls pointing to the sitemaps whose urls you want to
        crawl.

        You can also point to a
        [robots.txt](https://www.robotstxt.org/){.reference .external}
        and it will be parsed to extract sitemap urls from it.

    [[sitemap_rules]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.SitemapSpider.sitemap_rules "Permalink to this definition"){.headerlink}

    :   A list of tuples [`(regex,`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`callback)`{.docutils .literal
        .notranslate}]{.pre} where:

        -   [`regex`{.docutils .literal .notranslate}]{.pre} is a
            regular expression to match urls extracted from sitemaps.
            [`regex`{.docutils .literal .notranslate}]{.pre} can be
            either a str or a compiled regex object.

        -   callback is the callback to use for processing the urls that
            match the regular expression. [`callback`{.docutils .literal
            .notranslate}]{.pre} can be a string (indicating the name of
            a spider method) or a callable.

        For example:

        ::: {.highlight-default .notranslate}
        ::: highlight
            sitemap_rules = [('/product/', 'parse_product')]
        :::
        :::

        Rules are applied in order, and only the first one that matches
        will be used.

        If you omit this attribute, all urls found in sitemaps will be
        processed with the [`parse`{.docutils .literal
        .notranslate}]{.pre} callback.

    [[sitemap_follow]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.SitemapSpider.sitemap_follow "Permalink to this definition"){.headerlink}

    :   A list of regexes of sitemap that should be followed. This is
        only for sites that use [Sitemap index
        files](https://www.sitemaps.org/protocol.html#index){.reference
        .external} that point to other sitemap files.

        By default, all sitemaps are followed.

    [[sitemap_alternate_links]{.pre}]{.sig-name .descname}[¶](#scrapy.spiders.SitemapSpider.sitemap_alternate_links "Permalink to this definition"){.headerlink}

    :   Specifies if alternate links for one [`url`{.docutils .literal
        .notranslate}]{.pre} should be followed. These are links for the
        same website in another language passed within the same
        [`url`{.docutils .literal .notranslate}]{.pre} block.

        For example:

        ::: {.highlight-default .notranslate}
        ::: highlight
            <url>
                <loc>http://example.com/</loc>
                <xhtml:link rel="alternate" hreflang="de" href="http://example.com/de"/>
            </url>
        :::
        :::

        With [`sitemap_alternate_links`{.docutils .literal
        .notranslate}]{.pre} set, this would retrieve both URLs. With
        [`sitemap_alternate_links`{.docutils .literal
        .notranslate}]{.pre} disabled, only
        [`http://example.com/`{.docutils .literal .notranslate}]{.pre}
        would be retrieved.

        Default is [`sitemap_alternate_links`{.docutils .literal
        .notranslate}]{.pre} disabled.

    [[sitemap_filter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[entries]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiders/sitemap.html#SitemapSpider.sitemap_filter){.reference .internal}[¶](#scrapy.spiders.SitemapSpider.sitemap_filter "Permalink to this definition"){.headerlink}

    :   This is a filter function that could be overridden to select
        sitemap entries based on their attributes.

        For example:

        ::: {.highlight-default .notranslate}
        ::: highlight
            <url>
                <loc>http://example.com/</loc>
                <lastmod>2005-01-01</lastmod>
            </url>
        :::
        :::

        We can define a [`sitemap_filter`{.docutils .literal
        .notranslate}]{.pre} function to filter [`entries`{.docutils
        .literal .notranslate}]{.pre} by date:

        ::: {.highlight-python .notranslate}
        ::: highlight
            from datetime import datetime
            from scrapy.spiders import SitemapSpider


            class FilteredSitemapSpider(SitemapSpider):
                name = "filtered_sitemap_spider"
                allowed_domains = ["example.com"]
                sitemap_urls = ["http://example.com/sitemap.xml"]

                def sitemap_filter(self, entries):
                    for entry in entries:
                        date_time = datetime.strptime(entry["lastmod"], "%Y-%m-%d")
                        if date_time.year >= 2005:
                            yield entry
        :::
        :::

        This would retrieve only [`entries`{.docutils .literal
        .notranslate}]{.pre} modified on 2005 and the following years.

        Entries are dict objects extracted from the sitemap document.
        Usually, the key is the tag name and the value is the text
        inside it.

        It's important to notice that:

        -   as the loc attribute is required, entries without this tag
            are discarded

        -   alternate links are stored in a list with the key
            [`alternate`{.docutils .literal .notranslate}]{.pre} (see
            [`sitemap_alternate_links`{.docutils .literal
            .notranslate}]{.pre})

        -   namespaces are removed, so lxml tags named as
            [`{namespace}tagname`{.docutils .literal
            .notranslate}]{.pre} become only [`tagname`{.docutils
            .literal .notranslate}]{.pre}

        If you omit this method, all entries found in sitemaps will be
        processed, observing other attributes and their settings.

::: {#sitemapspider-examples .section}
###### SitemapSpider examples[¶](#sitemapspider-examples "Permalink to this heading"){.headerlink}

Simplest example: process all urls discovered through sitemaps using the
[`parse`{.docutils .literal .notranslate}]{.pre} callback:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import SitemapSpider


    class MySpider(SitemapSpider):
        sitemap_urls = ["http://www.example.com/sitemap.xml"]

        def parse(self, response):
            pass  # ... scrape item here ...
:::
:::

Process some urls with certain callback and other urls with a different
callback:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import SitemapSpider


    class MySpider(SitemapSpider):
        sitemap_urls = ["http://www.example.com/sitemap.xml"]
        sitemap_rules = [
            ("/product/", "parse_product"),
            ("/category/", "parse_category"),
        ]

        def parse_product(self, response):
            pass  # ... scrape product ...

        def parse_category(self, response):
            pass  # ... scrape category ...
:::
:::

Follow sitemaps defined in the
[robots.txt](https://www.robotstxt.org/){.reference .external} file and
only follow sitemaps whose url contains [`/sitemap_shop`{.docutils
.literal .notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import SitemapSpider


    class MySpider(SitemapSpider):
        sitemap_urls = ["http://www.example.com/robots.txt"]
        sitemap_rules = [
            ("/shop/", "parse_shop"),
        ]
        sitemap_follow = ["/sitemap_shops"]

        def parse_shop(self, response):
            pass  # ... scrape shop here ...
:::
:::

Combine SitemapSpider with other sources of urls:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import SitemapSpider


    class MySpider(SitemapSpider):
        sitemap_urls = ["http://www.example.com/robots.txt"]
        sitemap_rules = [
            ("/shop/", "parse_shop"),
        ]

        other_urls = ["http://www.example.com/about"]

        def start_requests(self):
            requests = list(super(MySpider, self).start_requests())
            requests += [scrapy.Request(x, self.parse_other) for x in self.other_urls]
            return requests

        def parse_shop(self, response):
            pass  # ... scrape shop here ...

        def parse_other(self, response):
            pass  # ... scrape other here ...
:::
:::
:::
:::
:::
:::

[]{#document-topics/selectors}

::: {#selectors .section}
[]{#topics-selectors}

### Selectors[¶](#selectors "Permalink to this heading"){.headerlink}

When you're scraping web pages, the most common task you need to perform
is to extract data from the HTML source. There are several libraries
available to achieve this, such as:

-   [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){.reference
    .external} is a very popular web scraping library among Python
    programmers which constructs a Python object based on the structure
    of the HTML code and also deals with bad markup reasonably well, but
    it has one drawback: it's slow.

-   [lxml](https://lxml.de/){.reference .external} is an XML parsing
    library (which also parses HTML) with a pythonic API based on
    [[`ElementTree`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/xml.etree.elementtree.html#module-xml.etree.ElementTree "(in Python v3.12)"){.reference
    .external}. (lxml is not part of the Python standard library.)

Scrapy comes with its own mechanism for extracting data. They're called
selectors because they "select" certain parts of the HTML document
specified either by [XPath](https://www.w3.org/TR/xpath/all/){.reference
.external} or [CSS](https://www.w3.org/TR/selectors){.reference
.external} expressions.

[XPath](https://www.w3.org/TR/xpath/all/){.reference .external} is a
language for selecting nodes in XML documents, which can also be used
with HTML. [CSS](https://www.w3.org/TR/selectors){.reference .external}
is a language for applying styles to HTML documents. It defines
selectors to associate those styles with specific HTML elements.

::: {.admonition .note}
Note

Scrapy Selectors is a thin wrapper around
[parsel](https://parsel.readthedocs.io/en/latest/){.reference .external}
library; the purpose of this wrapper is to provide better integration
with Scrapy Response objects.

[parsel](https://parsel.readthedocs.io/en/latest/){.reference .external}
is a stand-alone web scraping library which can be used without Scrapy.
It uses [lxml](https://lxml.de/){.reference .external} library under the
hood, and implements an easy API on top of lxml API. It means Scrapy
selectors are very similar in speed and parsing accuracy to lxml.
:::

::: {#using-selectors .section}
#### Using selectors[¶](#using-selectors "Permalink to this heading"){.headerlink}

::: {#constructing-selectors .section}
##### Constructing selectors[¶](#constructing-selectors "Permalink to this heading"){.headerlink}

Response objects expose a [`Selector`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre} instance on [`.selector`{.docutils
.literal .notranslate}]{.pre} attribute:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.selector.xpath("//span/text()").get()
    'good'
:::
:::

Querying responses using XPath and CSS is so common that responses
include two more shortcuts: [`response.xpath()`{.docutils .literal
.notranslate}]{.pre} and [`response.css()`{.docutils .literal
.notranslate}]{.pre}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//span/text()").get()
    'good'
    >>> response.css("span::text").get()
    'good'
:::
:::

Scrapy selectors are instances of [`Selector`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre} class constructed by passing
either [[`TextResponse`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
.internal} object or markup as a string (in [`text`{.docutils .literal
.notranslate}]{.pre} argument).

Usually there is no need to construct Scrapy selectors manually:
[`response`{.docutils .literal .notranslate}]{.pre} object is available
in Spider callbacks, so in most cases it is more convenient to use
[`response.css()`{.docutils .literal .notranslate}]{.pre} and
[`response.xpath()`{.docutils .literal .notranslate}]{.pre} shortcuts.
By using [`response.selector`{.docutils .literal .notranslate}]{.pre} or
one of these shortcuts you can also ensure the response body is parsed
only once.

But if required, it is possible to use [`Selector`{.docutils .literal
.notranslate}]{.pre} directly. Constructing from text:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy.selector import Selector
    >>> body = "<html><body><span>good</span></body></html>"
    >>> Selector(text=body).xpath("//span/text()").get()
    'good'
:::
:::

Constructing from response - [[`HtmlResponse`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.HtmlResponse "scrapy.http.HtmlResponse"){.reference
.internal} is one of [[`TextResponse`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
.internal} subclasses:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy.selector import Selector
    >>> from scrapy.http import HtmlResponse
    >>> response = HtmlResponse(url="http://example.com", body=body, encoding="utf-8")
    >>> Selector(response=response).xpath("//span/text()").get()
    'good'
:::
:::

[`Selector`{.docutils .literal .notranslate}]{.pre} automatically
chooses the best parsing rules (XML vs HTML) based on input type.
:::

::: {#id1 .section}
##### Using selectors[¶](#id1 "Permalink to this heading"){.headerlink}

To explain how to use the selectors we'll use the [`Scrapy`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`shell`{.docutils .literal .notranslate}]{.pre} (which
provides interactive testing) and an example page located in the Scrapy
documentation server:

> <div>
>
> [https://docs.scrapy.org/en/latest/\_static/selectors-sample1.html](https://docs.scrapy.org/en/latest/_static/selectors-sample1.html){.reference
> .external}
>
> </div>

For the sake of completeness, here's its full HTML code:

::: {.highlight-html .notranslate}
::: highlight
    <!DOCTYPE html>

    <html>
      <head>
        <base href='http://example.com/' />
        <title>Example website</title>
      </head>
      <body>
        <div id='images'>
          <a href='image1.html'>Name: My image 1 <br /><img src='image1_thumb.jpg' alt='image1'/></a>
          <a href='image2.html'>Name: My image 2 <br /><img src='image2_thumb.jpg' alt='image2'/></a>
          <a href='image3.html'>Name: My image 3 <br /><img src='image3_thumb.jpg' alt='image3'/></a>
          <a href='image4.html'>Name: My image 4 <br /><img src='image4_thumb.jpg' alt='image4'/></a>
          <a href='image5.html'>Name: My image 5 <br /><img src='image5_thumb.jpg' alt='image5'/></a>
        </div>
      </body>
    </html>
:::
:::

First, let's open the shell:

::: {.highlight-sh .notranslate}
::: highlight
    scrapy shell https://docs.scrapy.org/en/latest/_static/selectors-sample1.html
:::
:::

Then, after the shell loads, you'll have the response available as
[`response`{.docutils .literal .notranslate}]{.pre} shell variable, and
its attached selector in [`response.selector`{.docutils .literal
.notranslate}]{.pre} attribute.

Since we're dealing with HTML, the selector will automatically use an
HTML parser.

So, by looking at the [[HTML code]{.std
.std-ref}](#topics-selectors-htmlcode){.hoverxref .tooltip .reference
.internal} of that page, let's construct an XPath for selecting the text
inside the title tag:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//title/text()")
    [<Selector query='//title/text()' data='Example website'>]
:::
:::

To actually extract the textual data, you must call the selector
[`.get()`{.docutils .literal .notranslate}]{.pre} or
[`.getall()`{.docutils .literal .notranslate}]{.pre} methods, as
follows:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("//title/text()").getall()
    ['Example website']
    >>> response.xpath("//title/text()").get()
    'Example website'
:::
:::

[`.get()`{.docutils .literal .notranslate}]{.pre} always returns a
single result; if there are several matches, content of a first match is
returned; if there are no matches, None is returned.
[`.getall()`{.docutils .literal .notranslate}]{.pre} returns a list with
all results.

Notice that CSS selectors can select text or attribute nodes using CSS3
pseudo-elements:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("title::text").get()
    'Example website'
:::
:::

As you can see, [`.xpath()`{.docutils .literal .notranslate}]{.pre} and
[`.css()`{.docutils .literal .notranslate}]{.pre} methods return a
[[`SelectorList`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
.internal} instance, which is a list of new selectors. This API can be
used for quickly selecting nested data:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.css("img").xpath("@src").getall()
    ['image1_thumb.jpg',
    'image2_thumb.jpg',
    'image3_thumb.jpg',
    'image4_thumb.jpg',
    'image5_thumb.jpg']
:::
:::

If you want to extract only the first matched element, you can call the
selector [`.get()`{.docutils .literal .notranslate}]{.pre} (or its alias
[`.extract_first()`{.docutils .literal .notranslate}]{.pre} commonly
used in previous Scrapy versions):

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//div[@id="images"]/a/text()').get()
    'Name: My image 1 '
:::