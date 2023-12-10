    cc00ad2](https://github.com/scrapy/scrapy/commit/cc00ad2){.reference
    .external})

-   include tests/ to source distribution in MANIFEST.in ([commit
    eca227e](https://github.com/scrapy/scrapy/commit/eca227e){.reference
    .external})

-   DOC Fix SelectJmes documentation ([commit
    b8567bc](https://github.com/scrapy/scrapy/commit/b8567bc){.reference
    .external})

-   DOC Bring Ubuntu and Archlinux outside of Windows subsection
    ([commit
    392233f](https://github.com/scrapy/scrapy/commit/392233f){.reference
    .external})

-   DOC remove version suffix from Ubuntu package ([commit
    5303c66](https://github.com/scrapy/scrapy/commit/5303c66){.reference
    .external})

-   DOC Update release date for 1.0 ([commit
    c89fa29](https://github.com/scrapy/scrapy/commit/c89fa29){.reference
    .external})
:::

::: {#scrapy-1-0-0-2015-06-19 .section}
[]{#release-1-0-0}

#### Scrapy 1.0.0 (2015-06-19)[¶](#scrapy-1-0-0-2015-06-19 "Permalink to this heading"){.headerlink}

You will find a lot of new features and bugfixes in this major release.
Make sure to check our updated [[overview]{.std
.std-ref}](index.html#intro-overview){.hoverxref .tooltip .reference
.internal} to get a glance of some of the changes, along with our
brushed [[tutorial]{.std
.std-ref}](index.html#intro-tutorial){.hoverxref .tooltip .reference
.internal}.

::: {#support-for-returning-dictionaries-in-spiders .section}
##### Support for returning dictionaries in spiders[¶](#support-for-returning-dictionaries-in-spiders "Permalink to this heading"){.headerlink}

Declaring and returning Scrapy Items is no longer necessary to collect
the scraped data from your spider, you can now return explicit
dictionaries instead.

*Classic version*

::: {.highlight-default .notranslate}
::: highlight
    class MyItem(scrapy.Item):
        url = scrapy.Field()

    class MySpider(scrapy.Spider):
        def parse(self, response):
            return MyItem(url=response.url)
:::
:::

*New version*

::: {.highlight-default .notranslate}
::: highlight
    class MySpider(scrapy.Spider):
        def parse(self, response):
            return {'url': response.url}
:::
:::
:::

::: {#per-spider-settings-gsoc-2014 .section}
##### Per-spider settings (GSoC 2014)[¶](#per-spider-settings-gsoc-2014 "Permalink to this heading"){.headerlink}

Last Google Summer of Code project accomplished an important redesign of
the mechanism used for populating settings, introducing explicit
priorities to override any given setting. As an extension of that goal,
we included a new level of priority for settings that act exclusively
for a single spider, allowing them to redefine project settings.

Start using it by defining a [`custom_settings`{.xref .py .py-attr
.docutils .literal .notranslate}]{.pre} class variable in your spider:

::: {.highlight-default .notranslate}
::: highlight
    class MySpider(scrapy.Spider):
        custom_settings = {
            "DOWNLOAD_DELAY": 5.0,
            "RETRY_ENABLED": False,
        }
:::
:::

Read more about settings population: [[Settings]{.std
.std-ref}](index.html#topics-settings){.hoverxref .tooltip .reference
.internal}
:::

::: {#python-logging .section}
##### Python Logging[¶](#python-logging "Permalink to this heading"){.headerlink}

Scrapy 1.0 has moved away from Twisted logging to support Python built
in's as default logging system. We're maintaining backward compatibility
for most of the old custom interface to call logging functions, but
you'll get warnings to switch to the Python logging API entirely.

*Old version*

::: {.highlight-default .notranslate}
::: highlight
    from scrapy import log
    log.msg('MESSAGE', log.INFO)
:::
:::

*New version*

::: {.highlight-default .notranslate}
::: highlight
    import logging
    logging.info('MESSAGE')
:::
:::

Logging with spiders remains the same, but on top of the [`log()`{.xref
.py .py-meth .docutils .literal .notranslate}]{.pre} method you'll have
access to a custom [`logger`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} created for the spider to issue log events:

::: {.highlight-default .notranslate}
::: highlight
    class MySpider(scrapy.Spider):
        def parse(self, response):
            self.logger.info('Response received')
:::
:::

Read more in the logging documentation: [[Logging]{.std
.std-ref}](index.html#topics-logging){.hoverxref .tooltip .reference
.internal}
:::

::: {#crawler-api-refactoring-gsoc-2014 .section}
##### Crawler API refactoring (GSoC 2014)[¶](#crawler-api-refactoring-gsoc-2014 "Permalink to this heading"){.headerlink}

Another milestone for last Google Summer of Code was a refactoring of
the internal API, seeking a simpler and easier usage. Check new core
interface in: [[Core API]{.std
.std-ref}](index.html#topics-api){.hoverxref .tooltip .reference
.internal}

A common situation where you will face these changes is while running
Scrapy from scripts. Here's a quick example of how to run a Spider
manually with the new API:

::: {.highlight-default .notranslate}
::: highlight
    from scrapy.crawler import CrawlerProcess

    process = CrawlerProcess({
        'USER_AGENT': 'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)'
    })
    process.crawl(MySpider)
    process.start()
:::
:::

Bear in mind this feature is still under development and its API may
change until it reaches a stable status.

See more examples for scripts running Scrapy: [[Common Practices]{.std
.std-ref}](index.html#topics-practices){.hoverxref .tooltip .reference
.internal}
:::

::: {#module-relocations .section}
[]{#id128}

##### Module Relocations[¶](#module-relocations "Permalink to this heading"){.headerlink}

There's been a large rearrangement of modules trying to improve the
general structure of Scrapy. Main changes were separating various
subpackages into new projects and dissolving both
[`scrapy.contrib`{.docutils .literal .notranslate}]{.pre} and
[`scrapy.contrib_exp`{.docutils .literal .notranslate}]{.pre} into top
level packages. Backward compatibility was kept among internal
relocations, while importing deprecated modules expect warnings
indicating their new place.

::: {#full-list-of-relocations .section}
###### Full list of relocations[¶](#full-list-of-relocations "Permalink to this heading"){.headerlink}

Outsourced packages

::: {.admonition .note}
Note

These extensions went through some minor changes, e.g. some setting
names were changed. Please check the documentation in each new
repository to get familiar with the new usage.
:::

+-----------------------------------+-----------------------------------+
| Old location                      | New location                      |
+===================================+===================================+
| scrapy.commands.deploy            | [sc                               |
|                                   | rapyd-client](https://github.com/ |
|                                   | scrapy/scrapyd-client){.reference |
|                                   | .external} (See other             |
|                                   | alternatives here: [[Deploying    |
|                                   | Spiders]{.std                     |
|                                   | .std-ref}](ind                    |
|                                   | ex.html#topics-deploy){.hoverxref |
|                                   | .tooltip .reference .internal})   |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.djangoitem         | [scrapy-djangoite                 |
|                                   | m](https://github.com/scrapy-plug |
|                                   | ins/scrapy-djangoitem){.reference |
|                                   | .external}                        |
+-----------------------------------+-----------------------------------+
| scrapy.webservice                 | [scrapy-jso                       |
|                                   | nrpc](https://github.com/scrapy-p |
|                                   | lugins/scrapy-jsonrpc){.reference |
|                                   | .external}                        |
+-----------------------------------+-----------------------------------+

[`scrapy.contrib_exp`{.docutils .literal .notranslate}]{.pre} and
[`scrapy.contrib`{.docutils .literal .notranslate}]{.pre} dissolutions

+-----------------------------------+-----------------------------------+
| Old location                      | New location                      |
+===================================+===================================+
| scrapy.contrib_exp.d              | scrapy.do                         |
| ownloadermiddleware.decompression | wnloadermiddlewares.decompression |
+-----------------------------------+-----------------------------------+
| scrapy.contrib_exp.iterators      | scrapy.utils.iterators            |
+-----------------------------------+-----------------------------------+
| sc                                | scrapy.downloadermiddlewares      |
| rapy.contrib.downloadermiddleware |                                   |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.exporter           | scrapy.exporters                  |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.linkextractors     | scrapy.linkextractors             |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.loader             | scrapy.loader                     |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.loader.processor   | scrapy.loader.processors          |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.pipeline           | scrapy.pipelines                  |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.spidermiddleware   | scrapy.spidermiddlewares          |
+-----------------------------------+-----------------------------------+
| scrapy.contrib.spiders            | scrapy.spiders                    |
+-----------------------------------+-----------------------------------+
| -   scrapy.contrib.closespider    | scrapy.extensions.\*              |
|                                   |                                   |
| -   scrapy.contrib.corestats      |                                   |
|                                   |                                   |
| -   scrapy.contrib.debug          |                                   |
|                                   |                                   |
| -   scrapy.contrib.feedexport     |                                   |
|                                   |                                   |
| -   scrapy.contrib.httpcache      |                                   |
|                                   |                                   |
| -   scrapy.contrib.logstats       |                                   |
|                                   |                                   |
| -   scrapy.contrib.memdebug       |                                   |
|                                   |                                   |
| -   scrapy.contrib.memusage       |                                   |
|                                   |                                   |
| -   scrapy.contrib.spiderstate    |                                   |
|                                   |                                   |
| -   scrapy.contrib.statsmailer    |                                   |
|                                   |                                   |
| -   scrapy.contrib.throttle       |                                   |
+-----------------------------------+-----------------------------------+

Plural renames and Modules unification

+-----------------------------------+-----------------------------------+
| Old location                      | New location                      |
+===================================+===================================+
| scrapy.command                    | scrapy.commands                   |
+-----------------------------------+-----------------------------------+
| scrapy.dupefilter                 | scrapy.dupefilters                |
+-----------------------------------+-----------------------------------+
| scrapy.linkextractor              | scrapy.linkextractors             |
+-----------------------------------+-----------------------------------+
| scrapy.spider                     | scrapy.spiders                    |
+-----------------------------------+-----------------------------------+
| scrapy.squeue                     | scrapy.squeues                    |
+-----------------------------------+-----------------------------------+
| scrapy.statscol                   | scrapy.statscollectors            |
+-----------------------------------+-----------------------------------+
| scrapy.utils.decorator            | scrapy.utils.decorators           |
+-----------------------------------+-----------------------------------+

Class renames

+-----------------------------------+-----------------------------------+
| Old location                      | New location                      |
+===================================+===================================+
| s                                 | scrapy.spiderloader.SpiderLoader  |
| crapy.spidermanager.SpiderManager |                                   |
+-----------------------------------+-----------------------------------+

Settings renames

+-----------------------------------+-----------------------------------+
| Old location                      | New location                      |
+===================================+===================================+
| SPIDER_MANAGER_CLASS              | SPIDER_LOADER_CLASS               |
+-----------------------------------+-----------------------------------+
:::
:::

::: {#changelog .section}
##### Changelog[¶](#changelog "Permalink to this heading"){.headerlink}

New Features and Enhancements

-   Python logging ([issue
    1060](https://github.com/scrapy/scrapy/issues/1060){.reference
    .external}, [issue
    1235](https://github.com/scrapy/scrapy/issues/1235){.reference
    .external}, [issue
    1236](https://github.com/scrapy/scrapy/issues/1236){.reference
    .external}, [issue
    1240](https://github.com/scrapy/scrapy/issues/1240){.reference
    .external}, [issue
    1259](https://github.com/scrapy/scrapy/issues/1259){.reference
    .external}, [issue
    1278](https://github.com/scrapy/scrapy/issues/1278){.reference
    .external}, [issue
    1286](https://github.com/scrapy/scrapy/issues/1286){.reference
    .external})

-   FEED_EXPORT_FIELDS option ([issue
    1159](https://github.com/scrapy/scrapy/issues/1159){.reference
    .external}, [issue
    1224](https://github.com/scrapy/scrapy/issues/1224){.reference
    .external})

-   Dns cache size and timeout options ([issue
    1132](https://github.com/scrapy/scrapy/issues/1132){.reference
    .external})

-   support namespace prefix in xmliter_lxml ([issue
    963](https://github.com/scrapy/scrapy/issues/963){.reference
    .external})

-   Reactor threadpool max size setting ([issue
    1123](https://github.com/scrapy/scrapy/issues/1123){.reference
    .external})

-   Allow spiders to return dicts. ([issue
    1081](https://github.com/scrapy/scrapy/issues/1081){.reference
    .external})

-   Add Response.urljoin() helper ([issue
    1086](https://github.com/scrapy/scrapy/issues/1086){.reference
    .external})

-   look in \~/.config/scrapy.cfg for user config ([issue
    1098](https://github.com/scrapy/scrapy/issues/1098){.reference
    .external})

-   handle TLS SNI ([issue
    1101](https://github.com/scrapy/scrapy/issues/1101){.reference
    .external})

-   Selectorlist extract first ([issue
    624](https://github.com/scrapy/scrapy/issues/624){.reference
    .external}, [issue
    1145](https://github.com/scrapy/scrapy/issues/1145){.reference
    .external})

-   Added JmesSelect ([issue
    1016](https://github.com/scrapy/scrapy/issues/1016){.reference
    .external})

-   add gzip compression to filesystem http cache backend ([issue
    1020](https://github.com/scrapy/scrapy/issues/1020){.reference
    .external})

-   CSS support in link extractors ([issue
    983](https://github.com/scrapy/scrapy/issues/983){.reference
    .external})

-   httpcache dont_cache meta #19 #689 ([issue
    821](https://github.com/scrapy/scrapy/issues/821){.reference
    .external})

-   add signal to be sent when request is dropped by the scheduler
    ([issue 961](https://github.com/scrapy/scrapy/issues/961){.reference
    .external})

-   avoid download large response ([issue
    946](https://github.com/scrapy/scrapy/issues/946){.reference
    .external})

-   Allow to specify the quotechar in CSVFeedSpider ([issue
    882](https://github.com/scrapy/scrapy/issues/882){.reference
    .external})

-   Add referer to "Spider error processing" log message ([issue
    795](https://github.com/scrapy/scrapy/issues/795){.reference
    .external})

-   process robots.txt once ([issue
    896](https://github.com/scrapy/scrapy/issues/896){.reference
    .external})

-   GSoC Per-spider settings ([issue
    854](https://github.com/scrapy/scrapy/issues/854){.reference
    .external})

-   Add project name validation ([issue
    817](https://github.com/scrapy/scrapy/issues/817){.reference
    .external})

-   GSoC API cleanup ([issue
    816](https://github.com/scrapy/scrapy/issues/816){.reference
    .external}, [issue
    1128](https://github.com/scrapy/scrapy/issues/1128){.reference
    .external}, [issue
    1147](https://github.com/scrapy/scrapy/issues/1147){.reference
    .external}, [issue
    1148](https://github.com/scrapy/scrapy/issues/1148){.reference
    .external}, [issue
    1156](https://github.com/scrapy/scrapy/issues/1156){.reference
    .external}, [issue
    1185](https://github.com/scrapy/scrapy/issues/1185){.reference
    .external}, [issue
    1187](https://github.com/scrapy/scrapy/issues/1187){.reference
    .external}, [issue
    1258](https://github.com/scrapy/scrapy/issues/1258){.reference
    .external}, [issue
    1268](https://github.com/scrapy/scrapy/issues/1268){.reference
    .external}, [issue
    1276](https://github.com/scrapy/scrapy/issues/1276){.reference
    .external}, [issue
    1285](https://github.com/scrapy/scrapy/issues/1285){.reference
    .external}, [issue
    1284](https://github.com/scrapy/scrapy/issues/1284){.reference
    .external})

-   Be more responsive with IO operations ([issue
    1074](https://github.com/scrapy/scrapy/issues/1074){.reference
    .external} and [issue
    1075](https://github.com/scrapy/scrapy/issues/1075){.reference
    .external})

-   Do leveldb compaction for httpcache on closing ([issue
    1297](https://github.com/scrapy/scrapy/issues/1297){.reference
    .external})

Deprecations and Removals

-   Deprecate htmlparser link extractor ([issue
    1205](https://github.com/scrapy/scrapy/issues/1205){.reference
    .external})

-   remove deprecated code from FeedExporter ([issue
    1155](https://github.com/scrapy/scrapy/issues/1155){.reference
    .external})

-   a leftover for.15 compatibility ([issue
    925](https://github.com/scrapy/scrapy/issues/925){.reference
    .external})

-   drop support for CONCURRENT_REQUESTS_PER_SPIDER ([issue
    895](https://github.com/scrapy/scrapy/issues/895){.reference
    .external})

-   Drop old engine code ([issue
    911](https://github.com/scrapy/scrapy/issues/911){.reference
    .external})

-   Deprecate SgmlLinkExtractor ([issue
    777](https://github.com/scrapy/scrapy/issues/777){.reference
    .external})

Relocations

-   Move exporters/\_\_init\_\_.py to exporters.py ([issue
    1242](https://github.com/scrapy/scrapy/issues/1242){.reference
    .external})

-   Move base classes to their packages ([issue
    1218](https://github.com/scrapy/scrapy/issues/1218){.reference
    .external}, [issue
    1233](https://github.com/scrapy/scrapy/issues/1233){.reference
    .external})

-   Module relocation ([issue
    1181](https://github.com/scrapy/scrapy/issues/1181){.reference
    .external}, [issue
    1210](https://github.com/scrapy/scrapy/issues/1210){.reference
    .external})

-   rename SpiderManager to SpiderLoader ([issue
    1166](https://github.com/scrapy/scrapy/issues/1166){.reference
    .external})

-   Remove djangoitem ([issue
    1177](https://github.com/scrapy/scrapy/issues/1177){.reference
    .external})

-   remove scrapy deploy command ([issue
    1102](https://github.com/scrapy/scrapy/issues/1102){.reference
    .external})

-   dissolve contrib_exp ([issue
    1134](https://github.com/scrapy/scrapy/issues/1134){.reference
    .external})

-   Deleted bin folder from root, fixes #913 ([issue
    914](https://github.com/scrapy/scrapy/issues/914){.reference
    .external})

-   Remove jsonrpc based webservice ([issue
    859](https://github.com/scrapy/scrapy/issues/859){.reference
    .external})

-   Move Test cases under project root dir ([issue
    827](https://github.com/scrapy/scrapy/issues/827){.reference
    .external}, [issue
    841](https://github.com/scrapy/scrapy/issues/841){.reference
    .external})

-   Fix backward incompatibility for relocated paths in settings ([issue
    1267](https://github.com/scrapy/scrapy/issues/1267){.reference
    .external})

Documentation

-   CrawlerProcess documentation ([issue
    1190](https://github.com/scrapy/scrapy/issues/1190){.reference
    .external})

-   Favoring web scraping over screen scraping in the descriptions
    ([issue
    1188](https://github.com/scrapy/scrapy/issues/1188){.reference
    .external})

-   Some improvements for Scrapy tutorial ([issue
    1180](https://github.com/scrapy/scrapy/issues/1180){.reference
    .external})

-   Documenting Files Pipeline together with Images Pipeline ([issue
    1150](https://github.com/scrapy/scrapy/issues/1150){.reference
    .external})

-   deployment docs tweaks ([issue
    1164](https://github.com/scrapy/scrapy/issues/1164){.reference
    .external})

-   Added deployment section covering scrapyd-deploy and shub ([issue
    1124](https://github.com/scrapy/scrapy/issues/1124){.reference
    .external})

-   Adding more settings to project template ([issue
    1073](https://github.com/scrapy/scrapy/issues/1073){.reference
    .external})

-   some improvements to overview page ([issue
    1106](https://github.com/scrapy/scrapy/issues/1106){.reference
    .external})

-   Updated link in docs/topics/architecture.rst ([issue
    647](https://github.com/scrapy/scrapy/issues/647){.reference
    .external})

-   DOC reorder topics ([issue
    1022](https://github.com/scrapy/scrapy/issues/1022){.reference
    .external})

-   updating list of Request.meta special keys ([issue
    1071](https://github.com/scrapy/scrapy/issues/1071){.reference
    .external})

-   DOC document download_timeout ([issue
    898](https://github.com/scrapy/scrapy/issues/898){.reference
    .external})

-   DOC simplify extension docs ([issue
    893](https://github.com/scrapy/scrapy/issues/893){.reference
    .external})

-   Leaks docs ([issue
    894](https://github.com/scrapy/scrapy/issues/894){.reference
    .external})

-   DOC document from_crawler method for item pipelines ([issue
    904](https://github.com/scrapy/scrapy/issues/904){.reference
    .external})

-   Spider_error doesn't support deferreds ([issue
    1292](https://github.com/scrapy/scrapy/issues/1292){.reference
    .external})

-   Corrections & Sphinx related fixes ([issue
    1220](https://github.com/scrapy/scrapy/issues/1220){.reference
    .external}, [issue
    1219](https://github.com/scrapy/scrapy/issues/1219){.reference
    .external}, [issue
    1196](https://github.com/scrapy/scrapy/issues/1196){.reference
    .external}, [issue
    1172](https://github.com/scrapy/scrapy/issues/1172){.reference
    .external}, [issue
    1171](https://github.com/scrapy/scrapy/issues/1171){.reference
    .external}, [issue
    1169](https://github.com/scrapy/scrapy/issues/1169){.reference
    .external}, [issue
    1160](https://github.com/scrapy/scrapy/issues/1160){.reference
    .external}, [issue
    1154](https://github.com/scrapy/scrapy/issues/1154){.reference
    .external}, [issue
    1127](https://github.com/scrapy/scrapy/issues/1127){.reference
    .external}, [issue
    1112](https://github.com/scrapy/scrapy/issues/1112){.reference
    .external}, [issue
    1105](https://github.com/scrapy/scrapy/issues/1105){.reference
    .external}, [issue
    1041](https://github.com/scrapy/scrapy/issues/1041){.reference
    .external}, [issue
    1082](https://github.com/scrapy/scrapy/issues/1082){.reference
    .external}, [issue
    1033](https://github.com/scrapy/scrapy/issues/1033){.reference
    .external}, [issue
    944](https://github.com/scrapy/scrapy/issues/944){.reference
    .external}, [issue
    866](https://github.com/scrapy/scrapy/issues/866){.reference
    .external}, [issue
    864](https://github.com/scrapy/scrapy/issues/864){.reference
    .external}, [issue
    796](https://github.com/scrapy/scrapy/issues/796){.reference
    .external}, [issue
    1260](https://github.com/scrapy/scrapy/issues/1260){.reference
    .external}, [issue
    1271](https://github.com/scrapy/scrapy/issues/1271){.reference
    .external}, [issue
    1293](https://github.com/scrapy/scrapy/issues/1293){.reference
    .external}, [issue
    1298](https://github.com/scrapy/scrapy/issues/1298){.reference
    .external})

Bugfixes

-   Item multi inheritance fix ([issue
    353](https://github.com/scrapy/scrapy/issues/353){.reference
    .external}, [issue
    1228](https://github.com/scrapy/scrapy/issues/1228){.reference
    .external})

-   ItemLoader.load_item: iterate over copy of fields ([issue
    722](https://github.com/scrapy/scrapy/issues/722){.reference
    .external})

-   Fix Unhandled error in Deferred (RobotsTxtMiddleware) ([issue
    1131](https://github.com/scrapy/scrapy/issues/1131){.reference
    .external}, [issue
    1197](https://github.com/scrapy/scrapy/issues/1197){.reference
    .external})

-   Force to read DOWNLOAD_TIMEOUT as int ([issue
    954](https://github.com/scrapy/scrapy/issues/954){.reference
    .external})

-   scrapy.utils.misc.load_object should print full traceback ([issue
    902](https://github.com/scrapy/scrapy/issues/902){.reference
    .external})

-   Fix bug for ".local" host name ([issue
    878](https://github.com/scrapy/scrapy/issues/878){.reference
    .external})

-   Fix for Enabled extensions, middlewares, pipelines info not printed
    anymore ([issue
    879](https://github.com/scrapy/scrapy/issues/879){.reference
    .external})

-   fix dont_merge_cookies bad behaviour when set to false on meta
    ([issue 846](https://github.com/scrapy/scrapy/issues/846){.reference
    .external})

Python 3 In Progress Support

-   disable scrapy.telnet if twisted.conch is not available ([issue
    1161](https://github.com/scrapy/scrapy/issues/1161){.reference
    .external})

-   fix Python 3 syntax errors in ajaxcrawl.py ([issue
    1162](https://github.com/scrapy/scrapy/issues/1162){.reference
    .external})

-   more python3 compatibility changes for urllib ([issue
    1121](https://github.com/scrapy/scrapy/issues/1121){.reference
    .external})

-   assertItemsEqual was renamed to assertCountEqual in Python 3.
    ([issue
    1070](https://github.com/scrapy/scrapy/issues/1070){.reference
    .external})

-   Import unittest.mock if available. ([issue
    1066](https://github.com/scrapy/scrapy/issues/1066){.reference
    .external})

-   updated deprecated cgi.parse_qsl to use six's parse_qsl ([issue
    909](https://github.com/scrapy/scrapy/issues/909){.reference
    .external})

-   Prevent Python 3 port regressions ([issue
    830](https://github.com/scrapy/scrapy/issues/830){.reference
    .external})

-   PY3: use MutableMapping for python 3 ([issue
    810](https://github.com/scrapy/scrapy/issues/810){.reference
    .external})

-   PY3: use six.BytesIO and six.moves.cStringIO ([issue
    803](https://github.com/scrapy/scrapy/issues/803){.reference
    .external})

-   PY3: fix xmlrpclib and email imports ([issue
    801](https://github.com/scrapy/scrapy/issues/801){.reference
    .external})

-   PY3: use six for robotparser and urlparse ([issue
    800](https://github.com/scrapy/scrapy/issues/800){.reference
    .external})

-   PY3: use six.iterkeys, six.iteritems, and tempfile ([issue
    799](https://github.com/scrapy/scrapy/issues/799){.reference
    .external})

-   PY3: fix has_key and use six.moves.configparser ([issue
    798](https://github.com/scrapy/scrapy/issues/798){.reference
    .external})

-   PY3: use six.moves.cPickle ([issue
    797](https://github.com/scrapy/scrapy/issues/797){.reference
    .external})

-   PY3 make it possible to run some tests in Python3 ([issue
    776](https://github.com/scrapy/scrapy/issues/776){.reference
    .external})

Tests

-   remove unnecessary lines from py3-ignores ([issue
    1243](https://github.com/scrapy/scrapy/issues/1243){.reference
    .external})

-   Fix remaining warnings from pytest while collecting tests ([issue
    1206](https://github.com/scrapy/scrapy/issues/1206){.reference
    .external})

-   Add docs build to travis ([issue
    1234](https://github.com/scrapy/scrapy/issues/1234){.reference
    .external})

-   TST don't collect tests from deprecated modules. ([issue
    1165](https://github.com/scrapy/scrapy/issues/1165){.reference
    .external})

-   install service_identity package in tests to prevent warnings
    ([issue
    1168](https://github.com/scrapy/scrapy/issues/1168){.reference
    .external})

-   Fix deprecated settings API in tests ([issue
    1152](https://github.com/scrapy/scrapy/issues/1152){.reference
    .external})

-   Add test for webclient with POST method and no body given ([issue
    1089](https://github.com/scrapy/scrapy/issues/1089){.reference
    .external})

-   py3-ignores.txt supports comments ([issue
    1044](https://github.com/scrapy/scrapy/issues/1044){.reference
    .external})

-   modernize some of the asserts ([issue
    835](https://github.com/scrapy/scrapy/issues/835){.reference
    .external})

-   selector.\_\_repr\_\_ test ([issue
    779](https://github.com/scrapy/scrapy/issues/779){.reference
    .external})

Code refactoring

-   CSVFeedSpider cleanup: use iterate_spider_output ([issue
    1079](https://github.com/scrapy/scrapy/issues/1079){.reference
    .external})

-   remove unnecessary check from scrapy.utils.spider.iter_spider_output
    ([issue
    1078](https://github.com/scrapy/scrapy/issues/1078){.reference
    .external})

-   Pydispatch pep8 ([issue
    992](https://github.com/scrapy/scrapy/issues/992){.reference
    .external})

-   Removed unused 'load=False' parameter from walk_modules() ([issue
    871](https://github.com/scrapy/scrapy/issues/871){.reference
    .external})

-   For consistency, use [`job_dir`{.docutils .literal
    .notranslate}]{.pre} helper in [`SpiderState`{.docutils .literal
    .notranslate}]{.pre} extension. ([issue
    805](https://github.com/scrapy/scrapy/issues/805){.reference
    .external})

-   rename "sflo" local variables to less cryptic "log_observer" ([issue
    775](https://github.com/scrapy/scrapy/issues/775){.reference
    .external})
:::
:::

::: {#scrapy-0-24-6-2015-04-20 .section}
#### Scrapy 0.24.6 (2015-04-20)[¶](#scrapy-0-24-6-2015-04-20 "Permalink to this heading"){.headerlink}

-   encode invalid xpath with unicode_escape under PY2 ([commit
    07cb3e5](https://github.com/scrapy/scrapy/commit/07cb3e5){.reference
    .external})

-   fix IPython shell scope issue and load IPython user config ([commit
    2c8e573](https://github.com/scrapy/scrapy/commit/2c8e573){.reference
    .external})

-   Fix small typo in the docs ([commit
    d694019](https://github.com/scrapy/scrapy/commit/d694019){.reference
    .external})

-   Fix small typo ([commit
    f92fa83](https://github.com/scrapy/scrapy/commit/f92fa83){.reference
    .external})

-   Converted sel.xpath() calls to response.xpath() in Extracting the
    data ([commit
    c2c6d15](https://github.com/scrapy/scrapy/commit/c2c6d15){.reference
    .external})
:::

::: {#scrapy-0-24-5-2015-02-25 .section}
#### Scrapy 0.24.5 (2015-02-25)[¶](#scrapy-0-24-5-2015-02-25 "Permalink to this heading"){.headerlink}

-   Support new \_getEndpoint Agent signatures on Twisted 15.0.0
    ([commit
    540b9bc](https://github.com/scrapy/scrapy/commit/540b9bc){.reference
    .external})

-   DOC a couple more references are fixed ([commit
    b4c454b](https://github.com/scrapy/scrapy/commit/b4c454b){.reference
    .external})

-   DOC fix a reference ([commit
    e3c1260](https://github.com/scrapy/scrapy/commit/e3c1260){.reference
    .external})

-   t.i.b.ThreadedResolver is now a new-style class ([commit
    9e13f42](https://github.com/scrapy/scrapy/commit/9e13f42){.reference
    .external})

-   S3DownloadHandler: fix auth for requests with quoted paths/query
    params ([commit
    cdb9a0b](https://github.com/scrapy/scrapy/commit/cdb9a0b){.reference
    .external})

-   fixed the variable types in mailsender documentation ([commit
    bb3a848](https://github.com/scrapy/scrapy/commit/bb3a848){.reference
    .external})

-   Reset items_scraped instead of item_count ([commit
    edb07a4](https://github.com/scrapy/scrapy/commit/edb07a4){.reference
    .external})

-   Tentative attention message about what document to read for
    contributions ([commit
    7ee6f7a](https://github.com/scrapy/scrapy/commit/7ee6f7a){.reference
    .external})

-   mitmproxy 0.10.1 needs netlib 0.10.1 too ([commit
    874fcdd](https://github.com/scrapy/scrapy/commit/874fcdd){.reference
    .external})

-   pin mitmproxy 0.10.1 as \>0.11 does not work with tests ([commit
    c6b21f0](https://github.com/scrapy/scrapy/commit/c6b21f0){.reference
    .external})

-   Test the parse command locally instead of against an external url
    ([commit
    c3a6628](https://github.com/scrapy/scrapy/commit/c3a6628){.reference
    .external})

-   Patches Twisted issue while closing the connection pool on
    HTTPDownloadHandler ([commit
    d0bf957](https://github.com/scrapy/scrapy/commit/d0bf957){.reference
    .external})

-   Updates documentation on dynamic item classes. ([commit
    eeb589a](https://github.com/scrapy/scrapy/commit/eeb589a){.reference
    .external})

-   Merge pull request #943 from Lazar-T/patch-3 ([commit
    5fdab02](https://github.com/scrapy/scrapy/commit/5fdab02){.reference
    .external})

-   typo ([commit
    b0ae199](https://github.com/scrapy/scrapy/commit/b0ae199){.reference
    .external})

-   pywin32 is required by Twisted. closes #937 ([commit
    5cb0cfb](https://github.com/scrapy/scrapy/commit/5cb0cfb){.reference
    .external})

-   Update install.rst ([commit
    781286b](https://github.com/scrapy/scrapy/commit/781286b){.reference
    .external})

-   Merge pull request #928 from Lazar-T/patch-1 ([commit
    b415d04](https://github.com/scrapy/scrapy/commit/b415d04){.reference
    .external})

-   comma instead of fullstop ([commit
    627b9ba](https://github.com/scrapy/scrapy/commit/627b9ba){.reference
    .external})

-   Merge pull request #885 from jsma/patch-1 ([commit
    de909ad](https://github.com/scrapy/scrapy/commit/de909ad){.reference
    .external})

-   Update request-response.rst ([commit
    3f3263d](https://github.com/scrapy/scrapy/commit/3f3263d){.reference
    .external})

-   SgmlLinkExtractor - fix for parsing \<area\> tag with Unicode
    present ([commit
    49b40f0](https://github.com/scrapy/scrapy/commit/49b40f0){.reference
    .external})
:::

::: {#scrapy-0-24-4-2014-08-09 .section}
#### Scrapy 0.24.4 (2014-08-09)[¶](#scrapy-0-24-4-2014-08-09 "Permalink to this heading"){.headerlink}

-   pem file is used by mockserver and required by scrapy bench ([commit
    5eddc68](https://github.com/scrapy/scrapy/commit/5eddc68){.reference
    .external})

-   scrapy bench needs scrapy.tests\* ([commit
    d6cb999](https://github.com/scrapy/scrapy/commit/d6cb999){.reference
    .external})
:::

::: {#scrapy-0-24-3-2014-08-09 .section}
#### Scrapy 0.24.3 (2014-08-09)[¶](#scrapy-0-24-3-2014-08-09 "Permalink to this heading"){.headerlink}

-   no need to waste travis-ci time on py3 for 0.24 ([commit
    8e080c1](https://github.com/scrapy/scrapy/commit/8e080c1){.reference
    .external})

-   Update installation docs ([commit
    1d0c096](https://github.com/scrapy/scrapy/commit/1d0c096){.reference
    .external})

-   There is a trove classifier for Scrapy framework! ([commit
    4c701d7](https://github.com/scrapy/scrapy/commit/4c701d7){.reference
    .external})

-   update other places where w3lib version is mentioned ([commit
    d109c13](https://github.com/scrapy/scrapy/commit/d109c13){.reference
    .external})

-   Update w3lib requirement to 1.8.0 ([commit
    39d2ce5](https://github.com/scrapy/scrapy/commit/39d2ce5){.reference
    .external})

-   Use w3lib.html.replace_entities() (remove_entities() is deprecated)
    ([commit
    180d3ad](https://github.com/scrapy/scrapy/commit/180d3ad){.reference
    .external})

-   set zip_safe=False ([commit
    a51ee8b](https://github.com/scrapy/scrapy/commit/a51ee8b){.reference
    .external})

-   do not ship tests package ([commit
    ee3b371](https://github.com/scrapy/scrapy/commit/ee3b371){.reference
    .external})

-   scrapy.bat is not needed anymore ([commit
    c3861cf](https://github.com/scrapy/scrapy/commit/c3861cf){.reference
    .external})

-   Modernize setup.py ([commit
    362e322](https://github.com/scrapy/scrapy/commit/362e322){.reference
    .external})

-   headers can not handle non-string values ([commit
    94a5c65](https://github.com/scrapy/scrapy/commit/94a5c65){.reference
    .external})

-   fix ftp test cases ([commit
    a274a7f](https://github.com/scrapy/scrapy/commit/a274a7f){.reference
    .external})

-   The sum up of travis-ci builds are taking like 50min to complete
    ([commit
    ae1e2cc](https://github.com/scrapy/scrapy/commit/ae1e2cc){.reference
    .external})

-   Update shell.rst typo ([commit
    e49c96a](https://github.com/scrapy/scrapy/commit/e49c96a){.reference
    .external})

-   removes weird indentation in the shell results ([commit
    1ca489d](https://github.com/scrapy/scrapy/commit/1ca489d){.reference
    .external})

-   improved explanations, clarified blog post as source, added link for
    XPath string functions in the spec ([commit
    65c8f05](https://github.com/scrapy/scrapy/commit/65c8f05){.reference
    .external})

-   renamed UserTimeoutError and ServerTimeouterror #583 ([commit
    037f6ab](https://github.com/scrapy/scrapy/commit/037f6ab){.reference
    .external})

-   adding some xpath tips to selectors docs ([commit
    2d103e0](https://github.com/scrapy/scrapy/commit/2d103e0){.reference
    .external})

-   fix tests to account for
    [https://github.com/scrapy/w3lib/pull/23](https://github.com/scrapy/w3lib/pull/23){.reference
    .external} ([commit
    f8d366a](https://github.com/scrapy/scrapy/commit/f8d366a){.reference
    .external})

-   get_func_args maximum recursion fix #728 ([commit
    81344ea](https://github.com/scrapy/scrapy/commit/81344ea){.reference
    .external})

-   Updated input/output processor example according to #560. ([commit
    f7c4ea8](https://github.com/scrapy/scrapy/commit/f7c4ea8){.reference
    .external})

-   Fixed Python syntax in tutorial. ([commit
    db59ed9](https://github.com/scrapy/scrapy/commit/db59ed9){.reference
    .external})

-   Add test case for tunneling proxy ([commit
    f090260](https://github.com/scrapy/scrapy/commit/f090260){.reference
    .external})

-   Bugfix for leaking Proxy-Authorization header to remote host when
    using tunneling ([commit
    d8793af](https://github.com/scrapy/scrapy/commit/d8793af){.reference
    .external})

-   Extract links from XHTML documents with MIME-Type "application/xml"
    ([commit
    ed1f376](https://github.com/scrapy/scrapy/commit/ed1f376){.reference
    .external})

-   Merge pull request #793 from roysc/patch-1 ([commit
    91a1106](https://github.com/scrapy/scrapy/commit/91a1106){.reference
    .external})

-   Fix typo in commands.rst ([commit
    743e1e2](https://github.com/scrapy/scrapy/commit/743e1e2){.reference
    .external})

-   better testcase for settings.overrides.setdefault ([commit
    e22daaf](https://github.com/scrapy/scrapy/commit/e22daaf){.reference
    .external})

-   Using CRLF as line marker according to http 1.1 definition ([commit
    5ec430b](https://github.com/scrapy/scrapy/commit/5ec430b){.reference
    .external})
:::

