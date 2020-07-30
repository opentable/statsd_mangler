# Purpose
This tool is for normalizing metric names as they go out to statsd. It takes a
series of search and replace regexes and modifies metric names as they are
emitted. The intent is for this to listen on port 8125 and receive metrics and
forward them after changing the metric names.

# Usage
Simply write a config file as described below and run:

```
statsd_mangler config.toml
```

# Configuration
The configuration is written in toml. An example is below:

```
[listen]
port = 8125

[destination]
host = "127.0.0.1"
port = 8126

[log]
level = "DEBUG"

[[patterns]]
search = '^foo(.*)'
replace = '\1abc'

[[patterns]]
search = '^bar(.*)'
replace = '\1abc'
```

The listen section is just a port. It will listen on that port for statsd metrics.

The destination section is where it will forward metrics

The patterns are an array of search an replace regexes which can use references
to matches in the search.
