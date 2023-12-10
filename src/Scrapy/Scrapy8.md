    .external}).

-   An exception is now raised if [[`ASYNCIO_EVENT_LOOP`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ASYNCIO_EVENT_LOOP){.hoverxref
    .tooltip .reference .internal} has a value that does not match the
    asyncio event loop actually installed ([issue
    5529](https://github.com/scrapy/scrapy/issues/5529){.reference
    .external}).

-   Fixed [`Headers.getlist`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} returning only the last header ([issue
    5515](https://github.com/scrapy/scrapy/issues/5515){.reference
    .external}, [issue
    5526](https://github.com/scrapy/scrapy/issues/5526){.reference
    .external}).

-   Fixed [[`LinkExtractor`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} not ignoring the [`tar.gz`{.docutils .literal
    .notranslate}]{.pre} file extension by default ([issue
    1837](https://github.com/scrapy/scrapy/issues/1837){.reference
    .external}, [issue
    2067](https://github.com/scrapy/scrapy/issues/2067){.reference
    .external}, [issue
    4066](https://github.com/scrapy/scrapy/issues/4066){.reference
    .external})
:::

::: {#id27 .section}
##### Documentation[¶](#id27 "Permalink to this heading"){.headerlink}

-   Clarified the return type of [[`Spider.parse`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
    .internal} ([issue
    5602](https://github.com/scrapy/scrapy/issues/5602){.reference
    .external}, [issue
    5608](https://github.com/scrapy/scrapy/issues/5608){.reference
    .external}).

-   To enable [[`HttpCompressionMiddleware`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware "scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware"){.reference
    .internal} to do [brotli
    compression](https://www.ietf.org/rfc/rfc7932.txt){.reference
    .external}, installing
    [brotli](https://github.com/google/brotli){.reference .external} is
    now recommended instead of installing
    [brotlipy](https://github.com/python-hyper/brotlipy/){.reference
    .external}, as the former provides a more recent version of brotli.

-   [[Signal documentation]{.std
    .std-ref}](index.html#topics-signals){.hoverxref .tooltip .reference
    .internal} now mentions [[coroutine support]{.std
    .std-ref}](index.html#topics-coroutines){.hoverxref .tooltip
    .reference .internal} and uses it in code examples ([issue
    4852](https://github.com/scrapy/scrapy/issues/4852){.reference
    .external}, [issue
    5358](https://github.com/scrapy/scrapy/issues/5358){.reference
    .external}).

-   [[Avoiding getting banned]{.std
    .std-ref}](index.html#bans){.hoverxref .tooltip .reference
    .internal} now recommends [Common
    Crawl](https://commoncrawl.org/){.reference .external} instead of
    [Google
    cache](http://www.googleguide.com/cached_pages.html){.reference
    .external} ([issue
    3582](https://github.com/scrapy/scrapy/issues/3582){.reference
    .external}, [issue
    5432](https://github.com/scrapy/scrapy/issues/5432){.reference
    .external}).

-   The new [[Components]{.std
    .std-ref}](index.html#topics-components){.hoverxref .tooltip
    .reference .internal} topic covers enforcing requirements on Scrapy
    components, like [[downloader middlewares]{.std
    .std-ref}](index.html#topics-downloader-middleware){.hoverxref
    .tooltip .reference .internal}, [[extensions]{.std
    .std-ref}](index.html#topics-extensions){.hoverxref .tooltip
    .reference .internal}, [[item pipelines]{.std
    .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
    .reference .internal}, [[spider middlewares]{.std
    .std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
    .reference .internal}, and more; [[Enforcing asyncio as a
    requirement]{.std
    .std-ref}](index.html#enforce-asyncio-requirement){.hoverxref
    .tooltip .reference .internal} has also been added ([issue
    4978](https://github.com/scrapy/scrapy/issues/4978){.reference
    .external}).

-   [[Settings]{.std .std-ref}](index.html#topics-settings){.hoverxref
    .tooltip .reference .internal} now indicates that setting values
    must be [[picklable]{.xref .std
    .std-ref}](https://docs.python.org/3/library/pickle.html#pickle-picklable "(in Python v3.12)"){.reference
    .external} ([issue
    5607](https://github.com/scrapy/scrapy/issues/5607){.reference
    .external}, [issue
    5629](https://github.com/scrapy/scrapy/issues/5629){.reference
    .external}).

-   Removed outdated documentation ([issue
    5446](https://github.com/scrapy/scrapy/issues/5446){.reference
    .external}, [issue
    5373](https://github.com/scrapy/scrapy/issues/5373){.reference
    .external}, [issue
    5369](https://github.com/scrapy/scrapy/issues/5369){.reference
    .external}, [issue
    5370](https://github.com/scrapy/scrapy/issues/5370){.reference
    .external}, [issue
    5554](https://github.com/scrapy/scrapy/issues/5554){.reference
    .external}).

-   Fixed typos ([issue
    5442](https://github.com/scrapy/scrapy/issues/5442){.reference
    .external}, [issue
    5455](https://github.com/scrapy/scrapy/issues/5455){.reference
    .external}, [issue
    5457](https://github.com/scrapy/scrapy/issues/5457){.reference
    .external}, [issue
    5461](https://github.com/scrapy/scrapy/issues/5461){.reference
    .external}, [issue
    5538](https://github.com/scrapy/scrapy/issues/5538){.reference
    .external}, [issue
    5553](https://github.com/scrapy/scrapy/issues/5553){.reference
    .external}, [issue
    5558](https://github.com/scrapy/scrapy/issues/5558){.reference
    .external}, [issue
    5624](https://github.com/scrapy/scrapy/issues/5624){.reference
    .external}, [issue
    5631](https://github.com/scrapy/scrapy/issues/5631){.reference
    .external}).

-   Fixed other issues ([issue
    5283](https://github.com/scrapy/scrapy/issues/5283){.reference
    .external}, [issue
    5284](https://github.com/scrapy/scrapy/issues/5284){.reference
    .external}, [issue
    5559](https://github.com/scrapy/scrapy/issues/5559){.reference
    .external}, [issue
    5567](https://github.com/scrapy/scrapy/issues/5567){.reference
    .external}, [issue
    5648](https://github.com/scrapy/scrapy/issues/5648){.reference
    .external}, [issue
    5659](https://github.com/scrapy/scrapy/issues/5659){.reference
    .external}, [issue
    5665](https://github.com/scrapy/scrapy/issues/5665){.reference
    .external}).
:::

::: {#id28 .section}
##### Quality assurance[¶](#id28 "Permalink to this heading"){.headerlink}

-   Added a continuous integration job to run [twine
    check](https://twine.readthedocs.io/en/stable/#twine-check){.reference
    .external} ([issue
    5655](https://github.com/scrapy/scrapy/issues/5655){.reference
    .external}, [issue
    5656](https://github.com/scrapy/scrapy/issues/5656){.reference
    .external}).

-   Addressed test issues and warnings ([issue
    5560](https://github.com/scrapy/scrapy/issues/5560){.reference
    .external}, [issue
    5561](https://github.com/scrapy/scrapy/issues/5561){.reference
    .external}, [issue
    5612](https://github.com/scrapy/scrapy/issues/5612){.reference
    .external}, [issue
    5617](https://github.com/scrapy/scrapy/issues/5617){.reference
    .external}, [issue
    5639](https://github.com/scrapy/scrapy/issues/5639){.reference
    .external}, [issue
    5645](https://github.com/scrapy/scrapy/issues/5645){.reference
    .external}, [issue
    5662](https://github.com/scrapy/scrapy/issues/5662){.reference
    .external}, [issue
    5671](https://github.com/scrapy/scrapy/issues/5671){.reference
    .external}, [issue
    5675](https://github.com/scrapy/scrapy/issues/5675){.reference
    .external}).

-   Cleaned up code ([issue
    4991](https://github.com/scrapy/scrapy/issues/4991){.reference
    .external}, [issue
    4995](https://github.com/scrapy/scrapy/issues/4995){.reference
    .external}, [issue
    5451](https://github.com/scrapy/scrapy/issues/5451){.reference
    .external}, [issue
    5487](https://github.com/scrapy/scrapy/issues/5487){.reference
    .external}, [issue
    5542](https://github.com/scrapy/scrapy/issues/5542){.reference
    .external}, [issue
    5667](https://github.com/scrapy/scrapy/issues/5667){.reference
    .external}, [issue
    5668](https://github.com/scrapy/scrapy/issues/5668){.reference
    .external}, [issue
    5672](https://github.com/scrapy/scrapy/issues/5672){.reference
    .external}).

-   Applied minor code improvements ([issue
    5661](https://github.com/scrapy/scrapy/issues/5661){.reference
    .external}).
:::
:::

::: {#scrapy-2-6-3-2022-09-27 .section}
[]{#release-2-6-3}

#### Scrapy 2.6.3 (2022-09-27)[¶](#scrapy-2-6-3-2022-09-27 "Permalink to this heading"){.headerlink}

-   Added support for
    [pyOpenSSL](https://www.pyopenssl.org/en/stable/){.reference
    .external} 22.1.0, removing support for SSLv3 ([issue
    5634](https://github.com/scrapy/scrapy/issues/5634){.reference
    .external}, [issue
    5635](https://github.com/scrapy/scrapy/issues/5635){.reference
    .external}, [issue
    5636](https://github.com/scrapy/scrapy/issues/5636){.reference
    .external}).

-   Upgraded the minimum versions of the following dependencies:

    -   [cryptography](https://cryptography.io/en/latest/){.reference
        .external}: 2.0 → 3.3

    -   [pyOpenSSL](https://www.pyopenssl.org/en/stable/){.reference
        .external}: 16.2.0 → 21.0.0

    -   [service_identity](https://service-identity.readthedocs.io/en/stable/){.reference
        .external}: 16.0.0 → 18.1.0

    -   [Twisted](https://twistedmatrix.com/trac/){.reference
        .external}: 17.9.0 → 18.9.0

    -   [zope.interface](https://zopeinterface.readthedocs.io/en/latest/){.reference
        .external}: 4.1.3 → 5.0.0

    ([issue
    5621](https://github.com/scrapy/scrapy/issues/5621){.reference
    .external}, [issue
    5632](https://github.com/scrapy/scrapy/issues/5632){.reference
    .external})

-   Fixes test and documentation issues ([issue
    5612](https://github.com/scrapy/scrapy/issues/5612){.reference
    .external}, [issue
    5617](https://github.com/scrapy/scrapy/issues/5617){.reference
    .external}, [issue
    5631](https://github.com/scrapy/scrapy/issues/5631){.reference
    .external}).
:::

::: {#scrapy-2-6-2-2022-07-25 .section}
[]{#release-2-6-2}

#### Scrapy 2.6.2 (2022-07-25)[¶](#scrapy-2-6-2-2022-07-25 "Permalink to this heading"){.headerlink}

**Security bug fix:**

-   When [[`HttpProxyMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware"){.reference
    .internal} processes a request with [[`proxy`{.xref .std
    .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal} metadata, and that [[`proxy`{.xref
    .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal} metadata includes proxy credentials,
    [[`HttpProxyMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware"){.reference
    .internal} sets the [`Proxy-Authorization`{.docutils .literal
    .notranslate}]{.pre} header, but only if that header is not already
    set.

    There are third-party proxy-rotation downloader middlewares that set
    different [[`proxy`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal} metadata every time they process a
    request.

    Because of request retries and redirects, the same request can be
    processed by downloader middlewares more than once, including both
    [[`HttpProxyMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware"){.reference
    .internal} and any third-party proxy-rotation downloader middleware.

    These third-party proxy-rotation downloader middlewares could change
    the [[`proxy`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal} metadata of a request to a new value,
    but fail to remove the [`Proxy-Authorization`{.docutils .literal
    .notranslate}]{.pre} header from the previous value of the
    [[`proxy`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal} metadata, causing the credentials of
    one proxy to be sent to a different proxy.

    To prevent the unintended leaking of proxy credentials, the behavior
    of [[`HttpProxyMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware"){.reference
    .internal} is now as follows when processing a request:

    -   If the request being processed defines [[`proxy`{.xref .std
        .std-reqmeta .docutils .literal
        .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
        .tooltip .reference .internal} metadata that includes
        credentials, the [`Proxy-Authorization`{.docutils .literal
        .notranslate}]{.pre} header is always updated to feature those
        credentials.

    -   If the request being processed defines [[`proxy`{.xref .std
        .std-reqmeta .docutils .literal
        .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
        .tooltip .reference .internal} metadata without credentials, the
        [`Proxy-Authorization`{.docutils .literal .notranslate}]{.pre}
        header is removed *unless* it was originally defined for the
        same proxy URL.

        To remove proxy credentials while keeping the same proxy URL,
        remove the [`Proxy-Authorization`{.docutils .literal
        .notranslate}]{.pre} header.

    -   If the request has no [[`proxy`{.xref .std .std-reqmeta
        .docutils .literal
        .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
        .tooltip .reference .internal} metadata, or that metadata is a
        falsy value (e.g. [`None`{.docutils .literal
        .notranslate}]{.pre}), the [`Proxy-Authorization`{.docutils
        .literal .notranslate}]{.pre} header is removed.

        It is no longer possible to set a proxy URL through the
        [[`proxy`{.xref .std .std-reqmeta .docutils .literal
        .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
        .tooltip .reference .internal} metadata but set the credentials
        through the [`Proxy-Authorization`{.docutils .literal
        .notranslate}]{.pre} header. Set proxy credentials through the
        [[`proxy`{.xref .std .std-reqmeta .docutils .literal
        .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
        .tooltip .reference .internal} metadata instead.

Also fixes the following regressions introduced in 2.6.0:

-   [[`CrawlerProcess`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
    .internal} supports again crawling multiple spiders ([issue
    5435](https://github.com/scrapy/scrapy/issues/5435){.reference
    .external}, [issue
    5436](https://github.com/scrapy/scrapy/issues/5436){.reference
    .external})

-   Installing a Twisted reactor before Scrapy does (e.g. importing
    [[`twisted.internet.reactor`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
    .external} somewhere at the module level) no longer prevents Scrapy
    from starting, as long as a different reactor is not specified in
    [[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
    .tooltip .reference .internal} ([issue
    5525](https://github.com/scrapy/scrapy/issues/5525){.reference
    .external}, [issue
    5528](https://github.com/scrapy/scrapy/issues/5528){.reference
    .external})

-   Fixed an exception that was being logged after the spider finished
    under certain conditions ([issue
    5437](https://github.com/scrapy/scrapy/issues/5437){.reference
    .external}, [issue
    5440](https://github.com/scrapy/scrapy/issues/5440){.reference
    .external})

-   The [`--output`{.docutils .literal
    .notranslate}]{.pre}/[`-o`{.docutils .literal .notranslate}]{.pre}
    command-line parameter supports again a value starting with a hyphen
    ([issue
    5444](https://github.com/scrapy/scrapy/issues/5444){.reference
    .external}, [issue
    5445](https://github.com/scrapy/scrapy/issues/5445){.reference
    .external})

-   The [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`parse`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`-h`{.docutils .literal .notranslate}]{.pre} command
    no longer throws an error ([issue
    5481](https://github.com/scrapy/scrapy/issues/5481){.reference
    .external}, [issue
    5482](https://github.com/scrapy/scrapy/issues/5482){.reference
    .external})
:::

::: {#scrapy-2-6-1-2022-03-01 .section}
[]{#release-2-6-1}

#### Scrapy 2.6.1 (2022-03-01)[¶](#scrapy-2-6-1-2022-03-01 "Permalink to this heading"){.headerlink}

Fixes a regression introduced in 2.6.0 that would unset the request
method when following redirects.
:::

::: {#scrapy-2-6-0-2022-03-01 .section}
[]{#release-2-6-0}

#### Scrapy 2.6.0 (2022-03-01)[¶](#scrapy-2-6-0-2022-03-01 "Permalink to this heading"){.headerlink}

Highlights:

-   [[Security fixes for cookie handling]{.std
    .std-ref}](#security-fixes){.hoverxref .tooltip .reference
    .internal}

-   Python 3.10 support

-   [[asyncio support]{.std
    .std-ref}](index.html#using-asyncio){.hoverxref .tooltip .reference
    .internal} is no longer considered experimental, and works
    out-of-the-box on Windows regardless of your Python version

-   Feed exports now support [[`pathlib.Path`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.12)"){.reference
    .external} output paths and per-feed [[item filtering]{.std
    .std-ref}](index.html#item-filter){.hoverxref .tooltip .reference
    .internal} and [[post-processing]{.std
    .std-ref}](index.html#post-processing){.hoverxref .tooltip
    .reference .internal}

::: {#security-bug-fixes .section}
[]{#security-fixes}

##### Security bug fixes[¶](#security-bug-fixes "Permalink to this heading"){.headerlink}

-   When a [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object with cookies defined gets a redirect response
    causing a new [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object to be scheduled, the cookies defined in the
    original [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object are no longer copied into the new
    [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object.

    If you manually set the [`Cookie`{.docutils .literal
    .notranslate}]{.pre} header on a [[`Request`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object and the domain name of the redirect URL is not an
    exact match for the domain of the URL of the original
    [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object, your [`Cookie`{.docutils .literal
    .notranslate}]{.pre} header is now dropped from the new
    [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object.

    The old behavior could be exploited by an attacker to gain access to
    your cookies. Please, see the [cjvr-mfj7-j4j8 security
    advisory](https://github.com/scrapy/scrapy/security/advisories/GHSA-cjvr-mfj7-j4j8){.reference
    .external} for more information.

    ::: {.admonition .note}
    Note

    It is still possible to enable the sharing of cookies between
    different domains with a shared domain suffix (e.g.
    [`example.com`{.docutils .literal .notranslate}]{.pre} and any
    subdomain) by defining the shared domain suffix (e.g.
    [`example.com`{.docutils .literal .notranslate}]{.pre}) as the
    cookie domain when defining your cookies. See the documentation of
    the [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} class for more information.
    :::

-   When the domain of a cookie, either received in the
    [`Set-Cookie`{.docutils .literal .notranslate}]{.pre} header of a
    response or defined in a [[`Request`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object, is set to a [public
    suffix](https://publicsuffix.org/){.reference .external}, the cookie
    is now ignored unless the cookie domain is the same as the request
    domain.

    The old behavior could be exploited by an attacker to inject cookies
    from a controlled domain into your cookiejar that could be sent to
    other domains not controlled by the attacker. Please, see the
    [mfjm-vh54-3f96 security
    advisory](https://github.com/scrapy/scrapy/security/advisories/GHSA-mfjm-vh54-3f96){.reference
    .external} for more information.
:::

::: {#id29 .section}
##### Modified requirements[¶](#id29 "Permalink to this heading"){.headerlink}

-   The [h2](https://pypi.org/project/h2/){.reference .external}
    dependency is now optional, only needed to [[enable HTTP/2
    support]{.std .std-ref}](index.html#http2){.hoverxref .tooltip
    .reference .internal}. ([issue
    5113](https://github.com/scrapy/scrapy/issues/5113){.reference
    .external})
:::

::: {#id30 .section}
##### Backward-incompatible changes[¶](#id30 "Permalink to this heading"){.headerlink}

-   The [`formdata`{.docutils .literal .notranslate}]{.pre} parameter of
    [`FormRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}, if specified for a non-POST request, now
    overrides the URL query string, instead of being appended to it.
    ([issue
    2919](https://github.com/scrapy/scrapy/issues/2919){.reference
    .external}, [issue
    3579](https://github.com/scrapy/scrapy/issues/3579){.reference
    .external})

-   When a function is assigned to the [[`FEED_URI_PARAMS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_URI_PARAMS){.hoverxref
    .tooltip .reference .internal} setting, now the return value of that
    function, and not the [`params`{.docutils .literal
    .notranslate}]{.pre} input parameter, will determine the feed URI
    parameters, unless that return value is [`None`{.docutils .literal
    .notranslate}]{.pre}. ([issue
    4962](https://github.com/scrapy/scrapy/issues/4962){.reference
    .external}, [issue
    4966](https://github.com/scrapy/scrapy/issues/4966){.reference
    .external})

-   In [`scrapy.core.engine.ExecutionEngine`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre}, methods [`crawl()`{.xref
    .py .py-meth .docutils .literal .notranslate}]{.pre},
    [`download()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}, [`schedule()`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre}, and [`spider_is_idle()`{.xref .py
    .py-meth .docutils .literal .notranslate}]{.pre} now raise
    [[`RuntimeError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#RuntimeError "(in Python v3.12)"){.reference
    .external} if called before [`open_spider()`{.xref .py .py-meth
    .docutils .literal .notranslate}]{.pre}. ([issue
    5090](https://github.com/scrapy/scrapy/issues/5090){.reference
    .external})

    These methods used to assume that [`ExecutionEngine.slot`{.xref .py
    .py-attr .docutils .literal .notranslate}]{.pre} had been defined by
    a prior call to [`open_spider()`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre}, so they were raising
    [[`AttributeError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#AttributeError "(in Python v3.12)"){.reference
    .external} instead.

-   If the API of the configured [[scheduler]{.std
    .std-ref}](index.html#topics-scheduler){.hoverxref .tooltip
    .reference .internal} does not meet expectations,
    [[`TypeError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#TypeError "(in Python v3.12)"){.reference
    .external} is now raised at startup time. Before, other exceptions
    would be raised at run time. ([issue
    3559](https://github.com/scrapy/scrapy/issues/3559){.reference
    .external})

-   The [`_encoding`{.docutils .literal .notranslate}]{.pre} field of
    serialized [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} objects is now named [`encoding`{.docutils .literal
    .notranslate}]{.pre}, in line with all other fields ([issue
    5130](https://github.com/scrapy/scrapy/issues/5130){.reference
    .external})
:::

::: {#id31 .section}
##### Deprecation removals[¶](#id31 "Permalink to this heading"){.headerlink}

-   [`scrapy.http.TextResponse.body_as_unicode`{.docutils .literal
    .notranslate}]{.pre}, deprecated in Scrapy 2.2, has now been
    removed. ([issue
    5393](https://github.com/scrapy/scrapy/issues/5393){.reference
    .external})

-   [`scrapy.item.BaseItem`{.docutils .literal .notranslate}]{.pre},
    deprecated in Scrapy 2.2, has now been removed. ([issue
    5398](https://github.com/scrapy/scrapy/issues/5398){.reference
    .external})

-   [`scrapy.item.DictItem`{.docutils .literal .notranslate}]{.pre},
    deprecated in Scrapy 1.8, has now been removed. ([issue
    5398](https://github.com/scrapy/scrapy/issues/5398){.reference
    .external})

-   [`scrapy.Spider.make_requests_from_url`{.docutils .literal
    .notranslate}]{.pre}, deprecated in Scrapy 1.4, has now been
    removed. ([issue
    4178](https://github.com/scrapy/scrapy/issues/4178){.reference
    .external}, [issue
    4356](https://github.com/scrapy/scrapy/issues/4356){.reference
    .external})
:::

::: {#id32 .section}
##### Deprecations[¶](#id32 "Permalink to this heading"){.headerlink}

-   When a function is assigned to the [[`FEED_URI_PARAMS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_URI_PARAMS){.hoverxref
    .tooltip .reference .internal} setting, returning [`None`{.docutils
    .literal .notranslate}]{.pre} or modifying the [`params`{.docutils
    .literal .notranslate}]{.pre} input parameter is now deprecated.
    Return a new dictionary instead. ([issue
    4962](https://github.com/scrapy/scrapy/issues/4962){.reference
    .external}, [issue
    4966](https://github.com/scrapy/scrapy/issues/4966){.reference
    .external})

-   [`scrapy.utils.reqser`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre} is deprecated. ([issue
    5130](https://github.com/scrapy/scrapy/issues/5130){.reference
    .external})

    -   Instead of [`request_to_dict()`{.xref .py .py-func .docutils
        .literal .notranslate}]{.pre}, use the new
        [[`Request.to_dict`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request.to_dict "scrapy.http.Request.to_dict"){.reference
        .internal} method.

    -   Instead of [`request_from_dict()`{.xref .py .py-func .docutils
        .literal .notranslate}]{.pre}, use the new
        [[`scrapy.utils.request.request_from_dict()`{.xref .py .py-func
        .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.utils.request.request_from_dict "scrapy.utils.request.request_from_dict"){.reference
        .internal} function.

-   In [`scrapy.squeues`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}, the following queue classes are deprecated:
    [`PickleFifoDiskQueueNonRequest`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre},
    [`PickleLifoDiskQueueNonRequest`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre},
    [`MarshalFifoDiskQueueNonRequest`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre}, and
    [`MarshalLifoDiskQueueNonRequest`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre}. You should instead use:
    [`PickleFifoDiskQueue`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}, [`PickleLifoDiskQueue`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre},
    [`MarshalFifoDiskQueue`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}, and [`MarshalLifoDiskQueue`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre}. ([issue
    5117](https://github.com/scrapy/scrapy/issues/5117){.reference
    .external})

-   Many aspects of [`scrapy.core.engine.ExecutionEngine`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} that come from a
    time when this class could handle multiple [[`Spider`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
    .internal} objects at a time have been deprecated. ([issue
    5090](https://github.com/scrapy/scrapy/issues/5090){.reference
    .external})

    -   The [`has_capacity()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre} method is deprecated.

    -   The [`schedule()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre} method is deprecated, use [`crawl()`{.xref
        .py .py-meth .docutils .literal .notranslate}]{.pre} or
        [`download()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre} instead.

    -   The [`open_spiders`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre} attribute is deprecated, use
        [`spider`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre} instead.

    -   The [`spider`{.docutils .literal .notranslate}]{.pre} parameter
        is deprecated for the following methods:

        -   [`spider_is_idle()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [`crawl()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [`download()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        Instead, call [`open_spider()`{.xref .py .py-meth .docutils
        .literal .notranslate}]{.pre} first to set the [[`Spider`{.xref
        .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
        .internal} object.
:::

::: {#id33 .section}
##### New features[¶](#id33 "Permalink to this heading"){.headerlink}

-   You can now use [[item filtering]{.std
    .std-ref}](index.html#item-filter){.hoverxref .tooltip .reference
    .internal} to control which items are exported to each output feed.
    ([issue
    4575](https://github.com/scrapy/scrapy/issues/4575){.reference
    .external}, [issue
    5178](https://github.com/scrapy/scrapy/issues/5178){.reference
    .external}, [issue
    5161](https://github.com/scrapy/scrapy/issues/5161){.reference
    .external}, [issue
    5203](https://github.com/scrapy/scrapy/issues/5203){.reference
    .external})

-   You can now apply [[post-processing]{.std
    .std-ref}](index.html#post-processing){.hoverxref .tooltip
    .reference .internal} to feeds, and [[built-in post-processing
    plugins]{.std .std-ref}](index.html#builtin-plugins){.hoverxref
    .tooltip .reference .internal} are provided for output file
    compression. ([issue
    2174](https://github.com/scrapy/scrapy/issues/2174){.reference
    .external}, [issue
    5168](https://github.com/scrapy/scrapy/issues/5168){.reference
    .external}, [issue
    5190](https://github.com/scrapy/scrapy/issues/5190){.reference
    .external})

-   The [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} setting now supports
    [[`pathlib.Path`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.12)"){.reference
    .external} objects as keys. ([issue
    5383](https://github.com/scrapy/scrapy/issues/5383){.reference
    .external}, [issue
    5384](https://github.com/scrapy/scrapy/issues/5384){.reference
    .external})

-   Enabling [[asyncio]{.std
    .std-ref}](index.html#using-asyncio){.hoverxref .tooltip .reference
    .internal} while using Windows and Python 3.8 or later will
    automatically switch the asyncio event loop to one that allows
    Scrapy to work. See [[Windows-specific notes]{.std
    .std-ref}](index.html#asyncio-windows){.hoverxref .tooltip
    .reference .internal}. ([issue
    4976](https://github.com/scrapy/scrapy/issues/4976){.reference
    .external}, [issue
    5315](https://github.com/scrapy/scrapy/issues/5315){.reference
    .external})

-   The [[`genspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-genspider){.hoverxref
    .tooltip .reference .internal} command now supports a start URL
    instead of a domain name. ([issue
    4439](https://github.com/scrapy/scrapy/issues/4439){.reference
    .external})

-   [`scrapy.utils.defer`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre} gained 2 new functions,
    [[`deferred_to_future()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.utils.defer.deferred_to_future "scrapy.utils.defer.deferred_to_future"){.reference
    .internal} and [[`maybe_deferred_to_future()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.utils.defer.maybe_deferred_to_future "scrapy.utils.defer.maybe_deferred_to_future"){.reference
    .internal}, to help [[await on Deferreds when using the asyncio
    reactor]{.std .std-ref}](index.html#asyncio-await-dfd){.hoverxref
    .tooltip .reference .internal}. ([issue
    5288](https://github.com/scrapy/scrapy/issues/5288){.reference
    .external})

-   [[Amazon S3 feed export storage]{.std
    .std-ref}](index.html#topics-feed-storage-s3){.hoverxref .tooltip
    .reference .internal} gained support for [temporary security
    credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#temporary-access-keys){.reference
    .external} ([[`AWS_SESSION_TOKEN`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_SESSION_TOKEN){.hoverxref
    .tooltip .reference .internal}) and endpoint customization
    ([[`AWS_ENDPOINT_URL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_ENDPOINT_URL){.hoverxref
    .tooltip .reference .internal}). ([issue
    4998](https://github.com/scrapy/scrapy/issues/4998){.reference
    .external}, [issue
    5210](https://github.com/scrapy/scrapy/issues/5210){.reference
    .external})

-   New [[`LOG_FILE_APPEND`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_FILE_APPEND){.hoverxref
    .tooltip .reference .internal} setting to allow truncating the log
    file. ([issue
    5279](https://github.com/scrapy/scrapy/issues/5279){.reference
    .external})

-   [`Request.cookies`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} values that are [[`bool`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
    .external}, [[`float`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference
    .external} or [[`int`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
    .external} are cast to [[`str`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
    .external}. ([issue
    5252](https://github.com/scrapy/scrapy/issues/5252){.reference
    .external}, [issue
    5253](https://github.com/scrapy/scrapy/issues/5253){.reference
    .external})

-   You may now raise [[`CloseSpider`{.xref .py .py-exc .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.CloseSpider "scrapy.exceptions.CloseSpider"){.reference
    .internal} from a handler of the [[`spider_idle`{.xref .std
    .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-spider_idle){.hoverxref
    .tooltip .reference .internal} signal to customize the reason why
    the spider is stopping. ([issue
    5191](https://github.com/scrapy/scrapy/issues/5191){.reference
    .external})

-   When using [[`HttpProxyMiddleware`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware"){.reference
    .internal}, the proxy URL for non-HTTPS HTTP/1.1 requests no longer
    needs to include a URL scheme. ([issue
    4505](https://github.com/scrapy/scrapy/issues/4505){.reference
    .external}, [issue
    4649](https://github.com/scrapy/scrapy/issues/4649){.reference
    .external})

-   All built-in queues now expose a [`peek`{.docutils .literal
    .notranslate}]{.pre} method that returns the next queue object (like
    [`pop`{.docutils .literal .notranslate}]{.pre}) but does not remove
    the returned object from the queue. ([issue
    5112](https://github.com/scrapy/scrapy/issues/5112){.reference
    .external})

    If the underlying queue does not support peeking (e.g. because you
    are not using [`queuelib`{.docutils .literal .notranslate}]{.pre}
    1.6.1 or later), the [`peek`{.docutils .literal .notranslate}]{.pre}
    method raises [[`NotImplementedError`{.xref .py .py-exc .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#NotImplementedError "(in Python v3.12)"){.reference
    .external}.

-   [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} and [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} now have an [`attributes`{.docutils .literal
    .notranslate}]{.pre} attribute that makes subclassing easier. For
    [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal}, it also allows subclasses to work with
    [[`scrapy.utils.request.request_from_dict()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.utils.request.request_from_dict "scrapy.utils.request.request_from_dict"){.reference
    .internal}. ([issue
    1877](https://github.com/scrapy/scrapy/issues/1877){.reference
    .external}, [issue
    5130](https://github.com/scrapy/scrapy/issues/5130){.reference
    .external}, [issue
    5218](https://github.com/scrapy/scrapy/issues/5218){.reference
    .external})

-   The [[`open()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.core.scheduler.BaseScheduler.open "scrapy.core.scheduler.BaseScheduler.open"){.reference
    .internal} and [[`close()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.core.scheduler.BaseScheduler.close "scrapy.core.scheduler.BaseScheduler.close"){.reference
    .internal} methods of the [[scheduler]{.std
    .std-ref}](index.html#topics-scheduler){.hoverxref .tooltip
    .reference .internal} are now optional. ([issue
    3559](https://github.com/scrapy/scrapy/issues/3559){.reference
    .external})

-   HTTP/1.1 [`TunnelError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre} exceptions now only truncate response bodies
    longer than 1000 characters, instead of those longer than 32
    characters, making it easier to debug such errors. ([issue
    4881](https://github.com/scrapy/scrapy/issues/4881){.reference
    .external}, [issue
    5007](https://github.com/scrapy/scrapy/issues/5007){.reference
    .external})

-   [[`ItemLoader`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
    .internal} now supports non-text responses. ([issue
    5145](https://github.com/scrapy/scrapy/issues/5145){.reference
    .external}, [issue
    5269](https://github.com/scrapy/scrapy/issues/5269){.reference
    .external})
:::

::: {#id34 .section}
##### Bug fixes[¶](#id34 "Permalink to this heading"){.headerlink}

-   The [[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
    .tooltip .reference .internal} and [[`ASYNCIO_EVENT_LOOP`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ASYNCIO_EVENT_LOOP){.hoverxref
    .tooltip .reference .internal} settings are no longer ignored if
    defined in [[`custom_settings`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.custom_settings "scrapy.Spider.custom_settings"){.reference
    .internal}. ([issue
    4485](https://github.com/scrapy/scrapy/issues/4485){.reference
    .external}, [issue
    5352](https://github.com/scrapy/scrapy/issues/5352){.reference
    .external})

-   Removed a module-level Twisted reactor import that could prevent
    [[using the asyncio reactor]{.std
    .std-ref}](index.html#using-asyncio){.hoverxref .tooltip .reference
    .internal}. ([issue
    5357](https://github.com/scrapy/scrapy/issues/5357){.reference
    .external})

-   The [[`startproject`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} command works with existing folders
    again. ([issue
    4665](https://github.com/scrapy/scrapy/issues/4665){.reference
    .external}, [issue
    4676](https://github.com/scrapy/scrapy/issues/4676){.reference
    .external})

-   The [[`FEED_URI_PARAMS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_URI_PARAMS){.hoverxref
    .tooltip .reference .internal} setting now behaves as documented.
    ([issue
    4962](https://github.com/scrapy/scrapy/issues/4962){.reference
    .external}, [issue
    4966](https://github.com/scrapy/scrapy/issues/4966){.reference
    .external})

-   [`Request.cb_kwargs`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} once again allows the [`callback`{.docutils
    .literal .notranslate}]{.pre} keyword. ([issue
    5237](https://github.com/scrapy/scrapy/issues/5237){.reference
    .external}, [issue
    5251](https://github.com/scrapy/scrapy/issues/5251){.reference
    .external}, [issue
    5264](https://github.com/scrapy/scrapy/issues/5264){.reference
    .external})

-   Made [`scrapy.utils.response.open_in_browser()`{.xref .py .py-func
    .docutils .literal .notranslate}]{.pre} support more complex HTML.
    ([issue
    5319](https://github.com/scrapy/scrapy/issues/5319){.reference
    .external}, [issue
    5320](https://github.com/scrapy/scrapy/issues/5320){.reference
    .external})

-   Fixed [[`CSVFeedSpider.quotechar`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.CSVFeedSpider.quotechar "scrapy.spiders.CSVFeedSpider.quotechar"){.reference
    .internal} being interpreted as the CSV file encoding. ([issue
    5391](https://github.com/scrapy/scrapy/issues/5391){.reference
    .external}, [issue
    5394](https://github.com/scrapy/scrapy/issues/5394){.reference
    .external})

-   Added missing
    [setuptools](https://pypi.org/project/setuptools/){.reference
    .external} to the list of dependencies. ([issue
    5122](https://github.com/scrapy/scrapy/issues/5122){.reference
    .external})

-   [[`LinkExtractor`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} now also works as expected with links that have
    comma-separated [`rel`{.docutils .literal .notranslate}]{.pre}
    attribute values including [`nofollow`{.docutils .literal
    .notranslate}]{.pre}. ([issue
    5225](https://github.com/scrapy/scrapy/issues/5225){.reference
    .external})

-   Fixed a [[`TypeError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#TypeError "(in Python v3.12)"){.reference
    .external} that could be raised during [[feed export]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} parameter parsing. ([issue
    5359](https://github.com/scrapy/scrapy/issues/5359){.reference
    .external})
:::

::: {#id35 .section}
##### Documentation[¶](#id35 "Permalink to this heading"){.headerlink}

-   [[asyncio support]{.std
    .std-ref}](index.html#using-asyncio){.hoverxref .tooltip .reference
    .internal} is no longer considered experimental. ([issue
    5332](https://github.com/scrapy/scrapy/issues/5332){.reference
    .external})

-   Included [[Windows-specific help for asyncio usage]{.std
    .std-ref}](index.html#asyncio-windows){.hoverxref .tooltip
    .reference .internal}. ([issue
    4976](https://github.com/scrapy/scrapy/issues/4976){.reference
    .external}, [issue
    5315](https://github.com/scrapy/scrapy/issues/5315){.reference
    .external})

-   Rewrote [[Using a headless browser]{.std
    .std-ref}](index.html#topics-headless-browsing){.hoverxref .tooltip
    .reference .internal} with up-to-date best practices. ([issue
    4484](https://github.com/scrapy/scrapy/issues/4484){.reference
    .external}, [issue
    4613](https://github.com/scrapy/scrapy/issues/4613){.reference
    .external})

-   Documented [[local file naming in media pipelines]{.std
    .std-ref}](index.html#topics-file-naming){.hoverxref .tooltip
    .reference .internal}. ([issue
    5069](https://github.com/scrapy/scrapy/issues/5069){.reference
    .external}, [issue
    5152](https://github.com/scrapy/scrapy/issues/5152){.reference
    .external})

-   [[Frequently Asked Questions]{.std
    .std-ref}](index.html#faq){.hoverxref .tooltip .reference .internal}
    now covers spider file name collision issues. ([issue
    2680](https://github.com/scrapy/scrapy/issues/2680){.reference
    .external}, [issue
    3669](https://github.com/scrapy/scrapy/issues/3669){.reference
    .external})

-   Provided better context and instructions to disable the
    [[`URLLENGTH_LIMIT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-URLLENGTH_LIMIT){.hoverxref
    .tooltip .reference .internal} setting. ([issue
    5135](https://github.com/scrapy/scrapy/issues/5135){.reference
    .external}, [issue
    5250](https://github.com/scrapy/scrapy/issues/5250){.reference
    .external})

-   Documented that [[Reppy parser]{.std
    .std-ref}](index.html#reppy-parser){.hoverxref .tooltip .reference
    .internal} does not support Python 3.9+. ([issue
    5226](https://github.com/scrapy/scrapy/issues/5226){.reference
    .external}, [issue
    5231](https://github.com/scrapy/scrapy/issues/5231){.reference
    .external})

-   Documented [[the scheduler component]{.std
    .std-ref}](index.html#topics-scheduler){.hoverxref .tooltip
    .reference .internal}. ([issue
    3537](https://github.com/scrapy/scrapy/issues/3537){.reference
    .external}, [issue
    3559](https://github.com/scrapy/scrapy/issues/3559){.reference
    .external})

-   Documented the method used by [[media pipelines]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal} to [[determine if a file has expired]{.std
    .std-ref}](index.html#file-expiration){.hoverxref .tooltip
    .reference .internal}. ([issue
    5120](https://github.com/scrapy/scrapy/issues/5120){.reference
    .external}, [issue
    5254](https://github.com/scrapy/scrapy/issues/5254){.reference
    .external})

-   [[Running multiple spiders in the same process]{.std
    .std-ref}](index.html#run-multiple-spiders){.hoverxref .tooltip
    .reference .internal} now features
    [`scrapy.utils.project.get_project_settings()`{.xref .py .py-func
    .docutils .literal .notranslate}]{.pre} usage. ([issue
    5070](https://github.com/scrapy/scrapy/issues/5070){.reference
    .external})

-   [[Running multiple spiders in the same process]{.std
    .std-ref}](index.html#run-multiple-spiders){.hoverxref .tooltip
    .reference .internal} now covers what happens when you define
    different per-spider values for some settings that cannot differ at
    run time. ([issue
    4485](https://github.com/scrapy/scrapy/issues/4485){.reference
    .external}, [issue
    5352](https://github.com/scrapy/scrapy/issues/5352){.reference
    .external})

-   Extended the documentation of the [[`StatsMailer`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.extensions.statsmailer.StatsMailer "scrapy.extensions.statsmailer.StatsMailer"){.reference
    .internal} extension. ([issue
    5199](https://github.com/scrapy/scrapy/issues/5199){.reference
    .external}, [issue
    5217](https://github.com/scrapy/scrapy/issues/5217){.reference
    .external})

-   Added [[`JOBDIR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-JOBDIR){.hoverxref
    .tooltip .reference .internal} to [[Settings]{.std
    .std-ref}](index.html#topics-settings){.hoverxref .tooltip
    .reference .internal}. ([issue
    5173](https://github.com/scrapy/scrapy/issues/5173){.reference
    .external}, [issue
    5224](https://github.com/scrapy/scrapy/issues/5224){.reference
    .external})

-   Documented [`Spider.attribute`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}. ([issue
    5174](https://github.com/scrapy/scrapy/issues/5174){.reference
    .external}, [issue
    5244](https://github.com/scrapy/scrapy/issues/5244){.reference
    .external})

-   Documented [[`TextResponse.urljoin`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.urljoin "scrapy.http.TextResponse.urljoin"){.reference
    .internal}. ([issue
    1582](https://github.com/scrapy/scrapy/issues/1582){.reference
    .external})

-   Added the [`body_length`{.docutils .literal .notranslate}]{.pre}
    parameter to the documented signature of the
    [[`headers_received`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-headers_received){.hoverxref
    .tooltip .reference .internal} signal. ([issue
    5270](https://github.com/scrapy/scrapy/issues/5270){.reference
    .external})

-   Clarified [[`SelectorList.get`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.selector.SelectorList.get "scrapy.selector.SelectorList.get"){.reference
    .internal} usage in the [[tutorial]{.std
    .std-ref}](index.html#intro-tutorial){.hoverxref .tooltip .reference
    .internal}. ([issue
    5256](https://github.com/scrapy/scrapy/issues/5256){.reference
    .external})

-   The documentation now features the shortest import path of classes
    with multiple import paths. ([issue
    2733](https://github.com/scrapy/scrapy/issues/2733){.reference
    .external}, [issue
    5099](https://github.com/scrapy/scrapy/issues/5099){.reference
    .external})

-   [`quotes.toscrape.com`{.docutils .literal .notranslate}]{.pre}
    references now use HTTPS instead of HTTP. ([issue
    5395](https://github.com/scrapy/scrapy/issues/5395){.reference
    .external}, [issue
    5396](https://github.com/scrapy/scrapy/issues/5396){.reference
    .external})

-   Added a link to [our Discord
    server](https://discord.gg/mv3yErfpvq){.reference .external} to
    [[Getting help]{.std .std-ref}](index.html#getting-help){.hoverxref
    .tooltip .reference .internal}. ([issue
    5421](https://github.com/scrapy/scrapy/issues/5421){.reference
    .external}, [issue
    5422](https://github.com/scrapy/scrapy/issues/5422){.reference
    .external})

-   The pronunciation of the project name is now [[officially]{.std
    .std-ref}](index.html#intro-overview){.hoverxref .tooltip .reference
    .internal} /ˈskreɪpaɪ/. ([issue
    5280](https://github.com/scrapy/scrapy/issues/5280){.reference
    .external}, [issue
    5281](https://github.com/scrapy/scrapy/issues/5281){.reference
    .external})

-   Added the Scrapy logo to the README. ([issue
    5255](https://github.com/scrapy/scrapy/issues/5255){.reference
    .external}, [issue
    5258](https://github.com/scrapy/scrapy/issues/5258){.reference
    .external})

-   Fixed issues and implemented minor improvements. ([issue
    3155](https://github.com/scrapy/scrapy/issues/3155){.reference
    .external}, [issue
    4335](https://github.com/scrapy/scrapy/issues/4335){.reference
    .external}, [issue
    5074](https://github.com/scrapy/scrapy/issues/5074){.reference
    .external}, [issue
    5098](https://github.com/scrapy/scrapy/issues/5098){.reference
    .external}, [issue
    5134](https://github.com/scrapy/scrapy/issues/5134){.reference
    .external}, [issue
    5180](https://github.com/scrapy/scrapy/issues/5180){.reference
    .external}, [issue
    5194](https://github.com/scrapy/scrapy/issues/5194){.reference
    .external}, [issue
    5239](https://github.com/scrapy/scrapy/issues/5239){.reference
    .external}, [issue
    5266](https://github.com/scrapy/scrapy/issues/5266){.reference
    .external}, [issue
    5271](https://github.com/scrapy/scrapy/issues/5271){.reference
    .external}, [issue
    5273](https://github.com/scrapy/scrapy/issues/5273){.reference
    .external}, [issue
    5274](https://github.com/scrapy/scrapy/issues/5274){.reference
    .external}, [issue
    5276](https://github.com/scrapy/scrapy/issues/5276){.reference
    .external}, [issue
    5347](https://github.com/scrapy/scrapy/issues/5347){.reference
    .external}, [issue
    5356](https://github.com/scrapy/scrapy/issues/5356){.reference
    .external}, [issue
    5414](https://github.com/scrapy/scrapy/issues/5414){.reference
    .external}, [issue
    5415](https://github.com/scrapy/scrapy/issues/5415){.reference
    .external}, [issue
    5416](https://github.com/scrapy/scrapy/issues/5416){.reference
    .external}, [issue
    5419](https://github.com/scrapy/scrapy/issues/5419){.reference
    .external}, [issue
    5420](https://github.com/scrapy/scrapy/issues/5420){.reference
    .external})
:::

::: {#id36 .section}
##### Quality Assurance[¶](#id36 "Permalink to this heading"){.headerlink}

-   Added support for Python 3.10. ([issue
    5212](https://github.com/scrapy/scrapy/issues/5212){.reference
    .external}, [issue
    5221](https://github.com/scrapy/scrapy/issues/5221){.reference
    .external}, [issue
    5265](https://github.com/scrapy/scrapy/issues/5265){.reference
    .external})

-   Significantly reduced memory usage by
    [`scrapy.utils.response.response_httprepr()`{.xref .py .py-func
    .docutils .literal .notranslate}]{.pre}, used by the
    [[`DownloaderStats`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.stats.DownloaderStats "scrapy.downloadermiddlewares.stats.DownloaderStats"){.reference
    .internal} downloader middleware, which is enabled by default.
    ([issue
    4964](https://github.com/scrapy/scrapy/issues/4964){.reference
    .external}, [issue
    4972](https://github.com/scrapy/scrapy/issues/4972){.reference
    .external})

-   Removed uses of the deprecated [[`optparse`{.xref .py .py-mod
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/optparse.html#module-optparse "(in Python v3.12)"){.reference
    .external} module. ([issue
    5366](https://github.com/scrapy/scrapy/issues/5366){.reference
    .external}, [issue
    5374](https://github.com/scrapy/scrapy/issues/5374){.reference
    .external})

-   Extended typing hints. ([issue
    5077](https://github.com/scrapy/scrapy/issues/5077){.reference
    .external}, [issue
    5090](https://github.com/scrapy/scrapy/issues/5090){.reference
    .external}, [issue
    5100](https://github.com/scrapy/scrapy/issues/5100){.reference
    .external}, [issue
    5108](https://github.com/scrapy/scrapy/issues/5108){.reference
    .external}, [issue
    5171](https://github.com/scrapy/scrapy/issues/5171){.reference
    .external}, [issue
    5215](https://github.com/scrapy/scrapy/issues/5215){.reference
    .external}, [issue
    5334](https://github.com/scrapy/scrapy/issues/5334){.reference
    .external})

-   Improved tests, fixed CI issues, removed unused code. ([issue
    5094](https://github.com/scrapy/scrapy/issues/5094){.reference
    .external}, [issue
    5157](https://github.com/scrapy/scrapy/issues/5157){.reference
    .external}, [issue
    5162](https://github.com/scrapy/scrapy/issues/5162){.reference
    .external}, [issue
    5198](https://github.com/scrapy/scrapy/issues/5198){.reference
    .external}, [issue
    5207](https://github.com/scrapy/scrapy/issues/5207){.reference
    .external}, [issue
    5208](https://github.com/scrapy/scrapy/issues/5208){.reference
    .external}, [issue
    5229](https://github.com/scrapy/scrapy/issues/5229){.reference
    .external}, [issue
    5298](https://github.com/scrapy/scrapy/issues/5298){.reference
    .external}, [issue
    5299](https://github.com/scrapy/scrapy/issues/5299){.reference
    .external}, [issue
    5310](https://github.com/scrapy/scrapy/issues/5310){.reference
    .external}, [issue
    5316](https://github.com/scrapy/scrapy/issues/5316){.reference
    .external}, [issue
    5333](https://github.com/scrapy/scrapy/issues/5333){.reference
    .external}, [issue
    5388](https://github.com/scrapy/scrapy/issues/5388){.reference
    .external}, [issue
    5389](https://github.com/scrapy/scrapy/issues/5389){.reference
    .external}, [issue
    5400](https://github.com/scrapy/scrapy/issues/5400){.reference
    .external}, [issue
    5401](https://github.com/scrapy/scrapy/issues/5401){.reference
    .external}, [issue
    5404](https://github.com/scrapy/scrapy/issues/5404){.reference
    .external}, [issue
    5405](https://github.com/scrapy/scrapy/issues/5405){.reference
    .external}, [issue
    5407](https://github.com/scrapy/scrapy/issues/5407){.reference
    .external}, [issue
    5410](https://github.com/scrapy/scrapy/issues/5410){.reference
    .external}, [issue
    5412](https://github.com/scrapy/scrapy/issues/5412){.reference
    .external}, [issue
    5425](https://github.com/scrapy/scrapy/issues/5425){.reference
    .external}, [issue
    5427](https://github.com/scrapy/scrapy/issues/5427){.reference
    .external})

-   Implemented improvements for contributors. ([issue
    5080](https://github.com/scrapy/scrapy/issues/5080){.reference
    .external}, [issue
    5082](https://github.com/scrapy/scrapy/issues/5082){.reference
    .external}, [issue
    5177](https://github.com/scrapy/scrapy/issues/5177){.reference
    .external}, [issue
    5200](https://github.com/scrapy/scrapy/issues/5200){.reference
    .external})

-   Implemented cleanups. ([issue
    5095](https://github.com/scrapy/scrapy/issues/5095){.reference
    .external}, [issue
    5106](https://github.com/scrapy/scrapy/issues/5106){.reference
    .external}, [issue
    5209](https://github.com/scrapy/scrapy/issues/5209){.reference
    .external}, [issue
    5228](https://github.com/scrapy/scrapy/issues/5228){.reference
    .external}, [issue
    5235](https://github.com/scrapy/scrapy/issues/5235){.reference
    .external}, [issue
    5245](https://github.com/scrapy/scrapy/issues/5245){.reference
    .external}, [issue
    5246](https://github.com/scrapy/scrapy/issues/5246){.reference
    .external}, [issue
    5292](https://github.com/scrapy/scrapy/issues/5292){.reference
    .external}, [issue
    5314](https://github.com/scrapy/scrapy/issues/5314){.reference
    .external}, [issue
    5322](https://github.com/scrapy/scrapy/issues/5322){.reference
    .external})
:::
:::

::: {#scrapy-2-5-1-2021-10-05 .section}
[]{#release-2-5-1}

#### Scrapy 2.5.1 (2021-10-05)[¶](#scrapy-2-5-1-2021-10-05 "Permalink to this heading"){.headerlink}

-   **Security bug fix:**

    If you use [[`HttpAuthMiddleware`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware "scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware"){.reference
    .internal} (i.e. the [`http_user`{.docutils .literal
    .notranslate}]{.pre} and [`http_pass`{.docutils .literal
    .notranslate}]{.pre} spider attributes) for HTTP authentication, any
    request exposes your credentials to the request target.

    To prevent unintended exposure of authentication credentials to
    unintended domains, you must now additionally set a new, additional
    spider attribute, [`http_auth_domain`{.docutils .literal
    .notranslate}]{.pre}, and point it to the specific domain to which
    the authentication credentials must be sent.

    If the [`http_auth_domain`{.docutils .literal .notranslate}]{.pre}
    spider attribute is not set, the domain of the first request will be
    considered the HTTP authentication target, and authentication
    credentials will only be sent in requests targeting that domain.

    If you need to send the same HTTP authentication credentials to
    multiple domains, you can use
    [[`w3lib.http.basic_auth_header()`{.xref .py .py-func .docutils
    .literal
    .notranslate}]{.pre}](https://w3lib.readthedocs.io/en/latest/w3lib.html#w3lib.http.basic_auth_header "(in w3lib v2.1)"){.reference
    .external} instead to set the value of the
    [`Authorization`{.docutils .literal .notranslate}]{.pre} header of
    your requests.

    If you *really* want your spider to send the same HTTP
    authentication credentials to any domain, set the
    [`http_auth_domain`{.docutils .literal .notranslate}]{.pre} spider
    attribute to [`None`{.docutils .literal .notranslate}]{.pre}.

    Finally, if you are a user of
    [scrapy-splash](https://github.com/scrapy-plugins/scrapy-splash){.reference
    .external}, know that this version of Scrapy breaks compatibility
    with scrapy-splash 0.7.2 and earlier. You will need to upgrade
    scrapy-splash to a greater version for it to continue to work.
:::

::: {#scrapy-2-5-0-2021-04-06 .section}
[]{#release-2-5-0}

#### Scrapy 2.5.0 (2021-04-06)[¶](#scrapy-2-5-0-2021-04-06 "Permalink to this heading"){.headerlink}

Highlights:

-   Official Python 3.9 support

-   Experimental [[HTTP/2 support]{.std
    .std-ref}](index.html#http2){.hoverxref .tooltip .reference
    .internal}

-   New [[`get_retry_request()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.get_retry_request "scrapy.downloadermiddlewares.retry.get_retry_request"){.reference
    .internal} function to retry requests from spider callbacks

-   New [[`headers_received`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.signals.headers_received "scrapy.signals.headers_received"){.reference
    .internal} signal that allows stopping downloads early

-   New [[`Response.protocol`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.protocol "scrapy.http.Response.protocol"){.reference
    .internal} attribute

::: {#id37 .section}
##### Deprecation removals[¶](#id37 "Permalink to this heading"){.headerlink}

-   Removed all code that [[was deprecated in 1.7.0]{.std
    .std-ref}](#id96){.hoverxref .tooltip .reference .internal} and had
    not [[already been removed in 2.4.0]{.std
    .std-ref}](#id45){.hoverxref .tooltip .reference .internal}. ([issue
    4901](https://github.com/scrapy/scrapy/issues/4901){.reference
    .external})

-   Removed support for the
    [`SCRAPY_PICKLED_SETTINGS_TO_OVERRIDE`{.docutils .literal
    .notranslate}]{.pre} environment variable, [[deprecated in
    1.8.0]{.std .std-ref}](#id88){.hoverxref .tooltip .reference
    .internal}. ([issue
    4912](https://github.com/scrapy/scrapy/issues/4912){.reference
    .external})
:::

::: {#id38 .section}
##### Deprecations[¶](#id38 "Permalink to this heading"){.headerlink}

-   The [`scrapy.utils.py36`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre} module is now deprecated in favor of
    [`scrapy.utils.asyncgen`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}. ([issue
    4900](https://github.com/scrapy/scrapy/issues/4900){.reference
    .external})
:::

::: {#id39 .section}
##### New features[¶](#id39 "Permalink to this heading"){.headerlink}

-   Experimental [[HTTP/2 support]{.std
    .std-ref}](index.html#http2){.hoverxref .tooltip .reference
    .internal} through a new download handler that can be assigned to
    the [`https`{.docutils .literal .notranslate}]{.pre} protocol in the
    [[`DOWNLOAD_HANDLERS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal} setting. ([issue
    1854](https://github.com/scrapy/scrapy/issues/1854){.reference
    .external}, [issue
    4769](https://github.com/scrapy/scrapy/issues/4769){.reference
    .external}, [issue
    5058](https://github.com/scrapy/scrapy/issues/5058){.reference
    .external}, [issue
    5059](https://github.com/scrapy/scrapy/issues/5059){.reference
    .external}, [issue
    5066](https://github.com/scrapy/scrapy/issues/5066){.reference
    .external})

-   The new
    [[`scrapy.downloadermiddlewares.retry.get_retry_request()`{.xref .py
    .py-func .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.get_retry_request "scrapy.downloadermiddlewares.retry.get_retry_request"){.reference
    .internal} function may be used from spider callbacks or middlewares
    to handle the retrying of a request beyond the scenarios that
    [[`RetryMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.RetryMiddleware "scrapy.downloadermiddlewares.retry.RetryMiddleware"){.reference
    .internal} supports. ([issue
    3590](https://github.com/scrapy/scrapy/issues/3590){.reference
    .external}, [issue
    3685](https://github.com/scrapy/scrapy/issues/3685){.reference
    .external}, [issue
    4902](https://github.com/scrapy/scrapy/issues/4902){.reference
    .external})

-   The new [[`headers_received`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.signals.headers_received "scrapy.signals.headers_received"){.reference
    .internal} signal gives early access to response headers and allows
    [[stopping downloads]{.std
    .std-ref}](index.html#topics-stop-response-download){.hoverxref
    .tooltip .reference .internal}. ([issue
    1772](https://github.com/scrapy/scrapy/issues/1772){.reference
    .external}, [issue
    4897](https://github.com/scrapy/scrapy/issues/4897){.reference
    .external})

-   The new [[`Response.protocol`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.protocol "scrapy.http.Response.protocol"){.reference
    .internal} attribute gives access to the string that identifies the
    protocol used to download a response. ([issue
    4878](https://github.com/scrapy/scrapy/issues/4878){.reference
    .external})

-   [[Stats]{.std .std-ref}](index.html#topics-stats){.hoverxref
    .tooltip .reference .internal} now include the following entries
    that indicate the number of successes and failures in storing
    [[feeds]{.std .std-ref}](index.html#topics-feed-exports){.hoverxref
    .tooltip .reference .internal}:

    ::: {.highlight-default .notranslate}
    ::: highlight
        feedexport/success_count/<storage type>
        feedexport/failed_count/<storage type>
    :::
    :::

    Where [`<storage`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`type>`{.docutils .literal .notranslate}]{.pre} is the
    feed storage backend class name, such as [`FileFeedStorage`{.xref
    .py .py-class .docutils .literal .notranslate}]{.pre} or
    [`FTPFeedStorage`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}.

    ([issue
    3947](https://github.com/scrapy/scrapy/issues/3947){.reference
    .external}, [issue
    4850](https://github.com/scrapy/scrapy/issues/4850){.reference
    .external})

-   The [[`UrlLengthMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.urllength.UrlLengthMiddleware "scrapy.spidermiddlewares.urllength.UrlLengthMiddleware"){.reference
    .internal} spider middleware now logs ignored URLs with
    [`INFO`{.docutils .literal .notranslate}]{.pre} [[logging
    level]{.xref .std
    .std-ref}](https://docs.python.org/3/library/logging.html#levels "(in Python v3.12)"){.reference
    .external} instead of [`DEBUG`{.docutils .literal
    .notranslate}]{.pre}, and it now includes the following entry into
    [[stats]{.std .std-ref}](index.html#topics-stats){.hoverxref
    .tooltip .reference .internal} to keep track of the number of
    ignored URLs:

    ::: {.highlight-default .notranslate}
    ::: highlight
        urllength/request_ignored_count
    :::
    :::

    ([issue
    5036](https://github.com/scrapy/scrapy/issues/5036){.reference
    .external})

-   The [[`HttpCompressionMiddleware`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware "scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware"){.reference
    .internal} downloader middleware now logs the number of decompressed
    responses and the total count of resulting bytes:

    ::: {.highlight-default .notranslate}
    ::: highlight
        httpcompression/response_bytes
        httpcompression/response_count
    :::
    :::

    ([issue
    4797](https://github.com/scrapy/scrapy/issues/4797){.reference
    .external}, [issue
    4799](https://github.com/scrapy/scrapy/issues/4799){.reference
    .external})
:::

::: {#id40 .section}
##### Bug fixes[¶](#id40 "Permalink to this heading"){.headerlink}

-   Fixed installation on PyPy installing PyDispatcher in addition to
    PyPyDispatcher, which could prevent Scrapy from working depending on
    which package got imported. ([issue
    4710](https://github.com/scrapy/scrapy/issues/4710){.reference
    .external}, [issue
    4814](https://github.com/scrapy/scrapy/issues/4814){.reference
    .external})

-   When inspecting a callback to check if it is a generator that also
    returns a value, an exception is no longer raised if the callback
    has a docstring with lower indentation than the following code.
    ([issue
    4477](https://github.com/scrapy/scrapy/issues/4477){.reference
    .external}, [issue
    4935](https://github.com/scrapy/scrapy/issues/4935){.reference
    .external})

-   The
    [Content-Length](https://tools.ietf.org/html/rfc2616#section-14.13){.reference
    .external} header is no longer omitted from responses when using the
    default, HTTP/1.1 download handler (see [[`DOWNLOAD_HANDLERS`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal}). ([issue
    5009](https://github.com/scrapy/scrapy/issues/5009){.reference
    .external}, [issue
    5034](https://github.com/scrapy/scrapy/issues/5034){.reference
    .external}, [issue
    5045](https://github.com/scrapy/scrapy/issues/5045){.reference
    .external}, [issue
    5057](https://github.com/scrapy/scrapy/issues/5057){.reference
    .external}, [issue
    5062](https://github.com/scrapy/scrapy/issues/5062){.reference
    .external})

-   Setting the [[`handle_httpstatus_all`{.xref .std .std-reqmeta
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-handle_httpstatus_all){.hoverxref
    .tooltip .reference .internal} request meta key to
    [`False`{.docutils .literal .notranslate}]{.pre} now has the same
    effect as not setting it at all, instead of having the same effect
    as setting it to [`True`{.docutils .literal .notranslate}]{.pre}.
    ([issue
    3851](https://github.com/scrapy/scrapy/issues/3851){.reference
    .external}, [issue
    4694](https://github.com/scrapy/scrapy/issues/4694){.reference
    .external})
:::

::: {#id41 .section}
##### Documentation[¶](#id41 "Permalink to this heading"){.headerlink}

-   Added instructions to [[install Scrapy in Windows using pip]{.std
    .std-ref}](index.html#intro-install-windows){.hoverxref .tooltip
    .reference .internal}. ([issue
    4715](https://github.com/scrapy/scrapy/issues/4715){.reference
    .external}, [issue
    4736](https://github.com/scrapy/scrapy/issues/4736){.reference
    .external})

-   Logging documentation now includes [[additional ways to filter
    logs]{.std
    .std-ref}](index.html#topics-logging-advanced-customization){.hoverxref
    .tooltip .reference .internal}. ([issue
    4216](https://github.com/scrapy/scrapy/issues/4216){.reference
    .external}, [issue
    4257](https://github.com/scrapy/scrapy/issues/4257){.reference
    .external}, [issue
    4965](https://github.com/scrapy/scrapy/issues/4965){.reference
    .external})

-   Covered how to deal with long lists of allowed domains in the
    [[FAQ]{.std .std-ref}](index.html#faq){.hoverxref .tooltip
    .reference .internal}. ([issue
    2263](https://github.com/scrapy/scrapy/issues/2263){.reference
    .external}, [issue
    3667](https://github.com/scrapy/scrapy/issues/3667){.reference
    .external})

-   Covered
    [scrapy-bench](https://github.com/scrapy/scrapy-bench){.reference
    .external} in [[Benchmarking]{.std
    .std-ref}](index.html#benchmarking){.hoverxref .tooltip .reference
    .internal}. ([issue
    4996](https://github.com/scrapy/scrapy/issues/4996){.reference
    .external}, [issue
    5016](https://github.com/scrapy/scrapy/issues/5016){.reference
    .external})

-   Clarified that one [[extension]{.std
    .std-ref}](index.html#topics-extensions){.hoverxref .tooltip
    .reference .internal} instance is created per crawler. ([issue
    5014](https://github.com/scrapy/scrapy/issues/5014){.reference
    .external})

-   Fixed some errors in examples. ([issue
    4829](https://github.com/scrapy/scrapy/issues/4829){.reference
    .external}, [issue
    4830](https://github.com/scrapy/scrapy/issues/4830){.reference
    .external}, [issue
    4907](https://github.com/scrapy/scrapy/issues/4907){.reference
    .external}, [issue
    4909](https://github.com/scrapy/scrapy/issues/4909){.reference
    .external}, [issue
    5008](https://github.com/scrapy/scrapy/issues/5008){.reference
    .external})

-   Fixed some external links, typos, and so on. ([issue
    4892](https://github.com/scrapy/scrapy/issues/4892){.reference
    .external}, [issue
    4899](https://github.com/scrapy/scrapy/issues/4899){.reference
    .external}, [issue
    4936](https://github.com/scrapy/scrapy/issues/4936){.reference
    .external}, [issue
    4942](https://github.com/scrapy/scrapy/issues/4942){.reference
    .external}, [issue
    5005](https://github.com/scrapy/scrapy/issues/5005){.reference
    .external}, [issue
    5063](https://github.com/scrapy/scrapy/issues/5063){.reference
    .external})

-   The [[list of Request.meta keys]{.std
    .std-ref}](index.html#topics-request-meta){.hoverxref .tooltip
    .reference .internal} is now sorted alphabetically. ([issue
    5061](https://github.com/scrapy/scrapy/issues/5061){.reference
    .external}, [issue
    5065](https://github.com/scrapy/scrapy/issues/5065){.reference
    .external})

-   Updated references to Scrapinghub, which is now called Zyte. ([issue
    4973](https://github.com/scrapy/scrapy/issues/4973){.reference
    .external}, [issue
    5072](https://github.com/scrapy/scrapy/issues/5072){.reference
    .external})

-   Added a mention to contributors in the README. ([issue
    4956](https://github.com/scrapy/scrapy/issues/4956){.reference
    .external})

-   Reduced the top margin of lists. ([issue
    4974](https://github.com/scrapy/scrapy/issues/4974){.reference
    .external})
:::

::: {#id42 .section}
##### Quality Assurance[¶](#id42 "Permalink to this heading"){.headerlink}

-   Made Python 3.9 support official ([issue
    4757](https://github.com/scrapy/scrapy/issues/4757){.reference
    .external}, [issue
    4759](https://github.com/scrapy/scrapy/issues/4759){.reference
    .external})

-   Extended typing hints ([issue
    4895](https://github.com/scrapy/scrapy/issues/4895){.reference
    .external})

-   Fixed deprecated uses of the Twisted API. ([issue
    4940](https://github.com/scrapy/scrapy/issues/4940){.reference
    .external}, [issue
    4950](https://github.com/scrapy/scrapy/issues/4950){.reference
    .external}, [issue
    5073](https://github.com/scrapy/scrapy/issues/5073){.reference
    .external})

-   Made our tests run with the new pip resolver. ([issue
    4710](https://github.com/scrapy/scrapy/issues/4710){.reference
    .external}, [issue
    4814](https://github.com/scrapy/scrapy/issues/4814){.reference
    .external})

-   Added tests to ensure that [[coroutine support]{.std
    .std-ref}](index.html#coroutine-support){.hoverxref .tooltip
    .reference .internal} is tested. ([issue
    4987](https://github.com/scrapy/scrapy/issues/4987){.reference
    .external})

-   Migrated from Travis CI to GitHub Actions. ([issue
    4924](https://github.com/scrapy/scrapy/issues/4924){.reference
    .external})

-   Fixed CI issues. ([issue
    4986](https://github.com/scrapy/scrapy/issues/4986){.reference
    .external}, [issue
    5020](https://github.com/scrapy/scrapy/issues/5020){.reference
    .external}, [issue
    5022](https://github.com/scrapy/scrapy/issues/5022){.reference
    .external}, [issue
    5027](https://github.com/scrapy/scrapy/issues/5027){.reference
    .external}, [issue
    5052](https://github.com/scrapy/scrapy/issues/5052){.reference
    .external}, [issue
    5053](https://github.com/scrapy/scrapy/issues/5053){.reference
    .external})

-   Implemented code refactorings, style fixes and cleanups. ([issue
    4911](https://github.com/scrapy/scrapy/issues/4911){.reference
    .external}, [issue
    4982](https://github.com/scrapy/scrapy/issues/4982){.reference
    .external}, [issue
    5001](https://github.com/scrapy/scrapy/issues/5001){.reference
    .external}, [issue
    5002](https://github.com/scrapy/scrapy/issues/5002){.reference
    .external}, [issue
    5076](https://github.com/scrapy/scrapy/issues/5076){.reference
    .external})
:::
:::

::: {#scrapy-2-4-1-2020-11-17 .section}
[]{#release-2-4-1}

#### Scrapy 2.4.1 (2020-11-17)[¶](#scrapy-2-4-1-2020-11-17 "Permalink to this heading"){.headerlink}

-   Fixed [[feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} overwrite support ([issue
    4845](https://github.com/scrapy/scrapy/issues/4845){.reference
    .external}, [issue
    4857](https://github.com/scrapy/scrapy/issues/4857){.reference
    .external}, [issue
    4859](https://github.com/scrapy/scrapy/issues/4859){.reference
    .external})

-   Fixed the AsyncIO event loop handling, which could make code hang
    ([issue
    4855](https://github.com/scrapy/scrapy/issues/4855){.reference
    .external}, [issue
    4872](https://github.com/scrapy/scrapy/issues/4872){.reference
    .external})

-   Fixed the IPv6-capable DNS resolver [`CachingHostnameResolver`{.xref
    .py .py-class .docutils .literal .notranslate}]{.pre} for download
    handlers that call [[`reactor.resolve`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.interfaces.IReactorCore.html#resolve "(in Twisted)"){.reference
    .external} ([issue
    4802](https://github.com/scrapy/scrapy/issues/4802){.reference
    .external}, [issue
    4803](https://github.com/scrapy/scrapy/issues/4803){.reference
    .external})

-   Fixed the output of the [[`genspider`{.xref .std .std-command
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-genspider){.hoverxref
    .tooltip .reference .internal} command showing placeholders instead
    of the import path of the generated spider module ([issue
    4874](https://github.com/scrapy/scrapy/issues/4874){.reference
    .external})

-   Migrated Windows CI from Azure Pipelines to GitHub Actions ([issue
    4869](https://github.com/scrapy/scrapy/issues/4869){.reference
    .external}, [issue
    4876](https://github.com/scrapy/scrapy/issues/4876){.reference
    .external})
:::

::: {#scrapy-2-4-0-2020-10-11 .section}
[]{#release-2-4-0}

#### Scrapy 2.4.0 (2020-10-11)[¶](#scrapy-2-4-0-2020-10-11 "Permalink to this heading"){.headerlink}

Highlights:

-   Python 3.5 support has been dropped.

-   The [`file_path`{.docutils .literal .notranslate}]{.pre} method of
    [[media pipelines]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal} can now access the source [[item]{.std
    .std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
    .internal}.

    This allows you to set a download file path based on item data.

-   The new [`item_export_kwargs`{.docutils .literal
    .notranslate}]{.pre} key of the [[`FEEDS`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} setting allows to define keyword
    parameters to pass to [[item exporter classes]{.std
    .std-ref}](index.html#topics-exporters){.hoverxref .tooltip
    .reference .internal}

-   You can now choose whether [[feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} overwrite or append to the output file.

    For example, when using the [[`crawl`{.xref .std .std-command
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref
    .tooltip .reference .internal} or [[`runspider`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
    .tooltip .reference .internal} commands, you can use the
    [`-O`{.docutils .literal .notranslate}]{.pre} option instead of
    [`-o`{.docutils .literal .notranslate}]{.pre} to overwrite the
    output file.

-   Zstd-compressed responses are now supported if
    [zstandard](https://pypi.org/project/zstandard/){.reference
    .external} is installed.

-   In settings, where the import path of a class is required, it is now
    possible to pass a class object instead.

::: {#id43 .section}
##### Modified requirements[¶](#id43 "Permalink to this heading"){.headerlink}

-   Python 3.6 or greater is now required; support for Python 3.5 has
    been dropped

    As a result:

    -   When using PyPy, PyPy 7.2.0 or greater [[is now required]{.std
        .std-ref}](index.html#faq-python-versions){.hoverxref .tooltip
        .reference .internal}

    -   For Amazon S3 storage support in [[feed exports]{.std
        .std-ref}](index.html#topics-feed-storage-s3){.hoverxref
        .tooltip .reference .internal} or [[media pipelines]{.std
        .std-ref}](index.html#media-pipelines-s3){.hoverxref .tooltip
        .reference .internal},
        [botocore](https://github.com/boto/botocore){.reference
        .external} 1.4.87 or greater is now required

    -   To use the [[images pipeline]{.std
        .std-ref}](index.html#images-pipeline){.hoverxref .tooltip
        .reference .internal},
        [Pillow](https://python-pillow.org/){.reference .external} 4.0.0
        or greater is now required

    ([issue
    4718](https://github.com/scrapy/scrapy/issues/4718){.reference
    .external}, [issue
    4732](https://github.com/scrapy/scrapy/issues/4732){.reference
    .external}, [issue
    4733](https://github.com/scrapy/scrapy/issues/4733){.reference
    .external}, [issue
    4742](https://github.com/scrapy/scrapy/issues/4742){.reference
    .external}, [issue
    4743](https://github.com/scrapy/scrapy/issues/4743){.reference
    .external}, [issue
    4764](https://github.com/scrapy/scrapy/issues/4764){.reference
    .external})
:::

::: {#id44 .section}
##### Backward-incompatible changes[¶](#id44 "Permalink to this heading"){.headerlink}

-   [[`CookiesMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.cookies.CookiesMiddleware "scrapy.downloadermiddlewares.cookies.CookiesMiddleware"){.reference
    .internal} once again discards cookies defined in
    [[`Request.headers`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.headers "scrapy.http.Request.headers"){.reference
    .internal}.

    We decided to revert this bug fix, introduced in Scrapy 2.2.0,
    because it was reported that the current implementation could break
    existing code.

    If you need to set cookies for a request, use the
    [[`Request.cookies`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} parameter.

    A future version of Scrapy will include a new, better implementation
    of the reverted bug fix.

    ([issue
    4717](https://github.com/scrapy/scrapy/issues/4717){.reference
    .external}, [issue
    4823](https://github.com/scrapy/scrapy/issues/4823){.reference
    .external})
:::

::: {#id45 .section}
[]{#id46}

##### Deprecation removals[¶](#id45 "Permalink to this heading"){.headerlink}

-   [`scrapy.extensions.feedexport.S3FeedStorage`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} no longer reads the values
    of [`access_key`{.docutils .literal .notranslate}]{.pre} and
    [`secret_key`{.docutils .literal .notranslate}]{.pre} from the
    running project settings when they are not passed to its
    [`__init__`{.docutils .literal .notranslate}]{.pre} method; you must
    either pass those parameters to its [`__init__`{.docutils .literal
    .notranslate}]{.pre} method or use
    [`S3FeedStorage.from_crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} ([issue
    4356](https://github.com/scrapy/scrapy/issues/4356){.reference
    .external}, [issue
    4411](https://github.com/scrapy/scrapy/issues/4411){.reference
    .external}, [issue
    4688](https://github.com/scrapy/scrapy/issues/4688){.reference
    .external})

-   [`Rule.process_request`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} no longer admits callables which expect a
    single [`request`{.docutils .literal .notranslate}]{.pre} parameter,
    rather than both [`request`{.docutils .literal .notranslate}]{.pre}
    and [`response`{.docutils .literal .notranslate}]{.pre} ([issue
    4818](https://github.com/scrapy/scrapy/issues/4818){.reference
    .external})
:::

::: {#id47 .section}
##### Deprecations[¶](#id47 "Permalink to this heading"){.headerlink}

-   In custom [[media pipelines]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal}, signatures that do not accept a keyword-only
    [`item`{.docutils .literal .notranslate}]{.pre} parameter in any of
    the methods that [[now support this parameter]{.std
    .std-ref}](#media-pipeline-item-parameter){.hoverxref .tooltip
    .reference .internal} are now deprecated ([issue
    4628](https://github.com/scrapy/scrapy/issues/4628){.reference
    .external}, [issue
    4686](https://github.com/scrapy/scrapy/issues/4686){.reference
    .external})

-   In custom [[feed storage backend classes]{.std
    .std-ref}](index.html#topics-feed-storage){.hoverxref .tooltip
    .reference .internal}, [`__init__`{.docutils .literal
    .notranslate}]{.pre} method signatures that do not accept a
    keyword-only [`feed_options`{.docutils .literal .notranslate}]{.pre}
    parameter are now deprecated ([issue
    547](https://github.com/scrapy/scrapy/issues/547){.reference
    .external}, [issue
    716](https://github.com/scrapy/scrapy/issues/716){.reference
    .external}, [issue
    4512](https://github.com/scrapy/scrapy/issues/4512){.reference
    .external})

-   The [`scrapy.utils.python.WeakKeyCache`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} class is now deprecated
    ([issue
    4684](https://github.com/scrapy/scrapy/issues/4684){.reference
    .external}, [issue
    4701](https://github.com/scrapy/scrapy/issues/4701){.reference
    .external})

-   The [`scrapy.utils.boto.is_botocore()`{.xref .py .py-func .docutils
    .literal .notranslate}]{.pre} function is now deprecated, use
    [`scrapy.utils.boto.is_botocore_available()`{.xref .py .py-func
    .docutils .literal .notranslate}]{.pre} instead ([issue
    4734](https://github.com/scrapy/scrapy/issues/4734){.reference
    .external}, [issue
    4776](https://github.com/scrapy/scrapy/issues/4776){.reference
    .external})
:::

::: {#id48 .section}
##### New features[¶](#id48 "Permalink to this heading"){.headerlink}

-   The following methods of [[media pipelines]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal} now accept an [`item`{.docutils .literal
    .notranslate}]{.pre} keyword-only parameter containing the source
    [[item]{.std .std-ref}](index.html#topics-items){.hoverxref .tooltip
    .reference .internal}:

    -   In [[`scrapy.pipelines.files.FilesPipeline`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.pipelines.files.FilesPipeline "scrapy.pipelines.files.FilesPipeline"){.reference
        .internal}:

        -   [`file_downloaded()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [[`file_path()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.pipelines.files.FilesPipeline.file_path "scrapy.pipelines.files.FilesPipeline.file_path"){.reference
            .internal}

        -   [`media_downloaded()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [`media_to_download()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

    -   In [[`scrapy.pipelines.images.ImagesPipeline`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline "scrapy.pipelines.images.ImagesPipeline"){.reference
        .internal}:

        -   [`file_downloaded()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [[`file_path()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline.file_path "scrapy.pipelines.images.ImagesPipeline.file_path"){.reference
            .internal}

        -   [`get_images()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [`image_downloaded()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [`media_downloaded()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

        -   [`media_to_download()`{.xref .py .py-meth .docutils .literal
            .notranslate}]{.pre}

    ([issue
    4628](https://github.com/scrapy/scrapy/issues/4628){.reference
    .external}, [issue
    4686](https://github.com/scrapy/scrapy/issues/4686){.reference
    .external})

-   The new [`item_export_kwargs`{.docutils .literal
    .notranslate}]{.pre} key of the [[`FEEDS`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} setting allows to define keyword
    parameters to pass to [[item exporter classes]{.std
    .std-ref}](index.html#topics-exporters){.hoverxref .tooltip
    .reference .internal} ([issue
    4606](https://github.com/scrapy/scrapy/issues/4606){.reference
    .external}, [issue
    4768](https://github.com/scrapy/scrapy/issues/4768){.reference
    .external})

-   [[Feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} gained overwrite support:

    -   When using the [[`crawl`{.xref .std .std-command .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref
        .tooltip .reference .internal} or [[`runspider`{.xref .std
        .std-command .docutils .literal
        .notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
        .tooltip .reference .internal} commands, you can use the
        [`-O`{.docutils .literal .notranslate}]{.pre} option instead of
        [`-o`{.docutils .literal .notranslate}]{.pre} to overwrite the
        output file

    -   You can use the [`overwrite`{.docutils .literal
        .notranslate}]{.pre} key in the [[`FEEDS`{.xref .std
        .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
        .tooltip .reference .internal} setting to configure whether to
        overwrite the output file ([`True`{.docutils .literal
        .notranslate}]{.pre}) or append to its content
        ([`False`{.docutils .literal .notranslate}]{.pre})

    -   The [`__init__`{.docutils .literal .notranslate}]{.pre} and
        [`from_crawler`{.docutils .literal .notranslate}]{.pre} methods
        of [[feed storage backend classes]{.std
        .std-ref}](index.html#topics-feed-storage){.hoverxref .tooltip
        .reference .internal} now receive a new keyword-only parameter,
        [`feed_options`{.docutils .literal .notranslate}]{.pre}, which
        is a dictionary of [[feed options]{.std
        .std-ref}](index.html#feed-options){.hoverxref .tooltip
        .reference .internal}

    ([issue 547](https://github.com/scrapy/scrapy/issues/547){.reference
    .external}, [issue
    716](https://github.com/scrapy/scrapy/issues/716){.reference
    .external}, [issue
    4512](https://github.com/scrapy/scrapy/issues/4512){.reference
    .external})

-   Zstd-compressed responses are now supported if
    [zstandard](https://pypi.org/project/zstandard/){.reference
    .external} is installed ([issue
    4831](https://github.com/scrapy/scrapy/issues/4831){.reference
    .external})

-   In settings, where the import path of a class is required, it is now
    possible to pass a class object instead ([issue
    3870](https://github.com/scrapy/scrapy/issues/3870){.reference
    .external}, [issue
    3873](https://github.com/scrapy/scrapy/issues/3873){.reference
    .external}).

    This includes also settings where only part of its value is made of
    an import path, such as [[`DOWNLOADER_MIDDLEWARES`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES){.hoverxref
    .tooltip .reference .internal} or [[`DOWNLOAD_HANDLERS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal}.

-   [[Downloader middlewares]{.std
    .std-ref}](index.html#topics-downloader-middleware){.hoverxref
    .tooltip .reference .internal} can now override
    [[`response.request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.request "scrapy.http.Response.request"){.reference
    .internal}.

    If a [[downloader middleware]{.std
    .std-ref}](index.html#topics-downloader-middleware){.hoverxref
    .tooltip .reference .internal} returns a [[`Response`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} object from [[`process_response()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.DownloaderMiddleware.process_response "scrapy.downloadermiddlewares.DownloaderMiddleware.process_response"){.reference
    .internal} or [[`process_exception()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception "scrapy.downloadermiddlewares.DownloaderMiddleware.process_exception"){.reference
    .internal} with a custom [[`Request`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object assigned to [[`response.request`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.request "scrapy.http.Response.request"){.reference
    .internal}:

    -   The response is handled by the callback of that custom
        [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object, instead of being handled by the callback of
        the original [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object

    -   That custom [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object is now sent as the [`request`{.docutils
        .literal .notranslate}]{.pre} argument to the
        [[`response_received`{.xref .std .std-signal .docutils .literal
        .notranslate}]{.pre}](index.html#std-signal-response_received){.hoverxref
        .tooltip .reference .internal} signal, instead of the original
        [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object

    ([issue
    4529](https://github.com/scrapy/scrapy/issues/4529){.reference
    .external}, [issue
    4632](https://github.com/scrapy/scrapy/issues/4632){.reference
    .external})

-   When using the [[FTP feed storage backend]{.std
    .std-ref}](index.html#topics-feed-storage-ftp){.hoverxref .tooltip
    .reference .internal}:

    -   It is now possible to set the new [`overwrite`{.docutils
        .literal .notranslate}]{.pre} [[feed option]{.std
        .std-ref}](index.html#feed-options){.hoverxref .tooltip
        .reference .internal} to [`False`{.docutils .literal
        .notranslate}]{.pre} to append to an existing file instead of
        overwriting it

    -   The FTP password can now be omitted if it is not necessary

    ([issue 547](https://github.com/scrapy/scrapy/issues/547){.reference
    .external}, [issue
    716](https://github.com/scrapy/scrapy/issues/716){.reference
    .external}, [issue
    4512](https://github.com/scrapy/scrapy/issues/4512){.reference
    .external})

-   The [`__init__`{.docutils .literal .notranslate}]{.pre} method of
    [[`CsvItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.CsvItemExporter "scrapy.exporters.CsvItemExporter"){.reference
    .internal} now supports an [`errors`{.docutils .literal
    .notranslate}]{.pre} parameter to indicate how to handle encoding
    errors ([issue
    4755](https://github.com/scrapy/scrapy/issues/4755){.reference
    .external})

-   When [[using asyncio]{.std
    .std-ref}](index.html#using-asyncio){.hoverxref .tooltip .reference
    .internal}, it is now possible to [[set a custom asyncio loop]{.std
    .std-ref}](index.html#using-custom-loops){.hoverxref .tooltip
    .reference .internal} ([issue
    4306](https://github.com/scrapy/scrapy/issues/4306){.reference
    .external}, [issue
    4414](https://github.com/scrapy/scrapy/issues/4414){.reference
    .external})

-   Serialized requests (see [[Jobs: pausing and resuming crawls]{.std
    .std-ref}](index.html#topics-jobs){.hoverxref .tooltip .reference
    .internal}) now support callbacks that are spider methods that
    delegate on other callable ([issue
    4756](https://github.com/scrapy/scrapy/issues/4756){.reference
    .external})

-   When a response is larger than [[`DOWNLOAD_MAXSIZE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_MAXSIZE){.hoverxref
    .tooltip .reference .internal}, the logged message is now a warning,
    instead of an error ([issue
    3874](https://github.com/scrapy/scrapy/issues/3874){.reference
    .external}, [issue
    3886](https://github.com/scrapy/scrapy/issues/3886){.reference
    .external}, [issue
    4752](https://github.com/scrapy/scrapy/issues/4752){.reference
    .external})
:::

::: {#id49 .section}
##### Bug fixes[¶](#id49 "Permalink to this heading"){.headerlink}

-   The [[`genspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-genspider){.hoverxref
    .tooltip .reference .internal} command no longer overwrites existing
    files unless the [`--force`{.docutils .literal .notranslate}]{.pre}
    option is used ([issue
    4561](https://github.com/scrapy/scrapy/issues/4561){.reference
    .external}, [issue
    4616](https://github.com/scrapy/scrapy/issues/4616){.reference
    .external}, [issue
    4623](https://github.com/scrapy/scrapy/issues/4623){.reference
    .external})

-   Cookies with an empty value are no longer considered invalid cookies
    ([issue
    4772](https://github.com/scrapy/scrapy/issues/4772){.reference
    .external})

-   The [[`runspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
    .tooltip .reference .internal} command now supports files with the
    [`.pyw`{.docutils .literal .notranslate}]{.pre} file extension
    ([issue
    4643](https://github.com/scrapy/scrapy/issues/4643){.reference
    .external}, [issue
    4646](https://github.com/scrapy/scrapy/issues/4646){.reference
    .external})

-   The [[`HttpProxyMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware"){.reference
    .internal} middleware now simply ignores unsupported proxy values
    ([issue
    3331](https://github.com/scrapy/scrapy/issues/3331){.reference
    .external}, [issue
    4778](https://github.com/scrapy/scrapy/issues/4778){.reference
    .external})

-   Checks for generator callbacks with a [`return`{.docutils .literal
    .notranslate}]{.pre} statement no longer warn about
    [`return`{.docutils .literal .notranslate}]{.pre} statements in
    nested functions ([issue
    4720](https://github.com/scrapy/scrapy/issues/4720){.reference
    .external}, [issue
    4721](https://github.com/scrapy/scrapy/issues/4721){.reference
    .external})

-   The system file mode creation mask no longer affects the permissions
    of files generated using the [[`startproject`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} command ([issue
    4722](https://github.com/scrapy/scrapy/issues/4722){.reference
    .external})

-   [`scrapy.utils.iterators.xmliter()`{.xref .py .py-func .docutils
    .literal .notranslate}]{.pre} now supports namespaced node names
    ([issue 861](https://github.com/scrapy/scrapy/issues/861){.reference
    .external}, [issue
    4746](https://github.com/scrapy/scrapy/issues/4746){.reference
    .external})

-   [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} objects can now have [`about:`{.docutils
    .literal .notranslate}]{.pre} URLs, which can work when using a
    headless browser ([issue
    4835](https://github.com/scrapy/scrapy/issues/4835){.reference
    .external})
:::

::: {#id50 .section}
##### Documentation[¶](#id50 "Permalink to this heading"){.headerlink}

-   The [[`FEED_URI_PARAMS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_URI_PARAMS){.hoverxref
    .tooltip .reference .internal} setting is now documented ([issue
    4671](https://github.com/scrapy/scrapy/issues/4671){.reference
    .external}, [issue
    4724](https://github.com/scrapy/scrapy/issues/4724){.reference
    .external})

-   Improved the documentation of [[link extractors]{.std
    .std-ref}](index.html#topics-link-extractors){.hoverxref .tooltip
    .reference .internal} with an usage example from a spider callback
    and reference documentation for the [[`Link`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference
    .internal} class ([issue
    4751](https://github.com/scrapy/scrapy/issues/4751){.reference
    .external}, [issue
    4775](https://github.com/scrapy/scrapy/issues/4775){.reference
    .external})

-   Clarified the impact of [[`CONCURRENT_REQUESTS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS){.hoverxref
    .tooltip .reference .internal} when using the [[`CloseSpider`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.extensions.closespider.CloseSpider "scrapy.extensions.closespider.CloseSpider"){.reference
    .internal} extension ([issue
    4836](https://github.com/scrapy/scrapy/issues/4836){.reference
    .external})

-   Removed references to Python 2's [`unicode`{.docutils .literal
    .notranslate}]{.pre} type ([issue
    4547](https://github.com/scrapy/scrapy/issues/4547){.reference
    .external}, [issue
    4703](https://github.com/scrapy/scrapy/issues/4703){.reference
    .external})

-   We now have an [[official deprecation policy]{.std
    .std-ref}](index.html#deprecation-policy){.hoverxref .tooltip
    .reference .internal} ([issue
    4705](https://github.com/scrapy/scrapy/issues/4705){.reference
    .external})

-   Our [[documentation policies]{.std
    .std-ref}](index.html#documentation-policies){.hoverxref .tooltip
    .reference .internal} now cover usage of Sphinx's
    [[`versionadded`{.xref .rst .rst-dir .docutils .literal
    .notranslate}]{.pre}](https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#directive-versionadded "(in Sphinx v7.3.0)"){.reference
    .external} and [[`versionchanged`{.xref .rst .rst-dir .docutils
    .literal
    .notranslate}]{.pre}](https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#directive-versionchanged "(in Sphinx v7.3.0)"){.reference
    .external} directives, and we have removed usages referencing Scrapy
    1.4.0 and earlier versions ([issue
    3971](https://github.com/scrapy/scrapy/issues/3971){.reference
    .external}, [issue
    4310](https://github.com/scrapy/scrapy/issues/4310){.reference
    .external})

-   Other documentation cleanups ([issue
    4090](https://github.com/scrapy/scrapy/issues/4090){.reference
    .external}, [issue
    4782](https://github.com/scrapy/scrapy/issues/4782){.reference
    .external}, [issue
    4800](https://github.com/scrapy/scrapy/issues/4800){.reference
    .external}, [issue
    4801](https://github.com/scrapy/scrapy/issues/4801){.reference
    .external}, [issue
    4809](https://github.com/scrapy/scrapy/issues/4809){.reference
    .external}, [issue
    4816](https://github.com/scrapy/scrapy/issues/4816){.reference
    .external}, [issue
    4825](https://github.com/scrapy/scrapy/issues/4825){.reference
    .external})
:::

::: {#id51 .section}
##### Quality assurance[¶](#id51 "Permalink to this heading"){.headerlink}

-   Extended typing hints ([issue
    4243](https://github.com/scrapy/scrapy/issues/4243){.reference
    .external}, [issue
    4691](https://github.com/scrapy/scrapy/issues/4691){.reference
    .external})

-   Added tests for the [[`check`{.xref .std .std-command .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-command-check){.hoverxref
    .tooltip .reference .internal} command ([issue
    4663](https://github.com/scrapy/scrapy/issues/4663){.reference
    .external})

-   Fixed test failures on Debian ([issue
    4726](https://github.com/scrapy/scrapy/issues/4726){.reference
    .external}, [issue
    4727](https://github.com/scrapy/scrapy/issues/4727){.reference
    .external}, [issue
    4735](https://github.com/scrapy/scrapy/issues/4735){.reference
    .external})

-   Improved Windows test coverage ([issue
    4723](https://github.com/scrapy/scrapy/issues/4723){.reference
    .external})

-   Switched to [[formatted string literals]{.xref .std
    .std-ref}](https://docs.python.org/3/reference/lexical_analysis.html#f-strings "(in Python v3.12)"){.reference
    .external} where possible ([issue
    4307](https://github.com/scrapy/scrapy/issues/4307){.reference
    .external}, [issue
    4324](https://github.com/scrapy/scrapy/issues/4324){.reference
    .external}, [issue
    4672](https://github.com/scrapy/scrapy/issues/4672){.reference
    .external})

-   Modernized [`super()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre} usage ([issue
    4707](https://github.com/scrapy/scrapy/issues/4707){.reference
    .external})

-   Other code and test cleanups ([issue
    1790](https://github.com/scrapy/scrapy/issues/1790){.reference
    .external}, [issue
    3288](https://github.com/scrapy/scrapy/issues/3288){.reference
    .external}, [issue
    4165](https://github.com/scrapy/scrapy/issues/4165){.reference
    .external}, [issue
    4564](https://github.com/scrapy/scrapy/issues/4564){.reference
    .external}, [issue
    4651](https://github.com/scrapy/scrapy/issues/4651){.reference
    .external}, [issue
    4714](https://github.com/scrapy/scrapy/issues/4714){.reference
    .external}, [issue
    4738](https://github.com/scrapy/scrapy/issues/4738){.reference
    .external}, [issue
    4745](https://github.com/scrapy/scrapy/issues/4745){.reference
    .external}, [issue
    4747](https://github.com/scrapy/scrapy/issues/4747){.reference
    .external}, [issue
    4761](https://github.com/scrapy/scrapy/issues/4761){.reference
    .external}, [issue
    4765](https://github.com/scrapy/scrapy/issues/4765){.reference
    .external}, [issue
    4804](https://github.com/scrapy/scrapy/issues/4804){.reference
    .external}, [issue
    4817](https://github.com/scrapy/scrapy/issues/4817){.reference
    .external}, [issue
    4820](https://github.com/scrapy/scrapy/issues/4820){.reference
    .external}, [issue
    4822](https://github.com/scrapy/scrapy/issues/4822){.reference
    .external}, [issue
    4839](https://github.com/scrapy/scrapy/issues/4839){.reference
    .external})
:::
:::

::: {#scrapy-2-3-0-2020-08-04 .section}
[]{#release-2-3-0}

#### Scrapy 2.3.0 (2020-08-04)[¶](#scrapy-2-3-0-2020-08-04 "Permalink to this heading"){.headerlink}

Highlights:

-   [[Feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} now support [[Google Cloud Storage]{.std
    .std-ref}](index.html#topics-feed-storage-gcs){.hoverxref .tooltip
    .reference .internal} as a storage backend

-   The new [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
    .tooltip .reference .internal} setting allows to deliver output
    items in batches of up to the specified number of items.

    It also serves as a workaround for [[delayed file delivery]{.std
    .std-ref}](index.html#delayed-file-delivery){.hoverxref .tooltip
    .reference .internal}, which causes Scrapy to only start item
    delivery after the crawl has finished when using certain storage
    backends ([[S3]{.std
    .std-ref}](index.html#topics-feed-storage-s3){.hoverxref .tooltip
    .reference .internal}, [[FTP]{.std
    .std-ref}](index.html#topics-feed-storage-ftp){.hoverxref .tooltip
    .reference .internal}, and now [[GCS]{.std
    .std-ref}](index.html#topics-feed-storage-gcs){.hoverxref .tooltip
    .reference .internal}).

-   The base implementation of [[item loaders]{.std
    .std-ref}](index.html#topics-loaders){.hoverxref .tooltip .reference
    .internal} has been moved into a separate library,
    [[itemloaders]{.xref .std
    .std-doc}](https://itemloaders.readthedocs.io/en/latest/index.html "(in itemloaders)"){.reference
    .external}, allowing usage from outside Scrapy and a separate
    release schedule

::: {#id52 .section}
##### Deprecation removals[¶](#id52 "Permalink to this heading"){.headerlink}

-   Removed the following classes and their parent modules from
    [`scrapy.linkextractors`{.docutils .literal .notranslate}]{.pre}:

    -   [`htmlparser.HtmlParserLinkExtractor`{.docutils .literal
        .notranslate}]{.pre}

    -   [`regex.RegexLinkExtractor`{.docutils .literal
        .notranslate}]{.pre}

    -   [`sgml.BaseSgmlLinkExtractor`{.docutils .literal
        .notranslate}]{.pre}

    -   [`sgml.SgmlLinkExtractor`{.docutils .literal
        .notranslate}]{.pre}

    Use [[`LinkExtractor`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} instead ([issue
    4356](https://github.com/scrapy/scrapy/issues/4356){.reference
    .external}, [issue
    4679](https://github.com/scrapy/scrapy/issues/4679){.reference
    .external})
:::

::: {#id53 .section}
##### Deprecations[¶](#id53 "Permalink to this heading"){.headerlink}

-   The [`scrapy.utils.python.retry_on_eintr`{.docutils .literal
    .notranslate}]{.pre} function is now deprecated ([issue
    4683](https://github.com/scrapy/scrapy/issues/4683){.reference
    .external})
:::

::: {#id54 .section}
##### New features[¶](#id54 "Permalink to this heading"){.headerlink}

-   [[Feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} support [[Google Cloud Storage]{.std
    .std-ref}](index.html#topics-feed-storage-gcs){.hoverxref .tooltip
    .reference .internal} ([issue
    685](https://github.com/scrapy/scrapy/issues/685){.reference
    .external}, [issue
    3608](https://github.com/scrapy/scrapy/issues/3608){.reference
    .external})

-   New [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
    .tooltip .reference .internal} setting for batch deliveries ([issue
    4250](https://github.com/scrapy/scrapy/issues/4250){.reference
    .external}, [issue
    4434](https://github.com/scrapy/scrapy/issues/4434){.reference
    .external})

-   The [[`parse`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-parse){.hoverxref
    .tooltip .reference .internal} command now allows specifying an
    output file ([issue
    4317](https://github.com/scrapy/scrapy/issues/4317){.reference
    .external}, [issue
    4377](https://github.com/scrapy/scrapy/issues/4377){.reference
    .external})

-   [[`Request.from_curl`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.from_curl "scrapy.http.Request.from_curl"){.reference
    .internal} and [[`curl_to_request_kwargs()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.utils.curl.curl_to_request_kwargs "scrapy.utils.curl.curl_to_request_kwargs"){.reference
    .internal} now also support [`--data-raw`{.docutils .literal
    .notranslate}]{.pre} ([issue
    4612](https://github.com/scrapy/scrapy/issues/4612){.reference
    .external})

-   A [`parse`{.docutils .literal .notranslate}]{.pre} callback may now
    be used in built-in spider subclasses, such as [[`CrawlSpider`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.CrawlSpider "scrapy.spiders.CrawlSpider"){.reference
    .internal} ([issue
    712](https://github.com/scrapy/scrapy/issues/712){.reference
    .external}, [issue
    732](https://github.com/scrapy/scrapy/issues/732){.reference
    .external}, [issue
    781](https://github.com/scrapy/scrapy/issues/781){.reference
    .external}, [issue
    4254](https://github.com/scrapy/scrapy/issues/4254){.reference
    .external} )
:::

::: {#id55 .section}
##### Bug fixes[¶](#id55 "Permalink to this heading"){.headerlink}

-   Fixed the [[CSV exporting]{.std
    .std-ref}](index.html#topics-feed-format-csv){.hoverxref .tooltip
    .reference .internal} of [[dataclass items]{.std
    .std-ref}](index.html#dataclass-items){.hoverxref .tooltip
    .reference .internal} and [[attr.s items]{.std
    .std-ref}](index.html#attrs-items){.hoverxref .tooltip .reference
    .internal} ([issue
    4667](https://github.com/scrapy/scrapy/issues/4667){.reference
    .external}, [issue
    4668](https://github.com/scrapy/scrapy/issues/4668){.reference
    .external})

-   [[`Request.from_curl`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.from_curl "scrapy.http.Request.from_curl"){.reference
    .internal} and [[`curl_to_request_kwargs()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.utils.curl.curl_to_request_kwargs "scrapy.utils.curl.curl_to_request_kwargs"){.reference
    .internal} now set the request method to [`POST`{.docutils .literal
    .notranslate}]{.pre} when a request body is specified and no request
    method is specified ([issue
    4612](https://github.com/scrapy/scrapy/issues/4612){.reference
    .external})

-   The processing of ANSI escape sequences in enabled in Windows
    10.0.14393 and later, where it is required for colored output
    ([issue
    4393](https://github.com/scrapy/scrapy/issues/4393){.reference
    .external}, [issue
    4403](https://github.com/scrapy/scrapy/issues/4403){.reference
    .external})
:::

::: {#id56 .section}
##### Documentation[¶](#id56 "Permalink to this heading"){.headerlink}

-   Updated the [OpenSSL cipher list
    format](https://www.openssl.org/docs/manmaster/man1/openssl-ciphers.html#CIPHER-LIST-FORMAT){.reference
    .external} link in the documentation about the
    [[`DOWNLOADER_CLIENT_TLS_CIPHERS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENT_TLS_CIPHERS){.hoverxref
    .tooltip .reference .internal} setting ([issue
    4653](https://github.com/scrapy/scrapy/issues/4653){.reference
    .external})

-   Simplified the code example in [[Working with dataclass items]{.std
    .std-ref}](index.html#topics-loaders-dataclass){.hoverxref .tooltip
    .reference .internal} ([issue
    4652](https://github.com/scrapy/scrapy/issues/4652){.reference
    .external})
:::

::: {#id57 .section}
##### Quality assurance[¶](#id57 "Permalink to this heading"){.headerlink}

-   The base implementation of [[item loaders]{.std
    .std-ref}](index.html#topics-loaders){.hoverxref .tooltip .reference
    .internal} has been moved into [[itemloaders]{.xref .std
    .std-doc}](https://itemloaders.readthedocs.io/en/latest/index.html "(in itemloaders)"){.reference
    .external} ([issue
    4005](https://github.com/scrapy/scrapy/issues/4005){.reference
    .external}, [issue
    4516](https://github.com/scrapy/scrapy/issues/4516){.reference
    .external})

-   Fixed a silenced error in some scheduler tests ([issue
    4644](https://github.com/scrapy/scrapy/issues/4644){.reference
    .external}, [issue
    4645](https://github.com/scrapy/scrapy/issues/4645){.reference
    .external})

-   Renewed the localhost certificate used for SSL tests ([issue
    4650](https://github.com/scrapy/scrapy/issues/4650){.reference
    .external})

-   Removed cookie-handling code specific to Python 2 ([issue
    4682](https://github.com/scrapy/scrapy/issues/4682){.reference
    .external})

-   Stopped using Python 2 unicode literal syntax ([issue
    4704](https://github.com/scrapy/scrapy/issues/4704){.reference
    .external})

-   Stopped using a backlash for line continuation ([issue
    4673](https://github.com/scrapy/scrapy/issues/4673){.reference
    .external})

-   Removed unneeded entries from the MyPy exception list ([issue
    4690](https://github.com/scrapy/scrapy/issues/4690){.reference
    .external})

-   Automated tests now pass on Windows as part of our continuous
    integration system ([issue
    4458](https://github.com/scrapy/scrapy/issues/4458){.reference
    .external})

-   Automated tests now pass on the latest PyPy version for supported
    Python versions in our continuous integration system ([issue
    4504](https://github.com/scrapy/scrapy/issues/4504){.reference
    .external})
:::
:::

::: {#scrapy-2-2-1-2020-07-17 .section}
[]{#release-2-2-1}

#### Scrapy 2.2.1 (2020-07-17)[¶](#scrapy-2-2-1-2020-07-17 "Permalink to this heading"){.headerlink}

-   The [[`startproject`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} command no longer makes unintended
    changes to the permissions of files in the destination folder, such
    as removing execution permissions ([issue
    4662](https://github.com/scrapy/scrapy/issues/4662){.reference
    .external}, [issue
    4666](https://github.com/scrapy/scrapy/issues/4666){.reference
    .external})
:::

::: {#scrapy-2-2-0-2020-06-24 .section}
[]{#release-2-2-0}

#### Scrapy 2.2.0 (2020-06-24)[¶](#scrapy-2-2-0-2020-06-24 "Permalink to this heading"){.headerlink}

Highlights:

-   Python 3.5.2+ is required now

-   [[dataclass objects]{.std
    .std-ref}](index.html#dataclass-items){.hoverxref .tooltip
    .reference .internal} and [[attrs objects]{.std
    .std-ref}](index.html#attrs-items){.hoverxref .tooltip .reference
    .internal} are now valid [[item types]{.std
    .std-ref}](index.html#item-types){.hoverxref .tooltip .reference
    .internal}

-   New [[`TextResponse.json`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.json "scrapy.http.TextResponse.json"){.reference
    .internal} method

-   New [[`bytes_received`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-bytes_received){.hoverxref
    .tooltip .reference .internal} signal that allows canceling response
    download

-   [[`CookiesMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.cookies.CookiesMiddleware "scrapy.downloadermiddlewares.cookies.CookiesMiddleware"){.reference
    .internal} fixes

::: {#id58 .section}
##### Backward-incompatible changes[¶](#id58 "Permalink to this heading"){.headerlink}

-   Support for Python 3.5.0 and 3.5.1 has been dropped; Scrapy now
    refuses to run with a Python version lower than 3.5.2, which
    introduced [[`typing.Type`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/typing.html#typing.Type "(in Python v3.12)"){.reference
    .external} ([issue
    4615](https://github.com/scrapy/scrapy/issues/4615){.reference
    .external})
:::

::: {#id59 .section}
##### Deprecations[¶](#id59 "Permalink to this heading"){.headerlink}

-   [`TextResponse.body_as_unicode`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre} is now deprecated, use
    [[`TextResponse.text`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.text "scrapy.http.TextResponse.text"){.reference
    .internal} instead ([issue
    4546](https://github.com/scrapy/scrapy/issues/4546){.reference
    .external}, [issue
    4555](https://github.com/scrapy/scrapy/issues/4555){.reference
    .external}, [issue
    4579](https://github.com/scrapy/scrapy/issues/4579){.reference
    .external})

-   [`scrapy.item.BaseItem`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} is now deprecated, use
    [`scrapy.item.Item`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} instead ([issue
    4534](https://github.com/scrapy/scrapy/issues/4534){.reference
    .external})
:::

::: {#id60 .section}
##### New features[¶](#id60 "Permalink to this heading"){.headerlink}

-   [[dataclass objects]{.std
    .std-ref}](index.html#dataclass-items){.hoverxref .tooltip
    .reference .internal} and [[attrs objects]{.std
    .std-ref}](index.html#attrs-items){.hoverxref .tooltip .reference
    .internal} are now valid [[item types]{.std
    .std-ref}](index.html#item-types){.hoverxref .tooltip .reference
    .internal}, and a new
    [itemadapter](https://github.com/scrapy/itemadapter){.reference
    .external} library makes it easy to write code that [[supports any
    item type]{.std
    .std-ref}](index.html#supporting-item-types){.hoverxref .tooltip
    .reference .internal} ([issue
    2749](https://github.com/scrapy/scrapy/issues/2749){.reference
    .external}, [issue
    2807](https://github.com/scrapy/scrapy/issues/2807){.reference
    .external}, [issue
    3761](https://github.com/scrapy/scrapy/issues/3761){.reference
    .external}, [issue
    3881](https://github.com/scrapy/scrapy/issues/3881){.reference
    .external}, [issue
    4642](https://github.com/scrapy/scrapy/issues/4642){.reference
    .external})

-   A new [[`TextResponse.json`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.json "scrapy.http.TextResponse.json"){.reference
    .internal} method allows to deserialize JSON responses ([issue
    2444](https://github.com/scrapy/scrapy/issues/2444){.reference
    .external}, [issue
    4460](https://github.com/scrapy/scrapy/issues/4460){.reference
    .external}, [issue
    4574](https://github.com/scrapy/scrapy/issues/4574){.reference
    .external})

-   A new [[`bytes_received`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-bytes_received){.hoverxref
    .tooltip .reference .internal} signal allows monitoring response
    download progress and [[stopping downloads]{.std
    .std-ref}](index.html#topics-stop-response-download){.hoverxref
    .tooltip .reference .internal} ([issue
    4205](https://github.com/scrapy/scrapy/issues/4205){.reference
    .external}, [issue
    4559](https://github.com/scrapy/scrapy/issues/4559){.reference
    .external})

-   The dictionaries in the result list of a [[media pipeline]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal} now include a new key, [`status`{.docutils
    .literal .notranslate}]{.pre}, which indicates if the file was
    downloaded or, if the file was not downloaded, why it was not
    downloaded; see [[`FilesPipeline.get_media_requests`{.xref .py
    .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.files.FilesPipeline.get_media_requests "scrapy.pipelines.files.FilesPipeline.get_media_requests"){.reference
    .internal} for more information ([issue
    2893](https://github.com/scrapy/scrapy/issues/2893){.reference
    .external}, [issue
    4486](https://github.com/scrapy/scrapy/issues/4486){.reference
    .external})

-   When using [[Google Cloud Storage]{.std
    .std-ref}](index.html#media-pipeline-gcs){.hoverxref .tooltip
    .reference .internal} for a [[media pipeline]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal}, a warning is now logged if the configured
    credentials do not grant the required permissions ([issue
    4346](https://github.com/scrapy/scrapy/issues/4346){.reference
    .external}, [issue
    4508](https://github.com/scrapy/scrapy/issues/4508){.reference
    .external})

-   [[Link extractors]{.std
    .std-ref}](index.html#topics-link-extractors){.hoverxref .tooltip
    .reference .internal} are now serializable, as long as you do not
    use [[lambdas]{.xref .std
    .std-ref}](https://docs.python.org/3/reference/expressions.html#lambda "(in Python v3.12)"){.reference
    .external} for parameters; for example, you can now pass link
    extractors in [[`Request.cb_kwargs`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
    .internal} or [[`Request.meta`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
    .internal} when [[persisting scheduled requests]{.std
    .std-ref}](index.html#topics-jobs){.hoverxref .tooltip .reference
    .internal} ([issue
    4554](https://github.com/scrapy/scrapy/issues/4554){.reference
    .external})

-   Upgraded the [[pickle protocol]{.xref .std
    .std-ref}](https://docs.python.org/3/library/pickle.html#pickle-protocols "(in Python v3.12)"){.reference
    .external} that Scrapy uses from protocol 2 to protocol 4, improving
    serialization capabilities and performance ([issue
    4135](https://github.com/scrapy/scrapy/issues/4135){.reference
    .external}, [issue
    4541](https://github.com/scrapy/scrapy/issues/4541){.reference
    .external})

-   [`scrapy.utils.misc.create_instance()`{.xref .py .py-func .docutils
    .literal .notranslate}]{.pre} now raises a [[`TypeError`{.xref .py
    .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#TypeError "(in Python v3.12)"){.reference
    .external} exception if the resulting instance is [`None`{.docutils
    .literal .notranslate}]{.pre} ([issue
    4528](https://github.com/scrapy/scrapy/issues/4528){.reference
    .external}, [issue
    4532](https://github.com/scrapy/scrapy/issues/4532){.reference
    .external})
:::

::: {#id61 .section}
##### Bug fixes[¶](#id61 "Permalink to this heading"){.headerlink}

-   [[`CookiesMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.cookies.CookiesMiddleware "scrapy.downloadermiddlewares.cookies.CookiesMiddleware"){.reference
    .internal} no longer discards cookies defined in
    [[`Request.headers`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.headers "scrapy.http.Request.headers"){.reference
    .internal} ([issue
    1992](https://github.com/scrapy/scrapy/issues/1992){.reference
    .external}, [issue
    2400](https://github.com/scrapy/scrapy/issues/2400){.reference
    .external})

-   [[`CookiesMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.cookies.CookiesMiddleware "scrapy.downloadermiddlewares.cookies.CookiesMiddleware"){.reference
    .internal} no longer re-encodes cookies defined as [[`bytes`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
    .external} in the [`cookies`{.docutils .literal .notranslate}]{.pre}
    parameter of the [`__init__`{.docutils .literal .notranslate}]{.pre}
    method of [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} ([issue
    2400](https://github.com/scrapy/scrapy/issues/2400){.reference
    .external}, [issue
    3575](https://github.com/scrapy/scrapy/issues/3575){.reference
    .external})

-   When [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} defines multiple URIs,
    [[`FEED_STORE_EMPTY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_STORE_EMPTY){.hoverxref
    .tooltip .reference .internal} is [`False`{.docutils .literal
    .notranslate}]{.pre} and the crawl yields no items, Scrapy no longer
    stops feed exports after the first URI ([issue
    4621](https://github.com/scrapy/scrapy/issues/4621){.reference
    .external}, [issue
    4626](https://github.com/scrapy/scrapy/issues/4626){.reference
    .external})

-   [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} callbacks defined using [[coroutine
    syntax]{.doc}](index.html#document-topics/coroutines){.reference
    .internal} no longer need to return an iterable, and may instead
    return a [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} object, an [[item]{.std
    .std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
    .internal}, or [`None`{.docutils .literal .notranslate}]{.pre}
    ([issue
    4609](https://github.com/scrapy/scrapy/issues/4609){.reference
    .external})

-   The [[`startproject`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} command now ensures that the
    generated project folders and files have the right permissions
    ([issue
    4604](https://github.com/scrapy/scrapy/issues/4604){.reference
    .external})

-   Fix a [[`KeyError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#KeyError "(in Python v3.12)"){.reference
    .external} exception being sometimes raised from
    [`scrapy.utils.datatypes.LocalWeakReferencedCache`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} ([issue
    4597](https://github.com/scrapy/scrapy/issues/4597){.reference
    .external}, [issue
    4599](https://github.com/scrapy/scrapy/issues/4599){.reference
    .external})

-   When [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} defines multiple URIs, log messages
    about items being stored now contain information from the
    corresponding feed, instead of always containing information about
    only one of the feeds ([issue
    4619](https://github.com/scrapy/scrapy/issues/4619){.reference
    .external}, [issue
    4629](https://github.com/scrapy/scrapy/issues/4629){.reference
    .external})
:::

::: {#id62 .section}
##### Documentation[¶](#id62 "Permalink to this heading"){.headerlink}

-   Added a new section about [[accessing cb_kwargs from errbacks]{.std
    .std-ref}](index.html#errback-cb-kwargs){.hoverxref .tooltip
    .reference .internal} ([issue
    4598](https://github.com/scrapy/scrapy/issues/4598){.reference
    .external}, [issue
    4634](https://github.com/scrapy/scrapy/issues/4634){.reference
    .external})

-   Covered [chompjs](https://github.com/Nykakin/chompjs){.reference
    .external} in [[Parsing JavaScript code]{.std
    .std-ref}](index.html#topics-parsing-javascript){.hoverxref .tooltip
    .reference .internal} ([issue
    4556](https://github.com/scrapy/scrapy/issues/4556){.reference
    .external}, [issue
    4562](https://github.com/scrapy/scrapy/issues/4562){.reference
    .external})

-   Removed from
    [[Coroutines]{.doc}](index.html#document-topics/coroutines){.reference
    .internal} the warning about the API being experimental ([issue
    4511](https://github.com/scrapy/scrapy/issues/4511){.reference
    .external}, [issue
    4513](https://github.com/scrapy/scrapy/issues/4513){.reference
    .external})

-   Removed references to unsupported versions of [[Twisted]{.xref .std
    .std-doc}](https://docs.twisted.org/en/stable/index.html "(in Twisted v23.10)"){.reference
    .external} ([issue
    4533](https://github.com/scrapy/scrapy/issues/4533){.reference
    .external})

-   Updated the description of the [[screenshot pipeline example]{.std
    .std-ref}](index.html#screenshotpipeline){.hoverxref .tooltip
    .reference .internal}, which now uses [[coroutine
    syntax]{.doc}](index.html#document-topics/coroutines){.reference
    .internal} instead of returning a [[`Deferred`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
    .external} ([issue
    4514](https://github.com/scrapy/scrapy/issues/4514){.reference
    .external}, [issue
    4593](https://github.com/scrapy/scrapy/issues/4593){.reference
    .external})

-   Removed a misleading import line from the
    [[`scrapy.utils.log.configure_logging()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.utils.log.configure_logging "scrapy.utils.log.configure_logging"){.reference
    .internal} code example ([issue
    4510](https://github.com/scrapy/scrapy/issues/4510){.reference
    .external}, [issue
    4587](https://github.com/scrapy/scrapy/issues/4587){.reference
    .external})

-   The display-on-hover behavior of internal documentation references
    now also covers links to [[commands]{.std
    .std-ref}](index.html#topics-commands){.hoverxref .tooltip
    .reference .internal}, [[`Request.meta`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
    .internal} keys, [[settings]{.std
    .std-ref}](index.html#topics-settings){.hoverxref .tooltip
    .reference .internal} and [[signals]{.std
    .std-ref}](index.html#topics-signals){.hoverxref .tooltip .reference
    .internal} ([issue
    4495](https://github.com/scrapy/scrapy/issues/4495){.reference
    .external}, [issue
    4563](https://github.com/scrapy/scrapy/issues/4563){.reference
    .external})

-   It is again possible to download the documentation for offline
    reading ([issue
    4578](https://github.com/scrapy/scrapy/issues/4578){.reference
    .external}, [issue
    4585](https://github.com/scrapy/scrapy/issues/4585){.reference
    .external})

-   Removed backslashes preceding [`*args`{.docutils .literal
    .notranslate}]{.pre} and [`**kwargs`{.docutils .literal
    .notranslate}]{.pre} in some function and method signatures ([issue
    4592](https://github.com/scrapy/scrapy/issues/4592){.reference
    .external}, [issue
    4596](https://github.com/scrapy/scrapy/issues/4596){.reference
    .external})
:::

::: {#id63 .section}
##### Quality assurance[¶](#id63 "Permalink to this heading"){.headerlink}

-   Adjusted the code base further to our [[style guidelines]{.std
    .std-ref}](index.html#coding-style){.hoverxref .tooltip .reference
    .internal} ([issue
    4237](https://github.com/scrapy/scrapy/issues/4237){.reference
    .external}, [issue
    4525](https://github.com/scrapy/scrapy/issues/4525){.reference
    .external}, [issue
    4538](https://github.com/scrapy/scrapy/issues/4538){.reference
    .external}, [issue
    4539](https://github.com/scrapy/scrapy/issues/4539){.reference
    .external}, [issue
    4540](https://github.com/scrapy/scrapy/issues/4540){.reference
    .external}, [issue
    4542](https://github.com/scrapy/scrapy/issues/4542){.reference
    .external}, [issue
    4543](https://github.com/scrapy/scrapy/issues/4543){.reference
    .external}, [issue
    4544](https://github.com/scrapy/scrapy/issues/4544){.reference
    .external}, [issue
    4545](https://github.com/scrapy/scrapy/issues/4545){.reference
    .external}, [issue
    4557](https://github.com/scrapy/scrapy/issues/4557){.reference
    .external}, [issue
    4558](https://github.com/scrapy/scrapy/issues/4558){.reference
    .external}, [issue
    4566](https://github.com/scrapy/scrapy/issues/4566){.reference
    .external}, [issue
    4568](https://github.com/scrapy/scrapy/issues/4568){.reference
    .external}, [issue
    4572](https://github.com/scrapy/scrapy/issues/4572){.reference
    .external})

-   Removed remnants of Python 2 support ([issue
    4550](https://github.com/scrapy/scrapy/issues/4550){.reference
    .external}, [issue
    4553](https://github.com/scrapy/scrapy/issues/4553){.reference
    .external}, [issue
    4568](https://github.com/scrapy/scrapy/issues/4568){.reference
    .external})

-   Improved code sharing between the [[`crawl`{.xref .std .std-command
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref
    .tooltip .reference .internal} and [[`runspider`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
    .tooltip .reference .internal} commands ([issue
    4548](https://github.com/scrapy/scrapy/issues/4548){.reference
    .external}, [issue
    4552](https://github.com/scrapy/scrapy/issues/4552){.reference
    .external})

-   Replaced [`chain(*iterable)`{.docutils .literal .notranslate}]{.pre}
    with [`chain.from_iterable(iterable)`{.docutils .literal
    .notranslate}]{.pre} ([issue
    4635](https://github.com/scrapy/scrapy/issues/4635){.reference
    .external})

-   You may now run the [[`asyncio`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
    .external} tests with Tox on any Python version ([issue
    4521](https://github.com/scrapy/scrapy/issues/4521){.reference
    .external})

-   Updated test requirements to reflect an incompatibility with pytest
    5.4 and 5.4.1 ([issue
    4588](https://github.com/scrapy/scrapy/issues/4588){.reference
    .external})

-   Improved [[`SpiderLoader`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiderloader.SpiderLoader "scrapy.spiderloader.SpiderLoader"){.reference
    .internal} test coverage for scenarios involving duplicate spider
    names ([issue
    4549](https://github.com/scrapy/scrapy/issues/4549){.reference
    .external}, [issue
    4560](https://github.com/scrapy/scrapy/issues/4560){.reference
    .external})

-   Configured Travis CI to also run the tests with Python 3.5.2 ([issue
    4518](https://github.com/scrapy/scrapy/issues/4518){.reference
    .external}, [issue
    4615](https://github.com/scrapy/scrapy/issues/4615){.reference
    .external})

-   Added a [Pylint](https://www.pylint.org/){.reference .external} job
    to Travis CI ([issue
    3727](https://github.com/scrapy/scrapy/issues/3727){.reference
    .external})

-   Added a [Mypy](http://mypy-lang.org/){.reference .external} job to
    Travis CI ([issue
    4637](https://github.com/scrapy/scrapy/issues/4637){.reference
    .external})

-   Made use of set literals in tests ([issue
    4573](https://github.com/scrapy/scrapy/issues/4573){.reference
    .external})

-   Cleaned up the Travis CI configuration ([issue
    4517](https://github.com/scrapy/scrapy/issues/4517){.reference
    .external}, [issue
    4519](https://github.com/scrapy/scrapy/issues/4519){.reference
    .external}, [issue
    4522](https://github.com/scrapy/scrapy/issues/4522){.reference
    .external}, [issue
    4537](https://github.com/scrapy/scrapy/issues/4537){.reference
    .external})
:::
:::

::: {#scrapy-2-1-0-2020-04-24 .section}
[]{#release-2-1-0}

#### Scrapy 2.1.0 (2020-04-24)[¶](#scrapy-2-1-0-2020-04-24 "Permalink to this heading"){.headerlink}

Highlights:

-   New [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} setting to export to multiple feeds

-   New [[`Response.ip_address`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.ip_address "scrapy.http.Response.ip_address"){.reference
    .internal} attribute

::: {#id64 .section}
##### Backward-incompatible changes[¶](#id64 "Permalink to this heading"){.headerlink}

-   [[`AssertionError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#AssertionError "(in Python v3.12)"){.reference
    .external} exceptions triggered by [[assert]{.xref .std
    .std-ref}](https://docs.python.org/3/reference/simple_stmts.html#assert "(in Python v3.12)"){.reference
    .external} statements have been replaced by new exception types, to
    support running Python in optimized mode (see [[`-O`{.xref .std
    .std-option .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/using/cmdline.html#cmdoption-O "(in Python v3.12)"){.reference
    .external}) without changing Scrapy's behavior in any unexpected
    ways.

    If you catch an [[`AssertionError`{.xref .py .py-exc .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#AssertionError "(in Python v3.12)"){.reference
    .external} exception from Scrapy, update your code to catch the
    corresponding new exception.

    ([issue
    4440](https://github.com/scrapy/scrapy/issues/4440){.reference
    .external})
:::

::: {#id65 .section}
##### Deprecation removals[¶](#id65 "Permalink to this heading"){.headerlink}

-   The [`LOG_UNSERIALIZABLE_REQUESTS`{.docutils .literal
    .notranslate}]{.pre} setting is no longer supported, use
    [[`SCHEDULER_DEBUG`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DEBUG){.hoverxref
    .tooltip .reference .internal} instead ([issue
    4385](https://github.com/scrapy/scrapy/issues/4385){.reference
    .external})

-   The [`REDIRECT_MAX_METAREFRESH_DELAY`{.docutils .literal
    .notranslate}]{.pre} setting is no longer supported, use
    [[`METAREFRESH_MAXDELAY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-METAREFRESH_MAXDELAY){.hoverxref
    .tooltip .reference .internal} instead ([issue
    4385](https://github.com/scrapy/scrapy/issues/4385){.reference
    .external})

-   The [`ChunkedTransferMiddleware`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre} middleware has been removed, including
    the entire [`scrapy.downloadermiddlewares.chunked`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} module; chunked
    transfers work out of the box ([issue
    4431](https://github.com/scrapy/scrapy/issues/4431){.reference
    .external})

-   The [`spiders`{.docutils .literal .notranslate}]{.pre} property has
    been removed from [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal}, use [`CrawlerRunner.spider_loader`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} or instantiate
    [[`SPIDER_LOADER_CLASS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_LOADER_CLASS){.hoverxref
    .tooltip .reference .internal} with your settings instead ([issue
    4398](https://github.com/scrapy/scrapy/issues/4398){.reference
    .external})

-   The [`MultiValueDict`{.docutils .literal .notranslate}]{.pre},
    [`MultiValueDictKeyError`{.docutils .literal .notranslate}]{.pre},
    and [`SiteNode`{.docutils .literal .notranslate}]{.pre} classes have
    been removed from [`scrapy.utils.datatypes`{.xref .py .py-mod
    .docutils .literal .notranslate}]{.pre} ([issue
    4400](https://github.com/scrapy/scrapy/issues/4400){.reference
    .external})
:::

::: {#id66 .section}
##### Deprecations[¶](#id66 "Permalink to this heading"){.headerlink}

-   The [`FEED_FORMAT`{.docutils .literal .notranslate}]{.pre} and
    [`FEED_URI`{.docutils .literal .notranslate}]{.pre} settings have
    been deprecated in favor of the new [[`FEEDS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} setting ([issue
    1336](https://github.com/scrapy/scrapy/issues/1336){.reference
    .external}, [issue
    3858](https://github.com/scrapy/scrapy/issues/3858){.reference
    .external}, [issue
    4507](https://github.com/scrapy/scrapy/issues/4507){.reference
    .external})
:::

::: {#id67 .section}
##### New features[¶](#id67 "Permalink to this heading"){.headerlink}

-   A new setting, [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal}, allows configuring multiple output
    feeds with different settings each ([issue
    1336](https://github.com/scrapy/scrapy/issues/1336){.reference
    .external}, [issue
    3858](https://github.com/scrapy/scrapy/issues/3858){.reference
    .external}, [issue
    4507](https://github.com/scrapy/scrapy/issues/4507){.reference
    .external})

-   The [[`crawl`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref
    .tooltip .reference .internal} and [[`runspider`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
    .tooltip .reference .internal} commands now support multiple
    [`-o`{.docutils .literal .notranslate}]{.pre} parameters ([issue
    1336](https://github.com/scrapy/scrapy/issues/1336){.reference
    .external}, [issue
    3858](https://github.com/scrapy/scrapy/issues/3858){.reference
    .external}, [issue
    4507](https://github.com/scrapy/scrapy/issues/4507){.reference
    .external})

-   The [[`crawl`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref
    .tooltip .reference .internal} and [[`runspider`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
    .tooltip .reference .internal} commands now support specifying an
    output format by appending [`:<format>`{.docutils .literal
    .notranslate}]{.pre} to the output file ([issue
    1336](https://github.com/scrapy/scrapy/issues/1336){.reference
    .external}, [issue
    3858](https://github.com/scrapy/scrapy/issues/3858){.reference
    .external}, [issue
    4507](https://github.com/scrapy/scrapy/issues/4507){.reference
    .external})

-   The new [[`Response.ip_address`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.ip_address "scrapy.http.Response.ip_address"){.reference
    .internal} attribute gives access to the IP address that originated
    a response ([issue
    3903](https://github.com/scrapy/scrapy/issues/3903){.reference
    .external}, [issue
    3940](https://github.com/scrapy/scrapy/issues/3940){.reference
    .external})

-   A warning is now issued when a value in [`allowed_domains`{.xref .py
    .py-attr .docutils .literal .notranslate}]{.pre} includes a port
    ([issue 50](https://github.com/scrapy/scrapy/issues/50){.reference
    .external}, [issue
    3198](https://github.com/scrapy/scrapy/issues/3198){.reference
    .external}, [issue
    4413](https://github.com/scrapy/scrapy/issues/4413){.reference
    .external})

-   Zsh completion now excludes used option aliases from the completion
    list ([issue
    4438](https://github.com/scrapy/scrapy/issues/4438){.reference
    .external})
:::

::: {#id68 .section}
##### Bug fixes[¶](#id68 "Permalink to this heading"){.headerlink}

-   [[Request serialization]{.std
    .std-ref}](index.html#request-serialization){.hoverxref .tooltip
    .reference .internal} no longer breaks for callbacks that are spider
    attributes which are assigned a function with a different name
    ([issue
    4500](https://github.com/scrapy/scrapy/issues/4500){.reference
    .external})

-   [`None`{.docutils .literal .notranslate}]{.pre} values in
    [`allowed_domains`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} no longer cause a [[`TypeError`{.xref .py
    .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#TypeError "(in Python v3.12)"){.reference
    .external} exception ([issue
    4410](https://github.com/scrapy/scrapy/issues/4410){.reference
    .external})

-   Zsh completion no longer allows options after arguments ([issue
    4438](https://github.com/scrapy/scrapy/issues/4438){.reference
    .external})

-   zope.interface 5.0.0 and later versions are now supported ([issue
    4447](https://github.com/scrapy/scrapy/issues/4447){.reference
    .external}, [issue
    4448](https://github.com/scrapy/scrapy/issues/4448){.reference
    .external})

-   [`Spider.make_requests_from_url`{.docutils .literal
    .notranslate}]{.pre}, deprecated in Scrapy 1.4.0, now issues a
    warning when used ([issue
    4412](https://github.com/scrapy/scrapy/issues/4412){.reference
    .external})
:::

::: {#id69 .section}
##### Documentation[¶](#id69 "Permalink to this heading"){.headerlink}

-   Improved the documentation about signals that allow their handlers
    to return a [[`Deferred`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
    .external} ([issue
    4295](https://github.com/scrapy/scrapy/issues/4295){.reference
    .external}, [issue
    4390](https://github.com/scrapy/scrapy/issues/4390){.reference
    .external})

-   Our PyPI entry now includes links for our documentation, our source
    code repository and our issue tracker ([issue
    4456](https://github.com/scrapy/scrapy/issues/4456){.reference
    .external})

-   Covered the
    [curl2scrapy](https://michael-shub.github.io/curl2scrapy/){.reference
    .external} service in the documentation ([issue
    4206](https://github.com/scrapy/scrapy/issues/4206){.reference
    .external}, [issue
    4455](https://github.com/scrapy/scrapy/issues/4455){.reference
    .external})

-   Removed references to the Guppy library, which only works in Python
    2 ([issue
    4285](https://github.com/scrapy/scrapy/issues/4285){.reference
    .external}, [issue
    4343](https://github.com/scrapy/scrapy/issues/4343){.reference
    .external})

-   Extended use of InterSphinx to link to Python 3 documentation
    ([issue
    4444](https://github.com/scrapy/scrapy/issues/4444){.reference
    .external}, [issue
    4445](https://github.com/scrapy/scrapy/issues/4445){.reference
    .external})

-   Added support for Sphinx 3.0 and later ([issue
    4475](https://github.com/scrapy/scrapy/issues/4475){.reference
    .external}, [issue
    4480](https://github.com/scrapy/scrapy/issues/4480){.reference
    .external}, [issue
    4496](https://github.com/scrapy/scrapy/issues/4496){.reference
    .external}, [issue
    4503](https://github.com/scrapy/scrapy/issues/4503){.reference
    .external})
:::

::: {#id70 .section}
##### Quality assurance[¶](#id70 "Permalink to this heading"){.headerlink}

-   Removed warnings about using old, removed settings ([issue
    4404](https://github.com/scrapy/scrapy/issues/4404){.reference
    .external})

-   Removed a warning about importing [[`StringTransport`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.testing.StringTransport.html "(in Twisted)"){.reference
    .external} from [`twisted.test.proto_helpers`{.docutils .literal
    .notranslate}]{.pre} in Twisted 19.7.0 or newer ([issue
    4409](https://github.com/scrapy/scrapy/issues/4409){.reference
    .external})

-   Removed outdated Debian package build files ([issue
    4384](https://github.com/scrapy/scrapy/issues/4384){.reference
    .external})

-   Removed [[`object`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
    .external} usage as a base class ([issue
    4430](https://github.com/scrapy/scrapy/issues/4430){.reference
    .external})

-   Removed code that added support for old versions of Twisted that we
    no longer support ([issue
    4472](https://github.com/scrapy/scrapy/issues/4472){.reference
    .external})

-   Fixed code style issues ([issue
    4468](https://github.com/scrapy/scrapy/issues/4468){.reference
    .external}, [issue
    4469](https://github.com/scrapy/scrapy/issues/4469){.reference
    .external}, [issue
    4471](https://github.com/scrapy/scrapy/issues/4471){.reference
    .external}, [issue
    4481](https://github.com/scrapy/scrapy/issues/4481){.reference
    .external})

-   Removed [[`twisted.internet.defer.returnValue()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.html#returnValue "(in Twisted)"){.reference
    .external} calls ([issue
    4443](https://github.com/scrapy/scrapy/issues/4443){.reference
    .external}, [issue
    4446](https://github.com/scrapy/scrapy/issues/4446){.reference
    .external}, [issue
    4489](https://github.com/scrapy/scrapy/issues/4489){.reference
    .external})
:::
:::

::: {#scrapy-2-0-1-2020-03-18 .section}
[]{#release-2-0-1}

#### Scrapy 2.0.1 (2020-03-18)[¶](#scrapy-2-0-1-2020-03-18 "Permalink to this heading"){.headerlink}

-   [[`Response.follow_all`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.follow_all "scrapy.http.Response.follow_all"){.reference
    .internal} now supports an empty URL iterable as input ([issue
    4408](https://github.com/scrapy/scrapy/issues/4408){.reference
    .external}, [issue
    4420](https://github.com/scrapy/scrapy/issues/4420){.reference
    .external})

-   Removed top-level [[`reactor`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
    .external} imports to prevent errors about the wrong Twisted reactor
    being installed when setting a different Twisted reactor using
    [[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
    .tooltip .reference .internal} ([issue
    4401](https://github.com/scrapy/scrapy/issues/4401){.reference
    .external}, [issue
    4406](https://github.com/scrapy/scrapy/issues/4406){.reference
    .external})

-   Fixed tests ([issue
    4422](https://github.com/scrapy/scrapy/issues/4422){.reference
    .external})
:::

::: {#scrapy-2-0-0-2020-03-03 .section}
[]{#release-2-0-0}

#### Scrapy 2.0.0 (2020-03-03)[¶](#scrapy-2-0-0-2020-03-03 "Permalink to this heading"){.headerlink}

Highlights:

-   Python 2 support has been removed

-   [[Partial]{.doc}](index.html#document-topics/coroutines){.reference
    .internal} [[coroutine syntax]{.xref .std
    .std-ref}](https://docs.python.org/3/reference/compound_stmts.html#async "(in Python v3.12)"){.reference
    .external} support and
    [[experimental]{.doc}](index.html#document-topics/asyncio){.reference
    .internal} [[`asyncio`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
    .external} support

-   New [[`Response.follow_all`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.follow_all "scrapy.http.Response.follow_all"){.reference
    .internal} method

-   [[FTP support]{.std
    .std-ref}](index.html#media-pipeline-ftp){.hoverxref .tooltip
    .reference .internal} for media pipelines

-   New [[`Response.certificate`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.certificate "scrapy.http.Response.certificate"){.reference
    .internal} attribute

-   IPv6 support through [[`DNS_RESOLVER`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DNS_RESOLVER){.hoverxref
    .tooltip .reference .internal}

::: {#id71 .section}
##### Backward-incompatible changes[¶](#id71 "Permalink to this heading"){.headerlink}

-   Python 2 support has been removed, following [Python 2 end-of-life
    on January 1,
    2020](https://www.python.org/doc/sunset-python-2/){.reference
    .external} ([issue
    4091](https://github.com/scrapy/scrapy/issues/4091){.reference
    .external}, [issue
    4114](https://github.com/scrapy/scrapy/issues/4114){.reference
    .external}, [issue
    4115](https://github.com/scrapy/scrapy/issues/4115){.reference
    .external}, [issue
    4121](https://github.com/scrapy/scrapy/issues/4121){.reference
    .external}, [issue
    4138](https://github.com/scrapy/scrapy/issues/4138){.reference
    .external}, [issue
    4231](https://github.com/scrapy/scrapy/issues/4231){.reference
    .external}, [issue
    4242](https://github.com/scrapy/scrapy/issues/4242){.reference
    .external}, [issue
    4304](https://github.com/scrapy/scrapy/issues/4304){.reference
    .external}, [issue
    4309](https://github.com/scrapy/scrapy/issues/4309){.reference
    .external}, [issue
    4373](https://github.com/scrapy/scrapy/issues/4373){.reference
    .external})

-   Retry gaveups (see [[`RETRY_TIMES`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-RETRY_TIMES){.hoverxref
    .tooltip .reference .internal}) are now logged as errors instead of
    as debug information ([issue
    3171](https://github.com/scrapy/scrapy/issues/3171){.reference
    .external}, [issue
    3566](https://github.com/scrapy/scrapy/issues/3566){.reference
    .external})

-   File extensions that [[`LinkExtractor`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} ignores by default now also include [`7z`{.docutils
    .literal .notranslate}]{.pre}, [`7zip`{.docutils .literal
    .notranslate}]{.pre}, [`apk`{.docutils .literal
    .notranslate}]{.pre}, [`bz2`{.docutils .literal
    .notranslate}]{.pre}, [`cdr`{.docutils .literal
    .notranslate}]{.pre}, [`dmg`{.docutils .literal
    .notranslate}]{.pre}, [`ico`{.docutils .literal
    .notranslate}]{.pre}, [`iso`{.docutils .literal
    .notranslate}]{.pre}, [`tar`{.docutils .literal
    .notranslate}]{.pre}, [`tar.gz`{.docutils .literal
    .notranslate}]{.pre}, [`webm`{.docutils .literal
    .notranslate}]{.pre}, and [`xz`{.docutils .literal
    .notranslate}]{.pre} ([issue
    1837](https://github.com/scrapy/scrapy/issues/1837){.reference
    .external}, [issue
    2067](https://github.com/scrapy/scrapy/issues/2067){.reference
    .external}, [issue
    4066](https://github.com/scrapy/scrapy/issues/4066){.reference
    .external})

-   The [[`METAREFRESH_IGNORE_TAGS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-METAREFRESH_IGNORE_TAGS){.hoverxref
    .tooltip .reference .internal} setting is now an empty list by
    default, following web browser behavior ([issue
    3844](https://github.com/scrapy/scrapy/issues/3844){.reference
    .external}, [issue
    4311](https://github.com/scrapy/scrapy/issues/4311){.reference
    .external})

-   The [[`HttpCompressionMiddleware`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware "scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware"){.reference
    .internal} now includes spaces after commas in the value of the
    [`Accept-Encoding`{.docutils .literal .notranslate}]{.pre} header
    that it sets, following web browser behavior ([issue
    4293](https://github.com/scrapy/scrapy/issues/4293){.reference
    .external})

-   The [`__init__`{.docutils .literal .notranslate}]{.pre} method of
    custom download handlers (see [[`DOWNLOAD_HANDLERS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal}) or subclasses of the following
    downloader handlers no longer receives a [`settings`{.docutils
    .literal .notranslate}]{.pre} parameter:

    -   [`scrapy.core.downloader.handlers.datauri.DataURIDownloadHandler`{.xref
        .py .py-class .docutils .literal .notranslate}]{.pre}

    -   [`scrapy.core.downloader.handlers.file.FileDownloadHandler`{.xref
        .py .py-class .docutils .literal .notranslate}]{.pre}

    Use the [`from_settings`{.docutils .literal .notranslate}]{.pre} or
    [`from_crawler`{.docutils .literal .notranslate}]{.pre} class
    methods to expose such a parameter to your custom download handlers.

    ([issue
    4126](https://github.com/scrapy/scrapy/issues/4126){.reference
    .external})

-   We have refactored the [[`scrapy.core.scheduler.Scheduler`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.core.scheduler.Scheduler "scrapy.core.scheduler.Scheduler"){.reference
    .internal} class and related queue classes (see
    [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref
    .tooltip .reference .internal}, [[`SCHEDULER_DISK_QUEUE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DISK_QUEUE){.hoverxref
    .tooltip .reference .internal} and [[`SCHEDULER_MEMORY_QUEUE`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_MEMORY_QUEUE){.hoverxref
    .tooltip .reference .internal}) to make it easier to implement
    custom scheduler queue classes. See [[Changes to scheduler queue
    classes]{.std .std-ref}](#scheduler-queue-changes){.hoverxref
    .tooltip .reference .internal} below for details.

-   Overridden settings are now logged in a different format. This is
    more in line with similar information logged at startup ([issue
    4199](https://github.com/scrapy/scrapy/issues/4199){.reference
    .external})
:::

::: {#id72 .section}
##### Deprecation removals[¶](#id72 "Permalink to this heading"){.headerlink}

-   The [[Scrapy shell]{.std
    .std-ref}](index.html#topics-shell){.hoverxref .tooltip .reference
    .internal} no longer provides a sel proxy object, use
    [`response.selector`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} instead ([issue
    4347](https://github.com/scrapy/scrapy/issues/4347){.reference
    .external})

-   LevelDB support has been removed ([issue
    4112](https://github.com/scrapy/scrapy/issues/4112){.reference
    .external})

-   The following functions have been removed from
    [`scrapy.utils.python`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}: [`isbinarytext`{.docutils .literal
    .notranslate}]{.pre}, [`is_writable`{.docutils .literal
    .notranslate}]{.pre}, [`setattr_default`{.docutils .literal
    .notranslate}]{.pre}, [`stringify_dict`{.docutils .literal
    .notranslate}]{.pre} ([issue
    4362](https://github.com/scrapy/scrapy/issues/4362){.reference
    .external})
:::

::: {#id73 .section}
##### Deprecations[¶](#id73 "Permalink to this heading"){.headerlink}

-   Using environment variables prefixed with [`SCRAPY_`{.docutils
    .literal .notranslate}]{.pre} to override settings is deprecated
    ([issue
    4300](https://github.com/scrapy/scrapy/issues/4300){.reference
    .external}, [issue
    4374](https://github.com/scrapy/scrapy/issues/4374){.reference
    .external}, [issue
    4375](https://github.com/scrapy/scrapy/issues/4375){.reference
    .external})

-   [`scrapy.linkextractors.FilteringLinkExtractor`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} is deprecated, use
    [[`scrapy.linkextractors.LinkExtractor`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} instead ([issue
    4045](https://github.com/scrapy/scrapy/issues/4045){.reference
    .external})

-   The [`noconnect`{.docutils .literal .notranslate}]{.pre} query
    string argument of proxy URLs is deprecated and should be removed
    from proxy URLs ([issue
    4198](https://github.com/scrapy/scrapy/issues/4198){.reference
    .external})

-   The [`next`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} method of
    [`scrapy.utils.python.MutableChain`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre} is deprecated, use the global
    [[`next()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#next "(in Python v3.12)"){.reference
    .external} function or [`MutableChain.__next__`{.xref .py .py-meth
    .docutils .literal .notranslate}]{.pre} instead ([issue
    4153](https://github.com/scrapy/scrapy/issues/4153){.reference
    .external})
:::

::: {#id74 .section}
##### New features[¶](#id74 "Permalink to this heading"){.headerlink}

-   Added [[partial
    support]{.doc}](index.html#document-topics/coroutines){.reference
    .internal} for Python's [[coroutine syntax]{.xref .std
    .std-ref}](https://docs.python.org/3/reference/compound_stmts.html#async "(in Python v3.12)"){.reference
    .external} and [[experimental
    support]{.doc}](index.html#document-topics/asyncio){.reference
    .internal} for [[`asyncio`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
    .external} and [[`asyncio`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
    .external}-powered libraries ([issue
    4010](https://github.com/scrapy/scrapy/issues/4010){.reference
    .external}, [issue
    4259](https://github.com/scrapy/scrapy/issues/4259){.reference
    .external}, [issue
    4269](https://github.com/scrapy/scrapy/issues/4269){.reference
    .external}, [issue
    4270](https://github.com/scrapy/scrapy/issues/4270){.reference
    .external}, [issue
    4271](https://github.com/scrapy/scrapy/issues/4271){.reference
    .external}, [issue
    4316](https://github.com/scrapy/scrapy/issues/4316){.reference
    .external}, [issue
    4318](https://github.com/scrapy/scrapy/issues/4318){.reference
    .external})

-   The new [[`Response.follow_all`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.follow_all "scrapy.http.Response.follow_all"){.reference
    .internal} method offers the same functionality as
    [[`Response.follow`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.follow "scrapy.http.Response.follow"){.reference
    .internal} but supports an iterable of URLs as input and returns an
    iterable of requests ([issue
    2582](https://github.com/scrapy/scrapy/issues/2582){.reference
    .external}, [issue
    4057](https://github.com/scrapy/scrapy/issues/4057){.reference
    .external}, [issue
    4286](https://github.com/scrapy/scrapy/issues/4286){.reference
    .external})

-   [[Media pipelines]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal} now support [[FTP storage]{.std
    .std-ref}](index.html#media-pipeline-ftp){.hoverxref .tooltip
    .reference .internal} ([issue
    3928](https://github.com/scrapy/scrapy/issues/3928){.reference
    .external}, [issue
    3961](https://github.com/scrapy/scrapy/issues/3961){.reference
    .external})

-   The new [[`Response.certificate`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.certificate "scrapy.http.Response.certificate"){.reference
    .internal} attribute exposes the SSL certificate of the server as a
    [[`twisted.internet.ssl.Certificate`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.ssl.Certificate.html "(in Twisted)"){.reference
    .external} object for HTTPS responses ([issue
    2726](https://github.com/scrapy/scrapy/issues/2726){.reference
    .external}, [issue
    4054](https://github.com/scrapy/scrapy/issues/4054){.reference
    .external})

-   A new [[`DNS_RESOLVER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DNS_RESOLVER){.hoverxref
    .tooltip .reference .internal} setting allows enabling IPv6 support
    ([issue
    1031](https://github.com/scrapy/scrapy/issues/1031){.reference
    .external}, [issue
    4227](https://github.com/scrapy/scrapy/issues/4227){.reference
    .external})

-   A new [[`SCRAPER_SLOT_MAX_ACTIVE_SIZE`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCRAPER_SLOT_MAX_ACTIVE_SIZE){.hoverxref
    .tooltip .reference .internal} setting allows configuring the
    existing soft limit that pauses request downloads when the total
    response data being processed is too high ([issue
    1410](https://github.com/scrapy/scrapy/issues/1410){.reference
    .external}, [issue
    3551](https://github.com/scrapy/scrapy/issues/3551){.reference
    .external})

-   A new [[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
    .tooltip .reference .internal} setting allows customizing the
    [[`reactor`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
    .external} that Scrapy uses, allowing to [[enable asyncio
    support]{.doc}](index.html#document-topics/asyncio){.reference
    .internal} or deal with a [[common macOS issue]{.std
    .std-ref}](index.html#faq-specific-reactor){.hoverxref .tooltip
    .reference .internal} ([issue
    2905](https://github.com/scrapy/scrapy/issues/2905){.reference
    .external}, [issue
    4294](https://github.com/scrapy/scrapy/issues/4294){.reference
    .external})

-   Scheduler disk and memory queues may now use the class methods
    [`from_crawler`{.docutils .literal .notranslate}]{.pre} or
    [`from_settings`{.docutils .literal .notranslate}]{.pre} ([issue
    3884](https://github.com/scrapy/scrapy/issues/3884){.reference
    .external})

-   The new [[`Response.cb_kwargs`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.cb_kwargs "scrapy.http.Response.cb_kwargs"){.reference
    .internal} attribute serves as a shortcut for
    [[`Response.request.cb_kwargs`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
    .internal} ([issue
    4331](https://github.com/scrapy/scrapy/issues/4331){.reference
    .external})

-   [[`Response.follow`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response.follow "scrapy.http.Response.follow"){.reference
    .internal} now supports a [`flags`{.docutils .literal
    .notranslate}]{.pre} parameter, for consistency with
    [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} ([issue
    4277](https://github.com/scrapy/scrapy/issues/4277){.reference
    .external}, [issue
    4279](https://github.com/scrapy/scrapy/issues/4279){.reference
    .external})

-   [[Item loader processors]{.std
    .std-ref}](index.html#topics-loaders-processors){.hoverxref .tooltip
    .reference .internal} can now be regular functions, they no longer
    need to be methods ([issue
    3899](https://github.com/scrapy/scrapy/issues/3899){.reference
    .external})

-   [[`Rule`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
    .internal} now accepts an [`errback`{.docutils .literal
    .notranslate}]{.pre} parameter ([issue
    4000](https://github.com/scrapy/scrapy/issues/4000){.reference
    .external})

-   [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} no longer requires a [`callback`{.docutils .literal
    .notranslate}]{.pre} parameter when an [`errback`{.docutils .literal
    .notranslate}]{.pre} parameter is specified ([issue
    3586](https://github.com/scrapy/scrapy/issues/3586){.reference
    .external}, [issue
    4008](https://github.com/scrapy/scrapy/issues/4008){.reference
    .external})

-   [[`LogFormatter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.logformatter.LogFormatter "scrapy.logformatter.LogFormatter"){.reference
    .internal} now supports some additional methods:

    -   [[`download_error`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.logformatter.LogFormatter.download_error "scrapy.logformatter.LogFormatter.download_error"){.reference
        .internal} for download errors

    -   [[`item_error`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.logformatter.LogFormatter.item_error "scrapy.logformatter.LogFormatter.item_error"){.reference
        .internal} for exceptions raised during item processing by
        [[item pipelines]{.std
        .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
        .reference .internal}

    -   [[`spider_error`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.logformatter.LogFormatter.spider_error "scrapy.logformatter.LogFormatter.spider_error"){.reference
        .internal} for exceptions raised from [[spider callbacks]{.std
        .std-ref}](index.html#topics-spiders){.hoverxref .tooltip
        .reference .internal}

    ([issue 374](https://github.com/scrapy/scrapy/issues/374){.reference
    .external}, [issue
    3986](https://github.com/scrapy/scrapy/issues/3986){.reference
    .external}, [issue
    3989](https://github.com/scrapy/scrapy/issues/3989){.reference
    .external}, [issue
    4176](https://github.com/scrapy/scrapy/issues/4176){.reference
    .external}, [issue
    4188](https://github.com/scrapy/scrapy/issues/4188){.reference
    .external})

-   The [`FEED_URI`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre} setting now supports [[`pathlib.Path`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.12)"){.reference
    .external} values ([issue
    3731](https://github.com/scrapy/scrapy/issues/3731){.reference
    .external}, [issue
    4074](https://github.com/scrapy/scrapy/issues/4074){.reference
    .external})

-   A new [[`request_left_downloader`{.xref .std .std-signal .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-signal-request_left_downloader){.hoverxref
    .tooltip .reference .internal} signal is sent when a request leaves
    the downloader ([issue
    4303](https://github.com/scrapy/scrapy/issues/4303){.reference
    .external})

-   Scrapy logs a warning when it detects a request callback or errback
    that uses [`yield`{.docutils .literal .notranslate}]{.pre} but also
    returns a value, since the returned value would be lost ([issue
    3484](https://github.com/scrapy/scrapy/issues/3484){.reference
    .external}, [issue
    3869](https://github.com/scrapy/scrapy/issues/3869){.reference
    .external})

-   [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} objects now raise an [[`AttributeError`{.xref .py .py-exc
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#AttributeError "(in Python v3.12)"){.reference
    .external} exception if they do not have a [`start_urls`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} attribute nor
    reimplement [`start_requests`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}, but have a [`start_url`{.docutils .literal
    .notranslate}]{.pre} attribute ([issue
    4133](https://github.com/scrapy/scrapy/issues/4133){.reference
    .external}, [issue
    4170](https://github.com/scrapy/scrapy/issues/4170){.reference
    .external})

-   [[`BaseItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} subclasses may now use
    [`super().__init__(**kwargs)`{.docutils .literal
    .notranslate}]{.pre} instead of [`self._configure(kwargs)`{.docutils
    .literal .notranslate}]{.pre} in their [`__init__`{.docutils
    .literal .notranslate}]{.pre} method, passing
    [`dont_fail=True`{.docutils .literal .notranslate}]{.pre} to the
    parent [`__init__`{.docutils .literal .notranslate}]{.pre} method if
    needed, and accessing [`kwargs`{.docutils .literal
    .notranslate}]{.pre} at [`self._kwargs`{.docutils .literal
    .notranslate}]{.pre} after calling their parent
    [`__init__`{.docutils .literal .notranslate}]{.pre} method ([issue
    4193](https://github.com/scrapy/scrapy/issues/4193){.reference
    .external}, [issue
    4370](https://github.com/scrapy/scrapy/issues/4370){.reference
    .external})

-   A new [`keep_fragments`{.docutils .literal .notranslate}]{.pre}
    parameter of [`scrapy.utils.request.request_fingerprint`{.docutils
    .literal .notranslate}]{.pre} allows to generate different
    fingerprints for requests with different fragments in their URL
    ([issue
    4104](https://github.com/scrapy/scrapy/issues/4104){.reference
    .external})

-   Download handlers (see [[`DOWNLOAD_HANDLERS`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal}) may now use the
    [`from_settings`{.docutils .literal .notranslate}]{.pre} and
    [`from_crawler`{.docutils .literal .notranslate}]{.pre} class
    methods that other Scrapy components already supported ([issue
    4126](https://github.com/scrapy/scrapy/issues/4126){.reference
    .external})

-   [`scrapy.utils.python.MutableChain.__iter__`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} now returns
    [`self`{.docutils .literal .notranslate}]{.pre}, [allowing it to be
    used as a sequence](https://lgtm.com/rules/4850080/){.reference
    .external} ([issue
    4153](https://github.com/scrapy/scrapy/issues/4153){.reference
    .external})
:::

::: {#id75 .section}
##### Bug fixes[¶](#id75 "Permalink to this heading"){.headerlink}

-   The [[`crawl`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref
    .tooltip .reference .internal} command now also exits with exit code
    1 when an exception happens before the crawling starts ([issue
    4175](https://github.com/scrapy/scrapy/issues/4175){.reference
    .external}, [issue
    4207](https://github.com/scrapy/scrapy/issues/4207){.reference
    .external})

-   [[`LinkExtractor.extract_links`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor.extract_links "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor.extract_links"){.reference
    .internal} no longer re-encodes the query string or URLs from
    non-UTF-8 responses in UTF-8 ([issue
    998](https://github.com/scrapy/scrapy/issues/998){.reference
    .external}, [issue
    1403](https://github.com/scrapy/scrapy/issues/1403){.reference
    .external}, [issue
    1949](https://github.com/scrapy/scrapy/issues/1949){.reference
    .external}, [issue
    4321](https://github.com/scrapy/scrapy/issues/4321){.reference
    .external})

-   The first spider middleware (see [[`SPIDER_MIDDLEWARES`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES){.hoverxref
    .tooltip .reference .internal}) now also processes exceptions raised
    from callbacks that are generators ([issue
    4260](https://github.com/scrapy/scrapy/issues/4260){.reference
    .external}, [issue
    4272](https://github.com/scrapy/scrapy/issues/4272){.reference
    .external})

-   Redirects to URLs starting with 3 slashes ([`///`{.docutils .literal
    .notranslate}]{.pre}) are now supported ([issue
    4032](https://github.com/scrapy/scrapy/issues/4032){.reference
    .external}, [issue
    4042](https://github.com/scrapy/scrapy/issues/4042){.reference
    .external})

-   [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} no longer accepts strings as [`url`{.docutils .literal
    .notranslate}]{.pre} simply because they have a colon ([issue
    2552](https://github.com/scrapy/scrapy/issues/2552){.reference
    .external}, [issue
    4094](https://github.com/scrapy/scrapy/issues/4094){.reference
    .external})

-   The correct encoding is now used for attach names in
    [[`MailSender`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.mail.MailSender "scrapy.mail.MailSender"){.reference
    .internal} ([issue
    4229](https://github.com/scrapy/scrapy/issues/4229){.reference
    .external}, [issue
    4239](https://github.com/scrapy/scrapy/issues/4239){.reference
    .external})

-   [`RFPDupeFilter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}, the default [[`DUPEFILTER_CLASS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DUPEFILTER_CLASS){.hoverxref
    .tooltip .reference .internal}, no longer writes an extra
    [`\r`{.docutils .literal .notranslate}]{.pre} character on each line
    in Windows, which made the size of the [`requests.seen`{.docutils
    .literal .notranslate}]{.pre} file unnecessarily large on that
    platform ([issue
    4283](https://github.com/scrapy/scrapy/issues/4283){.reference
    .external})

-   Z shell auto-completion now looks for [`.html`{.docutils .literal
    .notranslate}]{.pre} files, not [`.http`{.docutils .literal
    .notranslate}]{.pre} files, and covers the [`-h`{.docutils .literal
    .notranslate}]{.pre} command-line switch ([issue
    4122](https://github.com/scrapy/scrapy/issues/4122){.reference
    .external}, [issue
    4291](https://github.com/scrapy/scrapy/issues/4291){.reference
    .external})

-   Adding items to a [`scrapy.utils.datatypes.LocalCache`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} object without a
    [`limit`{.docutils .literal .notranslate}]{.pre} defined no longer
    raises a [[`TypeError`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#TypeError "(in Python v3.12)"){.reference
    .external} exception ([issue
    4123](https://github.com/scrapy/scrapy/issues/4123){.reference
    .external})

-   Fixed a typo in the message of the [[`ValueError`{.xref .py .py-exc
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#ValueError "(in Python v3.12)"){.reference
    .external} exception raised when
    [`scrapy.utils.misc.create_instance()`{.xref .py .py-func .docutils
    .literal .notranslate}]{.pre} gets both [`settings`{.docutils
    .literal .notranslate}]{.pre} and [`crawler`{.docutils .literal
    .notranslate}]{.pre} set to [`None`{.docutils .literal
    .notranslate}]{.pre} ([issue
    4128](https://github.com/scrapy/scrapy/issues/4128){.reference
    .external})
:::

::: {#id76 .section}
##### Documentation[¶](#id76 "Permalink to this heading"){.headerlink}

-   API documentation now links to an online, syntax-highlighted view of
    the corresponding source code ([issue
    4148](https://github.com/scrapy/scrapy/issues/4148){.reference
    .external})

-   Links to unexisting documentation pages now allow access to the
    sidebar ([issue
    4152](https://github.com/scrapy/scrapy/issues/4152){.reference
    .external}, [issue
    4169](https://github.com/scrapy/scrapy/issues/4169){.reference
    .external})

-   Cross-references within our documentation now display a tooltip when
    hovered ([issue
    4173](https://github.com/scrapy/scrapy/issues/4173){.reference
    .external}, [issue
    4183](https://github.com/scrapy/scrapy/issues/4183){.reference
    .external})

-   Improved the documentation about
    [[`LinkExtractor.extract_links`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor.extract_links "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor.extract_links"){.reference
    .internal} and simplified [[Link Extractors]{.std
    .std-ref}](index.html#topics-link-extractors){.hoverxref .tooltip
    .reference .internal} ([issue
    4045](https://github.com/scrapy/scrapy/issues/4045){.reference
    .external})

-   Clarified how [[`ItemLoader.item`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.item "scrapy.loader.ItemLoader.item"){.reference
    .internal} works ([issue
    3574](https://github.com/scrapy/scrapy/issues/3574){.reference
    .external}, [issue
    4099](https://github.com/scrapy/scrapy/issues/4099){.reference
    .external})

-   Clarified that [[`logging.basicConfig()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/logging.html#logging.basicConfig "(in Python v3.12)"){.reference
    .external} should not be used when also using
    [[`CrawlerProcess`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
    .internal} ([issue
    2149](https://github.com/scrapy/scrapy/issues/2149){.reference
    .external}, [issue
    2352](https://github.com/scrapy/scrapy/issues/2352){.reference
    .external}, [issue
    3146](https://github.com/scrapy/scrapy/issues/3146){.reference
    .external}, [issue
    3960](https://github.com/scrapy/scrapy/issues/3960){.reference
    .external})

-   Clarified the requirements for [[`Request`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} objects [[when using persistence]{.std
    .std-ref}](index.html#request-serialization){.hoverxref .tooltip
    .reference .internal} ([issue
    4124](https://github.com/scrapy/scrapy/issues/4124){.reference
    .external}, [issue
    4139](https://github.com/scrapy/scrapy/issues/4139){.reference
    .external})

-   Clarified how to install a [[custom image pipeline]{.std
    .std-ref}](index.html#media-pipeline-example){.hoverxref .tooltip
    .reference .internal} ([issue
    4034](https://github.com/scrapy/scrapy/issues/4034){.reference
    .external}, [issue
    4252](https://github.com/scrapy/scrapy/issues/4252){.reference
    .external})

-   Fixed the signatures of the [`file_path`{.docutils .literal
    .notranslate}]{.pre} method in [[media pipeline]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal} examples ([issue
    4290](https://github.com/scrapy/scrapy/issues/4290){.reference
    .external})

-   Covered a backward-incompatible change in Scrapy 1.7.0 affecting
    custom [[`scrapy.core.scheduler.Scheduler`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.core.scheduler.Scheduler "scrapy.core.scheduler.Scheduler"){.reference
    .internal} subclasses ([issue
    4274](https://github.com/scrapy/scrapy/issues/4274){.reference
    .external})

-   Improved the [`README.rst`{.docutils .literal .notranslate}]{.pre}
    and [`CODE_OF_CONDUCT.md`{.docutils .literal .notranslate}]{.pre}
    files ([issue
    4059](https://github.com/scrapy/scrapy/issues/4059){.reference
    .external})

-   Documentation examples are now checked as part of our test suite and
    we have fixed some of the issues detected ([issue
    4142](https://github.com/scrapy/scrapy/issues/4142){.reference
    .external}, [issue
    4146](https://github.com/scrapy/scrapy/issues/4146){.reference
    .external}, [issue
    4171](https://github.com/scrapy/scrapy/issues/4171){.reference
    .external}, [issue
    4184](https://github.com/scrapy/scrapy/issues/4184){.reference
    .external}, [issue
    4190](https://github.com/scrapy/scrapy/issues/4190){.reference
    .external})

-   Fixed logic issues, broken links and typos ([issue
    4247](https://github.com/scrapy/scrapy/issues/4247){.reference
    .external}, [issue
    4258](https://github.com/scrapy/scrapy/issues/4258){.reference
    .external}, [issue
    4282](https://github.com/scrapy/scrapy/issues/4282){.reference
    .external}, [issue
    4288](https://github.com/scrapy/scrapy/issues/4288){.reference
    .external}, [issue
    4305](https://github.com/scrapy/scrapy/issues/4305){.reference
    .external}, [issue
    4308](https://github.com/scrapy/scrapy/issues/4308){.reference
    .external}, [issue
    4323](https://github.com/scrapy/scrapy/issues/4323){.reference
    .external}, [issue
    4338](https://github.com/scrapy/scrapy/issues/4338){.reference
    .external}, [issue
    4359](https://github.com/scrapy/scrapy/issues/4359){.reference
    .external}, [issue
    4361](https://github.com/scrapy/scrapy/issues/4361){.reference
    .external})

-   Improved consistency when referring to the [`__init__`{.docutils
    .literal .notranslate}]{.pre} method of an object ([issue
    4086](https://github.com/scrapy/scrapy/issues/4086){.reference
    .external}, [issue
    4088](https://github.com/scrapy/scrapy/issues/4088){.reference
    .external})

-   Fixed an inconsistency between code and output in [[Scrapy at a
    glance]{.std .std-ref}](index.html#intro-overview){.hoverxref
    .tooltip .reference .internal} ([issue
    4213](https://github.com/scrapy/scrapy/issues/4213){.reference
    .external})

-   Extended [[`intersphinx`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://www.sphinx-doc.org/en/master/usage/extensions/intersphinx.html#module-sphinx.ext.intersphinx "(in Sphinx v7.3.0)"){.reference
    .external} usage ([issue
    4147](https://github.com/scrapy/scrapy/issues/4147){.reference
    .external}, [issue
    4172](https://github.com/scrapy/scrapy/issues/4172){.reference
    .external}, [issue
    4185](https://github.com/scrapy/scrapy/issues/4185){.reference
    .external}, [issue
    4194](https://github.com/scrapy/scrapy/issues/4194){.reference
    .external}, [issue
    4197](https://github.com/scrapy/scrapy/issues/4197){.reference
    .external})

-   We now use a recent version of Python to build the documentation
    ([issue
    4140](https://github.com/scrapy/scrapy/issues/4140){.reference
    .external}, [issue
    4249](https://github.com/scrapy/scrapy/issues/4249){.reference
    .external})

-   Cleaned up documentation ([issue
    4143](https://github.com/scrapy/scrapy/issues/4143){.reference
    .external}, [issue
    4275](https://github.com/scrapy/scrapy/issues/4275){.reference
    .external})
:::

::: {#id77 .section}
##### Quality assurance[¶](#id77 "Permalink to this heading"){.headerlink}

-   Re-enabled proxy [`CONNECT`{.docutils .literal .notranslate}]{.pre}
    tests ([issue
    2545](https://github.com/scrapy/scrapy/issues/2545){.reference
    .external}, [issue
    4114](https://github.com/scrapy/scrapy/issues/4114){.reference
    .external})

-   Added [Bandit](https://bandit.readthedocs.io/){.reference .external}
    security checks to our test suite ([issue
    4162](https://github.com/scrapy/scrapy/issues/4162){.reference
    .external}, [issue
    4181](https://github.com/scrapy/scrapy/issues/4181){.reference
    .external})

-   Added [Flake8](https://flake8.pycqa.org/en/latest/){.reference
    .external} style checks to our test suite and applied many of the
    corresponding changes ([issue
    3944](https://github.com/scrapy/scrapy/issues/3944){.reference
    .external}, [issue
    3945](https://github.com/scrapy/scrapy/issues/3945){.reference
    .external}, [issue
    4137](https://github.com/scrapy/scrapy/issues/4137){.reference
    .external}, [issue
    4157](https://github.com/scrapy/scrapy/issues/4157){.reference
    .external}, [issue
    4167](https://github.com/scrapy/scrapy/issues/4167){.reference
    .external}, [issue
    4174](https://github.com/scrapy/scrapy/issues/4174){.reference
    .external}, [issue
    4186](https://github.com/scrapy/scrapy/issues/4186){.reference
    .external}, [issue
    4195](https://github.com/scrapy/scrapy/issues/4195){.reference
    .external}, [issue
    4238](https://github.com/scrapy/scrapy/issues/4238){.reference
    .external}, [issue
    4246](https://github.com/scrapy/scrapy/issues/4246){.reference
    .external}, [issue
    4355](https://github.com/scrapy/scrapy/issues/4355){.reference
    .external}, [issue
    4360](https://github.com/scrapy/scrapy/issues/4360){.reference
    .external}, [issue
    4365](https://github.com/scrapy/scrapy/issues/4365){.reference
    .external})

-   Improved test coverage ([issue
    4097](https://github.com/scrapy/scrapy/issues/4097){.reference
    .external}, [issue
    4218](https://github.com/scrapy/scrapy/issues/4218){.reference
    .external}, [issue
    4236](https://github.com/scrapy/scrapy/issues/4236){.reference
    .external})

-   Started reporting slowest tests, and improved the performance of
    some of them ([issue
    4163](https://github.com/scrapy/scrapy/issues/4163){.reference
    .external}, [issue
    4164](https://github.com/scrapy/scrapy/issues/4164){.reference
    .external})

-   Fixed broken tests and refactored some tests ([issue
    4014](https://github.com/scrapy/scrapy/issues/4014){.reference
    .external}, [issue
    4095](https://github.com/scrapy/scrapy/issues/4095){.reference
    .external}, [issue
    4244](https://github.com/scrapy/scrapy/issues/4244){.reference
    .external}, [issue
    4268](https://github.com/scrapy/scrapy/issues/4268){.reference
    .external}, [issue
    4372](https://github.com/scrapy/scrapy/issues/4372){.reference
    .external})

-   Modified the [[tox]{.xref .std
    .std-doc}](https://tox.wiki/en/latest/index.html "(in Python v4.11)"){.reference
    .external} configuration to allow running tests with any Python
    version, run [Bandit](https://bandit.readthedocs.io/){.reference
    .external} and
    [Flake8](https://flake8.pycqa.org/en/latest/){.reference .external}
    tests by default, and enforce a minimum tox version programmatically
    ([issue
    4179](https://github.com/scrapy/scrapy/issues/4179){.reference
    .external})

-   Cleaned up code ([issue
    3937](https://github.com/scrapy/scrapy/issues/3937){.reference
    .external}, [issue
    4208](https://github.com/scrapy/scrapy/issues/4208){.reference
    .external}, [issue
    4209](https://github.com/scrapy/scrapy/issues/4209){.reference
    .external}, [issue
    4210](https://github.com/scrapy/scrapy/issues/4210){.reference
    .external}, [issue
    4212](https://github.com/scrapy/scrapy/issues/4212){.reference
    .external}, [issue
    4369](https://github.com/scrapy/scrapy/issues/4369){.reference
    .external}, [issue
    4376](https://github.com/scrapy/scrapy/issues/4376){.reference
    .external}, [issue
    4378](https://github.com/scrapy/scrapy/issues/4378){.reference
    .external})
:::

::: {#changes-to-scheduler-queue-classes .section}
[]{#scheduler-queue-changes}

##### Changes to scheduler queue classes[¶](#changes-to-scheduler-queue-classes "Permalink to this heading"){.headerlink}

The following changes may impact any custom queue classes of all types:

-   The [`push`{.docutils .literal .notranslate}]{.pre} method no longer
    receives a second positional parameter containing
    [`request.priority`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`*`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`-1`{.docutils .literal .notranslate}]{.pre}. If you
    need that value, get it from the first positional parameter,
    [`request`{.docutils .literal .notranslate}]{.pre}, instead, or use
    the new [`priority()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} method in
    [`scrapy.core.scheduler.ScrapyPriorityQueue`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} subclasses.

The following changes may impact custom priority queue classes:

-   In the [`__init__`{.docutils .literal .notranslate}]{.pre} method or
    the [`from_crawler`{.docutils .literal .notranslate}]{.pre} or
    [`from_settings`{.docutils .literal .notranslate}]{.pre} class
    methods:

    -   The parameter that used to contain a factory function,
        [`qfactory`{.docutils .literal .notranslate}]{.pre}, is now
        passed as a keyword parameter named
        [`downstream_queue_cls`{.docutils .literal .notranslate}]{.pre}.

    -   A new keyword parameter has been added: [`key`{.docutils
        .literal .notranslate}]{.pre}. It is a string that is always an
        empty string for memory queues and indicates the
        [`JOB_DIR`{.xref .std .std-setting .docutils .literal
        .notranslate}]{.pre} value for disk queues.

    -   The parameter for disk queues that contains data from the
        previous crawl, [`startprios`{.docutils .literal
        .notranslate}]{.pre} or [`slot_startprios`{.docutils .literal
        .notranslate}]{.pre}, is now passed as a keyword parameter named
        [`startprios`{.docutils .literal .notranslate}]{.pre}.

    -   The [`serialize`{.docutils .literal .notranslate}]{.pre}
        parameter is no longer passed. The disk queue class must take
        care of request serialization on its own before writing to disk,
        using the [`request_to_dict()`{.xref .py .py-func .docutils
        .literal .notranslate}]{.pre} and [`request_from_dict()`{.xref
        .py .py-func .docutils .literal .notranslate}]{.pre} functions
        from the [`scrapy.utils.reqser`{.xref .py .py-mod .docutils
        .literal .notranslate}]{.pre} module.

The following changes may impact custom disk and memory queue classes:

-   The signature of the [`__init__`{.docutils .literal
    .notranslate}]{.pre} method is now [`__init__(self,`{.docutils
    .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`crawler,`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`key)`{.docutils .literal .notranslate}]{.pre}.

The following changes affect specifically the
[`ScrapyPriorityQueue`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} and [`DownloaderAwarePriorityQueue`{.xref .py
.py-class .docutils .literal .notranslate}]{.pre} classes from
[[`scrapy.core.scheduler`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](index.html#module-scrapy.core.scheduler "scrapy.core.scheduler"){.reference
.internal} and may affect subclasses:

-   In the [`__init__`{.docutils .literal .notranslate}]{.pre} method,
    most of the changes described above apply.

    [`__init__`{.docutils .literal .notranslate}]{.pre} may still
    receive all parameters as positional parameters, however:

    -   [`downstream_queue_cls`{.docutils .literal .notranslate}]{.pre},
        which replaced [`qfactory`{.docutils .literal
        .notranslate}]{.pre}, must be instantiated differently.

        [`qfactory`{.docutils .literal .notranslate}]{.pre} was
        instantiated with a priority value (integer).

        Instances of [`downstream_queue_cls`{.docutils .literal
        .notranslate}]{.pre} should be created using the new
        [`ScrapyPriorityQueue.qfactory`{.xref .py .py-meth .docutils
        .literal .notranslate}]{.pre} or
        [`DownloaderAwarePriorityQueue.pqfactory`{.xref .py .py-meth
        .docutils .literal .notranslate}]{.pre} methods.

    -   The new [`key`{.docutils .literal .notranslate}]{.pre} parameter
        displaced the [`startprios`{.docutils .literal
        .notranslate}]{.pre} parameter 1 position to the right.

-   The following class attributes have been added:

    -   [`crawler`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}

    -   [`downstream_queue_cls`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre} (details above)

    -   [`key`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre} (details above)

-   The [`serialize`{.docutils .literal .notranslate}]{.pre} attribute
    has been removed (details above)

The following changes affect specifically the
[`ScrapyPriorityQueue`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} class and may affect subclasses:

-   A new [`priority()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} method has been added which, given a request,
    returns [`request.priority`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal