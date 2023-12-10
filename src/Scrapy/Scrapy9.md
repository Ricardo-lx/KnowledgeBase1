    .notranslate}[`*`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`-1`{.docutils .literal .notranslate}]{.pre}.

    It is used in [`push()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} to make up for the removal of its
    [`priority`{.docutils .literal .notranslate}]{.pre} parameter.

-   The [`spider`{.docutils .literal .notranslate}]{.pre} attribute has
    been removed. Use [`crawler.spider`{.xref .py .py-attr .docutils
    .literal .notranslate}]{.pre} instead.

The following changes affect specifically the
[`DownloaderAwarePriorityQueue`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} class and may affect subclasses:

-   A new [`pqueues`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} attribute offers a mapping of downloader slot
    names to the corresponding instances of
    [`downstream_queue_cls`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}.

([issue 3884](https://github.com/scrapy/scrapy/issues/3884){.reference
.external})
:::
:::

::: {#scrapy-1-8-3-2022-07-25 .section}
[]{#release-1-8-3}

#### Scrapy 1.8.3 (2022-07-25)[¶](#scrapy-1-8-3-2022-07-25 "Permalink to this heading"){.headerlink}

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
:::

::: {#scrapy-1-8-2-2022-03-01 .section}
[]{#release-1-8-2}

#### Scrapy 1.8.2 (2022-03-01)[¶](#scrapy-1-8-2-2022-03-01 "Permalink to this heading"){.headerlink}

**Security bug fixes:**

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
    into your requests to some other domains. Please, see the
    [mfjm-vh54-3f96 security
    advisory](https://github.com/scrapy/scrapy/security/advisories/GHSA-mfjm-vh54-3f96){.reference
    .external} for more information.
:::

::: {#scrapy-1-8-1-2021-10-05 .section}
[]{#release-1-8-1}

#### Scrapy 1.8.1 (2021-10-05)[¶](#scrapy-1-8-1-2021-10-05 "Permalink to this heading"){.headerlink}

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

::: {#scrapy-1-8-0-2019-10-28 .section}
[]{#release-1-8-0}

#### Scrapy 1.8.0 (2019-10-28)[¶](#scrapy-1-8-0-2019-10-28 "Permalink to this heading"){.headerlink}

Highlights:

-   Dropped Python 3.4 support and updated minimum requirements; made
    Python 3.8 support official

-   New [[`Request.from_curl`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.from_curl "scrapy.http.Request.from_curl"){.reference
    .internal} class method

-   New [[`ROBOTSTXT_PARSER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_PARSER){.hoverxref
    .tooltip .reference .internal} and [[`ROBOTSTXT_USER_AGENT`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_USER_AGENT){.hoverxref
    .tooltip .reference .internal} settings

-   New [[`DOWNLOADER_CLIENT_TLS_CIPHERS`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENT_TLS_CIPHERS){.hoverxref
    .tooltip .reference .internal} and
    [[`DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING){.hoverxref
    .tooltip .reference .internal} settings

::: {#id82 .section}
##### Backward-incompatible changes[¶](#id82 "Permalink to this heading"){.headerlink}

-   Python 3.4 is no longer supported, and some of the minimum
    requirements of Scrapy have also changed:

    -   [[cssselect]{.xref .std
        .std-doc}](https://cssselect.readthedocs.io/en/latest/index.html "(in cssselect v1.2.0)"){.reference
        .external} 0.9.1

    -   [cryptography](https://cryptography.io/en/latest/){.reference
        .external} 2.0

    -   [lxml](https://lxml.de/){.reference .external} 3.5.0

    -   [pyOpenSSL](https://www.pyopenssl.org/en/stable/){.reference
        .external} 16.2.0

    -   [queuelib](https://github.com/scrapy/queuelib){.reference
        .external} 1.4.2

    -   [service_identity](https://service-identity.readthedocs.io/en/stable/){.reference
        .external} 16.0.0

    -   [six](https://six.readthedocs.io/){.reference .external} 1.10.0

    -   [Twisted](https://twistedmatrix.com/trac/){.reference .external}
        17.9.0 (16.0.0 with Python 2)

    -   [zope.interface](https://zopeinterface.readthedocs.io/en/latest/){.reference
        .external} 4.1.3

    ([issue
    3892](https://github.com/scrapy/scrapy/issues/3892){.reference
    .external})

-   [`JSONRequest`{.docutils .literal .notranslate}]{.pre} is now called
    [[`JsonRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.JsonRequest "scrapy.http.JsonRequest"){.reference
    .internal} for consistency with similar classes ([issue
    3929](https://github.com/scrapy/scrapy/issues/3929){.reference
    .external}, [issue
    3982](https://github.com/scrapy/scrapy/issues/3982){.reference
    .external})

-   If you are using a custom context factory
    ([[`DOWNLOADER_CLIENTCONTEXTFACTORY`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENTCONTEXTFACTORY){.hoverxref
    .tooltip .reference .internal}), its [`__init__`{.docutils .literal
    .notranslate}]{.pre} method must accept two new parameters:
    [`tls_verbose_logging`{.docutils .literal .notranslate}]{.pre} and
    [`tls_ciphers`{.docutils .literal .notranslate}]{.pre} ([issue
    2111](https://github.com/scrapy/scrapy/issues/2111){.reference
    .external}, [issue
    3392](https://github.com/scrapy/scrapy/issues/3392){.reference
    .external}, [issue
    3442](https://github.com/scrapy/scrapy/issues/3442){.reference
    .external}, [issue
    3450](https://github.com/scrapy/scrapy/issues/3450){.reference
    .external})

-   [[`ItemLoader`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
    .internal} now turns the values of its input item into lists:

    ::: {.highlight-pycon .notranslate}
    ::: highlight
        >>> item = MyItem()
        >>> item["field"] = "value1"
        >>> loader = ItemLoader(item=item)
        >>> item["field"]
        ['value1']
    :::
    :::

    This is needed to allow adding values to existing fields
    ([`loader.add_value('field',`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`'value2')`{.docutils .literal .notranslate}]{.pre}).

    ([issue
    3804](https://github.com/scrapy/scrapy/issues/3804){.reference
    .external}, [issue
    3819](https://github.com/scrapy/scrapy/issues/3819){.reference
    .external}, [issue
    3897](https://github.com/scrapy/scrapy/issues/3897){.reference
    .external}, [issue
    3976](https://github.com/scrapy/scrapy/issues/3976){.reference
    .external}, [issue
    3998](https://github.com/scrapy/scrapy/issues/3998){.reference
    .external}, [issue
    4036](https://github.com/scrapy/scrapy/issues/4036){.reference
    .external})

See also [[Deprecation removals]{.std .std-ref}](#id86){.hoverxref
.tooltip .reference .internal} below.
:::

::: {#id83 .section}
##### New features[¶](#id83 "Permalink to this heading"){.headerlink}

-   A new [[`Request.from_curl`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.from_curl "scrapy.http.Request.from_curl"){.reference
    .internal} class method allows [[creating a request from a cURL
    command]{.std .std-ref}](index.html#requests-from-curl){.hoverxref
    .tooltip .reference .internal} ([issue
    2985](https://github.com/scrapy/scrapy/issues/2985){.reference
    .external}, [issue
    3862](https://github.com/scrapy/scrapy/issues/3862){.reference
    .external})

-   A new [[`ROBOTSTXT_PARSER`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_PARSER){.hoverxref
    .tooltip .reference .internal} setting allows choosing which
    [robots.txt](https://www.robotstxt.org/){.reference .external}
    parser to use. It includes built-in support for
    [[RobotFileParser]{.std
    .std-ref}](index.html#python-robotfileparser){.hoverxref .tooltip
    .reference .internal}, [[Protego]{.std
    .std-ref}](index.html#protego-parser){.hoverxref .tooltip .reference
    .internal} (default), [[Reppy]{.std
    .std-ref}](index.html#reppy-parser){.hoverxref .tooltip .reference
    .internal}, and [[Robotexclusionrulesparser]{.std
    .std-ref}](index.html#rerp-parser){.hoverxref .tooltip .reference
    .internal}, and allows you to [[implement support for additional
    parsers]{.std
    .std-ref}](index.html#support-for-new-robots-parser){.hoverxref
    .tooltip .reference .internal} ([issue
    754](https://github.com/scrapy/scrapy/issues/754){.reference
    .external}, [issue
    2669](https://github.com/scrapy/scrapy/issues/2669){.reference
    .external}, [issue
    3796](https://github.com/scrapy/scrapy/issues/3796){.reference
    .external}, [issue
    3935](https://github.com/scrapy/scrapy/issues/3935){.reference
    .external}, [issue
    3969](https://github.com/scrapy/scrapy/issues/3969){.reference
    .external}, [issue
    4006](https://github.com/scrapy/scrapy/issues/4006){.reference
    .external})

-   A new [[`ROBOTSTXT_USER_AGENT`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_USER_AGENT){.hoverxref
    .tooltip .reference .internal} setting allows defining a separate
    user agent string to use for
    [robots.txt](https://www.robotstxt.org/){.reference .external}
    parsing ([issue
    3931](https://github.com/scrapy/scrapy/issues/3931){.reference
    .external}, [issue
    3966](https://github.com/scrapy/scrapy/issues/3966){.reference
    .external})

-   [[`Rule`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
    .internal} no longer requires a [[`LinkExtractor`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} parameter ([issue
    781](https://github.com/scrapy/scrapy/issues/781){.reference
    .external}, [issue
    4016](https://github.com/scrapy/scrapy/issues/4016){.reference
    .external})

-   Use the new [[`DOWNLOADER_CLIENT_TLS_CIPHERS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENT_TLS_CIPHERS){.hoverxref
    .tooltip .reference .internal} setting to customize the TLS/SSL
    ciphers used by the default HTTP/1.1 downloader ([issue
    3392](https://github.com/scrapy/scrapy/issues/3392){.reference
    .external}, [issue
    3442](https://github.com/scrapy/scrapy/issues/3442){.reference
    .external})

-   Set the new [[`DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING){.hoverxref
    .tooltip .reference .internal} setting to [`True`{.docutils .literal
    .notranslate}]{.pre} to enable debug-level messages about TLS
    connection parameters after establishing HTTPS connections ([issue
    2111](https://github.com/scrapy/scrapy/issues/2111){.reference
    .external}, [issue
    3450](https://github.com/scrapy/scrapy/issues/3450){.reference
    .external})

-   Callbacks that receive keyword arguments (see
    [[`Request.cb_kwargs`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
    .internal}) can now be tested using the new [[`@cb_kwargs`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.contracts.default.CallbackKeywordArgumentsContract "scrapy.contracts.default.CallbackKeywordArgumentsContract"){.reference
    .internal} [[spider contract]{.std
    .std-ref}](index.html#topics-contracts){.hoverxref .tooltip
    .reference .internal} ([issue
    3985](https://github.com/scrapy/scrapy/issues/3985){.reference
    .external}, [issue
    3988](https://github.com/scrapy/scrapy/issues/3988){.reference
    .external})

-   When a [[`@scrapes`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.contracts.default.ScrapesContract "scrapy.contracts.default.ScrapesContract"){.reference
    .internal} spider contract fails, all missing fields are now
    reported ([issue
    766](https://github.com/scrapy/scrapy/issues/766){.reference
    .external}, [issue
    3939](https://github.com/scrapy/scrapy/issues/3939){.reference
    .external})

-   [[Custom log formats]{.std
    .std-ref}](index.html#custom-log-formats){.hoverxref .tooltip
    .reference .internal} can now drop messages by having the
    corresponding methods of the configured [[`LOG_FORMATTER`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_FORMATTER){.hoverxref
    .tooltip .reference .internal} return [`None`{.docutils .literal
    .notranslate}]{.pre} ([issue
    3984](https://github.com/scrapy/scrapy/issues/3984){.reference
    .external}, [issue
    3987](https://github.com/scrapy/scrapy/issues/3987){.reference
    .external})

-   A much improved completion definition is now available for
    [Zsh](https://www.zsh.org/){.reference .external} ([issue
    4069](https://github.com/scrapy/scrapy/issues/4069){.reference
    .external})
:::

::: {#id84 .section}
##### Bug fixes[¶](#id84 "Permalink to this heading"){.headerlink}

-   [[`ItemLoader.load_item()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
    .internal} no longer makes later calls to
    [[`ItemLoader.get_output_value()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.get_output_value "scrapy.loader.ItemLoader.get_output_value"){.reference
    .internal} or [[`ItemLoader.load_item()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
    .internal} return empty data ([issue
    3804](https://github.com/scrapy/scrapy/issues/3804){.reference
    .external}, [issue
    3819](https://github.com/scrapy/scrapy/issues/3819){.reference
    .external}, [issue
    3897](https://github.com/scrapy/scrapy/issues/3897){.reference
    .external}, [issue
    3976](https://github.com/scrapy/scrapy/issues/3976){.reference
    .external}, [issue
    3998](https://github.com/scrapy/scrapy/issues/3998){.reference
    .external}, [issue
    4036](https://github.com/scrapy/scrapy/issues/4036){.reference
    .external})

-   Fixed [[`DummyStatsCollector`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.statscollectors.DummyStatsCollector "scrapy.statscollectors.DummyStatsCollector"){.reference
    .internal} raising a [[`TypeError`{.xref .py .py-exc .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#TypeError "(in Python v3.12)"){.reference
    .external} exception ([issue
    4007](https://github.com/scrapy/scrapy/issues/4007){.reference
    .external}, [issue
    4052](https://github.com/scrapy/scrapy/issues/4052){.reference
    .external})

-   [[`FilesPipeline.file_path`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.files.FilesPipeline.file_path "scrapy.pipelines.files.FilesPipeline.file_path"){.reference
    .internal} and [[`ImagesPipeline.file_path`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline.file_path "scrapy.pipelines.images.ImagesPipeline.file_path"){.reference
    .internal} no longer choose file extensions that are not [registered
    with
    IANA](https://www.iana.org/assignments/media-types/media-types.xhtml){.reference
    .external} ([issue
    1287](https://github.com/scrapy/scrapy/issues/1287){.reference
    .external}, [issue
    3953](https://github.com/scrapy/scrapy/issues/3953){.reference
    .external}, [issue
    3954](https://github.com/scrapy/scrapy/issues/3954){.reference
    .external})

-   When using [botocore](https://github.com/boto/botocore){.reference
    .external} to persist files in S3, all botocore-supported headers
    are properly mapped now ([issue
    3904](https://github.com/scrapy/scrapy/issues/3904){.reference
    .external}, [issue
    3905](https://github.com/scrapy/scrapy/issues/3905){.reference
    .external})

-   FTP passwords in [`FEED_URI`{.xref .std .std-setting .docutils
    .literal .notranslate}]{.pre} containing percent-escaped characters
    are now properly decoded ([issue
    3941](https://github.com/scrapy/scrapy/issues/3941){.reference
    .external})

-   A memory-handling and error-handling issue in
    [`scrapy.utils.ssl.get_temp_key_info()`{.xref .py .py-func .docutils
    .literal .notranslate}]{.pre} has been fixed ([issue
    3920](https://github.com/scrapy/scrapy/issues/3920){.reference
    .external})
:::

::: {#id85 .section}
##### Documentation[¶](#id85 "Permalink to this heading"){.headerlink}

-   The documentation now covers how to define and configure a [[custom
    log format]{.std
    .std-ref}](index.html#custom-log-formats){.hoverxref .tooltip
    .reference .internal} ([issue
    3616](https://github.com/scrapy/scrapy/issues/3616){.reference
    .external}, [issue
    3660](https://github.com/scrapy/scrapy/issues/3660){.reference
    .external})

-   API documentation added for [[`MarshalItemExporter`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.MarshalItemExporter "scrapy.exporters.MarshalItemExporter"){.reference
    .internal} and [[`PythonItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.PythonItemExporter "scrapy.exporters.PythonItemExporter"){.reference
    .internal} ([issue
    3973](https://github.com/scrapy/scrapy/issues/3973){.reference
    .external})

-   API documentation added for [`BaseItem`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} and [[`ItemMeta`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.item.ItemMeta "scrapy.item.ItemMeta"){.reference
    .internal} ([issue
    3999](https://github.com/scrapy/scrapy/issues/3999){.reference
    .external})

-   Minor documentation fixes ([issue
    2998](https://github.com/scrapy/scrapy/issues/2998){.reference
    .external}, [issue
    3398](https://github.com/scrapy/scrapy/issues/3398){.reference
    .external}, [issue
    3597](https://github.com/scrapy/scrapy/issues/3597){.reference
    .external}, [issue
    3894](https://github.com/scrapy/scrapy/issues/3894){.reference
    .external}, [issue
    3934](https://github.com/scrapy/scrapy/issues/3934){.reference
    .external}, [issue
    3978](https://github.com/scrapy/scrapy/issues/3978){.reference
    .external}, [issue
    3993](https://github.com/scrapy/scrapy/issues/3993){.reference
    .external}, [issue
    4022](https://github.com/scrapy/scrapy/issues/4022){.reference
    .external}, [issue
    4028](https://github.com/scrapy/scrapy/issues/4028){.reference
    .external}, [issue
    4033](https://github.com/scrapy/scrapy/issues/4033){.reference
    .external}, [issue
    4046](https://github.com/scrapy/scrapy/issues/4046){.reference
    .external}, [issue
    4050](https://github.com/scrapy/scrapy/issues/4050){.reference
    .external}, [issue
    4055](https://github.com/scrapy/scrapy/issues/4055){.reference
    .external}, [issue
    4056](https://github.com/scrapy/scrapy/issues/4056){.reference
    .external}, [issue
    4061](https://github.com/scrapy/scrapy/issues/4061){.reference
    .external}, [issue
    4072](https://github.com/scrapy/scrapy/issues/4072){.reference
    .external}, [issue
    4071](https://github.com/scrapy/scrapy/issues/4071){.reference
    .external}, [issue
    4079](https://github.com/scrapy/scrapy/issues/4079){.reference
    .external}, [issue
    4081](https://github.com/scrapy/scrapy/issues/4081){.reference
    .external}, [issue
    4089](https://github.com/scrapy/scrapy/issues/4089){.reference
    .external}, [issue
    4093](https://github.com/scrapy/scrapy/issues/4093){.reference
    .external})
:::

::: {#id86 .section}
[]{#id87}

##### Deprecation removals[¶](#id86 "Permalink to this heading"){.headerlink}

-   [`scrapy.xlib`{.docutils .literal .notranslate}]{.pre} has been
    removed ([issue
    4015](https://github.com/scrapy/scrapy/issues/4015){.reference
    .external})
:::

::: {#id88 .section}
[]{#id89}

##### Deprecations[¶](#id88 "Permalink to this heading"){.headerlink}

-   The [LevelDB](https://github.com/google/leveldb){.reference
    .external} storage backend
    ([`scrapy.extensions.httpcache.LeveldbCacheStorage`{.docutils
    .literal .notranslate}]{.pre}) of [[`HttpCacheMiddleware`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware "scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware"){.reference
    .internal} is deprecated ([issue
    4085](https://github.com/scrapy/scrapy/issues/4085){.reference
    .external}, [issue
    4092](https://github.com/scrapy/scrapy/issues/4092){.reference
    .external})

-   Use of the undocumented
    [`SCRAPY_PICKLED_SETTINGS_TO_OVERRIDE`{.docutils .literal
    .notranslate}]{.pre} environment variable is deprecated ([issue
    3910](https://github.com/scrapy/scrapy/issues/3910){.reference
    .external})

-   [`scrapy.item.DictItem`{.docutils .literal .notranslate}]{.pre} is
    deprecated, use [`Item`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} instead ([issue
    3999](https://github.com/scrapy/scrapy/issues/3999){.reference
    .external})
:::

::: {#other-changes .section}
##### Other changes[¶](#other-changes "Permalink to this heading"){.headerlink}

-   Minimum versions of optional Scrapy requirements that are covered by
    continuous integration tests have been updated:

    -   [botocore](https://github.com/boto/botocore){.reference
        .external} 1.3.23

    -   [Pillow](https://python-pillow.org/){.reference .external} 3.4.2

    Lower versions of these optional requirements may work, but it is
    not guaranteed ([issue
    3892](https://github.com/scrapy/scrapy/issues/3892){.reference
    .external})

-   GitHub templates for bug reports and feature requests ([issue
    3126](https://github.com/scrapy/scrapy/issues/3126){.reference
    .external}, [issue
    3471](https://github.com/scrapy/scrapy/issues/3471){.reference
    .external}, [issue
    3749](https://github.com/scrapy/scrapy/issues/3749){.reference
    .external}, [issue
    3754](https://github.com/scrapy/scrapy/issues/3754){.reference
    .external})

-   Continuous integration fixes ([issue
    3923](https://github.com/scrapy/scrapy/issues/3923){.reference
    .external})

-   Code cleanup ([issue
    3391](https://github.com/scrapy/scrapy/issues/3391){.reference
    .external}, [issue
    3907](https://github.com/scrapy/scrapy/issues/3907){.reference
    .external}, [issue
    3946](https://github.com/scrapy/scrapy/issues/3946){.reference
    .external}, [issue
    3950](https://github.com/scrapy/scrapy/issues/3950){.reference
    .external}, [issue
    4023](https://github.com/scrapy/scrapy/issues/4023){.reference
    .external}, [issue
    4031](https://github.com/scrapy/scrapy/issues/4031){.reference
    .external})
:::
:::

::: {#scrapy-1-7-4-2019-10-21 .section}
[]{#release-1-7-4}

#### Scrapy 1.7.4 (2019-10-21)[¶](#scrapy-1-7-4-2019-10-21 "Permalink to this heading"){.headerlink}

Revert the fix for [issue
3804](https://github.com/scrapy/scrapy/issues/3804){.reference
.external} ([issue
3819](https://github.com/scrapy/scrapy/issues/3819){.reference
.external}), which has a few undesired side effects ([issue
3897](https://github.com/scrapy/scrapy/issues/3897){.reference
.external}, [issue
3976](https://github.com/scrapy/scrapy/issues/3976){.reference
.external}).

As a result, when an item loader is initialized with an item,
[[`ItemLoader.load_item()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
.internal} once again makes later calls to
[[`ItemLoader.get_output_value()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.get_output_value "scrapy.loader.ItemLoader.get_output_value"){.reference
.internal} or [[`ItemLoader.load_item()`{.xref .py .py-meth .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
.internal} return empty data.
:::

::: {#scrapy-1-7-3-2019-08-01 .section}
[]{#release-1-7-3}

#### Scrapy 1.7.3 (2019-08-01)[¶](#scrapy-1-7-3-2019-08-01 "Permalink to this heading"){.headerlink}

Enforce lxml 4.3.5 or lower for Python 3.4 ([issue
3912](https://github.com/scrapy/scrapy/issues/3912){.reference
.external}, [issue
3918](https://github.com/scrapy/scrapy/issues/3918){.reference
.external}).
:::

::: {#scrapy-1-7-2-2019-07-23 .section}
[]{#release-1-7-2}

#### Scrapy 1.7.2 (2019-07-23)[¶](#scrapy-1-7-2-2019-07-23 "Permalink to this heading"){.headerlink}

Fix Python 2 support ([issue
3889](https://github.com/scrapy/scrapy/issues/3889){.reference
.external}, [issue
3893](https://github.com/scrapy/scrapy/issues/3893){.reference
.external}, [issue
3896](https://github.com/scrapy/scrapy/issues/3896){.reference
.external}).
:::

::: {#scrapy-1-7-1-2019-07-18 .section}
[]{#release-1-7-1}

#### Scrapy 1.7.1 (2019-07-18)[¶](#scrapy-1-7-1-2019-07-18 "Permalink to this heading"){.headerlink}

Re-packaging of Scrapy 1.7.0, which was missing some changes in PyPI.
:::

::: {#scrapy-1-7-0-2019-07-18 .section}
[]{#release-1-7-0}

#### Scrapy 1.7.0 (2019-07-18)[¶](#scrapy-1-7-0-2019-07-18 "Permalink to this heading"){.headerlink}

::: {.admonition .note}
Note

Make sure you install Scrapy 1.7.1. The Scrapy 1.7.0 package in PyPI is
the result of an erroneous commit tagging and does not include all the
changes described below.
:::

Highlights:

-   Improvements for crawls targeting multiple domains

-   A cleaner way to pass arguments to callbacks

-   A new class for JSON requests

-   Improvements for rule-based spiders

-   New features for feed exports

::: {#id90 .section}
##### Backward-incompatible changes[¶](#id90 "Permalink to this heading"){.headerlink}

-   [`429`{.docutils .literal .notranslate}]{.pre} is now part of the
    [[`RETRY_HTTP_CODES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-RETRY_HTTP_CODES){.hoverxref
    .tooltip .reference .internal} setting by default

    This change is **backward incompatible**. If you don't want to retry
    [`429`{.docutils .literal .notranslate}]{.pre}, you must override
    [[`RETRY_HTTP_CODES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-RETRY_HTTP_CODES){.hoverxref
    .tooltip .reference .internal} accordingly.

-   [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal}, [[`CrawlerRunner.crawl`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner.crawl "scrapy.crawler.CrawlerRunner.crawl"){.reference
    .internal} and [[`CrawlerRunner.create_crawler`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner.create_crawler "scrapy.crawler.CrawlerRunner.create_crawler"){.reference
    .internal} no longer accept a [[`Spider`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} subclass instance, they only accept a [[`Spider`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} subclass now.

    [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} subclass instances were never meant to work, and they
    were not working as one would expect: instead of using the passed
    [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} subclass instance, their [`from_crawler`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} method was called
    to generate a new instance.

-   Non-default values for the [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref
    .tooltip .reference .internal} setting may stop working. Scheduler
    priority queue classes now need to handle [[`Request`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} objects instead of arbitrary Python data structures.

-   An additional [`crawler`{.docutils .literal .notranslate}]{.pre}
    parameter has been added to the [`__init__`{.docutils .literal
    .notranslate}]{.pre} method of the [[`Scheduler`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.core.scheduler.Scheduler "scrapy.core.scheduler.Scheduler"){.reference
    .internal} class. Custom scheduler subclasses which don't accept
    arbitrary parameters in their [`__init__`{.docutils .literal
    .notranslate}]{.pre} method might break because of this change.

    For more information, see [[`SCHEDULER`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER){.hoverxref
    .tooltip .reference .internal}.

See also [[Deprecation removals]{.std .std-ref}](#id94){.hoverxref
.tooltip .reference .internal} below.
:::

::: {#id91 .section}
##### New features[¶](#id91 "Permalink to this heading"){.headerlink}

-   A new scheduler priority queue,
    [`scrapy.pqueues.DownloaderAwarePriorityQueue`{.docutils .literal
    .notranslate}]{.pre}, may be [[enabled]{.std
    .std-ref}](index.html#broad-crawls-scheduler-priority-queue){.hoverxref
    .tooltip .reference .internal} for a significant scheduling
    improvement on crawls targeting multiple web domains, at the cost of
    no [[`CONCURRENT_REQUESTS_PER_IP`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
    .tooltip .reference .internal} support ([issue
    3520](https://github.com/scrapy/scrapy/issues/3520){.reference
    .external})

-   A new [[`Request.cb_kwargs`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
    .internal} attribute provides a cleaner way to pass keyword
    arguments to callback methods ([issue
    1138](https://github.com/scrapy/scrapy/issues/1138){.reference
    .external}, [issue
    3563](https://github.com/scrapy/scrapy/issues/3563){.reference
    .external})

-   A new [[`JSONRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.JsonRequest "scrapy.http.JsonRequest"){.reference
    .internal} class offers a more convenient way to build JSON requests
    ([issue
    3504](https://github.com/scrapy/scrapy/issues/3504){.reference
    .external}, [issue
    3505](https://github.com/scrapy/scrapy/issues/3505){.reference
    .external})

-   A [`process_request`{.docutils .literal .notranslate}]{.pre}
    callback passed to the [[`Rule`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method now receives the [[`Response`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} object that originated the request as its second argument
    ([issue
    3682](https://github.com/scrapy/scrapy/issues/3682){.reference
    .external})

-   A new [`restrict_text`{.docutils .literal .notranslate}]{.pre}
    parameter for the [[`LinkExtractor`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method allows filtering links by linking text ([issue
    3622](https://github.com/scrapy/scrapy/issues/3622){.reference
    .external}, [issue
    3635](https://github.com/scrapy/scrapy/issues/3635){.reference
    .external})

-   A new [[`FEED_STORAGE_S3_ACL`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_STORAGE_S3_ACL){.hoverxref
    .tooltip .reference .internal} setting allows defining a custom ACL
    for feeds exported to Amazon S3 ([issue
    3607](https://github.com/scrapy/scrapy/issues/3607){.reference
    .external})

-   A new [[`FEED_STORAGE_FTP_ACTIVE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_STORAGE_FTP_ACTIVE){.hoverxref
    .tooltip .reference .internal} setting allows using FTP's active
    connection mode for feeds exported to FTP servers ([issue
    3829](https://github.com/scrapy/scrapy/issues/3829){.reference
    .external})

-   A new [[`METAREFRESH_IGNORE_TAGS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-METAREFRESH_IGNORE_TAGS){.hoverxref
    .tooltip .reference .internal} setting allows overriding which HTML
    tags are ignored when searching a response for HTML meta tags that
    trigger a redirect ([issue
    1422](https://github.com/scrapy/scrapy/issues/1422){.reference
    .external}, [issue
    3768](https://github.com/scrapy/scrapy/issues/3768){.reference
    .external})

-   A new [[`redirect_reasons`{.xref .std .std-reqmeta .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-redirect_reasons){.hoverxref
    .tooltip .reference .internal} request meta key exposes the reason
    (status code, meta refresh) behind every followed redirect ([issue
    3581](https://github.com/scrapy/scrapy/issues/3581){.reference
    .external}, [issue
    3687](https://github.com/scrapy/scrapy/issues/3687){.reference
    .external})

-   The [`SCRAPY_CHECK`{.docutils .literal .notranslate}]{.pre} variable
    is now set to the [`true`{.docutils .literal .notranslate}]{.pre}
    string during runs of the [[`check`{.xref .std .std-command
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-check){.hoverxref
    .tooltip .reference .internal} command, which allows [[detecting
    contract check runs from code]{.std
    .std-ref}](index.html#detecting-contract-check-runs){.hoverxref
    .tooltip .reference .internal} ([issue
    3704](https://github.com/scrapy/scrapy/issues/3704){.reference
    .external}, [issue
    3739](https://github.com/scrapy/scrapy/issues/3739){.reference
    .external})

-   A new [`Item.deepcopy()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} method makes it easier to [[deep-copy
    items]{.std .std-ref}](index.html#copying-items){.hoverxref .tooltip
    .reference .internal} ([issue
    1493](https://github.com/scrapy/scrapy/issues/1493){.reference
    .external}, [issue
    3671](https://github.com/scrapy/scrapy/issues/3671){.reference
    .external})

-   [[`CoreStats`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.extensions.corestats.CoreStats "scrapy.extensions.corestats.CoreStats"){.reference
    .internal} also logs [`elapsed_time_seconds`{.docutils .literal
    .notranslate}]{.pre} now ([issue
    3638](https://github.com/scrapy/scrapy/issues/3638){.reference
    .external})

-   Exceptions from [[`ItemLoader`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
    .internal} [[input and output processors]{.std
    .std-ref}](index.html#topics-loaders-processors){.hoverxref .tooltip
    .reference .internal} are now more verbose ([issue
    3836](https://github.com/scrapy/scrapy/issues/3836){.reference
    .external}, [issue
    3840](https://github.com/scrapy/scrapy/issues/3840){.reference
    .external})

-   [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal}, [[`CrawlerRunner.crawl`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner.crawl "scrapy.crawler.CrawlerRunner.crawl"){.reference
    .internal} and [[`CrawlerRunner.create_crawler`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner.create_crawler "scrapy.crawler.CrawlerRunner.create_crawler"){.reference
    .internal} now fail gracefully if they receive a [[`Spider`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} subclass instance instead of the subclass itself ([issue
    2283](https://github.com/scrapy/scrapy/issues/2283){.reference
    .external}, [issue
    3610](https://github.com/scrapy/scrapy/issues/3610){.reference
    .external}, [issue
    3872](https://github.com/scrapy/scrapy/issues/3872){.reference
    .external})
:::

::: {#id92 .section}
##### Bug fixes[¶](#id92 "Permalink to this heading"){.headerlink}

-   [[`process_spider_exception()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_exception"){.reference
    .internal} is now also invoked for generators ([issue
    220](https://github.com/scrapy/scrapy/issues/220){.reference
    .external}, [issue
    2061](https://github.com/scrapy/scrapy/issues/2061){.reference
    .external})

-   System exceptions like
    [KeyboardInterrupt](https://docs.python.org/3/library/exceptions.html#KeyboardInterrupt){.reference
    .external} are no longer caught ([issue
    3726](https://github.com/scrapy/scrapy/issues/3726){.reference
    .external})

-   [[`ItemLoader.load_item()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
    .internal} no longer makes later calls to
    [[`ItemLoader.get_output_value()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.get_output_value "scrapy.loader.ItemLoader.get_output_value"){.reference
    .internal} or [[`ItemLoader.load_item()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader.load_item "scrapy.loader.ItemLoader.load_item"){.reference
    .internal} return empty data ([issue
    3804](https://github.com/scrapy/scrapy/issues/3804){.reference
    .external}, [issue
    3819](https://github.com/scrapy/scrapy/issues/3819){.reference
    .external})

-   The images pipeline ([[`ImagesPipeline`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline "scrapy.pipelines.images.ImagesPipeline"){.reference
    .internal}) no longer ignores these Amazon S3 settings:
    [[`AWS_ENDPOINT_URL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_ENDPOINT_URL){.hoverxref
    .tooltip .reference .internal}, [[`AWS_REGION_NAME`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_REGION_NAME){.hoverxref
    .tooltip .reference .internal}, [[`AWS_USE_SSL`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_USE_SSL){.hoverxref
    .tooltip .reference .internal}, [[`AWS_VERIFY`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_VERIFY){.hoverxref
    .tooltip .reference .internal} ([issue
    3625](https://github.com/scrapy/scrapy/issues/3625){.reference
    .external})

-   Fixed a memory leak in
    [`scrapy.pipelines.media.MediaPipeline`{.docutils .literal
    .notranslate}]{.pre} affecting, for example, non-200 responses and
    exceptions from custom middlewares ([issue
    3813](https://github.com/scrapy/scrapy/issues/3813){.reference
    .external})

-   Requests with private callbacks are now correctly unserialized from
    disk ([issue
    3790](https://github.com/scrapy/scrapy/issues/3790){.reference
    .external})

-   [`FormRequest.from_response()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} now handles invalid methods like major web
    browsers ([issue
    3777](https://github.com/scrapy/scrapy/issues/3777){.reference
    .external}, [issue
    3794](https://github.com/scrapy/scrapy/issues/3794){.reference
    .external})
:::

::: {#id93 .section}
##### Documentation[¶](#id93 "Permalink to this heading"){.headerlink}

-   A new topic, [[Selecting dynamically-loaded content]{.std
    .std-ref}](index.html#topics-dynamic-content){.hoverxref .tooltip
    .reference .internal}, covers recommended approaches to read
    dynamically-loaded data ([issue
    3703](https://github.com/scrapy/scrapy/issues/3703){.reference
    .external})

-   [[Broad Crawls]{.std
    .std-ref}](index.html#topics-broad-crawls){.hoverxref .tooltip
    .reference .internal} now features information about memory usage
    ([issue
    1264](https://github.com/scrapy/scrapy/issues/1264){.reference
    .external}, [issue
    3866](https://github.com/scrapy/scrapy/issues/3866){.reference
    .external})

-   The documentation of [[`Rule`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
    .internal} now covers how to access the text of a link when using
    [[`CrawlSpider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.CrawlSpider "scrapy.spiders.CrawlSpider"){.reference
    .internal} ([issue
    3711](https://github.com/scrapy/scrapy/issues/3711){.reference
    .external}, [issue
    3712](https://github.com/scrapy/scrapy/issues/3712){.reference
    .external})

-   A new section, [[Writing your own storage backend]{.std
    .std-ref}](index.html#httpcache-storage-custom){.hoverxref .tooltip
    .reference .internal}, covers writing a custom cache storage backend
    for [[`HttpCacheMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware "scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware"){.reference
    .internal} ([issue
    3683](https://github.com/scrapy/scrapy/issues/3683){.reference
    .external}, [issue
    3692](https://github.com/scrapy/scrapy/issues/3692){.reference
    .external})

-   A new [[FAQ]{.std .std-ref}](index.html#faq){.hoverxref .tooltip
    .reference .internal} entry, [[How to split an item into multiple
    items in an item pipeline?]{.std
    .std-ref}](index.html#faq-split-item){.hoverxref .tooltip .reference
    .internal}, explains what to do when you want to split an item into
    multiple items from an item pipeline ([issue
    2240](https://github.com/scrapy/scrapy/issues/2240){.reference
    .external}, [issue
    3672](https://github.com/scrapy/scrapy/issues/3672){.reference
    .external})

-   Updated the [[FAQ entry about crawl order]{.std
    .std-ref}](index.html#faq-bfo-dfo){.hoverxref .tooltip .reference
    .internal} to explain why the first few requests rarely follow the
    desired order ([issue
    1739](https://github.com/scrapy/scrapy/issues/1739){.reference
    .external}, [issue
    3621](https://github.com/scrapy/scrapy/issues/3621){.reference
    .external})

-   The [[`LOGSTATS_INTERVAL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOGSTATS_INTERVAL){.hoverxref
    .tooltip .reference .internal} setting ([issue
    3730](https://github.com/scrapy/scrapy/issues/3730){.reference
    .external}), the [[`FilesPipeline.file_path`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.files.FilesPipeline.file_path "scrapy.pipelines.files.FilesPipeline.file_path"){.reference
    .internal} and [[`ImagesPipeline.file_path`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline.file_path "scrapy.pipelines.images.ImagesPipeline.file_path"){.reference
    .internal} methods ([issue
    2253](https://github.com/scrapy/scrapy/issues/2253){.reference
    .external}, [issue
    3609](https://github.com/scrapy/scrapy/issues/3609){.reference
    .external}) and the [[`Crawler.stop()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.stop "scrapy.crawler.Crawler.stop"){.reference
    .internal} method ([issue
    3842](https://github.com/scrapy/scrapy/issues/3842){.reference
    .external}) are now documented

-   Some parts of the documentation that were confusing or misleading
    are now clearer ([issue
    1347](https://github.com/scrapy/scrapy/issues/1347){.reference
    .external}, [issue
    1789](https://github.com/scrapy/scrapy/issues/1789){.reference
    .external}, [issue
    2289](https://github.com/scrapy/scrapy/issues/2289){.reference
    .external}, [issue
    3069](https://github.com/scrapy/scrapy/issues/3069){.reference
    .external}, [issue
    3615](https://github.com/scrapy/scrapy/issues/3615){.reference
    .external}, [issue
    3626](https://github.com/scrapy/scrapy/issues/3626){.reference
    .external}, [issue
    3668](https://github.com/scrapy/scrapy/issues/3668){.reference
    .external}, [issue
    3670](https://github.com/scrapy/scrapy/issues/3670){.reference
    .external}, [issue
    3673](https://github.com/scrapy/scrapy/issues/3673){.reference
    .external}, [issue
    3728](https://github.com/scrapy/scrapy/issues/3728){.reference
    .external}, [issue
    3762](https://github.com/scrapy/scrapy/issues/3762){.reference
    .external}, [issue
    3861](https://github.com/scrapy/scrapy/issues/3861){.reference
    .external}, [issue
    3882](https://github.com/scrapy/scrapy/issues/3882){.reference
    .external})

-   Minor documentation fixes ([issue
    3648](https://github.com/scrapy/scrapy/issues/3648){.reference
    .external}, [issue
    3649](https://github.com/scrapy/scrapy/issues/3649){.reference
    .external}, [issue
    3662](https://github.com/scrapy/scrapy/issues/3662){.reference
    .external}, [issue
    3674](https://github.com/scrapy/scrapy/issues/3674){.reference
    .external}, [issue
    3676](https://github.com/scrapy/scrapy/issues/3676){.reference
    .external}, [issue
    3694](https://github.com/scrapy/scrapy/issues/3694){.reference
    .external}, [issue
    3724](https://github.com/scrapy/scrapy/issues/3724){.reference
    .external}, [issue
    3764](https://github.com/scrapy/scrapy/issues/3764){.reference
    .external}, [issue
    3767](https://github.com/scrapy/scrapy/issues/3767){.reference
    .external}, [issue
    3791](https://github.com/scrapy/scrapy/issues/3791){.reference
    .external}, [issue
    3797](https://github.com/scrapy/scrapy/issues/3797){.reference
    .external}, [issue
    3806](https://github.com/scrapy/scrapy/issues/3806){.reference
    .external}, [issue
    3812](https://github.com/scrapy/scrapy/issues/3812){.reference
    .external})
:::

::: {#id94 .section}
[]{#id95}

##### Deprecation removals[¶](#id94 "Permalink to this heading"){.headerlink}

The following deprecated APIs have been removed ([issue
3578](https://github.com/scrapy/scrapy/issues/3578){.reference
.external}):

-   [`scrapy.conf`{.docutils .literal .notranslate}]{.pre} (use
    [[`Crawler.settings`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.settings "scrapy.crawler.Crawler.settings"){.reference
    .internal})

-   From [`scrapy.core.downloader.handlers`{.docutils .literal
    .notranslate}]{.pre}:

    -   [`http.HttpDownloadHandler`{.docutils .literal
        .notranslate}]{.pre} (use
        [`http10.HTTP10DownloadHandler`{.docutils .literal
        .notranslate}]{.pre})

-   [`scrapy.loader.ItemLoader._get_values`{.docutils .literal
    .notranslate}]{.pre} (use [`_get_xpathvalues`{.docutils .literal
    .notranslate}]{.pre})

-   [`scrapy.loader.XPathItemLoader`{.docutils .literal
    .notranslate}]{.pre} (use [[`ItemLoader`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.loader.ItemLoader "scrapy.loader.ItemLoader"){.reference
    .internal})

-   [`scrapy.log`{.docutils .literal .notranslate}]{.pre} (see
    [[Logging]{.std .std-ref}](index.html#topics-logging){.hoverxref
    .tooltip .reference .internal})

-   From [`scrapy.pipelines`{.docutils .literal .notranslate}]{.pre}:

    -   [`files.FilesPipeline.file_key`{.docutils .literal
        .notranslate}]{.pre} (use [`file_path`{.docutils .literal
        .notranslate}]{.pre})

    -   [`images.ImagesPipeline.file_key`{.docutils .literal
        .notranslate}]{.pre} (use [`file_path`{.docutils .literal
        .notranslate}]{.pre})

    -   [`images.ImagesPipeline.image_key`{.docutils .literal
        .notranslate}]{.pre} (use [`file_path`{.docutils .literal
        .notranslate}]{.pre})

    -   [`images.ImagesPipeline.thumb_key`{.docutils .literal
        .notranslate}]{.pre} (use [`thumb_path`{.docutils .literal
        .notranslate}]{.pre})

-   From both [`scrapy.selector`{.docutils .literal .notranslate}]{.pre}
    and [`scrapy.selector.lxmlsel`{.docutils .literal
    .notranslate}]{.pre}:

    -   [`HtmlXPathSelector`{.docutils .literal .notranslate}]{.pre}
        (use [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal})

    -   [`XmlXPathSelector`{.docutils .literal .notranslate}]{.pre} (use
        [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal})

    -   [`XPathSelector`{.docutils .literal .notranslate}]{.pre} (use
        [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal})

    -   [`XPathSelectorList`{.docutils .literal .notranslate}]{.pre}
        (use [[`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
        .internal})

-   From [`scrapy.selector.csstranslator`{.docutils .literal
    .notranslate}]{.pre}:

    -   [`ScrapyGenericTranslator`{.docutils .literal
        .notranslate}]{.pre} (use
        [parsel.csstranslator.GenericTranslator](https://parsel.readthedocs.io/en/latest/parsel.html#parsel.csstranslator.GenericTranslator){.reference
        .external})

    -   [`ScrapyHTMLTranslator`{.docutils .literal .notranslate}]{.pre}
        (use
        [parsel.csstranslator.HTMLTranslator](https://parsel.readthedocs.io/en/latest/parsel.html#parsel.csstranslator.HTMLTranslator){.reference
        .external})

    -   [`ScrapyXPathExpr`{.docutils .literal .notranslate}]{.pre} (use
        [parsel.csstranslator.XPathExpr](https://parsel.readthedocs.io/en/latest/parsel.html#parsel.csstranslator.XPathExpr){.reference
        .external})

-   From [[`Selector`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
    .internal}:

    -   [`_root`{.docutils .literal .notranslate}]{.pre} (both the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method
        argument and the object property, use [`root`{.docutils .literal
        .notranslate}]{.pre})

    -   [`extract_unquoted`{.docutils .literal .notranslate}]{.pre} (use
        [`getall`{.docutils .literal .notranslate}]{.pre})

    -   [`select`{.docutils .literal .notranslate}]{.pre} (use
        [`xpath`{.docutils .literal .notranslate}]{.pre})

-   From [[`SelectorList`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
    .internal}:

    -   [`extract_unquoted`{.docutils .literal .notranslate}]{.pre} (use
        [`getall`{.docutils .literal .notranslate}]{.pre})

    -   [`select`{.docutils .literal .notranslate}]{.pre} (use
        [`xpath`{.docutils .literal .notranslate}]{.pre})

    -   [`x`{.docutils .literal .notranslate}]{.pre} (use
        [`xpath`{.docutils .literal .notranslate}]{.pre})

-   [`scrapy.spiders.BaseSpider`{.docutils .literal .notranslate}]{.pre}
    (use [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal})

-   From [[`Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
    .internal} (and subclasses):

    -   [`DOWNLOAD_DELAY`{.docutils .literal .notranslate}]{.pre} (use
        [[download_delay]{.std
        .std-ref}](index.html#spider-download-delay-attribute){.hoverxref
        .tooltip .reference .internal})

    -   [`set_crawler`{.docutils .literal .notranslate}]{.pre} (use
        [`from_crawler()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre})

-   [`scrapy.spiders.spiders`{.docutils .literal .notranslate}]{.pre}
    (use [[`SpiderLoader`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiderloader.SpiderLoader "scrapy.spiderloader.SpiderLoader"){.reference
    .internal})

-   [`scrapy.telnet`{.docutils .literal .notranslate}]{.pre} (use
    [[`scrapy.extensions.telnet`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](index.html#module-scrapy.extensions.telnet "scrapy.extensions.telnet: Telnet console"){.reference
    .internal})

-   From [`scrapy.utils.python`{.docutils .literal .notranslate}]{.pre}:

    -   [`str_to_unicode`{.docutils .literal .notranslate}]{.pre} (use
        [`to_unicode`{.docutils .literal .notranslate}]{.pre})

    -   [`unicode_to_str`{.docutils .literal .notranslate}]{.pre} (use
        [`to_bytes`{.docutils .literal .notranslate}]{.pre})

-   [`scrapy.utils.response.body_or_str`{.docutils .literal
    .notranslate}]{.pre}

The following deprecated settings have also been removed ([issue
3578](https://github.com/scrapy/scrapy/issues/3578){.reference
.external}):

-   [`SPIDER_MANAGER_CLASS`{.docutils .literal .notranslate}]{.pre} (use
    [[`SPIDER_LOADER_CLASS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_LOADER_CLASS){.hoverxref
    .tooltip .reference .internal})
:::

::: {#id96 .section}
[]{#id97}

##### Deprecations[¶](#id96 "Permalink to this heading"){.headerlink}

-   The [`queuelib.PriorityQueue`{.docutils .literal
    .notranslate}]{.pre} value for the
    [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref
    .tooltip .reference .internal} setting is deprecated. Use
    [`scrapy.pqueues.ScrapyPriorityQueue`{.docutils .literal
    .notranslate}]{.pre} instead.

-   [`process_request`{.docutils .literal .notranslate}]{.pre} callbacks
    passed to [[`Rule`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
    .internal} that do not accept two arguments are deprecated.

-   The following modules are deprecated:

    -   [`scrapy.utils.http`{.docutils .literal .notranslate}]{.pre}
        (use
        [w3lib.http](https://w3lib.readthedocs.io/en/latest/w3lib.html#module-w3lib.http){.reference
        .external})

    -   [`scrapy.utils.markup`{.docutils .literal .notranslate}]{.pre}
        (use
        [w3lib.html](https://w3lib.readthedocs.io/en/latest/w3lib.html#module-w3lib.html){.reference
        .external})

    -   [`scrapy.utils.multipart`{.docutils .literal
        .notranslate}]{.pre} (use
        [urllib3](https://urllib3.readthedocs.io/en/latest/index.html){.reference
        .external})

-   The [`scrapy.utils.datatypes.MergeDict`{.docutils .literal
    .notranslate}]{.pre} class is deprecated for Python 3 code bases.
    Use [[`ChainMap`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/collections.html#collections.ChainMap "(in Python v3.12)"){.reference
    .external} instead. ([issue
    3878](https://github.com/scrapy/scrapy/issues/3878){.reference
    .external})

-   The [`scrapy.utils.gz.is_gzipped`{.docutils .literal
    .notranslate}]{.pre} function is deprecated. Use
    [`scrapy.utils.gz.gzip_magic_number`{.docutils .literal
    .notranslate}]{.pre} instead.
:::

::: {#id98 .section}
##### Other changes[¶](#id98 "Permalink to this heading"){.headerlink}

-   It is now possible to run all tests from the same
    [tox](https://pypi.org/project/tox/){.reference .external}
    environment in parallel; the documentation now covers [[this and
    other ways to run tests]{.std
    .std-ref}](index.html#running-tests){.hoverxref .tooltip .reference
    .internal} ([issue
    3707](https://github.com/scrapy/scrapy/issues/3707){.reference
    .external})

-   It is now possible to generate an API documentation coverage report
    ([issue
    3806](https://github.com/scrapy/scrapy/issues/3806){.reference
    .external}, [issue
    3810](https://github.com/scrapy/scrapy/issues/3810){.reference
    .external}, [issue
    3860](https://github.com/scrapy/scrapy/issues/3860){.reference
    .external})

-   The [[documentation policies]{.std
    .std-ref}](index.html#documentation-policies){.hoverxref .tooltip
    .reference .internal} now require
    [docstrings](https://docs.python.org/3/glossary.html#term-docstring){.reference
    .external} ([issue
    3701](https://github.com/scrapy/scrapy/issues/3701){.reference
    .external}) that follow [PEP
    257](https://www.python.org/dev/peps/pep-0257/){.reference
    .external} ([issue
    3748](https://github.com/scrapy/scrapy/issues/3748){.reference
    .external})

-   Internal fixes and cleanup ([issue
    3629](https://github.com/scrapy/scrapy/issues/3629){.reference
    .external}, [issue
    3643](https://github.com/scrapy/scrapy/issues/3643){.reference
    .external}, [issue
    3684](https://github.com/scrapy/scrapy/issues/3684){.reference
    .external}, [issue
    3698](https://github.com/scrapy/scrapy/issues/3698){.reference
    .external}, [issue
    3734](https://github.com/scrapy/scrapy/issues/3734){.reference
    .external}, [issue
    3735](https://github.com/scrapy/scrapy/issues/3735){.reference
    .external}, [issue
    3736](https://github.com/scrapy/scrapy/issues/3736){.reference
    .external}, [issue
    3737](https://github.com/scrapy/scrapy/issues/3737){.reference
    .external}, [issue
    3809](https://github.com/scrapy/scrapy/issues/3809){.reference
    .external}, [issue
    3821](https://github.com/scrapy/scrapy/issues/3821){.reference
    .external}, [issue
    3825](https://github.com/scrapy/scrapy/issues/3825){.reference
    .external}, [issue
    3827](https://github.com/scrapy/scrapy/issues/3827){.reference
    .external}, [issue
    3833](https://github.com/scrapy/scrapy/issues/3833){.reference
    .external}, [issue
    3857](https://github.com/scrapy/scrapy/issues/3857){.reference
    .external}, [issue
    3877](https://github.com/scrapy/scrapy/issues/3877){.reference
    .external})
:::
:::

::: {#scrapy-1-6-0-2019-01-30 .section}
[]{#release-1-6-0}

#### Scrapy 1.6.0 (2019-01-30)[¶](#scrapy-1-6-0-2019-01-30 "Permalink to this heading"){.headerlink}

Highlights:

-   better Windows support;

-   Python 3.7 compatibility;

-   big documentation improvements, including a switch from
    [`.extract_first()`{.docutils .literal .notranslate}]{.pre} +
    [`.extract()`{.docutils .literal .notranslate}]{.pre} API to
    [`.get()`{.docutils .literal .notranslate}]{.pre} +
    [`.getall()`{.docutils .literal .notranslate}]{.pre} API;

-   feed exports, FilePipeline and MediaPipeline improvements;

-   better extensibility: [[`item_error`{.xref .std .std-signal
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-item_error){.hoverxref
    .tooltip .reference .internal} and
    [[`request_reached_downloader`{.xref .std .std-signal .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-signal-request_reached_downloader){.hoverxref
    .tooltip .reference .internal} signals; [`from_crawler`{.docutils
    .literal .notranslate}]{.pre} support for feed exporters, feed
    storages and dupefilters.

-   [`scrapy.contracts`{.docutils .literal .notranslate}]{.pre} fixes
    and new features;

-   telnet console security improvements, first released as a backport
    in [[Scrapy 1.5.2 (2019-01-22)]{.std
    .std-ref}](#release-1-5-2){.hoverxref .tooltip .reference
    .internal};

-   clean-up of the deprecated code;

-   various bug fixes, small new features and usability improvements
    across the codebase.

::: {#selector-api-changes .section}
##### Selector API changes[¶](#selector-api-changes "Permalink to this heading"){.headerlink}

While these are not changes in Scrapy itself, but rather in the
[parsel](https://github.com/scrapy/parsel){.reference .external} library
which Scrapy uses for xpath/css selectors, these changes are worth
mentioning here. Scrapy now depends on parsel \>= 1.5, and Scrapy
documentation is updated to follow recent [`parsel`{.docutils .literal
.notranslate}]{.pre} API conventions.

Most visible change is that [`.get()`{.docutils .literal
.notranslate}]{.pre} and [`.getall()`{.docutils .literal
.notranslate}]{.pre} selector methods are now preferred over
[`.extract_first()`{.docutils .literal .notranslate}]{.pre} and
[`.extract()`{.docutils .literal .notranslate}]{.pre}. We feel that
these new methods result in a more concise and readable code. See
[[extract() and extract_first()]{.std
.std-ref}](index.html#old-extraction-api){.hoverxref .tooltip .reference
.internal} for more details.

::: {.admonition .note}
Note

There are currently **no plans** to deprecate [`.extract()`{.docutils
.literal .notranslate}]{.pre} and [`.extract_first()`{.docutils .literal
.notranslate}]{.pre} methods.
:::

Another useful new feature is the introduction of
[`Selector.attrib`{.docutils .literal .notranslate}]{.pre} and
[`SelectorList.attrib`{.docutils .literal .notranslate}]{.pre}
properties, which make it easier to get attributes of HTML elements. See
[[Selecting element attributes]{.std
.std-ref}](index.html#selecting-attributes){.hoverxref .tooltip
.reference .internal}.

CSS selectors are cached in parsel \>= 1.5, which makes them faster when
the same CSS path is used many times. This is very common in case of
Scrapy spiders: callbacks are usually called several times, on different
pages.

If you're using custom [`Selector`{.docutils .literal
.notranslate}]{.pre} or [`SelectorList`{.docutils .literal
.notranslate}]{.pre} subclasses, a **backward incompatible** change in
parsel may affect your code. See [parsel
changelog](https://parsel.readthedocs.io/en/latest/history.html){.reference
.external} for a detailed description, as well as for the full list of
improvements.
:::

::: {#telnet-console .section}
##### Telnet console[¶](#telnet-console "Permalink to this heading"){.headerlink}

**Backward incompatible**: Scrapy's telnet console now requires username
and password. See [[Telnet Console]{.std
.std-ref}](index.html#topics-telnetconsole){.hoverxref .tooltip
.reference .internal} for more details. This change fixes a **security
issue**; see [[Scrapy 1.5.2 (2019-01-22)]{.std
.std-ref}](#release-1-5-2){.hoverxref .tooltip .reference .internal}
release notes for details.
:::

::: {#new-extensibility-features .section}
##### New extensibility features[¶](#new-extensibility-features "Permalink to this heading"){.headerlink}

-   [`from_crawler`{.docutils .literal .notranslate}]{.pre} support is
    added to feed exporters and feed storages. This, among other things,
    allows to access Scrapy settings from custom feed storages and
    exporters ([issue
    1605](https://github.com/scrapy/scrapy/issues/1605){.reference
    .external}, [issue
    3348](https://github.com/scrapy/scrapy/issues/3348){.reference
    .external}).

-   [`from_crawler`{.docutils .literal .notranslate}]{.pre} support is
    added to dupefilters ([issue
    2956](https://github.com/scrapy/scrapy/issues/2956){.reference
    .external}); this allows to access e.g. settings or a spider from a
    dupefilter.

-   [[`item_error`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-item_error){.hoverxref
    .tooltip .reference .internal} is fired when an error happens in a
    pipeline ([issue
    3256](https://github.com/scrapy/scrapy/issues/3256){.reference
    .external});

-   [[`request_reached_downloader`{.xref .std .std-signal .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-signal-request_reached_downloader){.hoverxref
    .tooltip .reference .internal} is fired when Downloader gets a new
    Request; this signal can be useful e.g. for custom Schedulers
    ([issue
    3393](https://github.com/scrapy/scrapy/issues/3393){.reference
    .external}).

-   new SitemapSpider [[`sitemap_filter()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.SitemapSpider.sitemap_filter "scrapy.spiders.SitemapSpider.sitemap_filter"){.reference
    .internal} method which allows to select sitemap entries based on
    their attributes in SitemapSpider subclasses ([issue
    3512](https://github.com/scrapy/scrapy/issues/3512){.reference
    .external}).

-   Lazy loading of Downloader Handlers is now optional; this enables
    better initialization error handling in custom Downloader Handlers
    ([issue
    3394](https://github.com/scrapy/scrapy/issues/3394){.reference
    .external}).
:::

::: {#new-filepipeline-and-mediapipeline-features .section}
##### New FilePipeline and MediaPipeline features[¶](#new-filepipeline-and-mediapipeline-features "Permalink to this heading"){.headerlink}

-   Expose more options for S3FilesStore: [[`AWS_ENDPOINT_URL`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_ENDPOINT_URL){.hoverxref
    .tooltip .reference .internal}, [[`AWS_USE_SSL`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_USE_SSL){.hoverxref
    .tooltip .reference .internal}, [[`AWS_VERIFY`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_VERIFY){.hoverxref
    .tooltip .reference .internal}, [[`AWS_REGION_NAME`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_REGION_NAME){.hoverxref
    .tooltip .reference .internal}. For example, this allows to use
    alternative or self-hosted AWS-compatible providers ([issue
    2609](https://github.com/scrapy/scrapy/issues/2609){.reference
    .external}, [issue
    3548](https://github.com/scrapy/scrapy/issues/3548){.reference
    .external}).

-   ACL support for Google Cloud Storage: [[`FILES_STORE_GCS_ACL`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FILES_STORE_GCS_ACL){.hoverxref
    .tooltip .reference .internal} and [[`IMAGES_STORE_GCS_ACL`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-IMAGES_STORE_GCS_ACL){.hoverxref
    .tooltip .reference .internal} ([issue
    3199](https://github.com/scrapy/scrapy/issues/3199){.reference
    .external}).
:::

::: {#scrapy-contracts-improvements .section}
##### [`scrapy.contracts`{.docutils .literal .notranslate}]{.pre} improvements[¶](#scrapy-contracts-improvements "Permalink to this heading"){.headerlink}

-   Exceptions in contracts code are handled better ([issue
    3377](https://github.com/scrapy/scrapy/issues/3377){.reference
    .external});

-   [`dont_filter=True`{.docutils .literal .notranslate}]{.pre} is used
    for contract requests, which allows to test different callbacks with
    the same URL ([issue
    3381](https://github.com/scrapy/scrapy/issues/3381){.reference
    .external});

-   [`request_cls`{.docutils .literal .notranslate}]{.pre} attribute in
    Contract subclasses allow to use different Request classes in
    contracts, for example FormRequest ([issue
    3383](https://github.com/scrapy/scrapy/issues/3383){.reference
    .external}).

-   Fixed errback handling in contracts, e.g. for cases where a contract
    is executed for URL which returns non-200 response ([issue
    3371](https://github.com/scrapy/scrapy/issues/3371){.reference
    .external}).
:::

::: {#usability-improvements .section}
##### Usability improvements[¶](#usability-improvements "Permalink to this heading"){.headerlink}

-   more stats for RobotsTxtMiddleware ([issue
    3100](https://github.com/scrapy/scrapy/issues/3100){.reference
    .external})

-   INFO log level is used to show telnet host/port ([issue
    3115](https://github.com/scrapy/scrapy/issues/3115){.reference
    .external})

-   a message is added to IgnoreRequest in RobotsTxtMiddleware ([issue
    3113](https://github.com/scrapy/scrapy/issues/3113){.reference
    .external})

-   better validation of [`url`{.docutils .literal .notranslate}]{.pre}
    argument in [`Response.follow`{.docutils .literal
    .notranslate}]{.pre} ([issue
    3131](https://github.com/scrapy/scrapy/issues/3131){.reference
    .external})

-   non-zero exit code is returned from Scrapy commands when error
    happens on spider initialization ([issue
    3226](https://github.com/scrapy/scrapy/issues/3226){.reference
    .external})

-   Link extraction improvements: "ftp" is added to scheme list ([issue
    3152](https://github.com/scrapy/scrapy/issues/3152){.reference
    .external}); "flv" is added to common video extensions ([issue
    3165](https://github.com/scrapy/scrapy/issues/3165){.reference
    .external})

-   better error message when an exporter is disabled ([issue
    3358](https://github.com/scrapy/scrapy/issues/3358){.reference
    .external});

-   [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`shell`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`--help`{.docutils .literal .notranslate}]{.pre}
    mentions syntax required for local files ([`./file.html`{.docutils
    .literal .notranslate}]{.pre}) - [issue
    3496](https://github.com/scrapy/scrapy/issues/3496){.reference
    .external}.

-   Referer header value is added to RFPDupeFilter log messages ([issue
    3588](https://github.com/scrapy/scrapy/issues/3588){.reference
    .external})
:::

::: {#id99 .section}
##### Bug fixes[¶](#id99 "Permalink to this heading"){.headerlink}

-   fixed issue with extra blank lines in .csv exports under Windows
    ([issue
    3039](https://github.com/scrapy/scrapy/issues/3039){.reference
    .external});

-   proper handling of pickling errors in Python 3 when serializing
    objects for disk queues ([issue
    3082](https://github.com/scrapy/scrapy/issues/3082){.reference
    .external})

-   flags are now preserved when copying Requests ([issue
    3342](https://github.com/scrapy/scrapy/issues/3342){.reference
    .external});

-   FormRequest.from_response clickdata shouldn't ignore elements with
    [`input[type=image]`{.docutils .literal .notranslate}]{.pre} ([issue
    3153](https://github.com/scrapy/scrapy/issues/3153){.reference
    .external}).

-   FormRequest.from_response should preserve duplicate keys ([issue
    3247](https://github.com/scrapy/scrapy/issues/3247){.reference
    .external})
:::

::: {#documentation-improvements .section}
##### Documentation improvements[¶](#documentation-improvements "Permalink to this heading"){.headerlink}

-   Docs are re-written to suggest .get/.getall API instead of
    .extract/.extract_first. Also, [[Selectors]{.std
    .std-ref}](index.html#topics-selectors){.hoverxref .tooltip
    .reference .internal} docs are updated and re-structured to match
    latest parsel docs; they now contain more topics, such as
    [[Selecting element attributes]{.std
    .std-ref}](index.html#selecting-attributes){.hoverxref .tooltip
    .reference .internal} or [[Extensions to CSS Selectors]{.std
    .std-ref}](index.html#topics-selectors-css-extensions){.hoverxref
    .tooltip .reference .internal} ([issue
    3390](https://github.com/scrapy/scrapy/issues/3390){.reference
    .external}).

-   [[Using your browser's Developer Tools for scraping]{.std
    .std-ref}](index.html#topics-developer-tools){.hoverxref .tooltip
    .reference .internal} is a new tutorial which replaces old Firefox
    and Firebug tutorials ([issue
    3400](https://github.com/scrapy/scrapy/issues/3400){.reference
    .external}).

-   SCRAPY_PROJECT environment variable is documented ([issue
    3518](https://github.com/scrapy/scrapy/issues/3518){.reference
    .external});

-   troubleshooting section is added to install instructions ([issue
    3517](https://github.com/scrapy/scrapy/issues/3517){.reference
    .external});

-   improved links to beginner resources in the tutorial ([issue
    3367](https://github.com/scrapy/scrapy/issues/3367){.reference
    .external}, [issue
    3468](https://github.com/scrapy/scrapy/issues/3468){.reference
    .external});

-   fixed [[`RETRY_HTTP_CODES`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-RETRY_HTTP_CODES){.hoverxref
    .tooltip .reference .internal} default values in docs ([issue
    3335](https://github.com/scrapy/scrapy/issues/3335){.reference
    .external});

-   remove unused [`DEPTH_STATS`{.docutils .literal .notranslate}]{.pre}
    option from docs ([issue
    3245](https://github.com/scrapy/scrapy/issues/3245){.reference
    .external});

-   other cleanups ([issue
    3347](https://github.com/scrapy/scrapy/issues/3347){.reference
    .external}, [issue
    3350](https://github.com/scrapy/scrapy/issues/3350){.reference
    .external}, [issue
    3445](https://github.com/scrapy/scrapy/issues/3445){.reference
    .external}, [issue
    3544](https://github.com/scrapy/scrapy/issues/3544){.reference
    .external}, [issue
    3605](https://github.com/scrapy/scrapy/issues/3605){.reference
    .external}).
:::

::: {#id100 .section}
##### Deprecation removals[¶](#id100 "Permalink to this heading"){.headerlink}

Compatibility shims for pre-1.0 Scrapy module names are removed ([issue
3318](https://github.com/scrapy/scrapy/issues/3318){.reference
.external}):

-   [`scrapy.command`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.contrib`{.docutils .literal .notranslate}]{.pre} (with all
    submodules)

-   [`scrapy.contrib_exp`{.docutils .literal .notranslate}]{.pre} (with
    all submodules)

-   [`scrapy.dupefilter`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.linkextractor`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.project`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.spider`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.spidermanager`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.squeue`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.stats`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.statscol`{.docutils .literal .notranslate}]{.pre}

-   [`scrapy.utils.decorator`{.docutils .literal .notranslate}]{.pre}

See [[Module Relocations]{.std
.std-ref}](#module-relocations){.hoverxref .tooltip .reference
.internal} for more information, or use suggestions from Scrapy 1.5.x
deprecation warnings to update your code.

Other deprecation removals:

-   Deprecated scrapy.interfaces.ISpiderManager is removed; please use
    scrapy.interfaces.ISpiderLoader.

-   Deprecated [`CrawlerSettings`{.docutils .literal
    .notranslate}]{.pre} class is removed ([issue
    3327](https://github.com/scrapy/scrapy/issues/3327){.reference
    .external}).

-   Deprecated [`Settings.overrides`{.docutils .literal
    .notranslate}]{.pre} and [`Settings.defaults`{.docutils .literal
    .notranslate}]{.pre} attributes are removed ([issue
    3327](https://github.com/scrapy/scrapy/issues/3327){.reference
    .external}, [issue
    3359](https://github.com/scrapy/scrapy/issues/3359){.reference
    .external}).
:::

::: {#other-improvements-cleanups .section}
##### Other improvements, cleanups[¶](#other-improvements-cleanups "Permalink to this heading"){.headerlink}

-   All Scrapy tests now pass on Windows; Scrapy testing suite is
    executed in a Windows environment on CI ([issue
    3315](https://github.com/scrapy/scrapy/issues/3315){.reference
    .external}).

-   Python 3.7 support ([issue
    3326](https://github.com/scrapy/scrapy/issues/3326){.reference
    .external}, [issue
    3150](https://github.com/scrapy/scrapy/issues/3150){.reference
    .external}, [issue
    3547](https://github.com/scrapy/scrapy/issues/3547){.reference
    .external}).

-   Testing and CI fixes ([issue
    3526](https://github.com/scrapy/scrapy/issues/3526){.reference
    .external}, [issue
    3538](https://github.com/scrapy/scrapy/issues/3538){.reference
    .external}, [issue
    3308](https://github.com/scrapy/scrapy/issues/3308){.reference
    .external}, [issue
    3311](https://github.com/scrapy/scrapy/issues/3311){.reference
    .external}, [issue
    3309](https://github.com/scrapy/scrapy/issues/3309){.reference
    .external}, [issue
    3305](https://github.com/scrapy/scrapy/issues/3305){.reference
    .external}, [issue
    3210](https://github.com/scrapy/scrapy/issues/3210){.reference
    .external}, [issue
    3299](https://github.com/scrapy/scrapy/issues/3299){.reference
    .external})

-   [`scrapy.http.cookies.CookieJar.clear`{.docutils .literal
    .notranslate}]{.pre} accepts "domain", "path" and "name" optional
    arguments ([issue
    3231](https://github.com/scrapy/scrapy/issues/3231){.reference
    .external}).

-   additional files are included to sdist ([issue
    3495](https://github.com/scrapy/scrapy/issues/3495){.reference
    .external});

-   code style fixes ([issue
    3405](https://github.com/scrapy/scrapy/issues/3405){.reference
    .external}, [issue
    3304](https://github.com/scrapy/scrapy/issues/3304){.reference
    .external});

-   unneeded .strip() call is removed ([issue
    3519](https://github.com/scrapy/scrapy/issues/3519){.reference
    .external});

-   collections.deque is used to store MiddlewareManager methods instead
    of a list ([issue
    3476](https://github.com/scrapy/scrapy/issues/3476){.reference
    .external})
:::
:::

::: {#scrapy-1-5-2-2019-01-22 .section}
[]{#release-1-5-2}

#### Scrapy 1.5.2 (2019-01-22)[¶](#scrapy-1-5-2-2019-01-22 "Permalink to this heading"){.headerlink}

-   *Security bugfix*: Telnet console extension can be easily exploited
    by rogue websites POSTing content to
    [http://localhost:6023](http://localhost:6023){.reference
    .external}, we haven't found a way to exploit it from Scrapy, but it
    is very easy to trick a browser to do so and elevates the risk for
    local development environment.

    *The fix is backward incompatible*, it enables telnet user-password
    authentication by default with a random generated password. If you
    can't upgrade right away, please consider setting
    [[`TELNETCONSOLE_PORT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TELNETCONSOLE_PORT){.hoverxref
    .tooltip .reference .internal} out of its default value.

    See [[telnet console]{.std
    .std-ref}](index.html#topics-telnetconsole){.hoverxref .tooltip
    .reference .internal} documentation for more info

-   Backport CI build failure under GCE environment due to boto import
    error.
:::

::: {#scrapy-1-5-1-2018-07-12 .section}
[]{#release-1-5-1}

#### Scrapy 1.5.1 (2018-07-12)[¶](#scrapy-1-5-1-2018-07-12 "Permalink to this heading"){.headerlink}

This is a maintenance release with important bug fixes, but no new
features:

-   [`O(N^2)`{.docutils .literal .notranslate}]{.pre} gzip decompression
    issue which affected Python 3 and PyPy is fixed ([issue
    3281](https://github.com/scrapy/scrapy/issues/3281){.reference
    .external});

-   skipping of TLS validation errors is improved ([issue
    3166](https://github.com/scrapy/scrapy/issues/3166){.reference
    .external});

-   Ctrl-C handling is fixed in Python 3.5+ ([issue
    3096](https://github.com/scrapy/scrapy/issues/3096){.reference
    .external});

-   testing fixes ([issue
    3092](https://github.com/scrapy/scrapy/issues/3092){.reference
    .external}, [issue
    3263](https://github.com/scrapy/scrapy/issues/3263){.reference
    .external});

-   documentation improvements ([issue
    3058](https://github.com/scrapy/scrapy/issues/3058){.reference
    .external}, [issue
    3059](https://github.com/scrapy/scrapy/issues/3059){.reference
    .external}, [issue
    3089](https://github.com/scrapy/scrapy/issues/3089){.reference
    .external}, [issue
    3123](https://github.com/scrapy/scrapy/issues/3123){.reference
    .external}, [issue
    3127](https://github.com/scrapy/scrapy/issues/3127){.reference
    .external}, [issue
    3189](https://github.com/scrapy/scrapy/issues/3189){.reference
    .external}, [issue
    3224](https://github.com/scrapy/scrapy/issues/3224){.reference
    .external}, [issue
    3280](https://github.com/scrapy/scrapy/issues/3280){.reference
    .external}, [issue
    3279](https://github.com/scrapy/scrapy/issues/3279){.reference
    .external}, [issue
    3201](https://github.com/scrapy/scrapy/issues/3201){.reference
    .external}, [issue
    3260](https://github.com/scrapy/scrapy/issues/3260){.reference
    .external}, [issue
    3284](https://github.com/scrapy/scrapy/issues/3284){.reference
    .external}, [issue
    3298](https://github.com/scrapy/scrapy/issues/3298){.reference
    .external}, [issue
    3294](https://github.com/scrapy/scrapy/issues/3294){.reference
    .external}).
:::

::: {#scrapy-1-5-0-2017-12-29 .section}
[]{#release-1-5-0}

#### Scrapy 1.5.0 (2017-12-29)[¶](#scrapy-1-5-0-2017-12-29 "Permalink to this heading"){.headerlink}

This release brings small new features and improvements across the
codebase. Some highlights:

-   Google Cloud Storage is supported in FilesPipeline and
    ImagesPipeline.

-   Crawling with proxy servers becomes more efficient, as connections
    to proxies can be reused now.

-   Warnings, exception and logging messages are improved to make
    debugging easier.

-   [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`parse`{.docutils .literal
    .notranslate}]{.pre} command now allows to set custom request meta
    via [`--meta`{.docutils .literal .notranslate}]{.pre} argument.

-   Compatibility with Python 3.6, PyPy and PyPy3 is improved; PyPy and
    PyPy3 are now supported officially, by running tests on CI.

-   Better default handling of HTTP 308, 522 and 524 status codes.

-   Documentation is improved, as usual.

::: {#id101 .section}
##### Backward Incompatible Changes[¶](#id101 "Permalink to this heading"){.headerlink}

-   Scrapy 1.5 drops support for Python 3.3.

-   Default Scrapy User-Agent now uses https link to scrapy.org ([issue
    2983](https://github.com/scrapy/scrapy/issues/2983){.reference
    .external}). **This is technically backward-incompatible**; override
    [[`USER_AGENT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-USER_AGENT){.hoverxref
    .tooltip .reference .internal} if you relied on old value.

-   Logging of settings overridden by [`custom_settings`{.docutils
    .literal .notranslate}]{.pre} is fixed; **this is technically
    backward-incompatible** because the logger changes from
    [`[scrapy.utils.log]`{.docutils .literal .notranslate}]{.pre} to
    [`[scrapy.crawler]`{.docutils .literal .notranslate}]{.pre}. If
    you're parsing Scrapy logs, please update your log parsers ([issue
    1343](https://github.com/scrapy/scrapy/issues/1343){.reference
    .external}).

-   LinkExtractor now ignores [`m4v`{.docutils .literal
    .notranslate}]{.pre} extension by default, this is change in
    behavior.

-   522 and 524 status codes are added to [`RETRY_HTTP_CODES`{.docutils
    .literal .notranslate}]{.pre} ([issue
    2851](https://github.com/scrapy/scrapy/issues/2851){.reference
    .external})
:::

::: {#id102 .section}
##### New features[¶](#id102 "Permalink to this heading"){.headerlink}

-   Support [`<link>`{.docutils .literal .notranslate}]{.pre} tags in
    [`Response.follow`{.docutils .literal .notranslate}]{.pre} ([issue
    2785](https://github.com/scrapy/scrapy/issues/2785){.reference
    .external})

-   Support for [`ptpython`{.docutils .literal .notranslate}]{.pre} REPL
    ([issue
    2654](https://github.com/scrapy/scrapy/issues/2654){.reference
    .external})

-   Google Cloud Storage support for FilesPipeline and ImagesPipeline
    ([issue
    2923](https://github.com/scrapy/scrapy/issues/2923){.reference
    .external}).

-   New [`--meta`{.docutils .literal .notranslate}]{.pre} option of the
    "scrapy parse" command allows to pass additional request.meta
    ([issue
    2883](https://github.com/scrapy/scrapy/issues/2883){.reference
    .external})

-   Populate spider variable when using
    [`shell.inspect_response`{.docutils .literal .notranslate}]{.pre}
    ([issue
    2812](https://github.com/scrapy/scrapy/issues/2812){.reference
    .external})

-   Handle HTTP 308 Permanent Redirect ([issue
    2844](https://github.com/scrapy/scrapy/issues/2844){.reference
    .external})

-   Add 522 and 524 to [`RETRY_HTTP_CODES`{.docutils .literal
    .notranslate}]{.pre} ([issue
    2851](https://github.com/scrapy/scrapy/issues/2851){.reference
    .external})

-   Log versions information at startup ([issue
    2857](https://github.com/scrapy/scrapy/issues/2857){.reference
    .external})

-   [`scrapy.mail.MailSender`{.docutils .literal .notranslate}]{.pre}
    now works in Python 3 (it requires Twisted 17.9.0)

-   Connections to proxy servers are reused ([issue
    2743](https://github.com/scrapy/scrapy/issues/2743){.reference
    .external})

-   Add template for a downloader middleware ([issue
    2755](https://github.com/scrapy/scrapy/issues/2755){.reference
    .external})

-   Explicit message for NotImplementedError when parse callback not
    defined ([issue
    2831](https://github.com/scrapy/scrapy/issues/2831){.reference
    .external})

-   CrawlerProcess got an option to disable installation of root log
    handler ([issue
    2921](https://github.com/scrapy/scrapy/issues/2921){.reference
    .external})

-   LinkExtractor now ignores [`m4v`{.docutils .literal
    .notranslate}]{.pre} extension by default

-   Better log messages for responses over [[`DOWNLOAD_WARNSIZE`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_WARNSIZE){.hoverxref
    .tooltip .reference .internal} and [[`DOWNLOAD_MAXSIZE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_MAXSIZE){.hoverxref
    .tooltip .reference .internal} limits ([issue
    2927](https://github.com/scrapy/scrapy/issues/2927){.reference
    .external})

-   Show warning when a URL is put to
    [`Spider.allowed_domains`{.docutils .literal .notranslate}]{.pre}
    instead of a domain ([issue
    2250](https://github.com/scrapy/scrapy/issues/2250){.reference
    .external}).
:::

::: {#id103 .section}
##### Bug fixes[¶](#id103 "Permalink to this heading"){.headerlink}

-   Fix logging of settings overridden by [`custom_settings`{.docutils
    .literal .notranslate}]{.pre}; **this is technically
    backward-incompatible** because the logger changes from
    [`[scrapy.utils.log]`{.docutils .literal .notranslate}]{.pre} to
    [`[scrapy.crawler]`{.docutils .literal .notranslate}]{.pre}, so
    please update your log parsers if needed ([issue
    1343](https://github.com/scrapy/scrapy/issues/1343){.reference
    .external})

-   Default Scrapy User-Agent now uses https link to scrapy.org ([issue
    2983](https://github.com/scrapy/scrapy/issues/2983){.reference
    .external}). **This is technically backward-incompatible**; override
    [[`USER_AGENT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-USER_AGENT){.hoverxref
    .tooltip .reference .internal} if you relied on old value.

-   Fix PyPy and PyPy3 test failures, support them officially ([issue
    2793](https://github.com/scrapy/scrapy/issues/2793){.reference
    .external}, [issue
    2935](https://github.com/scrapy/scrapy/issues/2935){.reference
    .external}, [issue
    2990](https://github.com/scrapy/scrapy/issues/2990){.reference
    .external}, [issue
    3050](https://github.com/scrapy/scrapy/issues/3050){.reference
    .external}, [issue
    2213](https://github.com/scrapy/scrapy/issues/2213){.reference
    .external}, [issue
    3048](https://github.com/scrapy/scrapy/issues/3048){.reference
    .external})

-   Fix DNS resolver when [`DNSCACHE_ENABLED=False`{.docutils .literal
    .notranslate}]{.pre} ([issue
    2811](https://github.com/scrapy/scrapy/issues/2811){.reference
    .external})

-   Add [`cryptography`{.docutils .literal .notranslate}]{.pre} for
    Debian Jessie tox test env ([issue
    2848](https://github.com/scrapy/scrapy/issues/2848){.reference
    .external})

-   Add verification to check if Request callback is callable ([issue
    2766](https://github.com/scrapy/scrapy/issues/2766){.reference
    .external})

-   Port [`extras/qpsclient.py`{.docutils .literal .notranslate}]{.pre}
    to Python 3 ([issue
    2849](https://github.com/scrapy/scrapy/issues/2849){.reference
    .external})

-   Use getfullargspec under the scenes for Python 3 to stop
    DeprecationWarning ([issue
    2862](https://github.com/scrapy/scrapy/issues/2862){.reference
    .external})

-   Update deprecated test aliases ([issue
    2876](https://github.com/scrapy/scrapy/issues/2876){.reference
    .external})

-   Fix [`SitemapSpider`{.docutils .literal .notranslate}]{.pre} support
    for alternate links ([issue
    2853](https://github.com/scrapy/scrapy/issues/2853){.reference
    .external})
:::

::: {#docs .section}
##### Docs[¶](#docs "Permalink to this heading"){.headerlink}

-   Added missing bullet point for the
    [`AUTOTHROTTLE_TARGET_CONCURRENCY`{.docutils .literal
    .notranslate}]{.pre} setting. ([issue
    2756](https://github.com/scrapy/scrapy/issues/2756){.reference
    .external})

-   Update Contributing docs, document new support channels ([issue
    2762](https://github.com/scrapy/scrapy/issues/2762){.reference
    .external}, issue:3038)

-   Include references to Scrapy subreddit in the docs

-   Fix broken links; use [https://](https://){.reference .external} for
    external links ([issue
    2978](https://github.com/scrapy/scrapy/issues/2978){.reference
    .external}, [issue
    2982](https://github.com/scrapy/scrapy/issues/2982){.reference
    .external}, [issue
    2958](https://github.com/scrapy/scrapy/issues/2958){.reference
    .external})

-   Document CloseSpider extension better ([issue
    2759](https://github.com/scrapy/scrapy/issues/2759){.reference
    .external})

-   Use [`pymongo.collection.Collection.insert_one()`{.docutils .literal
    .notranslate}]{.pre} in MongoDB example ([issue
    2781](https://github.com/scrapy/scrapy/issues/2781){.reference
    .external})

-   Spelling mistake and typos ([issue
    2828](https://github.com/scrapy/scrapy/issues/2828){.reference
    .external}, [issue
    2837](https://github.com/scrapy/scrapy/issues/2837){.reference
    .external}, [issue
    2884](https://github.com/scrapy/scrapy/issues/2884){.reference
    .external}, [issue
    2924](https://github.com/scrapy/scrapy/issues/2924){.reference
    .external})

-   Clarify [`CSVFeedSpider.headers`{.docutils .literal
    .notranslate}]{.pre} documentation ([issue
    2826](https://github.com/scrapy/scrapy/issues/2826){.reference
    .external})

-   Document [`DontCloseSpider`{.docutils .literal .notranslate}]{.pre}
    exception and clarify [`spider_idle`{.docutils .literal
    .notranslate}]{.pre} ([issue
    2791](https://github.com/scrapy/scrapy/issues/2791){.reference
    .external})

-   Update "Releases" section in README ([issue
    2764](https://github.com/scrapy/scrapy/issues/2764){.reference
    .external})

-   Fix rst syntax in [`DOWNLOAD_FAIL_ON_DATALOSS`{.docutils .literal
    .notranslate}]{.pre} docs ([issue
    2763](https://github.com/scrapy/scrapy/issues/2763){.reference
    .external})

-   Small fix in description of startproject arguments ([issue
    2866](https://github.com/scrapy/scrapy/issues/2866){.reference
    .external})

-   Clarify data types in Response.body docs ([issue
    2922](https://github.com/scrapy/scrapy/issues/2922){.reference
    .external})

-   Add a note about [`request.meta['depth']`{.docutils .literal
    .notranslate}]{.pre} to DepthMiddleware docs ([issue
    2374](https://github.com/scrapy/scrapy/issues/2374){.reference
    .external})

-   Add a note about [`request.meta['dont_merge_cookies']`{.docutils
    .literal .notranslate}]{.pre} to CookiesMiddleware docs ([issue
    2999](https://github.com/scrapy/scrapy/issues/2999){.reference
    .external})

-   Up-to-date example of project structure ([issue
    2964](https://github.com/scrapy/scrapy/issues/2964){.reference
    .external}, [issue
    2976](https://github.com/scrapy/scrapy/issues/2976){.reference
    .external})

-   A better example of ItemExporters usage ([issue
    2989](https://github.com/scrapy/scrapy/issues/2989){.reference
    .external})

-   Document [`from_crawler`{.docutils .literal .notranslate}]{.pre}
    methods for spider and downloader middlewares ([issue
    3019](https://github.com/scrapy/scrapy/issues/3019){.reference
    .external})
:::
:::

::: {#scrapy-1-4-0-2017-05-18 .section}
[]{#release-1-4-0}

#### Scrapy 1.4.0 (2017-05-18)[¶](#scrapy-1-4-0-2017-05-18 "Permalink to this heading"){.headerlink}

Scrapy 1.4 does not bring that many breathtaking new features but quite
a few handy improvements nonetheless.

Scrapy now supports anonymous FTP sessions with customizable user and
password via the new [[`FTP_USER`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-FTP_USER){.hoverxref
.tooltip .reference .internal} and [[`FTP_PASSWORD`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-FTP_PASSWORD){.hoverxref
.tooltip .reference .internal} settings. And if you're using Twisted
version 17.1.0 or above, FTP is now available with Python 3.

There's a new [[`response.follow`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.TextResponse.follow "scrapy.http.TextResponse.follow"){.reference
.internal} method for creating requests; **it is now a recommended way
to create Requests in Scrapy spiders**. This method makes it easier to
write correct spiders; [`response.follow`{.docutils .literal
.notranslate}]{.pre} has several advantages over creating
[`scrapy.Request`{.docutils .literal .notranslate}]{.pre} objects
directly:

-   it handles relative URLs;

-   it works properly with non-ascii URLs on non-UTF8 pages;

-   in addition to absolute and relative URLs it supports Selectors; for
    [`<a>`{.docutils .literal .notranslate}]{.pre} elements it can also
    extract their href values.

For example, instead of this:

::: {.highlight-default .notranslate}
::: highlight
    for href in response.css('li.page a::attr(href)').extract():
        url = response.urljoin(href)
        yield scrapy.Request(url, self.parse, encoding=response.encoding)
:::
:::

One can now write this:

::: {.highlight-default .notranslate}
::: highlight
    for a in response.css('li.page a'):
        yield response.follow(a, self.parse)
:::
:::

Link extractors are also improved. They work similarly to what a regular
modern browser would do: leading and trailing whitespace are removed
from attributes (think [`href="`{.docutils .literal
.notranslate}]{.pre}`   `{.docutils .literal
.notranslate}[`http://example.com"`{.docutils .literal
.notranslate}]{.pre}) when building [`Link`{.docutils .literal
.notranslate}]{.pre} objects. This whitespace-stripping also happens for
[`action`{.docutils .literal .notranslate}]{.pre} attributes with
[`FormRequest`{.docutils .literal .notranslate}]{.pre}.

**Please also note that link extractors do not canonicalize URLs by
default anymore.** This was puzzling users every now and then, and it's
not what browsers do in fact, so we removed that extra transformation on
extracted links.

For those of you wanting more control on the [`Referer:`{.docutils
.literal .notranslate}]{.pre} header that Scrapy sends when following
links, you can set your own [`Referrer`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`Policy`{.docutils .literal .notranslate}]{.pre}. Prior to
Scrapy 1.4, the default [`RefererMiddleware`{.docutils .literal
.notranslate}]{.pre} would simply and blindly set it to the URL of the
response that generated the HTTP request (which could leak information
on your URL seeds). By default, Scrapy now behaves much like your
regular browser does. And this policy is fully customizable with W3C
standard values (or with something really custom of your own if you
wish). See [[`REFERRER_POLICY`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-REFERRER_POLICY){.hoverxref
.tooltip .reference .internal} for details.

To make Scrapy spiders easier to debug, Scrapy logs more stats by
default in 1.4: memory usage stats, detailed retry stats, detailed HTTP
error code stats. A similar change is that HTTP cache path is also
visible in logs now.

Last but not least, Scrapy now has the option to make JSON and XML items
more human-readable, with newlines between items and even custom
indenting offset, using the new [[`FEED_EXPORT_INDENT`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_INDENT){.hoverxref
.tooltip .reference .internal} setting.

Enjoy! (Or read on for the rest of changes in this release.)

::: {#deprecations-and-backward-incompatible-changes .section}
##### Deprecations and Backward Incompatible Changes[¶](#deprecations-and-backward-incompatible-changes "Permalink to this heading"){.headerlink}

-   Default to [`canonicalize=False`{.docutils .literal
    .notranslate}]{.pre} in
    [[`scrapy.linkextractors.LinkExtractor`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} ([issue
    2537](https://github.com/scrapy/scrapy/issues/2537){.reference
    .external}, fixes [issue
    1941](https://github.com/scrapy/scrapy/issues/1941){.reference
    .external} and [issue
    1982](https://github.com/scrapy/scrapy/issues/1982){.reference
    .external}): **warning, this is technically backward-incompatible**

-   Enable memusage extension by default ([issue
    2539](https://github.com/scrapy/scrapy/issues/2539){.reference
    .external}, fixes [issue
    2187](https://github.com/scrapy/scrapy/issues/2187){.reference
    .external}); **this is technically backward-incompatible** so please
    check if you have any non-default [`MEMUSAGE_***`{.docutils .literal
    .notranslate}]{.pre} options set.

-   [`EDITOR`{.docutils .literal .notranslate}]{.pre} environment
    variable now takes precedence over [`EDITOR`{.docutils .literal
    .notranslate}]{.pre} option defined in settings.py ([issue
    1829](https://github.com/scrapy/scrapy/issues/1829){.reference
    .external}); Scrapy default settings no longer depend on environment
    variables. **This is technically a backward incompatible change**.

-   [`Spider.make_requests_from_url`{.docutils .literal
    .notranslate}]{.pre} is deprecated ([issue
    1728](https://github.com/scrapy/scrapy/issues/1728){.reference
    .external}, fixes [issue
    1495](https://github.com/scrapy/scrapy/issues/1495){.reference
    .external}).
:::

::: {#id104 .section}
##### New Features[¶](#id104 "Permalink to this heading"){.headerlink}

-   Accept proxy credentials in [[`proxy`{.xref .std .std-reqmeta
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal} request meta key ([issue
    2526](https://github.com/scrapy/scrapy/issues/2526){.reference
    .external})

-   Support
    [brotli-compressed](https://www.ietf.org/rfc/rfc7932.txt){.reference
    .external} content; requires optional
    [brotlipy](https://github.com/python-hyper/brotlipy/){.reference
    .external} ([issue
    2535](https://github.com/scrapy/scrapy/issues/2535){.reference
    .external})

-   New [[response.follow]{.std
    .std-ref}](index.html#response-follow-example){.hoverxref .tooltip
    .reference .internal} shortcut for creating requests ([issue
    1940](https://github.com/scrapy/scrapy/issues/1940){.reference
    .external})

-   Added [`flags`{.docutils .literal .notranslate}]{.pre} argument and
    attribute to [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} objects ([issue
    2047](https://github.com/scrapy/scrapy/issues/2047){.reference
    .external})

-   Support Anonymous FTP ([issue
    2342](https://github.com/scrapy/scrapy/issues/2342){.reference
    .external})

-   Added [`retry/count`{.docutils .literal .notranslate}]{.pre},
    [`retry/max_reached`{.docutils .literal .notranslate}]{.pre} and
    [`retry/reason_count/<reason>`{.docutils .literal
    .notranslate}]{.pre} stats to [[`RetryMiddleware`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.RetryMiddleware "scrapy.downloadermiddlewares.retry.RetryMiddleware"){.reference
    .internal} ([issue
    2543](https://github.com/scrapy/scrapy/issues/2543){.reference
    .external})

-   Added [`httperror/response_ignored_count`{.docutils .literal
    .notranslate}]{.pre} and
    [`httperror/response_ignored_status_count/<status>`{.docutils
    .literal .notranslate}]{.pre} stats to [[`HttpErrorMiddleware`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.httperror.HttpErrorMiddleware "scrapy.spidermiddlewares.httperror.HttpErrorMiddleware"){.reference
    .internal} ([issue
    2566](https://github.com/scrapy/scrapy/issues/2566){.reference
    .external})

-   Customizable [[`Referrer`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}` `{.xref .std .std-setting .docutils .literal
    .notranslate}[`policy`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-REFERRER_POLICY){.hoverxref
    .tooltip .reference .internal} in [[`RefererMiddleware`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.referer.RefererMiddleware "scrapy.spidermiddlewares.referer.RefererMiddleware"){.reference
    .internal} ([issue
    2306](https://github.com/scrapy/scrapy/issues/2306){.reference
    .external})

-   New [`data:`{.docutils .literal .notranslate}]{.pre} URI download
    handler ([issue
    2334](https://github.com/scrapy/scrapy/issues/2334){.reference
    .external}, fixes [issue
    2156](https://github.com/scrapy/scrapy/issues/2156){.reference
    .external})

-   Log cache directory when HTTP Cache is used ([issue
    2611](https://github.com/scrapy/scrapy/issues/2611){.reference
    .external}, fixes [issue
    2604](https://github.com/scrapy/scrapy/issues/2604){.reference
    .external})

-   Warn users when project contains duplicate spider names (fixes
    [issue
    2181](https://github.com/scrapy/scrapy/issues/2181){.reference
    .external})

-   [`scrapy.utils.datatypes.CaselessDict`{.docutils .literal
    .notranslate}]{.pre} now accepts [`Mapping`{.docutils .literal
    .notranslate}]{.pre} instances and not only dicts ([issue
    2646](https://github.com/scrapy/scrapy/issues/2646){.reference
    .external})

-   [[Media downloads]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal}, with [[`FilesPipeline`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.files.FilesPipeline "scrapy.pipelines.files.FilesPipeline"){.reference
    .internal} or [[`ImagesPipeline`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline "scrapy.pipelines.images.ImagesPipeline"){.reference
    .internal}, can now optionally handle HTTP redirects using the new
    [[`MEDIA_ALLOW_REDIRECTS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-MEDIA_ALLOW_REDIRECTS){.hoverxref
    .tooltip .reference .internal} setting ([issue
    2616](https://github.com/scrapy/scrapy/issues/2616){.reference
    .external}, fixes [issue
    2004](https://github.com/scrapy/scrapy/issues/2004){.reference
    .external})

-   Accept non-complete responses from websites using a new
    [[`DOWNLOAD_FAIL_ON_DATALOSS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_FAIL_ON_DATALOSS){.hoverxref
    .tooltip .reference .internal} setting ([issue
    2590](https://github.com/scrapy/scrapy/issues/2590){.reference
    .external}, fixes [issue
    2586](https://github.com/scrapy/scrapy/issues/2586){.reference
    .external})

-   Optional pretty-printing of JSON and XML items via
    [[`FEED_EXPORT_INDENT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_INDENT){.hoverxref
    .tooltip .reference .internal} setting ([issue
    2456](https://github.com/scrapy/scrapy/issues/2456){.reference
    .external}, fixes [issue
    1327](https://github.com/scrapy/scrapy/issues/1327){.reference
    .external})

-   Allow dropping fields in [`FormRequest.from_response`{.docutils
    .literal .notranslate}]{.pre} formdata when [`None`{.docutils
    .literal .notranslate}]{.pre} value is passed ([issue
    667](https://github.com/scrapy/scrapy/issues/667){.reference
    .external})

-   Per-request retry times with the new [[`max_retry_times`{.xref .std
    .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-max_retry_times){.hoverxref
    .tooltip .reference .internal} meta key ([issue
    2642](https://github.com/scrapy/scrapy/issues/2642){.reference
    .external})

-   [`python`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`-m`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`scrapy`{.docutils .literal .notranslate}]{.pre} as a
    more explicit alternative to [`scrapy`{.docutils .literal
    .notranslate}]{.pre} command ([issue
    2740](https://github.com/scrapy/scrapy/issues/2740){.reference
    .external})
:::

::: {#id105 .section}
##### Bug fixes[¶](#id105 "Permalink to this heading"){.headerlink}

-   LinkExtractor now strips leading and trailing whitespaces from
    attributes ([issue
    2547](https://github.com/scrapy/scrapy/issues/2547){.reference
    .external}, fixes [issue
    1614](https://github.com/scrapy/scrapy/issues/1614){.reference
    .external})

-   Properly handle whitespaces in action attribute in
    [`FormRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} ([issue
    2548](https://github.com/scrapy/scrapy/issues/2548){.reference
    .external})

-   Buffer CONNECT response bytes from proxy until all HTTP headers are
    received ([issue
    2495](https://github.com/scrapy/scrapy/issues/2495){.reference
    .external}, fixes [issue
    2491](https://github.com/scrapy/scrapy/issues/2491){.reference
    .external})

-   FTP downloader now works on Python 3, provided you use
    Twisted\>=17.1 ([issue
    2599](https://github.com/scrapy/scrapy/issues/2599){.reference
    .external})

-   Use body to choose response type after decompressing content ([issue
    2393](https://github.com/scrapy/scrapy/issues/2393){.reference
    .external}, fixes [issue
    2145](https://github.com/scrapy/scrapy/issues/2145){.reference
    .external})

-   Always decompress [`Content-Encoding:`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`gzip`{.docutils .literal .notranslate}]{.pre} at
    [[`HttpCompressionMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware "scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware"){.reference
    .internal} stage ([issue
    2391](https://github.com/scrapy/scrapy/issues/2391){.reference
    .external})

-   Respect custom log level in [`Spider.custom_settings`{.docutils
    .literal .notranslate}]{.pre} ([issue
    2581](https://github.com/scrapy/scrapy/issues/2581){.reference
    .external}, fixes [issue
    1612](https://github.com/scrapy/scrapy/issues/1612){.reference
    .external})

-   'make htmlview' fix for macOS ([issue
    2661](https://github.com/scrapy/scrapy/issues/2661){.reference
    .external})

-   Remove "commands" from the command list ([issue
    2695](https://github.com/scrapy/scrapy/issues/2695){.reference
    .external})

-   Fix duplicate Content-Length header for POST requests with empty
    body ([issue
    2677](https://github.com/scrapy/scrapy/issues/2677){.reference
    .external})

-   Properly cancel large downloads, i.e. above
    [[`DOWNLOAD_MAXSIZE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_MAXSIZE){.hoverxref
    .tooltip .reference .internal} ([issue
    1616](https://github.com/scrapy/scrapy/issues/1616){.reference
    .external})

-   ImagesPipeline: fixed processing of transparent PNG images with
    palette ([issue
    2675](https://github.com/scrapy/scrapy/issues/2675){.reference
    .external})
:::

::: {#cleanups-refactoring .section}
##### Cleanups & Refactoring[¶](#cleanups-refactoring "Permalink to this heading"){.headerlink}

-   Tests: remove temp files and folders ([issue
    2570](https://github.com/scrapy/scrapy/issues/2570){.reference
    .external}), fixed ProjectUtilsTest on macOS ([issue
    2569](https://github.com/scrapy/scrapy/issues/2569){.reference
    .external}), use portable pypy for Linux on Travis CI ([issue
    2710](https://github.com/scrapy/scrapy/issues/2710){.reference
    .external})

-   Separate building request from [`_requests_to_follow`{.docutils
    .literal .notranslate}]{.pre} in CrawlSpider ([issue
    2562](https://github.com/scrapy/scrapy/issues/2562){.reference
    .external})

-   Remove "Python 3 progress" badge ([issue
    2567](https://github.com/scrapy/scrapy/issues/2567){.reference
    .external})

-   Add a couple more lines to [`.gitignore`{.docutils .literal
    .notranslate}]{.pre} ([issue
    2557](https://github.com/scrapy/scrapy/issues/2557){.reference
    .external})

-   Remove bumpversion prerelease configuration ([issue
    2159](https://github.com/scrapy/scrapy/issues/2159){.reference
    .external})

-   Add codecov.yml file ([issue
    2750](https://github.com/scrapy/scrapy/issues/2750){.reference
    .external})

-   Set context factory implementation based on Twisted version ([issue
    2577](https://github.com/scrapy/scrapy/issues/2577){.reference
    .external}, fixes [issue
    2560](https://github.com/scrapy/scrapy/issues/2560){.reference
    .external})

-   Add omitted [`self`{.docutils .literal .notranslate}]{.pre}
    arguments in default project middleware template ([issue
    2595](https://github.com/scrapy/scrapy/issues/2595){.reference
    .external})

-   Remove redundant [`slot.add_request()`{.docutils .literal
    .notranslate}]{.pre} call in ExecutionEngine ([issue
    2617](https://github.com/scrapy/scrapy/issues/2617){.reference
    .external})

-   Catch more specific [`os.error`{.docutils .literal
    .notranslate}]{.pre} exception in
    [`scrapy.pipelines.files.FSFilesStore`{.docutils .literal
    .notranslate}]{.pre} ([issue
    2644](https://github.com/scrapy/scrapy/issues/2644){.reference
    .external})

-   Change "localhost" test server certificate ([issue
    2720](https://github.com/scrapy/scrapy/issues/2720){.reference
    .external})

-   Remove unused [`MEMUSAGE_REPORT`{.docutils .literal
    .notranslate}]{.pre} setting ([issue
    2576](https://github.com/scrapy/scrapy/issues/2576){.reference
    .external})
:::

::: {#id106 .section}
##### Documentation[¶](#id106 "Permalink to this heading"){.headerlink}

-   Binary mode is required for exporters ([issue
    2564](https://github.com/scrapy/scrapy/issues/2564){.reference
    .external}, fixes [issue
    2553](https://github.com/scrapy/scrapy/issues/2553){.reference
    .external})

-   Mention issue with [`FormRequest.from_response`{.xref .py .py-meth
    .docutils .literal .notranslate}]{.pre} due to bug in lxml ([issue
    2572](https://github.com/scrapy/scrapy/issues/2572){.reference
    .external})

-   Use single quotes uniformly in templates ([issue
    2596](https://github.com/scrapy/scrapy/issues/2596){.reference
    .external})

-   Document [[`ftp_user`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-ftp_user){.hoverxref
    .tooltip .reference .internal} and [[`ftp_password`{.xref .std
    .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-ftp_password){.hoverxref
    .tooltip .reference .internal} meta keys ([issue
    2587](https://github.com/scrapy/scrapy/issues/2587){.reference
    .external})

-   Removed section on deprecated [`contrib/`{.docutils .literal
    .notranslate}]{.pre} ([issue
    2636](https://github.com/scrapy/scrapy/issues/2636){.reference
    .external})

-   Recommend Anaconda when installing Scrapy on Windows ([issue
    2477](https://github.com/scrapy/scrapy/issues/2477){.reference
    .external}, fixes [issue
    2475](https://github.com/scrapy/scrapy/issues/2475){.reference
    .external})

-   FAQ: rewrite note on Python 3 support on Windows ([issue
    2690](https://github.com/scrapy/scrapy/issues/2690){.reference
    .external})

-   Rearrange selector sections ([issue
    2705](https://github.com/scrapy/scrapy/issues/2705){.reference
    .external})

-   Remove [`__nonzero__`{.docutils .literal .notranslate}]{.pre} from
    [[`SelectorList`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.selector.SelectorList "scrapy.selector.SelectorList"){.reference
    .internal} docs ([issue
    2683](https://github.com/scrapy/scrapy/issues/2683){.reference
    .external})

-   Mention how to disable request filtering in documentation of
    [[`DUPEFILTER_CLASS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DUPEFILTER_CLASS){.hoverxref
    .tooltip .reference .internal} setting ([issue
    2714](https://github.com/scrapy/scrapy/issues/2714){.reference
    .external})

-   Add sphinx_rtd_theme to docs setup readme ([issue
    2668](https://github.com/scrapy/scrapy/issues/2668){.reference
    .external})

-   Open file in text mode in JSON item writer example ([issue
    2729](https://github.com/scrapy/scrapy/issues/2729){.reference
    .external})

-   Clarify [`allowed_domains`{.docutils .literal .notranslate}]{.pre}
    example ([issue
    2670](https://github.com/scrapy/scrapy/issues/2670){.reference
    .external})
:::
:::

::: {#scrapy-1-3-3-2017-03-10 .section}
[]{#release-1-3-3}

#### Scrapy 1.3.3 (2017-03-10)[¶](#scrapy-1-3-3-2017-03-10 "Permalink to this heading"){.headerlink}

::: {#id107 .section}
##### Bug fixes[¶](#id107 "Permalink to this heading"){.headerlink}

-   Make [`SpiderLoader`{.docutils .literal .notranslate}]{.pre} raise
    [`ImportError`{.docutils .literal .notranslate}]{.pre} again by
    default for missing dependencies and wrong [[`SPIDER_MODULES`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_MODULES){.hoverxref
    .tooltip .reference .internal}. These exceptions were silenced as
    warnings since 1.3.0. A new setting is introduced to toggle between
    warning or exception if needed ; see
    [[`SPIDER_LOADER_WARN_ONLY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_LOADER_WARN_ONLY){.hoverxref
    .tooltip .reference .internal} for details.
:::
:::

::: {#scrapy-1-3-2-2017-02-13 .section}
[]{#release-1-3-2}

#### Scrapy 1.3.2 (2017-02-13)[¶](#scrapy-1-3-2-2017-02-13 "Permalink to this heading"){.headerlink}

::: {#id108 .section}
##### Bug fixes[¶](#id108 "Permalink to this heading"){.headerlink}

-   Preserve request class when converting to/from dicts (utils.reqser)
    ([issue
    2510](https://github.com/scrapy/scrapy/issues/2510){.reference
    .external}).

-   Use consistent selectors for author field in tutorial ([issue
    2551](https://github.com/scrapy/scrapy/issues/2551){.reference
    .external}).

-   Fix TLS compatibility in Twisted 17+ ([issue
    2558](https://github.com/scrapy/scrapy/issues/2558){.reference
    .external})
:::
:::

::: {#scrapy-1-3-1-2017-02-08 .section}
[]{#release-1-3-1}

#### Scrapy 1.3.1 (2017-02-08)[¶](#scrapy-1-3-1-2017-02-08 "Permalink to this heading"){.headerlink}

::: {#id109 .section}
##### New features[¶](#id109 "Permalink to this heading"){.headerlink}

-   Support [`'True'`{.docutils .literal .notranslate}]{.pre} and
    [`'False'`{.docutils .literal .notranslate}]{.pre} string values for
    boolean settings ([issue
    2519](https://github.com/scrapy/scrapy/issues/2519){.reference
    .external}); you can now do something like [`scrapy`{.docutils
    .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`crawl`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`myspider`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`-s`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`REDIRECT_ENABLED=False`{.docutils .literal
    .notranslate}]{.pre}.

-   Support kwargs with [`response.xpath()`{.docutils .literal
    .notranslate}]{.pre} to use [[XPath variables]{.std
    .std-ref}](index.html#topics-selectors-xpath-variables){.hoverxref
    .tooltip .reference .internal} and ad-hoc namespaces declarations ;
    this requires at least Parsel v1.1 ([issue
    2457](https://github.com/scrapy/scrapy/issues/2457){.reference
    .external}).

-   Add support for Python 3.6 ([issue
    2485](https://github.com/scrapy/scrapy/issues/2485){.reference
    .external}).

-   Run tests on PyPy (warning: some tests still fail, so PyPy is not
    supported yet).
:::

::: {#id110 .section}
##### Bug fixes[¶](#id110 "Permalink to this heading"){.headerlink}

-   Enforce [`DNS_TIMEOUT`{.docutils .literal .notranslate}]{.pre}
    setting ([issue
    2496](https://github.com/scrapy/scrapy/issues/2496){.reference
    .external}).

-   Fix [[`view`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-view){.hoverxref
    .tooltip .reference .internal} command ; it was a regression in
    v1.3.0 ([issue
    2503](https://github.com/scrapy/scrapy/issues/2503){.reference
    .external}).

-   Fix tests regarding [`*_EXPIRES`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`settings`{.docutils .literal .notranslate}]{.pre}
    with Files/Images pipelines ([issue
    2460](https://github.com/scrapy/scrapy/issues/2460){.reference
    .external}).

-   Fix name of generated pipeline class when using basic project
    template ([issue
    2466](https://github.com/scrapy/scrapy/issues/2466){.reference
    .external}).

-   Fix compatibility with Twisted 17+ ([issue
    2496](https://github.com/scrapy/scrapy/issues/2496){.reference
    .external}, [issue
    2528](https://github.com/scrapy/scrapy/issues/2528){.reference
    .external}).

-   Fix [`scrapy.Item`{.docutils .literal .notranslate}]{.pre}
    inheritance on Python 3.6 ([issue
    2511](https://github.com/scrapy/scrapy/issues/2511){.reference
    .external}).

-   Enforce numeric values for components order in
    [`SPIDER_MIDDLEWARES`{.docutils .literal .notranslate}]{.pre},
    [`DOWNLOADER_MIDDLEWARES`{.docutils .literal .notranslate}]{.pre},
    [`EXTENSIONS`{.docutils .literal .notranslate}]{.pre} and
    [`SPIDER_CONTRACTS`{.docutils .literal .notranslate}]{.pre} ([issue
    2420](https://github.com/scrapy/scrapy/issues/2420){.reference
    .external}).
:::

::: {#id111 .section}
##### Documentation[¶](#id111 "Permalink to this heading"){.headerlink}

-   Reword Code of Conduct section and upgrade to Contributor Covenant
    v1.4 ([issue
    2469](https://github.com/scrapy/scrapy/issues/2469){.reference
    .external}).

-   Clarify that passing spider arguments converts them to spider
    attributes ([issue
    2483](https://github.com/scrapy/scrapy/issues/2483){.reference
    .external}).

-   Document [`formid`{.docutils .literal .notranslate}]{.pre} argument
    on [`FormRequest.from_response()`{.docutils .literal
    .notranslate}]{.pre} ([issue
    2497](https://github.com/scrapy/scrapy/issues/2497){.reference
    .external}).

-   Add .rst extension to README files ([issue
    2507](https://github.com/scrapy/scrapy/issues/2507){.reference
    .external}).

-   Mention LevelDB cache storage backend ([issue
    2525](https://github.com/scrapy/scrapy/issues/2525){.reference
    .external}).

-   Use [`yield`{.docutils .literal .notranslate}]{.pre} in sample
    callback code ([issue
    2533](https://github.com/scrapy/scrapy/issues/2533){.reference
    .external}).

-   Add note about HTML entities decoding with
    [`.re()/.re_first()`{.docutils .literal .notranslate}]{.pre} ([issue
    1704](https://github.com/scrapy/scrapy/issues/1704){.reference
    .external}).

-   Typos ([issue
    2512](https://github.com/scrapy/scrapy/issues/2512){.reference
    .external}, [issue
    2534](https://github.com/scrapy/scrapy/issues/2534){.reference
    .external}, [issue
    2531](https://github.com/scrapy/scrapy/issues/2531){.reference
    .external}).
:::

::: {#cleanups .section}
##### Cleanups[¶](#cleanups "Permalink to this heading"){.headerlink}

-   Remove redundant check in [`MetaRefreshMiddleware`{.docutils
    .literal .notranslate}]{.pre} ([issue
    2542](https://github.com/scrapy/scrapy/issues/2542){.reference
    .external}).

-   Faster checks in [`LinkExtractor`{.docutils .literal
    .notranslate}]{.pre} for allow/deny patterns ([issue
    2538](https://github.com/scrapy/scrapy/issues/2538){.reference
    .external}).

-   Remove dead code supporting old Twisted versions ([issue
    2544](https://github.com/scrapy/scrapy/issues/2544){.reference
    .external}).
:::
:::

::: {#scrapy-1-3-0-2016-12-21 .section}
[]{#release-1-3-0}

#### Scrapy 1.3.0 (2016-12-21)[¶](#scrapy-1-3-0-2016-12-21 "Permalink to this heading"){.headerlink}

This release comes rather soon after 1.2.2 for one main reason: it was
found out that releases since 0.18 up to 1.2.2 (included) use some
backported code from Twisted ([`scrapy.xlib.tx.*`{.docutils .literal
.notranslate}]{.pre}), even if newer Twisted modules are available.
Scrapy now uses [`twisted.web.client`{.docutils .literal
.notranslate}]{.pre} and [`twisted.internet.endpoints`{.docutils
.literal .notranslate}]{.pre} directly. (See also cleanups below.)

As it is a major change, we wanted to get the bug fix out quickly while
not breaking any projects using the 1.2 series.

::: {#id112 .section}
##### New Features[¶](#id112 "Permalink to this heading"){.headerlink}

-   [`MailSender`{.docutils .literal .notranslate}]{.pre} now accepts
    single strings as values for [`to`{.docutils .literal
    .notranslate}]{.pre} and [`cc`{.docutils .literal
    .notranslate}]{.pre} arguments ([issue
    2272](https://github.com/scrapy/scrapy/issues/2272){.reference
    .external})

-   [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`fetch`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`url`{.docutils .literal .notranslate}]{.pre},
    [`scrapy`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`shell`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`url`{.docutils .literal .notranslate}]{.pre} and
    [`fetch(url)`{.docutils .literal .notranslate}]{.pre} inside Scrapy
    shell now follow HTTP redirections by default ([issue
    2290](https://github.com/scrapy/scrapy/issues/2290){.reference
    .external}); See [[`fetch`{.xref .std .std-command .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-command-fetch){.hoverxref
    .tooltip .reference .internal} and [[`shell`{.xref .std .std-command
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-shell){.hoverxref
    .tooltip .reference .internal} for details.

-   [`HttpErrorMiddleware`{.docutils .literal .notranslate}]{.pre} now
    logs errors with [`INFO`{.docutils .literal .notranslate}]{.pre}
    level instead of [`DEBUG`{.docutils .literal .notranslate}]{.pre};
    this is technically **backward incompatible** so please check your
    log parsers.

-   By default, logger names now use a long-form path, e.g.
    [`[scrapy.extensions.logstats]`{.docutils .literal
    .notranslate}]{.pre}, instead of the shorter "top-level" variant of
    prior releases (e.g. [`[scrapy]`{.docutils .literal
    .notranslate}]{.pre}); this is **backward incompatible** if you have
    log parsers expecting the short logger name part. You can switch
    back to short logger names using [[`LOG_SHORT_NAMES`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_SHORT_NAMES){.hoverxref
    .tooltip .reference .internal} set to [`True`{.docutils .literal
    .notranslate}]{.pre}.
:::

::: {#dependencies-cleanups .section}
##### Dependencies & Cleanups[¶](#dependencies-cleanups "Permalink to this heading"){.headerlink}

-   Scrapy now requires Twisted \>= 13.1 which is the case for many
    Linux distributions already.

-   As a consequence, we got rid of [`scrapy.xlib.tx.*`{.docutils
    .literal .notranslate}]{.pre} modules, which copied some of Twisted
    code for users stuck with an "old" Twisted version

-   [`ChunkedTransferMiddleware`{.docutils .literal .notranslate}]{.pre}
    is deprecated and removed from the default downloader middlewares.
:::
:::

::: {#scrapy-1-2-3-2017-03-03 .section}
[]{#release-1-2-3}

#### Scrapy 1.2.3 (2017-03-03)[¶](#scrapy-1-2-3-2017-03-03 "Permalink to this heading"){.headerlink}

-   Packaging fix: disallow unsupported Twisted versions in setup.py
:::

::: {#scrapy-1-2-2-2016-12-06 .section}
[]{#release-1-2-2}

#### Scrapy 1.2.2 (2016-12-06)[¶](#scrapy-1-2-2-2016-12-06 "Permalink to this heading"){.headerlink}

::: {#id113 .section}
##### Bug fixes[¶](#id113 "Permalink to this heading"){.headerlink}

-   Fix a cryptic traceback when a pipeline fails on
    [`open_spider()`{.docutils .literal .notranslate}]{.pre} ([issue
    2011](https://github.com/scrapy/scrapy/issues/2011){.reference
    .external})

-   Fix embedded IPython shell variables (fixing [issue
    396](https://github.com/scrapy/scrapy/issues/396){.reference
    .external} that re-appeared in 1.2.0, fixed in [issue
    2418](https://github.com/scrapy/scrapy/issues/2418){.reference
    .external})

-   A couple of patches when dealing with robots.txt:

    -   handle (non-standard) relative sitemap URLs ([issue
        2390](https://github.com/scrapy/scrapy/issues/2390){.reference
        .external})

    -   handle non-ASCII URLs and User-Agents in Python 2 ([issue
        2373](https://github.com/scrapy/scrapy/issues/2373){.reference
        .external})
:::

::: {#id114 .section}
##### Documentation[¶](#id114 "Permalink to this heading"){.headerlink}

-   Document [`"download_latency"`{.docutils .literal
    .notranslate}]{.pre} key in [`Request`{.docutils .literal
    .notranslate}]{.pre}'s [`meta`{.docutils .literal
    .notranslate}]{.pre} dict ([issue
    2033](https://github.com/scrapy/scrapy/issues/2033){.reference
    .external})

-   Remove page on (deprecated & unsupported) Ubuntu packages from ToC
    ([issue
    2335](https://github.com/scrapy/scrapy/issues/2335){.reference
    .external})

-   A few fixed typos ([issue
    2346](https://github.com/scrapy/scrapy/issues/2346){.reference
    .external}, [issue
    2369](https://github.com/scrapy/scrapy/issues/2369){.reference
    .external}, [issue
    2369](https://github.com/scrapy/scrapy/issues/2369){.reference
    .external}, [issue
    2380](https://github.com/scrapy/scrapy/issues/2380){.reference
    .external}) and clarifications ([issue
    2354](https://github.com/scrapy/scrapy/issues/2354){.reference
    .external}, [issue
    2325](https://github.com/scrapy/scrapy/issues/2325){.reference
    .external}, [issue
    2414](https://github.com/scrapy/scrapy/issues/2414){.reference
    .external})
:::

::: {#id115 .section}
##### Other changes[¶](#id115 "Permalink to this heading"){.headerlink}

-   Advertize
    [conda-forge](https://anaconda.org/conda-forge/scrapy){.reference
    .external} as Scrapy's official conda channel ([issue
    2387](https://github.com/scrapy/scrapy/issues/2387){.reference
    .external})

-   More helpful error messages when trying to use [`.css()`{.docutils
    .literal .notranslate}]{.pre} or [`.xpath()`{.docutils .literal
    .notranslate}]{.pre} on non-Text Responses ([issue
    2264](https://github.com/scrapy/scrapy/issues/2264){.reference
    .external})

-   [`startproject`{.docutils .literal .notranslate}]{.pre} command now
    generates a sample [`middlewares.py`{.docutils .literal
    .notranslate}]{.pre} file ([issue
    2335](https://github.com/scrapy/scrapy/issues/2335){.reference
    .external})

-   Add more dependencies' version info in [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`version`{.docutils .literal .notranslate}]{.pre}
    verbose output ([issue
    2404](https://github.com/scrapy/scrapy/issues/2404){.reference
    .external})

-   Remove all [`*.pyc`{.docutils .literal .notranslate}]{.pre} files
    from source distribution ([issue
    2386](https://github.com/scrapy/scrapy/issues/2386){.reference
    .external})
:::
:::

::: {#scrapy-1-2-1-2016-10-21 .section}
[]{#release-1-2-1}

#### Scrapy 1.2.1 (2016-10-21)[¶](#scrapy-1-2-1-2016-10-21 "Permalink to this heading"){.headerlink}

::: {#id116 .section}
##### Bug fixes[¶](#id116 "Permalink to this heading"){.headerlink}

-   Include OpenSSL's more permissive default ciphers when establishing
    TLS/SSL connections ([issue
    2314](https://github.com/scrapy/scrapy/issues/2314){.reference
    .external}).

-   Fix "Location" HTTP header decoding on non-ASCII URL redirects
    ([issue
    2321](https://github.com/scrapy/scrapy/issues/2321){.reference
    .external}).
:::

::: {#id117 .section}
##### Documentation[¶](#id117 "Permalink to this heading"){.headerlink}

-   Fix JsonWriterPipeline example ([issue
    2302](https://github.com/scrapy/scrapy/issues/2302){.reference
    .external}).

-   Various notes: [issue
    2330](https://github.com/scrapy/scrapy/issues/2330){.reference
    .external} on spider names, [issue
    2329](https://github.com/scrapy/scrapy/issues/2329){.reference
    .external} on middleware methods processing order, [issue
    2327](https://github.com/scrapy/scrapy/issues/2327){.reference
    .external} on getting multi-valued HTTP headers as lists.
:::

::: {#id118 .section}
##### Other changes[¶](#id118 "Permalink to this heading"){.headerlink}

-   Removed [`www.`{.docutils .literal .notranslate}]{.pre} from
    [`start_urls`{.docutils .literal .notranslate}]{.pre} in built-in
    spider templates ([issue
    2299](https://github.com/scrapy/scrapy/issues/2299){.reference
    .external}).
:::
:::

::: {#scrapy-1-2-0-2016-10-03 .section}
[]{#release-1-2-0}

#### Scrapy 1.2.0 (2016-10-03)[¶](#scrapy-1-2-0-2016-10-03 "Permalink to this heading"){.headerlink}

::: {#id119 .section}
##### New Features[¶](#id119 "Permalink to this heading"){.headerlink}

-   New [[`FEED_EXPORT_ENCODING`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_ENCODING){.hoverxref
    .tooltip .reference .internal} setting to customize the encoding
    used when writing items to a file. This can be used to turn off
    [`\uXXXX`{.docutils .literal .notranslate}]{.pre} escapes in JSON
    output. This is also useful for those wanting something else than
    UTF-8 for XML or CSV output ([issue
    2034](https://github.com/scrapy/scrapy/issues/2034){.reference
    .external}).

-   [`startproject`{.docutils .literal .notranslate}]{.pre} command now
    supports an optional destination directory to override the default
    one based on the project name ([issue
    2005](https://github.com/scrapy/scrapy/issues/2005){.reference
    .external}).

-   New [[`SCHEDULER_DEBUG`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DEBUG){.hoverxref
    .tooltip .reference .internal} setting to log requests serialization
    failures ([issue
    1610](https://github.com/scrapy/scrapy/issues/1610){.reference
    .external}).

-   JSON encoder now supports serialization of [`set`{.docutils .literal
    .notranslate}]{.pre} instances ([issue
    2058](https://github.com/scrapy/scrapy/issues/2058){.reference
    .external}).

-   Interpret [`application/json-amazonui-streaming`{.docutils .literal
    .notranslate}]{.pre} as [`TextResponse`{.docutils .literal
    .notranslate}]{.pre} ([issue
    1503](https://github.com/scrapy/scrapy/issues/1503){.reference
    .external}).

-   [`scrapy`{.docutils .literal .notranslate}]{.pre} is imported by
    default when using shell tools ([[`shell`{.xref .std .std-command
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-shell){.hoverxref
    .tooltip .reference .internal}, [[inspect_response]{.std
    .std-ref}](index.html#topics-shell-inspect-response){.hoverxref
    .tooltip .reference .internal}) ([issue
    2248](https://github.com/scrapy/scrapy/issues/2248){.reference
    .external}).
:::

::: {#id120 .section}
##### Bug fixes[¶](#id120 "Permalink to this heading"){.headerlink}

-   DefaultRequestHeaders middleware now runs before UserAgent
    middleware ([issue
    2088](https://github.com/scrapy/scrapy/issues/2088){.reference
    .external}). **Warning: this is technically backward incompatible**,
    though we consider this a bug fix.

-   HTTP cache extension and plugins that use the [`.scrapy`{.docutils
    .literal .notranslate}]{.pre} data directory now work outside
    projects ([issue
    1581](https://github.com/scrapy/scrapy/issues/1581){.reference
    .external}). **Warning: this is technically backward incompatible**,
    though we consider this a bug fix.

-   [`Selector`{.docutils .literal .notranslate}]{.pre} does not allow
    passing both [`response`{.docutils .literal .notranslate}]{.pre} and
    [`text`{.docutils .literal .notranslate}]{.pre} anymore ([issue
    2153](https://github.com/scrapy/scrapy/issues/2153){.reference
    .external}).

-   Fixed logging of wrong callback name with [`scrapy`{.docutils
    .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`parse`{.docutils .literal .notranslate}]{.pre}
    ([issue
    2169](https://github.com/scrapy/scrapy/issues/2169){.reference
    .external}).

-   Fix for an odd gzip decompression bug ([issue
    1606](https://github.com/scrapy/scrapy/issues/1606){.reference
    .external}).

-   Fix for selected callbacks when using [`CrawlSpider`{.docutils
    .literal .notranslate}]{.pre} with [[`scrapy`{.xref .std
    .std-command .docutils .literal .notranslate}]{.pre}` `{.xref .std
    .std-command .docutils .literal .notranslate}[`parse`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-parse){.hoverxref
    .tooltip .reference .internal} ([issue
    2225](https://github.com/scrapy/scrapy/issues/2225){.reference
    .external}).

-   Fix for invalid JSON and XML files when spider yields no items
    ([issue 872](https://github.com/scrapy/scrapy/issues/872){.reference
    .external}).

-   Implement [`flush()`{.docutils .literal .notranslate}]{.pre} for
    [`StreamLogger`{.docutils .literal .notranslate}]{.pre} avoiding a
    warning in logs ([issue
    2125](https://github.com/scrapy/scrapy/issues/2125){.reference
    .external}).
:::

::: {#refactoring .section}
##### Refactoring[¶](#refactoring "Permalink to this heading"){.headerlink}

-   [`canonicalize_url`{.docutils .literal .notranslate}]{.pre} has been
    moved to
    [w3lib.url](https://w3lib.readthedocs.io/en/latest/w3lib.html#w3lib.url.canonicalize_url){.reference
    .external} ([issue
    2168](https://github.com/scrapy/scrapy/issues/2168){.reference
    .external}).
:::

::: {#tests-requirements .section}
##### Tests & Requirements[¶](#tests-requirements "Permalink to this heading"){.headerlink}

Scrapy's new requirements baseline is Debian 8 "Jessie". It was
previously Ubuntu 12.04 Precise. What this means in practice is that we
run continuous integration tests with these (main) packages versions at
a minimum: Twisted 14.0, pyOpenSSL 0.14, lxml 3.4.

Scrapy may very well work with older versions of these packages (the
code base still has switches for older Twisted versions for example) but
it is not guaranteed (because it's not tested anymore).
:::

::: {#id121 .section}
##### Documentation[¶](#id121 "Permalink to this heading"){.headerlink}

-   Grammar fixes: [issue
    2128](https://github.com/scrapy/scrapy/issues/2128){.reference
    .external}, [issue
    1566](https://github.com/scrapy/scrapy/issues/1566){.reference
    .external}.

-   Download stats badge removed from README ([issue
    2160](https://github.com/scrapy/scrapy/issues/2160){.reference
    .external}).

-   New Scrapy [[architecture diagram]{.std
    .std-ref}](index.html#topics-architecture){.hoverxref .tooltip
    .reference .internal} ([issue
    2165](https://github.com/scrapy/scrapy/issues/2165){.reference
    .external}).

-   Updated [`Response`{.docutils .literal .notranslate}]{.pre}
    parameters documentation ([issue
    2197](https://github.com/scrapy/scrapy/issues/2197){.reference
    .external}).

-   Reworded misleading [[`RANDOMIZE_DOWNLOAD_DELAY`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-RANDOMIZE_DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal} description ([issue
    2190](https://github.com/scrapy/scrapy/issues/2190){.reference
    .external}).

-   Add StackOverflow as a support channel ([issue
    2257](https://github.com/scrapy/scrapy/issues/2257){.reference
    .external}).
:::
:::

::: {#scrapy-1-1-4-2017-03-03 .section}
[]{#release-1-1-4}

#### Scrapy 1.1.4 (2017-03-03)[¶](#scrapy-1-1-4-2017-03-03 "Permalink to this heading"){.headerlink}

-   Packaging fix: disallow unsupported Twisted versions in setup.py
:::

::: {#scrapy-1-1-3-2016-09-22 .section}
[]{#release-1-1-3}

#### Scrapy 1.1.3 (2016-09-22)[¶](#scrapy-1-1-3-2016-09-22 "Permalink to this heading"){.headerlink}

::: {#id122 .section}
##### Bug fixes[¶](#id122 "Permalink to this heading"){.headerlink}

-   Class attributes for subclasses of [`ImagesPipeline`{.docutils
    .literal .notranslate}]{.pre} and [`FilesPipeline`{.docutils
    .literal .notranslate}]{.pre} work as they did before 1.1.1 ([issue
    2243](https://github.com/scrapy/scrapy/issues/2243){.reference
    .external}, fixes [issue
    2198](https://github.com/scrapy/scrapy/issues/2198){.reference
    .external})
:::

::: {#id123 .section}
##### Documentation[¶](#id123 "Permalink to this heading"){.headerlink}

-   [[Overview]{.std .std-ref}](index.html#intro-overview){.hoverxref
    .tooltip .reference .internal} and [[tutorial]{.std
    .std-ref}](index.html#intro-tutorial){.hoverxref .tooltip .reference
    .internal} rewritten to use
    [http://toscrape.com](http://toscrape.com){.reference .external}
    websites ([issue
    2236](https://github.com/scrapy/scrapy/issues/2236){.reference
    .external}, [issue
    2249](https://github.com/scrapy/scrapy/issues/2249){.reference
    .external}, [issue
    2252](https://github.com/scrapy/scrapy/issues/2252){.reference
    .external}).
:::
:::

::: {#scrapy-1-1-2-2016-08-18 .section}
[]{#release-1-1-2}

#### Scrapy 1.1.2 (2016-08-18)[¶](#scrapy-1-1-2-2016-08-18 "Permalink to this heading"){.headerlink}

::: {#id124 .section}
##### Bug fixes[¶](#id124 "Permalink to this heading"){.headerlink}

-   Introduce a missing [[`IMAGES_STORE_S3_ACL`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-IMAGES_STORE_S3_ACL){.hoverxref
    .tooltip .reference .internal} setting to override the default ACL
    policy in [`ImagesPipeline`{.docutils .literal .notranslate}]{.pre}
    when uploading images to S3 (note that default ACL policy is
    "private" -- instead of "public-read" -- since Scrapy 1.1.0)

-   [[`IMAGES_EXPIRES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-IMAGES_EXPIRES){.hoverxref
    .tooltip .reference .internal} default value set back to 90 (the
    regression was introduced in 1.1.1)
:::
:::

::: {#scrapy-1-1-1-2016-07-13 .section}
[]{#release-1-1-1}

#### Scrapy 1.1.1 (2016-07-13)[¶](#scrapy-1-1-1-2016-07-13 "Permalink to this heading"){.headerlink}

::: {#id125 .section}
##### Bug fixes[¶](#id125 "Permalink to this heading"){.headerlink}

-   Add "Host" header in CONNECT requests to HTTPS proxies ([issue
    2069](https://github.com/scrapy/scrapy/issues/2069){.reference
    .external})

-   Use response [`body`{.docutils .literal .notranslate}]{.pre} when
    choosing response class ([issue
    2001](https://github.com/scrapy/scrapy/issues/2001){.reference
    .external}, fixes [issue
    2000](https://github.com/scrapy/scrapy/issues/2000){.reference
    .external})

-   Do not fail on canonicalizing URLs with wrong netlocs ([issue
    2038](https://github.com/scrapy/scrapy/issues/2038){.reference
    .external}, fixes [issue
    2010](https://github.com/scrapy/scrapy/issues/2010){.reference
    .external})

-   a few fixes for [`HttpCompressionMiddleware`{.docutils .literal
    .notranslate}]{.pre} (and [`SitemapSpider`{.docutils .literal
    .notranslate}]{.pre}):

    -   Do not decode HEAD responses ([issue
        2008](https://github.com/scrapy/scrapy/issues/2008){.reference
        .external}, fixes [issue
        1899](https://github.com/scrapy/scrapy/issues/1899){.reference
        .external})

    -   Handle charset parameter in gzip Content-Type header ([issue
        2050](https://github.com/scrapy/scrapy/issues/2050){.reference
        .external}, fixes [issue
        2049](https://github.com/scrapy/scrapy/issues/2049){.reference
        .external})

    -   Do not decompress gzip octet-stream responses ([issue
        2065](https://github.com/scrapy/scrapy/issues/2065){.reference
        .external}, fixes [issue
        2063](https://github.com/scrapy/scrapy/issues/2063){.reference
        .external})

-   Catch (and ignore with a warning) exception when verifying
    certificate against IP-address hosts ([issue
    2094](https://github.com/scrapy/scrapy/issues/2094){.reference
    .external}, fixes [issue
    2092](https://github.com/scrapy/scrapy/issues/2092){.reference
    .external})

-   Make [`FilesPipeline`{.docutils .literal .notranslate}]{.pre} and
    [`ImagesPipeline`{.docutils .literal .notranslate}]{.pre} backward
    compatible again regarding the use of legacy class attributes for
    customization ([issue
    1989](https://github.com/scrapy/scrapy/issues/1989){.reference
    .external}, fixes [issue
    1985](https://github.com/scrapy/scrapy/issues/1985){.reference
    .external})
:::

::: {#id126 .section}
##### New features[¶](#id126 "Permalink to this heading"){.headerlink}

-   Enable genspider command outside project folder ([issue
    2052](https://github.com/scrapy/scrapy/issues/2052){.reference
    .external})

-   Retry HTTPS CONNECT [`TunnelError`{.docutils .literal
    .notranslate}]{.pre} by default ([issue
    1974](https://github.com/scrapy/scrapy/issues/1974){.reference
    .external})
:::

::: {#id127 .section}
##### Documentation[¶](#id127 "Permalink to this heading"){.headerlink}

-   [`FEED_TEMPDIR`{.docutils .literal .notranslate}]{.pre} setting at
    lexicographical position ([commit
    9b3c72c](https://github.com/scrapy/scrapy/commit/9b3c72c){.reference
    .external})

-   Use idiomatic [`.extract_first()`{.docutils .literal
    .notranslate}]{.pre} in overview ([issue
    1994](https://github.com/scrapy/scrapy/issues/1994){.reference
    .external})

-   Update years in copyright notice ([commit
    c2c8036](https://github.com/scrapy/scrapy/commit/c2c8036){.reference
    .external})

-   Add information and example on errbacks ([issue
    1995](https://github.com/scrapy/scrapy/issues/1995){.reference
    .external})

-   Use "url" variable in downloader middleware example ([issue
    2015](https://github.com/scrapy/scrapy/issues/2015){.reference
    .external})

-   Grammar fixes ([issue
    2054](https://github.com/scrapy/scrapy/issues/2054){.reference
    .external}, [issue
    2120](https://github.com/scrapy/scrapy/issues/2120){.reference
    .external})

-   New FAQ entry on using BeautifulSoup in spider callbacks ([issue
    2048](https://github.com/scrapy/scrapy/issues/2048){.reference
    .external})

-   Add notes about Scrapy not working on Windows with Python 3 ([issue
    2060](https://github.com/scrapy/scrapy/issues/2060){.reference
    .external})

-   Encourage complete titles in pull requests ([issue
    2026](https://github.com/scrapy/scrapy/issues/2026){.reference
    .external})
:::

::: {#tests .section}
##### Tests[¶](#tests "Permalink to this heading"){.headerlink}

-   Upgrade py.test requirement on Travis CI and Pin pytest-cov to 2.2.1
    ([issue
    2095](https://github.com/scrapy/scrapy/issues/2095){.reference
    .external})
:::
:::

::: {#scrapy-1-1-0-2016-05-11 .section}
[]{#release-1-1-0}

#### Scrapy 1.1.0 (2016-05-11)[¶](#scrapy-1-1-0-2016-05-11 "Permalink to this heading"){.headerlink}

This 1.1 release brings a lot of interesting features and bug fixes:

-   Scrapy 1.1 has beta Python 3 support (requires Twisted \>= 15.5).
    See [[Beta Python 3 Support]{.std
    .std-ref}](#news-betapy3){.hoverxref .tooltip .reference .internal}
    for more details and some limitations.

-   Hot new features:

    -   Item loaders now support nested loaders ([issue
        1467](https://github.com/scrapy/scrapy/issues/1467){.reference
        .external}).

    -   [`FormRequest.from_response`{.docutils .literal
        .notranslate}]{.pre} improvements ([issue
        1382](https://github.com/scrapy/scrapy/issues/1382){.reference
        .external}, [issue
        1137](https://github.com/scrapy/scrapy/issues/1137){.reference
        .external}).

    -   Added setting [[`AUTOTHROTTLE_TARGET_CONCURRENCY`{.xref .std
        .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-AUTOTHROTTLE_TARGET_CONCURRENCY){.hoverxref
        .tooltip .reference .internal} and improved AutoThrottle docs
        ([issue
        1324](https://github.com/scrapy/scrapy/issues/1324){.reference
        .external}).

    -   Added [`response.text`{.docutils .literal .notranslate}]{.pre}
        to get body as unicode ([issue
        1730](https://github.com/scrapy/scrapy/issues/1730){.reference
        .external}).

    -   Anonymous S3 connections ([issue
        1358](https://github.com/scrapy/scrapy/issues/1358){.reference
        .external}).

    -   Deferreds in downloader middlewares ([issue
        1473](https://github.com/scrapy/scrapy/issues/1473){.reference
        .external}). This enables better robots.txt handling ([issue
        1471](https://github.com/scrapy/scrapy/issues/1471){.reference
        .external}).

    -   HTTP caching now follows RFC2616 more closely, added settings
        [[`HTTPCACHE_ALWAYS_STORE`{.xref .std .std-setting .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_ALWAYS_STORE){.hoverxref
        .tooltip .reference .internal} and
        [[`HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS`{.xref .std
        .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS){.hoverxref
        .tooltip .reference .internal} ([issue
        1151](https://github.com/scrapy/scrapy/issues/1151){.reference
        .external}).

    -   Selectors were extracted to the
        [parsel](https://github.com/scrapy/parsel){.reference .external}
        library ([issue
        1409](https://github.com/scrapy/scrapy/issues/1409){.reference
        .external}). This means you can use Scrapy Selectors without
        Scrapy and also upgrade the selectors engine without needing to
        upgrade Scrapy.

    -   HTTPS downloader now does TLS protocol negotiation by default,
        instead of forcing TLS 1.0. You can also set the SSL/TLS method
        using the new [[`DOWNLOADER_CLIENT_TLS_METHOD`{.xref .std
        .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENT_TLS_METHOD){.hoverxref
        .tooltip .reference .internal}.

-   These bug fixes may require your attention:

    -   Don't retry bad requests (HTTP 400) by default ([issue
        1289](https://github.com/scrapy/scrapy/issues/1289){.reference
        .external}). If you need the old behavior, add [`400`{.docutils
        .literal .notranslate}]{.pre} to [[`RETRY_HTTP_CODES`{.xref .std
        .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-RETRY_HTTP_CODES){.hoverxref
        .tooltip .reference .internal}.

    -   Fix shell files argument handling ([issue
        1710](https://github.com/scrapy/scrapy/issues/1710){.reference
        .external}, [issue
        1550](https://github.com/scrapy/scrapy/issues/1550){.reference
        .external}). If you try [`scrapy`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`shell`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`index.html`{.docutils .literal
        .notranslate}]{.pre} it will try to load the URL
        [http://index.html](http://index.html){.reference .external},
        use [`scrapy`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`shell`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`./index.html`{.docutils .literal
        .notranslate}]{.pre} to load a local file.

    -   Robots.txt compliance is now enabled by default for
        newly-created projects ([issue
        1724](https://github.com/scrapy/scrapy/issues/1724){.reference
        .external}). Scrapy will also wait for robots.txt to be
        downloaded before proceeding with the crawl ([issue
        1735](https://github.com/scrapy/scrapy/issues/1735){.reference
        .external}). If you want to disable this behavior, update
        [[`ROBOTSTXT_OBEY`{.xref .std .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-ROBOTSTXT_OBEY){.hoverxref
        .tooltip .reference .internal} in [`settings.py`{.docutils
        .literal .notranslate}]{.pre} file after creating a new project.

    -   Exporters now work on unicode, instead of bytes by default
        ([issue
        1080](https://github.com/scrapy/scrapy/issues/1080){.reference
        .external}). If you use [[`PythonItemExporter`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.exporters.PythonItemExporter "scrapy.exporters.PythonItemExporter"){.reference
        .internal}, you may want to update your code to disable binary
        mode which is now deprecated.

    -   Accept XML node names containing dots as valid ([issue
        1533](https://github.com/scrapy/scrapy/issues/1533){.reference
        .external}).

    -   When uploading files or images to S3 (with
        [`FilesPipeline`{.docutils .literal .notranslate}]{.pre} or
        [`ImagesPipeline`{.docutils .literal .notranslate}]{.pre}), the
        default ACL policy is now "private" instead of "public"
        **Warning: backward incompatible!**. You can use
        [[`FILES_STORE_S3_ACL`{.xref .std .std-setting .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-setting-FILES_STORE_S3_ACL){.hoverxref
        .tooltip .reference .internal} to change it.

    -   We've reimplemented [`canonicalize_url()`{.docutils .literal
        .notranslate}]{.pre} for more correct output, especially for
        URLs with non-ASCII characters ([issue
        1947](https://github.com/scrapy/scrapy/issues/1947){.reference
        .external}). This could change link extractors output compared
        to previous Scrapy versions. This may also invalidate some cache
        entries you could still have from pre-1.1 runs. **Warning:
        backward incompatible!**.

Keep reading for more details on other improvements and bug fixes.

::: {#beta-python-3-support .section}
[]{#news-betapy3}

##### Beta Python 3 Support[¶](#beta-python-3-support "Permalink to this heading"){.headerlink}

We have been [hard at work to make Scrapy run on Python
3](https://github.com/scrapy/scrapy/wiki/Python-3-Porting){.reference
.external}. As a result, now you can run spiders on Python 3.3, 3.4 and
3.5 (Twisted \>= 15.5 required). Some features are still missing (and
some may never be ported).

Almost all builtin extensions/middlewares are expected to work. However,
we are aware of some limitations in Python 3:

-   Scrapy does not work on Windows with Python 3

-   Sending emails is not supported

-   FTP download handler is not supported

-   Telnet console is not supported
:::

::: {#additional-new-features-and-enhancements .section}
##### Additional New Features and Enhancements[¶](#additional-new-features-and-enhancements "Permalink to this heading"){.headerlink}

-   Scrapy now has a [Code of
    Conduct](https://github.com/scrapy/scrapy/blob/master/CODE_OF_CONDUCT.md){.reference
    .external} ([issue
    1681](https://github.com/scrapy/scrapy/issues/1681){.reference
    .external}).

-   Command line tool now has completion for zsh ([issue
    934](https://github.com/scrapy/scrapy/issues/934){.reference
    .external}).

-   Improvements to [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`shell`{.docutils .literal .notranslate}]{.pre}:

    -   Support for bpython and configure preferred Python shell via
        [`SCRAPY_PYTHON_SHELL`{.docutils .literal .notranslate}]{.pre}
        ([issue
        1100](https://github.com/scrapy/scrapy/issues/1100){.reference
        .external}, [issue
        1444](https://github.com/scrapy/scrapy/issues/1444){.reference
        .external}).

    -   Support URLs without scheme ([issue
        1498](https://github.com/scrapy/scrapy/issues/1498){.reference
        .external}) **Warning: backward incompatible!**

    -   Bring back support for relative file path ([issue
        1710](https://github.com/scrapy/scrapy/issues/1710){.reference
        .external}, [issue
        1550](https://github.com/scrapy/scrapy/issues/1550){.reference
        .external}).

-   Added [[`MEMUSAGE_CHECK_INTERVAL_SECONDS`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-MEMUSAGE_CHECK_INTERVAL_SECONDS){.hoverxref
    .tooltip .reference .internal} setting to change default check
    interval ([issue
    1282](https://github.com/scrapy/scrapy/issues/1282){.reference
    .external}).

-   Download handlers are now lazy-loaded on first request using their
    scheme ([issue
    1390](https://github.com/scrapy/scrapy/issues/1390){.reference
    .external}, [issue
    1421](https://github.com/scrapy/scrapy/issues/1421){.reference
    .external}).

-   HTTPS download handlers do not force TLS 1.0 anymore; instead,
    OpenSSL's [`SSLv23_method()/TLS_method()`{.docutils .literal
    .notranslate}]{.pre} is used allowing to try negotiating with the
    remote hosts the highest TLS protocol version it can ([issue
    1794](https://github.com/scrapy/scrapy/issues/1794){.reference
    .external}, [issue
    1629](https://github.com/scrapy/scrapy/issues/1629){.reference
    .external}).

-   [`RedirectMiddleware`{.docutils .literal .notranslate}]{.pre} now
    skips the status codes from [`handle_httpstatus_list`{.docutils
    .literal .notranslate}]{.pre} on spider attribute or in
    [`Request`{.docutils .literal .notranslate}]{.pre}'s
    [`meta`{.docutils .literal .notranslate}]{.pre} key ([issue
    1334](https://github.com/scrapy/scrapy/issues/1334){.reference
    .external}, [issue
    1364](https://github.com/scrapy/scrapy/issues/1364){.reference
    .external}, [issue
    1447](https://github.com/scrapy/scrapy/issues/1447){.reference
    .external}).

-   Form submission:

    -   now works with [`<button>`{.docutils .literal
        .notranslate}]{.pre} elements too ([issue
        1469](https://github.com/scrapy/scrapy/issues/1469){.reference
        .external}).

    -   an empty string is now used for submit buttons without a value
        ([issue
        1472](https://github.com/scrapy/scrapy/issues/1472){.reference
        .external})

-   Dict-like settings now have per-key priorities ([issue
    1135](https://github.com/scrapy/scrapy/issues/1135){.reference
    .external}, [issue
    1149](https://github.com/scrapy/scrapy/issues/1149){.reference
    .external} and [issue
    1586](https://github.com/scrapy/scrapy/issues/1586){.reference
    .external}).

-   Sending non-ASCII emails ([issue
    1662](https://github.com/scrapy/scrapy/issues/1662){.reference
    .external})

-   [`CloseSpider`{.docutils .literal .notranslate}]{.pre} and
    [`SpiderState`{.docutils .literal .notranslate}]{.pre} extensions
    now get disabled if no relevant setting is set ([issue
    1723](https://github.com/scrapy/scrapy/issues/1723){.reference
    .external}, [issue
    1725](https://github.com/scrapy/scrapy/issues/1725){.reference
    .external}).

-   Added method [`ExecutionEngine.close`{.docutils .literal
    .notranslate}]{.pre} ([issue
    1423](https://github.com/scrapy/scrapy/issues/1423){.reference
    .external}).

-   Added method [`CrawlerRunner.create_crawler`{.docutils .literal
    .notranslate}]{.pre} ([issue
    1528](https://github.com/scrapy/scrapy/issues/1528){.reference
    .external}).

-   Scheduler priority queue can now be customized via
    [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref
    .tooltip .reference .internal} ([issue
    1822](https://github.com/scrapy/scrapy/issues/1822){.reference
    .external}).

-   [`.pps`{.docutils .literal .notranslate}]{.pre} links are now
    ignored by default in link extractors ([issue
    1835](https://github.com/scrapy/scrapy/issues/1835){.reference
    .external}).

-   temporary data folder for FTP and S3 feed storages can be customized
    using a new [[`FEED_TEMPDIR`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_TEMPDIR){.hoverxref
    .tooltip .reference .internal} setting ([issue
    1847](https://github.com/scrapy/scrapy/issues/1847){.reference
    .external}).

-   [`FilesPipeline`{.docutils .literal .notranslate}]{.pre} and
    [`ImagesPipeline`{.docutils .literal .notranslate}]{.pre} settings
    are now instance attributes instead of class attributes, enabling
    spider-specific behaviors ([issue
    1891](https://github.com/scrapy/scrapy/issues/1891){.reference
    .external}).

-   [`JsonItemExporter`{.docutils .literal .notranslate}]{.pre} now
    formats opening and closing square brackets on their own line (first
    and last lines of output file) ([issue
    1950](https://github.com/scrapy/scrapy/issues/1950){.reference
    .external}).

-   If available, [`botocore`{.docutils .literal .notranslate}]{.pre} is
    used for [`S3FeedStorage`{.docutils .literal .notranslate}]{.pre},
    [`S3DownloadHandler`{.docutils .literal .notranslate}]{.pre} and
    [`S3FilesStore`{.docutils .literal .notranslate}]{.pre} ([issue
    1761](https://github.com/scrapy/scrapy/issues/1761){.reference
    .external}, [issue
    1883](https://github.com/scrapy/scrapy/issues/1883){.reference
    .external}).

-   Tons of documentation updates and related fixes ([issue
    1291](https://github.com/scrapy/scrapy/issues/1291){.reference
    .external}, [issue
    1302](https://github.com/scrapy/scrapy/issues/1302){.reference
    .external}, [issue
    1335](https://github.com/scrapy/scrapy/issues/1335){.reference
    .external}, [issue
    1683](https://github.com/scrapy/scrapy/issues/1683){.reference
    .external}, [issue
    1660](https://github.com/scrapy/scrapy/issues/1660){.reference
    .external}, [issue
    1642](https://github.com/scrapy/scrapy/issues/1642){.reference
    .external}, [issue
    1721](https://github.com/scrapy/scrapy/issues/1721){.reference
    .external}, [issue
    1727](https://github.com/scrapy/scrapy/issues/1727){.reference
    .external}, [issue
    1879](https://github.com/scrapy/scrapy/issues/1879){.reference
    .external}).

-   Other refactoring, optimizations and cleanup ([issue
    1476](https://github.com/scrapy/scrapy/issues/1476){.reference
    .external}, [issue
    1481](https://github.com/scrapy/scrapy/issues/1481){.reference
    .external}, [issue
    1477](https://github.com/scrapy/scrapy/issues/1477){.reference
    .external}, [issue
    1315](https://github.com/scrapy/scrapy/issues/1315){.reference
    .external}, [issue
    1290](https://github.com/scrapy/scrapy/issues/1290){.reference
    .external}, [issue
    1750](https://github.com/scrapy/scrapy/issues/1750){.reference
    .external}, [issue
    1881](https://github.com/scrapy/scrapy/issues/1881){.reference
    .external}).
:::

::: {#deprecations-and-removals .section}
##### Deprecations and Removals[¶](#deprecations-and-removals "Permalink to this heading"){.headerlink}

-   Added [`to_bytes`{.docutils .literal .notranslate}]{.pre} and
    [`to_unicode`{.docutils .literal .notranslate}]{.pre}, deprecated
    [`str_to_unicode`{.docutils .literal .notranslate}]{.pre} and
    [`unicode_to_str`{.docutils .literal .notranslate}]{.pre} functions
    ([issue 778](https://github.com/scrapy/scrapy/issues/778){.reference
    .external}).

-   [`binary_is_text`{.docutils .literal .notranslate}]{.pre} is
    introduced, to replace use of [`isbinarytext`{.docutils .literal
    .notranslate}]{.pre} (but with inverse return value) ([issue
    1851](https://github.com/scrapy/scrapy/issues/1851){.reference
    .external})

-   The [`optional_features`{.docutils .literal .notranslate}]{.pre} set
    has been removed ([issue
    1359](https://github.com/scrapy/scrapy/issues/1359){.reference
    .external}).

-   The [`--lsprof`{.docutils .literal .notranslate}]{.pre} command line
    option has been removed ([issue
    1689](https://github.com/scrapy/scrapy/issues/1689){.reference
    .external}). **Warning: backward incompatible**, but doesn't break
    user code.

-   The following datatypes were deprecated ([issue
    1720](https://github.com/scrapy/scrapy/issues/1720){.reference
    .external}):

    -   [`scrapy.utils.datatypes.MultiValueDictKeyError`{.docutils
        .literal .notranslate}]{.pre}

    -   [`scrapy.utils.datatypes.MultiValueDict`{.docutils .literal
        .notranslate}]{.pre}

    -   [`scrapy.utils.datatypes.SiteNode`{.docutils .literal
        .notranslate}]{.pre}

-   The previously bundled [`scrapy.xlib.pydispatch`{.docutils .literal
    .notranslate}]{.pre} library was deprecated and replaced by
    [pydispatcher](https://pypi.org/project/PyDispatcher/){.reference
    .external}.
:::

::: {#relocations .section}
##### Relocations[¶](#relocations "Permalink to this heading"){.headerlink}

-   [`telnetconsole`{.docutils .literal .notranslate}]{.pre} was
    relocated to [`extensions/`{.docutils .literal .notranslate}]{.pre}
    ([issue
    1524](https://github.com/scrapy/scrapy/issues/1524){.reference
    .external}).

    -   Note: telnet is not enabled on Python 3
        ([https://github.com/scrapy/scrapy/pull/1524#issuecomment-146985595](https://github.com/scrapy/scrapy/pull/1524#issuecomment-146985595){.reference
        .external})
:::

::: {#bugfixes .section}
##### Bugfixes[¶](#bugfixes "Permalink to this heading"){.headerlink}

-   Scrapy does not retry requests that got a [`HTTP`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`400`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`Bad`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`Request`{.docutils .literal .notranslate}]{.pre}
    response anymore ([issue
    1289](https://github.com/scrapy/scrapy/issues/1289){.reference
    .external}). **Warning: backward incompatible!**

-   Support empty password for http_proxy config ([issue
    1274](https://github.com/scrapy/scrapy/issues/1274){.reference
    .external}).

-   Interpret [`application/x-json`{.docutils .literal
    .notranslate}]{.pre} as [`TextResponse`{.docutils .literal
    .notranslate}]{.pre} ([issue
    1333](https://github.com/scrapy/scrapy/issues/1333){.reference
    .external}).

-   Support link rel attribute with multiple values ([issue
    1201](https://github.com/scrapy/scrapy/issues/1201){.reference
    .external}).

-   Fixed [`scrapy.http.FormRequest.from_response`{.docutils .literal
    .notranslate}]{.pre} when there is a [`<base>`{.docutils .literal
    .notranslate}]{.pre} tag ([issue
    1564](https://github.com/scrapy/scrapy/issues/1564){.reference
    .external}).

-   Fixed [[`TEMPLATES_DIR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-TEMPLATES_DIR){.hoverxref
    .tooltip .reference .internal} handling ([issue
    1575](https://github.com/scrapy/scrapy/issues/1575){.reference
    .external}).

-   Various [`FormRequest`{.docutils .literal .notranslate}]{.pre} fixes
    ([issue
    1595](https://github.com/scrapy/scrapy/issues/1595){.reference
    .external}, [issue
    1596](https://github.com/scrapy/scrapy/issues/1596){.reference
    .external}, [issue
    1597](https://github.com/scrapy/scrapy/issues/1597){.reference
    .external}).

-   Makes [`_monkeypatches`{.docutils .literal .notranslate}]{.pre} more
    robust ([issue
    1634](https://github.com/scrapy/scrapy/issues/1634){.reference
    .external}).

-   Fixed bug on [`XMLItemExporter`{.docutils .literal
    .notranslate}]{.pre} with non-string fields in items ([issue
    1738](https://github.com/scrapy/scrapy/issues/1738){.reference
    .external}).

-   Fixed startproject command in macOS ([issue
    1635](https://github.com/scrapy/scrapy/issues/1635){.reference
    .external}).

-   Fixed [[`PythonItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.PythonItemExporter "scrapy.exporters.PythonItemExporter"){.reference
    .internal} and CSVExporter for non-string item types ([issue
    1737](https://github.com/scrapy/scrapy/issues/1737){.reference
    .external}).

-   Various logging related fixes ([issue
    1294](https://github.com/scrapy/scrapy/issues/1294){.reference
    .external}, [issue
    1419](https://github.com/scrapy/scrapy/issues/1419){.reference
    .external}, [issue
    1263](https://github.com/scrapy/scrapy/issues/1263){.reference
    .external}, [issue
    1624](https://github.com/scrapy/scrapy/issues/1624){.reference
    .external}, [issue
    1654](https://github.com/scrapy/scrapy/issues/1654){.reference
    .external}, [issue
    1722](https://github.com/scrapy/scrapy/issues/1722){.reference
    .external}, [issue
    1726](https://github.com/scrapy/scrapy/issues/1726){.reference
    .external} and [issue
    1303](https://github.com/scrapy/scrapy/issues/1303){.reference
    .external}).

-   Fixed bug in [`utils.template.render_templatefile()`{.docutils
    .literal .notranslate}]{.pre} ([issue
    1212](https://github.com/scrapy/scrapy/issues/1212){.reference
    .external}).

-   sitemaps extraction from [`robots.txt`{.docutils .literal
    .notranslate}]{.pre} is now case-insensitive ([issue
    1902](https://github.com/scrapy/scrapy/issues/1902){.reference
    .external}).

-   HTTPS+CONNECT tunnels could get mixed up when using multiple proxies
    to same remote host ([issue
    1912](https://github.com/scrapy/scrapy/issues/1912){.reference
    .external}).
:::
:::

::: {#scrapy-1-0-7-2017-03-03 .section}
[]{#release-1-0-7}

#### Scrapy 1.0.7 (2017-03-03)[¶](#scrapy-1-0-7-2017-03-03 "Permalink to this heading"){.headerlink}

-   Packaging fix: disallow unsupported Twisted versions in setup.py
:::

::: {#scrapy-1-0-6-2016-05-04 .section}
[]{#release-1-0-6}

#### Scrapy 1.0.6 (2016-05-04)[¶](#scrapy-1-0-6-2016-05-04 "Permalink to this heading"){.headerlink}

-   FIX: RetryMiddleware is now robust to non-standard HTTP status codes
    ([issue
    1857](https://github.com/scrapy/scrapy/issues/1857){.reference
    .external})

-   FIX: Filestorage HTTP cache was checking wrong modified time ([issue
    1875](https://github.com/scrapy/scrapy/issues/1875){.reference
    .external})

-   DOC: Support for Sphinx 1.4+ ([issue
    1893](https://github.com/scrapy/scrapy/issues/1893){.reference
    .external})

-   DOC: Consistency in selectors examples ([issue
    1869](https://github.com/scrapy/scrapy/issues/1869){.reference
    .external})
:::

::: {#scrapy-1-0-5-2016-02-04 .section}
[]{#release-1-0-5}

#### Scrapy 1.0.5 (2016-02-04)[¶](#scrapy-1-0-5-2016-02-04 "Permalink to this heading"){.headerlink}

-   FIX: \[Backport\] Ignore bogus links in LinkExtractors (fixes [issue
    907](https://github.com/scrapy/scrapy/issues/907){.reference
    .external}, [commit
    108195e](https://github.com/scrapy/scrapy/commit/108195e){.reference
    .external})

-   TST: Changed buildbot makefile to use 'pytest' ([commit
    1f3d90a](https://github.com/scrapy/scrapy/commit/1f3d90a){.reference
    .external})

-   DOC: Fixed typos in tutorial and media-pipeline ([commit
    808a9ea](https://github.com/scrapy/scrapy/commit/808a9ea){.reference
    .external} and [commit
    803bd87](https://github.com/scrapy/scrapy/commit/803bd87){.reference
    .external})

-   DOC: Add AjaxCrawlMiddleware to DOWNLOADER_MIDDLEWARES_BASE in
    settings docs ([commit
    aa94121](https://github.com/scrapy/scrapy/commit/aa94121){.reference
    .external})
:::

::: {#scrapy-1-0-4-2015-12-30 .section}
[]{#release-1-0-4}

#### Scrapy 1.0.4 (2015-12-30)[¶](#scrapy-1-0-4-2015-12-30 "Permalink to this heading"){.headerlink}

-   Ignoring xlib/tx folder, depending on Twisted version. ([commit
    7dfa979](https://github.com/scrapy/scrapy/commit/7dfa979){.reference
    .external})

-   Run on new travis-ci infra ([commit
    6e42f0b](https://github.com/scrapy/scrapy/commit/6e42f0b){.reference
    .external})

-   Spelling fixes ([commit
    823a1cc](https://github.com/scrapy/scrapy/commit/823a1cc){.reference
    .external})

-   escape nodename in xmliter regex ([commit
    da3c155](https://github.com/scrapy/scrapy/commit/da3c155){.reference
    .external})

-   test xml nodename with dots ([commit
    4418fc3](https://github.com/scrapy/scrapy/commit/4418fc3){.reference
    .external})

-   TST don't use broken Pillow version in tests ([commit
    a55078c](https://github.com/scrapy/scrapy/commit/a55078c){.reference
    .external})

-   disable log on version command. closes #1426 ([commit
    86fc330](https://github.com/scrapy/scrapy/commit/86fc330){.reference
    .external})

-   disable log on startproject command ([commit
    db4c9fe](https://github.com/scrapy/scrapy/commit/db4c9fe){.reference
    .external})

-   Add PyPI download stats badge ([commit
    df2b944](https://github.com/scrapy/scrapy/commit/df2b944){.reference
    .external})

-   don't run tests twice on Travis if a PR is made from a scrapy/scrapy
    branch ([commit
    a83ab41](https://github.com/scrapy/scrapy/commit/a83ab41){.reference
    .external})

-   Add Python 3 porting status badge to the README ([commit
    73ac80d](https://github.com/scrapy/scrapy/commit/73ac80d){.reference
    .external})

-   fixed RFPDupeFilter persistence ([commit
    97d080e](https://github.com/scrapy/scrapy/commit/97d080e){.reference
    .external})

-   TST a test to show that dupefilter persistence is not working
    ([commit
    97f2fb3](https://github.com/scrapy/scrapy/commit/97f2fb3){.reference
    .external})

-   explicit close file on [file://](file://){.reference .external}
    scheme handler ([commit
    d9b4850](https://github.com/scrapy/scrapy/commit/d9b4850){.reference
    .external})

-   Disable dupefilter in shell ([commit
    c0d0734](https://github.com/scrapy/scrapy/commit/c0d0734){.reference
    .external})

-   DOC: Add captions to toctrees which appear in sidebar ([commit
    aa239ad](https://github.com/scrapy/scrapy/commit/aa239ad){.reference
    .external})

-   DOC Removed pywin32 from install instructions as it's already
    declared as dependency. ([commit
    10eb400](https://github.com/scrapy/scrapy/commit/10eb400){.reference
    .external})

-   Added installation notes about using Conda for Windows and other
    OSes. ([commit
    1c3600a](https://github.com/scrapy/scrapy/commit/1c3600a){.reference
    .external})

-   Fixed minor grammar issues. ([commit
    7f4ddd5](https://github.com/scrapy/scrapy/commit/7f4ddd5){.reference
    .external})

-   fixed a typo in the documentation. ([commit
    b71f677](https://github.com/scrapy/scrapy/commit/b71f677){.reference
    .external})

-   Version 1 now exists ([commit
    5456c0e](https://github.com/scrapy/scrapy/commit/5456c0e){.reference
    .external})

-   fix another invalid xpath error ([commit
    0a1366e](https://github.com/scrapy/scrapy/commit/0a1366e){.reference
    .external})

-   fix ValueError: Invalid XPath: //div/\[id="not-exists"\]/text() on
    selectors.rst ([commit
    ca8d60f](https://github.com/scrapy/scrapy/commit/ca8d60f){.reference
    .external})

-   Typos corrections ([commit
    7067117](https://github.com/scrapy/scrapy/commit/7067117){.reference
    .external})

-   fix typos in downloader-middleware.rst and exceptions.rst, middlware
    -\> middleware ([commit
    32f115c](https://github.com/scrapy/scrapy/commit/32f115c){.reference
    .external})

-   Add note to Ubuntu install section about Debian compatibility
    ([commit
    23fda69](https://github.com/scrapy/scrapy/commit/23fda69){.reference
    .external})

-   Replace alternative macOS install workaround with virtualenv
    ([commit
    98b63ee](https://github.com/scrapy/scrapy/commit/98b63ee){.reference
    .external})

-   Reference Homebrew's homepage for installation instructions ([commit
    1925db1](https://github.com/scrapy/scrapy/commit/1925db1){.reference
    .external})

-   Add oldest supported tox version to contributing docs ([commit
    5d10d6d](https://github.com/scrapy/scrapy/commit/5d10d6d){.reference
    .external})

-   Note in install docs about pip being already included in
    python\>=2.7.9 ([commit
    85c980e](https://github.com/scrapy/scrapy/commit/85c980e){.reference
    .external})

-   Add non-python dependencies to Ubuntu install section in the docs
    ([commit
    fbd010d](https://github.com/scrapy/scrapy/commit/fbd010d){.reference
    .external})

-   Add macOS installation section to docs ([commit
    d8f4cba](https://github.com/scrapy/scrapy/commit/d8f4cba){.reference
    .external})

-   DOC(ENH): specify path to rtd theme explicitly ([commit
    de73b1a](https://github.com/scrapy/scrapy/commit/de73b1a){.reference
    .external})

-   minor: scrapy.Spider docs grammar ([commit
    1ddcc7b](https://github.com/scrapy/scrapy/commit/1ddcc7b){.reference
    .external})

-   Make common practices sample code match the comments ([commit
    1b85bcf](https://github.com/scrapy/scrapy/commit/1b85bcf){.reference
    .external})

-   nextcall repetitive calls (heartbeats). ([commit
    55f7104](https://github.com/scrapy/scrapy/commit/55f7104){.reference
    .external})

-   Backport fix compatibility with Twisted 15.4.0 ([commit
    b262411](https://github.com/scrapy/scrapy/commit/b262411){.reference
    .external})

-   pin pytest to 2.7.3 ([commit
    a6535c2](https://github.com/scrapy/scrapy/commit/a6535c2){.reference
    .external})

-   Merge pull request #1512 from mgedmin/patch-1 ([commit
    8876111](https://github.com/scrapy/scrapy/commit/8876111){.reference
    .external})

-   Merge pull request #1513 from mgedmin/patch-2 ([commit
    5d4daf8](https://github.com/scrapy/scrapy/commit/5d4daf8){.reference
    .external})

-   Typo ([commit
    f8d0682](https://github.com/scrapy/scrapy/commit/f8d0682){.reference
    .external})

-   Fix list formatting ([commit
    5f83a93](https://github.com/scrapy/scrapy/commit/5f83a93){.reference
    .external})

-   fix Scrapy squeue tests after recent changes to queuelib ([commit
    3365c01](https://github.com/scrapy/scrapy/commit/3365c01){.reference
    .external})

-   Merge pull request #1475 from rweindl/patch-1 ([commit
    2d688cd](https://github.com/scrapy/scrapy/commit/2d688cd){.reference
    .external})

-   Update tutorial.rst ([commit
    fbc1f25](https://github.com/scrapy/scrapy/commit/fbc1f25){.reference
    .external})

-   Merge pull request #1449 from rhoekman/patch-1 ([commit
    7d6538c](https://github.com/scrapy/scrapy/commit/7d6538c){.reference
    .external})

-   Small grammatical change ([commit
    8752294](https://github.com/scrapy/scrapy/commit/8752294){.reference
    .external})

-   Add openssl version to version command ([commit
    13c45ac](https://github.com/scrapy/scrapy/commit/13c45ac){.reference
    .external})
:::

::: {#scrapy-1-0-3-2015-08-11 .section}
[]{#release-1-0-3}

#### Scrapy 1.0.3 (2015-08-11)[¶](#scrapy-1-0-3-2015-08-11 "Permalink to this heading"){.headerlink}

-   add service_identity to Scrapy install_requires ([commit
    cbc2501](https://github.com/scrapy/scrapy/commit/cbc2501){.reference
    .external})

-   Workaround for travis#296 ([commit
    66af9cd](https://github.com/scrapy/scrapy/commit/66af9cd){.reference
    .external})
:::

::: {#scrapy-1-0-2-2015-08-06 .section}
[]{#release-1-0-2}

#### Scrapy 1.0.2 (2015-08-06)[¶](#scrapy-1-0-2-2015-08-06 "Permalink to this heading"){.headerlink}

-   Twisted 15.3.0 does not raises PicklingError serializing lambda
    functions ([commit
    b04dd7d](https://github.com/scrapy/scrapy/commit/b04dd7d){.reference
    .external})

-   Minor method name fix ([commit
    6f85c7f](https://github.com/scrapy/scrapy/commit/6f85c7f){.reference
    .external})

-   minor: scrapy.Spider grammar and clarity ([commit
    9c9d2e0](https://github.com/scrapy/scrapy/commit/9c9d2e0){.reference
    .external})

-   Put a blurb about support channels in CONTRIBUTING ([commit
    c63882b](https://github.com/scrapy/scrapy/commit/c63882b){.reference
    .external})

-   Fixed typos ([commit
    a9ae7b0](https://github.com/scrapy/scrapy/commit/a9ae7b0){.reference
    .external})

-   Fix doc reference. ([commit
    7c8a4fe](https://github.com/scrapy/scrapy/commit/7c8a4fe){.reference
    .external})
:::

::: {#scrapy-1-0-1-2015-07-01 .section}
[]{#release-1-0-1}

#### Scrapy 1.0.1 (2015-07-01)[¶](#scrapy-1-0-1-2015-07-01 "Permalink to this heading"){.headerlink}

-   Unquote request path before passing to FTPClient, it already escape
    paths ([commit