# xsnippet

Simple script to extract snippets from text file(s) and write to other files.

## Usage

	xsnippet.sh todir [src ...]

## Steps taken in script

1. Concatenate the `src`s, the marked up source codes from which to extract snippets;
2. Search for all lines matching the `TAGPATTERN` (as showin in the next section) and get the tag names, each denoted by `tagname`;
3. Extract snippet enclosed by a pair of begin/end tag and write snippet to file `tofile/tagname`.


## Detailed instruction on markup

> Copied from `xsnippet.sh:show_help`

### Markup format (sed regex)

```regex
^# *<snippet-\(begin\|end\) \([^ \t>]\+\)>$
```

### Example use case

The marked up source code, denoted as "src.py":

```python
#!/usr/bin/env python

# <snippet-begin xxx>
# <snippet-begin yyy>
def f():
    print('f')
# <snippet-end xxx>

def g():
    print('g')
# <snippet-end yyy>

# <snippet-begin xxx>
def h():
    print('h')

# <snippet-end xxx>

def abc():
    pass
```

Commands (bash) and results:

```
$ ls
$ xsnippet.sh . src.py
Warning: reentrant tag "xxx"
$ ls
xxx  yyy
$ cat xxx
def f():
    print('f')
def h():
    print('h')

$ cat yyy
def f():
    print('f')

def g():
    print('g')
$ 
```
