        -   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal} object) -- the response from where the item was
            scraped
:::

::: {#item-dropped .section}
###### item_dropped[¶](#item-dropped "Permalink to this heading"){.headerlink}

[]{#std-signal-item_dropped .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[item_dropped]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}*, *[[response]{.pre}]{.n}*, *[[exception]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.item_dropped "Permalink to this definition"){.headerlink}

:   Sent after an item has been dropped from the [[Item Pipeline]{.std
    .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
    .reference .internal} when some stage raised a [[`DropItem`{.xref
    .py .py-exc .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.DropItem "scrapy.exceptions.DropItem"){.reference
    .internal} exception.

    This signal supports returning deferreds from its handlers.

    Parameters

    :   -   **item** ([[item object]{.std
            .std-ref}](index.html#item-types){.hoverxref .tooltip
            .reference .internal}) -- the item dropped from the [[Item
            Pipeline]{.std
            .std-ref}](index.html#topics-item-pipeline){.hoverxref
            .tooltip .reference .internal}

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which scraped the item

        -   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal} object) -- the response from where the item was
            dropped

        -   **exception** ([[`DropItem`{.xref .py .py-exc .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.exceptions.DropItem "scrapy.exceptions.DropItem"){.reference
            .internal} exception) -- the exception (which must be a
            [[`DropItem`{.xref .py .py-exc .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.exceptions.DropItem "scrapy.exceptions.DropItem"){.reference
            .internal} subclass) which caused the item to be dropped
:::

::: {#item-error .section}
###### item_error[¶](#item-error "Permalink to this heading"){.headerlink}

[]{#std-signal-item_error .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[item_error]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}*, *[[response]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*, *[[failure]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.item_error "Permalink to this definition"){.headerlink}

:   Sent when a [[Item Pipeline]{.std
    .std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
    .reference .internal} generates an error (i.e. raises an exception),
    except [[`DropItem`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.DropItem "scrapy.exceptions.DropItem"){.reference
    .internal} exception.

    This signal supports returning deferreds from its handlers.

    Parameters

    :   -   **item** ([[item object]{.std
            .std-ref}](index.html#item-types){.hoverxref .tooltip
            .reference .internal}) -- the item that caused the error in
            the [[Item Pipeline]{.std
            .std-ref}](index.html#topics-item-pipeline){.hoverxref
            .tooltip .reference .internal}

        -   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal} object) -- the response being processed when the
            exception was raised

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which raised the exception

        -   **failure**
            ([*twisted.python.failure.Failure*](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference
            .external}) -- the exception raised
:::
:::

::: {#spider-signals .section}
##### Spider signals[¶](#spider-signals "Permalink to this heading"){.headerlink}

::: {#spider-closed .section}
###### spider_closed[¶](#spider-closed "Permalink to this heading"){.headerlink}

[]{#std-signal-spider_closed .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[spider_closed]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*, *[[reason]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.spider_closed "Permalink to this definition"){.headerlink}

:   Sent after a spider has been closed. This can be used to release
    per-spider resources reserved on [[`spider_opened`{.xref .std
    .std-signal .docutils .literal
    .notranslate}]{.pre}](#std-signal-spider_opened){.hoverxref .tooltip
    .reference .internal}.

    This signal supports returning deferreds from its handlers.

    Parameters

    :   -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which has been closed

        -   **reason**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- a string which describes the reason why the
            spider was closed. If it was closed because the spider has
            completed scraping, the reason is [`'finished'`{.docutils
            .literal .notranslate}]{.pre}. Otherwise, if the spider was
            manually closed by calling the [`close_spider`{.docutils
            .literal .notranslate}]{.pre} engine method, then the reason
            is the one passed in the [`reason`{.docutils .literal
            .notranslate}]{.pre} argument of that method (which defaults
            to [`'cancelled'`{.docutils .literal .notranslate}]{.pre}).
            If the engine was shutdown (for example, by hitting Ctrl-C
            to stop it) the reason will be [`'shutdown'`{.docutils
            .literal .notranslate}]{.pre}.
:::

::: {#spider-opened .section}
###### spider_opened[¶](#spider-opened "Permalink to this heading"){.headerlink}

[]{#std-signal-spider_opened .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[spider_opened]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.spider_opened "Permalink to this definition"){.headerlink}

:   Sent after a spider has been opened for crawling. This is typically
    used to reserve per-spider resources, but can be used for any task
    that needs to be performed when a spider is opened.

    This signal supports returning deferreds from its handlers.

    Parameters

    :   **spider** ([[`Spider`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
        .internal} object) -- the spider which has been opened
:::

::: {#spider-idle .section}
###### spider_idle[¶](#spider-idle "Permalink to this heading"){.headerlink}

[]{#std-signal-spider_idle .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[spider_idle]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.spider_idle "Permalink to this definition"){.headerlink}

:   Sent when a spider has gone idle, which means the spider has no
    further:

    > <div>
    >
    > -   requests waiting to be downloaded
    >
    > -   requests scheduled
    >
    > -   items being processed in the item pipeline
    >
    > </div>

    If the idle state persists after all handlers of this signal have
    finished, the engine starts closing the spider. After the spider has
    finished closing, the [[`spider_closed`{.xref .std .std-signal
    .docutils .literal
    .notranslate}]{.pre}](#std-signal-spider_closed){.hoverxref .tooltip
    .reference .internal} signal is sent.

    You may raise a [[`DontCloseSpider`{.xref .py .py-exc .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.DontCloseSpider "scrapy.exceptions.DontCloseSpider"){.reference
    .internal} exception to prevent the spider from being closed.

    Alternatively, you may raise a [[`CloseSpider`{.xref .py .py-exc
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.CloseSpider "scrapy.exceptions.CloseSpider"){.reference
    .internal} exception to provide a custom spider closing reason. An
    idle handler is the perfect place to put some code that assesses the
    final spider results and update the final closing reason accordingly
    (e.g. setting it to 'too_few_results' instead of 'finished').

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   **spider** ([[`Spider`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
        .internal} object) -- the spider which has gone idle

::: {.admonition .note}
Note

Scheduling some requests in your [[`spider_idle`{.xref .std .std-signal
.docutils .literal
.notranslate}]{.pre}](#std-signal-spider_idle){.hoverxref .tooltip
.reference .internal} handler does **not** guarantee that it can prevent
the spider from being closed, although it sometimes can. That's because
the spider may still remain idle if all the scheduled requests are
rejected by the scheduler (e.g. filtered due to duplication).
:::
:::

::: {#spider-error .section}
###### spider_error[¶](#spider-error "Permalink to this heading"){.headerlink}

[]{#std-signal-spider_error .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[spider_error]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[failure]{.pre}]{.n}*, *[[response]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.spider_error "Permalink to this definition"){.headerlink}

:   Sent when a spider callback generates an error (i.e. raises an
    exception).

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **failure**
            ([*twisted.python.failure.Failure*](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference
            .external}) -- the exception raised

        -   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal} object) -- the response being processed when the
            exception was raised

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider which raised the exception
:::

::: {#feed-slot-closed .section}
###### feed_slot_closed[¶](#feed-slot-closed "Permalink to this heading"){.headerlink}

[]{#std-signal-feed_slot_closed .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[feed_slot_closed]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[slot]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.feed_slot_closed "Permalink to this definition"){.headerlink}

:   Sent when a [[feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} slot is closed.

    This signal supports returning deferreds from its handlers.

    Parameters

    :   **slot** (*scrapy.extensions.feedexport.FeedSlot*) -- the slot
        closed
:::

::: {#feed-exporter-closed .section}
###### feed_exporter_closed[¶](#feed-exporter-closed "Permalink to this heading"){.headerlink}

[]{#std-signal-feed_exporter_closed .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[feed_exporter_closed]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[¶](#scrapy.signals.feed_exporter_closed "Permalink to this definition"){.headerlink}

:   Sent when the [[feed exports]{.std
    .std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
    .reference .internal} extension is closed, during the handling of
    the [[`spider_closed`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](#std-signal-spider_closed){.hoverxref .tooltip
    .reference .internal} signal by the extension, after all feed
    exporting has been handled.

    This signal supports returning deferreds from its handlers.
:::
:::

::: {#request-signals .section}
##### Request signals[¶](#request-signals "Permalink to this heading"){.headerlink}

::: {#request-scheduled .section}
###### request_scheduled[¶](#request-scheduled "Permalink to this heading"){.headerlink}

[]{#std-signal-request_scheduled .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[request_scheduled]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.request_scheduled "Permalink to this definition"){.headerlink}

:   Sent when the engine schedules a [`Request`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre}, to be downloaded later.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            reached the scheduler

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider that yielded the request
:::

::: {#request-dropped .section}
###### request_dropped[¶](#request-dropped "Permalink to this heading"){.headerlink}

[]{#std-signal-request_dropped .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[request_dropped]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.request_dropped "Permalink to this definition"){.headerlink}

:   Sent when a [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}, scheduled by the engine to be downloaded
    later, is rejected by the scheduler.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            reached the scheduler

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider that yielded the request
:::

::: {#request-reached-downloader .section}
###### request_reached_downloader[¶](#request-reached-downloader "Permalink to this heading"){.headerlink}

[]{#std-signal-request_reached_downloader .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[request_reached_downloader]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.request_reached_downloader "Permalink to this definition"){.headerlink}

:   Sent when a [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} reached downloader.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            reached downloader

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider that yielded the request
:::

::: {#request-left-downloader .section}
###### request_left_downloader[¶](#request-left-downloader "Permalink to this heading"){.headerlink}

[]{#std-signal-request_left_downloader .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[request_left_downloader]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.request_left_downloader "Permalink to this definition"){.headerlink}

:   ::: versionadded
    [New in version 2.0.]{.versionmodified .added}
    :::

    Sent when a [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} leaves the downloader, even in case of failure.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            reached the downloader

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider that yielded the request
:::

::: {#bytes-received .section}
###### bytes_received[¶](#bytes-received "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.2.]{.versionmodified .added}
:::

[]{#std-signal-bytes_received .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[bytes_received]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[data]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.bytes_received "Permalink to this definition"){.headerlink}

:   Sent by the HTTP 1.1 and S3 download handlers when a group of bytes
    is received for a specific request. This signal might be fired
    multiple times for the same request, with partial data each time.
    For instance, a possible scenario for a 25 kb response would be two
    signals fired with 10 kb of data, and a final one with 5 kb of data.

    Handlers for this signal can stop the download of a response while
    it is in progress by raising the [[`StopDownload`{.xref .py .py-exc
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.StopDownload "scrapy.exceptions.StopDownload"){.reference
    .internal} exception. Please refer to the [[Stopping the download of
    a Response]{.std
    .std-ref}](index.html#topics-stop-response-download){.hoverxref
    .tooltip .reference .internal} topic for additional information and
    examples.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **data** ([[`bytes`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
            .external} object) -- the data received by the download
            handler

        -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            generated the download

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider associated with the
            response
:::

::: {#headers-received .section}
###### headers_received[¶](#headers-received "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.5.]{.versionmodified .added}
:::

[]{#std-signal-headers_received .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[headers_received]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[headers]{.pre}]{.n}*, *[[body_length]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.headers_received "Permalink to this definition"){.headerlink}

:   Sent by the HTTP 1.1 and S3 download handlers when the response
    headers are available for a given request, before downloading any
    additional content.

    Handlers for this signal can stop the download of a response while
    it is in progress by raising the [[`StopDownload`{.xref .py .py-exc
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.StopDownload "scrapy.exceptions.StopDownload"){.reference
    .internal} exception. Please refer to the [[Stopping the download of
    a Response]{.std
    .std-ref}](index.html#topics-stop-response-download){.hoverxref
    .tooltip .reference .internal} topic for additional information and
    examples.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **headers** ([`scrapy.http.headers.Headers`{.xref .py
            .py-class .docutils .literal .notranslate}]{.pre} object) --
            the headers received by the download handler

        -   **body_length** (int) -- expected size of the response body,
            in bytes

        -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            generated the download

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider associated with the
            response
:::
:::

::: {#response-signals .section}
##### Response signals[¶](#response-signals "Permalink to this heading"){.headerlink}

::: {#response-received .section}
###### response_received[¶](#response-received "Permalink to this heading"){.headerlink}

[]{#std-signal-response_received .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[response_received]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.response_received "Permalink to this definition"){.headerlink}

:   Sent when the engine receives a new [[`Response`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} from the downloader.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal} object) -- the response received

        -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            generated the response

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider for which the response is
            intended

::: {.admonition .note}
Note

The [`request`{.docutils .literal .notranslate}]{.pre} argument might
not contain the original request that reached the downloader, if a
[[Downloader Middleware]{.std
.std-ref}](index.html#topics-downloader-middleware){.hoverxref .tooltip
.reference .internal} modifies the [[`Response`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} object and sets a specific [`request`{.docutils .literal
.notranslate}]{.pre} attribute.
:::
:::

::: {#response-downloaded .section}
###### response_downloaded[¶](#response-downloaded "Permalink to this heading"){.headerlink}

[]{#std-signal-response_downloaded .target}

[[scrapy.signals.]{.pre}]{.sig-prename .descclassname}[[response_downloaded]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.signals.response_downloaded "Permalink to this definition"){.headerlink}

:   Sent by the downloader right after a [`HTTPResponse`{.docutils
    .literal .notranslate}]{.pre} is downloaded.

    This signal does not support returning deferreds from its handlers.

    Parameters

    :   -   **response** ([[`Response`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
            .internal} object) -- the response downloaded

        -   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} object) -- the request that
            generated the response

        -   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal} object) -- the spider for which the response is
            intended
:::
:::
:::
:::

[]{#document-topics/scheduler}

::: {#module-scrapy.core.scheduler .section}
[]{#scheduler}[]{#topics-scheduler}

### Scheduler[¶](#module-scrapy.core.scheduler "Permalink to this heading"){.headerlink}

The scheduler component receives requests from the [[engine]{.std
.std-ref}](index.html#component-engine){.hoverxref .tooltip .reference
.internal} and stores them into persistent and/or non-persistent data
structures. It also gets those requests and feeds them back to the
engine when it asks for a next request to be downloaded.

::: {#overriding-the-default-scheduler .section}
#### Overriding the default scheduler[¶](#overriding-the-default-scheduler "Permalink to this heading"){.headerlink}

You can use your own custom scheduler class by supplying its full Python
path in the [[`SCHEDULER`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-SCHEDULER){.hoverxref
.tooltip .reference .internal} setting.
:::

::: {#minimal-scheduler-interface .section}
#### Minimal scheduler interface[¶](#minimal-scheduler-interface "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.core.scheduler.]{.pre}]{.sig-prename .descclassname}[[BaseScheduler]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#BaseScheduler){.reference .internal}[¶](#scrapy.core.scheduler.BaseScheduler "Permalink to this definition"){.headerlink}

:   The scheduler component is responsible for storing requests received
    from the engine, and feeding them back upon request (also to the
    engine).

    The original sources of said requests are:

    -   Spider: [`start_requests`{.docutils .literal
        .notranslate}]{.pre} method, requests created for URLs in the
        [`start_urls`{.docutils .literal .notranslate}]{.pre} attribute,
        request callbacks

    -   Spider middleware: [`process_spider_output`{.docutils .literal
        .notranslate}]{.pre} and [`process_spider_exception`{.docutils
        .literal .notranslate}]{.pre} methods

    -   Downloader middleware: [`process_request`{.docutils .literal
        .notranslate}]{.pre}, [`process_response`{.docutils .literal
        .notranslate}]{.pre} and [`process_exception`{.docutils .literal
        .notranslate}]{.pre} methods

    The order in which the scheduler returns its stored requests (via
    the [`next_request`{.docutils .literal .notranslate}]{.pre} method)
    plays a great part in determining the order in which those requests
    are downloaded.

    The methods defined in this class constitute the minimal interface
    that the Scrapy engine will interact with.

    [[close]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[reason]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#BaseScheduler.close){.reference .internal}[¶](#scrapy.core.scheduler.BaseScheduler.close "Permalink to this definition"){.headerlink}

    :   Called when the spider is closed by the engine. It receives the
        reason why the crawl finished as argument and it's useful to
        execute cleaning code.

        Parameters

        :   **reason** ([[`str`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- a string which describes the reason why the
            spider was closed

    *[abstract]{.pre}[ ]{.w}*[[enqueue_request]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#BaseScheduler.enqueue_request){.reference .internal}[¶](#scrapy.core.scheduler.BaseScheduler.enqueue_request "Permalink to this definition"){.headerlink}

    :   Process a request received by the engine.

        Return [`True`{.docutils .literal .notranslate}]{.pre} if the
        request is stored correctly, [`False`{.docutils .literal
        .notranslate}]{.pre} otherwise.

        If [`False`{.docutils .literal .notranslate}]{.pre}, the engine
        will fire a [`request_dropped`{.docutils .literal
        .notranslate}]{.pre} signal, and will not make further attempts
        to schedule the request at a later time. For reference, the
        default Scrapy scheduler returns [`False`{.docutils .literal
        .notranslate}]{.pre} when the request is rejected by the
        dupefilter.

    *[classmethod]{.pre}[ ]{.w}*[[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[Self]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#BaseScheduler.from_crawler){.reference .internal}[¶](#scrapy.core.scheduler.BaseScheduler.from_crawler "Permalink to this definition"){.headerlink}

    :   Factory method which receives the current [[`Crawler`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} object as argument.

    *[abstract]{.pre}[ ]{.w}*[[has_pending_requests]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#BaseScheduler.has_pending_requests){.reference .internal}[¶](#scrapy.core.scheduler.BaseScheduler.has_pending_requests "Permalink to this definition"){.headerlink}

    :   [`True`{.docutils .literal .notranslate}]{.pre} if the scheduler
        has enqueued requests, [`False`{.docutils .literal
        .notranslate}]{.pre} otherwise

    *[abstract]{.pre}[ ]{.w}*[[next_request]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#BaseScheduler.next_request){.reference .internal}[¶](#scrapy.core.scheduler.BaseScheduler.next_request "Permalink to this definition"){.headerlink}

    :   Return the next [[`Request`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} to be processed, or [`None`{.docutils .literal
        .notranslate}]{.pre} to indicate that there are no requests to
        be considered ready at the moment.

        Returning [`None`{.docutils .literal .notranslate}]{.pre}
        implies that no request from the scheduler will be sent to the
        downloader in the current reactor cycle. The engine will
        continue calling [`next_request`{.docutils .literal
        .notranslate}]{.pre} until [`has_pending_requests`{.docutils
        .literal .notranslate}]{.pre} is [`False`{.docutils .literal
        .notranslate}]{.pre}.

    [[open]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#BaseScheduler.open){.reference .internal}[¶](#scrapy.core.scheduler.BaseScheduler.open "Permalink to this definition"){.headerlink}

    :   Called when the spider is opened by the engine. It receives the
        spider instance as argument and it's useful to execute
        initialization code.

        Parameters

        :   **spider** ([[`Spider`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
            .internal}) -- the spider object for the current crawl
:::

::: {#default-scrapy-scheduler .section}
#### Default Scrapy scheduler[¶](#default-scrapy-scheduler "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.core.scheduler.]{.pre}]{.sig-prename .descclassname}[[Scheduler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[dupefilter]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[BaseDupeFilter]{.pre}]{.n}*, *[[jobdir]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[dqclass]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[mqclass]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[logunser]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*, *[[stats]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[StatsCollector]{.pre}](index.html#scrapy.statscollectors.StatsCollector "scrapy.statscollectors.StatsCollector"){.reference .internal}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[pqclass]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[crawler]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler "Permalink to this definition"){.headerlink}

:   Default Scrapy scheduler. This implementation also handles
    duplication filtering via the [[`dupefilter`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DUPEFILTER_CLASS){.hoverxref
    .tooltip .reference .internal}.

    This scheduler stores requests into several priority queues (defined
    by the [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref
    .tooltip .reference .internal} setting). In turn, said priority
    queues are backed by either memory or disk based queues
    (respectively defined by the [[`SCHEDULER_MEMORY_QUEUE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_MEMORY_QUEUE){.hoverxref
    .tooltip .reference .internal} and [[`SCHEDULER_DISK_QUEUE`{.xref
    .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DISK_QUEUE){.hoverxref
    .tooltip .reference .internal} settings).

    Request prioritization is almost entirely delegated to the priority
    queue. The only prioritization performed by this scheduler is using
    the disk-based queue if present (i.e. if the [[`JOBDIR`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-JOBDIR){.hoverxref
    .tooltip .reference .internal} setting is defined) and falling back
    to the memory-based queue if a serialization error occurs. If the
    disk queue is not present, the memory one is used directly.

    Parameters

    :   -   **dupefilter** ([`scrapy.dupefilters.BaseDupeFilter`{.xref
            .py .py-class .docutils .literal .notranslate}]{.pre}
            instance or similar: any class that implements the
            BaseDupeFilter interface) -- An object responsible for
            checking and filtering duplicate requests. The value for the
            [[`DUPEFILTER_CLASS`{.xref .std .std-setting .docutils
            .literal
            .notranslate}]{.pre}](index.html#std-setting-DUPEFILTER_CLASS){.hoverxref
            .tooltip .reference .internal} setting is used by default.

        -   **jobdir** ([[`str`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} or [`None`{.docutils .literal
            .notranslate}]{.pre}) -- The path of a directory to be used
            for persisting the crawl's state. The value for the
            [[`JOBDIR`{.xref .std .std-setting .docutils .literal
            .notranslate}]{.pre}](index.html#std-setting-JOBDIR){.hoverxref
            .tooltip .reference .internal} setting is used by default.
            See [[Jobs: pausing and resuming crawls]{.std
            .std-ref}](index.html#topics-jobs){.hoverxref .tooltip
            .reference .internal}.

        -   **dqclass** (*class*) -- A class to be used as persistent
            request queue. The value for the
            [[`SCHEDULER_DISK_QUEUE`{.xref .std .std-setting .docutils
            .literal
            .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DISK_QUEUE){.hoverxref
            .tooltip .reference .internal} setting is used by default.

        -   **mqclass** (*class*) -- A class to be used as
            non-persistent request queue. The value for the
            [[`SCHEDULER_MEMORY_QUEUE`{.xref .std .std-setting .docutils
            .literal
            .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_MEMORY_QUEUE){.hoverxref
            .tooltip .reference .internal} setting is used by default.

        -   **logunser**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- A boolean that indicates whether or not
            unserializable requests should be logged. The value for the
            [[`SCHEDULER_DEBUG`{.xref .std .std-setting .docutils
            .literal
            .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DEBUG){.hoverxref
            .tooltip .reference .internal} setting is used by default.

        -   **stats** ([[`scrapy.statscollectors.StatsCollector`{.xref
            .py .py-class .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.statscollectors.StatsCollector "scrapy.statscollectors.StatsCollector"){.reference
            .internal} instance or similar: any class that implements
            the StatsCollector interface) -- A stats collector object to
            record stats about the request scheduling process. The value
            for the [[`STATS_CLASS`{.xref .std .std-setting .docutils
            .literal
            .notranslate}]{.pre}](index.html#std-setting-STATS_CLASS){.hoverxref
            .tooltip .reference .internal} setting is used by default.

        -   **pqclass** (*class*) -- A class to be used as priority
            queue for requests. The value for the
            [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std .std-setting
            .docutils .literal
            .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref
            .tooltip .reference .internal} setting is used by default.

        -   **crawler** ([[`scrapy.crawler.Crawler`{.xref .py .py-class
            .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
            .internal}) -- The crawler object corresponding to the
            current crawl.

    [[\_\_len\_\_]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler.__len__){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler.__len__ "Permalink to this definition"){.headerlink}

    :   Return the total amount of enqueued requests

    [[close]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[reason]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler.close){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler.close "Permalink to this definition"){.headerlink}

    :   1.  dump pending requests to disk if there is a disk queue

        2.  return the result of the dupefilter's [`close`{.docutils
            .literal .notranslate}]{.pre} method

    [[enqueue_request]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler.enqueue_request){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler.enqueue_request "Permalink to this definition"){.headerlink}

    :   Unless the received request is filtered out by the Dupefilter,
        attempt to push it into the disk queue, falling back to pushing
        it into the memory queue.

        Increment the appropriate stats, such as:
        [`scheduler/enqueued`{.docutils .literal .notranslate}]{.pre},
        [`scheduler/enqueued/disk`{.docutils .literal
        .notranslate}]{.pre}, [`scheduler/enqueued/memory`{.docutils
        .literal .notranslate}]{.pre}.

        Return [`True`{.docutils .literal .notranslate}]{.pre} if the
        request was stored successfully, [`False`{.docutils .literal
        .notranslate}]{.pre} otherwise.

    *[classmethod]{.pre}[ ]{.w}*[[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[SchedulerTV]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler.from_crawler){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler.from_crawler "Permalink to this definition"){.headerlink}

    :   Factory method, initializes the scheduler with arguments taken
        from the crawl settings

    [[has_pending_requests]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler.has_pending_requests){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler.has_pending_requests "Permalink to this definition"){.headerlink}

    :   [`True`{.docutils .literal .notranslate}]{.pre} if the scheduler
        has enqueued requests, [`False`{.docutils .literal
        .notranslate}]{.pre} otherwise

    [[next_request]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler.next_request){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler.next_request "Permalink to this definition"){.headerlink}

    :   Return a [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object from the memory queue, falling back to the
        disk queue if the memory queue is empty. Return
        [`None`{.docutils .literal .notranslate}]{.pre} if there are no
        more enqueued requests.

        Increment the appropriate stats, such as:
        [`scheduler/dequeued`{.docutils .literal .notranslate}]{.pre},
        [`scheduler/dequeued/disk`{.docutils .literal
        .notranslate}]{.pre}, [`scheduler/dequeued/memory`{.docutils
        .literal .notranslate}]{.pre}.

    [[open]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/core/scheduler.html#Scheduler.open){.reference .internal}[¶](#scrapy.core.scheduler.Scheduler.open "Permalink to this definition"){.headerlink}

    :   1.  initialize the memory queue

        2.  initialize the disk queue if the [`jobdir`{.docutils
            .literal .notranslate}]{.pre} attribute is a valid directory

        3.  return the result of the dupefilter's [`open`{.docutils
            .literal .notranslate}]{.pre} method
:::
:::

[]{#document-topics/exporters}

::: {#module-scrapy.exporters .section}
[]{#item-exporters}[]{#topics-exporters}

### Item Exporters[¶](#module-scrapy.exporters "Permalink to this heading"){.headerlink}

Once you have scraped your items, you often want to persist or export
those items, to use the data in some other application. That is, after
all, the whole purpose of the scraping process.

For this purpose Scrapy provides a collection of Item Exporters for
different output formats, such as XML, CSV or JSON.

::: {#using-item-exporters .section}
#### Using Item Exporters[¶](#using-item-exporters "Permalink to this heading"){.headerlink}

If you are in a hurry, and just want to use an Item Exporter to output
scraped data see the [[Feed exports]{.std
.std-ref}](index.html#topics-feed-exports){.hoverxref .tooltip
.reference .internal}. Otherwise, if you want to know how Item Exporters
work or need more custom functionality (not covered by the default
exports), continue reading below.

In order to use an Item Exporter, you must instantiate it with its
required args. Each Item Exporter requires different arguments, so check
each exporter documentation to be sure, in [[Built-in Item Exporters
reference]{.std .std-ref}](#topics-exporters-reference){.hoverxref
.tooltip .reference .internal}. After you have instantiated your
exporter, you have to:

1\. call the method [[`start_exporting()`{.xref .py .py-meth .docutils
.literal
.notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.start_exporting "scrapy.exporters.BaseItemExporter.start_exporting"){.reference
.internal} in order to signal the beginning of the exporting process

2\. call the [[`export_item()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.export_item "scrapy.exporters.BaseItemExporter.export_item"){.reference
.internal} method for each item you want to export

3\. and finally call the [[`finish_exporting()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.finish_exporting "scrapy.exporters.BaseItemExporter.finish_exporting"){.reference
.internal} to signal the end of the exporting process

Here you can see an [[Item
Pipeline]{.doc}](index.html#document-topics/item-pipeline){.reference
.internal} which uses multiple Item Exporters to group scraped items to
different files according to the value of one of their fields:

::: {.highlight-python .notranslate}
::: highlight
    from itemadapter import ItemAdapter
    from scrapy.exporters import XmlItemExporter


    class PerYearXmlExportPipeline:
        """Distribute items across multiple XML files according to their 'year' field"""

        def open_spider(self, spider):
            self.year_to_exporter = {}

        def close_spider(self, spider):
            for exporter, xml_file in self.year_to_exporter.values():
                exporter.finish_exporting()
                xml_file.close()

        def _exporter_for_item(self, item):
            adapter = ItemAdapter(item)
            year = adapter["year"]
            if year not in self.year_to_exporter:
                xml_file = open(f"{year}.xml", "wb")
                exporter = XmlItemExporter(xml_file)
                exporter.start_exporting()
                self.year_to_exporter[year] = (exporter, xml_file)
            return self.year_to_exporter[year][0]

        def process_item(self, item, spider):
            exporter = self._exporter_for_item(item)
            exporter.export_item(item)
            return item
:::
:::
:::

::: {#serialization-of-item-fields .section}
[]{#topics-exporters-field-serialization}

#### Serialization of item fields[¶](#serialization-of-item-fields "Permalink to this heading"){.headerlink}

By default, the field values are passed unmodified to the underlying
serialization library, and the decision of how to serialize them is
delegated to each particular serialization library.

However, you can customize how each field value is serialized *before it
is passed to the serialization library*.

There are two ways to customize how a field will be serialized, which
are described next.

::: {#declaring-a-serializer-in-the-field .section}
[]{#topics-exporters-serializers}

##### 1. Declaring a serializer in the field[¶](#declaring-a-serializer-in-the-field "Permalink to this heading"){.headerlink}

If you use [`Item`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} you can declare a serializer in the [[field
metadata]{.std .std-ref}](index.html#topics-items-fields){.hoverxref
.tooltip .reference .internal}. The serializer must be a callable which
receives a value and returns its serialized form.

Example:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    def serialize_price(value):
        return f"$ {str(value)}"


    class Product(scrapy.Item):
        name = scrapy.Field()
        price = scrapy.Field(serializer=serialize_price)
:::
:::
:::

::: {#overriding-the-serialize-field-method .section}
##### 2. Overriding the serialize_field() method[¶](#overriding-the-serialize-field-method "Permalink to this heading"){.headerlink}

You can also override the [[`serialize_field()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.serialize_field "scrapy.exporters.BaseItemExporter.serialize_field"){.reference
.internal} method to customize how your field value will be exported.

Make sure you call the base class [[`serialize_field()`{.xref .py
.py-meth .docutils .literal
.notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.serialize_field "scrapy.exporters.BaseItemExporter.serialize_field"){.reference
.internal} method after your custom code.

Example:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.exporters import XmlItemExporter


    class ProductXmlExporter(XmlItemExporter):
        def serialize_field(self, field, name, value):
            if name == "price":
                return f"$ {str(value)}"
            return super().serialize_field(field, name, value)
:::
:::
:::
:::

::: {#built-in-item-exporters-reference .section}
[]{#topics-exporters-reference}

#### Built-in Item Exporters reference[¶](#built-in-item-exporters-reference "Permalink to this heading"){.headerlink}

Here is a list of the Item Exporters bundled with Scrapy. Some of them
contain output examples, which assume you're exporting these two items:

::: {.highlight-python .notranslate}
::: highlight
    Item(name="Color TV", price="1200")
    Item(name="DVD player", price="200")
:::
:::

::: {#baseitemexporter .section}
##### BaseItemExporter[¶](#baseitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[BaseItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[fields_to_export]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[export_empty_fields]{.pre}]{.n}[[=]{.pre}]{.o}[[False]{.pre}]{.default_value}*, *[[encoding]{.pre}]{.n}[[=]{.pre}]{.o}[[\'utf-8\']{.pre}]{.default_value}*, *[[indent]{.pre}]{.n}[[=]{.pre}]{.o}[[0]{.pre}]{.default_value}*, *[[dont_fail]{.pre}]{.n}[[=]{.pre}]{.o}[[False]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#BaseItemExporter){.reference .internal}[¶](#scrapy.exporters.BaseItemExporter "Permalink to this definition"){.headerlink}

:   This is the (abstract) base class for all Item Exporters. It
    provides support for common features used by all (concrete) Item
    Exporters, such as defining what fields to export, whether to export
    empty fields, or which encoding to use.

    These features can be configured through the [`__init__`{.docutils
    .literal .notranslate}]{.pre} method arguments which populate their
    respective instance attributes: [[`fields_to_export`{.xref .py
    .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.fields_to_export "scrapy.exporters.BaseItemExporter.fields_to_export"){.reference
    .internal}, [[`export_empty_fields`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.export_empty_fields "scrapy.exporters.BaseItemExporter.export_empty_fields"){.reference
    .internal}, [[`encoding`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.encoding "scrapy.exporters.BaseItemExporter.encoding"){.reference
    .internal}, [[`indent`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.indent "scrapy.exporters.BaseItemExporter.indent"){.reference
    .internal}.

    ::: versionadded
    [New in version 2.0: ]{.versionmodified .added}The *dont_fail*
    parameter.
    :::

    [[export_item]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[item]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#BaseItemExporter.export_item){.reference .internal}[¶](#scrapy.exporters.BaseItemExporter.export_item "Permalink to this definition"){.headerlink}

    :   Exports the given item. This method must be implemented in
        subclasses.

    [[serialize_field]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[field]{.pre}]{.n}*, *[[name]{.pre}]{.n}*, *[[value]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#BaseItemExporter.serialize_field){.reference .internal}[¶](#scrapy.exporters.BaseItemExporter.serialize_field "Permalink to this definition"){.headerlink}

    :   Return the serialized value for the given field. You can
        override this method (in your custom Item Exporters) if you want
        to control how a particular field or value will be
        serialized/exported.

        By default, this method looks for a serializer [[declared in the
        item field]{.std
        .std-ref}](#topics-exporters-serializers){.hoverxref .tooltip
        .reference .internal} and returns the result of applying that
        serializer to the value. If no serializer is found, it returns
        the value unchanged.

        Parameters

        :   -   **field** ([`Field`{.xref .py .py-class .docutils
                .literal .notranslate}]{.pre} object or a [[`dict`{.xref
                .py .py-class .docutils .literal
                .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
                .external} instance) -- the field being serialized. If
                the source [[item object]{.std
                .std-ref}](index.html#item-types){.hoverxref .tooltip
                .reference .internal} does not define field metadata,
                *field* is an empty [[`dict`{.xref .py .py-class
                .docutils .literal
                .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
                .external}.

            -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the name of the field being serialized

            -   **value** -- the value being serialized

    [[start_exporting]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#BaseItemExporter.start_exporting){.reference .internal}[¶](#scrapy.exporters.BaseItemExporter.start_exporting "Permalink to this definition"){.headerlink}

    :   Signal the beginning of the exporting process. Some exporters
        may use this to generate some required header (for example, the
        [[`XmlItemExporter`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.exporters.XmlItemExporter "scrapy.exporters.XmlItemExporter"){.reference
        .internal}). You must call this method before exporting any
        items.

    [[finish_exporting]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#BaseItemExporter.finish_exporting){.reference .internal}[¶](#scrapy.exporters.BaseItemExporter.finish_exporting "Permalink to this definition"){.headerlink}

    :   Signal the end of the exporting process. Some exporters may use
        this to generate some required footer (for example, the
        [[`XmlItemExporter`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.exporters.XmlItemExporter "scrapy.exporters.XmlItemExporter"){.reference
        .internal}). You must always call this method after you have no
        more items to export.

    [[fields_to_export]{.pre}]{.sig-name .descname}[¶](#scrapy.exporters.BaseItemExporter.fields_to_export "Permalink to this definition"){.headerlink}

    :   Fields to export, their order [1](#id3){#id1 .footnote-reference
        .brackets} and their output names.

        Possible values are:

        -   [`None`{.docutils .literal .notranslate}]{.pre} (all fields
            [2](#id4){#id2 .footnote-reference .brackets}, default)

        -   A list of fields:

            ::: {.highlight-default .notranslate}
            ::: highlight
                ['field1', 'field2']
            :::
            :::

        -   A dict where keys are fields and values are output names:

            ::: {.highlight-default .notranslate}
            ::: highlight
                {'field1': 'Field 1', 'field2': 'Field 2'}
            :::
            :::

        [[1](#id1){.fn-backref}]{.brackets}

        :   Not all exporters respect the specified field order.

        [[2](#id2){.fn-backref}]{.brackets}

        :   When using [[item objects]{.std
            .std-ref}](index.html#item-types){.hoverxref .tooltip
            .reference .internal} that do not expose all their possible
            fields, exporters that do not support exporting a different
            subset of fields per item will only export the fields found
            in the first item exported.

    [[export_empty_fields]{.pre}]{.sig-name .descname}[¶](#scrapy.exporters.BaseItemExporter.export_empty_fields "Permalink to this definition"){.headerlink}

    :   Whether to include empty/unpopulated item fields in the exported
        data. Defaults to [`False`{.docutils .literal
        .notranslate}]{.pre}. Some exporters (like
        [[`CsvItemExporter`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.exporters.CsvItemExporter "scrapy.exporters.CsvItemExporter"){.reference
        .internal}) ignore this attribute and always export all empty
        fields.

        This option is ignored for dict items.

    [[encoding]{.pre}]{.sig-name .descname}[¶](#scrapy.exporters.BaseItemExporter.encoding "Permalink to this definition"){.headerlink}

    :   The output character encoding.

    [[indent]{.pre}]{.sig-name .descname}[¶](#scrapy.exporters.BaseItemExporter.indent "Permalink to this definition"){.headerlink}

    :   Amount of spaces used to indent the output on each level.
        Defaults to [`0`{.docutils .literal .notranslate}]{.pre}.

        -   [`indent=None`{.docutils .literal .notranslate}]{.pre}
            selects the most compact representation, all items in the
            same line with no indentation

        -   [`indent<=0`{.docutils .literal .notranslate}]{.pre} each
            item on its own line, no indentation

        -   [`indent>0`{.docutils .literal .notranslate}]{.pre} each
            item on its own line, indented with the provided numeric
            value
:::

::: {#pythonitemexporter .section}
##### PythonItemExporter[¶](#pythonitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[PythonItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[\*]{.pre}]{.o}*, *[[dont_fail]{.pre}]{.n}[[=]{.pre}]{.o}[[False]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#PythonItemExporter){.reference .internal}[¶](#scrapy.exporters.PythonItemExporter "Permalink to this definition"){.headerlink}

:   This is a base class for item exporters that extends
    [[`BaseItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} with support for nested items.

    It serializes items to built-in Python types, so that any
    serialization library (e.g. [[`json`{.xref .py .py-mod .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#module-json "(in Python v3.12)"){.reference
    .external} or
    [msgpack](https://pypi.org/project/msgpack/){.reference .external})
    can be used on top of it.
:::

::: {#xmlitemexporter .section}
##### XmlItemExporter[¶](#xmlitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[XmlItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}*, *[[item_element]{.pre}]{.n}[[=]{.pre}]{.o}[[\'item\']{.pre}]{.default_value}*, *[[root_element]{.pre}]{.n}[[=]{.pre}]{.o}[[\'items\']{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#XmlItemExporter){.reference .internal}[¶](#scrapy.exporters.XmlItemExporter "Permalink to this definition"){.headerlink}

:   Exports items in XML format to the specified file object.

    Parameters

    :   -   **file** -- the file-like object to use for exporting the
            data. Its [`write`{.docutils .literal .notranslate}]{.pre}
            method should accept [`bytes`{.docutils .literal
            .notranslate}]{.pre} (a disk file opened in binary mode, a
            [`io.BytesIO`{.docutils .literal .notranslate}]{.pre}
            object, etc)

        -   **root_element**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- The name of root element in the exported XML.

        -   **item_element**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- The name of each item element in the exported
            XML.

    The additional keyword arguments of this [`__init__`{.docutils
    .literal .notranslate}]{.pre} method are passed to the
    [[`BaseItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method.

    A typical output of this exporter would be:

    ::: {.highlight-none .notranslate}
    ::: highlight
        <?xml version="1.0" encoding="utf-8"?>
        <items>
          <item>
            <name>Color TV</name>
            <price>1200</price>
         </item>
          <item>
            <name>DVD player</name>
            <price>200</price>
         </item>
        </items>
    :::
    :::

    Unless overridden in the [`serialize_field()`{.xref .py .py-meth
    .docutils .literal .notranslate}]{.pre} method, multi-valued fields
    are exported by serializing each value inside a [`<value>`{.docutils
    .literal .notranslate}]{.pre} element. This is for convenience, as
    multi-valued fields are very common.

    For example, the item:

    ::: {.highlight-none .notranslate}
    ::: highlight
        Item(name=['John', 'Doe'], age='23')
    :::
    :::

    Would be serialized as:

    ::: {.highlight-none .notranslate}
    ::: highlight
        <?xml version="1.0" encoding="utf-8"?>
        <items>
          <item>
            <name>
              <value>John</value>
              <value>Doe</value>
            </name>
            <age>23</age>
          </item>
        </items>
    :::
    :::
:::

::: {#csvitemexporter .section}
##### CsvItemExporter[¶](#csvitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[CsvItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}*, *[[include_headers_line]{.pre}]{.n}[[=]{.pre}]{.o}[[True]{.pre}]{.default_value}*, *[[join_multivalued]{.pre}]{.n}[[=]{.pre}]{.o}[[\',\']{.pre}]{.default_value}*, *[[errors]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#CsvItemExporter){.reference .internal}[¶](#scrapy.exporters.CsvItemExporter "Permalink to this definition"){.headerlink}

:   Exports items in CSV format to the given file-like object. If the
    [`fields_to_export`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} attribute is set, it will be used to define the
    CSV columns, their order and their column names. The
    [`export_empty_fields`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} attribute has no effect on this exporter.

    Parameters

    :   -   **file** -- the file-like object to use for exporting the
            data. Its [`write`{.docutils .literal .notranslate}]{.pre}
            method should accept [`bytes`{.docutils .literal
            .notranslate}]{.pre} (a disk file opened in binary mode, a
            [`io.BytesIO`{.docutils .literal .notranslate}]{.pre}
            object, etc)

        -   **include_headers_line**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- If enabled, makes the exporter output a
            header line with the field names taken from
            [[`BaseItemExporter.fields_to_export`{.xref .py .py-attr
            .docutils .literal
            .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter.fields_to_export "scrapy.exporters.BaseItemExporter.fields_to_export"){.reference
            .internal} or the first exported item fields.

        -   **join_multivalued** -- The char (or chars) that will be
            used for joining multi-valued fields, if found.

        -   **errors**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- The optional string that specifies how
            encoding and decoding errors are to be handled. For more
            information see [[`io.TextIOWrapper`{.xref .py .py-class
            .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/io.html#io.TextIOWrapper "(in Python v3.12)"){.reference
            .external}.

    The additional keyword arguments of this [`__init__`{.docutils
    .literal .notranslate}]{.pre} method are passed to the
    [[`BaseItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method, and the leftover arguments to the [[`csv.writer()`{.xref .py
    .py-func .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/csv.html#csv.writer "(in Python v3.12)"){.reference
    .external} function, so you can use any [[`csv.writer()`{.xref .py
    .py-func .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/csv.html#csv.writer "(in Python v3.12)"){.reference
    .external} function argument to customize this exporter.

    A typical output of this exporter would be:

    ::: {.highlight-none .notranslate}
    ::: highlight
        product,price
        Color TV,1200
        DVD player,200
    :::
    :::
:::

::: {#pickleitemexporter .section}
##### PickleItemExporter[¶](#pickleitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[PickleItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}*, *[[protocol]{.pre}]{.n}[[=]{.pre}]{.o}[[0]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#PickleItemExporter){.reference .internal}[¶](#scrapy.exporters.PickleItemExporter "Permalink to this definition"){.headerlink}

:   Exports items in pickle format to the given file-like object.

    Parameters

    :   -   **file** -- the file-like object to use for exporting the
            data. Its [`write`{.docutils .literal .notranslate}]{.pre}
            method should accept [`bytes`{.docutils .literal
            .notranslate}]{.pre} (a disk file opened in binary mode, a
            [`io.BytesIO`{.docutils .literal .notranslate}]{.pre}
            object, etc)

        -   **protocol**
            ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
            .external}) -- The pickle protocol to use.

    For more information, see [[`pickle`{.xref .py .py-mod .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/pickle.html#module-pickle "(in Python v3.12)"){.reference
    .external}.

    The additional keyword arguments of this [`__init__`{.docutils
    .literal .notranslate}]{.pre} method are passed to the
    [[`BaseItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method.

    Pickle isn't a human readable format, so no output examples are
    provided.
:::

::: {#pprintitemexporter .section}
##### PprintItemExporter[¶](#pprintitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[PprintItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#PprintItemExporter){.reference .internal}[¶](#scrapy.exporters.PprintItemExporter "Permalink to this definition"){.headerlink}

:   Exports items in pretty print format to the specified file object.

    Parameters

    :   **file** -- the file-like object to use for exporting the data.
        Its [`write`{.docutils .literal .notranslate}]{.pre} method
        should accept [`bytes`{.docutils .literal .notranslate}]{.pre}
        (a disk file opened in binary mode, a [`io.BytesIO`{.docutils
        .literal .notranslate}]{.pre} object, etc)

    The additional keyword arguments of this [`__init__`{.docutils
    .literal .notranslate}]{.pre} method are passed to the
    [[`BaseItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method.

    A typical output of this exporter would be:

    ::: {.highlight-none .notranslate}
    ::: highlight
        {'name': 'Color TV', 'price': '1200'}
        {'name': 'DVD player', 'price': '200'}
    :::
    :::

    Longer lines (when present) are pretty-formatted.
:::

::: {#jsonitemexporter .section}
##### JsonItemExporter[¶](#jsonitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[JsonItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#JsonItemExporter){.reference .internal}[¶](#scrapy.exporters.JsonItemExporter "Permalink to this definition"){.headerlink}

:   Exports items in JSON format to the specified file-like object,
    writing all objects as a list of objects. The additional
    [`__init__`{.docutils .literal .notranslate}]{.pre} method arguments
    are passed to the [[`BaseItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method, and the leftover arguments to the [[`JSONEncoder`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.JSONEncoder "(in Python v3.12)"){.reference
    .external} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method, so you can use any [[`JSONEncoder`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.JSONEncoder "(in Python v3.12)"){.reference
    .external} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method argument to customize this exporter.

    Parameters

    :   **file** -- the file-like object to use for exporting the data.
        Its [`write`{.docutils .literal .notranslate}]{.pre} method
        should accept [`bytes`{.docutils .literal .notranslate}]{.pre}
        (a disk file opened in binary mode, a [`io.BytesIO`{.docutils
        .literal .notranslate}]{.pre} object, etc)

    A typical output of this exporter would be:

    ::: {.highlight-none .notranslate}
    ::: highlight
        [{"name": "Color TV", "price": "1200"},
        {"name": "DVD player", "price": "200"}]
    :::
    :::

    ::: {#json-with-large-data .admonition .warning}
    Warning

    JSON is very simple and flexible serialization format, but it
    doesn't scale well for large amounts of data since incremental (aka.
    stream-mode) parsing is not well supported (if at all) among JSON
    parsers (on any language), and most of them just parse the entire
    object in memory. If you want the power and simplicity of JSON with
    a more stream-friendly format, consider using
    [[`JsonLinesItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.JsonLinesItemExporter "scrapy.exporters.JsonLinesItemExporter"){.reference
    .internal} instead, or splitting the output in multiple chunks.
    :::
:::

::: {#jsonlinesitemexporter .section}
##### JsonLinesItemExporter[¶](#jsonlinesitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[JsonLinesItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#JsonLinesItemExporter){.reference .internal}[¶](#scrapy.exporters.JsonLinesItemExporter "Permalink to this definition"){.headerlink}

:   Exports items in JSON format to the specified file-like object,
    writing one JSON-encoded item per line. The additional
    [`__init__`{.docutils .literal .notranslate}]{.pre} method arguments
    are passed to the [[`BaseItemExporter`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.exporters.BaseItemExporter "scrapy.exporters.BaseItemExporter"){.reference
    .internal} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method, and the leftover arguments to the [[`JSONEncoder`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.JSONEncoder "(in Python v3.12)"){.reference
    .external} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method, so you can use any [[`JSONEncoder`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.JSONEncoder "(in Python v3.12)"){.reference
    .external} [`__init__`{.docutils .literal .notranslate}]{.pre}
    method argument to customize this exporter.

    Parameters

    :   **file** -- the file-like object to use for exporting the data.
        Its [`write`{.docutils .literal .notranslate}]{.pre} method
        should accept [`bytes`{.docutils .literal .notranslate}]{.pre}
        (a disk file opened in binary mode, a [`io.BytesIO`{.docutils
        .literal .notranslate}]{.pre} object, etc)

    A typical output of this exporter would be:

    ::: {.highlight-none .notranslate}
    ::: highlight
        {"name": "Color TV", "price": "1200"}
        {"name": "DVD player", "price": "200"}
    :::
    :::

    Unlike the one produced by [[`JsonItemExporter`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.exporters.JsonItemExporter "scrapy.exporters.JsonItemExporter"){.reference
    .internal}, the format produced by this exporter is well suited for
    serializing large amounts of data.
:::

::: {#marshalitemexporter .section}
##### MarshalItemExporter[¶](#marshalitemexporter "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.exporters.]{.pre}]{.sig-prename .descclassname}[[MarshalItemExporter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/exporters.html#MarshalItemExporter){.reference .internal}[¶](#scrapy.exporters.MarshalItemExporter "Permalink to this definition"){.headerlink}

:   Exports items in a Python-specific binary format (see
    [[`marshal`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/marshal.html#module-marshal "(in Python v3.12)"){.reference
    .external}).

    Parameters

    :   **file** -- The file-like object to use for exporting the data.
        Its [`write`{.docutils .literal .notranslate}]{.pre} method
        should accept [[`bytes`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
        .external} (a disk file opened in binary mode, a
        [[`BytesIO`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/io.html#io.BytesIO "(in Python v3.12)"){.reference
        .external} object, etc)
:::
:::
:::

[]{#document-topics/components}

::: {#components .section}
[]{#topics-components}

### Components[¶](#components "Permalink to this heading"){.headerlink}

A Scrapy component is any class whose objects are created using
[`scrapy.utils.misc.create_instance()`{.xref .py .py-func .docutils
.literal .notranslate}]{.pre}.

That includes the classes that you may assign to the following settings:

-   [[`DNS_RESOLVER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DNS_RESOLVER){.hoverxref
    .tooltip .reference .internal}

-   [[`DOWNLOAD_HANDLERS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_HANDLERS){.hoverxref
    .tooltip .reference .internal}

-   [[`DOWNLOADER_CLIENTCONTEXTFACTORY`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENTCONTEXTFACTORY){.hoverxref
    .tooltip .reference .internal}

-   [[`DOWNLOADER_MIDDLEWARES`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_MIDDLEWARES){.hoverxref
    .tooltip .reference .internal}

-   [[`DUPEFILTER_CLASS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DUPEFILTER_CLASS){.hoverxref
    .tooltip .reference .internal}

-   [[`EXTENSIONS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-EXTENSIONS){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_EXPORTERS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORTERS){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_STORAGES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_STORAGES){.hoverxref
    .tooltip .reference .internal}

-   [[`ITEM_PIPELINES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-ITEM_PIPELINES){.hoverxref
    .tooltip .reference .internal}

-   [[`SCHEDULER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER){.hoverxref
    .tooltip .reference .internal}

-   [[`SCHEDULER_DISK_QUEUE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_DISK_QUEUE){.hoverxref
    .tooltip .reference .internal}

-   [[`SCHEDULER_MEMORY_QUEUE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_MEMORY_QUEUE){.hoverxref
    .tooltip .reference .internal}

-   [[`SCHEDULER_PRIORITY_QUEUE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-SCHEDULER_PRIORITY_QUEUE){.hoverxref
    .tooltip .reference .internal}

-   [[`SPIDER_MIDDLEWARES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_MIDDLEWARES){.hoverxref
    .tooltip .reference .internal}

Third-party Scrapy components may also let you define additional Scrapy
components, usually configurable through [[settings]{.std
.std-ref}](index.html#topics-settings){.hoverxref .tooltip .reference
.internal}, to modify their behavior.

::: {#enforcing-component-requirements .section}
[]{#enforce-component-requirements}

#### Enforcing component requirements[¶](#enforcing-component-requirements "Permalink to this heading"){.headerlink}

Sometimes, your components may only be intended to work under certain
conditions. For example, they may require a minimum version of Scrapy to
work as intended, or they may require certain settings to have specific
values.

In addition to describing those conditions in the documentation of your
component, it is a good practice to raise an exception from the
[`__init__`{.docutils .literal .notranslate}]{.pre} method of your
component if those conditions are not met at run time.

In the case of [[downloader middlewares]{.std
.std-ref}](index.html#topics-downloader-middleware){.hoverxref .tooltip
.reference .internal}, [[extensions]{.std
.std-ref}](index.html#topics-extensions){.hoverxref .tooltip .reference
.internal}, [[item pipelines]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal}, and [[spider middlewares]{.std
.std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
.reference .internal}, you should raise
[[`scrapy.exceptions.NotConfigured`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.NotConfigured "scrapy.exceptions.NotConfigured"){.reference
.internal}, passing a description of the issue as a parameter to the
exception so that it is printed in the logs, for the user to see. For
other components, feel free to raise whatever other exception feels
right to you; for example, [[`RuntimeError`{.xref .py .py-exc .docutils
.literal
.notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#RuntimeError "(in Python v3.12)"){.reference
.external} would make sense for a Scrapy version mismatch, while
[[`ValueError`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#ValueError "(in Python v3.12)"){.reference
.external} may be better if the issue is the value of a setting.

If your requirement is a minimum Scrapy version, you may use
[`scrapy.__version__`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre} to enforce your requirement. For example:

::: {.highlight-python .notranslate}
::: highlight
    from packaging.version import parse as parse_version

    import scrapy


    class MyComponent:
        def __init__(self):
            if parse_version(scrapy.__version__) < parse_version("2.7"):
                raise RuntimeError(
                    f"{MyComponent.__qualname__} requires Scrapy 2.7 or "
                    f"later, which allow defining the process_spider_output "
                    f"method of spider middlewares as an asynchronous "
                    f"generator."
                )
:::
:::
:::
:::

[]{#document-topics/api}

::: {#core-api .section}
[]{#topics-api}

### Core API[¶](#core-api "Permalink to this heading"){.headerlink}

This section documents the Scrapy core API, and it's intended for
developers of extensions and middlewares.

::: {#crawler-api .section}
[]{#topics-api-crawler}

#### Crawler API[¶](#crawler-api "Permalink to this heading"){.headerlink}

The main entry point to Scrapy API is the [[`Crawler`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
.internal} object, passed to extensions through the
[`from_crawler`{.docutils .literal .notranslate}]{.pre} class method.
This object provides access to all Scrapy core components, and it's the
only way for extensions to access them and hook their functionality into
Scrapy.

[]{#module-scrapy.crawler .target}

The Extension Manager is responsible for loading and keeping track of
installed extensions and it's configured through the
[[`EXTENSIONS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-EXTENSIONS){.hoverxref
.tooltip .reference .internal} setting which contains a dictionary of
all available extensions and their order similar to how you [[configure
the downloader middlewares]{.std
.std-ref}](index.html#topics-downloader-middleware-setting){.hoverxref
.tooltip .reference .internal}.

*[class]{.pre}[ ]{.w}*[[scrapy.crawler.]{.pre}]{.sig-prename .descclassname}[[Crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spidercls]{.pre}]{.n}*, *[[settings]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#Crawler){.reference .internal}[¶](#scrapy.crawler.Crawler "Permalink to this definition"){.headerlink}

:   The Crawler object must be instantiated with a
    [[`scrapy.Spider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider "scrapy.Spider"){.reference
    .internal} subclass and a [[`scrapy.settings.Settings`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
    .internal} object.

    [[request_fingerprinter]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.Crawler.request_fingerprinter "Permalink to this definition"){.headerlink}

    :   The request fingerprint builder of this crawler.

        This is used from extensions and middlewares to build short,
        unique identifiers for requests. See [[Request
        fingerprints]{.std
        .std-ref}](index.html#request-fingerprints){.hoverxref .tooltip
        .reference .internal}.

    [[settings]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.Crawler.settings "Permalink to this definition"){.headerlink}

    :   The settings manager of this crawler.

        This is used by extensions & middlewares to access the Scrapy
        settings of this crawler.

        For an introduction on Scrapy settings see [[Settings]{.std
        .std-ref}](index.html#topics-settings){.hoverxref .tooltip
        .reference .internal}.

        For the API see [[`Settings`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
        .internal} class.

    [[signals]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.Crawler.signals "Permalink to this definition"){.headerlink}

    :   The signals manager of this crawler.

        This is used by extensions & middlewares to hook themselves into
        Scrapy functionality.

        For an introduction on signals see [[Signals]{.std
        .std-ref}](index.html#topics-signals){.hoverxref .tooltip
        .reference .internal}.

        For the API see [[`SignalManager`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.signalmanager.SignalManager "scrapy.signalmanager.SignalManager"){.reference
        .internal} class.

    [[stats]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.Crawler.stats "Permalink to this definition"){.headerlink}

    :   The stats collector of this crawler.

        This is used from extensions & middlewares to record stats of
        their behaviour, or access stats collected by other extensions.

        For an introduction on stats collection see [[Stats
        Collection]{.std .std-ref}](index.html#topics-stats){.hoverxref
        .tooltip .reference .internal}.

        For the API see [[`StatsCollector`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.statscollectors.StatsCollector "scrapy.statscollectors.StatsCollector"){.reference
        .internal} class.

    [[extensions]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.Crawler.extensions "Permalink to this definition"){.headerlink}

    :   The extension manager that keeps track of enabled extensions.

        Most extensions won't need to access this attribute.

        For an introduction on extensions and a list of available
        extensions on Scrapy see [[Extensions]{.std
        .std-ref}](index.html#topics-extensions){.hoverxref .tooltip
        .reference .internal}.

    [[engine]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.Crawler.engine "Permalink to this definition"){.headerlink}

    :   The execution engine, which coordinates the core crawling logic
        between the scheduler, downloader and spiders.

        Some extension may want to access the Scrapy engine, to inspect
        or modify the downloader and scheduler behaviour, although this
        is an advanced use and this API is not yet stable.

    [[spider]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.Crawler.spider "Permalink to this definition"){.headerlink}

    :   Spider currently being crawled. This is an instance of the
        spider class provided while constructing the crawler, and it is
        created after the arguments given in the [[`crawl()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler.crawl "scrapy.crawler.Crawler.crawl"){.reference
        .internal} method.

    [[crawl]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[\*]{.pre}]{.o}[[args]{.pre}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#Crawler.crawl){.reference .internal}[¶](#scrapy.crawler.Crawler.crawl "Permalink to this definition"){.headerlink}

    :   Starts the crawler by instantiating its spider class with the
        given [`args`{.docutils .literal .notranslate}]{.pre} and
        [`kwargs`{.docutils .literal .notranslate}]{.pre} arguments,
        while setting the execution engine in motion. Should be called
        only once.

        Returns a deferred that is fired when the crawl is finished.

    [[stop]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[Generator]{.pre}](https://docs.python.org/3/library/typing.html#typing.Generator "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#Crawler.stop){.reference .internal}[¶](#scrapy.crawler.Crawler.stop "Permalink to this definition"){.headerlink}

    :   Starts a graceful stop of the crawler and returns a deferred
        that is fired when the crawler is stopped.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.crawler.]{.pre}]{.sig-prename .descclassname}[[CrawlerRunner]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[settings]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Settings]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference .internal}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#CrawlerRunner){.reference .internal}[¶](#scrapy.crawler.CrawlerRunner "Permalink to this definition"){.headerlink}

:   This is a convenient helper class that keeps track of, manages and
    runs crawlers inside an already setup [[`reactor`{.xref .py .py-mod
    .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
    .external}.

    The CrawlerRunner object must be instantiated with a
    [[`Settings`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
    .internal} object.

    This class shouldn't be needed (since Scrapy is responsible of using
    it accordingly) unless writing scripts that manually handle the
    crawling process. See [[Run Scrapy from a script]{.std
    .std-ref}](index.html#run-from-script){.hoverxref .tooltip
    .reference .internal} for an example.

    [[crawl]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler_or_spidercls]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Type]{.pre}](https://docs.python.org/3/library/typing.html#typing.Type "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}[[\]]{.pre}]{.p}]{.n}*, *[[\*]{.pre}]{.o}[[args]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#CrawlerRunner.crawl){.reference .internal}[¶](#scrapy.crawler.CrawlerRunner.crawl "Permalink to this definition"){.headerlink}

    :   Run a crawler with the provided arguments.

        It will call the given Crawler's [[`crawl()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler.crawl "scrapy.crawler.Crawler.crawl"){.reference
        .internal} method, while keeping track of it so it can be
        stopped later.

        If [`crawler_or_spidercls`{.docutils .literal
        .notranslate}]{.pre} isn't a [[`Crawler`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} instance, this method will try to create one using
        this parameter as the spider class given to it.

        Returns a deferred that is fired when the crawling is finished.

        Parameters

        :   -   **crawler_or_spidercls** ([[`Crawler`{.xref .py
                .py-class .docutils .literal
                .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
                .internal} instance, [[`Spider`{.xref .py .py-class
                .docutils .literal
                .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
                .internal} subclass or string) -- already created
                crawler, or a spider class or spider's name inside the
                project to create it

            -   **args** -- arguments to initialize the spider

            -   **kwargs** -- keyword arguments to initialize the spider

    *[property]{.pre}[ ]{.w}*[[crawlers]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.CrawlerRunner.crawlers "Permalink to this definition"){.headerlink}

    :   Set of [[`crawlers`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} started by [[`crawl()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.crawler.CrawlerRunner.crawl "scrapy.crawler.CrawlerRunner.crawl"){.reference
        .internal} and managed by this class.

    [[create_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler_or_spidercls]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Type]{.pre}](https://docs.python.org/3/library/typing.html#typing.Type "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#CrawlerRunner.create_crawler){.reference .internal}[¶](#scrapy.crawler.CrawlerRunner.create_crawler "Permalink to this definition"){.headerlink}

    :   Return a [[`Crawler`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} object.

        -   If [`crawler_or_spidercls`{.docutils .literal
            .notranslate}]{.pre} is a Crawler, it is returned as-is.

        -   If [`crawler_or_spidercls`{.docutils .literal
            .notranslate}]{.pre} is a Spider subclass, a new Crawler is
            constructed for it.

        -   If [`crawler_or_spidercls`{.docutils .literal
            .notranslate}]{.pre} is a string, this function finds a
            spider with this name in a Scrapy project (using spider
            loader), then creates a Crawler instance for it.

    [[join]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#CrawlerRunner.join){.reference .internal}[¶](#scrapy.crawler.CrawlerRunner.join "Permalink to this definition"){.headerlink}

    :   Returns a deferred that is fired when all managed
        [[`crawlers`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.CrawlerRunner.crawlers "scrapy.crawler.CrawlerRunner.crawlers"){.reference
        .internal} have completed their executions.

    [[stop]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#CrawlerRunner.stop){.reference .internal}[¶](#scrapy.crawler.CrawlerRunner.stop "Permalink to this definition"){.headerlink}

    :   Stops simultaneously all the crawling jobs taking place.

        Returns a deferred that is fired when they all have ended.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.crawler.]{.pre}]{.sig-prename .descclassname}[[CrawlerProcess]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[settings]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Settings]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference .internal}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[install_root_handler]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#CrawlerProcess){.reference .internal}[¶](#scrapy.crawler.CrawlerProcess "Permalink to this definition"){.headerlink}

:   Bases: [[`CrawlerRunner`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
    .internal}

    A class to run multiple scrapy crawlers in a process simultaneously.

    This class extends [[`CrawlerRunner`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
    .internal} by adding support for starting a [[`reactor`{.xref .py
    .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
    .external} and handling shutdown signals, like the keyboard
    interrupt command Ctrl-C. It also configures top-level logging.

    This utility should be a better fit than [[`CrawlerRunner`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.crawler.CrawlerRunner "scrapy.crawler.CrawlerRunner"){.reference
    .internal} if you aren't running another [[`reactor`{.xref .py
    .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
    .external} within your application.

    The CrawlerProcess object must be instantiated with a
    [[`Settings`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
    .internal} object.

    Parameters

    :   **install_root_handler** -- whether to install root logging
        handler (default: True)

    This class shouldn't be needed (since Scrapy is responsible of using
    it accordingly) unless writing scripts that manually handle the
    crawling process. See [[Run Scrapy from a script]{.std
    .std-ref}](index.html#run-from-script){.hoverxref .tooltip
    .reference .internal} for an example.

    [[crawl]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler_or_spidercls]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Type]{.pre}](https://docs.python.org/3/library/typing.html#typing.Type "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}[[\]]{.pre}]{.p}]{.n}*, *[[\*]{.pre}]{.o}[[args]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[¶](#scrapy.crawler.CrawlerProcess.crawl "Permalink to this definition"){.headerlink}

    :   Run a crawler with the provided arguments.

        It will call the given Crawler's [[`crawl()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler.crawl "scrapy.crawler.Crawler.crawl"){.reference
        .internal} method, while keeping track of it so it can be
        stopped later.

        If [`crawler_or_spidercls`{.docutils .literal
        .notranslate}]{.pre} isn't a [[`Crawler`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} instance, this method will try to create one using
        this parameter as the spider class given to it.

        Returns a deferred that is fired when the crawling is finished.

        Parameters

        :   -   **crawler_or_spidercls** ([[`Crawler`{.xref .py
                .py-class .docutils .literal
                .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
                .internal} instance, [[`Spider`{.xref .py .py-class
                .docutils .literal
                .notranslate}]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference
                .internal} subclass or string) -- already created
                crawler, or a spider class or spider's name inside the
                project to create it

            -   **args** -- arguments to initialize the spider

            -   **kwargs** -- keyword arguments to initialize the spider

    *[property]{.pre}[ ]{.w}*[[crawlers]{.pre}]{.sig-name .descname}[¶](#scrapy.crawler.CrawlerProcess.crawlers "Permalink to this definition"){.headerlink}

    :   Set of [[`crawlers`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} started by [[`crawl()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.crawler.CrawlerProcess.crawl "scrapy.crawler.CrawlerProcess.crawl"){.reference
        .internal} and managed by this class.

    [[create_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler_or_spidercls]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Type]{.pre}](https://docs.python.org/3/library/typing.html#typing.Type "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}]{.sig-return-typehint}]{.sig-return}[¶](#scrapy.crawler.CrawlerProcess.create_crawler "Permalink to this definition"){.headerlink}

    :   Return a [[`Crawler`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} object.

        -   If [`crawler_or_spidercls`{.docutils .literal
            .notranslate}]{.pre} is a Crawler, it is returned as-is.

        -   If [`crawler_or_spidercls`{.docutils .literal
            .notranslate}]{.pre} is a Spider subclass, a new Crawler is
            constructed for it.

        -   If [`crawler_or_spidercls`{.docutils .literal
            .notranslate}]{.pre} is a string, this function finds a
            spider with this name in a Scrapy project (using spider
            loader), then creates a Crawler instance for it.

    [[join]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[¶](#scrapy.crawler.CrawlerProcess.join "Permalink to this definition"){.headerlink}

    :   Returns a deferred that is fired when all managed
        [[`crawlers`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.CrawlerProcess.crawlers "scrapy.crawler.CrawlerProcess.crawlers"){.reference
        .internal} have completed their executions.

    [[start]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[stop_after_crawl]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*, *[[install_signal_handlers]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/crawler.html#CrawlerProcess.start){.reference .internal}[¶](#scrapy.crawler.CrawlerProcess.start "Permalink to this definition"){.headerlink}

    :   This method starts a [[`reactor`{.xref .py .py-mod .docutils
        .literal
        .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.reactor.html "(in Twisted)"){.reference
        .external}, adjusts its pool size to
        [[`REACTOR_THREADPOOL_MAXSIZE`{.xref .std .std-setting .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-setting-REACTOR_THREADPOOL_MAXSIZE){.hoverxref
        .tooltip .reference .internal}, and installs a DNS cache based
        on [[`DNSCACHE_ENABLED`{.xref .std .std-setting .docutils
        .literal
        .notranslate}]{.pre}](index.html#std-setting-DNSCACHE_ENABLED){.hoverxref
        .tooltip .reference .internal} and [[`DNSCACHE_SIZE`{.xref .std
        .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-DNSCACHE_SIZE){.hoverxref
        .tooltip .reference .internal}.

        If [`stop_after_crawl`{.docutils .literal .notranslate}]{.pre}
        is True, the reactor will be stopped after all crawlers have
        finished, using [[`join()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.crawler.CrawlerProcess.join "scrapy.crawler.CrawlerProcess.join"){.reference
        .internal}.

        Parameters

        :   -   **stop_after_crawl**
                ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
                .external}) -- stop or not the reactor when all crawlers
                have finished

            -   **install_signal_handlers**
                ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
                .external}) -- whether to install the OS signal handlers
                from Twisted and Scrapy (default: True)

    [[stop]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[¶](#scrapy.crawler.CrawlerProcess.stop "Permalink to this definition"){.headerlink}

    :   Stops simultaneously all the crawling jobs taking place.

        Returns a deferred that is fired when they all have ended.
:::

::: {#module-scrapy.settings .section}
[]{#settings-api}[]{#topics-api-settings}

#### Settings API[¶](#module-scrapy.settings "Permalink to this heading"){.headerlink}

[[scrapy.settings.]{.pre}]{.sig-prename .descclassname}[[SETTINGS_PRIORITIES]{.pre}]{.sig-name .descname}[¶](#scrapy.settings.SETTINGS_PRIORITIES "Permalink to this definition"){.headerlink}

:   Dictionary that sets the key name and priority level of the default
    settings priorities used in Scrapy.

    Each item defines a settings entry point, giving it a code name for
    identification and an integer priority. Greater priorities take more
    precedence over lesser ones when setting and retrieving values in
    the [[`Settings`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
    .internal} class.

    ::: {.highlight-python .notranslate}
    ::: highlight
        SETTINGS_PRIORITIES = {
            "default": 0,
            "command": 10,
            "addon": 15,
            "project": 20,
            "spider": 30,
            "cmdline": 40,
        }
    :::
    :::

    For a detailed explanation on each settings sources, see:
    [[Settings]{.std .std-ref}](index.html#topics-settings){.hoverxref
    .tooltip .reference .internal}.

```{=html}
<!-- -->
```

[[scrapy.settings.]{.pre}]{.sig-prename .descclassname}[[get_settings_priority]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#get_settings_priority){.reference .internal}[¶](#scrapy.settings.get_settings_priority "Permalink to this definition"){.headerlink}

:   Small helper function that looks up a given string priority in the
    [[`SETTINGS_PRIORITIES`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.SETTINGS_PRIORITIES "scrapy.settings.SETTINGS_PRIORITIES"){.reference
    .internal} dictionary and returns its numerical value, or directly
    returns a given numerical priority.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.settings.]{.pre}]{.sig-prename .descclassname}[[Settings]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[values]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[\_SettingsInputT]{.pre}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[Union]{.pre}[[\[]{.pre}]{.p}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'project\']{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#Settings){.reference .internal}[¶](#scrapy.settings.Settings "Permalink to this definition"){.headerlink}

:   Bases: [[`BaseSettings`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.BaseSettings "scrapy.settings.BaseSettings"){.reference
    .internal}

    This object stores Scrapy settings for the configuration of internal
    components, and can be used for any further customization.

    It is a direct subclass and supports all methods of
    [[`BaseSettings`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.BaseSettings "scrapy.settings.BaseSettings"){.reference
    .internal}. Additionally, after instantiation of this class, the new
    object will have the global default settings described on [[Built-in
    settings reference]{.std
    .std-ref}](index.html#topics-settings-ref){.hoverxref .tooltip
    .reference .internal} already populated.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.settings.]{.pre}]{.sig-prename .descclassname}[[BaseSettings]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[values]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[\_SettingsInputT]{.pre}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[Union]{.pre}[[\[]{.pre}]{.p}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'project\']{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings){.reference .internal}[¶](#scrapy.settings.BaseSettings "Permalink to this definition"){.headerlink}

:   Instances of this class behave like dictionaries, but store
    priorities along with their [`(key,`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`value)`{.docutils .literal .notranslate}]{.pre}
    pairs, and can be frozen (i.e. marked immutable).

    Key-value entries can be passed on initialization with the
    [`values`{.docutils .literal .notranslate}]{.pre} argument, and they
    would take the [`priority`{.docutils .literal .notranslate}]{.pre}
    level (unless [`values`{.docutils .literal .notranslate}]{.pre} is
    already an instance of [[`BaseSettings`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.BaseSettings "scrapy.settings.BaseSettings"){.reference
    .internal}, in which case the existing priority levels will be
    kept). If the [`priority`{.docutils .literal .notranslate}]{.pre}
    argument is a string, the priority name will be looked up in
    [[`SETTINGS_PRIORITIES`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.SETTINGS_PRIORITIES "scrapy.settings.SETTINGS_PRIORITIES"){.reference
    .internal}. Otherwise, a specific integer should be provided.

    Once the object is created, new settings can be loaded or updated
    with the [[`set()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.BaseSettings.set "scrapy.settings.BaseSettings.set"){.reference
    .internal} method, and can be accessed with the square bracket
    notation of dictionaries, or with the [[`get()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.settings.BaseSettings.get "scrapy.settings.BaseSettings.get"){.reference
    .internal} method of the instance and its value conversion variants.
    When requesting a stored key, the value with the highest priority
    will be retrieved.

    [[copy]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[Self]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.copy){.reference .internal}[¶](#scrapy.settings.BaseSettings.copy "Permalink to this definition"){.headerlink}

    :   Make a deep copy of current settings.

        This method returns a new instance of the [[`Settings`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
        .internal} class, populated with the same values and their
        priorities.

        Modifications to the new object won't be reflected on the
        original settings.

    [[copy_to_dict]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.copy_to_dict){.reference .internal}[¶](#scrapy.settings.BaseSettings.copy_to_dict "Permalink to this definition"){.headerlink}

    :   Make a copy of current settings and convert to a dict.

        This method returns a new dict populated with the same values
        and their priorities as the current settings.

        Modifications to the returned dict won't be reflected on the
        original settings.

        This method can be useful for example for printing settings in
        Scrapy shell.

    [[freeze]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.freeze){.reference .internal}[¶](#scrapy.settings.BaseSettings.freeze "Permalink to this definition"){.headerlink}

    :   Disable further changes to the current settings.

        After calling this method, the present state of the settings
        will become immutable. Trying to change values through the
        [[`set()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings.set "scrapy.settings.BaseSettings.set"){.reference
        .internal} method and its variants won't be possible and will be
        alerted.

    [[frozencopy]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[Self]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.frozencopy){.reference .internal}[¶](#scrapy.settings.BaseSettings.frozencopy "Permalink to this definition"){.headerlink}

    :   Return an immutable copy of the current settings.

        Alias for a [[`freeze()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings.freeze "scrapy.settings.BaseSettings.freeze"){.reference
        .internal} call in the object returned by [[`copy()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings.copy "scrapy.settings.BaseSettings.copy"){.reference
        .internal}.

    [[get]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.get){.reference .internal}[¶](#scrapy.settings.BaseSettings.get "Permalink to this definition"){.headerlink}

    :   Get a setting value without affecting its original type.

        Parameters

        :   -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the setting name

            -   **default**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the value to return if no setting is
                found

    [[getbool]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getbool){.reference .internal}[¶](#scrapy.settings.BaseSettings.getbool "Permalink to this definition"){.headerlink}

    :   Get a setting value as a boolean.

        [`1`{.docutils .literal .notranslate}]{.pre}, [`'1'`{.docutils
        .literal .notranslate}]{.pre}, True\` and [`'True'`{.docutils
        .literal .notranslate}]{.pre} return [`True`{.docutils .literal
        .notranslate}]{.pre}, while [`0`{.docutils .literal
        .notranslate}]{.pre}, [`'0'`{.docutils .literal
        .notranslate}]{.pre}, [`False`{.docutils .literal
        .notranslate}]{.pre}, [`'False'`{.docutils .literal
        .notranslate}]{.pre} and [`None`{.docutils .literal
        .notranslate}]{.pre} return [`False`{.docutils .literal
        .notranslate}]{.pre}.

        For example, settings populated through environment variables
        set to [`'0'`{.docutils .literal .notranslate}]{.pre} will
        return [`False`{.docutils .literal .notranslate}]{.pre} when
        using this method.

        Parameters

        :   -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the setting name

            -   **default**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the value to return if no setting is
                found

    [[getdict]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getdict){.reference .internal}[¶](#scrapy.settings.BaseSettings.getdict "Permalink to this definition"){.headerlink}

    :   Get a setting value as a dictionary. If the setting original
        type is a dictionary, a copy of it will be returned. If it is a
        string it will be evaluated as a JSON dictionary. In the case
        that it is a [[`BaseSettings`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings "scrapy.settings.BaseSettings"){.reference
        .internal} instance itself, it will be converted to a
        dictionary, containing all its current settings values as they
        would be returned by [[`get()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings.get "scrapy.settings.BaseSettings.get"){.reference
        .internal}, and losing all information about priority and
        mutability.

        Parameters

        :   -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the setting name

            -   **default**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the value to return if no setting is
                found

    [[getdictorlist]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getdictorlist){.reference .internal}[¶](#scrapy.settings.BaseSettings.getdictorlist "Permalink to this definition"){.headerlink}

    :   Get a setting value as either a [[`dict`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
        .external} or a [[`list`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
        .external}.

        If the setting is already a dict or a list, a copy of it will be
        returned.

        If it is a string it will be evaluated as JSON, or as a
        comma-separated list of strings as a fallback.

        For example, settings populated from the command line will
        return:

        -   [`{'key1':`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`'value1',`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`'key2':`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`'value2'}`{.docutils .literal
            .notranslate}]{.pre} if set to [`'{"key1":`{.docutils
            .literal .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`"value1",`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`"key2":`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`"value2"}'`{.docutils .literal
            .notranslate}]{.pre}

        -   [`['one',`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`'two']`{.docutils .literal
            .notranslate}]{.pre} if set to [`'["one",`{.docutils
            .literal .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`"two"]'`{.docutils .literal
            .notranslate}]{.pre} or [`'one,two'`{.docutils .literal
            .notranslate}]{.pre}

        Parameters

        :   -   **name** (*string*) -- the setting name

            -   **default** (*any*) -- the value to return if no setting
                is found

    [[getfloat]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[0.0]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getfloat){.reference .internal}[¶](#scrapy.settings.BaseSettings.getfloat "Permalink to this definition"){.headerlink}

    :   Get a setting value as a float.

        Parameters

        :   -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the setting name

            -   **default**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the value to return if no setting is
                found

    [[getint]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[0]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getint){.reference .internal}[¶](#scrapy.settings.BaseSettings.getint "Permalink to this definition"){.headerlink}

    :   Get a setting value as an int.

        Parameters

        :   -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the setting name

            -   **default**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the value to return if no setting is
                found

    [[getlist]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[default]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getlist){.reference .internal}[¶](#scrapy.settings.BaseSettings.getlist "Permalink to this definition"){.headerlink}

    :   Get a setting value as a list. If the setting original type is a
        list, a copy of it will be returned. If it's a string it will be
        split by ",".

        For example, settings populated through environment variables
        set to [`'one,two'`{.docutils .literal .notranslate}]{.pre} will
        return a list \['one', 'two'\] when using this method.

        Parameters

        :   -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the setting name

            -   **default**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the value to return if no setting is
                found

    [[getpriority]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getpriority){.reference .internal}[¶](#scrapy.settings.BaseSettings.getpriority "Permalink to this definition"){.headerlink}

    :   Return the current numerical priority value of a setting, or
        [`None`{.docutils .literal .notranslate}]{.pre} if the given
        [`name`{.docutils .literal .notranslate}]{.pre} does not exist.

        Parameters

        :   **name**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the setting name

    [[getwithbase]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[BaseSettings]{.pre}](index.html#scrapy.settings.BaseSettings "scrapy.settings.BaseSettings"){.reference .internal}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.getwithbase){.reference .internal}[¶](#scrapy.settings.BaseSettings.getwithbase "Permalink to this definition"){.headerlink}

    :   Get a composition of a dictionary-like setting and its \_BASE
        counterpart.

        Parameters

        :   **name**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- name of the dictionary-like setting

    [[maxpriority]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren} [[→]{.sig-return-icon} [[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.maxpriority){.reference .internal}[¶](#scrapy.settings.BaseSettings.maxpriority "Permalink to this definition"){.headerlink}

    :   Return the numerical value of the highest priority present
        throughout all settings, or the numerical value for
        [`default`{.docutils .literal .notranslate}]{.pre} from
        [[`SETTINGS_PRIORITIES`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.settings.SETTINGS_PRIORITIES "scrapy.settings.SETTINGS_PRIORITIES"){.reference
        .internal} if there are no settings stored.

    [[pop]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[k]{.pre}]{.n}*[\[]{.optional}, *[[d]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren} [[→]{.sig-return-icon} [[v,]{.pre} [remove]{.pre} [specified]{.pre} [key]{.pre} [and]{.pre} [return]{.pre} [the]{.pre} [corresponding]{.pre} [value.]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.pop){.reference .internal}[¶](#scrapy.settings.BaseSettings.pop "Permalink to this definition"){.headerlink}

    :   If key is not found, d is returned if given, otherwise KeyError
        is raised.

    [[set]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[name]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[float]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[value]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'project\']{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.set){.reference .internal}[¶](#scrapy.settings.BaseSettings.set "Permalink to this definition"){.headerlink}

    :   Store a key/value attribute with a given priority.

        Settings should be populated *before* configuring the Crawler
        object (through the [`configure()`{.xref .py .py-meth .docutils
        .literal .notranslate}]{.pre} method), otherwise they won't have
        any effect.

        Parameters

        :   -   **name**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the setting name

            -   **value**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the value to associate with the setting

            -   **priority**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
                .external}) -- the priority of the setting. Should be a
                key of [[`SETTINGS_PRIORITIES`{.xref .py .py-attr
                .docutils .literal
                .notranslate}]{.pre}](#scrapy.settings.SETTINGS_PRIORITIES "scrapy.settings.SETTINGS_PRIORITIES"){.reference
                .internal} or an integer

    [[setdefault]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[k]{.pre}]{.n}*[\[]{.optional}, *[[d]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren} [[→]{.sig-return-icon} [[D.get(k,d),]{.pre} [also]{.pre} [set]{.pre} [D\[k\]=d]{.pre} [if]{.pre} [k]{.pre} [not]{.pre} [in]{.pre} [D]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.setdefault){.reference .internal}[¶](#scrapy.settings.BaseSettings.setdefault "Permalink to this definition"){.headerlink}

    :   

    [[setmodule]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[module]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[module]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'project\']{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.setmodule){.reference .internal}[¶](#scrapy.settings.BaseSettings.setmodule "Permalink to this definition"){.headerlink}

    :   Store settings from a module with a given priority.

        This is a helper function that calls [[`set()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings.set "scrapy.settings.BaseSettings.set"){.reference
        .internal} for every globally declared uppercase variable of
        [`module`{.docutils .literal .notranslate}]{.pre} with the
        provided [`priority`{.docutils .literal .notranslate}]{.pre}.

        Parameters

        :   -   **module**
                ([*types.ModuleType*](https://docs.python.org/3/library/types.html#types.ModuleType "(in Python v3.12)"){.reference
                .external} *or*
                [*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- the module or the path of the module

            -   **priority**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
                .external}) -- the priority of the settings. Should be a
                key of [[`SETTINGS_PRIORITIES`{.xref .py .py-attr
                .docutils .literal
                .notranslate}]{.pre}](#scrapy.settings.SETTINGS_PRIORITIES "scrapy.settings.SETTINGS_PRIORITIES"){.reference
                .internal} or an integer

    [[update]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[values]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[\_SettingsInputT]{.pre}]{.n}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[Union]{.pre}[[\[]{.pre}]{.p}[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'project\']{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/settings.html#BaseSettings.update){.reference .internal}[¶](#scrapy.settings.BaseSettings.update "Permalink to this definition"){.headerlink}

    :   Store key/value pairs with a given priority.

        This is a helper function that calls [[`set()`{.xref .py
        .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings.set "scrapy.settings.BaseSettings.set"){.reference
        .internal} for every item of [`values`{.docutils .literal
        .notranslate}]{.pre} with the provided [`priority`{.docutils
        .literal .notranslate}]{.pre}.

        If [`values`{.docutils .literal .notranslate}]{.pre} is a
        string, it is assumed to be JSON-encoded and parsed into a dict
        with [`json.loads()`{.docutils .literal .notranslate}]{.pre}
        first. If it is a [[`BaseSettings`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.settings.BaseSettings "scrapy.settings.BaseSettings"){.reference
        .internal} instance, the per-key priorities will be used and the
        [`priority`{.docutils .literal .notranslate}]{.pre} parameter
        ignored. This allows inserting/updating settings with different
        priorities with a single command.

        Parameters

        :   -   **values** (dict or string or [[`BaseSettings`{.xref .py
                .py-class .docutils .literal
                .notranslate}]{.pre}](#scrapy.settings.BaseSettings "scrapy.settings.BaseSettings"){.reference
                .internal}) -- the settings names and values

            -   **priority**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external} *or*
                [*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
                .external}) -- the priority of the settings. Should be a
                key of [[`SETTINGS_PRIORITIES`{.xref .py .py-attr
                .docutils .literal
                .notranslate}]{.pre}](#scrapy.settings.SETTINGS_PRIORITIES "scrapy.settings.SETTINGS_PRIORITIES"){.reference
                .internal} or an integer
:::

::: {#module-scrapy.spiderloader .section}
[]{#spiderloader-api}[]{#topics-api-spiderloader}

#### SpiderLoader API[¶](#module-scrapy.spiderloader "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.spiderloader.]{.pre}]{.sig-prename .descclassname}[[SpiderLoader]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiderloader.html#SpiderLoader){.reference .internal}[¶](#scrapy.spiderloader.SpiderLoader "Permalink to this definition"){.headerlink}

:   This class is in charge of retrieving and handling the spider
    classes defined across the project.

    Custom spider loaders can be employed by specifying their path in
    the [[`SPIDER_LOADER_CLASS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-SPIDER_LOADER_CLASS){.hoverxref
    .tooltip .reference .internal} project setting. They must fully
    implement the [`scrapy.interfaces.ISpiderLoader`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} interface to guarantee an
    errorless execution.

    [[from_settings]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[settings]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiderloader.html#SpiderLoader.from_settings){.reference .internal}[¶](#scrapy.spiderloader.SpiderLoader.from_settings "Permalink to this definition"){.headerlink}

    :   This class method is used by Scrapy to create an instance of the
        class. It's called with the current project settings, and it
        loads the spiders found recursively in the modules of the
        [[`SPIDER_MODULES`{.xref .std .std-setting .docutils .literal
        .notranslate}]{.pre}](index.html#std-setting-SPIDER_MODULES){.hoverxref
        .tooltip .reference .internal} setting.

        Parameters

        :   **settings** ([[`Settings`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
            .internal} instance) -- project settings

    [[load]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider_name]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiderloader.html#SpiderLoader.load){.reference .internal}[¶](#scrapy.spiderloader.SpiderLoader.load "Permalink to this definition"){.headerlink}

    :   Get the Spider class with the given name. It'll look into the
        previously loaded spiders for a spider class with name
        [`spider_name`{.docutils .literal .notranslate}]{.pre} and will
        raise a KeyError if not found.

        Parameters

        :   **spider_name**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- spider class name

    [[list]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiderloader.html#SpiderLoader.list){.reference .internal}[¶](#scrapy.spiderloader.SpiderLoader.list "Permalink to this definition"){.headerlink}

    :   Get the names of the available spiders in the project.

    [[find_by_request]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/spiderloader.html#SpiderLoader.find_by_request){.reference .internal}[¶](#scrapy.spiderloader.SpiderLoader.find_by_request "Permalink to this definition"){.headerlink}

    :   List the spiders' names that can handle the given request. Will
        try to match the request's url against the domains of the
        spiders.

        Parameters

        :   **request** ([`Request`{.xref .py .py-class .docutils
            .literal .notranslate}]{.pre} instance) -- queried request
:::

::: {#module-scrapy.signalmanager .section}
[]{#signals-api}[]{#topics-api-signals}

#### Signals API[¶](#module-scrapy.signalmanager "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.signalmanager.]{.pre}]{.sig-prename .descclassname}[[SignalManager]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[sender]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\_Anonymous]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/signalmanager.html#SignalManager){.reference .internal}[¶](#scrapy.signalmanager.SignalManager "Permalink to this definition"){.headerlink}

:   

    [[connect]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[receiver]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[signal]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/signalmanager.html#SignalManager.connect){.reference .internal}[¶](#scrapy.signalmanager.SignalManager.connect "Permalink to this definition"){.headerlink}

    :   Connect a receiver function to a signal.

        The signal can be any object, although Scrapy comes with some
        predefined signals that are documented in the [[Signals]{.std
        .std-ref}](index.html#topics-signals){.hoverxref .tooltip
        .reference .internal} section.

        Parameters

        :   -   **receiver**
                ([*collections.abc.Callable*](https://docs.python.org/3/library/collections.abc.html#collections.abc.Callable "(in Python v3.12)"){.reference
                .external}) -- the function to be connected

            -   **signal**
                ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
                .external}) -- the signal to connect to

    [[disconnect]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[receiver]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[signal]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/signalmanager.html#SignalManager.disconnect){.reference .internal}[¶](#scrapy.signalmanager.SignalManager.disconnect "Permalink to this definition"){.headerlink}

    :   Disconnect a receiver function from a signal. This has the
        opposite effect of the [[`connect()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.signalmanager.SignalManager.connect "scrapy.signalmanager.SignalManager.connect"){.reference
        .internal} method, and the arguments are the same.

    [[disconnect_all]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[signal]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/signalmanager.html#SignalManager.disconnect_all){.reference .internal}[¶](#scrapy.signalmanager.SignalManager.disconnect_all "Permalink to this definition"){.headerlink}

    :   Disconnect all receivers from the given signal.

        Parameters

        :   **signal**
            ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
            .external}) -- the signal to disconnect from

    [[send_catch_log]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[signal]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/signalmanager.html#SignalManager.send_catch_log){.reference .internal}[¶](#scrapy.signalmanager.SignalManager.send_catch_log "Permalink to this definition"){.headerlink}

    :   Send a signal, catch exceptions and log them.

        The keyword arguments are passed to the signal handlers
        (connected through the [[`connect()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.signalmanager.SignalManager.connect "scrapy.signalmanager.SignalManager.connect"){.reference
        .internal} method).

    [[send_catch_log_deferred]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[signal]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Deferred]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/signalmanager.html#SignalManager.send_catch_log_deferred){.reference .internal}[¶](#scrapy.signalmanager.SignalManager.send_catch_log_deferred "Permalink to this definition"){.headerlink}

    :   Like [[`send_catch_log()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.signalmanager.SignalManager.send_catch_log "scrapy.signalmanager.SignalManager.send_catch_log"){.reference
        .internal} but supports returning [[`Deferred`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.defer.Deferred.html "(in Twisted)"){.reference
        .external} objects from signal handlers.

        Returns a Deferred that gets fired once all signal handlers
        deferreds were fired. Send a signal, catch exceptions and log
        them.

        The keyword arguments are passed to the signal handlers
        (connected through the [[`connect()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.signalmanager.SignalManager.connect "scrapy.signalmanager.SignalManager.connect"){.reference
        .internal} method).
:::

::: {#stats-collector-api .section}
[]{#topics-api-stats}

#### Stats Collector API[¶](#stats-collector-api "Permalink to this heading"){.headerlink}

There are several Stats Collectors available under the
[[`scrapy.statscollectors`{.xref .py .py-mod .docutils .literal
.notranslate}]{.pre}](#module-scrapy.statscollectors "scrapy.statscollectors: Stats Collectors"){.reference
.internal} module and they all implement the Stats Collector API defined
by the [[`StatsCollector`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.statscollectors.StatsCollector "scrapy.statscollectors.StatsCollector"){.reference
.internal} class (which they all inherit from).

[]{#module-scrapy.statscollectors .target}

*[class]{.pre}[ ]{.w}*[[scrapy.statscollectors.]{.pre}]{.sig-prename .descclassname}[[StatsCollector]{.pre}]{.sig-name .descname}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector "Permalink to this definition"){.headerlink}

:   

    [[get_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[key]{.pre}]{.n}*, *[[default]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.get_value){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.get_value "Permalink to this definition"){.headerlink}

    :   Return the value for the given stats key or default if it
        doesn't exist.

    [[get_stats]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.get_stats){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.get_stats "Permalink to this definition"){.headerlink}

    :   Get all stats from the currently running spider as a dict.

    [[set_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[key]{.pre}]{.n}*, *[[value]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.set_value){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.set_value "Permalink to this definition"){.headerlink}

    :   Set the given value for the given stats key.

    [[set_stats]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[stats]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.set_stats){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.set_stats "Permalink to this definition"){.headerlink}

    :   Override the current stats with the dict passed in
        [`stats`{.docutils .literal .notranslate}]{.pre} argument.

    [[inc_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[key]{.pre}]{.n}*, *[[count]{.pre}]{.n}[[=]{.pre}]{.o}[[1]{.pre}]{.default_value}*, *[[start]{.pre}]{.n}[[=]{.pre}]{.o}[[0]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.inc_value){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.inc_value "Permalink to this definition"){.headerlink}

    :   Increment the value of the given stats key, by the given count,
        assuming the start value given (when it's not set).

    [[max_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[key]{.pre}]{.n}*, *[[value]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.max_value){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.max_value "Permalink to this definition"){.headerlink}

    :   Set the given value for the given key only if current value for
        the same key is lower than value. If there is no current value
        for the given key, the value is always set.

    [[min_value]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[key]{.pre}]{.n}*, *[[value]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.min_value){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.min_value "Permalink to this definition"){.headerlink}

    :   Set the given value for the given key only if current value for
        the same key is greater than value. If there is no current value
        for the given key, the value is always set.

    [[clear_stats]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.clear_stats){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.clear_stats "Permalink to this definition"){.headerlink}

    :   Clear all stats.

    The following methods are not part of the stats collection api but
    instead used when implementing custom stats collectors:

    [[open_spider]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.open_spider){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.open_spider "Permalink to this definition"){.headerlink}

    :   Open the given spider for stats collection.

    [[close_spider]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[spider]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/statscollectors.html#StatsCollector.close_spider){.reference .internal}[¶](#scrapy.statscollectors.StatsCollector.close_spider "Permalink to this definition"){.headerlink}

    :   Close the given spider. After this is called, no more specific
        stats can be accessed or collected.
:::
:::
:::

[[Architecture overview]{.doc}](index.html#document-topics/architecture){.reference .internal}

:   Understand the Scrapy architecture.

[[Add-ons]{.doc}](index.html#document-topics/addons){.reference .internal}

:   Enable and configure third-party extensions.

[[Downloader Middleware]{.doc}](index.html#document-topics/downloader-middleware){.reference .internal}

:   Customize how pages get requested and downloaded.

[[Spider Middleware]{.doc}](index.html#document-topics/spider-middleware){.reference .internal}

:   Customize the input and output of your spiders.

[[Extensions]{.doc}](index.html#document-topics/extensions){.reference .internal}

:   Extend Scrapy with your custom functionality

[[Signals]{.doc}](index.html#document-topics/signals){.reference .internal}

:   See all available signals and how to work with them.

[[Scheduler]{.doc}](index.html#document-topics/scheduler){.reference .internal}

:   Understand the scheduler component.

[[Item Exporters]{.doc}](index.html#document-topics/exporters){.reference .internal}

:   Quickly export your scraped items to a file (XML, CSV, etc).

[[Components]{.doc}](index.html#document-topics/components){.reference .internal}

:   Learn the common API and some good practices when building custom
    Scrapy components.

[[Core API]{.doc}](index.html#document-topics/api){.reference .internal}

:   Use it on extensions and middlewares to extend Scrapy functionality.
:::

::: {#all-the-rest .section}
## All the rest[¶](#all-the-rest "Permalink to this heading"){.headerlink}

::: {.toctree-wrapper .compound}
[]{#document-news}

::: {#release-notes .section}
[]{#news}

### Release notes[¶](#release-notes "Permalink to this heading"){.headerlink}

::: {#scrapy-2-11-0-2023-09-18 .section}
[]{#release-2-11-0}

#### Scrapy 2.11.0 (2023-09-18)[¶](#scrapy-2-11-0-2023-09-18 "Permalink to this heading"){.headerlink}

Highlights:

-   Spiders can now modify [[settings]{.std
    .std-ref}](index.html#topics-settings){.hoverxref .tooltip
    .reference .internal} in their [[`from_crawler()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.from_crawler "scrapy.Spider.from_crawler"){.reference
    .internal} methods, e.g. based on [[spider arguments]{.std
    .std-ref}](index.html#spiderargs){.hoverxref .tooltip .reference
    .internal}.

-   Periodic logging of stats.

::: {#backward-incompatible-changes .section}
##### Backward-incompatible changes[¶](#backward-incompatible-changes "Permalink to this heading"){.headerlink}

-   Most of the initialization of [[`scrapy.crawler.Crawler`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal} instances is now done in [[`crawl()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.crawl "scrapy.crawler.Crawler.crawl"){.reference
    .internal}, so the state of instances before that method is called
    is now different compared to older Scrapy versions. We do not
    recommend using the [[`Crawler`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal} instances before [[`crawl()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.crawl "scrapy.crawler.Crawler.crawl"){.reference
    .internal} is called. ([issue
    6038](https://github.com/scrapy/scrapy/issues/6038){.reference
    .external})

-   [[`scrapy.Spider.from_crawler()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.from_crawler "scrapy.Spider.from_crawler"){.reference
    .internal} is now called before the initialization of various
    components previously initialized in
    [`scrapy.crawler.Crawler.__init__()`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre} and before the settings are finalized
    and frozen. This change was needed to allow changing the settings in
    [[`scrapy.Spider.from_crawler()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.from_crawler "scrapy.Spider.from_crawler"){.reference
    .internal}. If you want to access the final setting values and the
    initialized [[`Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal} attributes in the spider code as early as possible you
    can do this in [[`start_requests()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.start_requests "scrapy.Spider.start_requests"){.reference
    .internal} or in a handler of the [[`engine_started`{.xref .std
    .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-engine_started){.hoverxref
    .tooltip .reference .internal} signal. ([issue
    6038](https://github.com/scrapy/scrapy/issues/6038){.reference
    .external})

-   The [[`TextResponse.json`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.json "scrapy.http.TextResponse.json"){.reference
    .internal} method now requires the response to be in a valid JSON
    encoding (UTF-8, UTF-16, or UTF-32). If you need to deal with JSON
    documents in an invalid encoding, use
    [`json.loads(response.text)`{.docutils .literal .notranslate}]{.pre}
    instead. ([issue
    6016](https://github.com/scrapy/scrapy/issues/6016){.reference
    .external})

-   [[`PythonItemExporter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.PythonItemExporter "scrapy.exporters.PythonItemExporter"){.reference
    .internal} used the binary output by default but it no longer does.
    ([issue
    6006](https://github.com/scrapy/scrapy/issues/6006){.reference
    .external}, [issue
    6007](https://github.com/scrapy/scrapy/issues/6007){.reference
    .external})
:::

::: {#deprecation-removals .section}
##### Deprecation removals[¶](#deprecation-removals "Permalink to this heading"){.headerlink}

-   Removed the binary export mode of [[`PythonItemExporter`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exporters.PythonItemExporter "scrapy.exporters.PythonItemExporter"){.reference
    .internal}, deprecated in Scrapy 1.1.0. ([issue
    6006](https://github.com/scrapy/scrapy/issues/6006){.reference
    .external}, [issue
    6007](https://github.com/scrapy/scrapy/issues/6007){.reference
    .external})

    ::: {.admonition .note}
    Note

    If you are using this Scrapy version on Scrapy Cloud with a stack
    that includes an older Scrapy version and get a "TypeError:
    Unexpected options: binary" error, you may need to add
    [`scrapinghub-entrypoint-scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`>=`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`0.14.1`{.docutils .literal .notranslate}]{.pre} to
    your project requirements or switch to a stack that includes Scrapy
    2.11.
    :::

-   Removed the [`CrawlerRunner.spiders`{.docutils .literal
    .notranslate}]{.pre} attribute, deprecated in Scrapy 1.0.0, use
    [`CrawlerRunner.spider_loader`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre} instead. ([issue
    6010](https://github.com/scrapy/scrapy/issues/6010){.reference
    .external})
:::

::: {#deprecations .section}
##### Deprecations[¶](#deprecations "Permalink to this heading"){.headerlink}

-   Running [[`crawl()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.crawl "scrapy.crawler.Crawler.crawl"){.reference
    .internal} more than once on the same
    [[`scrapy.crawler.Crawler`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal} instance is now deprecated. ([issue
    1587](https://github.com/scrapy/scrapy/issues/1587){.reference
    .external}, [issue
    6040](https://github.com/scrapy/scrapy/issues/6040){.reference
    .external})
:::

::: {#new-features .section}
##### New features[¶](#new-features "Permalink to this heading"){.headerlink}

-   Spiders can now modify settings in their [[`from_crawler()`{.xref
    .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.from_crawler "scrapy.Spider.from_crawler"){.reference
    .internal} method, e.g. based on [[spider arguments]{.std
    .std-ref}](index.html#spiderargs){.hoverxref .tooltip .reference
    .internal}. ([issue
    1305](https://github.com/scrapy/scrapy/issues/1305){.reference
    .external}, [issue
    1580](https://github.com/scrapy/scrapy/issues/1580){.reference
    .external}, [issue
    2392](https://github.com/scrapy/scrapy/issues/2392){.reference
    .external}, [issue
    3663](https://github.com/scrapy/scrapy/issues/3663){.reference
    .external}, [issue
    6038](https://github.com/scrapy/scrapy/issues/6038){.reference
    .external})

-   Added the [[`PeriodicLog`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.extensions.periodic_log.PeriodicLog "scrapy.extensions.periodic_log.PeriodicLog"){.reference
    .internal} extension which can be enabled to log stats and/or their
    differences periodically. ([issue
    5926](https://github.com/scrapy/scrapy/issues/5926){.reference
    .external})

-   Optimized the memory usage in [[`TextResponse.json`{.xref .py
    .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse.json "scrapy.http.TextResponse.json"){.reference
    .internal} by removing unnecessary body decoding. ([issue
    5968](https://github.com/scrapy/scrapy/issues/5968){.reference
    .external}, [issue
    6016](https://github.com/scrapy/scrapy/issues/6016){.reference
    .external})

-   Links to [`.webp`{.docutils .literal .notranslate}]{.pre} files are
    now ignored by [[link extractors]{.std
    .std-ref}](index.html#topics-link-extractors){.hoverxref .tooltip
    .reference .internal}. ([issue
    6021](https://github.com/scrapy/scrapy/issues/6021){.reference
    .external})
:::

::: {#bug-fixes .section}
##### Bug fixes[¶](#bug-fixes "Permalink to this heading"){.headerlink}

-   Fixed logging enabled add-ons. ([issue
    6036](https://github.com/scrapy/scrapy/issues/6036){.reference
    .external})

-   Fixed [[`MailSender`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.mail.MailSender "scrapy.mail.MailSender"){.reference
    .internal} producing invalid message bodies when the
    [`charset`{.docutils .literal .notranslate}]{.pre} argument is
    passed to [[`send()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.mail.MailSender.send "scrapy.mail.MailSender.send"){.reference
    .internal}. ([issue
    5096](https://github.com/scrapy/scrapy/issues/5096){.reference
    .external}, [issue
    5118](https://github.com/scrapy/scrapy/issues/5118){.reference
    .external})

-   Fixed an exception when accessing
    [`self.EXCEPTIONS_TO_RETRY`{.docutils .literal .notranslate}]{.pre}
    from a subclass of [[`RetryMiddleware`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.RetryMiddleware "scrapy.downloadermiddlewares.retry.RetryMiddleware"){.reference
    .internal}. ([issue
    6049](https://github.com/scrapy/scrapy/issues/6049){.reference
    .external}, [issue
    6050](https://github.com/scrapy/scrapy/issues/6050){.reference
    .external})

-   [[`scrapy.settings.BaseSettings.getdictorlist()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.settings.BaseSettings.getdictorlist "scrapy.settings.BaseSettings.getdictorlist"){.reference
    .internal}, used to parse [[`FEED_EXPORT_FIELDS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_FIELDS){.hoverxref
    .tooltip .reference .internal}, now handles tuple values. ([issue
    6011](https://github.com/scrapy/scrapy/issues/6011){.reference
    .external}, [issue
    6013](https://github.com/scrapy/scrapy/issues/6013){.reference
    .external})

-   Calls to [`datetime.utcnow()`{.docutils .literal
    .notranslate}]{.pre}, no longer recommended to be used, have been
    replaced with calls to [`datetime.now()`{.docutils .literal
    .notranslate}]{.pre} with a timezone. ([issue
    6014](https://github.com/scrapy/scrapy/issues/6014){.reference
    .external})
:::

::: {#documentation .section}
##### Documentation[¶](#documentation "Permalink to this heading"){.headerlink}

-   Updated a deprecated function call in a pipeline example. ([issue
    6008](https://github.com/scrapy/scrapy/issues/6008){.reference
    .external}, [issue
    6009](https://github.com/scrapy/scrapy/issues/6009){.reference
    .external})
:::

::: {#quality-assurance .section}
##### Quality assurance[¶](#quality-assurance "Permalink to this heading"){.headerlink}

-   Extended typing hints. ([issue
    6003](https://github.com/scrapy/scrapy/issues/6003){.reference
    .external}, [issue
    6005](https://github.com/scrapy/scrapy/issues/6005){.reference
    .external}, [issue
    6031](https://github.com/scrapy/scrapy/issues/6031){.reference
    .external}, [issue
    6034](https://github.com/scrapy/scrapy/issues/6034){.reference
    .external})

-   Pinned [brotli](https://github.com/google/brotli){.reference
    .external} to 1.0.9 for the PyPy tests as 1.1.0 breaks them. ([issue
    6044](https://github.com/scrapy/scrapy/issues/6044){.reference
    .external}, [issue
    6045](https://github.com/scrapy/scrapy/issues/6045){.reference
    .external})

-   Other CI and pre-commit improvements. ([issue
    6002](https://github.com/scrapy/scrapy/issues/6002){.reference
    .external}, [issue
    6013](https://github.com/scrapy/scrapy/issues/6013){.reference
    .external}, [issue
    6046](https://github.com/scrapy/scrapy/issues/6046){.reference
    .external})
:::
:::

::: {#scrapy-2-10-1-2023-08-30 .section}
[]{#release-2-10-1}

#### Scrapy 2.10.1 (2023-08-30)[¶](#scrapy-2-10-1-2023-08-30 "Permalink to this heading"){.headerlink}

Marked [`Twisted`{.docutils .literal .notranslate}]{.pre}` `{.docutils
.literal .notranslate}[`>=`{.docutils .literal
.notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`23.8.0`{.docutils .literal .notranslate}]{.pre} as
unsupported. ([issue
6024](https://github.com/scrapy/scrapy/issues/6024){.reference
.external}, [issue
6026](https://github.com/scrapy/scrapy/issues/6026){.reference
.external})
:::

::: {#scrapy-2-10-0-2023-08-04 .section}
[]{#release-2-10-0}

#### Scrapy 2.10.0 (2023-08-04)[¶](#scrapy-2-10-0-2023-08-04 "Permalink to this heading"){.headerlink}

Highlights:

-   Added Python 3.12 support, dropped Python 3.7 support.

-   The new add-ons framework simplifies configuring 3rd-party
    components that support it.

-   Exceptions to retry can now be configured.

-   Many fixes and improvements for feed exports.

::: {#modified-requirements .section}
##### Modified requirements[¶](#modified-requirements "Permalink to this heading"){.headerlink}

-   Dropped support for Python 3.7. ([issue
    5953](https://github.com/scrapy/scrapy/issues/5953){.reference
    .external})

-   Added support for the upcoming Python 3.12. ([issue
    5984](https://github.com/scrapy/scrapy/issues/5984){.reference
    .external})

-   Minimum versions increased for these dependencies:

    -   [lxml](https://lxml.de/){.reference .external}: 4.3.0 → 4.4.1

    -   [cryptography](https://cryptography.io/en/latest/){.reference
        .external}: 3.4.6 → 36.0.0

-   [`pkg_resources`{.docutils .literal .notranslate}]{.pre} is no
    longer used. ([issue
    5956](https://github.com/scrapy/scrapy/issues/5956){.reference
    .external}, [issue
    5958](https://github.com/scrapy/scrapy/issues/5958){.reference
    .external})

-   [boto3](https://github.com/boto/boto3){.reference .external} is now
    recommended instead of
    [botocore](https://github.com/boto/botocore){.reference .external}
    for exporting to S3. ([issue
    5833](https://github.com/scrapy/scrapy/issues/5833){.reference
    .external}).
:::

::: {#id1 .section}
##### Backward-incompatible changes[¶](#id1 "Permalink to this heading"){.headerlink}

-   The value of the [[`FEED_STORE_EMPTY`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_STORE_EMPTY){.hoverxref
    .tooltip .reference .internal} setting is now [`True`{.docutils
    .literal .notranslate}]{.pre} instead of [`False`{.docutils .literal
    .notranslate}]{.pre}. In earlier Scrapy versions empty files were
    created even when this setting was [`False`{.docutils .literal
    .notranslate}]{.pre} (which was a bug that is now fixed), so the new
    default should keep the old behavior. ([issue
    872](https://github.com/scrapy/scrapy/issues/872){.reference
    .external}, [issue
    5847](https://github.com/scrapy/scrapy/issues/5847){.reference
    .external})
:::

::: {#id2 .section}
##### Deprecation removals[¶](#id2 "Permalink to this heading"){.headerlink}

-   When a function is assigned to the [[`FEED_URI_PARAMS`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_URI_PARAMS){.hoverxref
    .tooltip .reference .internal} setting, returning [`None`{.docutils
    .literal .notranslate}]{.pre} or modifying the [`params`{.docutils
    .literal .notranslate}]{.pre} input parameter, deprecated in Scrapy
    2.6, is no longer supported. ([issue
    5994](https://github.com/scrapy/scrapy/issues/5994){.reference
    .external}, [issue
    5996](https://github.com/scrapy/scrapy/issues/5996){.reference
    .external})

-   The [`scrapy.utils.reqser`{.docutils .literal .notranslate}]{.pre}
    module, deprecated in Scrapy 2.6, is removed. ([issue
    5994](https://github.com/scrapy/scrapy/issues/5994){.reference
    .external}, [issue
    5996](https://github.com/scrapy/scrapy/issues/5996){.reference
    .external})

-   The [`scrapy.squeues`{.docutils .literal .notranslate}]{.pre}
    classes [`PickleFifoDiskQueueNonRequest`{.docutils .literal
    .notranslate}]{.pre}, [`PickleLifoDiskQueueNonRequest`{.docutils
    .literal .notranslate}]{.pre},
    [`MarshalFifoDiskQueueNonRequest`{.docutils .literal
    .notranslate}]{.pre}, and
    [`MarshalLifoDiskQueueNonRequest`{.docutils .literal
    .notranslate}]{.pre}, deprecated in Scrapy 2.6, are removed. ([issue
    5994](https://github.com/scrapy/scrapy/issues/5994){.reference
    .external}, [issue
    5996](https://github.com/scrapy/scrapy/issues/5996){.reference
    .external})

-   The property [`open_spiders`{.docutils .literal .notranslate}]{.pre}
    and the methods [`has_capacity`{.docutils .literal
    .notranslate}]{.pre} and [`schedule`{.docutils .literal
    .notranslate}]{.pre} of [`scrapy.core.engine.ExecutionEngine`{.xref
    .py .py-class .docutils .literal .notranslate}]{.pre}, deprecated in
    Scrapy 2.6, are removed. ([issue
    5994](https://github.com/scrapy/scrapy/issues/5994){.reference
    .external}, [issue
    5998](https://github.com/scrapy/scrapy/issues/5998){.reference
    .external})

-   Passing a [`spider`{.docutils .literal .notranslate}]{.pre} argument
    to the [`spider_is_idle()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}, [`crawl()`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre} and [`download()`{.xref .py .py-meth
    .docutils .literal .notranslate}]{.pre} methods of
    [`scrapy.core.engine.ExecutionEngine`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre}, deprecated in Scrapy 2.6, is no
    longer supported. ([issue
    5994](https://github.com/scrapy/scrapy/issues/5994){.reference
    .external}, [issue
    5998](https://github.com/scrapy/scrapy/issues/5998){.reference
    .external})
:::

::: {#id3 .section}
##### Deprecations[¶](#id3 "Permalink to this heading"){.headerlink}

-   [`scrapy.utils.datatypes.CaselessDict`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre} is deprecated, use
    [`scrapy.utils.datatypes.CaseInsensitiveDict`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} instead. ([issue
    5146](https://github.com/scrapy/scrapy/issues/5146){.reference
    .external})

-   Passing the [`custom`{.docutils .literal .notranslate}]{.pre}
    argument to [`scrapy.utils.conf.build_component_list()`{.xref .py
    .py-func .docutils .literal .notranslate}]{.pre} is deprecated, it
    was used in the past to merge [`FOO`{.docutils .literal
    .notranslate}]{.pre} and [`FOO_BASE`{.docutils .literal
    .notranslate}]{.pre} setting values but now Scrapy uses
    [[`scrapy.settings.BaseSettings.getwithbase()`{.xref .py .py-func
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.settings.BaseSettings.getwithbase "scrapy.settings.BaseSettings.getwithbase"){.reference
    .internal} to do the same. Code that uses this argument and cannot
    be switched to [`getwithbase()`{.docutils .literal
    .notranslate}]{.pre} can be switched to merging the values
    explicitly. ([issue
    5726](https://github.com/scrapy/scrapy/issues/5726){.reference
    .external}, [issue
    5923](https://github.com/scrapy/scrapy/issues/5923){.reference
    .external})
:::

::: {#id4 .section}
##### New features[¶](#id4 "Permalink to this heading"){.headerlink}

-   Added support for [[Scrapy add-ons]{.std
    .std-ref}](index.html#topics-addons){.hoverxref .tooltip .reference
    .internal}. ([issue
    5950](https://github.com/scrapy/scrapy/issues/5950){.reference
    .external})

-   Added the [[`RETRY_EXCEPTIONS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-RETRY_EXCEPTIONS){.hoverxref
    .tooltip .reference .internal} setting that configures which
    exceptions will be retried by [[`RetryMiddleware`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.RetryMiddleware "scrapy.downloadermiddlewares.retry.RetryMiddleware"){.reference
    .internal}. ([issue
    2701](https://github.com/scrapy/scrapy/issues/2701){.reference
    .external}, [issue
    5929](https://github.com/scrapy/scrapy/issues/5929){.reference
    .external})

-   Added the possiiblity to close the spider if no items were produced
    in the specified time, configured by
    [[`CLOSESPIDER_TIMEOUT_NO_ITEM`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-CLOSESPIDER_TIMEOUT_NO_ITEM){.hoverxref
    .tooltip .reference .internal}. ([issue
    5979](https://github.com/scrapy/scrapy/issues/5979){.reference
    .external})

-   Added support for the [[`AWS_REGION_NAME`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-AWS_REGION_NAME){.hoverxref
    .tooltip .reference .internal} setting to feed exports. ([issue
    5980](https://github.com/scrapy/scrapy/issues/5980){.reference
    .external})

-   Added support for using [[`pathlib.Path`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.12)"){.reference
    .external} objects that refer to absolute Windows paths in the
    [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEEDS){.hoverxref
    .tooltip .reference .internal} setting. ([issue
    5939](https://github.com/scrapy/scrapy/issues/5939){.reference
    .external})
:::

::: {#id5 .section}
##### Bug fixes[¶](#id5 "Permalink to this heading"){.headerlink}

-   Fixed creating empty feeds even with
    [`FEED_STORE_EMPTY=False`{.docutils .literal .notranslate}]{.pre}.
    ([issue 872](https://github.com/scrapy/scrapy/issues/872){.reference
    .external}, [issue
    5847](https://github.com/scrapy/scrapy/issues/5847){.reference
    .external})

-   Fixed using absolute Windows paths when specifying output files.
    ([issue
    5969](https://github.com/scrapy/scrapy/issues/5969){.reference
    .external}, [issue
    5971](https://github.com/scrapy/scrapy/issues/5971){.reference
    .external})

-   Fixed problems with uploading large files to S3 by switching to
    multipart uploads (requires
    [boto3](https://github.com/boto/boto3){.reference .external}).
    ([issue 960](https://github.com/scrapy/scrapy/issues/960){.reference
    .external}, [issue
    5735](https://github.com/scrapy/scrapy/issues/5735){.reference
    .external}, [issue
    5833](https://github.com/scrapy/scrapy/issues/5833){.reference
    .external})

-   Fixed the JSON exporter writing extra commas when some exceptions
    occur. ([issue
    3090](https://github.com/scrapy/scrapy/issues/3090){.reference
    .external}, [issue
    5952](https://github.com/scrapy/scrapy/issues/5952){.reference
    .external})

-   Fixed the "read of closed file" error in the CSV exporter. ([issue
    5043](https://github.com/scrapy/scrapy/issues/5043){.reference
    .external}, [issue
    5705](https://github.com/scrapy/scrapy/issues/5705){.reference
    .external})

-   Fixed an error when a component added by the class object throws
    [[`NotConfigured`{.xref .py .py-exc .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.exceptions.NotConfigured "scrapy.exceptions.NotConfigured"){.reference
    .internal} with a message. ([issue
    5950](https://github.com/scrapy/scrapy/issues/5950){.reference
    .external}, [issue
    5992](https://github.com/scrapy/scrapy/issues/5992){.reference
    .external})

-   Added the missing [[`scrapy.settings.BaseSettings.pop()`{.xref .py
    .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.settings.BaseSettings.pop "scrapy.settings.BaseSettings.pop"){.reference
    .internal} method. ([issue
    5959](https://github.com/scrapy/scrapy/issues/5959){.reference
    .external}, [issue
    5960](https://github.com/scrapy/scrapy/issues/5960){.reference
    .external}, [issue
    5963](https://github.com/scrapy/scrapy/issues/5963){.reference
    .external})

-   Added [`CaseInsensitiveDict`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} as a replacement for [`CaselessDict`{.xref .py
    .py-class .docutils .literal .notranslate}]{.pre} that fixes some
    API inconsistencies. ([issue
    5146](https://github.com/scrapy/scrapy/issues/5146){.reference
    .external})
:::

::: {#id6 .section}
##### Documentation[¶](#id6 "Permalink to this heading"){.headerlink}

-   Documented [[`scrapy.Spider.update_settings()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.update_settings "scrapy.Spider.update_settings"){.reference
    .internal}. ([issue
    5745](https://github.com/scrapy/scrapy/issues/5745){.reference
    .external}, [issue
    5846](https://github.com/scrapy/scrapy/issues/5846){.reference
    .external})

-   Documented possible problems with early Twisted reactor installation
    and their solutions. ([issue
    5981](https://github.com/scrapy/scrapy/issues/5981){.reference
    .external}, [issue
    6000](https://github.com/scrapy/scrapy/issues/6000){.reference
    .external})

-   Added examples of making additional requests in callbacks. ([issue
    5927](https://github.com/scrapy/scrapy/issues/5927){.reference
    .external})

-   Improved the feed export docs. ([issue
    5579](https://github.com/scrapy/scrapy/issues/5579){.reference
    .external}, [issue
    5931](https://github.com/scrapy/scrapy/issues/5931){.reference
    .external})

-   Clarified the docs about request objects on redirection. ([issue
    5707](https://github.com/scrapy/scrapy/issues/5707){.reference
    .external}, [issue
    5937](https://github.com/scrapy/scrapy/issues/5937){.reference
    .external})
:::

::: {#id7 .section}
##### Quality assurance[¶](#id7 "Permalink to this heading"){.headerlink}

-   Added support for running tests against the installed Scrapy
    version. ([issue
    4914](https://github.com/scrapy/scrapy/issues/4914){.reference
    .external}, [issue
    5949](https://github.com/scrapy/scrapy/issues/5949){.reference
    .external})

-   Extended typing hints. ([issue
    5925](https://github.com/scrapy/scrapy/issues/5925){.reference
    .external}, [issue
    5977](https://github.com/scrapy/scrapy/issues/5977){.reference
    .external})

-   Fixed the
    [`test_utils_asyncio.AsyncioTest.test_set_asyncio_event_loop`{.docutils
    .literal .notranslate}]{.pre} test. ([issue
    5951](https://github.com/scrapy/scrapy/issues/5951){.reference
    .external})

-   Fixed the
    [`test_feedexport.BatchDeliveriesTest.test_batch_path_differ`{.docutils
    .literal .notranslate}]{.pre} test on Windows. ([issue
    5847](https://github.com/scrapy/scrapy/issues/5847){.reference
    .external})

-   Enabled CI runs for Python 3.11 on Windows. ([issue
    5999](https://github.com/scrapy/scrapy/issues/5999){.reference
    .external})

-   Simplified skipping tests that depend on [`uvloop`{.docutils
    .literal .notranslate}]{.pre}. ([issue
    5984](https://github.com/scrapy/scrapy/issues/5984){.reference
    .external})

-   Fixed the [`extra-deps-pinned`{.docutils .literal
    .notranslate}]{.pre} tox env. ([issue
    5948](https://github.com/scrapy/scrapy/issues/5948){.reference
    .external})

-   Implemented cleanups. ([issue
    5965](https://github.com/scrapy/scrapy/issues/5965){.reference
    .external}, [issue
    5986](https://github.com/scrapy/scrapy/issues/5986){.reference
    .external})
:::
:::

::: {#scrapy-2-9-0-2023-05-08 .section}
[]{#release-2-9-0}

#### Scrapy 2.9.0 (2023-05-08)[¶](#scrapy-2-9-0-2023-05-08 "Permalink to this heading"){.headerlink}

Highlights:

-   Per-domain download settings.

-   Compatibility with new
    [cryptography](https://cryptography.io/en/latest/){.reference
    .external} and new
    [parsel](https://github.com/scrapy/parsel){.reference .external}.

-   JMESPath selectors from the new
    [parsel](https://github.com/scrapy/parsel){.reference .external}.

-   Bug fixes.

::: {#id8 .section}
##### Deprecations[¶](#id8 "Permalink to this heading"){.headerlink}

-   [`scrapy.extensions.feedexport._FeedSlot`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} is renamed to
    [`scrapy.extensions.feedexport.FeedSlot`{.xref .py .py-class
    .docutils .literal .notranslate}]{.pre} and the old name is
    deprecated. ([issue
    5876](https://github.com/scrapy/scrapy/issues/5876){.reference
    .external})
:::

::: {#id9 .section}
##### New features[¶](#id9 "Permalink to this heading"){.headerlink}

-   Settings corresponding to [[`DOWNLOAD_DELAY`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal},
    [[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
    .tooltip .reference .internal} and
    [[`RANDOMIZE_DOWNLOAD_DELAY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-RANDOMIZE_DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal} can now be set on a per-domain basis
    via the new [[`DOWNLOAD_SLOTS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_SLOTS){.hoverxref
    .tooltip .reference .internal} setting. ([issue
    5328](https://github.com/scrapy/scrapy/issues/5328){.reference
    .external})

-   Added [`TextResponse.jmespath()`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre}, a shortcut for JMESPath selectors
    available since
    [parsel](https://github.com/scrapy/parsel){.reference .external}
    1.8.1. ([issue
    5894](https://github.com/scrapy/scrapy/issues/5894){.reference
    .external}, [issue
    5915](https://github.com/scrapy/scrapy/issues/5915){.reference
    .external})

-   Added [[`feed_slot_closed`{.xref .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-feed_slot_closed){.hoverxref
    .tooltip .reference .internal} and [[`feed_exporter_closed`{.xref
    .std .std-signal .docutils .literal
    .notranslate}]{.pre}](index.html#std-signal-feed_exporter_closed){.hoverxref
    .tooltip .reference .internal} signals. ([issue
    5876](https://github.com/scrapy/scrapy/issues/5876){.reference
    .external})

-   Added [`scrapy.utils.request.request_to_curl()`{.xref .py .py-func
    .docutils .literal .notranslate}]{.pre}, a function to produce a
    curl command from a [`Request`{.xref .py .py-class .docutils
    .literal .notranslate}]{.pre} object. ([issue
    5892](https://github.com/scrapy/scrapy/issues/5892){.reference
    .external})

-   Values of [[`FILES_STORE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FILES_STORE){.hoverxref
    .tooltip .reference .internal} and [[`IMAGES_STORE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-IMAGES_STORE){.hoverxref
    .tooltip .reference .internal} can now be [[`pathlib.Path`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.12)"){.reference
    .external} instances. ([issue
    5801](https://github.com/scrapy/scrapy/issues/5801){.reference
    .external})
:::

::: {#id10 .section}
##### Bug fixes[¶](#id10 "Permalink to this heading"){.headerlink}

-   Fixed a warning with Parsel 1.8.1+. ([issue
    5903](https://github.com/scrapy/scrapy/issues/5903){.reference
    .external}, [issue
    5918](https://github.com/scrapy/scrapy/issues/5918){.reference
    .external})

-   Fixed an error when using feed postprocessing with S3 storage.
    ([issue
    5500](https://github.com/scrapy/scrapy/issues/5500){.reference
    .external}, [issue
    5581](https://github.com/scrapy/scrapy/issues/5581){.reference
    .external})

-   Added the missing
    [[`scrapy.settings.BaseSettings.setdefault()`{.xref .py .py-meth
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.settings.BaseSettings.setdefault "scrapy.settings.BaseSettings.setdefault"){.reference
    .internal} method. ([issue
    5811](https://github.com/scrapy/scrapy/issues/5811){.reference
    .external}, [issue
    5821](https://github.com/scrapy/scrapy/issues/5821){.reference
    .external})

-   Fixed an error when using
    [cryptography](https://cryptography.io/en/latest/){.reference
    .external} 40.0.0+ and
    [[`DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING){.hoverxref
    .tooltip .reference .internal} is enabled. ([issue
    5857](https://github.com/scrapy/scrapy/issues/5857){.reference
    .external}, [issue
    5858](https://github.com/scrapy/scrapy/issues/5858){.reference
    .external})

-   The checksums returned by [[`FilesPipeline`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.files.FilesPipeline "scrapy.pipelines.files.FilesPipeline"){.reference
    .internal} for files on Google Cloud Storage are no longer
    Base64-encoded. ([issue
    5874](https://github.com/scrapy/scrapy/issues/5874){.reference
    .external}, [issue
    5891](https://github.com/scrapy/scrapy/issues/5891){.reference
    .external})

-   [`scrapy.utils.request.request_from_curl()`{.xref .py .py-func
    .docutils .literal .notranslate}]{.pre} now supports \$-prefixed
    string values for the curl [`--data-raw`{.docutils .literal
    .notranslate}]{.pre} argument, which are produced by browsers for
    data that includes certain symbols. ([issue
    5899](https://github.com/scrapy/scrapy/issues/5899){.reference
    .external}, [issue
    5901](https://github.com/scrapy/scrapy/issues/5901){.reference
    .external})

-   The [[`parse`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-parse){.hoverxref
    .tooltip .reference .internal} command now also works with async
    generator callbacks. ([issue
    5819](https://github.com/scrapy/scrapy/issues/5819){.reference
    .external}, [issue
    5824](https://github.com/scrapy/scrapy/issues/5824){.reference
    .external})

-   The [[`genspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-genspider){.hoverxref
    .tooltip .reference .internal} command now properly works with HTTPS
    URLs. ([issue
    3553](https://github.com/scrapy/scrapy/issues/3553){.reference
    .external}, [issue
    5808](https://github.com/scrapy/scrapy/issues/5808){.reference
    .external})

-   Improved handling of asyncio loops. ([issue
    5831](https://github.com/scrapy/scrapy/issues/5831){.reference
    .external}, [issue
    5832](https://github.com/scrapy/scrapy/issues/5832){.reference
    .external})

-   [[`LinkExtractor`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} now skips certain malformed URLs instead of raising an
    exception. ([issue
    5881](https://github.com/scrapy/scrapy/issues/5881){.reference
    .external})

-   [`scrapy.utils.python.get_func_args()`{.xref .py .py-func .docutils
    .literal .notranslate}]{.pre} now supports more types of callables.
    ([issue
    5872](https://github.com/scrapy/scrapy/issues/5872){.reference
    .external}, [issue
    5885](https://github.com/scrapy/scrapy/issues/5885){.reference
    .external})

-   Fixed an error when processing non-UTF8 values of
    [`Content-Type`{.docutils .literal .notranslate}]{.pre} headers.
    ([issue
    5914](https://github.com/scrapy/scrapy/issues/5914){.reference
    .external}, [issue
    5917](https://github.com/scrapy/scrapy/issues/5917){.reference
    .external})

-   Fixed an error breaking user handling of send failures in
    [[`scrapy.mail.MailSender.send()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.mail.MailSender.send "scrapy.mail.MailSender.send"){.reference
    .internal}. ([issue
    1611](https://github.com/scrapy/scrapy/issues/1611){.reference
    .external}, [issue
    5880](https://github.com/scrapy/scrapy/issues/5880){.reference
    .external})
:::

::: {#id11 .section}
##### Documentation[¶](#id11 "Permalink to this heading"){.headerlink}

-   Expanded contributing docs. ([issue
    5109](https://github.com/scrapy/scrapy/issues/5109){.reference
    .external}, [issue
    5851](https://github.com/scrapy/scrapy/issues/5851){.reference
    .external})

-   Added
    [blacken-docs](https://github.com/adamchainz/blacken-docs){.reference
    .external} to pre-commit and reformatted the docs with it. ([issue
    5813](https://github.com/scrapy/scrapy/issues/5813){.reference
    .external}, [issue
    5816](https://github.com/scrapy/scrapy/issues/5816){.reference
    .external})

-   Fixed a JS issue. ([issue
    5875](https://github.com/scrapy/scrapy/issues/5875){.reference
    .external}, [issue
    5877](https://github.com/scrapy/scrapy/issues/5877){.reference
    .external})

-   Fixed [`make`{.docutils .literal .notranslate}]{.pre}` `{.docutils
    .literal .notranslate}[`htmlview`{.docutils .literal
    .notranslate}]{.pre}. ([issue
    5878](https://github.com/scrapy/scrapy/issues/5878){.reference
    .external}, [issue
    5879](https://github.com/scrapy/scrapy/issues/5879){.reference
    .external})

-   Fixed typos and other small errors. ([issue
    5827](https://github.com/scrapy/scrapy/issues/5827){.reference
    .external}, [issue
    5839](https://github.com/scrapy/scrapy/issues/5839){.reference
    .external}, [issue
    5883](https://github.com/scrapy/scrapy/issues/5883){.reference
    .external}, [issue
    5890](https://github.com/scrapy/scrapy/issues/5890){.reference
    .external}, [issue
    5895](https://github.com/scrapy/scrapy/issues/5895){.reference
    .external}, [issue
    5904](https://github.com/scrapy/scrapy/issues/5904){.reference
    .external})
:::

::: {#id12 .section}
##### Quality assurance[¶](#id12 "Permalink to this heading"){.headerlink}

-   Extended typing hints. ([issue
    5805](https://github.com/scrapy/scrapy/issues/5805){.reference
    .external}, [issue
    5889](https://github.com/scrapy/scrapy/issues/5889){.reference
    .external}, [issue
    5896](https://github.com/scrapy/scrapy/issues/5896){.reference
    .external})

-   Tests for most of the examples in the docs are now run as a part of
    CI, found problems were fixed. ([issue
    5816](https://github.com/scrapy/scrapy/issues/5816){.reference
    .external}, [issue
    5826](https://github.com/scrapy/scrapy/issues/5826){.reference
    .external}, [issue
    5919](https://github.com/scrapy/scrapy/issues/5919){.reference
    .external})

-   Removed usage of deprecated Python classes. ([issue
    5849](https://github.com/scrapy/scrapy/issues/5849){.reference
    .external})

-   Silenced [`include-ignored`{.docutils .literal .notranslate}]{.pre}
    warnings from coverage. ([issue
    5820](https://github.com/scrapy/scrapy/issues/5820){.reference
    .external})

-   Fixed a random failure of the
    [`test_feedexport.test_batch_path_differ`{.docutils .literal
    .notranslate}]{.pre} test. ([issue
    5855](https://github.com/scrapy/scrapy/issues/5855){.reference
    .external}, [issue
    5898](https://github.com/scrapy/scrapy/issues/5898){.reference
    .external})

-   Updated docstrings to match output produced by
    [parsel](https://github.com/scrapy/parsel){.reference .external}
    1.8.1 so that they don't cause test failures. ([issue
    5902](https://github.com/scrapy/scrapy/issues/5902){.reference
    .external}, [issue
    5919](https://github.com/scrapy/scrapy/issues/5919){.reference
    .external})

-   Other CI and pre-commit improvements. ([issue
    5802](https://github.com/scrapy/scrapy/issues/5802){.reference
    .external}, [issue
    5823](https://github.com/scrapy/scrapy/issues/5823){.reference
    .external}, [issue
    5908](https://github.com/scrapy/scrapy/issues/5908){.reference
    .external})
:::
:::

::: {#scrapy-2-8-0-2023-02-02 .section}
[]{#release-2-8-0}

#### Scrapy 2.8.0 (2023-02-02)[¶](#scrapy-2-8-0-2023-02-02 "Permalink to this heading"){.headerlink}

This is a maintenance release, with minor features, bug fixes, and
cleanups.

::: {#id13 .section}
##### Deprecation removals[¶](#id13 "Permalink to this heading"){.headerlink}

-   The [`scrapy.utils.gz.read1`{.docutils .literal .notranslate}]{.pre}
    function, deprecated in Scrapy 2.0, has now been removed. Use the
    [[`read1()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/io.html#io.BufferedIOBase.read1 "(in Python v3.12)"){.reference
    .external} method of [[`GzipFile`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/gzip.html#gzip.GzipFile "(in Python v3.12)"){.reference
    .external} instead. ([issue
    5719](https://github.com/scrapy/scrapy/issues/5719){.reference
    .external})

-   The [`scrapy.utils.python.to_native_str`{.docutils .literal
    .notranslate}]{.pre} function, deprecated in Scrapy 2.0, has now
    been removed. Use [`scrapy.utils.python.to_unicode()`{.xref .py
    .py-func .docutils .literal .notranslate}]{.pre} instead. ([issue
    5719](https://github.com/scrapy/scrapy/issues/5719){.reference
    .external})

-   The [`scrapy.utils.python.MutableChain.next`{.docutils .literal
    .notranslate}]{.pre} method, deprecated in Scrapy 2.0, has now been
    removed. Use [`__next__()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre} instead. ([issue
    5719](https://github.com/scrapy/scrapy/issues/5719){.reference
    .external})

-   The [`scrapy.linkextractors.FilteringLinkExtractor`{.docutils
    .literal .notranslate}]{.pre} class, deprecated in Scrapy 2.0, has
    now been removed. Use [[`LinkExtractor`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} instead. ([issue
    5720](https://github.com/scrapy/scrapy/issues/5720){.reference
    .external})

-   Support for using environment variables prefixed with
    [`SCRAPY_`{.docutils .literal .notranslate}]{.pre} to override
    settings, deprecated in Scrapy 2.0, has now been removed. ([issue
    5724](https://github.com/scrapy/scrapy/issues/5724){.reference
    .external})

-   Support for the [`noconnect`{.docutils .literal .notranslate}]{.pre}
    query string argument in proxy URLs, deprecated in Scrapy 2.0, has
    now been removed. We expect proxies that used to need it to work
    fine without it. ([issue
    5731](https://github.com/scrapy/scrapy/issues/5731){.reference
    .external})

-   The [`scrapy.utils.python.retry_on_eintr`{.docutils .literal
    .notranslate}]{.pre} function, deprecated in Scrapy 2.3, has now
    been removed. ([issue
    5719](https://github.com/scrapy/scrapy/issues/5719){.reference
    .external})

-   The [`scrapy.utils.python.WeakKeyCache`{.docutils .literal
    .notranslate}]{.pre} class, deprecated in Scrapy 2.4, has now been
    removed. ([issue
    5719](https://github.com/scrapy/scrapy/issues/5719){.reference
    .external})

-   The [`scrapy.utils.boto.is_botocore()`{.docutils .literal
    .notranslate}]{.pre} function, deprecated in Scrapy 2.4, has now
    been removed. ([issue
    5719](https://github.com/scrapy/scrapy/issues/5719){.reference
    .external})
:::

::: {#id14 .section}
##### Deprecations[¶](#id14 "Permalink to this heading"){.headerlink}

-   [`scrapy.pipelines.images.NoimagesDrop`{.xref .py .py-exc .docutils
    .literal .notranslate}]{.pre} is now deprecated. ([issue
    5368](https://github.com/scrapy/scrapy/issues/5368){.reference
    .external}, [issue
    5489](https://github.com/scrapy/scrapy/issues/5489){.reference
    .external})

-   [`ImagesPipeline.convert_image`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre} must now accept a
    [`response_body`{.docutils .literal .notranslate}]{.pre} parameter.
    ([issue
    3055](https://github.com/scrapy/scrapy/issues/3055){.reference
    .external}, [issue
    3689](https://github.com/scrapy/scrapy/issues/3689){.reference
    .external}, [issue
    4753](https://github.com/scrapy/scrapy/issues/4753){.reference
    .external})
:::

::: {#id15 .section}
##### New features[¶](#id15 "Permalink to this heading"){.headerlink}

-   Applied [black](https://black.readthedocs.io/en/stable/){.reference
    .external} coding style to files generated with the
    [[`genspider`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-genspider){.hoverxref
    .tooltip .reference .internal} and [[`startproject`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} commands. ([issue
    5809](https://github.com/scrapy/scrapy/issues/5809){.reference
    .external}, [issue
    5814](https://github.com/scrapy/scrapy/issues/5814){.reference
    .external})

-   [[`FEED_EXPORT_ENCODING`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_ENCODING){.hoverxref
    .tooltip .reference .internal} is now set to [`"utf-8"`{.docutils
    .literal .notranslate}]{.pre} in the [`settings.py`{.docutils
    .literal .notranslate}]{.pre} file that the [[`startproject`{.xref
    .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} command generates. With this value,
    JSON exports won't force the use of escape sequences for non-ASCII
    characters. ([issue
    5797](https://github.com/scrapy/scrapy/issues/5797){.reference
    .external}, [issue
    5800](https://github.com/scrapy/scrapy/issues/5800){.reference
    .external})

-   The [[`MemoryUsage`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.extensions.memusage.MemoryUsage "scrapy.extensions.memusage.MemoryUsage"){.reference
    .internal} extension now logs the peak memory usage during checks,
    and the binary unit MiB is now used to avoid confusion. ([issue
    5717](https://github.com/scrapy/scrapy/issues/5717){.reference
    .external}, [issue
    5722](https://github.com/scrapy/scrapy/issues/5722){.reference
    .external}, [issue
    5727](https://github.com/scrapy/scrapy/issues/5727){.reference
    .external})

-   The [`callback`{.docutils .literal .notranslate}]{.pre} parameter of
    [[`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} can now be set to
    [[`scrapy.http.request.NO_CALLBACK()`{.xref .py .py-func .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.http.request.NO_CALLBACK "scrapy.http.request.NO_CALLBACK"){.reference
    .internal}, to distinguish it from [`None`{.docutils .literal
    .notranslate}]{.pre}, as the latter indicates that the default
    spider callback ([[`parse()`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
    .internal}) is to be used. ([issue
    5798](https://github.com/scrapy/scrapy/issues/5798){.reference
    .external})
:::

::: {#id16 .section}
##### Bug fixes[¶](#id16 "Permalink to this heading"){.headerlink}

-   Enabled unsafe legacy SSL renegotiation to fix access to some
    outdated websites. ([issue
    5491](https://github.com/scrapy/scrapy/issues/5491){.reference
    .external}, [issue
    5790](https://github.com/scrapy/scrapy/issues/5790){.reference
    .external})

-   Fixed STARTTLS-based email delivery not working with Twisted 21.2.0
    and better. ([issue
    5386](https://github.com/scrapy/scrapy/issues/5386){.reference
    .external}, [issue
    5406](https://github.com/scrapy/scrapy/issues/5406){.reference
    .external})

-   Fixed the [`finish_exporting()`{.xref .py .py-meth .docutils
    .literal .notranslate}]{.pre} method of [[item exporters]{.std
    .std-ref}](index.html#topics-exporters){.hoverxref .tooltip
    .reference .internal} not being called for empty files. ([issue
    5537](https://github.com/scrapy/scrapy/issues/5537){.reference
    .external}, [issue
    5758](https://github.com/scrapy/scrapy/issues/5758){.reference
    .external})

-   Fixed HTTP/2 responses getting only the last value for a header when
    multiple headers with the same name are received. ([issue
    5777](https://github.com/scrapy/scrapy/issues/5777){.reference
    .external})

-   Fixed an exception raised by the [[`shell`{.xref .std .std-command
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-shell){.hoverxref
    .tooltip .reference .internal} command on some cases when [[using
    asyncio]{.std .std-ref}](index.html#using-asyncio){.hoverxref
    .tooltip .reference .internal}. ([issue
    5740](https://github.com/scrapy/scrapy/issues/5740){.reference
    .external}, [issue
    5742](https://github.com/scrapy/scrapy/issues/5742){.reference
    .external}, [issue
    5748](https://github.com/scrapy/scrapy/issues/5748){.reference
    .external}, [issue
    5759](https://github.com/scrapy/scrapy/issues/5759){.reference
    .external}, [issue
    5760](https://github.com/scrapy/scrapy/issues/5760){.reference
    .external}, [issue
    5771](https://github.com/scrapy/scrapy/issues/5771){.reference
    .external})

-   When using [[`CrawlSpider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.CrawlSpider "scrapy.spiders.CrawlSpider"){.reference
    .internal}, callback keyword arguments ([`cb_kwargs`{.docutils
    .literal .notranslate}]{.pre}) added to a request in the
    [`process_request`{.docutils .literal .notranslate}]{.pre} callback
    of a [[`Rule`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
    .internal} will no longer be ignored. ([issue
    5699](https://github.com/scrapy/scrapy/issues/5699){.reference
    .external})

-   The [[images pipeline]{.std
    .std-ref}](index.html#images-pipeline){.hoverxref .tooltip
    .reference .internal} no longer re-encodes JPEG files. ([issue
    3055](https://github.com/scrapy/scrapy/issues/3055){.reference
    .external}, [issue
    3689](https://github.com/scrapy/scrapy/issues/3689){.reference
    .external}, [issue
    4753](https://github.com/scrapy/scrapy/issues/4753){.reference
    .external})

-   Fixed the handling of transparent WebP images by the [[images
    pipeline]{.std .std-ref}](index.html#images-pipeline){.hoverxref
    .tooltip .reference .internal}. ([issue
    3072](https://github.com/scrapy/scrapy/issues/3072){.reference
    .external}, [issue
    5766](https://github.com/scrapy/scrapy/issues/5766){.reference
    .external}, [issue
    5767](https://github.com/scrapy/scrapy/issues/5767){.reference
    .external})

-   [`scrapy.shell.inspect_response()`{.xref .py .py-func .docutils
    .literal .notranslate}]{.pre} no longer inhibits [`SIGINT`{.docutils
    .literal .notranslate}]{.pre} (Ctrl+C). ([issue
    2918](https://github.com/scrapy/scrapy/issues/2918){.reference
    .external})

-   [[`LinkExtractor`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
    .internal} with [`unique=False`{.docutils .literal
    .notranslate}]{.pre} no longer filters out links that have identical
    URL *and* text. ([issue
    3798](https://github.com/scrapy/scrapy/issues/3798){.reference
    .external}, [issue
    3799](https://github.com/scrapy/scrapy/issues/3799){.reference
    .external}, [issue
    4695](https://github.com/scrapy/scrapy/issues/4695){.reference
    .external}, [issue
    5458](https://github.com/scrapy/scrapy/issues/5458){.reference
    .external})

-   [[`RobotsTxtMiddleware`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware "scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware"){.reference
    .internal} now ignores URL protocols that do not support
    [`robots.txt`{.docutils .literal .notranslate}]{.pre}
    ([`data://`{.docutils .literal .notranslate}]{.pre},
    [`file://`{.docutils .literal .notranslate}]{.pre}). ([issue
    5807](https://github.com/scrapy/scrapy/issues/5807){.reference
    .external})

-   Silenced the [`filelock`{.docutils .literal .notranslate}]{.pre}
    debug log messages introduced in Scrapy 2.6. ([issue
    5753](https://github.com/scrapy/scrapy/issues/5753){.reference
    .external}, [issue
    5754](https://github.com/scrapy/scrapy/issues/5754){.reference
    .external})

-   Fixed the output of [`scrapy`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`-h`{.docutils .literal .notranslate}]{.pre} showing
    an unintended [`**commands**`{.docutils .literal
    .notranslate}]{.pre} line. ([issue
    5709](https://github.com/scrapy/scrapy/issues/5709){.reference
    .external}, [issue
    5711](https://github.com/scrapy/scrapy/issues/5711){.reference
    .external}, [issue
    5712](https://github.com/scrapy/scrapy/issues/5712){.reference
    .external})

-   Made the active project indication in the output of [[commands]{.std
    .std-ref}](index.html#topics-commands){.hoverxref .tooltip
    .reference .internal} more clear. ([issue
    5715](https://github.com/scrapy/scrapy/issues/5715){.reference
    .external})
:::

::: {#id17 .section}
##### Documentation[¶](#id17 "Permalink to this heading"){.headerlink}

-   Documented how to [[debug spiders from Visual Studio Code]{.std
    .std-ref}](index.html#debug-vscode){.hoverxref .tooltip .reference
    .internal}. ([issue
    5721](https://github.com/scrapy/scrapy/issues/5721){.reference
    .external})

-   Documented how [[`DOWNLOAD_DELAY`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_DELAY){.hoverxref
    .tooltip .reference .internal} affects per-domain concurrency.
    ([issue
    5083](https://github.com/scrapy/scrapy/issues/5083){.reference
    .external}, [issue
    5540](https://github.com/scrapy/scrapy/issues/5540){.reference
    .external})

-   Improved consistency. ([issue
    5761](https://github.com/scrapy/scrapy/issues/5761){.reference
    .external})

-   Fixed typos. ([issue
    5714](https://github.com/scrapy/scrapy/issues/5714){.reference
    .external}, [issue
    5744](https://github.com/scrapy/scrapy/issues/5744){.reference
    .external}, [issue
    5764](https://github.com/scrapy/scrapy/issues/5764){.reference
    .external})
:::

::: {#id18 .section}
##### Quality assurance[¶](#id18 "Permalink to this heading"){.headerlink}

-   Applied [[black coding style]{.std
    .std-ref}](index.html#coding-style){.hoverxref .tooltip .reference
    .internal}, sorted import statements, and introduced
    [[pre-commit]{.std
    .std-ref}](index.html#scrapy-pre-commit){.hoverxref .tooltip
    .reference .internal}. ([issue
    4654](https://github.com/scrapy/scrapy/issues/4654){.reference
    .external}, [issue
    4658](https://github.com/scrapy/scrapy/issues/4658){.reference
    .external}, [issue
    5734](https://github.com/scrapy/scrapy/issues/5734){.reference
    .external}, [issue
    5737](https://github.com/scrapy/scrapy/issues/5737){.reference
    .external}, [issue
    5806](https://github.com/scrapy/scrapy/issues/5806){.reference
    .external}, [issue
    5810](https://github.com/scrapy/scrapy/issues/5810){.reference
    .external})

-   Switched from [[`os.path`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/os.path.html#module-os.path "(in Python v3.12)"){.reference
    .external} to [[`pathlib`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#module-pathlib "(in Python v3.12)"){.reference
    .external}. ([issue
    4916](https://github.com/scrapy/scrapy/issues/4916){.reference
    .external}, [issue
    4497](https://github.com/scrapy/scrapy/issues/4497){.reference
    .external}, [issue
    5682](https://github.com/scrapy/scrapy/issues/5682){.reference
    .external})

-   Addressed many issues reported by Pylint. ([issue
    5677](https://github.com/scrapy/scrapy/issues/5677){.reference
    .external})

-   Improved code readability. ([issue
    5736](https://github.com/scrapy/scrapy/issues/5736){.reference
    .external})

-   Improved package metadata. ([issue
    5768](https://github.com/scrapy/scrapy/issues/5768){.reference
    .external})

-   Removed direct invocations of [`setup.py`{.docutils .literal
    .notranslate}]{.pre}. ([issue
    5774](https://github.com/scrapy/scrapy/issues/5774){.reference
    .external}, [issue
    5776](https://github.com/scrapy/scrapy/issues/5776){.reference
    .external})

-   Removed unnecessary [[`OrderedDict`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/collections.html#collections.OrderedDict "(in Python v3.12)"){.reference
    .external} usages. ([issue
    5795](https://github.com/scrapy/scrapy/issues/5795){.reference
    .external})

-   Removed unnecessary [`__str__`{.docutils .literal
    .notranslate}]{.pre} definitions. ([issue
    5150](https://github.com/scrapy/scrapy/issues/5150){.reference
    .external})

-   Removed obsolete code and comments. ([issue
    5725](https://github.com/scrapy/scrapy/issues/5725){.reference
    .external}, [issue
    5729](https://github.com/scrapy/scrapy/issues/5729){.reference
    .external}, [issue
    5730](https://github.com/scrapy/scrapy/issues/5730){.reference
    .external}, [issue
    5732](https://github.com/scrapy/scrapy/issues/5732){.reference
    .external})

-   Fixed test and CI issues. ([issue
    5749](https://github.com/scrapy/scrapy/issues/5749){.reference
    .external}, [issue
    5750](https://github.com/scrapy/scrapy/issues/5750){.reference
    .external}, [issue
    5756](https://github.com/scrapy/scrapy/issues/5756){.reference
    .external}, [issue
    5762](https://github.com/scrapy/scrapy/issues/5762){.reference
    .external}, [issue
    5765](https://github.com/scrapy/scrapy/issues/5765){.reference
    .external}, [issue
    5780](https://github.com/scrapy/scrapy/issues/5780){.reference
    .external}, [issue
    5781](https://github.com/scrapy/scrapy/issues/5781){.reference
    .external}, [issue
    5782](https://github.com/scrapy/scrapy/issues/5782){.reference
    .external}, [issue
    5783](https://github.com/scrapy/scrapy/issues/5783){.reference
    .external}, [issue
    5785](https://github.com/scrapy/scrapy/issues/5785){.reference
    .external}, [issue
    5786](https://github.com/scrapy/scrapy/issues/5786){.reference
    .external})
:::
:::

::: {#scrapy-2-7-1-2022-11-02 .section}
[]{#release-2-7-1}

#### Scrapy 2.7.1 (2022-11-02)[¶](#scrapy-2-7-1-2022-11-02 "Permalink to this heading"){.headerlink}

::: {#id19 .section}
##### New features[¶](#id19 "Permalink to this heading"){.headerlink}

-   Relaxed the restriction introduced in 2.6.2 so that the
    [`Proxy-Authorization`{.docutils .literal .notranslate}]{.pre}
    header can again be set explicitly, as long as the proxy URL in the
    [[`proxy`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal} metadata has no other credentials,
    and for as long as that proxy URL remains the same; this restores
    compatibility with scrapy-zyte-smartproxy 2.1.0 and older ([issue
    5626](https://github.com/scrapy/scrapy/issues/5626){.reference
    .external}).
:::

::: {#id20 .section}
##### Bug fixes[¶](#id20 "Permalink to this heading"){.headerlink}

-   Using [`-O`{.docutils .literal
    .notranslate}]{.pre}/[`--overwrite-output`{.docutils .literal
    .notranslate}]{.pre} and [`-t`{.docutils .literal
    .notranslate}]{.pre}/[`--output-format`{.docutils .literal
    .notranslate}]{.pre} options together now produces an error instead
    of ignoring the former option ([issue
    5516](https://github.com/scrapy/scrapy/issues/5516){.reference
    .external}, [issue
    5605](https://github.com/scrapy/scrapy/issues/5605){.reference
    .external}).

-   Replaced deprecated [[`asyncio`{.xref .py .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/asyncio.html#module-asyncio "(in Python v3.12)"){.reference
    .external} APIs that implicitly use the current event loop with code
    that explicitly requests a loop from the event loop policy ([issue
    5685](https://github.com/scrapy/scrapy/issues/5685){.reference
    .external}, [issue
    5689](https://github.com/scrapy/scrapy/issues/5689){.reference
    .external}).

-   Fixed uses of deprecated Scrapy APIs in Scrapy itself ([issue
    5588](https://github.com/scrapy/scrapy/issues/5588){.reference
    .external}, [issue
    5589](https://github.com/scrapy/scrapy/issues/5589){.reference
    .external}).

-   Fixed uses of a deprecated Pillow API ([issue
    5684](https://github.com/scrapy/scrapy/issues/5684){.reference
    .external}, [issue
    5692](https://github.com/scrapy/scrapy/issues/5692){.reference
    .external}).

-   Improved code that checks if generators return values, so that it no
    longer fails on decorated methods and partial methods ([issue
    5323](https://github.com/scrapy/scrapy/issues/5323){.reference
    .external}, [issue
    5592](https://github.com/scrapy/scrapy/issues/5592){.reference
    .external}, [issue
    5599](https://github.com/scrapy/scrapy/issues/5599){.reference
    .external}, [issue
    5691](https://github.com/scrapy/scrapy/issues/5691){.reference
    .external}).
:::

::: {#id21 .section}
##### Documentation[¶](#id21 "Permalink to this heading"){.headerlink}

-   Upgraded the Code of Conduct to Contributor Covenant v2.1 ([issue
    5698](https://github.com/scrapy/scrapy/issues/5698){.reference
    .external}).

-   Fixed typos ([issue
    5681](https://github.com/scrapy/scrapy/issues/5681){.reference
    .external}, [issue
    5694](https://github.com/scrapy/scrapy/issues/5694){.reference
    .external}).
:::

::: {#id22 .section}
##### Quality assurance[¶](#id22 "Permalink to this heading"){.headerlink}

-   Re-enabled some erroneously disabled flake8 checks ([issue
    5688](https://github.com/scrapy/scrapy/issues/5688){.reference
    .external}).

-   Ignored harmless deprecation warnings from [[`typing`{.xref .py
    .py-mod .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/typing.html#module-typing "(in Python v3.12)"){.reference
    .external} in tests ([issue
    5686](https://github.com/scrapy/scrapy/issues/5686){.reference
    .external}, [issue
    5697](https://github.com/scrapy/scrapy/issues/5697){.reference
    .external}).

-   Modernized our CI configuration ([issue
    5695](https://github.com/scrapy/scrapy/issues/5695){.reference
    .external}, [issue
    5696](https://github.com/scrapy/scrapy/issues/5696){.reference
    .external}).
:::
:::

::: {#scrapy-2-7-0-2022-10-17 .section}
[]{#release-2-7-0}

#### Scrapy 2.7.0 (2022-10-17)[¶](#scrapy-2-7-0-2022-10-17 "Permalink to this heading"){.headerlink}

Highlights:

-   Added Python 3.11 support, dropped Python 3.6 support

-   Improved support for [[asynchronous callbacks]{.std
    .std-ref}](index.html#topics-coroutines){.hoverxref .tooltip
    .reference .internal}

-   [[Asyncio support]{.std
    .std-ref}](index.html#using-asyncio){.hoverxref .tooltip .reference
    .internal} is enabled by default on new projects

-   Output names of item fields can now be arbitrary strings

-   Centralized [[request fingerprinting]{.std
    .std-ref}](index.html#request-fingerprints){.hoverxref .tooltip
    .reference .internal} configuration is now possible

::: {#id23 .section}
##### Modified requirements[¶](#id23 "Permalink to this heading"){.headerlink}

Python 3.7 or greater is now required; support for Python 3.6 has been
dropped. Support for the upcoming Python 3.11 has been added.

The minimum required version of some dependencies has changed as well:

-   [lxml](https://lxml.de/){.reference .external}: 3.5.0 → 4.3.0

-   [Pillow](https://python-pillow.org/){.reference .external} ([[images
    pipeline]{.std .std-ref}](index.html#images-pipeline){.hoverxref
    .tooltip .reference .internal}): 4.0.0 → 7.1.0

-   [zope.interface](https://zopeinterface.readthedocs.io/en/latest/){.reference
    .external}: 5.0.0 → 5.1.0

([issue 5512](https://github.com/scrapy/scrapy/issues/5512){.reference
.external}, [issue
5514](https://github.com/scrapy/scrapy/issues/5514){.reference
.external}, [issue
5524](https://github.com/scrapy/scrapy/issues/5524){.reference
.external}, [issue
5563](https://github.com/scrapy/scrapy/issues/5563){.reference
.external}, [issue
5664](https://github.com/scrapy/scrapy/issues/5664){.reference
.external}, [issue
5670](https://github.com/scrapy/scrapy/issues/5670){.reference
.external}, [issue
5678](https://github.com/scrapy/scrapy/issues/5678){.reference
.external})
:::

::: {#id24 .section}
##### Deprecations[¶](#id24 "Permalink to this heading"){.headerlink}

-   [[`ImagesPipeline.thumb_path`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline.thumb_path "scrapy.pipelines.images.ImagesPipeline.thumb_path"){.reference
    .internal} must now accept an [`item`{.docutils .literal
    .notranslate}]{.pre} parameter ([issue
    5504](https://github.com/scrapy/scrapy/issues/5504){.reference
    .external}, [issue
    5508](https://github.com/scrapy/scrapy/issues/5508){.reference
    .external}).

-   The [`scrapy.downloadermiddlewares.decompression`{.docutils .literal
    .notranslate}]{.pre} module is now deprecated ([issue
    5546](https://github.com/scrapy/scrapy/issues/5546){.reference
    .external}, [issue
    5547](https://github.com/scrapy/scrapy/issues/5547){.reference
    .external}).
:::

::: {#id25 .section}
##### New features[¶](#id25 "Permalink to this heading"){.headerlink}

-   The [[`process_spider_output()`{.xref .py .py-meth .docutils
    .literal
    .notranslate}]{.pre}](index.html#scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output "scrapy.spidermiddlewares.SpiderMiddleware.process_spider_output"){.reference
    .internal} method of [[spider middlewares]{.std
    .std-ref}](index.html#topics-spider-middleware){.hoverxref .tooltip
    .reference .internal} can now be defined as an [[asynchronous
    generator]{.xref .std
    .std-term}](https://docs.python.org/3/glossary.html#term-asynchronous-generator "(in Python v3.12)"){.reference
    .external} ([issue
    4978](https://github.com/scrapy/scrapy/issues/4978){.reference
    .external}).

-   The output of [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} callbacks defined as [[coroutines]{.std
    .std-ref}](index.html#topics-coroutines){.hoverxref .tooltip
    .reference .internal} is now processed asynchronously ([issue
    4978](https://github.com/scrapy/scrapy/issues/4978){.reference
    .external}).

-   [`CrawlSpider`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} now supports [[asynchronous callbacks]{.std
    .std-ref}](index.html#topics-coroutines){.hoverxref .tooltip
    .reference .internal} ([issue
    5657](https://github.com/scrapy/scrapy/issues/5657){.reference
    .external}).

-   New projects created with the [[`startproject`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} command have [[asyncio support]{.std
    .std-ref}](index.html#using-asyncio){.hoverxref .tooltip .reference
    .internal} enabled by default ([issue
    5590](https://github.com/scrapy/scrapy/issues/5590){.reference
    .external}, [issue
    5679](https://github.com/scrapy/scrapy/issues/5679){.reference
    .external}).

-   The [[`FEED_EXPORT_FIELDS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-FEED_EXPORT_FIELDS){.hoverxref
    .tooltip .reference .internal} setting can now be defined as a
    dictionary to customize the output name of item fields, lifting the
    restriction that required output names to be valid Python
    identifiers, e.g. preventing them to have whitespace ([issue
    1008](https://github.com/scrapy/scrapy/issues/1008){.reference
    .external}, [issue
    3266](https://github.com/scrapy/scrapy/issues/3266){.reference
    .external}, [issue
    3696](https://github.com/scrapy/scrapy/issues/3696){.reference
    .external}).

-   You can now customize [[request fingerprinting]{.std
    .std-ref}](index.html#request-fingerprints){.hoverxref .tooltip
    .reference .internal} through the new
    [[`REQUEST_FINGERPRINTER_CLASS`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-setting-REQUEST_FINGERPRINTER_CLASS){.hoverxref
    .tooltip .reference .internal} setting, instead of having to change
    it on every Scrapy component that relies on request fingerprinting
    ([issue 900](https://github.com/scrapy/scrapy/issues/900){.reference
    .external}, [issue
    3420](https://github.com/scrapy/scrapy/issues/3420){.reference
    .external}, [issue
    4113](https://github.com/scrapy/scrapy/issues/4113){.reference
    .external}, [issue
    4762](https://github.com/scrapy/scrapy/issues/4762){.reference
    .external}, [issue
    4524](https://github.com/scrapy/scrapy/issues/4524){.reference
    .external}).

-   [`jsonl`{.docutils .literal .notranslate}]{.pre} is now supported
    and encouraged as a file extension for [JSON
    Lines](https://jsonlines.org/){.reference .external} files ([issue
    4848](https://github.com/scrapy/scrapy/issues/4848){.reference
    .external}).

-   [[`ImagesPipeline.thumb_path`{.xref .py .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.pipelines.images.ImagesPipeline.thumb_path "scrapy.pipelines.images.ImagesPipeline.thumb_path"){.reference
    .internal} now receives the source [[item]{.std
    .std-ref}](index.html#topics-items){.hoverxref .tooltip .reference
    .internal} ([issue
    5504](https://github.com/scrapy/scrapy/issues/5504){.reference
    .external}, [issue
    5508](https://github.com/scrapy/scrapy/issues/5508){.reference
    .external}).
:::

::: {#id26 .section}
##### Bug fixes[¶](#id26 "Permalink to this heading"){.headerlink}

-   When using Google Cloud Storage with a [[media pipeline]{.std
    .std-ref}](index.html#topics-media-pipeline){.hoverxref .tooltip
    .reference .internal}, [[`FILES_EXPIRES`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FILES_EXPIRES){.hoverxref
    .tooltip .reference .internal} now also works when
    [[`FILES_STORE`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FILES_STORE){.hoverxref
    .tooltip .reference .internal} does not point at the root of your
    Google Cloud Storage bucket ([issue
    5317](https://github.com/scrapy/scrapy/issues/5317){.reference
    .external}, [issue
    5318](https://github.com/scrapy/scrapy/issues/5318){.reference
    .external}).

-   The [[`parse`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-parse){.hoverxref
    .tooltip .reference .internal} command now supports [[asynchronous
    callbacks]{.std .std-ref}](index.html#topics-coroutines){.hoverxref
    .tooltip .reference .internal} ([issue
    5424](https://github.com/scrapy/scrapy/issues/5424){.reference
    .external}, [issue
    5577](https://github.com/scrapy/scrapy/issues/5577){.reference
    .external}).

-   When using the [[`parse`{.xref .std .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-parse){.hoverxref
    .tooltip .reference .internal} command with a URL for which there is
    no available spider, an exception is no longer raised ([issue
    3264](https://github.com/scrapy/scrapy/issues/3264){.reference
    .external}, [issue
    3265](https://github.com/scrapy/scrapy/issues/3265){.reference
    .external}, [issue
    5375](https://github.com/scrapy/scrapy/issues/5375){.reference
    .external}, [issue
    5376](https://github.com/scrapy/scrapy/issues/5376){.reference
    .external}, [issue
    5497](https://github.com/scrapy/scrapy/issues/5497){.reference
    .external}).

-   [[`TextResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} now gives higher priority to the [byte order
    mark](https://en.wikipedia.org/wiki/Byte_order_mark){.reference
    .external} when determining the text encoding of the response body,
    following the [HTML living
    standard](https://html.spec.whatwg.org/multipage/parsing.html#determining-the-character-encoding){.reference
    .external} ([issue
    5601](https://github.com/scrapy/scrapy/issues/5601){.reference
    .external}, [issue
    5611](https://github.com/scrapy/scrapy/issues/5611){.reference
    .external}).

-   MIME sniffing takes the response body into account in FTP and
    HTTP/1.0 requests, as well as in cached requests ([issue
    4873](https://github.com/scrapy/scrapy/issues/4873){.reference
    .external}).

-   MIME sniffing now detects valid HTML 5 documents even if the
    [`html`{.docutils .literal .notranslate}]{.pre} tag is missing
    ([issue
    4873](https://github.com/scrapy/scrapy/issues/4873){.reference