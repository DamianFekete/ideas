http://python-future.org/compatible_idioms.html

https://github.com/PythonCharmers/python-future

# Cheat Sheet: Writing Python 2-3 compatible code — Python-Future  documentation


[Python-Future][3] 

* **Copyright (c):** 2013-2015 Python Charmers Pty Ltd, Australia.
* **Author:** Ed Schofield.
* **Licence:** Creative Commons Attribution.

A PDF version is here: 

This notebook shows you idioms for writing future-proof code that is compatible with both versions of Python: 2 and 3. It accompanies Ed Schofield’s talk at PyCon AU 2014, “Writing 2/3 compatible code”. (The video is here: [http://www.youtube.com/watch?v=KOqk8j11aAI&t=10m14s][181].)

Minimum versions:

* Python 2: 2.6+
* Python 3: 3.3+

## Setup

The imports below refer to these `pip`-installable packages on PyPI:

```python
    import future        # pip install future
    import builtins      # pip install future
    import past          # pip install future
    import six           # pip install six

```
The following scripts are also `pip`-installable:

```python
    futurize             # pip install future
    pasteurize           # pip install future

```
See  and  for more information.

## Essential syntax differences

### print

```python
    # Python 2 only:
    print 'Hello'

    # Python 2 and 3:
    print('Hello')

```
To print multiple strings, import `print_function` to prevent Py2 from interpreting it as a tuple:

```python
    # Python 2 only:
    print 'Hello', 'Guido'

    # Python 2 and 3:
    from __future__ import print_function    # (at top of module)

    print('Hello', 'Guido')

    # Python 2 only:
    print >> sys.stderr, 'Hello'

    # Python 2 and 3:
    from __future__ import print_function

    print('Hello', file=sys.stderr)

    # Python 2 only:
    print 'Hello',

    # Python 2 and 3:
    from __future__ import print_function

    print('Hello', end='')

```
### Raising exceptions

```python
    # Python 2 only:
    raise ValueError, "dodgy value"

    # Python 2 and 3:
    raise ValueError("dodgy value")

```
Raising exceptions with a traceback:

```python
    # Python 2 only:
    traceback = sys.exc_info()[2]
    raise ValueError, "dodgy value", traceback

    # Python 3 only:
    raise ValueError("dodgy value").with_traceback()

    # Python 2 and 3: option 1
    from six import reraise as raise_
    # or
    from future.utils import raise_

    traceback = sys.exc_info()[2]
    raise_(ValueError, "dodgy value", traceback)

    # Python 2 and 3: option 2
    from future.utils import raise_with_traceback

    raise_with_traceback(ValueError("dodgy value"))

```
Exception chaining (PEP 3134):

```python
    # Setup:
    class DatabaseError(Exception):
        pass

    # Python 3 only
    class FileDatabase:
        def __init__(self, filename):
            try:
                self.file = open(filename)
            except IOError as exc:
                raise DatabaseError('failed to open') from exc

    # Python 2 and 3:
    from future.utils import raise_from

    class FileDatabase:
        def __init__(self, filename):
            try:
                self.file = open(filename)
            except IOError as exc:
                raise_from(DatabaseError('failed to open'), exc)

    # Testing the above:
    try:
        fd = FileDatabase('non_existent_file.txt')
    except Exception as e:
        assert isinstance(e.__cause__, IOError)    # FileNotFoundError on Py3.3+ inherits from IOError

```
### Catching exceptions

```python
    # Python 2 only:
    try:
        ...
    except ValueError, e:
        ...

    # Python 2 and 3:
    try:
        ...
    except ValueError as e:
        ...

```
### Division

Integer division (rounding down):

```python
    # Python 2 only:
    assert 2 / 3 == 0

    # Python 2 and 3:
    assert 2 // 3 == 0

```
“True division” (float division):

```python
    # Python 3 only:
    assert 3 / 2 == 1.5

    # Python 2 and 3:
    from __future__ import division    # (at top of module)

    assert 3 / 2 == 1.5

```
“Old division” (i.e. compatible with Py2 behaviour):

```python
    # Python 2 only:
    a = b / c            # with any types

    # Python 2 and 3:
    from past.utils import old_div

    a = old_div(b, c)    # always same as / on Py2

```
### Long integers

Short integers are gone in Python 3 and `long` has become `int` (without the trailing `L` in the `repr`).

```python
    # Python 2 only
    k = 9223372036854775808L

    # Python 2 and 3:
    k = 9223372036854775808

    # Python 2 only
    bigint = 1L

    # Python 2 and 3
    from builtins import int
    bigint = int(1)

```
To test whether a value is an integer (of any kind):

```python
    # Python 2 only:
    if isinstance(x, (int, long)):
        ...

    # Python 3 only:
    if isinstance(x, int):
        ...

    # Python 2 and 3: option 1
    from builtins import int    # subclass of long on Py2

    if isinstance(x, int):             # matches both int and long on Py2
        ...

    # Python 2 and 3: option 2
    from past.builtins import long

    if isinstance(x, (int, long)):
        ...

```
### Octal constants

```python
    0644     # Python 2 only

    0o644    # Python 2 and 3

```
### Backtick repr

```python
    `x`      # Python 2 only

    repr(x)  # Python 2 and 3

```
### Metaclasses

```python
    class BaseForm(object):
        pass

    class FormType(type):
        pass

    # Python 2 only:
    class Form(BaseForm):
        __metaclass__ = FormType
        pass

    # Python 3 only:
    class Form(BaseForm, metaclass=FormType):
        pass

    # Python 2 and 3:
    from six import with_metaclass
    # or
    from future.utils import with_metaclass

    class Form(with_metaclass(FormType, BaseForm)):
        pass

```
## Strings and bytes

### Unicode (text) string literals

If you are upgrading an existing Python 2 codebase, it may be preferable to mark up all string literals as unicode explicitly with `u` prefixes:

```python
    # Python 2 only
    s1 = 'The Zen of Python'
    s2 = u'???????????????n'

    # Python 2 and 3
    s1 = u'The Zen of Python'
    s2 = u'???????????????n'

```
The `futurize` and `python-modernize` tools do not currently offer an option to do this automatically.

If you are writing code for a new project or new codebase, you can use this idiom to make all string literals in a module unicode strings:

```python
    # Python 2 and 3
    from __future__ import unicode_literals    # at top of module

    s1 = 'The Zen of Python'
    s2 = '???????????????n'

```
See  for more discussion on which style to use.

### Byte-string literals

```python
    # Python 2 only
    s = 'This must be a byte-string'

    # Python 2 and 3
    s = b'This must be a byte-string'

```
To loop over a byte-string with possible high-bit characters, obtaining each character as a byte-string of length 1:

```python
    # Python 2 only:
    for bytechar in 'byte-string with high-bit chars like xf9':
        ...

    # Python 3 only:
    for myint in b'byte-string with high-bit chars like xf9':
        bytechar = bytes([myint])

    # Python 2 and 3:
    from builtins import bytes
    for myint in bytes(b'byte-string with high-bit chars like xf9'):
        bytechar = bytes([myint])

```
As an alternative, `chr()` and `.encode('latin-1')` can be used to convert an int into a 1-char byte string:

```python
    # Python 3 only:
    for myint in b'byte-string with high-bit chars like xf9':
        char = chr(myint)    # returns a unicode string
        bytechar = char.encode('latin-1')

    # Python 2 and 3:
    from builtins import bytes, chr
    for myint in bytes(b'byte-string with high-bit chars like xf9'):
        char = chr(myint)    # returns a unicode string
        bytechar = char.encode('latin-1')    # forces returning a byte str

```
### basestring

```python
    # Python 2 only:
    a = u'abc'
    b = 'def'
    assert (isinstance(a, basestring) and isinstance(b, basestring))

    # Python 2 and 3: alternative 1
    from past.builtins import basestring    # pip install future

    a = u'abc'
    b = b'def'
    assert (isinstance(a, basestring) and isinstance(b, basestring))

    # Python 2 and 3: alternative 2: refactor the code to avoid considering
    # byte-strings as strings.

    from builtins import str
    a = u'abc'
    b = b'def'
    c = b.decode()
    assert isinstance(a, str) and isinstance(c, str)
    # ...

```
### unicode

```python
    # Python 2 only:
    templates = [u"blog/blog_post_detail_%s.html" % unicode(slug)]

    # Python 2 and 3: alternative 1
    from builtins import str
    templates = [u"blog/blog_post_detail_%s.html" % str(slug)]

    # Python 2 and 3: alternative 2
    from builtins import str as text
    templates = [u"blog/blog_post_detail_%s.html" % text(slug)]

```
### StringIO

```python
    # Python 2 only:
    from StringIO import StringIO
    # or:
    from cStringIO import StringIO

    # Python 2 and 3:
    from io import BytesIO     # for handling byte strings
    from io import StringIO    # for handling unicode strings

```
## Imports relative to a package

Suppose the package is:

```python
    mypackage/
        __init__.py
        submodule1.py
        submodule2.py

```
and the code below is in `submodule1.py`:

```python
    # Python 2 only:
    import submodule2

    # Python 2 and 3:
    from . import submodule2

    # Python 2 and 3:
    # To make Py2 code safer (more like Py3) by preventing
    # implicit relative imports, you can also add this to the top:
    from __future__ import absolute_import

```
## Dictionaries

```python
    heights = {'Fred': 175, 'Anne': 166, 'Joe': 192}

```
### Iterating through `dict` keys/values/items

Iterable dict keys:

```python
    # Python 2 only:
    for key in heights.iterkeys():
        ...

    # Python 2 and 3:
    for key in heights:
        ...

```
Iterable dict values:

```python
    # Python 2 only:
    for value in heights.itervalues():
        ...

    # Idiomatic Python 3
    for value in heights.values():    # extra memory overhead on Py2
        ...

    # Python 2 and 3: option 1
    from builtins import dict

    heights = dict(Fred=175, Anne=166, Joe=192)
    for key in heights.values():    # efficient on Py2 and Py3
        ...

    # Python 2 and 3: option 2
    from builtins import itervalues
    # or
    from six import itervalues

    for key in itervalues(heights):
        ...

```
Iterable dict items:

```python
    # Python 2 only:
    for (key, value) in heights.iteritems():
        ...

    # Python 2 and 3: option 1
    for (key, value) in heights.items():    # inefficient on Py2
        ...

    # Python 2 and 3: option 2
    from future.utils import viewitems

    for (key, value) in viewitems(heights):   # also behaves like a set
        ...

    # Python 2 and 3: option 3
    from future.utils import iteritems
    # or
    from six import iteritems

    for (key, value) in iteritems(heights):
        ...

```
### dict keys/values/items as a list

dict keys as a list:

```python
    # Python 2 only:
    keylist = heights.keys()
    assert isinstance(keylist, list)

    # Python 2 and 3:
    keylist = list(heights)
    assert isinstance(keylist, list)

```
dict values as a list:

```python
    # Python 2 only:
    heights = {'Fred': 175, 'Anne': 166, 'Joe': 192}
    valuelist = heights.values()
    assert isinstance(valuelist, list)

    # Python 2 and 3: option 1
    valuelist = list(heights.values())    # inefficient on Py2

    # Python 2 and 3: option 2
    from builtins import dict

    heights = dict(Fred=175, Anne=166, Joe=192)
    valuelist = list(heights.values())

    # Python 2 and 3: option 3
    from future.utils import listvalues

    valuelist = listvalues(heights)

    # Python 2 and 3: option 4
    from future.utils import itervalues
    # or
    from six import itervalues

    valuelist = list(itervalues(heights))

```
dict items as a list:

```python
    # Python 2 and 3: option 1
    itemlist = list(heights.items())    # inefficient on Py2

    # Python 2 and 3: option 2
    from future.utils import listitems

    itemlist = listitems(heights)

    # Python 2 and 3: option 3
    from future.utils import iteritems
    # or
    from six import iteritems

    itemlist = list(iteritems(heights))

```
## Custom class behaviour

### Custom iterators

```python
    # Python 2 only
    class Upper(object):
        def __init__(self, iterable):
            self._iter = iter(iterable)
        def next(self):          # Py2-style
            return self._iter.next().upper()
        def __iter__(self):
            return self

    itr = Upper('hello')
    assert itr.next() == 'H'     # Py2-style
    assert list(itr) == list('ELLO')

    # Python 2 and 3: option 1
    from builtins import object

    class Upper(object):
        def __init__(self, iterable):
            self._iter = iter(iterable)
        def __next__(self):      # Py3-style iterator interface
            return next(self._iter).upper()  # builtin next() function calls
        def __iter__(self):
            return self

    itr = Upper('hello')
    assert next(itr) == 'H'      # compatible style
    assert list(itr) == list('ELLO')

    # Python 2 and 3: option 2
    from future.utils import implements_iterator

    @implements_iterator
    class Upper(object):
        def __init__(self, iterable):
            self._iter = iter(iterable)
        def __next__(self):                  # Py3-style iterator interface
            return next(self._iter).upper()  # builtin next() function calls
        def __iter__(self):
            return self

    itr = Upper('hello')
    assert next(itr) == 'H'
    assert list(itr) == list('ELLO')

```
### Custom `__str__` methods

```python
    # Python 2 only:
    class MyClass(object):
        def __unicode__(self):
            return 'Unicode string: u5b54u5b50'
        def __str__(self):
            return unicode(self).encode('utf-8')

    a = MyClass()
    print(a)    # prints encoded string

    # Python 2 and 3:
    from future.utils import python_2_unicode_compatible

    @python_2_unicode_compatible
    class MyClass(object):
        def __str__(self):
            return u'Unicode string: u5b54u5b50'

    a = MyClass()
    print(a)    # prints string encoded as utf-8 on Py2

    Unicode string: ??

```
### Custom `__nonzero__` vs `__bool__` method:

```python
    # Python 2 only:
    class AllOrNothing(object):
        def __init__(self, l):
            self.l = l
        def __nonzero__(self):
            return all(self.l)

    container = AllOrNothing([0, 100, 200])
    assert not bool(container)

    # Python 2 and 3:
    from builtins import object

    class AllOrNothing(object):
        def __init__(self, l):
            self.l = l
        def __bool__(self):
            return all(self.l)

    container = AllOrNothing([0, 100, 200])
    assert not bool(container)

```
## Lists versus iterators

### xrange

```python
    # Python 2 only:
    for i in xrange(10**8):
        ...

    # Python 2 and 3: forward-compatible
    from builtins import range
    for i in range(10**8):
        ...

    # Python 2 and 3: backward-compatible
    from past.builtins import xrange
    for i in xrange(10**8):
        ...

```
### range

```python
    # Python 2 only
    mylist = range(5)
    assert mylist == [0, 1, 2, 3, 4]

    # Python 2 and 3: forward-compatible: option 1
    mylist = list(range(5))            # copies memory on Py2
    assert mylist == [0, 1, 2, 3, 4]

    # Python 2 and 3: forward-compatible: option 2
    from builtins import range

    mylist = list(range(5))
    assert mylist == [0, 1, 2, 3, 4]

    # Python 2 and 3: option 3
    from future.utils import lrange

    mylist = lrange(5)
    assert mylist == [0, 1, 2, 3, 4]

    # Python 2 and 3: backward compatible
    from past.builtins import range

    mylist = range(5)
    assert mylist == [0, 1, 2, 3, 4]

```
### map

```python
    # Python 2 only:
    mynewlist = map(f, myoldlist)
    assert mynewlist == [f(x) for x in myoldlist]

    # Python 2 and 3: option 1
    # Idiomatic Py3, but inefficient on Py2
    mynewlist = list(map(f, myoldlist))
    assert mynewlist == [f(x) for x in myoldlist]

    # Python 2 and 3: option 2
    from builtins import map

    mynewlist = list(map(f, myoldlist))
    assert mynewlist == [f(x) for x in myoldlist]

    # Python 2 and 3: option 3
    try:
        import itertools.imap as map
    except ImportError:
        pass

    mynewlist = list(map(f, myoldlist))    # inefficient on Py2
    assert mynewlist == [f(x) for x in myoldlist]

    # Python 2 and 3: option 4
    from future.utils import lmap

    mynewlist = lmap(f, myoldlist)
    assert mynewlist == [f(x) for x in myoldlist]

    # Python 2 and 3: option 5
    from past.builtins import map

    mynewlist = map(f, myoldlist)
    assert mynewlist == [f(x) for x in myoldlist]

```
### imap

```python
    # Python 2 only:
    from itertools import imap

    myiter = imap(func, myoldlist)
    assert isinstance(myiter, iter)

    # Python 3 only:
    myiter = map(func, myoldlist)
    assert isinstance(myiter, iter)

    # Python 2 and 3: option 1
    from builtins import map

    myiter = map(func, myoldlist)
    assert isinstance(myiter, iter)

    # Python 2 and 3: option 2
    try:
        import itertools.imap as map
    except ImportError:
        pass

    myiter = map(func, myoldlist)
    assert isinstance(myiter, iter)

```
### zip, izip

As above with `zip` and `itertools.izip`.

### filter, ifilter

As above with `filter` and `itertools.ifilter` too.

## Other builtins

### File IO with open()

```python
    # Python 2 only
    f = open('myfile.txt')
    data = f.read()              # as a byte string
    text = data.decode('utf-8')

    # Python 2 and 3: alternative 1
    from io import open
    f = open('myfile.txt', 'rb')
    data = f.read()              # as bytes
    text = data.decode('utf-8')  # unicode, not bytes

    # Python 2 and 3: alternative 2
    from io import open
    f = open('myfile.txt', encoding='utf-8')
    text = f.read()    # unicode, not bytes

```
### reduce()

```python
    # Python 2 only:
    assert reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]) == 1+2+3+4+5

    # Python 2 and 3:
    from functools import reduce

    assert reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]) == 1+2+3+4+5

```
### raw_input()

```python
    # Python 2 only:
    name = raw_input('What is your name? ')
    assert isinstance(name, str)    # native str

    # Python 2 and 3:
    from builtins import input

    name = input('What is your name? ')
    assert isinstance(name, str)    # native str on Py2 and Py3

```
### input()

```python
    # Python 2 only:
    input("Type something safe please: ")

    # Python 2 and 3
    from builtins import input
    eval(input("Type something safe please: "))

```
Warning: using either of these is **unsafe** with untrusted input.

### file()

```python
    # Python 2 only:
    f = file(pathname)

    # Python 2 and 3:
    f = open(pathname)

    # But preferably, use this:
    from io import open
    f = open(pathname, 'rb')   # if f.read() should return bytes
    # or
    f = open(pathname, 'rt')   # if f.read() should return unicode text

```
### exec

```python
    # Python 2 only:
    exec 'x = 10'

    # Python 2 and 3:
    exec('x = 10')

    # Python 2 only:
    g = globals()
    exec 'x = 10' in g

    # Python 2 and 3:
    g = globals()
    exec('x = 10', g)

    # Python 2 only:
    l = locals()
    exec 'x = 10' in g, l

    # Python 2 and 3:
    exec('x = 10', g, l)

```
### execfile()

```python
    # Python 2 only:
    execfile('myfile.py')

    # Python 2 and 3: alternative 1
    from past.builtins import execfile

    execfile('myfile.py')

    # Python 2 and 3: alternative 2
    exec(compile(open('myfile.py').read()))

    # This can sometimes cause this:
    #     SyntaxError: function ... uses import * and bare exec ...
    # See https://github.com/PythonCharmers/python-future/issues/37

```
### unichr()

```python
    # Python 2 only:
    assert unichr(8364) == '€'

    # Python 3 only:
    assert chr(8364) == '€'

    # Python 2 and 3:
    from builtins import chr
    assert chr(8364) == '€'

```
### intern()

```python
    # Python 2 only:
    intern('mystring')

    # Python 3 only:
    from sys import intern
    intern('mystring')

    # Python 2 and 3: alternative 1
    from past.builtins import intern
    intern('mystring')

    # Python 2 and 3: alternative 2
    from six.moves import intern
    intern('mystring')

    # Python 2 and 3: alternative 3
    from future.standard_library import install_aliases
    install_aliases()
    from sys import intern
    intern('mystring')

    # Python 2 and 3: alternative 2
    try:
        from sys import intern
    except ImportError:
        pass
    intern('mystring')

```
### apply()

```python
    args = ('a', 'b')
    kwargs = {'kwarg1': True}

    # Python 2 only:
    apply(f, args, kwargs)

    # Python 2 and 3: alternative 1
    f(*args, **kwargs)

    # Python 2 and 3: alternative 2
    from past.builtins import apply
    apply(f, args, kwargs)

```
### chr()

```python
    # Python 2 only:
    assert chr(64) == b'@'
    assert chr(200) == b'xc8'

    # Python 3 only: option 1
    assert chr(64).encode('latin-1') == b'@'
    assert chr(0xc8).encode('latin-1') == b'xc8'

    # Python 2 and 3: option 1
    from builtins import chr

    assert chr(64).encode('latin-1') == b'@'
    assert chr(0xc8).encode('latin-1') == b'xc8'

    # Python 3 only: option 2
    assert bytes([64]) == b'@'
    assert bytes([0xc8]) == b'xc8'

    # Python 2 and 3: option 2
    from builtins import bytes

    assert bytes([64]) == b'@'
    assert bytes([0xc8]) == b'xc8'

```
### cmp()

```python
    # Python 2 only:
    assert cmp('a', 'b') < 0 and cmp('b', 'a') > 0 and cmp('c', 'c') == 0

    # Python 2 and 3: alternative 1
    from past.builtins import cmp
    assert cmp('a', 'b') < 0 and cmp('b', 'a') > 0 and cmp('c', 'c') == 0

    # Python 2 and 3: alternative 2
    cmp = lambda(x, y): (x > y) - (x < y)
    assert cmp('a', 'b') < 0 and cmp('b', 'a') > 0 and cmp('c', 'c') == 0

```
### reload()

```python
    # Python 2 only:
    reload(mymodule)

    # Python 2 and 3
    from imp import reload
    reload(mymodule)

```
## Standard library

### dbm modules

```python
    # Python 2 only
    import anydbm
    import whichdb
    import dbm
    import dumbdbm
    import gdbm

    # Python 2 and 3: alternative 1
    from future import standard_library
    standard_library.install_aliases()

    import dbm
    import dbm.ndbm
    import dbm.dumb
    import dbm.gnu

    # Python 2 and 3: alternative 2
    from future.moves import dbm
    from future.moves.dbm import dumb
    from future.moves.dbm import ndbm
    from future.moves.dbm import gnu

    # Python 2 and 3: alternative 3
    from six.moves import dbm_gnu
    # (others not supported)

```
### commands / subprocess modules

```python
    # Python 2 only
    from commands import getoutput, getstatusoutput

    # Python 2 and 3
    from future import standard_library
    standard_library.install_aliases()

    from subprocess import getoutput, getstatusoutput

```
### subprocess.check_output()

```python
    # Python 2.7 and above
    from subprocess import check_output

    # Python 2.6 and above: alternative 1
    from future.moves.subprocess import check_output

    # Python 2.6 and above: alternative 2
    from future import standard_library
    standard_library.install_aliases()

    from subprocess import check_output

```
### collections: Counter and OrderedDict

```python
    # Python 2.7 and above
    from collections import Counter, OrderedDict

    # Python 2.6 and above: alternative 1
    from future.moves.collections import Counter, OrderedDict

    # Python 2.6 and above: alternative 2
    from future import standard_library
    standard_library.install_aliases()

    from collections import Counter, OrderedDict

```
### StringIO module

```python
    # Python 2 only
    from StringIO import StringIO
    from cStringIO import StringIO

    # Python 2 and 3
    from io import BytesIO
    # and refactor StringIO() calls to BytesIO() if passing byte-strings

```
### http module

```python
    # Python 2 only:
    import httplib
    import Cookie
    import cookielib
    import BaseHTTPServer
    import SimpleHTTPServer
    import CGIHttpServer

    # Python 2 and 3 (after ``pip install future``):
    import http.client
    import http.cookies
    import http.cookiejar
    import http.server

```
### xmlrpc module

```python
    # Python 2 only:
    import DocXMLRPCServer
    import SimpleXMLRPCServer

    # Python 2 and 3 (after ``pip install future``):
    import xmlrpc.server

    # Python 2 only:
    import xmlrpclib

    # Python 2 and 3 (after ``pip install future``):
    import xmlrpc.client

```
### html escaping and entities

```python
    # Python 2 and 3:
    from cgi import escape

    # Safer (Python 2 and 3, after ``pip install future``):
    from html import escape

    # Python 2 only:
    from htmlentitydefs import codepoint2name, entitydefs, name2codepoint

    # Python 2 and 3 (after ``pip install future``):
    from html.entities import codepoint2name, entitydefs, name2codepoint

```
### html parsing

```python
    # Python 2 only:
    from HTMLParser import HTMLParser

    # Python 2 and 3 (after ``pip install future``)
    from html.parser import HTMLParser

    # Python 2 and 3 (alternative 2):
    from future.moves.html.parser import HTMLParser

```
### urllib module

`urllib` is the hardest module to use from Python 2/3 compatible code. You may like to use Requests () instead.

```python
    # Python 2 only:
    from urlparse import urlparse
    from urllib import urlencode
    from urllib2 import urlopen, Request, HTTPError

    # Python 3 only:
    from urllib.parse import urlparse, urlencode
    from urllib.request import urlopen, Request
    from urllib.error import HTTPError

    # Python 2 and 3: easiest option
    from future.standard_library import install_aliases
    install_aliases()

    from urllib.parse import urlparse, urlencode
    from urllib.request import urlopen, Request
    from urllib.error import HTTPError

    # Python 2 and 3: alternative 2
    from future.standard_library import hooks

    with hooks():
        from urllib.parse import urlparse, urlencode
        from urllib.request import urlopen, Request
        from urllib.error import HTTPError

    # Python 2 and 3: alternative 3
    from future.moves.urllib.parse import urlparse, urlencode
    from future.moves.urllib.request import urlopen, Request
    from future.moves.urllib.error import HTTPError
    # or
    from six.moves.urllib.parse import urlparse, urlencode
    from six.moves.urllib.request import urlopen
    from six.moves.urllib.error import HTTPError

    # Python 2 and 3: alternative 4
    try:
        from urllib.parse import urlparse, urlencode
        from urllib.request import urlopen, Request
        from urllib.error import HTTPError
    except ImportError:
        from urlparse import urlparse
        from urllib import urlencode
        from urllib2 import urlopen, Request, HTTPError

```
### Tkinter

```python
    # Python 2 only:
    import Tkinter
    import Dialog
    import FileDialog
    import ScrolledText
    import SimpleDialog
    import Tix
    import Tkconstants
    import Tkdnd
    import tkColorChooser
    import tkCommonDialog
    import tkFileDialog
    import tkFont
    import tkMessageBox
    import tkSimpleDialog
    import ttk

    # Python 2 and 3 (after ``pip install future``):
    import tkinter
    import tkinter.dialog
    import tkinter.filedialog
    import tkinter.scrolledtext
    import tkinter.simpledialog
    import tkinter.tix
    import tkinter.constants
    import tkinter.dnd
    import tkinter.colorchooser
    import tkinter.commondialog
    import tkinter.filedialog
    import tkinter.font
    import tkinter.messagebox
    import tkinter.simpledialog
    import tkinter.ttk

```
### socketserver

```python
    # Python 2 only:
    import SocketServer

    # Python 2 and 3 (after ``pip install future``):
    import socketserver

```
### copy_reg, copyreg

```python
    # Python 2 only:
    import copy_reg

    # Python 2 and 3 (after ``pip install future``):
    import copyreg

```
### configparser

```python
    # Python 2 only:
    from ConfigParser import ConfigParser

    # Python 2 and 3 (after ``pip install future``):
    from configparser import ConfigParser

```
### queue

```python
    # Python 2 only:
    from Queue import Queue, heapq, deque

    # Python 2 and 3 (after ``pip install future``):
    from queue import Queue, heapq, deque

```
### repr, reprlib

```python
    # Python 2 only:
    from repr import aRepr, repr

    # Python 2 and 3 (after ``pip install future``):
    from reprlib import aRepr, repr

```
### UserDict, UserList, UserString

```python
    # Python 2 only:
    from UserDict import UserDict
    from UserList import UserList
    from UserString import UserString

    # Python 3 only:
    from collections import UserDict, UserList, UserString

    # Python 2 and 3: alternative 1
    from future.moves.collections import UserDict, UserList, UserString

    # Python 2 and 3: alternative 2
    from six.moves import UserDict, UserList, UserString

    # Python 2 and 3: alternative 3
    from future.standard_library import install_aliases
    install_aliases()
    from collections import UserDict, UserList, UserString

```
### itertools: filterfalse, zip_longest

```python
    # Python 2 only:
    from itertools import ifilterfalse, izip_longest

    # Python 3 only:
    from itertools import filterfalse, zip_longest

    # Python 2 and 3: alternative 1
    from future.moves.itertools import filterfalse, zip_longest

    # Python 2 and 3: alternative 2
    from six.moves import filterfalse, zip_longest

    # Python 2 and 3: alternative 3
    from future.standard_library import install_aliases
    install_aliases()
    from itertools import filterfalse, zip_longest

```
Back to top

© Copyright 2013-2015, Python Charmers Pty Ltd, Australia.  

[1]: https://s3.amazonaws.com/github/ribbons/forkme_right_orange_ff7600.png
[2]: http://python-future.org/_static/python-future-logo-textless-transparent.png
[3]: index.html
[4]: overview.html
[5]: faq.html
[6]: whatsnew.html
[7]: whatsnew.html#what-s-new-in-version-0-15-2-2015-09-11
[8]: whatsnew.html#what-s-new-in-version-0-15-1-2015-09-09
[9]: whatsnew.html#what-s-new-in-version-0-15-0-2015-07-25
[10]: whatsnew.html#previous-versions
[11]: overview.html#features
[12]: overview.html#code-examples
[13]: overview.html#automatic-conversion-to-py2-3-compatible-code
[14]: overview.html#futurize-2-to-both
[15]: overview.html#automatic-translation
[16]: overview.html#licensing
[17]: overview.html#next-steps
[18]: quickstart.html
[19]: quickstart.html#installation
[20]: quickstart.html#if-you-are-writing-code-from-scratch
[21]: quickstart.html#to-convert-existing-python-3-code
[22]: quickstart.html#to-convert-existing-python-2-code
[23]: quickstart.html#standard-library-reorganization
[24]: quickstart.html#python-2-only-dependencies
[25]: quickstart.html#next-steps
[27]: imports.html
[28]: imports.html#future-imports
[29]: imports.html#imports-of-builtins
[30]: imports.html#implicit-imports
[31]: imports.html#explicit-imports
[32]: imports.html#standard-library-imports
[33]: imports.html#direct-imports
[34]: imports.html#aliased-imports
[35]: imports.html#external-standard-library-backports
[36]: imports.html#included-full-backports
[37]: imports.html#using-python-2-only-dependencies-on-python-3
[38]: imports.html#should-i-import-unicode-literals
[39]: imports.html#benefits
[40]: imports.html#drawbacks
[41]: imports.html#others-perspectives
[42]: imports.html#next-steps
[43]: what_else.html
[44]: what_else.html#bytes
[45]: what_else.html#str
[46]: what_else.html#dict
[47]: what_else.html#memory-efficiency-and-alternatives
[48]: what_else.html#int
[49]: what_else.html#isinstance
[50]: what_else.html#passing-data-to-from-python-2-libraries
[51]: what_else.html#native-string-type
[52]: what_else.html#open
[53]: what_else.html#custom-str-methods
[54]: what_else.html#custom-iterators
[55]: what_else.html#binding-a-method-to-a-class
[56]: what_else.html#metaclasses
[57]: automatic_conversion.html
[58]: automatic_conversion.html#futurize-py2-to-py2-3
[59]: automatic_conversion.html#stage-1-safe-fixes
[60]: automatic_conversion.html#stage-2-py3-style-code-with-wrappers-for-py2
[61]: automatic_conversion.html#separating-text-from-bytes
[62]: automatic_conversion.html#post-conversion
[63]: automatic_conversion.html#futurize-quick-start-guide
[64]: automatic_conversion.html#step-0-setup
[65]: automatic_conversion.html#step-1-modern-py2-code
[66]: automatic_conversion.html#step-2-working-py3-code-that-still-supports-py2
[67]: automatic_conversion.html#pasteurize-py3-to-py2-3
[68]: automatic_conversion.html#known-limitations
[69]: faq.html#who-is-this-for
[70]: faq.html#why-upgrade-to-python-3
[71]: faq.html#porting-philosophy
[72]: faq.html#why-write-python-3-style-code
[73]: faq.html#can-t-i-just-roll-my-own-py2-3-compatibility-layer
[74]: faq.html#what-inspired-this-project
[75]: faq.html#maturity
[76]: faq.html#how-well-has-it-been-tested
[77]: faq.html#is-the-api-stable
[78]: faq.html#relationship-between-python-future-and-other-compatibility-tools
[79]: faq.html#how-does-this-relate-to-2to3
[80]: faq.html#can-i-maintain-a-python-2-codebase-and-use-2to3-to-automatically-convert-to-python-3-in-the-setup-script
[81]: faq.html#what-is-the-relationship-between-future-and-six
[82]: faq.html#what-is-the-relationship-between-python-future-and-python-modernize
[83]: faq.html#platform-and-version-support
[84]: faq.html#which-versions-of-python-does-python-future-support
[85]: faq.html#support
[86]: faq.html#is-there-a-mailing-list
[87]: faq.html#contributing
[88]: faq.html#can-i-help
[89]: faq.html#where-is-the-repo
[90]: stdlib_incompatibilities.html
[91]: stdlib_incompatibilities.html#array-array
[92]: stdlib_incompatibilities.html#array-array-read
[93]: stdlib_incompatibilities.html#base64-decodebytes-and-base64-encodebytes
[94]: stdlib_incompatibilities.html#re-ascii
[95]: stdlib_incompatibilities.html#struct-pack
[96]: older_interfaces.html
[97]: older_interfaces.html#context-manager-for-import-hooks
[98]: older_interfaces.html#future-moves-interface
[99]: older_interfaces.html#comparing-future-moves-and-six-moves
[100]: older_interfaces.html#import-and-from-import-functions
[101]: older_interfaces.html#install-hooks-call
[102]: changelog.html
[103]: changelog.html#changes-in-version-0-14-3-2014-12-15
[104]: changelog.html#changes-in-version-0-14-2-2014-11-21
[105]: changelog.html#changes-in-version-0-14-1-2014-10-02
[106]: changelog.html#changes-in-version-0-14-0-2014-10-02
[107]: changelog.html#bug-fixes
[108]: changelog.html#internal-cleanups
[109]: changelog.html#deprecations
[110]: changelog.html#changes-in-version-0-13-1-2014-09-23
[111]: changelog.html#changes-in-version-0-13-0-2014-08-13
[112]: changelog.html#id1
[113]: changelog.html#new-features
[114]: changelog.html#id2
[115]: changelog.html#changes-in-version-0-12-4-2014-07-18
[116]: changelog.html#changes-in-version-0-12-3-2014-06-19
[117]: changelog.html#changes-in-version-0-12-2-2014-05-25
[118]: changelog.html#changes-in-version-0-12-1-2014-05-14
[119]: changelog.html#changes-in-version-0-12-0-2014-05-06
[120]: changelog.html#more-robust-standard-library-import-hooks
[121]: changelog.html#newobject-base-object-defines-fallback-py2-compatible-special-methods
[122]: changelog.html#past-builtins-module-improved
[123]: changelog.html#surrogateescape-error-handler
[124]: changelog.html#newlist-type
[125]: changelog.html#listvalues-and-listitems
[126]: changelog.html#tests
[127]: changelog.html#refactoring-of-future-standard-library-future-backports
[128]: changelog.html#backported-http-server-and-urllib-modules
[129]: changelog.html#internal-refactoring
[130]: changelog.html#id3
[131]: changelog.html#changes-in-version-0-11-4-2014-05-25
[132]: changelog.html#changes-in-version-0-11-3-2014-02-27
[133]: changelog.html#improved-compatibility-with-requests
[134]: changelog.html#conversion-scripts-explicitly-install-import-hooks
[135]: changelog.html#futurize-script-no-longer-adds-unicode-literals-by-default
[136]: changelog.html#changes-in-version-0-11-2014-01-28
[137]: changelog.html#past-package
[138]: changelog.html#auto-translation-of-python-2-modules-upon-import
[139]: changelog.html#separate-pasteurize-script
[140]: changelog.html#pow
[141]: changelog.html#input-no-longer-disabled-globally-on-py2
[142]: changelog.html#deprecated-feature-auto-installation-of-standard-library-import-hooks
[143]: changelog.html#internal-changes
[144]: changelog.html#changes-in-version-0-10-2-2014-01-11
[145]: changelog.html#new-context-manager-interface-to-standard-library-hooks
[146]: changelog.html#changes-in-version-0-10-0-2013-12-02
[147]: changelog.html#backported-dict-type
[148]: changelog.html#utility-functions-raise-and-exec
[149]: changelog.html#bugfixes
[150]: changelog.html#changes-in-version-0-9-2013-11-06
[151]: changelog.html#isinstance-checks-are-supported-natively-with-backported-types
[152]: changelog.html#futurize-minimal-imports-by-default
[153]: changelog.html#looser-type-checking-for-the-backported-str-object
[154]: changelog.html#suspend-hooks-context-manager-added-to-future-standard-library
[155]: changelog.html#changes-in-version-0-8-2013-10-28
[156]: changelog.html#python-2-6-support
[157]: changelog.html#unused-modules-removed
[158]: changelog.html#isinstance-added-to-future-builtins-v0-8-2
[159]: changelog.html#summary-of-all-changes
[160]: credits.html
[161]: credits.html#licence
[162]: credits.html#sponsor
[163]: credits.html#authors
[164]: credits.html#development-lead
[165]: credits.html#patches
[166]: credits.html#suggestions-and-feedback
[167]: credits.html#other-credits
[168]: reference.html
[169]: reference.html#module-future.builtins
[170]: reference.html#module-future.types
[171]: reference.html#for-more-information
[172]: reference.html#range
[173]: reference.html#super
[174]: reference.html#round
[175]: reference.html#module-future.standard_library
[176]: reference.html#limitations
[177]: reference.html#module-future.utils
[178]: reference.html#module-past.builtins
[179]: reference.html#module-past.types
[180]: http://python-future.org
[181]: http://www.youtube.com/watch?v=KOqk8j11aAI&t=10m14s
  