::: {#scrapy-0-24-2-2014-07-08 .section}
#### Scrapy 0.24.2 (2014-07-08)[¶](#scrapy-0-24-2-2014-07-08 "Permalink to this heading"){.headerlink}

-   Use a mutable mapping to proxy deprecated settings.overrides and
    settings.defaults attribute ([commit
    e5e8133](https://github.com/scrapy/scrapy/commit/e5e8133){.reference
    .external})

-   there is not support for python3 yet ([commit
    3cd6146](https://github.com/scrapy/scrapy/commit/3cd6146){.reference
    .external})

-   Update python compatible version set to Debian packages ([commit
    fa5d76b](https://github.com/scrapy/scrapy/commit/fa5d76b){.reference
    .external})

-   DOC fix formatting in release notes ([commit
    c6a9e20](https://github.com/scrapy/scrapy/commit/c6a9e20){.reference
    .external})
:::

::: {#scrapy-0-24-1-2014-06-27 .section}
#### Scrapy 0.24.1 (2014-06-27)[¶](#scrapy-0-24-1-2014-06-27 "Permalink to this heading"){.headerlink}

-   Fix deprecated CrawlerSettings and increase backward compatibility
    with .defaults attribute ([commit
    8e3f20a](https://github.com/scrapy/scrapy/commit/8e3f20a){.reference
    .external})
:::

::: {#scrapy-0-24-0-2014-06-26 .section}
#### Scrapy 0.24.0 (2014-06-26)[¶](#scrapy-0-24-0-2014-06-26 "Permalink to this heading"){.headerlink}

::: {#enhancements .section}
##### Enhancements[¶](#enhancements "Permalink to this heading"){.headerlink}

-   Improve Scrapy top-level namespace ([issue
    494](https://github.com/scrapy/scrapy/issues/494){.reference
    .external}, [issue
    684](https://github.com/scrapy/scrapy/issues/684){.reference
    .external})

-   Add selector shortcuts to responses ([issue
    554](https://github.com/scrapy/scrapy/issues/554){.reference
    .external}, [issue
    690](https://github.com/scrapy/scrapy/issues/690){.reference
    .external})

-   Add new lxml based LinkExtractor to replace unmaintained
    SgmlLinkExtractor ([issue
    559](https://github.com/scrapy/scrapy/issues/559){.reference
    .external}, [issue
    761](https://github.com/scrapy/scrapy/issues/761){.reference
    .external}, [issue
    763](https://github.com/scrapy/scrapy/issues/763){.reference
    .external})

-   Cleanup settings API - part of per-spider settings **GSoC project**
    ([issue 737](https://github.com/scrapy/scrapy/issues/737){.reference
    .external})

-   Add UTF8 encoding header to templates ([issue
    688](https://github.com/scrapy/scrapy/issues/688){.reference
    .external}, [issue
    762](https://github.com/scrapy/scrapy/issues/762){.reference
    .external})

-   Telnet console now binds to 127.0.0.1 by default ([issue
    699](https://github.com/scrapy/scrapy/issues/699){.reference
    .external})

-   Update Debian/Ubuntu install instructions ([issue
    509](https://github.com/scrapy/scrapy/issues/509){.reference
    .external}, [issue
    549](https://github.com/scrapy/scrapy/issues/549){.reference
    .external})

-   Disable smart strings in lxml XPath evaluations ([issue
    535](https://github.com/scrapy/scrapy/issues/535){.reference
    .external})

-   Restore filesystem based cache as default for http cache middleware
    ([issue 541](https://github.com/scrapy/scrapy/issues/541){.reference
    .external}, [issue
    500](https://github.com/scrapy/scrapy/issues/500){.reference
    .external}, [issue
    571](https://github.com/scrapy/scrapy/issues/571){.reference
    .external})

-   Expose current crawler in Scrapy shell ([issue
    557](https://github.com/scrapy/scrapy/issues/557){.reference
    .external})

-   Improve testsuite comparing CSV and XML exporters ([issue
    570](https://github.com/scrapy/scrapy/issues/570){.reference
    .external})

-   New [`offsite/filtered`{.docutils .literal .notranslate}]{.pre} and
    [`offsite/domains`{.docutils .literal .notranslate}]{.pre} stats
    ([issue 566](https://github.com/scrapy/scrapy/issues/566){.reference
    .external})

-   Support process_links as generator in CrawlSpider ([issue
    555](https://github.com/scrapy/scrapy/issues/555){.reference
    .external})

-   Verbose logging and new stats counters for DupeFilter ([issue
    553](https://github.com/scrapy/scrapy/issues/553){.reference
    .external})

-   Add a mimetype parameter to [`MailSender.send()`{.docutils .literal
    .notranslate}]{.pre} ([issue
    602](https://github.com/scrapy/scrapy/issues/602){.reference
    .external})

-   Generalize file pipeline log messages ([issue
    622](https://github.com/scrapy/scrapy/issues/622){.reference
    .external})

-   Replace unencodeable codepoints with html entities in
    SGMLLinkExtractor ([issue
    565](https://github.com/scrapy/scrapy/issues/565){.reference
    .external})

-   Converted SEP documents to rst format ([issue
    629](https://github.com/scrapy/scrapy/issues/629){.reference
    .external}, [issue
    630](https://github.com/scrapy/scrapy/issues/630){.reference
    .external}, [issue
    638](https://github.com/scrapy/scrapy/issues/638){.reference
    .external}, [issue
    632](https://github.com/scrapy/scrapy/issues/632){.reference
    .external}, [issue
    636](https://github.com/scrapy/scrapy/issues/636){.reference
    .external}, [issue
    640](https://github.com/scrapy/scrapy/issues/640){.reference
    .external}, [issue
    635](https://github.com/scrapy/scrapy/issues/635){.reference
    .external}, [issue
    634](https://github.com/scrapy/scrapy/issues/634){.reference
    .external}, [issue
    639](https://github.com/scrapy/scrapy/issues/639){.reference
    .external}, [issue
    637](https://github.com/scrapy/scrapy/issues/637){.reference
    .external}, [issue
    631](https://github.com/scrapy/scrapy/issues/631){.reference
    .external}, [issue
    633](https://github.com/scrapy/scrapy/issues/633){.reference
    .external}, [issue
    641](https://github.com/scrapy/scrapy/issues/641){.reference
    .external}, [issue
    642](https://github.com/scrapy/scrapy/issues/642){.reference
    .external})

-   Tests and docs for clickdata's nr index in FormRequest ([issue
    646](https://github.com/scrapy/scrapy/issues/646){.reference
    .external}, [issue
    645](https://github.com/scrapy/scrapy/issues/645){.reference
    .external})

-   Allow to disable a downloader handler just like any other component
    ([issue 650](https://github.com/scrapy/scrapy/issues/650){.reference
    .external})

-   Log when a request is discarded after too many redirections ([issue
    654](https://github.com/scrapy/scrapy/issues/654){.reference
    .external})

-   Log error responses if they are not handled by spider callbacks
    ([issue 612](https://github.com/scrapy/scrapy/issues/612){.reference
    .external}, [issue
    656](https://github.com/scrapy/scrapy/issues/656){.reference
    .external})

-   Add content-type check to http compression mw ([issue
    193](https://github.com/scrapy/scrapy/issues/193){.reference
    .external}, [issue
    660](https://github.com/scrapy/scrapy/issues/660){.reference
    .external})

-   Run pypy tests using latest pypi from ppa ([issue
    674](https://github.com/scrapy/scrapy/issues/674){.reference
    .external})

-   Run test suite using pytest instead of trial ([issue
    679](https://github.com/scrapy/scrapy/issues/679){.reference
    .external})

-   Build docs and check for dead links in tox environment ([issue
    687](https://github.com/scrapy/scrapy/issues/687){.reference
    .external})

-   Make scrapy.version_info a tuple of integers ([issue
    681](https://github.com/scrapy/scrapy/issues/681){.reference
    .external}, [issue
    692](https://github.com/scrapy/scrapy/issues/692){.reference
    .external})

-   Infer exporter's output format from filename extensions ([issue
    546](https://github.com/scrapy/scrapy/issues/546){.reference
    .external}, [issue
    659](https://github.com/scrapy/scrapy/issues/659){.reference
    .external}, [issue
    760](https://github.com/scrapy/scrapy/issues/760){.reference
    .external})

-   Support case-insensitive domains in
    [`url_is_from_any_domain()`{.docutils .literal .notranslate}]{.pre}
    ([issue 693](https://github.com/scrapy/scrapy/issues/693){.reference
    .external})

-   Remove pep8 warnings in project and spider templates ([issue
    698](https://github.com/scrapy/scrapy/issues/698){.reference
    .external})

-   Tests and docs for [`request_fingerprint`{.docutils .literal
    .notranslate}]{.pre} function ([issue
    597](https://github.com/scrapy/scrapy/issues/597){.reference
    .external})

-   Update SEP-19 for GSoC project [`per-spider`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`settings`{.docutils .literal .notranslate}]{.pre}
    ([issue 705](https://github.com/scrapy/scrapy/issues/705){.reference
    .external})

-   Set exit code to non-zero when contracts fails ([issue
    727](https://github.com/scrapy/scrapy/issues/727){.reference
    .external})

-   Add a setting to control what class is instantiated as Downloader
    component ([issue
    738](https://github.com/scrapy/scrapy/issues/738){.reference
    .external})

-   Pass response in [`item_dropped`{.docutils .literal
    .notranslate}]{.pre} signal ([issue
    724](https://github.com/scrapy/scrapy/issues/724){.reference
    .external})

-   Improve [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`check`{.docutils .literal .notranslate}]{.pre}
    contracts command ([issue
    733](https://github.com/scrapy/scrapy/issues/733){.reference
    .external}, [issue
    752](https://github.com/scrapy/scrapy/issues/752){.reference
    .external})

-   Document [`spider.closed()`{.docutils .literal .notranslate}]{.pre}
    shortcut ([issue
    719](https://github.com/scrapy/scrapy/issues/719){.reference
    .external})

-   Document [`request_scheduled`{.docutils .literal
    .notranslate}]{.pre} signal ([issue
    746](https://github.com/scrapy/scrapy/issues/746){.reference
    .external})

-   Add a note about reporting security issues ([issue
    697](https://github.com/scrapy/scrapy/issues/697){.reference
    .external})

-   Add LevelDB http cache storage backend ([issue
    626](https://github.com/scrapy/scrapy/issues/626){.reference
    .external}, [issue
    500](https://github.com/scrapy/scrapy/issues/500){.reference
    .external})

-   Sort spider list output of [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`list`{.docutils .literal .notranslate}]{.pre} command
    ([issue 742](https://github.com/scrapy/scrapy/issues/742){.reference
    .external})

-   Multiple documentation enhancements and fixes ([issue
    575](https://github.com/scrapy/scrapy/issues/575){.reference
    .external}, [issue
    587](https://github.com/scrapy/scrapy/issues/587){.reference
    .external}, [issue
    590](https://github.com/scrapy/scrapy/issues/590){.reference
    .external}, [issue
    596](https://github.com/scrapy/scrapy/issues/596){.reference
    .external}, [issue
    610](https://github.com/scrapy/scrapy/issues/610){.reference
    .external}, [issue
    617](https://github.com/scrapy/scrapy/issues/617){.reference
    .external}, [issue
    618](https://github.com/scrapy/scrapy/issues/618){.reference
    .external}, [issue
    627](https://github.com/scrapy/scrapy/issues/627){.reference
    .external}, [issue
    613](https://github.com/scrapy/scrapy/issues/613){.reference
    .external}, [issue
    643](https://github.com/scrapy/scrapy/issues/643){.reference
    .external}, [issue
    654](https://github.com/scrapy/scrapy/issues/654){.reference
    .external}, [issue
    675](https://github.com/scrapy/scrapy/issues/675){.reference
    .external}, [issue
    663](https://github.com/scrapy/scrapy/issues/663){.reference
    .external}, [issue
    711](https://github.com/scrapy/scrapy/issues/711){.reference
    .external}, [issue
    714](https://github.com/scrapy/scrapy/issues/714){.reference
    .external})
:::

::: {#id129 .section}
##### Bugfixes[¶](#id129 "Permalink to this heading"){.headerlink}

-   Encode unicode URL value when creating Links in RegexLinkExtractor
    ([issue 561](https://github.com/scrapy/scrapy/issues/561){.reference
    .external})

-   Ignore None values in ItemLoader processors ([issue
    556](https://github.com/scrapy/scrapy/issues/556){.reference
    .external})

-   Fix link text when there is an inner tag in SGMLLinkExtractor and
    HtmlParserLinkExtractor ([issue
    485](https://github.com/scrapy/scrapy/issues/485){.reference
    .external}, [issue
    574](https://github.com/scrapy/scrapy/issues/574){.reference
    .external})

-   Fix wrong checks on subclassing of deprecated classes ([issue
    581](https://github.com/scrapy/scrapy/issues/581){.reference
    .external}, [issue
    584](https://github.com/scrapy/scrapy/issues/584){.reference
    .external})

-   Handle errors caused by inspect.stack() failures ([issue
    582](https://github.com/scrapy/scrapy/issues/582){.reference
    .external})

-   Fix a reference to unexistent engine attribute ([issue
    593](https://github.com/scrapy/scrapy/issues/593){.reference
    .external}, [issue
    594](https://github.com/scrapy/scrapy/issues/594){.reference
    .external})

-   Fix dynamic itemclass example usage of type() ([issue
    603](https://github.com/scrapy/scrapy/issues/603){.reference
    .external})

-   Use lucasdemarchi/codespell to fix typos ([issue
    628](https://github.com/scrapy/scrapy/issues/628){.reference
    .external})

-   Fix default value of attrs argument in SgmlLinkExtractor to be tuple
    ([issue 661](https://github.com/scrapy/scrapy/issues/661){.reference
    .external})

-   Fix XXE flaw in sitemap reader ([issue
    676](https://github.com/scrapy/scrapy/issues/676){.reference
    .external})

-   Fix engine to support filtered start requests ([issue
    707](https://github.com/scrapy/scrapy/issues/707){.reference
    .external})

-   Fix offsite middleware case on urls with no hostnames ([issue
    745](https://github.com/scrapy/scrapy/issues/745){.reference
    .external})

-   Testsuite doesn't require PIL anymore ([issue
    585](https://github.com/scrapy/scrapy/issues/585){.reference
    .external})
:::
:::

::: {#scrapy-0-22-2-released-2014-02-14 .section}
#### Scrapy 0.22.2 (released 2014-02-14)[¶](#scrapy-0-22-2-released-2014-02-14 "Permalink to this heading"){.headerlink}

-   fix a reference to unexistent engine.slots. closes #593 ([commit
    13c099a](https://github.com/scrapy/scrapy/commit/13c099a){.reference
    .external})

-   downloaderMW doc typo (spiderMW doc copy remnant) ([commit
    8ae11bf](https://github.com/scrapy/scrapy/commit/8ae11bf){.reference
    .external})

-   Correct typos ([commit
    1346037](https://github.com/scrapy/scrapy/commit/1346037){.reference
    .external})
:::

::: {#scrapy-0-22-1-released-2014-02-08 .section}
#### Scrapy 0.22.1 (released 2014-02-08)[¶](#scrapy-0-22-1-released-2014-02-08 "Permalink to this heading"){.headerlink}

-   localhost666 can resolve under certain circumstances ([commit
    2ec2279](https://github.com/scrapy/scrapy/commit/2ec2279){.reference
    .external})

-   test inspect.stack failure ([commit
    cc3eda3](https://github.com/scrapy/scrapy/commit/cc3eda3){.reference
    .external})

-   Handle cases when inspect.stack() fails ([commit
    8cb44f9](https://github.com/scrapy/scrapy/commit/8cb44f9){.reference
    .external})

-   Fix wrong checks on subclassing of deprecated classes. closes #581
    ([commit
    46d98d6](https://github.com/scrapy/scrapy/commit/46d98d6){.reference
    .external})

-   Docs: 4-space indent for final spider example ([commit
    13846de](https://github.com/scrapy/scrapy/commit/13846de){.reference
    .external})

-   Fix HtmlParserLinkExtractor and tests after #485 merge ([commit
    368a946](https://github.com/scrapy/scrapy/commit/368a946){.reference
    .external})

-   BaseSgmlLinkExtractor: Fixed the missing space when the link has an
    inner tag ([commit
    b566388](https://github.com/scrapy/scrapy/commit/b566388){.reference
    .external})

-   BaseSgmlLinkExtractor: Added unit test of a link with an inner tag
    ([commit
    c1cb418](https://github.com/scrapy/scrapy/commit/c1cb418){.reference
    .external})

-   BaseSgmlLinkExtractor: Fixed unknown_endtag() so that it only set
    current_link=None when the end tag match the opening tag ([commit
    7e4d627](https://github.com/scrapy/scrapy/commit/7e4d627){.reference
    .external})

-   Fix tests for Travis-CI build ([commit
    76c7e20](https://github.com/scrapy/scrapy/commit/76c7e20){.reference
    .external})

-   replace unencodeable codepoints with html entities. fixes #562 and
    #285 ([commit
    5f87b17](https://github.com/scrapy/scrapy/commit/5f87b17){.reference
    .external})

-   RegexLinkExtractor: encode URL unicode value when creating Links
    ([commit
    d0ee545](https://github.com/scrapy/scrapy/commit/d0ee545){.reference
    .external})

-   Updated the tutorial crawl output with latest output. ([commit
    8da65de](https://github.com/scrapy/scrapy/commit/8da65de){.reference
    .external})

-   Updated shell docs with the crawler reference and fixed the actual
    shell output. ([commit
    875b9ab](https://github.com/scrapy/scrapy/commit/875b9ab){.reference
    .external})

-   PEP8 minor edits. ([commit
    f89efaf](https://github.com/scrapy/scrapy/commit/f89efaf){.reference
    .external})

-   Expose current crawler in the Scrapy shell. ([commit
    5349cec](https://github.com/scrapy/scrapy/commit/5349cec){.reference
    .external})

-   Unused re import and PEP8 minor edits. ([commit
    387f414](https://github.com/scrapy/scrapy/commit/387f414){.reference
    .external})

-   Ignore None's values when using the ItemLoader. ([commit
    0632546](https://github.com/scrapy/scrapy/commit/0632546){.reference
    .external})

-   DOC Fixed HTTPCACHE_STORAGE typo in the default value which is now
    Filesystem instead Dbm. ([commit
    cde9a8c](https://github.com/scrapy/scrapy/commit/cde9a8c){.reference
    .external})

-   show Ubuntu setup instructions as literal code ([commit
    fb5c9c5](https://github.com/scrapy/scrapy/commit/fb5c9c5){.reference
    .external})

-   Update Ubuntu installation instructions ([commit
    70fb105](https://github.com/scrapy/scrapy/commit/70fb105){.reference
    .external})

-   Merge pull request #550 from stray-leone/patch-1 ([commit
    6f70b6a](https://github.com/scrapy/scrapy/commit/6f70b6a){.reference
    .external})

-   modify the version of Scrapy Ubuntu package ([commit
    725900d](https://github.com/scrapy/scrapy/commit/725900d){.reference
    .external})

-   fix 0.22.0 release date ([commit
    af0219a](https://github.com/scrapy/scrapy/commit/af0219a){.reference
    .external})

-   fix typos in news.rst and remove (not released yet) header ([commit
    b7f58f4](https://github.com/scrapy/scrapy/commit/b7f58f4){.reference
    .external})
:::

::: {#scrapy-0-22-0-released-2014-01-17 .section}
#### Scrapy 0.22.0 (released 2014-01-17)[¶](#scrapy-0-22-0-released-2014-01-17 "Permalink to this heading"){.headerlink}

::: {#id130 .section}
##### Enhancements[¶](#id130 "Permalink to this heading"){.headerlink}

-   \[**Backward incompatible**\] Switched HTTPCacheMiddleware backend
    to filesystem ([issue
    541](https://github.com/scrapy/scrapy/issues/541){.reference
    .external}) To restore old backend set
    [`HTTPCACHE_STORAGE`{.docutils .literal .notranslate}]{.pre} to
    [`scrapy.contrib.httpcache.DbmCacheStorage`{.docutils .literal
    .notranslate}]{.pre}

-   Proxy https:// urls using CONNECT method ([issue
    392](https://github.com/scrapy/scrapy/issues/392){.reference
    .external}, [issue
    397](https://github.com/scrapy/scrapy/issues/397){.reference
    .external})

-   Add a middleware to crawl ajax crawlable pages as defined by google
    ([issue 343](https://github.com/scrapy/scrapy/issues/343){.reference
    .external})

-   Rename scrapy.spider.BaseSpider to scrapy.spider.Spider ([issue
    510](https://github.com/scrapy/scrapy/issues/510){.reference
    .external}, [issue
    519](https://github.com/scrapy/scrapy/issues/519){.reference
    .external})

-   Selectors register EXSLT namespaces by default ([issue
    472](https://github.com/scrapy/scrapy/issues/472){.reference
    .external})

-   Unify item loaders similar to selectors renaming ([issue
    461](https://github.com/scrapy/scrapy/issues/461){.reference
    .external})

-   Make [`RFPDupeFilter`{.docutils .literal .notranslate}]{.pre} class
    easily subclassable ([issue
    533](https://github.com/scrapy/scrapy/issues/533){.reference
    .external})

-   Improve test coverage and forthcoming Python 3 support ([issue
    525](https://github.com/scrapy/scrapy/issues/525){.reference
    .external})

-   Promote startup info on settings and middleware to INFO level
    ([issue 520](https://github.com/scrapy/scrapy/issues/520){.reference
    .external})

-   Support partials in [`get_func_args`{.docutils .literal
    .notranslate}]{.pre} util ([issue
    506](https://github.com/scrapy/scrapy/issues/506){.reference
    .external}, issue:504)

-   Allow running individual tests via tox ([issue
    503](https://github.com/scrapy/scrapy/issues/503){.reference
    .external})

-   Update extensions ignored by link extractors ([issue
    498](https://github.com/scrapy/scrapy/issues/498){.reference
    .external})

-   Add middleware methods to get files/images/thumbs paths ([issue
    490](https://github.com/scrapy/scrapy/issues/490){.reference
    .external})

-   Improve offsite middleware tests ([issue
    478](https://github.com/scrapy/scrapy/issues/478){.reference
    .external})

-   Add a way to skip default Referer header set by RefererMiddleware
    ([issue 475](https://github.com/scrapy/scrapy/issues/475){.reference
    .external})

-   Do not send [`x-gzip`{.docutils .literal .notranslate}]{.pre} in
    default [`Accept-Encoding`{.docutils .literal .notranslate}]{.pre}
    header ([issue
    469](https://github.com/scrapy/scrapy/issues/469){.reference
    .external})

-   Support defining http error handling using settings ([issue
    466](https://github.com/scrapy/scrapy/issues/466){.reference
    .external})

-   Use modern python idioms wherever you find legacies ([issue
    497](https://github.com/scrapy/scrapy/issues/497){.reference
    .external})

-   Improve and correct documentation ([issue
    527](https://github.com/scrapy/scrapy/issues/527){.reference
    .external}, [issue
    524](https://github.com/scrapy/scrapy/issues/524){.reference
    .external}, [issue
    521](https://github.com/scrapy/scrapy/issues/521){.reference
    .external}, [issue
    517](https://github.com/scrapy/scrapy/issues/517){.reference
    .external}, [issue
    512](https://github.com/scrapy/scrapy/issues/512){.reference
    .external}, [issue
    505](https://github.com/scrapy/scrapy/issues/505){.reference
    .external}, [issue
    502](https://github.com/scrapy/scrapy/issues/502){.reference
    .external}, [issue
    489](https://github.com/scrapy/scrapy/issues/489){.reference
    .external}, [issue
    465](https://github.com/scrapy/scrapy/issues/465){.reference
    .external}, [issue
    460](https://github.com/scrapy/scrapy/issues/460){.reference
    .external}, [issue
    425](https://github.com/scrapy/scrapy/issues/425){.reference
    .external}, [issue
    536](https://github.com/scrapy/scrapy/issues/536){.reference
    .external})
:::

