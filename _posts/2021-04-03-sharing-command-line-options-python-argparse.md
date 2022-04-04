---
title: Sharing Command-line Options in Python Argparse
author:
  name: Benjamin Kan
categories: [Software Engineering]
tags: [python, argparse]
pin: false
---

This is probably no big news that [argparse](https://docs.python.org/3/library/argparse.html) makes it easy to write
user-friendly command-line interfaces. It comes out-of-the-box and is therefore the standard tool if you create
a [CLI](https://en.wikipedia.org/wiki/CLI) tool in Python.

## Basic usage of argparse

The following snippet shows a basic usage example of _argparse_ with a single `param` argument that can be passed to
the command line.

```python
import argparse

def main(argv):
  print(argv.param)

if __name__ == '__main__':
  parser = argparse.ArgumentParser()
  parser.add_argument('--param', type=int, default=64,
                      help='The param value. Default is 64.')
  args = parser.parse_args()
  main(args)
```
{: file='argparse_example.py'}

This optional argument can then be used used by appending `--param VALUE` when executing script.

```console
$ python argparse_example.py --param 128
```

## Introducing subparsers

I recently used [subparsers](https://docs.python.org/3/library/argparse.html#sub-commands) for the first time that might not be
very commonly known. Many CLI tool's split up their functionality into a number of sub-commands. For instance, the `git` program
can invoke sub-commands like `git init`, `git clone`, or `git pull`. And this is exactly where subparsers come in handy.

### Basic usage of subparsers

The following code snippet shows a basic usage example of subparsers by defining a single command.

```python
import argparse

def command_main(argv):
    print(argv.param, argv.verbose)

if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument('--verbose', type=bool, default=True,
                        action=argparse.BooleanOptionalAction,
                        help='Enable or disable verbosity. Default is True')
    parser.set_defaults(func=lambda argv: parser.print_help())
    subparsers = parser.add_subparsers()

    command = subparsers.add_parser('command')
    command.add_argument('--param', type=int, default=64,
                         help='The param value. Default is 64.')
    command.set_defaults(func=command_main)

    args = parser.parse_args()
    args.func(args)
```
{: file='subparsers_example.py'}

This adds a single sub-command called `command` that has one optional `--param` parameter. Using the `parser.set_defaults(...)`
on the root parser, we define that the help page is printed when no command is given at all. Furthermore, we also define a
`--verbose` parameter, which needs to be specified **before** the command. Consequently, a usage example could look like the
following.

```console
$ python subparsers_example.py --no-verbose command --param 128
```

### Sharing arguments between subparsers

The same way as above, you can obviously add multiple commands. 

```python
import argparse

def init_main(argv):
    print(argv.param, argv.verbose)

def start_main(argv):
    print(argv.param, argv.verbose)

if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.set_defaults(func=lambda argv: parser.print_help())
    subparsers = parser.add_subparsers()

    init = subparsers.add_parser('init')
    init.add_argument('--param', type=str, required=True,
                      help='The required param value.')
    init.set_defaults(func=init_main)

    start = subparsers.add_parser('start')
    start.add_argument('--param', type=str, required=True,
                       help='The required param value.')
    start.set_defaults(func=start_main)

    args = parser.parse_args()
    args.func(args)
```
{: file='shared_args_example.py'}

This basically enables you to have multiple entry points to your script. Great!

However, as you can see, we ended up with redundantly defining a single param used in both commands twice. Well, you might think
we could simply move it to the root `parser`. However, this would have the effect that the user needs to define this parameter
**before** the command, such as `python shared_args_example.py --param value init`. But what if you would like to have these params
**after** the command as in `python shared_args_example.py init --param value`?

Fortunately, this is possible by using a shared argument parser as shown in the following snipped.

```python
subparsers = parser.add_subparsers()

shared_parser = argparse.ArgumentParser(add_help=False)
shared_parser.add_argument('--param', type=str, required=True,
                            help='The required param value.')

init = subparsers.add_parser('init', parents=[shared_parser])
init.set_defaults(func=init_main)

start = subparsers.add_parser('start', parents=[shared_parser])
start.set_defaults(func=start_main)
```

By defining a separate argument parser via `argparse.ArgumentParser(add_help=False)`, you can define common parameters and share
these between different subparser commands using the `parents` param.

## Putting everything together

Finally, putting everything togehter, the following can be used as a copy-paste **template** for any new script or CLI tool
that you are building using Python.

```python
import argparse

def first_command(argv):
    pass

def second_command(argv):
    pass

if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument('--root', type=bool, default=False,
                        action=argparse.BooleanOptionalAction,
                        help='Enable or disable the root param. Default is False')
    parser.set_defaults(func=lambda argv: parser.print_help())
    subparsers = parser.add_subparsers()

    shared_parser = argparse.ArgumentParser(add_help=False)
    shared_parser.add_argument('--shared', type=str, required=True,
                               help='The required shared param value.')

    cmd1 = subparsers.add_parser('first-command', parents=[shared_parser])
    cmd1.add_argument('--local-int', type=int, default=64,
                      help='The local int param value. Default is 64.')
    cmd1.set_defaults(func=first_command)

    cmd2 = subparsers.add_parser('second-command', parents=[shared_parser])
    cmd2.add_argument('--local-float', type=float, default=1.23,
                      help='The local float param value. Default is 1.23.')
    cmd2.set_defaults(func=second_command)

    args = parser.parse_args()
    args.func(args)
```
{: file='cli_template.py'}

It follows a usage example of the template above.

```console
$ python cli_template.py --no-root second-command --shared value --local-float 2.34
```

I hope this turns out to be useful to you some day.