# CLASP.Python Example - **show_usage_and_version**

## Summary

Simple example supporting ```--help``` and ```--version```.

## Source

```python
#!/usr/bin/env python

# examples/show_usage_and_version.py


# imports

import pyclasp as clasp

import sys

# constants

VERSION = [ 0, 0, 2 ]

INFO_LINES = (

    'CLASP.Python examples',
    ':version:',
    "Illustrates use of CLASP.Python's clasp.show_usage() and clasp.show_version() methods",
	'',
)

# Specify specifications, parse, and checking standard flags

specifications = (

    clasp.HelpFlag(),
    clasp.VersionFlag(),
)

args = clasp.parse(sys.argv, specifications)

if args.flag_is_specified('--help'):

    clasp.show_usage(specifications, exit_code=0, version=VERSION, stream=sys.stdout, info_lines=INFO_LINES)

if args.flag_is_specified('--version'):

    clasp.show_version(specifications, exit_code=0, version=VERSION, stream=sys.stdout)


# Check for any unrecognised flags or options

unused = args.get_first_unused_flag_or_option();
if (unused):

    sys.stderr.write("%s: unrecognised flag/option: %s\n" % (args.program_name, unused))

    sys.exit(1)


sys.stdout.write("no flags specified\n");

```

## Usage

### No arguments

If executed with no arguments

```
    python examples/show_usage_and_version.py
```

or (in a Unix shell):

```
    ./examples/show_usage_and_version.py
```

it gives the output:

```
no flags specified
```

### Show usage

If executed with the arguments

```
    python examples/show_usage_and_version.py --help
```

it gives the output:

```
CLASP.Python examples
show_usage_and_version.py 0.0.2
Illustrates use of CLASP.Python's show_usage() and show_version() methods

USAGE: show_usage_and_version.py [ ... flags and options ... ]

flags/options:

	--help
		Shows usage and terminates

	--version
		Shows version and terminates
```

### Show version

If executed with the arguments

```
    python examples/show_usage_and_version.py --version
```

it gives the output:

```
show_usage_and_version.py 0.0.2
```

### Unknown option

If executed with the arguments

```
    python examples/show_usage_and_version.py --unknown=value
```

it gives the output (on the standard error stream):

```
show_usage_and_version.py: unrecognised flag/option: --unknown=value
```

with an exit code of 1