::: {#fixes .section}
##### Fixes[¶](#fixes "Permalink to this heading"){.headerlink}

-   Update Selector class imports in CrawlSpider template ([issue
    484](https://github.com/scrapy/scrapy/issues/484){.reference
    .external})

-   Fix unexistent reference to [`engine.slots`{.docutils .literal
    .notranslate}]{.pre} ([issue
    464](https://github.com/scrapy/scrapy/issues/464){.reference
    .external})

-   Do not try to call [`body_as_unicode()`{.docutils .literal
    .notranslate}]{.pre} on a non-TextResponse instance ([issue
    462](https://github.com/scrapy/scrapy/issues/462){.reference
    .external})

-   Warn when subclassing XPathItemLoader, previously it only warned on
    instantiation. ([issue
    523](https://github.com/scrapy/scrapy/issues/523){.reference
    .external})

-   Warn when subclassing XPathSelector, previously it only warned on
    instantiation. ([issue
    537](https://github.com/scrapy/scrapy/issues/537){.reference
    .external})

-   Multiple fixes to memory stats ([issue
    531](https://github.com/scrapy/scrapy/issues/531){.reference
    .external}, [issue
    530](https://github.com/scrapy/scrapy/issues/530){.reference
    .external}, [issue
    529](https://github.com/scrapy/scrapy/issues/529){.reference
    .external})

-   Fix overriding url in [`FormRequest.from_response()`{.docutils
    .literal .notranslate}]{.pre} ([issue
    507](https://github.com/scrapy/scrapy/issues/507){.reference
    .external})

-   Fix tests runner under pip 1.5 ([issue
    513](https://github.com/scrapy/scrapy/issues/513){.reference
    .external})

-   Fix logging error when spider name is unicode ([issue
    479](https://github.com/scrapy/scrapy/issues/479){.reference
    .external})
:::
:::

::: {#scrapy-0-20-2-released-2013-12-09 .section}
#### Scrapy 0.20.2 (released 2013-12-09)[¶](#scrapy-0-20-2-released-2013-12-09 "Permalink to this heading"){.headerlink}

-   Update CrawlSpider Template with Selector changes ([commit
    6d1457d](https://github.com/scrapy/scrapy/commit/6d1457d){.reference
    .external})

-   fix method name in tutorial. closes GH-480 ([commit
    b4fc359](https://github.com/scrapy/scrapy/commit/b4fc359){.reference
    .external}
:::

::: {#scrapy-0-20-1-released-2013-11-28 .section}
#### Scrapy 0.20.1 (released 2013-11-28)[¶](#scrapy-0-20-1-released-2013-11-28 "Permalink to this heading"){.headerlink}

-   include_package_data is required to build wheels from published
    sources ([commit
    5ba1ad5](https://github.com/scrapy/scrapy/commit/5ba1ad5){.reference
    .external})

-   process_parallel was leaking the failures on its internal deferreds.
    closes #458 ([commit
    419a780](https://github.com/scrapy/scrapy/commit/419a780){.reference
    .external})
:::

::: {#scrapy-0-20-0-released-2013-11-08 .section}
#### Scrapy 0.20.0 (released 2013-11-08)[¶](#scrapy-0-20-0-released-2013-11-08 "Permalink to this heading"){.headerlink}

::: {#id131 .section}
##### Enhancements[¶](#id131 "Permalink to this heading"){.headerlink}

-   New Selector's API including CSS selectors ([issue
    395](https://github.com/scrapy/scrapy/issues/395){.reference
    .external} and [issue
    426](https://github.com/scrapy/scrapy/issues/426){.reference
    .external}),

-   Request/Response url/body attributes are now immutable (modifying
    them had been deprecated for a long time)

-   [[`ITEM_PIPELINES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
    .tooltip .reference .internal} is now defined as a dict (instead of
    a list)

-   Sitemap spider can fetch alternate URLs ([issue
    360](https://github.com/scrapy/scrapy/issues/360){.reference
    .external})

-   [`Selector.remove_namespaces()`{.docutils .literal
    .notranslate}]{.pre} now remove namespaces from element's
    attributes. ([issue
    416](https://github.com/scrapy/scrapy/issues/416){.reference
    .external})

-   Paved the road for Python 3.3+ ([issue
    435](https://github.com/scrapy/scrapy/issues/435){.reference
    .external}, [issue
    436](https://github.com/scrapy/scrapy/issues/436){.reference
    .external}, [issue
    431](https://github.com/scrapy/scrapy/issues/431){.reference
    .external}, [issue
    452](https://github.com/scrapy/scrapy/issues/452){.reference
    .external})

-   New item exporter using native python types with nesting support
    ([issue 366](https://github.com/scrapy/scrapy/issues/366){.reference
    .external})

-   Tune HTTP1.1 pool size so it matches concurrency defined by settings
    ([commit
    b43b5f575](https://github.com/scrapy/scrapy/commit/b43b5f575){.reference
    .external})

-   scrapy.mail.MailSender now can connect over TLS or upgrade using
    STARTTLS ([issue
    327](https://github.com/scrapy/scrapy/issues/327){.reference
    .external})

-   New FilesPipeline with functionality factored out from
    ImagesPipeline ([issue
    370](https://github.com/scrapy/scrapy/issues/370){.reference
    .external}, [issue
    409](https://github.com/scrapy/scrapy/issues/409){.reference
    .external})

-   Recommend Pillow instead of PIL for image handling ([issue
    317](https://github.com/scrapy/scrapy/issues/317){.reference
    .external})

-   Added Debian packages for Ubuntu Quantal and Raring ([commit
    86230c0](https://github.com/scrapy/scrapy/commit/86230c0){.reference
    .external})

-   Mock server (used for tests) can listen for HTTPS requests ([issue
    410](https://github.com/scrapy/scrapy/issues/410){.reference
    .external})

-   Remove multi spider support from multiple core components ([issue
    422](https://github.com/scrapy/scrapy/issues/422){.reference
    .external}, [issue
    421](https://github.com/scrapy/scrapy/issues/421){.reference
    .external}, [issue
    420](https://github.com/scrapy/scrapy/issues/420){.reference
    .external}, [issue
    419](https://github.com/scrapy/scrapy/issues/419){.reference
    .external}, [issue
    423](https://github.com/scrapy/scrapy/issues/423){.reference
    .external}, [issue
    418](https://github.com/scrapy/scrapy/issues/418){.reference
    .external})

-   Travis-CI now tests Scrapy changes against development versions of
    [`w3lib`{.docutils .literal .notranslate}]{.pre} and
    [`queuelib`{.docutils .literal .notranslate}]{.pre} python packages.

-   Add pypy 2.1 to continuous integration tests ([commit
    ecfa7431](https://github.com/scrapy/scrapy/commit/ecfa7431){.reference
    .external})

-   Pylinted, pep8 and removed old-style exceptions from source ([issue
    430](https://github.com/scrapy/scrapy/issues/430){.reference
    .external}, [issue
    432](https://github.com/scrapy/scrapy/issues/432){.reference
    .external})

-   Use importlib for parametric imports ([issue
    445](https://github.com/scrapy/scrapy/issues/445){.reference
    .external})

-   Handle a regression introduced in Python 2.7.5 that affects
    XmlItemExporter ([issue
    372](https://github.com/scrapy/scrapy/issues/372){.reference
    .external})

-   Bugfix crawling shutdown on SIGINT ([issue
    450](https://github.com/scrapy/scrapy/issues/450){.reference
    .external})

-   Do not submit [`reset`{.docutils .literal .notranslate}]{.pre} type
    inputs in FormRequest.from_response ([commit
    b326b87](https://github.com/scrapy/scrapy/commit/b326b87){.reference
    .external})

-   Do not silence download errors when request errback raises an
    exception ([commit
    684cfc0](https://github.com/scrapy/scrapy/commit/684cfc0){.reference
    .external})
:::

::: {#id132 .section}
##### Bugfixes[¶](#id132 "Permalink to this heading"){.headerlink}

-   Fix tests under Django 1.6 ([commit
    b6bed44c](https://github.com/scrapy/scrapy/commit/b6bed44c){.reference
    .external})

-   Lot of bugfixes to retry middleware under disconnections using HTTP
    1.1 download handler

-   Fix inconsistencies among Twisted releases ([issue
    406](https://github.com/scrapy/scrapy/issues/406){.reference
    .external})

-   Fix Scrapy shell bugs ([issue
    418](https://github.com/scrapy/scrapy/issues/418){.reference
    .external}, [issue
    407](https://github.com/scrapy/scrapy/issues/407){.reference
    .external})

-   Fix invalid variable name in setup.py ([issue
    429](https://github.com/scrapy/scrapy/issues/429){.reference
    .external})

-   Fix tutorial references ([issue
    387](https://github.com/scrapy/scrapy/issues/387){.reference
    .external})

-   Improve request-response docs ([issue
    391](https://github.com/scrapy/scrapy/issues/391){.reference
    .external})

-   Improve best practices docs ([issue
    399](https://github.com/scrapy/scrapy/issues/399){.reference
    .external}, [issue
    400](https://github.com/scrapy/scrapy/issues/400){.reference
    .external}, [issue
    401](https://github.com/scrapy/scrapy/issues/401){.reference
    .external}, [issue
    402](https://github.com/scrapy/scrapy/issues/402){.reference
    .external})

-   Improve django integration docs ([issue
    404](https://github.com/scrapy/scrapy/issues/404){.reference
    .external})

-   Document [`bindaddress`{.docutils .literal .notranslate}]{.pre}
    request meta ([commit
    37c24e01d7](https://github.com/scrapy/scrapy/commit/37c24e01d7){.reference
    .external})

-   Improve [`Request`{.docutils .literal .notranslate}]{.pre} class
    documentation ([issue
    226](https://github.com/scrapy/scrapy/issues/226){.reference
    .external})
:::

::: {#other .section}
##### Other[¶](#other "Permalink to this heading"){.headerlink}

-   Dropped Python 2.6 support ([issue
    448](https://github.com/scrapy/scrapy/issues/448){.reference
    .external})

-   Add [[cssselect]{.xref .std
    .std-doc}](https://cssselect.readthedocs.io/en/latest/index.html "(in cssselect v1.2.0)"){.reference
    .external} python package as install dependency

-   Drop libxml2 and multi selector's backend support,
    [lxml](https://lxml.de/){.reference .external} is required from now
    on.

-   Minimum Twisted version increased to 10.0.0, dropped Twisted 8.0
    support.

-   Running test suite now requires [`mock`{.docutils .literal
    .notranslate}]{.pre} python library ([issue
    390](https://github.com/scrapy/scrapy/issues/390){.reference
    .external})
:::

::: {#thanks .section}
##### Thanks[¶](#thanks "Permalink to this heading"){.headerlink}

Thanks to everyone who contribute to this release!

List of contributors sorted by number of commits:

::: {.highlight-default .notranslate}
::: highlight
    69 Daniel Graña <dangra@...>
    37 Pablo Hoffman <pablo@...>
    13 Mikhail Korobov <kmike84@...>
     9 Alex Cepoi <alex.cepoi@...>
     9 alexanderlukanin13 <alexander.lukanin.13@...>
     8 Rolando Espinoza La fuente <darkrho@...>
     8 Lukasz Biedrycki <lukasz.biedrycki@...>
     6 Nicolas Ramirez <nramirez.uy@...>
     3 Paul Tremberth <paul.tremberth@...>
     2 Martin Olveyra <molveyra@...>
     2 Stefan <misc@...>
     2 Rolando Espinoza <darkrho@...>
     2 Loren Davie <loren@...>
     2 irgmedeiros <irgmedeiros@...>
     1 Stefan Koch <taikano@...>
     1 Stefan <cct@...>
     1 scraperdragon <dragon@...>
     1 Kumara Tharmalingam <ktharmal@...>
     1 Francesco Piccinno <stack.box@...>
     1 Marcos Campal <duendex@...>
     1 Dragon Dave <dragon@...>
     1 Capi Etheriel <barraponto@...>
     1 cacovsky <amarquesferraz@...>
     1 Berend Iwema <berend@...>
:::
:::
:::
:::

::: {#scrapy-0-18-4-released-2013-10-10 .section}
#### Scrapy 0.18.4 (released 2013-10-10)[¶](#scrapy-0-18-4-released-2013-10-10 "Permalink to this heading"){.headerlink}

-   IPython refuses to update the namespace. fix #396 ([commit
    3d32c4f](https://github.com/scrapy/scrapy/commit/3d32c4f){.reference
    .external})

-   Fix AlreadyCalledError replacing a request in shell command. closes
    #407 ([commit
    b1d8919](https://github.com/scrapy/scrapy/commit/b1d8919){.reference
    .external})

-   Fix start_requests laziness and early hangs ([commit
    89faf52](https://github.com/scrapy/scrapy/commit/89faf52){.reference
    .external})
:::

::: {#scrapy-0-18-3-released-2013-10-03 .section}
#### Scrapy 0.18.3 (released 2013-10-03)[¶](#scrapy-0-18-3-released-2013-10-03 "Permalink to this heading"){.headerlink}

-   fix regression on lazy evaluation of start requests ([commit
    12693a5](https://github.com/scrapy/scrapy/commit/12693a5){.reference
    .external})

-   forms: do not submit reset inputs ([commit
    e429f63](https://github.com/scrapy/scrapy/commit/e429f63){.reference
    .external})

-   increase unittest timeouts to decrease travis false positive
    failures ([commit
    912202e](https://github.com/scrapy/scrapy/commit/912202e){.reference
    .external})

-   backport master fixes to json exporter ([commit
    cfc2d46](https://github.com/scrapy/scrapy/commit/cfc2d46){.reference
    .external})

-   Fix permission and set umask before generating sdist tarball
    ([commit
    06149e0](https://github.com/scrapy/scrapy/commit/06149e0){.reference
    .external})
:::

::: {#scrapy-0-18-2-released-2013-09-03 .section}
#### Scrapy 0.18.2 (released 2013-09-03)[¶](#scrapy-0-18-2-released-2013-09-03 "Permalink to this heading"){.headerlink}

-   Backport [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`check`{.docutils .literal .notranslate}]{.pre}
    command fixes and backward compatible multi crawler process([issue
    339](https://github.com/scrapy/scrapy/issues/339){.reference
    .external})
:::

::: {#scrapy-0-18-1-released-2013-08-27 .section}
#### Scrapy 0.18.1 (released 2013-08-27)[¶](#scrapy-0-18-1-released-2013-08-27 "Permalink to this heading"){.headerlink}

-   remove extra import added by cherry picked changes ([commit
    d20304e](https://github.com/scrapy/scrapy/commit/d20304e){.reference
    .external})

-   fix crawling tests under twisted pre 11.0.0 ([commit
    1994f38](https://github.com/scrapy/scrapy/commit/1994f38){.reference
    .external})

-   py26 can not format zero length fields {} ([commit
    abf756f](https://github.com/scrapy/scrapy/commit/abf756f){.reference
    .external})

-   test PotentiaDataLoss errors on unbound responses ([commit
    b15470d](https://github.com/scrapy/scrapy/commit/b15470d){.reference
    .external})

-   Treat responses without content-length or Transfer-Encoding as good
    responses ([commit
    c4bf324](https://github.com/scrapy/scrapy/commit/c4bf324){.reference
    .external})

-   do no include ResponseFailed if http11 handler is not enabled
    ([commit
    6cbe684](https://github.com/scrapy/scrapy/commit/6cbe684){.reference
    .external})

-   New HTTP client wraps connection lost in ResponseFailed exception.
    fix #373 ([commit
    1a20bba](https://github.com/scrapy/scrapy/commit/1a20bba){.reference
    .external})

-   limit travis-ci build matrix ([commit
    3b01bb8](https://github.com/scrapy/scrapy/commit/3b01bb8){.reference
    .external})

-   Merge pull request #375 from peterarenot/patch-1 ([commit
    fa766d7](https://github.com/scrapy/scrapy/commit/fa766d7){.reference
    .external})

-   Fixed so it refers to the correct folder ([commit
    3283809](https://github.com/scrapy/scrapy/commit/3283809){.reference
    .external})

-   added Quantal & Raring to support Ubuntu releases ([commit
    1411923](https://github.com/scrapy/scrapy/commit/1411923){.reference
    .external})

-   fix retry middleware which didn't retry certain connection errors
    after the upgrade to http1 client, closes GH-373 ([commit
    bb35ed0](https://github.com/scrapy/scrapy/commit/bb35ed0){.reference
    .external})

-   fix XmlItemExporter in Python 2.7.4 and 2.7.5 ([commit
    de3e451](https://github.com/scrapy/scrapy/commit/de3e451){.reference
    .external})

-   minor updates to 0.18 release notes ([commit
    c45e5f1](https://github.com/scrapy/scrapy/commit/c45e5f1){.reference
    .external})

-   fix contributors list format ([commit
    0b60031](https://github.com/scrapy/scrapy/commit/0b60031){.reference
    .external})
:::

::: {#scrapy-0-18-0-released-2013-08-09 .section}
#### Scrapy 0.18.0 (released 2013-08-09)[¶](#scrapy-0-18-0-released-2013-08-09 "Permalink to this heading"){.headerlink}

-   Lot of improvements to testsuite run using Tox, including a way to
    test on pypi

-   Handle GET parameters for AJAX crawlable urls ([commit
    3fe2a32](https://github.com/scrapy/scrapy/commit/3fe2a32){.reference
    .external})

-   Use lxml recover option to parse sitemaps ([issue
    347](https://github.com/scrapy/scrapy/issues/347){.reference
    .external})

-   Bugfix cookie merging by hostname and not by netloc ([issue
    352](https://github.com/scrapy/scrapy/issues/352){.reference
    .external})

-   Support disabling [`HttpCompressionMiddleware`{.docutils .literal
    .notranslate}]{.pre} using a flag setting ([issue
    359](https://github.com/scrapy/scrapy/issues/359){.reference
    .external})

-   Support xml namespaces using [`iternodes`{.docutils .literal
    .notranslate}]{.pre} parser in [`XMLFeedSpider`{.docutils .literal
    .notranslate}]{.pre} ([issue
    12](https://github.com/scrapy/scrapy/issues/12){.reference
    .external})

-   Support [`dont_cache`{.docutils .literal .notranslate}]{.pre}
    request meta flag ([issue
    19](https://github.com/scrapy/scrapy/issues/19){.reference
    .external})

-   Bugfix [`scrapy.utils.gz.gunzip`{.docutils .literal
    .notranslate}]{.pre} broken by changes in python 2.7.4 ([commit
    4dc76e](https://github.com/scrapy/scrapy/commit/4dc76e){.reference
    .external})

-   Bugfix url encoding on [`SgmlLinkExtractor`{.docutils .literal
    .notranslate}]{.pre} ([issue
    24](https://github.com/scrapy/scrapy/issues/24){.reference
    .external})

-   Bugfix [`TakeFirst`{.docutils .literal .notranslate}]{.pre}
    processor shouldn't discard zero (0) value ([issue
    59](https://github.com/scrapy/scrapy/issues/59){.reference
    .external})

-   Support nested items in xml exporter ([issue
    66](https://github.com/scrapy/scrapy/issues/66){.reference
    .external})

-   Improve cookies handling performance ([issue
    77](https://github.com/scrapy/scrapy/issues/77){.reference
    .external})

-   Log dupe filtered requests once ([issue
    105](https://github.com/scrapy/scrapy/issues/105){.reference
    .external})

-   Split redirection middleware into status and meta based middlewares
    ([issue 78](https://github.com/scrapy/scrapy/issues/78){.reference
    .external})

-   Use HTTP1.1 as default downloader handler ([issue
    109](https://github.com/scrapy/scrapy/issues/109){.reference
    .external} and [issue
    318](https://github.com/scrapy/scrapy/issues/318){.reference
    .external})

-   Support xpath form selection on
    [`FormRequest.from_response`{.docutils .literal .notranslate}]{.pre}
    ([issue 185](https://github.com/scrapy/scrapy/issues/185){.reference
    .external})

-   Bugfix unicode decoding error on [`SgmlLinkExtractor`{.docutils
    .literal .notranslate}]{.pre} ([issue
    199](https://github.com/scrapy/scrapy/issues/199){.reference
    .external})

-   Bugfix signal dispatching on pypi interpreter ([issue
    205](https://github.com/scrapy/scrapy/issues/205){.reference
    .external})

-   Improve request delay and concurrency handling ([issue
    206](https://github.com/scrapy/scrapy/issues/206){.reference
    .external})

-   Add RFC2616 cache policy to [`HttpCacheMiddleware`{.docutils
    .literal .notranslate}]{.pre} ([issue
    212](https://github.com/scrapy/scrapy/issues/212){.reference
    .external})

-   Allow customization of messages logged by engine ([issue
    214](https://github.com/scrapy/scrapy/issues/214){.reference
    .external})

-   Multiples improvements to [`DjangoItem`{.docutils .literal
    .notranslate}]{.pre} ([issue
    217](https://github.com/scrapy/scrapy/issues/217){.reference
    .external}, [issue
    218](https://github.com/scrapy/scrapy/issues/218){.reference
    .external}, [issue
    221](https://github.com/scrapy/scrapy/issues/221){.reference
    .external})

-   Extend Scrapy commands using setuptools entry points ([issue
    260](https://github.com/scrapy/scrapy/issues/260){.reference
    .external})

-   Allow spider [`allowed_domains`{.docutils .literal
    .notranslate}]{.pre} value to be set/tuple ([issue
    261](https://github.com/scrapy/scrapy/issues/261){.reference
    .external})

-   Support [`settings.getdict`{.docutils .literal .notranslate}]{.pre}
    ([issue 269](https://github.com/scrapy/scrapy/issues/269){.reference
    .external})

-   Simplify internal [`scrapy.core.scraper`{.docutils .literal
    .notranslate}]{.pre} slot handling ([issue
    271](https://github.com/scrapy/scrapy/issues/271){.reference
    .external})

-   Added [`Item.copy`{.docutils .literal .notranslate}]{.pre} ([issue
    290](https://github.com/scrapy/scrapy/issues/290){.reference
    .external})

-   Collect idle downloader slots ([issue
    297](https://github.com/scrapy/scrapy/issues/297){.reference
    .external})

-   Add [`ftp://`{.docutils .literal .notranslate}]{.pre} scheme
    downloader handler ([issue
    329](https://github.com/scrapy/scrapy/issues/329){.reference
    .external})

-   Added downloader benchmark webserver and spider tools
    [[Benchmarking]{.std .std-ref}](index.html#benchmarking){.hoverxref
    .tooltip .reference .internal}

-   Moved persistent (on disk) queues to a separate project
    ([queuelib](https://github.com/scrapy/queuelib){.reference
    .external}) which Scrapy now depends on

-   Add Scrapy commands using external libraries ([issue
    260](https://github.com/scrapy/scrapy/issues/260){.reference
    .external})

-   Added [`--pdb`{.docutils .literal .notranslate}]{.pre} option to
    [`scrapy`{.docutils .literal .notranslate}]{.pre} command line tool

-   Added [[`XPathSelector.remove_namespaces`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.selector.Selector.remove_namespaces "scrapy.selector.Selector.remove_namespaces"){.reference
    .internal} which allows to remove all namespaces from XML documents
    for convenience (to work with namespace-less XPaths). Documented in
    [[Selectors]{.std .std-ref}](index.html#topics-selectors){.hoverxref
    .tooltip .reference .internal}.

-   Several improvements to spider contracts

-   New default middleware named MetaRefreshMiddleware that handles
    meta-refresh html tag redirections,

-   MetaRefreshMiddleware and RedirectMiddleware have different
    priorities to address #62

-   added from_crawler method to spiders

-   added system tests with mock server

-   more improvements to macOS compatibility (thanks Alex Cepoi)

-   several more cleanups to singletons and multi-spider support (thanks
    Nicolas Ramirez)

-   support custom download slots

-   added --spider option to "shell" command.

-   log overridden settings when Scrapy starts

Thanks to everyone who contribute to this release. Here is a list of
contributors sorted by number of commits:

::: {.highlight-default .notranslate}
::: highlight
    130 Pablo Hoffman <pablo@...>
     97 Daniel Graña <dangra@...>
     20 Nicolás Ramírez <nramirez.uy@...>
     13 Mikhail Korobov <kmike84@...>
     12 Pedro Faustino <pedrobandim@...>
     11 Steven Almeroth <sroth77@...>
      5 Rolando Espinoza La fuente <darkrho@...>
      4 Michal Danilak <mimino.coder@...>
      4 Alex Cepoi <alex.cepoi@...>
      4 Alexandr N Zamaraev (aka tonal) <tonal@...>
      3 paul <paul.tremberth@...>
      3 Martin Olveyra <molveyra@...>
      3 Jordi Llonch <llonchj@...>
      3 arijitchakraborty <myself.arijit@...>
      2 Shane Evans <shane.evans@...>
      2 joehillen <joehillen@...>
      2 Hart <HartSimha@...>
      2 Dan <ellisd23@...>
      1 Zuhao Wan <wanzuhao@...>
      1 whodatninja <blake@...>
      1 vkrest <v.krestiannykov@...>
      1 tpeng <pengtaoo@...>
      1 Tom Mortimer-Jones <tom@...>
      1 Rocio Aramberri <roschegel@...>
      1 Pedro <pedro@...>
      1 notsobad <wangxiaohugg@...>
      1 Natan L <kuyanatan.nlao@...>
      1 Mark Grey <mark.grey@...>
      1 Luan <luanpab@...>
      1 Libor Nenadál <libor.nenadal@...>
      1 Juan M Uys <opyate@...>
      1 Jonas Brunsgaard <jonas.brunsgaard@...>
      1 Ilya Baryshev <baryshev@...>
      1 Hasnain Lakhani <m.hasnain.lakhani@...>
      1 Emanuel Schorsch <emschorsch@...>
      1 Chris Tilden <chris.tilden@...>
      1 Capi Etheriel <barraponto@...>
      1 cacovsky <amarquesferraz@...>
      1 Berend Iwema <berend@...>
:::
:::
:::

::: {#scrapy-0-16-5-released-2013-05-30 .section}
#### Scrapy 0.16.5 (released 2013-05-30)[¶](#scrapy-0-16-5-released-2013-05-30 "Permalink to this heading"){.headerlink}

-   obey request method when Scrapy deploy is redirected to a new
    endpoint ([commit
    8c4fcee](https://github.com/scrapy/scrapy/commit/8c4fcee){.reference
    .external})

-   fix inaccurate downloader middleware documentation. refs #280
    ([commit
    40667cb](https://github.com/scrapy/scrapy/commit/40667cb){.reference
    .external})

-   doc: remove links to diveintopython.org, which is no longer
    available. closes #246 ([commit
    bd58bfa](https://github.com/scrapy/scrapy/commit/bd58bfa){.reference
    .external})

-   Find form nodes in invalid html5 documents ([commit
    e3d6945](https://github.com/scrapy/scrapy/commit/e3d6945){.reference
    .external})

-   Fix typo labeling attrs type bool instead of list ([commit
    a274276](https://github.com/scrapy/scrapy/commit/a274276){.reference
    .external})
:::

::: {#scrapy-0-16-4-released-2013-01-23 .section}
#### Scrapy 0.16.4 (released 2013-01-23)[¶](#scrapy-0-16-4-released-2013-01-23 "Permalink to this heading"){.headerlink}

-   fixes spelling errors in documentation ([commit
    6d2b3aa](https://github.com/scrapy/scrapy/commit/6d2b3aa){.reference
    .external})

-   add doc about disabling an extension. refs #132 ([commit
    c90de33](https://github.com/scrapy/scrapy/commit/c90de33){.reference
    .external})

-   Fixed error message formatting. log.err() doesn't support cool
    formatting and when error occurred, the message was: "ERROR: Error
    processing %(item)s" ([commit
    c16150c](https://github.com/scrapy/scrapy/commit/c16150c){.reference
    .external})

-   lint and improve images pipeline error logging ([commit
    56b45fc](https://github.com/scrapy/scrapy/commit/56b45fc){.reference
    .external})

-   fixed doc typos ([commit
    243be84](https://github.com/scrapy/scrapy/commit/243be84){.reference
    .external})

-   add documentation topics: Broad Crawls & Common Practices ([commit
    1fbb715](https://github.com/scrapy/scrapy/commit/1fbb715){.reference
    .external})

-   fix bug in Scrapy parse command when spider is not specified
    explicitly. closes #209 ([commit
    c72e682](https://github.com/scrapy/scrapy/commit/c72e682){.reference
    .external})

