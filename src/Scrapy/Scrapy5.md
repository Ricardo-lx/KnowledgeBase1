:::

Checking items scraped from a single start_url, can also be easily
achieved using:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy parse --spider=myspider -d 3 'http://example.com/page1'
:::
:::
:::

::: {#scrapy-shell .section}
#### Scrapy Shell[¶](#scrapy-shell "Permalink to this heading"){.headerlink}

While the [[`parse`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-parse){.hoverxref .tooltip
.reference .internal} command is very useful for checking behaviour of a
spider, it is of little help to check what happens inside a callback,
besides showing the response received and the output. How to debug the
situation when [`parse_details`{.docutils .literal .notranslate}]{.pre}
sometimes receives no item?

Fortunately, the [[`shell`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-shell){.hoverxref .tooltip
.reference .internal} is your bread and butter in this case (see
[[Invoking the shell from spiders to inspect responses]{.std
.std-ref}](index.html#topics-shell-inspect-response){.hoverxref .tooltip
.reference .internal}):

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.shell import inspect_response


    def parse_details(self, response, item=None):
        if item:
            # populate more `item` fields
            return item
        else:
            inspect_response(response, self)
:::
:::

See also: [[Invoking the shell from spiders to inspect responses]{.std
.std-ref}](index.html#topics-shell-inspect-response){.hoverxref .tooltip
.reference .internal}.
:::

::: {#open-in-browser .section}
#### Open in browser[¶](#open-in-browser "Permalink to this heading"){.headerlink}

Sometimes you just want to see how a certain response looks in a
browser, you can use the [`open_in_browser`{.docutils .literal
.notranslate}]{.pre} function for that. Here is an example of how you
would use it:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.utils.response import open_in_browser


    def parse_details(self, response):
        if "item name" not in response.body:
            open_in_browser(response)
:::
:::

[`open_in_browser`{.docutils .literal .notranslate}]{.pre} will open a
browser with the response received by Scrapy at that point, adjusting
the [base tag](https://www.w3schools.com/tags/tag_base.asp){.reference
.external} so that images and styles are displayed properly.
:::

::: {#logging .section}
#### Logging[¶](#logging "Permalink to this heading"){.headerlink}

Logging is another useful option for getting information about your
spider run. Although not as convenient, it comes with the advantage that
the logs will be available in all future runs should they be necessary
again:

::: {.highlight-python .notranslate}
::: highlight
    def parse_details(self, response, item=None):
        if item:
            # populate more `item` fields
            return item
        else:
            self.logger.warning("No item received for %s", response.url)
:::
:::

For more information, check the [[Logging]{.std
.std-ref}](index.html#topics-logging){.hoverxref .tooltip .reference
.internal} section.
:::

::: {#visual-studio-code .section}
[]{#debug-vscode}

#### Visual Studio Code[¶](#visual-studio-code "Permalink to this heading"){.headerlink}

To debug spiders with Visual Studio Code you can use the following
[`launch.json`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-json .notranslate}
::: highlight
    {
        "version": "0.1.0",
        "configurations": [
            {
                "name": "Python: Launch Scrapy Spider",
                "type": "python",
                "request": "launch",
                "module": "scrapy",
                "args": [
                    "runspider",
                    "${file}"
                ],
                "console": "integratedTerminal"
            }
        ]
    }
:::
:::

Also, make sure you enable "User Uncaught Exceptions", to catch
exceptions in your Scrapy spider.
:::
:::

[]{#document-topics/contracts}

::: {#spiders-contracts .section}
[]{#topics-contracts}

### Spiders Contracts[¶](#spiders-contracts "Permalink to this heading"){.headerlink}

Testing spiders can get particularly annoying and while nothing prevents
you from writing unit tests the task gets cumbersome quickly. Scrapy
offers an integrated way of testing your spiders by the means of
contracts.

This allows you to test each callback of your spider by hardcoding a
sample url and check various constraints for how the callback processes
the response. Each contract is prefixed with an [`@`{.docutils .literal
.notranslate}]{.pre} and included in the docstring. See the following
example:

::: {.highlight-python .notranslate}
::: highlight
    def parse(self, response):
        """
        This function parses a sample response. Some contracts are mingled
        with this docstring.

        @url http://www.amazon.com/s?field-keywords=selfish+gene
        @returns items 1 16
        @returns requests 0 0
        @scrapes Title Author Year Price
        """
:::
:::

This callback is tested using three built-in contracts:

[]{#module-scrapy.contracts.default .target}

*[class]{.pre}[ ]{.w}*[[scrapy.contracts.default.]{.pre}]{.sig-prename .descclassname}[[UrlContract]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/contracts/default.html#UrlContract){.reference .internal}[¶](#scrapy.contracts.default.UrlContract "Permalink to this definition"){.headerlink}

:   This contract ([`@url`{.docutils .literal .notranslate}]{.pre}) sets
    the sample URL used when checking other contract conditions for this
    spider. This contract is mandatory. All callbacks lacking this
    contract are ignored when running the checks:

    ::: {.highlight-default .notranslate}
    ::: highlight
        @url url
    :::
    :::

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.contracts.default.]{.pre}]{.sig-prename .descclassname}[[CallbackKeywordArgumentsContract]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/contracts/default.html#CallbackKeywordArgumentsContract){.reference .internal}[¶](#scrapy.contracts.default.CallbackKeywordArgumentsContract "Permalink to this definition"){.headerlink}

:   This contract ([`@cb_kwargs`{.docutils .literal
    .notranslate}]{.pre}) sets the [`cb_kwargs`{.xref .py .py-attr
    .docutils .literal .notranslate}]{.pre} attribute for the sample
    request. It must be a valid JSON dictionary.

    ::: {.highlight-default .notranslate}
    ::: highlight
        @cb_kwargs {"arg1": "value1", "arg2": "value2", ...}
    :::
    :::

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.contracts.default.]{.pre}]{.sig-prename .descclassname}[[ReturnsContract]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/contracts/default.html#ReturnsContract){.reference .internal}[¶](#scrapy.contracts.default.ReturnsContract "Permalink to this definition"){.headerlink}

:   This contract ([`@returns`{.docutils .literal .notranslate}]{.pre})
    sets lower and upper bounds for the items and requests returned by
    the spider. The upper bound is optional:

    ::: {.highlight-default .notranslate}
    ::: highlight
        @returns item(s)|request(s) [min [max]]
    :::
    :::

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.contracts.default.]{.pre}]{.sig-prename .descclassname}[[ScrapesContract]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/contracts/default.html#ScrapesContract){.reference .internal}[¶](#scrapy.contracts.default.ScrapesContract "Permalink to this definition"){.headerlink}

:   This contract ([`@scrapes`{.docutils .literal .notranslate}]{.pre})
    checks that all the items returned by the callback have the
    specified fields:

    ::: {.highlight-default .notranslate}
    ::: highlight
        @scrapes field_1 field_2 ...
    :::
    :::

Use the [[`check`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-check){.hoverxref .tooltip
.reference .internal} command to run the contract checks.

::: {#custom-contracts .section}
#### Custom Contracts[¶](#custom-contracts "Permalink to this heading"){.headerlink}

If you find you need more power than the built-in Scrapy contracts you
can create and load your own contracts in the project by using the
[[`SPIDER_CONTRACTS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SPIDER_CONTRACTS){.hoverxref
.tooltip .reference .internal} setting:

::: {.highlight-python .notranslate}
::: highlight
    SPIDER_CONTRACTS = {
        "myproject.contracts.ResponseCheck": 10,
        "myproject.contracts.ItemValidate": 10,
    }
:::
:::

Each contract must inherit from [[`Contract`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.contracts.Contract "scrapy.contracts.Contract"){.reference
.internal} and can override three methods:

[]{#module-scrapy.contracts .target}

*[class]{.pre}[ ]{.w}*[[scrapy.contracts.]{.pre}]{.sig-prename .descclassname}[[Contract]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[method]{.pre}]{.n}*, *[[\*]{.pre}]{.o}[[args]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/contracts.html#Contract){.reference .internal}[¶](#scrapy.contracts.Contract "Permalink to this definition"){.headerlink}

:   

    Parameters

    :   -   **method**
            ([*collections.abc.Callable*](https://docs.python.org/3/library/collections.abc.html#collections.abc.Callable "(in Python v3.12)"){.reference
            .external}) -- callback function to which the contract is
            associated

        -   **args**
            ([*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- list of arguments passed into the docstring
            (whitespace separated)

    [[adjust_request_args]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[args]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/contracts.html#Contract.adjust_request_args){.reference .internal}[¶](#scrapy.contracts.Contract.adjust_request_args "Permalink to this definition"){.headerlink}

    :   This receives a [`dict`{.docutils .literal .notranslate}]{.pre}
        as an argument containing default arguments for request object.
        [`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre} is used by default, but this can be changed
        with the [`request_cls`{.docutils .literal .notranslate}]{.pre}
        attribute. If multiple contracts in chain have this attribute
        defined, the last one is used.

        Must return the same or a modified version of it.

    [[pre_process]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.contracts.Contract.pre_process "Permalink to this definition"){.headerlink}

    :   This allows hooking in various checks on the response received
        from the sample request, before it's being passed to the
        callback.

    [[post_process]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[output]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.contracts.Contract.post_process "Permalink to this definition"){.headerlink}

    :   This allows processing the output of the callback. Iterators are
        converted to lists before being passed to this hook.

Raise [[`ContractFail`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.exceptions.ContractFail "scrapy.exceptions.ContractFail"){.reference
.internal} from [[`pre_process`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.contracts.Contract.pre_process "scrapy.contracts.Contract.pre_process"){.reference
.internal} or [[`post_process`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.contracts.Contract.post_process "scrapy.contracts.Contract.post_process"){.reference
.internal} if expectations are not met:

*[class]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[ContractFail]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#ContractFail){.reference .internal}[¶](#scrapy.exceptions.ContractFail "Permalink to this definition"){.headerlink}

:   Error raised in case of a failing contract

Here is a demo contract which checks the presence of a custom header in
the response received:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.contracts import Contract
    from scrapy.exceptions import ContractFail


    class HasHeaderContract(Contract):
        """
        Demo contract which checks the presence of a custom header
        @has_header X-CustomHeader
        """

        name = "has_header"

        def pre_process(self, response):
            for header in self.args:
                if header not in response.headers:
                    raise ContractFail("X-CustomHeader not present")
:::
:::
:::

::: {#detecting-check-runs .section}
[]{#detecting-contract-check-runs}

#### Detecting check runs[¶](#detecting-check-runs "Permalink to this heading"){.headerlink}

When [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`check`{.docutils .literal .notranslate}]{.pre}
is running, the [`SCRAPY_CHECK`{.docutils .literal .notranslate}]{.pre}
environment variable is set to the [`true`{.docutils .literal
.notranslate}]{.pre} string. You can use [[`os.environ`{.xref .py
.py-data .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/os.html#os.environ "(in Python v3.12)"){.reference
.external} to perform any change to your spiders or your settings when
[`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`check`{.docutils .literal .notranslate}]{.pre} is used:

::: {.highlight-python .notranslate}
::: highlight
    import os
    import scrapy


    class ExampleSpider(scrapy.Spider):
        name = "example"

        def __init__(self):
            if os.environ.get("SCRAPY_CHECK"):
                pass  # Do some scraper adjustments when a check is running
:::
:::
:::
:::

[]{#document-topics/practices}

::: {#common-practices .section}
[]{#topics-practices}

### Common Practices[¶](#common-practices "Permalink to this heading"){.headerlink}

This section documents common practices when using Scrapy. These are
things that cover many topics and don't often fall into any other
specific section.

::: {#run-scrapy-from-a-script .section}
[]{#run-from-script}

#### Run Scrapy from a script[¶](#run-scrapy-from-a-script "Permalink to this heading"){.headerlink}

You can use the [[API]{.std .std-ref}](index.html#topics-api){.hoverxref
.tooltip .reference .internal} to run Scrapy from a script, instead of
the typical way of running Scrapy via [`scrapy`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`crawl`{.docutils .literal .notranslate}]{.pre}.

Remember that Scrapy is built on top of the Twisted asynchronous
networking library, so you need to run it inside the Twisted reactor.

The first utility you can use to run your spiders is
[[`scrapy.crawler.CrawlerProcess`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
.internal}. This class will start a Twisted reactor for you, configuring
the logging and setting shutdown handlers. This class is the one used by
all Scrapy commands.

Here's an example showing how to run a single spider with it.

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from scrapy.crawler import CrawlerProcess


    class MySpider(scrapy.Spider):
        # Your spider definition
        ...


    process = CrawlerProcess(
        settings={
            "FEEDS": {
                "items.json": {"format": "json"},
            },
        }
    )

    process.crawl(MySpider)
    process.start()  # the script will block here until the crawling is finished
:::
:::

Define settings within dictionary in CrawlerProcess. Make sure to check
[[`CrawlerProcess`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
.internal} documentation to get acquainted with its usage details.

If you are inside a Scrapy project there are some additional helpers you
can use to import those components within the project. You can
automatically import your spiders passing their name to
[[`CrawlerProcess`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
.internal}, and use [`get_project_settings`{.docutils .literal
.notranslate}]{.pre} to get a [[`Settings`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
.internal} instance with your project settings.

What follows is a working example of how to do that, using the
[testspiders](https://github.com/scrapinghub/testspiders){.reference
.external} project as example.

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.crawler import CrawlerProcess
    from scrapy.utils.project import get_project_settings

    process = CrawlerProcess(get_project_settings())

    # 'followall' is the name of one of the spiders of the project.
    process.crawl("followall", domain="scrapy.org")
    process.start()  # the script will block here until the crawling is finished
:::
:::

There's another Scrapy utility that provides more control over the
crawling process: [[`scrapy.crawler.CrawlerRunner`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
.internal}. This class is a thin wrapper that encapsulates some simple
helpers to run multiple crawlers, but it won't start or interfere with
existing reactors in any way.

Using this class the reactor should be explicitly run after scheduling
your spiders. It's recommended you use [[`CrawlerRunner`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
.internal} instead of [[`CrawlerProcess`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
.internal} if your application is already using Twisted and you want to
run Scrapy in the same reactor.

Note that you will also have to shutdown the Twisted reactor yourself
after the spider is finished. This can be achieved by adding callbacks
to the deferred returned by the [[`CrawlerRunner.crawl`{.xref .py
.py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner.crawl "scrapy.crawler.CrawlerRunner.crawl"){.reference
.internal} method.

Here's an example of its usage, along with a callback to manually stop
the reactor after [`MySpider`{.docutils .literal .notranslate}]{.pre}
has finished running.

::: {.highlight-python .notranslate}
::: highlight
    from twisted.internet import reactor
    import scrapy
    from scrapy.crawler import CrawlerRunner
    from scrapy.utils.log import configure_logging


    class MySpider(scrapy.Spider):
        # Your spider definition
        ...


    configure_logging({"LOG_FORMAT": "%(levelname)s: %(message)s"})
    runner = CrawlerRunner()

    d = runner.crawl(MySpider)
    d.addBoth(lambda _: reactor.stop())
    reactor.run()  # the script will block here until the crawling is finished
:::
:::

::: {.admonition .seealso}
See also

[Reactor
Overview](https://docs.twisted.org/en/stable/core/howto/reactor-basics.html "(in Twisted v23.10)"){.reference
.external}
:::
:::

::: {#running-multiple-spiders-in-the-same-process .section}
[]{#run-multiple-spiders}

#### Running multiple spiders in the same process[¶](#running-multiple-spiders-in-the-same-process "Permalink to this heading"){.headerlink}

By default, Scrapy runs a single spider per process when you run
[`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`crawl`{.docutils .literal .notranslate}]{.pre}. However,
Scrapy supports running multiple spiders per process using the
[[internal API]{.std .std-ref}](index.html#topics-api){.hoverxref
.tooltip .reference .internal}.

Here is an example that runs multiple spiders simultaneously:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from scrapy.crawler import CrawlerProcess
    from scrapy.utils.project import get_project_settings


    class MySpider1(scrapy.Spider):
        # Your first spider definition
        ...


    class MySpider2(scrapy.Spider):
        # Your second spider definition
        ...


    settings = get_project_settings()
    process = CrawlerProcess(settings)
    process.crawl(MySpider1)
    process.crawl(MySpider2)
    process.start()  # the script will block here until all crawling jobs are finished
:::
:::

Same example using [[`CrawlerRunner`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
.internal}:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from twisted.internet import reactor
    from scrapy.crawler import CrawlerRunner
    from scrapy.utils.log import configure_logging
    from scrapy.utils.project import get_project_settings


    class MySpider1(scrapy.Spider):
        # Your first spider definition
        ...


    class MySpider2(scrapy.Spider):
        # Your second spider definition
        ...


    configure_logging()
    settings = get_project_settings()
    runner = CrawlerRunner(settings)
    runner.crawl(MySpider1)
    runner.crawl(MySpider2)
    d = runner.join()
    d.addBoth(lambda _: reactor.stop())

    reactor.run()  # the script will block here until all crawling jobs are finished
:::
:::

Same example but running the spiders sequentially by chaining the
deferreds:

::: {.highlight-python .notranslate}
::: highlight
    from twisted.internet import reactor, defer
    from scrapy.crawler import CrawlerRunner
    from scrapy.utils.log import configure_logging
    from scrapy.utils.project import get_project_settings


    class MySpider1(scrapy.Spider):
        # Your first spider definition
        ...


    class MySpider2(scrapy.Spider):
        # Your second spider definition
        ...


    settings = get_project_settings()
    configure_logging(settings)
    runner = CrawlerRunner(settings)


    @defer.inlineCallbacks
    def crawl():
        yield runner.crawl(MySpider1)
        yield runner.crawl(MySpider2)
        reactor.stop()


    crawl()
    reactor.run()  # the script will block here until the last crawl call is finished
:::
:::

Different spiders can set different values for the same setting, but
when they run in the same process it may be impossible, by design or
because of some limitations, to use these different values. What happens
in practice is different for different settings:

-   [[`SPIDER_LOADER_CLASS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_LOADER_CLASS){.hoverxref
    .tooltip .reference .internal} and the ones used by its value
    ([[`SPIDER_MODULES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_MODULES){.hoverxref
    .tooltip .reference .internal}, [[`SPIDER_LOADER_WARN_ONLY`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_LOADER_WARN_ONLY){.hoverxref
    .tooltip .reference .internal} for the default one) cannot be read
    from the per-spider settings. These are applied when the
    [[`CrawlerRunner`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
    .internal} or [[`CrawlerProcess`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
    .internal} object is created.

-   For [[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
    .tooltip .reference .internal} and [[`ASYNCIO_EVENT_LOOP`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ASYNCIO_EVENT_LOOP){.hoverxref
    .tooltip .reference .internal} the first available value is used,
    and if a spider requests a different reactor an exception will be
    raised. These are applied when the reactor is installed.

-   For [[`REACTOR_THREADPOOL_MAXSIZE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-REACTOR_THREADPOOL_MAXSIZE){.hoverxref
    .tooltip .reference .internal}, [[`DNS_RESOLVER`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DNS_RESOLVER){.hoverxref
    .tooltip .reference .internal} and the ones used by the resolver
    ([[`DNSCACHE_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DNSCACHE_ENABLED){.hoverxref
    .tooltip .reference .internal}, [[`DNSCACHE_SIZE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DNSCACHE_SIZE){.hoverxref
    .tooltip .reference .internal}, [[`DNS_TIMEOUT`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DNS_TIMEOUT){.hoverxref
    .tooltip .reference .internal} for ones included in Scrapy) the
    first available value is used. These are applied when the reactor is
    started.

::: {.admonition .seealso}
See also

[[Run Scrapy from a script]{.std .std-ref}](#run-from-script){.hoverxref
.tooltip .reference .internal}.
:::
:::

::: {#distributed-crawls .section}
[]{#id1}

#### Distributed crawls[¶](#distributed-crawls "Permalink to this heading"){.headerlink}

Scrapy doesn't provide any built-in facility for running crawls in a
distribute (multi-server) manner. However, there are some ways to
distribute crawls, which vary depending on how you plan to distribute
them.

If you have many spiders, the obvious way to distribute the load is to
setup many Scrapyd instances and distribute spider runs among those.

If you instead want to run a single (big) spider through many machines,
what you usually do is partition the urls to crawl and send them to each
separate spider. Here is a concrete example:

First, you prepare the list of urls to crawl and put them into separate
files/urls:

::: {.highlight-default .notranslate}
::: highlight
    http://somedomain.com/urls-to-crawl/spider1/part1.list
    http://somedomain.com/urls-to-crawl/spider1/part2.list
    http://somedomain.com/urls-to-crawl/spider1/part3.list
:::
:::

Then you fire a spider run on 3 different Scrapyd servers. The spider
would receive a (spider) argument [`part`{.docutils .literal
.notranslate}]{.pre} with the number of the partition to crawl:

::: {.highlight-default .notranslate}
::: highlight
    curl http://scrapy1.mycompany.com:6800/schedule.json -d project=myproject -d spider=spider1 -d part=1
    curl http://scrapy2.mycompany.com:6800/schedule.json -d project=myproject -d spider=spider1 -d part=2
    curl http://scrapy3.mycompany.com:6800/schedule.json -d project=myproject -d spider=spider1 -d part=3
:::
:::
:::

::: {#avoiding-getting-banned .section}
[]{#bans}

#### Avoiding getting banned[¶](#avoiding-getting-banned "Permalink to this heading"){.headerlink}

Some websites implement certain measures to prevent bots from crawling
them, with varying degrees of sophistication. Getting around those
measures can be difficult and tricky, and may sometimes require special
infrastructure. Please consider contacting [commercial
support](https://scrapy.org/support/){.reference .external} if in doubt.

Here are some tips to keep in mind when dealing with these kinds of
sites:

-   rotate your user agent from a pool of well-known ones from browsers
    (google around to get a list of them)

-   disable cookies (see [[`COOKIES_ENABLED`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-COOKIES_ENABLED){.hoverxref
    .tooltip .reference .internal}) as some sites may use cookies to
    spot bot behaviour

-   use download delays (2 or higher). See [[`DOWNLOAD_DELAY`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal} setting.

-   if possible, use [Common Crawl](https://commoncrawl.org/){.reference
    .external} to fetch pages, instead of hitting the sites directly

-   use a pool of rotating IPs. For example, the free [Tor
    project](https://www.torproject.org/){.reference .external} or paid
    services like [ProxyMesh](https://proxymesh.com/){.reference
    .external}. An open source alternative is
    [scrapoxy](https://scrapoxy.io/){.reference .external}, a super
    proxy that you can attach your own proxies to.

-   use a ban avoidance service, such as [Zyte
    API](https://docs.zyte.com/zyte-api/get-started.html){.reference
    .external}, which provides a [Scrapy
    plugin](https://github.com/scrapy-plugins/scrapy-zyte-api){.reference
    .external}

If you are still unable to prevent your bot getting banned, consider
contacting [commercial support](https://scrapy.org/support/){.reference
.external}.
:::
:::

[]{#document-topics/broad-crawls}

::: {#broad-crawls .section}
[]{#topics-broad-crawls}

### Broad Crawls[¶](#broad-crawls "Permalink to this heading"){.headerlink}

Scrapy defaults are optimized for crawling specific sites. These sites
are often handled by a single Scrapy spider, although this is not
necessary or required (for example, there are generic spiders that
handle any given site thrown at them).

In addition to this "focused crawl", there is another common type of
crawling which covers a large (potentially unlimited) number of domains,
and is only limited by time or other arbitrary constraint, rather than
stopping when the domain was crawled to completion or when there are no
more requests to perform. These are called "broad crawls" and is the
typical crawlers employed by search engines.

These are some common properties often found in broad crawls:

-   they crawl many domains (often, unbounded) instead of a specific set
    of sites

-   they don't necessarily crawl domains to completion, because it would
    be impractical (or impossible) to do so, and instead limit the crawl
    by time or number of pages crawled

-   they are simpler in logic (as opposed to very complex spiders with
    many extraction rules) because data is often post-processed in a
    separate stage

-   they crawl many domains concurrently, which allows them to achieve
    faster crawl speeds by not being limited by any particular site
    constraint (each site is crawled slowly to respect politeness, but
    many sites are crawled in parallel)

As said above, Scrapy default settings are optimized for focused crawls,
not broad crawls. However, due to its asynchronous architecture, Scrapy
is very well suited for performing fast broad crawls. This page
summarizes some things you need to keep in mind when using Scrapy for
doing broad crawls, along with concrete suggestions of Scrapy settings
to tune in order to achieve an efficient broad crawl.

::: {#use-the-right-scheduler-priority-queue .section}
[]{#broad-crawls-scheduler-priority-queue}

#### Use the right [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std .std-setting .docutils .literal .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref .tooltip .reference .internal}[¶](#use-the-right-scheduler-priority-queue "Permalink to this heading"){.headerlink}

Scrapy's default scheduler priority queue is
[`'scrapy.pqueues.ScrapyPriorityQueue'`{.docutils .literal
.notranslate}]{.pre}. It works best during single-domain crawl. It does
not work well with crawling many different domains in parallel

To apply the recommended priority queue use:

::: {.highlight-python .notranslate}
::: highlight
    SCHEDULER_PRIORITY_QUEUE = "scrapy.pqueues.DownloaderAwarePriorityQueue"
:::
:::
:::

::: {#increase-concurrency .section}
[]{#broad-crawls-concurrency}

#### Increase concurrency[¶](#increase-concurrency "Permalink to this heading"){.headerlink}

Concurrency is the number of requests that are processed in parallel.
There is a global limit ([[`CONCURRENT_REQUESTS`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS){.hoverxref
.tooltip .reference .internal}) and an additional limit that can be set
either per domain ([[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal}) or per IP
([[`CONCURRENT_REQUESTS_PER_IP`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal}).

::: {.admonition .note}
Note

The scheduler priority queue [[recommended for broad crawls]{.std
.std-ref}](#broad-crawls-scheduler-priority-queue){.hoverxref .tooltip
.reference .internal} does not support
[[`CONCURRENT_REQUESTS_PER_IP`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal}.
:::

The default global concurrency limit in Scrapy is not suitable for
crawling many different domains in parallel, so you will want to
increase it. How much to increase it will depend on how much CPU and
memory your crawler will have available.

A good starting point is [`100`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    CONCURRENT_REQUESTS = 100
:::
:::

But the best way to find out is by doing some trials and identifying at
what concurrency your Scrapy process gets CPU bounded. For optimum
performance, you should pick a concurrency where CPU usage is at 80-90%.

Increasing concurrency also increases memory usage. If memory usage is a
concern, you might need to lower your global concurrency limit
accordingly.
:::

::: {#increase-twisted-io-thread-pool-maximum-size .section}
#### Increase Twisted IO thread pool maximum size[¶](#increase-twisted-io-thread-pool-maximum-size "Permalink to this heading"){.headerlink}

Currently Scrapy does DNS resolution in a blocking way with usage of
thread pool. With higher concurrency levels the crawling could be slow
or even fail hitting DNS resolver timeouts. Possible solution to
increase the number of threads handling DNS queries. The DNS queue will
be processed faster speeding up establishing of connection and crawling
overall.

To increase maximum thread pool size use:

::: {.highlight-python .notranslate}
::: highlight
    REACTOR_THREADPOOL_MAXSIZE = 20
:::
:::
:::

::: {#setup-your-own-dns .section}
#### Setup your own DNS[¶](#setup-your-own-dns "Permalink to this heading"){.headerlink}

If you have multiple crawling processes and single central DNS, it can
act like DoS attack on the DNS server resulting to slow down of entire
network or even blocking your machines. To avoid this setup your own DNS
server with local cache and upstream to some large DNS like OpenDNS or
Verizon.
:::

::: {#reduce-log-level .section}
#### Reduce log level[¶](#reduce-log-level "Permalink to this heading"){.headerlink}

When doing broad crawls you are often only interested in the crawl rates
you get and any errors found. These stats are reported by Scrapy when
using the [`INFO`{.docutils .literal .notranslate}]{.pre} log level. In
order to save CPU (and log storage requirements) you should not use
[`DEBUG`{.docutils .literal .notranslate}]{.pre} log level when
preforming large broad crawls in production. Using [`DEBUG`{.docutils
.literal .notranslate}]{.pre} level when developing your (broad) crawler
may be fine though.

To set the log level use:

::: {.highlight-python .notranslate}
::: highlight
    LOG_LEVEL = "INFO"
:::
:::
:::

::: {#disable-cookies .section}
#### Disable cookies[¶](#disable-cookies "Permalink to this heading"){.headerlink}

Disable cookies unless you *really* need. Cookies are often not needed
when doing broad crawls (search engine crawlers ignore them), and they
improve performance by saving some CPU cycles and reducing the memory
footprint of your Scrapy crawler.

To disable cookies use:

::: {.highlight-python .notranslate}
::: highlight
    COOKIES_ENABLED = False
:::
:::
:::

::: {#disable-retries .section}
#### Disable retries[¶](#disable-retries "Permalink to this heading"){.headerlink}

Retrying failed HTTP requests can slow down the crawls substantially,
specially when sites causes are very slow (or fail) to respond, thus
causing a timeout error which gets retried many times, unnecessarily,
preventing crawler capacity to be reused for other domains.

To disable retries use:

::: {.highlight-python .notranslate}
::: highlight
    RETRY_ENABLED = False
:::
:::
:::

::: {#reduce-download-timeout .section}
#### Reduce download timeout[¶](#reduce-download-timeout "Permalink to this heading"){.headerlink}

Unless you are crawling from a very slow connection (which shouldn't be
the case for broad crawls) reduce the download timeout so that stuck
requests are discarded quickly and free up capacity to process the next
ones.

To reduce the download timeout use:

::: {.highlight-python .notranslate}
::: highlight
    DOWNLOAD_TIMEOUT = 15
:::
:::
:::

::: {#disable-redirects .section}
#### Disable redirects[¶](#disable-redirects "Permalink to this heading"){.headerlink}

Consider disabling redirects, unless you are interested in following
them. When doing broad crawls it's common to save redirects and resolve
them when revisiting the site at a later crawl. This also help to keep
the number of request constant per crawl batch, otherwise redirect loops
may cause the crawler to dedicate too many resources on any specific
domain.

To disable redirects use:

::: {.highlight-python .notranslate}
::: highlight
    REDIRECT_ENABLED = False
:::
:::
:::

::: {#enable-crawling-of-ajax-crawlable-pages .section}
#### Enable crawling of "Ajax Crawlable Pages"[¶](#enable-crawling-of-ajax-crawlable-pages "Permalink to this heading"){.headerlink}

Some pages (up to 1%, based on empirical data from year 2013) declare
themselves as [ajax
crawlable](https://developers.google.com/search/docs/ajax-crawling/docs/getting-started){.reference
.external}. This means they provide plain HTML version of content that
is usually available only via AJAX. Pages can indicate it in two ways:

1.  by using [`#!`{.docutils .literal .notranslate}]{.pre} in URL - this
    is the default way;

2.  by using a special meta tag - this way is used on "main", "index"
    website pages.

Scrapy handles (1) automatically; to handle (2) enable
[[AjaxCrawlMiddleware]{.std
.std-ref}](index.html#ajaxcrawl-middleware){.hoverxref .tooltip
.reference .internal}:

::: {.highlight-python .notranslate}
::: highlight
    AJAXCRAWL_ENABLED = True
:::
:::

When doing broad crawls it's common to crawl a lot of "index" web pages;
AjaxCrawlMiddleware helps to crawl them correctly. It is turned OFF by
default because it has some performance overhead, and enabling it for
focused crawls doesn't make much sense.
:::

::: {#crawl-in-bfo-order .section}
[]{#broad-crawls-bfo}

#### Crawl in BFO order[¶](#crawl-in-bfo-order "Permalink to this heading"){.headerlink}

[[Scrapy crawls in DFO order by default]{.std
.std-ref}](index.html#faq-bfo-dfo){.hoverxref .tooltip .reference
.internal}.

In broad crawls, however, page crawling tends to be faster than page
processing. As a result, unprocessed early requests stay in memory until
the final depth is reached, which can significantly increase memory
usage.

[[Crawl in BFO order]{.std .std-ref}](index.html#faq-bfo-dfo){.hoverxref
.tooltip .reference .internal} instead to save memory.
:::

::: {#be-mindful-of-memory-leaks .section}
#### Be mindful of memory leaks[¶](#be-mindful-of-memory-leaks "Permalink to this heading"){.headerlink}

If your broad crawl shows a high memory usage, in addition to [[crawling
in BFO order]{.std .std-ref}](#broad-crawls-bfo){.hoverxref .tooltip
.reference .internal} and [[lowering concurrency]{.std
.std-ref}](#broad-crawls-concurrency){.hoverxref .tooltip .reference
.internal} you should [[debug your memory leaks]{.std
.std-ref}](index.html#topics-leaks){.hoverxref .tooltip .reference
.internal}.
:::

::: {#install-a-specific-twisted-reactor .section}
#### Install a specific Twisted reactor[¶](#install-a-specific-twisted-reactor "Permalink to this heading"){.headerlink}

If the crawl is exceeding the system's capabilities, you might want to
try installing a specific Twisted reactor, via the
[[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
.tooltip .reference .internal} setting.
:::
:::

[]{#document-topics/developer-tools}

::: {#using-your-browser-s-developer-tools-for-scraping .section}
[]{#topics-developer-tools}

### Using your browser's Developer Tools for scraping[¶](#using-your-browser-s-developer-tools-for-scraping "Permalink to this heading"){.headerlink}

Here is a general guide on how to use your browser's Developer Tools to
ease the scraping process. Today almost all browsers come with built in
[Developer
Tools](https://en.wikipedia.org/wiki/Web_development_tools){.reference
.external} and although we will use Firefox in this guide, the concepts
are applicable to any other browser.

In this guide we'll introduce the basic tools to use from a browser's
Developer Tools by scraping
[quotes.toscrape.com](https://quotes.toscrape.com){.reference
.external}.

::: {#caveats-with-inspecting-the-live-browser-dom .section}
[]{#topics-livedom}

#### Caveats with inspecting the live browser DOM[¶](#caveats-with-inspecting-the-live-browser-dom "Permalink to this heading"){.headerlink}

Since Developer Tools operate on a live browser DOM, what you'll
actually see when inspecting the page source is not the original HTML,
but a modified one after applying some browser clean up and executing
JavaScript code. Firefox, in particular, is known for adding
[`<tbody>`{.docutils .literal .notranslate}]{.pre} elements to tables.
Scrapy, on the other hand, does not modify the original page HTML, so
you won't be able to extract any data if you use [`<tbody>`{.docutils
.literal .notranslate}]{.pre} in your XPath expressions.

Therefore, you should keep in mind the following things:

-   Disable JavaScript while inspecting the DOM looking for XPaths to be
    used in Scrapy (in the Developer Tools settings click Disable
    JavaScript)

-   Never use full XPath paths, use relative and clever ones based on
    attributes (such as [`id`{.docutils .literal .notranslate}]{.pre},
    [`class`{.docutils .literal .notranslate}]{.pre}, [`width`{.docutils
    .literal .notranslate}]{.pre}, etc) or any identifying features like
    [`contains(@href,`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`'image')`{.docutils .literal .notranslate}]{.pre}.

-   Never include [`<tbody>`{.docutils .literal .notranslate}]{.pre}
    elements in your XPath expressions unless you really know what
    you're doing
:::

::: {#inspecting-a-website .section}
[]{#topics-inspector}

#### Inspecting a website[¶](#inspecting-a-website "Permalink to this heading"){.headerlink}

By far the most handy feature of the Developer Tools is the Inspector
feature, which allows you to inspect the underlying HTML code of any
webpage. To demonstrate the Inspector, let's look at the
[quotes.toscrape.com](https://quotes.toscrape.com){.reference
.external}-site.

On the site we have a total of ten quotes from various authors with
specific tags, as well as the Top Ten Tags. Let's say we want to extract
all the quotes on this page, without any meta-information about authors,
tags, etc.

Instead of viewing the whole source code for the page, we can simply
right click on a quote and select [`Inspect`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`Element`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`(Q)`{.docutils
.literal .notranslate}]{.pre}, which opens up the Inspector. In it you
should see something like this:

[![Firefox\'s
Inspector-tool](_images/inspector_01.png){style="width: 777px; height: 469px;"}](_images/inspector_01.png){.reference
.internal .image-reference}

The interesting part for us is this:

::: {.highlight-html .notranslate}
::: highlight
    <div class="quote" itemscope="" itemtype="http://schema.org/CreativeWork">
      <span class="text" itemprop="text">(...)</span>
      <span>(...)</span>
      <div class="tags">(...)</div>
    </div>
:::
:::

If you hover over the first [`div`{.docutils .literal
.notranslate}]{.pre} directly above the [`span`{.docutils .literal
.notranslate}]{.pre} tag highlighted in the screenshot, you'll see that
the corresponding section of the webpage gets highlighted as well. So
now we have a section, but we can't find our quote text anywhere.

The advantage of the Inspector is that it automatically expands and
collapses sections and tags of a webpage, which greatly improves
readability. You can expand and collapse a tag by clicking on the arrow
in front of it or by double clicking directly on the tag. If we expand
the [`span`{.docutils .literal .notranslate}]{.pre} tag with the
[`class=`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`"text"`{.docutils .literal .notranslate}]{.pre} we will
see the quote-text we clicked on. The Inspector lets you copy XPaths to
selected elements. Let's try it out.

First open the Scrapy shell at
[https://quotes.toscrape.com/](https://quotes.toscrape.com/){.reference
.external} in a terminal:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy shell "https://quotes.toscrape.com/"
:::
:::

Then, back to your web browser, right-click on the [`span`{.docutils
.literal .notranslate}]{.pre} tag, select [`Copy`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`>`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`XPath`{.docutils .literal .notranslate}]{.pre} and paste
it in the Scrapy shell like so:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath("/html/body/div/div[2]/div[1]/div[1]/span[1]/text()").getall()
    ['“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”']
:::
:::

Adding [`text()`{.docutils .literal .notranslate}]{.pre} at the end we
are able to extract the first quote with this basic selector. But this
XPath is not really that clever. All it does is go down a desired path
in the source code starting from [`html`{.docutils .literal
.notranslate}]{.pre}. So let's see if we can refine our XPath a bit:

If we check the Inspector again we'll see that directly beneath our
expanded [`div`{.docutils .literal .notranslate}]{.pre} tag we have nine
identical [`div`{.docutils .literal .notranslate}]{.pre} tags, each with
the same attributes as our first. If we expand any of them, we'll see
the same structure as with our first quote: Two [`span`{.docutils
.literal .notranslate}]{.pre} tags and one [`div`{.docutils .literal
.notranslate}]{.pre} tag. We can expand each [`span`{.docutils .literal
.notranslate}]{.pre} tag with the [`class="text"`{.docutils .literal
.notranslate}]{.pre} inside our [`div`{.docutils .literal
.notranslate}]{.pre} tags and see each quote:

::: {.highlight-html .notranslate}
::: highlight
    <div class="quote" itemscope="" itemtype="http://schema.org/CreativeWork">
      <span class="text" itemprop="text">
        “The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”
      </span>
      <span>(...)</span>
      <div class="tags">(...)</div>
    </div>
:::
:::

With this knowledge we can refine our XPath: Instead of a path to
follow, we'll simply select all [`span`{.docutils .literal
.notranslate}]{.pre} tags with the [`class="text"`{.docutils .literal
.notranslate}]{.pre} by using the
[has-class-extension](https://parsel.readthedocs.io/en/latest/usage.html#other-xpath-extensions){.reference
.external}:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> response.xpath('//span[has-class("text")]/text()').getall()
    ['“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”',
    '“It is our choices, Harry, that show what we truly are, far more than our abilities.”',
    '“There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.”',
    ...]
:::
:::

And with one simple, cleverer XPath we are able to extract all quotes
from the page. We could have constructed a loop over our first XPath to
increase the number of the last [`div`{.docutils .literal
.notranslate}]{.pre}, but this would have been unnecessarily complex and
by simply constructing an XPath with [`has-class("text")`{.docutils
.literal .notranslate}]{.pre} we were able to extract all quotes in one
line.

The Inspector has a lot of other helpful features, such as searching in
the source code or directly scrolling to an element you selected. Let's
demonstrate a use case:

Say you want to find the [`Next`{.docutils .literal .notranslate}]{.pre}
button on the page. Type [`Next`{.docutils .literal .notranslate}]{.pre}
into the search bar on the top right of the Inspector. You should get
two results. The first is a [`li`{.docutils .literal
.notranslate}]{.pre} tag with the [`class="next"`{.docutils .literal
.notranslate}]{.pre}, the second the text of an [`a`{.docutils .literal
.notranslate}]{.pre} tag. Right click on the [`a`{.docutils .literal
.notranslate}]{.pre} tag and select [`Scroll`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`into`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`View`{.docutils .literal .notranslate}]{.pre}. If you
hover over the tag, you'll see the button highlighted. From here we
could easily create a [[Link Extractor]{.std
.std-ref}](index.html#topics-link-extractors){.hoverxref .tooltip
.reference .internal} to follow the pagination. On a simple site such as
this, there may not be the need to find an element visually but the
[`Scroll`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`into`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`View`{.docutils .literal .notranslate}]{.pre} function
can be quite useful on complex sites.

Note that the search bar can also be used to search for and test CSS
selectors. For example, you could search for [`span.text`{.docutils
.literal .notranslate}]{.pre} to find all quote texts. Instead of a full
text search, this searches for exactly the [`span`{.docutils .literal
.notranslate}]{.pre} tag with the [`class="text"`{.docutils .literal
.notranslate}]{.pre} in the page.
:::

::: {#the-network-tool .section}
[]{#topics-network-tool}

#### The Network-tool[¶](#the-network-tool "Permalink to this heading"){.headerlink}

While scraping you may come across dynamic webpages where some parts of
the page are loaded dynamically through multiple requests. While this
can be quite tricky, the Network-tool in the Developer Tools greatly
facilitates this task. To demonstrate the Network-tool, let's take a
look at the page
[quotes.toscrape.com/scroll](https://quotes.toscrape.com/scroll){.reference
.external}.

The page is quite similar to the basic
[quotes.toscrape.com](https://quotes.toscrape.com){.reference
.external}-page, but instead of the above-mentioned [`Next`{.docutils
.literal .notranslate}]{.pre} button, the page automatically loads new
quotes when you scroll to the bottom. We could go ahead and try out
different XPaths directly, but instead we'll check another quite useful
command from the Scrapy shell:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy shell "quotes.toscrape.com/scroll"
    (...)
    >>> view(response)
:::
:::

A browser window should open with the webpage but with one crucial
difference: Instead of the quotes we just see a greenish bar with the
word [`Loading...`{.docutils .literal .notranslate}]{.pre}.

[![Response from
quotes.toscrape.com/scroll](_images/network_01.png){style="width: 777px; height: 296px;"}](_images/network_01.png){.reference
.internal .image-reference}

The [`view(response)`{.docutils .literal .notranslate}]{.pre} command
let's us view the response our shell or later our spider receives from
the server. Here we see that some basic template is loaded which
includes the title, the login-button and the footer, but the quotes are
missing. This tells us that the quotes are being loaded from a different
request than [`quotes.toscrape/scroll`{.docutils .literal
.notranslate}]{.pre}.

If you click on the [`Network`{.docutils .literal .notranslate}]{.pre}
tab, you will probably only see two entries. The first thing we do is
enable persistent logs by clicking on [`Persist`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`Logs`{.docutils .literal .notranslate}]{.pre}. If this
option is disabled, the log is automatically cleared each time you
navigate to a different page. Enabling this option is a good default,
since it gives us control on when to clear the logs.

If we reload the page now, you'll see the log get populated with six new
requests.

[![Network tab with persistent logs and
requests](_images/network_02.png){style="width: 777px; height: 241px;"}](_images/network_02.png){.reference
.internal .image-reference}

Here we see every request that has been made when reloading the page and
can inspect each request and its response. So let's find out where our
quotes are coming from:

First click on the request with the name [`scroll`{.docutils .literal
.notranslate}]{.pre}. On the right you can now inspect the request. In
[`Headers`{.docutils .literal .notranslate}]{.pre} you'll find details
about the request headers, such as the URL, the method, the IP-address,
and so on. We'll ignore the other tabs and click directly on
[`Response`{.docutils .literal .notranslate}]{.pre}.

What you should see in the [`Preview`{.docutils .literal
.notranslate}]{.pre} pane is the rendered HTML-code, that is exactly
what we saw when we called [`view(response)`{.docutils .literal
.notranslate}]{.pre} in the shell. Accordingly the [`type`{.docutils
.literal .notranslate}]{.pre} of the request in the log is
[`html`{.docutils .literal .notranslate}]{.pre}. The other requests have
types like [`css`{.docutils .literal .notranslate}]{.pre} or
[`js`{.docutils .literal .notranslate}]{.pre}, but what interests us is
the one request called [`quotes?page=1`{.docutils .literal
.notranslate}]{.pre} with the type [`json`{.docutils .literal
.notranslate}]{.pre}.

If we click on this request, we see that the request URL is
[`https://quotes.toscrape.com/api/quotes?page=1`{.docutils .literal
.notranslate}]{.pre} and the response is a JSON-object that contains our
quotes. We can also right-click on the request and open
[`Open`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`in`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`new`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`tab`{.docutils
.literal .notranslate}]{.pre} to get a better overview.

[![JSON-object returned from the quotes.toscrape
API](_images/network_03.png){style="width: 777px; height: 375px;"}](_images/network_03.png){.reference
.internal .image-reference}

With this response we can now easily parse the JSON-object and also
request each page to get every quote on the site:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    import json


    class QuoteSpider(scrapy.Spider):
        name = "quote"
        allowed_domains = ["quotes.toscrape.com"]
        page = 1
        start_urls = ["https://quotes.toscrape.com/api/quotes?page=1"]

        def parse(self, response):
            data = json.loads(response.text)
            for quote in data["quotes"]:
                yield {"quote": quote["text"]}
            if data["has_next"]:
                self.page += 1
                url = f"https://quotes.toscrape.com/api/quotes?page={self.page}"
                yield scrapy.Request(url=url, callback=self.parse)
:::
:::

This spider starts at the first page of the quotes-API. With each
response, we parse the [`response.text`{.docutils .literal
.notranslate}]{.pre} and assign it to [`data`{.docutils .literal
.notranslate}]{.pre}. This lets us operate on the JSON-object like on a
Python dictionary. We iterate through the [`quotes`{.docutils .literal
.notranslate}]{.pre} and print out the [`quote["text"]`{.docutils
.literal .notranslate}]{.pre}. If the handy [`has_next`{.docutils
.literal .notranslate}]{.pre} element is [`true`{.docutils .literal
.notranslate}]{.pre} (try loading
[quotes.toscrape.com/api/quotes?page=10](https://quotes.toscrape.com/api/quotes?page=10){.reference
.external} in your browser or a page-number greater than 10), we
increment the [`page`{.docutils .literal .notranslate}]{.pre} attribute
and [`yield`{.docutils .literal .notranslate}]{.pre} a new request,
inserting the incremented page-number into our [`url`{.docutils .literal
.notranslate}]{.pre}.

In more complex websites, it could be difficult to easily reproduce the
requests, as we could need to add [`headers`{.docutils .literal
.notranslate}]{.pre} or [`cookies`{.docutils .literal
.notranslate}]{.pre} to make it work. In those cases you can export the
requests in [cURL](https://curl.haxx.se/){.reference .external} format,
by right-clicking on each of them in the network tool and using the
[`from_curl()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre} method to generate an equivalent request:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy import Request

    request = Request.from_curl(
        "curl 'https://quotes.toscrape.com/api/quotes?page=1' -H 'User-Agent: Mozil"
        "la/5.0 (X11; Linux x86_64; rv:67.0) Gecko/20100101 Firefox/67.0' -H 'Acce"
        "pt: */*' -H 'Accept-Language: ca,en-US;q=0.7,en;q=0.3' --compressed -H 'X"
        "-Requested-With: XMLHttpRequest' -H 'Proxy-Authorization: Basic QFRLLTAzM"
        "zEwZTAxLTk5MWUtNDFiNC1iZWRmLTJjNGI4M2ZiNDBmNDpAVEstMDMzMTBlMDEtOTkxZS00MW"
        "I0LWJlZGYtMmM0YjgzZmI0MGY0' -H 'Connection: keep-alive' -H 'Referer: http"
        "://quotes.toscrape.com/scroll' -H 'Cache-Control: max-age=0'"
    )
:::
:::

Alternatively, if you want to know the arguments needed to recreate that
request you can use the [[`curl_to_request_kwargs()`{.xref .py .py-func
.docutils .literal
.notranslate}]{.pre}](#scrapy.utils.curl.curl_to_request_kwargs "scrapy.utils.curl.curl_to_request_kwargs"){.reference
.internal} function to get a dictionary with the equivalent arguments:

[[scrapy.utils.curl.]{.pre}]{.sig-prename .descclassname}[[curl_to_request_kwargs]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[curl_command]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[ignore_unknown_options]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/curl.html#curl_to_request_kwargs){.reference .internal}[¶](#scrapy.utils.curl.curl_to_request_kwargs "Permalink to this definition"){.headerlink}

:   Convert a cURL command syntax to Request kwargs.

    Parameters

    :   -   **curl_command**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- string containing the curl command

        -   **ignore_unknown_options**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- If true, only a warning is emitted when cURL
            options are unknown. Otherwise raises an error. (default:
            True)

    Returns

    :   dictionary of Request kwargs

Note that to translate a cURL command into a Scrapy request, you may use
[curl2scrapy](https://michael-shub.github.io/curl2scrapy/){.reference
.external}.

As you can see, with a few inspections in the Network-tool we were able
to easily replicate the dynamic requests of the scrolling functionality
of the page. Crawling dynamic pages can be quite daunting and pages can
be very complex, but it (mostly) boils down to identifying the correct
request and replicating it in your spider.
:::
:::

[]{#document-topics/dynamic-content}

::: {#selecting-dynamically-loaded-content .section}
[]{#topics-dynamic-content}

### Selecting dynamically-loaded content[¶](#selecting-dynamically-loaded-content "Permalink to this heading"){.headerlink}

Some webpages show the desired data when you load them in a web browser.
However, when you download them using Scrapy, you cannot reach the
desired data using [[selectors]{.std
.std-ref}](index.html#topics-selectors){.hoverxref .tooltip .reference
.internal}.

When this happens, the recommended approach is to [[find the data
source]{.std .std-ref}](#topics-finding-data-source){.hoverxref .tooltip
.reference .internal} and extract the data from it.

If you fail to do that, and you can nonetheless access the desired data
through the [[DOM]{.std .std-ref}](index.html#topics-livedom){.hoverxref
.tooltip .reference .internal} from your web browser, see
[[Pre-rendering JavaScript]{.std
.std-ref}](#topics-javascript-rendering){.hoverxref .tooltip .reference
.internal}.

::: {#finding-the-data-source .section}
[]{#topics-finding-data-source}

#### Finding the data source[¶](#finding-the-data-source "Permalink to this heading"){.headerlink}

To extract the desired data, you must first find its source location.

If the data is in a non-text-based format, such as an image or a PDF
document, use the [[network tool]{.std
.std-ref}](index.html#topics-network-tool){.hoverxref .tooltip
.reference .internal} of your web browser to find the corresponding
request, and [[reproduce it]{.std
.std-ref}](#topics-reproducing-requests){.hoverxref .tooltip .reference
.internal}.

If your web browser lets you select the desired data as text, the data
may be defined in embedded JavaScript code, or loaded from an external
resource in a text-based format.

In that case, you can use a tool like
[wgrep](https://github.com/stav/wgrep){.reference .external} to find the
URL of that resource.

If the data turns out to come from the original URL itself, you must
[[inspect the source code of the webpage]{.std
.std-ref}](#topics-inspecting-source){.hoverxref .tooltip .reference
.internal} to determine where the data is located.

If the data comes from a different URL, you will need to [[reproduce the
corresponding request]{.std
.std-ref}](#topics-reproducing-requests){.hoverxref .tooltip .reference
.internal}.
:::

::: {#inspecting-the-source-code-of-a-webpage .section}
[]{#topics-inspecting-source}

#### Inspecting the source code of a webpage[¶](#inspecting-the-source-code-of-a-webpage "Permalink to this heading"){.headerlink}

Sometimes you need to inspect the source code of a webpage (not the
[[DOM]{.std .std-ref}](index.html#topics-livedom){.hoverxref .tooltip
.reference .internal}) to determine where some desired data is located.

Use Scrapy's [[`fetch`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-fetch){.hoverxref .tooltip
.reference .internal} command to download the webpage contents as seen
by Scrapy:

::: {.highlight-default .notranslate}
::: highlight
    scrapy fetch --nolog https://example.com > response.html
:::
:::

If the desired data is in embedded JavaScript code within a
[`<script/>`{.docutils .literal .notranslate}]{.pre} element, see
[[Parsing JavaScript code]{.std
.std-ref}](#topics-parsing-javascript){.hoverxref .tooltip .reference
.internal}.

If you cannot find the desired data, first make sure it's not just
Scrapy: download the webpage with an HTTP client like
[curl](https://curl.haxx.se/){.reference .external} or
[wget](https://www.gnu.org/software/wget/){.reference .external} and see
if the information can be found in the response they get.

If they get a response with the desired data, modify your Scrapy
[`Request`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
to match that of the other HTTP client. For example, try using the same
user-agent string ([[`USER_AGENT`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-USER_AGENT){.hoverxref
.tooltip .reference .internal}) or the same [`headers`{.xref .py
.py-attr .docutils .literal .notranslate}]{.pre}.

If they also get a response without the desired data, you'll need to
take steps to make your request more similar to that of the web browser.
See [[Reproducing requests]{.std
.std-ref}](#topics-reproducing-requests){.hoverxref .tooltip .reference
.internal}.
:::

::: {#reproducing-requests .section}
[]{#topics-reproducing-requests}

#### Reproducing requests[¶](#reproducing-requests "Permalink to this heading"){.headerlink}

Sometimes we need to reproduce a request the way our web browser
performs it.

Use the [[network tool]{.std
.std-ref}](index.html#topics-network-tool){.hoverxref .tooltip
.reference .internal} of your web browser to see how your web browser
performs the desired request, and try to reproduce that request with
Scrapy.

It might be enough to yield a [`Request`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre} with the same HTTP method and URL.
However, you may also need to reproduce the body, headers and form
parameters (see [`FormRequest`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}) of that request.

As all major browsers allow to export the requests in
[cURL](https://curl.haxx.se/){.reference .external} format, Scrapy
incorporates the method [`from_curl()`{.xref .py .py-meth .docutils
.literal .notranslate}]{.pre} to generate an equivalent [`Request`{.xref
.py .py-class .docutils .literal .notranslate}]{.pre} from a cURL
command. To get more information visit [[request from curl]{.std
.std-ref}](index.html#requests-from-curl){.hoverxref .tooltip .reference
.internal} inside the network tool section.

Once you get the expected response, you can [[extract the desired data
from it]{.std .std-ref}](#topics-handling-response-formats){.hoverxref
.tooltip .reference .internal}.

You can reproduce any request with Scrapy. However, some times
reproducing all necessary requests may not seem efficient in developer
time. If that is your case, and crawling speed is not a major concern
for you, you can alternatively consider [[JavaScript pre-rendering]{.std
.std-ref}](#topics-javascript-rendering){.hoverxref .tooltip .reference
.internal}.

If you get the expected response sometimes, but not always, the issue is
probably not your request, but the target server. The target server
might be buggy, overloaded, or [[banning]{.std
.std-ref}](index.html#bans){.hoverxref .tooltip .reference .internal}
some of your requests.

Note that to translate a cURL command into a Scrapy request, you may use
[curl2scrapy](https://michael-shub.github.io/curl2scrapy/){.reference
.external}.
:::

::: {#handling-different-response-formats .section}
[]{#topics-handling-response-formats}

#### Handling different response formats[¶](#handling-different-response-formats "Permalink to this heading"){.headerlink}

Once you have a response with the desired data, how you extract the
desired data from it depends on the type of response:

-   If the response is HTML or XML, use [[selectors]{.std
    .std-ref}](index.html#topics-selectors){.hoverxref .tooltip
    .reference .internal} as usual.

-   If the response is JSON, use [[`json.loads()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.loads "(in Python v3.12)"){.reference
    .external} to load the desired data from [[`response.text`{.xref .py
    .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.text "scrapy.http.TextResponse.text"){.reference
    .internal}:

    ::: {.highlight-python .notranslate}
    ::: highlight
        data = json.loads(response.text)
    :::
    :::

    If the desired data is inside HTML or XML code embedded within JSON
    data, you can load that HTML or XML code into a [`Selector`{.xref
    .py .py-class .docutils .literal .notranslate}]{.pre} and then [[use
    it]{.std .std-ref}](index.html#topics-selectors){.hoverxref .tooltip
    .reference .internal} as usual:

    ::: {.highlight-python .notranslate}
    ::: highlight
        selector = Selector(data["html"])
    :::
    :::

-   If the response is JavaScript, or HTML with a [`<script/>`{.docutils
    .literal .notranslate}]{.pre} element containing the desired data,
    see [[Parsing JavaScript code]{.std
    .std-ref}](#topics-parsing-javascript){.hoverxref .tooltip
    .reference .internal}.

-   If the response is CSS, use a [[regular expression]{.xref .std
    .std-doc}](https://docs.python.org/3/library/re.html "(in Python v3.12)"){.reference
    .external} to extract the desired data from [[`response.text`{.xref
    .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.text "scrapy.http.TextResponse.text"){.reference
    .internal}.

```{=html}
<!-- -->
```
-   If the response is an image or another format based on images (e.g.
    PDF), read the response as bytes from [`response.body`{.xref .py
    .py-attr .docutils .literal .notranslate}]{.pre} and use an OCR
    solution to extract the desired data as text.

    For example, you can use
    [pytesseract](https://github.com/madmaze/pytesseract){.reference
    .external}. To read a table from a PDF,
    [tabula-py](https://github.com/chezou/tabula-py){.reference
    .external} may be a better choice.

-   If the response is SVG, or HTML with embedded SVG containing the
    desired data, you may be able to extract the desired data using
    [[selectors]{.std .std-ref}](index.html#topics-selectors){.hoverxref
    .tooltip .reference .internal}, since SVG is based on XML.

    Otherwise, you might need to convert the SVG code into a raster
    image, and [[handle that raster image]{.std
    .std-ref}](#topics-parsing-images){.hoverxref .tooltip .reference
    .internal}.
:::

::: {#parsing-javascript-code .section}
[]{#topics-parsing-javascript}

#### Parsing JavaScript code[¶](#parsing-javascript-code "Permalink to this heading"){.headerlink}

If the desired data is hardcoded in JavaScript, you first need to get
the JavaScript code:

-   If the JavaScript code is in a JavaScript file, simply read
    [[`response.text`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.text "scrapy.http.TextResponse.text"){.reference
    .internal}.

-   If the JavaScript code is within a [`<script/>`{.docutils .literal
    .notranslate}]{.pre} element of an HTML page, use [[selectors]{.std
    .std-ref}](index.html#topics-selectors){.hoverxref .tooltip
    .reference .internal} to extract the text within that
    [`<script/>`{.docutils .literal .notranslate}]{.pre} element.

Once you have a string with the JavaScript code, you can extract the
desired data from it:

-   You might be able to use a [[regular expression]{.xref .std
    .std-doc}](https://docs.python.org/3/library/re.html "(in Python v3.12)"){.reference
    .external} to extract the desired data in JSON format, which you can
    then parse with [[`json.loads()`{.xref .py .py-func .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.loads "(in Python v3.12)"){.reference
    .external}.

    For example, if the JavaScript code contains a separate line like
    [`var`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`data`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`=`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`{"field":`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`"value"};`{.docutils .literal .notranslate}]{.pre}
    you can extract that data as follows:

    ::: {.highlight-pycon .notranslate}
    ::: highlight
        >>> pattern = r"\bvar\s+data\s*=\s*(\{.*?\})\s*;\s*\n"
        >>> json_data = response.css("script::text").re_first(pattern)
        >>> json.loads(json_data)
        {'field': 'value'}
    :::
    :::

-   [chompjs](https://github.com/Nykakin/chompjs){.reference .external}
    provides an API to parse JavaScript objects into a [[`dict`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
    .external}.

    For example, if the JavaScript code contains [`var`{.docutils
    .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`data`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`=`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`{field:`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`"value",`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`secondField:`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`"second`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`value"};`{.docutils .literal .notranslate}]{.pre} you
    can extract that data as follows:

    ::: {.highlight-pycon .notranslate}
    ::: highlight
        >>> import chompjs
        >>> javascript = response.css("script::text").get()
        >>> data = chompjs.parse_js_object(javascript)
        >>> data
        {'field': 'value', 'secondField': 'second value'}
    :::
    :::

-   Otherwise, use
    [js2xml](https://github.com/scrapinghub/js2xml){.reference
    .external} to convert the JavaScript code into an XML document that
    you can parse using [[selectors]{.std
    .std-ref}](index.html#topics-selectors){.hoverxref .tooltip
    .reference .internal}.

    For example, if the JavaScript code contains [`var`{.docutils
    .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`data`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`=`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`{field:`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`"value"};`{.docutils .literal .notranslate}]{.pre}
    you can extract that data as follows:

    ::: {.highlight-pycon .notranslate}
    ::: highlight
        >>> import js2xml
        >>> import lxml.etree
        >>> from parsel import Selector
        >>> javascript = response.css("script::text").get()
        >>> xml = lxml.etree.tostring(js2xml.parse(javascript), encoding="unicode")
        >>> selector = Selector(text=xml)
        >>> selector.css('var[name="data"]').get()
        '<var name="data"><object><property name="field"><string>value</string></property></object></var>'
    :::
    :::
:::

::: {#pre-rendering-javascript .section}
[]{#topics-javascript-rendering}

#### Pre-rendering JavaScript[¶](#pre-rendering-javascript "Permalink to this heading"){.headerlink}

On webpages that fetch data from additional requests, reproducing those
requests that contain the desired data is the preferred approach. The
effort is often worth the result: structured, complete data with minimum
parsing time and network transfer.

However, sometimes it can be really hard to reproduce certain requests.
Or you may need something that no request can give you, such as a
screenshot of a webpage as seen in a web browser.

In these cases use the
[Splash](https://github.com/scrapinghub/splash){.reference .external}
JavaScript-rendering service, along with
[scrapy-splash](https://github.com/scrapy-plugins/scrapy-splash){.reference
.external} for seamless integration.

Splash returns as HTML the [[DOM]{.std
.std-ref}](index.html#topics-livedom){.hoverxref .tooltip .reference
.internal} of a webpage, so that you can parse it with [[selectors]{.std
.std-ref}](index.html#topics-selectors){.hoverxref .tooltip .reference
.internal}. It provides great flexibility through
[configuration](https://splash.readthedocs.io/en/stable/api.html){.reference
.external} or
[scripting](https://splash.readthedocs.io/en/stable/scripting-tutorial.html){.reference
.external}.

If you need something beyond what Splash offers, such as interacting
with the DOM on-the-fly from Python code instead of using a
previously-written script, or handling multiple web browser windows, you
might need to [[use a headless browser]{.std
.std-ref}](#topics-headless-browsing){.hoverxref .tooltip .reference
.internal} instead.
:::

::: {#using-a-headless-browser .section}
[]{#topics-headless-browsing}

#### Using a headless browser[¶](#using-a-headless-browser "Permalink to this heading"){.headerlink}

A [headless
browser](https://en.wikipedia.org/wiki/Headless_browser){.reference
.external} is a special web browser that provides an API for automation.
By installing the [[asyncio reactor]{.std
.std-ref}](index.html#install-asyncio){.hoverxref .tooltip .reference
.internal}, it is possible to integrate [`asyncio`{.docutils .literal
.notranslate}]{.pre}-based libraries which handle headless browsers.

One such library is
[playwright-python](https://github.com/microsoft/playwright-python){.reference
.external} (an official Python port of
[playwright](https://github.com/microsoft/playwright){.reference
.external}). The following is a simple snippet to illustrate its usage
within a Scrapy spider:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from playwright.async_api import async_playwright


    class PlaywrightSpider(scrapy.Spider):
        name = "playwright"
        start_urls = ["data:,"]  # avoid using the default Scrapy downloader

        async def parse(self, response):
            async with async_playwright() as pw:
                browser = await pw.chromium.launch()
                page = await browser.new_page()
                await page.goto("https://example.org")
                title = await page.title()
                return {"title": title}
:::
:::

However, using
[playwright-python](https://github.com/microsoft/playwright-python){.reference
.external} directly as in the above example circumvents most of the
Scrapy components (middlewares, dupefilter, etc). We recommend using
[scrapy-playwright](https://github.com/scrapy-plugins/scrapy-playwright){.reference
.external} for a better integration.
:::
:::

[]{#document-topics/leaks}

::: {#debugging-memory-leaks .section}
[]{#topics-leaks}

### Debugging memory leaks[¶](#debugging-memory-leaks "Permalink to this heading"){.headerlink}

In Scrapy, objects such as requests, responses and items have a finite
lifetime: they are created, used for a while, and finally destroyed.

From all those objects, the Request is probably the one with the longest
lifetime, as it stays waiting in the Scheduler queue until it's time to
process it. For more info see [[Architecture overview]{.std
.std-ref}](index.html#topics-architecture){.hoverxref .tooltip
.reference .internal}.

As these Scrapy objects have a (rather long) lifetime, there is always
the risk of accumulating them in memory without releasing them properly
and thus causing what is known as a "memory leak".

To help debugging memory leaks, Scrapy provides a built-in mechanism for
tracking objects references called [[trackref]{.std
.std-ref}](#topics-leaks-trackrefs){.hoverxref .tooltip .reference
.internal}, and you can also use a third-party library called
[[muppy]{.std .std-ref}](#topics-leaks-muppy){.hoverxref .tooltip
.reference .internal} for more advanced memory debugging (see below for
more info). Both mechanisms must be used from the [[Telnet Console]{.std
.std-ref}](index.html#topics-telnetconsole){.hoverxref .tooltip
.reference .internal}.

::: {#common-causes-of-memory-leaks .section}
#### Common causes of memory leaks[¶](#common-causes-of-memory-leaks "Permalink to this heading"){.headerlink}

It happens quite often (sometimes by accident, sometimes on purpose)
that the Scrapy developer passes objects referenced in Requests (for
example, using the [`cb_kwargs`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} or [`meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} attributes or the request callback function) and
that effectively bounds the lifetime of those referenced objects to the
lifetime of the Request. This is, by far, the most common cause of
memory leaks in Scrapy projects, and a quite difficult one to debug for
newcomers.

In big projects, the spiders are typically written by different people
and some of those spiders could be "leaking" and thus affecting the rest
of the other (well-written) spiders when they get to run concurrently,
which, in turn, affects the whole crawling process.

The leak could also come from a custom middleware, pipeline or extension
that you have written, if you are not releasing the (previously
allocated) resources properly. For example, allocating resources on
[[`spider_opened`{.xref .std .std-signal .docutils .literal
.notranslate}]{.pre}](index.html#std-signal-spider_opened){.hoverxref
.tooltip .reference .internal} but not releasing them on
[[`spider_closed`{.xref .std .std-signal .docutils .literal
.notranslate}]{.pre}](index.html#std-signal-spider_closed){.hoverxref
.tooltip .reference .internal} may cause problems if you're running
[[multiple spiders per process]{.std
.std-ref}](index.html#run-multiple-spiders){.hoverxref .tooltip
.reference .internal}.

::: {#too-many-requests .section}
##### Too Many Requests?[¶](#too-many-requests "Permalink to this heading"){.headerlink}

By default Scrapy keeps the request queue in memory; it includes
[`Request`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
objects and all objects referenced in Request attributes (e.g. in
[`cb_kwargs`{.xref .py .py-attr .docutils .literal .notranslate}]{.pre}
and [`meta`{.xref .py .py-attr .docutils .literal .notranslate}]{.pre}).
While not necessarily a leak, this can take a lot of memory. Enabling
[[persistent job queue]{.std
.std-ref}](index.html#topics-jobs){.hoverxref .tooltip .reference
.internal} could help keeping memory usage in control.
:::
:::

::: {#debugging-memory-leaks-with-trackref .section}
[]{#topics-leaks-trackrefs}

#### Debugging memory leaks with [`trackref`{.docutils .literal .notranslate}]{.pre}[¶](#debugging-memory-leaks-with-trackref "Permalink to this heading"){.headerlink}

[`trackref`{.xref .py .py-mod .docutils .literal .notranslate}]{.pre} is
a module provided by Scrapy to debug the most common cases of memory
leaks. It basically tracks the references to all live Request, Response,
Item, Spider and Selector objects.

You can enter the telnet console and inspect how many objects (of the
classes mentioned above) are currently alive using the
[`prefs()`{.docutils .literal .notranslate}]{.pre} function which is an
alias to the [[`print_live_refs()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.trackref.print_live_refs "scrapy.utils.trackref.print_live_refs"){.reference
.internal} function:

::: {.highlight-default .notranslate}
::: highlight
    telnet localhost 6023

    .. code-block:: pycon

        >>> prefs()
        Live References

        ExampleSpider                       1   oldest: 15s ago
        HtmlResponse                       10   oldest: 1s ago
        Selector                            2   oldest: 0s ago
        FormRequest                       878   oldest: 7s ago
:::
:::

As you can see, that report also shows the "age" of the oldest object in
each class. If you're running multiple spiders per process chances are
you can figure out which spider is leaking by looking at the oldest
request or response. You can get the oldest object of each class using
the [[`get_oldest()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.trackref.get_oldest "scrapy.utils.trackref.get_oldest"){.reference
.internal} function (from the telnet console).

::: {#which-objects-are-tracked .section}
##### Which objects are tracked?[¶](#which-objects-are-tracked "Permalink to this heading"){.headerlink}

The objects tracked by [`trackrefs`{.docutils .literal
.notranslate}]{.pre} are all from these classes (and all its
subclasses):

-   [`scrapy.Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}

-   [[`scrapy.http.Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal}

-   [`scrapy.Item`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}

-   [`scrapy.Selector`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}

-   [[`scrapy.Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
    .internal}
:::

::: {#a-real-example .section}
##### A real example[¶](#a-real-example "Permalink to this heading"){.headerlink}

Let's see a concrete example of a hypothetical case of memory leaks.
Suppose we have some spider with a line similar to this one:

::: {.highlight-default .notranslate}
::: highlight
    return Request(f"http://www.somenastyspider.com/product.php?pid={product_id}",
                   callback=self.parse, cb_kwargs={'referer': response})
:::
:::

That line is passing a response reference inside a request which
effectively ties the response lifetime to the requests' one, and that
would definitely cause memory leaks.

Let's see how we can discover the cause (without knowing it a priori, of
course) by using the [`trackref`{.docutils .literal .notranslate}]{.pre}
tool.

After the crawler is running for a few minutes and we notice its memory
usage has grown a lot, we can enter its telnet console and check the
live references:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> prefs()
    Live References

    SomenastySpider                     1   oldest: 15s ago
    HtmlResponse                     3890   oldest: 265s ago
    Selector                            2   oldest: 0s ago
    Request                          3878   oldest: 250s ago
:::
:::

The fact that there are so many live responses (and that they're so old)
is definitely suspicious, as responses should have a relatively short
lifetime compared to Requests. The number of responses is similar to the
number of requests, so it looks like they are tied in a some way. We can
now go and check the code of the spider to discover the nasty line that
is generating the leaks (passing response references inside requests).

Sometimes extra information about live objects can be helpful. Let's
check the oldest response:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy.utils.trackref import get_oldest
    >>> r = get_oldest("HtmlResponse")
    >>> r.url
    'http://www.somenastyspider.com/product.php?pid=123'
:::
:::

If you want to iterate over all objects, instead of getting the oldest
one, you can use the [[`scrapy.utils.trackref.iter_all()`{.xref .py
.py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.trackref.iter_all "scrapy.utils.trackref.iter_all"){.reference
.internal} function:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy.utils.trackref import iter_all
    >>> [r.url for r in iter_all("HtmlResponse")]
    ['http://www.somenastyspider.com/product.php?pid=123',
    'http://www.somenastyspider.com/product.php?pid=584',
    ...]
:::
:::
:::

::: {#too-many-spiders .section}
##### Too many spiders?[¶](#too-many-spiders "Permalink to this heading"){.headerlink}

If your project has too many spiders executed in parallel, the output of
[`prefs()`{.xref .py .py-func .docutils .literal .notranslate}]{.pre}
can be difficult to read. For this reason, that function has a
[`ignore`{.docutils .literal .notranslate}]{.pre} argument which can be
used to ignore a particular class (and all its subclasses). For example,
this won't show any live references to spiders:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from scrapy.spiders import Spider
    >>> prefs(ignore=Spider)
:::
:::

[]{#module-scrapy.utils.trackref .target}
:::

::: {#scrapy-utils-trackref-module .section}
##### scrapy.utils.trackref module[¶](#scrapy-utils-trackref-module "Permalink to this heading"){.headerlink}

Here are the functions available in the [[`trackref`{.xref .py .py-mod
.docutils .literal
.notranslate}]{.pre}](#module-scrapy.utils.trackref "scrapy.utils.trackref: Track references of live objects"){.reference
.internal} module.

*[class]{.pre}[ ]{.w}*[[scrapy.utils.trackref.]{.pre}]{.sig-prename .descclassname}[[object_ref]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/trackref.html#object_ref){.reference .internal}[¶](#scrapy.utils.trackref.object_ref "Permalink to this definition"){.headerlink}

:   Inherit from this class if you want to track live instances with the
    [`trackref`{.docutils .literal .notranslate}]{.pre} module.

```{=html}
<!-- -->
```

[[scrapy.utils.trackref.]{.pre}]{.sig-prename .descclassname}[[print_live_refs]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[class_name]{.pre}]{.n}*, *[[ignore]{.pre}]{.n}[[=]{.pre}]{.o}[[NoneType]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/trackref.html#print_live_refs){.reference .internal}[¶](#scrapy.utils.trackref.print_live_refs "Permalink to this definition"){.headerlink}

:   Print a report of live references, grouped by class name.

    Parameters

    :   **ignore**
        ([*type*](https://docs.python.org/3/library/functions.html#type "(in Python v3.12)"){.reference
        .external} *or*
        [*tuple*](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.12)"){.reference
        .external}) -- if given, all objects from the specified class
        (or tuple of classes) will be ignored.

```{=html}
<!-- -->
```

[[scrapy.utils.trackref.]{.pre}]{.sig-prename .descclassname}[[get_oldest]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[class_name]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/trackref.html#get_oldest){.reference .internal}[¶](#scrapy.utils.trackref.get_oldest "Permalink to this definition"){.headerlink}

:   Return the oldest object alive with the given class name, or
    [`None`{.docutils .literal .notranslate}]{.pre} if none is found.
    Use [[`print_live_refs()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre}](#scrapy.utils.trackref.print_live_refs "scrapy.utils.trackref.print_live_refs"){.reference
    .internal} first to get a list of all tracked live objects per class
    name.

```{=html}
<!-- -->
```

[[scrapy.utils.trackref.]{.pre}]{.sig-prename .descclassname}[[iter_all]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[class_name]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/trackref.html#iter_all){.reference .internal}[¶](#scrapy.utils.trackref.iter_all "Permalink to this definition"){.headerlink}

:   Return an iterator over all objects alive with the given class name,
    or [`None`{.docutils .literal .notranslate}]{.pre} if none is found.
    Use [[`print_live_refs()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre}](#scrapy.utils.trackref.print_live_refs "scrapy.utils.trackref.print_live_refs"){.reference
    .internal} first to get a list of all tracked live objects per class
    name.
:::
:::

::: {#debugging-memory-leaks-with-muppy .section}
[]{#topics-leaks-muppy}

#### Debugging memory leaks with muppy[¶](#debugging-memory-leaks-with-muppy "Permalink to this heading"){.headerlink}

[`trackref`{.docutils .literal .notranslate}]{.pre} provides a very
convenient mechanism for tracking down memory leaks, but it only keeps
track of the objects that are more likely to cause memory leaks.
However, there are other cases where the memory leaks could come from
other (more or less obscure) objects. If this is your case, and you
can't find your leaks using [`trackref`{.docutils .literal
.notranslate}]{.pre}, you still have another resource: the muppy
library.

You can use muppy from
[Pympler](https://pypi.org/project/Pympler/){.reference .external}.

If you use [`pip`{.docutils .literal .notranslate}]{.pre}, you can
install muppy with the following command:

::: {.highlight-default .notranslate}
::: highlight
    pip install Pympler
:::
:::

Here's an example to view all Python objects available in the heap using
muppy:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> from pympler import muppy
    >>> all_objects = muppy.get_objects()
    >>> len(all_objects)
    28667
    >>> from pympler import summary
    >>> suml = summary.summarize(all_objects)
    >>> summary.print_(suml)
                                   types |   # objects |   total size
    ==================================== | =========== | ============
                             <class 'str |        9822 |      1.10 MB
                            <class 'dict |        1658 |    856.62 KB
                            <class 'type |         436 |    443.60 KB
                            <class 'code |        2974 |    419.56 KB
              <class '_io.BufferedWriter |           2 |    256.34 KB
                             <class 'set |         420 |    159.88 KB
              <class '_io.BufferedReader |           1 |    128.17 KB
              <class 'wrapper_descriptor |        1130 |     88.28 KB
                           <class 'tuple |        1304 |     86.57 KB
                         <class 'weakref |        1013 |     79.14 KB
      <class 'builtin_function_or_method |         958 |     67.36 KB
               <class 'method_descriptor |         865 |     60.82 KB
                     <class 'abc.ABCMeta |          62 |     59.96 KB
                            <class 'list |         446 |     58.52 KB
                             <class 'int |        1425 |     43.20 KB
:::
:::

For more info about muppy, refer to the [muppy
documentation](https://pythonhosted.org/Pympler/muppy.html){.reference
.external}.
:::

::: {#leaks-without-leaks .section}
[]{#topics-leaks-without-leaks}

#### Leaks without leaks[¶](#leaks-without-leaks "Permalink to this heading"){.headerlink}

Sometimes, you may notice that the memory usage of your Scrapy process
will only increase, but never decrease. Unfortunately, this could happen
even though neither Scrapy nor your project are leaking memory. This is
due to a (not so well) known problem of Python, which may not return
released memory to the operating system in some cases. For more
information on this issue see:

-   [Python Memory
    Management](https://www.evanjones.ca/python-memory.html){.reference
    .external}

-   [Python Memory Management Part
    2](https://www.evanjones.ca/python-memory-part2.html){.reference
    .external}

-   [Python Memory Management Part
    3](https://www.evanjones.ca/python-memory-part3.html){.reference
    .external}

The improvements proposed by Evan Jones, which are detailed in [this
paper](https://www.evanjones.ca/memoryallocator/){.reference .external},
got merged in Python 2.5, but this only reduces the problem, it doesn't
fix it completely. To quote the paper:

> <div>
>
> *Unfortunately, this patch can only free an arena if there are no more
> objects allocated in it anymore. This means that fragmentation is a
> large issue. An application could have many megabytes of free memory,
> scattered throughout all the arenas, but it will be unable to free any
> of it. This is a problem experienced by all memory allocators. The
> only way to solve it is to move to a compacting garbage collector,
> which is able to move objects in memory. This would require
> significant changes to the Python interpreter.*
>
> </div>

To keep memory consumption reasonable you can split the job into several
smaller jobs or enable [[persistent job queue]{.std
.std-ref}](index.html#topics-jobs){.hoverxref .tooltip .reference
.internal} and stop/start spider from time to time.
:::
:::

[]{#document-topics/media-pipeline}

::: {#downloading-and-processing-files-and-images .section}
[]{#topics-media-pipeline}

### Downloading and processing files and images[¶](#downloading-and-processing-files-and-images "Permalink to this heading"){.headerlink}

Scrapy provides reusable [[item
pipelines]{.doc}](index.html#document-topics/item-pipeline){.reference
.internal} for downloading files attached to a particular item (for
example, when you scrape products and also want to download their images
locally). These pipelines share a bit of functionality and structure (we
refer to them as media pipelines), but typically you'll either use the
Files Pipeline or the Images Pipeline.

Both pipelines implement these features:

-   Avoid re-downloading media that was downloaded recently

-   Specifying where to store the media (filesystem directory, FTP
    server, Amazon S3 bucket, Google Cloud Storage bucket)

The Images Pipeline has a few extra functions for processing images:

-   Convert all downloaded images to a common format (JPG) and mode
    (RGB)

-   Thumbnail generation

-   Check images width/height to make sure they meet a minimum
    constraint

The pipelines also keep an internal queue of those media URLs which are
currently being scheduled for download, and connect those responses that
arrive containing the same media to that queue. This avoids downloading
the same media more than once when it's shared by several items.

::: {#using-the-files-pipeline .section}
#### Using the Files Pipeline[¶](#using-the-files-pipeline "Permalink to this heading"){.headerlink}

The typical workflow, when using the [`FilesPipeline`{.xref .py
.py-class .docutils .literal .notranslate}]{.pre} goes like this:

1.  In a Spider, you scrape an item and put the URLs of the desired into
    a [`file_urls`{.docutils .literal .notranslate}]{.pre} field.

2.  The item is returned from the spider and goes to the item pipeline.

3.  When the item reaches the [`FilesPipeline`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre}, the URLs in the
    [`file_urls`{.docutils .literal .notranslate}]{.pre} field are
    scheduled for download using the standard Scrapy scheduler and
    downloader (which means the scheduler and downloader middlewares are
    reused), but with a higher priority, processing them before other
    pages are scraped. The item remains "locked" at that particular
    pipeline stage until the files have finish downloading (or fail for
    some reason).

4.  When the files are downloaded, another field ([`files`{.docutils
    .literal .notranslate}]{.pre}) will be populated with the results.
    This field will contain a list of dicts with information about the
    downloaded files, such as the downloaded path, the original scraped
    url (taken from the [`file_urls`{.docutils .literal
    .notranslate}]{.pre} field), the file checksum and the file status.
    The files in the list of the [`files`{.docutils .literal
    .notranslate}]{.pre} field will retain the same order of the
    original [`file_urls`{.docutils .literal .notranslate}]{.pre} field.
    If some file failed downloading, an error will be logged and the
    file won't be present in the [`files`{.docutils .literal
    .notranslate}]{.pre} field.
:::

::: {#using-the-images-pipeline .section}
[]{#images-pipeline}

#### Using the Images Pipeline[¶](#using-the-images-pipeline "Permalink to this heading"){.headerlink}

Using the [[`ImagesPipeline`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.pipelines.images.ImagesPipeline "scrapy.pipelines.images.ImagesPipeline"){.reference
.internal} is a lot like using the [`FilesPipeline`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre}, except the default field names
used are different: you use [`image_urls`{.docutils .literal
.notranslate}]{.pre} for the image URLs of an item and it will populate
an [`images`{.docutils .literal .notranslate}]{.pre} field for the
information about the downloaded images.

The advantage of using the [[`ImagesPipeline`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.pipelines.images.ImagesPipeline "scrapy.pipelines.images.ImagesPipeline"){.reference
.internal} for image files is that you can configure some extra
functions like generating thumbnails and filtering the images based on
their size.

The Images Pipeline requires
[Pillow](https://github.com/python-pillow/Pillow){.reference .external}
7.1.0 or greater. It is used for thumbnailing and normalizing images to
JPEG/RGB format.
:::

::: {#enabling-your-media-pipeline .section}
[]{#topics-media-pipeline-enabling}

#### Enabling your Media Pipeline[¶](#enabling-your-media-pipeline "Permalink to this heading"){.headerlink}

[]{#std-setting-IMAGES_STORE .target}

To enable your media pipeline you must first add it to your project
[[`ITEM_PIPELINES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
.tooltip .reference .internal} setting.

For Images Pipeline, use:

::: {.highlight-python .notranslate}
::: highlight
    ITEM_PIPELINES = {"scrapy.pipelines.images.ImagesPipeline": 1}
:::
:::

For Files Pipeline, use:

::: {.highlight-python .notranslate}
::: highlight
    ITEM_PIPELINES = {"scrapy.pipelines.files.FilesPipeline": 1}
:::
:::

::: {.admonition .note}
Note

You can also use both the Files and Images Pipeline at the same time.
:::

Then, configure the target storage setting to a valid value that will be
used for storing the downloaded images. Otherwise the pipeline will
remain disabled, even if you include it in the [[`ITEM_PIPELINES`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
.tooltip .reference .internal} setting.

For the Files Pipeline, set the [[`FILES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_STORE){.hoverxref .tooltip
.reference .internal} setting:

::: {.highlight-python .notranslate}
::: highlight
    FILES_STORE = "/path/to/valid/dir"
:::
:::

For the Images Pipeline, set the [[`IMAGES_STORE`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
.reference .internal} setting:

::: {.highlight-python .notranslate}
::: highlight
    IMAGES_STORE = "/path/to/valid/dir"
:::
:::
:::

::: {#file-naming .section}
[]{#topics-file-naming}

#### File Naming[¶](#file-naming "Permalink to this heading"){.headerlink}

::: {#default-file-naming .section}
##### Default File Naming[¶](#default-file-naming "Permalink to this heading"){.headerlink}

By default, files are stored using an [SHA-1
hash](https://en.wikipedia.org/wiki/SHA_hash_functions){.reference
.external} of their URLs for the file names.

For example, the following image URL:

::: {.highlight-default .notranslate}
::: highlight
    http://www.example.com/image.jpg
:::
:::

Whose [`SHA-1`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`hash`{.docutils .literal .notranslate}]{.pre}
is:

::: {.highlight-default .notranslate}
::: highlight
    3afec3b4765f8f0a07b78f98c07b83f013567a0a
:::
:::

Will be downloaded and stored using your chosen [[storage method]{.std
.std-ref}](#topics-supported-storage){.hoverxref .tooltip .reference
.internal} and the following file name:

::: {.highlight-default .notranslate}
::: highlight
    3afec3b4765f8f0a07b78f98c07b83f013567a0a.jpg
:::
:::
:::

::: {#custom-file-naming .section}
##### Custom File Naming[¶](#custom-file-naming "Permalink to this heading"){.headerlink}

You may wish to use a different calculated file name for saved files.
For example, classifying an image by including meta in the file name.

Customize file names by overriding the [`file_path`{.docutils .literal
.notranslate}]{.pre} method of your media pipeline.

For example, an image pipeline with image URL:

::: {.highlight-default .notranslate}
::: highlight
    http://www.example.com/product/images/large/front/0000000004166
:::
:::

Can be processed into a file name with a condensed hash and the
perspective [`front`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-default .notranslate}
::: highlight
    00b08510e4_front.jpg
:::
:::

By overriding [`file_path`{.docutils .literal .notranslate}]{.pre} like
this:

::: {.highlight-python .notranslate}
::: highlight
    import hashlib


    def file_path(self, request, response=None, info=None, *, item=None):
        image_url_hash = hashlib.shake_256(request.url.encode()).hexdigest(5)
        image_perspective = request.url.split("/")[-2]
        image_filename = f"{image_url_hash}_{image_perspective}.jpg"

        return image_filename
:::
:::

::: {.admonition .warning}
Warning

If your custom file name scheme relies on meta data that can vary
between scrapes it may lead to unexpected re-downloading of existing
media using new file names.

For example, if your custom file name scheme uses a product title and
the site changes an item's product title between scrapes, Scrapy will
re-download the same media using updated file names.
:::

For more information about the [`file_path`{.docutils .literal
.notranslate}]{.pre} method, see [[Extending the Media Pipelines]{.std
.std-ref}](#topics-media-pipeline-override){.hoverxref .tooltip
.reference .internal}.
:::
:::

::: {#supported-storage .section}
[]{#topics-supported-storage}

#### Supported Storage[¶](#supported-storage "Permalink to this heading"){.headerlink}

::: {#file-system-storage .section}
##### File system storage[¶](#file-system-storage "Permalink to this heading"){.headerlink}

File system storage will save files to the following path:

::: {.highlight-default .notranslate}
::: highlight
    <IMAGES_STORE>/full/<FILE_NAME>
:::
:::

Where:

-   [`<IMAGES_STORE>`{.docutils .literal .notranslate}]{.pre} is the
    directory defined in [[`IMAGES_STORE`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
    .reference .internal} setting for the Images Pipeline.

-   [`full`{.docutils .literal .notranslate}]{.pre} is a sub-directory
    to separate full images from thumbnails (if used). For more info see
    [[Thumbnail generation for images]{.std
    .std-ref}](#topics-images-thumbnails){.hoverxref .tooltip .reference
    .internal}.

-   [`<FILE_NAME>`{.docutils .literal .notranslate}]{.pre} is the file
    name assigned to the file. For more info see [[File Naming]{.std
    .std-ref}](#topics-file-naming){.hoverxref .tooltip .reference
    .internal}.
:::

::: {#ftp-server-storage .section}
[]{#media-pipeline-ftp}

##### FTP server storage[¶](#ftp-server-storage "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.0.]{.versionmodified .added}
:::

[[`FILES_STORE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_STORE){.hoverxref .tooltip
.reference .internal} and [[`IMAGES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
.reference .internal} can point to an FTP server. Scrapy will
automatically upload the files to the server.

[[`FILES_STORE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_STORE){.hoverxref .tooltip
.reference .internal} and [[`IMAGES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
.reference .internal} should be written in one of the following forms:

::: {.highlight-default .notranslate}
::: highlight
    ftp://username:password@address:port/path
    ftp://address:port/path
:::
:::

If [`username`{.docutils .literal .notranslate}]{.pre} and
[`password`{.docutils .literal .notranslate}]{.pre} are not provided,
they are taken from the [[`FTP_USER`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-FTP_USER){.hoverxref
.tooltip .reference .internal} and [[`FTP_PASSWORD`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-FTP_PASSWORD){.hoverxref
.tooltip .reference .internal} settings respectively.

FTP supports two different connection modes: active or passive. Scrapy
uses the passive connection mode by default. To use the active
connection mode instead, set the [[`FEED_STORAGE_FTP_ACTIVE`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-FEED_STORAGE_FTP_ACTIVE){.hoverxref
.tooltip .reference .internal} setting to [`True`{.docutils .literal
.notranslate}]{.pre}.
:::

::: {#amazon-s3-storage .section}
[]{#media-pipelines-s3}

##### Amazon S3 storage[¶](#amazon-s3-storage "Permalink to this heading"){.headerlink}

[]{#std-setting-FILES_STORE_S3_ACL .target}

If [botocore](https://github.com/boto/botocore){.reference .external}
\>= 1.4.87 is installed, [[`FILES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_STORE){.hoverxref .tooltip
.reference .internal} and [[`IMAGES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
.reference .internal} can represent an Amazon S3 bucket. Scrapy will
automatically upload the files to the bucket.

For example, this is a valid [[`IMAGES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
.reference .internal} value:

::: {.highlight-python .notranslate}
::: highlight
    IMAGES_STORE = "s3://bucket/images"
:::
:::

You can modify the Access Control List (ACL) policy used for the stored
files, which is defined by the [[`FILES_STORE_S3_ACL`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_STORE_S3_ACL){.hoverxref
.tooltip .reference .internal} and [[`IMAGES_STORE_S3_ACL`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE_S3_ACL){.hoverxref
.tooltip .reference .internal} settings. By default, the ACL is set to
[`private`{.docutils .literal .notranslate}]{.pre}. To make the files
publicly available use the [`public-read`{.docutils .literal
.notranslate}]{.pre} policy:

::: {.highlight-python .notranslate}
::: highlight
    IMAGES_STORE_S3_ACL = "public-read"
:::
:::

For more information, see [canned
ACLs](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl){.reference
.external} in the Amazon S3 Developer Guide.

You can also use other S3-like storages. Storages like self-hosted
[Minio](https://github.com/minio/minio){.reference .external} or
[s3.scality](https://s3.scality.com/){.reference .external}. All you
need to do is set endpoint option in you Scrapy settings:

::: {.highlight-python .notranslate}
::: highlight
    AWS_ENDPOINT_URL = "http://minio.example.com:9000"
:::
:::

For self-hosting you also might feel the need not to use SSL and not to
verify SSL connection:

::: {.highlight-python .notranslate}
::: highlight
    AWS_USE_SSL = False  # or True (None by default)
    AWS_VERIFY = False  # or True (None by default)
:::
:::
:::

::: {#google-cloud-storage .section}
[]{#media-pipeline-gcs}

##### Google Cloud Storage[¶](#google-cloud-storage "Permalink to this heading"){.headerlink}

[]{#std-setting-FILES_STORE_GCS_ACL .target}

[[`FILES_STORE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_STORE){.hoverxref .tooltip
.reference .internal} and [[`IMAGES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
.reference .internal} can represent a Google Cloud Storage bucket.
Scrapy will automatically upload the files to the bucket. (requires
[google-cloud-storage](https://cloud.google.com/storage/docs/reference/libraries#client-libraries-install-python){.reference
.external} )

For example, these are valid [[`IMAGES_STORE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE){.hoverxref .tooltip
.reference .internal} and [[`GCS_PROJECT_ID`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-GCS_PROJECT_ID){.hoverxref
.tooltip .reference .internal} settings:

::: {.highlight-python .notranslate}
::: highlight
    IMAGES_STORE = "gs://bucket/images/"
    GCS_PROJECT_ID = "project_id"
:::
:::

For information about authentication, see this
[documentation](https://cloud.google.com/docs/authentication/production){.reference
.external}.

You can modify the Access Control List (ACL) policy used for the stored
files, which is defined by the [[`FILES_STORE_GCS_ACL`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_STORE_GCS_ACL){.hoverxref
.tooltip .reference .internal} and [[`IMAGES_STORE_GCS_ACL`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_STORE_GCS_ACL){.hoverxref
.tooltip .reference .internal} settings. By default, the ACL is set to
[`''`{.docutils .literal .notranslate}]{.pre} (empty string) which means
that Cloud Storage applies the bucket's default object ACL to the
object. To make the files publicly available use the
[`publicRead`{.docutils .literal .notranslate}]{.pre} policy:

::: {.highlight-python .notranslate}
::: highlight
    IMAGES_STORE_GCS_ACL = "publicRead"
:::
:::

For more information, see [Predefined
ACLs](https://cloud.google.com/storage/docs/access-control/lists#predefined-acl){.reference
.external} in the Google Cloud Platform Developer Guide.
:::
:::

::: {#usage-example .section}
#### Usage example[¶](#usage-example "Permalink to this heading"){.headerlink}

[]{#std-setting-FILES_URLS_FIELD
.target}[]{#std-setting-FILES_RESULT_FIELD
.target}[]{#std-setting-IMAGES_URLS_FIELD .target}

In order to use a media pipeline, first [[enable it]{.std
.std-ref}](#topics-media-pipeline-enabling){.hoverxref .tooltip
.reference .internal}.

Then, if a spider returns an [[item object]{.std
.std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
.internal} with the URLs field ([`file_urls`{.docutils .literal
.notranslate}]{.pre} or [`image_urls`{.docutils .literal
.notranslate}]{.pre}, for the Files or Images Pipeline respectively),
the pipeline will put the results under the respective field
([`files`{.docutils .literal .notranslate}]{.pre} or [`images`{.docutils
.literal .notranslate}]{.pre}).

When using [[item types]{.std
.std-ref}](index.html#item-types){.hoverxref .tooltip .reference
.internal} for which fields are defined beforehand, you must define both
the URLs field and the results field. For example, when using the images
pipeline, items must define both the [`image_urls`{.docutils .literal
.notranslate}]{.pre} and the [`images`{.docutils .literal
.notranslate}]{.pre} field. For instance, using the [`Item`{.xref .py
.py-class .docutils .literal .notranslate}]{.pre} class:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MyItem(scrapy.Item):
        # ... other item fields ...
        image_urls = scrapy.Field()
        images = scrapy.Field()
:::
:::

If you want to use another field name for the URLs key or for the
results key, it is also possible to override it.

For the Files Pipeline, set [[`FILES_URLS_FIELD`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_URLS_FIELD){.hoverxref .tooltip
.reference .internal} and/or [[`FILES_RESULT_FIELD`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_RESULT_FIELD){.hoverxref
.tooltip .reference .internal} settings:

::: {.highlight-python .notranslate}
::: highlight
    FILES_URLS_FIELD = "field_name_for_your_files_urls"
    FILES_RESULT_FIELD = "field_name_for_your_processed_files"
:::
:::

For the Images Pipeline, set [[`IMAGES_URLS_FIELD`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_URLS_FIELD){.hoverxref
.tooltip .reference .internal} and/or [[`IMAGES_RESULT_FIELD`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_RESULT_FIELD){.hoverxref
.tooltip .reference .internal} settings:

::: {.highlight-python .notranslate}
::: highlight
    IMAGES_URLS_FIELD = "field_name_for_your_images_urls"
    IMAGES_RESULT_FIELD = "field_name_for_your_processed_images"
:::
:::

If you need something more complex and want to override the custom
pipeline behaviour, see [[Extending the Media Pipelines]{.std
.std-ref}](#topics-media-pipeline-override){.hoverxref .tooltip
.reference .internal}.

If you have multiple image pipelines inheriting from ImagePipeline and
you want to have different settings in different pipelines you can set
setting keys preceded with uppercase name of your pipeline class. E.g.
if your pipeline is called MyPipeline and you want to have custom
IMAGES_URLS_FIELD you define setting MYPIPELINE_IMAGES_URLS_FIELD and
your custom settings will be used.
:::

::: {#additional-features .section}
#### Additional features[¶](#additional-features "Permalink to this heading"){.headerlink}

::: {#file-expiration .section}
[]{#id2}

##### File expiration[¶](#file-expiration "Permalink to this heading"){.headerlink}

[]{#std-setting-IMAGES_EXPIRES .target}

The Image Pipeline avoids downloading files that were downloaded
recently. To adjust this retention delay use the [[`FILES_EXPIRES`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FILES_EXPIRES){.hoverxref .tooltip
.reference .internal} setting (or [[`IMAGES_EXPIRES`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_EXPIRES){.hoverxref .tooltip
.reference .internal}, in case of Images Pipeline), which specifies the
delay in number of days:

::: {.highlight-python .notranslate}
::: highlight
    # 120 days of delay for files expiration
    FILES_EXPIRES = 120

    # 30 days of delay for images expiration
    IMAGES_EXPIRES = 30
:::
:::

The default value for both settings is 90 days.

If you have pipeline that subclasses FilesPipeline and you'd like to
have different setting for it you can set setting keys preceded by
uppercase class name. E.g. given pipeline class called MyPipeline you
can set setting key:

> <div>
>
> MYPIPELINE_FILES_EXPIRES = 180
>
> </div>

and pipeline class MyPipeline will have expiration time set to 180.

The last modified time from the file is used to determine the age of the
file in days, which is then compared to the set expiration time to
determine if the file is expired.
:::

::: {#thumbnail-generation-for-images .section}
[]{#topics-images-thumbnails}

##### Thumbnail generation for images[¶](#thumbnail-generation-for-images "Permalink to this heading"){.headerlink}

The Images Pipeline can automatically create thumbnails of the
downloaded images.

In order to use this feature, you must set [[`IMAGES_THUMBS`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_THUMBS){.hoverxref .tooltip
.reference .internal} to a dictionary where the keys are the thumbnail
names and the values are their dimensions.

For example:

::: {.highlight-python .notranslate}
::: highlight
    IMAGES_THUMBS = {
        "small": (50, 50),
        "big": (270, 270),
    }
:::
:::

When you use this feature, the Images Pipeline will create thumbnails of
the each specified size with this format:

::: {.highlight-default .notranslate}
::: highlight
    <IMAGES_STORE>/thumbs/<size_name>/<image_id>.jpg
:::
:::

Where:

-   [`<size_name>`{.docutils .literal .notranslate}]{.pre} is the one
    specified in the [[`IMAGES_THUMBS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-IMAGES_THUMBS){.hoverxref
    .tooltip .reference .internal} dictionary keys ([`small`{.docutils
    .literal .notranslate}]{.pre}, [`big`{.docutils .literal
    .notranslate}]{.pre}, etc)

-   [`<image_id>`{.docutils .literal .notranslate}]{.pre} is the [SHA-1
    hash](https://en.wikipedia.org/wiki/SHA_hash_functions){.reference
    .external} of the image url

Example of image files stored using [`small`{.docutils .literal
.notranslate}]{.pre} and [`big`{.docutils .literal .notranslate}]{.pre}
thumbnail names:

::: {.highlight-default .notranslate}
::: highlight
    <IMAGES_STORE>/full/63bbfea82b8880ed33cdb762aa11fab722a90a24.jpg
    <IMAGES_STORE>/thumbs/small/63bbfea82b8880ed33cdb762aa11fab722a90a24.jpg
    <IMAGES_STORE>/thumbs/big/63bbfea82b8880ed33cdb762aa11fab722a90a24.jpg
:::
:::

The first one is the full image, as downloaded from the site.
:::

::: {#filtering-out-small-images .section}
##### Filtering out small images[¶](#filtering-out-small-images "Permalink to this heading"){.headerlink}

[]{#std-setting-IMAGES_MIN_HEIGHT .target}

When using the Images Pipeline, you can drop images which are too small,
by specifying the minimum allowed size in the
[[`IMAGES_MIN_HEIGHT`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_MIN_HEIGHT){.hoverxref
.tooltip .reference .internal} and [[`IMAGES_MIN_WIDTH`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-IMAGES_MIN_WIDTH){.hoverxref .tooltip
.reference .internal} settings.

For example:

::: {.highlight-default .notranslate}
::: highlight
    IMAGES_MIN_HEIGHT = 110
    IMAGES_MIN_WIDTH = 110
:::
:::

::: {.admonition .note}
Note

The size constraints don't affect thumbnail generation at all.
:::

It is possible to set just one size constraint or both. When setting
both of them, only images that satisfy both minimum sizes will be saved.
For the above example, images of sizes (105 x 105) or (105 x 200) or
(200 x 105) will all be dropped because at least one dimension is
shorter than the constraint.

By default, there are no size constraints, so all images are processed.
:::

::: {#allowing-redirections .section}
##### Allowing redirections[¶](#allowing-redirections "Permalink to this heading"){.headerlink}

By default media pipelines ignore redirects, i.e. an HTTP redirection to
a media file URL request will mean the media download is considered
failed.

To handle media redirections, set this setting to [`True`{.docutils
.literal .notranslate}]{.pre}:

::: {.highlight-default .notranslate}
::: highlight
    MEDIA_ALLOW_REDIRECTS = True
:::
:::
:::
:::

::: {#module-scrapy.pipelines.files .section}
[]{#extending-the-media-pipelines}[]{#topics-media-pipeline-override}

#### Extending the Media Pipelines[¶](#module-scrapy.pipelines.files "Permalink to this heading"){.headerlink}

See here the methods that you can override in your custom Files
Pipeline:

*[class]{.pre}[ ]{.w}*[[scrapy.pipelines.files.]{.pre}]{.sig-prename .descclassname}[[FilesPipeline]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/files.html#FilesPipeline){.reference .internal}[¶](#scrapy.pipelines.files.FilesPipeline "Permalink to this definition"){.headerlink}

:   

    [[file_path]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[response]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[info]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*]{.pre}]{.o}*, *[[item]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/files.html#FilesPipeline.file_path){.reference .internal}[¶](#scrapy.pipelines.files.FilesPipeline.file_path "Permalink to this definition"){.headerlink}

    :   This method is called once per downloaded item. It returns the
        download path of the file originating from the specified
        [[`response`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal}.

        In addition to [`response`{.docutils .literal
        .notranslate}]{.pre}, this method receives the original
        [`request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}, [`info`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} and [`item`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre}

        You can override this method to customize the download path of
        each file.

        For example, if file URLs end like regular paths (e.g.
        [`https://example.com/a/b/c/foo.png`{.docutils .literal
        .notranslate}]{.pre}), you can use the following approach to
        download all files into the [`files`{.docutils .literal
        .notranslate}]{.pre} folder with their original filenames (e.g.
        [`files/foo.png`{.docutils .literal .notranslate}]{.pre}):

        ::: {.highlight-python .notranslate}
        ::: highlight
            from pathlib import PurePosixPath
            from urllib.parse import urlparse

            from scrapy.pipelines.files import FilesPipeline


            class MyFilesPipeline(FilesPipeline):
                def file_path(self, request, response=None, info=None, *, item=None):
                    return "files/" + PurePosixPath(urlparse(request.url).path).name
        :::
        :::

        Similarly, you can use the [`item`{.docutils .literal
        .notranslate}]{.pre} to determine the file path based on some
        item property.

        By default the [[`file_path()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.file_path "scrapy.pipelines.files.FilesPipeline.file_path"){.reference
        .internal} method returns [`full/<request`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`URL`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`hash>.<extension>`{.docutils .literal
        .notranslate}]{.pre}.

        ::: versionadded
        [New in version 2.4: ]{.versionmodified .added}The *item*
        parameter.
        :::

    [[get_media_requests]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}*, *[[info]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/files.html#FilesPipeline.get_media_requests){.reference .internal}[¶](#scrapy.pipelines.files.FilesPipeline.get_media_requests "Permalink to this definition"){.headerlink}

    :   As seen on the workflow, the pipeline will get the URLs of the
        images to download from the item. In order to do this, you can
        override the [[`get_media_requests()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.get_media_requests "scrapy.pipelines.files.FilesPipeline.get_media_requests"){.reference
        .internal} method and return a Request for each file URL:

        ::: {.highlight-python .notranslate}
        ::: highlight
            from itemadapter import ItemAdapter


            def get_media_requests(self, item, info):
                adapter = ItemAdapter(item)
                for file_url in adapter["file_urls"]:
                    yield scrapy.Request(file_url)
        :::
        :::

        Those requests will be processed by the pipeline and, when they
        have finished downloading, the results will be sent to the
        [[`item_completed()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.item_completed "scrapy.pipelines.files.FilesPipeline.item_completed"){.reference
        .internal} method, as a list of 2-element tuples. Each tuple
        will contain [`(success,`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`file_info_or_error)`{.docutils .literal
        .notranslate}]{.pre} where:

        -   [`success`{.docutils .literal .notranslate}]{.pre} is a
            boolean which is [`True`{.docutils .literal
            .notranslate}]{.pre} if the image was downloaded
            successfully or [`False`{.docutils .literal
            .notranslate}]{.pre} if it failed for some reason

        -   [`file_info_or_error`{.docutils .literal
            .notranslate}]{.pre} is a dict containing the following keys
            (if success is [`True`{.docutils .literal
            .notranslate}]{.pre}) or a [[`Failure`{.xref .py .py-exc
            .docutils .literal
            .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference
            .external} if there was a problem.

            -   [`url`{.docutils .literal .notranslate}]{.pre} - the url
                where the file was downloaded from. This is the url of
                the request returned from the
                [[`get_media_requests()`{.xref .py .py-meth .docutils
                .literal
                .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.get_media_requests "scrapy.pipelines.files.FilesPipeline.get_media_requests"){.reference
                .internal} method.

            -   [`path`{.docutils .literal .notranslate}]{.pre} - the
                path (relative to [[`FILES_STORE`{.xref .std
                .std-setting .docutils .literal
                .notranslate}]{.pre}](#std-setting-FILES_STORE){.hoverxref
                .tooltip .reference .internal}) where the file was
                stored

            -   [`checksum`{.docutils .literal .notranslate}]{.pre} - a
                [MD5 hash](https://en.wikipedia.org/wiki/MD5){.reference
                .external} of the image contents

            -   [`status`{.docutils .literal .notranslate}]{.pre} - the
                file status indication.

                ::: versionadded
                [New in version 2.2.]{.versionmodified .added}
                :::

                It can be one of the following:

                -   [`downloaded`{.docutils .literal
                    .notranslate}]{.pre} - file was downloaded.

                -   [`uptodate`{.docutils .literal
                    .notranslate}]{.pre} - file was not downloaded, as
                    it was downloaded recently, according to the file
                    expiration policy.

                -   [`cached`{.docutils .literal .notranslate}]{.pre} -
                    file was already scheduled for download, by another
                    item sharing the same file.

        The list of tuples received by [[`item_completed()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.item_completed "scrapy.pipelines.files.FilesPipeline.item_completed"){.reference
        .internal} is guaranteed to retain the same order of the
        requests returned from the [[`get_media_requests()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.get_media_requests "scrapy.pipelines.files.FilesPipeline.get_media_requests"){.reference
        .internal} method.

        Here's a typical value of the [`results`{.docutils .literal
        .notranslate}]{.pre} argument:

        ::: {.highlight-python .notranslate}
        ::: highlight
            [
                (
                    True,
                    {
                        "checksum": "2b00042f7481c7b056c4b410d28f33cf",
                        "path": "full/0a79c461a4062ac383dc4fade7bc09f1384a3910.jpg",
                        "url": "http://www.example.com/files/product1.pdf",
                        "status": "downloaded",
                    },
                ),
                (False, Failure(...)),
            ]
        :::
        :::

        By default the [[`get_media_requests()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.get_media_requests "scrapy.pipelines.files.FilesPipeline.get_media_requests"){.reference
        .internal} method returns [`None`{.docutils .literal
        .notranslate}]{.pre} which means there are no files to download
        for the item.

    [[item_completed]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[results]{.pre}]{.n}*, *[[item]{.pre}]{.n}*, *[[info]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/files.html#FilesPipeline.item_completed){.reference .internal}[¶](#scrapy.pipelines.files.FilesPipeline.item_completed "Permalink to this definition"){.headerlink}

    :   The [[`FilesPipeline.item_completed()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.item_completed "scrapy.pipelines.files.FilesPipeline.item_completed"){.reference
        .internal} method called when all file requests for a single
        item have completed (either finished downloading, or failed for
        some reason).

        The [[`item_completed()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.item_completed "scrapy.pipelines.files.FilesPipeline.item_completed"){.reference
        .internal} method must return the output that will be sent to
        subsequent item pipeline stages, so you must return (or drop)
        the item, as you would in any pipeline.

        Here is an example of the [[`item_completed()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.item_completed "scrapy.pipelines.files.FilesPipeline.item_completed"){.reference
        .internal} method where we store the downloaded file paths
        (passed in results) in the [`file_paths`{.docutils .literal
        .notranslate}]{.pre} item field, and we drop the item if it
        doesn't contain any files:

        ::: {.highlight-python .notranslate}
        ::: highlight
            from itemadapter import ItemAdapter
            from scrapy.exceptions import DropItem


            def item_completed(self, results, item, info):
                file_paths = [x["path"] for ok, x in results if ok]
                if not file_paths:
                    raise DropItem("Item contains no files")
                adapter = ItemAdapter(item)
                adapter["file_paths"] = file_paths
                return item
        :::
        :::

        By default, the [[`item_completed()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.files.FilesPipeline.item_completed "scrapy.pipelines.files.FilesPipeline.item_completed"){.reference
        .internal} method returns the item.

[]{#module-scrapy.pipelines.images .target}

See here the methods that you can override in your custom Images
Pipeline:

*[class]{.pre}[ ]{.w}*[[scrapy.pipelines.images.]{.pre}]{.sig-prename .descclassname}[[ImagesPipeline]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/images.html#ImagesPipeline){.reference .internal}[¶](#scrapy.pipelines.images.ImagesPipeline "Permalink to this definition"){.headerlink}

:   <div>
    >
    > The [[`ImagesPipeline`{.xref .py .py-class .docutils .literal
    > .notranslate}]{.pre}](#scrapy.pipelines.images.ImagesPipeline "scrapy.pipelines.images.ImagesPipeline"){.reference
    > .internal} is an extension of the [`FilesPipeline`{.xref .py
    > .py-class .docutils .literal .notranslate}]{.pre}, customizing the
    > field names and adding custom behavior for images.
    >
    > </div>

    [[file_path]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[response]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[info]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*]{.pre}]{.o}*, *[[item]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/images.html#ImagesPipeline.file_path){.reference .internal}[¶](#scrapy.pipelines.images.ImagesPipeline.file_path "Permalink to this definition"){.headerlink}

    :   This method is called once per downloaded item. It returns the
        download path of the file originating from the specified
        [[`response`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal}.

        In addition to [`response`{.docutils .literal
        .notranslate}]{.pre}, this method receives the original
        [`request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}, [`info`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} and [`item`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre}

        You can override this method to customize the download path of
        each file.

        For example, if file URLs end like regular paths (e.g.
        [`https://example.com/a/b/c/foo.png`{.docutils .literal
        .notranslate}]{.pre}), you can use the following approach to
        download all files into the [`files`{.docutils .literal
        .notranslate}]{.pre} folder with their original filenames (e.g.
        [`files/foo.png`{.docutils .literal .notranslate}]{.pre}):

        ::: {.highlight-python .notranslate}
        ::: highlight
            from pathlib import PurePosixPath
            from urllib.parse import urlparse

            from scrapy.pipelines.images import ImagesPipeline


            class MyImagesPipeline(ImagesPipeline):
                def file_path(self, request, response=None, info=None, *, item=None):
                    return "files/" + PurePosixPath(urlparse(request.url).path).name
        :::
        :::

        Similarly, you can use the [`item`{.docutils .literal
        .notranslate}]{.pre} to determine the file path based on some
        item property.

        By default the [[`file_path()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.pipelines.images.ImagesPipeline.file_path "scrapy.pipelines.images.ImagesPipeline.file_path"){.reference
        .internal} method returns [`full/<request`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`URL`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`hash>.<extension>`{.docutils .literal
        .notranslate}]{.pre}.

        ::: versionadded
        [New in version 2.4: ]{.versionmodified .added}The *item*
        parameter.
        :::

    [[thumb_path]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[thumb_id]{.pre}]{.n}*, *[[response]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[info]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*]{.pre}]{.o}*, *[[item]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/images.html#ImagesPipeline.thumb_path){.reference .internal}[¶](#scrapy.pipelines.images.ImagesPipeline.thumb_path "Permalink to this definition"){.headerlink}

    :   This method is called for every item of [[`IMAGES_THUMBS`{.xref
        .std .std-setting .docutils .literal
        .notranslate}]{.pre}](#std-setting-IMAGES_THUMBS){.hoverxref
        .tooltip .reference .internal} per downloaded item. It returns
        the thumbnail download path of the image originating from the
        specified [[`response`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal}.

        In addition to [`response`{.docutils .literal
        .notranslate}]{.pre}, this method receives the original
        [`request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}, [`thumb_id`{.docutils .literal
        .notranslate}]{.pre}, [`info`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} and [`item`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre}.

        You can override this method to customize the thumbnail download
        path of each image. You can use the [`item`{.docutils .literal
        .notranslate}]{.pre} to determine the file path based on some
        item property.

        By default the [[`thumb_path()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.pipelines.images.ImagesPipeline.thumb_path "scrapy.pipelines.images.ImagesPipeline.thumb_path"){.reference
        .internal} method returns [`thumbs/<size`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`name>/<request`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`URL`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`hash>.<extension>`{.docutils .literal
        .notranslate}]{.pre}.

    [[get_media_requests]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}*, *[[info]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/images.html#ImagesPipeline.get_media_requests){.reference .internal}[¶](#scrapy.pipelines.images.ImagesPipeline.get_media_requests "Permalink to this definition"){.headerlink}

    :   Works the same way as
        [`FilesPipeline.get_media_requests()`{.xref .py .py-meth
        .docutils .literal .notranslate}]{.pre} method, but using a
        different field name for image urls.

        Must return a Request for each image URL.

    [[item_completed]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[results]{.pre}]{.n}*, *[[item]{.pre}]{.n}*, *[[info]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/pipelines/images.html#ImagesPipeline.item_completed){.reference .internal}[¶](#scrapy.pipelines.images.ImagesPipeline.item_completed "Permalink to this definition"){.headerlink}

    :   The [[`ImagesPipeline.item_completed()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.images.ImagesPipeline.item_completed "scrapy.pipelines.images.ImagesPipeline.item_completed"){.reference
        .internal} method is called when all image requests for a single
        item have completed (either finished downloading, or failed for
        some reason).

        Works the same way as [`FilesPipeline.item_completed()`{.xref
        .py .py-meth .docutils .literal .notranslate}]{.pre} method, but
        using a different field names for storing image downloading
        results.

        By default, the [[`item_completed()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.pipelines.images.ImagesPipeline.item_completed "scrapy.pipelines.images.ImagesPipeline.item_completed"){.reference
        .internal} method returns the item.
:::

::: {#custom-images-pipeline-example .section}
[]{#media-pipeline-example}

#### Custom Images pipeline example[¶](#custom-images-pipeline-example "Permalink to this heading"){.headerlink}

Here is a full example of the Images Pipeline whose methods are
exemplified above:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from itemadapter import ItemAdapter
    from scrapy.exceptions import DropItem
    from scrapy.pipelines.images import ImagesPipeline


    class MyImagesPipeline(ImagesPipeline):
        def get_media_requests(self, item, info):
            for image_url in item["image_urls"]:
                yield scrapy.Request(image_url)

        def item_completed(self, results, item, info):
            image_paths = [x["path"] for ok, x in results if ok]
            if not image_paths:
                raise DropItem("Item contains no images")
            adapter = ItemAdapter(item)
            adapter["image_paths"] = image_paths
            return item
:::
:::

To enable your custom media pipeline component you must add its class
import path to the [[`ITEM_PIPELINES`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
.tooltip .reference .internal} setting, like in the following example:

::: {.highlight-python .notranslate}
::: highlight
    ITEM_PIPELINES = {"myproject.pipelines.MyImagesPipeline": 300}
:::
:::
:::
:::

[]{#document-topics/deploy}

::: {#deploying-spiders .section}
[]{#topics-deploy}

### Deploying Spiders[¶](#deploying-spiders "Permalink to this heading"){.headerlink}

This section describes the different options you have for deploying your
Scrapy spiders to run them on a regular basis. Running Scrapy spiders in
your local machine is very convenient for the (early) development stage,
but not so much when you need to execute long-running spiders or move
spiders to run in production continuously. This is where the solutions
for deploying Scrapy spiders come in.

Popular choices for deploying Scrapy spiders are:

-   [[Scrapyd]{.std .std-ref}](#deploy-scrapyd){.hoverxref .tooltip
    .reference .internal} (open source)

-   [[Zyte Scrapy Cloud]{.std
    .std-ref}](#deploy-scrapy-cloud){.hoverxref .tooltip .reference
    .internal} (cloud-based)

::: {#deploying-to-a-scrapyd-server .section}
[]{#deploy-scrapyd}

#### Deploying to a Scrapyd Server[¶](#deploying-to-a-scrapyd-server "Permalink to this heading"){.headerlink}

[Scrapyd](https://github.com/scrapy/scrapyd){.reference .external} is an
open source application to run Scrapy spiders. It provides a server with
HTTP API, capable of running and monitoring Scrapy spiders.

To deploy spiders to Scrapyd, you can use the scrapyd-deploy tool
provided by the
[scrapyd-client](https://github.com/scrapy/scrapyd-client){.reference
.external} package. Please refer to the [scrapyd-deploy
documentation](https://scrapyd.readthedocs.io/en/latest/deploy.html){.reference
.external} for more information.

Scrapyd is maintained by some of the Scrapy developers.
:::

::: {#deploying-to-zyte-scrapy-cloud .section}
[]{#deploy-scrapy-cloud}

#### Deploying to Zyte Scrapy Cloud[¶](#deploying-to-zyte-scrapy-cloud "Permalink to this heading"){.headerlink}

[Zyte Scrapy Cloud](https://www.zyte.com/scrapy-cloud/){.reference
.external} is a hosted, cloud-based service by
[Zyte](https://zyte.com/){.reference .external}, the company behind
Scrapy.

Zyte Scrapy Cloud removes the need to setup and monitor servers and
provides a nice UI to manage spiders and review scraped items, logs and
stats.

To deploy spiders to Zyte Scrapy Cloud you can use the
[shub](https://shub.readthedocs.io/en/latest/){.reference .external}
command line tool. Please refer to the [Zyte Scrapy Cloud
documentation](https://docs.zyte.com/scrapy-cloud.html){.reference
.external} for more information.

Zyte Scrapy Cloud is compatible with Scrapyd and one can switch between
them as needed - the configuration is read from the
[`scrapy.cfg`{.docutils .literal .notranslate}]{.pre} file just like
[`scrapyd-deploy`{.docutils .literal .notranslate}]{.pre}.
:::
:::

[]{#document-topics/autothrottle}

::: {#autothrottle-extension .section}
[]{#topics-autothrottle}

### AutoThrottle extension[¶](#autothrottle-extension "Permalink to this heading"){.headerlink}

This is an extension for automatically throttling crawling speed based
on load of both the Scrapy server and the website you are crawling.

::: {#design-goals .section}
#### Design goals[¶](#design-goals "Permalink to this heading"){.headerlink}

1.  be nicer to sites instead of using default download delay of zero

2.  automatically adjust Scrapy to the optimum crawling speed, so the
    user doesn't have to tune the download delays to find the optimum
    one. The user only needs to specify the maximum concurrent requests
    it allows, and the extension does the rest.
:::

::: {#how-it-works .section}
[]{#autothrottle-algorithm}

#### How it works[¶](#how-it-works "Permalink to this heading"){.headerlink}

AutoThrottle extension adjusts download delays dynamically to make
spider send [[`AUTOTHROTTLE_TARGET_CONCURRENCY`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_TARGET_CONCURRENCY){.hoverxref
.tooltip .reference .internal} concurrent requests on average to each
remote website.

It uses download latency to compute the delays. The main idea is the
following: if a server needs [`latency`{.docutils .literal
.notranslate}]{.pre} seconds to respond, a client should send a request
each [`latency/N`{.docutils .literal .notranslate}]{.pre} seconds to
have [`N`{.docutils .literal .notranslate}]{.pre} requests processed in
parallel.

Instead of adjusting the delays one can just set a small fixed download
delay and impose hard limits on concurrency using
[[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} or [[`CONCURRENT_REQUESTS_PER_IP`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal} options. It will provide a similar
effect, but there are some important differences:

-   because the download delay is small there will be occasional bursts
    of requests;

-   often non-200 (error) responses can be returned faster than regular
    responses, so with a small download delay and a hard concurrency
    limit crawler will be sending requests to server faster when server
    starts to return errors. But this is an opposite of what crawler
    should do - in case of errors it makes more sense to slow down:
    these errors may be caused by the high request rate.

AutoThrottle doesn't have these issues.
:::

::: {#throttling-algorithm .section}
#### Throttling algorithm[¶](#throttling-algorithm "Permalink to this heading"){.headerlink}

AutoThrottle algorithm adjusts download delays based on the following
rules:

1.  spiders always start with a download delay of
    [[`AUTOTHROTTLE_START_DELAY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_START_DELAY){.hoverxref
    .tooltip .reference .internal};

2.  when a response is received, the target download delay is calculated
    as [`latency`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`/`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`N`{.docutils .literal .notranslate}]{.pre} where
    [`latency`{.docutils .literal .notranslate}]{.pre} is a latency of
    the response, and [`N`{.docutils .literal .notranslate}]{.pre} is
    [[`AUTOTHROTTLE_TARGET_CONCURRENCY`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_TARGET_CONCURRENCY){.hoverxref
    .tooltip .reference .internal}.

3.  download delay for next requests is set to the average of previous
    download delay and the target download delay;

4.  latencies of non-200 responses are not allowed to decrease the
    delay;

5.  download delay can't become less than [[`DOWNLOAD_DELAY`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal} or greater than
    [[`AUTOTHROTTLE_MAX_DELAY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_MAX_DELAY){.hoverxref
    .tooltip .reference .internal}

::: {.admonition .note}
Note

The AutoThrottle extension honours the standard Scrapy settings for
concurrency and delay. This means that it will respect
[[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} and [[`CONCURRENT_REQUESTS_PER_IP`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal} options and never set a download delay
lower than [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_DELAY){.hoverxref
.tooltip .reference .internal}.
:::

In Scrapy, the download latency is measured as the time elapsed between
establishing the TCP connection and receiving the HTTP headers.

Note that these latencies are very hard to measure accurately in a
cooperative multitasking environment because Scrapy may be busy
processing a spider callback, for example, and unable to attend
downloads. However, these latencies should still give a reasonable
estimate of how busy Scrapy (and ultimately, the server) is, and this
extension builds on that premise.
:::

::: {#settings .section}
#### Settings[¶](#settings "Permalink to this heading"){.headerlink}

The settings used to control the AutoThrottle extension are:

-   [[`AUTOTHROTTLE_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_ENABLED){.hoverxref
    .tooltip .reference .internal}

-   [[`AUTOTHROTTLE_START_DELAY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_START_DELAY){.hoverxref
    .tooltip .reference .internal}

-   [[`AUTOTHROTTLE_MAX_DELAY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_MAX_DELAY){.hoverxref
    .tooltip .reference .internal}

-   [[`AUTOTHROTTLE_TARGET_CONCURRENCY`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_TARGET_CONCURRENCY){.hoverxref
    .tooltip .reference .internal}

-   [[`AUTOTHROTTLE_DEBUG`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-AUTOTHROTTLE_DEBUG){.hoverxref
    .tooltip .reference .internal}

-   [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
    .tooltip .reference .internal}

-   [[`CONCURRENT_REQUESTS_PER_IP`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
    .tooltip .reference .internal}

-   [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal}

For more information see [[How it works]{.std
.std-ref}](#autothrottle-algorithm){.hoverxref .tooltip .reference
.internal}.

::: {#autothrottle-enabled .section}
[]{#std-setting-AUTOTHROTTLE_ENABLED}

##### AUTOTHROTTLE_ENABLED[¶](#autothrottle-enabled "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Enables the AutoThrottle extension.
:::

::: {#autothrottle-start-delay .section}
[]{#std-setting-AUTOTHROTTLE_START_DELAY}

##### AUTOTHROTTLE_START_DELAY[¶](#autothrottle-start-delay "Permalink to this heading"){.headerlink}

Default: [`5.0`{.docutils .literal .notranslate}]{.pre}

The initial download delay (in seconds).
:::

::: {#autothrottle-max-delay .section}
[]{#std-setting-AUTOTHROTTLE_MAX_DELAY}

##### AUTOTHROTTLE_MAX_DELAY[¶](#autothrottle-max-delay "Permalink to this heading"){.headerlink}

Default: [`60.0`{.docutils .literal .notranslate}]{.pre}

The maximum download delay (in seconds) to be set in case of high
latencies.
:::

::: {#autothrottle-target-concurrency .section}
[]{#std-setting-AUTOTHROTTLE_TARGET_CONCURRENCY}

##### AUTOTHROTTLE_TARGET_CONCURRENCY[¶](#autothrottle-target-concurrency "Permalink to this heading"){.headerlink}

Default: [`1.0`{.docutils .literal .notranslate}]{.pre}

Average number of requests Scrapy should be sending in parallel to
remote websites.

By default, AutoThrottle adjusts the delay to send a single concurrent
request to each of the remote websites. Set this option to a higher
value (e.g. [`2.0`{.docutils .literal .notranslate}]{.pre}) to increase
the throughput and the load on remote servers. A lower
[`AUTOTHROTTLE_TARGET_CONCURRENCY`{.docutils .literal
.notranslate}]{.pre} value (e.g. [`0.5`{.docutils .literal
.notranslate}]{.pre}) makes the crawler more conservative and polite.

Note that [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} and [[`CONCURRENT_REQUESTS_PER_IP`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal} options are still respected when
AutoThrottle extension is enabled. This means that if
[`AUTOTHROTTLE_TARGET_CONCURRENCY`{.docutils .literal
.notranslate}]{.pre} is set to a value higher than
[[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} or [[`CONCURRENT_REQUESTS_PER_IP`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal}, the crawler won't reach this number of
concurrent requests.

At every given time point Scrapy can be sending more or less concurrent
requests than [`AUTOTHROTTLE_TARGET_CONCURRENCY`{.docutils .literal
.notranslate}]{.pre}; it is a suggested value the crawler tries to
approach, not a hard limit.
:::

::: {#autothrottle-debug .section}
[]{#std-setting-AUTOTHROTTLE_DEBUG}

##### AUTOTHROTTLE_DEBUG[¶](#autothrottle-debug "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Enable AutoThrottle debug mode which will display stats on every
response received, so you can see how the throttling parameters are
being adjusted in real time.
:::
:::
:::

[]{#document-topics/benchmarking}

::: {#benchmarking .section}
[]{#id1}

### Benchmarking[¶](#benchmarking "Permalink to this heading"){.headerlink}

Scrapy comes with a simple benchmarking suite that spawns a local HTTP
server and crawls it at the maximum possible speed. The goal of this
benchmarking is to get an idea of how Scrapy performs in your hardware,
in order to have a common baseline for comparisons. It uses a simple
spider that does nothing and just follows links.

To run it use:

::: {.highlight-default .notranslate}
::: highlight
    scrapy bench
:::
:::

You should see an output like this:

::: {.highlight-default .notranslate}
::: highlight
    2016-12-16 21:18:48 [scrapy.utils.log] INFO: Scrapy 1.2.2 started (bot: quotesbot)
    2016-12-16 21:18:48 [scrapy.utils.log] INFO: Overridden settings: {'CLOSESPIDER_TIMEOUT': 10, 'ROBOTSTXT_OBEY': True, 'SPIDER_MODULES': ['quotesbot.spiders'], 'LOGSTATS_INTERVAL': 1, 'BOT_NAME': 'quotesbot', 'LOG_LEVEL': 'INFO', 'NEWSPIDER_MODULE': 'quotesbot.spiders'}
    2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled extensions:
    ['scrapy.extensions.closespider.CloseSpider',
     'scrapy.extensions.logstats.LogStats',
     'scrapy.extensions.telnet.TelnetConsole',
     'scrapy.extensions.corestats.CoreStats']
    2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled downloader middlewares:
    ['scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware',
     'scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware',
     'scrapy.downloadermiddlewares.downloadtimeout.DownloadTimeoutMiddleware',
     'scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware',
     'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware',
     'scrapy.downloadermiddlewares.retry.RetryMiddleware',
     'scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware',
     'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware',
     'scrapy.downloadermiddlewares.redirect.RedirectMiddleware',
     'scrapy.downloadermiddlewares.cookies.CookiesMiddleware',
     'scrapy.downloadermiddlewares.stats.DownloaderStats']
    2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled spider middlewares:
    ['scrapy.spidermiddlewares.httperror.HttpErrorMiddleware',
     'scrapy.spidermiddlewares.offsite.OffsiteMiddleware',
     'scrapy.spidermiddlewares.referer.RefererMiddleware',
     'scrapy.spidermiddlewares.urllength.UrlLengthMiddleware',
     'scrapy.spidermiddlewares.depth.DepthMiddleware']
    2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled item pipelines:
    []
    2016-12-16 21:18:49 [scrapy.core.engine] INFO: Spider opened
    2016-12-16 21:18:49 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:50 [scrapy.extensions.logstats] INFO: Crawled 70 pages (at 4200 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:51 [scrapy.extensions.logstats] INFO: Crawled 134 pages (at 3840 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:52 [scrapy.extensions.logstats] INFO: Crawled 198 pages (at 3840 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:53 [scrapy.extensions.logstats] INFO: Crawled 254 pages (at 3360 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:54 [scrapy.extensions.logstats] INFO: Crawled 302 pages (at 2880 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:55 [scrapy.extensions.logstats] INFO: Crawled 358 pages (at 3360 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:56 [scrapy.extensions.logstats] INFO: Crawled 406 pages (at 2880 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:57 [scrapy.extensions.logstats] INFO: Crawled 438 pages (at 1920 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:58 [scrapy.extensions.logstats] INFO: Crawled 470 pages (at 1920 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:18:59 [scrapy.core.engine] INFO: Closing spider (closespider_timeout)
    2016-12-16 21:18:59 [scrapy.extensions.logstats] INFO: Crawled 518 pages (at 2880 pages/min), scraped 0 items (at 0 items/min)
    2016-12-16 21:19:00 [scrapy.statscollectors] INFO: Dumping Scrapy stats:
    {'downloader/request_bytes': 229995,
     'downloader/request_count': 534,
     'downloader/request_method_count/GET': 534,
     'downloader/response_bytes': 1565504,
     'downloader/response_count': 534,
     'downloader/response_status_count/200': 534,
     'finish_reason': 'closespider_timeout',
     'finish_time': datetime.datetime(2016, 12, 16, 16, 19, 0, 647725),
     'log_count/INFO': 17,
     'request_depth_max': 19,
     'response_received_count': 534,
     'scheduler/dequeued': 533,
     'scheduler/dequeued/memory': 533,
     'scheduler/enqueued': 10661,
     'scheduler/enqueued/memory': 10661,
     'start_time': datetime.datetime(2016, 12, 16, 16, 18, 49, 799869)}
    2016-12-16 21:19:00 [scrapy.core.engine] INFO: Spider closed (closespider_timeout)
:::
:::

That tells you that Scrapy is able to crawl about 3000 pages per minute
in the hardware where you run it. Note that this is a very simple spider
intended to follow links, any custom spider you write will probably do
more stuff which results in slower crawl rates. How slower depends on
how much your spider does and how well it's written.

Use [scrapy-bench](https://github.com/scrapy/scrapy-bench){.reference
.external} for more complex benchmarking.
:::

[]{#document-topics/jobs}

::: {#jobs-pausing-and-resuming-crawls .section}
[]{#topics-jobs}

### Jobs: pausing and resuming crawls[¶](#jobs-pausing-and-resuming-crawls "Permalink to this heading"){.headerlink}

Sometimes, for big sites, it's desirable to pause crawls and be able to
resume them later.

Scrapy supports this functionality out of the box by providing the
following facilities:

-   a scheduler that persists scheduled requests on disk

-   a duplicates filter that persists visited requests on disk

-   an extension that keeps some spider state (key/value pairs)
    persistent between batches

::: {#job-directory .section}
#### Job directory[¶](#job-directory "Permalink to this heading"){.headerlink}

To enable persistence support you just need to define a *job directory*
through the [`JOBDIR`{.docutils .literal .notranslate}]{.pre} setting.
This directory will be for storing all required data to keep the state
of a single job (i.e. a spider run). It's important to note that this
directory must not be shared by different spiders, or even different
jobs/runs of the same spider, as it's meant to be used for storing the
state of a *single* job.
:::

::: {#how-to-use-it .section}
#### How to use it[¶](#how-to-use-it "Permalink to this heading"){.headerlink}

To start a spider with persistence support enabled, run it like this:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl somespider -s JOBDIR=crawls/somespider-1
:::
:::

Then, you can stop the spider safely at any time (by pressing Ctrl-C or
sending a signal), and resume it later by issuing the same command:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl somespider -s JOBDIR=crawls/somespider-1
:::
:::
:::

::: {#keeping-persistent-state-between-batches .section}
[]{#topics-keeping-persistent-state-between-batches}

#### Keeping persistent state between batches[¶](#keeping-persistent-state-between-batches "Permalink to this heading"){.headerlink}

Sometimes you'll want to keep some persistent spider state between
pause/resume batches. You can use the [`spider.state`{.docutils .literal
.notranslate}]{.pre} attribute for that, which should be a dict. There's
a built-in extension that takes care of serializing, storing and loading
that attribute from the job directory, when the spider starts and stops.

Here's an example of a callback that uses the spider state (other spider
code is omitted for brevity):

::: {.highlight-python .notranslate}
::: highlight
    def parse_item(self, response):
        # parse item here
        self.state["items_count"] = self.state.get("items_count", 0) + 1
:::
:::
:::

::: {#persistence-gotchas .section}
#### Persistence gotchas[¶](#persistence-gotchas "Permalink to this heading"){.headerlink}

There are a few things to keep in mind if you want to be able to use the
Scrapy persistence support:

::: {#cookies-expiration .section}
##### Cookies expiration[¶](#cookies-expiration "Permalink to this heading"){.headerlink}

Cookies may expire. So, if you don't resume your spider quickly the
requests scheduled may no longer work. This won't be an issue if your
spider doesn't rely on cookies.
:::

::: {#request-serialization .section}
[]{#id1}

##### Request serialization[¶](#request-serialization "Permalink to this heading"){.headerlink}

For persistence to work, [`Request`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre} objects must be serializable with
[[`pickle`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/pickle.html#module-pickle "(in Python v3.12)"){.reference
.external}, except for the [`callback`{.docutils .literal
.notranslate}]{.pre} and [`errback`{.docutils .literal
.notranslate}]{.pre} values passed to their [`__init__`{.docutils
.literal .notranslate}]{.pre} method, which must be methods of the
running [[`Spider`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
.internal} class.

If you wish to log the requests that couldn't be serialized, you can set
the [[`SCHEDULER_DEBUG`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DEBUG){.hoverxref
.tooltip .reference .internal} setting to [`True`{.docutils .literal
.notranslate}]{.pre} in the project's settings page. It is
[`False`{.docutils .literal .notranslate}]{.pre} by default.
:::
:::
:::

[]{#document-topics/coroutines}

::: {#coroutines .section}
[]{#topics-coroutines}

### Coroutines[¶](#coroutines "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.0.]{.versionmodified .added}
:::

Scrapy has [[partial support]{.std
.std-ref}](#coroutine-support){.hoverxref .tooltip .reference .internal}
for the [[coroutine syntax]{.xref .std
.std-ref}](https://docs.python.org/3/reference/compound_stmts.html#async "(in Python v3.12)"){.reference
.external}.

::: {#supported-callables .section}
[]{#coroutine-support}

#### Supported callables[¶](#supported-callables "Permalink to this heading"){.headerlink}

The following callables may be defined as coroutines using
[`async`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`def`{.docutils .literal .notranslate}]{.pre}, and hence
use coroutine syntax (e.g. [`await`{.docutils .literal
.notranslate}]{.pre}, [`async`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`for`{.docutils
.literal .notranslate}]{.pre}, [`async`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`with`{.docutils .literal .notranslate}]{.pre}):

-   [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} callbacks.

    If you are using any custom or third-party [[spider middleware]{.std
    .std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
    .reference .internal}, see [[Mixing synchronous and asynchronous
    spider middlewares]{.std
    .std-ref}](#sync-async-spider-middleware){.hoverxref .tooltip
    .reference .internal}.

    ::: versionchanged
    [Changed in version 2.7: ]{.versionmodified .changed}Output of async
    callbacks is now processed asynchronously instead of collecting all
    of it first.
    :::

-   The [[`process_item()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#process_item "process_item"){.reference
    .internal} method of [[item pipelines]{.std
    .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
    .reference .internal}.

-   The [[`process_request()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.DownloaderMiddleware.process_request "scrapy.downloadermiddlewares.DownloaderMiddleware.process_request"){.reference
    .internal}, [[`process_response()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
    .internal}, and [[`process_exception()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
    .internal} methods of [[downloader middlewares]{.std
    .std-ref}](index.html#topics-downloader-middleware-custom){.hoverxref
    .tooltip .reference .internal}.

-   [[Signal handlers that support deferreds]{.std
    .std-ref}](index.html#signal-deferred){.hoverxref .tooltip
    .reference .internal}.

-   The [[`process_spider_output()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
    .internal} method of [[spider middlewares]{.std
    .std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
    .reference .internal}.

    It must be defined as an [[asynchronous generator]{.xref .std
    .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-generator "(in Python v3.12)"){.reference
    .external}. The input [`result`{.docutils .literal
    .notranslate}]{.pre} parameter is an [[asynchronous iterable]{.xref
    .std
    .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-iterable "(in Python v3.12)"){.reference
    .external}.

    See also [[Mixing synchronous and asynchronous spider
    middlewares]{.std
    .std-ref}](#sync-async-spider-middleware){.hoverxref .tooltip
    .reference .internal} and [[Universal spider middlewares]{.std
    .std-ref}](#universal-spider-middleware){.hoverxref .tooltip
    .reference .internal}.

    ::: versionadded
    [New in version 2.7.]{.versionmodified .added}
    :::
:::

::: {#general-usage .section}
#### General usage[¶](#general-usage "Permalink to this heading"){.headerlink}

There are several use cases for coroutines in Scrapy.

Code that would return Deferreds when written for previous Scrapy
versions, such as downloader middlewares and signal handlers, can be
rewritten to be shorter and cleaner:

::: {.highlight-python .notranslate}
::: highlight
    from itemadapter import ItemAdapter


    class DbPipeline:
        def _update_item(self, data, item):
            adapter = ItemAdapter(item)
            adapter["field"] = data
            return item

        def process_item(self, item, spider):
            adapter = ItemAdapter(item)
            dfd = db.get_some_data(adapter["id"])
            dfd.addCallback(self._update_item, item)
            return dfd
:::
:::

becomes:

::: {.highlight-python .notranslate}
::: highlight
    from itemadapter import ItemAdapter


    class DbPipeline:
        async def process_item(self, item, spider):
            adapter = ItemAdapter(item)
            adapter["field"] = await db.get_some_data(adapter["id"])
            return item
:::
:::

Coroutines may be used to call asynchronous code. This includes other
coroutines, functions that return Deferreds and functions that return
[[awaitable objects]{.xref .std
.std-term}](https://docs.python.org/3/glossary.html#term-awaitable "(in Python v3.12)"){.reference
.external} such as [[`Future`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-future.html#asyncio.Future "(in Python v3.12)"){.reference
.external}. This means you can use many useful Python libraries
providing such code:

::: {.highlight-python .notranslate}
::: highlight
    class MySpiderDeferred(Spider):
        # ...
        async def parse(self, response):
            additional_response = await treq.get("https://additional.url")
            additional_data = await treq.content(additional_response)
            # ... use response and additional_data to yield items and requests


    class MySpiderAsyncio(Spider):
        # ...
        async def parse(self, response):
            async with aiohttp.ClientSession() as session:
                async with session.get("https://additional.url") as additional_response:
                    additional_data = await additional_response.text()
            # ... use response and additional_data to yield items and requests
:::
:::

::: {.admonition .note}
Note

Many libraries that use coroutines, such as
[aio-libs](https://github.com/aio-libs){.reference .external}, require
the [[`asyncio`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
.external} loop and to use them you need to [[enable asyncio support in
Scrapy]{.doc}](index.html#document-topics/asyncio){.reference
.internal}.
:::

::: {.admonition .note}
Note

If you want to [`await`{.docutils .literal .notranslate}]{.pre} on
Deferreds while using the asyncio reactor, you need to [[wrap them]{.std
.std-ref}](index.html#asyncio-await-dfd){.hoverxref .tooltip .reference
.internal}.
:::

Common use cases for asynchronous code include:

-   requesting data from websites, databases and other services (in
    callbacks, pipelines and middlewares);

-   storing data in databases (in pipelines and middlewares);

-   delaying the spider initialization until some external event (in the
    [[`spider_opened`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-spider_opened){.hoverxref
    .tooltip .reference .internal} handler);

-   calling asynchronous Scrapy methods like
    [`ExecutionEngine.download()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} (see [[the screenshot pipeline example]{.std
    .std-ref}](index.html#screenshotpipeline){.hoverxref .tooltip
    .reference .internal}).
:::

::: {#inline-requests .section}
[]{#id1}

#### Inline requests[¶](#inline-requests "Permalink to this heading"){.headerlink}

The spider below shows how to send a request and await its response all
from within a spider callback:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy import Spider, Request
    from scrapy.utils.defer import maybe_deferred_to_future


    class SingleRequestSpider(Spider):
        name = "single"
        start_urls = ["https://example.org/product"]

        async def parse(self, response, **kwargs):
            additional_request = Request("https://example.org/price")
            deferred = self.crawler.engine.download(additional_request)
            additional_response = await maybe_deferred_to_future(deferred)
            yield {
                "h1": response.css("h1").get(),
                "price": additional_response.css("#price").get(),
            }
:::
:::

You can also send multiple requests in parallel:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy import Spider, Request
    from scrapy.utils.defer import maybe_deferred_to_future
    from twisted.internet.defer import DeferredList


    class MultipleRequestsSpider(Spider):
        name = "multiple"
        start_urls = ["https://example.com/product"]

        async def parse(self, response, **kwargs):
            additional_requests = [
                Request("https://example.com/price"),
                Request("https://example.com/color"),
            ]
            deferreds = []
            for r in additional_requests:
                deferred = self.crawler.engine.download(r)
                deferreds.append(deferred)
            responses = await maybe_deferred_to_future(DeferredList(deferreds))
            yield {
                "h1": response.css("h1::text").get(),
                "price": responses[0][1].css(".price::text").get(),
                "price2": responses[1][1].css(".color::text").get(),
            }
:::
:::
:::

::: {#mixing-synchronous-and-asynchronous-spider-middlewares .section}
[]{#sync-async-spider-middleware}

#### Mixing synchronous and asynchronous spider middlewares[¶](#mixing-synchronous-and-asynchronous-spider-middlewares "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.7.]{.versionmodified .added}
:::

The output of a [`Request`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} callback is passed as the [`result`{.docutils
.literal .notranslate}]{.pre} parameter to the
[[`process_spider_output()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
.internal} method of the first [[spider middleware]{.std
.std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
.reference .internal} from the [[list of active spider middlewares]{.std
.std-ref}](index.html#topics-spider-middleware-setting){.hoverxref
.tooltip .reference .internal}. Then the output of that
[`process_spider_output`{.docutils .literal .notranslate}]{.pre} method
is passed to the [`process_spider_output`{.docutils .literal
.notranslate}]{.pre} method of the next spider middleware, and so on for
every active spider middleware.

Scrapy supports mixing [[coroutine methods]{.xref .std
.std-ref}](https://docs.python.org/3/reference/compound_stmts.html#async "(in Python v3.12)"){.reference
.external} and synchronous methods in this chain of calls.

However, if any of the [`process_spider_output`{.docutils .literal
.notranslate}]{.pre} methods is defined as a synchronous method, and the
previous [`Request`{.docutils .literal .notranslate}]{.pre} callback or
[`process_spider_output`{.docutils .literal .notranslate}]{.pre} method
is a coroutine, there are some drawbacks to the
asynchronous-to-synchronous conversion that Scrapy does so that the
synchronous [`process_spider_output`{.docutils .literal
.notranslate}]{.pre} method gets a synchronous iterable as its
[`result`{.docutils .literal .notranslate}]{.pre} parameter:

-   The whole output of the previous [`Request`{.docutils .literal
    .notranslate}]{.pre} callback or [`process_spider_output`{.docutils
    .literal .notranslate}]{.pre} method is awaited at this point.

-   If an exception raises while awaiting the output of the previous
    [`Request`{.docutils .literal .notranslate}]{.pre} callback or
    [`process_spider_output`{.docutils .literal .notranslate}]{.pre}
    method, none of that output will be processed.

    This contrasts with the regular behavior, where all items yielded
    before an exception raises are processed.

Asynchronous-to-synchronous conversions are supported for backward
compatibility, but they are deprecated and will stop working in a future
version of Scrapy.

To avoid asynchronous-to-synchronous conversions, when defining
[`Request`{.docutils .literal .notranslate}]{.pre} callbacks as
coroutine methods or when using spider middlewares whose
[`process_spider_output`{.docutils .literal .notranslate}]{.pre} method
is an [[asynchronous generator]{.xref .std
.std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-generator "(in Python v3.12)"){.reference
.external}, all active spider middlewares must either have their
[`process_spider_output`{.docutils .literal .notranslate}]{.pre} method
defined as an asynchronous generator or [[define a
process_spider_output_async method]{.std
.std-ref}](#universal-spider-middleware){.hoverxref .tooltip .reference
.internal}.

::: {.admonition .note}
Note

When using third-party spider middlewares that only define a synchronous
[`process_spider_output`{.docutils .literal .notranslate}]{.pre} method,
consider [[making them universal]{.std
.std-ref}](#universal-spider-middleware){.hoverxref .tooltip .reference
.internal} through [[subclassing]{.xref .std
.std-ref}](https://docs.python.org/3/tutorial/classes.html#tut-inheritance "(in Python v3.12)"){.reference
.external}.
:::
:::

::: {#universal-spider-middlewares .section}
[]{#universal-spider-middleware}

#### Universal spider middlewares[¶](#universal-spider-middlewares "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.7.]{.versionmodified .added}
:::

To allow writing a spider middleware that supports asynchronous
execution of its [`process_spider_output`{.docutils .literal
.notranslate}]{.pre} method in Scrapy 2.7 and later (avoiding
[[asynchronous-to-synchronous conversions]{.std
.std-ref}](#sync-async-spider-middleware){.hoverxref .tooltip .reference
.internal}) while maintaining support for older Scrapy versions, you may
define [`process_spider_output`{.docutils .literal .notranslate}]{.pre}
as a synchronous method and define an [[asynchronous generator]{.xref
.std
.std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-generator "(in Python v3.12)"){.reference
.external} version of that method with an alternative name:
[`process_spider_output_async`{.docutils .literal .notranslate}]{.pre}.

For example:

::: {.highlight-python .notranslate}
::: highlight
    class UniversalSpiderMiddleware:
        def process_spider_output(self, response, result, spider):
            for r in result:
                # ... do something with r
                yield r

        async def process_spider_output_async(self, response, result, spider):
            async for r in result:
                # ... do something with r
                yield r
:::
:::

::: {.admonition .note}
Note

This is an interim measure to allow, for a time, to write code that
works in Scrapy 2.7 and later without requiring
asynchronous-to-synchronous conversions, and works in earlier Scrapy
versions as well.

In some future version of Scrapy, however, this feature will be
deprecated and, eventually, in a later version of Scrapy, this feature
will be removed, and all spider middlewares will be expected to define
their [`process_spider_output`{.docutils .literal .notranslate}]{.pre}
method as an asynchronous generator.
:::
:::
:::

[]{#document-topics/asyncio}

::: {#asyncio .section}
[]{#using-asyncio}

### asyncio[¶](#asyncio "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.0.]{.versionmodified .added}
:::

Scrapy has partial support for [[`asyncio`{.xref .py .py-mod .docutils
.literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
.external}. After you [[install the asyncio reactor]{.std
.std-ref}](#install-asyncio){.hoverxref .tooltip .reference .internal},
you may use [[`asyncio`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
.external} and [[`asyncio`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
.external}-powered libraries in any
[[coroutine]{.doc}](index.html#document-topics/coroutines){.reference
.internal}.

::: {#installing-the-asyncio-reactor .section}
[]{#install-asyncio}

#### Installing the asyncio reactor[¶](#installing-the-asyncio-reactor "Permalink to this heading"){.headerlink}

To enable [[`asyncio`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
.external} support, set the [[`TWISTED_REACTOR`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
.tooltip .reference .internal} setting to
[`'twisted.internet.asyncioreactor.AsyncioSelectorReactor'`{.docutils
.literal .notranslate}]{.pre}.

If you are using [[`CrawlerRunner`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
.internal}, you also need to install the
[[`AsyncioSelectorReactor`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.asyncioreactor.AsyncioSelectorReactor.html "(in Twisted)"){.reference
.external} reactor manually. You can do that using
[[`install_reactor()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.utils.reactor.install_reactor "scrapy.utils.reactor.install_reactor"){.reference
.internal}:

::: {.highlight-default .notranslate}
::: highlight
    install_reactor('twisted.internet.asyncioreactor.AsyncioSelectorReactor')
:::
:::
:::

::: {#handling-a-pre-installed-reactor .section}
[]{#asyncio-preinstalled-reactor}

#### Handling a pre-installed reactor[¶](#handling-a-pre-installed-reactor "Permalink to this heading"){.headerlink}

[`twisted.internet.reactor`{.docutils .literal .notranslate}]{.pre} and
some other Twisted imports install the default Twisted reactor as a side
effect. Once a Twisted reactor is installed, it is not possible to
switch to a different reactor at run time.

If you [[configure the asyncio Twisted reactor]{.std
.std-ref}](#install-asyncio){.hoverxref .tooltip .reference .internal}
and, at run time, Scrapy complains that a different reactor is already
installed, chances are you have some such imports in your code.

You can usually fix the issue by moving those offending module-level
Twisted imports to the method or function definitions where they are
used. For example, if you have something like:

::: {.highlight-python .notranslate}
::: highlight