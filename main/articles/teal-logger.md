# Getting started

## Introduction

The `teal.logger` package utilizes the `logger` framework to record
events within a package. `logger` is an R package that supports logging
namespaces, hierarchical logging, various log destinations,
vectorization, and more. For further details about `logger`, you can
refer to:

- [GitHub](https://github.com/daroczig/logger)
- [CRAN](https://CRAN.R-project.org/package=logger)

## Default Logging Setup of `teal.logger`

`teal.logger` employs the
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)
function to create a new logger in a user-defined namespace.
`teal.logger` comes with a predefined pair of layout and logging level.
Other packages in the `teal` framework utilize `teal.logger` to log
crucial events, such as setting up `teal` data, alterations in the
filter panel, records of merging data slices inside modules, and so on.

Defaults of `teal.logger`:

- Logging level: `logger.INFO`
- Logging layout:
  `[{level}] {format(time, \"%Y-%m-%d %H:%M:%OS4\")} pid:{pid} token:[{token}] {ans} {msg}`
- Logs emitted to `stdout`

For a more comprehensive understanding of various logging levels and
layout interpretation, you can explore the [`logger`
documentation](https://daroczig.github.io/logger/articles/customize_logger.html).

## Customizing the Log Level

While utilizing
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md),
the default logging level for the new logger is
[`logger::INFO`](https://daroczig.github.io/logger/reference/log_levels.html).
You can modify this behavior in four distinct ways:

1.  Using the `logger` interface.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``)`\
`logger``::`[`log_threshold`](https://daroczig.github.io/logger/reference/log_threshold.html)`(``logger``::`[`TRACE`](https://daroczig.github.io/logger/reference/log_levels.html)`, namespace ``=`` ``"my_namespace"``)`

Customizing `teal`’s logging level:

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
`logger``::`[`log_threshold`](https://daroczig.github.io/logger/reference/log_threshold.html)`(``logger``::`[`TRACE`](https://daroczig.github.io/logger/reference/log_levels.html)`, namespace ``=`` ``"teal"``)`

2.  Utilizing the function argument of
    [`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md).

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``, level ``=`` ``logger``::`[`TRACE`](https://daroczig.github.io/logger/reference/log_levels.html)`)`

Customizing `teal`’s logging level:

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``namespace ``=`` ``"teal"``, level ``=`` ``logger``::`[`TRACE`](https://daroczig.github.io/logger/reference/log_levels.html)`)`

3.  Setting an environment variable.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LEVEL ``=`` ``"TRACE"``)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``)`

Customizing `teal`’s logging level:

\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LEVEL ``=`` ``"TRACE"``)`\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`

4.  Setting an `option`.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`options`](https://rdrr.io/r/base/options.html)`(``teal.log_level ``=`` ``logger``::`[`TRACE`](https://daroczig.github.io/logger/reference/log_levels.html)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``)`

Customizing `teal`’s logging level:

\
[`options`](https://rdrr.io/r/base/options.html)`(``teal.log_level ``=`` ``logger``::`[`TRACE`](https://daroczig.github.io/logger/reference/log_levels.html)`)`\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`

Do keep in mind that packages in the `teal` framework register their
loggers upon library loading. Therefore, if you intend to alter the
default logging level via an option or a system environment variable,
ensure you modify the variable before loading the library.

Example below:

\
`# library(teal)`\
`# Sys.setenv(TEAL.LOG_LEVEL = "TRACE") # won't change the default`

\
`# Sys.setenv(TEAL.LOG_LEVEL = "TRACE")`\
`# library(teal)`\
`# will change the default because teal is attached after changing the variable`

Alternatively, you can change the options after loading a package and
then call
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)
with the appropriate namespace name to change the default of a single
package. E.g. this will change the defaults of `teal.logger`. Replace
`teal.logger` with the name of the package you want to change.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LEVEL ``=`` ``"TRACE"``)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``'teal.logger'``)`

For a more comprehensive understanding, consult the [`logger`
documentation](https://daroczig.github.io/logger/articles/customize_logger.html)
and the documentation for
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md).

## Customizing the Log Layout

When using
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md),
the default log layout for the new logger is
`[{level}] {format(time, \"%Y-%m-%d %H:%M:%OS4\")} pid:{pid} token:[{token}] {ans} {msg}`.You
can modify this behavior in four distinct ways:

1.  Using the `logger` interface.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``)`\
`logger``::`[`log_layout`](https://daroczig.github.io/logger/reference/log_layout.html)`(``"{level} {msg}"``, namespace ``=`` ``"my_namespace"``)`

Customizing `teal`’s logging layout:

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
`logger``::`[`log_layout`](https://daroczig.github.io/logger/reference/log_layout.html)`(``"{level} {msg}"``, namespace ``=`` ``"teal"``)`

2.  Utilizing the function argument of
    [`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md).

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``, layout ``=`` ``"{level} {msg}"``)`

Customizing `teal`’s logging layout:

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``namespace ``=`` ``"teal"``, layout ``=`` ``"{level} {msg}"``)`