-   Update docs/topics/commands.rst ([commit
    28eac7a](https://github.com/scrapy/scrapy/commit/28eac7a){.reference
    .external})
:::

::: {#scrapy-0-16-3-released-2012-12-07 .section}
#### Scrapy 0.16.3 (released 2012-12-07)[¶](#scrapy-0-16-3-released-2012-12-07 "Permalink to this heading"){.headerlink}

-   Remove concurrency limitation when using download delays and still
    ensure inter-request delays are enforced ([commit
    487b9b5](https://github.com/scrapy/scrapy/commit/487b9b5){.reference
    .external})

-   add error details when image pipeline fails ([commit
    8232569](https://github.com/scrapy/scrapy/commit/8232569){.reference
    .external})

-   improve macOS compatibility ([commit
    8dcf8aa](https://github.com/scrapy/scrapy/commit/8dcf8aa){.reference
    .external})

-   setup.py: use README.rst to populate long_description ([commit
    7b5310d](https://github.com/scrapy/scrapy/commit/7b5310d){.reference
    .external})

-   doc: removed obsolete references to ClientForm ([commit
    80f9bb6](https://github.com/scrapy/scrapy/commit/80f9bb6){.reference
    .external})

-   correct docs for default storage backend ([commit
    2aa491b](https://github.com/scrapy/scrapy/commit/2aa491b){.reference
    .external})

-   doc: removed broken proxyhub link from FAQ ([commit
    bdf61c4](https://github.com/scrapy/scrapy/commit/bdf61c4){.reference
    .external})

-   Fixed docs typo in SpiderOpenCloseLogging example ([commit
    7184094](https://github.com/scrapy/scrapy/commit/7184094){.reference
    .external})
:::

::: {#scrapy-0-16-2-released-2012-11-09 .section}
#### Scrapy 0.16.2 (released 2012-11-09)[¶](#scrapy-0-16-2-released-2012-11-09 "Permalink to this heading"){.headerlink}

-   Scrapy contracts: python2.6 compat ([commit
    a4a9199](https://github.com/scrapy/scrapy/commit/a4a9199){.reference
    .external})

-   Scrapy contracts verbose option ([commit
    ec41673](https://github.com/scrapy/scrapy/commit/ec41673){.reference
    .external})

-   proper unittest-like output for Scrapy contracts ([commit
    86635e4](https://github.com/scrapy/scrapy/commit/86635e4){.reference
    .external})

-   added open_in_browser to debugging doc ([commit
    c9b690d](https://github.com/scrapy/scrapy/commit/c9b690d){.reference
    .external})

-   removed reference to global Scrapy stats from settings doc ([commit
    dd55067](https://github.com/scrapy/scrapy/commit/dd55067){.reference
    .external})

-   Fix SpiderState bug in Windows platforms ([commit
    58998f4](https://github.com/scrapy/scrapy/commit/58998f4){.reference
    .external})
:::

::: {#scrapy-0-16-1-released-2012-10-26 .section}
#### Scrapy 0.16.1 (released 2012-10-26)[¶](#scrapy-0-16-1-released-2012-10-26 "Permalink to this heading"){.headerlink}

-   fixed LogStats extension, which got broken after a wrong merge
    before the 0.16 release ([commit
    8c780fd](https://github.com/scrapy/scrapy/commit/8c780fd){.reference
    .external})

-   better backward compatibility for scrapy.conf.settings ([commit
    3403089](https://github.com/scrapy/scrapy/commit/3403089){.reference
    .external})

-   extended documentation on how to access crawler stats from
    extensions ([commit
    c4da0b5](https://github.com/scrapy/scrapy/commit/c4da0b5){.reference
    .external})

-   removed .hgtags (no longer needed now that Scrapy uses git) ([commit
    d52c188](https://github.com/scrapy/scrapy/commit/d52c188){.reference
    .external})

-   fix dashes under rst headers ([commit
    fa4f7f9](https://github.com/scrapy/scrapy/commit/fa4f7f9){.reference
    .external})

-   set release date for 0.16.0 in news ([commit
    e292246](https://github.com/scrapy/scrapy/commit/e292246){.reference
    .external})
:::

::: {#scrapy-0-16-0-released-2012-10-18 .section}
#### Scrapy 0.16.0 (released 2012-10-18)[¶](#scrapy-0-16-0-released-2012-10-18 "Permalink to this heading"){.headerlink}

Scrapy changes:

-   added [[Spiders Contracts]{.std
    .std-ref}](index.html#topics-contracts){.hoverxref .tooltip
    .reference .internal}, a mechanism for testing spiders in a
    formal/reproducible way

-   added options [`-o`{.docutils .literal .notranslate}]{.pre} and
    [`-t`{.docutils .literal .notranslate}]{.pre} to the
    [[`runspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
    .tooltip .reference .internal} command

-   documented [[AutoThrottle
    extension]{.doc}](index.html#document-topics/autothrottle){.reference
    .internal} and added to extensions installed by default. You still
    need to enable it with [[`AUTOTHROTTLE_ENABLED`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AUTOTHROTTLE_ENABLED){.hoverxref
    .tooltip .reference .internal}

-   major Stats Collection refactoring: removed separation of
    global/per-spider stats, removed stats-related signals
    ([`stats_spider_opened`{.docutils .literal .notranslate}]{.pre},
    etc). Stats are much simpler now, backward compatibility is kept on
    the Stats Collector API and signals.

-   added [[`process_start_requests()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_start_requests "scrapy.spidermiddlewares.SpiderMiddleware.process_start_requests"){.reference
    .internal} method to spider middlewares

-   dropped Signals singleton. Signals should now be accessed through
    the Crawler.signals attribute. See the signals documentation for
    more info.

-   dropped Stats Collector singleton. Stats can now be accessed through
    the Crawler.stats attribute. See the stats collection documentation
    for more info.

-   documented [[Core API]{.std
    .std-ref}](index.html#topics-api){.hoverxref .tooltip .reference
    .internal}

-   [`lxml`{.docutils .literal .notranslate}]{.pre} is now the default
    selectors backend instead of [`libxml2`{.docutils .literal
    .notranslate}]{.pre}

-   ported FormRequest.from_response() to use
    [lxml](https://lxml.de/){.reference .external} instead of
    [ClientForm](http://wwwsearch.sourceforge.net/old/ClientForm/){.reference
    .external}

-   removed modules: [`scrapy.xlib.BeautifulSoup`{.docutils .literal
    .notranslate}]{.pre} and [`scrapy.xlib.ClientForm`{.docutils
    .literal .notranslate}]{.pre}

-   SitemapSpider: added support for sitemap urls ending in .xml and
    .xml.gz, even if they advertise a wrong content type ([commit
    10ed28b](https://github.com/scrapy/scrapy/commit/10ed28b){.reference
    .external})

-   StackTraceDump extension: also dump trackref live references
    ([commit
    fe2ce93](https://github.com/scrapy/scrapy/commit/fe2ce93){.reference
    .external})

-   nested items now fully supported in JSON and JSONLines exporters

-   added [[`cookiejar`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-cookiejar){.hoverxref
    .tooltip .reference .internal} Request meta key to support multiple
    cookie sessions per spider

-   decoupled encoding detection code to
    [w3lib.encoding](https://github.com/scrapy/w3lib/blob/master/w3lib/encoding.py){.reference
    .external}, and ported Scrapy code to use that module

-   dropped support for Python 2.5. See
    [https://blog.scrapinghub.com/2012/02/27/scrapy-0-15-dropping-support-for-python-2-5/](https://blog.scrapinghub.com/2012/02/27/scrapy-0-15-dropping-support-for-python-2-5/){.reference
    .external}

-   dropped support for Twisted 2.5

-   added [[`REFERER_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-REFERER_ENABLED){.hoverxref
    .tooltip .reference .internal} setting, to control referer
    middleware

-   changed default user agent to: [`Scrapy/VERSION`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`(+http://scrapy.org)`{.docutils .literal
    .notranslate}]{.pre}

-   removed (undocumented) [`HTMLImageLinkExtractor`{.docutils .literal
    .notranslate}]{.pre} class from
    [`scrapy.contrib.linkextractors.image`{.docutils .literal
    .notranslate}]{.pre}

-   removed per-spider settings (to be replaced by instantiating
    multiple crawler objects)

-   [`USER_AGENT`{.docutils .literal .notranslate}]{.pre} spider
    attribute will no longer work, use [`user_agent`{.docutils .literal
    .notranslate}]{.pre} attribute instead

-   [`DOWNLOAD_TIMEOUT`{.docutils .literal .notranslate}]{.pre} spider
    attribute will no longer work, use [`download_timeout`{.docutils
    .literal .notranslate}]{.pre} attribute instead

-   removed [`ENCODING_ALIASES`{.docutils .literal .notranslate}]{.pre}
    setting, as encoding auto-detection has been moved to the
    [w3lib](https://github.com/scrapy/w3lib){.reference .external}
    library

-   promoted [[DjangoItem]{.std
    .std-ref}](index.html#topics-djangoitem){.hoverxref .tooltip
    .reference .internal} to main contrib

-   LogFormatter method now return dicts(instead of strings) to support
    lazy formatting ([issue
    164](https://github.com/scrapy/scrapy/issues/164){.reference
    .external}, [commit
    dcef7b0](https://github.com/scrapy/scrapy/commit/dcef7b0){.reference
    .external})

-   downloader handlers ([[`DOWNLOAD_HANDLERS`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal} setting) now receive settings as the
    first argument of the [`__init__`{.docutils .literal
    .notranslate}]{.pre} method

-   replaced memory usage accounting with (more portable)
    [resource](https://docs.python.org/2/library/resource.html){.reference
    .external} module, removed [`scrapy.utils.memory`{.docutils .literal
    .notranslate}]{.pre} module

-   removed signal: [`scrapy.mail.mail_sent`{.docutils .literal
    .notranslate}]{.pre}

-   removed [`TRACK_REFS`{.docutils .literal .notranslate}]{.pre}
    setting, now [[trackrefs]{.std
    .std-ref}](index.html#topics-leaks-trackrefs){.hoverxref .tooltip
    .reference .internal} is always enabled

-   DBM is now the default storage backend for HTTP cache middleware

-   number of log messages (per level) are now tracked through Scrapy
    stats (stat name: [`log_count/LEVEL`{.docutils .literal
    .notranslate}]{.pre})

-   number received responses are now tracked through Scrapy stats (stat
    name: [`response_received_count`{.docutils .literal
    .notranslate}]{.pre})

-   removed [`scrapy.log.started`{.docutils .literal
    .notranslate}]{.pre} attribute
:::

::: {#scrapy-0-14-4 .section}
#### Scrapy 0.14.4[¶](#scrapy-0-14-4 "Permalink to this heading"){.headerlink}

-   added precise to supported Ubuntu distros ([commit
    b7e46df](https://github.com/scrapy/scrapy/commit/b7e46df){.reference
    .external})

-   fixed bug in json-rpc webservice reported in
    [https://groups.google.com/forum/#!topic/scrapy-users/qgVBmFybNAQ/discussion](https://groups.google.com/forum/#!topic/scrapy-users/qgVBmFybNAQ/discussion){.reference
    .external}. also removed no longer supported 'run' command from
    extras/scrapy-ws.py ([commit
    340fbdb](https://github.com/scrapy/scrapy/commit/340fbdb){.reference
    .external})

-   meta tag attributes for content-type http equiv can be in any order.
    #123 ([commit
    0cb68af](https://github.com/scrapy/scrapy/commit/0cb68af){.reference
    .external})

-   replace "import Image" by more standard "from PIL import Image".
    closes #88 ([commit
    4d17048](https://github.com/scrapy/scrapy/commit/4d17048){.reference
    .external})

-   return trial status as bin/runtests.sh exit value. #118 ([commit
    b7b2e7f](https://github.com/scrapy/scrapy/commit/b7b2e7f){.reference
    .external})
:::

::: {#scrapy-0-14-3 .section}
#### Scrapy 0.14.3[¶](#scrapy-0-14-3 "Permalink to this heading"){.headerlink}

-   forgot to include pydispatch license. #118 ([commit
    fd85f9c](https://github.com/scrapy/scrapy/commit/fd85f9c){.reference
    .external})

-   include egg files used by testsuite in source distribution. #118
    ([commit
    c897793](https://github.com/scrapy/scrapy/commit/c897793){.reference
    .external})

-   update docstring in project template to avoid confusion with
    genspider command, which may be considered as an advanced feature.
    refs #107 ([commit
    2548dcc](https://github.com/scrapy/scrapy/commit/2548dcc){.reference
    .external})

-   added note to docs/topics/firebug.rst about google directory being
    shut down ([commit
    668e352](https://github.com/scrapy/scrapy/commit/668e352){.reference
    .external})

-   don't discard slot when empty, just save in another dict in order to
    recycle if needed again. ([commit
    8e9f607](https://github.com/scrapy/scrapy/commit/8e9f607){.reference
    .external})

-   do not fail handling unicode xpaths in libxml2 backed selectors
    ([commit
    b830e95](https://github.com/scrapy/scrapy/commit/b830e95){.reference
    .external})

-   fixed minor mistake in Request objects documentation ([commit
    bf3c9ee](https://github.com/scrapy/scrapy/commit/bf3c9ee){.reference
    .external})

-   fixed minor defect in link extractors documentation ([commit
    ba14f38](https://github.com/scrapy/scrapy/commit/ba14f38){.reference
    .external})

-   removed some obsolete remaining code related to sqlite support in
    Scrapy ([commit
    0665175](https://github.com/scrapy/scrapy/commit/0665175){.reference
    .external})
:::

::: {#scrapy-0-14-2 .section}
#### Scrapy 0.14.2[¶](#scrapy-0-14-2 "Permalink to this heading"){.headerlink}

-   move buffer pointing to start of file before computing checksum.
    refs #92 ([commit
    6a5bef2](https://github.com/scrapy/scrapy/commit/6a5bef2){.reference
    .external})

-   Compute image checksum before persisting images. closes #92 ([commit
    9817df1](https://github.com/scrapy/scrapy/commit/9817df1){.reference
    .external})

-   remove leaking references in cached failures ([commit
    673a120](https://github.com/scrapy/scrapy/commit/673a120){.reference
    .external})

-   fixed bug in MemoryUsage extension: get_engine_status() takes
    exactly 1 argument (0 given) ([commit
    11133e9](https://github.com/scrapy/scrapy/commit/11133e9){.reference
    .external})

-   fixed struct.error on http compression middleware. closes #87
    ([commit
    1423140](https://github.com/scrapy/scrapy/commit/1423140){.reference
    .external})

-   ajax crawling wasn't expanding for unicode urls ([commit
    0de3fb4](https://github.com/scrapy/scrapy/commit/0de3fb4){.reference
    .external})

-   Catch start_requests iterator errors. refs #83 ([commit
    454a21d](https://github.com/scrapy/scrapy/commit/454a21d){.reference
    .external})

-   Speed-up libxml2 XPathSelector ([commit
    2fbd662](https://github.com/scrapy/scrapy/commit/2fbd662){.reference
    .external})

-   updated versioning doc according to recent changes ([commit
    0a070f5](https://github.com/scrapy/scrapy/commit/0a070f5){.reference
    .external})

-   scrapyd: fixed documentation link ([commit
    2b4e4c3](https://github.com/scrapy/scrapy/commit/2b4e4c3){.reference
    .external})

-   extras/makedeb.py: no longer obtaining version from git ([commit
    caffe0e](https://github.com/scrapy/scrapy/commit/caffe0e){.reference
    .external})
:::

