# spidy Web Crawler
Spidy (/spˈɪdi/) is the simple, easy to use command line web crawler.<br>
This is the very technical documentation file.<br>
Heads up: We have no idea how to do this! If you wish to help please do, just edit and make a Pull Request!<br>
If you're looking for the plain English, check out the [README](https://github.com/rivermont/spidy).

--------------------

# Table of Contents

  - [spidy](#spidy-web-crawler)
  - [Table of Contents](#table-of-contents)
  - [Errors](#errors)
    - [HeaderError](#headererror--source)
  - [Functions](#functions)
    - [check_link](#check_link--source)
	- [info_log](#info_log--source)
    - [mime_lookup](#mime_lookup--source]
  - [Global Variables](#global-variables)
    - [CRAWLER_DIR](#crawler_dir--source)
	- [KILL_LIST](#kill_list--source)
	- [LOG_FILE](#log_file--source)
	- [LOG_FILE_NAME](#log_file_name--source)
    - [MIME_TYPES](#mime_types--source)
	- [START_TIME](#start_time--source)
	- [START_TIME_LONG](#start_time_long--source)
	- [VERSION](#version--source)


# Errors
This section lists the custom Errors and Exceptions in `crawler.py` that may be raised throughout the code.

## `HeaderError` - [Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L50))
Raised when there is a problem deciphering HTTP headers returned from a website.


# Functions
This section lists the functions in `crawler.py` that are used throughout the code.

## `check_link` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L64))
Important to not breaking the crawler.<br>
Determines whether links should be crawled.<br>
Types of links that will be pruned:

  - Links that are too long or short.
  - Links that don't start with `http(s)`.
  - Links that have already been crawled.
  - Links in [`KILL_LIST`](#kill_list--source).

## `info_log` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L209))
Logs important information to the console and log file.<br>
Example log:

> [23:17:06] [spidy] [INFO]: Queried 100 links.
> [23:17:06] [spidy] [INFO]: Started at 23:15:33.
> [23:17:06] [spidy] [INFO]: Log location: logs/spidy_log_1499483733
> [23:17:06] [spidy] [INFO]: Error log location: logs/spidy_error_log_1499483733.txt
> [23:17:06] [spidy] [INFO]: 1901 links in TODO.
> [23:17:06] [spidy] [INFO]: 110446 links in done.
> [23:17:06] [spidy] [INFO]: 0/5 new errors caught.
> [23:17:06] [spidy] [INFO]: 0/20 HTTP errors encountered.
> [23:17:06] [spidy] [INFO]: 1/10 new MIMEs found.
> [23:17:06] [spidy] [INFO]: 3/20 known errors caught.
> [23:17:06] [spidy] [INFO]: Saving files...
> [23:17:06] [spidy] [LOG]: Saved TODO list to crawler_todo.txt
> [23:17:06] [spidy] [LOG]: Saved done list to crawler_done.txt
> [23:17:06] [spidy] [LOG]: Saved 90 bad links to crawler_bad.txt

## `mime_lookup` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L171))
This finds the correct file extension for a MIME type using the [`MIME_TYPES`](#mime_types--source) dictionary.<br>
If the MIME type is blank it defaults to `.html`, and if the MIME type is not in the dictionary a [`HeaderError`](#headererror--source) is raised.<br>
Usage:

> mime_lookup(value)

Where `value` is the MIME type.


# Global Variables
This section lists the variables in [`crawler.py`](#https://github.om/rivermont/spidy/blob/master/crawler.py) that are used throughout the code.

## `CRAWLER_DIR` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L24))
The directory that `crawler.py` is located in.

## `KILL_LIST` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L403))
A list of pages that are known to cause problems with the crawler.

  - `scores.usaultimate.org/` - 

## `LOG_FILE` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L27))
The file that the command line logs are written to.<br>
Kept open until the crawler stops for whatever reason so that it can be written to.

## `LOG_FILE_NAME`  - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L28))
The actual file name of [`LOG_FILE`](#log_file--source).<br>
Used in [`info_log`](#info_log--source).

## `MIME_TYPES` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L298))
A dictionary of [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) encountered by the crawler.<br>
While there are [thousands of other types](https://www.iana.org/assignments/media-types/media-types.xhtml) that are not listed, to list them all would be impractical:
  - The size of the list would be huge, using memory, space, etc.
  - Lookup times would likely be much longer due to the size.
  - Many of the types are outdated or rarely used.
However there are many incorrect usages out there, as the list shows.
  - `text/xml`, `text/rss+xml` are both wrong for RSS feeds: [StackOverflow](https://stackoverflow.com/q/595616/4381663)
  - `html` should never be used. Only `text/html`.

The extension for a MIME type can be found using the dictionary itself or by calling `mime_lookup(value)`<br>
To use the dictionary, use:

> MIME_TYPES[value]

Where `value` is the MIME type.<br>
This will return the extension associated with the MIME type if it exists, however this will throw an [`IndexError`](https://docs.python.org/2/library/exceptions.html#exceptions.IndexError) if the MIME type is not in the dictionary.<br>
Because of this, it is recommended to use the [`mime_lookup`](#mime_lookup--source) function.

## `START_TIME` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L15))
The time that `crawler.py` was started, in seconds from the epoch.<br>
More information can be found on the page for the Python [time](https://docs.python.org/3/library/time.html) library.

## `START_TIME_LONG` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L18))
The time that `crawler.py` was started, in the format `HH:MM:SS, Date Month Year`.<br>
Used in `info_log`.

## `VERSION` - ([Source](https://github.com/rivermont/spidy/blob/master/crawler.py#L5))
The current version of the crawler.