3.  Setting an environment variable.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LAYOUT ``=`` ``"{level} {msg}"``)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``)`

Customizing `teal`’s logging layout:

\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LAYOUT ``=`` ``"{level} {msg}"``)`\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`

4.  Setting an `option`.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`options`](https://rdrr.io/r/base/options.html)`(``teal.log_layout ``=`` ``"{level} {msg}"``)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``"my_namespace"``)`

Customizing `teal`’s logging layout:

\
[`options`](https://rdrr.io/r/base/options.html)`(``teal.log_layout ``=`` ``"{level} {msg}"``)`\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`

Like changing the log level, remember that `teal` registers its logger
during library loading. Thus, if you aim to modify the default logging
layout via an option or a system environment variable, ensure you adjust
the variable prior to loading the library.

Example below:

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LAYOUT ``=`` ``"{level} {msg}"``)`` ``# won't change the default`

\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LAYOUT ``=`` ``"{level} {msg}"``)`\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
`# will change the default because teal is attached after changing the variable`

Alternatively, you can change the options after loading a package and
then call
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)
with the appropriate namespace name to change the default of a single
package. E.g. this will change the defaults of `teal.logger`. Replace
`teal.logger` with the name of the package you want to change.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`Sys.setenv`](https://rdrr.io/r/base/Sys.setenv.html)`(``TEAL.LOG_LAYOUT ``=`` ``"{level} {msg}"``)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``'teal.logger'``)`

For additional insights, consult the [`logger`
documentation](https://daroczig.github.io/logger/articles/customize_logger.html)
and the documentation for
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md).

## Customizing the Log Destination

By default, `teal.logger` sends logs to `stdout`. If you wish to alter
this behavior, you need to employ [`logger`’s
API](https://daroczig.github.io/logger/articles/customize_logger.html#delivering-log-records-to-their-destination-1).

For instance, to redirect `teal`’s logs to `stderr` using `logger`’s
API:

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
`logger``::`[`log_appender`](https://daroczig.github.io/logger/reference/log_appender.html)`(``logger``::`[`appender_stderr`](https://daroczig.github.io/logger/reference/appender_console.html)`, namespace ``=`` ``"teal"``)`

## Logging in Other `teal.X` Packages

Additional `teal.X` packages, such as `teal.data`, employ
[`register_logger()`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)
to enroll loggers in their namespace. Each package establishes a logger
in the namespace equivalent to the package name, e.g., `teal.data`
creates a logger in the `teal.data` namespace. A package initializes its
logger during package loading and utilizes default logging settings,
subject to modifications explained in the preceding sections.

## Example of Usage

Below is a minimal working example that demonstrates logging using
`teal`’s logging setup. The default `TEAL.LOG.LEVEL` is `"INFO"`,
implying that logs with a level above `level = 400` won’t appear in
`stdout`.

\
[`library`](https://rdrr.io/r/base/library.html)`(`[`teal.logger`](https://pharmaverse.github.io/teal.logger/)`)`\
[`register_logger`](https://pharmaverse.github.io/teal.logger/reference/register_logger.md)`(``namespace ``=`` ``"my_module"``)`\
\
`logger``::`[`log_error`](https://daroczig.github.io/logger/reference/log_level.html)`(``"This is an ERROR level log from my module"``, namespace ``=`` ``"my_module"``)`` ``# 200`\
`logger``::`[`log_warn`](https://daroczig.github.io/logger/reference/log_level.html)`(``"This is a WARN level log from my module"``, namespace ``=`` ``"my_module"``)`` ``# 300`\
`logger``::`[`log_success`](https://daroczig.github.io/logger/reference/log_level.html)`(``"This is a SUCCESS level log from my module"``, namespace ``=`` ``"my_module"``)`` ``# 350`\
`logger``::`[`log_info`](https://daroczig.github.io/logger/reference/log_level.html)`(``"This is an INFO level log from my module"``, namespace ``=`` ``"my_module"``)`` ``# 400`\
`logger``::`[`log_debug`](https://daroczig.github.io/logger/reference/log_level.html)`(``"This is a DEBUG level log from my module"``, namespace ``=`` ``"my_module"``)`` ``# 500`\
`logger``::`[`log_trace`](https://daroczig.github.io/logger/reference/log_level.html)`(``"This is a TRACE level log from my module"``, namespace ``=`` ``"my_module"``)`` ``# 600`