::: {#scrapy-0-14-1 .section}
#### Scrapy 0.14.1[¶](#scrapy-0-14-1 "Permalink to this heading"){.headerlink}

-   extras/makedeb.py: no longer obtaining version from git ([commit
    caffe0e](https://github.com/scrapy/scrapy/commit/caffe0e){.reference
    .external})

-   bumped version to 0.14.1 ([commit
    6cb9e1c](https://github.com/scrapy/scrapy/commit/6cb9e1c){.reference
    .external})

-   fixed reference to tutorial directory ([commit
    4b86bd6](https://github.com/scrapy/scrapy/commit/4b86bd6){.reference
    .external})

-   doc: removed duplicated callback argument from Request.replace()
    ([commit
    1aeccdd](https://github.com/scrapy/scrapy/commit/1aeccdd){.reference
    .external})

-   fixed formatting of scrapyd doc ([commit
    8bf19e6](https://github.com/scrapy/scrapy/commit/8bf19e6){.reference
    .external})

-   Dump stacks for all running threads and fix engine status dumped by
    StackTraceDump extension ([commit
    14a8e6e](https://github.com/scrapy/scrapy/commit/14a8e6e){.reference
    .external})

-   added comment about why we disable ssl on boto images upload
    ([commit
    5223575](https://github.com/scrapy/scrapy/commit/5223575){.reference
    .external})

-   SSL handshaking hangs when doing too many parallel connections to S3
    ([commit
    63d583d](https://github.com/scrapy/scrapy/commit/63d583d){.reference
    .external})

-   change tutorial to follow changes on dmoz site ([commit
    bcb3198](https://github.com/scrapy/scrapy/commit/bcb3198){.reference
    .external})

-   Avoid \_disconnectedDeferred AttributeError exception in
    Twisted\>=11.1.0 ([commit
    98f3f87](https://github.com/scrapy/scrapy/commit/98f3f87){.reference
    .external})

-   allow spider to set autothrottle max concurrency ([commit
    175a4b5](https://github.com/scrapy/scrapy/commit/175a4b5){.reference
    .external})
:::

::: {#scrapy-0-14 .section}
#### Scrapy 0.14[¶](#scrapy-0-14 "Permalink to this heading"){.headerlink}

::: {#new-features-and-settings .section}
##### New features and settings[¶](#new-features-and-settings "Permalink to this heading"){.headerlink}

-   Support for [AJAX crawlable
    urls](https://developers.google.com/search/docs/ajax-crawling/docs/getting-started?csw=1){.reference
    .external}

-   New persistent scheduler that stores requests on disk, allowing to
    suspend and resume crawls
    ([r2737](http://hg.scrapy.org/scrapy/changeset/2737){.reference
    .external})

-   added [`-o`{.docutils .literal .notranslate}]{.pre} option to
    [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`crawl`{.docutils .literal
    .notranslate}]{.pre}, a shortcut for dumping scraped items into a
    file (or standard output using [`-`{.docutils .literal
    .notranslate}]{.pre})

-   Added support for passing custom settings to Scrapyd
    [`schedule.json`{.docutils .literal .notranslate}]{.pre} api
    ([r2779](http://hg.scrapy.org/scrapy/changeset/2779){.reference
    .external},
    [r2783](http://hg.scrapy.org/scrapy/changeset/2783){.reference
    .external})

-   New [`ChunkedTransferMiddleware`{.docutils .literal
    .notranslate}]{.pre} (enabled by default) to support [chunked
    transfer
    encoding](https://en.wikipedia.org/wiki/Chunked_transfer_encoding){.reference
    .external}
    ([r2769](http://hg.scrapy.org/scrapy/changeset/2769){.reference
    .external})

-   Add boto 2.0 support for S3 downloader handler
    ([r2763](http://hg.scrapy.org/scrapy/changeset/2763){.reference
    .external})

-   Added
    [marshal](https://docs.python.org/2/library/marshal.html){.reference
    .external} to formats supported by feed exports
    ([r2744](http://hg.scrapy.org/scrapy/changeset/2744){.reference
    .external})

-   In request errbacks, offending requests are now received in
    [`failure.request`{.docutils .literal .notranslate}]{.pre} attribute
    ([r2738](http://hg.scrapy.org/scrapy/changeset/2738){.reference
    .external})

-   

    Big downloader refactoring to support per domain/ip concurrency limits ([r2732](http://hg.scrapy.org/scrapy/changeset/2732){.reference .external})

    :   -   

            [`CONCURRENT_REQUESTS_PER_SPIDER`{.docutils .literal .notranslate}]{.pre} setting has been deprecated and replaced by:

            :   -   [[`CONCURRENT_REQUESTS`{.xref .std .std-setting
                    .docutils .literal
                    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS){.hoverxref
                    .tooltip .reference .internal},
                    [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std
                    .std-setting .docutils .literal
                    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
                    .tooltip .reference .internal},
                    [[`CONCURRENT_REQUESTS_PER_IP`{.xref .std
                    .std-setting .docutils .literal
                    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
                    .tooltip .reference .internal}

        -   check the documentation for more details

-   Added builtin caching DNS resolver
    ([r2728](http://hg.scrapy.org/scrapy/changeset/2728){.reference
    .external})

-   Moved Amazon AWS-related components/extensions (SQS spider queue,
    SimpleDB stats collector) to a separate project:
    \[scaws\]([https://github.com/scrapinghub/scaws](https://github.com/scrapinghub/scaws){.reference
    .external})
    ([r2706](http://hg.scrapy.org/scrapy/changeset/2706){.reference
    .external},
    [r2714](http://hg.scrapy.org/scrapy/changeset/2714){.reference
    .external})

-   Moved spider queues to scrapyd: [`scrapy.spiderqueue`{.docutils
    .literal .notranslate}]{.pre} -\> [`scrapyd.spiderqueue`{.docutils
    .literal .notranslate}]{.pre}
    ([r2708](http://hg.scrapy.org/scrapy/changeset/2708){.reference
    .external})

-   Moved sqlite utils to scrapyd: [`scrapy.utils.sqlite`{.docutils
    .literal .notranslate}]{.pre} -\> [`scrapyd.sqlite`{.docutils
    .literal .notranslate}]{.pre}
    ([r2781](http://hg.scrapy.org/scrapy/changeset/2781){.reference
    .external})

-   Real support for returning iterators on
    [`start_requests()`{.docutils .literal .notranslate}]{.pre} method.
    The iterator is now consumed during the crawl when the spider is
    getting idle
    ([r2704](http://hg.scrapy.org/scrapy/changeset/2704){.reference
    .external})

-   Added [[`REDIRECT_ENABLED`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-REDIRECT_ENABLED){.hoverxref
    .tooltip .reference .internal} setting to quickly enable/disable the
    redirect middleware
    ([r2697](http://hg.scrapy.org/scrapy/changeset/2697){.reference
    .external})

-   Added [[`RETRY_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-RETRY_ENABLED){.hoverxref
    .tooltip .reference .internal} setting to quickly enable/disable the
    retry middleware
    ([r2694](http://hg.scrapy.org/scrapy/changeset/2694){.reference
    .external})

-   Added [`CloseSpider`{.docutils .literal .notranslate}]{.pre}
    exception to manually close spiders
    ([r2691](http://hg.scrapy.org/scrapy/changeset/2691){.reference
    .external})

-   Improved encoding detection by adding support for HTML5 meta charset
    declaration
    ([r2690](http://hg.scrapy.org/scrapy/changeset/2690){.reference
    .external})

-   Refactored close spider behavior to wait for all downloads to finish
    and be processed by spiders, before closing the spider
    ([r2688](http://hg.scrapy.org/scrapy/changeset/2688){.reference
    .external})

-   Added [`SitemapSpider`{.docutils .literal .notranslate}]{.pre} (see
    documentation in Spiders page)
    ([r2658](http://hg.scrapy.org/scrapy/changeset/2658){.reference
    .external})

-   Added [`LogStats`{.docutils .literal .notranslate}]{.pre} extension
    for periodically logging basic stats (like crawled pages and scraped
    items)
    ([r2657](http://hg.scrapy.org/scrapy/changeset/2657){.reference
    .external})

-   Make handling of gzipped responses more robust (#319,
    [r2643](http://hg.scrapy.org/scrapy/changeset/2643){.reference
    .external}). Now Scrapy will try and decompress as much as possible
    from a gzipped response, instead of failing with an
    [`IOError`{.docutils .literal .notranslate}]{.pre}.

-   Simplified !MemoryDebugger extension to use stats for dumping memory
    debugging info
    ([r2639](http://hg.scrapy.org/scrapy/changeset/2639){.reference
    .external})

-   Added new command to edit spiders: [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`edit`{.docutils .literal .notranslate}]{.pre}
    ([r2636](http://hg.scrapy.org/scrapy/changeset/2636){.reference
    .external}) and [`-e`{.docutils .literal .notranslate}]{.pre} flag
    to [`genspider`{.docutils .literal .notranslate}]{.pre} command that
    uses it
    ([r2653](http://hg.scrapy.org/scrapy/changeset/2653){.reference
    .external})

-   Changed default representation of items to pretty-printed dicts.
    ([r2631](http://hg.scrapy.org/scrapy/changeset/2631){.reference
    .external}). This improves default logging by making log more
    readable in the default case, for both Scraped and Dropped lines.

-   Added [[`spider_error`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-spider_error){.hoverxref
    .tooltip .reference .internal} signal
    ([r2628](http://hg.scrapy.org/scrapy/changeset/2628){.reference
    .external})

-   Added [[`COOKIES_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-COOKIES_ENABLED){.hoverxref
    .tooltip .reference .internal} setting
    ([r2625](http://hg.scrapy.org/scrapy/changeset/2625){.reference
    .external})

-   Stats are now dumped to Scrapy log (default value of
    [[`STATS_DUMP`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-STATS_DUMP){.hoverxref
    .tooltip .reference .internal} setting has been changed to
    [`True`{.docutils .literal .notranslate}]{.pre}). This is to make
    Scrapy users more aware of Scrapy stats and the data that is
    collected there.

-   Added support for dynamically adjusting download delay and maximum
    concurrent requests
    ([r2599](http://hg.scrapy.org/scrapy/changeset/2599){.reference
    .external})

-   Added new DBM HTTP cache storage backend
    ([r2576](http://hg.scrapy.org/scrapy/changeset/2576){.reference
    .external})

-   Added [`listjobs.json`{.docutils .literal .notranslate}]{.pre} API
    to Scrapyd
    ([r2571](http://hg.scrapy.org/scrapy/changeset/2571){.reference
    .external})

-   [`CsvItemExporter`{.docutils .literal .notranslate}]{.pre}: added
    [`join_multivalued`{.docutils .literal .notranslate}]{.pre}
    parameter
    ([r2578](http://hg.scrapy.org/scrapy/changeset/2578){.reference
    .external})

-   Added namespace support to [`xmliter_lxml`{.docutils .literal
    .notranslate}]{.pre}
    ([r2552](http://hg.scrapy.org/scrapy/changeset/2552){.reference
    .external})

-   Improved cookies middleware by making [`COOKIES_DEBUG`{.docutils
    .literal .notranslate}]{.pre} nicer and documenting it
    ([r2579](http://hg.scrapy.org/scrapy/changeset/2579){.reference
    .external})

-   Several improvements to Scrapyd and Link extractors
:::

::: {#code-rearranged-and-removed .section}
##### Code rearranged and removed[¶](#code-rearranged-and-removed "Permalink to this heading"){.headerlink}

-   

    Merged item passed and item scraped concepts, as they have often proved confusing in the past. This means: ([r2630](http://hg.scrapy.org/scrapy/changeset/2630){.reference .external})

    :   -   original item_scraped signal was removed

        -   original item_passed signal was renamed to item_scraped

        -   old log lines [`Scraped`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`Item...`{.docutils .literal
            .notranslate}]{.pre} were removed

        -   old log lines [`Passed`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`Item...`{.docutils .literal
            .notranslate}]{.pre} were renamed to [`Scraped`{.docutils
            .literal .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`Item...`{.docutils .literal
            .notranslate}]{.pre} lines and downgraded to
            [`DEBUG`{.docutils .literal .notranslate}]{.pre} level

-   

    Reduced Scrapy codebase by striping part of Scrapy code into two new libraries:

    :   -   [w3lib](https://github.com/scrapy/w3lib){.reference
            .external} (several functions from
            [`scrapy.utils.{http,markup,multipart,response,url}`{.docutils
            .literal .notranslate}]{.pre}, done in
            [r2584](http://hg.scrapy.org/scrapy/changeset/2584){.reference
            .external})

        -   [scrapely](https://github.com/scrapy/scrapely){.reference
            .external} (was [`scrapy.contrib.ibl`{.docutils .literal
            .notranslate}]{.pre}, done in
            [r2586](http://hg.scrapy.org/scrapy/changeset/2586){.reference
            .external})

-   Removed unused function:
    [`scrapy.utils.request.request_info()`{.docutils .literal
    .notranslate}]{.pre}
    ([r2577](http://hg.scrapy.org/scrapy/changeset/2577){.reference
    .external})

-   Removed googledir project from [`examples/googledir`{.docutils
    .literal .notranslate}]{.pre}. There's now a new example project
    called [`dirbot`{.docutils .literal .notranslate}]{.pre} available
    on GitHub:
    [https://github.com/scrapy/dirbot](https://github.com/scrapy/dirbot){.reference
    .external}

-   Removed support for default field values in Scrapy items
    ([r2616](http://hg.scrapy.org/scrapy/changeset/2616){.reference
    .external})

-   Removed experimental crawlspider v2
    ([r2632](http://hg.scrapy.org/scrapy/changeset/2632){.reference
    .external})

-   Removed scheduler middleware to simplify architecture. Duplicates
    filter is now done in the scheduler itself, using the same dupe
    filtering class as before ([`DUPEFILTER_CLASS`{.docutils .literal
    .notranslate}]{.pre} setting)
    ([r2640](http://hg.scrapy.org/scrapy/changeset/2640){.reference
    .external})

-   Removed support for passing urls to [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`crawl`{.docutils .literal .notranslate}]{.pre}
    command (use [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`parse`{.docutils .literal .notranslate}]{.pre}
    instead)
    ([r2704](http://hg.scrapy.org/scrapy/changeset/2704){.reference
    .external})

-   Removed deprecated Execution Queue
    ([r2704](http://hg.scrapy.org/scrapy/changeset/2704){.reference
    .external})

-   Removed (undocumented) spider context extension (from
    scrapy.contrib.spidercontext)
    ([r2780](http://hg.scrapy.org/scrapy/changeset/2780){.reference
    .external})

-   removed [`CONCURRENT_SPIDERS`{.docutils .literal
    .notranslate}]{.pre} setting (use scrapyd maxproc instead)
    ([r2789](http://hg.scrapy.org/scrapy/changeset/2789){.reference
    .external})

-   Renamed attributes of core components: downloader.sites -\>
    downloader.slots, scraper.sites -\> scraper.slots
    ([r2717](http://hg.scrapy.org/scrapy/changeset/2717){.reference
    .external},
    [r2718](http://hg.scrapy.org/scrapy/changeset/2718){.reference
    .external})

-   Renamed setting [`CLOSESPIDER_ITEMPASSED`{.docutils .literal
    .notranslate}]{.pre} to [[`CLOSESPIDER_ITEMCOUNT`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-CLOSESPIDER_ITEMCOUNT){.hoverxref
    .tooltip .reference .internal}
    ([r2655](http://hg.scrapy.org/scrapy/changeset/2655){.reference
    .external}). Backward compatibility kept.
:::
:::

::: {#scrapy-0-12 .section}
#### Scrapy 0.12[¶](#scrapy-0-12 "Permalink to this heading"){.headerlink}

The numbers like #NNN reference tickets in the old issue tracker (Trac)
which is no longer available.

::: {#new-features-and-improvements .section}
##### New features and improvements[¶](#new-features-and-improvements "Permalink to this heading"){.headerlink}

-   Passed item is now sent in the [`item`{.docutils .literal
    .notranslate}]{.pre} argument of the [[`item_passed`{.xref .std
    .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-item_scraped){.hoverxref
    .tooltip .reference .internal} (#273)

-   Added verbose option to [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`version`{.docutils .literal .notranslate}]{.pre}
    command, useful for bug reports (#298)

-   HTTP cache now stored by default in the project data dir (#279)

-   Added project data storage directory (#276, #277)

-   Documented file structure of Scrapy projects (see command-line tool
    doc)

-   New lxml backend for XPath selectors (#147)

-   Per-spider settings (#245)

-   Support exit codes to signal errors in Scrapy commands (#248)

-   Added [`-c`{.docutils .literal .notranslate}]{.pre} argument to
    [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`shell`{.docutils .literal
    .notranslate}]{.pre} command

-   Made [`libxml2`{.docutils .literal .notranslate}]{.pre} optional
    (#260)

-   New [`deploy`{.docutils .literal .notranslate}]{.pre} command (#261)

-   Added [[`CLOSESPIDER_PAGECOUNT`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-CLOSESPIDER_PAGECOUNT){.hoverxref
    .tooltip .reference .internal} setting (#253)

-   Added [[`CLOSESPIDER_ERRORCOUNT`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-CLOSESPIDER_ERRORCOUNT){.hoverxref
    .tooltip .reference .internal} setting (#254)
:::

::: {#scrapyd-changes .section}
##### Scrapyd changes[¶](#scrapyd-changes "Permalink to this heading"){.headerlink}

-   Scrapyd now uses one process per spider

-   It stores one log file per spider run, and rotate them keeping the
    latest 5 logs per spider (by default)

-   A minimal web ui was added, available at
    [http://localhost:6800](http://localhost:6800){.reference .external}
    by default

-   There is now a [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`server`{.docutils .literal .notranslate}]{.pre}
    command to start a Scrapyd server of the current project
:::

::: {#changes-to-settings .section}
##### Changes to settings[¶](#changes-to-settings "Permalink to this heading"){.headerlink}

-   added [`HTTPCACHE_ENABLED`{.docutils .literal .notranslate}]{.pre}
    setting (False by default) to enable HTTP cache middleware

-   changed [`HTTPCACHE_EXPIRATION_SECS`{.docutils .literal
    .notranslate}]{.pre} semantics: now zero means "never expire".
:::

::: {#deprecated-obsoleted-functionality .section}
##### Deprecated/obsoleted functionality[¶](#deprecated-obsoleted-functionality "Permalink to this heading"){.headerlink}

-   Deprecated [`runserver`{.docutils .literal .notranslate}]{.pre}
    command in favor of [`server`{.docutils .literal
    .notranslate}]{.pre} command which starts a Scrapyd server. See
    also: Scrapyd changes

-   Deprecated [`queue`{.docutils .literal .notranslate}]{.pre} command
    in favor of using Scrapyd [`schedule.json`{.docutils .literal
    .notranslate}]{.pre} API. See also: Scrapyd changes

-   Removed the !LxmlItemLoader (experimental contrib which never
    graduated to main contrib)
:::
:::

::: {#scrapy-0-10 .section}
#### Scrapy 0.10[¶](#scrapy-0-10 "Permalink to this heading"){.headerlink}

The numbers like #NNN reference tickets in the old issue tracker (Trac)
which is no longer available.

::: {#id133 .section}
##### New features and improvements[¶](#id133 "Permalink to this heading"){.headerlink}

-   New Scrapy service called [`scrapyd`{.docutils .literal
    .notranslate}]{.pre} for deploying Scrapy crawlers in production
    (#218) (documentation available)

-   Simplified Images pipeline usage which doesn't require subclassing
    your own images pipeline now (#217)

-   Scrapy shell now shows the Scrapy log by default (#206)

-   Refactored execution queue in a common base code and pluggable
    backends called "spider queues" (#220)

-   New persistent spider queue (based on SQLite) (#198), available by
    default, which allows to start Scrapy in server mode and then
    schedule spiders to run.

-   Added documentation for Scrapy command-line tool and all its
    available sub-commands. (documentation available)

-   Feed exporters with pluggable backends (#197) (documentation
    available)

-   Deferred signals (#193)

-   Added two new methods to item pipeline open_spider(), close_spider()
    with deferred support (#195)

-   Support for overriding default request headers per spider (#181)

-   Replaced default Spider Manager with one with similar functionality
    but not depending on Twisted Plugins (#186)

-   Split Debian package into two packages - the library and the service
    (#187)

-   Scrapy log refactoring (#188)

-   New extension for keeping persistent spider contexts among different
    runs (#203)

-   Added [`dont_redirect`{.docutils .literal .notranslate}]{.pre}
    request.meta key for avoiding redirects (#233)

-   Added [`dont_retry`{.docutils .literal .notranslate}]{.pre}
    request.meta key for avoiding retries (#234)
:::

::: {#command-line-tool-changes .section}
##### Command-line tool changes[¶](#command-line-tool-changes "Permalink to this heading"){.headerlink}

-   New [`scrapy`{.docutils .literal .notranslate}]{.pre} command which
    replaces the old [`scrapy-ctl.py`{.docutils .literal
    .notranslate}]{.pre} (#199) - there is only one global
    [`scrapy`{.docutils .literal .notranslate}]{.pre} command now,
    instead of one [`scrapy-ctl.py`{.docutils .literal
    .notranslate}]{.pre} per project - Added [`scrapy.bat`{.docutils
    .literal .notranslate}]{.pre} script for running more conveniently
    from Windows

-   Added bash completion to command-line tool (#210)

-   Renamed command [`start`{.docutils .literal .notranslate}]{.pre} to
    [`runserver`{.docutils .literal .notranslate}]{.pre} (#209)
:::

::: {#api-changes .section}
##### API changes[¶](#api-changes "Permalink to this heading"){.headerlink}

-   [`url`{.docutils .literal .notranslate}]{.pre} and [`body`{.docutils
    .literal .notranslate}]{.pre} attributes of Request objects are now
    read-only (#230)

-   [`Request.copy()`{.docutils .literal .notranslate}]{.pre} and
    [`Request.replace()`{.docutils .literal .notranslate}]{.pre} now
    also copies their [`callback`{.docutils .literal
    .notranslate}]{.pre} and [`errback`{.docutils .literal
    .notranslate}]{.pre} attributes (#231)

-   Removed [`UrlFilterMiddleware`{.docutils .literal
    .notranslate}]{.pre} from [`scrapy.contrib`{.docutils .literal
    .notranslate}]{.pre} (already disabled by default)

-   Offsite middleware doesn't filter out any request coming from a
    spider that doesn't have a allowed_domains attribute (#225)

-   Removed Spider Manager [`load()`{.docutils .literal
    .notranslate}]{.pre} method. Now spiders are loaded in the
    [`__init__`{.docutils .literal .notranslate}]{.pre} method itself.

-   

    Changes to Scrapy Manager (now called "Crawler"):

    :   -   [`scrapy.core.manager.ScrapyManager`{.docutils .literal
            .notranslate}]{.pre} class renamed to
            [`scrapy.crawler.Crawler`{.docutils .literal
            .notranslate}]{.pre}

        -   [`scrapy.core.manager.scrapymanager`{.docutils .literal
            .notranslate}]{.pre} singleton moved to
            [`scrapy.project.crawler`{.docutils .literal
            .notranslate}]{.pre}

-   Moved module: [`scrapy.contrib.spidermanager`{.docutils .literal
    .notranslate}]{.pre} to [`scrapy.spidermanager`{.docutils .literal
    .notranslate}]{.pre}

-   Spider Manager singleton moved from
    [`scrapy.spider.spiders`{.docutils .literal .notranslate}]{.pre} to
    the [`` spiders` ``{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`attribute`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`of`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[``` ``scrapy.project.crawler ```{.docutils .literal
    .notranslate}]{.pre} singleton.

-   

    moved Stats Collector classes: (#204)

    :   -   [`scrapy.stats.collector.StatsCollector`{.docutils .literal
            .notranslate}]{.pre} to
            [`scrapy.statscol.StatsCollector`{.docutils .literal
            .notranslate}]{.pre}

        -   [`scrapy.stats.collector.SimpledbStatsCollector`{.docutils
            .literal .notranslate}]{.pre} to
            [`scrapy.contrib.statscol.SimpledbStatsCollector`{.docutils
            .literal .notranslate}]{.pre}

-   default per-command settings are now specified in the
    [`default_settings`{.docutils .literal .notranslate}]{.pre}
    attribute of command object class (#201)

-   

    changed arguments of Item pipeline [`process_item()`{.docutils .literal .notranslate}]{.pre} method from [`(spider,`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`item)`{.docutils .literal .notranslate}]{.pre} to [`(item,`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`spider)`{.docutils .literal .notranslate}]{.pre}

    :   -   backward compatibility kept (with deprecation warning)

-   

    moved [`scrapy.core.signals`{.docutils .literal .notranslate}]{.pre} module to [`scrapy.signals`{.docutils .literal .notranslate}]{.pre}

    :   -   backward compatibility kept (with deprecation warning)

-   

    moved [`scrapy.core.exceptions`{.docutils .literal .notranslate}]{.pre} module to [`scrapy.exceptions`{.docutils .literal .notranslate}]{.pre}

    :   -   backward compatibility kept (with deprecation warning)

-   added [`handles_request()`{.docutils .literal .notranslate}]{.pre}
    class method to [`BaseSpider`{.docutils .literal
    .notranslate}]{.pre}

-   dropped [`scrapy.log.exc()`{.docutils .literal .notranslate}]{.pre}
    function (use [`scrapy.log.err()`{.docutils .literal
    .notranslate}]{.pre} instead)

-   dropped [`component`{.docutils .literal .notranslate}]{.pre}
    argument of [`scrapy.log.msg()`{.docutils .literal
    .notranslate}]{.pre} function

-   dropped [`scrapy.log.log_level`{.docutils .literal
    .notranslate}]{.pre} attribute

-   Added [`from_settings()`{.docutils .literal .notranslate}]{.pre}
    class methods to Spider Manager, and Item Pipeline Manager
:::

::: {#id134 .section}
##### Changes to settings[¶](#id134 "Permalink to this heading"){.headerlink}

-   Added [`HTTPCACHE_IGNORE_SCHEMES`{.docutils .literal
    .notranslate}]{.pre} setting to ignore certain schemes on
    !HttpCacheMiddleware (#225)

-   Added [`SPIDER_QUEUE_CLASS`{.docutils .literal .notranslate}]{.pre}
    setting which defines the spider queue to use (#220)

-   Added [`KEEP_ALIVE`{.docutils .literal .notranslate}]{.pre} setting
    (#220)

-   Removed [`SERVICE_QUEUE`{.docutils .literal .notranslate}]{.pre}
    setting (#220)

-   Removed [`COMMANDS_SETTINGS_MODULE`{.docutils .literal
    .notranslate}]{.pre} setting (#201)

-   Renamed [`REQUEST_HANDLERS`{.docutils .literal .notranslate}]{.pre}
    to [`DOWNLOAD_HANDLERS`{.docutils .literal .notranslate}]{.pre} and
    make download handlers classes (instead of functions)
:::
:::

::: {#scrapy-0-9 .section}
#### Scrapy 0.9[¶](#scrapy-0-9 "Permalink to this heading"){.headerlink}

The numbers like #NNN reference tickets in the old issue tracker (Trac)
which is no longer available.

::: {#id135 .section}
##### New features and improvements[¶](#id135 "Permalink to this heading"){.headerlink}

-   Added SMTP-AUTH support to scrapy.mail

-   New settings added: [`MAIL_USER`{.docutils .literal
    .notranslate}]{.pre}, [`MAIL_PASS`{.docutils .literal
    .notranslate}]{.pre}
    ([r2065](http://hg.scrapy.org/scrapy/changeset/2065){.reference
    .external} \| #149)

-   Added new scrapy-ctl view command - To view URL in the browser, as
    seen by Scrapy
    ([r2039](http://hg.scrapy.org/scrapy/changeset/2039){.reference
    .external})

-   Added web service for controlling Scrapy process (this also
    deprecates the web console.
    ([r2053](http://hg.scrapy.org/scrapy/changeset/2053){.reference
    .external} \| #167)

-   Support for running Scrapy as a service, for production systems
    ([r1988](http://hg.scrapy.org/scrapy/changeset/1988){.reference
    .external},
    [r2054](http://hg.scrapy.org/scrapy/changeset/2054){.reference
    .external},
    [r2055](http://hg.scrapy.org/scrapy/changeset/2055){.reference
    .external},
    [r2056](http://hg.scrapy.org/scrapy/changeset/2056){.reference
    .external},
    [r2057](http://hg.scrapy.org/scrapy/changeset/2057){.reference
    .external} \| #168)

-   Added wrapper induction library (documentation only available in
    source code for now).
    ([r2011](http://hg.scrapy.org/scrapy/changeset/2011){.reference
    .external})

-   Simplified and improved response encoding support
    ([r1961](http://hg.scrapy.org/scrapy/changeset/1961){.reference
    .external},
    [r1969](http://hg.scrapy.org/scrapy/changeset/1969){.reference
    .external})

-   Added [`LOG_ENCODING`{.docutils .literal .notranslate}]{.pre}
    setting
    ([r1956](http://hg.scrapy.org/scrapy/changeset/1956){.reference
    .external}, documentation available)

-   Added [`RANDOMIZE_DOWNLOAD_DELAY`{.docutils .literal
    .notranslate}]{.pre} setting (enabled by default)
    ([r1923](http://hg.scrapy.org/scrapy/changeset/1923){.reference
    .external}, doc available)

-   [`MailSender`{.docutils .literal .notranslate}]{.pre} is no longer
    IO-blocking
    ([r1955](http://hg.scrapy.org/scrapy/changeset/1955){.reference
    .external} \| #146)

-   Linkextractors and new Crawlspider now handle relative base tag urls
    ([r1960](http://hg.scrapy.org/scrapy/changeset/1960){.reference
    .external} \| #148)

-   Several improvements to Item Loaders and processors
    ([r2022](http://hg.scrapy.org/scrapy/changeset/2022){.reference
    .external},
    [r2023](http://hg.scrapy.org/scrapy/changeset/2023){.reference
    .external},
    [r2024](http://hg.scrapy.org/scrapy/changeset/2024){.reference
    .external},
    [r2025](http://hg.scrapy.org/scrapy/changeset/2025){.reference
    .external},
    [r2026](http://hg.scrapy.org/scrapy/changeset/2026){.reference
    .external},
    [r2027](http://hg.scrapy.org/scrapy/changeset/2027){.reference
    .external},
    [r2028](http://hg.scrapy.org/scrapy/changeset/2028){.reference
    .external},
    [r2029](http://hg.scrapy.org/scrapy/changeset/2029){.reference
    .external},
    [r2030](http://hg.scrapy.org/scrapy/changeset/2030){.reference
    .external})

-   Added support for adding variables to telnet console
    ([r2047](http://hg.scrapy.org/scrapy/changeset/2047){.reference
    .external} \| #165)

-   Support for requests without callbacks
    ([r2050](http://hg.scrapy.org/scrapy/changeset/2050){.reference
    .external} \| #166)
:::

::: {#id136 .section}
##### API changes[¶](#id136 "Permalink to this heading"){.headerlink}

-   Change [`Spider.domain_name`{.docutils .literal .notranslate}]{.pre}
    to [`Spider.name`{.docutils .literal .notranslate}]{.pre} (SEP-012,
    [r1975](http://hg.scrapy.org/scrapy/changeset/1975){.reference
    .external})

-   [`Response.encoding`{.docutils .literal .notranslate}]{.pre} is now
    the detected encoding
    ([r1961](http://hg.scrapy.org/scrapy/changeset/1961){.reference
    .external})

-   [`HttpErrorMiddleware`{.docutils .literal .notranslate}]{.pre} now
    returns None or raises an exception
    ([r2006](http://hg.scrapy.org/scrapy/changeset/2006){.reference
    .external} \| #157)

-   [`scrapy.command`{.docutils .literal .notranslate}]{.pre} modules
    relocation
    ([r2035](http://hg.scrapy.org/scrapy/changeset/2035){.reference
    .external},
    [r2036](http://hg.scrapy.org/scrapy/changeset/2036){.reference
    .external},
    [r2037](http://hg.scrapy.org/scrapy/changeset/2037){.reference
    .external})

-   Added [`ExecutionQueue`{.docutils .literal .notranslate}]{.pre} for
    feeding spiders to scrape
    ([r2034](http://hg.scrapy.org/scrapy/changeset/2034){.reference
    .external})

-   Removed [`ExecutionEngine`{.docutils .literal .notranslate}]{.pre}
    singleton
    ([r2039](http://hg.scrapy.org/scrapy/changeset/2039){.reference
    .external})

-   Ported [`S3ImagesStore`{.docutils .literal .notranslate}]{.pre}
    (images pipeline) to use boto and threads
    ([r2033](http://hg.scrapy.org/scrapy/changeset/2033){.reference
    .external})

-   Moved module: [`scrapy.management.telnet`{.docutils .literal
    .notranslate}]{.pre} to [`scrapy.telnet`{.docutils .literal
    .notranslate}]{.pre}
    ([r2047](http://hg.scrapy.org/scrapy/changeset/2047){.reference
    .external})
:::

::: {#changes-to-default-settings .section}
##### Changes to default settings[¶](#changes-to-default-settings "Permalink to this heading"){.headerlink}

-   Changed default [`SCHEDULER_ORDER`{.docutils .literal
    .notranslate}]{.pre} to [`DFO`{.docutils .literal
    .notranslate}]{.pre}
    ([r1939](http://hg.scrapy.org/scrapy/changeset/1939){.reference
    .external})
:::
:::

::: {#scrapy-0-8 .section}
#### Scrapy 0.8[¶](#scrapy-0-8 "Permalink to this heading"){.headerlink}

The numbers like #NNN reference tickets in the old issue tracker (Trac)
which is no longer available.

::: {#id137 .section}
##### New features[¶](#id137 "Permalink to this heading"){.headerlink}

-   Added DEFAULT_RESPONSE_ENCODING setting
    ([r1809](http://hg.scrapy.org/scrapy/changeset/1809){.reference
    .external})

-   Added [`dont_click`{.docutils .literal .notranslate}]{.pre} argument
    to [`FormRequest.from_response()`{.docutils .literal
    .notranslate}]{.pre} method
    ([r1813](http://hg.scrapy.org/scrapy/changeset/1813){.reference
    .external},
    [r1816](http://hg.scrapy.org/scrapy/changeset/1816){.reference
    .external})

-   Added [`clickdata`{.docutils .literal .notranslate}]{.pre} argument
    to [`FormRequest.from_response()`{.docutils .literal
    .notranslate}]{.pre} method
    ([r1802](http://hg.scrapy.org/scrapy/changeset/1802){.reference
    .external},
    [r1803](http://hg.scrapy.org/scrapy/changeset/1803){.reference
    .external})

-   Added support for HTTP proxies ([`HttpProxyMiddleware`{.docutils
    .literal .notranslate}]{.pre})
    ([r1781](http://hg.scrapy.org/scrapy/changeset/1781){.reference
    .external},
    [r1785](http://hg.scrapy.org/scrapy/changeset/1785){.reference
    .external})

-   Offsite spider middleware now logs messages when filtering out
    requests
    ([r1841](http://hg.scrapy.org/scrapy/changeset/1841){.reference
    .external})
:::

::: {#id138 .section}
##### Backward-incompatible changes[¶](#id138 "Permalink to this heading"){.headerlink}

-   Changed [`scrapy.utils.response.get_meta_refresh()`{.docutils
    .literal .notranslate}]{.pre} signature
    ([r1804](http://hg.scrapy.org/scrapy/changeset/1804){.reference
    .external})

-   Removed deprecated [`scrapy.item.ScrapedItem`{.docutils .literal
    .notranslate}]{.pre} class - use [`scrapy.item.Item`{.docutils
    .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`instead`{.docutils .literal .notranslate}]{.pre}
    ([r1838](http://hg.scrapy.org/scrapy/changeset/1838){.reference
    .external})

-   Removed deprecated [`scrapy.xpath`{.docutils .literal
    .notranslate}]{.pre} module - use [`scrapy.selector`{.docutils
    .literal .notranslate}]{.pre} instead.
    ([r1836](http://hg.scrapy.org/scrapy/changeset/1836){.reference
    .external})

-   Removed deprecated [`core.signals.domain_open`{.docutils .literal
    .notranslate}]{.pre} signal - use
    [`core.signals.domain_opened`{.docutils .literal
    .notranslate}]{.pre} instead
    ([r1822](http://hg.scrapy.org/scrapy/changeset/1822){.reference
    .external})

-   

    [`log.msg()`{.docutils .literal .notranslate}]{.pre} now receives a [`spider`{.docutils .literal .notranslate}]{.pre} argument ([r1822](http://hg.scrapy.org/scrapy/changeset/1822){.reference .external})

    :   -   Old domain argument has been deprecated and will be removed
            in 0.9. For spiders, you should always use the
            [`spider`{.docutils .literal .notranslate}]{.pre} argument
            and pass spider references. If you really want to pass a
            string, use the [`component`{.docutils .literal
            .notranslate}]{.pre} argument instead.

-   Changed core signals [`domain_opened`{.docutils .literal
    .notranslate}]{.pre}, [`domain_closed`{.docutils .literal
    .notranslate}]{.pre}, [`domain_idle`{.docutils .literal
    .notranslate}]{.pre}

-   

    Changed Item pipeline to use spiders instead of domains

    :   -   The [`domain`{.docutils .literal .notranslate}]{.pre}
            argument of [`process_item()`{.docutils .literal
            .notranslate}]{.pre} item pipeline method was changed to
            [`spider`{.docutils .literal .notranslate}]{.pre}, the new
            signature is: [`process_item(spider,`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`item)`{.docutils .literal
            .notranslate}]{.pre}
            ([r1827](http://hg.scrapy.org/scrapy/changeset/1827){.reference
            .external} \| #105)

        -   To quickly port your code (to work with Scrapy 0.8) just use
            [`spider.domain_name`{.docutils .literal
            .notranslate}]{.pre} where you previously used
            [`domain`{.docutils .literal .notranslate}]{.pre}.

-   

    Changed Stats API to use spiders instead of domains ([r1849](http://hg.scrapy.org/scrapy/changeset/1849){.reference .external} \| #113)

    :   -   [`StatsCollector`{.docutils .literal .notranslate}]{.pre}
            was changed to receive spider references (instead of
            domains) in its methods ([`set_value`{.docutils .literal
            .notranslate}]{.pre}, [`inc_value`{.docutils .literal
            .notranslate}]{.pre}, etc).

        -   added [`StatsCollector.iter_spider_stats()`{.docutils
            .literal .notranslate}]{.pre} method

        -   removed [`StatsCollector.list_domains()`{.docutils .literal
            .notranslate}]{.pre} method

        -   Also, Stats signals were renamed and now pass around spider
            references (instead of domains). Here's a summary of the
            changes:

        -   To quickly port your code (to work with Scrapy 0.8) just use
            [`spider.domain_name`{.docutils .literal
            .notranslate}]{.pre} where you previously used
            [`domain`{.docutils .literal .notranslate}]{.pre}.
            [`spider_stats`{.docutils .literal .notranslate}]{.pre}
            contains exactly the same data as [`domain_stats`{.docutils
            .literal .notranslate}]{.pre}.

-   

    [`CloseDomain`{.docutils .literal .notranslate}]{.pre} extension moved to [`scrapy.contrib.closespider.CloseSpider`{.docutils .literal .notranslate}]{.pre} ([r1833](http://hg.scrapy.org/scrapy/changeset/1833){.reference .external})

    :   -   

            Its settings were also renamed:

            :   -   [`CLOSEDOMAIN_TIMEOUT`{.docutils .literal
                    .notranslate}]{.pre} to
                    [`CLOSESPIDER_TIMEOUT`{.docutils .literal
                    .notranslate}]{.pre}

                -   [`CLOSEDOMAIN_ITEMCOUNT`{.docutils .literal
                    .notranslate}]{.pre} to
                    [`CLOSESPIDER_ITEMCOUNT`{.docutils .literal
                    .notranslate}]{.pre}

-   Removed deprecated [`SCRAPYSETTINGS_MODULE`{.docutils .literal
    .notranslate}]{.pre} environment variable - use
    [`SCRAPY_SETTINGS_MODULE`{.docutils .literal .notranslate}]{.pre}
    instead
    ([r1840](http://hg.scrapy.org/scrapy/changeset/1840){.reference
    .external})

-   Renamed setting: [`REQUESTS_PER_DOMAIN`{.docutils .literal
    .notranslate}]{.pre} to [`CONCURRENT_REQUESTS_PER_SPIDER`{.docutils
    .literal .notranslate}]{.pre}
    ([r1830](http://hg.scrapy.org/scrapy/changeset/1830){.reference
    .external},
    [r1844](http://hg.scrapy.org/scrapy/changeset/1844){.reference
    .external})

-   Renamed setting: [`CONCURRENT_DOMAINS`{.docutils .literal
    .notranslate}]{.pre} to [`CONCURRENT_SPIDERS`{.docutils .literal
    .notranslate}]{.pre}
    ([r1830](http://hg.scrapy.org/scrapy/changeset/1830){.reference
    .external})

-   Refactored HTTP Cache middleware

-   HTTP Cache middleware has been heavily refactored, retaining the
    same functionality except for the domain sectorization which was
    removed.
    ([r1843](http://hg.scrapy.org/scrapy/changeset/1843){.reference
    .external} )

-   Renamed exception: [`DontCloseDomain`{.docutils .literal
    .notranslate}]{.pre} to [`DontCloseSpider`{.docutils .literal
    .notranslate}]{.pre}
    ([r1859](http://hg.scrapy.org/scrapy/changeset/1859){.reference
    .external} \| #120)

-   Renamed extension: [`DelayedCloseDomain`{.docutils .literal
    .notranslate}]{.pre} to [`SpiderCloseDelay`{.docutils .literal
    .notranslate}]{.pre}
    ([r1861](http://hg.scrapy.org/scrapy/changeset/1861){.reference
    .external} \| #121)

-   Removed obsolete
    [`scrapy.utils.markup.remove_escape_chars`{.docutils .literal
    .notranslate}]{.pre} function - use
    [`scrapy.utils.markup.replace_escape_chars`{.docutils .literal
    .notranslate}]{.pre} instead
    ([r1865](http://hg.scrapy.org/scrapy/changeset/1865){.reference
    .external})
:::
:::

::: {#scrapy-0-7 .section}
#### Scrapy 0.7[¶](#scrapy-0-7 "Permalink to this heading"){.headerlink}

First release of Scrapy.
:::
:::

[]{#document-contributing}

::: {#contributing-to-scrapy .section}
[]{#topics-contributing}

### Contributing to Scrapy[¶](#contributing-to-scrapy "Permalink to this heading"){.headerlink}

::: {.admonition .important}
Important

Double check that you are reading the most recent version of this
document at
[https://docs.scrapy.org/en/master/contributing.html](https://docs.scrapy.org/en/master/contributing.html){.reference
.external}
:::

There are many ways to contribute to Scrapy. Here are some of them:

-   Report bugs and request features in the [issue
    tracker](https://github.com/scrapy/scrapy/issues){.reference
    .external}, trying to follow the guidelines detailed in [Reporting
    bugs](#reporting-bugs){.reference .internal} below.

-   Submit patches for new functionalities and/or bug fixes. Please read
    [[Writing patches]{.std .std-ref}](#writing-patches){.hoverxref
    .tooltip .reference .internal} and [Submitting
    patches](#id2){.reference .internal} below for details on how to
    write and submit a patch.

-   Blog about Scrapy. Tell the world how you're using Scrapy. This will
    help newcomers with more examples and will help the Scrapy project
    to increase its visibility.

-   Join the [Scrapy subreddit](https://reddit.com/r/scrapy){.reference
    .external} and share your ideas on how to improve Scrapy. We're
    always open to suggestions.

-   Answer Scrapy questions at [Stack
    Overflow](https://stackoverflow.com/questions/tagged/scrapy){.reference
    .external}.

::: {#reporting-bugs .section}
#### Reporting bugs[¶](#reporting-bugs "Permalink to this heading"){.headerlink}

::: {.admonition .note}
Note

Please report security issues **only** to
[scrapy-security@googlegroups.com](mailto:scrapy-security%40googlegroups.com){.reference
.external}. This is a private list only open to trusted Scrapy
developers, and its archives are not public.
:::

Well-written bug reports are very helpful, so keep in mind the following
guidelines when you're going to report a new bug.

-   check the [[FAQ]{.std .std-ref}](index.html#faq){.hoverxref .tooltip
    .reference .internal} first to see if your issue is addressed in a
    well-known question

-   if you have a general question about Scrapy usage, please ask it at
    [Stack
    Overflow](https://stackoverflow.com/questions/tagged/scrapy){.reference
    .external} (use "scrapy" tag).

-   check the [open
    issues](https://github.com/scrapy/scrapy/issues){.reference
    .external} to see if the issue has already been reported. If it has,
    don't dismiss the report, but check the ticket history and comments.
    If you have additional useful information, please leave a comment,
    or consider [[sending a pull request]{.std
    .std-ref}](#writing-patches){.hoverxref .tooltip .reference
    .internal} with a fix.

-   search the
    [scrapy-users](https://groups.google.com/forum/#!forum/scrapy-users){.reference
    .external} list and [Scrapy
    subreddit](https://reddit.com/r/scrapy){.reference .external} to see
    if it has been discussed there, or if you're not sure if what you're
    seeing is a bug. You can also ask in the [`#scrapy`{.docutils
    .literal .notranslate}]{.pre} IRC channel.

-   write **complete, reproducible, specific bug reports**. The smaller
    the test case, the better. Remember that other developers won't have
    your project to reproduce the bug, so please include all relevant
    files required to reproduce it. See for example StackOverflow's
    guide on creating a [Minimal, Complete, and Verifiable
    example](https://stackoverflow.com/help/mcve){.reference .external}
    exhibiting the issue.

-   the most awesome way to provide a complete reproducible example is
    to send a pull request which adds a failing test case to the Scrapy
    testing suite (see [[Submitting patches]{.std
    .std-ref}](#submitting-patches){.hoverxref .tooltip .reference
    .internal}). This is helpful even if you don't have an intention to
    fix the issue yourselves.

-   include the output of [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`version`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`-v`{.docutils .literal .notranslate}]{.pre} so
    developers working on your bug know exactly which version and
    platform it occurred on, which is often very helpful for reproducing
    it, or knowing if it was already fixed.
:::

::: {#writing-patches .section}
[]{#id1}

#### Writing patches[¶](#writing-patches "Permalink to this heading"){.headerlink}

Scrapy has a list of [good first
issues](https://github.com/scrapy/scrapy/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22){.reference
.external} and [help wanted
issues](https://github.com/scrapy/scrapy/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22){.reference
.external} that you can work on. These issues are a great way to get
started with contributing to Scrapy. If you're new to the codebase, you
may want to focus on documentation or testing-related issues, as they
are always useful and can help you get more familiar with the project.
You can also check Scrapy's [test
coverage](https://app.codecov.io/gh/scrapy/scrapy){.reference .external}
to see which areas may benefit from more tests.

The better a patch is written, the higher the chances that it'll get
accepted and the sooner it will be merged.

Well-written patches should:

-   contain the minimum amount of code required for the specific change.
    Small patches are easier to review and merge. So, if you're doing
    more than one change (or bug fix), please consider submitting one
    patch per change. Do not collapse multiple changes into a single
    patch. For big changes consider using a patch queue.

-   pass all unit-tests. See [Running tests](#id6){.reference .internal}
    below.

-   include one (or more) test cases that check the bug fixed or the new
    functionality added. See [Writing tests](#writing-tests){.reference
    .internal} below.

-   if you're adding or changing a public (documented) API, please
    include the documentation changes in the same patch. See
    [Documentation policies](#id5){.reference .internal} below.

-   if you're adding a private API, please add a regular expression to
    the [`coverage_ignore_pyobjects`{.docutils .literal
    .notranslate}]{.pre} variable of [`docs/conf.py`{.docutils .literal
    .notranslate}]{.pre} to exclude the new private API from
    documentation coverage checks.

    To see if your private API is skipped properly, generate a
    documentation coverage report as follows:

    ::: {.highlight-default .notranslate}
    ::: highlight
        tox -e docs-coverage
    :::
    :::

-   if you are removing deprecated code, first make sure that at least 1
    year (12 months) has passed since the release that introduced the
    deprecation. See [[Deprecation policy]{.std
    .std-ref}](index.html#deprecation-policy){.hoverxref .tooltip
    .reference .internal}.
:::

::: {#submitting-patches .section}
[]{#id2}

#### Submitting patches[¶](#submitting-patches "Permalink to this heading"){.headerlink}

The best way to submit a patch is to issue a [pull
request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request){.reference
.external} on GitHub, optionally creating a new issue first.

Remember to explain what was fixed or the new functionality (what it is,
why it's needed, etc). The more info you include, the easier will be for
core developers to understand and accept your patch.

You can also discuss the new functionality (or bug fix) before creating
the patch, but it's always good to have a patch ready to illustrate your
arguments and show that you have put some additional thought into the
subject. A good starting point is to send a pull request on GitHub. It
can be simple enough to illustrate your idea, and leave
documentation/tests for later, after the idea has been validated and
proven useful. Alternatively, you can start a conversation in the
[Scrapy subreddit](https://reddit.com/r/scrapy){.reference .external} to
discuss your idea first.

Sometimes there is an existing pull request for the problem you'd like
to solve, which is stalled for some reason. Often the pull request is in
a right direction, but changes are requested by Scrapy maintainers, and
the original pull request author hasn't had time to address them. In
this case consider picking up this pull request: open a new pull request
with all commits from the original pull request, as well as additional
changes to address the raised issues. Doing so helps a lot; it is not
considered rude as long as the original author is acknowledged by
keeping his/her commits.

You can pull an existing pull request to a local branch by running
[`git`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`fetch`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`upstream`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`pull/$PR_NUMBER/head:$BRANCH_NAME_TO_CREATE`{.docutils
.literal .notranslate}]{.pre} (replace 'upstream' with a remote name for
scrapy repository, [`$PR_NUMBER`{.docutils .literal .notranslate}]{.pre}
with an ID of the pull request, and [`$BRANCH_NAME_TO_CREATE`{.docutils
.literal .notranslate}]{.pre} with a name of the branch you want to
create locally). See also:
[https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/checking-out-pull-requests-locally#modifying-an-inactive-pull-request-locally](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/checking-out-pull-requests-locally#modifying-an-inactive-pull-request-locally){.reference
.external}.

When writing GitHub pull requests, try to keep titles short but
descriptive. E.g. For bug #411: "Scrapy hangs if an exception raises in
start_requests" prefer "Fix hanging when exception occurs in
start_requests (#411)" instead of "Fix for #411". Complete titles make
it easy to skim through the issue tracker.

Finally, try to keep aesthetic changes ([]{#index-0 .target}[**PEP
8**](https://peps.python.org/pep-0008/){.pep .reference .external}
compliance, unused imports removal, etc) in separate commits from
functional changes. This will make pull requests easier to review and
more likely to get merged.
:::

::: {#coding-style .section}
[]{#id3}

#### Coding style[¶](#coding-style "Permalink to this heading"){.headerlink}

Please follow these coding conventions when writing code for inclusion
in Scrapy:

-   We use [black](https://black.readthedocs.io/en/stable/){.reference
    .external} for code formatting. There is a hook in the pre-commit
    config that will automatically format your code before every commit.
    You can also run black manually with [`tox`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`-e`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`black`{.docutils .literal .notranslate}]{.pre}.

-   Don't put your name in the code you contribute; git provides enough
    metadata to identify author of the code. See
    [https://help.github.com/en/github/using-git/setting-your-username-in-git](https://help.github.com/en/github/using-git/setting-your-username-in-git){.reference
    .external} for setup instructions.
:::

::: {#pre-commit .section}
[]{#scrapy-pre-commit}

#### Pre-commit[¶](#pre-commit "Permalink to this heading"){.headerlink}

We use [pre-commit](https://pre-commit.com/){.reference .external} to
automatically address simple code issues before every commit.

After your create a local clone of your fork of the Scrapy repository:

1.  [Install
    pre-commit](https://pre-commit.com/#installation){.reference
    .external}.

2.  On the root of your local clone of the Scrapy repository, run the
    following command:

    ::: {.highlight-bash .notranslate}
    ::: highlight
        pre-commit install
    :::
    :::

Now pre-commit will check your changes every time you create a Git
commit. Upon finding issues, pre-commit aborts your commit, and either
fixes those issues automatically, or only reports them to you. If it
fixes those issues automatically, creating your commit again should
succeed. Otherwise, you may need to address the corresponding issues
manually first.
:::

::: {#documentation-policies .section}
[]{#id5}

#### Documentation policies[¶](#documentation-policies "Permalink to this heading"){.headerlink}

For reference documentation of API members (classes, methods, etc.) use
docstrings and make sure that the Sphinx documentation uses the
[[`autodoc`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html#module-sphinx.ext.autodoc "(in Sphinx v7.3.0)"){.reference
.external} extension to pull the docstrings. API reference documentation
should follow docstring conventions ([PEP
257](https://www.python.org/dev/peps/pep-0257/){.reference .external})
and be IDE-friendly: short, to the point, and it may provide short
examples.

Other types of documentation, such as tutorials or topics, should be
covered in files within the [`docs/`{.docutils .literal
.notranslate}]{.pre} directory. This includes documentation that is
specific to an API member, but goes beyond API reference documentation.

In any case, if something is covered in a docstring, use the
[[`autodoc`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html#module-sphinx.ext.autodoc "(in Sphinx v7.3.0)"){.reference
.external} extension to pull the docstring into the documentation
instead of duplicating the docstring in files within the
[`docs/`{.docutils .literal .notranslate}]{.pre} directory.

Documentation updates that cover new or modified features must use
Sphinx's [[`versionadded`{.xref .rst .rst-dir .docutils .literal
.notranslate}]{.pre}](https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#directive-versionadded "(in Sphinx v7.3.0)"){.reference
.external} and [[`versionchanged`{.xref .rst .rst-dir .docutils .literal
.notranslate}]{.pre}](https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#directive-versionchanged "(in Sphinx v7.3.0)"){.reference
.external} directives. Use [`VERSION`{.docutils .literal
.notranslate}]{.pre} as version, we will replace it with the actual
version right before the corresponding release. When we release a new
major or minor version of Scrapy, we remove these directives if they are
older than 3 years.

Documentation about deprecated features must be removed as those
features are deprecated, so that new readers do not run into it. New
deprecations and deprecation removals are documented in the [[release
notes]{.std .std-ref}](index.html#news){.hoverxref .tooltip .reference
.internal}.
:::

::: {#tests .section}
#### Tests[¶](#tests "Permalink to this heading"){.headerlink}

Tests are implemented using the [[Twisted unit-testing framework]{.xref
.std
.std-doc}](https://docs.twisted.org/en/stable/development/test-standard.html "(in Twisted v23.10)"){.reference
.external}. Running tests requires [[tox]{.xref .std
.std-doc}](https://tox.wiki/en/latest/index.html "(in Python v4.11)"){.reference
.external}.

::: {#running-tests .section}
[]{#id6}

##### Running tests[¶](#running-tests "Permalink to this heading"){.headerlink}

To run all tests:

::: {.highlight-default .notranslate}
::: highlight
    tox
:::
:::

To run a specific test (say [`tests/test_loader.py`{.docutils .literal
.notranslate}]{.pre}) use:

> <div>
>
> [`tox`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
> .notranslate}[`--`{.docutils .literal
> .notranslate}]{.pre}` `{.docutils .literal
> .notranslate}[`tests/test_loader.py`{.docutils .literal
> .notranslate}]{.pre}
>
> </div>

To run the tests on a specific [[tox]{.xref .std
.std-doc}](https://tox.wiki/en/latest/index.html "(in Python v4.11)"){.reference
.external} environment, use [`-e`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`<name>`{.docutils .literal .notranslate}]{.pre} with an
environment name from [`tox.ini`{.docutils .literal
.notranslate}]{.pre}. For example, to run the tests with Python 3.10
use:

::: {.highlight-default .notranslate}
::: highlight
    tox -e py310
:::
:::

You can also specify a comma-separated list of environments, and use
[[tox's parallel mode]{.xref .std
.std-ref}](https://tox.wiki/en/latest/user_guide.html#parallel-mode "(in Python v4.11)"){.reference
.external} to run the tests on multiple environments in parallel:

::: {.highlight-default .notranslate}
::: highlight
    tox -e py39,py310 -p auto
:::
:::

To pass command-line options to [[pytest]{.xref .std
.std-doc}](https://docs.pytest.org/en/latest/index.html "(in pytest v0.1.dev83+g81c06b3)"){.reference
.external}, add them after [`--`{.docutils .literal .notranslate}]{.pre}
in your call to [[tox]{.xref .std
.std-doc}](https://tox.wiki/en/latest/index.html "(in Python v4.11)"){.reference
.external}. Using [`--`{.docutils .literal .notranslate}]{.pre}
overrides the default positional arguments defined in
[`tox.ini`{.docutils .literal .notranslate}]{.pre}, so you must include
those default positional arguments ([`scrapy`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`tests`{.docutils .literal .notranslate}]{.pre}) after
[`--`{.docutils .literal .notranslate}]{.pre} as well:

::: {.highlight-default .notranslate}
::: highlight
    tox -- scrapy tests -x  # stop after first failure
:::
:::

You can also use the
[pytest-xdist](https://github.com/pytest-dev/pytest-xdist){.reference
.external} plugin. For example, to run all tests on the Python 3.10
[[tox]{.xref .std
.std-doc}](https://tox.wiki/en/latest/index.html "(in Python v4.11)"){.reference
.external} environment using all your CPU cores:

::: {.highlight-default .notranslate}
::: highlight
    tox -e py310 -- scrapy tests -n auto
:::
:::

To see coverage report install [[coverage]{.xref .std
.std-doc}](https://coverage.readthedocs.io/en/latest/index.html "(in Coverage.py v7.3.2)"){.reference
.external} ([`pip`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`install`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`coverage`{.docutils .literal .notranslate}]{.pre}) and
run:

> <div>
>
> [`coverage`{.docutils .literal .notranslate}]{.pre}` `{.docutils
> .literal .notranslate}[`report`{.docutils .literal
> .notranslate}]{.pre}
>
> </div>

see output of [`coverage`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`--help`{.docutils .literal .notranslate}]{.pre} for more
options like html or xml report.
:::

::: {#writing-tests .section}
##### Writing tests[¶](#writing-tests "Permalink to this heading"){.headerlink}

All functionality (including new features and bug fixes) must include a
test case to check that it works as expected, so please include tests
for your patches if you want them to get accepted sooner.

Scrapy uses unit-tests, which are located in the
[tests/](https://github.com/scrapy/scrapy/tree/master/tests){.reference
.external} directory. Their module name typically resembles the full
path of the module they're testing. For example, the item loaders code
is in:

::: {.highlight-default .notranslate}
::: highlight
    scrapy.loader
:::
:::

And their unit-tests are in:

::: {.highlight-default .notranslate}
::: highlight
    tests/test_loader.py
:::
:::
:::
:::
:::

[]{#document-versioning}

::: {#versioning-and-api-stability .section}
[]{#versioning}

### Versioning and API stability[¶](#versioning-and-api-stability "Permalink to this heading"){.headerlink}

::: {#id1 .section}
#### Versioning[¶](#id1 "Permalink to this heading"){.headerlink}

There are 3 numbers in a Scrapy version: *A.B.C*

-   *A* is the major version. This will rarely change and will signify
    very large changes.

-   *B* is the release number. This will include many changes including
    features and things that possibly break backward compatibility,
    although we strive to keep these cases at a minimum.

-   *C* is the bugfix release number.

Backward-incompatibilities are explicitly mentioned in the [[release
notes]{.std .std-ref}](index.html#news){.hoverxref .tooltip .reference
.internal}, and may require special attention before upgrading.

Development releases do not follow 3-numbers version and are generally
released as [`dev`{.docutils .literal .notranslate}]{.pre} suffixed
versions, e.g. [`1.3dev`{.docutils .literal .notranslate}]{.pre}.

::: {.admonition .note}
Note

With Scrapy 0.\* series, Scrapy used [odd-numbered versions for
development
releases](https://en.wikipedia.org/wiki/Software_versioning#Odd-numbered_versions_for_development_releases){.reference
.external}. This is not the case anymore from Scrapy 1.0 onwards.

Starting with Scrapy 1.0, all releases should be considered
production-ready.
:::

For example:

-   *1.1.1* is the first bugfix release of the *1.1* series (safe to use
    in production)
:::

::: {#api-stability .section}
#### API stability[¶](#api-stability "Permalink to this heading"){.headerlink}

API stability was one of the major goals for the *1.0* release.

Methods or functions that start with a single dash ([`_`{.docutils
.literal .notranslate}]{.pre}) are private and should never be relied as
stable.

Also, keep in mind that stable doesn't mean complete: stable APIs could
grow new methods or functionality but the existing methods should keep
working the same way.
:::

::: {#deprecation-policy .section}
[]{#id2}

#### Deprecation policy[¶](#deprecation-policy "Permalink to this heading"){.headerlink}

We aim to maintain support for deprecated Scrapy features for at least 1
year.

For example, if a feature is deprecated in a Scrapy version released on
June 15th 2020, that feature should continue to work in versions
released on June 14th 2021 or before that.

Any new Scrapy release after a year *may* remove support for that
deprecated feature.

All deprecated features removed in a Scrapy release are explicitly
mentioned in the [[release notes]{.std
.std-ref}](index.html#news){.hoverxref .tooltip .reference .internal}.
:::
:::
:::

[[Release notes]{.doc}](index.html#document-news){.reference .internal}

:   See what has changed in recent Scrapy versions.

[[Contributing to Scrapy]{.doc}](index.html#document-contributing){.reference .internal}

:   Learn how to contribute to the Scrapy project.

[[Versioning and API stability]{.doc}](index.html#document-versioning){.reference .internal}

:   Understand Scrapy versioning and API stability.
:::
:::
:::
:::

------------------------------------------------------------------------

::: {role="contentinfo"}
© Copyright 2008--2023, Scrapy developers. [Revision `70ba3a08`.
]{.commit} [Last updated on Nov 30, 2023. ]{.lastupdated}
:::

Built with [Sphinx](https://www.sphinx-doc.org/) using a
[theme](https://github.com/readthedocs/sphinx_rtd_theme) provided by
[Read the Docs](https://readthedocs.org).
:::
:::
:::
:::

::: {.rst-versions toggle="rst-versions" role="note" aria-label="Versions"}
[ [ Read the Docs]{.fa .fa-book} v: master []{.fa .fa-caret-down}
]{.rst-current-version toggle="rst-current-version"}

::: rst-other-versions

Versions
:   [master](/en/master/)
:   [latest](/en/latest/)
:   [stable](/en/stable/)
:   [2.11](/en/2.11/)
:   [2.10](/en/2.10/)
:   [2.9](/en/2.9/)
:   [2.8](/en/2.8/)
:   [2.7](/en/2.7/)
:   [2.6](/en/2.6/)
:   [2.5](/en/2.5/)
:   [2.4](/en/2.4/)
:   [2.3](/en/2.3/)
:   [2.2](/en/2.2/)
:   [2.1](/en/2.1/)
:   [2.0](/en/2.0/)
:   [1.8](/en/1.8/)
:   [1.7](/en/1.7/)
:   [1.6](/en/1.6/)
:   [1.5](/en/1.5/)
:   [1.4](/en/1.4/)
:   [1.3](/en/1.3/)
:   [1.2](/en/1.2/)
:   [1.1](/en/1.1/)
:   [1.0](/en/1.0/)
:   [0.24](/en/0.24/)
:   [0.22](/en/0.22/)
:   [0.20](/en/0.20/)
:   [0.18](/en/0.18/)
:   [0.16](/en/0.16/)
:   [0.14](/en/0.14/)
:   [0.12](/en/0.12/)
:   [0.10.3](/en/0.10.3/)
:   [0.9](/en/0.9/)
:   [xpath-tutorial](/en/xpath-tutorial/)

```{=html}
<!-- -->
```

Downloads
:   [pdf](//docs.scrapy.org/_/downloads/en/master/pdf/)
:   [html](//docs.scrapy.org/_/downloads/en/master/htmlzip/)
:   [epub](//docs.scrapy.org/_/downloads/en/master/epub/)

```{=html}
<!-- -->
```

On Read the Docs
:   [Project Home](//readthedocs.org/projects/scrapy/?fromdocs=scrapy)
:   [Builds](//readthedocs.org/builds/scrapy/?fromdocs=scrapy)
:::
:::
