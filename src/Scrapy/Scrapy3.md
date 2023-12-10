
        :   [bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}
:::
:::

::: {#post-processing .section}
[]{#id2}

#### Post-Processing[¶](#post-processing "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.6.0.]{.versionmodified .added}
:::

Scrapy provides an option to activate plugins to post-process feeds
before they are exported to feed storages. In addition to using
[[builtin plugins]{.std .std-ref}](#builtin-plugins){.hoverxref .tooltip
.reference .internal}, you can create your own [[plugins]{.std
.std-ref}](#custom-plugins){.hoverxref .tooltip .reference .internal}.

These plugins can be activated through the [`postprocessing`{.docutils
.literal .notranslate}]{.pre} option of a feed. The option must be
passed a list of post-processing plugins in the order you want the feed
to be processed. These plugins can be declared either as an import
string or with the imported class of the plugin. Parameters to plugins
can be passed through the feed options. See [[feed options]{.std
.std-ref}](#feed-options){.hoverxref .tooltip .reference .internal} for
examples.

::: {#built-in-plugins .section}
[]{#builtin-plugins}

##### Built-in Plugins[¶](#built-in-plugins "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.postprocessing.]{.pre}]{.sig-prename .descclassname}[[GzipPlugin]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[BinaryIO]{.pre}](https://docs.python.org/3/library/typing.html#typing.BinaryIO "(in Python v3.12)"){.reference .external}]{.n}*, *[[feed_options]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/postprocessing.html#GzipPlugin){.reference .internal}[¶](#scrapy.extensions.postprocessing.GzipPlugin "Permalink to this definition"){.headerlink}

:   Compresses received data using
    [gzip](https://en.wikipedia.org/wiki/Gzip){.reference .external}.

    Accepted [`feed_options`{.docutils .literal .notranslate}]{.pre}
    parameters:

    -   gzip_compresslevel

    -   gzip_mtime

    -   gzip_filename

    See [[`gzip.GzipFile`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/gzip.html#gzip.GzipFile "(in Python v3.12)"){.reference
    .external} for more info about parameters.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.postprocessing.]{.pre}]{.sig-prename .descclassname}[[LZMAPlugin]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[BinaryIO]{.pre}](https://docs.python.org/3/library/typing.html#typing.BinaryIO "(in Python v3.12)"){.reference .external}]{.n}*, *[[feed_options]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/postprocessing.html#LZMAPlugin){.reference .internal}[¶](#scrapy.extensions.postprocessing.LZMAPlugin "Permalink to this definition"){.headerlink}

:   Compresses received data using
    [lzma](https://en.wikipedia.org/wiki/Lempel–Ziv–Markov_chain_algorithm){.reference
    .external}.

    Accepted [`feed_options`{.docutils .literal .notranslate}]{.pre}
    parameters:

    -   lzma_format

    -   lzma_check

    -   lzma_preset

    -   lzma_filters

    ::: {.admonition .note}
    Note

    [`lzma_filters`{.docutils .literal .notranslate}]{.pre} cannot be
    used in pypy version 7.3.1 and older.
    :::

    See [[`lzma.LZMAFile`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/lzma.html#lzma.LZMAFile "(in Python v3.12)"){.reference
    .external} for more info about parameters.

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.extensions.postprocessing.]{.pre}]{.sig-prename .descclassname}[[Bz2Plugin]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[file]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[BinaryIO]{.pre}](https://docs.python.org/3/library/typing.html#typing.BinaryIO "(in Python v3.12)"){.reference .external}]{.n}*, *[[feed_options]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/extensions/postprocessing.html#Bz2Plugin){.reference .internal}[¶](#scrapy.extensions.postprocessing.Bz2Plugin "Permalink to this definition"){.headerlink}

:   Compresses received data using
    [bz2](https://en.wikipedia.org/wiki/Bzip2){.reference .external}.

    Accepted [`feed_options`{.docutils .literal .notranslate}]{.pre}
    parameters:

    -   bz2_compresslevel

    See [[`bz2.BZ2File`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/bz2.html#bz2.BZ2File "(in Python v3.12)"){.reference
    .external} for more info about parameters.
:::

::: {#custom-plugins .section}
[]{#id3}

##### Custom Plugins[¶](#custom-plugins "Permalink to this heading"){.headerlink}

Each plugin is a class that must implement the following methods:

[[\_\_init\_\_]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[file]{.pre}]{.n}*, *[[feed_options]{.pre}]{.n}*[)]{.sig-paren}[¶](#init__ "Permalink to this definition"){.headerlink}

:   Initialize the plugin.

    Parameters

    :   -   **file** -- file-like object having at least the write, tell
            and close methods implemented

        -   **feed_options** ([[`dict`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external}) -- feed-specific [[options]{.std
            .std-ref}](#feed-options){.hoverxref .tooltip .reference
            .internal}

```{=html}
<!-- -->
```

[[write]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[data]{.pre}]{.n}*[)]{.sig-paren}[¶](#write "Permalink to this definition"){.headerlink}

:   Process and write data ([[`bytes`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
    .external} or [[`memoryview`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#memoryview "(in Python v3.12)"){.reference
    .external}) into the plugin's target file. It must return number of
    bytes written.

```{=html}
<!-- -->
```

[[close]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*[)]{.sig-paren}[¶](#close "Permalink to this definition"){.headerlink}

:   Close the target file object.

To pass a parameter to your plugin, use [[feed options]{.std
.std-ref}](#feed-options){.hoverxref .tooltip .reference .internal}. You
can then access those parameters from the [`__init__`{.docutils .literal
.notranslate}]{.pre} method of your plugin.
:::
:::

::: {#settings .section}
#### Settings[¶](#settings "Permalink to this heading"){.headerlink}

These are the settings used for configuring the feed exports:

-   [[`FEEDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEEDS){.hoverxref .tooltip
    .reference .internal} (mandatory)

-   [[`FEED_EXPORT_ENCODING`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_ENCODING){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_STORE_EMPTY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_STORE_EMPTY){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_EXPORT_FIELDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_FIELDS){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_EXPORT_INDENT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_INDENT){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_STORAGES`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_STORAGES){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_STORAGE_FTP_ACTIVE`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-FEED_STORAGE_FTP_ACTIVE){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_STORAGE_S3_ACL`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_STORAGE_S3_ACL){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_EXPORTERS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORTERS){.hoverxref
    .tooltip .reference .internal}

-   [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std .std-setting .docutils
    .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
    .tooltip .reference .internal}

::: {#feeds .section}
[]{#std-setting-FEEDS}

##### FEEDS[¶](#feeds "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.1.]{.versionmodified .added}
:::

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

A dictionary in which every key is a feed URI (or a
[[`pathlib.Path`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.12)"){.reference
.external} object) and each value is a nested dictionary containing
configuration parameters for the specific feed.

This setting is required for enabling the feed export feature.

See [[Storage backends]{.std
.std-ref}](#topics-feed-storage-backends){.hoverxref .tooltip .reference
.internal} for supported URI schemes.

For instance:

::: {.highlight-default .notranslate}
::: highlight
    {
        'items.json': {
            'format': 'json',
            'encoding': 'utf8',
            'store_empty': False,
            'item_classes': [MyItemClass1, 'myproject.items.MyItemClass2'],
            'fields': None,
            'indent': 4,
            'item_export_kwargs': {
               'export_empty_fields': True,
            },
        },
        '/home/user/documents/items.xml': {
            'format': 'xml',
            'fields': ['name', 'price'],
            'item_filter': MyCustomFilter1,
            'encoding': 'latin1',
            'indent': 8,
        },
        pathlib.Path('items.csv.gz'): {
            'format': 'csv',
            'fields': ['price', 'name'],
            'item_filter': 'myproject.filters.MyCustomFilter2',
            'postprocessing': [MyPlugin1, 'scrapy.extensions.postprocessing.GzipPlugin'],
            'gzip_compresslevel': 5,
        },
    }
:::
:::

The following is a list of the accepted keys and the setting that is
used as a fallback value if that key is not provided for a specific feed
definition:

-   [`format`{.docutils .literal .notranslate}]{.pre}: the
    [[serialization format]{.std
    .std-ref}](#topics-feed-format){.hoverxref .tooltip .reference
    .internal}.

    This setting is mandatory, there is no fallback value.

-   [`batch_item_count`{.docutils .literal .notranslate}]{.pre}: falls
    back to [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
    .tooltip .reference .internal}.

    ::: versionadded
    [New in version 2.3.0.]{.versionmodified .added}
    :::

-   [`encoding`{.docutils .literal .notranslate}]{.pre}: falls back to
    [[`FEED_EXPORT_ENCODING`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_ENCODING){.hoverxref
    .tooltip .reference .internal}.

-   [`fields`{.docutils .literal .notranslate}]{.pre}: falls back to
    [[`FEED_EXPORT_FIELDS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_FIELDS){.hoverxref
    .tooltip .reference .internal}.

-   [`item_classes`{.docutils .literal .notranslate}]{.pre}: list of
    [[item classes]{.std .std-ref}](index.html#topics-items){.hoverxref
    .tooltip .reference .internal} to export.

    If undefined or empty, all items are exported.

    ::: versionadded
    [New in version 2.6.0.]{.versionmodified .added}
    :::

-   [`item_filter`{.docutils .literal .notranslate}]{.pre}: a [[filter
    class]{.std .std-ref}](#item-filter){.hoverxref .tooltip .reference
    .internal} to filter items to export.

    [[`ItemFilter`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.extensions.feedexport.ItemFilter "scrapy.extensions.feedexport.ItemFilter"){.reference
    .internal} is used be default.

    ::: versionadded
    [New in version 2.6.0.]{.versionmodified .added}
    :::

-   [`indent`{.docutils .literal .notranslate}]{.pre}: falls back to
    [[`FEED_EXPORT_INDENT`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_EXPORT_INDENT){.hoverxref
    .tooltip .reference .internal}.

-   [`item_export_kwargs`{.docutils .literal .notranslate}]{.pre}:
    [[`dict`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
    .external} with keyword arguments for the corresponding [[item
    exporter class]{.std
    .std-ref}](index.html#topics-exporters){.hoverxref .tooltip
    .reference .internal}.

    ::: versionadded
    [New in version 2.4.0.]{.versionmodified .added}
    :::

-   [`overwrite`{.docutils .literal .notranslate}]{.pre}: whether to
    overwrite the file if it already exists ([`True`{.docutils .literal
    .notranslate}]{.pre}) or append to its content ([`False`{.docutils
    .literal .notranslate}]{.pre}).

    The default value depends on the [[storage backend]{.std
    .std-ref}](#topics-feed-storage-backends){.hoverxref .tooltip
    .reference .internal}:

    -   [[Local filesystem]{.std
        .std-ref}](#topics-feed-storage-fs){.hoverxref .tooltip
        .reference .internal}: [`False`{.docutils .literal
        .notranslate}]{.pre}

    -   [[FTP]{.std .std-ref}](#topics-feed-storage-ftp){.hoverxref
        .tooltip .reference .internal}: [`True`{.docutils .literal
        .notranslate}]{.pre}

        ::: {.admonition .note}
        Note

        Some FTP servers may not support appending to files (the
        [`APPE`{.docutils .literal .notranslate}]{.pre} FTP command).
        :::

    -   [[S3]{.std .std-ref}](#topics-feed-storage-s3){.hoverxref
        .tooltip .reference .internal}: [`True`{.docutils .literal
        .notranslate}]{.pre} (appending [is not
        supported](https://forums.aws.amazon.com/message.jspa?messageID=540395){.reference
        .external})

    -   [[Google Cloud Storage (GCS)]{.std
        .std-ref}](#topics-feed-storage-gcs){.hoverxref .tooltip
        .reference .internal}: [`True`{.docutils .literal
        .notranslate}]{.pre} (appending is not supported)

    -   [[Standard output]{.std
        .std-ref}](#topics-feed-storage-stdout){.hoverxref .tooltip
        .reference .internal}: [`False`{.docutils .literal
        .notranslate}]{.pre} (overwriting is not supported)

    ::: versionadded
    [New in version 2.4.0.]{.versionmodified .added}
    :::

-   [`store_empty`{.docutils .literal .notranslate}]{.pre}: falls back
    to [[`FEED_STORE_EMPTY`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_STORE_EMPTY){.hoverxref
    .tooltip .reference .internal}.

-   [`uri_params`{.docutils .literal .notranslate}]{.pre}: falls back to
    [[`FEED_URI_PARAMS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_URI_PARAMS){.hoverxref
    .tooltip .reference .internal}.

-   [`postprocessing`{.docutils .literal .notranslate}]{.pre}: list of
    [[plugins]{.std .std-ref}](#post-processing){.hoverxref .tooltip
    .reference .internal} to use for post-processing.

    The plugins will be used in the order of the list passed.

    ::: versionadded
    [New in version 2.6.0.]{.versionmodified .added}
    :::
:::

::: {#feed-export-encoding .section}
[]{#std-setting-FEED_EXPORT_ENCODING}

##### FEED_EXPORT_ENCODING[¶](#feed-export-encoding "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The encoding to be used for the feed.

If unset or set to [`None`{.docutils .literal .notranslate}]{.pre}
(default) it uses UTF-8 for everything except JSON output, which uses
safe numeric encoding ([`\uXXXX`{.docutils .literal .notranslate}]{.pre}
sequences) for historic reasons.

Use [`utf-8`{.docutils .literal .notranslate}]{.pre} if you want UTF-8
for JSON too.

::: versionchanged
[Changed in version 2.8: ]{.versionmodified .changed}The
[[`startproject`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
.tooltip .reference .internal} command now sets this setting to
[`utf-8`{.docutils .literal .notranslate}]{.pre} in the generated
[`settings.py`{.docutils .literal .notranslate}]{.pre} file.
:::
:::

::: {#feed-export-fields .section}
[]{#std-setting-FEED_EXPORT_FIELDS}

##### FEED_EXPORT_FIELDS[¶](#feed-export-fields "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

Use the [`FEED_EXPORT_FIELDS`{.docutils .literal .notranslate}]{.pre}
setting to define the fields to export, their order and their output
names. See [[`BaseItemExporter.fields_to_export`{.xref .py .py-attr
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exporters.BaseItemExporter.fields_to_export "scrapy.exporters.BaseItemExporter.fields_to_export"){.reference
.internal} for more information.
:::

::: {#feed-export-indent .section}
[]{#std-setting-FEED_EXPORT_INDENT}

##### FEED_EXPORT_INDENT[¶](#feed-export-indent "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

Amount of spaces used to indent the output on each level. If
[`FEED_EXPORT_INDENT`{.docutils .literal .notranslate}]{.pre} is a
non-negative integer, then array elements and object members will be
pretty-printed with that indent level. An indent level of [`0`{.docutils
.literal .notranslate}]{.pre} (the default), or negative, will put each
item on a new line. [`None`{.docutils .literal .notranslate}]{.pre}
selects the most compact representation.

Currently implemented only by [[`JsonItemExporter`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exporters.JsonItemExporter "scrapy.exporters.JsonItemExporter"){.reference
.internal} and [[`XmlItemExporter`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.exporters.XmlItemExporter "scrapy.exporters.XmlItemExporter"){.reference
.internal}, i.e. when you are exporting to [`.json`{.docutils .literal
.notranslate}]{.pre} or [`.xml`{.docutils .literal .notranslate}]{.pre}.
:::

::: {#feed-store-empty .section}
[]{#std-setting-FEED_STORE_EMPTY}

##### FEED_STORE_EMPTY[¶](#feed-store-empty "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether to export empty feeds (i.e. feeds with no items). If
[`False`{.docutils .literal .notranslate}]{.pre}, and there are no items
to export, no new files are created and existing files are not modified,
even if the [[overwrite feed option]{.std
.std-ref}](#feed-options){.hoverxref .tooltip .reference .internal} is
enabled.
:::

::: {#feed-storages .section}
[]{#std-setting-FEED_STORAGES}

##### FEED_STORAGES[¶](#feed-storages "Permalink to this heading"){.headerlink}

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing additional feed storage backends supported by your
project. The keys are URI schemes and the values are paths to storage
classes.
:::

::: {#feed-storage-ftp-active .section}
[]{#std-setting-FEED_STORAGE_FTP_ACTIVE}

##### FEED_STORAGE_FTP_ACTIVE[¶](#feed-storage-ftp-active "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Whether to use the active connection mode when exporting feeds to an FTP
server ([`True`{.docutils .literal .notranslate}]{.pre}) or use the
passive connection mode instead ([`False`{.docutils .literal
.notranslate}]{.pre}, default).

For information about FTP connection modes, see [What is the difference
between active and passive
FTP?](https://stackoverflow.com/a/1699163){.reference .external}.
:::

::: {#feed-storage-s3-acl .section}
[]{#std-setting-FEED_STORAGE_S3_ACL}

##### FEED_STORAGE_S3_ACL[¶](#feed-storage-s3-acl "Permalink to this heading"){.headerlink}

Default: [`''`{.docutils .literal .notranslate}]{.pre} (empty string)

A string containing a custom ACL for feeds exported to Amazon S3 by your
project.

For a complete list of available values, access the [Canned
ACL](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl){.reference
.external} section on Amazon S3 docs.
:::

::: {#feed-storages-base .section}
[]{#std-setting-FEED_STORAGES_BASE}

##### FEED_STORAGES_BASE[¶](#feed-storages-base "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "": "scrapy.extensions.feedexport.FileFeedStorage",
        "file": "scrapy.extensions.feedexport.FileFeedStorage",
        "stdout": "scrapy.extensions.feedexport.StdoutFeedStorage",
        "s3": "scrapy.extensions.feedexport.S3FeedStorage",
        "ftp": "scrapy.extensions.feedexport.FTPFeedStorage",
    }
:::
:::

A dict containing the built-in feed storage backends supported by
Scrapy. You can disable any of these backends by assigning
[`None`{.docutils .literal .notranslate}]{.pre} to their URI scheme in
[[`FEED_STORAGES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FEED_STORAGES){.hoverxref .tooltip
.reference .internal}. E.g., to disable the built-in FTP storage backend
(without replacement), place this in your [`settings.py`{.docutils
.literal .notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    FEED_STORAGES = {
        "ftp": None,
    }
:::
:::
:::

::: {#feed-exporters .section}
[]{#std-setting-FEED_EXPORTERS}

##### FEED_EXPORTERS[¶](#feed-exporters "Permalink to this heading"){.headerlink}

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing additional exporters supported by your project. The
keys are serialization formats and the values are paths to [[Item
exporter]{.std .std-ref}](index.html#topics-exporters){.hoverxref
.tooltip .reference .internal} classes.
:::

::: {#feed-exporters-base .section}
[]{#std-setting-FEED_EXPORTERS_BASE}

##### FEED_EXPORTERS_BASE[¶](#feed-exporters-base "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "json": "scrapy.exporters.JsonItemExporter",
        "jsonlines": "scrapy.exporters.JsonLinesItemExporter",
        "jsonl": "scrapy.exporters.JsonLinesItemExporter",
        "jl": "scrapy.exporters.JsonLinesItemExporter",
        "csv": "scrapy.exporters.CsvItemExporter",
        "xml": "scrapy.exporters.XmlItemExporter",
        "marshal": "scrapy.exporters.MarshalItemExporter",
        "pickle": "scrapy.exporters.PickleItemExporter",
    }
:::
:::

A dict containing the built-in feed exporters supported by Scrapy. You
can disable any of these exporters by assigning [`None`{.docutils
.literal .notranslate}]{.pre} to their serialization format in
[[`FEED_EXPORTERS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-FEED_EXPORTERS){.hoverxref .tooltip
.reference .internal}. E.g., to disable the built-in CSV exporter
(without replacement), place this in your [`settings.py`{.docutils
.literal .notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    FEED_EXPORTERS = {
        "csv": None,
    }
:::
:::
:::

::: {#feed-export-batch-item-count .section}
[]{#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT}

##### FEED_EXPORT_BATCH_ITEM_COUNT[¶](#feed-export-batch-item-count "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.3.0.]{.versionmodified .added}
:::

Default: [`0`{.docutils .literal .notranslate}]{.pre}

If assigned an integer number higher than [`0`{.docutils .literal
.notranslate}]{.pre}, Scrapy generates multiple output files storing up
to the specified number of items in each output file.

When generating multiple output files, you must use at least one of the
following placeholders in the feed URI to indicate how the different
output file names are generated:

-   [`%(batch_time)s`{.docutils .literal .notranslate}]{.pre} - gets
    replaced by a timestamp when the feed is being created (e.g.
    [`2020-03-28T14-45-08.237134`{.docutils .literal
    .notranslate}]{.pre})

-   [`%(batch_id)d`{.docutils .literal .notranslate}]{.pre} - gets
    replaced by the 1-based sequence number of the batch.

    Use [[printf-style string formatting]{.xref .std
    .std-ref}](https://docs.python.org/3/library/stdtypes.html#old-string-formatting "(in Python v3.12)"){.reference
    .external} to alter the number format. For example, to make the
    batch ID a 5-digit number by introducing leading zeroes as needed,
    use [`%(batch_id)05d`{.docutils .literal .notranslate}]{.pre} (e.g.
    [`3`{.docutils .literal .notranslate}]{.pre} becomes
    [`00003`{.docutils .literal .notranslate}]{.pre}, [`123`{.docutils
    .literal .notranslate}]{.pre} becomes [`00123`{.docutils .literal
    .notranslate}]{.pre}).

For instance, if your settings include:

::: {.highlight-python .notranslate}
::: highlight
    FEED_EXPORT_BATCH_ITEM_COUNT = 100
:::
:::

And your [[`crawl`{.xref .std .std-command .docutils .literal
.notranslate}]{.pre}](index.html#std-command-crawl){.hoverxref .tooltip
.reference .internal} command line is:

::: {.highlight-default .notranslate}
::: highlight
    scrapy crawl spidername -o "dirname/%(batch_id)d-filename%(batch_time)s.json"
:::
:::

The command line above can generate a directory tree like:

::: {.highlight-default .notranslate}
::: highlight
    ->projectname
    -->dirname
    --->1-filename2020-03-28T14-45-08.237134.json
    --->2-filename2020-03-28T14-45-09.148903.json
    --->3-filename2020-03-28T14-45-10.046092.json
:::
:::

Where the first and second files contain exactly 100 items. The last one
contains 100 items or fewer.
:::

::: {#feed-uri-params .section}
[]{#std-setting-FEED_URI_PARAMS}

##### FEED_URI_PARAMS[¶](#feed-uri-params "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

A string with the import path of a function to set the parameters to
apply with [[printf-style string formatting]{.xref .std
.std-ref}](https://docs.python.org/3/library/stdtypes.html#old-string-formatting "(in Python v3.12)"){.reference
.external} to the feed URI.

The function signature should be as follows:

[[scrapy.extensions.feedexport.]{.pre}]{.sig-prename .descclassname}[[uri_params]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[params]{.pre}]{.n}*, *[[spider]{.pre}]{.n}*[)]{.sig-paren}[¶](#scrapy.extensions.feedexport.uri_params "Permalink to this definition"){.headerlink}

:   Return a [[`dict`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
    .external} of key-value pairs to apply to the feed URI using
    [[printf-style string formatting]{.xref .std
    .std-ref}](https://docs.python.org/3/library/stdtypes.html#old-string-formatting "(in Python v3.12)"){.reference
    .external}.

    Parameters

    :   -   **params**
            ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external}) --

            default key-value pairs

            Specifically:

            -   [`batch_id`{.docutils .literal .notranslate}]{.pre}: ID
                of the file batch. See
                [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std .std-setting
                .docutils .literal
                .notranslate}]{.pre}](#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
                .tooltip .reference .internal}.

                If [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std
                .std-setting .docutils .literal
                .notranslate}]{.pre}](#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
                .tooltip .reference .internal} is [`0`{.docutils
                .literal .notranslate}]{.pre}, [`batch_id`{.docutils
                .literal .notranslate}]{.pre} is always [`1`{.docutils
                .literal .notranslate}]{.pre}.

                ::: versionadded
                [New in version 2.3.0.]{.versionmodified .added}
                :::

            -   [`batch_time`{.docutils .literal .notranslate}]{.pre}:
                UTC date and time, in ISO format with [`:`{.docutils
                .literal .notranslate}]{.pre} replaced with
                [`-`{.docutils .literal .notranslate}]{.pre}.

                See [[`FEED_EXPORT_BATCH_ITEM_COUNT`{.xref .std
                .std-setting .docutils .literal
                .notranslate}]{.pre}](#std-setting-FEED_EXPORT_BATCH_ITEM_COUNT){.hoverxref
                .tooltip .reference .internal}.

                ::: versionadded
                [New in version 2.3.0.]{.versionmodified .added}
                :::

            -   [`time`{.docutils .literal .notranslate}]{.pre}:
                [`batch_time`{.docutils .literal .notranslate}]{.pre},
                with microseconds set to [`0`{.docutils .literal
                .notranslate}]{.pre}.

        -   **spider**
            ([*scrapy.Spider*](index.html#scrapy.Spider "scrapy.Spider"){.reference
            .internal}) -- source spider of the feed items

    ::: {.admonition .caution}
    Caution

    The function should return a new dictionary, modifying the received
    [`params`{.docutils .literal .notranslate}]{.pre} in-place is
    deprecated.
    :::

For example, to include the [[`name`{.xref .py .py-attr .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.Spider.name "scrapy.Spider.name"){.reference
.internal} of the source spider in the feed URI:

1.  Define the following function somewhere in your project:

    ::: {.highlight-python .notranslate}
    ::: highlight
        # myproject/utils.py
        def uri_params(params, spider):
            return {**params, "spider_name": spider.name}
    :::
    :::

2.  Point [[`FEED_URI_PARAMS`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](#std-setting-FEED_URI_PARAMS){.hoverxref
    .tooltip .reference .internal} to that function in your settings:

    ::: {.highlight-python .notranslate}
    ::: highlight
        # myproject/settings.py
        FEED_URI_PARAMS = "myproject.utils.uri_params"
    :::
    :::

3.  Use [`%(spider_name)s`{.docutils .literal .notranslate}]{.pre} in
    your feed URI:

    ::: {.highlight-default .notranslate}
    ::: highlight
        scrapy crawl <spider_name> -o "%(spider_name)s.jsonl"
    :::
    :::
:::
:::
:::

[]{#document-topics/request-response}

::: {#module-scrapy.http .section}
[]{#requests-and-responses}[]{#topics-request-response}

### Requests and Responses[¶](#module-scrapy.http "Permalink to this heading"){.headerlink}

Scrapy uses [[`Request`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
.internal} and [[`Response`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} objects for crawling web sites.

Typically, [[`Request`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
.internal} objects are generated in the spiders and pass across the
system until they reach the Downloader, which executes the request and
returns a [[`Response`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} object which travels back to the spider that issued the
request.

Both [[`Request`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
.internal} and [[`Response`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} classes have subclasses which add functionality not required
in the base classes. These are described below in [[Request
subclasses]{.std
.std-ref}](#topics-request-response-ref-request-subclasses){.hoverxref
.tooltip .reference .internal} and [[Response subclasses]{.std
.std-ref}](#topics-request-response-ref-response-subclasses){.hoverxref
.tooltip .reference .internal}.

::: {#request-objects .section}
#### Request objects[¶](#request-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.http.]{.pre}]{.sig-prename .descclassname}[[Request]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[\*]{.pre}]{.o}[[args]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/request.html#Request){.reference .internal}[¶](#scrapy.http.Request "Permalink to this definition"){.headerlink}

:   Represents an HTTP request, which is usually generated in a Spider
    and executed by the Downloader, thus generating a [[`Response`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal}.

    Parameters

    :   -   **url**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) --

            the URL of this request

            If the URL is invalid, a [[`ValueError`{.xref .py .py-exc
            .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/exceptions.html#ValueError "(in Python v3.12)"){.reference
            .external} exception is raised.

        -   **callback**
            ([*collections.abc.Callable*](https://docs.python.org/3/library/collections.abc.html#collections.abc.Callable "(in Python v3.12)"){.reference
            .external}) --

            the function that will be called with the response of this
            request (once it's downloaded) as its first parameter.

            In addition to a function, the following values are
            supported:

            -   [`None`{.docutils .literal .notranslate}]{.pre}
                (default), which indicates that the spider's
                [[`parse()`{.xref .py .py-meth .docutils .literal
                .notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
                .internal} method must be used.

            -   [[`NO_CALLBACK()`{.xref .py .py-func .docutils .literal
                .notranslate}]{.pre}](#scrapy.http.request.NO_CALLBACK "scrapy.http.request.NO_CALLBACK"){.reference
                .internal}

            For more information, see [[Passing additional data to
            callback functions]{.std
            .std-ref}](#topics-request-response-ref-request-callback-arguments){.hoverxref
            .tooltip .reference .internal}.

            ::: {.admonition .note}
            Note

            If exceptions are raised during processing,
            [`errback`{.docutils .literal .notranslate}]{.pre} is called
            instead.
            :::

        -   **method**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the HTTP method of this request. Defaults to
            [`'GET'`{.docutils .literal .notranslate}]{.pre}.

        -   **meta**
            ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external}) -- the initial values for the
            [[`Request.meta`{.xref .py .py-attr .docutils .literal
            .notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
            .internal} attribute. If given, the dict passed in this
            parameter will be shallow copied.

        -   **body**
            ([*bytes*](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
            .external} *or*
            [*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the request body. If a string is passed, then
            it's encoded as bytes using the [`encoding`{.docutils
            .literal .notranslate}]{.pre} passed (which defaults to
            [`utf-8`{.docutils .literal .notranslate}]{.pre}). If
            [`body`{.docutils .literal .notranslate}]{.pre} is not
            given, an empty bytes object is stored. Regardless of the
            type of this argument, the final value stored will be a
            bytes object (never a string or [`None`{.docutils .literal
            .notranslate}]{.pre}).

        -   **headers**
            ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external}) --

            the headers of this request. The dict values can be strings
            (for single valued headers) or lists (for multi-valued
            headers). If [`None`{.docutils .literal .notranslate}]{.pre}
            is passed as value, the HTTP header will not be sent at all.

            > <div>
            >
            > ::: {.admonition .caution}
            > Caution
            >
            > Cookies set via the [`Cookie`{.docutils .literal
            > .notranslate}]{.pre} header are not considered by the
            > [[CookiesMiddleware]{.std
            > .std-ref}](index.html#cookies-mw){.hoverxref .tooltip
            > .reference .internal}. If you need to set cookies for a
            > request, use the [`Request.cookies`{.xref .py .py-class
            > .docutils .literal .notranslate}]{.pre} parameter. This is
            > a known current limitation that is being worked on.
            > :::
            >
            > </div>

        -   **cookies**
            ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) --

            the request cookies. These can be sent in two forms.

            1.  Using a dict:

            ::: {.highlight-python .notranslate}
            ::: highlight
                request_with_cookies = Request(
                    url="http://www.example.com",
                    cookies={"currency": "USD", "country": "UY"},
                )
            :::
            :::

            2.  Using a list of dicts:

            ::: {.highlight-python .notranslate}
            ::: highlight
                request_with_cookies = Request(
                    url="http://www.example.com",
                    cookies=[
                        {
                            "name": "currency",
                            "value": "USD",
                            "domain": "example.com",
                            "path": "/currency",
                        },
                    ],
                )
            :::
            :::

            The latter form allows for customizing the
            [`domain`{.docutils .literal .notranslate}]{.pre} and
            [`path`{.docutils .literal .notranslate}]{.pre} attributes
            of the cookie. This is only useful if the cookies are saved
            for later requests.

            []{#std-reqmeta-dont_merge_cookies .target}

            When some site returns cookies (in a response) those are
            stored in the cookies for that domain and will be sent again
            in future requests. That's the typical behaviour of any
            regular web browser.

            Note that setting the [[`dont_merge_cookies`{.xref .std
            .std-reqmeta .docutils .literal
            .notranslate}]{.pre}](#std-reqmeta-dont_merge_cookies){.hoverxref
            .tooltip .reference .internal} key to [`True`{.docutils
            .literal .notranslate}]{.pre} in [`request.meta`{.xref .py
            .py-attr .docutils .literal .notranslate}]{.pre} causes
            custom cookies to be ignored.

            For more info see [[CookiesMiddleware]{.std
            .std-ref}](index.html#cookies-mw){.hoverxref .tooltip
            .reference .internal}.

            ::: {.admonition .caution}
            Caution

            Cookies set via the [`Cookie`{.docutils .literal
            .notranslate}]{.pre} header are not considered by the
            [[CookiesMiddleware]{.std
            .std-ref}](index.html#cookies-mw){.hoverxref .tooltip
            .reference .internal}. If you need to set cookies for a
            request, use the [`Request.cookies`{.xref .py .py-class
            .docutils .literal .notranslate}]{.pre} parameter. This is a
            known current limitation that is being worked on.
            :::

            ::: versionadded
            [New in version 2.6.0: ]{.versionmodified .added}Cookie
            values that are [[`bool`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}, [[`float`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#float "(in Python v3.12)"){.reference
            .external} or [[`int`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
            .external} are casted to [[`str`{.xref .py .py-class
            .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}.
            :::

        -   **encoding**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the encoding of this request (defaults to
            [`'utf-8'`{.docutils .literal .notranslate}]{.pre}). This
            encoding will be used to percent-encode the URL and to
            convert the body to bytes (if given as a string).

        -   **priority**
            ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
            .external}) -- the priority of this request (defaults to
            [`0`{.docutils .literal .notranslate}]{.pre}). The priority
            is used by the scheduler to define the order used to process
            requests. Requests with a higher priority value will execute
            earlier. Negative values are allowed in order to indicate
            relatively low-priority.

        -   **dont_filter**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- indicates that this request should not be
            filtered by the scheduler. This is used when you want to
            perform an identical request multiple times, to ignore the
            duplicates filter. Use it with care, or you will get into
            crawling loops. Default to [`False`{.docutils .literal
            .notranslate}]{.pre}.

        -   **errback**
            ([*collections.abc.Callable*](https://docs.python.org/3/library/collections.abc.html#collections.abc.Callable "(in Python v3.12)"){.reference
            .external}) --

            a function that will be called if any exception was raised
            while processing the request. This includes pages that
            failed with 404 HTTP errors and such. It receives a
            [[`Failure`{.xref .py .py-exc .docutils .literal
            .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference
            .external} as first parameter. For more information, see
            [[Using errbacks to catch exceptions in request
            processing]{.std
            .std-ref}](#topics-request-response-ref-errbacks){.hoverxref
            .tooltip .reference .internal} below.

            ::: versionchanged
            [Changed in version 2.0: ]{.versionmodified .changed}The
            *callback* parameter is no longer required when the
            *errback* parameter is specified.
            :::

        -   **flags**
            ([*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- Flags sent to the request, can be used for
            logging or similar purposes.

        -   **cb_kwargs**
            ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external}) -- A dict with arbitrary data that will be
            passed as keyword arguments to the Request's callback.

    [[url]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Request.url "Permalink to this definition"){.headerlink}

    :   A string containing the URL of this request. Keep in mind that
        this attribute contains the escaped URL, so it can differ from
        the URL passed in the [`__init__`{.docutils .literal
        .notranslate}]{.pre} method.

        This attribute is read-only. To change the URL of a Request use
        [[`replace()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.replace "scrapy.http.Request.replace"){.reference
        .internal}.

    [[method]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Request.method "Permalink to this definition"){.headerlink}

    :   A string representing the HTTP method in the request. This is
        guaranteed to be uppercase. Example: [`"GET"`{.docutils .literal
        .notranslate}]{.pre}, [`"POST"`{.docutils .literal
        .notranslate}]{.pre}, [`"PUT"`{.docutils .literal
        .notranslate}]{.pre}, etc

    [[headers]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Request.headers "Permalink to this definition"){.headerlink}

    :   A dictionary-like object which contains the request headers.

    [[body]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Request.body "Permalink to this definition"){.headerlink}

    :   The request body as bytes.

        This attribute is read-only. To change the body of a Request use
        [[`replace()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.replace "scrapy.http.Request.replace"){.reference
        .internal}.

    [[meta]{.pre}]{.sig-name .descname}*[ ]{.w}[[=]{.pre}]{.p}[ ]{.w}[{}]{.pre}*[¶](#scrapy.http.Request.meta "Permalink to this definition"){.headerlink}

    :   <div>
        >
        > A dictionary of arbitrary metadata for the request.
        >
        > You may extend request metadata as you see fit.
        >
        > Request metadata can also be accessed through the
        > [[`meta`{.xref .py .py-attr .docutils .literal
        > .notranslate}]{.pre}](#scrapy.http.Response.meta "scrapy.http.Response.meta"){.reference
        > .internal} attribute of a response.
        >
        > To pass data from one spider callback to another, consider
        > using [[`cb_kwargs`{.xref .py .py-attr .docutils .literal
        > .notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
        > .internal} instead. However, request metadata may be the right
        > choice in certain scenarios, such as to maintain some
        > debugging data across all follow-up requests (e.g. the source
        > URL).
        >
        > A common use of request metadata is to define request-specific
        > parameters for Scrapy components (extensions, middlewares,
        > etc.). For example, if you set [`dont_retry`{.docutils
        > .literal .notranslate}]{.pre} to [`True`{.docutils .literal
        > .notranslate}]{.pre}, [[`RetryMiddleware`{.xref .py .py-class
        > .docutils .literal
        > .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.RetryMiddleware "scrapy.downloadermiddlewares.retry.RetryMiddleware"){.reference
        > .internal} will never retry that request, even if it fails.
        > See [[Request.meta special keys]{.std
        > .std-ref}](#topics-request-meta){.hoverxref .tooltip
        > .reference .internal}.
        >
        > You may also use request metadata in your custom Scrapy
        > components, for example, to keep request state information
        > relevant to your component. For example,
        > [[`RetryMiddleware`{.xref .py .py-class .docutils .literal
        > .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.retry.RetryMiddleware "scrapy.downloadermiddlewares.retry.RetryMiddleware"){.reference
        > .internal} uses the [`retry_times`{.docutils .literal
        > .notranslate}]{.pre} metadata key to keep track of how many
        > times a request has been retried so far.
        >
        > Copying all the metadata of a previous request into a new,
        > follow-up request in a spider callback is a bad practice,
        > because request metadata may include metadata set by Scrapy
        > components that is not meant to be copied into other requests.
        > For example, copying the [`retry_times`{.docutils .literal
        > .notranslate}]{.pre} metadata key into follow-up requests can
        > lower the amount of retries allowed for those follow-up
        > requests.
        >
        > You should only copy all request metadata from one request to
        > another if the new request is meant to replace the old
        > request, as is often the case when returning a request from a
        > [[downloader middleware]{.std
        > .std-ref}](index.html#topics-downloader-middleware){.hoverxref
        > .tooltip .reference .internal} method.
        >
        > Also mind that the [[`copy()`{.xref .py .py-meth .docutils
        > .literal
        > .notranslate}]{.pre}](#scrapy.http.Request.copy "scrapy.http.Request.copy"){.reference
        > .internal} and [[`replace()`{.xref .py .py-meth .docutils
        > .literal
        > .notranslate}]{.pre}](#scrapy.http.Request.replace "scrapy.http.Request.replace"){.reference
        > .internal} request methods [[shallow-copy]{.xref .std
        > .std-doc}](https://docs.python.org/3/library/copy.html "(in Python v3.12)"){.reference
        > .external} request metadata.
        >
        > </div>

    [[cb_kwargs]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Request.cb_kwargs "Permalink to this definition"){.headerlink}

    :   A dictionary that contains arbitrary metadata for this request.
        Its contents will be passed to the Request's callback as keyword
        arguments. It is empty for new Requests, which means by default
        callbacks only get a [[`Response`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal} object as argument.

        This dict is [[shallow copied]{.xref .std
        .std-doc}](https://docs.python.org/3/library/copy.html "(in Python v3.12)"){.reference
        .external} when the request is cloned using the
        [`copy()`{.docutils .literal .notranslate}]{.pre} or
        [`replace()`{.docutils .literal .notranslate}]{.pre} methods,
        and can also be accessed, in your spider, from the
        [`response.cb_kwargs`{.docutils .literal .notranslate}]{.pre}
        attribute.

        In case of a failure to process the request, this dict can be
        accessed as [`failure.request.cb_kwargs`{.docutils .literal
        .notranslate}]{.pre} in the request's errback. For more
        information, see [[Accessing additional data in errback
        functions]{.std .std-ref}](#errback-cb-kwargs){.hoverxref
        .tooltip .reference .internal}.

    [[attributes]{.pre}]{.sig-name .descname}*[[:]{.pre}]{.p}[ ]{.w}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[\...]{.pre}]{.p}[[\]]{.pre}]{.p}[ ]{.w}[[=]{.pre}]{.p}[ ]{.w}[(\'url\',]{.pre} [\'callback\',]{.pre} [\'method\',]{.pre} [\'headers\',]{.pre} [\'body\',]{.pre} [\'cookies\',]{.pre} [\'meta\',]{.pre} [\'encoding\',]{.pre} [\'priority\',]{.pre} [\'dont_filter\',]{.pre} [\'errback\',]{.pre} [\'flags\',]{.pre} [\'cb_kwargs\')]{.pre}*[¶](#scrapy.http.Request.attributes "Permalink to this definition"){.headerlink}

    :   A tuple of [[`str`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
        .external} objects containing the name of all public attributes
        of the class that are also keyword parameters of the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method.

        Currently used by [[`Request.replace()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.replace "scrapy.http.Request.replace"){.reference
        .internal}, [[`Request.to_dict()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Request.to_dict "scrapy.http.Request.to_dict"){.reference
        .internal} and [[`request_from_dict()`{.xref .py .py-func
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.utils.request.request_from_dict "scrapy.utils.request.request_from_dict"){.reference
        .internal}.

    [[copy]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/request.html#Request.copy){.reference .internal}[¶](#scrapy.http.Request.copy "Permalink to this definition"){.headerlink}

    :   Return a new Request which is a copy of this Request. See also:
        [[Passing additional data to callback functions]{.std
        .std-ref}](#topics-request-response-ref-request-callback-arguments){.hoverxref
        .tooltip .reference .internal}.

    [[replace]{.pre}]{.sig-name .descname}[(]{.sig-paren}[\[]{.optional}*[[url]{.pre}]{.n}*, *[[method]{.pre}]{.n}*, *[[headers]{.pre}]{.n}*, *[[body]{.pre}]{.n}*, *[[cookies]{.pre}]{.n}*, *[[meta]{.pre}]{.n}*, *[[flags]{.pre}]{.n}*, *[[encoding]{.pre}]{.n}*, *[[priority]{.pre}]{.n}*, *[[dont_filter]{.pre}]{.n}*, *[[callback]{.pre}]{.n}*, *[[errback]{.pre}]{.n}*, *[[cb_kwargs]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/request.html#Request.replace){.reference .internal}[¶](#scrapy.http.Request.replace "Permalink to this definition"){.headerlink}

    :   Return a Request object with the same members, except for those
        members given new values by whichever keyword arguments are
        specified. The [[`Request.cb_kwargs`{.xref .py .py-attr
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
        .internal} and [[`Request.meta`{.xref .py .py-attr .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
        .internal} attributes are shallow copied by default (unless new
        values are given as arguments). See also [[Passing additional
        data to callback functions]{.std
        .std-ref}](#topics-request-response-ref-request-callback-arguments){.hoverxref
        .tooltip .reference .internal}.

    *[classmethod]{.pre}[ ]{.w}*[[from_curl]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[curl_command]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[ignore_unknown_options]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[True]{.pre}]{.default_value}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[RequestTypeVar]{.pre}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/request.html#Request.from_curl){.reference .internal}[¶](#scrapy.http.Request.from_curl "Permalink to this definition"){.headerlink}

    :   Create a Request object from a string containing a
        [cURL](https://curl.haxx.se/){.reference .external} command. It
        populates the HTTP method, the URL, the headers, the cookies and
        the body. It accepts the same arguments as the [[`Request`{.xref
        .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} class, taking preference and overriding the values of
        the same arguments contained in the cURL command.

        Unrecognized options are ignored by default. To raise an error
        when finding unknown options call this method by passing
        [`ignore_unknown_options=False`{.docutils .literal
        .notranslate}]{.pre}.

        ::: {.admonition .caution}
        Caution

        Using [[`from_curl()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.from_curl "scrapy.http.Request.from_curl"){.reference
        .internal} from [[`Request`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} subclasses, such as [[`JsonRequest`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.JsonRequest "scrapy.http.JsonRequest"){.reference
        .internal}, or [`XmlRpcRequest`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre}, as well as having [[downloader
        middlewares]{.std
        .std-ref}](index.html#topics-downloader-middleware){.hoverxref
        .tooltip .reference .internal} and [[spider middlewares]{.std
        .std-ref}](index.html#topics-spider-middleware){.hoverxref
        .tooltip .reference .internal} enabled, such as
        [[`DefaultHeadersMiddleware`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware "scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware"){.reference
        .internal}, [[`UserAgentMiddleware`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.useragent.UserAgentMiddleware "scrapy.downloadermiddlewares.useragent.UserAgentMiddleware"){.reference
        .internal}, or [[`HttpCompressionMiddleware`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware "scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware"){.reference
        .internal}, may modify the [[`Request`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object.
        :::

        To translate a cURL command into a Scrapy request, you may use
        [curl2scrapy](https://michael-shub.github.io/curl2scrapy/){.reference
        .external}.

    [[to_dict]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[\*]{.pre}]{.o}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/request.html#Request.to_dict){.reference .internal}[¶](#scrapy.http.Request.to_dict "Permalink to this definition"){.headerlink}

    :   Return a dictionary containing the Request's data.

        Use [[`request_from_dict()`{.xref .py .py-func .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.utils.request.request_from_dict "scrapy.utils.request.request_from_dict"){.reference
        .internal} to convert back into a [`Request`{.xref .py .py-class
        .docutils .literal .notranslate}]{.pre} object.

        If a spider is given, this method will try to find out the name
        of the spider methods used as callback and errback and include
        them in the output dict, raising an exception if they cannot be
        found.

::: {#other-functions-related-to-requests .section}
##### Other functions related to requests[¶](#other-functions-related-to-requests "Permalink to this heading"){.headerlink}

[[scrapy.http.request.]{.pre}]{.sig-prename .descclassname}[[NO_CALLBACK]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[\*]{.pre}]{.o}[[args]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[NoReturn]{.pre}](https://docs.python.org/3/library/typing.html#typing.NoReturn "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/request.html#NO_CALLBACK){.reference .internal}[¶](#scrapy.http.request.NO_CALLBACK "Permalink to this definition"){.headerlink}

:   When assigned to the [`callback`{.docutils .literal
    .notranslate}]{.pre} parameter of [[`Request`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal}, it indicates that the request is not meant to have a
    spider callback at all.

    For example:

    ::: {.highlight-python .notranslate}
    ::: highlight
        Request("https://example.com", callback=NO_CALLBACK)
    :::
    :::

    This value should be used by [[components]{.std
    .std-ref}](index.html#topics-components){.hoverxref .tooltip
    .reference .internal} that create and handle their own requests,
    e.g. through [`scrapy.core.engine.ExecutionEngine.download()`{.xref
    .py .py-meth .docutils .literal .notranslate}]{.pre}, so that
    downloader middlewares handling such requests can treat them
    differently from requests intended for the [[`parse()`{.xref .py
    .py-meth .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.Spider.parse "scrapy.Spider.parse"){.reference
    .internal} callback.

```{=html}
<!-- -->
```

[[scrapy.utils.request.]{.pre}]{.sig-prename .descclassname}[[request_from_dict]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[d]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*]{.pre}]{.o}*, *[[spider]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Spider]{.pre}](index.html#scrapy.spiders.Spider "scrapy.spiders.Spider"){.reference .internal}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/request.html#request_from_dict){.reference .internal}[¶](#scrapy.utils.request.request_from_dict "Permalink to this definition"){.headerlink}

:   Create a [`Request`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} object from a dict.

    If a spider is given, it will try to resolve the callbacks looking
    at the spider for methods with the same name.
:::

::: {#passing-additional-data-to-callback-functions .section}
[]{#topics-request-response-ref-request-callback-arguments}

##### Passing additional data to callback functions[¶](#passing-additional-data-to-callback-functions "Permalink to this heading"){.headerlink}

The callback of a request is a function that will be called when the
response of that request is downloaded. The callback function will be
called with the downloaded [[`Response`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} object as its first argument.

Example:

::: {.highlight-python .notranslate}
::: highlight
    def parse_page1(self, response):
        return scrapy.Request(
            "http://www.example.com/some_page.html", callback=self.parse_page2
        )


    def parse_page2(self, response):
        # this would log http://www.example.com/some_page.html
        self.logger.info("Visited %s", response.url)
:::
:::

In some cases you may be interested in passing arguments to those
callback functions so you can receive the arguments later, in the second
callback. The following example shows how to achieve this by using the
[[`Request.cb_kwargs`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
.internal} attribute:

::: {.highlight-python .notranslate}
::: highlight
    def parse(self, response):
        request = scrapy.Request(
            "http://www.example.com/index.html",
            callback=self.parse_page2,
            cb_kwargs=dict(main_url=response.url),
        )
        request.cb_kwargs["foo"] = "bar"  # add more arguments for the callback
        yield request


    def parse_page2(self, response, main_url, foo):
        yield dict(
            main_url=main_url,
            other_url=response.url,
            foo=foo,
        )
:::
:::

::: {.admonition .caution}
Caution

[[`Request.cb_kwargs`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
.internal} was introduced in version [`1.7`{.docutils .literal
.notranslate}]{.pre}. Prior to that, using [[`Request.meta`{.xref .py
.py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
.internal} was recommended for passing information around callbacks.
After [`1.7`{.docutils .literal .notranslate}]{.pre},
[[`Request.cb_kwargs`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
.internal} became the preferred way for handling user information,
leaving [[`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
.internal} for communication with components like middlewares and
extensions.
:::
:::

::: {#using-errbacks-to-catch-exceptions-in-request-processing .section}
[]{#topics-request-response-ref-errbacks}

##### Using errbacks to catch exceptions in request processing[¶](#using-errbacks-to-catch-exceptions-in-request-processing "Permalink to this heading"){.headerlink}

The errback of a request is a function that will be called when an
exception is raise while processing it.

It receives a [[`Failure`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.python.failure.Failure.html "(in Twisted)"){.reference
.external} as first parameter and can be used to track connection
establishment timeouts, DNS errors etc.

Here's an example spider logging all errors and catching some specific
errors if needed:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy

    from scrapy.spidermiddlewares.httperror import HttpError
    from twisted.internet.error import DNSLookupError
    from twisted.internet.error import TimeoutError, TCPTimedOutError


    class ErrbackSpider(scrapy.Spider):
        name = "errback_example"
        start_urls = [
            "http://www.httpbin.org/",  # HTTP 200 expected
            "http://www.httpbin.org/status/404",  # Not found error
            "http://www.httpbin.org/status/500",  # server issue
            "http://www.httpbin.org:12345/",  # non-responding host, timeout expected
            "https://example.invalid/",  # DNS error expected
        ]

        def start_requests(self):
            for u in self.start_urls:
                yield scrapy.Request(
                    u,
                    callback=self.parse_httpbin,
                    errback=self.errback_httpbin,
                    dont_filter=True,
                )

        def parse_httpbin(self, response):
            self.logger.info("Got successful response from {}".format(response.url))
            # do something useful here...

        def errback_httpbin(self, failure):
            # log all failures
            self.logger.error(repr(failure))

            # in case you want to do something special for some errors,
            # you may need the failure's type:

            if failure.check(HttpError):
                # these exceptions come from HttpError spider middleware
                # you can get the non-200 response
                response = failure.value.response
                self.logger.error("HttpError on %s", response.url)

            elif failure.check(DNSLookupError):
                # this is the original request
                request = failure.request
                self.logger.error("DNSLookupError on %s", request.url)

            elif failure.check(TimeoutError, TCPTimedOutError):
                request = failure.request
                self.logger.error("TimeoutError on %s", request.url)
:::
:::
:::

::: {#accessing-additional-data-in-errback-functions .section}
[]{#errback-cb-kwargs}

##### Accessing additional data in errback functions[¶](#accessing-additional-data-in-errback-functions "Permalink to this heading"){.headerlink}

In case of a failure to process the request, you may be interested in
accessing arguments to the callback functions so you can process further
based on the arguments in the errback. The following example shows how
to achieve this by using [`Failure.request.cb_kwargs`{.docutils .literal
.notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    def parse(self, response):
        request = scrapy.Request(
            "http://www.example.com/index.html",
            callback=self.parse_page2,
            errback=self.errback_page2,
            cb_kwargs=dict(main_url=response.url),
        )
        yield request


    def parse_page2(self, response, main_url):
        pass


    def errback_page2(self, failure):
        yield dict(
            main_url=failure.request.cb_kwargs["main_url"],
        )
:::
:::
:::

::: {#request-fingerprints .section}
[]{#id1}

##### Request fingerprints[¶](#request-fingerprints "Permalink to this heading"){.headerlink}

There are some aspects of scraping, such as filtering out duplicate
requests (see [[`DUPEFILTER_CLASS`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DUPEFILTER_CLASS){.hoverxref
.tooltip .reference .internal}) or caching responses (see
[[`HTTPCACHE_POLICY`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_POLICY){.hoverxref
.tooltip .reference .internal}), where you need the ability to generate
a short, unique identifier from a [[`Request`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
.internal} object: a request fingerprint.

You often do not need to worry about request fingerprints, the default
request fingerprinter works for most projects.

However, there is no universal way to generate a unique identifier from
a request, because different situations require comparing requests
differently. For example, sometimes you may need to compare URLs
case-insensitively, include URL fragments, exclude certain URL query
parameters, include some or all headers, etc.

To change how request fingerprints are built for your requests, use the
[[`REQUEST_FINGERPRINTER_CLASS`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-REQUEST_FINGERPRINTER_CLASS){.hoverxref
.tooltip .reference .internal} setting.

::: {#request-fingerprinter-class .section}
[]{#std-setting-REQUEST_FINGERPRINTER_CLASS}

###### REQUEST_FINGERPRINTER_CLASS[¶](#request-fingerprinter-class "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.7.]{.versionmodified .added}
:::

Default: [[`scrapy.utils.request.RequestFingerprinter`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.request.RequestFingerprinter "scrapy.utils.request.RequestFingerprinter"){.reference
.internal}

A [[request fingerprinter class]{.std
.std-ref}](#custom-request-fingerprinter){.hoverxref .tooltip .reference
.internal} or its import path.

*[class]{.pre}[ ]{.w}*[[scrapy.utils.request.]{.pre}]{.sig-prename .descclassname}[[RequestFingerprinter]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[crawler]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Crawler]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference .internal}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/request.html#RequestFingerprinter){.reference .internal}[¶](#scrapy.utils.request.RequestFingerprinter "Permalink to this definition"){.headerlink}

:   Default fingerprinter.

    It takes into account a canonical version
    ([[`w3lib.url.canonicalize_url()`{.xref .py .py-func .docutils
    .literal
    .notranslate}]{.pre}](https://w3lib.readthedocs.io/en/latest/w3lib.html#w3lib.url.canonicalize_url "(in w3lib v2.1)"){.reference
    .external}) of [[`request.url`{.xref .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Request.url "scrapy.http.Request.url"){.reference
    .internal} and the values of [[`request.method`{.xref .py .py-attr
    .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Request.method "scrapy.http.Request.method"){.reference
    .internal} and [[`request.body`{.xref .py .py-attr .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.http.Request.body "scrapy.http.Request.body"){.reference
    .internal}. It then generates an
    [SHA1](https://en.wikipedia.org/wiki/SHA-1){.reference .external}
    hash.

    ::: {.admonition .seealso}
    See also

    [[`REQUEST_FINGERPRINTER_IMPLEMENTATION`{.xref .std .std-setting
    .docutils .literal
    .notranslate}]{.pre}](#std-setting-REQUEST_FINGERPRINTER_IMPLEMENTATION){.hoverxref
    .tooltip .reference .internal}.
    :::
:::

::: {#request-fingerprinter-implementation .section}
[]{#std-setting-REQUEST_FINGERPRINTER_IMPLEMENTATION}

###### REQUEST_FINGERPRINTER_IMPLEMENTATION[¶](#request-fingerprinter-implementation "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.7.]{.versionmodified .added}
:::

Default: [`'2.6'`{.docutils .literal .notranslate}]{.pre}

Determines which request fingerprinting algorithm is used by the default
request fingerprinter class (see [[`REQUEST_FINGERPRINTER_CLASS`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-REQUEST_FINGERPRINTER_CLASS){.hoverxref
.tooltip .reference .internal}).

Possible values are:

-   [`'2.6'`{.docutils .literal .notranslate}]{.pre} (default)

    This implementation uses the same request fingerprinting algorithm
    as Scrapy 2.6 and earlier versions.

    Even though this is the default value for backward compatibility
    reasons, it is a deprecated value.

-   [`'2.7'`{.docutils .literal .notranslate}]{.pre}

    This implementation was introduced in Scrapy 2.7 to fix an issue of
    the previous implementation.

    New projects should use this value. The [[`startproject`{.xref .std
    .std-command .docutils .literal
    .notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
    .tooltip .reference .internal} command sets this value in the
    generated [`settings.py`{.docutils .literal .notranslate}]{.pre}
    file.

If you are using the default value ([`'2.6'`{.docutils .literal
.notranslate}]{.pre}) for this setting, and you are using Scrapy
components where changing the request fingerprinting algorithm would
cause undesired results, you need to carefully decide when to change the
value of this setting, or switch the
[[`REQUEST_FINGERPRINTER_CLASS`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-REQUEST_FINGERPRINTER_CLASS){.hoverxref
.tooltip .reference .internal} setting to a custom request fingerprinter
class that implements the 2.6 request fingerprinting algorithm and does
not log this warning ( [[Writing your own request fingerprinter]{.std
.std-ref}](#request-fingerprinter){.hoverxref .tooltip .reference
.internal} includes an example implementation of such a class).

Scenarios where changing the request fingerprinting algorithm may cause
undesired results include, for example, using the HTTP cache middleware
(see [[`HttpCacheMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware "scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware"){.reference
.internal}). Changing the request fingerprinting algorithm would
invalidate the current cache, requiring you to redownload all requests
again.

Otherwise, set [[`REQUEST_FINGERPRINTER_IMPLEMENTATION`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-REQUEST_FINGERPRINTER_IMPLEMENTATION){.hoverxref
.tooltip .reference .internal} to [`'2.7'`{.docutils .literal
.notranslate}]{.pre} in your settings to switch already to the request
fingerprinting implementation that will be the only request
fingerprinting implementation available in a future version of Scrapy,
and remove the deprecation warning triggered by using the default value
([`'2.6'`{.docutils .literal .notranslate}]{.pre}).
:::

::: {#writing-your-own-request-fingerprinter .section}
[]{#custom-request-fingerprinter}[]{#request-fingerprinter}

###### Writing your own request fingerprinter[¶](#writing-your-own-request-fingerprinter "Permalink to this heading"){.headerlink}

A request fingerprinter is a class that must implement the following
method:

[[fingerprint]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[self]{.pre}]{.n}*, *[[request]{.pre}]{.n}*[)]{.sig-paren}[¶](#fingerprint "Permalink to this definition"){.headerlink}

:   Return a [[`bytes`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
    .external} object that uniquely identifies *request*.

    See also [[Request fingerprint restrictions]{.std
    .std-ref}](#request-fingerprint-restrictions){.hoverxref .tooltip
    .reference .internal}.

    Parameters

    :   **request**
        ([*scrapy.http.Request*](index.html#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal}) -- request to fingerprint

Additionally, it may also implement the following methods:

*[classmethod]{.pre}[ ]{.w}*[[from_crawler]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[cls]{.pre}]{.n}*, *[[crawler]{.pre}]{.n}*[)]{.sig-paren}

:   If present, this class method is called to create a request
    fingerprinter instance from a [[`Crawler`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
    .internal} object. It must return a new instance of the request
    fingerprinter.

    *crawler* provides access to all Scrapy core components like
    settings and signals; it is a way for the request fingerprinter to
    access them and hook its functionality into Scrapy.

    Parameters

    :   **crawler** ([[`Crawler`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.crawler.Crawler "scrapy.crawler.Crawler"){.reference
        .internal} object) -- crawler that uses this request
        fingerprinter

```{=html}
<!-- -->
```

*[classmethod]{.pre}[ ]{.w}*[[from_settings]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[cls]{.pre}]{.n}*, *[[settings]{.pre}]{.n}*[)]{.sig-paren}[¶](#from_settings "Permalink to this definition"){.headerlink}

:   If present, and [`from_crawler`{.docutils .literal
    .notranslate}]{.pre} is not defined, this class method is called to
    create a request fingerprinter instance from a [[`Settings`{.xref
    .py .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
    .internal} object. It must return a new instance of the request
    fingerprinter.

The [[`fingerprint()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](#fingerprint "fingerprint"){.reference .internal}
method of the default request fingerprinter,
[[`scrapy.utils.request.RequestFingerprinter`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.utils.request.RequestFingerprinter "scrapy.utils.request.RequestFingerprinter"){.reference
.internal}, uses [[`scrapy.utils.request.fingerprint()`{.xref .py
.py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.request.fingerprint "scrapy.utils.request.fingerprint"){.reference
.internal} with its default parameters. For some common use cases you
can use [[`scrapy.utils.request.fingerprint()`{.xref .py .py-func
.docutils .literal
.notranslate}]{.pre}](#scrapy.utils.request.fingerprint "scrapy.utils.request.fingerprint"){.reference
.internal} as well in your [[`fingerprint()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](#fingerprint "fingerprint"){.reference .internal}
method implementation:

[[scrapy.utils.request.]{.pre}]{.sig-prename .descclassname}[[fingerprint]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[request]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.n}*, *[[\*]{.pre}]{.o}*, *[[include_headers]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Iterable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Iterable "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[keep_fragments]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/utils/request.html#fingerprint){.reference .internal}[¶](#scrapy.utils.request.fingerprint "Permalink to this definition"){.headerlink}

:   Return the request fingerprint.

    The request fingerprint is a hash that uniquely identifies the
    resource the request points to. For example, take the following two
    urls:

    [http://www.example.com/query?id=111&cat=222](http://www.example.com/query?id=111&cat=222){.reference
    .external}
    [http://www.example.com/query?cat=222&id=111](http://www.example.com/query?cat=222&id=111){.reference
    .external}

    Even though those are two different URLs both point to the same
    resource and are equivalent (i.e. they should return the same
    response).

    Another example are cookies used to store session ids. Suppose the
    following page is only accessible to authenticated users:

    [http://www.example.com/members/offers.html](http://www.example.com/members/offers.html){.reference
    .external}

    Lots of sites use a cookie to store the session id, which adds a
    random component to the HTTP Request and thus should be ignored when
    calculating the fingerprint.

    For this reason, request headers are ignored by default when
    calculating the fingerprint. If you want to include specific headers
    use the include_headers argument, which is a list of Request headers
    to include.

    Also, servers usually ignore fragments in urls when handling
    requests, so they are also ignored by default when calculating the
    fingerprint. If you want to include them, set the keep_fragments
    argument to True (for instance when handling requests with a
    headless browser).

For example, to take the value of a request header named
[`X-ID`{.docutils .literal .notranslate}]{.pre} into account:

::: {.highlight-python .notranslate}
::: highlight
    # my_project/settings.py
    REQUEST_FINGERPRINTER_CLASS = "my_project.utils.RequestFingerprinter"

    # my_project/utils.py
    from scrapy.utils.request import fingerprint


    class RequestFingerprinter:
        def fingerprint(self, request):
            return fingerprint(request, include_headers=["X-ID"])
:::
:::

You can also write your own fingerprinting logic from scratch.

However, if you do not use [[`scrapy.utils.request.fingerprint()`{.xref
.py .py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.request.fingerprint "scrapy.utils.request.fingerprint"){.reference
.internal}, make sure you use [[`WeakKeyDictionary`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/weakref.html#weakref.WeakKeyDictionary "(in Python v3.12)"){.reference
.external} to cache request fingerprints:

-   Caching saves CPU by ensuring that fingerprints are calculated only
    once per request, and not once per Scrapy component that needs the
    fingerprint of a request.

-   Using [[`WeakKeyDictionary`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](https://docs.python.org/3/library/weakref.html#weakref.WeakKeyDictionary "(in Python v3.12)"){.reference
    .external} saves memory by ensuring that request objects do not stay
    in memory forever just because you have references to them in your
    cache dictionary.

For example, to take into account only the URL of a request, without any
prior URL canonicalization or taking the request method or body into
account:

::: {.highlight-python .notranslate}
::: highlight
    from hashlib import sha1
    from weakref import WeakKeyDictionary

    from scrapy.utils.python import to_bytes


    class RequestFingerprinter:
        cache = WeakKeyDictionary()

        def fingerprint(self, request):
            if request not in self.cache:
                fp = sha1()
                fp.update(to_bytes(request.url))
                self.cache[request] = fp.digest()
            return self.cache[request]
:::
:::

If you need to be able to override the request fingerprinting for
arbitrary requests from your spider callbacks, you may implement a
request fingerprinter that reads fingerprints from
[[`request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
.internal} when available, and then falls back to
[[`scrapy.utils.request.fingerprint()`{.xref .py .py-func .docutils
.literal
.notranslate}]{.pre}](#scrapy.utils.request.fingerprint "scrapy.utils.request.fingerprint"){.reference
.internal}. For example:

::: {.highlight-python .notranslate}
::: highlight
    from scrapy.utils.request import fingerprint


    class RequestFingerprinter:
        def fingerprint(self, request):
            if "fingerprint" in request.meta:
                return request.meta["fingerprint"]
            return fingerprint(request)
:::
:::

If you need to reproduce the same fingerprinting algorithm as Scrapy 2.6
without using the deprecated [`'2.6'`{.docutils .literal
.notranslate}]{.pre} value of the
[[`REQUEST_FINGERPRINTER_IMPLEMENTATION`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-REQUEST_FINGERPRINTER_IMPLEMENTATION){.hoverxref
.tooltip .reference .internal} setting, use the following request
fingerprinter:

::: {.highlight-python .notranslate}
::: highlight
    from hashlib import sha1
    from weakref import WeakKeyDictionary

    from scrapy.utils.python import to_bytes
    from w3lib.url import canonicalize_url


    class RequestFingerprinter:
        cache = WeakKeyDictionary()

        def fingerprint(self, request):
            if request not in self.cache:
                fp = sha1()
                fp.update(to_bytes(request.method))
                fp.update(to_bytes(canonicalize_url(request.url)))
                fp.update(request.body or b"")
                self.cache[request] = fp.digest()
            return self.cache[request]
:::
:::
:::

::: {#request-fingerprint-restrictions .section}
[]{#id2}

###### Request fingerprint restrictions[¶](#request-fingerprint-restrictions "Permalink to this heading"){.headerlink}

Scrapy components that use request fingerprints may impose additional
restrictions on the format of the fingerprints that your [[request
fingerprinter]{.std .std-ref}](#custom-request-fingerprinter){.hoverxref
.tooltip .reference .internal} generates.

The following built-in Scrapy components have such restrictions:

-   [[`scrapy.extensions.httpcache.FilesystemCacheStorage`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.extensions.httpcache.FilesystemCacheStorage "scrapy.extensions.httpcache.FilesystemCacheStorage"){.reference
    .internal} (default value of [[`HTTPCACHE_STORAGE`{.xref .std
    .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_STORAGE){.hoverxref
    .tooltip .reference .internal})

    Request fingerprints must be at least 1 byte long.

    Path and filename length limits of the file system of
    [[`HTTPCACHE_DIR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_DIR){.hoverxref
    .tooltip .reference .internal} also apply. Inside
    [[`HTTPCACHE_DIR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_DIR){.hoverxref
    .tooltip .reference .internal}, the following directory structure is
    created:

    -   [`Spider.name`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}

        -   first byte of a request fingerprint as hexadecimal

            -   fingerprint as hexadecimal

                -   filenames up to 16 characters long

    For example, if a request fingerprint is made of 20 bytes (default),
    [[`HTTPCACHE_DIR`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-HTTPCACHE_DIR){.hoverxref
    .tooltip .reference .internal} is
    [`'/home/user/project/.scrapy/httpcache'`{.docutils .literal
    .notranslate}]{.pre}, and the name of your spider is
    [`'my_spider'`{.docutils .literal .notranslate}]{.pre} your file
    system must support a file path like:

    ::: {.highlight-default .notranslate}
    ::: highlight
        /home/user/project/.scrapy/httpcache/my_spider/01/0123456789abcdef0123456789abcdef01234567/response_headers
    :::
    :::

-   [[`scrapy.extensions.httpcache.DbmCacheStorage`{.xref .py .py-class
    .docutils .literal
    .notranslate}]{.pre}](index.html#scrapy.extensions.httpcache.DbmCacheStorage "scrapy.extensions.httpcache.DbmCacheStorage"){.reference
    .internal}

    The underlying DBM implementation must support keys as long as twice
    the number of bytes of a request fingerprint, plus 5. For example,
    if a request fingerprint is made of 20 bytes (default),
    45-character-long keys must be supported.
:::
:::
:::

::: {#request-meta-special-keys .section}
[]{#topics-request-meta}

#### Request.meta special keys[¶](#request-meta-special-keys "Permalink to this heading"){.headerlink}

The [[`Request.meta`{.xref .py .py-attr .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
.internal} attribute can contain any arbitrary data, but there are some
special keys recognized by Scrapy and its built-in extensions.

Those are:

-   [[`bindaddress`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](#std-reqmeta-bindaddress){.hoverxref .tooltip
    .reference .internal}

-   [[`cookiejar`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-cookiejar){.hoverxref
    .tooltip .reference .internal}

-   [[`dont_cache`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-dont_cache){.hoverxref
    .tooltip .reference .internal}

-   [[`dont_merge_cookies`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](#std-reqmeta-dont_merge_cookies){.hoverxref
    .tooltip .reference .internal}

-   [[`dont_obey_robotstxt`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-dont_obey_robotstxt){.hoverxref
    .tooltip .reference .internal}

-   [[`dont_redirect`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-dont_redirect){.hoverxref
    .tooltip .reference .internal}

-   [[`dont_retry`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-dont_retry){.hoverxref
    .tooltip .reference .internal}

-   [[`download_fail_on_dataloss`{.xref .std .std-reqmeta .docutils
    .literal
    .notranslate}]{.pre}](#std-reqmeta-download_fail_on_dataloss){.hoverxref
    .tooltip .reference .internal}

-   [[`download_latency`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](#std-reqmeta-download_latency){.hoverxref
    .tooltip .reference .internal}

-   [[`download_maxsize`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-download_maxsize){.hoverxref
    .tooltip .reference .internal}

-   [[`download_timeout`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](#std-reqmeta-download_timeout){.hoverxref
    .tooltip .reference .internal}

-   [`ftp_password`{.docutils .literal .notranslate}]{.pre} (See
    [[`FTP_PASSWORD`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FTP_PASSWORD){.hoverxref
    .tooltip .reference .internal} for more info)

-   [`ftp_user`{.docutils .literal .notranslate}]{.pre} (See
    [[`FTP_USER`{.xref .std .std-setting .docutils .literal
    .notranslate}]{.pre}](index.html#std-setting-FTP_USER){.hoverxref
    .tooltip .reference .internal} for more info)

-   [[`handle_httpstatus_all`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-handle_httpstatus_all){.hoverxref
    .tooltip .reference .internal}

-   [[`handle_httpstatus_list`{.xref .std .std-reqmeta .docutils
    .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-handle_httpstatus_list){.hoverxref
    .tooltip .reference .internal}

-   [[`max_retry_times`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](#std-reqmeta-max_retry_times){.hoverxref
    .tooltip .reference .internal}

-   [[`proxy`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-proxy){.hoverxref
    .tooltip .reference .internal}

-   [[`redirect_reasons`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-redirect_reasons){.hoverxref
    .tooltip .reference .internal}

-   [[`redirect_urls`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-redirect_urls){.hoverxref
    .tooltip .reference .internal}

-   [[`referrer_policy`{.xref .std .std-reqmeta .docutils .literal
    .notranslate}]{.pre}](index.html#std-reqmeta-referrer_policy){.hoverxref
    .tooltip .reference .internal}

::: {#bindaddress .section}
[]{#std-reqmeta-bindaddress}

##### bindaddress[¶](#bindaddress "Permalink to this heading"){.headerlink}

The IP of the outgoing IP address to use for the performing the request.
:::

::: {#download-timeout .section}
[]{#std-reqmeta-download_timeout}

##### download_timeout[¶](#download-timeout "Permalink to this heading"){.headerlink}

The amount of time (in secs) that the downloader will wait before timing
out. See also: [[`DOWNLOAD_TIMEOUT`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_TIMEOUT){.hoverxref
.tooltip .reference .internal}.
:::

::: {#download-latency .section}
[]{#std-reqmeta-download_latency}

##### download_latency[¶](#download-latency "Permalink to this heading"){.headerlink}

The amount of time spent to fetch the response, since the request has
been started, i.e. HTTP message sent over the network. This meta key
only becomes available when the response has been downloaded. While most
other meta keys are used to control Scrapy behavior, this one is
supposed to be read-only.
:::

::: {#download-fail-on-dataloss .section}
[]{#std-reqmeta-download_fail_on_dataloss}

##### download_fail_on_dataloss[¶](#download-fail-on-dataloss "Permalink to this heading"){.headerlink}

Whether or not to fail on broken responses. See:
[[`DOWNLOAD_FAIL_ON_DATALOSS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-DOWNLOAD_FAIL_ON_DATALOSS){.hoverxref
.tooltip .reference .internal}.
:::

::: {#max-retry-times .section}
[]{#std-reqmeta-max_retry_times}

##### max_retry_times[¶](#max-retry-times "Permalink to this heading"){.headerlink}

The meta key is used set retry times per request. When initialized, the
[[`max_retry_times`{.xref .std .std-reqmeta .docutils .literal
.notranslate}]{.pre}](#std-reqmeta-max_retry_times){.hoverxref .tooltip
.reference .internal} meta key takes higher precedence over the
[[`RETRY_TIMES`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-RETRY_TIMES){.hoverxref
.tooltip .reference .internal} setting.
:::
:::

::: {#stopping-the-download-of-a-response .section}
[]{#topics-stop-response-download}

#### Stopping the download of a Response[¶](#stopping-the-download-of-a-response "Permalink to this heading"){.headerlink}

Raising a [[`StopDownload`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.StopDownload "scrapy.exceptions.StopDownload"){.reference
.internal} exception from a handler for the [[`bytes_received`{.xref .py
.py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.signals.bytes_received "scrapy.signals.bytes_received"){.reference
.internal} or [[`headers_received`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.signals.headers_received "scrapy.signals.headers_received"){.reference
.internal} signals will stop the download of a given response. See the
following example:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class StopSpider(scrapy.Spider):
        name = "stop"
        start_urls = ["https://docs.scrapy.org/en/latest/"]

        @classmethod
        def from_crawler(cls, crawler):
            spider = super().from_crawler(crawler)
            crawler.signals.connect(
                spider.on_bytes_received, signal=scrapy.signals.bytes_received
            )
            return spider

        def parse(self, response):
            # 'last_chars' show that the full response was not downloaded
            yield {"len": len(response.text), "last_chars": response.text[-40:]}

        def on_bytes_received(self, data, request, spider):
            raise scrapy.exceptions.StopDownload(fail=False)
:::
:::

which produces the following output:

::: {.highlight-default .notranslate}
::: highlight
    2020-05-19 17:26:12 [scrapy.core.engine] INFO: Spider opened
    2020-05-19 17:26:12 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min)
    2020-05-19 17:26:13 [scrapy.core.downloader.handlers.http11] DEBUG: Download stopped for <GET https://docs.scrapy.org/en/latest/> from signal handler StopSpider.on_bytes_received
    2020-05-19 17:26:13 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://docs.scrapy.org/en/latest/> (referer: None) ['download_stopped']
    2020-05-19 17:26:13 [scrapy.core.scraper] DEBUG: Scraped from <200 https://docs.scrapy.org/en/latest/>
    {'len': 279, 'last_chars': 'dth, initial-scale=1.0">\n  \n  <title>Scr'}
    2020-05-19 17:26:13 [scrapy.core.engine] INFO: Closing spider (finished)
:::
:::

By default, resulting responses are handled by their corresponding
errbacks. To call their callback instead, like in this example, pass
[`fail=False`{.docutils .literal .notranslate}]{.pre} to the
[[`StopDownload`{.xref .py .py-exc .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.exceptions.StopDownload "scrapy.exceptions.StopDownload"){.reference
.internal} exception.
:::

::: {#request-subclasses .section}
[]{#topics-request-response-ref-request-subclasses}

#### Request subclasses[¶](#request-subclasses "Permalink to this heading"){.headerlink}

Here is the list of built-in [[`Request`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
.internal} subclasses. You can also subclass it to implement your own
custom functionality.

::: {#formrequest-objects .section}
##### FormRequest objects[¶](#formrequest-objects "Permalink to this heading"){.headerlink}

The FormRequest class extends the base [[`Request`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
.internal} with functionality for dealing with HTML forms. It uses
[lxml.html forms](https://lxml.de/lxmlhtml.html#forms){.reference
.external} to pre-populate form fields with form data from
[[`Response`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} objects.

*[class]{.pre}[ ]{.w}*[[scrapy.http.request.form.]{.pre}]{.sig-prename .descclassname}[[FormRequest]{.pre}]{.sig-name .descname}[¶](#scrapy.http.scrapy.http.request.form.FormRequest "Permalink to this definition"){.headerlink}

:   

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.http.]{.pre}]{.sig-prename .descclassname}[[FormRequest]{.pre}]{.sig-name .descname}[¶](#scrapy.http.scrapy.http.FormRequest "Permalink to this definition"){.headerlink}

:   

```{=html}
<!-- -->
```

*[class]{.pre}[ ]{.w}*[[scrapy.]{.pre}]{.sig-prename .descclassname}[[FormRequest]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}*[\[]{.optional}, *[[formdata]{.pre}]{.n}*, *[[\...]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[¶](#scrapy.http.scrapy.FormRequest "Permalink to this definition"){.headerlink}

:   The [`FormRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} class adds a new keyword parameter to the
    [`__init__`{.docutils .literal .notranslate}]{.pre} method. The
    remaining arguments are the same as for the [[`Request`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} class and are not documented here.

    Parameters

    :   **formdata**
        ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
        .external} *or*
        [*collections.abc.Iterable*](https://docs.python.org/3/library/collections.abc.html#collections.abc.Iterable "(in Python v3.12)"){.reference
        .external}) -- is a dictionary (or iterable of (key, value)
        tuples) containing HTML Form data which will be url-encoded and
        assigned to the body of the request.

    The [`FormRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre} objects support the following class method in
    addition to the standard [[`Request`{.xref .py .py-class .docutils
    .literal
    .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} methods:

    *[classmethod]{.pre}[ ]{.w}*[[FormRequest.]{.pre}]{.sig-prename .descclassname}[[from_response]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*[\[]{.optional}, *[[formname=None]{.pre}]{.n}*, *[[formid=None]{.pre}]{.n}*, *[[formnumber=0]{.pre}]{.n}*, *[[formdata=None]{.pre}]{.n}*, *[[formxpath=None]{.pre}]{.n}*, *[[formcss=None]{.pre}]{.n}*, *[[clickdata=None]{.pre}]{.n}*, *[[dont_click=False]{.pre}]{.n}*, *[[\...]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[¶](#scrapy.http.scrapy.FormRequest.FormRequest.from_response "Permalink to this definition"){.headerlink}

    :   Returns a new [`FormRequest`{.xref .py .py-class .docutils
        .literal .notranslate}]{.pre} object with its form field values
        pre-populated with those found in the HTML [`<form>`{.docutils
        .literal .notranslate}]{.pre} element contained in the given
        response. For an example see [[Using FormRequest.from_response()
        to simulate a user login]{.std
        .std-ref}](#topics-request-response-ref-request-userlogin){.hoverxref
        .tooltip .reference .internal}.

        The policy is to automatically simulate a click, by default, on
        any form control that looks clickable, like a
        [`<input`{.docutils .literal .notranslate}]{.pre}` `{.docutils
        .literal .notranslate}[`type="submit">`{.docutils .literal
        .notranslate}]{.pre}. Even though this is quite convenient, and
        often the desired behaviour, sometimes it can cause problems
        which could be hard to debug. For example, when working with
        forms that are filled and/or submitted using javascript, the
        default [`from_response()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre} behaviour may not be the most appropriate.
        To disable this behaviour you can set the
        [`dont_click`{.docutils .literal .notranslate}]{.pre} argument
        to [`True`{.docutils .literal .notranslate}]{.pre}. Also, if you
        want to change the control clicked (instead of disabling it) you
        can also use the [`clickdata`{.docutils .literal
        .notranslate}]{.pre} argument.

        ::: {.admonition .caution}
        Caution

        Using this method with select elements which have leading or
        trailing whitespace in the option values will not work due to a
        [bug in
        lxml](https://bugs.launchpad.net/lxml/+bug/1665241){.reference
        .external}, which should be fixed in lxml 3.8 and above.
        :::

        Parameters

        :   -   **response** ([[`Response`{.xref .py .py-class .docutils
                .literal
                .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
                .internal} object) -- the response containing a HTML
                form which will be used to pre-populate the form fields

            -   **formname**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- if given, the form with name attribute
                set to this value will be used.

            -   **formid**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- if given, the form with id attribute set
                to this value will be used.

            -   **formxpath**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- if given, the first form that matches the
                xpath will be used.

            -   **formcss**
                ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
                .external}) -- if given, the first form that matches the
                css selector will be used.

            -   **formnumber**
                ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
                .external}) -- the number of form to use, when the
                response contains multiple forms. The first one (and
                also the default) is [`0`{.docutils .literal
                .notranslate}]{.pre}.

            -   **formdata**
                ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
                .external}) -- fields to override in the form data. If a
                field was already present in the response
                [`<form>`{.docutils .literal .notranslate}]{.pre}
                element, its value is overridden by the one passed in
                this parameter. If a value passed in this parameter is
                [`None`{.docutils .literal .notranslate}]{.pre}, the
                field will not be included in the request, even if it
                was present in the response [`<form>`{.docutils .literal
                .notranslate}]{.pre} element.

            -   **clickdata**
                ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
                .external}) -- attributes to lookup the control clicked.
                If it's not given, the form data will be submitted
                simulating a click on the first clickable element. In
                addition to html attributes, the control can be
                identified by its zero-based index relative to other
                submittable inputs inside the form, via the
                [`nr`{.docutils .literal .notranslate}]{.pre} attribute.

            -   **dont_click**
                ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
                .external}) -- If True, the form data will be submitted
                without clicking in any element.

        The other parameters of this class method are passed directly to
        the [`FormRequest`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre} [`__init__`{.docutils .literal
        .notranslate}]{.pre} method.
:::

::: {#request-usage-examples .section}
##### Request usage examples[¶](#request-usage-examples "Permalink to this heading"){.headerlink}

::: {#using-formrequest-to-send-data-via-http-post .section}
###### Using FormRequest to send data via HTTP POST[¶](#using-formrequest-to-send-data-via-http-post "Permalink to this heading"){.headerlink}

If you want to simulate a HTML Form POST in your spider and send a
couple of key-value fields, you can return a [`FormRequest`{.xref .py
.py-class .docutils .literal .notranslate}]{.pre} object (from your
spider) like this:

::: {.highlight-python .notranslate}
::: highlight
    return [
        FormRequest(
            url="http://www.example.com/post/action",
            formdata={"name": "John Doe", "age": "27"},
            callback=self.after_post,
        )
    ]
:::
:::
:::

::: {#using-formrequest-from-response-to-simulate-a-user-login .section}
[]{#topics-request-response-ref-request-userlogin}

###### Using FormRequest.from_response() to simulate a user login[¶](#using-formrequest-from-response-to-simulate-a-user-login "Permalink to this heading"){.headerlink}

It is usual for web sites to provide pre-populated form fields through
[`<input`{.docutils .literal .notranslate}]{.pre}` `{.docutils .literal
.notranslate}[`type="hidden">`{.docutils .literal .notranslate}]{.pre}
elements, such as session related data or authentication tokens (for
login pages). When scraping, you'll want these fields to be
automatically pre-populated and only override a couple of them, such as
the user name and password. You can use the
[`FormRequest.from_response()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre} method for this job. Here's an example spider which
uses it:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    def authentication_failed(response):
        # TODO: Check the contents of the response and return True if it failed
        # or False if it succeeded.
        pass


    class LoginSpider(scrapy.Spider):
        name = "example.com"
        start_urls = ["http://www.example.com/users/login.php"]

        def parse(self, response):
            return scrapy.FormRequest.from_response(
                response,
                formdata={"username": "john", "password": "secret"},
                callback=self.after_login,
            )

        def after_login(self, response):
            if authentication_failed(response):
                self.logger.error("Login failed")
                return

            # continue scraping with authenticated session...
:::
:::
:::
:::

::: {#jsonrequest .section}
##### JsonRequest[¶](#jsonrequest "Permalink to this heading"){.headerlink}

The JsonRequest class extends the base [[`Request`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
.internal} class with functionality for dealing with JSON requests.

*[class]{.pre}[ ]{.w}*[[scrapy.http.]{.pre}]{.sig-prename .descclassname}[[JsonRequest]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}*[\[]{.optional}, *[[\...]{.pre} [data]{.pre}]{.n}*, *[[dumps_kwargs]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/request/json_request.html#JsonRequest){.reference .internal}[¶](#scrapy.http.JsonRequest "Permalink to this definition"){.headerlink}

:   The [[`JsonRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.JsonRequest "scrapy.http.JsonRequest"){.reference
    .internal} class adds two new keyword parameters to the
    [`__init__`{.docutils .literal .notranslate}]{.pre} method. The
    remaining arguments are the same as for the [[`Request`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
    .internal} class and are not documented here.

    Using the [[`JsonRequest`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.JsonRequest "scrapy.http.JsonRequest"){.reference
    .internal} will set the [`Content-Type`{.docutils .literal
    .notranslate}]{.pre} header to [`application/json`{.docutils
    .literal .notranslate}]{.pre} and [`Accept`{.docutils .literal
    .notranslate}]{.pre} header to [`application/json,`{.docutils
    .literal .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`text/javascript,`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`*/*;`{.docutils .literal
    .notranslate}]{.pre}` `{.docutils .literal
    .notranslate}[`q=0.01`{.docutils .literal .notranslate}]{.pre}

    Parameters

    :   -   **data**
            ([*object*](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)"){.reference
            .external}) -- is any JSON serializable object that needs to
            be JSON encoded and assigned to body. if
            [[`Request.body`{.xref .py .py-attr .docutils .literal
            .notranslate}]{.pre}](#scrapy.http.Request.body "scrapy.http.Request.body"){.reference
            .internal} argument is provided this parameter will be
            ignored. if [[`Request.body`{.xref .py .py-attr .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.http.Request.body "scrapy.http.Request.body"){.reference
            .internal} argument is not provided and data argument is
            provided [[`Request.method`{.xref .py .py-attr .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.http.Request.method "scrapy.http.Request.method"){.reference
            .internal} will be set to [`'POST'`{.docutils .literal
            .notranslate}]{.pre} automatically.

        -   **dumps_kwargs**
            ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external}) -- Parameters that will be passed to underlying
            [[`json.dumps()`{.xref .py .py-func .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/json.html#json.dumps "(in Python v3.12)"){.reference
            .external} method which is used to serialize data into JSON
            format.

    [[attributes]{.pre}]{.sig-name .descname}*[[:]{.pre}]{.p}[ ]{.w}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[\...]{.pre}]{.p}[[\]]{.pre}]{.p}[ ]{.w}[[=]{.pre}]{.p}[ ]{.w}[(\'url\',]{.pre} [\'callback\',]{.pre} [\'method\',]{.pre} [\'headers\',]{.pre} [\'body\',]{.pre} [\'cookies\',]{.pre} [\'meta\',]{.pre} [\'encoding\',]{.pre} [\'priority\',]{.pre} [\'dont_filter\',]{.pre} [\'errback\',]{.pre} [\'flags\',]{.pre} [\'cb_kwargs\',]{.pre} [\'dumps_kwargs\')]{.pre}*[¶](#scrapy.http.JsonRequest.attributes "Permalink to this definition"){.headerlink}

    :   A tuple of [[`str`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
        .external} objects containing the name of all public attributes
        of the class that are also keyword parameters of the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method.

        Currently used by [[`Request.replace()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.replace "scrapy.http.Request.replace"){.reference
        .internal}, [[`Request.to_dict()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Request.to_dict "scrapy.http.Request.to_dict"){.reference
        .internal} and [[`request_from_dict()`{.xref .py .py-func
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.utils.request.request_from_dict "scrapy.utils.request.request_from_dict"){.reference
        .internal}.
:::

::: {#jsonrequest-usage-example .section}
##### JsonRequest usage example[¶](#jsonrequest-usage-example "Permalink to this heading"){.headerlink}

Sending a JSON POST request with a JSON payload:

::: {.highlight-python .notranslate}
::: highlight
    data = {
        "name1": "value1",
        "name2": "value2",
    }
    yield JsonRequest(url="http://www.example.com/post/action", data=data)
:::
:::
:::
:::

::: {#response-objects .section}
#### Response objects[¶](#response-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.http.]{.pre}]{.sig-prename .descclassname}[[Response]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[\*]{.pre}]{.o}[[args]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*, *[[\*\*]{.pre}]{.o}[[kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response.html#Response){.reference .internal}[¶](#scrapy.http.Response "Permalink to this definition"){.headerlink}

:   An object that represents an HTTP response, which is usually
    downloaded (by the Downloader) and fed to the Spiders for
    processing.

    Parameters

    :   -   **url**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- the URL of this response

        -   **status**
            ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference
            .external}) -- the HTTP status of the response. Defaults to
            [`200`{.docutils .literal .notranslate}]{.pre}.

        -   **headers**
            ([*dict*](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference
            .external}) -- the headers of this response. The dict values
            can be strings (for single valued headers) or lists (for
            multi-valued headers).

        -   **body**
            ([*bytes*](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference
            .external}) -- the response body. To access the decoded text
            as a string, use [`response.text`{.docutils .literal
            .notranslate}]{.pre} from an encoding-aware [[Response
            subclass]{.std
            .std-ref}](#topics-request-response-ref-response-subclasses){.hoverxref
            .tooltip .reference .internal}, such as
            [[`TextResponse`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
            .internal}.

        -   **flags**
            ([*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- is a list containing the initial values for
            the [[`Response.flags`{.xref .py .py-attr .docutils .literal
            .notranslate}]{.pre}](#scrapy.http.Response.flags "scrapy.http.Response.flags"){.reference
            .internal} attribute. If given, the list will be shallow
            copied.

        -   **request** (*scrapy.Request*) -- the initial value of the
            [[`Response.request`{.xref .py .py-attr .docutils .literal
            .notranslate}]{.pre}](#scrapy.http.Response.request "scrapy.http.Response.request"){.reference
            .internal} attribute. This represents the [[`Request`{.xref
            .py .py-class .docutils .literal
            .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
            .internal} that generated this response.

        -   **certificate**
            ([*twisted.internet.ssl.Certificate*](https://docs.twisted.org/en/stable/api/twisted.internet.ssl.Certificate.html "(in Twisted)"){.reference
            .external}) -- an object representing the server's SSL
            certificate.

        -   **ip_address** ([[`ipaddress.IPv4Address`{.xref .py
            .py-class .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/ipaddress.html#ipaddress.IPv4Address "(in Python v3.12)"){.reference
            .external} or [[`ipaddress.IPv6Address`{.xref .py .py-class
            .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/ipaddress.html#ipaddress.IPv6Address "(in Python v3.12)"){.reference
            .external}) -- The IP address of the server from which the
            Response originated.

        -   **protocol** ([[`str`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external}) -- The protocol that was used to download the
            response. For instance: "HTTP/1.0", "HTTP/1.1", "h2"

    ::: versionadded
    [New in version 2.0.0: ]{.versionmodified .added}The
    [`certificate`{.docutils .literal .notranslate}]{.pre} parameter.
    :::

    ::: versionadded
    [New in version 2.1.0: ]{.versionmodified .added}The
    [`ip_address`{.docutils .literal .notranslate}]{.pre} parameter.
    :::

    ::: versionadded
    [New in version 2.5.0: ]{.versionmodified .added}The
    [`protocol`{.docutils .literal .notranslate}]{.pre} parameter.
    :::

    [[url]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.url "Permalink to this definition"){.headerlink}

    :   A string containing the URL of the response.

        This attribute is read-only. To change the URL of a Response use
        [[`replace()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.replace "scrapy.http.Response.replace"){.reference
        .internal}.

    [[status]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.status "Permalink to this definition"){.headerlink}

    :   An integer representing the HTTP status of the response.
        Example: [`200`{.docutils .literal .notranslate}]{.pre},
        [`404`{.docutils .literal .notranslate}]{.pre}.

    [[headers]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.headers "Permalink to this definition"){.headerlink}

    :   A dictionary-like object which contains the response headers.
        Values can be accessed using [`get()`{.xref .py .py-meth
        .docutils .literal .notranslate}]{.pre} to return the first
        header value with the specified name or [`getlist()`{.xref .py
        .py-meth .docutils .literal .notranslate}]{.pre} to return all
        header values with the specified name. For example, this call
        will give you all cookies in the headers:

        ::: {.highlight-default .notranslate}
        ::: highlight
            response.headers.getlist('Set-Cookie')
        :::
        :::

    [[body]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.body "Permalink to this definition"){.headerlink}

    :   The response body as bytes.

        If you want the body as a string, use
        [[`TextResponse.text`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.TextResponse.text "scrapy.http.TextResponse.text"){.reference
        .internal} (only available in [[`TextResponse`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
        .internal} and subclasses).

        This attribute is read-only. To change the body of a Response
        use [[`replace()`{.xref .py .py-meth .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.replace "scrapy.http.Response.replace"){.reference
        .internal}.

    [[request]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.request "Permalink to this definition"){.headerlink}

    :   The [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} object that generated this response. This attribute
        is assigned in the Scrapy engine, after the response and the
        request have passed through all [[Downloader Middlewares]{.std
        .std-ref}](index.html#topics-downloader-middleware){.hoverxref
        .tooltip .reference .internal}. In particular, this means that:

        -   HTTP redirections will create a new request from the request
            before redirection. It has the majority of the same metadata
            and original request attributes and gets assigned to the
            redirected response instead of the propagation of the
            original request.

        -   Response.request.url doesn't always equal Response.url

        -   This attribute is only available in the spider code, and in
            the [[Spider Middlewares]{.std
            .std-ref}](index.html#topics-spider-middleware){.hoverxref
            .tooltip .reference .internal}, but not in Downloader
            Middlewares (although you have the Request available there
            by other means) and handlers of the
            [[`response_downloaded`{.xref .std .std-signal .docutils
            .literal
            .notranslate}]{.pre}](index.html#std-signal-response_downloaded){.hoverxref
            .tooltip .reference .internal} signal.

    [[meta]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.meta "Permalink to this definition"){.headerlink}

    :   A shortcut to the [[`Request.meta`{.xref .py .py-attr .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
        .internal} attribute of the [[`Response.request`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.request "scrapy.http.Response.request"){.reference
        .internal} object (i.e. [`self.request.meta`{.docutils .literal
        .notranslate}]{.pre}).

        Unlike the [[`Response.request`{.xref .py .py-attr .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Response.request "scrapy.http.Response.request"){.reference
        .internal} attribute, the [[`Response.meta`{.xref .py .py-attr
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.meta "scrapy.http.Response.meta"){.reference
        .internal} attribute is propagated along redirects and retries,
        so you will get the original [[`Request.meta`{.xref .py .py-attr
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
        .internal} sent from your spider.

        ::: {.admonition .seealso}
        See also

        [[`Request.meta`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.meta "scrapy.http.Request.meta"){.reference
        .internal} attribute
        :::

    [[cb_kwargs]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.cb_kwargs "Permalink to this definition"){.headerlink}

    :   ::: versionadded
        [New in version 2.0.]{.versionmodified .added}
        :::

        A shortcut to the [[`Request.cb_kwargs`{.xref .py .py-attr
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
        .internal} attribute of the [[`Response.request`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.request "scrapy.http.Response.request"){.reference
        .internal} object (i.e. [`self.request.cb_kwargs`{.docutils
        .literal .notranslate}]{.pre}).

        Unlike the [[`Response.request`{.xref .py .py-attr .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Response.request "scrapy.http.Response.request"){.reference
        .internal} attribute, the [[`Response.cb_kwargs`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.cb_kwargs "scrapy.http.Response.cb_kwargs"){.reference
        .internal} attribute is propagated along redirects and retries,
        so you will get the original [[`Request.cb_kwargs`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
        .internal} sent from your spider.

        ::: {.admonition .seealso}
        See also

        [[`Request.cb_kwargs`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request.cb_kwargs "scrapy.http.Request.cb_kwargs"){.reference
        .internal} attribute
        :::

    [[flags]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.flags "Permalink to this definition"){.headerlink}

    :   A list that contains flags for this response. Flags are labels
        used for tagging Responses. For example: [`'cached'`{.docutils
        .literal .notranslate}]{.pre}, [`'redirected`{.docutils .literal
        .notranslate}]{.pre}', etc. And they're shown on the string
        representation of the Response (\_\_str\_\_ method) which is
        used by the engine for logging.

    [[certificate]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.certificate "Permalink to this definition"){.headerlink}

    :   ::: versionadded
        [New in version 2.0.0.]{.versionmodified .added}
        :::

        A [[`twisted.internet.ssl.Certificate`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](https://docs.twisted.org/en/stable/api/twisted.internet.ssl.Certificate.html "(in Twisted)"){.reference
        .external} object representing the server's SSL certificate.

        Only populated for [`https`{.docutils .literal
        .notranslate}]{.pre} responses, [`None`{.docutils .literal
        .notranslate}]{.pre} otherwise.

    [[ip_address]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.ip_address "Permalink to this definition"){.headerlink}

    :   ::: versionadded
        [New in version 2.1.0.]{.versionmodified .added}
        :::

        The IP address of the server from which the Response originated.

        This attribute is currently only populated by the HTTP 1.1
        download handler, i.e. for [`http(s)`{.docutils .literal
        .notranslate}]{.pre} responses. For other handlers,
        [[`ip_address`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.ip_address "scrapy.http.Response.ip_address"){.reference
        .internal} is always [`None`{.docutils .literal
        .notranslate}]{.pre}.

    [[protocol]{.pre}]{.sig-name .descname}[¶](#scrapy.http.Response.protocol "Permalink to this definition"){.headerlink}

    :   ::: versionadded
        [New in version 2.5.0.]{.versionmodified .added}
        :::

        The protocol that was used to download the response. For
        instance: "HTTP/1.0", "HTTP/1.1"

        This attribute is currently only populated by the HTTP download
        handlers, i.e. for [`http(s)`{.docutils .literal
        .notranslate}]{.pre} responses. For other handlers,
        [[`protocol`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.protocol "scrapy.http.Response.protocol"){.reference
        .internal} is always [`None`{.docutils .literal
        .notranslate}]{.pre}.

    [[attributes]{.pre}]{.sig-name .descname}*[[:]{.pre}]{.p}[ ]{.w}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[\...]{.pre}]{.p}[[\]]{.pre}]{.p}[ ]{.w}[[=]{.pre}]{.p}[ ]{.w}[(\'url\',]{.pre} [\'status\',]{.pre} [\'headers\',]{.pre} [\'body\',]{.pre} [\'flags\',]{.pre} [\'request\',]{.pre} [\'certificate\',]{.pre} [\'ip_address\',]{.pre} [\'protocol\')]{.pre}*[¶](#scrapy.http.Response.attributes "Permalink to this definition"){.headerlink}

    :   A tuple of [[`str`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
        .external} objects containing the name of all public attributes
        of the class that are also keyword parameters of the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method.

        Currently used by [[`Response.replace()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.replace "scrapy.http.Response.replace"){.reference
        .internal}.

    [[copy]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response.html#Response.copy){.reference .internal}[¶](#scrapy.http.Response.copy "Permalink to this definition"){.headerlink}

    :   Returns a new Response which is a copy of this Response.

    [[replace]{.pre}]{.sig-name .descname}[(]{.sig-paren}[\[]{.optional}*[[url]{.pre}]{.n}*, *[[status]{.pre}]{.n}*, *[[headers]{.pre}]{.n}*, *[[body]{.pre}]{.n}*, *[[request]{.pre}]{.n}*, *[[flags]{.pre}]{.n}*, *[[cls]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response.html#Response.replace){.reference .internal}[¶](#scrapy.http.Response.replace "Permalink to this definition"){.headerlink}

    :   Returns a Response object with the same members, except for
        those members given new values by whichever keyword arguments
        are specified. The attribute [[`Response.meta`{.xref .py
        .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.meta "scrapy.http.Response.meta"){.reference
        .internal} is copied by default.

    [[urljoin]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response.html#Response.urljoin){.reference .internal}[¶](#scrapy.http.Response.urljoin "Permalink to this definition"){.headerlink}

    :   Constructs an absolute url by combining the Response's
        [[`url`{.xref .py .py-attr .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.url "scrapy.http.Response.url"){.reference
        .internal} with a possible relative url.

        This is a wrapper over [[`urljoin()`{.xref .py .py-func
        .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/urllib.parse.html#urllib.parse.urljoin "(in Python v3.12)"){.reference
        .external}, it's merely an alias for making this call:

        ::: {.highlight-default .notranslate}
        ::: highlight
            urllib.parse.urljoin(response.url, url)
        :::
        :::

    [[follow]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Link]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference .internal}[[\]]{.pre}]{.p}]{.n}*, *[[callback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[method]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'GET\']{.pre}]{.default_value}*, *[[headers]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Mapping]{.pre}](https://docs.python.org/3/library/typing.html#typing.Mapping "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Iterable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Iterable "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[body]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cookies]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[meta]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[encoding]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'utf-8\']{.pre}]{.default_value}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[0]{.pre}]{.default_value}*, *[[dont_filter]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*, *[[errback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cb_kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[flags]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response.html#Response.follow){.reference .internal}[¶](#scrapy.http.Response.follow "Permalink to this definition"){.headerlink}

    :   Return a [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} instance to follow a link [`url`{.docutils .literal
        .notranslate}]{.pre}. It accepts the same arguments as
        [`Request.__init__`{.docutils .literal .notranslate}]{.pre}
        method, but [`url`{.docutils .literal .notranslate}]{.pre} can
        be a relative URL or a [`scrapy.link.Link`{.docutils .literal
        .notranslate}]{.pre} object, not only an absolute URL.

        [[`TextResponse`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
        .internal} provides a [[`follow()`{.xref .py .py-meth .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.TextResponse.follow "scrapy.http.TextResponse.follow"){.reference
        .internal} method which supports selectors in addition to
        absolute/relative URLs and Link objects.

        ::: versionadded
        [New in version 2.0: ]{.versionmodified .added}The *flags*
        parameter.
        :::

    [[follow_all]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[urls]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Iterable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Iterable "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Link]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference .internal}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}*, *[[callback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[method]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'GET\']{.pre}]{.default_value}*, *[[headers]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Mapping]{.pre}](https://docs.python.org/3/library/typing.html#typing.Mapping "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Iterable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Iterable "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[body]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cookies]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[meta]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[encoding]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'utf-8\']{.pre}]{.default_value}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[0]{.pre}]{.default_value}*, *[[dont_filter]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*, *[[errback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cb_kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[flags]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Generator]{.pre}](https://docs.python.org/3/library/typing.html#typing.Generator "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}[[,]{.pre}]{.p}[ ]{.w}[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response.html#Response.follow_all){.reference .internal}[¶](#scrapy.http.Response.follow_all "Permalink to this definition"){.headerlink}

    :   ::: versionadded
        [New in version 2.0.]{.versionmodified .added}
        :::

        Return an iterable of [[`Request`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} instances to follow all links in [`urls`{.docutils
        .literal .notranslate}]{.pre}. It accepts the same arguments as
        [`Request.__init__`{.docutils .literal .notranslate}]{.pre}
        method, but elements of [`urls`{.docutils .literal
        .notranslate}]{.pre} can be relative URLs or [[`Link`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference
        .internal} objects, not only absolute URLs.

        [[`TextResponse`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
        .internal} provides a [[`follow_all()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.TextResponse.follow_all "scrapy.http.TextResponse.follow_all"){.reference
        .internal} method which supports selectors in addition to
        absolute/relative URLs and Link objects.
:::

::: {#response-subclasses .section}
[]{#topics-request-response-ref-response-subclasses}

#### Response subclasses[¶](#response-subclasses "Permalink to this heading"){.headerlink}

Here is the list of available built-in Response subclasses. You can also
subclass the Response class to implement your own functionality.

::: {#textresponse-objects .section}
##### TextResponse objects[¶](#textresponse-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.http.]{.pre}]{.sig-prename .descclassname}[[TextResponse]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}*[\[]{.optional}, *[[encoding]{.pre}]{.n}*[\[]{.optional}, *[[\...]{.pre}]{.n}*[\]]{.optional}[\]]{.optional}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse){.reference .internal}[¶](#scrapy.http.TextResponse "Permalink to this definition"){.headerlink}

:   [[`TextResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} objects adds encoding capabilities to the base
    [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} class, which is meant to be used only for binary data,
    such as images, sounds or any media file.

    [[`TextResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} objects support a new [`__init__`{.docutils .literal
    .notranslate}]{.pre} method argument, in addition to the base
    [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} objects. The remaining functionality is the same as for
    the [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} class and is not documented here.

    Parameters

    :   **encoding**
        ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
        .external}) -- is a string which contains the encoding to use
        for this response. If you create a [[`TextResponse`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
        .internal} object with a string as body, it will be converted to
        bytes encoded using this encoding. If *encoding* is
        [`None`{.docutils .literal .notranslate}]{.pre} (default), the
        encoding will be looked up in the response headers and body
        instead.

    [[`TextResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} objects support the following attributes in addition to
    the standard [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} ones:

    [[text]{.pre}]{.sig-name .descname}[¶](#scrapy.http.TextResponse.text "Permalink to this definition"){.headerlink}

    :   Response body, as a string.

        The same as [`response.body.decode(response.encoding)`{.docutils
        .literal .notranslate}]{.pre}, but the result is cached after
        the first call, so you can access [`response.text`{.docutils
        .literal .notranslate}]{.pre} multiple times without extra
        overhead.

        ::: {.admonition .note}
        Note

        [`str(response.body)`{.docutils .literal .notranslate}]{.pre} is
        not a correct way to convert the response body into a string:

        ::: {.highlight-pycon .notranslate}
        ::: highlight
            >>> str(b"body")
            "b'body'"
        :::
        :::
        :::

    [[encoding]{.pre}]{.sig-name .descname}[¶](#scrapy.http.TextResponse.encoding "Permalink to this definition"){.headerlink}

    :   A string with the encoding of this response. The encoding is
        resolved by trying the following mechanisms, in order:

        1.  the encoding passed in the [`__init__`{.docutils .literal
            .notranslate}]{.pre} method [`encoding`{.docutils .literal
            .notranslate}]{.pre} argument

        2.  the encoding declared in the Content-Type HTTP header. If
            this encoding is not valid (i.e. unknown), it is ignored and
            the next resolution mechanism is tried.

        3.  the encoding declared in the response body. The TextResponse
            class doesn't provide any special functionality for this.
            However, the [[`HtmlResponse`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.http.HtmlResponse "scrapy.http.HtmlResponse"){.reference
            .internal} and [[`XmlResponse`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](#scrapy.http.XmlResponse "scrapy.http.XmlResponse"){.reference
            .internal} classes do.

        4.  the encoding inferred by looking at the response body. This
            is the more fragile method but also the last one tried.

    [[selector]{.pre}]{.sig-name .descname}[¶](#scrapy.http.TextResponse.selector "Permalink to this definition"){.headerlink}

    :   A [`Selector`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre} instance using the response as target. The
        selector is lazily instantiated on first access.

    [[attributes]{.pre}]{.sig-name .descname}*[[:]{.pre}]{.p}[ ]{.w}[Tuple]{.pre}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[\...]{.pre}]{.p}[[\]]{.pre}]{.p}[ ]{.w}[[=]{.pre}]{.p}[ ]{.w}[(\'url\',]{.pre} [\'status\',]{.pre} [\'headers\',]{.pre} [\'body\',]{.pre} [\'flags\',]{.pre} [\'request\',]{.pre} [\'certificate\',]{.pre} [\'ip_address\',]{.pre} [\'protocol\',]{.pre} [\'encoding\')]{.pre}*[¶](#scrapy.http.TextResponse.attributes "Permalink to this definition"){.headerlink}

    :   A tuple of [[`str`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
        .external} objects containing the name of all public attributes
        of the class that are also keyword parameters of the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method.

        Currently used by [[`Response.replace()`{.xref .py .py-meth
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Response.replace "scrapy.http.Response.replace"){.reference
        .internal}.

    [[`TextResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} objects support the following methods in addition to the
    standard [[`Response`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.Response "scrapy.http.Response"){.reference
    .internal} ones:

    [[jmespath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[query]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse.jmespath){.reference .internal}[¶](#scrapy.http.TextResponse.jmespath "Permalink to this definition"){.headerlink}

    :   A shortcut to [`TextResponse.selector.jmespath(query)`{.docutils
        .literal .notranslate}]{.pre}:

        ::: {.highlight-default .notranslate}
        ::: highlight
            response.jmespath('object.[*]')
        :::
        :::

    [[xpath]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[query]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse.xpath){.reference .internal}[¶](#scrapy.http.TextResponse.xpath "Permalink to this definition"){.headerlink}

    :   A shortcut to [`TextResponse.selector.xpath(query)`{.docutils
        .literal .notranslate}]{.pre}:

        ::: {.highlight-default .notranslate}
        ::: highlight
            response.xpath('//p')
        :::
        :::

    [[css]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[query]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse.css){.reference .internal}[¶](#scrapy.http.TextResponse.css "Permalink to this definition"){.headerlink}

    :   A shortcut to [`TextResponse.selector.css(query)`{.docutils
        .literal .notranslate}]{.pre}:

        ::: {.highlight-default .notranslate}
        ::: highlight
            response.css('p')
        :::
        :::

    [[follow]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Link]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference .internal}[[,]{.pre}]{.p}[ ]{.w}[Selector]{.pre}[[\]]{.pre}]{.p}]{.n}*, *[[callback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[method]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'GET\']{.pre}]{.default_value}*, *[[headers]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Mapping]{.pre}](https://docs.python.org/3/library/typing.html#typing.Mapping "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Iterable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Iterable "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[body]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cookies]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[meta]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[encoding]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[0]{.pre}]{.default_value}*, *[[dont_filter]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*, *[[errback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cb_kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[flags]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse.follow){.reference .internal}[¶](#scrapy.http.TextResponse.follow "Permalink to this definition"){.headerlink}

    :   Return a [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} instance to follow a link [`url`{.docutils .literal
        .notranslate}]{.pre}. It accepts the same arguments as
        [`Request.__init__`{.docutils .literal .notranslate}]{.pre}
        method, but [`url`{.docutils .literal .notranslate}]{.pre} can
        be not only an absolute URL, but also

        -   a relative URL

        -   a [[`Link`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference
            .internal} object, e.g. the result of [[Link
            Extractors]{.std
            .std-ref}](index.html#topics-link-extractors){.hoverxref
            .tooltip .reference .internal}

        -   a [[`Selector`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
            .internal} object for a [`<link>`{.docutils .literal
            .notranslate}]{.pre} or [`<a>`{.docutils .literal
            .notranslate}]{.pre} element, e.g.
            [`response.css('a.my_link')[0]`{.docutils .literal
            .notranslate}]{.pre}

        -   an attribute [[`Selector`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
            .internal} (not SelectorList), e.g.
            [`response.css('a::attr(href)')[0]`{.docutils .literal
            .notranslate}]{.pre} or
            [`response.xpath('//img/@src')[0]`{.docutils .literal
            .notranslate}]{.pre}

        See [[A shortcut for creating Requests]{.std
        .std-ref}](index.html#response-follow-example){.hoverxref
        .tooltip .reference .internal} for usage examples.

    [[follow_all]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[urls]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Iterable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Iterable "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Link]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference .internal}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[SelectorList]{.pre}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[callback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[method]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'GET\']{.pre}]{.default_value}*, *[[headers]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Mapping]{.pre}](https://docs.python.org/3/library/typing.html#typing.Mapping "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[,]{.pre}]{.p}[ ]{.w}[[Iterable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Iterable "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Tuple]{.pre}](https://docs.python.org/3/library/typing.html#typing.Tuple "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[AnyStr]{.pre}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[body]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[bytes]{.pre}](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cookies]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Union]{.pre}](https://docs.python.org/3/library/typing.html#typing.Union "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[dict]{.pre}](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[meta]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[encoding]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[priority]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[int]{.pre}](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[0]{.pre}]{.default_value}*, *[[dont_filter]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*, *[[errback]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Callable]{.pre}](https://docs.python.org/3/library/typing.html#typing.Callable "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[cb_kwargs]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Dict]{.pre}](https://docs.python.org/3/library/typing.html#typing.Dict "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[Any]{.pre}](https://docs.python.org/3/library/typing.html#typing.Any "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[flags]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[List]{.pre}](https://docs.python.org/3/library/typing.html#typing.List "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[css]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*, *[[xpath]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[Optional]{.pre}](https://docs.python.org/3/library/typing.html#typing.Optional "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[None]{.pre}]{.default_value}*[)]{.sig-paren} [[→]{.sig-return-icon} [[[Generator]{.pre}](https://docs.python.org/3/library/typing.html#typing.Generator "(in Python v3.12)"){.reference .external}[[\[]{.pre}]{.p}[[Request]{.pre}](index.html#scrapy.http.Request "scrapy.http.request.Request"){.reference .internal}[[,]{.pre}]{.p}[ ]{.w}[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}[[,]{.pre}]{.p}[ ]{.w}[[None]{.pre}](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"){.reference .external}[[\]]{.pre}]{.p}]{.sig-return-typehint}]{.sig-return}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse.follow_all){.reference .internal}[¶](#scrapy.http.TextResponse.follow_all "Permalink to this definition"){.headerlink}

    :   A generator that produces [[`Request`{.xref .py .py-class
        .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal} instances to follow all links in [`urls`{.docutils
        .literal .notranslate}]{.pre}. It accepts the same arguments as
        the [[`Request`{.xref .py .py-class .docutils .literal
        .notranslate}]{.pre}](#scrapy.http.Request "scrapy.http.Request"){.reference
        .internal}'s [`__init__`{.docutils .literal .notranslate}]{.pre}
        method, except that each [`urls`{.docutils .literal
        .notranslate}]{.pre} element does not need to be an absolute
        URL, it can be any of the following:

        -   a relative URL

        -   a [[`Link`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.link.Link "scrapy.link.Link"){.reference
            .internal} object, e.g. the result of [[Link
            Extractors]{.std
            .std-ref}](index.html#topics-link-extractors){.hoverxref
            .tooltip .reference .internal}

        -   a [[`Selector`{.xref .py .py-class .docutils .literal
            .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
            .internal} object for a [`<link>`{.docutils .literal
            .notranslate}]{.pre} or [`<a>`{.docutils .literal
            .notranslate}]{.pre} element, e.g.
            [`response.css('a.my_link')[0]`{.docutils .literal
            .notranslate}]{.pre}

        -   an attribute [[`Selector`{.xref .py .py-class .docutils
            .literal
            .notranslate}]{.pre}](index.html#scrapy.selector.Selector "scrapy.selector.Selector"){.reference
            .internal} (not SelectorList), e.g.
            [`response.css('a::attr(href)')[0]`{.docutils .literal
            .notranslate}]{.pre} or
            [`response.xpath('//img/@src')[0]`{.docutils .literal
            .notranslate}]{.pre}

        In addition, [`css`{.docutils .literal .notranslate}]{.pre} and
        [`xpath`{.docutils .literal .notranslate}]{.pre} arguments are
        accepted to perform the link extraction within the
        [`follow_all`{.docutils .literal .notranslate}]{.pre} method
        (only one of [`urls`{.docutils .literal .notranslate}]{.pre},
        [`css`{.docutils .literal .notranslate}]{.pre} and
        [`xpath`{.docutils .literal .notranslate}]{.pre} is accepted).

        Note that when passing a [`SelectorList`{.docutils .literal
        .notranslate}]{.pre} as argument for the [`urls`{.docutils
        .literal .notranslate}]{.pre} parameter or using the
        [`css`{.docutils .literal .notranslate}]{.pre} or
        [`xpath`{.docutils .literal .notranslate}]{.pre} parameters,
        this method will not produce requests for selectors from which
        links cannot be obtained (for instance, anchor tags without an
        [`href`{.docutils .literal .notranslate}]{.pre} attribute)

    [[json]{.pre}]{.sig-name .descname}[(]{.sig-paren}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse.json){.reference .internal}[¶](#scrapy.http.TextResponse.json "Permalink to this definition"){.headerlink}

    :   ::: versionadded
        [New in version 2.2.]{.versionmodified .added}
        :::

        Deserialize a JSON document to a Python object.

        Returns a Python object from deserialized JSON document. The
        result is cached after the first call.

    [[urljoin]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/text.html#TextResponse.urljoin){.reference .internal}[¶](#scrapy.http.TextResponse.urljoin "Permalink to this definition"){.headerlink}

    :   Constructs an absolute url by combining the Response's base url
        with a possible relative url. The base url shall be extracted
        from the [`<base>`{.docutils .literal .notranslate}]{.pre} tag,
        or just the Response's [`url`{.xref .py .py-attr .docutils
        .literal .notranslate}]{.pre} if there is no such tag.
:::

::: {#htmlresponse-objects .section}
##### HtmlResponse objects[¶](#htmlresponse-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.http.]{.pre}]{.sig-prename .descclassname}[[HtmlResponse]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}*[\[]{.optional}, *[[\...]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/html.html#HtmlResponse){.reference .internal}[¶](#scrapy.http.HtmlResponse "Permalink to this definition"){.headerlink}

:   The [[`HtmlResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.HtmlResponse "scrapy.http.HtmlResponse"){.reference
    .internal} class is a subclass of [[`TextResponse`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} which adds encoding auto-discovering support by looking
    into the HTML [meta
    http-equiv](https://www.w3schools.com/TAGS/att_meta_http_equiv.asp){.reference
    .external} attribute. See [[`TextResponse.encoding`{.xref .py
    .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse.encoding "scrapy.http.TextResponse.encoding"){.reference
    .internal}.
:::

::: {#xmlresponse-objects .section}
##### XmlResponse objects[¶](#xmlresponse-objects "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.http.]{.pre}]{.sig-prename .descclassname}[[XmlResponse]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}*[\[]{.optional}, *[[\...]{.pre}]{.n}*[\]]{.optional}[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/http/response/xml.html#XmlResponse){.reference .internal}[¶](#scrapy.http.XmlResponse "Permalink to this definition"){.headerlink}

:   The [[`XmlResponse`{.xref .py .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.XmlResponse "scrapy.http.XmlResponse"){.reference
    .internal} class is a subclass of [[`TextResponse`{.xref .py
    .py-class .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse "scrapy.http.TextResponse"){.reference
    .internal} which adds encoding auto-discovering support by looking
    into the XML declaration line. See [[`TextResponse.encoding`{.xref
    .py .py-attr .docutils .literal
    .notranslate}]{.pre}](#scrapy.http.TextResponse.encoding "scrapy.http.TextResponse.encoding"){.reference
    .internal}.
:::
:::
:::

[]{#document-topics/link-extractors}

::: {#link-extractors .section}
[]{#topics-link-extractors}

### Link Extractors[¶](#link-extractors "Permalink to this heading"){.headerlink}

A link extractor is an object that extracts links from responses.

The [`__init__`{.docutils .literal .notranslate}]{.pre} method of
[[`LxmlLinkExtractor`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
.internal} takes settings that determine which links may be extracted.
[[`LxmlLinkExtractor.extract_links`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor.extract_links "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor.extract_links"){.reference
.internal} returns a list of matching [[`Link`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.link.Link "scrapy.link.Link"){.reference
.internal} objects from a [[`Response`{.xref .py .py-class .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
.internal} object.

Link extractors are used in [[`CrawlSpider`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.spiders.CrawlSpider "scrapy.spiders.CrawlSpider"){.reference
.internal} spiders through a set of [[`Rule`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.spiders.Rule "scrapy.spiders.Rule"){.reference
.internal} objects.

You can also use link extractors in regular spiders. For example, you
can instantiate [[`LinkExtractor`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
.internal} into a class variable in your spider, and use it from your
spider callbacks:

::: {.highlight-python .notranslate}
::: highlight
    def parse(self, response):
        for link in self.link_extractor.extract_links(response):
            yield Request(link.url, callback=self.parse)
:::
:::

::: {#module-scrapy.linkextractors .section}
[]{#link-extractor-reference}[]{#topics-link-extractors-ref}

#### Link extractor reference[¶](#module-scrapy.linkextractors "Permalink to this heading"){.headerlink}

The link extractor class is
[[`scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor`{.xref .py .py-class
.docutils .literal
.notranslate}]{.pre}](#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor"){.reference
.internal}. For convenience it can also be imported as
[`scrapy.linkextractors.LinkExtractor`{.docutils .literal
.notranslate}]{.pre}:

::: {.highlight-default .notranslate}
::: highlight
    from scrapy.linkextractors import LinkExtractor
:::
:::

::: {#module-scrapy.linkextractors.lxmlhtml .section}
[]{#lxmllinkextractor}

##### LxmlLinkExtractor[¶](#module-scrapy.linkextractors.lxmlhtml "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.linkextractors.lxmlhtml.]{.pre}]{.sig-prename .descclassname}[[LxmlLinkExtractor]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[allow]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[deny]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[allow_domains]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[deny_domains]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[deny_extensions]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[restrict_xpaths]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[restrict_css]{.pre}]{.n}[[=]{.pre}]{.o}[[()]{.pre}]{.default_value}*, *[[tags]{.pre}]{.n}[[=]{.pre}]{.o}[[(\'a\',]{.pre} [\'area\')]{.pre}]{.default_value}*, *[[attrs]{.pre}]{.n}[[=]{.pre}]{.o}[[(\'href\',)]{.pre}]{.default_value}*, *[[canonicalize]{.pre}]{.n}[[=]{.pre}]{.o}[[False]{.pre}]{.default_value}*, *[[unique]{.pre}]{.n}[[=]{.pre}]{.o}[[True]{.pre}]{.default_value}*, *[[process_value]{.pre}]{.n}[[=]{.pre}]{.o}[[None]{.pre}]{.default_value}*, *[[strip]{.pre}]{.n}[[=]{.pre}]{.o}[[True]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/linkextractors/lxmlhtml.html#LxmlLinkExtractor){.reference .internal}[¶](#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor "Permalink to this definition"){.headerlink}

:   LxmlLinkExtractor is the recommended link extractor with handy
    filtering options. It is implemented using lxml's robust HTMLParser.

    Parameters

    :   -   **allow**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- a single regular expression (or list of
            regular expressions) that the (absolute) urls must match in
            order to be extracted. If not given (or empty), it will
            match all links.

        -   **deny**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- a single regular expression (or list of
            regular expressions) that the (absolute) urls must match in
            order to be excluded (i.e. not extracted). It has precedence
            over the [`allow`{.docutils .literal .notranslate}]{.pre}
            parameter. If not given (or empty) it won't exclude any
            links.

        -   **allow_domains**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- a single value or a list of string containing
            domains which will be considered for extracting the links

        -   **deny_domains**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- a single value or a list of strings
            containing domains which won't be considered for extracting
            the links

        -   **deny_extensions**
            ([*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) --

            a single value or list of strings containing extensions that
            should be ignored when extracting links. If not given, it
            will default to
            [`scrapy.linkextractors.IGNORED_EXTENSIONS`{.xref .py
            .py-data .docutils .literal .notranslate}]{.pre}.

            ::: versionchanged
            [Changed in version 2.0: ]{.versionmodified
            .changed}[`IGNORED_EXTENSIONS`{.xref .py .py-data .docutils
            .literal .notranslate}]{.pre} now includes [`7z`{.docutils
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
            .notranslate}]{.pre}.
            :::

        -   **restrict_xpaths**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- is an XPath (or list of XPath's) which
            defines regions inside the response where links should be
            extracted from. If given, only the text selected by those
            XPath will be scanned for links. See examples below.

        -   **restrict_css**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- a CSS selector (or list of selectors) which
            defines regions inside the response where links should be
            extracted from. Has the same behaviour as
            [`restrict_xpaths`{.docutils .literal .notranslate}]{.pre}.

        -   **restrict_text**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- a single regular expression (or list of
            regular expressions) that the link's text must match in
            order to be extracted. If not given (or empty), it will
            match all links. If a list of regular expressions is given,
            the link will be extracted if it matches at least one.

        -   **tags**
            ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference
            .external} *or*
            [*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- a tag or a list of tags to consider when
            extracting links. Defaults to [`('a',`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`'area')`{.docutils .literal
            .notranslate}]{.pre}.

        -   **attrs**
            ([*list*](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.12)"){.reference
            .external}) -- an attribute or list of attributes which
            should be considered when looking for links to extract (only
            for those tags specified in the [`tags`{.docutils .literal
            .notranslate}]{.pre} parameter). Defaults to
            [`('href',)`{.docutils .literal .notranslate}]{.pre}

        -   **canonicalize**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- canonicalize each extracted url (using
            w3lib.url.canonicalize_url). Defaults to [`False`{.docutils
            .literal .notranslate}]{.pre}. Note that canonicalize_url is
            meant for duplicate checking; it can change the URL visible
            at server side, so the response can be different for
            requests with canonicalized and raw URLs. If you're using
            LinkExtractor to follow links it is more robust to keep the
            default [`canonicalize=False`{.docutils .literal
            .notranslate}]{.pre}.

        -   **unique**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- whether duplicate filtering should be applied
            to extracted links.

        -   **process_value**
            ([*collections.abc.Callable*](https://docs.python.org/3/library/collections.abc.html#collections.abc.Callable "(in Python v3.12)"){.reference
            .external}) --

            a function which receives each value extracted from the tag
            and attributes scanned and can modify the value and return a
            new one, or return [`None`{.docutils .literal
            .notranslate}]{.pre} to ignore the link altogether. If not
            given, [`process_value`{.docutils .literal
            .notranslate}]{.pre} defaults to [`lambda`{.docutils
            .literal .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`x:`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`x`{.docutils .literal .notranslate}]{.pre}.

            For example, to extract links from this code:

            ::: {.highlight-html .notranslate}
            ::: highlight
                <a href="javascript:goToPage('../other/page.html'); return false">Link text</a>
            :::
            :::

            You can use the following function in
            [`process_value`{.docutils .literal .notranslate}]{.pre}:

            ::: {.highlight-python .notranslate}
            ::: highlight
                def process_value(value):
                    m = re.search(r"javascript:goToPage\('(.*?)'", value)
                    if m:
                        return m.group(1)
            :::
            :::

        -   **strip**
            ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference
            .external}) -- whether to strip whitespaces from extracted
            attributes. According to HTML5 standard, leading and
            trailing whitespaces must be stripped from [`href`{.docutils
            .literal .notranslate}]{.pre} attributes of [`<a>`{.docutils
            .literal .notranslate}]{.pre}, [`<area>`{.docutils .literal
            .notranslate}]{.pre} and many other elements,
            [`src`{.docutils .literal .notranslate}]{.pre} attribute of
            [`<img>`{.docutils .literal .notranslate}]{.pre},
            [`<iframe>`{.docutils .literal .notranslate}]{.pre}
            elements, etc., so LinkExtractor strips space chars by
            default. Set [`strip=False`{.docutils .literal
            .notranslate}]{.pre} to turn it off (e.g. if you're
            extracting urls from elements or attributes which allow
            leading/trailing whitespaces).

    [[extract_links]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[response]{.pre}]{.n}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/linkextractors/lxmlhtml.html#LxmlLinkExtractor.extract_links){.reference .internal}[¶](#scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor.extract_links "Permalink to this definition"){.headerlink}

    :   Returns a list of [[`Link`{.xref .py .py-class .docutils
        .literal
        .notranslate}]{.pre}](#scrapy.link.Link "scrapy.link.Link"){.reference
        .internal} objects from the specified [[`response`{.xref .py
        .py-class .docutils .literal
        .notranslate}]{.pre}](index.html#scrapy.http.Response "scrapy.http.Response"){.reference
        .internal}.

        Only links that match the settings passed to the
        [`__init__`{.docutils .literal .notranslate}]{.pre} method of
        the link extractor are returned.

        Duplicate links are omitted if the [`unique`{.docutils .literal
        .notranslate}]{.pre} attribute is set to [`True`{.docutils
        .literal .notranslate}]{.pre}, otherwise they are returned.
:::

::: {#module-scrapy.link .section}
[]{#link}

##### Link[¶](#module-scrapy.link "Permalink to this heading"){.headerlink}

*[class]{.pre}[ ]{.w}*[[scrapy.link.]{.pre}]{.sig-prename .descclassname}[[Link]{.pre}]{.sig-name .descname}[(]{.sig-paren}*[[url]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}*, *[[text]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'\']{.pre}]{.default_value}*, *[[fragment]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[str]{.pre}](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[\'\']{.pre}]{.default_value}*, *[[nofollow]{.pre}]{.n}[[:]{.pre}]{.p}[ ]{.w}[[[bool]{.pre}](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)"){.reference .external}]{.n}[ ]{.w}[[=]{.pre}]{.o}[ ]{.w}[[False]{.pre}]{.default_value}*[)]{.sig-paren}[[[\[source\]]{.pre}]{.viewcode-link}](_modules/scrapy/link.html#Link){.reference .internal}[¶](#scrapy.link.Link "Permalink to this definition"){.headerlink}

:   Link objects represent an extracted link by the LinkExtractor.

    Using the anchor tag sample below to illustrate the parameters:

    ::: {.highlight-python .notranslate}
    ::: highlight
        <a href="https://example.com/nofollow.html#foo" rel="nofollow">Dont follow this one</a>
    :::
    :::

    Parameters

    :   -   **url** -- the absolute url being linked to in the anchor
            tag. From the sample, this is
            [`https://example.com/nofollow.html`{.docutils .literal
            .notranslate}]{.pre}.

        -   **text** -- the text in the anchor tag. From the sample,
            this is [`Dont`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`follow`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`this`{.docutils .literal
            .notranslate}]{.pre}` `{.docutils .literal
            .notranslate}[`one`{.docutils .literal .notranslate}]{.pre}.

        -   **fragment** -- the part of the url after the hash symbol.
            From the sample, this is [`foo`{.docutils .literal
            .notranslate}]{.pre}.

        -   **nofollow** -- an indication of the presence or absence of
            a nofollow value in the [`rel`{.docutils .literal
            .notranslate}]{.pre} attribute of the anchor tag.
:::
:::
:::

[]{#document-topics/settings}

::: {#settings .section}
[]{#topics-settings}

### Settings[¶](#settings "Permalink to this heading"){.headerlink}

The Scrapy settings allows you to customize the behaviour of all Scrapy
components, including the core, extensions, pipelines and spiders
themselves.

The infrastructure of the settings provides a global namespace of
key-value mappings that the code can use to pull configuration values
from. The settings can be populated through different mechanisms, which
are described below.

The settings are also the mechanism for selecting the currently active
Scrapy project (in case you have many).

For a list of available built-in settings see: [[Built-in settings
reference]{.std .std-ref}](#topics-settings-ref){.hoverxref .tooltip
.reference .internal}.

::: {#designating-the-settings .section}
[]{#topics-settings-module-envvar}

#### Designating the settings[¶](#designating-the-settings "Permalink to this heading"){.headerlink}

When you use Scrapy, you have to tell it which settings you're using.
You can do this by using an environment variable,
[`SCRAPY_SETTINGS_MODULE`{.docutils .literal .notranslate}]{.pre}.

The value of [`SCRAPY_SETTINGS_MODULE`{.docutils .literal
.notranslate}]{.pre} should be in Python path syntax, e.g.
[`myproject.settings`{.docutils .literal .notranslate}]{.pre}. Note that
the settings module should be on the Python [[import search path]{.xref
.std
.std-ref}](https://docs.python.org/3/tutorial/modules.html#tut-searchpath "(in Python v3.12)"){.reference
.external}.
:::

::: {#populating-the-settings .section}
[]{#populating-settings}

#### Populating the settings[¶](#populating-the-settings "Permalink to this heading"){.headerlink}

Settings can be populated using different mechanisms, each of which
having a different precedence. Here is the list of them in decreasing
order of precedence:

> <div>
>
> 1.  Command line options (most precedence)
>
> 2.  Settings per-spider
>
> 3.  Project settings module
>
> 4.  Settings set by add-ons
>
> 5.  Default settings per-command
>
> 6.  Default global settings (less precedence)
>
> </div>

The population of these settings sources is taken care of internally,
but a manual handling is possible using API calls. See the [[Settings
API]{.std .std-ref}](index.html#topics-api-settings){.hoverxref .tooltip
.reference .internal} topic for reference.

These mechanisms are described in more detail below.

::: {#command-line-options .section}
##### 1. Command line options[¶](#command-line-options "Permalink to this heading"){.headerlink}

Arguments provided by the command line are the ones that take most
precedence, overriding any other options. You can explicitly override
one (or more) settings using the [`-s`{.docutils .literal
.notranslate}]{.pre} (or [`--set`{.docutils .literal
.notranslate}]{.pre}) command line option.

Example:

::: {.highlight-sh .notranslate}
::: highlight
    scrapy crawl myspider -s LOG_FILE=scrapy.log
:::
:::
:::

::: {#settings-per-spider .section}
##### 2. Settings per-spider[¶](#settings-per-spider "Permalink to this heading"){.headerlink}

Spiders (See the [[Spiders]{.std
.std-ref}](index.html#topics-spiders){.hoverxref .tooltip .reference
.internal} chapter for reference) can define their own settings that
will take precedence and override the project ones. One way to do so is
by setting their [[`custom_settings`{.xref .py .py-attr .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.Spider.custom_settings "scrapy.Spider.custom_settings"){.reference
.internal} attribute:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "myspider"

        custom_settings = {
            "SOME_SETTING": "some value",
        }
:::
:::

It's often better to implement [[`update_settings()`{.xref .py .py-meth
.docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.update_settings "scrapy.Spider.update_settings"){.reference
.internal} instead, and settings set there should use the "spider"
priority explicitly:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "myspider"

        @classmethod
        def update_settings(cls, settings):
            super().update_settings(settings)
            settings.set("SOME_SETTING", "some value", priority="spider")
:::
:::

::: versionadded
[New in version 2.11.]{.versionmodified .added}
:::

It's also possible to modify the settings in the
[[`from_crawler()`{.xref .py .py-meth .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.Spider.from_crawler "scrapy.Spider.from_crawler"){.reference
.internal} method, e.g. based on [[spider arguments]{.std
.std-ref}](index.html#spiderargs){.hoverxref .tooltip .reference
.internal} or other logic:

::: {.highlight-python .notranslate}
::: highlight
    import scrapy


    class MySpider(scrapy.Spider):
        name = "myspider"

        @classmethod
        def from_crawler(cls, crawler, *args, **kwargs):
            spider = super().from_crawler(crawler, *args, **kwargs)
            if "some_argument" in kwargs:
                spider.settings.set(
                    "SOME_SETTING", kwargs["some_argument"], priority="spider"
                )
            return spider
:::
:::
:::

::: {#project-settings-module .section}
##### 3. Project settings module[¶](#project-settings-module "Permalink to this heading"){.headerlink}

The project settings module is the standard configuration file for your
Scrapy project, it's where most of your custom settings will be
populated. For a standard Scrapy project, this means you'll be adding or
changing the settings in the [`settings.py`{.docutils .literal
.notranslate}]{.pre} file created for your project.
:::

::: {#settings-set-by-add-ons .section}
##### 4. Settings set by add-ons[¶](#settings-set-by-add-ons "Permalink to this heading"){.headerlink}

[[Add-ons]{.std .std-ref}](index.html#topics-addons){.hoverxref .tooltip
.reference .internal} can modify settings. They should do this with this
priority, though this is not enforced.
:::

::: {#default-settings-per-command .section}
##### 5. Default settings per-command[¶](#default-settings-per-command "Permalink to this heading"){.headerlink}

Each [[Scrapy
tool]{.doc}](index.html#document-topics/commands){.reference .internal}
command can have its own default settings, which override the global
default settings. Those custom command settings are specified in the
[`default_settings`{.docutils .literal .notranslate}]{.pre} attribute of
the command class.
:::

::: {#default-global-settings .section}
##### 6. Default global settings[¶](#default-global-settings "Permalink to this heading"){.headerlink}

The global defaults are located in the
[`scrapy.settings.default_settings`{.docutils .literal
.notranslate}]{.pre} module and documented in the [[Built-in settings
reference]{.std .std-ref}](#topics-settings-ref){.hoverxref .tooltip
.reference .internal} section.
:::
:::

::: {#compatibility-with-pickle .section}
#### Compatibility with pickle[¶](#compatibility-with-pickle "Permalink to this heading"){.headerlink}

Setting values must be [[picklable]{.xref .std
.std-ref}](https://docs.python.org/3/library/pickle.html#pickle-picklable "(in Python v3.12)"){.reference
.external}.
:::

::: {#import-paths-and-classes .section}
#### Import paths and classes[¶](#import-paths-and-classes "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.4.0.]{.versionmodified .added}
:::

When a setting references a callable object to be imported by Scrapy,
such as a class or a function, there are two different ways you can
specify that object:

-   As a string containing the import path of that object

-   As the object itself

For example:

::: {.highlight-python .notranslate}
::: highlight
    from mybot.pipelines.validate import ValidateMyItem

    ITEM_PIPELINES = {
        # passing the classname...
        ValidateMyItem: 300,
        # ...equals passing the class path
        "mybot.pipelines.validate.ValidateMyItem": 300,
    }
:::
:::

::: {.admonition .note}
Note

Passing non-callable objects is not supported.
:::
:::

::: {#how-to-access-settings .section}
#### How to access settings[¶](#how-to-access-settings "Permalink to this heading"){.headerlink}

In a spider, the settings are available through
[`self.settings`{.docutils .literal .notranslate}]{.pre}:

::: {.highlight-python .notranslate}
::: highlight
    class MySpider(scrapy.Spider):
        name = "myspider"
        start_urls = ["http://example.com"]

        def parse(self, response):
            print(f"Existing settings: {self.settings.attributes.keys()}")
:::
:::

::: {.admonition .note}
Note

The [`settings`{.docutils .literal .notranslate}]{.pre} attribute is set
in the base Spider class after the spider is initialized. If you want to
use the settings before the initialization (e.g., in your spider's
[`__init__()`{.docutils .literal .notranslate}]{.pre} method), you'll
need to override the [[`from_crawler()`{.xref .py .py-meth .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.Spider.from_crawler "scrapy.Spider.from_crawler"){.reference
.internal} method.
:::

Settings can be accessed through the
[[`scrapy.crawler.Crawler.settings`{.xref .py .py-attr .docutils
.literal
.notranslate}]{.pre}](index.html#scrapy.crawler.Crawler.settings "scrapy.crawler.Crawler.settings"){.reference
.internal} attribute of the Crawler that is passed to
[`from_crawler`{.docutils .literal .notranslate}]{.pre} method in
extensions, middlewares and item pipelines:

::: {.highlight-python .notranslate}
::: highlight
    class MyExtension:
        def __init__(self, log_is_enabled=False):
            if log_is_enabled:
                print("log is enabled!")

        @classmethod
        def from_crawler(cls, crawler):
            settings = crawler.settings
            return cls(settings.getbool("LOG_ENABLED"))
:::
:::

The settings object can be used like a dict (e.g.,
[`settings['LOG_ENABLED']`{.docutils .literal .notranslate}]{.pre}), but
it's usually preferred to extract the setting in the format you need it
to avoid type errors, using one of the methods provided by the
[[`Settings`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.settings.Settings "scrapy.settings.Settings"){.reference
.internal} API.
:::

::: {#rationale-for-setting-names .section}
#### Rationale for setting names[¶](#rationale-for-setting-names "Permalink to this heading"){.headerlink}

Setting names are usually prefixed with the component that they
configure. For example, proper setting names for a fictional robots.txt
extension would be [`ROBOTSTXT_ENABLED`{.docutils .literal
.notranslate}]{.pre}, [`ROBOTSTXT_OBEY`{.docutils .literal
.notranslate}]{.pre}, [`ROBOTSTXT_CACHEDIR`{.docutils .literal
.notranslate}]{.pre}, etc.
:::

::: {#built-in-settings-reference .section}
[]{#topics-settings-ref}

#### Built-in settings reference[¶](#built-in-settings-reference "Permalink to this heading"){.headerlink}

Here's a list of all available Scrapy settings, in alphabetical order,
along with their default values and the scope where they apply.

The scope, where available, shows where the setting is being used, if
it's tied to any particular component. In that case the module of that
component will be shown, typically an extension, middleware or pipeline.
It also means that the component must be enabled in order for the
setting to have any effect.

::: {#addons .section}
[]{#std-setting-ADDONS}

##### ADDONS[¶](#addons "Permalink to this heading"){.headerlink}

Default: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing paths to the add-ons enabled in your project and their
priorities. For more information, see [[Add-ons]{.std
.std-ref}](index.html#topics-addons){.hoverxref .tooltip .reference
.internal}.
:::

::: {#aws-access-key-id .section}
[]{#std-setting-AWS_ACCESS_KEY_ID}

##### AWS_ACCESS_KEY_ID[¶](#aws-access-key-id "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The AWS access key used by code that requires access to [Amazon Web
services](https://aws.amazon.com/){.reference .external}, such as the
[[S3 feed storage backend]{.std
.std-ref}](index.html#topics-feed-storage-s3){.hoverxref .tooltip
.reference .internal}.
:::

::: {#aws-secret-access-key .section}
[]{#std-setting-AWS_SECRET_ACCESS_KEY}

##### AWS_SECRET_ACCESS_KEY[¶](#aws-secret-access-key "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The AWS secret key used by code that requires access to [Amazon Web
services](https://aws.amazon.com/){.reference .external}, such as the
[[S3 feed storage backend]{.std
.std-ref}](index.html#topics-feed-storage-s3){.hoverxref .tooltip
.reference .internal}.
:::

::: {#aws-session-token .section}
[]{#std-setting-AWS_SESSION_TOKEN}

##### AWS_SESSION_TOKEN[¶](#aws-session-token "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The AWS security token used by code that requires access to [Amazon Web
services](https://aws.amazon.com/){.reference .external}, such as the
[[S3 feed storage backend]{.std
.std-ref}](index.html#topics-feed-storage-s3){.hoverxref .tooltip
.reference .internal}, when using [temporary security
credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#temporary-access-keys){.reference
.external}.
:::

::: {#aws-endpoint-url .section}
[]{#std-setting-AWS_ENDPOINT_URL}

##### AWS_ENDPOINT_URL[¶](#aws-endpoint-url "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

Endpoint URL used for S3-like storage, for example Minio or s3.scality.
:::

::: {#aws-use-ssl .section}
[]{#std-setting-AWS_USE_SSL}

##### AWS_USE_SSL[¶](#aws-use-ssl "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

Use this option if you want to disable SSL connection for communication
with S3 or S3-like storage. By default SSL will be used.
:::

::: {#aws-verify .section}
[]{#std-setting-AWS_VERIFY}

##### AWS_VERIFY[¶](#aws-verify "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

Verify SSL connection between Scrapy and S3 or S3-like storage. By
default SSL verification will occur.
:::

::: {#aws-region-name .section}
[]{#std-setting-AWS_REGION_NAME}

##### AWS_REGION_NAME[¶](#aws-region-name "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

The name of the region associated with the AWS client.
:::

::: {#asyncio-event-loop .section}
[]{#std-setting-ASYNCIO_EVENT_LOOP}

##### ASYNCIO_EVENT_LOOP[¶](#asyncio-event-loop "Permalink to this heading"){.headerlink}

Default: [`None`{.docutils .literal .notranslate}]{.pre}

Import path of a given [`asyncio`{.docutils .literal
.notranslate}]{.pre} event loop class.

If the asyncio reactor is enabled (see [[`TWISTED_REACTOR`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-TWISTED_REACTOR){.hoverxref .tooltip
.reference .internal}) this setting can be used to specify the asyncio
event loop to be used with it. Set the setting to the import path of the
desired asyncio event loop class. If the setting is set to
[`None`{.docutils .literal .notranslate}]{.pre} the default asyncio
event loop will be used.

If you are installing the asyncio reactor manually using the
[[`install_reactor()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.reactor.install_reactor "scrapy.utils.reactor.install_reactor"){.reference
.internal} function, you can use the [`event_loop_path`{.docutils
.literal .notranslate}]{.pre} parameter to indicate the import path of
the event loop class to be used.

Note that the event loop class must inherit from
[[`asyncio.AbstractEventLoop`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-eventloop.html#asyncio.AbstractEventLoop "(in Python v3.12)"){.reference
.external}.

::: {.admonition .caution}
Caution

Please be aware that, when using a non-default event loop (either
defined via [[`ASYNCIO_EVENT_LOOP`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-ASYNCIO_EVENT_LOOP){.hoverxref
.tooltip .reference .internal} or installed with
[[`install_reactor()`{.xref .py .py-func .docutils .literal
.notranslate}]{.pre}](#scrapy.utils.reactor.install_reactor "scrapy.utils.reactor.install_reactor"){.reference
.internal}), Scrapy will call [[`asyncio.set_event_loop()`{.xref .py
.py-func .docutils .literal
.notranslate}]{.pre}](https://docs.python.org/3/library/asyncio-eventloop.html#asyncio.set_event_loop "(in Python v3.12)"){.reference
.external}, which will set the specified event loop as the current loop
for the current OS thread.
:::
:::

::: {#bot-name .section}
[]{#std-setting-BOT_NAME}

##### BOT_NAME[¶](#bot-name "Permalink to this heading"){.headerlink}

Default: [`'scrapybot'`{.docutils .literal .notranslate}]{.pre}

The name of the bot implemented by this Scrapy project (also known as
the project name). This name will be used for the logging too.

It's automatically populated with your project name when you create your
project with the [[`startproject`{.xref .std .std-command .docutils
.literal
.notranslate}]{.pre}](index.html#std-command-startproject){.hoverxref
.tooltip .reference .internal} command.
:::

::: {#concurrent-items .section}
[]{#std-setting-CONCURRENT_ITEMS}

##### CONCURRENT_ITEMS[¶](#concurrent-items "Permalink to this heading"){.headerlink}

Default: [`100`{.docutils .literal .notranslate}]{.pre}

Maximum number of concurrent items (per response) to process in parallel
in [[item pipelines]{.std
.std-ref}](index.html#topics-item-pipeline){.hoverxref .tooltip
.reference .internal}.
:::

::: {#concurrent-requests .section}
[]{#std-setting-CONCURRENT_REQUESTS}

##### CONCURRENT_REQUESTS[¶](#concurrent-requests "Permalink to this heading"){.headerlink}

Default: [`16`{.docutils .literal .notranslate}]{.pre}

The maximum number of concurrent (i.e. simultaneous) requests that will
be performed by the Scrapy downloader.
:::

::: {#concurrent-requests-per-domain .section}
[]{#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN}

##### CONCURRENT_REQUESTS_PER_DOMAIN[¶](#concurrent-requests-per-domain "Permalink to this heading"){.headerlink}

Default: [`8`{.docutils .literal .notranslate}]{.pre}

The maximum number of concurrent (i.e. simultaneous) requests that will
be performed to any single domain.

See also: [[AutoThrottle extension]{.std
.std-ref}](index.html#topics-autothrottle){.hoverxref .tooltip
.reference .internal} and its [[`AUTOTHROTTLE_TARGET_CONCURRENCY`{.xref
.std .std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-AUTOTHROTTLE_TARGET_CONCURRENCY){.hoverxref
.tooltip .reference .internal} option.
:::

::: {#concurrent-requests-per-ip .section}
[]{#std-setting-CONCURRENT_REQUESTS_PER_IP}

##### CONCURRENT_REQUESTS_PER_IP[¶](#concurrent-requests-per-ip "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

The maximum number of concurrent (i.e. simultaneous) requests that will
be performed to any single IP. If non-zero, the
[[`CONCURRENT_REQUESTS_PER_DOMAIN`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_DOMAIN){.hoverxref
.tooltip .reference .internal} setting is ignored, and this one is used
instead. In other words, concurrency limits will be applied per IP, not
per domain.

This setting also affects [[`DOWNLOAD_DELAY`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_DELAY){.hoverxref .tooltip
.reference .internal} and [[AutoThrottle extension]{.std
.std-ref}](index.html#topics-autothrottle){.hoverxref .tooltip
.reference .internal}: if [[`CONCURRENT_REQUESTS_PER_IP`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-CONCURRENT_REQUESTS_PER_IP){.hoverxref
.tooltip .reference .internal} is non-zero, download delay is enforced
per IP, not per domain.
:::

::: {#default-item-class .section}
[]{#std-setting-DEFAULT_ITEM_CLASS}

##### DEFAULT_ITEM_CLASS[¶](#default-item-class "Permalink to this heading"){.headerlink}

Default: [`'scrapy.Item'`{.docutils .literal .notranslate}]{.pre}

The default class that will be used for instantiating items in the [[the
Scrapy shell]{.std .std-ref}](index.html#topics-shell){.hoverxref
.tooltip .reference .internal}.
:::

::: {#default-request-headers .section}
[]{#std-setting-DEFAULT_REQUEST_HEADERS}

##### DEFAULT_REQUEST_HEADERS[¶](#default-request-headers "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
        "Accept-Language": "en",
    }
:::
:::

The default headers used for Scrapy HTTP Requests. They're populated in
the [[`DefaultHeadersMiddleware`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre}](index.html#scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware "scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware"){.reference
.internal}.

::: {.admonition .caution}
Caution

Cookies set via the [`Cookie`{.docutils .literal .notranslate}]{.pre}
header are not considered by the [[CookiesMiddleware]{.std
.std-ref}](index.html#cookies-mw){.hoverxref .tooltip .reference
.internal}. If you need to set cookies for a request, use the
[`Request.cookies`{.xref .py .py-class .docutils .literal
.notranslate}]{.pre} parameter. This is a known current limitation that
is being worked on.
:::
:::

::: {#depth-limit .section}
[]{#std-setting-DEPTH_LIMIT}

##### DEPTH_LIMIT[¶](#depth-limit "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.spidermiddlewares.depth.DepthMiddleware`{.docutils
.literal .notranslate}]{.pre}

The maximum depth that will be allowed to crawl for any site. If zero,
no limit will be imposed.
:::

::: {#depth-priority .section}
[]{#std-setting-DEPTH_PRIORITY}

##### DEPTH_PRIORITY[¶](#depth-priority "Permalink to this heading"){.headerlink}

Default: [`0`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.spidermiddlewares.depth.DepthMiddleware`{.docutils
.literal .notranslate}]{.pre}

An integer that is used to adjust the [`priority`{.xref .py .py-attr
.docutils .literal .notranslate}]{.pre} of a [`Request`{.xref .py
.py-class .docutils .literal .notranslate}]{.pre} based on its depth.

The priority of a request is adjusted as follows:

::: {.highlight-python .notranslate}
::: highlight
    request.priority = request.priority - (depth * DEPTH_PRIORITY)
:::
:::

As depth increases, positive values of [`DEPTH_PRIORITY`{.docutils
.literal .notranslate}]{.pre} decrease request priority (BFO), while
negative values increase request priority (DFO). See also [[Does Scrapy
crawl in breadth-first or depth-first order?]{.std
.std-ref}](index.html#faq-bfo-dfo){.hoverxref .tooltip .reference
.internal}.

::: {.admonition .note}
Note

This setting adjusts priority **in the opposite way** compared to other
priority settings [[`REDIRECT_PRIORITY_ADJUST`{.xref .std .std-setting
.docutils .literal
.notranslate}]{.pre}](#std-setting-REDIRECT_PRIORITY_ADJUST){.hoverxref
.tooltip .reference .internal} and [[`RETRY_PRIORITY_ADJUST`{.xref .std
.std-setting .docutils .literal
.notranslate}]{.pre}](index.html#std-setting-RETRY_PRIORITY_ADJUST){.hoverxref
.tooltip .reference .internal}.
:::
:::

::: {#depth-stats-verbose .section}
[]{#std-setting-DEPTH_STATS_VERBOSE}

##### DEPTH_STATS_VERBOSE[¶](#depth-stats-verbose "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Scope: [`scrapy.spidermiddlewares.depth.DepthMiddleware`{.docutils
.literal .notranslate}]{.pre}

Whether to collect verbose depth stats. If this is enabled, the number
of requests for each depth is collected in the stats.
:::

::: {#dnscache-enabled .section}
[]{#std-setting-DNSCACHE_ENABLED}

##### DNSCACHE_ENABLED[¶](#dnscache-enabled "Permalink to this heading"){.headerlink}

Default: [`True`{.docutils .literal .notranslate}]{.pre}

Whether to enable DNS in-memory cache.
:::

::: {#dnscache-size .section}
[]{#std-setting-DNSCACHE_SIZE}

##### DNSCACHE_SIZE[¶](#dnscache-size "Permalink to this heading"){.headerlink}

Default: [`10000`{.docutils .literal .notranslate}]{.pre}

DNS in-memory cache size.
:::

::: {#dns-resolver .section}
[]{#std-setting-DNS_RESOLVER}

##### DNS_RESOLVER[¶](#dns-resolver "Permalink to this heading"){.headerlink}

::: versionadded
[New in version 2.0.]{.versionmodified .added}
:::

Default: [`'scrapy.resolver.CachingThreadedResolver'`{.docutils .literal
.notranslate}]{.pre}

The class to be used to resolve DNS names. The default
[`scrapy.resolver.CachingThreadedResolver`{.docutils .literal
.notranslate}]{.pre} supports specifying a timeout for DNS requests via
the [[`DNS_TIMEOUT`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DNS_TIMEOUT){.hoverxref .tooltip
.reference .internal} setting, but works only with IPv4 addresses.
Scrapy provides an alternative resolver,
[`scrapy.resolver.CachingHostnameResolver`{.docutils .literal
.notranslate}]{.pre}, which supports IPv4/IPv6 addresses but does not
take the [[`DNS_TIMEOUT`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DNS_TIMEOUT){.hoverxref .tooltip
.reference .internal} setting into account.
:::

::: {#dns-timeout .section}
[]{#std-setting-DNS_TIMEOUT}

##### DNS_TIMEOUT[¶](#dns-timeout "Permalink to this heading"){.headerlink}

Default: [`60`{.docutils .literal .notranslate}]{.pre}

Timeout for processing of DNS queries in seconds. Float is supported.
:::

::: {#downloader .section}
[]{#std-setting-DOWNLOADER}

##### DOWNLOADER[¶](#downloader "Permalink to this heading"){.headerlink}

Default: [`'scrapy.core.downloader.Downloader'`{.docutils .literal
.notranslate}]{.pre}

The downloader to use for crawling.
:::

::: {#downloader-httpclientfactory .section}
[]{#std-setting-DOWNLOADER_HTTPCLIENTFACTORY}

##### DOWNLOADER_HTTPCLIENTFACTORY[¶](#downloader-httpclientfactory "Permalink to this heading"){.headerlink}

Default:
[`'scrapy.core.downloader.webclient.ScrapyHTTPClientFactory'`{.docutils
.literal .notranslate}]{.pre}

Defines a Twisted [`protocol.ClientFactory`{.docutils .literal
.notranslate}]{.pre} class to use for HTTP/1.0 connections (for
[`HTTP10DownloadHandler`{.docutils .literal .notranslate}]{.pre}).

::: {.admonition .note}
Note

HTTP/1.0 is rarely used nowadays so you can safely ignore this setting,
unless you really want to use HTTP/1.0 and override
[[`DOWNLOAD_HANDLERS`{.xref .std .std-setting .docutils .literal
.notranslate}]{.pre}](#std-setting-DOWNLOAD_HANDLERS){.hoverxref
.tooltip .reference .internal} for [`http(s)`{.docutils .literal
.notranslate}]{.pre} scheme accordingly, i.e. to
[`'scrapy.core.downloader.handlers.http.HTTP10DownloadHandler'`{.docutils
.literal .notranslate}]{.pre}.
:::
:::

::: {#downloader-clientcontextfactory .section}
[]{#std-setting-DOWNLOADER_CLIENTCONTEXTFACTORY}

##### DOWNLOADER_CLIENTCONTEXTFACTORY[¶](#downloader-clientcontextfactory "Permalink to this heading"){.headerlink}

Default:
[`'scrapy.core.downloader.contextfactory.ScrapyClientContextFactory'`{.docutils
.literal .notranslate}]{.pre}

Represents the classpath to the ContextFactory to use.

Here, "ContextFactory" is a Twisted term for SSL/TLS contexts, defining
the TLS/SSL protocol version to use, whether to do certificate
verification, or even enable client-side authentication (and various
other things).

::: {.admonition .note}
Note

Scrapy default context factory **does NOT perform remote server
certificate verification**. This is usually fine for web scraping.

If you do need remote server certificate verification enabled, Scrapy
also has another context factory class that you can set,
[`'scrapy.core.downloader.contextfactory.BrowserLikeContextFactory'`{.docutils
.literal .notranslate}]{.pre}, which uses the platform's certificates to
validate remote endpoints.
:::

If you do use a custom ContextFactory, make sure its
[`__init__`{.docutils .literal .notranslate}]{.pre} method accepts a
[`method`{.docutils .literal .notranslate}]{.pre} parameter (this is the
[`OpenSSL.SSL`{.docutils .literal .notranslate}]{.pre} method mapping
[[`DOWNLOADER_CLIENT_TLS_METHOD`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-DOWNLOADER_CLIENT_TLS_METHOD){.hoverxref
.tooltip .reference .internal}), a [`tls_verbose_logging`{.docutils
.literal .notranslate}]{.pre} parameter ([`bool`{.docutils .literal
.notranslate}]{.pre}) and a [`tls_ciphers`{.docutils .literal
.notranslate}]{.pre} parameter (see
[[`DOWNLOADER_CLIENT_TLS_CIPHERS`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-DOWNLOADER_CLIENT_TLS_CIPHERS){.hoverxref
.tooltip .reference .internal}).
:::

::: {#downloader-client-tls-ciphers .section}
[]{#std-setting-DOWNLOADER_CLIENT_TLS_CIPHERS}

##### DOWNLOADER_CLIENT_TLS_CIPHERS[¶](#downloader-client-tls-ciphers "Permalink to this heading"){.headerlink}

Default: [`'DEFAULT'`{.docutils .literal .notranslate}]{.pre}

Use this setting to customize the TLS/SSL ciphers used by the default
HTTP/1.1 downloader.

The setting should contain a string in the [OpenSSL cipher list
format](https://www.openssl.org/docs/manmaster/man1/openssl-ciphers.html#CIPHER-LIST-FORMAT){.reference
.external}, these ciphers will be used as client ciphers. Changing this
setting may be necessary to access certain HTTPS websites: for example,
you may need to use [`'DEFAULT:!DH'`{.docutils .literal
.notranslate}]{.pre} for a website with weak DH parameters or enable a
specific cipher that is not included in [`DEFAULT`{.docutils .literal
.notranslate}]{.pre} if a website requires it.
:::

::: {#downloader-client-tls-method .section}
[]{#std-setting-DOWNLOADER_CLIENT_TLS_METHOD}

##### DOWNLOADER_CLIENT_TLS_METHOD[¶](#downloader-client-tls-method "Permalink to this heading"){.headerlink}

Default: [`'TLS'`{.docutils .literal .notranslate}]{.pre}

Use this setting to customize the TLS/SSL method used by the default
HTTP/1.1 downloader.

This setting must be one of these string values:

-   [`'TLS'`{.docutils .literal .notranslate}]{.pre}: maps to OpenSSL's
    [`TLS_method()`{.docutils .literal .notranslate}]{.pre} (a.k.a
    [`SSLv23_method()`{.docutils .literal .notranslate}]{.pre}), which
    allows protocol negotiation, starting from the highest supported by
    the platform; **default, recommended**

-   [`'TLSv1.0'`{.docutils .literal .notranslate}]{.pre}: this value
    forces HTTPS connections to use TLS version 1.0 ; set this if you
    want the behavior of Scrapy\<1.1

-   [`'TLSv1.1'`{.docutils .literal .notranslate}]{.pre}: forces TLS
    version 1.1

-   [`'TLSv1.2'`{.docutils .literal .notranslate}]{.pre}: forces TLS
    version 1.2
:::

::: {#downloader-client-tls-verbose-logging .section}
[]{#std-setting-DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING}

##### DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING[¶](#downloader-client-tls-verbose-logging "Permalink to this heading"){.headerlink}

Default: [`False`{.docutils .literal .notranslate}]{.pre}

Setting this to [`True`{.docutils .literal .notranslate}]{.pre} will
enable DEBUG level messages about TLS connection parameters after
establishing HTTPS connections. The kind of information logged depends
on the versions of OpenSSL and pyOpenSSL.

This setting is only used for the default
[[`DOWNLOADER_CLIENTCONTEXTFACTORY`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-DOWNLOADER_CLIENTCONTEXTFACTORY){.hoverxref
.tooltip .reference .internal}.
:::

::: {#downloader-middlewares .section}
[]{#std-setting-DOWNLOADER_MIDDLEWARES}

##### DOWNLOADER_MIDDLEWARES[¶](#downloader-middlewares "Permalink to this heading"){.headerlink}

Default:: [`{}`{.docutils .literal .notranslate}]{.pre}

A dict containing the downloader middlewares enabled in your project,
and their orders. For more info see [[Activating a downloader
middleware]{.std
.std-ref}](index.html#topics-downloader-middleware-setting){.hoverxref
.tooltip .reference .internal}.
:::

::: {#downloader-middlewares-base .section}
[]{#std-setting-DOWNLOADER_MIDDLEWARES_BASE}

##### DOWNLOADER_MIDDLEWARES_BASE[¶](#downloader-middlewares-base "Permalink to this heading"){.headerlink}

Default:

::: {.highlight-python .notranslate}
::: highlight
    {
        "scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware": 100,
        "scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware": 300,
        "scrapy.downloadermiddlewares.downloadtimeout.DownloadTimeoutMiddleware": 350,
        "scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware": 400,
        "scrapy.downloadermiddlewares.useragent.UserAgentMiddleware": 500,
        "scrapy.downloadermiddlewares.retry.RetryMiddleware": 550,
        "scrapy.downloadermiddlewares.ajaxcrawl.AjaxCrawlMiddleware": 560,
        "scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware": 580,
        "scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware": 590,
        "scrapy.downloadermiddlewares.redirect.RedirectMiddleware": 600,
        "scrapy.downloadermiddlewares.cookies.CookiesMiddleware": 700,
        "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware": 750,
        "scrapy.downloadermiddlewares.stats.DownloaderStats": 850,
        "scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware": 900,
    }
:::
:::

A dict containing the downloader middlewares enabled by default in
Scrapy. Low orders are closer to the engine, high orders are closer to
the downloader. You should never modify this setting in your project,
modify [[`DOWNLOADER_MIDDLEWARES`{.xref .std .std-setting .docutils
.literal
.notranslate}]{.pre}](#std-setting-DOWNLOADER_MIDDLEWARES){.hoverxref
.tooltip .reference .internal} instead. For more info see [[Activating a
downloader middleware]{.std