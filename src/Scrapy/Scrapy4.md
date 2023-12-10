.std-ref}](index.html#topics-downloader-middleware-setting){.hoverxref
.tooltip .reference .internal}.
:::

::: {#downloader-stats .section}
[]{#std-setting-DOWNLOADER_STATS}

##### DOWNLOADER_STATS[¶](#downloader-stats "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether to enable downloader stats collection.
:::

::: {#download-delay .section}
[]{#std-setting-DOWNLOAD_DELAY}

##### DOWNLOAD_DELAY[¶](#download-delay "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

Minimum seconds to wait between 2 consecutive requests to the same
domain.

Use [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal} to throttle your crawling speed, to avoid hitting
servers too hard.

Decimal numbers are supported. For example, to send a maximum of 4
requests every 10 seconds:

::: {.highlight-python .notranslate}
::: highlight
    DOWNLOAD_DELAY = 2.5
:::
:::

This setting is also affected by the [[`RANDOMIZE_DOWNLOAD_DELAY`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-RANDOMIZE_DOWNLOAD_DELAY){.hoverxref
.tooltip .reference .internal} setting, which is enabled by default.

When [[`CONCURRENT_REQUESTS_PER_IP`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal} is non-zero, delays are enforced per IP
address instead of per domain.

Note that [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal} can lower the effective per-domain concurrency
below [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal}. If the response time of a domain is
lower than [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal}, the effective concurrency for that domain is 1.
When testing throttling configurations, it usually makes sense to lower
[[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} first, and only increase
[[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal} once [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} is 1 but a higher throttling is desired.

::: {#spider-download-delay-attribute .admonition .note}
Note

This delay can be set per spider using [`download_delay`{.xref .py
.py-attr .docutils .literal .notranslate}]{.pre} spider attribute.
:::

It is also possible to change this setting per domain, although it
requires non-trivial code. See the implementation of the
[[AutoThrottle]{.std
.std-ref}](index.html#topics-autothrottle){.hoverxref .tooltip
.reference .internal} extension for an example.
:::

::: {#download-handlers .section}
[]{#std-setting-DOWNLOAD_HANDLERS}

##### DOWNLOAD_HANDLERS[¶](#download-handlers "Permalink to this heading"){.headerlink}

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing the request downloader handlers enabled in your
project. See [[`DOWNLOAD_HANDLERS_BASE`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_HANDLERS_BASE){.hoverxref
.tooltip .reference .internal} for example format.
:::

::: {#download-handlers-base .section}
[]{#std-setting-DOWNLOAD_HANDLERS_BASE}

##### DOWNLOAD_HANDLERS_BASE[¶](#download-handlers-base "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "data": "scrapy.core.downloader.handlers.datauri.DataURIDownloadHandler",
        "file": "scrapy.core.downloader.handlers.file.FileDownloadHandler",
        "http": "scrapy.core.downloader.handlers.http.HTTPDownloadHandler",
        "https": "scrapy.core.downloader.handlers.http.HTTPDownloadHandler",
        "s3": "scrapy.core.downloader.handlers.s3.S3DownloadHandler",
        "ftp": "scrapy.core.downloader.handlers.ftp.FTPDownloadHandler",
    }
:::
:::

A dict containing the request download handlers enabled by default in
Scrapy. You should never modify this setting in your project, modify
[[`DOWNLOAD_HANDLERS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_HANDLERS){.hoverxref
.tooltip .reference .internal} instead.

You can disable any of these download handlers by assigning
[`None`{.docutils .literal .notranslate}]{.pre} to their URI scheme in
[[`DOWNLOAD_HANDLERS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_HANDLERS){.hoverxref
.tooltip .reference .internal}. E.g., to disable the built-in FTP
handler (without replacement), place this in your
[`settings.py`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    DOWNLOAD_HANDLERS = {
        "ftp": None,
    }
:::
:::

The default HTTPS handler uses HTTP/1.1. To use HTTP/2:

1.  Install [`Twisted[http2]>=17.9.0`{.docutils .literal
    .notranslate}]{.pre} to install the packages required to enable
    HTTP/2 support in Twisted.

2.  Update [[`DOWNLOAD_HANDLERS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal} as follows:

    ::: {.highlight-python .notranslate}
    ::: highlight
        DOWNLOAD_HANDLERS = {
            "https": "scrapy.core.downloader.handlers.http2.H2DownloadHandler",
        }
    :::
    :::

::: {.admonition .warning}
Warning

HTTP/2 support in Scrapy is experimental, and not yet recommended for
production environments. Future Scrapy versions may introduce related
changes without a deprecation period or warning.
:::

::: {.admonition .note}
Note

Known limitations of the current HTTP/2 implementation of Scrapy
include:

-   No support for HTTP/2 Cleartext (h2c), since no major browser
    supports HTTP/2 unencrypted (refer [http2
    faq](https://http2.github.io/faq/#does-http2-require-encryption){.reference
    .external}).

-   No setting to specify a maximum [frame
    size](https://tools.ietf.org/html/rfc7540#section-4.2){.reference
    .external} larger than the default value, 16384. Connections to
    servers that send a larger frame will fail.

-   No support for [server
    pushes](https://tools.ietf.org/html/rfc7540#section-8.2){.reference
    .external}, which are ignored.

-   No support for the [[`bytes_received`{.xref .std .std-signal
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-bytes_received){.hoverxref
    .tooltip .reference .internal} and [[`headers_received`{.xref .std
    .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-headers_received){.hoverxref
    .tooltip .reference .internal} signals.
:::
:::

::: {#download-slots .section}
[]{#std-setting-DOWNLOAD_SLOTS}

##### DOWNLOAD_SLOTS[¶](#download-slots "Permalink to this heading"){.headerlink}

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

Allows to define concurrency/delay parameters on per slot (domain)
basis:

> <div>
>
> ::: {.highlight-python .notranslate}
> ::: highlight
>     DOWNLOAD_SLOTS = {
>         "quotes.toscrape.com": {"concurrency": 1, "delay": 2, "randomize_delay": False},
>         "books.toscrape.com": {"delay": 3, "randomize_delay": False},
>     }
> :::
> :::
>
> </div>

::: {.admonition .note}
Note

For other downloader slots default settings values will be used:

-   [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal}: [`delay`{.docutils .literal
    .notranslate}]{.pre}

-   [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
    .tooltip .reference .internal}: [`concurrency`{.docutils .literal
    .notranslate}]{.pre}

-   [[`RANDOMIZE_DOWNLOAD_DELAY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-RANDOMIZE_DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal}: [`randomize_delay`{.docutils
    .literal .notranslate}]{.pre}
:::
:::

::: {#download-timeout .section}
[]{#std-setting-DOWNLOAD_TIMEOUT}

##### DOWNLOAD_TIMEOUT[¶](#download-timeout "Permalink to this heading"){.headerlink}

Default: [`180`{.docutils .literal .notranslate}]{.pre}

The amount of time (in secs) that the downloader will wait before timing
out.

::: {.admonition .note}
Note

This timeout can be set per spider using [`download_timeout`{.xref .py
.py-attr .docutils .literal .notranslate}]{.pre} spider attribute and
per-request using [[`download_timeout`{.xref .std .std-reqmeta .docutils
.literal
.notranslate}]{.pre}](index.html#std-reqmeta-download_timeout){.hoverxref
.tooltip .reference .internal} Request.meta key.
:::
:::

::: {#download-maxsize .section}
[]{#std-setting-DOWNLOAD_MAXSIZE}

##### DOWNLOAD_MAXSIZE[¶](#download-maxsize "Permalink to this heading"){.headerlink}

Default: [`1073741824`{.docutils .literal .notranslate}]{.pre} (1024MB)

The maximum response size (in bytes) that downloader will download.

If you want to disable it set to 0.

::: {#std-reqmeta-download_maxsize .admonition .note}
Note

This size can be set per spider using [`download_maxsize`{.xref .py
.py-attr .docutils .literal .notranslate}]{.pre} spider attribute and
per-request using [[`download_maxsize`{.xref .std .std-reqmeta .docutils
.literal .notranslate}]{.pre}](#std-reqmeta-download_maxsize){.hoverxref
.tooltip .reference .internal} Request.meta key.
:::
:::

::: {#download-warnsize .section}
[]{#std-setting-DOWNLOAD_WARNSIZE}

##### DOWNLOAD_WARNSIZE[¶](#download-warnsize "Permalink to this heading"){.headerlink}

Default: [`33554432`{.docutils .literal .notranslate}]{.pre} (32MB)

The response size (in bytes) that downloader will start to warn.

If you want to disable it set to 0.

::: {.admonition .note}
Note

This size can be set per spider using [`download_warnsize`{.xref .py
.py-attr .docutils .literal .notranslate}]{.pre} spider attribute and
per-request using [`download_warnsize`{.xref .std .std-reqmeta .docutils
.literal .notranslate}]{.pre} Request.meta key.
:::
:::

::: {#download-fail-on-dataloss .section}
[]{#std-setting-DOWNLOAD_FAIL_ON_DATALOSS}

##### DOWNLOAD_FAIL_ON_DATALOSS[¶](#download-fail-on-dataloss "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether or not to fail on broken responses, that is, declared
[`Content-Length`{.docutils .literal .notranslate}]{.pre} does not match
content sent by the server or chunked response was not properly finish.
If [`True`{.docutils .literal .notranslate}]{.pre}, these responses
raise a [`ResponseFailed([_DataLoss])`{.docutils .literal
.notranslate}]{.pre} error. If [`False`{.docutils .literal
.notranslate}]{.pre}, these responses are passed through and the flag
[`dataloss`{.docutils .literal .notranslate}]{.pre} is added to the
response, i.e.: [`'dataloss'`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`in`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`response.flags`{.docutils .literal .notranslate}]{.pre}
is [`True`{.docutils .literal .notranslate}]{.pre}.

Optionally, this can be set per-request basis by using the
[[`download_fail_on_dataloss`{.xref .std .std-reqmeta .docutils .literal
.notranslate}]{.pre}](index.html#std-reqmeta-download_fail_on_dataloss){.hoverxref
.tooltip .reference .internal} Request.meta key to [`False`{.docutils
.literal .notranslate}]{.pre}.

::: {.admonition .note}
Note

A broken response, or data loss error, may happen under several
circumstances, from server misconfiguration to network errors to data
corruption. It is up to the user to decide if it makes sense to process
broken responses considering they may contain partial or incomplete
content. If [[`RETRY_ENABLED`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-RETRY_ENABLED){.hoverxref
.tooltip .reference .internal} is [`True`{.docutils .literal
.notranslate}]{.pre} and this setting is set to [`True`{.docutils
.literal .notranslate}]{.pre}, the
[`ResponseFailed([_DataLoss])`{.docutils .literal .notranslate}]{.pre}
failure will be retried as usual.
:::

::: {.admonition .warning}
Warning

This setting is ignored by the [`H2DownloadHandler`{.xref .py .py-class
.docutils .literal .notranslate}]{.pre} download handler (see
[[`DOWNLOAD_HANDLERS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_HANDLERS){.hoverxref
.tooltip .reference .internal}). In case of a data loss error, the
corresponding HTTP/2 connection may be corrupted, affecting other
requests that use the same connection; hence, a
[`ResponseFailed([InvalidBodyLengthError])`{.docutils .literal
.notranslate}]{.pre} failure is always raised for every request that was
using that connection.
:::
:::

::: {#dupefilter-class .section}
[]{#std-setting-DUPEFILTER_CLASS}

##### DUPEFILTER_CLASS[¶](#dupefilter-class "Permalink to this heading"){.headerlink}

Default: [`'scrapy.dupefilters.RFPDupeFilter'`{.docutils .literal
.notranslate}]{.pre}

The class used to detect and filter duplicate requests.

The default ([`RFPDupeFilter`{.docutils .literal .notranslate}]{.pre})
filters based on the [[`REQUEST_FINGERPRINTER_CLASS`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-REQUEST_FINGERPRINTER_CLASS){.hoverxref
.tooltip .reference .internal} setting.

You can disable filtering of duplicate requests by setting
[[`DUPEFILTER_CLASS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DUPEFILTER_CLASS){.hoverxref .tooltip
.reference .internal} to
[`'scrapy.dupefilters.BaseDupeFilter'`{.docutils .literal
.notranslate}]{.pre}. Be very careful about this however, because you
can get into crawling loops. It's usually a better idea to set the
[`dont_filter`{.docutils .literal .notranslate}]{.pre} parameter to
[`True`{.docutils .literal .notranslate}]{.pre} on the specific
[`Request`{.xref .py .py-class .docutils .literal .notranslate}]{.pre}
that should not be filtered.
:::

::: {#dupefilter-debug .section}
[]{#std-setting-DUPEFILTER_DEBUG}

##### DUPEFILTER_DEBUG[¶](#dupefilter-debug "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

By default, [`RFPDupeFilter`{.docutils .literal .notranslate}]{.pre}
only logs the first duplicate request. Setting
[[`DUPEFILTER_DEBUG`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DUPEFILTER_DEBUG){.hoverxref .tooltip
.reference .internal} to [`True`{.docutils .literal .notranslate}]{.pre}
will make it log all duplicate requests.
:::

::: {#editor .section}
[]{#std-setting-EDITOR}

##### EDITOR[¶](#editor "Permalink to this heading"){.headerlink}

Default: [`vi`{.docutils .literal .notranslate}]{.pre} (on Unix systems)
or the IDLE editor (on Windows)

The editor to use for editing spiders with the [[`edit`{.xref .std
.std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-edit){.hoverxref .tooltip
.reference .internal} command. Additionally, if the [`EDITOR`{.docutils
.literal .notranslate}]{.pre} environment variable is set, the
[[`edit`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-edit){.hoverxref .tooltip
.reference .internal} command will prefer it over the default setting.
:::

::: {#extensions .section}
[]{#std-setting-EXTENSIONS}

##### EXTENSIONS[¶](#extensions "Permalink to this heading"){.headerlink}

Default:: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing the extensions enabled in your project, and their
orders.
:::

::: {#extensions-base .section}
[]{#std-setting-EXTENSIONS_BASE}

##### EXTENSIONS_BASE[¶](#extensions-base "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "scrapy.extensions.corestats.CoreStats": 0,
        "scrapy.extensions.telnet.TelnetConsole": 0,
        "scrapy.extensions.memusage.MemoryUsage": 0,
        "scrapy.extensions.memdebug.MemoryDebugger": 0,
        "scrapy.extensions.closespider.CloseSpider": 0,
        "scrapy.extensions.feedexport.FeedExporter": 0,
        "scrapy.extensions.logstats.LogStats": 0,
        "scrapy.extensions.spiderstate.SpiderState": 0,
        "scrapy.extensions.throttle.AutoThrottle": 0,
    }
:::
:::

A dict containing the extensions available by default in Scrapy, and
their orders. This setting contains all stable built-in extensions. Keep
in mind that some of them need to be enabled through a setting.

For more information See the [[extensions user guide]{.std
.std-ref}](index.html#topics-extensions){.hoverxref .tooltip .reference
.internal} and the [[list of available extensions]{.std
.std-ref}](index.html#topics-extensions-ref){.hoverxref .tooltip
.reference .internal}.
:::

::: {#feed-tempdir .section}
[]{#std-setting-FEED_TEMPDIR}

##### FEED_TEMPDIR[¶](#feed-tempdir "Permalink to this heading"){.headerlink}

The Feed Temp dir allows you to set a custom folder to save crawler
temporary files before uploading with [[FTP feed storage]{.std
.std-ref}](index.html#topics-feed-storage-ftp){.hoverxref .tooltip
.reference .internal} and [[Amazon S3]{.std
.std-ref}](index.html#topics-feed-storage-s3){.hoverxref .tooltip
.reference .internal}.
:::

::: {#feed-storage-gcs-acl .section}
[]{#std-setting-FEED_STORAGE_GCS_ACL}

##### FEED_STORAGE_GCS_ACL[¶](#feed-storage-gcs-acl "Permalink to this heading"){.headerlink}

The Access Control List (ACL) used when storing items to [[Google Cloud
Storage]{.std .std-ref}](index.html#topics-feed-storage-gcs){.hoverxref
.tooltip .reference .internal}. For more information on how to set this
value, please refer to the column *JSON API* in [Google Cloud
documentation](https://cloud.google.com/storage/docs/access-control/lists){.reference
.external}.
:::

::: {#ftp-passive-mode .section}
[]{#std-setting-FTP_PASSIVE_MODE}

##### FTP_PASSIVE_MODE[¶](#ftp-passive-mode "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether or not to use passive mode when initiating FTP transfers.

[]{#std-reqmeta-ftp_password .target}
:::

::: {#ftp-password .section}
[]{#std-setting-FTP_PASSWORD}

##### FTP_PASSWORD[¶](#ftp-password "Permalink to this heading"){.headerlink}

Default: [`"guest"`{.docutils .literal .notranslate}]{.pre}

The password to use for FTP connections when there is no
[`"ftp_password"`{.docutils .literal .notranslate}]{.pre} in
[`Request`{.docutils .literal .notranslate}]{.pre} meta.

::: {.admonition .note}
Note

Paraphrasing [RFC 1635](https://tools.ietf.org/html/rfc1635){.reference
.external}, although it is common to use either the password "guest" or
one's e-mail address for anonymous FTP, some FTP servers explicitly ask
for the user's e-mail address and will not allow login with the "guest"
password.
:::

[]{#std-reqmeta-ftp_user .target}
:::

::: {#ftp-user .section}
[]{#std-setting-FTP_USER}

##### FTP_USER[¶](#ftp-user "Permalink to this heading"){.headerlink}

Default: [`"anonymous"`{.docutils .literal .notranslate}]{.pre}

The username to use for FTP connections when there is no
[`"ftp_user"`{.docutils .literal .notranslate}]{.pre} in
[`Request`{.docutils .literal .notranslate}]{.pre} meta.
:::

::: {#gcs-project-id .section}
[]{#std-setting-GCS_PROJECT_ID}

##### GCS_PROJECT_ID[¶](#gcs-project-id "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The Project ID that will be used when storing data on [Google Cloud
Storage](https://cloud.google.com/storage/){.reference .external}.
:::

::: {#item-pipelines .section}
[]{#std-setting-ITEM_PIPELINES}

##### ITEM_PIPELINES[¶](#item-pipelines "Permalink to this heading"){.headerlink}

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing the item pipelines to use, and their orders. Order
values are arbitrary, but it is customary to define them in the 0-1000
range. Lower orders process before higher orders.

Example:

::: {.highlight-python .notranslate}
::: highlight
    ITEM_PIPELINES = {
        "mybot.pipelines.validate.ValidateMyItem": 300,
        "mybot.pipelines.validate.StoreMyItem": 800,
    }
:::
:::
:::

::: {#item-pipelines-base .section}
[]{#std-setting-ITEM_PIPELINES_BASE}

##### ITEM_PIPELINES_BASE[¶](#item-pipelines-base "Permalink to this heading"){.headerlink}

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing the pipelines enabled by default in Scrapy. You should
never modify this setting in your project, modify
[[`ITEM_PIPELINES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-ITEM_PIPELINES){.hoverxref .tooltip
.reference .internal} instead.
:::

::: {#jobdir .section}
[]{#std-setting-JOBDIR}

##### JOBDIR[¶](#jobdir "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

A string indicating the directory for storing the state of a crawl when
[[pausing and resuming crawls]{.std
.std-ref}](index.html#topics-jobs){.hoverxref .tooltip .reference
.internal}.
:::

::: {#log-enabled .section}
[]{#std-setting-LOG_ENABLED}

##### LOG_ENABLED[¶](#log-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether to enable logging.
:::

::: {#log-encoding .section}
[]{#std-setting-LOG_ENCODING}

##### LOG_ENCODING[¶](#log-encoding "Permalink to this heading"){.headerlink}

Default: [`'utf-8'`{.docutils .literal .notranslate}]{.pre}

The encoding to use for logging.
:::

::: {#log-file .section}
[]{#std-setting-LOG_FILE}

##### LOG_FILE[¶](#log-file "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

File name to use for logging output. If [`None`{.docutils .literal
.notranslate}]{.pre}, standard error will be used.
:::

::: {#log-file-append .section}
[]{#std-setting-LOG_FILE_APPEND}

##### LOG_FILE_APPEND[¶](#log-file-append "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

If [`False`{.docutils .literal .notranslate}]{.pre}, the log file
specified with [[`LOG_FILE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-LOG_FILE){.hoverxref .tooltip
.reference .internal} will be overwritten (discarding the output from
previous runs, if any).
:::

::: {#log-format .section}
[]{#std-setting-LOG_FORMAT}

##### LOG_FORMAT[¶](#log-format "Permalink to this heading"){.headerlink}

Default: [`'%(asctime)s`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`[%(name)s]`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`%(levelname)s:`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`%(message)s'`{.docutils .literal .notranslate}]{.pre}

String for formatting log messages. Refer to the [[Python logging
documentation]{.xref .std
.std-ref}](https://docs.python.org/3/library/logging.html#logrecord-attributes "(in Python v3.12)"){.reference
.external} for the whole list of available placeholders.
:::

::: {#log-dateformat .section}
[]{#std-setting-LOG_DATEFORMAT}

##### LOG_DATEFORMAT[¶](#log-dateformat "Permalink to this heading"){.headerlink}

Default: [`'%Y-%m-%d`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`%H:%M:%S'`{.docutils .literal .notranslate}]{.pre}

String for formatting date/time, expansion of the
[`%(asctime)s`{.docutils .literal .notranslate}]{.pre} placeholder in
[[`LOG_FORMAT`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-LOG_FORMAT){.hoverxref .tooltip
.reference .internal}. Refer to the [[Python datetime
documentation]{.xref .std
.std-ref}](https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior "(in Python v3.12)"){.reference
.external} for the whole list of available directives.
:::

::: {#log-formatter .section}
[]{#std-setting-LOG_FORMATTER}

##### LOG_FORMATTER[¶](#log-formatter "Permalink to this heading"){.headerlink}

Default: [[`scrapy.logformatter.LogFormatter`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.logformatter.LogFormatter "scrapy.logformatter.LogFormatter"){.reference
.internal}

The class to use for [[formatting log messages]{.std
.std-ref}](index.html#custom-log-formats){.hoverxref .tooltip .reference
.internal} for different actions.
:::

::: {#log-level .section}
[]{#std-setting-LOG_LEVEL}

##### LOG_LEVEL[¶](#log-level "Permalink to this heading"){.headerlink}

Default: [`'DEBUG'`{.docutils .literal .notranslate}]{.pre}

Minimum level to log. Available levels are: CRITICAL, ERROR, WARNING,
INFO, DEBUG. For more info see [[Logging]{.std
.std-ref}](index.html#topics-logging){.hoverxref .tooltip .reference
.internal}.
:::

::: {#log-stdout .section}
[]{#std-setting-LOG_STDOUT}

##### LOG_STDOUT[¶](#log-stdout "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

If [`True`{.docutils .literal .notranslate}]{.pre}, all standard output
(and error) of your process will be redirected to the log. For example
if you [`print('hello')`{.docutils .literal .notranslate}]{.pre} it will
appear in the Scrapy log.
:::

::: {#log-short-names .section}
[]{#std-setting-LOG_SHORT_NAMES}

##### LOG_SHORT_NAMES[¶](#log-short-names "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

If [`True`{.docutils .literal .notranslate}]{.pre}, the logs will just
contain the root path. If it is set to [`False`{.docutils .literal
.notranslate}]{.pre} then it displays the component responsible for the
log output
:::

::: {#logstats-interval .section}
[]{#std-setting-LOGSTATS_INTERVAL}

##### LOGSTATS_INTERVAL[¶](#logstats-interval "Permalink to this heading"){.headerlink}

Default: [`60.0`{.docutils .literal .notranslate}]{.pre}

The interval (in seconds) between each logging printout of the stats by
[[`LogStats`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.extensions.logstats.LogStats "scrapy.extensions.logstats.LogStats"){.reference
.internal}.
:::

::: {#memdebug-enabled .section}
[]{#std-setting-MEMDEBUG_ENABLED}

##### MEMDEBUG_ENABLED[¶](#memdebug-enabled "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Whether to enable memory debugging.
:::

::: {#memdebug-notify .section}
[]{#std-setting-MEMDEBUG_NOTIFY}

##### MEMDEBUG_NOTIFY[¶](#memdebug-notify "Permalink to this heading"){.headerlink}

Default: [`[]`{.docutils .literal .notranslate}]{.pre}

When memory debugging is enabled a memory report will be sent to the
specified addresses if this setting is not empty, otherwise the report
will be written to the log.

Example:

::: {.highlight-python .notranslate}
::: highlight
    MEMDEBUG_NOTIFY = ['user@example.com']
:::
:::
:::

::: {#memusage-enabled .section}
[]{#std-setting-MEMUSAGE_ENABLED}

##### MEMUSAGE_ENABLED[¶](#memusage-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.extensions.memusage`{.docutils .literal
.notranslate}]{.pre}

Whether to enable the memory usage extension. This extension keeps track
of a peak memory used by the process (it writes it to stats). It can
also optionally shutdown the Scrapy process when it exceeds a memory
limit (see [[`MEMUSAGE_LIMIT_MB`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-MEMUSAGE_LIMIT_MB){.hoverxref
.tooltip .reference .internal}), and notify by email when that happened
(see [[`MEMUSAGE_NOTIFY_MAIL`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-MEMUSAGE_NOTIFY_MAIL){.hoverxref
.tooltip .reference .internal}).

See [[Memory usage extension]{.std
.std-ref}](index.html#topics-extensions-ref-memusage){.hoverxref
.tooltip .reference .internal}.
:::

::: {#memusage-limit-mb .section}
[]{#std-setting-MEMUSAGE_LIMIT_MB}

##### MEMUSAGE_LIMIT_MB[¶](#memusage-limit-mb "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.extensions.memusage`{.docutils .literal
.notranslate}]{.pre}

The maximum amount of memory to allow (in megabytes) before shutting
down Scrapy (if MEMUSAGE_ENABLED is True). If zero, no check will be
performed.

See [[Memory usage extension]{.std
.std-ref}](index.html#topics-extensions-ref-memusage){.hoverxref
.tooltip .reference .internal}.
:::

::: {#memusage-check-interval-seconds .section}
[]{#std-setting-MEMUSAGE_CHECK_INTERVAL_SECONDS}

##### MEMUSAGE_CHECK_INTERVAL_SECONDS[¶](#memusage-check-interval-seconds "Permalink to this heading"){.headerlink}

Default: [`60.0`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.extensions.memusage`{.docutils .literal
.notranslate}]{.pre}

The [[Memory usage extension]{.std
.std-ref}](index.html#topics-extensions-ref-memusage){.hoverxref
.tooltip .reference .internal} checks the current memory usage, versus
the limits set by [[`MEMUSAGE_LIMIT_MB`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-MEMUSAGE_LIMIT_MB){.hoverxref
.tooltip .reference .internal} and [[`MEMUSAGE_WARNING_MB`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-MEMUSAGE_WARNING_MB){.hoverxref
.tooltip .reference .internal}, at fixed time intervals.

This sets the length of these intervals, in seconds.

See [[Memory usage extension]{.std
.std-ref}](index.html#topics-extensions-ref-memusage){.hoverxref
.tooltip .reference .internal}.
:::

::: {#memusage-notify-mail .section}
[]{#std-setting-MEMUSAGE_NOTIFY_MAIL}

##### MEMUSAGE_NOTIFY_MAIL[¶](#memusage-notify-mail "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.extensions.memusage`{.docutils .literal
.notranslate}]{.pre}

A list of emails to notify if the memory limit has been reached.

Example:

::: {.highlight-python .notranslate}
::: highlight
    MEMUSAGE_NOTIFY_MAIL = ['user@example.com']
:::
:::

See [[Memory usage extension]{.std
.std-ref}](index.html#topics-extensions-ref-memusage){.hoverxref
.tooltip .reference .internal}.
:::

::: {#memusage-warning-mb .section}
[]{#std-setting-MEMUSAGE_WARNING_MB}

##### MEMUSAGE_WARNING_MB[¶](#memusage-warning-mb "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.extensions.memusage`{.docutils .literal
.notranslate}]{.pre}

The maximum amount of memory to allow (in megabytes) before sending a
warning email notifying about it. If zero, no warning will be produced.
:::

::: {#newspider-module .section}
[]{#std-setting-NEWSPIDER_MODULE}

##### NEWSPIDER_MODULE[¶](#newspider-module "Permalink to this heading"){.headerlink}

Default: [`''`{.docutils .literal .notranslate}]{.pre}

Module where to create new spiders using the [[`genspider`{.xref .std
.std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-genspider){.hoverxref
.tooltip .reference .internal} command.

Example:

::: {.highlight-python .notranslate}
::: highlight
    NEWSPIDER_MODULE = 'mybot.spiders_dev'
:::
:::
:::

::: {#randomize-download-delay .section}
[]{#std-setting-RANDOMIZE_DOWNLOAD_DELAY}

##### RANDOMIZE_DOWNLOAD_DELAY[¶](#randomize-download-delay "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

If enabled, Scrapy will wait a random amount of time (between 0.5 \*
[[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal} and 1.5 \* [[`DOWNLOAD_DELAY`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal}) while fetching requests from the same website.

This randomization decreases the chance of the crawler being detected
(and subsequently blocked) by sites which analyze requests looking for
statistically significant similarities in the time between their
requests.

The randomization policy is the same used by
[wget](https://www.gnu.org/software/wget/manual/wget.html){.reference
.external} [`--random-wait`{.docutils .literal .notranslate}]{.pre}
option.

If [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal} is zero (default) this option has no effect.
:::

::: {#reactor-threadpool-maxsize .section}
[]{#std-setting-REACTOR_THREADPOOL_MAXSIZE}

##### REACTOR_THREADPOOL_MAXSIZE[¶](#reactor-threadpool-maxsize "Permalink to this heading"){.headerlink}

Default: [`10`{.docutils .literal .notranslate}]{.pre}

The maximum limit for Twisted Reactor thread pool size. This is common
multi-purpose thread pool used by various Scrapy components. Threaded
DNS Resolver, BlockingFeedStorage, S3FilesStore just to name a few.
Increase this value if you're experiencing problems with insufficient
blocking IO.
:::

::: {#redirect-priority-adjust .section}
[]{#std-setting-REDIRECT_PRIORITY_ADJUST}

##### REDIRECT_PRIORITY_ADJUST[¶](#redirect-priority-adjust "Permalink to this heading"){.headerlink}

Default: [`+2`{.docutils .literal .notranslate}]{.pre}

Scope:
[`scrapy.downloadermiddlewares.redirect.RedirectMiddleware`{.docutils
.literal .notranslate}]{.pre}

Adjust redirect request priority relative to original request:

-   **a positive priority adjust (default) means higher priority.**

-   a negative priority adjust means lower priority.
:::

::: {#robotstxt-obey .section}
[]{#std-setting-ROBOTSTXT_OBEY}

##### ROBOTSTXT_OBEY[¶](#robotstxt-obey "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.downloadermiddlewares.robotstxt`{.docutils .literal
.notranslate}]{.pre}

If enabled, Scrapy will respect robots.txt policies. For more
information see [[RobotsTxtMiddleware]{.std
.std-ref}](index.html#topics-dlmw-robots){.hoverxref .tooltip .reference
.internal}.

::: {.admonition .note}
Note

While the default value is [`False`{.docutils .literal
.notranslate}]{.pre} for historical reasons, this option is enabled by
default in settings.py file generated by [`scrapy`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`startproject`{.docutils .literal .notranslate}]{.pre}
command.
:::
:::

::: {#robotstxt-parser .section}
[]{#std-setting-ROBOTSTXT_PARSER}

##### ROBOTSTXT_PARSER[¶](#robotstxt-parser "Permalink to this heading"){.headerlink}

Default: [`'scrapy.robotstxt.ProtegoRobotParser'`{.docutils .literal
.notranslate}]{.pre}

The parser backend to use for parsing [`robots.txt`{.docutils .literal
.notranslate}]{.pre} files. For more information see
[[RobotsTxtMiddleware]{.std
.std-ref}](index.html#topics-dlmw-robots){.hoverxref .tooltip .reference
.internal}.

::: {#robotstxt-user-agent .section}
[]{#std-setting-ROBOTSTXT_USER_AGENT}

###### ROBOTSTXT_USER_AGENT[¶](#robotstxt-user-agent "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The user agent string to use for matching in the robots.txt file. If
[`None`{.docutils .literal .notranslate}]{.pre}, the User-Agent header
you are sending with the request or the [[`USER_AGENT`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-USER_AGENT){.hoverxref .tooltip
.reference .internal} setting (in that order) will be used for
determining the user agent to use in the robots.txt file.
:::
:::

::: {#scheduler .section}
[]{#std-setting-SCHEDULER}

##### SCHEDULER[¶](#scheduler "Permalink to this heading"){.headerlink}

Default: [`'scrapy.core.scheduler.Scheduler'`{.docutils .literal
.notranslate}]{.pre}

The scheduler class to be used for crawling. See the [[Scheduler]{.std
.std-ref}](index.html#topics-scheduler){.hoverxref .tooltip .reference
.internal} topic for details.
:::

::: {#scheduler-debug .section}
[]{#std-setting-SCHEDULER_DEBUG}

##### SCHEDULER_DEBUG[¶](#scheduler-debug "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Setting to [`True`{.docutils .literal .notranslate}]{.pre} will log
debug information about the requests scheduler. This currently logs
(only once) if the requests cannot be serialized to disk. Stats counter
([`scheduler/unserializable`{.docutils .literal .notranslate}]{.pre})
tracks the number of times this happens.

Example entry in logs:

::: {.highlight-python .notranslate}
::: highlight
    1956-01-31 00:00:00+0800 [scrapy.core.scheduler] ERROR: Unable to serialize request:
    <GET http://example.com> - reason: cannot serialize <Request at 0x9a7c7ec>
    (type Request)> - no more unserializable requests will be logged
    (see 'scheduler/unserializable' stats counter)
:::
:::
:::

::: {#scheduler-disk-queue .section}
[]{#std-setting-SCHEDULER_DISK_QUEUE}

##### SCHEDULER_DISK_QUEUE[¶](#scheduler-disk-queue "Permalink to this heading"){.headerlink}

Default: [`'scrapy.squeues.PickleLifoDiskQueue'`{.docutils .literal
.notranslate}]{.pre}

Type of disk queue that will be used by scheduler. Other available types
are [`scrapy.squeues.PickleFifoDiskQueue`{.docutils .literal
.notranslate}]{.pre}, [`scrapy.squeues.MarshalFifoDiskQueue`{.docutils
.literal .notranslate}]{.pre},
[`scrapy.squeues.MarshalLifoDiskQueue`{.docutils .literal
.notranslate}]{.pre}.
:::

::: {#scheduler-memory-queue .section}
[]{#std-setting-SCHEDULER_MEMORY_QUEUE}

##### SCHEDULER_MEMORY_QUEUE[¶](#scheduler-memory-queue "Permalink to this heading"){.headerlink}

Default: [`'scrapy.squeues.LifoMemoryQueue'`{.docutils .literal
.notranslate}]{.pre}

Type of in-memory queue used by scheduler. Other available type is:
[`scrapy.squeues.FifoMemoryQueue`{.docutils .literal
.notranslate}]{.pre}.
:::

::: {#scheduler-priority-queue .section}
[]{#std-setting-SCHEDULER_PRIORITY_QUEUE}

##### SCHEDULER_PRIORITY_QUEUE[¶](#scheduler-priority-queue "Permalink to this heading"){.headerlink}

Default: [`'scrapy.pqueues.ScrapyPriorityQueue'`{.docutils .literal
.notranslate}]{.pre}

Type of priority queue used by the scheduler. Another available type is
[`scrapy.pqueues.DownloaderAwarePriorityQueue`{.docutils .literal
.notranslate}]{.pre}.
[`scrapy.pqueues.DownloaderAwarePriorityQueue`{.docutils .literal
.notranslate}]{.pre} works better than
[`scrapy.pqueues.ScrapyPriorityQueue`{.docutils .literal
.notranslate}]{.pre} when you crawl many different domains in parallel.
But currently [`scrapy.pqueues.DownloaderAwarePriorityQueue`{.docutils
.literal .notranslate}]{.pre} does not work together with
[[`CONCURRENT_REQUESTS_PER_IP`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal}.
:::

::: {#scraper-slot-max-active-size .section}
[]{#std-setting-SCRAPER_SLOT_MAX_ACTIVE_SIZE}

##### SCRAPER_SLOT_MAX_ACTIVE_SIZE[¶](#scraper-slot-max-active-size "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.0.]{.versionmodified .added}
:::

Default: [`5_000_000`{.docutils .literal .notranslate}]{.pre}

Soft limit (in bytes) for response data being processed.

While the sum of the sizes of all responses being processed is above
this value, Scrapy does not process new requests.
:::

::: {#spider-contracts .section}
[]{#std-setting-SPIDER_CONTRACTS}

##### SPIDER_CONTRACTS[¶](#spider-contracts "Permalink to this heading"){.headerlink}

Default:: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing the spider contracts enabled in your project, used for
testing spiders. For more info see [[Spiders Contracts]{.std
.std-ref}](index.html#topics-contracts){.hoverxref .tooltip .reference
.internal}.
:::

::: {#spider-contracts-base .section}
[]{#std-setting-SPIDER_CONTRACTS_BASE}

##### SPIDER_CONTRACTS_BASE[¶](#spider-contracts-base "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "scrapy.contracts.default.UrlContract": 1,
        "scrapy.contracts.default.ReturnsContract": 2,
        "scrapy.contracts.default.ScrapesContract": 3,
    }
:::
:::

A dict containing the Scrapy contracts enabled by default in Scrapy. You
should never modify this setting in your project, modify
[[`SPIDER_CONTRACTS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-SPIDER_CONTRACTS){.hoverxref .tooltip
.reference .internal} instead. For more info see [[Spiders
Contracts]{.std .std-ref}](index.html#topics-contracts){.hoverxref
.tooltip .reference .internal}.

You can disable any of these contracts by assigning [`None`{.docutils
.literal .notranslate}]{.pre} to their class path in
[[`SPIDER_CONTRACTS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-SPIDER_CONTRACTS){.hoverxref .tooltip
.reference .internal}. E.g., to disable the built-in
[`ScrapesContract`{.docutils .literal .notranslate}]{.pre}, place this
in your [`settings.py`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    SPIDER_CONTRACTS = {
        "scrapy.contracts.default.ScrapesContract": None,
    }
:::
:::
:::

::: {#spider-loader-class .section}
[]{#std-setting-SPIDER_LOADER_CLASS}

##### SPIDER_LOADER_CLASS[¶](#spider-loader-class "Permalink to this heading"){.headerlink}

Default: [`'scrapy.spiderloader.SpiderLoader'`{.docutils .literal
.notranslate}]{.pre}

The class that will be used for loading spiders, which must implement
the [[SpiderLoader API]{.std
.std-ref}](index.html#topics-api-spiderloader){.hoverxref .tooltip
.reference .internal}.
:::

::: {#spider-loader-warn-only .section}
[]{#std-setting-SPIDER_LOADER_WARN_ONLY}

##### SPIDER_LOADER_WARN_ONLY[¶](#spider-loader-warn-only "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

By default, when Scrapy tries to import spider classes from
[[`SPIDER_MODULES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-SPIDER_MODULES){.hoverxref .tooltip
.reference .internal}, it will fail loudly if there is any
[`ImportError`{.docutils .literal .notranslate}]{.pre} exception. But
you can choose to silence this exception and turn it into a simple
warning by setting [`SPIDER_LOADER_WARN_ONLY`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal .notranslate}[`=`{.docutils
.literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`True`{.docutils .literal .notranslate}]{.pre}.

::: {.admonition .note}
Note

Some [[scrapy commands]{.std
.std-ref}](index.html#topics-commands){.hoverxref .tooltip .reference
.internal} run with this setting to [`True`{.docutils .literal
.notranslate}]{.pre} already (i.e. they will only issue a warning and
will not fail) since they do not actually need to load spider classes to
work: [[`scrapy`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}` `{.xref .std .std-command .docutils .literal
.notranslate}[`runspider`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
.tooltip .reference .internal}, [[`scrapy`{.xref .std .std-command
.docutils .literal .notranslate}]{.pre}` `{.xref .std .std-command
.docutils .literal .notranslate}[`settings`{.xref .std .std-command
.docutils .literal
.notranslate}]{.pre}](index.html#std-command-settings){.hoverxref
.tooltip .reference .internal}, [[`scrapy`{.xref .std .std-command
.docutils .literal .notranslate}]{.pre}` `{.xref .std .std-command
.docutils .literal .notranslate}[`startproject`{.xref .std .std-command
.docutils .literal
.notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
.tooltip .reference .internal}, [[`scrapy`{.xref .std .std-command
.docutils .literal .notranslate}]{.pre}` `{.xref .std .std-command
.docutils .literal .notranslate}[`version`{.xref .std .std-command
.docutils .literal
.notranslate}]{.pre}](index.html#std-command-version){.hoverxref
.tooltip .reference .internal}.
:::
:::

::: {#spider-middlewares .section}
[]{#std-setting-SPIDER_MIDDLEWARES}

##### SPIDER_MIDDLEWARES[¶](#spider-middlewares "Permalink to this heading"){.headerlink}

Default:: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing the spider middlewares enabled in your project, and
their orders. For more info see [[Activating a spider middleware]{.std
.std-ref}](index.html#topics-spider-middleware-setting){.hoverxref
.tooltip .reference .internal}.
:::

::: {#spider-middlewares-base .section}
[]{#std-setting-SPIDER_MIDDLEWARES_BASE}

##### SPIDER_MIDDLEWARES_BASE[¶](#spider-middlewares-base "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "scrapy.spidermiddlewares.httperror.HttpErrorMiddleware": 50,
        "scrapy.spidermiddlewares.offsite.OffsiteMiddleware": 500,
        "scrapy.spidermiddlewares.referer.RefererMiddleware": 700,
        "scrapy.spidermiddlewares.urllength.UrlLengthMiddleware": 800,
        "scrapy.spidermiddlewares.depth.DepthMiddleware": 900,
    }
:::
:::

A dict containing the spider middlewares enabled by default in Scrapy,
and their orders. Low orders are closer to the engine, high orders are
closer to the spider. For more info see [[Activating a spider
middleware]{.std
.std-ref}](index.html#topics-spider-middleware-setting){.hoverxref
.tooltip .reference .internal}.
:::

::: {#spider-modules .section}
[]{#std-setting-SPIDER_MODULES}

##### SPIDER_MODULES[¶](#spider-modules "Permalink to this heading"){.headerlink}

Default: [`[]`{.docutils .literal .notranslate}]{.pre}

A list of modules where Scrapy will look for spiders.

Example:

::: {.highlight-python .notranslate}
::: highlight
    SPIDER_MODULES = ["mybot.spiders_prod", "mybot.spiders_dev"]
:::
:::
:::

::: {#stats-class .section}
[]{#std-setting-STATS_CLASS}

##### STATS_CLASS[¶](#stats-class "Permalink to this heading"){.headerlink}

Default: [`'scrapy.statscollectors.MemoryStatsCollector'`{.docutils
.literal .notranslate}]{.pre}

The class to use for collecting stats, who must implement the [[Stats
Collector API]{.std .std-ref}](index.html#topics-api-stats){.hoverxref
.tooltip .reference .internal}.
:::

::: {#stats-dump .section}
[]{#std-setting-STATS_DUMP}

##### STATS_DUMP[¶](#stats-dump "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Dump the [[Scrapy stats]{.std
.std-ref}](index.html#topics-stats){.hoverxref .tooltip .reference
.internal} (to the Scrapy log) once the spider finishes.

For more info see: [[Stats Collection]{.std
.std-ref}](index.html#topics-stats){.hoverxref .tooltip .reference
.internal}.
:::

::: {#statsmailer-rcpts .section}
[]{#std-setting-STATSMAILER_RCPTS}

##### STATSMAILER_RCPTS[¶](#statsmailer-rcpts "Permalink to this heading"){.headerlink}

Default: [`[]`{.docutils .literal .notranslate}]{.pre} (empty list)

Send Scrapy stats after spiders finish scraping. See
[[`StatsMailer`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.extensions.statsmailer.StatsMailer "scrapy.extensions.statsmailer.StatsMailer"){.reference
.internal} for more info.
:::

::: {#telnetconsole-enabled .section}
[]{#std-setting-TELNETCONSOLE_ENABLED}

##### TELNETCONSOLE_ENABLED[¶](#telnetconsole-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

A boolean which specifies if the [[telnet console]{.std
.std-ref}](index.html#topics-telnetconsole){.hoverxref .tooltip
.reference .internal} will be enabled (provided its extension is also
enabled).
:::

::: {#templates-dir .section}
[]{#std-setting-TEMPLATES_DIR}

##### TEMPLATES_DIR[¶](#templates-dir "Permalink to this heading"){.headerlink}

Default: [`templates`{.docutils .literal .notranslate}]{.pre} dir inside
scrapy module

The directory where to look for templates when creating new projects
with [[`startproject`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
.tooltip .reference .internal} command and new spiders with
[[`genspider`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-genspider){.hoverxref
.tooltip .reference .internal} command.

The project name must not conflict with the name of custom files or
directories in the [`project`{.docutils .literal .notranslate}]{.pre}
subdirectory.
:::

::: {#twisted-reactor .section}
[]{#std-setting-TWISTED_REACTOR}

##### TWISTED_REACTOR[¶](#twisted-reactor "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.0.]{.versionmodified .added}
:::

Default: [`None`{.docutils .literal .notranslate}]{.pre}

Import path of a given [[`reactor`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
.external}.

Scrapy will install this reactor if no other reactor is installed yet,
such as when the [`scrapy`{.docutils .literal .notranslate}]{.pre} CLI
program is invoked or when using the [[`CrawlerProcess`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
.internal} class.

If you are using the [[`CrawlerRunner`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
.internal} class, you also need to install the correct reactor manually.
You can do that using [[`install_reactor()`{.xref .py .py-func .docutils
.literal
.notranslate}]{.pre}](#scrapy.utils.reactor.install_reactor "scrapy.utils.reactor.install_reactor"){.reference
.internal}:

[[scrapy.utils.reactor.]{.pre}]{.sig-prename .descclassname}[[install_reactor]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[reactor_path]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[event_loop_path]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/reactor.html#install_reactor){.reference .internal}[¶](#scrapy.utils.reactor.install_reactor "Permalink to this definition"){.headerlink}

:   Installs the [[`reactor`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
    .external} with the specified import path. Also installs the asyncio
    event loop with the specified import path if the asyncio reactor is
    enabled

If a reactor is already installed, [[`install_reactor()`{.xref .py
.py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.reactor.install_reactor "scrapy.utils.reactor.install_reactor"){.reference
.internal} has no effect.

[`CrawlerRunner.__init__`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre} raises [[`Exception`{.xref .py .py-exc .docutils
.literal
.notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#Exception "(in Python v3.12)"){.reference
.external} if the installed reactor does not match the
[[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-TWISTED_REACTOR){.hoverxref .tooltip
.reference .internal} setting; therefore, having top-level
[[`reactor`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
.external} imports in project files and imported third-party libraries
will make Scrapy raise [[`Exception`{.xref .py .py-exc .docutils
.literal
.notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#Exception "(in Python v3.12)"){.reference
.external} when it checks which reactor is installed.

In order to use the reactor installed by Scrapy:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from twisted.internet import reactor


    class QuotesSpider(scrapy.Spider):
        name = "quotes"

        def __init__(self, *args, **kwargs):
            self.timeout = int(kwargs.pop("timeout", "60"))
            super(QuotesSpider, self).__init__(*args, **kwargs)

        def start_requests(self):
            reactor.callLater(self.timeout, self.stop)

            urls = ["https://quotes.toscrape.com/page/1"]
            for url in urls:
                yield scrapy.Request(url=url, callback=self.parse)

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {"text": quote.css("span.text::text").get()}

        def stop(self):
            self.crawler.engine.close_spider(self, "timeout")
:::
:::

which raises [[`Exception`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#Exception "(in Python v3.12)"){.reference
.external}, becomes:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class QuotesSpider(scrapy.Spider):
        name = "quotes"

        def __init__(self, *args, **kwargs):
            self.timeout = int(kwargs.pop("timeout", "60"))
            super(QuotesSpider, self).__init__(*args, **kwargs)

        def start_requests(self):
            from twisted.internet import reactor

            reactor.callLater(self.timeout, self.stop)

            urls = ["https://quotes.toscrape.com/page/1"]
            for url in urls:
                yield scrapy.Request(url=url, callback=self.parse)

        def parse(self, response):
            for quote in response.css("div.quote"):
                yield {"text": quote.css("span.text::text").get()}

        def stop(self):
            self.crawler.engine.close_spider(self, "timeout")
:::
:::

The default value of the [[`TWISTED_REACTOR`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-TWISTED_REACTOR){.hoverxref .tooltip
.reference .internal} setting is [`None`{.docutils .literal
.notranslate}]{.pre}, which means that Scrapy will use the existing
reactor if one is already installed, or install the default reactor
defined by Twisted for the current platform. This is to maintain
backward compatibility and avoid possible problems caused by using a
non-default reactor.

::: versionchanged
[Changed in version 2.7: ]{.versionmodified .changed}The
[[`startproject`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
.tooltip .reference .internal} command now sets this setting to
[`twisted.internet.asyncioreactor.AsyncioSelectorReactor`{.docutils
.literal .notranslate}]{.pre} in the generated [`settings.py`{.docutils
.literal .notranslate}]{.pre} file.
:::

For additional information, see [Choosing a Reactor and GUI Toolkit
Integration](https://docs.twisted.org/en/stable/core/howto/choosing-reactor.html "(in Twisted v23.10)"){.reference
.external}.
:::

::: {#urllength-limit .section}
[]{#std-setting-URLLENGTH_LIMIT}

##### URLLENGTH_LIMIT[¶](#urllength-limit "Permalink to this heading"){.headerlink}

Default: [`2083`{.docutils .literal .notranslate}]{.pre}

Scope: [`spidermiddlewares.urllength`{.docutils .literal
.notranslate}]{.pre}

The maximum URL length to allow for crawled URLs.

This setting can act as a stopping condition in case of URLs of
ever-increasing length, which may be caused for example by a programming
error either in the target server or in your code. See also
[[`REDIRECT_MAX_TIMES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-REDIRECT_MAX_TIMES){.hoverxref
.tooltip .reference .internal} and [[`DEPTH_LIMIT`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DEPTH_LIMIT){.hoverxref .tooltip
.reference .internal}.

Use [`0`{.docutils .literal .notranslate}]{.pre} to allow URLs of any
length.

The default value is copied from the [Microsoft Internet Explorer
maximum URL
length](https://support.microsoft.com/en-us/topic/maximum-url-length-is-2-083-characters-in-internet-explorer-174e7c8a-6666-f4e0-6fd6-908b53c12246){.reference
.external}, even though this setting exists for different reasons.
:::

::: {#user-agent .section}
[]{#std-setting-USER_AGENT}

##### USER_AGENT[¶](#user-agent "Permalink to this heading"){.headerlink}

Default: [`"Scrapy/VERSION`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`(+https://scrapy.org)"`{.docutils .literal
.notranslate}]{.pre}

The default User-Agent to use when crawling, unless overridden. This
user agent is also used by [[`RobotsTxtMiddleware`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware "scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware"){.reference
.internal} if [[`ROBOTSTXT_USER_AGENT`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-ROBOTSTXT_USER_AGENT){.hoverxref
.tooltip .reference .internal} setting is [`None`{.docutils .literal
.notranslate}]{.pre} and there is no overriding User-Agent header
specified for the request.
:::

::: {#settings-documented-elsewhere .section}
##### Settings documented elsewhere:[¶](#settings-documented-elsewhere "Permalink to this heading"){.headerlink}

The following settings are documented elsewhere, please check each
specific case to see how to enable and use them.

-   [ADDONS](index.html#std-setting-ADDONS){.reference .internal}

-   [AJAXCRAWL_ENABLED](index.html#std-setting-AJAXCRAWL_ENABLED){.reference
    .internal}

-   [ASYNCIO_EVENT_LOOP](index.html#std-setting-ASYNCIO_EVENT_LOOP){.reference
    .internal}

-   [AUTOTHROTTLE_DEBUG](index.html#std-setting-AUTOTHROTTLE_DEBUG){.reference
    .internal}

-   [AUTOTHROTTLE_ENABLED](index.html#std-setting-AUTOTHROTTLE_ENABLED){.reference
    .internal}

-   [AUTOTHROTTLE_MAX_DELAY](index.html#std-setting-AUTOTHROTTLE_MAX_DELAY){.reference
    .internal}

-   [AUTOTHROTTLE_START_DELAY](index.html#std-setting-AUTOTHROTTLE_START_DELAY){.reference
    .internal}

-   [AUTOTHROTTLE_TARGET_CONCURRENCY](index.html#std-setting-AUTOTHROTTLE_TARGET_CONCURRENCY){.reference
    .internal}

-   [AWS_ACCESS_KEY_ID](index.html#std-setting-AWS_ACCESS_KEY_ID){.reference
    .internal}

-   [AWS_ENDPOINT_URL](index.html#std-setting-AWS_ENDPOINT_URL){.reference
    .internal}

-   [AWS_REGION_NAME](index.html#std-setting-AWS_REGION_NAME){.reference
    .internal}

-   [AWS_SECRET_ACCESS_KEY](index.html#std-setting-AWS_SECRET_ACCESS_KEY){.reference
    .internal}

-   [AWS_SESSION_TOKEN](index.html#std-setting-AWS_SESSION_TOKEN){.reference
    .internal}

-   [AWS_USE_SSL](index.html#std-setting-AWS_USE_SSL){.reference
    .internal}

-   [AWS_VERIFY](index.html#std-setting-AWS_VERIFY){.reference
    .internal}

-   [BOT_NAME](index.html#std-setting-BOT_NAME){.reference .internal}

-   [CLOSESPIDER_ERRORCOUNT](index.html#std-setting-CLOSESPIDER_ERRORCOUNT){.reference
    .internal}

-   [CLOSESPIDER_ITEMCOUNT](index.html#std-setting-CLOSESPIDER_ITEMCOUNT){.reference
    .internal}

-   [CLOSESPIDER_PAGECOUNT](index.html#std-setting-CLOSESPIDER_PAGECOUNT){.reference
    .internal}

-   [CLOSESPIDER_TIMEOUT](index.html#std-setting-CLOSESPIDER_TIMEOUT){.reference
    .internal}

-   [CLOSESPIDER_TIMEOUT_NO_ITEM](index.html#std-setting-CLOSESPIDER_TIMEOUT_NO_ITEM){.reference
    .internal}

-   [COMMANDS_MODULE](index.html#std-setting-COMMANDS_MODULE){.reference
    .internal}

-   [COMPRESSION_ENABLED](index.html#std-setting-COMPRESSION_ENABLED){.reference
    .internal}

-   [CONCURRENT_ITEMS](index.html#std-setting-CONCURRENT_ITEMS){.reference
    .internal}

-   [CONCURRENT_REQUESTS](index.html#std-setting-CONCURRENT_REQUESTS){.reference
    .internal}

-   [CONCURRENT_REQUESTS_PER_DOMAIN](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.reference
    .internal}

-   [CONCURRENT_REQUESTS_PER_IP](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.reference
    .internal}

-   [COOKIES_DEBUG](index.html#std-setting-COOKIES_DEBUG){.reference
    .internal}

-   [COOKIES_ENABLED](index.html#std-setting-COOKIES_ENABLED){.reference
    .internal}

-   [DEFAULT_ITEM_CLASS](index.html#std-setting-DEFAULT_ITEM_CLASS){.reference
    .internal}

-   [DEFAULT_REQUEST_HEADERS](index.html#std-setting-DEFAULT_REQUEST_HEADERS){.reference
    .internal}

-   [DEPTH_LIMIT](index.html#std-setting-DEPTH_LIMIT){.reference
    .internal}

-   [DEPTH_PRIORITY](index.html#std-setting-DEPTH_PRIORITY){.reference
    .internal}

-   [DEPTH_STATS_VERBOSE](index.html#std-setting-DEPTH_STATS_VERBOSE){.reference
    .internal}

-   [DNSCACHE_ENABLED](index.html#std-setting-DNSCACHE_ENABLED){.reference
    .internal}

-   [DNSCACHE_SIZE](index.html#std-setting-DNSCACHE_SIZE){.reference
    .internal}

-   [DNS_RESOLVER](index.html#std-setting-DNS_RESOLVER){.reference
    .internal}

-   [DNS_TIMEOUT](index.html#std-setting-DNS_TIMEOUT){.reference
    .internal}

-   [DOWNLOADER](index.html#std-setting-DOWNLOADER){.reference
    .internal}

-   [DOWNLOADER_CLIENTCONTEXTFACTORY](index.html#std-setting-DOWNLOADER_CLIENTCONTEXTFACTORY){.reference
    .internal}

-   [DOWNLOADER_CLIENT_TLS_CIPHERS](index.html#std-setting-DOWNLOADER_CLIENT_TLS_CIPHERS){.reference
    .internal}

-   [DOWNLOADER_CLIENT_TLS_METHOD](index.html#std-setting-DOWNLOADER_CLIENT_TLS_METHOD){.reference
    .internal}

-   [DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING](index.html#std-setting-DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING){.reference
    .internal}

-   [DOWNLOADER_HTTPCLIENTFACTORY](index.html#std-setting-DOWNLOADER_HTTPCLIENTFACTORY){.reference
    .internal}

-   [DOWNLOADER_MIDDLEWARES](index.html#std-setting-DOWNLOADER_MIDDLEWARES){.reference
    .internal}

-   [DOWNLOADER_MIDDLEWARES_BASE](index.html#std-setting-DOWNLOADER_MIDDLEWARES_BASE){.reference
    .internal}

-   [DOWNLOADER_STATS](index.html#std-setting-DOWNLOADER_STATS){.reference
    .internal}

-   [DOWNLOAD_DELAY](index.html#std-setting-DOWNLOAD_DELAY){.reference
    .internal}

-   [DOWNLOAD_FAIL_ON_DATALOSS](index.html#std-setting-DOWNLOAD_FAIL_ON_DATALOSS){.reference
    .internal}

-   [DOWNLOAD_HANDLERS](index.html#std-setting-DOWNLOAD_HANDLERS){.reference
    .internal}

-   [DOWNLOAD_HANDLERS_BASE](index.html#std-setting-DOWNLOAD_HANDLERS_BASE){.reference
    .internal}

-   [DOWNLOAD_MAXSIZE](index.html#std-setting-DOWNLOAD_MAXSIZE){.reference
    .internal}

-   [DOWNLOAD_SLOTS](index.html#std-setting-DOWNLOAD_SLOTS){.reference
    .internal}

-   [DOWNLOAD_TIMEOUT](index.html#std-setting-DOWNLOAD_TIMEOUT){.reference
    .internal}

-   [DOWNLOAD_WARNSIZE](index.html#std-setting-DOWNLOAD_WARNSIZE){.reference
    .internal}

-   [DUPEFILTER_CLASS](index.html#std-setting-DUPEFILTER_CLASS){.reference
    .internal}

-   [DUPEFILTER_DEBUG](index.html#std-setting-DUPEFILTER_DEBUG){.reference
    .internal}

-   [EDITOR](index.html#std-setting-EDITOR){.reference .internal}

-   [EXTENSIONS](index.html#std-setting-EXTENSIONS){.reference
    .internal}

-   [EXTENSIONS_BASE](index.html#std-setting-EXTENSIONS_BASE){.reference
    .internal}

-   [FEEDS](index.html#std-setting-FEEDS){.reference .internal}

-   [FEED_EXPORTERS](index.html#std-setting-FEED_EXPORTERS){.reference
    .internal}

-   [FEED_EXPORTERS_BASE](index.html#std-setting-FEED_EXPORTERS_BASE){.reference
    .internal}

-   [FEED_EXPORT_BATCH_ITEM_COUNT](index.html#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.reference
    .internal}

-   [FEED_EXPORT_ENCODING](index.html#std-setting-FEED_EXPORT_ENCODING){.reference
    .internal}

-   [FEED_EXPORT_FIELDS](index.html#std-setting-FEED_EXPORT_FIELDS){.reference
    .internal}

-   [FEED_EXPORT_INDENT](index.html#std-setting-FEED_EXPORT_INDENT){.reference
    .internal}

-   [FEED_STORAGES](index.html#std-setting-FEED_STORAGES){.reference
    .internal}

-   [FEED_STORAGES_BASE](index.html#std-setting-FEED_STORAGES_BASE){.reference
    .internal}

-   [FEED_STORAGE_FTP_ACTIVE](index.html#std-setting-FEED_STORAGE_FTP_ACTIVE){.reference
    .internal}

-   [FEED_STORAGE_GCS_ACL](index.html#std-setting-FEED_STORAGE_GCS_ACL){.reference
    .internal}

-   [FEED_STORAGE_S3_ACL](index.html#std-setting-FEED_STORAGE_S3_ACL){.reference
    .internal}

-   [FEED_STORE_EMPTY](index.html#std-setting-FEED_STORE_EMPTY){.reference
    .internal}

-   [FEED_TEMPDIR](index.html#std-setting-FEED_TEMPDIR){.reference
    .internal}

-   [FEED_URI_PARAMS](index.html#std-setting-FEED_URI_PARAMS){.reference
    .internal}

-   [FILES_EXPIRES](index.html#std-setting-FILES_EXPIRES){.reference
    .internal}

-   [FILES_RESULT_FIELD](index.html#std-setting-FILES_RESULT_FIELD){.reference
    .internal}

-   [FILES_STORE](index.html#std-setting-FILES_STORE){.reference
    .internal}

-   [FILES_STORE_GCS_ACL](index.html#std-setting-FILES_STORE_GCS_ACL){.reference
    .internal}

-   [FILES_STORE_S3_ACL](index.html#std-setting-FILES_STORE_S3_ACL){.reference
    .internal}

-   [FILES_URLS_FIELD](index.html#std-setting-FILES_URLS_FIELD){.reference
    .internal}

-   [FTP_PASSIVE_MODE](index.html#std-setting-FTP_PASSIVE_MODE){.reference
    .internal}

-   [FTP_PASSWORD](index.html#std-setting-FTP_PASSWORD){.reference
    .internal}

-   [FTP_USER](index.html#std-setting-FTP_USER){.reference .internal}

-   [GCS_PROJECT_ID](index.html#std-setting-GCS_PROJECT_ID){.reference
    .internal}

-   [HTTPCACHE_ALWAYS_STORE](index.html#std-setting-HTTPCACHE_ALWAYS_STORE){.reference
    .internal}

-   [HTTPCACHE_DBM_MODULE](index.html#std-setting-HTTPCACHE_DBM_MODULE){.reference
    .internal}

-   [HTTPCACHE_DIR](index.html#std-setting-HTTPCACHE_DIR){.reference
    .internal}

-   [HTTPCACHE_ENABLED](index.html#std-setting-HTTPCACHE_ENABLED){.reference
    .internal}

-   [HTTPCACHE_EXPIRATION_SECS](index.html#std-setting-HTTPCACHE_EXPIRATION_SECS){.reference
    .internal}

-   [HTTPCACHE_GZIP](index.html#std-setting-HTTPCACHE_GZIP){.reference
    .internal}

-   [HTTPCACHE_IGNORE_HTTP_CODES](index.html#std-setting-HTTPCACHE_IGNORE_HTTP_CODES){.reference
    .internal}

-   [HTTPCACHE_IGNORE_MISSING](index.html#std-setting-HTTPCACHE_IGNORE_MISSING){.reference
    .internal}

-   [HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS](index.html#std-setting-HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS){.reference
    .internal}

-   [HTTPCACHE_IGNORE_SCHEMES](index.html#std-setting-HTTPCACHE_IGNORE_SCHEMES){.reference
    .internal}

-   [HTTPCACHE_POLICY](index.html#std-setting-HTTPCACHE_POLICY){.reference
    .internal}

-   [HTTPCACHE_STORAGE](index.html#std-setting-HTTPCACHE_STORAGE){.reference
    .internal}

-   [HTTPERROR_ALLOWED_CODES](index.html#std-setting-HTTPERROR_ALLOWED_CODES){.reference
    .internal}

-   [HTTPERROR_ALLOW_ALL](index.html#std-setting-HTTPERROR_ALLOW_ALL){.reference
    .internal}

-   [HTTPPROXY_AUTH_ENCODING](index.html#std-setting-HTTPPROXY_AUTH_ENCODING){.reference
    .internal}

-   [HTTPPROXY_ENABLED](index.html#std-setting-HTTPPROXY_ENABLED){.reference
    .internal}

-   [IMAGES_EXPIRES](index.html#std-setting-IMAGES_EXPIRES){.reference
    .internal}

-   [IMAGES_MIN_HEIGHT](index.html#std-setting-IMAGES_MIN_HEIGHT){.reference
    .internal}

-   [IMAGES_MIN_WIDTH](index.html#std-setting-IMAGES_MIN_WIDTH){.reference
    .internal}

-   [IMAGES_RESULT_FIELD](index.html#std-setting-IMAGES_RESULT_FIELD){.reference
    .internal}

-   [IMAGES_STORE](index.html#std-setting-IMAGES_STORE){.reference
    .internal}

-   [IMAGES_STORE_GCS_ACL](index.html#std-setting-IMAGES_STORE_GCS_ACL){.reference
    .internal}

-   [IMAGES_STORE_S3_ACL](index.html#std-setting-IMAGES_STORE_S3_ACL){.reference
    .internal}

-   [IMAGES_THUMBS](index.html#std-setting-IMAGES_THUMBS){.reference
    .internal}

-   [IMAGES_URLS_FIELD](index.html#std-setting-IMAGES_URLS_FIELD){.reference
    .internal}

-   [ITEM_PIPELINES](index.html#std-setting-ITEM_PIPELINES){.reference
    .internal}

-   [ITEM_PIPELINES_BASE](index.html#std-setting-ITEM_PIPELINES_BASE){.reference
    .internal}

-   [JOBDIR](index.html#std-setting-JOBDIR){.reference .internal}

-   [LOGSTATS_INTERVAL](index.html#std-setting-LOGSTATS_INTERVAL){.reference
    .internal}

-   [LOG_DATEFORMAT](index.html#std-setting-LOG_DATEFORMAT){.reference
    .internal}

-   [LOG_ENABLED](index.html#std-setting-LOG_ENABLED){.reference
    .internal}

-   [LOG_ENCODING](index.html#std-setting-LOG_ENCODING){.reference
    .internal}

-   [LOG_FILE](index.html#std-setting-LOG_FILE){.reference .internal}

-   [LOG_FILE_APPEND](index.html#std-setting-LOG_FILE_APPEND){.reference
    .internal}

-   [LOG_FORMAT](index.html#std-setting-LOG_FORMAT){.reference
    .internal}

-   [LOG_FORMATTER](index.html#std-setting-LOG_FORMATTER){.reference
    .internal}

-   [LOG_LEVEL](index.html#std-setting-LOG_LEVEL){.reference .internal}

-   [LOG_SHORT_NAMES](index.html#std-setting-LOG_SHORT_NAMES){.reference
    .internal}

-   [LOG_STDOUT](index.html#std-setting-LOG_STDOUT){.reference
    .internal}

-   [MAIL_FROM](index.html#std-setting-MAIL_FROM){.reference .internal}

-   [MAIL_HOST](index.html#std-setting-MAIL_HOST){.reference .internal}

-   [MAIL_PASS](index.html#std-setting-MAIL_PASS){.reference .internal}

-   [MAIL_PORT](index.html#std-setting-MAIL_PORT){.reference .internal}

-   [MAIL_SSL](index.html#std-setting-MAIL_SSL){.reference .internal}

-   [MAIL_TLS](index.html#std-setting-MAIL_TLS){.reference .internal}

-   [MAIL_USER](index.html#std-setting-MAIL_USER){.reference .internal}

-   [MEDIA_ALLOW_REDIRECTS](index.html#std-setting-MEDIA_ALLOW_REDIRECTS){.reference
    .internal}

-   [MEMDEBUG_ENABLED](index.html#std-setting-MEMDEBUG_ENABLED){.reference
    .internal}

-   [MEMDEBUG_NOTIFY](index.html#std-setting-MEMDEBUG_NOTIFY){.reference
    .internal}

-   [MEMUSAGE_CHECK_INTERVAL_SECONDS](index.html#std-setting-MEMUSAGE_CHECK_INTERVAL_SECONDS){.reference
    .internal}

-   [MEMUSAGE_ENABLED](index.html#std-setting-MEMUSAGE_ENABLED){.reference
    .internal}

-   [MEMUSAGE_LIMIT_MB](index.html#std-setting-MEMUSAGE_LIMIT_MB){.reference
    .internal}

-   [MEMUSAGE_NOTIFY_MAIL](index.html#std-setting-MEMUSAGE_NOTIFY_MAIL){.reference
    .internal}

-   [MEMUSAGE_WARNING_MB](index.html#std-setting-MEMUSAGE_WARNING_MB){.reference
    .internal}

-   [METAREFRESH_ENABLED](index.html#std-setting-METAREFRESH_ENABLED){.reference
    .internal}

-   [METAREFRESH_IGNORE_TAGS](index.html#std-setting-METAREFRESH_IGNORE_TAGS){.reference
    .internal}

-   [METAREFRESH_MAXDELAY](index.html#std-setting-METAREFRESH_MAXDELAY){.reference
    .internal}

-   [NEWSPIDER_MODULE](index.html#std-setting-NEWSPIDER_MODULE){.reference
    .internal}

-   [PERIODIC_LOG_DELTA](index.html#std-setting-PERIODIC_LOG_DELTA){.reference
    .internal}

-   [PERIODIC_LOG_STATS](index.html#std-setting-PERIODIC_LOG_STATS){.reference
    .internal}

-   [PERIODIC_LOG_TIMING_ENABLED](index.html#std-setting-PERIODIC_LOG_TIMING_ENABLED){.reference
    .internal}

-   [RANDOMIZE_DOWNLOAD_DELAY](index.html#std-setting-RANDOMIZE_DOWNLOAD_DELAY){.reference
    .internal}

-   [REACTOR_THREADPOOL_MAXSIZE](index.html#std-setting-REACTOR_THREADPOOL_MAXSIZE){.reference
    .internal}

-   [REDIRECT_ENABLED](index.html#std-setting-REDIRECT_ENABLED){.reference
    .internal}

-   [REDIRECT_MAX_TIMES](index.html#std-setting-REDIRECT_MAX_TIMES){.reference
    .internal}

-   [REDIRECT_PRIORITY_ADJUST](index.html#std-setting-REDIRECT_PRIORITY_ADJUST){.reference
    .internal}

-   [REFERER_ENABLED](index.html#std-setting-REFERER_ENABLED){.reference
    .internal}

-   [REFERRER_POLICY](index.html#std-setting-REFERRER_POLICY){.reference
    .internal}

-   [REQUEST_FINGERPRINTER_CLASS](index.html#std-setting-REQUEST_FINGERPRINTER_CLASS){.reference
    .internal}

-   [REQUEST_FINGERPRINTER_IMPLEMENTATION](index.html#std-setting-REQUEST_FINGERPRINTER_IMPLEMENTATION){.reference
    .internal}

-   [RETRY_ENABLED](index.html#std-setting-RETRY_ENABLED){.reference
    .internal}

-   [RETRY_EXCEPTIONS](index.html#std-setting-RETRY_EXCEPTIONS){.reference
    .internal}

-   [RETRY_HTTP_CODES](index.html#std-setting-RETRY_HTTP_CODES){.reference
    .internal}

-   [RETRY_PRIORITY_ADJUST](index.html#std-setting-RETRY_PRIORITY_ADJUST){.reference
    .internal}

-   [RETRY_TIMES](index.html#std-setting-RETRY_TIMES){.reference
    .internal}

-   [ROBOTSTXT_OBEY](index.html#std-setting-ROBOTSTXT_OBEY){.reference
    .internal}

-   [ROBOTSTXT_PARSER](index.html#std-setting-ROBOTSTXT_PARSER){.reference
    .internal}

-   [ROBOTSTXT_USER_AGENT](index.html#std-setting-ROBOTSTXT_USER_AGENT){.reference
    .internal}

-   [SCHEDULER](index.html#std-setting-SCHEDULER){.reference .internal}

-   [SCHEDULER_DEBUG](index.html#std-setting-SCHEDULER_DEBUG){.reference
    .internal}

-   [SCHEDULER_DISK_QUEUE](index.html#std-setting-SCHEDULER_DISK_QUEUE){.reference
    .internal}

-   [SCHEDULER_MEMORY_QUEUE](index.html#std-setting-SCHEDULER_MEMORY_QUEUE){.reference
    .internal}

-   [SCHEDULER_PRIORITY_QUEUE](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.reference
    .internal}

-   [SCRAPER_SLOT_MAX_ACTIVE_SIZE](index.html#std-setting-SCRAPER_SLOT_MAX_ACTIVE_SIZE){.reference
    .internal}

-   [SPIDER_CONTRACTS](index.html#std-setting-SPIDER_CONTRACTS){.reference
    .internal}

-   [SPIDER_CONTRACTS_BASE](index.html#std-setting-SPIDER_CONTRACTS_BASE){.reference
    .internal}

-   [SPIDER_LOADER_CLASS](index.html#std-setting-SPIDER_LOADER_CLASS){.reference
    .internal}

-   [SPIDER_LOADER_WARN_ONLY](index.html#std-setting-SPIDER_LOADER_WARN_ONLY){.reference
    .internal}

-   [SPIDER_MIDDLEWARES](index.html#std-setting-SPIDER_MIDDLEWARES){.reference
    .internal}

-   [SPIDER_MIDDLEWARES_BASE](index.html#std-setting-SPIDER_MIDDLEWARES_BASE){.reference
    .internal}

-   [SPIDER_MODULES](index.html#std-setting-SPIDER_MODULES){.reference
    .internal}

-   [STATSMAILER_RCPTS](index.html#std-setting-STATSMAILER_RCPTS){.reference
    .internal}

-   [STATS_CLASS](index.html#std-setting-STATS_CLASS){.reference
    .internal}

-   [STATS_DUMP](index.html#std-setting-STATS_DUMP){.reference
    .internal}

-   [TELNETCONSOLE_ENABLED](index.html#std-setting-TELNETCONSOLE_ENABLED){.reference
    .internal}

-   [TELNETCONSOLE_HOST](index.html#std-setting-TELNETCONSOLE_HOST){.reference
    .internal}

-   [TELNETCONSOLE_PASSWORD](index.html#std-setting-TELNETCONSOLE_PASSWORD){.reference
    .internal}

-   [TELNETCONSOLE_PORT](index.html#std-setting-TELNETCONSOLE_PORT){.reference
    .internal}

-   [TELNETCONSOLE_USERNAME](index.html#std-setting-TELNETCONSOLE_USERNAME){.reference
    .internal}

-   [TEMPLATES_DIR](index.html#std-setting-TEMPLATES_DIR){.reference
    .internal}

-   [TWISTED_REACTOR](index.html#std-setting-TWISTED_REACTOR){.reference
    .internal}

-   [URLLENGTH_LIMIT](index.html#std-setting-URLLENGTH_LIMIT){.reference
    .internal}

-   [USER_AGENT](index.html#std-setting-USER_AGENT){.reference
    .internal}
:::
:::
:::

[]{#document-topics/exceptions}

::: {#module-scrapy.exceptions .section}
[]{#exceptions}[]{#topics-exceptions}

### Exceptions[¶](#module-scrapy.exceptions "Permalink to this heading"){.headerlink}

::: {#built-in-exceptions-reference .section}
[]{#topics-exceptions-ref}

#### Built-in Exceptions reference[¶](#built-in-exceptions-reference "Permalink to this heading"){.headerlink}

Here's a list of all exceptions included in Scrapy and their usage.

::: {#closespider .section}
##### CloseSpider[¶](#closespider "Permalink to this heading"){.headerlink}

*[exception]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[CloseSpider]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[reason]{.pre}]{.n}[[=]{.pre}]{.o}[[\'cancelled\']{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#CloseSpider){.reference .internal}[¶](#scrapy.exceptions.CloseSpider "Permalink to this definition"){.headerlink}

:   This exception can be raised from a spider callback to request the
    spider to be closed/stopped. Supported arguments:

    Parameters

    :   **reason**
        ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
        .external}) -- the reason for closing

For example:

::: {.highlight-python .notranslate}
::: highlight
    def parse_page(self, response):
        if "Bandwidth exceeded" in response.body:
            raise CloseSpider("bandwidth_exceeded")
:::
:::
:::

::: {#dontclosespider .section}
##### DontCloseSpider[¶](#dontclosespider "Permalink to this heading"){.headerlink}

*[exception]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[DontCloseSpider]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#DontCloseSpider){.reference .internal}[¶](#scrapy.exceptions.DontCloseSpider "Permalink to this definition"){.headerlink}

:   

This exception can be raised in a [[`spider_idle`{.xref .std .std-signal
.docutils .literal
.notranslate}]{.pre}](index.html#std-signal-spider_idle){.hoverxref
.tooltip .reference .internal} signal handler to prevent the spider from
being closed.
:::

::: {#dropitem .section}
##### DropItem[¶](#dropitem "Permalink to this heading"){.headerlink}

*[exception]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[DropItem]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#DropItem){.reference .internal}[¶](#scrapy.exceptions.DropItem "Permalink to this definition"){.headerlink}

:   

The exception that must be raised by item pipeline stages to stop
processing an Item. For more information see [[Item Pipeline]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal}.
:::

::: {#ignorerequest .section}
##### IgnoreRequest[¶](#ignorerequest "Permalink to this heading"){.headerlink}

*[exception]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[IgnoreRequest]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#IgnoreRequest){.reference .internal}[¶](#scrapy.exceptions.IgnoreRequest "Permalink to this definition"){.headerlink}

:   

This exception can be raised by the Scheduler or any downloader
middleware to indicate that the request should be ignored.
:::

::: {#notconfigured .section}
##### NotConfigured[¶](#notconfigured "Permalink to this heading"){.headerlink}

*[exception]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[NotConfigured]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#NotConfigured){.reference .internal}[¶](#scrapy.exceptions.NotConfigured "Permalink to this definition"){.headerlink}

:   

This exception can be raised by some components to indicate that they
will remain disabled. Those components include:

-   Extensions

-   Item pipelines

-   Downloader middlewares

-   Spider middlewares

The exception must be raised in the component's [`__init__`{.docutils
.literal .notranslate}]{.pre} method.
:::

::: {#notsupported .section}
##### NotSupported[¶](#notsupported "Permalink to this heading"){.headerlink}

*[exception]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[NotSupported]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#NotSupported){.reference .internal}[¶](#scrapy.exceptions.NotSupported "Permalink to this definition"){.headerlink}

:   

This exception is raised to indicate an unsupported feature.
:::

::: {#stopdownload .section}
##### StopDownload[¶](#stopdownload "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.2.]{.versionmodified .added}
:::

*[exception]{.pre}[ ]{.w}*[[scrapy.exceptions.]{.pre}]{.sig-prename .descclassname}[[StopDownload]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[fail]{.pre}]{.n}[[=]{.pre}]{.o}[[True]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exceptions.html#StopDownload){.reference .internal}[¶](#scrapy.exceptions.StopDownload "Permalink to this definition"){.headerlink}

:   

Raised from a [[`bytes_received`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.signals.bytes_received "scrapy.signals.bytes_received"){.reference
.internal} or [[`headers_received`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.signals.headers_received "scrapy.signals.headers_received"){.reference
.internal} signal handler to indicate that no further bytes should be
downloaded for a response.

The [`fail`{.docutils .literal .notranslate}]{.pre} boolean parameter
controls which method will handle the resulting response:

-   If [`fail=True`{.docutils .literal .notranslate}]{.pre} (default),
    the request errback is called. The response object is available as
    the [`response`{.docutils .literal .notranslate}]{.pre} attribute of
    the [`StopDownload`{.docutils .literal .notranslate}]{.pre}
    exception, which is in turn stored as the [`value`{.docutils
    .literal .notranslate}]{.pre} attribute of the received
    [[`Failure`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference
    .external} object. This means that in an errback defined as
    [`def`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`errback(self,`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`failure)`{.docutils .literal .notranslate}]{.pre},
    the response can be accessed though
    [`failure.value.response`{.docutils .literal .notranslate}]{.pre}.

-   If [`fail=False`{.docutils .literal .notranslate}]{.pre}, the
    request callback is called instead.

In both cases, the response could have its body truncated: the body
contains all bytes received up until the exception is raised, including
the bytes received in the signal handler that raises the exception.
Also, the response object is marked with [`"download_stopped"`{.docutils
.literal .notranslate}]{.pre} in its [`Response.flags`{.xref .py
.py-attr .docutils .literal .notranslate}]{.pre} attribute.

::: {.admonition .note}
Note

[`fail`{.docutils .literal .notranslate}]{.pre} is a keyword-only
parameter, i.e. raising [`StopDownload(False)`{.docutils .literal
.notranslate}]{.pre} or [`StopDownload(True)`{.docutils .literal
.notranslate}]{.pre} will raise a [[`TypeError`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#TypeError "(in Python v3.12)"){.reference
.external}.
:::

See the documentation for the [[`bytes_received`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.signals.bytes_received "scrapy.signals.bytes_received"){.reference
.internal} and [[`headers_received`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.signals.headers_received "scrapy.signals.headers_received"){.reference
.internal} signals and the [[Stopping the download of a Response]{.std
.std-ref}](index.html#topics-stop-response-download){.hoverxref .tooltip
.reference .internal} topic for additional information and examples.
:::
:::
:::
:::

[[Command line tool]{.doc}](index.html#document-topics/commands){.reference .internal}

:   Learn about the command-line tool used to manage your Scrapy
    project.

[[Spiders]{.doc}](index.html#document-topics/spiders){.reference .internal}

:   Write the rules to crawl your websites.

[[Selectors]{.doc}](index.html#document-topics/selectors){.reference .internal}

:   Extract the data from web pages using XPath.

[[Scrapy shell]{.doc}](index.html#document-topics/shell){.reference .internal}

:   Test your extraction code in an interactive environment.

[[Items]{.doc}](index.html#document-topics/items){.reference .internal}

:   Define the data you want to scrape.

[[Item Loaders]{.doc}](index.html#document-topics/loaders){.reference .internal}

:   Populate your items with the extracted data.

[[Item Pipeline]{.doc}](index.html#document-topics/item-pipeline){.reference .internal}

:   Post-process and store your scraped data.

[[Feed exports]{.doc}](index.html#document-topics/feed-exports){.reference .internal}

:   Output your scraped data using different formats and storages.

[[Requests and Responses]{.doc}](index.html#document-topics/request-response){.reference .internal}

:   Understand the classes used to represent HTTP requests and
    responses.

[[Link Extractors]{.doc}](index.html#document-topics/link-extractors){.reference .internal}

:   Convenient classes to extract links to follow from pages.

[[Settings]{.doc}](index.html#document-topics/settings){.reference .internal}

:   Learn how to configure Scrapy and see all [[available settings]{.std
    .std-ref}](index.html#topics-settings-ref){.hoverxref .tooltip
    .reference .internal}.

[[Exceptions]{.doc}](index.html#document-topics/exceptions){.reference .internal}

:   See all available exceptions and their meaning.
:::

::: {#built-in-services .section}
## Built-in services[¶](#built-in-services "Permalink to this heading"){.headerlink}

::: {.toctree-wrapper .compound}
[]{#document-topics/logging}

::: {#logging .section}
[]{#topics-logging}

### Logging[¶](#logging "Permalink to this heading"){.headerlink}

::: {.admonition .note}
Note

[`scrapy.log`{.xref .py .py-mod .docutils .literal .notranslate}]{.pre}
has been deprecated alongside its functions in favor of explicit calls
to the Python standard logging. Keep reading to learn more about the new
logging system.
:::

Scrapy uses [[`logging`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/logging.html#module-logging "(in Python v3.12)"){.reference
.external} for event logging. We'll provide some simple examples to get
you started, but for more advanced use-cases it's strongly suggested to
read thoroughly its documentation.

Logging works out of the box, and can be configured to some extent with
the Scrapy settings listed in [[Logging settings]{.std
.std-ref}](#topics-logging-settings){.hoverxref .tooltip .reference
.internal}.

Scrapy calls [[`scrapy.utils.log.configure_logging()`{.xref .py .py-func
.docutils .literal
.notranslate}]{.pre}](#scrapy.utils.log.configure_logging "scrapy.utils.log.configure_logging"){.reference
.internal} to set some reasonable defaults and handle those settings in
[[Logging settings]{.std .std-ref}](#topics-logging-settings){.hoverxref
.tooltip .reference .internal} when running commands, so it's
recommended to manually call it if you're running Scrapy from scripts as
described in [[Run Scrapy from a script]{.std
.std-ref}](index.html#run-from-script){.hoverxref .tooltip .reference
.internal}.

::: {#log-levels .section}
[]{#topics-logging-levels}

#### Log levels[¶](#log-levels "Permalink to this heading"){.headerlink}

Python's builtin logging defines 5 different levels to indicate the
severity of a given log message. Here are the standard ones, listed in
decreasing order:

1.  [`logging.CRITICAL`{.docutils .literal .notranslate}]{.pre} - for
    critical errors (highest severity)

2.  [`logging.ERROR`{.docutils .literal .notranslate}]{.pre} - for
    regular errors

3.  [`logging.WARNING`{.docutils .literal .notranslate}]{.pre} - for
    warning messages

4.  [`logging.INFO`{.docutils .literal .notranslate}]{.pre} - for
    informational messages

5.  [`logging.DEBUG`{.docutils .literal .notranslate}]{.pre} - for
    debugging messages (lowest severity)
:::

::: {#how-to-log-messages .section}
#### How to log messages[¶](#how-to-log-messages "Permalink to this heading"){.headerlink}

Here's a quick example of how to log a message using the
[`logging.WARNING`{.docutils .literal .notranslate}]{.pre} level:

::: {.highlight-python .notranslate}
::: highlight
    import logging

    logging.warning("This is a warning")
:::
:::

There are shortcuts for issuing log messages on any of the standard 5
levels, and there's also a general [`logging.log`{.docutils .literal
.notranslate}]{.pre} method which takes a given level as argument. If
needed, the last example could be rewritten as:

::: {.highlight-python .notranslate}
::: highlight
    import logging

    logging.log(logging.WARNING, "This is a warning")
:::
:::

On top of that, you can create different "loggers" to encapsulate
messages. (For example, a common practice is to create different loggers
for every module). These loggers can be configured independently, and
they allow hierarchical constructions.

The previous examples use the root logger behind the scenes, which is a
top level logger where all messages are propagated to (unless otherwise
specified). Using [`logging`{.docutils .literal .notranslate}]{.pre}
helpers is merely a shortcut for getting the root logger explicitly, so
this is also an equivalent of the last snippets:

::: {.highlight-python .notranslate}
::: highlight
    import logging

    logger = logging.getLogger()
    logger.warning("This is a warning")
:::
:::

You can use a different logger just by getting its name with the
[`logging.getLogger`{.docutils .literal .notranslate}]{.pre} function:

::: {.highlight-python .notranslate}
::: highlight
    import logging

    logger = logging.getLogger("mycustomlogger")
    logger.warning("This is a warning")
:::
:::

Finally, you can ensure having a custom logger for any module you're
working on by using the [`__name__`{.docutils .literal
.notranslate}]{.pre} variable, which is populated with current module's
path:

::: {.highlight-python .notranslate}
::: highlight
    import logging

    logger = logging.getLogger(__name__)
    logger.warning("This is a warning")
:::
:::

::: {.admonition .seealso}
See also

Module logging, [[HowTo]{.xref .std .std-doc}](https://docs.python.org/3/howto/logging.html "(in Python v3.12)"){.reference .external}

:   Basic Logging Tutorial

Module logging, [[Loggers]{.xref .std .std-ref}](https://docs.python.org/3/library/logging.html#logger "(in Python v3.12)"){.reference .external}

:   Further documentation on loggers
:::
:::

::: {#logging-from-spiders .section}
[]{#topics-logging-from-spiders}

#### Logging from Spiders[¶](#logging-from-spiders "Permalink to this heading"){.headerlink}

Scrapy provides a [[`logger`{.xref .py .py-data .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.logger "scrapy.Spider.logger"){.reference
.internal} within each Spider instance, which can be accessed and used
like this:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "myspider"
        start_urls = ["https://scrapy.org"]

        def parse(self, response):
            self.logger.info("Parse function called on %s", response.url)
:::
:::

That logger is created using the Spider's name, but you can use any
custom Python logger you want. For example:

::: {.highlight-python .notranslate}
::: highlight
    import logging
    import scrapy

    logger = logging.getLogger("mycustomlogger")


    class MySpider(scrapy.Spider):
        name = "myspider"
        start_urls = ["https://scrapy.org"]

        def parse(self, response):
            logger.info("Parse function called on %s", response.url)
:::
:::
:::

::: {#logging-configuration .section}
[]{#topics-logging-configuration}

#### Logging configuration[¶](#logging-configuration "Permalink to this heading"){.headerlink}

Loggers on their own don't manage how messages sent through them are
displayed. For this task, different "handlers" can be attached to any
logger instance and they will redirect those messages to appropriate
destinations, such as the standard output, files, emails, etc.

By default, Scrapy sets and configures a handler for the root logger,
based on the settings below.

::: {#logging-settings .section}
[]{#topics-logging-settings}

##### Logging settings[¶](#logging-settings "Permalink to this heading"){.headerlink}

These settings can be used to configure the logging:

-   [[`LOG_FILE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_FILE){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_FILE_APPEND`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_FILE_APPEND){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_ENABLED`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_ENABLED){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_ENCODING`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_ENCODING){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_LEVEL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_LEVEL){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_FORMAT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_FORMAT){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_DATEFORMAT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_DATEFORMAT){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_STDOUT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_STDOUT){.hoverxref
    .tooltip .reference .internal}

-   [[`LOG_SHORT_NAMES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-LOG_SHORT_NAMES){.hoverxref
    .tooltip .reference .internal}

The first couple of settings define a destination for log messages. If
[[`LOG_FILE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_FILE){.hoverxref
.tooltip .reference .internal} is set, messages sent through the root
logger will be redirected to a file named [[`LOG_FILE`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_FILE){.hoverxref
.tooltip .reference .internal} with encoding [[`LOG_ENCODING`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_ENCODING){.hoverxref
.tooltip .reference .internal}. If unset and [[`LOG_ENABLED`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_ENABLED){.hoverxref
.tooltip .reference .internal} is [`True`{.docutils .literal
.notranslate}]{.pre}, log messages will be displayed on the standard
error. If [[`LOG_FILE`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_FILE){.hoverxref
.tooltip .reference .internal} is set and [[`LOG_FILE_APPEND`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_FILE_APPEND){.hoverxref
.tooltip .reference .internal} is [`False`{.docutils .literal
.notranslate}]{.pre}, the file will be overwritten (discarding the
output from previous runs, if any). Lastly, if [[`LOG_ENABLED`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_ENABLED){.hoverxref
.tooltip .reference .internal} is [`False`{.docutils .literal
.notranslate}]{.pre}, there won't be any visible log output.

[[`LOG_LEVEL`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_LEVEL){.hoverxref
.tooltip .reference .internal} determines the minimum level of severity
to display, those messages with lower severity will be filtered out. It
ranges through the possible levels listed in [[Log levels]{.std
.std-ref}](#topics-logging-levels){.hoverxref .tooltip .reference
.internal}.

[[`LOG_FORMAT`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_FORMAT){.hoverxref
.tooltip .reference .internal} and [[`LOG_DATEFORMAT`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_DATEFORMAT){.hoverxref
.tooltip .reference .internal} specify formatting strings used as
layouts for all messages. Those strings can contain any placeholders
listed in [[logging's logrecord attributes docs]{.xref .std
.std-ref}](https://docs.python.org/3/library/logging.html#logrecord-attributes "(in Python v3.12)"){.reference
.external} and [[datetime's strftime and strptime directives]{.xref .std
.std-ref}](https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior "(in Python v3.12)"){.reference
.external} respectively.

If [[`LOG_SHORT_NAMES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_SHORT_NAMES){.hoverxref
.tooltip .reference .internal} is set, then the logs will not display
the Scrapy component that prints the log. It is unset by default, hence
logs contain the Scrapy component responsible for that log output.
:::

::: {#command-line-options .section}
##### Command-line options[¶](#command-line-options "Permalink to this heading"){.headerlink}

There are command-line arguments, available for all commands, that you
can use to override some of the Scrapy settings regarding logging.

-   

    [`--logfile`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`FILE`{.docutils .literal .notranslate}]{.pre}

    :   Overrides [[`LOG_FILE`{.xref .std .std-setting .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-setting-LOG_FILE){.hoverxref
        .tooltip .reference .internal}

-   

    [`--loglevel/-L`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`LEVEL`{.docutils .literal .notranslate}]{.pre}

    :   Overrides [[`LOG_LEVEL`{.xref .std .std-setting .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-setting-LOG_LEVEL){.hoverxref
        .tooltip .reference .internal}

-   

    [`--nolog`{.docutils .literal .notranslate}]{.pre}

    :   Sets [[`LOG_ENABLED`{.xref .std .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-LOG_ENABLED){.hoverxref
        .tooltip .reference .internal} to [`False`{.docutils .literal
        .notranslate}]{.pre}

::: {.admonition .seealso}
See also

Module [[`logging.handlers`{.xref .py .py-mod .docutils .literal .notranslate}]{.pre}](https://docs.python.org/3/library/logging.handlers.html#module-logging.handlers "(in Python v3.12)"){.reference .external}

:   Further documentation on available handlers
:::
:::

::: {#custom-log-formats .section}
[]{#id1}

##### Custom Log Formats[¶](#custom-log-formats "Permalink to this heading"){.headerlink}

A custom log format can be set for different actions by extending
[[`LogFormatter`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.logformatter.LogFormatter "scrapy.logformatter.LogFormatter"){.reference
.internal} class and making [[`LOG_FORMATTER`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_FORMATTER){.hoverxref
.tooltip .reference .internal} point to your new class.

*[class]{.pre}[ ]{.w}*[[scrapy.logformatter.]{.pre}]{.sig-prename .descclassname}[[LogFormatter]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/logformatter.html#LogFormatter){.reference .internal}[¶](#scrapy.logformatter.LogFormatter "Permalink to this definition"){.headerlink}

:   Class for generating log messages for different actions.

    All methods must return a dictionary listing the parameters
    [`level`{.docutils .literal .notranslate}]{.pre}, [`msg`{.docutils
    .literal .notranslate}]{.pre} and [`args`{.docutils .literal
    .notranslate}]{.pre} which are going to be used for constructing the
    log message when calling [`logging.log`{.docutils .literal
    .notranslate}]{.pre}.

    Dictionary keys for the method outputs:

    -   [`level`{.docutils .literal .notranslate}]{.pre} is the log
        level for that action, you can use those from the [python
        logging
        library](https://docs.python.org/3/library/logging.html){.reference
        .external} : [`logging.DEBUG`{.docutils .literal
        .notranslate}]{.pre}, [`logging.INFO`{.docutils .literal
        .notranslate}]{.pre}, [`logging.WARNING`{.docutils .literal
        .notranslate}]{.pre}, [`logging.ERROR`{.docutils .literal
        .notranslate}]{.pre} and [`logging.CRITICAL`{.docutils .literal
        .notranslate}]{.pre}.

    -   [`msg`{.docutils .literal .notranslate}]{.pre} should be a
        string that can contain different formatting placeholders. This
        string, formatted with the provided [`args`{.docutils .literal
        .notranslate}]{.pre}, is going to be the long message for that
        action.

    -   [`args`{.docutils .literal .notranslate}]{.pre} should be a
        tuple or dict with the formatting placeholders for
        [`msg`{.docutils .literal .notranslate}]{.pre}. The final log
        message is computed as [`msg`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`%`{.docutils .literal
        .notranslate}]{.pre}` `{.docutils .literal
        .notranslate}[`args`{.docutils .literal .notranslate}]{.pre}.

    Users can define their own [`LogFormatter`{.docutils .literal
    .notranslate}]{.pre} class if they want to customize how each action
    is logged or if they want to omit it entirely. In order to omit
    logging an action the method must return [`None`{.docutils .literal
    .notranslate}]{.pre}.

    Here is an example on how to create a custom log formatter to lower
    the severity level of the log message when an item is dropped from
    the pipeline:

    ::: {.highlight-default .notranslate}
    ::: highlight
        class PoliteLogFormatter(logformatter.LogFormatter):
            def dropped(self, item, exception, response, spider):
                return {
                    'level': logging.INFO, # lowering the level from logging.WARNING
                    'msg': "Dropped: %(exception)s" + os.linesep + "%(item)s",
                    'args': {
                        'exception': exception,
                        'item': item,
                    }
                }
    :::
    :::

    [[crawled]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.n}*, *[[response]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Response]{.pre}](index.html#scrapy.http.Response "scrapy.http.response.Response"){.reference .internal}]{.n}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/logformatter.html#LogFormatter.crawled){.reference .internal}[¶](#scrapy.logformatter.LogFormatter.crawled "Permalink to this definition"){.headerlink}

    :   Logs a message when the crawler finds a webpage.

    [[download_error]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[failure]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Failure]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference .external}]{.n}*, *[[request]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.n}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*, *[[errmsg]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/logformatter.html#LogFormatter.download_error){.reference .internal}[¶](#scrapy.logformatter.LogFormatter.download_error "Permalink to this definition"){.headerlink}

    :   Logs a download error message from a spider (typically coming
        from the engine).

        ::: versionadded
        [New in version 2.0.]{.versionmodified .added}
        :::

    [[dropped]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[exception]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[BaseException]{.pre}](https://docs.python.org/3/library/exceptions.html#BaseException "(in Python v3.12)"){.reference .external}]{.n}*, *[[response]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Response]{.pre}](index.html#scrapy.http.Response "scrapy.http.response.Response"){.reference .internal}]{.n}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/logformatter.html#LogFormatter.dropped){.reference .internal}[¶](#scrapy.logformatter.LogFormatter.dropped "Permalink to this definition"){.headerlink}

    :   Logs a message when an item is dropped while it is passing
        through the item pipeline.

    [[item_error]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[exception]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[BaseException]{.pre}](https://docs.python.org/3/library/exceptions.html#BaseException "(in Python v3.12)"){.reference .external}]{.n}*, *[[response]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Response]{.pre}](index.html#scrapy.http.Response "scrapy.http.response.Response"){.reference .internal}]{.n}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/logformatter.html#LogFormatter.item_error){.reference .internal}[¶](#scrapy.logformatter.LogFormatter.item_error "Permalink to this definition"){.headerlink}

    :   Logs a message when an item causes an error while it is passing
        through the item pipeline.

        ::: versionadded
        [New in version 2.0.]{.versionmodified .added}
        :::

    [[scraped]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[response]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Response]{.pre}](index.html#scrapy.http.Response "scrapy.http.response.Response"){.reference .internal}[[,]{.pre}]{.p}[ ]{.w}[[Failure]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/logformatter.html#LogFormatter.scraped){.reference .internal}[¶](#scrapy.logformatter.LogFormatter.scraped "Permalink to this definition"){.headerlink}

    :   Logs a message when an item is scraped by a spider.

    [[spider_error]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[failure]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Failure]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference .external}]{.n}*, *[[request]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.n}*, *[[response]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Response]{.pre}](index.html#scrapy.http.Response "scrapy.http.response.Response"){.reference .internal}[[,]{.pre}]{.p}[ ]{.w}[[Failure]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/logformatter.html#LogFormatter.spider_error){.reference .internal}[¶](#scrapy.logformatter.LogFormatter.spider_error "Permalink to this definition"){.headerlink}

    :   Logs an error message from a spider.

        ::: versionadded
        [New in version 2.0.]{.versionmodified .added}
        :::
:::

::: {#advanced-customization .section}
[]{#topics-logging-advanced-customization}

##### Advanced customization[¶](#advanced-customization "Permalink to this heading"){.headerlink}

Because Scrapy uses stdlib logging module, you can customize logging
using all features of stdlib logging.

For example, let's say you're scraping a website which returns many HTTP
404 and 500 responses, and you want to hide all messages like this:

::: {.highlight-default .notranslate}
::: highlight
    2016-12-16 22:00:06 [scrapy.spidermiddlewares.httperror] INFO: Ignoring
    response <500 https://quotes.toscrape.com/page/1-34/>: HTTP status code
    is not handled or not allowed
:::
:::

The first thing to note is a logger name - it is in brackets:
[`[scrapy.spidermiddlewares.httperror]`{.docutils .literal
.notranslate}]{.pre}. If you get just [`[scrapy]`{.docutils .literal
.notranslate}]{.pre} then [[`LOG_SHORT_NAMES`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](index.html#std-setting-LOG_SHORT_NAMES){.hoverxref
.tooltip .reference .internal} is likely set to True; set it to False
and re-run the crawl.

Next, we can see that the message has INFO level. To hide it we should
set logging level for [`scrapy.spidermiddlewares.httperror`{.docutils
.literal .notranslate}]{.pre} higher than INFO; next level after INFO is
WARNING. It could be done e.g. in the spider's [`__init__`{.docutils
.literal .notranslate}]{.pre} method:

::: {.highlight-python .notranslate}
::: highlight
    import logging
    import scrapy


    class MySpider(scrapy.Spider):
        # ...
        def __init__(self, *args, **kwargs):
            logger = logging.getLogger("scrapy.spidermiddlewares.httperror")
            logger.setLevel(logging.WARNING)
            super().__init__(*args, **kwargs)
:::
:::

If you run this spider again then INFO messages from
[`scrapy.spidermiddlewares.httperror`{.docutils .literal
.notranslate}]{.pre} logger will be gone.

You can also filter log records by [[`LogRecord`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/logging.html#logging.LogRecord "(in Python v3.12)"){.reference
.external} data. For example, you can filter log records by message
content using a substring or a regular expression. Create a
[[`logging.Filter`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/logging.html#logging.Filter "(in Python v3.12)"){.reference
.external} subclass and equip it with a regular expression pattern to
filter out unwanted messages:

::: {.highlight-python .notranslate}
::: highlight
    import logging
    import re


    class ContentFilter(logging.Filter):
        def filter(self, record):
            match = re.search(r"\d{3} [Ee]rror, retrying", record.message)
            if match:
                return False
:::
:::

A project-level filter may be attached to the root handler created by
Scrapy, this is a wieldy way to filter all loggers in different parts of
the project (middlewares, spider, etc.):

::: {.highlight-python .notranslate}
::: highlight
    import logging
    import scrapy


    class MySpider(scrapy.Spider):
        # ...
        def __init__(self, *args, **kwargs):
            for handler in logging.root.handlers:
                handler.addFilter(ContentFilter())
:::
:::

Alternatively, you may choose a specific logger and hide it without
affecting other loggers:

::: {.highlight-python .notranslate}
::: highlight
    import logging
    import scrapy


    class MySpider(scrapy.Spider):
        # ...
        def __init__(self, *args, **kwargs):
            logger = logging.getLogger("my_logger")
            logger.addFilter(ContentFilter())
:::
:::
:::
:::

::: {#module-scrapy.utils.log .section}
[]{#scrapy-utils-log-module}

#### scrapy.utils.log module[¶](#module-scrapy.utils.log "Permalink to this heading"){.headerlink}

[[scrapy.utils.log.]{.pre}]{.sig-prename .descclassname}[[configure_logging]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[settings]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Settings]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference .internal}[[,]{.pre}]{.p}[ ]{.w}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[install_root_handler]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/log.html#configure_logging){.reference .internal}[¶](#scrapy.utils.log.configure_logging "Permalink to this definition"){.headerlink}

:   Initialize logging defaults for Scrapy.

    Parameters

    :   -   **settings** (dict, [[`Settings`{.xref .py .py-class
            .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
            .internal} object or [`None`{.docutils .literal
            .notranslate}]{.pre}) -- settings used to create and
            configure a handler for the root logger (default: None).

        -   **install_root_handler**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- whether to install root logging handler
            (default: True)

    This function does:

    -   Route warnings and twisted logging through Python standard
        logging

    -   Assign DEBUG and ERROR level to Scrapy and Twisted loggers
        respectively

    -   Route stdout to log if LOG_STDOUT setting is True

    When [`install_root_handler`{.docutils .literal .notranslate}]{.pre}
    is True (default), this function also creates a handler for the root
    logger according to given settings (see [[Logging settings]{.std
    .std-ref}](#topics-logging-settings){.hoverxref .tooltip .reference
    .internal}). You can override default options using
    [`settings`{.docutils .literal .notranslate}]{.pre} argument. When
    [`settings`{.docutils .literal .notranslate}]{.pre} is empty or
    None, defaults are used.

    [`configure_logging`{.docutils .literal .notranslate}]{.pre} is
    automatically called when using Scrapy commands or
    [[`CrawlerProcess`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
    .internal}, but needs to be called explicitly when running custom
    scripts using [[`CrawlerRunner`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
    .internal}. In that case, its usage is not required but it's
    recommended.

    Another option when running custom scripts is to manually configure
    the logging. To do this you can use [[`logging.basicConfig()`{.xref
    .py .py-func .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/logging.html#logging.basicConfig "(in Python v3.12)"){.reference
    .external} to set a basic root handler.

    Note that [[`CrawlerProcess`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerProcess "scrapy.crawler.CrawlerProcess"){.reference
    .internal} automatically calls [`configure_logging`{.docutils
    .literal .notranslate}]{.pre}, so it is recommended to only use
    [[`logging.basicConfig()`{.xref .py .py-func .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/logging.html#logging.basicConfig "(in Python v3.12)"){.reference
    .external} together with [[`CrawlerRunner`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
    .internal}.

    This is an example on how to redirect [`INFO`{.docutils .literal
    .notranslate}]{.pre} or higher messages to a file:

    ::: {.highlight-python .notranslate}
    ::: highlight
        import logging

        logging.basicConfig(
            filename="log.txt", format="%(levelname)s: %(message)s", level=logging.INFO
        )
    :::
    :::

    Refer to [[Run Scrapy from a script]{.std
    .std-ref}](index.html#run-from-script){.hoverxref .tooltip
    .reference .internal} for more details about using Scrapy this way.
:::
:::

[]{#document-topics/stats}

::: {#stats-collection .section}
[]{#topics-stats}

### Stats Collection[¶](#stats-collection "Permalink to this heading"){.headerlink}

Scrapy provides a convenient facility for collecting stats in the form
of key/values, where values are often counters. The facility is called
the Stats Collector, and can be accessed through the [[`stats`{.xref .py
.py-attr .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.stats "scrapy.crawler.Crawler.stats"){.reference
.internal} attribute of the [[Crawler API]{.std
.std-ref}](index.html#topics-api-crawler){.hoverxref .tooltip .reference
.internal}, as illustrated by the examples in the [[Common Stats
Collector uses]{.std .std-ref}](#topics-stats-usecases){.hoverxref
.tooltip .reference .internal} section below.

However, the Stats Collector is always available, so you can always
import it in your module and use its API (to increment or set new stat
keys), regardless of whether the stats collection is enabled or not. If
it's disabled, the API will still work but it won't collect anything.
This is aimed at simplifying the stats collector usage: you should spend
no more than one line of code for collecting stats in your spider,
Scrapy extension, or whatever code you're using the Stats Collector
from.

Another feature of the Stats Collector is that it's very efficient (when
enabled) and extremely efficient (almost unnoticeable) when disabled.

The Stats Collector keeps a stats table per open spider which is
automatically opened when the spider is opened, and closed when the
spider is closed.

::: {#common-stats-collector-uses .section}
[]{#topics-stats-usecases}

#### Common Stats Collector uses[¶](#common-stats-collector-uses "Permalink to this heading"){.headerlink}

Access the stats collector through the [[`stats`{.xref .py .py-attr
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.stats "scrapy.crawler.Crawler.stats"){.reference
.internal} attribute. Here is an example of an extension that access
stats:

::: {.highlight-python .notranslate}
::: highlight
    class ExtensionThatAccessStats:
        def __init__(self, stats):
            self.stats = stats

        @classmethod
        def from_crawler(cls, crawler):
            return cls(crawler.stats)
:::
:::

Set stat value:

::: {.highlight-python .notranslate}
::: highlight
    stats.set_value("hostname", socket.gethostname())
:::
:::

Increment stat value:

::: {.highlight-python .notranslate}
::: highlight
    stats.inc_value("custom_count")
:::
:::

Set stat value only if greater than previous:

::: {.highlight-python .notranslate}
::: highlight
    stats.max_value("max_items_scraped", value)
:::
:::

Set stat value only if lower than previous:

::: {.highlight-python .notranslate}
::: highlight
    stats.min_value("min_free_memory_percent", value)
:::
:::

Get stat value:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> stats.get_value("custom_count")
    1
:::
:::

Get all stats:

::: {.highlight-pycon .notranslate}
::: highlight
    >>> stats.get_stats()
    {'custom_count': 1, 'start_time': datetime.datetime(2009, 7, 14, 21, 47, 28, 977139)}
:::
:::
:::

::: {#available-stats-collectors .section}
#### Available Stats Collectors[¶](#available-stats-collectors "Permalink to this heading"){.headerlink}

Besides the basic [`StatsCollector`{.xref .py .py-class .docutils
.literal .notranslate}]{.pre} there are other Stats Collectors available
in Scrapy which extend the basic Stats Collector. You can select which
Stats Collector to use through the [[`STATS_CLASS`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-STATS_CLASS){.hoverxref
.tooltip .reference .internal} setting. The default Stats Collector used
is the [`MemoryStatsCollector`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}.

::: {#memorystatscollector .section}
##### MemoryStatsCollector[¶](#memorystatscollector "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.statscollectors.]{.pre}]{.sig-prename .descclassname}[[MemoryStatsCollector]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#MemoryStatsCollector){.reference .internal}[¶](#scrapy.statscollectors.MemoryStatsCollector "Permalink to this definition"){.headerlink}

:   A simple stats collector that keeps the stats of the last scraping
    run (for each spider) in memory, after they're closed. The stats can
    be accessed through the [[`spider_stats`{.xref .py .py-attr
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.statscollectors.MemoryStatsCollector.spider_stats "scrapy.statscollectors.MemoryStatsCollector.spider_stats"){.reference
    .internal} attribute, which is a dict keyed by spider domain name.

    This is the default Stats Collector used in Scrapy.

    [[spider_stats]{.pre}]{.sig-name .descname}[¶](#scrapy.statscollectors.MemoryStatsCollector.spider_stats "Permalink to this definition"){.headerlink}

    :   A dict of dicts (keyed by spider name) containing the stats of
        the last scraping run for each spider.
:::

::: {#dummystatscollector .section}
##### DummyStatsCollector[¶](#dummystatscollector "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.statscollectors.]{.pre}]{.sig-prename .descclassname}[[DummyStatsCollector]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#DummyStatsCollector){.reference .internal}[¶](#scrapy.statscollectors.DummyStatsCollector "Permalink to this definition"){.headerlink}

:   A Stats collector which does nothing but is very efficient (because
    it does nothing). This stats collector can be set via the
    [[`STATS_CLASS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-STATS_CLASS){.hoverxref
    .tooltip .reference .internal} setting, to disable stats collect in
    order to improve performance. However, the performance penalty of
    stats collection is usually marginal compared to other Scrapy
    workload like parsing pages.
:::
:::
:::

[]{#document-topics/email}

::: {#module-scrapy.mail .section}
[]{#sending-e-mail}[]{#topics-email}

### Sending e-mail[¶](#module-scrapy.mail "Permalink to this heading"){.headerlink}

Although Python makes sending e-mails relatively easy via the
[[`smtplib`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/smtplib.html#module-smtplib "(in Python v3.12)"){.reference
.external} library, Scrapy provides its own facility for sending e-mails
which is very easy to use and it's implemented using [[Twisted
non-blocking IO]{.xref .std
.std-doc}](https://docs.twisted.org/en/stable/core/howto/defer-intro.html "(in Twisted v23.10)"){.reference
.external}, to avoid interfering with the non-blocking IO of the
crawler. It also provides a simple API for sending attachments and it's
very easy to configure, with a few [[settings]{.std
.std-ref}](#topics-email-settings){.hoverxref .tooltip .reference
.internal}.

::: {#quick-example .section}
#### Quick example[¶](#quick-example "Permalink to this heading"){.headerlink}

There are two ways to instantiate the mail sender. You can instantiate
it using the standard [`__init__`{.docutils .literal
.notranslate}]{.pre} method:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.mail import MailSender

    mailer = MailSender()
:::
:::

Or you can instantiate it passing a Scrapy settings object, which will
respect the [[settings]{.std
.std-ref}](#topics-email-settings){.hoverxref .tooltip .reference
.internal}:

::: {.highlight-python .notranslate}
::: highlight
    mailer = MailSender.from_settings(settings)
:::
:::

And here is how to use it to send an e-mail (without attachments):

::: {.highlight-python .notranslate}
::: highlight
    mailer.send(
        to=["someone@example.com"],
        subject="Some subject",
        body="Some body",
        cc=["another@example.com"],
    )
:::
:::
:::

::: {#mailsender-class-reference .section}
#### MailSender class reference[¶](#mailsender-class-reference "Permalink to this heading"){.headerlink}

MailSender is the preferred class to use for sending emails from Scrapy,
as it uses [[Twisted non-blocking IO]{.xref .std
.std-doc}](https://docs.twisted.org/en/stable/core/howto/defer-intro.html "(in Twisted v23.10)"){.reference
.external}, like the rest of the framework.

*[class]{.pre}[ ]{.w}*[[scrapy.mail.]{.pre}]{.sig-prename .descclassname}[[MailSender]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[smtphost]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[mailfrom]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[smtpuser]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[smtppass]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[smtpport]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/mail.html#MailSender){.reference .internal}[¶](#scrapy.mail.MailSender "Permalink to this definition"){.headerlink}

:   

    Parameters

    :   -   **smtphost**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*bytes*](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
            .external}) -- the SMTP host to use for sending the emails.
            If omitted, the [[`MAIL_HOST`{.xref .std .std-setting
            .docutils .literal
            .notranslate}]{.pre}](#std-setting-MAIL_HOST){.hoverxref
            .tooltip .reference .internal} setting will be used.

        -   **mailfrom**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the address used to send emails (in the
            [`From:`{.docutils .literal .notranslate}]{.pre} header). If
            omitted, the [[`MAIL_FROM`{.xref .std .std-setting .docutils
            .literal
            .notranslate}]{.pre}](#std-setting-MAIL_FROM){.hoverxref
            .tooltip .reference .internal} setting will be used.

        -   **smtpuser** -- the SMTP user. If omitted, the
            [[`MAIL_USER`{.xref .std .std-setting .docutils .literal
            .notranslate}]{.pre}](#std-setting-MAIL_USER){.hoverxref
            .tooltip .reference .internal} setting will be used. If not
            given, no SMTP authentication will be performed.

        -   **smtppass**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*bytes*](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
            .external}) -- the SMTP pass for authentication.

        -   **smtpport**
            ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
            .external}) -- the SMTP port to connect to

        -   **smtptls**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- enforce using SMTP STARTTLS

        -   **smtpssl**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- enforce using a secure SSL connection

    *[classmethod]{.pre}[ ]{.w}*[[from_settings]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[settings]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/mail.html#MailSender.from_settings){.reference .internal}[¶](#scrapy.mail.MailSender.from_settings "Permalink to this definition"){.headerlink}

    :   Instantiate using a Scrapy settings object, which will respect
        [[these Scrapy settings]{.std
        .std-ref}](#topics-email-settings){.hoverxref .tooltip
        .reference .internal}.

        Parameters

        :   **settings** ([[`scrapy.settings.Settings`{.xref .py
            .py-class .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
            .internal} object) -- the e-mail recipients

    [[send]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[to]{.pre}]{.n}*, *[[subject]{.pre}]{.n}*, *[[body]{.pre}]{.n}*, *[[cc]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[attachs]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[mimetype]{.pre}]{.n}[[=]{.pre}]{.o}[[\'text/plain\']{.pre}]{.default_value}*, *[[charset]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/mail.html#MailSender.send){.reference .internal}[¶](#scrapy.mail.MailSender.send "Permalink to this definition"){.headerlink}

    :   Send email to the given recipients.

        Parameters

        :   -   **to**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
                .external}) -- the e-mail recipients as a string or as a
                list of strings

            -   **subject**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the subject of the e-mail

            -   **cc**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
                .external}) -- the e-mails to CC as a string or as a
                list of strings

            -   **body**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the e-mail body

            -   **attachs**
                ([*collections.abc.Iterable*](https://docs.python.org/3/library/collections.abc.html#collections.abc.Iterable "(in Python v3.12)"){.reference
                .external}) -- an iterable of tuples
                [`(attach_name,`{.docutils .literal
                .notranslate}]{.pre}` `{.docutils .literal
                .notranslate}[`mimetype,`{.docutils .literal
                .notranslate}]{.pre}` `{.docutils .literal
                .notranslate}[`file_object)`{.docutils .literal
                .notranslate}]{.pre} where [`attach_name`{.docutils
                .literal .notranslate}]{.pre} is a string with the name
                that will appear on the e-mail's attachment,
                [`mimetype`{.docutils .literal .notranslate}]{.pre} is
                the mimetype of the attachment and
                [`file_object`{.docutils .literal .notranslate}]{.pre}
                is a readable file object with the contents of the
                attachment

            -   **mimetype**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the MIME type of the e-mail

            -   **charset**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the character encoding to use for the
                e-mail contents
:::

::: {#mail-settings .section}
[]{#topics-email-settings}

#### Mail settings[¶](#mail-settings "Permalink to this heading"){.headerlink}

These settings define the default [`__init__`{.docutils .literal
.notranslate}]{.pre} method values of the [[`MailSender`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.mail.MailSender "scrapy.mail.MailSender"){.reference
.internal} class, and can be used to configure e-mail notifications in
your project without writing any code (for those extensions and code
that uses [[`MailSender`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.mail.MailSender "scrapy.mail.MailSender"){.reference
.internal}).

::: {#mail-from .section}
[]{#std-setting-MAIL_FROM}

##### MAIL_FROM[¶](#mail-from "Permalink to this heading"){.headerlink}

Default: [`'scrapy@localhost'`{.docutils .literal .notranslate}]{.pre}

Sender email to use ([`From:`{.docutils .literal .notranslate}]{.pre}
header) for sending emails.
:::

::: {#mail-host .section}
[]{#std-setting-MAIL_HOST}

##### MAIL_HOST[¶](#mail-host "Permalink to this heading"){.headerlink}

Default: [`'localhost'`{.docutils .literal .notranslate}]{.pre}

SMTP host to use for sending emails.
:::

::: {#mail-port .section}
[]{#std-setting-MAIL_PORT}

##### MAIL_PORT[¶](#mail-port "Permalink to this heading"){.headerlink}

Default: [`25`{.docutils .literal .notranslate}]{.pre}

SMTP port to use for sending emails.
:::

::: {#mail-user .section}
[]{#std-setting-MAIL_USER}

##### MAIL_USER[¶](#mail-user "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

User to use for SMTP authentication. If disabled no SMTP authentication
will be performed.
:::

::: {#mail-pass .section}
[]{#std-setting-MAIL_PASS}

##### MAIL_PASS[¶](#mail-pass "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

Password to use for SMTP authentication, along with [[`MAIL_USER`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-MAIL_USER){.hoverxref .tooltip
.reference .internal}.
:::

::: {#mail-tls .section}
[]{#std-setting-MAIL_TLS}

##### MAIL_TLS[¶](#mail-tls "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Enforce using STARTTLS. STARTTLS is a way to take an existing insecure
connection, and upgrade it to a secure connection using SSL/TLS.
:::

::: {#mail-ssl .section}
[]{#std-setting-MAIL_SSL}

##### MAIL_SSL[¶](#mail-ssl "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Enforce connecting using an SSL encrypted connection
:::
:::
:::

[]{#document-topics/telnetconsole}

::: {#telnet-console .section}
[]{#topics-telnetconsole}

### Telnet Console[¶](#telnet-console "Permalink to this heading"){.headerlink}

Scrapy comes with a built-in telnet console for inspecting and
controlling a Scrapy running process. The telnet console is just a
regular python shell running inside the Scrapy process, so you can do
literally anything from it.

The telnet console is a [[built-in Scrapy extension]{.std
.std-ref}](index.html#topics-extensions-ref){.hoverxref .tooltip
.reference .internal} which comes enabled by default, but you can also
disable it if you want. For more information about the extension itself
see [[Telnet console extension]{.std
.std-ref}](index.html#topics-extensions-ref-telnetconsole){.hoverxref
.tooltip .reference .internal}.

::: {.admonition .warning}
Warning

It is not secure to use telnet console via public networks, as telnet
doesn't provide any transport-layer security. Having username/password
authentication doesn't change that.

Intended usage is connecting to a running Scrapy spider locally (spider
process and telnet client are on the same machine) or over a secure
connection (VPN, SSH tunnel). Please avoid using telnet console over
insecure connections, or disable it completely using
[[`TELNETCONSOLE_ENABLED`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-TELNETCONSOLE_ENABLED){.hoverxref
.tooltip .reference .internal} option.
:::

::: {#how-to-access-the-telnet-console .section}
#### How to access the telnet console[¶](#how-to-access-the-telnet-console "Permalink to this heading"){.headerlink}

The telnet console listens in the TCP port defined in the
[[`TELNETCONSOLE_PORT`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-TELNETCONSOLE_PORT){.hoverxref
.tooltip .reference .internal} setting, which defaults to
[`6023`{.docutils .literal .notranslate}]{.pre}. To access the console
you need to type:

::: {.highlight-none .notranslate}
::: highlight
    telnet localhost 6023
    Trying localhost...
    Connected to localhost.
    Escape character is '^]'.
    Username:
    Password:
    >>>
:::
:::

By default Username is [`scrapy`{.docutils .literal .notranslate}]{.pre}
and Password is autogenerated. The autogenerated Password can be seen on
Scrapy logs like the example below:

::: {.highlight-none .notranslate}
::: highlight
    2018-10-16 14:35:21 [scrapy.extensions.telnet] INFO: Telnet Password: 16f92501e8a59326
:::
:::

Default Username and Password can be overridden by the settings
[[`TELNETCONSOLE_USERNAME`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-TELNETCONSOLE_USERNAME){.hoverxref
.tooltip .reference .internal} and [[`TELNETCONSOLE_PASSWORD`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-TELNETCONSOLE_PASSWORD){.hoverxref
.tooltip .reference .internal}.

::: {.admonition .warning}
Warning

Username and password provide only a limited protection, as telnet is
not using secure transport - by default traffic is not encrypted even if
username and password are set.
:::

You need the telnet program which comes installed by default in Windows,
and most Linux distros.
:::

::: {#available-variables-in-the-telnet-console .section}
#### Available variables in the telnet console[¶](#available-variables-in-the-telnet-console "Permalink to this heading"){.headerlink}

The telnet console is like a regular Python shell running inside the
Scrapy process, so you can do anything from it including importing new
modules, etc.

However, the telnet console comes with some default variables defined
for convenience:

+------------+---------------------------------------------------------+
| Shortcut   | Description                                             |
+============+=========================================================+
| [`crawler` | the Scrapy Crawler ([[`scrapy.crawler.Crawler`{.xref    |
| {.docutils | .py .py-class .docutils .literal                        |
| .literal   | .notranslate}]{.pre}](index.html#scra                   |
| .notransla | py.crawler.Crawler "scrapy.crawler.Crawler"){.reference |
| te}]{.pre} | .internal} object)                                      |
+------------+---------------------------------------------------------+
| [`engine`  | Crawler.engine attribute                                |
| {.docutils |                                                         |
| .literal   |                                                         |
| .notransla |                                                         |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [`spider`  | the active spider                                       |
| {.docutils |                                                         |
| .literal   |                                                         |
| .notransla |                                                         |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [`slot`    | the engine slot                                         |
| {.docutils |                                                         |
| .literal   |                                                         |
| .notransla |                                                         |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [`e        | the Extension Manager (Crawler.extensions attribute)    |
| xtensions` |                                                         |
| {.docutils |                                                         |
| .literal   |                                                         |
| .notransla |                                                         |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [`stats`   | the Stats Collector (Crawler.stats attribute)           |
| {.docutils |                                                         |
| .literal   |                                                         |
| .notransla |                                                         |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [          | the Scrapy settings object (Crawler.settings attribute) |
| `settings` |                                                         |
| {.docutils |                                                         |
| .literal   |                                                         |
| .notransla |                                                         |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [`est`     | print a report of the engine status                     |
| {.docutils |                                                         |
| .literal   |                                                         |
| .notransla |                                                         |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [`prefs`   | for memory debugging (see [[Debugging memory            |
| {.docutils | leaks]{.std                                             |
| .literal   | .std-ref}](index.html#topics-leaks){.hoverxref .tooltip |
| .notransla | .reference .internal})                                  |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
| [`p`       | a shortcut to the [[`pprint.pprint()`{.xref .py         |
| {.docutils | .py-func .docutils .literal                             |
| .literal   | .no                                                     |
| .notransla | translate}]{.pre}](https://docs.python.org/3/library/pp |
| te}]{.pre} | rint.html#pprint.pprint "(in Python v3.12)"){.reference |
|            | .external} function                                     |
+------------+---------------------------------------------------------+
| [`hpy`     | for memory debugging (see [[Debugging memory            |
| {.docutils | leaks]{.std                                             |
| .literal   | .std-ref}](index.html#topics-leaks){.hoverxref .tooltip |
| .notransla | .reference .internal})                                  |
| te}]{.pre} |                                                         |
+------------+---------------------------------------------------------+
:::

::: {#telnet-console-usage-examples .section}
#### Telnet console usage examples[¶](#telnet-console-usage-examples "Permalink to this heading"){.headerlink}

Here are some example tasks you can do with the telnet console:

::: {#view-engine-status .section}
##### View engine status[¶](#view-engine-status "Permalink to this heading"){.headerlink}

You can use the [`est()`{.docutils .literal .notranslate}]{.pre} method
of the Scrapy engine to quickly show its state using the telnet console:

::: {.highlight-none .notranslate}
::: highlight
    telnet localhost 6023
    >>> est()
    Execution engine status

    time()-engine.start_time                        : 8.62972998619
    len(engine.downloader.active)                   : 16
    engine.scraper.is_idle()                        : False
    engine.spider.name                              : followall
    engine.spider_is_idle()                         : False
    engine.slot.closing                             : False
    len(engine.slot.inprogress)                     : 16
    len(engine.slot.scheduler.dqs or [])            : 0
    len(engine.slot.scheduler.mqs)                  : 92
    len(engine.scraper.slot.queue)                  : 0
    len(engine.scraper.slot.active)                 : 0
    engine.scraper.slot.active_size                 : 0
    engine.scraper.slot.itemproc_size               : 0
    engine.scraper.slot.needs_backout()             : False
:::
:::
:::

::: {#pause-resume-and-stop-the-scrapy-engine .section}
##### Pause, resume and stop the Scrapy engine[¶](#pause-resume-and-stop-the-scrapy-engine "Permalink to this heading"){.headerlink}

To pause:

::: {.highlight-none .notranslate}
::: highlight
    telnet localhost 6023
    >>> engine.pause()
    >>>
:::
:::

To resume:

::: {.highlight-none .notranslate}
::: highlight
    telnet localhost 6023
    >>> engine.unpause()
    >>>
:::
:::

To stop:

::: {.highlight-none .notranslate}
::: highlight
    telnet localhost 6023
    >>> engine.stop()
    Connection closed by foreign host.
:::
:::
:::
:::

::: {#telnet-console-signals .section}
#### Telnet Console signals[¶](#telnet-console-signals "Permalink to this heading"){.headerlink}

[]{#std-signal-update_telnet_vars .target}

[[scrapy.extensions.telnet.]{.pre}]{.sig-prename .descclassname}[[update_telnet_vars]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[telnet_vars]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.extensions.telnet.update_telnet_vars "Permalink to this definition"){.headerlink}

:   Sent just before the telnet console is opened. You can hook up to
    this signal to add, remove or update the variables that will be
    available in the telnet local namespace. In order to do that, you
    need to update the [`telnet_vars`{.docutils .literal
    .notranslate}]{.pre} dict in your handler.

    Parameters

    :   **telnet_vars**
        ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
        .external}) -- the dict of telnet variables
:::

::: {#telnet-settings .section}
#### Telnet settings[¶](#telnet-settings "Permalink to this heading"){.headerlink}

These are the settings that control the telnet console's behaviour:

::: {#telnetconsole-port .section}
[]{#std-setting-TELNETCONSOLE_PORT}

##### TELNETCONSOLE_PORT[¶](#telnetconsole-port "Permalink to this heading"){.headerlink}

Default: [`[6023,`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`6073]`{.docutils .literal .notranslate}]{.pre}

The port range to use for the telnet console. If set to
[`None`{.docutils .literal .notranslate}]{.pre} or [`0`{.docutils
.literal .notranslate}]{.pre}, a dynamically assigned port is used.
:::

::: {#telnetconsole-host .section}
[]{#std-setting-TELNETCONSOLE_HOST}

##### TELNETCONSOLE_HOST[¶](#telnetconsole-host "Permalink to this heading"){.headerlink}

Default: [`'127.0.0.1'`{.docutils .literal .notranslate}]{.pre}

The interface the telnet console should listen on
:::

::: {#telnetconsole-username .section}
[]{#std-setting-TELNETCONSOLE_USERNAME}

##### TELNETCONSOLE_USERNAME[¶](#telnetconsole-username "Permalink to this heading"){.headerlink}

Default: [`'scrapy'`{.docutils .literal .notranslate}]{.pre}

The username used for the telnet console
:::

::: {#telnetconsole-password .section}
[]{#std-setting-TELNETCONSOLE_PASSWORD}

##### TELNETCONSOLE_PASSWORD[¶](#telnetconsole-password "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The password used for the telnet console, default behaviour is to have
it autogenerated
:::
:::
:::
:::

[[Logging]{.doc}](index.html#document-topics/logging){.reference .internal}

:   Learn how to use Python's builtin logging on Scrapy.

[[Stats Collection]{.doc}](index.html#document-topics/stats){.reference .internal}

:   Collect statistics about your scraping crawler.

[[Sending e-mail]{.doc}](index.html#document-topics/email){.reference .internal}

:   Send email notifications when certain events occur.

[[Telnet Console]{.doc}](index.html#document-topics/telnetconsole){.reference .internal}

:   Inspect a running crawler using a built-in Python console.
:::

::: {#solving-specific-problems .section}
## Solving specific problems[¶](#solving-specific-problems "Permalink to this heading"){.headerlink}

::: {.toctree-wrapper .compound}
[]{#document-faq}

::: {#frequently-asked-questions .section}
[]{#faq}

### Frequently Asked Questions[¶](#frequently-asked-questions "Permalink to this heading"){.headerlink}

::: {#how-does-scrapy-compare-to-beautifulsoup-or-lxml .section}
[]{#faq-scrapy-bs-cmp}

#### How does Scrapy compare to BeautifulSoup or lxml?[¶](#how-does-scrapy-compare-to-beautifulsoup-or-lxml "Permalink to this heading"){.headerlink}

[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){.reference
.external} and [lxml](https://lxml.de/){.reference .external} are
libraries for parsing HTML and XML. Scrapy is an application framework
for writing web spiders that crawl web sites and extract data from them.

Scrapy provides a built-in mechanism for extracting data (called
[[selectors]{.std .std-ref}](index.html#topics-selectors){.hoverxref
.tooltip .reference .internal}) but you can easily use
[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){.reference
.external} (or [lxml](https://lxml.de/){.reference .external}) instead,
if you feel more comfortable working with them. After all, they're just
parsing libraries which can be imported and used from any Python code.

In other words, comparing
[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){.reference
.external} (or [lxml](https://lxml.de/){.reference .external}) to Scrapy
is like comparing
[jinja2](https://palletsprojects.com/p/jinja/){.reference .external} to
[Django](https://www.djangoproject.com/){.reference .external}.
:::

::: {#can-i-use-scrapy-with-beautifulsoup .section}
#### Can I use Scrapy with BeautifulSoup?[¶](#can-i-use-scrapy-with-beautifulsoup "Permalink to this heading"){.headerlink}

Yes, you can. As mentioned [[above]{.std
.std-ref}](#faq-scrapy-bs-cmp){.hoverxref .tooltip .reference
.internal},
[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){.reference
.external} can be used for parsing HTML responses in Scrapy callbacks.
You just have to feed the response's body into a
[`BeautifulSoup`{.docutils .literal .notranslate}]{.pre} object and
extract whatever data you need from it.

Here's an example spider using BeautifulSoup API, with [`lxml`{.docutils
.literal .notranslate}]{.pre} as the HTML parser:

::: {.highlight-python .notranslate}
::: highlight
    from bs4 import BeautifulSoup
    import scrapy


    class ExampleSpider(scrapy.Spider):
        name = "example"
        allowed_domains = ["example.com"]
        start_urls = ("http://www.example.com/",)

        def parse(self, response):
            # use lxml to get decent HTML parsing speed
            soup = BeautifulSoup(response.text, "lxml")
            yield {"url": response.url, "title": soup.h1.string}
:::
:::

::: {.admonition .note}
Note

[`BeautifulSoup`{.docutils .literal .notranslate}]{.pre} supports
several HTML/XML parsers. See [BeautifulSoup's official
documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#specifying-the-parser-to-use){.reference
.external} on which ones are available.
:::
:::

::: {#did-scrapy-steal-x-from-django .section}
#### Did Scrapy "steal" X from Django?[¶](#did-scrapy-steal-x-from-django "Permalink to this heading"){.headerlink}

Probably, but we don't like that word. We think
[Django](https://www.djangoproject.com/){.reference .external} is a
great open source project and an example to follow, so we've used it as
an inspiration for Scrapy.

We believe that, if something is already done well, there's no need to
reinvent it. This concept, besides being one of the foundations for open
source and free software, not only applies to software but also to
documentation, procedures, policies, etc. So, instead of going through
each problem ourselves, we choose to copy ideas from those projects that
have already solved them properly, and focus on the real problems we
need to solve.

We'd be proud if Scrapy serves as an inspiration for other projects.
Feel free to steal from us!
:::

::: {#does-scrapy-work-with-http-proxies .section}
#### Does Scrapy work with HTTP proxies?[¶](#does-scrapy-work-with-http-proxies "Permalink to this heading"){.headerlink}

Yes. Support for HTTP proxies is provided (since Scrapy 0.8) through the
HTTP Proxy downloader middleware. See [[`HttpProxyMiddleware`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware"){.reference
.internal}.
:::

::: {#how-can-i-scrape-an-item-with-attributes-in-different-pages .section}
#### How can I scrape an item with attributes in different pages?[¶](#how-can-i-scrape-an-item-with-attributes-in-different-pages "Permalink to this heading"){.headerlink}

See [[Passing additional data to callback functions]{.std
.std-ref}](index.html#topics-request-response-ref-request-callback-arguments){.hoverxref
.tooltip .reference .internal}.
:::

::: {#how-can-i-simulate-a-user-login-in-my-spider .section}
#### How can I simulate a user login in my spider?[¶](#how-can-i-simulate-a-user-login-in-my-spider "Permalink to this heading"){.headerlink}

See [[Using FormRequest.from_response() to simulate a user login]{.std
.std-ref}](index.html#topics-request-response-ref-request-userlogin){.hoverxref
.tooltip .reference .internal}.
:::

::: {#does-scrapy-crawl-in-breadth-first-or-depth-first-order .section}
[]{#faq-bfo-dfo}

#### Does Scrapy crawl in breadth-first or depth-first order?[¶](#does-scrapy-crawl-in-breadth-first-or-depth-first-order "Permalink to this heading"){.headerlink}

By default, Scrapy uses a
[LIFO](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)){.reference
.external} queue for storing pending requests, which basically means
that it crawls in [DFO
order](https://en.wikipedia.org/wiki/Depth-first_search){.reference
.external}. This order is more convenient in most cases.

If you do want to crawl in true [BFO
order](https://en.wikipedia.org/wiki/Breadth-first_search){.reference
.external}, you can do it by setting the following settings:

::: {.highlight-python .notranslate}
::: highlight
    DEPTH_PRIORITY = 1
    SCHEDULER_DISK_QUEUE = "scrapy.squeues.PickleFifoDiskQueue"
    SCHEDULER_MEMORY_QUEUE = "scrapy.squeues.FifoMemoryQueue"
:::
:::

While pending requests are below the configured values of
[[`CONCURRENT_REQUESTS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS){.hoverxref
.tooltip .reference .internal}, [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} or [[`CONCURRENT_REQUESTS_PER_IP`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal}, those requests are sent concurrently. As
a result, the first few requests of a crawl rarely follow the desired
order. Lowering those settings to [`1`{.docutils .literal
.notranslate}]{.pre} enforces the desired order, but it significantly
slows down the crawl as a whole.
:::

::: {#my-scrapy-crawler-has-memory-leaks-what-can-i-do .section}
#### My Scrapy crawler has memory leaks. What can I do?[¶](#my-scrapy-crawler-has-memory-leaks-what-can-i-do "Permalink to this heading"){.headerlink}

See [[Debugging memory leaks]{.std
.std-ref}](index.html#topics-leaks){.hoverxref .tooltip .reference
.internal}.

Also, Python has a builtin memory leak issue which is described in
[[Leaks without leaks]{.std
.std-ref}](index.html#topics-leaks-without-leaks){.hoverxref .tooltip
.reference .internal}.
:::

::: {#how-can-i-make-scrapy-consume-less-memory .section}
#### How can I make Scrapy consume less memory?[¶](#how-can-i-make-scrapy-consume-less-memory "Permalink to this heading"){.headerlink}

See previous question.
:::

::: {#how-can-i-prevent-memory-errors-due-to-many-allowed-domains .section}
#### How can I prevent memory errors due to many allowed domains?[¶](#how-can-i-prevent-memory-errors-due-to-many-allowed-domains "Permalink to this heading"){.headerlink}

If you have a spider with a long list of [[`allowed_domains`{.xref .py
.py-attr .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.allowed_domains "scrapy.Spider.allowed_domains"){.reference
.internal} (e.g. 50,000+), consider replacing the default
[[`OffsiteMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.offsite.OffsiteMiddleware "scrapy.spidermiddlewares.offsite.OffsiteMiddleware"){.reference
.internal} spider middleware with a [[custom spider middleware]{.std
.std-ref}](index.html#custom-spider-middleware){.hoverxref .tooltip
.reference .internal} that requires less memory. For example:

-   If your domain names are similar enough, use your own regular
    expression instead joining the strings in [[`allowed_domains`{.xref
    .py .py-attr .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.allowed_domains "scrapy.Spider.allowed_domains"){.reference
    .internal} into a complex regular expression.

-   If you can [meet the installation
    requirements](https://github.com/andreasvc/pyre2#installation){.reference
    .external}, use
    [pyre2](https://github.com/andreasvc/pyre2){.reference .external}
    instead of Python's
    [re](https://docs.python.org/library/re.html){.reference .external}
    to compile your URL-filtering regular expression. See [issue
    1908](https://github.com/scrapy/scrapy/issues/1908){.reference
    .external}.

See also other suggestions at
[StackOverflow](https://stackoverflow.com/q/36440681/939364){.reference
.external}.

::: {.admonition .note}
Note

Remember to disable
[[`scrapy.spidermiddlewares.offsite.OffsiteMiddleware`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.offsite.OffsiteMiddleware "scrapy.spidermiddlewares.offsite.OffsiteMiddleware"){.reference
.internal} when you enable your custom implementation:

::: {.highlight-python .notranslate}
::: highlight
    SPIDER_MIDDLEWARES = {
        "scrapy.spidermiddlewares.offsite.OffsiteMiddleware": None,
        "myproject.middlewares.CustomOffsiteMiddleware": 500,
    }
:::
:::
:::
:::

::: {#can-i-use-basic-http-authentication-in-my-spiders .section}
#### Can I use Basic HTTP Authentication in my spiders?[¶](#can-i-use-basic-http-authentication-in-my-spiders "Permalink to this heading"){.headerlink}

Yes, see [[`HttpAuthMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware "scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware"){.reference
.internal}.
:::

::: {#why-does-scrapy-download-pages-in-english-instead-of-my-native-language .section}
#### Why does Scrapy download pages in English instead of my native language?[¶](#why-does-scrapy-download-pages-in-english-instead-of-my-native-language "Permalink to this heading"){.headerlink}

Try changing the default
[Accept-Language](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4){.reference
.external} request header by overriding the
[[`DEFAULT_REQUEST_HEADERS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DEFAULT_REQUEST_HEADERS){.hoverxref
.tooltip .reference .internal} setting.
:::

::: {#where-can-i-find-some-example-scrapy-projects .section}
#### Where can I find some example Scrapy projects?[¶](#where-can-i-find-some-example-scrapy-projects "Permalink to this heading"){.headerlink}

See [[Examples]{.std .std-ref}](index.html#intro-examples){.hoverxref
.tooltip .reference .internal}.
:::

::: {#can-i-run-a-spider-without-creating-a-project .section}
#### Can I run a spider without creating a project?[¶](#can-i-run-a-spider-without-creating-a-project "Permalink to this heading"){.headerlink}

Yes. You can use the [[`runspider`{.xref .std .std-command .docutils
.literal
.notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
.tooltip .reference .internal} command. For example, if you have a
spider written in a [`my_spider.py`{.docutils .literal
.notranslate}]{.pre} file you can run it with:

::: {.highlight-default .notranslate}
::: highlight
    scrapy runspider my_spider.py
:::
:::

See [[`runspider`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-runspider){.hoverxref
.tooltip .reference .internal} command for more info.
:::

::: {#i-get-filtered-offsite-request-messages-how-can-i-fix-them .section}
#### I get "Filtered offsite request" messages. How can I fix them?[¶](#i-get-filtered-offsite-request-messages-how-can-i-fix-them "Permalink to this heading"){.headerlink}

Those messages (logged with [`DEBUG`{.docutils .literal
.notranslate}]{.pre} level) don't necessarily mean there is a problem,
so you may not need to fix them.

Those messages are thrown by the Offsite Spider Middleware, which is a
spider middleware (enabled by default) whose purpose is to filter out
requests to domains outside the ones covered by the spider.

For more info see: [[`OffsiteMiddleware`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.offsite.OffsiteMiddleware "scrapy.spidermiddlewares.offsite.OffsiteMiddleware"){.reference
.internal}.
:::

::: {#what-is-the-recommended-way-to-deploy-a-scrapy-crawler-in-production .section}
#### What is the recommended way to deploy a Scrapy crawler in production?[¶](#what-is-the-recommended-way-to-deploy-a-scrapy-crawler-in-production "Permalink to this heading"){.headerlink}

See [[Deploying Spiders]{.std
.std-ref}](index.html#topics-deploy){.hoverxref .tooltip .reference
.internal}.
:::

::: {#can-i-use-json-for-large-exports .section}
#### Can I use JSON for large exports?[¶](#can-i-use-json-for-large-exports "Permalink to this heading"){.headerlink}

It'll depend on how large your output is. See [[this warning]{.std
.std-ref}](index.html#json-with-large-data){.hoverxref .tooltip
.reference .internal} in [[`JsonItemExporter`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exporters.JsonItemExporter "scrapy.exporters.JsonItemExporter"){.reference
.internal} documentation.
:::

::: {#can-i-return-twisted-deferreds-from-signal-handlers .section}
#### Can I return (Twisted) deferreds from signal handlers?[¶](#can-i-return-twisted-deferreds-from-signal-handlers "Permalink to this heading"){.headerlink}

Some signals support returning deferreds from their handlers, others
don't. See the [[Built-in signals reference]{.std
.std-ref}](index.html#topics-signals-ref){.hoverxref .tooltip .reference
.internal} to know which ones.
:::

::: {#what-does-the-response-status-code-999-mean .section}
#### What does the response status code 999 mean?[¶](#what-does-the-response-status-code-999-mean "Permalink to this heading"){.headerlink}

999 is a custom response status code used by Yahoo sites to throttle
requests. Try slowing down the crawling speed by using a download delay
of [`2`{.docutils .literal .notranslate}]{.pre} (or higher) in your
spider:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.spiders import CrawlSpider


    class MySpider(CrawlSpider):
        name = "myspider"

        download_delay = 2

        # [ ... rest of the spider code ... ]
:::
:::

Or by setting a global download delay in your project with the
[[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_DELAY){.hoverxref
.tooltip .reference .internal} setting.
:::

::: {#can-i-call-pdb-set-trace-from-my-spiders-to-debug-them .section}
#### Can I call [`pdb.set_trace()`{.docutils .literal .notranslate}]{.pre} from my spiders to debug them?[¶](#can-i-call-pdb-set-trace-from-my-spiders-to-debug-them "Permalink to this heading"){.headerlink}

Yes, but you can also use the Scrapy shell which allows you to quickly
analyze (and even modify) the response being processed by your spider,
which is, quite often, more useful than plain old
[`pdb.set_trace()`{.docutils .literal .notranslate}]{.pre}.

For more info see [[Invoking the shell from spiders to inspect
responses]{.std
.std-ref}](index.html#topics-shell-inspect-response){.hoverxref .tooltip
.reference .internal}.
:::

::: {#simplest-way-to-dump-all-my-scraped-items-into-a-json-csv-xml-file .section}
#### Simplest way to dump all my scraped items into a JSON/CSV/XML file?[¶](#simplest-way-to-dump-all-my-scraped-items-into-a-json-csv-xml-file "Permalink to this heading"){.headerlink}

To dump into a JSON file:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl myspider -O items.json
:::
:::

To dump into a CSV file:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl myspider -O items.csv
:::
:::

To dump into a XML file:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl myspider -O items.xml
:::
:::

For more information see [[Feed exports]{.std
.std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
.reference .internal}
:::

::: {#what-s-this-huge-cryptic-viewstate-parameter-used-in-some-forms .section}
#### What's this huge cryptic [`__VIEWSTATE`{.docutils .literal .notranslate}]{.pre} parameter used in some forms?[¶](#what-s-this-huge-cryptic-viewstate-parameter-used-in-some-forms "Permalink to this heading"){.headerlink}

The [`__VIEWSTATE`{.docutils .literal .notranslate}]{.pre} parameter is
used in sites built with ASP.NET/VB.NET. For more info on how it works
see [this
page](https://metacpan.org/pod/release/ECARROLL/HTML-TreeBuilderX-ASP_NET-0.09/lib/HTML/TreeBuilderX/ASP_NET.pm){.reference
.external}. Also, here's an [example
spider](https://github.com/AmbientLighter/rpn-fas/blob/master/fas/spiders/rnp.py){.reference
.external} which scrapes one of these sites.
:::

::: {#what-s-the-best-way-to-parse-big-xml-csv-data-feeds .section}
#### What's the best way to parse big XML/CSV data feeds?[¶](#what-s-the-best-way-to-parse-big-xml-csv-data-feeds "Permalink to this heading"){.headerlink}

Parsing big feeds with XPath selectors can be problematic since they
need to build the DOM of the entire feed in memory, and this can be
quite slow and consume a lot of memory.

In order to avoid parsing all the entire feed at once in memory, you can
use the functions [`xmliter`{.docutils .literal .notranslate}]{.pre} and
[`csviter`{.docutils .literal .notranslate}]{.pre} from
[`scrapy.utils.iterators`{.docutils .literal .notranslate}]{.pre}
module. In fact, this is what the feed spiders (see [[Spiders]{.std
.std-ref}](index.html#topics-spiders){.hoverxref .tooltip .reference
.internal}) use under the cover.
:::

::: {#does-scrapy-manage-cookies-automatically .section}
#### Does Scrapy manage cookies automatically?[¶](#does-scrapy-manage-cookies-automatically "Permalink to this heading"){.headerlink}

Yes, Scrapy receives and keeps track of cookies sent by servers, and
sends them back on subsequent requests, like any regular web browser
does.

For more info see [[Requests and Responses]{.std
.std-ref}](index.html#topics-request-response){.hoverxref .tooltip
.reference .internal} and [[CookiesMiddleware]{.std
.std-ref}](index.html#cookies-mw){.hoverxref .tooltip .reference
.internal}.
:::

::: {#how-can-i-see-the-cookies-being-sent-and-received-from-scrapy .section}
#### How can I see the cookies being sent and received from Scrapy?[¶](#how-can-i-see-the-cookies-being-sent-and-received-from-scrapy "Permalink to this heading"){.headerlink}

Enable the [[`COOKIES_DEBUG`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-COOKIES_DEBUG){.hoverxref
.tooltip .reference .internal} setting.
:::

::: {#how-can-i-instruct-a-spider-to-stop-itself .section}
#### How can I instruct a spider to stop itself?[¶](#how-can-i-instruct-a-spider-to-stop-itself "Permalink to this heading"){.headerlink}

Raise the [[`CloseSpider`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.CloseSpider "scrapy.exceptions.CloseSpider"){.reference
.internal} exception from a callback. For more info see:
[[`CloseSpider`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.CloseSpider "scrapy.exceptions.CloseSpider"){.reference
.internal}.
:::

::: {#how-can-i-prevent-my-scrapy-bot-from-getting-banned .section}
#### How can I prevent my Scrapy bot from getting banned?[¶](#how-can-i-prevent-my-scrapy-bot-from-getting-banned "Permalink to this heading"){.headerlink}

See [[Avoiding getting banned]{.std
.std-ref}](index.html#bans){.hoverxref .tooltip .reference .internal}.
:::

::: {#should-i-use-spider-arguments-or-settings-to-configure-my-spider .section}
#### Should I use spider arguments or settings to configure my spider?[¶](#should-i-use-spider-arguments-or-settings-to-configure-my-spider "Permalink to this heading"){.headerlink}

Both [[spider arguments]{.std
.std-ref}](index.html#spiderargs){.hoverxref .tooltip .reference
.internal} and [[settings]{.std
.std-ref}](index.html#topics-settings){.hoverxref .tooltip .reference
.internal} can be used to configure your spider. There is no strict rule
that mandates to use one or the other, but settings are more suited for
parameters that, once set, don't change much, while spider arguments are
meant to change more often, even on each spider run and sometimes are
required for the spider to run at all (for example, to set the start url
of a spider).

To illustrate with an example, assuming you have a spider that needs to
log into a site to scrape data, and you only want to scrape data from a
certain section of the site (which varies each time). In that case, the
credentials to log in would be settings, while the url of the section to
scrape would be a spider argument.
:::

::: {#i-m-scraping-a-xml-document-and-my-xpath-selector-doesn-t-return-any-items .section}
#### I'm scraping a XML document and my XPath selector doesn't return any items[¶](#i-m-scraping-a-xml-document-and-my-xpath-selector-doesn-t-return-any-items "Permalink to this heading"){.headerlink}

You may need to remove namespaces. See [[Removing namespaces]{.std
.std-ref}](index.html#removing-namespaces){.hoverxref .tooltip
.reference .internal}.
:::

::: {#how-to-split-an-item-into-multiple-items-in-an-item-pipeline .section}
[]{#faq-split-item}

#### How to split an item into multiple items in an item pipeline?[¶](#how-to-split-an-item-into-multiple-items-in-an-item-pipeline "Permalink to this heading"){.headerlink}

[[Item pipelines]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal} cannot yield multiple items per input item.
[[Create a spider middleware]{.std
.std-ref}](index.html#custom-spider-middleware){.hoverxref .tooltip
.reference .internal} instead, and use its
[[`process_spider_output()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
.internal} method for this purpose. For example:

::: {.highlight-python .notranslate}
::: highlight
    from copy import deepcopy

    from itemadapter import is_item, ItemAdapter


    class MultiplyItemsMiddleware:
        def process_spider_output(self, response, result, spider):
            for item in result:
                if is_item(item):
                    adapter = ItemAdapter(item)
                    for _ in range(adapter["multiply_by"]):
                        yield deepcopy(item)
:::
:::
:::

::: {#does-scrapy-support-ipv6-addresses .section}
#### Does Scrapy support IPv6 addresses?[¶](#does-scrapy-support-ipv6-addresses "Permalink to this heading"){.headerlink}

Yes, by setting [[`DNS_RESOLVER`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DNS_RESOLVER){.hoverxref
.tooltip .reference .internal} to
[`scrapy.resolver.CachingHostnameResolver`{.docutils .literal
.notranslate}]{.pre}. Note that by doing so, you lose the ability to set
a specific timeout for DNS requests (the value of the
[[`DNS_TIMEOUT`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DNS_TIMEOUT){.hoverxref
.tooltip .reference .internal} setting is ignored).
:::

::: {#how-to-deal-with-class-valueerror-filedescriptor-out-of-range-in-select-exceptions .section}
[]{#faq-specific-reactor}

#### How to deal with [`<class`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`'ValueError'>:`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`filedescriptor`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`out`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`of`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`range`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`in`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`select()`{.docutils .literal .notranslate}]{.pre} exceptions?[¶](#how-to-deal-with-class-valueerror-filedescriptor-out-of-range-in-select-exceptions "Permalink to this heading"){.headerlink}

This issue [has been
reported](https://github.com/scrapy/scrapy/issues/2905){.reference
.external} to appear when running broad crawls in macOS, where the
default Twisted reactor is
[[`twisted.internet.selectreactor.SelectReactor`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.selectreactor.SelectReactor.html "(in Twisted)"){.reference
.external}. Switching to a different reactor is possible by using the
[[`TWISTED_REACTOR`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-TWISTED_REACTOR){.hoverxref
.tooltip .reference .internal} setting.
:::

::: {#how-can-i-cancel-the-download-of-a-given-response .section}
[]{#faq-stop-response-download}

#### How can I cancel the download of a given response?[¶](#how-can-i-cancel-the-download-of-a-given-response "Permalink to this heading"){.headerlink}

In some situations, it might be useful to stop the download of a certain
response. For instance, sometimes you can determine whether or not you
need the full contents of a response by inspecting its headers or the
first bytes of its body. In that case, you could save resources by
attaching a handler to the [[`bytes_received`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.signals.bytes_received "scrapy.signals.bytes_received"){.reference
.internal} or [[`headers_received`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.signals.headers_received "scrapy.signals.headers_received"){.reference
.internal} signals and raising a [[`StopDownload`{.xref .py .py-exc
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.StopDownload "scrapy.exceptions.StopDownload"){.reference
.internal} exception. Please refer to the [[Stopping the download of a
Response]{.std
.std-ref}](index.html#topics-stop-response-download){.hoverxref .tooltip
.reference .internal} topic for additional information and examples.
:::

::: {#running-runspider-i-get-error-no-spider-found-in-file-filename .section}
#### Running [`runspider`{.docutils .literal .notranslate}]{.pre} I get [`error:`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`No`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`spider`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`found`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`in`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`file:`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal .notranslate}[`<filename>`{.docutils .literal .notranslate}]{.pre}[¶](#running-runspider-i-get-error-no-spider-found-in-file-filename "Permalink to this heading"){.headerlink}

This may happen if your Scrapy project has a spider module with a name
that conflicts with the name of one of the [Python standard library
modules](https://docs.python.org/py-modindex.html){.reference
.external}, such as [`csv.py`{.docutils .literal .notranslate}]{.pre} or
[`os.py`{.docutils .literal .notranslate}]{.pre}, or any [Python
package](https://pypi.org/){.reference .external} that you have
installed. See [issue
2680](https://github.com/scrapy/scrapy/issues/2680){.reference
.external}.
:::
:::

[]{#document-topics/debug}

::: {#debugging-spiders .section}
[]{#topics-debug}

### Debugging Spiders[¶](#debugging-spiders "Permalink to this heading"){.headerlink}

This document explains the most common techniques for debugging spiders.
Consider the following Scrapy spider below:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy
    from myproject.items import MyItem


    class MySpider(scrapy.Spider):
        name = "myspider"
        start_urls = (
            "http://example.com/page1",
            "http://example.com/page2",
        )

        def parse(self, response):
            # <processing code not shown>
            # collect `item_urls`
            for item_url in item_urls:
                yield scrapy.Request(item_url, self.parse_item)

        def parse_item(self, response):
            # <processing code not shown>
            item = MyItem()
            # populate `item` fields
            # and extract item_details_url
            yield scrapy.Request(
                item_details_url, self.parse_details, cb_kwargs={"item": item}
            )

        def parse_details(self, response, item):
            # populate more `item` fields
            return item
:::
:::

Basically this is a simple spider which parses two pages of items (the
start_urls). Items also have a details page with additional information,
so we use the [`cb_kwargs`{.docutils .literal .notranslate}]{.pre}
functionality of [`Request`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} to pass a partially populated item.

::: {#parse-command .section}
#### Parse Command[¶](#parse-command "Permalink to this heading"){.headerlink}

The most basic way of checking the output of your spider is to use the
[[`parse`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-parse){.hoverxref .tooltip
.reference .internal} command. It allows to check the behaviour of
different parts of the spider at the method level. It has the advantage
of being flexible and simple to use, but does not allow debugging code
inside a method.

In order to see the item scraped from a specific url:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy parse --spider=myspider -c parse_item -d 2 <item_url>
    [ ... scrapy log lines crawling example.com spider ... ]

    >>> STATUS DEPTH LEVEL 2 <<<
    # Scraped Items  ------------------------------------------------------------
    [{'url': <item_url>}]

    # Requests  -----------------------------------------------------------------
    []
:::
:::

Using the [`--verbose`{.docutils .literal .notranslate}]{.pre} or
[`-v`{.docutils .literal .notranslate}]{.pre} option we can see the
status at each depth level:

::: {.highlight-none .notranslate}
::: highlight
    $ scrapy parse --spider=myspider -c parse_item -d 2 -v <item_url>
    [ ... scrapy log lines crawling example.com spider ... ]

    >>> DEPTH LEVEL: 1 <<<
    # Scraped Items  ------------------------------------------------------------
    []

    # Requests  -----------------------------------------------------------------
    [<GET item_details_url>]


    >>> DEPTH LEVEL: 2 <<<
    # Scraped Items  ------------------------------------------------------------
    [{'url': <item_url>}]

    # Requests  -----------------------------------------------------------------
    []
:::