    from twisted.internet import reactor


    def my_function():
        reactor.callLater(...)
:::
:::

Switch to something like:

::: {.highlight-python .notranslate}
::: highlight
    def my_function():
        from twisted.internet import reactor

        reactor.callLater(...)
:::
:::

Alternatively, you can try to [[manually install the asyncio
reactor]{.std .std-ref}](#install-asyncio){.hoverxref .tooltip
.reference .internal}, with [[`install_reactor()`{.xref .py .py-func
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.utils.reactor.install_reactor "scrapy.utils.reactor.install_reactor"){.reference
.internal}, before those imports happen.
:::

::: {#awaiting-on-deferreds .section}
[]{#asyncio-await-dfd}

#### Awaiting on Deferreds[¶](#awaiting-on-deferreds "Permalink to this heading"){.headerlink}

When the asyncio reactor isn't installed, you can await on Deferreds in
the coroutines directly. When it is installed, this is not possible
anymore, due to specifics of the Scrapy coroutine integration (the
coroutines are wrapped into [[`asyncio.Future`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-future.html#asyncio.Future "(in Python v3.12)"){.reference
.external} objects, not into [[`Deferred`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
.external} directly), and you need to wrap them into Futures. Scrapy
provides two helpers for this:

[[scrapy.utils.defer.]{.pre}]{.sig-prename .descclassname}[[deferred_to_future]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[d]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[Future]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/defer.html#deferred_to_future){.reference .internal}[¶](#scrapy.utils.defer.deferred_to_future "Permalink to this definition"){.headerlink}

:   ::: versionadded
    [New in version 2.6.0.]{.versionmodified .added}
    :::

    Return an [[`asyncio.Future`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-future.html#asyncio.Future "(in Python v3.12)"){.reference
    .external} object that wraps *d*.

    When [[using the asyncio reactor]{.std
    .std-ref}](#install-asyncio){.hoverxref .tooltip .reference
    .internal}, you cannot await on [[`Deferred`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
    .external} objects from [[Scrapy callables defined as
    coroutines]{.std .std-ref}](index.html#coroutine-support){.hoverxref
    .tooltip .reference .internal}, you can only await on
    [`Future`{.docutils .literal .notranslate}]{.pre} objects. Wrapping
    [`Deferred`{.docutils .literal .notranslate}]{.pre} objects into
    [`Future`{.docutils .literal .notranslate}]{.pre} objects allows you
    to wait on them:

    ::: {.highlight-default .notranslate}
    ::: highlight
        class MySpider(Spider):
            ...
            async def parse(self, response):
                additional_request = scrapy.Request('https://example.org/price')
                deferred = self.crawler.engine.download(additional_request)
                additional_response = await deferred_to_future(deferred)
    :::
    :::

```{=html}
<!-- -->
```

[[scrapy.utils.defer.]{.pre}]{.sig-prename .descclassname}[[maybe_deferred_to_future]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[d]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[Future]{.pre}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/defer.html#maybe_deferred_to_future){.reference .internal}[¶](#scrapy.utils.defer.maybe_deferred_to_future "Permalink to this definition"){.headerlink}

:   ::: versionadded
    [New in version 2.6.0.]{.versionmodified .added}
    :::

    Return *d* as an object that can be awaited from a [[Scrapy callable
    defined as a coroutine]{.std
    .std-ref}](index.html#coroutine-support){.hoverxref .tooltip
    .reference .internal}.

    What you can await in Scrapy callables defined as coroutines depends
    on the value of [[`TWISTED_REACTOR`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
    .tooltip .reference .internal}:

    -   When not using the asyncio reactor, you can only await on
        [[`Deferred`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
        .external} objects.

    -   When [[using the asyncio reactor]{.std
        .std-ref}](#install-asyncio){.hoverxref .tooltip .reference
        .internal}, you can only await on [[`asyncio.Future`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-future.html#asyncio.Future "(in Python v3.12)"){.reference
        .external} objects.

    If you want to write code that uses [`Deferred`{.docutils .literal
    .notranslate}]{.pre} objects but works with any reactor, use this
    function on all [`Deferred`{.docutils .literal .notranslate}]{.pre}
    objects:

    ::: {.highlight-default .notranslate}
    ::: highlight
        class MySpider(Spider):
            ...
            async def parse(self, response):
                additional_request = scrapy.Request('https://example.org/price')
                deferred = self.crawler.engine.download(additional_request)
                additional_response = await maybe_deferred_to_future(deferred)
    :::
    :::

::: {.admonition .tip}
Tip

If you need to use these functions in code that aims to be compatible
with lower versions of Scrapy that do not provide these functions, down
to Scrapy 2.0 (earlier versions do not support [[`asyncio`{.xref .py
.py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
.external}), you can copy the implementation of these functions into
your own code.
:::
:::

::: {#enforcing-asyncio-as-a-requirement .section}
[]{#enforce-asyncio-requirement}

#### Enforcing asyncio as a requirement[¶](#enforcing-asyncio-as-a-requirement "Permalink to this heading"){.headerlink}

If you are writing a [[component]{.std
.std-ref}](index.html#topics-components){.hoverxref .tooltip .reference
.internal} that requires asyncio to work, use
[`scrapy.utils.reactor.is_asyncio_reactor_installed()`{.xref .py
.py-func .docutils .literal .notranslate}]{.pre} to [[enforce it as a
requirement]{.std
.std-ref}](index.html#enforce-component-requirements){.hoverxref
.tooltip .reference .internal}. For example:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.utils.reactor import is_asyncio_reactor_installed


    class MyComponent:
        def __init__(self):
            if not is_asyncio_reactor_installed():
                raise ValueError(
                    f"{MyComponent.__qualname__} requires the asyncio Twisted "
                    f"reactor. Make sure you have it configured in the "
                    f"TWISTED_REACTOR setting. See the asyncio documentation "
                    f"of Scrapy for more information."
                )
:::
:::
:::

::: {#windows-specific-notes .section}
[]{#asyncio-windows}

#### Windows-specific notes[¶](#windows-specific-notes "Permalink to this heading"){.headerlink}

The Windows implementation of [[`asyncio`{.xref .py .py-mod .docutils
.literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
.external} can use two event loop implementations,
[[`ProactorEventLoop`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-eventloop.html#asyncio.ProactorEventLoop "(in Python v3.12)"){.reference
.external} (default) and [[`SelectorEventLoop`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-eventloop.html#asyncio.SelectorEventLoop "(in Python v3.12)"){.reference
.external}. However, only [[`SelectorEventLoop`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-eventloop.html#asyncio.SelectorEventLoop "(in Python v3.12)"){.reference
.external} works with Twisted.

Scrapy changes the event loop class to [[`SelectorEventLoop`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-eventloop.html#asyncio.SelectorEventLoop "(in Python v3.12)"){.reference
.external} automatically when you change the [[`TWISTED_REACTOR`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
.tooltip .reference .internal} setting or call
[[`install_reactor()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.utils.reactor.install_reactor "scrapy.utils.reactor.install_reactor"){.reference
.internal}.

::: {.admonition .note}
Note

Other libraries you use may require [[`ProactorEventLoop`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-eventloop.html#asyncio.ProactorEventLoop "(in Python v3.12)"){.reference
.external}, e.g. because it supports subprocesses (this is the case with
[playwright](https://github.com/microsoft/playwright-python){.reference
.external}), so you cannot use them together with Scrapy on Windows (but
you should be able to use them on WSL or native Linux).
:::
:::

::: {#using-custom-asyncio-loops .section}
[]{#using-custom-loops}

#### Using custom asyncio loops[¶](#using-custom-asyncio-loops "Permalink to this heading"){.headerlink}

You can also use custom asyncio event loops with the asyncio reactor.
Set the [[`ASYNCIO_EVENT_LOOP`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-ASYNCIO_EVENT_LOOP){.hoverxref
.tooltip .reference .internal} setting to the import path of the desired
event loop class to use it instead of the default asyncio event loop.
:::
:::
:::

[[Frequently Asked Questions]{.doc}](index.html#document-faq){.reference .internal}

:   Get answers to most frequently asked questions.

[[Debugging Spiders]{.doc}](index.html#document-topics/debug){.reference .internal}

:   Learn how to debug common problems of your Scrapy spider.

[[Spiders Contracts]{.doc}](index.html#document-topics/contracts){.reference .internal}

:   Learn how to use contracts for testing your spiders.

[[Common Practices]{.doc}](index.html#document-topics/practices){.reference .internal}

:   Get familiar with some Scrapy common practices.

[[Broad Crawls]{.doc}](index.html#document-topics/broad-crawls){.reference .internal}

:   Tune Scrapy for crawling a lot domains in parallel.

[[Using your browser's Developer Tools for scraping]{.doc}](index.html#document-topics/developer-tools){.reference .internal}

:   Learn how to scrape with your browser's developer tools.

[[Selecting dynamically-loaded content]{.doc}](index.html#document-topics/dynamic-content){.reference .internal}

:   Read webpage data that is loaded dynamically.

[[Debugging memory leaks]{.doc}](index.html#document-topics/leaks){.reference .internal}

:   Learn how to find and get rid of memory leaks in your crawler.

[[Downloading and processing files and images]{.doc}](index.html#document-topics/media-pipeline){.reference .internal}

:   Download files and/or images associated with your scraped items.

[[Deploying Spiders]{.doc}](index.html#document-topics/deploy){.reference .internal}

:   Deploying your Scrapy spiders and run them in a remote server.

[[AutoThrottle extension]{.doc}](index.html#document-topics/autothrottle){.reference .internal}

:   Adjust crawl rate dynamically based on load.

[[Benchmarking]{.doc}](index.html#document-topics/benchmarking){.reference .internal}

:   Check how Scrapy performs on your hardware.

[[Jobs: pausing and resuming crawls]{.doc}](index.html#document-topics/jobs){.reference .internal}

:   Learn how to pause and resume crawls for large spiders.

[[Coroutines]{.doc}](index.html#document-topics/coroutines){.reference .internal}

:   Use the [[coroutine syntax]{.xref .std
    .std-ref}](https://docs.python.org/3/reference/compound_stmts.html#async "(in Python v3.12)"){.reference
    .external}.

[[asyncio]{.doc}](index.html#document-topics/asyncio){.reference .internal}

:   Use [[`asyncio`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
    .external} and [[`asyncio`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
    .external}-powered libraries.
:::

::: {#extending-scrapy .section}
[]{#id2}

## Extending Scrapy[¶](#extending-scrapy "Permalink to this heading"){.headerlink}

::: {.toctree-wrapper .compound}
[]{#document-topics/architecture}

::: {#architecture-overview .section}
[]{#topics-architecture}

### Architecture overview[¶](#architecture-overview "Permalink to this heading"){.headerlink}

This document describes the architecture of Scrapy and how its
components interact.

::: {#overview .section}
#### Overview[¶](#overview "Permalink to this heading"){.headerlink}

The following diagram shows an overview of the Scrapy architecture with
its components and an outline of the data flow that takes place inside
the system (shown by the red arrows). A brief description of the
components is included below with links for more detailed information
about them. The data flow is also described below.
:::

::: {#data-flow .section}
[]{#id1}

#### Data flow[¶](#data-flow "Permalink to this heading"){.headerlink}

[![Scrapy
architecture](_images/scrapy_architecture_02.png){style="width: 700px; height: 470px;"}](_images/scrapy_architecture_02.png){.reference
.internal .image-reference}

The data flow in Scrapy is controlled by the execution engine, and goes
like this:

1.  The [[Engine]{.std .std-ref}](#component-engine){.hoverxref .tooltip
    .reference .internal} gets the initial Requests to crawl from the
    [[Spider]{.std .std-ref}](#component-spiders){.hoverxref .tooltip
    .reference .internal}.

2.  The [[Engine]{.std .std-ref}](#component-engine){.hoverxref .tooltip
    .reference .internal} schedules the Requests in the
    [[Scheduler]{.std .std-ref}](#component-scheduler){.hoverxref
    .tooltip .reference .internal} and asks for the next Requests to
    crawl.

3.  The [[Scheduler]{.std .std-ref}](#component-scheduler){.hoverxref
    .tooltip .reference .internal} returns the next Requests to the
    [[Engine]{.std .std-ref}](#component-engine){.hoverxref .tooltip
    .reference .internal}.

4.  The [[Engine]{.std .std-ref}](#component-engine){.hoverxref .tooltip
    .reference .internal} sends the Requests to the [[Downloader]{.std
    .std-ref}](#component-downloader){.hoverxref .tooltip .reference
    .internal}, passing through the [[Downloader Middlewares]{.std
    .std-ref}](#component-downloader-middleware){.hoverxref .tooltip
    .reference .internal} (see [[`process_request()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
    .internal}).

5.  Once the page finishes downloading the [[Downloader]{.std
    .std-ref}](#component-downloader){.hoverxref .tooltip .reference
    .internal} generates a Response (with that page) and sends it to the
    Engine, passing through the [[Downloader Middlewares]{.std
    .std-ref}](#component-downloader-middleware){.hoverxref .tooltip
    .reference .internal} (see [[`process_response()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
    .internal}).

6.  The [[Engine]{.std .std-ref}](#component-engine){.hoverxref .tooltip
    .reference .internal} receives the Response from the
    [[Downloader]{.std .std-ref}](#component-downloader){.hoverxref
    .tooltip .reference .internal} and sends it to the [[Spider]{.std
    .std-ref}](#component-spiders){.hoverxref .tooltip .reference
    .internal} for processing, passing through the [[Spider
    Middleware]{.std .std-ref}](#component-spider-middleware){.hoverxref
    .tooltip .reference .internal} (see [[`process_spider_input()`{.xref
    .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input"){.reference
    .internal}).

7.  The [[Spider]{.std .std-ref}](#component-spiders){.hoverxref
    .tooltip .reference .internal} processes the Response and returns
    scraped items and new Requests (to follow) to the [[Engine]{.std
    .std-ref}](#component-engine){.hoverxref .tooltip .reference
    .internal}, passing through the [[Spider Middleware]{.std
    .std-ref}](#component-spider-middleware){.hoverxref .tooltip
    .reference .internal} (see [[`process_spider_output()`{.xref .py
    .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
    .internal}).

8.  The [[Engine]{.std .std-ref}](#component-engine){.hoverxref .tooltip
    .reference .internal} sends processed items to [[Item
    Pipelines]{.std .std-ref}](#component-pipelines){.hoverxref .tooltip
    .reference .internal}, then send processed Requests to the
    [[Scheduler]{.std .std-ref}](#component-scheduler){.hoverxref
    .tooltip .reference .internal} and asks for possible next Requests
    to crawl.

9.  The process repeats (from step 3) until there are no more requests
    from the [[Scheduler]{.std
    .std-ref}](#component-scheduler){.hoverxref .tooltip .reference
    .internal}.
:::

::: {#components .section}
#### Components[¶](#components "Permalink to this heading"){.headerlink}

::: {#scrapy-engine .section}
[]{#component-engine}

##### Scrapy Engine[¶](#scrapy-engine "Permalink to this heading"){.headerlink}

The engine is responsible for controlling the data flow between all
components of the system, and triggering events when certain actions
occur. See the [[Data Flow]{.std .std-ref}](#data-flow){.hoverxref
.tooltip .reference .internal} section above for more details.
:::

::: {#scheduler .section}
[]{#component-scheduler}

##### Scheduler[¶](#scheduler "Permalink to this heading"){.headerlink}

The [[scheduler]{.std .std-ref}](index.html#topics-scheduler){.hoverxref
.tooltip .reference .internal} receives requests from the engine and
enqueues them for feeding them later (also to the engine) when the
engine requests them.
:::

::: {#downloader .section}
[]{#component-downloader}

##### Downloader[¶](#downloader "Permalink to this heading"){.headerlink}

The Downloader is responsible for fetching web pages and feeding them to
the engine which, in turn, feeds them to the spiders.
:::

::: {#spiders .section}
[]{#component-spiders}

##### Spiders[¶](#spiders "Permalink to this heading"){.headerlink}

Spiders are custom classes written by Scrapy users to parse responses
and extract [[items]{.std .std-ref}](index.html#topics-items){.hoverxref
.tooltip .reference .internal} from them or additional requests to
follow. For more information see [[Spiders]{.std
.std-ref}](index.html#topics-spiders){.hoverxref .tooltip .reference
.internal}.
:::

::: {#item-pipeline .section}
[]{#component-pipelines}

##### Item Pipeline[¶](#item-pipeline "Permalink to this heading"){.headerlink}

The Item Pipeline is responsible for processing the items once they have
been extracted (or scraped) by the spiders. Typical tasks include
cleansing, validation and persistence (like storing the item in a
database). For more information see [[Item Pipeline]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal}.
:::

::: {#downloader-middlewares .section}
[]{#component-downloader-middleware}

##### Downloader middlewares[¶](#downloader-middlewares "Permalink to this heading"){.headerlink}

Downloader middlewares are specific hooks that sit between the Engine
and the Downloader and process requests when they pass from the Engine
to the Downloader, and responses that pass from Downloader to the
Engine.

Use a Downloader middleware if you need to do one of the following:

-   process a request just before it is sent to the Downloader (i.e.
    right before Scrapy sends the request to the website);

-   change received response before passing it to a spider;

-   send a new Request instead of passing received response to a spider;

-   pass response to a spider without fetching a web page;

-   silently drop some requests.

For more information see [[Downloader Middleware]{.std
.std-ref}](index.html#topics-downloader-middleware){.hoverxref .tooltip
.reference .internal}.
:::

::: {#spider-middlewares .section}
[]{#component-spider-middleware}

##### Spider middlewares[¶](#spider-middlewares "Permalink to this heading"){.headerlink}

Spider middlewares are specific hooks that sit between the Engine and
the Spiders and are able to process spider input (responses) and output
(items and requests).

Use a Spider middleware if you need to

-   post-process output of spider callbacks - change/add/remove requests
    or items;

-   post-process start_requests;

-   handle spider exceptions;

-   call errback instead of callback for some of the requests based on
    response content.

For more information see [[Spider Middleware]{.std
.std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
.reference .internal}.
:::
:::

::: {#event-driven-networking .section}
#### Event-driven networking[¶](#event-driven-networking "Permalink to this heading"){.headerlink}

Scrapy is written with
[Twisted](https://twistedmatrix.com/trac/){.reference .external}, a
popular event-driven networking framework for Python. Thus, it's
implemented using a non-blocking (aka asynchronous) code for
concurrency.

For more information about asynchronous programming and Twisted see
these links:

-   [Introduction to
    Deferreds](https://docs.twisted.org/en/stable/core/howto/defer-intro.html "(in Twisted v23.10)"){.reference
    .external}

-   [Twisted - hello, asynchronous
    programming](http://jessenoller.com/blog/2009/02/11/twisted-hello-asynchronous-programming/){.reference
    .external}

-   [Twisted Introduction -
    Krondo](http://krondo.com/an-introduction-to-asynchronous-programming-and-twisted/){.reference
    .external}
:::
:::

[]{#document-topics/addons}

::: {#add-ons .section}
[]{#topics-addons}

### Add-ons[¶](#add-ons "Permalink to this heading"){.headerlink}

Scrapy's add-on system is a framework which unifies managing and
configuring components that extend Scrapy's core functionality, such as
middlewares, extensions, or pipelines. It provides users with a
plug-and-play experience in Scrapy extension management, and grants
extensive configuration control to developers.

::: {#activating-and-configuring-add-ons .section}
#### Activating and configuring add-ons[¶](#activating-and-configuring-add-ons "Permalink to this heading"){.headerlink}

During [[`Crawler`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
.internal} initialization, the list of enabled add-ons is read from your
[`ADDONS`{.docutils .literal .notranslate}]{.pre} setting.

The [`ADDONS`{.docutils .literal .notranslate}]{.pre} setting is a dict
in which every key is an add-on class or its import path and the value
is its priority.

This is an example where two add-ons are enabled in a project's
[`settings.py`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-default .notranslate}
::: highlight
    ADDONS = {
        'path.to.someaddon': 0,
        SomeAddonClass: 1,
    }
:::
:::
:::

::: {#writing-your-own-add-ons .section}
#### Writing your own add-ons[¶](#writing-your-own-add-ons "Permalink to this heading"){.headerlink}

Add-ons are Python classes that include the following method:

[[update_settings]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[settings]{.pre}]{.n}*[)]{.sig-paren}[¶](#update_settings "Permalink to this definition"){.headerlink}

:   This method is called during the initialization of the
    [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal}. Here, you should perform dependency checks (e.g. for
    external Python libraries) and update the [[`Settings`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
    .internal} object as wished, e.g. enable components for this add-on
    or set required configuration of other extensions.

    Parameters

    :   **settings** ([[`Settings`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
        .internal}) -- The settings object storing Scrapy/component
        configuration

They can also have the following method:

*[classmethod]{.pre}[ ]{.w}*[[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[cls]{.pre}]{.n}*, *[[crawler]{.pre}]{.n}*[)]{.sig-paren}

:   If present, this class method is called to create an add-on instance
    from a [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal}. It must return a new instance of the add-on. The crawler
    object provides access to all Scrapy core components like settings
    and signals; it is a way for the add-on to access them and hook its
    functionality into Scrapy.

    Parameters

    :   **crawler** ([[`Crawler`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal}) -- The crawler that uses this add-on

The settings set by the add-on should use the [`addon`{.docutils
.literal .notranslate}]{.pre} priority (see [[Populating the
settings]{.std .std-ref}](index.html#populating-settings){.hoverxref
.tooltip .reference .internal} and
[[`scrapy.settings.BaseSettings.set()`{.xref .py .py-func .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.settings.BaseSettings.set "scrapy.settings.BaseSettings.set"){.reference
.internal}):

::: {.highlight-default .notranslate}
::: highlight
    class MyAddon:
        def update_settings(self, settings):
            settings.set("DNSCACHE_ENABLED", True, "addon")
:::
:::

This allows users to override these settings in the project or spider
configuration. This is not possible with settings that are mutable
objects, such as the dict that is a value of [[`ITEM_PIPELINES`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
.tooltip .reference .internal}. In these cases you can provide an
add-on-specific setting that governs whether the add-on will modify
[[`ITEM_PIPELINES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
.tooltip .reference .internal}:

::: {.highlight-default .notranslate}
::: highlight
    class MyAddon:
        def update_settings(self, settings):
            if settings.getbool("MYADDON_ENABLE_PIPELINE"):
                settings["ITEM_PIPELINES"]["path.to.mypipeline"] = 200
:::
:::

If the [`update_settings`{.docutils .literal .notranslate}]{.pre} method
raises [[`scrapy.exceptions.NotConfigured`{.xref .py .py-exc .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.NotConfigured "scrapy.exceptions.NotConfigured"){.reference
.internal}, the add-on will be skipped. This makes it easy to enable an
add-on only when some conditions are met.

::: {#fallbacks .section}
##### Fallbacks[¶](#fallbacks "Permalink to this heading"){.headerlink}

Some components provided by add-ons need to fall back to "default"
implementations, e.g. a custom download handler needs to send the
request that it doesn't handle via the default download handler, or a
stats collector that includes some additional processing but otherwise
uses the default stats collector. And it's possible that a project needs
to use several custom components of the same type, e.g. two custom
download handlers that support different kinds of custom requests and
still need to use the default download handler for other requests. To
make such use cases easier to configure, we recommend that such custom
components should be written in the following way:

1.  The custom component (e.g. [`MyDownloadHandler`{.docutils .literal
    .notranslate}]{.pre}) shouldn't inherit from the default Scrapy one
    (e.g.
    [`scrapy.core.downloader.handlers.http.HTTPDownloadHandler`{.docutils
    .literal .notranslate}]{.pre}), but instead be able to load the
    class of the fallback component from a special setting (e.g.
    [`MY_FALLBACK_DOWNLOAD_HANDLER`{.docutils .literal
    .notranslate}]{.pre}), create an instance of it and use it.

2.  The add-ons that include these components should read the current
    value of the default setting (e.g. [`DOWNLOAD_HANDLERS`{.docutils
    .literal .notranslate}]{.pre}) in their
    [`update_settings()`{.docutils .literal .notranslate}]{.pre}
    methods, save that value into the fallback setting
    ([`MY_FALLBACK_DOWNLOAD_HANDLER`{.docutils .literal
    .notranslate}]{.pre} mentioned earlier) and set the default setting
    to the component provided by the add-on (e.g.
    [`MyDownloadHandler`{.docutils .literal .notranslate}]{.pre}). If
    the fallback setting is already set by the user, they shouldn't
    change it.

3.  This way, if there are several add-ons that want to modify the same
    setting, all of them will fallback to the component from the
    previous one and then to the Scrapy default. The order of that
    depends on the priority order in the [`ADDONS`{.docutils .literal
    .notranslate}]{.pre} setting.
:::
:::

::: {#add-on-examples .section}
#### Add-on examples[¶](#add-on-examples "Permalink to this heading"){.headerlink}

Set some basic configuration:

::: {.highlight-python .notranslate}
::: highlight
    class MyAddon:
        def update_settings(self, settings):
            settings["ITEM_PIPELINES"]["path.to.mypipeline"] = 200
            settings.set("DNSCACHE_ENABLED", True, "addon")
:::
:::

Check dependencies:

::: {.highlight-python .notranslate}
::: highlight
    class MyAddon:
        def update_settings(self, settings):
            try:
                import boto
            except ImportError:
                raise NotConfigured("MyAddon requires the boto library")
            ...
:::
:::

Access the crawler instance:

::: {.highlight-python .notranslate}
::: highlight
    class MyAddon:
        def __init__(self, crawler) -> None:
            super().__init__()
            self.crawler = crawler

        @classmethod
        def from_crawler(cls, crawler):
            return cls(crawler)

        def update_settings(self, settings):
            ...
:::
:::

Use a fallback component:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.core.downloader.handlers.http import HTTPDownloadHandler


    FALLBACK_SETTING = "MY_FALLBACK_DOWNLOAD_HANDLER"


    class MyHandler:
        lazy = False

        def __init__(self, settings, crawler):
            dhcls = load_object(settings.get(FALLBACK_SETTING))
            self._fallback_handler = create_instance(
                dhcls,
                settings=None,
                crawler=crawler,
            )

        def download_request(self, request, spider):
            if request.meta.get("my_params"):
                # handle the request
                ...
            else:
                return self._fallback_handler.download_request(request, spider)


    class MyAddon:
        def update_settings(self, settings):
            if not settings.get(FALLBACK_SETTING):
                settings.set(
                    FALLBACK_SETTING,
                    settings.getwithbase("DOWNLOAD_HANDLERS")["https"],
                    "addon",
                )
            settings["DOWNLOAD_HANDLERS"]["https"] = MyHandler
:::
:::
:::
:::

[]{#document-topics/downloader-middleware}

::: {#downloader-middleware .section}
[]{#topics-downloader-middleware}

### Downloader Middleware[¶](#downloader-middleware "Permalink to this heading"){.headerlink}

The downloader middleware is a framework of hooks into Scrapy's
request/response processing. It's a light, low-level system for globally
altering Scrapy's requests and responses.

::: {#activating-a-downloader-middleware .section}
[]{#topics-downloader-middleware-setting}

#### Activating a downloader middleware[¶](#activating-a-downloader-middleware "Permalink to this heading"){.headerlink}

To activate a downloader middleware component, add it to the
[[`DOWNLOADER_MIDDLEWARES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES){.hoverxref
.tooltip .reference .internal} setting, which is a dict whose keys are
the middleware class paths and their values are the middleware orders.

Here's an example:

::: {.highlight-python .notranslate}
::: highlight
    DOWNLOADER_MIDDLEWARES = {
        "myproject.middlewares.CustomDownloaderMiddleware": 543,
    }
:::
:::

The [[`DOWNLOADER_MIDDLEWARES`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES){.hoverxref
.tooltip .reference .internal} setting is merged with the
[[`DOWNLOADER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal} setting defined in Scrapy (and not meant
to be overridden) and then sorted by order to get the final sorted list
of enabled middlewares: the first middleware is the one closer to the
engine and the last is the one closer to the downloader. In other words,
the [[`process_request()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
.internal} method of each middleware will be invoked in increasing
middleware order (100, 200, 300, ...) and the
[[`process_response()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
.internal} method of each middleware will be invoked in decreasing
order.

To decide which order to assign to your middleware see the
[[`DOWNLOADER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal} setting and pick a value according to
where you want to insert the middleware. The order does matter because
each middleware performs a different action and your middleware could
depend on some previous (or subsequent) middleware being applied.

If you want to disable a built-in middleware (the ones defined in
[[`DOWNLOADER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal} and enabled by default) you must define
it in your project's [[`DOWNLOADER_MIDDLEWARES`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES){.hoverxref
.tooltip .reference .internal} setting and assign [`None`{.docutils
.literal .notranslate}]{.pre} as its value. For example, if you want to
disable the user-agent middleware:

::: {.highlight-python .notranslate}
::: highlight
    DOWNLOADER_MIDDLEWARES = {
        "myproject.middlewares.CustomDownloaderMiddleware": 543,
        "scrapy.downloadermiddlewares.useragent.UserAgentMiddleware": None,
    }
:::
:::

Finally, keep in mind that some middlewares may need to be enabled
through a particular setting. See each middleware documentation for more
info.
:::

::: {#writing-your-own-downloader-middleware .section}
[]{#topics-downloader-middleware-custom}

#### Writing your own downloader middleware[¶](#writing-your-own-downloader-middleware "Permalink to this heading"){.headerlink}

Each downloader middleware is a Python class that defines one or more of
the methods defined below.

The main entry point is the [`from_crawler`{.docutils .literal
.notranslate}]{.pre} class method, which receives a [[`Crawler`{.xref
.py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
.internal} instance. The [[`Crawler`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
.internal} object gives you access, for example, to the [[settings]{.std
.std-ref}](index.html#topics-settings){.hoverxref .tooltip .reference
.internal}.

[]{#module-scrapy.downloadermiddlewares .target}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.]{.pre}]{.sig-prename .descclassname}[[DownloaderMiddleware]{.pre}]{.sig-name .descname}[¶](#scrapy.downloadermiddlewares.DownloaderMiddleware "Permalink to this definition"){.headerlink}

:   ::: {.admonition .note}
    Note

    Any of the downloader middleware methods may also return a deferred.
    :::

    [[process_request]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "Permalink to this definition"){.headerlink}

    :   This method is called for each request that goes through the
        download middleware.

        [[`process_request()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
        .internal} should either: return [`None`{.docutils .literal
        .notranslate}]{.pre}, return a [`Response`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre} object, return a
        [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object, or raise [[`IgnoreRequest`{.xref .py .py-exc
        .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.exceptions.IgnoreRequest "scrapy.exceptions.IgnoreRequest"){.reference
        .internal}.

        If it returns [`None`{.docutils .literal .notranslate}]{.pre},
        Scrapy will continue processing this request, executing all
        other middlewares until, finally, the appropriate downloader
        handler is called the request performed (and its response
        downloaded).

        If it returns a [[`Response`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal} object, Scrapy won't bother calling *any* other
        [[`process_request()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
        .internal} or [[`process_exception()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
        .internal} methods, or the appropriate download function; it'll
        return that response. The [[`process_response()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
        .internal} methods of installed middleware is always called on
        every response.

        If it returns a [`Request`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} object, Scrapy will stop calling
        [[`process_request()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
        .internal} methods and reschedule the returned request. Once the
        newly returned request is performed, the appropriate middleware
        chain will be called on the downloaded response.

        If it raises an [[`IgnoreRequest`{.xref .py .py-exc .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.exceptions.IgnoreRequest "scrapy.exceptions.IgnoreRequest"){.reference
        .internal} exception, the [[`process_exception()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
        .internal} methods of installed downloader middleware will be
        called. If none of them handle the exception, the errback
        function of the request ([`Request.errback`{.docutils .literal
        .notranslate}]{.pre}) is called. If no code handles the raised
        exception, it is ignored and not logged (unlike other
        exceptions).

        Parameters

        :   -   **request** ([`Request`{.xref .py .py-class .docutils
                .literal .notranslate}]{.pre} object) -- the request
                being processed

            -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider for which this request
                is intended

    [[process_response]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*, *[[response]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "Permalink to this definition"){.headerlink}

    :   [[`process_response()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
        .internal} should either: return a [[`Response`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal} object, return a [`Request`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre} object or raise a
        [[`IgnoreRequest`{.xref .py .py-exc .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.exceptions.IgnoreRequest "scrapy.exceptions.IgnoreRequest"){.reference
        .internal} exception.

        If it returns a [[`Response`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal} (it could be the same given response, or a brand-new
        one), that response will continue to be processed with the
        [[`process_response()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
        .internal} of the next middleware in the chain.

        If it returns a [`Request`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} object, the middleware chain is
        halted and the returned request is rescheduled to be downloaded
        in the future. This is the same behavior as if a request is
        returned from [[`process_request()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
        .internal}.

        If it raises an [[`IgnoreRequest`{.xref .py .py-exc .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.exceptions.IgnoreRequest "scrapy.exceptions.IgnoreRequest"){.reference
        .internal} exception, the errback function of the request
        ([`Request.errback`{.docutils .literal .notranslate}]{.pre}) is
        called. If no code handles the raised exception, it is ignored
        and not logged (unlike other exceptions).

        Parameters

        :   -   **request** (is a [`Request`{.xref .py .py-class
                .docutils .literal .notranslate}]{.pre} object) -- the
                request that originated the response

            -   **response** ([[`Response`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
                .internal} object) -- the response being processed

            -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider for which this response
                is intended

    [[process_exception]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*, *[[exception]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "Permalink to this definition"){.headerlink}

    :   Scrapy calls [[`process_exception()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
        .internal} when a download handler or a
        [[`process_request()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
        .internal} (from a downloader middleware) raises an exception
        (including an [[`IgnoreRequest`{.xref .py .py-exc .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.exceptions.IgnoreRequest "scrapy.exceptions.IgnoreRequest"){.reference
        .internal} exception)

        [[`process_exception()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
        .internal} should return: either [`None`{.docutils .literal
        .notranslate}]{.pre}, a [[`Response`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal} object, or a [`Request`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} object.

        If it returns [`None`{.docutils .literal .notranslate}]{.pre},
        Scrapy will continue processing this exception, executing any
        other [[`process_exception()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
        .internal} methods of installed middleware, until no middleware
        is left and the default exception handling kicks in.

        If it returns a [[`Response`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal} object, the [[`process_response()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
        .internal} method chain of installed middleware is started, and
        Scrapy won't bother calling any other
        [[`process_exception()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
        .internal} methods of middleware.

        If it returns a [`Request`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} object, the returned request is
        rescheduled to be downloaded in the future. This stops the
        execution of [[`process_exception()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
        .internal} methods of the middleware the same as returning a
        response would.

        Parameters

        :   -   **request** (is a [`Request`{.xref .py .py-class
                .docutils .literal .notranslate}]{.pre} object) -- the
                request that generated the exception

            -   **exception** (an [`Exception`{.docutils .literal
                .notranslate}]{.pre} object) -- the raised exception

            -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider for which this request
                is intended

    [[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[cls]{.pre}]{.n}*, *[[crawler]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.downloadermiddlewares.DownloaderMiddleware.from_crawler "Permalink to this definition"){.headerlink}

    :   If present, this classmethod is called to create a middleware
        instance from a [[`Crawler`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal}. It must return a new instance of the middleware.
        Crawler object provides access to all Scrapy core components
        like settings and signals; it is a way for middleware to access
        them and hook its functionality into Scrapy.

        Parameters

        :   **crawler** ([[`Crawler`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
            .internal} object) -- crawler that uses this middleware
:::

::: {#built-in-downloader-middleware-reference .section}
[]{#topics-downloader-middleware-ref}

#### Built-in downloader middleware reference[¶](#built-in-downloader-middleware-reference "Permalink to this heading"){.headerlink}

This page describes all downloader middleware components that come with
Scrapy. For information on how to use them and how to write your own
downloader middleware, see the [[downloader middleware usage guide]{.std
.std-ref}](#topics-downloader-middleware){.hoverxref .tooltip .reference
.internal}.

For a list of the components enabled by default (and their orders) see
the [[`DOWNLOADER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal} setting.

::: {#module-scrapy.downloadermiddlewares.cookies .section}
[]{#cookiesmiddleware}[]{#cookies-mw}

##### CookiesMiddleware[¶](#module-scrapy.downloadermiddlewares.cookies "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.cookies.]{.pre}]{.sig-prename .descclassname}[[CookiesMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/cookies.html#CookiesMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.cookies.CookiesMiddleware "Permalink to this definition"){.headerlink}

:   This middleware enables working with sites that require cookies,
    such as those that use sessions. It keeps track of cookies sent by
    web servers, and sends them back on subsequent requests (from that
    spider), just like web browsers do.

    ::: {.admonition .caution}
    Caution

    When non-UTF8 encoded byte sequences are passed to a
    [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}, the [`CookiesMiddleware`{.docutils .literal
    .notranslate}]{.pre} will log a warning. Refer to [[Advanced
    customization]{.std
    .std-ref}](index.html#topics-logging-advanced-customization){.hoverxref
    .tooltip .reference .internal} to customize the logging behaviour.
    :::

    ::: {.admonition .caution}
    Caution

    Cookies set via the [`Cookie`{.docutils .literal
    .notranslate}]{.pre} header are not considered by the
    [[CookiesMiddleware]{.std .std-ref}](#cookies-mw){.hoverxref
    .tooltip .reference .internal}. If you need to set cookies for a
    request, use the [`Request.cookies`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre} parameter. This is a known current
    limitation that is being worked on.
    :::

The following settings can be used to configure the cookie middleware:

-   [[`COOKIES_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-COOKIES_ENABLED){.hoverxref
    .tooltip .reference .internal}

-   [[`COOKIES_DEBUG`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-COOKIES_DEBUG){.hoverxref
    .tooltip .reference .internal}

::: {#multiple-cookie-sessions-per-spider .section}
[]{#std-reqmeta-cookiejar}

###### Multiple cookie sessions per spider[¶](#multiple-cookie-sessions-per-spider "Permalink to this heading"){.headerlink}

There is support for keeping multiple cookie sessions per spider by
using the [[`cookiejar`{.xref .std .std-reqmeta .docutils .literal
.notranslate}]{.pre}](#std-reqmeta-cookiejar){.hoverxref .tooltip
.reference .internal} Request meta key. By default it uses a single
cookie jar (session), but you can pass an identifier to use different
ones.

For example:

::: {.highlight-python .notranslate}
::: highlight
    for i, url in enumerate(urls):
        yield scrapy.Request(url, meta={"cookiejar": i}, callback=self.parse_page)
:::
:::

Keep in mind that the [[`cookiejar`{.xref .std .std-reqmeta .docutils
.literal .notranslate}]{.pre}](#std-reqmeta-cookiejar){.hoverxref
.tooltip .reference .internal} meta key is not "sticky". You need to
keep passing it along on subsequent requests. For example:

::: {.highlight-python .notranslate}
::: highlight
    def parse_page(self, response):
        # do some processing
        return scrapy.Request(
            "http://www.example.com/otherpage",
            meta={"cookiejar": response.meta["cookiejar"]},
            callback=self.parse_other_page,
        )
:::
:::
:::

::: {#cookies-enabled .section}
[]{#std-setting-COOKIES_ENABLED}

###### COOKIES_ENABLED[¶](#cookies-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether to enable the cookies middleware. If disabled, no cookies will
be sent to web servers.

Notice that despite the value of [[`COOKIES_ENABLED`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-COOKIES_ENABLED){.hoverxref .tooltip
.reference .internal} setting if [`Request.`{.docutils .literal
.notranslate}]{.pre}[[`meta['dont_merge_cookies']`{.xref .std
.std-reqmeta .docutils .literal
.notranslate}]{.pre}](index.html#std-reqmeta-dont_merge_cookies){.hoverxref
.tooltip .reference .internal} evaluates to [`True`{.docutils .literal
.notranslate}]{.pre} the request cookies will **not** be sent to the web
server and received cookies in [[`Response`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} will **not** be merged with the existing cookies.

For more detailed information see the [`cookies`{.docutils .literal
.notranslate}]{.pre} parameter in [`Request`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre}.
:::

::: {#cookies-debug .section}
[]{#std-setting-COOKIES_DEBUG}

###### COOKIES_DEBUG[¶](#cookies-debug "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

If enabled, Scrapy will log all cookies sent in requests (i.e.
[`Cookie`{.docutils .literal .notranslate}]{.pre} header) and all
cookies received in responses (i.e. [`Set-Cookie`{.docutils .literal
.notranslate}]{.pre} header).

Here's an example of a log with [[`COOKIES_DEBUG`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-COOKIES_DEBUG){.hoverxref .tooltip
.reference .internal} enabled:

::: {.highlight-default .notranslate}
::: highlight
    2011-04-06 14:35:10-0300 [scrapy.core.engine] INFO: Spider opened
    2011-04-06 14:35:10-0300 [scrapy.downloadermiddlewares.cookies] DEBUG: Sending cookies to: <GET http://www.diningcity.com/netherlands/index.html>
            Cookie: clientlanguage_nl=en_EN
    2011-04-06 14:35:14-0300 [scrapy.downloadermiddlewares.cookies] DEBUG: Received cookies from: <200 http://www.diningcity.com/netherlands/index.html>
            Set-Cookie: JSESSIONID=B~FA4DC0C496C8762AE4F1A620EAB34F38; Path=/
            Set-Cookie: ip_isocode=US
            Set-Cookie: clientlanguage_nl=en_EN; Expires=Thu, 07-Apr-2011 21:21:34 GMT; Path=/
    2011-04-06 14:49:50-0300 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://www.diningcity.com/netherlands/index.html> (referer: None)
    [...]
:::
:::
:::
:::

::: {#module-scrapy.downloadermiddlewares.defaultheaders .section}
[]{#defaultheadersmiddleware}

##### DefaultHeadersMiddleware[¶](#module-scrapy.downloadermiddlewares.defaultheaders "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.defaultheaders.]{.pre}]{.sig-prename .descclassname}[[DefaultHeadersMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/defaultheaders.html#DefaultHeadersMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware "Permalink to this definition"){.headerlink}

:   This middleware sets all default requests headers specified in the
    [[`DEFAULT_REQUEST_HEADERS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-DEFAULT_REQUEST_HEADERS){.hoverxref
    .tooltip .reference .internal} setting.
:::

::: {#module-scrapy.downloadermiddlewares.downloadtimeout .section}
[]{#downloadtimeoutmiddleware}

##### DownloadTimeoutMiddleware[¶](#module-scrapy.downloadermiddlewares.downloadtimeout "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.downloadtimeout.]{.pre}]{.sig-prename .descclassname}[[DownloadTimeoutMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/downloadtimeout.html#DownloadTimeoutMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.downloadtimeout.DownloadTimeoutMiddleware "Permalink to this definition"){.headerlink}

:   This middleware sets the download timeout for requests specified in
    the [[`DOWNLOAD_TIMEOUT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_TIMEOUT){.hoverxref
    .tooltip .reference .internal} setting or [`download_timeout`{.xref
    .py .py-attr .docutils .literal .notranslate}]{.pre} spider
    attribute.

::: {.admonition .note}
Note

You can also set download timeout per-request using
[[`download_timeout`{.xref .std .std-reqmeta .docutils .literal
.notranslate}]{.pre}](index.html#std-reqmeta-download_timeout){.hoverxref
.tooltip .reference .internal} Request.meta key; this is supported even
when DownloadTimeoutMiddleware is disabled.
:::
:::

::: {#module-scrapy.downloadermiddlewares.httpauth .section}
[]{#httpauthmiddleware}

##### HttpAuthMiddleware[¶](#module-scrapy.downloadermiddlewares.httpauth "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.httpauth.]{.pre}]{.sig-prename .descclassname}[[HttpAuthMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/httpauth.html#HttpAuthMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware "Permalink to this definition"){.headerlink}

:   This middleware authenticates all requests generated from certain
    spiders using [Basic access
    authentication](https://en.wikipedia.org/wiki/Basic_access_authentication){.reference
    .external} (aka. HTTP auth).

    To enable HTTP authentication for a spider, set the
    [`http_user`{.docutils .literal .notranslate}]{.pre} and
    [`http_pass`{.docutils .literal .notranslate}]{.pre} spider
    attributes to the authentication data and the
    [`http_auth_domain`{.docutils .literal .notranslate}]{.pre} spider
    attribute to the domain which requires this authentication (its
    subdomains will be also handled in the same way). You can set
    [`http_auth_domain`{.docutils .literal .notranslate}]{.pre} to
    [`None`{.docutils .literal .notranslate}]{.pre} to enable the
    authentication for all requests but you risk leaking your
    authentication credentials to unrelated domains.

    ::: {.admonition .warning}
    Warning

    In previous Scrapy versions HttpAuthMiddleware sent the
    authentication data with all requests, which is a security problem
    if the spider makes requests to several different domains. Currently
    if the [`http_auth_domain`{.docutils .literal .notranslate}]{.pre}
    attribute is not set, the middleware will use the domain of the
    first request, which will work for some spiders but not for others.
    In the future the middleware will produce an error instead.
    :::

    Example:

    ::: {.highlight-python .notranslate}
    ::: highlight
        from scrapy.spiders import CrawlSpider


        class SomeIntranetSiteSpider(CrawlSpider):
            http_user = "someuser"
            http_pass = "somepass"
            http_auth_domain = "intranet.example.com"
            name = "intranet.example.com"

            # .. rest of the spider code omitted ...
    :::
    :::
:::

::: {#module-scrapy.downloadermiddlewares.httpcache .section}
[]{#httpcachemiddleware}

##### HttpCacheMiddleware[¶](#module-scrapy.downloadermiddlewares.httpcache "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.httpcache.]{.pre}]{.sig-prename .descclassname}[[HttpCacheMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/httpcache.html#HttpCacheMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware "Permalink to this definition"){.headerlink}

:   This middleware provides low-level cache to all HTTP requests and
    responses. It has to be combined with a cache storage backend as
    well as a cache policy.

    Scrapy ships with the following HTTP cache storage backends:

    > <div>
    >
    > -   [[Filesystem storage backend (default)]{.std
    >     .std-ref}](#httpcache-storage-fs){.hoverxref .tooltip
    >     .reference .internal}
    >
    > -   [[DBM storage backend]{.std
    >     .std-ref}](#httpcache-storage-dbm){.hoverxref .tooltip
    >     .reference .internal}
    >
    > </div>

    You can change the HTTP cache storage backend with the
    [[`HTTPCACHE_STORAGE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-HTTPCACHE_STORAGE){.hoverxref
    .tooltip .reference .internal} setting. Or you can also [[implement
    your own storage backend.]{.std
    .std-ref}](#httpcache-storage-custom){.hoverxref .tooltip .reference
    .internal}

    Scrapy ships with two HTTP cache policies:

    > <div>
    >
    > -   [[RFC2616 policy]{.std
    >     .std-ref}](#httpcache-policy-rfc2616){.hoverxref .tooltip
    >     .reference .internal}
    >
    > -   [[Dummy policy (default)]{.std
    >     .std-ref}](#httpcache-policy-dummy){.hoverxref .tooltip
    >     .reference .internal}
    >
    > </div>

    You can change the HTTP cache policy with the
    [[`HTTPCACHE_POLICY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-HTTPCACHE_POLICY){.hoverxref
    .tooltip .reference .internal} setting. Or you can also implement
    your own policy.

    You can also avoid caching a response on every policy using
    [[`dont_cache`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](#std-reqmeta-dont_cache){.hoverxref .tooltip
    .reference .internal} meta key equals [`True`{.docutils .literal
    .notranslate}]{.pre}.

::: {#dummy-policy-default .section}
[]{#httpcache-policy-dummy}

###### Dummy policy (default)[¶](#dummy-policy-default "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.httpcache.]{.pre}]{.sig-prename .descclassname}[[DummyPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/httpcache.html#DummyPolicy){.reference .internal}[¶](#scrapy.extensions.httpcache.DummyPolicy "Permalink to this definition"){.headerlink}

:   This policy has no awareness of any HTTP Cache-Control directives.
    Every request and its corresponding response are cached. When the
    same request is seen again, the response is returned without
    transferring anything from the Internet.

    The Dummy policy is useful for testing spiders faster (without
    having to wait for downloads every time) and for trying your spider
    offline, when an Internet connection is not available. The goal is
    to be able to "replay" a spider run *exactly as it ran before*.
:::

::: {#rfc2616-policy .section}
[]{#httpcache-policy-rfc2616}

###### RFC2616 policy[¶](#rfc2616-policy "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.httpcache.]{.pre}]{.sig-prename .descclassname}[[RFC2616Policy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/httpcache.html#RFC2616Policy){.reference .internal}[¶](#scrapy.extensions.httpcache.RFC2616Policy "Permalink to this definition"){.headerlink}

:   This policy provides a RFC2616 compliant HTTP cache, i.e. with HTTP
    Cache-Control awareness, aimed at production and used in continuous
    runs to avoid downloading unmodified data (to save bandwidth and
    speed up crawls).

    What is implemented:

    -   Do not attempt to store responses/requests with
        [`no-store`{.docutils .literal .notranslate}]{.pre}
        cache-control directive set

    -   Do not serve responses from cache if [`no-cache`{.docutils
        .literal .notranslate}]{.pre} cache-control directive is set
        even for fresh responses

    -   Compute freshness lifetime from [`max-age`{.docutils .literal
        .notranslate}]{.pre} cache-control directive

    -   Compute freshness lifetime from [`Expires`{.docutils .literal
        .notranslate}]{.pre} response header

    -   Compute freshness lifetime from [`Last-Modified`{.docutils
        .literal .notranslate}]{.pre} response header (heuristic used by
        Firefox)

    -   Compute current age from [`Age`{.docutils .literal
        .notranslate}]{.pre} response header

    -   Compute current age from [`Date`{.docutils .literal
        .notranslate}]{.pre} header

    -   Revalidate stale responses based on [`Last-Modified`{.docutils
        .literal .notranslate}]{.pre} response header

    -   Revalidate stale responses based on [`ETag`{.docutils .literal
        .notranslate}]{.pre} response header

    -   Set [`Date`{.docutils .literal .notranslate}]{.pre} header for
        any received response missing it

    -   Support [`max-stale`{.docutils .literal .notranslate}]{.pre}
        cache-control directive in requests

    This allows spiders to be configured with the full RFC2616 cache
    policy, but avoid revalidation on a request-by-request basis, while
    remaining conformant with the HTTP spec.

    Example:

    Add [`Cache-Control:`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`max-stale=600`{.docutils .literal
    .notranslate}]{.pre} to Request headers to accept responses that
    have exceeded their expiration time by no more than 600 seconds.

    See also: RFC2616, 14.9.3

    What is missing:

    -   [`Pragma:`{.docutils .literal .notranslate}]{.pre}` `{.docutils
        .literal .notranslate}[`no-cache`{.docutils .literal
        .notranslate}]{.pre} support
        [https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9.1](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9.1){.reference
        .external}

    -   [`Vary`{.docutils .literal .notranslate}]{.pre} header support
        [https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.6](https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.6){.reference
        .external}

    -   Invalidation after updates or deletes
        [https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.10](https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.10){.reference
        .external}

    -   ... probably others ..
:::

::: {#filesystem-storage-backend-default .section}
[]{#httpcache-storage-fs}

###### Filesystem storage backend (default)[¶](#filesystem-storage-backend-default "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.httpcache.]{.pre}]{.sig-prename .descclassname}[[FilesystemCacheStorage]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/httpcache.html#FilesystemCacheStorage){.reference .internal}[¶](#scrapy.extensions.httpcache.FilesystemCacheStorage "Permalink to this definition"){.headerlink}

:   File system storage backend is available for the HTTP cache
    middleware.

    Each request/response pair is stored in a different directory
    containing the following files:

    -   [`request_body`{.docutils .literal .notranslate}]{.pre} - the
        plain request body

    -   [`request_headers`{.docutils .literal .notranslate}]{.pre} - the
        request headers (in raw HTTP format)

    -   [`response_body`{.docutils .literal .notranslate}]{.pre} - the
        plain response body

    -   [`response_headers`{.docutils .literal .notranslate}]{.pre} -
        the request headers (in raw HTTP format)

    -   [`meta`{.docutils .literal .notranslate}]{.pre} - some metadata
        of this cache resource in Python [`repr()`{.docutils .literal
        .notranslate}]{.pre} format (grep-friendly format)

    -   [`pickled_meta`{.docutils .literal .notranslate}]{.pre} - the
        same metadata in [`meta`{.docutils .literal .notranslate}]{.pre}
        but pickled for more efficient deserialization

    The directory name is made from the request fingerprint (see
    [`scrapy.utils.request.fingerprint`{.docutils .literal
    .notranslate}]{.pre}), and one level of subdirectories is used to
    avoid creating too many files into the same directory (which is
    inefficient in many file systems). An example directory could be:

    ::: {.highlight-default .notranslate}
    ::: highlight
        /path/to/cache/dir/example.com/72/72811f648e718090f041317756c03adb0ada46c7
    :::
    :::
:::

::: {#dbm-storage-backend .section}
[]{#httpcache-storage-dbm}

###### DBM storage backend[¶](#dbm-storage-backend "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.httpcache.]{.pre}]{.sig-prename .descclassname}[[DbmCacheStorage]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/httpcache.html#DbmCacheStorage){.reference .internal}[¶](#scrapy.extensions.httpcache.DbmCacheStorage "Permalink to this definition"){.headerlink}

:   A [DBM](https://en.wikipedia.org/wiki/Dbm){.reference .external}
    storage backend is also available for the HTTP cache middleware.

    By default, it uses the [[`dbm`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/dbm.html#module-dbm "(in Python v3.12)"){.reference
    .external}, but you can change it with the
    [[`HTTPCACHE_DBM_MODULE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-HTTPCACHE_DBM_MODULE){.hoverxref
    .tooltip .reference .internal} setting.
:::

::: {#writing-your-own-storage-backend .section}
[]{#httpcache-storage-custom}

###### Writing your own storage backend[¶](#writing-your-own-storage-backend "Permalink to this heading"){.headerlink}

You can implement a cache storage backend by creating a Python class
that defines the methods described below.

[]{#module-scrapy.extensions.httpcache .target}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.httpcache.]{.pre}]{.sig-prename .descclassname}[[CacheStorage]{.pre}]{.sig-name .descname}[¶](#scrapy.extensions.httpcache.CacheStorage "Permalink to this definition"){.headerlink}

:   

    [[open_spider]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.extensions.httpcache.CacheStorage.open_spider "Permalink to this definition"){.headerlink}

    :   This method gets called after a spider has been opened for
        crawling. It handles the [[`open_spider`{.xref .std .std-signal
        .docutils .literal
        .notranslate}]{.pre}](index.html#std-signal-spider_opened){.hoverxref
        .tooltip .reference .internal} signal.

        Parameters

        :   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which has been opened

    [[close_spider]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.extensions.httpcache.CacheStorage.close_spider "Permalink to this definition"){.headerlink}

    :   This method gets called after a spider has been closed. It
        handles the [[`close_spider`{.xref .std .std-signal .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-signal-spider_closed){.hoverxref
        .tooltip .reference .internal} signal.

        Parameters

        :   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which has been closed

    [[retrieve_response]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*, *[[request]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.extensions.httpcache.CacheStorage.retrieve_response "Permalink to this definition"){.headerlink}

    :   Return response if present in cache, or [`None`{.docutils
        .literal .notranslate}]{.pre} otherwise.

        Parameters

        :   -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider which generated the
                request

            -   **request** ([`Request`{.xref .py .py-class .docutils
                .literal .notranslate}]{.pre} object) -- the request to
                find cached response for

    [[store_response]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[response]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.extensions.httpcache.CacheStorage.store_response "Permalink to this definition"){.headerlink}

    :   Store the given response in the cache.

        Parameters

        :   -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider for which the response
                is intended

            -   **request** ([`Request`{.xref .py .py-class .docutils
                .literal .notranslate}]{.pre} object) -- the
                corresponding request the spider generated

            -   **response** ([[`Response`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
                .internal} object) -- the response to store in the cache

In order to use your storage backend, set:

-   [[`HTTPCACHE_STORAGE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-HTTPCACHE_STORAGE){.hoverxref
    .tooltip .reference .internal} to the Python import path of your
    custom storage class.
:::

::: {#httpcache-middleware-settings .section}
###### HTTPCache middleware settings[¶](#httpcache-middleware-settings "Permalink to this heading"){.headerlink}

The [`HttpCacheMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} can be configured through the following settings:

::: {#httpcache-enabled .section}
[]{#std-setting-HTTPCACHE_ENABLED}HTTPCACHE_ENABLED[¶](#httpcache-enabled "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Whether the HTTP cache will be enabled.
:::

::: {#httpcache-expiration-secs .section}
[]{#std-setting-HTTPCACHE_EXPIRATION_SECS}HTTPCACHE_EXPIRATION_SECS[¶](#httpcache-expiration-secs "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

Expiration time for cached requests, in seconds.

Cached requests older than this time will be re-downloaded. If zero,
cached requests will never expire.
:::

::: {#httpcache-dir .section}
[]{#std-setting-HTTPCACHE_DIR}HTTPCACHE_DIR[¶](#httpcache-dir "Permalink to this heading"){.headerlink}

Default: [`'httpcache'`{.docutils .literal .notranslate}]{.pre}

The directory to use for storing the (low-level) HTTP cache. If empty,
the HTTP cache will be disabled. If a relative path is given, is taken
relative to the project data dir. For more info see: [[Default structure
of Scrapy projects]{.std
.std-ref}](index.html#topics-project-structure){.hoverxref .tooltip
.reference .internal}.
:::

::: {#httpcache-ignore-http-codes .section}
[]{#std-setting-HTTPCACHE_IGNORE_HTTP_CODES}HTTPCACHE_IGNORE_HTTP_CODES[¶](#httpcache-ignore-http-codes "Permalink to this heading"){.headerlink}

Default: [`[]`{.docutils .literal .notranslate}]{.pre}

Don't cache response with these HTTP codes.
:::

::: {#httpcache-ignore-missing .section}
[]{#std-setting-HTTPCACHE_IGNORE_MISSING}HTTPCACHE_IGNORE_MISSING[¶](#httpcache-ignore-missing "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

If enabled, requests not found in the cache will be ignored instead of
downloaded.
:::

::: {#httpcache-ignore-schemes .section}
[]{#std-setting-HTTPCACHE_IGNORE_SCHEMES}HTTPCACHE_IGNORE_SCHEMES[¶](#httpcache-ignore-schemes "Permalink to this heading"){.headerlink}

Default: [`['file']`{.docutils .literal .notranslate}]{.pre}

Don't cache responses with these URI schemes.
:::

::: {#httpcache-storage .section}
[]{#std-setting-HTTPCACHE_STORAGE}HTTPCACHE_STORAGE[¶](#httpcache-storage "Permalink to this heading"){.headerlink}

Default:
[`'scrapy.extensions.httpcache.FilesystemCacheStorage'`{.docutils
.literal .notranslate}]{.pre}

The class which implements the cache storage backend.
:::

::: {#httpcache-dbm-module .section}
[]{#std-setting-HTTPCACHE_DBM_MODULE}HTTPCACHE_DBM_MODULE[¶](#httpcache-dbm-module "Permalink to this heading"){.headerlink}

Default: [`'dbm'`{.docutils .literal .notranslate}]{.pre}

The database module to use in the [[DBM storage backend]{.std
.std-ref}](#httpcache-storage-dbm){.hoverxref .tooltip .reference
.internal}. This setting is specific to the DBM backend.
:::

::: {#httpcache-policy .section}
[]{#std-setting-HTTPCACHE_POLICY}HTTPCACHE_POLICY[¶](#httpcache-policy "Permalink to this heading"){.headerlink}

Default: [`'scrapy.extensions.httpcache.DummyPolicy'`{.docutils .literal
.notranslate}]{.pre}

The class which implements the cache policy.
:::

::: {#httpcache-gzip .section}
[]{#std-setting-HTTPCACHE_GZIP}HTTPCACHE_GZIP[¶](#httpcache-gzip "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

If enabled, will compress all cached data with gzip. This setting is
specific to the Filesystem backend.
:::

::: {#httpcache-always-store .section}
[]{#std-setting-HTTPCACHE_ALWAYS_STORE}HTTPCACHE_ALWAYS_STORE[¶](#httpcache-always-store "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

If enabled, will cache pages unconditionally.

A spider may wish to have all responses available in the cache, for
future use with [`Cache-Control:`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`max-stale`{.docutils .literal .notranslate}]{.pre}, for
instance. The DummyPolicy caches all responses but never revalidates
them, and sometimes a more nuanced policy is desirable.

This setting still respects [`Cache-Control:`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`no-store`{.docutils .literal .notranslate}]{.pre}
directives in responses. If you don't want that, filter
[`no-store`{.docutils .literal .notranslate}]{.pre} out of the
Cache-Control headers in responses you feed to the cache middleware.
:::

::: {#httpcache-ignore-response-cache-controls .section}
[]{#std-setting-HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS}HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS[¶](#httpcache-ignore-response-cache-controls "Permalink to this heading"){.headerlink}

Default: [`[]`{.docutils .literal .notranslate}]{.pre}

List of Cache-Control directives in responses to be ignored.

Sites often set "no-store", "no-cache", "must-revalidate", etc., but get
upset at the traffic a spider can generate if it actually respects those
directives. This allows to selectively ignore Cache-Control directives
that are known to be unimportant for the sites being crawled.

We assume that the spider will not issue Cache-Control directives in
requests unless it actually needs them, so directives in requests are
not filtered.
:::
:::
:::

::: {#module-scrapy.downloadermiddlewares.httpcompression .section}
[]{#httpcompressionmiddleware}

##### HttpCompressionMiddleware[¶](#module-scrapy.downloadermiddlewares.httpcompression "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.httpcompression.]{.pre}]{.sig-prename .descclassname}[[HttpCompressionMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/httpcompression.html#HttpCompressionMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware "Permalink to this definition"){.headerlink}

:   This middleware allows compressed (gzip, deflate) traffic to be
    sent/received from web sites.

    This middleware also supports decoding
    [brotli-compressed](https://www.ietf.org/rfc/rfc7932.txt){.reference
    .external} as well as
    [zstd-compressed](https://www.ietf.org/rfc/rfc8478.txt){.reference
    .external} responses, provided that
    [brotli](https://pypi.org/project/Brotli/){.reference .external} or
    [zstandard](https://pypi.org/project/zstandard/){.reference
    .external} is installed, respectively.

::: {#httpcompressionmiddleware-settings .section}
###### HttpCompressionMiddleware Settings[¶](#httpcompressionmiddleware-settings "Permalink to this heading"){.headerlink}

::: {#compression-enabled .section}
[]{#std-setting-COMPRESSION_ENABLED}COMPRESSION_ENABLED[¶](#compression-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether the Compression middleware will be enabled.
:::
:::
:::

::: {#module-scrapy.downloadermiddlewares.httpproxy .section}
[]{#httpproxymiddleware}

##### HttpProxyMiddleware[¶](#module-scrapy.downloadermiddlewares.httpproxy "Permalink to this heading"){.headerlink}

[]{#std-reqmeta-proxy .target}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.httpproxy.]{.pre}]{.sig-prename .descclassname}[[HttpProxyMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/httpproxy.html#HttpProxyMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "Permalink to this definition"){.headerlink}

:   This middleware sets the HTTP proxy to use for requests, by setting
    the [`proxy`{.docutils .literal .notranslate}]{.pre} meta value for
    [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} objects.

    Like the Python standard library module [[`urllib.request`{.xref .py
    .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/urllib.request.html#module-urllib.request "(in Python v3.12)"){.reference
    .external}, it obeys the following environment variables:

    -   [`http_proxy`{.docutils .literal .notranslate}]{.pre}

    -   [`https_proxy`{.docutils .literal .notranslate}]{.pre}

    -   [`no_proxy`{.docutils .literal .notranslate}]{.pre}

    You can also set the meta key [`proxy`{.docutils .literal
    .notranslate}]{.pre} per-request, to a value like
    [`http://some_proxy_server:port`{.docutils .literal
    .notranslate}]{.pre} or
    [`http://username:password@some_proxy_server:port`{.docutils
    .literal .notranslate}]{.pre}. Keep in mind this value will take
    precedence over [`http_proxy`{.docutils .literal
    .notranslate}]{.pre}/[`https_proxy`{.docutils .literal
    .notranslate}]{.pre} environment variables, and it will also ignore
    [`no_proxy`{.docutils .literal .notranslate}]{.pre} environment
    variable.
:::

::: {#module-scrapy.downloadermiddlewares.redirect .section}
[]{#redirectmiddleware}

##### RedirectMiddleware[¶](#module-scrapy.downloadermiddlewares.redirect "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.redirect.]{.pre}]{.sig-prename .descclassname}[[RedirectMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/redirect.html#RedirectMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.redirect.RedirectMiddleware "Permalink to this definition"){.headerlink}

:   This middleware handles redirection of requests based on response
    status.

The urls which the request goes through (while being redirected) can be
found in the [`redirect_urls`{.docutils .literal .notranslate}]{.pre}
[`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} key.

The reason behind each redirect in [[`redirect_urls`{.xref .std
.std-reqmeta .docutils .literal
.notranslate}]{.pre}](#std-reqmeta-redirect_urls){.hoverxref .tooltip
.reference .internal} can be found in the [`redirect_reasons`{.docutils
.literal .notranslate}]{.pre} [`Request.meta`{.xref .py .py-attr
.docutils .literal .notranslate}]{.pre} key. For example:
[`[301,`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`302,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`307,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`'meta`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`refresh']`{.docutils .literal .notranslate}]{.pre}.

The format of a reason depends on the middleware that handled the
corresponding redirect. For example, [[`RedirectMiddleware`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.redirect.RedirectMiddleware "scrapy.downloadermiddlewares.redirect.RedirectMiddleware"){.reference
.internal} indicates the triggering response status code as an integer,
while [[`MetaRefreshMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware "scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware"){.reference
.internal} always uses the [`'meta`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`refresh'`{.docutils .literal .notranslate}]{.pre} string
as reason.

The [[`RedirectMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.redirect.RedirectMiddleware "scrapy.downloadermiddlewares.redirect.RedirectMiddleware"){.reference
.internal} can be configured through the following settings (see the
settings documentation for more info):

-   [[`REDIRECT_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-REDIRECT_ENABLED){.hoverxref
    .tooltip .reference .internal}

-   [[`REDIRECT_MAX_TIMES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-REDIRECT_MAX_TIMES){.hoverxref
    .tooltip .reference .internal}

If [`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} has [`dont_redirect`{.docutils .literal
.notranslate}]{.pre} key set to True, the request will be ignored by
this middleware.

If you want to handle some redirect status codes in your spider, you can
specify these in the [`handle_httpstatus_list`{.docutils .literal
.notranslate}]{.pre} spider attribute.

For example, if you want the redirect middleware to ignore 301 and 302
responses (and pass them through to your spider) you can do this:

::: {.highlight-python .notranslate}
::: highlight
    class MySpider(CrawlSpider):
        handle_httpstatus_list = [301, 302]
:::
:::

The [`handle_httpstatus_list`{.docutils .literal .notranslate}]{.pre}
key of [`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} can also be used to specify which response codes to
allow on a per-request basis. You can also set the meta key
[`handle_httpstatus_all`{.docutils .literal .notranslate}]{.pre} to
[`True`{.docutils .literal .notranslate}]{.pre} if you want to allow any
response code for a request.

::: {#redirectmiddleware-settings .section}
###### RedirectMiddleware settings[¶](#redirectmiddleware-settings "Permalink to this heading"){.headerlink}

::: {#redirect-enabled .section}
[]{#std-setting-REDIRECT_ENABLED}REDIRECT_ENABLED[¶](#redirect-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether the Redirect middleware will be enabled.
:::

::: {#redirect-max-times .section}
[]{#std-setting-REDIRECT_MAX_TIMES}REDIRECT_MAX_TIMES[¶](#redirect-max-times "Permalink to this heading"){.headerlink}

Default: [`20`{.docutils .literal .notranslate}]{.pre}

The maximum number of redirections that will be followed for a single
request. After this maximum, the request's response is returned as is.
:::
:::
:::

::: {#metarefreshmiddleware .section}
##### MetaRefreshMiddleware[¶](#metarefreshmiddleware "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.redirect.]{.pre}]{.sig-prename .descclassname}[[MetaRefreshMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/redirect.html#MetaRefreshMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware "Permalink to this definition"){.headerlink}

:   This middleware handles redirection of requests based on
    meta-refresh html tag.

The [[`MetaRefreshMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware "scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware"){.reference
.internal} can be configured through the following settings (see the
settings documentation for more info):

-   [[`METAREFRESH_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-METAREFRESH_ENABLED){.hoverxref
    .tooltip .reference .internal}

-   [[`METAREFRESH_IGNORE_TAGS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-METAREFRESH_IGNORE_TAGS){.hoverxref
    .tooltip .reference .internal}

-   [[`METAREFRESH_MAXDELAY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-METAREFRESH_MAXDELAY){.hoverxref
    .tooltip .reference .internal}

This middleware obey [[`REDIRECT_MAX_TIMES`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-REDIRECT_MAX_TIMES){.hoverxref
.tooltip .reference .internal} setting, [[`dont_redirect`{.xref .std
.std-reqmeta .docutils .literal
.notranslate}]{.pre}](#std-reqmeta-dont_redirect){.hoverxref .tooltip
.reference .internal}, [[`redirect_urls`{.xref .std .std-reqmeta
.docutils .literal
.notranslate}]{.pre}](#std-reqmeta-redirect_urls){.hoverxref .tooltip
.reference .internal} and [[`redirect_reasons`{.xref .std .std-reqmeta
.docutils .literal
.notranslate}]{.pre}](#std-reqmeta-redirect_reasons){.hoverxref .tooltip
.reference .internal} request meta keys as described for
[[`RedirectMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.redirect.RedirectMiddleware "scrapy.downloadermiddlewares.redirect.RedirectMiddleware"){.reference
.internal}

::: {#metarefreshmiddleware-settings .section}
###### MetaRefreshMiddleware settings[¶](#metarefreshmiddleware-settings "Permalink to this heading"){.headerlink}

::: {#metarefresh-enabled .section}
[]{#std-setting-METAREFRESH_ENABLED}METAREFRESH_ENABLED[¶](#metarefresh-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether the Meta Refresh middleware will be enabled.
:::

::: {#metarefresh-ignore-tags .section}
[]{#std-setting-METAREFRESH_IGNORE_TAGS}METAREFRESH_IGNORE_TAGS[¶](#metarefresh-ignore-tags "Permalink to this heading"){.headerlink}

Default: [`[]`{.docutils .literal .notranslate}]{.pre}

Meta tags within these tags are ignored.

::: versionchanged
[Changed in version 2.0: ]{.versionmodified .changed}The default value
of [[`METAREFRESH_IGNORE_TAGS`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-METAREFRESH_IGNORE_TAGS){.hoverxref
.tooltip .reference .internal} changed from [`['script',`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`'noscript']`{.docutils .literal .notranslate}]{.pre} to
[`[]`{.docutils .literal .notranslate}]{.pre}.
:::
:::

::: {#metarefresh-maxdelay .section}
[]{#std-setting-METAREFRESH_MAXDELAY}METAREFRESH_MAXDELAY[¶](#metarefresh-maxdelay "Permalink to this heading"){.headerlink}

Default: [`100`{.docutils .literal .notranslate}]{.pre}

The maximum meta-refresh delay (in seconds) to follow the redirection.
Some sites use meta-refresh for redirecting to a session expired page,
so we restrict automatic redirection to the maximum delay.
:::
:::
:::

::: {#module-scrapy.downloadermiddlewares.retry .section}
[]{#retrymiddleware}

##### RetryMiddleware[¶](#module-scrapy.downloadermiddlewares.retry "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.retry.]{.pre}]{.sig-prename .descclassname}[[RetryMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/retry.html#RetryMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.retry.RetryMiddleware "Permalink to this definition"){.headerlink}

:   A middleware to retry failed requests that are potentially caused by
    temporary problems such as a connection timeout or HTTP 500 error.

Failed pages are collected on the scraping process and rescheduled at
the end, once the spider has finished crawling all regular (non failed)
pages.

The [[`RetryMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.retry.RetryMiddleware "scrapy.downloadermiddlewares.retry.RetryMiddleware"){.reference
.internal} can be configured through the following settings (see the
settings documentation for more info):

-   [[`RETRY_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-RETRY_ENABLED){.hoverxref
    .tooltip .reference .internal}

-   [[`RETRY_TIMES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-RETRY_TIMES){.hoverxref .tooltip
    .reference .internal}

-   [[`RETRY_HTTP_CODES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-RETRY_HTTP_CODES){.hoverxref
    .tooltip .reference .internal}

-   [[`RETRY_EXCEPTIONS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-RETRY_EXCEPTIONS){.hoverxref
    .tooltip .reference .internal}

If [`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} has [`dont_retry`{.docutils .literal
.notranslate}]{.pre} key set to True, the request will be ignored by
this middleware.

To retry requests from a spider callback, you can use the
[[`get_retry_request()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.retry.get_retry_request "scrapy.downloadermiddlewares.retry.get_retry_request"){.reference
.internal} function:

[[scrapy.downloadermiddlewares.retry.]{.pre}]{.sig-prename .descclassname}[[get_retry_request]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request:]{.pre} [\~scrapy.http.request.Request]{.pre}]{.n}*, *[[\*]{.pre}]{.n}*, *[[spider:]{.pre} [\~scrapy.spiders.Spider]{.pre}]{.n}*, *[[reason:]{.pre} [\~typing.Union\[str]{.pre}]{.n}*, *[[Exception]{.pre}]{.n}*, *[[\~typing.Type\[Exception\]\]]{.pre} [=]{.pre} [\'unspecified\']{.pre}]{.n}*, *[[max_retry_times:]{.pre} [\~typing.Optional\[int\]]{.pre} [=]{.pre} [None]{.pre}]{.n}*, *[[priority_adjust:]{.pre} [\~typing.Optional\[int\]]{.pre} [=]{.pre} [None]{.pre}]{.n}*, *[[logger:]{.pre} [\~logging.Logger]{.pre} [=]{.pre} [\<Logger]{.pre} [scrapy.downloadermiddlewares.retry]{.pre} [(WARNING)\>]{.pre}]{.n}*, *[[stats_base_key:]{.pre} [str]{.pre} [=]{.pre} [\'retry\']{.pre}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/retry.html#get_retry_request){.reference .internal}[¶](#scrapy.downloadermiddlewares.retry.get_retry_request "Permalink to this definition"){.headerlink}

:   Returns a new [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} object to retry the specified request, or
    [`None`{.docutils .literal .notranslate}]{.pre} if retries of the
    specified request have been exhausted.

    For example, in a [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
    .internal} callback, you could use it as follows:

    ::: {.highlight-default .notranslate}
    ::: highlight
        def parse(self, response):
            if not response.text:
                new_request_or_none = get_retry_request(
                    response.request,
                    spider=self,
                    reason='empty',
                )
                return new_request_or_none
    :::
    :::

    *spider* is the [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
    .internal} instance which is asking for the retry request. It is
    used to access the [[settings]{.std
    .std-ref}](index.html#topics-settings){.hoverxref .tooltip
    .reference .internal} and [[stats]{.std
    .std-ref}](index.html#topics-stats){.hoverxref .tooltip .reference
    .internal}, and to provide extra logging context (see
    [[`logging.debug()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/logging.html#logging.debug "(in Python v3.12)"){.reference
    .external}).

    *reason* is a string or an [[`Exception`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#Exception "(in Python v3.12)"){.reference
    .external} object that indicates the reason why the request needs to
    be retried. It is used to name retry stats.

    *max_retry_times* is a number that determines the maximum number of
    times that *request* can be retried. If not specified or
    [`None`{.docutils .literal .notranslate}]{.pre}, the number is read
    from the [[`max_retry_times`{.xref .std .std-reqmeta .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-max_retry_times){.hoverxref
    .tooltip .reference .internal} meta key of the request. If the
    [[`max_retry_times`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-max_retry_times){.hoverxref
    .tooltip .reference .internal} meta key is not defined or
    [`None`{.docutils .literal .notranslate}]{.pre}, the number is read
    from the [[`RETRY_TIMES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-RETRY_TIMES){.hoverxref .tooltip
    .reference .internal} setting.

    *priority_adjust* is a number that determines how the priority of
    the new request changes in relation to *request*. If not specified,
    the number is read from the [[`RETRY_PRIORITY_ADJUST`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-RETRY_PRIORITY_ADJUST){.hoverxref
    .tooltip .reference .internal} setting.

    *logger* is the logging.Logger object to be used when logging
    messages

    *stats_base_key* is a string to be used as the base key for the
    retry-related job stats

::: {#retrymiddleware-settings .section}
###### RetryMiddleware Settings[¶](#retrymiddleware-settings "Permalink to this heading"){.headerlink}

::: {#retry-enabled .section}
[]{#std-setting-RETRY_ENABLED}RETRY_ENABLED[¶](#retry-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether the Retry middleware will be enabled.
:::

::: {#retry-times .section}
[]{#std-setting-RETRY_TIMES}RETRY_TIMES[¶](#retry-times "Permalink to this heading"){.headerlink}

Default: [`2`{.docutils .literal .notranslate}]{.pre}

Maximum number of times to retry, in addition to the first download.

Maximum number of retries can also be specified per-request using
[[`max_retry_times`{.xref .std .std-reqmeta .docutils .literal
.notranslate}]{.pre}](index.html#std-reqmeta-max_retry_times){.hoverxref
.tooltip .reference .internal} attribute of [`Request.meta`{.xref .py
.py-attr .docutils .literal .notranslate}]{.pre}. When initialized, the
[[`max_retry_times`{.xref .std .std-reqmeta .docutils .literal
.notranslate}]{.pre}](index.html#std-reqmeta-max_retry_times){.hoverxref
.tooltip .reference .internal} meta key takes higher precedence over the
[[`RETRY_TIMES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-RETRY_TIMES){.hoverxref .tooltip
.reference .internal} setting.
:::

::: {#retry-http-codes .section}
[]{#std-setting-RETRY_HTTP_CODES}RETRY_HTTP_CODES[¶](#retry-http-codes "Permalink to this heading"){.headerlink}

Default: [`[500,`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`502,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`503,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`504,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`522,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`524,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`408,`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`429]`{.docutils .literal .notranslate}]{.pre}

Which HTTP response codes to retry. Other errors (DNS lookup issues,
connections lost, etc) are always retried.

In some cases you may want to add 400 to [[`RETRY_HTTP_CODES`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-RETRY_HTTP_CODES){.hoverxref .tooltip
.reference .internal} because it is a common code used to indicate
server overload. It is not included by default because HTTP specs say
so.
:::

::: {#retry-exceptions .section}
[]{#std-setting-RETRY_EXCEPTIONS}RETRY_EXCEPTIONS[¶](#retry-exceptions "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-default .notranslate}
::: highlight
    [
        'twisted.internet.defer.TimeoutError',
        'twisted.internet.error.TimeoutError',
        'twisted.internet.error.DNSLookupError',
        'twisted.internet.error.ConnectionRefusedError',
        'twisted.internet.error.ConnectionDone',
        'twisted.internet.error.ConnectError',
        'twisted.internet.error.ConnectionLost',
        'twisted.internet.error.TCPTimedOutError',
        'twisted.web.client.ResponseFailed',
        IOError,
        'scrapy.core.downloader.handlers.http11.TunnelError',
    ]
:::
:::

List of exceptions to retry.

Each list entry may be an exception type or its import path as a string.

An exception will not be caught when the exception type is not in
[[`RETRY_EXCEPTIONS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-RETRY_EXCEPTIONS){.hoverxref .tooltip
.reference .internal} or when the maximum number of retries for a
request has been exceeded (see [[`RETRY_TIMES`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-RETRY_TIMES){.hoverxref .tooltip
.reference .internal}). To learn about uncaught exception propagation,
see [[`process_exception()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
.internal}.
:::

::: {#retry-priority-adjust .section}
[]{#std-setting-RETRY_PRIORITY_ADJUST}RETRY_PRIORITY_ADJUST[¶](#retry-priority-adjust "Permalink to this heading"){.headerlink}

Default: [`-1`{.docutils .literal .notranslate}]{.pre}

Adjust retry request priority relative to original request:

-   a positive priority adjust means higher priority.

-   **a negative priority adjust (default) means lower priority.**
:::
:::
:::

::: {#module-scrapy.downloadermiddlewares.robotstxt .section}
[]{#robotstxtmiddleware}[]{#topics-dlmw-robots}

##### RobotsTxtMiddleware[¶](#module-scrapy.downloadermiddlewares.robotstxt "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.robotstxt.]{.pre}]{.sig-prename .descclassname}[[RobotsTxtMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/robotstxt.html#RobotsTxtMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware "Permalink to this definition"){.headerlink}

:   This middleware filters out requests forbidden by the robots.txt
    exclusion standard.

    To make sure Scrapy respects robots.txt make sure the middleware is
    enabled and the [[`ROBOTSTXT_OBEY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_OBEY){.hoverxref
    .tooltip .reference .internal} setting is enabled.

    The [[`ROBOTSTXT_USER_AGENT`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_USER_AGENT){.hoverxref
    .tooltip .reference .internal} setting can be used to specify the
    user agent string to use for matching in the
    [robots.txt](https://www.robotstxt.org/){.reference .external} file.
    If it is [`None`{.docutils .literal .notranslate}]{.pre}, the
    User-Agent header you are sending with the request or the
    [[`USER_AGENT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-USER_AGENT){.hoverxref
    .tooltip .reference .internal} setting (in that order) will be used
    for determining the user agent to use in the
    [robots.txt](https://www.robotstxt.org/){.reference .external} file.

    This middleware has to be combined with a
    [robots.txt](https://www.robotstxt.org/){.reference .external}
    parser.

    Scrapy ships with support for the following
    [robots.txt](https://www.robotstxt.org/){.reference .external}
    parsers:

    -   [[Protego]{.std .std-ref}](#protego-parser){.hoverxref .tooltip
        .reference .internal} (default)

    -   [[RobotFileParser]{.std
        .std-ref}](#python-robotfileparser){.hoverxref .tooltip
        .reference .internal}

    -   [[Robotexclusionrulesparser]{.std
        .std-ref}](#rerp-parser){.hoverxref .tooltip .reference
        .internal}

    -   [[Reppy]{.std .std-ref}](#reppy-parser){.hoverxref .tooltip
        .reference .internal} (deprecated)

    You can change the
    [robots.txt](https://www.robotstxt.org/){.reference .external}
    parser with the [[`ROBOTSTXT_PARSER`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_PARSER){.hoverxref
    .tooltip .reference .internal} setting. Or you can also [[implement
    support for a new parser]{.std
    .std-ref}](#support-for-new-robots-parser){.hoverxref .tooltip
    .reference .internal}.

If [`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} has [`dont_obey_robotstxt`{.docutils .literal
.notranslate}]{.pre} key set to True the request will be ignored by this
middleware even if [[`ROBOTSTXT_OBEY`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_OBEY){.hoverxref
.tooltip .reference .internal} is enabled.

Parsers vary in several aspects:

-   Language of implementation

-   Supported specification

-   Support for wildcard matching

-   Usage of [length based
    rule](https://developers.google.com/search/reference/robots_txt#order-of-precedence-for-group-member-lines){.reference
    .external}: in particular for [`Allow`{.docutils .literal
    .notranslate}]{.pre} and [`Disallow`{.docutils .literal
    .notranslate}]{.pre} directives, where the most specific rule based
    on the length of the path trumps the less specific (shorter) rule

Performance comparison of different parsers is available at [the
following link](https://github.com/scrapy/scrapy/issues/3969){.reference
.external}.

::: {#protego-parser .section}
[]{#id1}

###### Protego parser[¶](#protego-parser "Permalink to this heading"){.headerlink}

Based on [Protego](https://github.com/scrapy/protego){.reference
.external}:

-   implemented in Python

-   is compliant with [Google's Robots.txt
    Specification](https://developers.google.com/search/reference/robots_txt){.reference
    .external}

-   supports wildcard matching

-   uses the length based rule

Scrapy uses this parser by default.
:::

::: {#robotfileparser .section}
[]{#python-robotfileparser}

###### RobotFileParser[¶](#robotfileparser "Permalink to this heading"){.headerlink}

Based on [[`RobotFileParser`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/urllib.robotparser.html#urllib.robotparser.RobotFileParser "(in Python v3.12)"){.reference
.external}:

-   is Python's built-in
    [robots.txt](https://www.robotstxt.org/){.reference .external}
    parser

-   is compliant with [Martijn Koster's 1996 draft
    specification](https://www.robotstxt.org/norobots-rfc.txt){.reference
    .external}

-   lacks support for wildcard matching

-   doesn't use the length based rule

It is faster than Protego and backward-compatible with versions of
Scrapy before 1.8.0.

In order to use this parser, set:

-   [[`ROBOTSTXT_PARSER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_PARSER){.hoverxref
    .tooltip .reference .internal} to
    [`scrapy.robotstxt.PythonRobotParser`{.docutils .literal
    .notranslate}]{.pre}
:::

::: {#reppy-parser .section}
[]{#id2}

###### Reppy parser[¶](#reppy-parser "Permalink to this heading"){.headerlink}

Based on [Reppy](https://github.com/seomoz/reppy/){.reference
.external}:

-   is a Python wrapper around [Robots Exclusion Protocol Parser for
    C++](https://github.com/seomoz/rep-cpp){.reference .external}

-   is compliant with [Martijn Koster's 1996 draft
    specification](https://www.robotstxt.org/norobots-rfc.txt){.reference
    .external}

-   supports wildcard matching

-   uses the length based rule

Native implementation, provides better speed than Protego.

In order to use this parser:

-   Install [Reppy](https://github.com/seomoz/reppy/){.reference
    .external} by running [`pip`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`install`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`reppy`{.docutils .literal .notranslate}]{.pre}

    > <div>
    >
    > ::: {.admonition .warning}
    > Warning
    >
    > [Upstream issue
    > #122](https://github.com/seomoz/reppy/issues/122){.reference
    > .external} prevents reppy usage in Python 3.9+. Because of this
    > the Reppy parser is deprecated.
    > :::
    >
    > </div>

-   Set [[`ROBOTSTXT_PARSER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_PARSER){.hoverxref
    .tooltip .reference .internal} setting to
    [`scrapy.robotstxt.ReppyRobotParser`{.docutils .literal
    .notranslate}]{.pre}
:::

::: {#robotexclusionrulesparser .section}
[]{#rerp-parser}

###### Robotexclusionrulesparser[¶](#robotexclusionrulesparser "Permalink to this heading"){.headerlink}

Based on
[Robotexclusionrulesparser](http://nikitathespider.com/python/rerp/){.reference
.external}:

-   implemented in Python

-   is compliant with [Martijn Koster's 1996 draft
    specification](https://www.robotstxt.org/norobots-rfc.txt){.reference
    .external}

-   supports wildcard matching

-   doesn't use the length based rule

In order to use this parser:

-   Install
    [Robotexclusionrulesparser](http://nikitathespider.com/python/rerp/){.reference
    .external} by running [`pip`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`install`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`robotexclusionrulesparser`{.docutils .literal
    .notranslate}]{.pre}

-   Set [[`ROBOTSTXT_PARSER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_PARSER){.hoverxref
    .tooltip .reference .internal} setting to
    [`scrapy.robotstxt.RerpRobotParser`{.docutils .literal
    .notranslate}]{.pre}
:::

::: {#implementing-support-for-a-new-parser .section}
[]{#support-for-new-robots-parser}

###### Implementing support for a new parser[¶](#implementing-support-for-a-new-parser "Permalink to this heading"){.headerlink}

You can implement support for a new
[robots.txt](https://www.robotstxt.org/){.reference .external} parser by
subclassing the abstract base class [[`RobotParser`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.robotstxt.RobotParser "scrapy.robotstxt.RobotParser"){.reference
.internal} and implementing the methods described below.

[]{#module-scrapy.robotstxt .target}

*[class]{.pre}[ ]{.w}*[[scrapy.robotstxt.]{.pre}]{.sig-prename .descclassname}[[RobotParser]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/robotstxt.html#RobotParser){.reference .internal}[¶](#scrapy.robotstxt.RobotParser "Permalink to this definition"){.headerlink}

:   

    *[abstract]{.pre}[ ]{.w}*[[allowed]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*, *[[user_agent]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/robotstxt.html#RobotParser.allowed){.reference .internal}[¶](#scrapy.robotstxt.RobotParser.allowed "Permalink to this definition"){.headerlink}

    :   Return [`True`{.docutils .literal .notranslate}]{.pre} if
        [`user_agent`{.docutils .literal .notranslate}]{.pre} is allowed
        to crawl [`url`{.docutils .literal .notranslate}]{.pre},
        otherwise return [`False`{.docutils .literal
        .notranslate}]{.pre}.

        Parameters

        :   -   **url**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*bytes*](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
                .external}) -- Absolute URL

            -   **user_agent**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*bytes*](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
                .external}) -- User agent

    *[abstract]{.pre}[ ]{.w}[classmethod]{.pre}[ ]{.w}*[[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}]{.n}*, *[[robotstxt_body]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[Self]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/robotstxt.html#RobotParser.from_crawler){.reference .internal}[¶](#scrapy.robotstxt.RobotParser.from_crawler "Permalink to this definition"){.headerlink}

    :   Parse the content of a
        [robots.txt](https://www.robotstxt.org/){.reference .external}
        file as bytes. This must be a class method. It must return a new
        instance of the parser backend.

        Parameters

        :   -   **crawler** ([[`Crawler`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
                .internal} instance) -- crawler which made the request

            -   **robotstxt_body**
                ([*bytes*](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
                .external}) -- content of a
                [robots.txt](https://www.robotstxt.org/){.reference
                .external} file.
:::
:::

::: {#module-scrapy.downloadermiddlewares.stats .section}
[]{#downloaderstats}

##### DownloaderStats[¶](#module-scrapy.downloadermiddlewares.stats "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.stats.]{.pre}]{.sig-prename .descclassname}[[DownloaderStats]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/stats.html#DownloaderStats){.reference .internal}[¶](#scrapy.downloadermiddlewares.stats.DownloaderStats "Permalink to this definition"){.headerlink}

:   Middleware that stores stats of all requests, responses and
    exceptions that pass through it.

    To use this middleware you must enable the
    [[`DOWNLOADER_STATS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_STATS){.hoverxref
    .tooltip .reference .internal} setting.
:::

::: {#module-scrapy.downloadermiddlewares.useragent .section}
[]{#useragentmiddleware}

##### UserAgentMiddleware[¶](#module-scrapy.downloadermiddlewares.useragent "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.useragent.]{.pre}]{.sig-prename .descclassname}[[UserAgentMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/useragent.html#UserAgentMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.useragent.UserAgentMiddleware "Permalink to this definition"){.headerlink}

:   Middleware that allows spiders to override the default user agent.

    In order for a spider to override the default user agent, its
    [`user_agent`{.docutils .literal .notranslate}]{.pre} attribute must
    be set.
:::

::: {#module-scrapy.downloadermiddlewares.ajaxcrawl .section}
[]{#ajaxcrawlmiddleware}[]{#ajaxcrawl-middleware}

##### AjaxCrawlMiddleware[¶](#module-scrapy.downloadermiddlewares.ajaxcrawl "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.downloadermiddlewares.ajaxcrawl.]{.pre}]{.sig-prename .descclassname}[[AjaxCrawlMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/downloadermiddlewares/ajaxcrawl.html#AjaxCrawlMiddleware){.reference .internal}[¶](#scrapy.downloadermiddlewares.ajaxcrawl.AjaxCrawlMiddleware "Permalink to this definition"){.headerlink}

:   Middleware that finds 'AJAX crawlable' page variants based on
    meta-fragment html tag. See
    [https://developers.google.com/search/docs/ajax-crawling/docs/getting-started](https://developers.google.com/search/docs/ajax-crawling/docs/getting-started){.reference
    .external} for more info.

    ::: {.admonition .note}
    Note

    Scrapy finds 'AJAX crawlable' pages for URLs like
    [`'http://example.com/!#foo=bar'`{.docutils .literal
    .notranslate}]{.pre} even without this middleware.
    AjaxCrawlMiddleware is necessary when URL doesn't contain
    [`'!#'`{.docutils .literal .notranslate}]{.pre}. This is often a
    case for 'index' or 'main' website pages.
    :::

::: {#ajaxcrawlmiddleware-settings .section}
###### AjaxCrawlMiddleware Settings[¶](#ajaxcrawlmiddleware-settings "Permalink to this heading"){.headerlink}

::: {#ajaxcrawl-enabled .section}
[]{#std-setting-AJAXCRAWL_ENABLED}AJAXCRAWL_ENABLED[¶](#ajaxcrawl-enabled "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Whether the AjaxCrawlMiddleware will be enabled. You may want to enable
it for [[broad crawls]{.std
.std-ref}](index.html#topics-broad-crawls){.hoverxref .tooltip
.reference .internal}.
:::
:::

::: {#httpproxymiddleware-settings .section}
###### HttpProxyMiddleware settings[¶](#httpproxymiddleware-settings "Permalink to this heading"){.headerlink}

[]{#std-setting-HTTPPROXY_ENABLED .target}

::: {#httpproxy-enabled .section}
[]{#std-setting-HTTPPROXY_AUTH_ENCODING}HTTPPROXY_ENABLED[¶](#httpproxy-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether or not to enable the [`HttpProxyMiddleware`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre}.
:::

::: {#httpproxy-auth-encoding .section}
HTTPPROXY_AUTH_ENCODING[¶](#httpproxy-auth-encoding "Permalink to this heading"){.headerlink}

Default: [`"latin-1"`{.docutils .literal .notranslate}]{.pre}

The default encoding for proxy authentication on
[`HttpProxyMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}.
:::
:::
:::
:::
:::

[]{#document-topics/spider-middleware}

::: {#spider-middleware .section}
[]{#topics-spider-middleware}

### Spider Middleware[¶](#spider-middleware "Permalink to this heading"){.headerlink}

The spider middleware is a framework of hooks into Scrapy's spider
processing mechanism where you can plug custom functionality to process
the responses that are sent to [[Spiders]{.std
.std-ref}](index.html#topics-spiders){.hoverxref .tooltip .reference
.internal} for processing and to process the requests and items that are
generated from spiders.

::: {#activating-a-spider-middleware .section}
[]{#topics-spider-middleware-setting}

#### Activating a spider middleware[¶](#activating-a-spider-middleware "Permalink to this heading"){.headerlink}

To activate a spider middleware component, add it to the
[[`SPIDER_MIDDLEWARES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES){.hoverxref
.tooltip .reference .internal} setting, which is a dict whose keys are
the middleware class path and their values are the middleware orders.

Here's an example:

::: {.highlight-python .notranslate}
::: highlight
    SPIDER_MIDDLEWARES = {
        "myproject.middlewares.CustomSpiderMiddleware": 543,
    }
:::
:::

The [[`SPIDER_MIDDLEWARES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES){.hoverxref
.tooltip .reference .internal} setting is merged with the
[[`SPIDER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal} setting defined in Scrapy (and not meant
to be overridden) and then sorted by order to get the final sorted list
of enabled middlewares: the first middleware is the one closer to the
engine and the last is the one closer to the spider. In other words, the
[[`process_spider_input()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input"){.reference
.internal} method of each middleware will be invoked in increasing
middleware order (100, 200, 300, ...), and the
[[`process_spider_output()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
.internal} method of each middleware will be invoked in decreasing
order.

To decide which order to assign to your middleware see the
[[`SPIDER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal} setting and pick a value according to
where you want to insert the middleware. The order does matter because
each middleware performs a different action and your middleware could
depend on some previous (or subsequent) middleware being applied.

If you want to disable a builtin middleware (the ones defined in
[[`SPIDER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal}, and enabled by default) you must define
it in your project [[`SPIDER_MIDDLEWARES`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES){.hoverxref
.tooltip .reference .internal} setting and assign [`None`{.docutils
.literal .notranslate}]{.pre} as its value. For example, if you want to
disable the off-site middleware:

::: {.highlight-python .notranslate}
::: highlight
    SPIDER_MIDDLEWARES = {
        "myproject.middlewares.CustomSpiderMiddleware": 543,
        "scrapy.spidermiddlewares.offsite.OffsiteMiddleware": None,
    }
:::
:::

Finally, keep in mind that some middlewares may need to be enabled
through a particular setting. See each middleware documentation for more
info.
:::

::: {#writing-your-own-spider-middleware .section}
[]{#custom-spider-middleware}

#### Writing your own spider middleware[¶](#writing-your-own-spider-middleware "Permalink to this heading"){.headerlink}

Each spider middleware is a Python class that defines one or more of the
methods defined below.

The main entry point is the [`from_crawler`{.docutils .literal
.notranslate}]{.pre} class method, which receives a [[`Crawler`{.xref
.py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
.internal} instance. The [[`Crawler`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
.internal} object gives you access, for example, to the [[settings]{.std
.std-ref}](index.html#topics-settings){.hoverxref .tooltip .reference
.internal}.

[]{#module-scrapy.spidermiddlewares .target}

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.]{.pre}]{.sig-prename .descclassname}[[SpiderMiddleware]{.pre}]{.sig-name .descname}[¶](#scrapy.spidermiddlewares.SpiderMiddleware "Permalink to this definition"){.headerlink}

:   

    [[process_spider_input]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input "Permalink to this definition"){.headerlink}

    :   This method is called for each response that goes through the
        spider middleware and into the spider, for processing.

        [[`process_spider_input()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input"){.reference
        .internal} should return [`None`{.docutils .literal
        .notranslate}]{.pre} or raise an exception.

        If it returns [`None`{.docutils .literal .notranslate}]{.pre},
        Scrapy will continue processing this response, executing all
        other middlewares until, finally, the response is handed to the
        spider for processing.

        If it raises an exception, Scrapy won't bother calling any other
        spider middleware [[`process_spider_input()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_input"){.reference
        .internal} and will call the request errback if there is one,
        otherwise it will start the [[`process_spider_exception()`{.xref
        .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception"){.reference
        .internal} chain. The output of the errback is chained back in
        the other direction for [[`process_spider_output()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
        .internal} to process it, or
        [[`process_spider_exception()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception"){.reference
        .internal} if it raised an exception.

        Parameters

        :   -   **response** ([[`Response`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
                .internal} object) -- the response being processed

            -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider for which this response
                is intended

    [[process_spider_output]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[result]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "Permalink to this definition"){.headerlink}

    :   This method is called with the results returned from the Spider,
        after it has processed the response.

        [[`process_spider_output()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
        .internal} must return an iterable of [`Request`{.xref .py
        .py-class .docutils .literal .notranslate}]{.pre} objects and
        [[item objects]{.std
        .std-ref}](index.html#topics-items){.hoverxref .tooltip
        .reference .internal}.

        ::: versionchanged
        [Changed in version 2.7: ]{.versionmodified .changed}This method
        may be defined as an [[asynchronous generator]{.xref .std
        .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-generator "(in Python v3.12)"){.reference
        .external}, in which case [`result`{.docutils .literal
        .notranslate}]{.pre} is an [[asynchronous iterable]{.xref .std
        .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-iterable "(in Python v3.12)"){.reference
        .external}.
        :::

        Consider defining this method as an [[asynchronous
        generator]{.xref .std
        .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-generator "(in Python v3.12)"){.reference
        .external}, which will be a requirement in a future version of
        Scrapy. However, if you plan on sharing your spider middleware
        with other people, consider either [[enforcing Scrapy 2.7]{.std
        .std-ref}](index.html#enforce-component-requirements){.hoverxref
        .tooltip .reference .internal} as a minimum requirement of your
        spider middleware, or [[making your spider middleware
        universal]{.std
        .std-ref}](index.html#universal-spider-middleware){.hoverxref
        .tooltip .reference .internal} so that it works with Scrapy
        versions earlier than Scrapy 2.7.

        Parameters

        :   -   **response** ([[`Response`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
                .internal} object) -- the response which generated this
                output from the spider

            -   **result** (an iterable of [`Request`{.xref .py
                .py-class .docutils .literal .notranslate}]{.pre}
                objects and [[item objects]{.std
                .std-ref}](index.html#topics-items){.hoverxref .tooltip
                .reference .internal}) -- the result returned by the
                spider

            -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider whose result is being
                processed

    [[process_spider_output_async]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[result]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output_async "Permalink to this definition"){.headerlink}

    :   ::: versionadded
        [New in version 2.7.]{.versionmodified .added}
        :::

        If defined, this method must be an [[asynchronous
        generator]{.xref .std
        .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-generator "(in Python v3.12)"){.reference
        .external}, which will be called instead of
        [[`process_spider_output()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
        .internal} if [`result`{.docutils .literal .notranslate}]{.pre}
        is an [[asynchronous iterable]{.xref .std
        .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-iterable "(in Python v3.12)"){.reference
        .external}.

    [[process_spider_exception]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[exception]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception "Permalink to this definition"){.headerlink}

    :   This method is called when a spider or
        [[`process_spider_output()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
        .internal} method (from a previous spider middleware) raises an
        exception.

        [[`process_spider_exception()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception"){.reference
        .internal} should return either [`None`{.docutils .literal
        .notranslate}]{.pre} or an iterable of [`Request`{.xref .py
        .py-class .docutils .literal .notranslate}]{.pre} or
        [[item]{.std .std-ref}](index.html#topics-items){.hoverxref
        .tooltip .reference .internal} objects.

        If it returns [`None`{.docutils .literal .notranslate}]{.pre},
        Scrapy will continue processing this exception, executing any
        other [[`process_spider_exception()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception"){.reference
        .internal} in the following middleware components, until no
        middleware components are left and the exception reaches the
        engine (where it's logged and discarded).

        If it returns an iterable the [[`process_spider_output()`{.xref
        .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
        .internal} pipeline kicks in, starting from the next spider
        middleware, and no other [[`process_spider_exception()`{.xref
        .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception"){.reference
        .internal} will be called.

        Parameters

        :   -   **response** ([[`Response`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
                .internal} object) -- the response being processed when
                the exception was raised

            -   **exception** ([[`Exception`{.xref .py .py-exc .docutils
                .literal
                .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#Exception "(in Python v3.12)"){.reference
                .external} object) -- the exception raised

            -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider which raised the
                exception

    [[process_start_requests]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[start_requests]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.spidermiddlewares.SpiderMiddleware.process_start_requests "Permalink to this definition"){.headerlink}

    :   This method is called with the start requests of the spider, and
        works similarly to the [[`process_spider_output()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
        .internal} method, except that it doesn't have a response
        associated and must return only requests (not items).

        It receives an iterable (in the [`start_requests`{.docutils
        .literal .notranslate}]{.pre} parameter) and must return another
        iterable of [`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre} objects.

        ::: {.admonition .note}
        Note

        When implementing this method in your spider middleware, you
        should always return an iterable (that follows the input one)
        and not consume all [`start_requests`{.docutils .literal
        .notranslate}]{.pre} iterator because it can be very large (or
        even unbounded) and cause a memory overflow. The Scrapy engine
        is designed to pull start requests while it has capacity to
        process them, so the start requests iterator can be effectively
        endless where there is some other condition for stopping the
        spider (like a time limit or item/page count).
        :::

        Parameters

        :   -   **start_requests** (an iterable of [`Request`{.xref .py
                .py-class .docutils .literal .notranslate}]{.pre}) --
                the start requests

            -   **spider** ([[`Spider`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
                .internal} object) -- the spider to whom the start
                requests belong

    [[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[cls]{.pre}]{.n}*, *[[crawler]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.spidermiddlewares.SpiderMiddleware.from_crawler "Permalink to this definition"){.headerlink}

    :   If present, this classmethod is called to create a middleware
        instance from a [[`Crawler`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal}. It must return a new instance of the middleware.
        Crawler object provides access to all Scrapy core components
        like settings and signals; it is a way for middleware to access
        them and hook its functionality into Scrapy.

        Parameters

        :   **crawler** ([[`Crawler`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
            .internal} object) -- crawler that uses this middleware
:::

::: {#built-in-spider-middleware-reference .section}
[]{#topics-spider-middleware-ref}

#### Built-in spider middleware reference[¶](#built-in-spider-middleware-reference "Permalink to this heading"){.headerlink}

This page describes all spider middleware components that come with
Scrapy. For information on how to use them and how to write your own
spider middleware, see the [[spider middleware usage guide]{.std
.std-ref}](#topics-spider-middleware){.hoverxref .tooltip .reference
.internal}.

For a list of the components enabled by default (and their orders) see
the [[`SPIDER_MIDDLEWARES_BASE`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES_BASE){.hoverxref
.tooltip .reference .internal} setting.

::: {#module-scrapy.spidermiddlewares.depth .section}
[]{#depthmiddleware}

##### DepthMiddleware[¶](#module-scrapy.spidermiddlewares.depth "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.depth.]{.pre}]{.sig-prename .descclassname}[[DepthMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/depth.html#DepthMiddleware){.reference .internal}[¶](#scrapy.spidermiddlewares.depth.DepthMiddleware "Permalink to this definition"){.headerlink}

:   DepthMiddleware is used for tracking the depth of each Request
    inside the site being scraped. It works by setting
    [`request.meta['depth']`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`=`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`0`{.docutils .literal .notranslate}]{.pre} whenever
    there is no value previously set (usually just the first Request)
    and incrementing it by 1 otherwise.

    It can be used to limit the maximum depth to scrape, control Request
    priority based on their depth, and things like that.

    The [[`DepthMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.spidermiddlewares.depth.DepthMiddleware "scrapy.spidermiddlewares.depth.DepthMiddleware"){.reference
    .internal} can be configured through the following settings (see the
    settings documentation for more info):

    > <div>
    >
    > -   [[`DEPTH_LIMIT`{.xref .std .std-setting .docutils .literal
    >     .notranslate}]{.pre}](index.html#std-setting-DEPTH_LIMIT){.hoverxref
    >     .tooltip .reference .internal} - The maximum depth that will
    >     be allowed to crawl for any site. If zero, no limit will be
    >     imposed.
    >
    > -   [[`DEPTH_STATS_VERBOSE`{.xref .std .std-setting .docutils
    >     .literal
    >     .notranslate}]{.pre}](index.html#std-setting-DEPTH_STATS_VERBOSE){.hoverxref
    >     .tooltip .reference .internal} - Whether to collect the number
    >     of requests for each depth.
    >
    > -   [[`DEPTH_PRIORITY`{.xref .std .std-setting .docutils .literal
    >     .notranslate}]{.pre}](index.html#std-setting-DEPTH_PRIORITY){.hoverxref
    >     .tooltip .reference .internal} - Whether to prioritize the
    >     requests based on their depth.
    >
    > </div>
:::

::: {#module-scrapy.spidermiddlewares.httperror .section}
[]{#httperrormiddleware}

##### HttpErrorMiddleware[¶](#module-scrapy.spidermiddlewares.httperror "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.httperror.]{.pre}]{.sig-prename .descclassname}[[HttpErrorMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/httperror.html#HttpErrorMiddleware){.reference .internal}[¶](#scrapy.spidermiddlewares.httperror.HttpErrorMiddleware "Permalink to this definition"){.headerlink}

:   Filter out unsuccessful (erroneous) HTTP responses so that spiders
    don't have to deal with them, which (most of the time) imposes an
    overhead, consumes more resources, and makes the spider logic more
    complex.

According to the [HTTP
standard](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html){.reference
.external}, successful responses are those whose status codes are in the
200-300 range.

If you still want to process response codes outside that range, you can
specify which response codes the spider is able to handle using the
[`handle_httpstatus_list`{.docutils .literal .notranslate}]{.pre} spider
attribute or [[`HTTPERROR_ALLOWED_CODES`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-HTTPERROR_ALLOWED_CODES){.hoverxref
.tooltip .reference .internal} setting.

For example, if you want your spider to handle 404 responses you can do
this:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import CrawlSpider


    class MySpider(CrawlSpider):
        handle_httpstatus_list = [404]
:::
:::

[]{#std-reqmeta-handle_httpstatus_list .target}

The [`handle_httpstatus_list`{.docutils .literal .notranslate}]{.pre}
key of [`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} can also be used to specify which response codes to
allow on a per-request basis. You can also set the meta key
[`handle_httpstatus_all`{.docutils .literal .notranslate}]{.pre} to
[`True`{.docutils .literal .notranslate}]{.pre} if you want to allow any
response code for a request, and [`False`{.docutils .literal
.notranslate}]{.pre} to disable the effects of the
[`handle_httpstatus_all`{.docutils .literal .notranslate}]{.pre} key.

Keep in mind, however, that it's usually a bad idea to handle non-200
responses, unless you really know what you're doing.

For more information see: [HTTP Status Code
Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html){.reference
.external}.

::: {#httperrormiddleware-settings .section}
###### HttpErrorMiddleware settings[¶](#httperrormiddleware-settings "Permalink to this heading"){.headerlink}

::: {#httperror-allowed-codes .section}
[]{#std-setting-HTTPERROR_ALLOWED_CODES}HTTPERROR_ALLOWED_CODES[¶](#httperror-allowed-codes "Permalink to this heading"){.headerlink}

Default: [`[]`{.docutils .literal .notranslate}]{.pre}

Pass all responses with non-200 status codes contained in this list.
:::

::: {#httperror-allow-all .section}
[]{#std-setting-HTTPERROR_ALLOW_ALL}HTTPERROR_ALLOW_ALL[¶](#httperror-allow-all "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Pass all responses, regardless of its status code.
:::
:::
:::

::: {#module-scrapy.spidermiddlewares.offsite .section}
[]{#offsitemiddleware}

##### OffsiteMiddleware[¶](#module-scrapy.spidermiddlewares.offsite "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.offsite.]{.pre}]{.sig-prename .descclassname}[[OffsiteMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/offsite.html#OffsiteMiddleware){.reference .internal}[¶](#scrapy.spidermiddlewares.offsite.OffsiteMiddleware "Permalink to this definition"){.headerlink}

:   Filters out Requests for URLs outside the domains covered by the
    spider.

    This middleware filters out every request whose host names aren't in
    the spider's [[`allowed_domains`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.allowed_domains "scrapy.Spider.allowed_domains"){.reference
    .internal} attribute. All subdomains of any domain in the list are
    also allowed. E.g. the rule [`www.example.org`{.docutils .literal
    .notranslate}]{.pre} will also allow
    [`bob.www.example.org`{.docutils .literal .notranslate}]{.pre} but
    not [`www2.example.com`{.docutils .literal .notranslate}]{.pre} nor
    [`example.com`{.docutils .literal .notranslate}]{.pre}.

    When your spider returns a request for a domain not belonging to
    those covered by the spider, this middleware will log a debug
    message similar to this one:

    ::: {.highlight-default .notranslate}
    ::: highlight
        DEBUG: Filtered offsite request to 'www.othersite.com': <GET http://www.othersite.com/some/page.html>
    :::
    :::

    To avoid filling the log with too much noise, it will only print one
    of these messages for each new domain filtered. So, for example, if
    another request for [`www.othersite.com`{.docutils .literal
    .notranslate}]{.pre} is filtered, no log message will be printed.
    But if a request for [`someothersite.com`{.docutils .literal
    .notranslate}]{.pre} is filtered, a message will be printed (but
    only for the first request filtered).

    If the spider doesn't define an [[`allowed_domains`{.xref .py
    .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.allowed_domains "scrapy.Spider.allowed_domains"){.reference
    .internal} attribute, or the attribute is empty, the offsite
    middleware will allow all requests.

    If the request has the [`dont_filter`{.xref .py .py-attr .docutils
    .literal .notranslate}]{.pre} attribute set, the offsite middleware
    will allow the request even if its domain is not listed in allowed
    domains.
:::

::: {#module-scrapy.spidermiddlewares.referer .section}
[]{#referermiddleware}

##### RefererMiddleware[¶](#module-scrapy.spidermiddlewares.referer "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[RefererMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#RefererMiddleware){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.RefererMiddleware "Permalink to this definition"){.headerlink}

:   Populates Request [`Referer`{.docutils .literal .notranslate}]{.pre}
    header, based on the URL of the Response which generated it.

::: {#referermiddleware-settings .section}
###### RefererMiddleware settings[¶](#referermiddleware-settings "Permalink to this heading"){.headerlink}

::: {#referer-enabled .section}
[]{#std-setting-REFERER_ENABLED}REFERER_ENABLED[¶](#referer-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether to enable referer middleware.
:::

::: {#referrer-policy .section}
[]{#std-setting-REFERRER_POLICY}REFERRER_POLICY[¶](#referrer-policy "Permalink to this heading"){.headerlink}

Default:
[`'scrapy.spidermiddlewares.referer.DefaultReferrerPolicy'`{.docutils
.literal .notranslate}]{.pre}

[Referrer Policy](https://www.w3.org/TR/referrer-policy){.reference
.external} to apply when populating Request "Referer" header.

::: {.admonition .note}
Note

You can also set the Referrer Policy per request, using the special
[`"referrer_policy"`{.docutils .literal .notranslate}]{.pre}
[[Request.meta]{.std
.std-ref}](index.html#topics-request-meta){.hoverxref .tooltip
.reference .internal} key, with the same acceptable values as for the
[`REFERRER_POLICY`{.docutils .literal .notranslate}]{.pre} setting.
:::

::: {#acceptable-values-for-referrer-policy .section}
Acceptable values for
REFERRER_POLICY[¶](#acceptable-values-for-referrer-policy "Permalink to this heading"){.headerlink}

-   either a path to a
    [`scrapy.spidermiddlewares.referer.ReferrerPolicy`{.docutils
    .literal .notranslate}]{.pre} subclass --- a custom policy or one of
    the built-in ones (see classes below),

-   or one of the standard W3C-defined string values,

-   or the special [`"scrapy-default"`{.docutils .literal
    .notranslate}]{.pre}.

+-----------------------+----------------------------------------------+
| String value          | Class name (as a string)                     |
+=======================+==============================================+
| [`"scrap              | [[`scrapy.spidermidd                         |
| y-default"`{.docutils | lewares.referer.DefaultReferrerPolicy`{.xref |
| .literal              | .py .py-class .docutils .literal             |
| .notranslate}]{.pre}  | .notranslate}]                               |
| (default)             | {.pre}](#scrapy.spidermiddlewares.referer.De |
|                       | faultReferrerPolicy "scrapy.spidermiddleware |
|                       | s.referer.DefaultReferrerPolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["no-refer            | [[`scrapy.spide                              |
| rer"](https://www.w3. | rmiddlewares.referer.NoReferrerPolicy`{.xref |
| org/TR/referrer-polic | .py .py-class .docutils .literal             |
| y/#referrer-policy-no | .not                                         |
| -referrer){.reference | ranslate}]{.pre}](#scrapy.spidermiddlewares. |
| .external}            | referer.NoReferrerPolicy "scrapy.spidermiddl |
|                       | ewares.referer.NoReferrerPolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["no-referrer-when-   | [[`scrapy.spidermiddlewares.                 |
| downgrade"](https://w | referer.NoReferrerWhenDowngradePolicy`{.xref |
| ww.w3.org/TR/referrer | .py .py-class .docutils .literal             |
| -policy/#referrer-pol | .notranslate}]{.pre}](#scrapy.               |
| icy-no-referrer-when- | spidermiddlewares.referer.NoReferrerWhenDown |
| downgrade){.reference | gradePolicy "scrapy.spidermiddlewares.refere |
| .external}            | r.NoReferrerWhenDowngradePolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["same-ori            | [[`scrapy.spide                              |
| gin"](https://www.w3. | rmiddlewares.referer.SameOriginPolicy`{.xref |
| org/TR/referrer-polic | .py .py-class .docutils .literal             |
| y/#referrer-policy-sa | .not                                         |
| me-origin){.reference | ranslate}]{.pre}](#scrapy.spidermiddlewares. |
| .external}            | referer.SameOriginPolicy "scrapy.spidermiddl |
|                       | ewares.referer.SameOriginPolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["origin"](https://ww | [[`scrapy.s                                  |
| w.w3.org/TR/referrer- | pidermiddlewares.referer.OriginPolicy`{.xref |
| policy/#referrer-poli | .py .py-class .docutils .literal             |
| cy-origin){.reference | .notranslate}]{.pre}](#scrapy.spidermidd     |
| .external}            | lewares.referer.OriginPolicy "scrapy.spiderm |
|                       | iddlewares.referer.OriginPolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["strict-origi        | [[`scrapy.spiderm                            |
| n"](https://www.w3.or | iddlewares.referer.StrictOriginPolicy`{.xref |
| g/TR/referrer-policy/ | .py .py-class .docutils .literal             |
| #referrer-policy-stri | .notrans                                     |
| ct-origin){.reference | late}]{.pre}](#scrapy.spidermiddlewares.refe |
| .external}            | rer.StrictOriginPolicy "scrapy.spidermiddlew |
|                       | ares.referer.StrictOriginPolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["origin-when-c       | [[`scrapy.spidermiddleware                   |
| ross-origin"](https:/ | s.referer.OriginWhenCrossOriginPolicy`{.xref |
| /www.w3.org/TR/referr | .py .py-class .docutils .literal             |
| er-policy/#referrer-p | .notranslate}]{.pre}](#scr                   |
| olicy-origin-when-cro | apy.spidermiddlewares.referer.OriginWhenCros |
| ss-origin){.reference | sOriginPolicy "scrapy.spidermiddlewares.refe |
| .external}            | rer.OriginWhenCrossOriginPolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["strict              | [[`scrapy.spidermiddlewares.refe             |
| -origin-when-cross-or | rer.StrictOriginWhenCrossOriginPolicy`{.xref |
| igin"](https://www.w3 | .py .py-class .docutils .literal             |
| .org/TR/referrer-poli | .notranslate}]{.pre}](#scrapy.spidermi       |
| cy/#referrer-policy-s | ddlewares.referer.StrictOriginWhenCrossOrigi |
| trict-origin-when-cro | nPolicy "scrapy.spidermiddlewares.referer.St |
| ss-origin){.reference | rictOriginWhenCrossOriginPolicy"){.reference |
| .external}            | .internal}                                   |
+-----------------------+----------------------------------------------+
| ["unsafe              | [[`scrapy.spid                               |
| -url"](https://www.w3 | ermiddlewares.referer.UnsafeUrlPolicy`{.xref |
| .org/TR/referrer-poli | .py .py-class .docutils .literal             |
| cy/#referrer-policy-u | .n                                           |
| nsafe-url){.reference | otranslate}]{.pre}](#scrapy.spidermiddleware |
| .external}            | s.referer.UnsafeUrlPolicy "scrapy.spidermidd |
|                       | lewares.referer.UnsafeUrlPolicy"){.reference |
|                       | .internal}                                   |
+-----------------------+----------------------------------------------+

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[DefaultReferrerPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#DefaultReferrerPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.DefaultReferrerPolicy "Permalink to this definition"){.headerlink}

:   A variant of "no-referrer-when-downgrade", with the addition that
    "Referer" is not sent if the parent request was using
    [`file://`{.docutils .literal .notranslate}]{.pre} or
    [`s3://`{.docutils .literal .notranslate}]{.pre} scheme.

::: {.admonition .warning}
Warning

Scrapy's default referrer policy --- just like
["no-referrer-when-downgrade"](https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer-when-downgrade){.reference
.external}, the W3C-recommended value for browsers --- will send a
non-empty "Referer" header from any [`http(s)://`{.docutils .literal
.notranslate}]{.pre} to any [`https://`{.docutils .literal
.notranslate}]{.pre} URL, even if the domain is different.

["same-origin"](https://www.w3.org/TR/referrer-policy/#referrer-policy-same-origin){.reference
.external} may be a better choice if you want to remove referrer
information for cross-domain requests.
:::

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[NoReferrerPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#NoReferrerPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.NoReferrerPolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer](https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer){.reference
    .external}

    The simplest policy is "no-referrer", which specifies that no
    referrer information is to be sent along with requests made from a
    particular request client to any origin. The header will be omitted
    entirely.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[NoReferrerWhenDowngradePolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#NoReferrerWhenDowngradePolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.NoReferrerWhenDowngradePolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer-when-downgrade](https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer-when-downgrade){.reference
    .external}

    The "no-referrer-when-downgrade" policy sends a full URL along with
    requests from a TLS-protected environment settings object to a
    potentially trustworthy URL, and requests from clients which are not
    TLS-protected to any origin.

    Requests from TLS-protected clients to non-potentially trustworthy
    URLs, on the other hand, will contain no referrer information. A
    Referer HTTP header will not be sent.

    This is a user agent's default behavior, if no policy is otherwise
    specified.

::: {.admonition .note}
Note

"no-referrer-when-downgrade" policy is the W3C-recommended default, and
is used by major web browsers.

However, it is NOT Scrapy's default referrer policy (see
[[`DefaultReferrerPolicy`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.spidermiddlewares.referer.DefaultReferrerPolicy "scrapy.spidermiddlewares.referer.DefaultReferrerPolicy"){.reference
.internal}).
:::

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[SameOriginPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#SameOriginPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.SameOriginPolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-same-origin](https://www.w3.org/TR/referrer-policy/#referrer-policy-same-origin){.reference
    .external}

    The "same-origin" policy specifies that a full URL, stripped for use
    as a referrer, is sent as referrer information when making
    same-origin requests from a particular request client.

    Cross-origin requests, on the other hand, will contain no referrer
    information. A Referer HTTP header will not be sent.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[OriginPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#OriginPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.OriginPolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-origin](https://www.w3.org/TR/referrer-policy/#referrer-policy-origin){.reference
    .external}

    The "origin" policy specifies that only the ASCII serialization of
    the origin of the request client is sent as referrer information
    when making both same-origin requests and cross-origin requests from
    a particular request client.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[StrictOriginPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#StrictOriginPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.StrictOriginPolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-strict-origin](https://www.w3.org/TR/referrer-policy/#referrer-policy-strict-origin){.reference
    .external}

    The "strict-origin" policy sends the ASCII serialization of the
    origin of the request client when making requests: - from a
    TLS-protected environment settings object to a potentially
    trustworthy URL, and - from non-TLS-protected environment settings
    objects to any origin.

    Requests from TLS-protected request clients to non- potentially
    trustworthy URLs, on the other hand, will contain no referrer
    information. A Referer HTTP header will not be sent.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[OriginWhenCrossOriginPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#OriginWhenCrossOriginPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.OriginWhenCrossOriginPolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-origin-when-cross-origin](https://www.w3.org/TR/referrer-policy/#referrer-policy-origin-when-cross-origin){.reference
    .external}

    The "origin-when-cross-origin" policy specifies that a full URL,
    stripped for use as a referrer, is sent as referrer information when
    making same-origin requests from a particular request client, and
    only the ASCII serialization of the origin of the request client is
    sent as referrer information when making cross-origin requests from
    a particular request client.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[StrictOriginWhenCrossOriginPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#StrictOriginWhenCrossOriginPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.StrictOriginWhenCrossOriginPolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-strict-origin-when-cross-origin](https://www.w3.org/TR/referrer-policy/#referrer-policy-strict-origin-when-cross-origin){.reference
    .external}

    The "strict-origin-when-cross-origin" policy specifies that a full
    URL, stripped for use as a referrer, is sent as referrer information
    when making same-origin requests from a particular request client,
    and only the ASCII serialization of the origin of the request client
    when making cross-origin requests:

    -   from a TLS-protected environment settings object to a
        potentially trustworthy URL, and

    -   from non-TLS-protected environment settings objects to any
        origin.

    Requests from TLS-protected clients to non- potentially trustworthy
    URLs, on the other hand, will contain no referrer information. A
    Referer HTTP header will not be sent.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.referer.]{.pre}]{.sig-prename .descclassname}[[UnsafeUrlPolicy]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/referer.html#UnsafeUrlPolicy){.reference .internal}[¶](#scrapy.spidermiddlewares.referer.UnsafeUrlPolicy "Permalink to this definition"){.headerlink}

:   [https://www.w3.org/TR/referrer-policy/#referrer-policy-unsafe-url](https://www.w3.org/TR/referrer-policy/#referrer-policy-unsafe-url){.reference
    .external}

    The "unsafe-url" policy specifies that a full URL, stripped for use
    as a referrer, is sent along with both cross-origin requests and
    same-origin requests made from a particular request client.

    Note: The policy's name doesn't lie; it is unsafe. This policy will
    leak origins and paths from TLS-protected resources to insecure
    origins. Carefully consider the impact of setting such a policy for
    potentially sensitive documents.

::: {.admonition .warning}
Warning

"unsafe-url" policy is NOT recommended.
:::
:::
:::
:::
:::

::: {#module-scrapy.spidermiddlewares.urllength .section}
[]{#urllengthmiddleware}

##### UrlLengthMiddleware[¶](#module-scrapy.spidermiddlewares.urllength "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spidermiddlewares.urllength.]{.pre}]{.sig-prename .descclassname}[[UrlLengthMiddleware]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spidermiddlewares/urllength.html#UrlLengthMiddleware){.reference .internal}[¶](#scrapy.spidermiddlewares.urllength.UrlLengthMiddleware "Permalink to this definition"){.headerlink}

:   Filters out requests with URLs longer than URLLENGTH_LIMIT

    The [[`UrlLengthMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.spidermiddlewares.urllength.UrlLengthMiddleware "scrapy.spidermiddlewares.urllength.UrlLengthMiddleware"){.reference
    .internal} can be configured through the following settings (see the
    settings documentation for more info):

    > <div>
    >
    > -   [[`URLLENGTH_LIMIT`{.xref .std .std-setting .docutils .literal
    >     .notranslate}]{.pre}](index.html#std-setting-URLLENGTH_LIMIT){.hoverxref
    >     .tooltip .reference .internal} - The maximum URL length to
    >     allow for crawled URLs.
    >
    > </div>
:::
:::
:::

[]{#document-topics/extensions}

::: {#extensions .section}
[]{#topics-extensions}

### Extensions[¶](#extensions "Permalink to this heading"){.headerlink}

The extensions framework provides a mechanism for inserting your own
custom functionality into Scrapy.

Extensions are just regular classes.

::: {#extension-settings .section}
#### Extension settings[¶](#extension-settings "Permalink to this heading"){.headerlink}

Extensions use the [[Scrapy settings]{.std
.std-ref}](index.html#topics-settings){.hoverxref .tooltip .reference
.internal} to manage their settings, just like any other Scrapy code.

It is customary for extensions to prefix their settings with their own
name, to avoid collision with existing (and future) extensions. For
example, a hypothetical extension to handle [Google
Sitemaps](https://en.wikipedia.org/wiki/Sitemaps){.reference .external}
would use settings like [`GOOGLESITEMAP_ENABLED`{.docutils .literal
.notranslate}]{.pre}, [`GOOGLESITEMAP_DEPTH`{.docutils .literal
.notranslate}]{.pre}, and so on.
:::

::: {#loading-activating-extensions .section}
#### Loading & activating extensions[¶](#loading-activating-extensions "Permalink to this heading"){.headerlink}

Extensions are loaded and activated at startup by instantiating a single
instance of the extension class per spider being run. All the extension
initialization code must be performed in the class [`__init__`{.docutils
.literal .notranslate}]{.pre} method.

To make an extension available, add it to the [[`EXTENSIONS`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS){.hoverxref
.tooltip .reference .internal} setting in your Scrapy settings. In
[[`EXTENSIONS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS){.hoverxref
.tooltip .reference .internal}, each extension is represented by a
string: the full Python path to the extension's class name. For example:

::: {.highlight-python .notranslate}
::: highlight
    EXTENSIONS = {
        "scrapy.extensions.corestats.CoreStats": 500,
        "scrapy.extensions.telnet.TelnetConsole": 500,
    }
:::
:::

As you can see, the [[`EXTENSIONS`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS){.hoverxref
.tooltip .reference .internal} setting is a dict where the keys are the
extension paths, and their values are the orders, which define the
extension *loading* order. The [[`EXTENSIONS`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS){.hoverxref
.tooltip .reference .internal} setting is merged with the
[[`EXTENSIONS_BASE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS_BASE){.hoverxref
.tooltip .reference .internal} setting defined in Scrapy (and not meant
to be overridden) and then sorted by order to get the final sorted list
of enabled extensions.

As extensions typically do not depend on each other, their loading order
is irrelevant in most cases. This is why the [[`EXTENSIONS_BASE`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS_BASE){.hoverxref
.tooltip .reference .internal} setting defines all extensions with the
same order ([`0`{.docutils .literal .notranslate}]{.pre}). However, this
feature can be exploited if you need to add an extension which depends
on other extensions already loaded.
:::

::: {#available-enabled-and-disabled-extensions .section}
#### Available, enabled and disabled extensions[¶](#available-enabled-and-disabled-extensions "Permalink to this heading"){.headerlink}

Not all available extensions will be enabled. Some of them usually
depend on a particular setting. For example, the HTTP Cache extension is
available by default but disabled unless the [[`HTTPCACHE_ENABLED`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_ENABLED){.hoverxref
.tooltip .reference .internal} setting is set.
:::

::: {#disabling-an-extension .section}
#### Disabling an extension[¶](#disabling-an-extension "Permalink to this heading"){.headerlink}

In order to disable an extension that comes enabled by default (i.e.
those included in the [[`EXTENSIONS_BASE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS_BASE){.hoverxref
.tooltip .reference .internal} setting) you must set its order to
[`None`{.docutils .literal .notranslate}]{.pre}. For example:

::: {.highlight-python .notranslate}
::: highlight
    EXTENSIONS = {
        "scrapy.extensions.corestats.CoreStats": None,
    }
:::
:::
:::

::: {#writing-your-own-extension .section}
#### Writing your own extension[¶](#writing-your-own-extension "Permalink to this heading"){.headerlink}

Each extension is a Python class. The main entry point for a Scrapy
extension (this also includes middlewares and pipelines) is the
[`from_crawler`{.docutils .literal .notranslate}]{.pre} class method
which receives a [`Crawler`{.docutils .literal .notranslate}]{.pre}
instance. Through the Crawler object you can access settings, signals,
stats, and also control the crawling behaviour.

Typically, extensions connect to [[signals]{.std
.std-ref}](index.html#topics-signals){.hoverxref .tooltip .reference
.internal} and perform tasks triggered by them.

Finally, if the [`from_crawler`{.docutils .literal .notranslate}]{.pre}
method raises the [[`NotConfigured`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.NotConfigured "scrapy.exceptions.NotConfigured"){.reference
.internal} exception, the extension will be disabled. Otherwise, the
extension will be enabled.

::: {#sample-extension .section}
##### Sample extension[¶](#sample-extension "Permalink to this heading"){.headerlink}

Here we will implement a simple extension to illustrate the concepts
described in the previous section. This extension will log a message
every time:

-   a spider is opened

-   a spider is closed

-   a specific number of items are scraped

The extension will be enabled through the [`MYEXT_ENABLED`{.docutils
.literal .notranslate}]{.pre} setting and the number of items will be
specified through the [`MYEXT_ITEMCOUNT`{.docutils .literal
.notranslate}]{.pre} setting.

Here is the code of such extension:

::: {.highlight-python .notranslate}
::: highlight
    import logging
    from scrapy import signals
    from scrapy.exceptions import NotConfigured

    logger = logging.getLogger(__name__)


    class SpiderOpenCloseLogging:
        def __init__(self, item_count):
            self.item_count = item_count
            self.items_scraped = 0

        @classmethod
        def from_crawler(cls, crawler):
            # first check if the extension should be enabled and raise
            # NotConfigured otherwise
            if not crawler.settings.getbool("MYEXT_ENABLED"):
                raise NotConfigured

            # get the number of items from settings
            item_count = crawler.settings.getint("MYEXT_ITEMCOUNT", 1000)

            # instantiate the extension object
            ext = cls(item_count)

            # connect the extension object to signals
            crawler.signals.connect(ext.spider_opened, signal=signals.spider_opened)
            crawler.signals.connect(ext.spider_closed, signal=signals.spider_closed)
            crawler.signals.connect(ext.item_scraped, signal=signals.item_scraped)

            # return the extension object
            return ext

        def spider_opened(self, spider):
            logger.info("opened spider %s", spider.name)

        def spider_closed(self, spider):
            logger.info("closed spider %s", spider.name)

        def item_scraped(self, item, spider):
            self.items_scraped += 1
            if self.items_scraped % self.item_count == 0:
                logger.info("scraped %d items", self.items_scraped)
:::
:::
:::
:::

::: {#built-in-extensions-reference .section}
[]{#topics-extensions-ref}

#### Built-in extensions reference[¶](#built-in-extensions-reference "Permalink to this heading"){.headerlink}

::: {#general-purpose-extensions .section}
##### General purpose extensions[¶](#general-purpose-extensions "Permalink to this heading"){.headerlink}

::: {#module-scrapy.extensions.logstats .section}
[]{#log-stats-extension}

###### Log Stats extension[¶](#module-scrapy.extensions.logstats "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.logstats.]{.pre}]{.sig-prename .descclassname}[[LogStats]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/logstats.html#LogStats){.reference .internal}[¶](#scrapy.extensions.logstats.LogStats "Permalink to this definition"){.headerlink}

:   

Log basic stats like crawled pages and scraped items.
:::

::: {#module-scrapy.extensions.corestats .section}
[]{#core-stats-extension}

###### Core Stats extension[¶](#module-scrapy.extensions.corestats "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.corestats.]{.pre}]{.sig-prename .descclassname}[[CoreStats]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/corestats.html#CoreStats){.reference .internal}[¶](#scrapy.extensions.corestats.CoreStats "Permalink to this definition"){.headerlink}

:   

Enable the collection of core statistics, provided the stats collection
is enabled (see [[Stats Collection]{.std
.std-ref}](index.html#topics-stats){.hoverxref .tooltip .reference
.internal}).
:::

::: {#module-scrapy.extensions.telnet .section}
[]{#telnet-console-extension}[]{#topics-extensions-ref-telnetconsole}

###### Telnet console extension[¶](#module-scrapy.extensions.telnet "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.telnet.]{.pre}]{.sig-prename .descclassname}[[TelnetConsole]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/telnet.html#TelnetConsole){.reference .internal}[¶](#scrapy.extensions.telnet.TelnetConsole "Permalink to this definition"){.headerlink}

:   

Provides a telnet console for getting into a Python interpreter inside
the currently running Scrapy process, which can be very useful for
debugging.

The telnet console must be enabled by the
[[`TELNETCONSOLE_ENABLED`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-TELNETCONSOLE_ENABLED){.hoverxref
.tooltip .reference .internal} setting, and the server will listen in
the port specified in [[`TELNETCONSOLE_PORT`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-TELNETCONSOLE_PORT){.hoverxref
.tooltip .reference .internal}.
:::

::: {#module-scrapy.extensions.memusage .section}
[]{#memory-usage-extension}[]{#topics-extensions-ref-memusage}

###### Memory usage extension[¶](#module-scrapy.extensions.memusage "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.memusage.]{.pre}]{.sig-prename .descclassname}[[MemoryUsage]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/memusage.html#MemoryUsage){.reference .internal}[¶](#scrapy.extensions.memusage.MemoryUsage "Permalink to this definition"){.headerlink}

:   

::: {.admonition .note}
Note

This extension does not work in Windows.
:::

Monitors the memory used by the Scrapy process that runs the spider and:

1.  sends a notification e-mail when it exceeds a certain value

2.  closes the spider when it exceeds a certain value

The notification e-mails can be triggered when a certain warning value
is reached ([[`MEMUSAGE_WARNING_MB`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_WARNING_MB){.hoverxref
.tooltip .reference .internal}) and when the maximum value is reached
([[`MEMUSAGE_LIMIT_MB`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_LIMIT_MB){.hoverxref
.tooltip .reference .internal}) which will also cause the spider to be
closed and the Scrapy process to be terminated.

This extension is enabled by the [[`MEMUSAGE_ENABLED`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_ENABLED){.hoverxref
.tooltip .reference .internal} setting and can be configured with the
following settings:

-   [[`MEMUSAGE_LIMIT_MB`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_LIMIT_MB){.hoverxref
    .tooltip .reference .internal}

-   [[`MEMUSAGE_WARNING_MB`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_WARNING_MB){.hoverxref
    .tooltip .reference .internal}

-   [[`MEMUSAGE_NOTIFY_MAIL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_NOTIFY_MAIL){.hoverxref
    .tooltip .reference .internal}

-   [[`MEMUSAGE_CHECK_INTERVAL_SECONDS`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_CHECK_INTERVAL_SECONDS){.hoverxref
    .tooltip .reference .internal}
:::

::: {#module-scrapy.extensions.memdebug .section}
[]{#memory-debugger-extension}

###### Memory debugger extension[¶](#module-scrapy.extensions.memdebug "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.memdebug.]{.pre}]{.sig-prename .descclassname}[[MemoryDebugger]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/memdebug.html#MemoryDebugger){.reference .internal}[¶](#scrapy.extensions.memdebug.MemoryDebugger "Permalink to this definition"){.headerlink}

:   

An extension for debugging memory usage. It collects information about:

-   objects uncollected by the Python garbage collector

-   objects left alive that shouldn't. For more info, see [[Debugging
    memory leaks with trackref]{.std
    .std-ref}](index.html#topics-leaks-trackrefs){.hoverxref .tooltip
    .reference .internal}

To enable this extension, turn on the [[`MEMDEBUG_ENABLED`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-MEMDEBUG_ENABLED){.hoverxref
.tooltip .reference .internal} setting. The info will be stored in the
stats.
:::

::: {#module-scrapy.extensions.closespider .section}
[]{#close-spider-extension}

###### Close spider extension[¶](#module-scrapy.extensions.closespider "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.closespider.]{.pre}]{.sig-prename .descclassname}[[CloseSpider]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/closespider.html#CloseSpider){.reference .internal}[¶](#scrapy.extensions.closespider.CloseSpider "Permalink to this definition"){.headerlink}

:   

Closes a spider automatically when some conditions are met, using a
specific closing reason for each condition.

The conditions for closing a spider can be configured through the
following settings:

-   [[`CLOSESPIDER_TIMEOUT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-CLOSESPIDER_TIMEOUT){.hoverxref
    .tooltip .reference .internal}

-   [[`CLOSESPIDER_TIMEOUT_NO_ITEM`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-CLOSESPIDER_TIMEOUT_NO_ITEM){.hoverxref
    .tooltip .reference .internal}

-   [[`CLOSESPIDER_ITEMCOUNT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-CLOSESPIDER_ITEMCOUNT){.hoverxref
    .tooltip .reference .internal}

-   [[`CLOSESPIDER_PAGECOUNT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-CLOSESPIDER_PAGECOUNT){.hoverxref
    .tooltip .reference .internal}

-   [[`CLOSESPIDER_ERRORCOUNT`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-CLOSESPIDER_ERRORCOUNT){.hoverxref
    .tooltip .reference .internal}

::: {.admonition .note}
Note

When a certain closing condition is met, requests which are currently in
the downloader queue (up to [[`CONCURRENT_REQUESTS`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS){.hoverxref
.tooltip .reference .internal} requests) are still processed.
:::

::: {#closespider-timeout .section}
[]{#std-setting-CLOSESPIDER_TIMEOUT}CLOSESPIDER_TIMEOUT[¶](#closespider-timeout "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

An integer which specifies a number of seconds. If the spider remains
open for more than that number of second, it will be automatically
closed with the reason [`closespider_timeout`{.docutils .literal
.notranslate}]{.pre}. If zero (or non set), spiders won't be closed by
timeout.
:::

::: {#closespider-timeout-no-item .section}
[]{#std-setting-CLOSESPIDER_TIMEOUT_NO_ITEM}CLOSESPIDER_TIMEOUT_NO_ITEM[¶](#closespider-timeout-no-item "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

An integer which specifies a number of seconds. If the spider has not
produced any items in the last number of seconds, it will be closed with
the reason [`closespider_timeout_no_item`{.docutils .literal
.notranslate}]{.pre}. If zero (or non set), spiders won't be closed
regardless if it hasn't produced any items.
:::

::: {#closespider-itemcount .section}
[]{#std-setting-CLOSESPIDER_ITEMCOUNT}CLOSESPIDER_ITEMCOUNT[¶](#closespider-itemcount "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

An integer which specifies a number of items. If the spider scrapes more
than that amount and those items are passed by the item pipeline, the
spider will be closed with the reason [`closespider_itemcount`{.docutils
.literal .notranslate}]{.pre}. If zero (or non set), spiders won't be
closed by number of passed items.
:::

::: {#closespider-pagecount .section}
[]{#std-setting-CLOSESPIDER_PAGECOUNT}CLOSESPIDER_PAGECOUNT[¶](#closespider-pagecount "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

An integer which specifies the maximum number of responses to crawl. If
the spider crawls more than that, the spider will be closed with the
reason [`closespider_pagecount`{.docutils .literal .notranslate}]{.pre}.
If zero (or non set), spiders won't be closed by number of crawled
responses.
:::

::: {#closespider-errorcount .section}
[]{#std-setting-CLOSESPIDER_ERRORCOUNT}CLOSESPIDER_ERRORCOUNT[¶](#closespider-errorcount "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

An integer which specifies the maximum number of errors to receive
before closing the spider. If the spider generates more than that number
of errors, it will be closed with the reason
[`closespider_errorcount`{.docutils .literal .notranslate}]{.pre}. If
zero (or non set), spiders won't be closed by number of errors.
:::
:::

::: {#module-scrapy.extensions.statsmailer .section}
[]{#statsmailer-extension}

###### StatsMailer extension[¶](#module-scrapy.extensions.statsmailer "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.statsmailer.]{.pre}]{.sig-prename .descclassname}[[StatsMailer]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/statsmailer.html#StatsMailer){.reference .internal}[¶](#scrapy.extensions.statsmailer.StatsMailer "Permalink to this definition"){.headerlink}

:   

This simple extension can be used to send a notification e-mail every
time a domain has finished scraping, including the Scrapy stats
collected. The email will be sent to all recipients specified in the
[[`STATSMAILER_RCPTS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-STATSMAILER_RCPTS){.hoverxref
.tooltip .reference .internal} setting.

Emails can be sent using the [[`MailSender`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.mail.MailSender "scrapy.mail.MailSender"){.reference
.internal} class. To see a full list of parameters, including examples
on how to instantiate [[`MailSender`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.mail.MailSender "scrapy.mail.MailSender"){.reference
.internal} and use mail settings, see [[Sending e-mail]{.std
.std-ref}](index.html#topics-email){.hoverxref .tooltip .reference
.internal}.

[]{#module-scrapy.extensions.debug
.target}[]{#module-scrapy.extensions.periodic_log .target}
:::

::: {#periodic-log-extension .section}
###### Periodic log extension[¶](#periodic-log-extension "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.periodic_log.]{.pre}]{.sig-prename .descclassname}[[PeriodicLog]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/periodic_log.html#PeriodicLog){.reference .internal}[¶](#scrapy.extensions.periodic_log.PeriodicLog "Permalink to this definition"){.headerlink}

:   

This extension periodically logs rich stat data as a JSON object:

::: {.highlight-default .notranslate}
::: highlight
    2023-08-04 02:30:57 [scrapy.extensions.logstats] INFO: Crawled 976 pages (at 162 pages/min), scraped 925 items (at 161 items/min)
    2023-08-04 02:30:57 [scrapy.extensions.periodic_log] INFO: {
        "delta": {
            "downloader/request_bytes": 55582,
            "downloader/request_count": 162,
            "downloader/request_method_count/GET": 162,
            "downloader/response_bytes": 618133,
            "downloader/response_count": 162,
            "downloader/response_status_count/200": 162,
            "item_scraped_count": 161
        },
        "stats": {
            "downloader/request_bytes": 338243,
            "downloader/request_count": 992,
            "downloader/request_method_count/GET": 992,
            "downloader/response_bytes": 3836736,
            "downloader/response_count": 976,
            "downloader/response_status_count/200": 976,
            "item_scraped_count": 925,
            "log_count/INFO": 21,
            "log_count/WARNING": 1,
            "scheduler/dequeued": 992,
            "scheduler/dequeued/memory": 992,
            "scheduler/enqueued": 1050,
            "scheduler/enqueued/memory": 1050
        },
        "time": {
            "elapsed": 360.008903,
            "log_interval": 60.0,
            "log_interval_real": 60.006694,
            "start_time": "2023-08-03 23:24:57",
            "utcnow": "2023-08-03 23:30:57"
        }
    }
:::
:::

This extension logs the following configurable sections:

-   [`"delta"`{.docutils .literal .notranslate}]{.pre} shows how some
    numeric stats have changed since the last stats log message.

    The [[`PERIODIC_LOG_DELTA`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-PERIODIC_LOG_DELTA){.hoverxref
    .tooltip .reference .internal} setting determines the target stats.
    They must have [`int`{.docutils .literal .notranslate}]{.pre} or
    [`float`{.docutils .literal .notranslate}]{.pre} values.

-   [`"stats"`{.docutils .literal .notranslate}]{.pre} shows the current
    value of some stats.

    The [[`PERIODIC_LOG_STATS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-PERIODIC_LOG_STATS){.hoverxref
    .tooltip .reference .internal} setting determines the target stats.

-   [`"time"`{.docutils .literal .notranslate}]{.pre} shows detailed
    timing data.

    The [[`PERIODIC_LOG_TIMING_ENABLED`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](#std-setting-PERIODIC_LOG_TIMING_ENABLED){.hoverxref
    .tooltip .reference .internal} setting determines whether or not to
    show this section.

This extension logs data at the start, then on a fixed time interval
configurable through the [[`LOGSTATS_INTERVAL`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOGSTATS_INTERVAL){.hoverxref
.tooltip .reference .internal} setting, and finally right before the
crawl ends.

Example extension configuration:

::: {.highlight-python .notranslate}
::: highlight
    custom_settings = {
        "LOG_LEVEL": "INFO",
        "PERIODIC_LOG_STATS": {
            "include": ["downloader/", "scheduler/", "log_count/", "item_scraped_count/"],
        },
        "PERIODIC_LOG_DELTA": {"include": ["downloader/"]},
        "PERIODIC_LOG_TIMING_ENABLED": True,
        "EXTENSIONS": {
            "scrapy.extensions.periodic_log.PeriodicLog": 0,
        },
    }
:::
:::

::: {#periodic-log-delta .section}
[]{#std-setting-PERIODIC_LOG_DELTA}PERIODIC_LOG_DELTA[¶](#periodic-log-delta "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

-   [`"PERIODIC_LOG_DELTA":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`True`{.docutils .literal .notranslate}]{.pre} - show
    deltas for all [`int`{.docutils .literal .notranslate}]{.pre} and
    [`float`{.docutils .literal .notranslate}]{.pre} stat values.

-   [`"PERIODIC_LOG_DELTA":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`{"include":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`["downloader/",`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`"scheduler/"]}`{.docutils .literal
    .notranslate}]{.pre} - show deltas for stats with names containing
    any configured substring.

-   [`"PERIODIC_LOG_DELTA":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`{"exclude":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`["downloader/"]}`{.docutils .literal
    .notranslate}]{.pre} - show deltas for all stats with names not
    containing any configured substring.
:::

::: {#periodic-log-stats .section}
[]{#std-setting-PERIODIC_LOG_STATS}PERIODIC_LOG_STATS[¶](#periodic-log-stats "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

-   [`"PERIODIC_LOG_STATS":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`True`{.docutils .literal .notranslate}]{.pre} - show
    the current value of all stats.

-   [`"PERIODIC_LOG_STATS":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`{"include":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`["downloader/",`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`"scheduler/"]}`{.docutils .literal
    .notranslate}]{.pre} - show current values for stats with names
    containing any configured substring.

-   [`"PERIODIC_LOG_STATS":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`{"exclude":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`["downloader/"]}`{.docutils .literal
    .notranslate}]{.pre} - show current values for all stats with names
    not containing any configured substring.
:::

::: {#periodic-log-timing-enabled .section}
[]{#std-setting-PERIODIC_LOG_TIMING_ENABLED}PERIODIC_LOG_TIMING_ENABLED[¶](#periodic-log-timing-enabled "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

[`True`{.docutils .literal .notranslate}]{.pre} enables logging of
timing data (i.e. the [`"time"`{.docutils .literal .notranslate}]{.pre}
section).
:::
:::
:::

::: {#debugging-extensions .section}
##### Debugging extensions[¶](#debugging-extensions "Permalink to this heading"){.headerlink}

::: {#stack-trace-dump-extension .section}
###### Stack trace dump extension[¶](#stack-trace-dump-extension "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.periodic_log.]{.pre}]{.sig-prename .descclassname}[[StackTraceDump]{.pre}]{.sig-name .descname}[¶](#scrapy.extensions.periodic_log.StackTraceDump "Permalink to this definition"){.headerlink}

:   

Dumps information about the running process when a
[SIGQUIT](https://en.wikipedia.org/wiki/SIGQUIT){.reference .external}
or
[SIGUSR2](https://en.wikipedia.org/wiki/SIGUSR1_and_SIGUSR2){.reference
.external} signal is received. The information dumped is the following:

1.  engine status (using
    [`scrapy.utils.engine.get_engine_status()`{.docutils .literal
    .notranslate}]{.pre})

2.  live references (see [[Debugging memory leaks with trackref]{.std
    .std-ref}](index.html#topics-leaks-trackrefs){.hoverxref .tooltip
    .reference .internal})

3.  stack trace of all threads

After the stack trace and engine status is dumped, the Scrapy process
continues running normally.

This extension only works on POSIX-compliant platforms (i.e. not
Windows), because the
[SIGQUIT](https://en.wikipedia.org/wiki/SIGQUIT){.reference .external}
and
[SIGUSR2](https://en.wikipedia.org/wiki/SIGUSR1_and_SIGUSR2){.reference
.external} signals are not available on Windows.

There are at least two ways to send Scrapy the
[SIGQUIT](https://en.wikipedia.org/wiki/SIGQUIT){.reference .external}
signal:

1.  By pressing Ctrl-while a Scrapy process is running (Linux only?)

2.  By running this command (assuming [`<pid>`{.docutils .literal
    .notranslate}]{.pre} is the process id of the Scrapy process):

    ::: {.highlight-default .notranslate}
    ::: highlight
        kill -QUIT <pid>
    :::
    :::
:::

::: {#debugger-extension .section}
###### Debugger extension[¶](#debugger-extension "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.periodic_log.]{.pre}]{.sig-prename .descclassname}[[Debugger]{.pre}]{.sig-name .descname}[¶](#scrapy.extensions.periodic_log.Debugger "Permalink to this definition"){.headerlink}

:   

Invokes a [[Python debugger]{.xref .std
.std-doc}](https://docs.python.org/3/library/pdb.html "(in Python v3.12)"){.reference
.external} inside a running Scrapy process when a
[SIGUSR2](https://en.wikipedia.org/wiki/SIGUSR1_and_SIGUSR2){.reference
.external} signal is received. After the debugger is exited, the Scrapy
process continues running normally.

For more info see [Debugging in
Python](https://pythonconquerstheuniverse.wordpress.com/2009/09/10/debugging-in-python/){.reference
.external}.

This extension only works on POSIX-compliant platforms (i.e. not
Windows).
:::
:::
:::
:::

[]{#document-topics/signals}

::: {#signals .section}
[]{#topics-signals}

### Signals[¶](#signals "Permalink to this heading"){.headerlink}

Scrapy uses signals extensively to notify when certain events occur. You
can catch some of those signals in your Scrapy project (using an
[[extension]{.std .std-ref}](index.html#topics-extensions){.hoverxref
.tooltip .reference .internal}, for example) to perform additional tasks
or extend Scrapy to add functionality not provided out of the box.

Even though signals provide several arguments, the handlers that catch
them don't need to accept all of them - the signal dispatching mechanism
will only deliver the arguments that the handler receives.

You can connect to signals (or send your own) through the [[Signals
API]{.std .std-ref}](index.html#topics-api-signals){.hoverxref .tooltip
.reference .internal}.

Here is a simple example showing how you can catch signals and perform
some action:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy import signals
    from scrapy import Spider


    class DmozSpider(Spider):
        name = "dmoz"
        allowed_domains = ["dmoz.org"]
        start_urls = [
            "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
            "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/",
        ]

        @classmethod
        def from_crawler(cls, crawler, *args, **kwargs):
            spider = super(DmozSpider, cls).from_crawler(crawler, *args, **kwargs)
            crawler.signals.connect(spider.spider_closed, signal=signals.spider_closed)
            return spider

        def spider_closed(self, spider):
            spider.logger.info("Spider closed: %s", spider.name)

        def parse(self, response):
            pass
:::
:::

::: {#deferred-signal-handlers .section}
[]{#signal-deferred}

#### Deferred signal handlers[¶](#deferred-signal-handlers "Permalink to this heading"){.headerlink}

Some signals support returning [[`Deferred`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
.external} or [[awaitable objects]{.xref .std
.std-term}](https://docs.python.org/3/glossary.html#term-awaitable "(in Python v3.12)"){.reference
.external} from their handlers, allowing you to run asynchronous code
that does not block Scrapy. If a signal handler returns one of these
objects, Scrapy waits for that asynchronous operation to finish.

Let's take an example using [[coroutines]{.std
.std-ref}](index.html#topics-coroutines){.hoverxref .tooltip .reference
.internal}:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class SignalSpider(scrapy.Spider):
        name = "signals"
        start_urls = ["https://quotes.toscrape.com/page/1/"]

        @classmethod
        def from_crawler(cls, crawler, *args, **kwargs):
            spider = super(SignalSpider, cls).from_crawler(crawler, *args, **kwargs)
            crawler.signals.connect(spider.item_scraped, signal=signals.item_scraped)
            return spider

        async def item_scraped(self, item):
            # Send the scraped item to the server
            response = await treq.post(
                "http://example.com/post",
                json.dumps(item).encode("ascii"),
                headers={b"Content-Type": [b"application/json"]},
            )

            return response

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {
                    "text": quote.css("span.text::text").get(),
                    "author": quote.css("small.author::text").get(),
                    "tags": quote.css("div.tags a.tag::text").getall(),
                }
:::
:::

See the [[Built-in signals reference]{.std
.std-ref}](#topics-signals-ref){.hoverxref .tooltip .reference
.internal} below to know which signals support [[`Deferred`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
.external} and [[awaitable objects]{.xref .std
.std-term}](https://docs.python.org/3/glossary.html#term-awaitable "(in Python v3.12)"){.reference
.external}.
:::

::: {#module-scrapy.signals .section}
[]{#built-in-signals-reference}[]{#topics-signals-ref}

#### Built-in signals reference[¶](#module-scrapy.signals "Permalink to this heading"){.headerlink}

Here's the list of Scrapy built-in signals and their meaning.

::: {#engine-signals .section}
##### Engine signals[¶](#engine-signals "Permalink to this heading"){.headerlink}

::: {#engine-started .section}
###### engine_started[¶](#engine-started "Permalink to this heading"){.headerlink}

[]{#std-signal-engine_started .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[engine_started]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[¶](#scrapy.signals.engine_started "Permalink to this definition"){.headerlink}

:   Sent when the Scrapy engine has started crawling.

    This signal supports returning deferreds from its handlers.

::: {.admonition .note}
Note

This signal may be fired *after* the [[`spider_opened`{.xref .std
.std-signal .docutils .literal
.notranslate}]{.pre}](#std-signal-spider_opened){.hoverxref .tooltip
.reference .internal} signal, depending on how the spider was started.
So **don't** rely on this signal getting fired before
[[`spider_opened`{.xref .std .std-signal .docutils .literal
.notranslate}]{.pre}](#std-signal-spider_opened){.hoverxref .tooltip
.reference .internal}.
:::
:::

::: {#engine-stopped .section}
###### engine_stopped[¶](#engine-stopped "Permalink to this heading"){.headerlink}

[]{#std-signal-engine_stopped .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[engine_stopped]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[¶](#scrapy.signals.engine_stopped "Permalink to this definition"){.headerlink}

:   Sent when the Scrapy engine is stopped (for example, when a crawling
    process has finished).

    This signal supports returning deferreds from its handlers.
:::
:::

::: {#item-signals .section}
##### Item signals[¶](#item-signals "Permalink to this heading"){.headerlink}

::: {.admonition .note}
Note

As at max [[`CONCURRENT_ITEMS`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_ITEMS){.hoverxref
.tooltip .reference .internal} items are processed in parallel, many
deferreds are fired together using [[`DeferredList`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.DeferredList.html "(in Twisted)"){.reference
.external}. Hence the next batch waits for the [[`DeferredList`{.xref
.py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.DeferredList.html "(in Twisted)"){.reference
.external} to fire and then runs the respective item signal handler for
the next batch of scraped items.
:::

::: {#item-scraped .section}
###### item_scraped[¶](#item-scraped "Permalink to this heading"){.headerlink}

[]{#std-signal-item_scraped .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[item_scraped]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}*, *[[response]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.item_scraped "Permalink to this definition"){.headerlink}

:   Sent when an item has been scraped, after it has passed all the
    [[Item Pipeline]{.std
    .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
    .reference .internal} stages (without being dropped).

    This signal supports returning deferreds from its handlers.

    Parameters

    :   -   **item** ([[item object]{.std
            .std-ref}](index.html#item-types){.hoverxref .tooltip
            .reference .internal}) -- the scraped item

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which scraped the item
