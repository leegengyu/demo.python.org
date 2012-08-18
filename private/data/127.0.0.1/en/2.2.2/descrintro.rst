Unifying types and classes in Python 2.2
========================================

**Python Version: 2.2.2** 

(For a newer version of this tutorial, see `Python 2.2.3 <../../2.2.3/descrintro.html>`_)

*Guido van Rossum* 

**This paper is an incomplete draft.  I am soliciting feedback.
If you find any problems, please write me at `guido@python.org <mailto:guido@python.org>`_.**

Table of Contents
~~~~~~~~~~~~~~~~~

- `Change Log <#changes>`_
- `Introduction <#introduction>`_
- `Subclassing built-in types <#subclassing>`_
- `Built-in types as factory functions <#factories>`_
- `Introspecting instances of built-in types <#introspection>`_
- `Static methods and class methods <#staticmethods>`_
- `Properties: attributes defined by get/set methods <#property>`_
- `Method resolution order <#mro>`_
- `Cooperative methods and "super" <#cooperation>`_
- `Overriding the __new__ method <#__new__>`_
- `Metaclasses <#metaclasses>`_
- `Backwards incompatibilities <#incompatibilities>`_
- `References <#references>`_

    Change Log

    Changes since the original Python
    2.2 version of this tutorial:

    - Don't scare people by suggesting classmethod may go away. (4-Apr-2002)

    Introduction

    Python 2.2 introduces the first phase of "type/class unification".
    This is a series of changes to Python intended to remove most of the
    differences between built-in types and user-defined classes.  Perhaps
    the most obvious one is the restriction against using built-in types
    (such as the type of lists and dictionaries) as a base class in a
    class statement.

    This is one of the biggest changes to Python ever, and yet it can
    be done with very few backwards incompatibilities.  The changes are
    described in minute detail in a series of `PEPs <#references>`_ (Python Enhancement Proposals).  PEPs are not designed to be
    tutorials, and the PEPs describing the type/class unification are
    sometimes hard to read.  They also aren't finished yet.  That's where
    this paper comes in: it introduces the key elements of the type/class
    unification for the average Python programmer.

    A bit of terminology: "classic Python" refers to Python 2.1 (and
    its patch releases such as 2.1.1) or
    earlier versions, while "classic classes" refer to classes defined
    with a class statement that does not have a built-in object amongst
    its bases: either because it has no bases, or because all of its bases
    are classic classes themselves - applying the definition recursively.

    Classic classes are still a special category in Python 2.2.
    Eventually they will be totally unified with types, but because of
    additional backwards incompatibilities, this will be done after 2.2 is
    released (maybe not before Python 3.0).  I'll try to say "type" when I
    mean a built-in type, and "class" when I'm referring to a classic
    class or something that could be either; if it wouldn't be clear from
    the context which interpretation is meant, I'll try to be explicit,
    using "classic class" or "class or type".

    Subclassing built-in types

    Let's start with the juiciest bit: you can subtype built-in types
    like dictionaries and lists.  All you need is a name for a base class
    that is a built-in type and you're in business.

    There's a new built-in name, "dict", for the type of dictionaries.
    (In version 2.2b1 and before, this was called "dictionary"; while in
    general I don't like abbreviations, "dictionary" was just too long to
    type, and we've been saying "dict" for years.)

    This is really just sugar, since there are already two other ways to
    name this type: type({}) and (after importing the types
    module) types.DictType (and a third, types.DictionaryType).  But now
    that types play a more central role, it seems appropriate to have
    built-in names for the types that you're likely to encounter.

    Here's an example of a simple dict subclass, which provides a
    "default value" that is returned when a missing key is requested:

    .. code-block::

        class defaultdict(dict):

                def __init__(self, default=None):
                    dict.__init__(self)
                    self.default = default

                def __getitem__(self, key):
                    try:
                        return dict.__getitem__(self, key)
                    except KeyError:
                        return self.default

    This example shows a few things.  The __init__() method extends the
    dict.__init__() method.  Like __init__() methods are wont to do,
    it has a different argument list than the base class __init__()
    method.  Likewise, the __getitem__() method extends the base class
    __getitem__() method.

    The __getitem__() method could also be written as follows, using
    the new "key in dict" test introduced in Python 2.2:

    .. code-block::

        def __getitem__(self, key):
                    if key in self:
                        return dict.__getitem__(self, key)
                    else:
                        return self.default

    I believe that this version is less efficient, because it does the
    key lookup twice.  The exception would be when we expect that the
    requested key is almost never in the dictionary: then setting up the
    try/except statement is more expensive than the failing "key in self"
    test.

    To be complete, the get() method should probably also be
    extended, to make it use the same default as __getitem__():

    .. code-block::

        def get(self, key, *args):
                    if not args:
                        args = (self.default,)
                    return dict.get(self, key, *args)

    (Although this function is declared with a variable-length argument
    list, it really should only be called with one or two arguments; if
    more are passed, the base class method call will raise a TypeError
    exception.)

    We're not restricted to extending methods defined on the
    base class.  Here's a useful method that does something similar to
    update(), but keeps existing values rather than overwriting them with
    new values if a key exists in both dictionaries:

    .. code-block::

        def merge(self, other):
                    for key in other:
                        if key not in self:
                            self[key] = other[key]

    This uses the new "key not in dict" test as well as the new "for
    key in dict:" to iterate efficiently (without making a copy of the
    list of keys) over all keys in a dictionary.  It doesn't require the
    other argument to be a defaultdict or even a dictionary: any mapping
    object that supports "for key in other" and other[key] will do.

    Here's the new type at work:

    .. code-block::

        >>> print defaultdict               # show our type
            <;class '__main__.defaultdict'>
            >>> print type(defaultdict)         # its metatype
            <;type 'type'>
            >>> a = defaultdict(default=0.0)    # create an instance
            >>> print a                         # show the instance
            {}
            >>> print type(a)                   # show its type
            <;class '__main__.defaultdict'>
            >>> print a.__class__               # show its class
            <;class '__main__.defaultdict'>
            >>> print type(a) is a.__class__    # its type is its class
            >>> a[1] = 3.25                     # modify the instance
            >>> print a                         # show the new value
            {1: 3.25}
            >>> print a[1]                      # show the new item
            3.25
            >>> print a[0]                      # a non-existant item
            0.0
            >>> a.merge({1:100, 2:200})         # use a dictionary method
            >>> print a                         # show the result
            {1: 3.25, 2: 200}

    We can also use the new type in contexts where classic only allows
    "real" dictionaries, such as the locals/globals dictionaries for the
    exec statement or the built-in function eval():

    .. code-block::

        >>> print a.keys()
            [1, 2]
            >>> exec "x = 3; print x" in a
            >>> print a.keys()
            ['__builtins__', 1, 2, 'x']
            >>> print a['x']

    However, our __getitem__() method is not used for variable access
    by the interpreter:

    .. code-block::

        >>> exec "print foo" in a
            Traceback (most recent call last):
              File "<;stdin>", line 1, in ?
              File "<;string>", line 1, in ?
            NameError: name 'foo' is not defined

    Why doesn't this print 0.0?  The interpreter uses an internal
    function to access the dictionary, which bypasses our __getitem__()
    override.  I admit that this can be a problem (although it is
    *only* a problem in this context, when a dict subclass is
    used as a locals/globals dictionary); it remains to be seen if I can
    fix this without compromising performance in the common case.

    Now we'll see that defaultdict instances have dynamic instance
    variables, just like classic classes:

    .. code-block::

        >>> a.default = -1
            >>> print a["noway"]
            -1
            >>> a.default = -1000
            >>> print a["noway"]
            -1000
            >>> print a.__dict__.keys()
            ['default']
            >>> a.x1 = 100
            >>> a.x2 = 200
            >>> print a.x1
            100
            >>> print a.__dict__.keys()
            ['default', 'x2', 'x1']
            >>> print a.__dict__
            {'default': -1000, 'x2': 200, 'x1': 100}

    This is not always what you want; in particular, using a separate
    dictionary to hold a single instance variable doubles the memory used
    by a defaultdict instance compared to using a regular dictionary!
    There's a way to avoid this:

    .. code-block::

        class defaultdict2(dict):

                __slots__ = ['default']

                def __init__(self, default=None):
                *...(like before)...*

    The __slots__ declaration takes a list of instance variables, and
    reserves space in the instance for exactly these in the instance.
    When __slots__ is used, other instance variables cannot be assigned
    to:

    .. code-block::

        >>> a = defaultdict2(default=0.0)
            >>> a[1]
            0.0
            >>> a.default = -1
            >>> a[1]
            -1
            >>> a.x1 = 1
            Traceback (most recent call last):
              File "<;stdin>", line 1, in ?
            AttributeError: 'defaultdict2' object has no attribute 'x1'

    Some noteworthy tidbits and warnings about __slots__:

    - An undefined slot variable will raise AttributeError as expected.  (Note that in Python 2.2b2 and earlier, slot variables had the value None by default, and "deleting" them restores this default value.)
    - You cannot use a class attribute to define a default value for an instance variable defined by __slots__.  The __slots__ declaration creates a class attribute containing a descriptor for each slot, and setting a class attribute to a default value would overwrite this descriptor.
    - There's no check to prevent name conflicts between the slots defined in a class and the slots defined in its base classes.  If a class defines a slot that's also defined in a base class, the instance variable defined by the base class slot is inaccessible (except by retrieving its descriptor directly from the base class; this could be used to rename it).  Doing this renders the meaning of your program undefined; a check to prevent this may be added in the future.
    - Instances of a class that uses __slots__ don't have a __dict__ (unless a base class defines a __dict__); but instances of derived classes of it do have a __dict__, unless their class also uses __slots__.
    - You can define an object with no instance variables and no __dict__ by using  __slots__ = [].
    - You cannot use slots with "variable-length" built-in types as base class.  Variable-length built-in types are long, str and tuple.
    - A class using __slots__ does not support weak references to its instances, unless one of the strings in the __slots__ list equals "__weakref__".  (In Python 2.3, this feature has been extended to "__dict__")
    - The __slots__ variable doesn't have to be a list; any non-string that can be iterated over will do, and the values returned by the iteration are used as the slot names.  In particular, a dictionary can be used. You can also use a single string, to declare a single slot. However, in the future, an additional meaning may be assigned to using a dictionary, for example, the dictionary values may be used to restrict the type of an instance variable or provide a doc string; the effect of using something that's not a list renders the meaning of your program undefined.

    Note that while in general operator overloading works just as for
    classic classes, there are some differences.  (The biggest one is the
    lack of support for __coerce__; new-style classes should always use
    the new-style numeric API, which passes the other operand uncoerced to
    the __add__ and __radd__ methods, etc.)

    There's a new way of overriding attribute access.  The __getattr__
    hook, if defined, works the same way as it does for classic classes:
    it is only called if the regular way of searching for the
    attribute doesn't find it.  But you can now also override
    __getattribute__, a new operation that is called for *all*
    attribute references.

    When overriding __getattribute__, bear in mind that it is easy to
    cause infinite recursion: whenever __getattribute__ references an
    attribute of self (even self.__dict__!), it is called recursively.
    (This is similar to __setattr__, which gets called for all attribute
    assignments; __getattr__ can also suffer from this when it is
    carelessly written and references a non-existent attribute of self.)

    The correct way to get any attribute from self inside
    __getattribute__ is to call the base class's __getattribute__ method,
    in the same way any method that overrides a base class method can call
    the base class method: Base.__getattribute__(self, name).  (See also
    the discussion of `super() <#cooperation>`_ below if you want
    to be correct in a multiple inheritance world.)

    Here's an example of overriding __getattribute__ (really extending
    it, since the overriding method calls the base class method):

    .. code-block::

        class C(object):
                def __getattribute__(self, name):
                    print "accessing %r.%s" % (self, name)
                    return object.__getattribute__(self, name)

    A note about __setattr__: sometimes attributes are not stored in
    self.__dict__ (for example when using __slots__ or properties, or when
    using a built-in base class).  The
    same pattern as for __getattribute__ applies, where you call the base
    class __setattr__ to do the actual work.  Here's an example:

    .. code-block::

        class C(object):
                def __setattr__(self, name, value):
                    if hasattr(self, name):
                        raise AttributeError, "attributes are write-once"
                    object.__setattr__(self, name, value)

    C++ programmers may find it useful to realize that this form of
    subtyping in Python is implemented very similarly to
    single-inheritance subclassing in C++, with __class__ in the role of
    the vtable.

    There's much more that could be explained (like the __metaclass__
    declaration, and the __new__ method), but most of that is pretty
    esoteric.  See `below <#__new__>`_ if you're interested.

    I'll end with a list of caveats:

    - You can use multiple inheritance, but you can't multiply inherit from different built-in types (for example, you can't create a type that inherits from both the built-in dict and list types).  This is a permanent restriction; it would require too many changes to Python's object implementation to lift it.  However, you can create mix-in classes by inheriting from "object".  This is a new built-in, naming the featureless base type of all built-in types under the new system.
    - When using multiple inheritance, you can mix classic classes and built-in types (or types derived from built-in types) in the list of base classes.  (This is new in Python 2.2b2; in earlier versions you couldn't.)
    - See also the general `bugs in 2.2 list <../bugs>`_.

    Built-in types as factory functions

    The previous section showed that an instance of the built-in subtype
    defaultdict can be created by calling defaultdict().  This is
    expected, because this also works for classic classes.  But here's a
    new feature: built-in base types themselves can also be instantiated
    by calling the type directly.

    For several built-in types, there are already factory functions
    named after the type in classic Python, for example str() and int().
    I've changed these built-ins so that they are now names for the
    corresponding types.  While this changes the type of these names from
    built-in function to built-in type, I don't expect that this will create
    backward compatibility problems: I've made sure that the types can be
    called with exactly the same argument lists as the former functions.
    (They can also generally be called without arguments, producing an
    object with a suitable default value, such as zero or empty; this is
    new.)

    These are the affected built-ins:

    - int([number_or_string[, base_number]])
    - long([number_or_string])
    - float([number_or_string])
    - complex([number_or_string[, imag_number]])
    - str([object])
    - unicode([string[, encoding_string]])
    - tuple([iterable])
    - list([iterable])
    - type(object) or type(name_string, bases_tuple, methods_dict)

    The signature of type() requires an explanation: traditionally,
    type(x) returns the type of object x, and this usage is still
    supported.  However, type(name, bases, methods) is a new usage that
    creates a brand new type object.  (This gets into `metaclass programming <#metaclasses>`_, and I won't go into
    this further here except to note that this signature is the same as
    that used by the Don Beaudry hook of metaclass fame.)

    There are also a few new built-ins that follow the same pattern.
    These have been described above or will be described below:

    - dict([mapping_or_iterable]) - return a new dictionary; the optional argument must be either a mapping whose items are copied, or a sequence of 2-tuples of length 2 giving the (key, value) pairs to be inserted into the new dictionary
    - object([...]) - return a new featureless object; arguments are ignored
    - classmethod(function) - see `below <#staticmethods>`_
    - staticmethod(function) - see `below <#staticmethods>`_
    - super(class_or_type[, instance]) - see `below <#cooperation>`_
    - property([fget[, fset[, fdel[, doc]]]]) - see `below <#property>`_

    The purpose of this change is twofold.  First, this makes it
    convenient to use any of these types as a base class in a class
    statement.  Second, it makes testing for a specific type a little
    easier: rather than writing type(x) is type(0), you can now write
    isinstance(x, int).

    Which reminds me.  The second argument of isinstance() may now be a
    tuple of classes or types.  For example, isinstance(x, (int, long))
    returns true when x is an int or a long (or an instance of a subclass
    of either of those types), and similarly isinstance(x, (str, unicode))
    tests for a string of either variety.  We didn't do this to isclass().

    Introspecting instances of built-in types

    For instances of built-in types (and for new-style classes in
    general), x.__class__ is now the same as type(x):

    .. code-block::

        >>> type([])
            <;type 'list'>
            >>> [].__class__
            <;type 'list'>
            >>> list
            <;type 'list'>
            >>> isinstance([], list)
            >>> isinstance([], dict)
            >>> isinstance([], object)

    In classic Python, the method names of lists were available as the
    __methods__ attribute of list objects, with the same effect as using
    the built-in dir() function:

    .. code-block::

        Python 2.1 (#30, Apr 18 2001, 00:47:18) 
            [GCC egcs-2.91.66 19990314/Linux (egcs-1.1.2 release)] on linux2
            Type "copyright", "credits" or "license" for more information.
            >>> [].__methods__
            ['append', 'count', 'extend', 'index', 'insert', 'pop',
            'remove', 'reverse', 'sort']
            >>> dir([])
            ['append', 'count', 'extend', 'index', 'insert', 'pop',
            'remove', 'reverse', 'sort']

    Under the new proposal, the __methods__ attribute no longer exists:

    .. code-block::

        Python 2.2c1 (#803, Dec 13 2001, 23:06:05) 
            [GCC egcs-2.91.66 19990314/Linux (egcs-1.1.2 release)] on linux2
            Type "copyright", "credits" or "license" for more information.
            >>> [].__methods__
            Traceback (most recent call last):
              File "<;stdin>", line 1, in ?
            AttributeError: 'list' object has no attribute '__methods__'

    Instead, you can get the same information from the dir() function,
    which gives more information:

    .. code-block::

        >>> dir([])
            ['__add__', '__class__', '__contains__', '__delattr__',
            '__delitem__', '__eq__', '__ge__', '__getattribute__',
            '__getitem__', '__getslice__', '__gt__', '__hash__', '__iadd__',
            '__imul__', '__init__', '__le__', '__len__', '__lt__', '__mul__',
            '__ne__', '__new__', '__reduce__', '__repr__', '__rmul__',
            '__setattr__', '__setitem__', '__setslice__', '__str__', 'append',
            'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse',
            'sort']

    The new dir() gives more information than the old one: in addition
    to the names of instance variables and regular methods, it also shows
    the methods that are normally invoked through special notations, like
    __iadd__ (+=), __len__ (len), __ne__ (!=).

    More about the new dir() function:

    - dir() on an instance (classic or new-style) shows the instance variables as well as the methods and class attributes defined by the instance's class and all its base classes.
    - dir() on a class (classic or new-style) shows the contents of the __dict__ of the class and all its base classes.  It does not show class attributes that are defined by a metaclass.
    - dir() on a module shows the contents of the module's __dict__. (This is unchanged.)
    - dir() without arguments shows the caller's local variables. (Again, unchanged.)
    - There's a new C API that implements the dir() function: PyObject_Dir().
    - There are more details; in particular, for objects that override __dict__ or __class__, these are honored, and for backwards compatibility, __members__ and __methods__ are honored if they are defined.

    You can use a method of a built-in type as an "unbound method":

    .. code-block::

        >>> a = ['tic', 'tac']
            >>> list.__len__(a)          # same as len(a)
            >>> list.append(a, 'toe')    # same as a.append('toe')
            >>> a
            ['tic', 'tac', 'toe']

    This is just like using an unbound method of a user-defined class
    - and similarly, it's mostly useful from inside a subclass
    method, to call the corresponding base class method.

    Unlike user-defined classes, you cannot change built-in types:
    attempts to assign an attribute of a built-in type raises a TypeError,
    and their __dict__ is a read-only proxy object.  The restriction on
    attribute assignment is lifted for new-style user-defined classes,
    including subclasses of built-in types; however even those have a
    read-only __dict__ proxy, and you must use attribute assignment to
    replace or add a method of a new-style class.  Example session:

    .. code-block::

        >>> list.append
            <;method 'append' of 'list' objects>
            >>> list.append = list.append
            Traceback (most recent call last):
              File "<;stdin>", line 1, in ?
            TypeError: can't set attributes of built-in/extension type 'list'
            >>> list.answer = 42
            Traceback (most recent call last):
              File "<;stdin>", line 1, in ?
            TypeError: can't set attributes of built-in/extension type 'list'
            >>> list.__dict__['append']
            <;method 'append' of 'list' objects>
            >>> list.__dict__['answer'] = 42
            Traceback (most recent call last):
              File "<;stdin>", line 1, in ?
            TypeError: object does not support item assignment
            >>> class L(list):
            ...     pass
            >>> L.append = list.append
            >>> L.answer = 42
            >>> L.__dict__['answer']
            42
            >>> L.__dict__['answer'] = 42
            Traceback (most recent call last):
              File "<;stdin>", line 1, in ?
            TypeError: object does not support item assignment

    For the curious: there are two reasons why changing built-in
    classes is disallowed.
    First, it would be too easy to break an invariant of a
    built-in type that is relied upon elsewhere, either by the standard
    library, or by the run-time code.  Second, when Python is embedded in
    another application that creates multiple Python interpreters, the
    built-in class objects (being statically allocated data structures)
    are shared between all interpreters; thus, code running in one
    interpreter might wreak havoc on another interpreter, which is a
    no-no.

    Static methods and class methods

    The new descriptor API makes it possible to add static methods
    and class methods.  Static methods are easy to describe: they behave
    pretty much like static methods in C++ or Java.  Here's an example:

    .. code-block::

        class C:

                def foo(x, y):
                    print "staticmethod", x, y
                foo = staticmethod(foo)

            C.foo(1, 2)
            c = C()
            c.foo(1, 2)

    Both the call C.foo(1, 2) and the call c.foo(1, 2) call foo() with
    two arguments, and print "staticmethod 1 2".  No "self" is declared in
    the definition of foo(), and no instance is required in the call.  If
    an instance is used, it is only used to find the class that defines
    the static method. This works for classic and new classes!

    The line "foo = staticmethod(foo)" in the class statement is the
    crucial element: this makes foo() a static method.  The built-in
    staticmethod() wraps its function argument in a special kind of
    descriptor whose __get__() method returns the original function
    unchanged.

    More on __get__ methods: in Python 2.2, the magic of binding
    methods to instances (even for classic classes!) is done through the
    __get__ method of the object found in the class.  The __get__ method
    for regular function objects returns a bound method object; the
    __get__ method for staticfunction objects returns the underlying
    function.  If a class attribute has no __get__ method, it is never
    bound to an instance, or in other words there's a default __get__
    operation that returns the object unchanged; this is how simple class
    variables (for example numerical values) are handled.

    Class methods use a similar pattern to declare methods that receive
    an implicit first argument that is the *class* for which they are
    invoked.  This has no C++ or Java equivalent, and is not quite the
    same as what class methods are in Smalltalk, but may serve a similar
    purpose.  (Python also has real `metaclasses <#metaclasses>`_, and perhaps methods defined in a metaclass have more
    right to the name "class method"; but I expect that most programmers
    won't be using metaclasses.)  Here's an example:

    .. code-block::

        class C:

                def foo(cls, y):
                    print "classmethod", cls, y
                foo = classmethod(foo)

            C.foo(1)
            c = C()
            c.foo(1)

    Both the call C.foo(1) and the call c.foo(1) end up calling foo()
    with *two* arguments, and print "classmethod __main__.C 1".  The first
    argument of foo() is implied, and it is the class, even if the method
    was invoked via an instance.  Now let's continue the example:

    .. code-block::

        class D(C):
                pass

            D.foo(1)
            d = D()
            d.foo(1)

    This prints "classmethod __main__.D 1" both times; in other words,
    the class passed as the first argument of foo() is the class involved
    in the call, not the class involved in the definition of foo().

    But notice this:

    .. code-block::

        class E(C):
                def foo(cls, y): # override C.foo
                    print "E.foo() called"
                    C.foo(y)
                foo = classmethod(foo)

            E.foo(1)
            e = E()
            e.foo(1)

    In this example, the call to C.foo() from E.foo() will see class C
    as its first argument, not class E.  This is to be expected, since the
    call specifies the class C.  But it stresses the difference between
    these class methods and methods defined in `metaclasses <#metaclasses>`_, where an upcall to a metamethod would pass the
    target class as an explicit first argument.  (If you don't understand
    this, don't worry, you're not alone. :-)

    Properties: attributes managed by get/set methods

    Properties are a neat way to implement attributes whose
    *usage* resembles attribute access, but whose
    *implementation* uses method calls.  These are sometimes known
    as "managed attributes".  In prior Python versions, you could only do
    this by overriding __getattr__ and __setattr__; but overriding
    __setattr__ slows down *all* attribute assignments considerably,
    and overriding __getattr__ is always a bit tricky to get right.
    Properties let you do this painlessly, without having to override
    __getattr__ or __setattr__.

    I'll show an example first.  Let's define a class with an attribute
    x defined by a pair of methods, getx() and setx():

    .. code-block::

        class C(object):

                def __init__(self):
                    self.__x = 0

                def getx(self):
                    return self.__x

                def setx(self, x):
                    if x <; 0: x = 0
                    self.__x = x

                x = property(getx, setx)

    Here's a small demonstration:

    .. code-block::

        >>> a = C()
            >>> a.x = 10
            >>> print a.x
            10
            >>> a.x = -10
            >>> print a.x
            >>> a.setx(12)
            >>> print a.getx()
            12

    The full signature is property(fget=None, fset=None, fdel=None,
    doc=None).  The fget, fset and fdel arguments are the methods called
    when the attribute is get, set or deleted.  If any of these three is
    unspecified or None, the corresponding operation will raise an
    AttributeError exception.  The fourth argument is the doc string for
    the attribute; it can be retrieved from the class as the following
    example shows:

    .. code-block::

        >>> class C(object):
            ...     def getx(self): return 42
            ...     x = property(getx, doc="hello")
            >>> C.x.__doc__
            'hello'

    Things to notice about property() (all advanced material except the
    first one):

    - **Properties do not work for classic classes**, but you don't get a clear error when you try this.  Your get method will be called, so it appears to work, but upon attribute assignment, a classic class instance will simply set the value in its __dict__ without calling the property's set method, and after that, the property's get method won't be called either.  (You could override __setattr__ to fix this, but it would be prohibitively expensive.)    As far as property() is concerned, its fget, fset and fdel arguments are functions, not methods - they are passed an explicit reference to the object as their first argument.  Since property() is typically used in a class statement, this is correct (the methods really *are* function objects at the time when property() is called) but you can still think of them as methods - as long as you aren't using a `metaclass <#metaclasses>`_ that does special things to methods.
    - The get method won't be called when the property is accessed as a class attribute (C.x) instead of as an instance attribute (C().x). If you want to override the __get__ operation for properties when used as a class attribute, you can subclass property - it is a new-style type itself - to extend its __get__ method, or you can define a descriptor type from scratch by creating a new-style class that defines __get__, __set__ and __delete__ methods.

    Method resolution order

    With multiple inheritance comes the question of method resolution
    order: the order in which a class and its bases are searched
    looking for a method of a given name.

    In classic Python, the rule is given by the following recursive
    function, also known as the left-to-right depth-first rule:

    .. code-block::

        def classic_lookup(cls, name):
                "Look up name in cls and its base classes."
                if cls.__dict__.has_key(name):
                    return cls.__dict__[name]
                for base in cls.__bases__:
                    try:
                        return classic_lookup(base, name)
                    except AttributeError:
                        pass
                raise AttributeError, name

    In Python 2.2, I've decided to adopt a different lookup rule for
    new-style classes.  (The rule for classic classes remains unchanged
    for backwards compatibility considerations; eventually all classes
    will be new-style classes and then the distinction will go away.)  I'll
    try to explain what's wrong with the classic rule first.

    The problem with the classic rule becomes apparent when we consider
    a "diamond diagram":

    .. code-block::

        class A:
                        ^ ^  def save(self): ...
                       /   \
                      /     \
                     /       \
                    /         \
                class B     class C:
                    ^         ^  def save(self): ...
                     \       /
                      \     /
                       \   /
                        \ /
                      class D

    Arrows point from a subtype to its base type(s).  This particular
    diagram means B and C derive from A, and D derives from B and C (and
    hence also, indirectly, from A).

    Assume that C overrides the method save(), which is defined in the
    base A.  (C.save() probably calls A.save() and then saves some of its
    own state.)  B and D don't override save().  When we invoke save() on
    a D instance, which method is called?  According to the classic lookup
    rule, A.save() is called, ignoring C.save()!

    This is not good.  It probably breaks C (its state doesn't get
    saved), defeating the whole purpose of inheriting from C in the first
    place.

    Why wasn't this a problem in classic Python?  Diamond diagrams are
    rarely found in classic Python class hierarchies.  Most class
    hierarchies use single inheritance, and multiple inheritance is
    usually limited to mix-in classes.  In fact, the problem shown here
    is probably the reason why multiple inheritance is unpopular in
    classic Python!

    Why will this be a problem in the new system?  The 'object' type at
    the top of the type hierarchy defines a number of methods that can
    usefully be extended by subtypes, for example __getattribute__() and
    __setattr__().

    (Aside: the __getattr__() method is not really the implementation
    for the get-attribute operation; it is a hook that only gets invoked
    when an attribute cannot be found by normal means.  This has often
    been cited as a shortcoming - some class designs have a legitimate
    need for a get-attribute method that gets called for *all*
    attribute references, and this problem is solved now by making
    __getattribute__() available.  But then this method has to
    be able to invoke the default implementation somehow.  The most
    natural way is to make the default implementation available as
    object.__getattribute__(self, name).)

    Thus, a classic class hierarchy like this:

    .. code-block::

        class B     class C:
                    ^         ^  __setattr__()
                     \       /
                      \     /
                       \   /
                        \ /
                      class D

    will change into a diamond diagram under the new system:

    .. code-block::

        object:
                        ^ ^  __setattr__()
                       /   \
                      /     \
                     /       \
                    /         \
                class B     class C:
                    ^         ^  __setattr__()
                     \       /
                      \     /
                       \   /
                        \ /
                      class D

    and while in the original diagram C.__setattr__() is invoked, under
    the new system with the classic lookup rule, object.__setattr__()
    would be invoked!

    Fortunately, there's a lookup rule that's better.  It's a bit
    difficult to explain, but it does the right thing in the diamond
    diagram, and it is the same as the classic lookup rule when there are
    no diamonds in the inheritance graph (when it is a tree).

    The new lookup rule constructs a list of all classes in the
    inheritance diagram in the order in which they will be searched.  This
    construction is done when the class is defined, to save time.  To
    explain the new lookup rule, let's first consider what such a list
    would look like for the classic lookup rule.  Note that in the
    presence of diamonds the classic lookup visits some classes multiple
    times.  For example, in the ABCD diamond diagram above, the classic
    lookup rule visits the classes in this order:

    .. code-block::

        D, B, A, C, A

    Note how A occurs twice in the list.  The second occurrence is
    redundant, since anything that could be found there would already have
    been found when searching the first occurrence.  But it is visited
    nonetheless (the recursive implementation of the classic rule doesn't
    remember which classes it has already visited).

    Under the new rule, the list will be

    .. code-block::

        D, B, C, A

    Searching for methods in this order will do the right thing for the
    diamond diagram.  Because of the way the list is constructed, it
    never changes the search order in situations where no diamond is
    involved.

    The exact rule used will be explained in the next section.  I note
    here only the important property of *monotonicity* in the lookup
    rule: if class X precedes class Y in the lookup order for any of the
    base classes of class D, then class X will also precede class Y in the
    lookup order for class D.  For example, since B precedes A in the
    lookup list for B, it also precedes A in the lookup list for D; and
    ditto for C preceding A.  Exception: if, amongst the bases of class D,
    there is one where X precedes Y and another where Y precedes X, the
    algorithm has to break a tie.  In this case, all bets are off; in the
    future, this condition may cause a warning or an error.

    (A rule previously described at this place was proven not to have
    the monotonicity property.  See a `thread on python-dev started by Samuele Pedroni <http://mail.python.org/pipermail/python-dev/2002-October/029035.html>`_.)

    Isn't this backwards incompatible?  Won't it break existing code?
    It would, if we changed the method resolution order for all classes.
    However, in Python 2.2, the new lookup rule will only be applied to
    types derived from built-in types, which is a new feature.  Class
    statements without a base class create "classic classes", and so do
    class statements whose base classes are themselves classic classes.
    For classic classes the classic lookup rule will be used.
    We may also provide
    a tool that analyzes a class hierarchy looking for methods that would
    be affected by a change in method resolution order.

    Order Disagreements and Other Anomalies

    (This section is for advanced readers only.) 

    Any algorithm for deciding the method resolution order may be
    confronted with contradicting requirements.  This shows up for
    example when two given base classes occur in a different order in the
    inheritance list of two different derived classes, and those derived
    classes are both inherited by yet another class.  Here's an example:

    .. code-block::

        class A(object):
                def meth(self): return "A"
            class B(object):
                def meth(self): return "B"

            class X(A, B): pass
            class Y(B, A): pass

            class Z(X, Y): pass

    If you try this, (using Z.__mro__, see `below <#cooperation>`_), you get [Z, X, Y, A, B, object], which
    does not maintain the monotonicity requirement mentioned above: the
    MRO for Y is [Y, B, A, object], and this is not a subsequence of the
    above list!  In fact, there is no solution that satisfies the
    monotonicity requirement for both X and Y here.  This is called an
    *order disagreement*.  In a future version, we may decide to
    outlaw such order disagreements under certain circumstances, or issue
    warnings for them.

    The book `"Putting Metaclasses to Work" <#references>`_,
    which inspired me to change the MRO, defines the MRO algorithm that's
    currently implemented, but its description of the algorithm is pretty
    hard to grasp - I had originally documented a different, naive,
    algorithm and didn't even realize that it didn't always compute the
    same MRO until `Tim Peters <http://www.python.org/tim_one/>`_
    found a counterexample.  More recently, Samuele Pedroni has found a
    counterexample showing that the naive algorithm fails to maintain
    monotonicity, so I won't even describe it any more.  Samuele has
    convinced me to use a newer MRO algorithm named C3, described in the
    paper "A Monotonic Superclass Linearization for
    Dylan".  This algorithm will be used in Python 2.3.  C3 is
    monotonic just like the book's algorithm, but in addition maintains
    the order of the immediate base classes, which the book's algorithm
    doesn't always do.  A very accessible description of C3 for Python is
    `The Python 2.3 Method Resolution Order <../../2.3/mro.html>`_
    by Michele Simionato.

    The book outlaws classes containing such order disagreements, if
    the order disagreement is "serious".  An order disagreement between
    two classes is serious when the two classes define at least one method
    with the same name.  In the example above, the order disagreement is
    serious.  In Python 2.2, I chose not to check for serious order
    disagreements; but the meaning of a program containing a serious order
    disagreement is undefined, and its effect may change in the future.
    But since Samuele's counterexample, we know that outlawing order
    disagreements isn't enough to avoid different outcomes between the
    Python 2.2 algorithm (from the book) and the Python 2.3 algorithm (C3,
    from the Dylan paper).

    Cooperative methods and "super"

    One of the coolest, but perhaps also one of the most unusual
    features of the new classes is the possibility to write "cooperative" classes.
    Cooperative classes are written with multiple inheritance in mind,
    using a pattern that I call a "cooperative super call".  This is known
    in some other multiple-inheritance languages as "call-next-method",
    and is more powerful than the super call found in single-inheritance
    languages like Java or Smalltalk.  C++ has neither form of super call,
    relying instead on an explicit mechanism similar to that used in
    classic Python.  (The term "cooperative method" comes from
    `"Putting Metaclasses to Work" <#references>`_.)

    As a refresher, let's first review the traditional,
    non-cooperative super call.  When a class C derives from a base class
    B, C often wants to override a method m defined in B.  A "super call"
    occurs when C's definition of m calls B's definition of m to do some of its
    work.  In Java, the body of m in C can write super(a, b, c) to call
    B's definition of m with argument list (a, b, c).  In Python, C.m writes
    B.m(self, a, b, c) to accomplish the same effect.  For example:

    .. code-block::

        class B:
                def m(self):
                    print "B here"

            class C(B):
                def m(self):
                    print "C here"
                    B.m(self)

    We say that C's method m "extends" B's method m.  The pattern here
    works well as long as we're using single inheritance, but it breaks
    down with multiple inheritance.  Let's look at four classes whose
    inheritance diagram forms a "diamond" (the same diagram was
    shown graphically in the previous section):

    .. code-block::

        class A(object): ..
            class B(A): ...
            class C(A): ...
            class D(B, C): ...

    Suppose A defines a method m, which is extended by both B and C.
    Now what is D to do?  It inherits two implementations of m, one from B
    and one from C.  Traditionally, Python simply picks the first one
    found, in this case the definition from B.  This is not ideal, because
    this completely ignores C's definition.  To see what's wrong with
    ignoring C's m, assume that these classes represent some kind of
    persistent container hierarchy, and consider a method that implements
    the operation "save your data to disk".  Presumably, a D instance has
    both B's data and C's data, as well as A's data (a single copy of the
    latter).  Ignoring C's definition of the save method would mean that a D
    instance, when requested to save itself, only saves the A and B parts
    of its data, but not the part of its data defined by class C!

    C++ notices that D inherits two conflicting definitions of method m,
    and issues an error message.  The author of D is then supposed to
    override m to resolve the conflict.  But what is D's definition of m
    supposed to do?  It can call B's m followed by C's m, but because both
    definitions call the definition of m inherited from A, A's m ends up being
    called twice!  Depending on the details of the operation, this is at
    best an inefficiency (when m is idempotent), at worst an error.
    Classic Python has the same problem, except it doesn't even consider it an
    error to inherit two conflicting definitions of a method: it simply picks
    the first one.

    The traditional solution to this dilemma is to split each derived
    definition of m into two parts: a partial implementation _m, which only
    saves the data that is unique to one class, and a full implementation
    m, which calls its own _m and that of the base class(es).  For
    example:

    .. code-block::

        class A(object):
                def m(self): "save A's data"
            class B(A):
                def _m(self): "save B's data"
                def m(self):  self._m(); A.m(self)
            class C(A):
                def _m(self): "save C's data"
                def m(self):  self._m(); A.m(self)
            class D(B, C):
                def _m(self): "save D's data"
                def m(self):  self._m(); B._m(self); C._m(self); A.m(self)

    There are several problems with this pattern.  First of all, there
    is the proliferation of extra methods and calls.  But perhaps more
    importantly, it creates an undesirable dependency in the derived classes
    on details of the dependency graph of their base classes: the
    existence of A can no longer be considered an implementation detail of
    B and C, since class D needs to know about it.  If, in a future
    version of the program, we want to remove the dependency on A from B
    and C, this will affect derived classes like D as well; likewise, if we
    want to add another base class AA to B and C, all their derived
    classes must be updated as well.

    The "call-next-method" pattern solves this problem nicely, in
    combination with the new method resolution order.  Here's how:

    .. code-block::

        class A(object):
                def m(self): "save A's data"
            class B(A):
                def m(self): "save B's data"; super(B, self).m()
            class C(A):
                def m(self): "save C's data"; super(C, self).m()
            class D(B, C):
                def m(self): "save D's data"; super(D, self).m()

    Note that the first argument to super is always the class in which
    it occurs; the second argument is always self.  Also note that self is
    not repeated in the argument list for m.

    Now, in order to explain how super works, consider the MRO for each
    of these classes.  The MRO is given by the __mro__ class attribute:

    .. code-block::

        A.__mro__ == (A, object)
            B.__mro__ == (B, A, object)
            C.__mro__ == (C, A, object)
            D.__mro__ == (D, B, C, A, object)

    The expression super(C, self).m should only be used inside the
    implementation of method m in class C.  Bear in mind that while self
    is an instance of C, self.__class__ may not be C: it may be a class
    derived from C (for example, D).  The expression super(C, self).m,
    then, searches self.__class__.__mro__ (the MRO of the class that was
    used to create the instance in self) for the occurrence of C, and then
    starts looking for an implementation of method m *following* that
    point.

    For example, if self is a C instance, super(C, self).m will find
    A's implementation of m, as will super(B, self).m if self is a B
    instance.  But now consider a D instance.  In D's m, super(D,
    self).m() will find and call B.m(self), since B is the first base
    class following D in D.__mro__ that defines m.  Now in B.m, super(B,
    self).m() is called.  Since self is a D instance, the MRO is (D, B, C,
    A, object) and the class following B is C.  This is where the search
    for a definition of m continues.  This finds C.m, which is called, and
    in turn calls super(C, self).m().  Still using the same MRO, we see
    that the class following C is A, and thus A.m is called.  This is the
    original definition of m, so no super call is made at this point.

    Note how the same super expression finds a different class
    implementing a method depending on the class of self!  This is the
    crux of the cooperative super mechanism.

    The super call as shown above is
    somewhat prone to errors: it is easy to copy and paste a super call
    from one class to another while forgetting to change the class name to
    that of the target class, and this mistake won't be detected if both
    classes are part of the same inheritance graph.  (You can even cause
    infinite recursion by mistakenly passing in the name of a derived
    class of the class containing the super call.)  It would be nice if we
    didn't have to name the class explicitly, but this would require more
    help from Python's parser than we can currently get.  I hope to fix
    this in a future Python release by making the parser recognize super.

    In the mean time, here's a trick you can apply.  We can create a
    class variable named __super that has "binding" behavior.  (Binding
    behavior is a new concept in Python 2.2, but it formalizes a
    well-known concept from classic Python: the transformation from an
    unbound method to a bound method when it is accessed via the getattr
    operation on an instance.  It is implemented by the __get__ method
    discussed `above <#staticmethods>`_.)  Here's a simple
    example:

    .. code-block::

        class A:
                def m(self): "save A's data"
            class B(A):
                def m(self): "save B's data"; self.__super.m()
            B._B__super = super(B)
            class C(A):
                def m(self): "save C's data"; self.__super.m()
            C._C__super = super(C)
            class D(B, C):
                def m(self): "save D's data"; self.__super.m()
            D._D__super = super(D)

    Part of the trick is in the use of the name __super, which (through
    the name mangling transformation) contains the class name.  This
    ensures that self.__super means something different in each class (as
    long as the class names differ; unfortunately, it *is* possible
    in Python to reuse the name of a base class for a derived class).
    Another part of the trick is that the super built-in can be called
    with a single argument, and then creates an unbound version that can be
    bound by a later instance getattr operation.

    Unfortunately, this example is still rather ugly for a number of
    reasons: super requires that the class is passed in, but the class is
    not available until after execution of the class statement is
    completed, so the __super class attribute must be assigned outside the
    class.  Outside the class, name mangling doesn't work (after all it is
    intended to be a privacy feature) so the assignment must use the
    unmangled name.  Fortunately, it's possible to write a `metaclass <#metaclasses>`_ that automatically adds a __super
    attribute to its classes; see the `autosuper metaclass example below <#metaclass_examples>`_.

    Note that super(class, subclass) also works; this is needed for
    `__new__ <#__new__>`_ and other static methods.

    Example: coding super in Python.

    As an illustration of the power of the new system, here's a fully
    functional implementation of the super() built-in class in pure
    Python.  This may also help clarify the semantics of super() by
    spelling out the search in ample detail.  The print statement at the
    bottom of the following code prints "DCBA".

    .. code-block::

        class Super(object):
            def __init__(self, type, obj=None):
                self.__type__ = type
                self.__obj__ = obj
            def __get__(self, obj, type=None):
                if self.__obj__ is None and obj is not None:
                    return Super(self.__type__, obj)
                else:
                    return self
            def __getattr__(self, attr):
                if isinstance(self.__obj__, self.__type__):
                    starttype = self.__obj__.__class__
                else:
                    starttype = self.__obj__
                mro = iter(starttype.__mro__)
                for cls in mro:
                    if cls is self.__type__:
                        break
                # Note: mro is an iterator, so the second loop
                # picks up where the first one left off!
                for cls in mro:
                    if attr in cls.__dict__:
                        x = cls.__dict__[attr]
                        if hasattr(x, "__get__"):
                            x = x.__get__(self.__obj__)
                        return x
                raise AttributeError, attr

        class A(object):
            def m(self):
                return "A"

        class B(A):
            def m(self):
                return "B" + Super(B, self).m()

        class C(A):
            def m(self):
                return "C" + Super(C, self).m()

        class D(C, B):
            def m(self):
                return "D" + Super(D, self).m()

        print D().m() # "DCBA"

    Overriding the __new__ method

    When subclassing immutable built-in types like numbers and strings,
    and occasionally in other situations, the static method __new__ comes
    in handy.  __new__ is the first step in instance construction, invoked
    *before* __init__.  The __new__ method is called with the class
    as its first argument; its responsibility is to return a new instance
    of that class.  Compare this to __init__: __init__ is called with an
    instance as its first argument, and it doesn't return anything; its
    responsibility is to initialize the instance.  There are situations
    where a new instance is created without calling __init__ (for example when
    the instance is loaded from a pickle).  There is no way to create a
    new instance without calling __new__ (although in some cases you can
    get away with calling a base class's __new__).

    Recall that you create class instances by calling the class.  When
    the class is a new-style class, the following happens when it is
    called.  First, the class's __new__ method is called, passing the class
    itself as first argument, followed by any (positional as well as
    keyword) arguments received by the original call.  This returns a new
    instance.  Then that instance's __init__ method is called to further
    initialize it.  (This is all controlled by the __call__ method of the
    metaclass, by the way.)

    Here is an example of a subclass that overrides __new__ - this
    is how you would normally use it.

    .. code-block::

        >>> class inch(float):
            ...     "Convert from inch to meter"
            ...     def __new__(cls, arg=0.0):
            ...         return float.__new__(cls, arg*0.0254)
            >>> print inch(12)
            0.3048

    This class isn't very useful (it's not even the right way to go
    about unit conversions) but it shows how to extend the constructor of
    an immutable type.  If instead of __new__ we had tried to override
    __init__, it wouldn't have worked:

    .. code-block::

        >>> class inch(float):
            ...     "THIS DOESN'T WORK!!!"
            ...     def __init__(self, arg=0.0):
            ...         float.__init__(self, arg*0.0254)
            >>> print inch(12)
            12.0

    The version overriding __init__ doesn't work because the float
    type's __init__ is a no-op: it returns immediately, ignoring its
    arguments.

    All this is done so that immutable types can preserve their
    immutability while allowing subclassing.  If the value of a float
    object were initialized by its __init__ method, you could change the
    value of an existing float object!  For example, this would work:

    .. code-block::

        >>> # THIS DOESN'T WORK!!!
            >>> import math
            >>> math.pi.__init__(3.0)
            >>> print math.pi
            3.0

    I could have fixed this problem in other ways, for example by adding an
    "already initialized" flag or only allowing __init__ to be called on
    subclass instances, but those solutions are inelegant.
    Instead, I added __new__, which is a perfectly general mechanism that
    can be used by built-in and user-defined classes, for immutable and
    mutable objects.

    Here are some rules for __new__:

    - __new__ is a static method.  When defining it, you don't need to (but may!) use the phrase "__new__ = staticmethod(__new__)", because this is implied by its name (it is special-cased by the class constructor).
    - The first argument to __new__ must be a class; the remaining arguments are the arguments as seen by the constructor call.
    - A __new__ method that overrides a base class's __new__ method may call that base class's __new__ method.  The first argument to the base class's __new__ method call should be the class argument to the overriding __new__ method, not the base class; if you were to pass in the base class, you would get an instance of the base class.
    - Unless you want to play games like those described in the next two bullets, a __new__ method *must* call its base class's __new__ method; that's the only way to create an instance of your object.  The subclass __new__ can do two things to affect the resulting object: pass different arguments to the base class __new__, and modify the resulting object after it's been created (for example to initialize essential instance variables).
    - __new__ must return an object.  There's nothing that requires that it return a new object that is an instance of its class argument, although that is the convention.  If you return an existing object, the constructor call will still call its __init__ method.  If you return an object of a different class, *its* __init__ method will be called.  If you forget to return something, Python will unhelpfully return None, and your caller will probably be very confused.
    - For immutable classes, your __new__ may return a cached reference to an existing object with the same value; this is what the int, str and tuple types do for small values.  This is one of the reasons why their __init__ does nothing: cached objects would be re-initialized over and over.  (The other reason is that there's nothing left for __init__ to initialize: __new__ returns a fully initialized object.)
    - If you subclass a built-in immutable type and want to add some mutable state (maybe you add a default conversion to a string type), it's best to initialize the mutable state in the __init__ method and leave __new__ alone.
    - If you want to change the constructor's signature, you often have to override both __new__ and __init__ to accept the new signature. However, most built-in types ignore the arguments to the method they don't use; in particular, the immutable types (int, long, float, complex, str, unicode, and tuple) have a dummy __init__, while the mutable types (dict, list, file, and also super, classmethod, staticmethod, and property) have a dummy __new__.  The built-in type 'object' has a dummy __new__ and a dummy __init__ (which the others inherit).  The built-in type 'type' is special in many respects; see the section on `metaclasses <#metaclasses>`_.
    - (This has nothing to do to __new__, but is handy to know anyway.)  If you subclass a built-in type, extra space is automatically added to the instances to accomodate __dict__ and __weakrefs__.  (The __dict__ is not initialized until you use it though, so you shouldn't worry about the space occupied by an empty dictionary for each instance you create.)  If you don't need this extra space, you can add the phrase "__slots__ = []" to your class. (See `above <#subclassing>`_ for more about __slots__.)
    - Factoid: __new__ is a static method, not a class method.  I initially thought it would have to be a class method, and that's why I added the classmethod primitive.  Unfortunately, with class methods, upcalls don't work right in this case, so I had to make it a static method with an explicit class as its first argument.  Ironically, there are now no known uses for class methods in the Python distribution (other than in the test suite).  However, class methods are still useful in other places, for example, to program inheritable alternate constructors.

    As another example of __new__, here's a way to implement the
    singleton pattern.

    .. code-block::

        class Singleton(object):
                def __new__(cls, *args, **kwds):
                    it = cls.__dict__.get("__it__")
                    if it is not None:
                        return it
                    cls.__it__ = it = object.__new__(cls)
                    it.init(*args, **kwds)
                    return it
                def init(self, *args, **kwds):
                    pass

    To create a singleton class, you subclass from Singleton; each
    subclass will have a single instance, no matter how many times its
    constructor is called.  To further initialize the subclass instance,
    subclasses should override 'init' instead of __init__ - the __init__
    method is called each time the constructor is called.  For example:

    .. code-block::

        >>> class MySingleton(Singleton):
            ...     def init(self):
            ...         print "calling init"
            ...     def __init__(self):
            ...         print "calling __init__"
            >>> x = MySingleton()
            calling init
            calling __init__
            >>> assert x.__class__ is MySingleton
            >>> y = MySingleton()
            calling __init__
            >>> assert x is y

    Metaclasses

    In the past, the subject of metaclasses in Python has caused hairs
    to raise and even brains to explode (see, for example `Metaclasses in Python 1.5 <#references>`_).  Fortunately, in
    Python 2.2, metaclasses are more accessible and less dangerous.

    Terminology-wise, a metaclass is simply "the class of a class".
    Any class whose instances are themselves classes, is a metaclass.
    When we talk about an instance that's not a class, the instance's
    metaclass is the class of its class: by definition, x's metaclass is
    x.__class__.__class__.  But when we talk about a class C, we often
    refer to its metaclass when we mean C.__class__ (not
    C.__class__.__class__, which would be a meta-metaclass; there's not
    much use for those although we don't rule them out).

    The built-in 'type' is the most common metaclass; it is the
    metaclass of all built-in types.  Classic classes use a different
    metaclass: the type known as types.ClassType.  The latter is
    relatively uninteresting; it's a historical artefact that's needed
    to give classic classes their classic behavior.  You can't get to the
    metaclass of a classic instance using x.__class__.__class__; you have
    to use type(x.__class__), because classic classes don't support the
    __class__ attribute on classes (only on instances).

    When a class statement is executed, the interpreter first
    determines the appropriate metaclass M, and then calls M(name, bases,
    dict).  All this happens at the *end* of the class statement,
    after the body of the class (where methods and class variables are
    defined) has already been executed.  The arguments to M are the class
    name (a string taken from the class statement), a tuple of base
    classes (expressions evaluated at the start of the class statement;
    this is () if no bases are specified in the class statement), and a
    dictionary containing the methods and class variables defined by the
    class statement.  Whatever this call M(name, bases, dict) returns is
    then assigned to the variable corresponding to the class name, and
    that's all there is to the class statement.

    How is M determined?

    - If dict['__metaclass__'] exists, it is used.
    - Otherwise, if there is at least one base class, its metaclass is used (this looks for a __class__ attribute first and if that's not found, uses its type).  (In classic Python, this step existed too, but was only executed when the metaclass was callable.  This was called the Don Beaudry hook - may it rest in peace.)
    - Otherwise, if there's a global variable named __metaclass__, it is used.
    - Otherwise, the classic metaclass (types.ClassType) is used.

    The most common outcomes here are that M is either types.ClassType
    (creating a classic class), or 'type' (creating a new-style class).
    Other common outcomes are a custom extension type (like Jim Fulton's
    ExtensionClass), or a subtype of 'type' (when we're using new-style
    metaclasses).  But it's possible to have something completely
    outlandish here: if we specify a base class that has a custom
    __class__ attribute, we can use anything as a "metaclass".  That was
    the brain-exploding topic of my original `metaclass paper <#references>`_, and I won't repeat it here.

    There's always an additional wrinkle.  When you mix
    classic classes and new-style classes in the list of bases, the
    metaclass of the first new-style base class is used instead of
    types.ClassType (assuming dict['__metaclass__'] is undefined).  The
    effect is that when you cross a classic class and a new-style class,
    the offspring is a new-style class.

    And another one (I promise this is the last wrinkle in the
    metaclass determination).  For new-style metaclasses, there is a
    constraint that the chosen metaclass is equal to, or a subclass of, each
    of the metaclasses of the bases.  Consider a class C with two base
    classes, B1 and B2.  Let's say M = C.__class__, M1 = B1.__class__, M2
    = B2.__class__.  Then we require issubclass(M, M1) and issubclass(M,
    M2).  (This is because a method of B1 should be able to call a
    meta-method defined in M1 on self.__class__, even when self is an
    instance of a subclass of B1.)

    The `metaclasses book <#references>`_ describes a mechanism
    whereby a suitable metaclass is automatically created, when necessary,
    through multiple inheritance from M1 and M2.  In Python 2.2, I have
    chosen a simpler approach which raises an exception if the
    metaclass constraint is not satisfied; it is up to the programmer to
    provide a suitable metaclass through the __metaclass__ class variable.
    However, if one of the base metaclasses satisfies the constraint
    (including the explicitly given __metaclass__, if any), the first base
    metaclass found satisfying the constraint will be used as the
    metaclass.

    In practice, this means that if you have a degenerate metaclass
    hierarchy that has the shape of a tower (meaning that for two
    metaclasses M1 and M2, at least one of issubclass(M1, M2) or
    issubclass(M2, M1) is always true), you don't have to worry about the
    metaclass constraint.  For example:

    .. code-block::

        # Metaclasses
            class M1(type): ...
            class M2(M1): ...
            class M3(M2): ...
            class M4(type): ...

            # Regular classes
            class C1:
                __metaclass__ = M1
            class C2(C1):
                __metaclass__ = M2
            class C3(C1, C2):
                __metaclass__ = M3
            class D(C2, C3):
                __metaclass__ = M1
            class C4:
                __metaclass__ = M4
            class E(C3, C4):
                pass

    For class C2, the constraint is satisfied because M2 is a subclass
    of M1.  For class C3, it is satisfied because M3 is a subclass of both
    M1 and M2.  For class D, the explicit metaclass M1 is not a subclass
    of the base metaclasses (M2, M3), but choosing M3 satisfies the
    constraint, so D.__class__ is M3.  However, class E is an error: the
    two metaclasses involved are M3 and M4, and neither is a subclass of
    the other.  We can fix this latter case as follows:

    .. code-block::

        # A new metaclass
            class M5(M3, M4): pass

            # Fixed class E
            class E(C3, C4):
                __metaclass__ = M5

    (The approach from the metaclasses book would automatically supply
    the class definition for M5 given the original definition of class E.)

    Metaclass examples

    Let's refresh some theory first.  Remember that a class statement
    causes a call to M(name, bases, dict) where M is the metaclass.  Now,
    a metaclass is a class, and we've already established that when a
    class is called, its __new__ and __init__ methods are called in
    sequence.  Therefore, something like this will happen:

    .. code-block::

        cls = M.__new__(M, name, bases, dict)
            assert cls.__class__ is M
            M.__init__(cls, name, bases, dict)

    I'm writing the __init__ call as an unbound method call here.  This
    clarifies that we're calling the __init__ defined by M, not the
    __init__ defined in cls (which would be the initialization for
    instances of cls).  But it really calls the __init__ method of object
    cls; cls just happens to be a class.

    Our first example is a metaclass that looks through the methods of
    a class for methods named _get_<;something> and _set_<;something>,
    and automatically adds property descriptors named <;something>.  It
    turns out that it's sufficient to override __init__ to do what we
    want.  The algorithm makes two passes: first it collects names of
    properties, then it adds them to the class.  The collection pass looks
    through dict, which is the dictionary representing the class variables
    and methods (excluding base class variables and methods).  But the
    second pass, the property construction pass, looks up
    _get_<;something> and _set_<;something> as class attributes.  This
    means that if a base class defines _get_x and a subclass defines
    _set_x, the subclass will have a property x created from both methods,
    even though only _set_x occurs in the subclass's dictionary.  Thus,
    you can extend properties in a subclass.  Note that we use the
    three-argument form of getattr(), so a missing _get_x or _set_x will
    be translated into None, not raise an AttributeError.  We also call
    the base class __init__ method, in cooperative fashion using super().

    .. code-block::

        class autoprop(type):
                def __init__(cls, name, bases, dict):
                    super(autoprop, cls).__init__(name, bases, dict)
                    props = {}
                    for name in dict.keys():
                        if name.startswith("_get_") or name.startswith("_set_"):
                            props[name[5:]] = 1
                    for name in props.keys():
                        fget = getattr(cls, "_get_%s" % name, None)
                        fset = getattr(cls, "_set_%s" % name, None)
                        setattr(cls, name, property(fget, fset))

    Let's test autoprop with a silly example.  Here's a class that
    stores an attribute x as its inverted value under self.__x:

    .. code-block::

        class InvertedX:
                __metaclass__ = autoprop
                def _get_x(self):
                    return -self.__x
                def _set_x(self, x):
                    self.__x = -x

            a = InvertedX()
            assert not hasattr(a, "x")
            a.x = 12
            assert a.x == 12
            assert a._InvertedX__x == -12

    Our second example creates a class, 'autosuper', which will add a
    private class variable named __super, set to the value super(cls).
    (Recall the discussion of self.__super `above <#cooperation>`_.)  Now, __super is a private name
    (starts with double underscore) but we want it to be a private name of
    the class to be created, not a private name of autosuper.  Thus, we
    must do the name mangling ourselves, and use setattr() to set the
    class variable.  For the purpose of this example, I'm simplifying the
    name mangling to "prepend an underscore and the class name".  Again,
    it's sufficient to override __init__ to do what we want, and again, we
    call the base class __init__ cooperatively.

    .. code-block::

        class autosuper(type):
                def __init__(cls, name, bases, dict):
                    super(autosuper, cls).__init__(name, bases, dict)
                    setattr(cls, "_%s__super" % name, super(cls))

    Now let's test autosuper with the classic diamond diagram:

    .. code-block::

        class A:
                __metaclass__ = autosuper
                def meth(self):
                    return "A"
            class B(A):
                def meth(self):
                    return "B" + self.__super.meth()
            class C(A):
                def meth(self):
                    return "C" + self.__super.meth()
            class D(C, B):
                def meth(self):
                    return "D" + self.__super.meth()

            assert D().meth() == "DCBA"

    (Our autosuper metaclass is easily fooled if you define a subclass
    with the same name as a base class; it should really check for that
    condition and raise an error if it occurs.  But that's more code than
    feels right for an example, so I'll leave it as an exercise for the
    reader.)

    Now we have two independently developed metaclasses, we can combine
    the two into a third metaclass that inherits from them both:

    .. code-block::

        class autosuprop(autosuper, autoprop):
                pass

    Simple eh?  Because we wrote both metaclasses cooperatively
    (meaning their methods use super() to call the base class method),
    that's all we need.  Let's test it:

    .. code-block::

        class A:
                __metaclass__ = autosuprop
                def _get_x(self):
                    return "A"
            class B(A):
                def _get_x(self):
                    return "B" + self.__super._get_x()
            class C(A):
                def _get_x(self):
                    return "C" + self.__super._get_x()
            class D(C, B):
                def _get_x(self):
                    return "D" + self.__super._get_x()

            assert D().x == "DCBA"

    That's all for today.  I hope your brain doesn't hurt too much!

    Backwards incompatibilities

    **Relax!** Most features described above are only invoked when
    you use a class statement with a built-in object as a base class (or
    when you use an explicit __metaclass__ assignment).

    Some things that might affect old code:

    - See also the `bugs in 2.2 list <../bugs>`_.
    - Introspection works differently (see PEP 252).  In particular, most objects now have a __class__ attribute, and the __methods__ and __members__ attributes no longer work, and the dir() function works differently.  See also `above <#introspection>`_.
    - Several built-ins that can be seen as coercions or constructors are now type objects rather than factory functions; the type objects support the same behaviors as the old factory functions.  Affected are: complex, float, long, int, str, tuple, list, unicode, and type. (There are also new ones: dict, object, classmethod, staticmethod, but since these are new built-ins I can't see how this would break old code.)  See also `above <#factories>`_.
    - There's one very specific (and fortunately uncommon) bug that used to go undetected, but which is now reported as an error:    .. code-block::      class A:             def foo(self): pass              class B(A): pass              class C(A):             def foo(self):                 B.foo(self)    Here, C.foo wants to call A.foo, but by mistake calls B.foo.  In the old system, because B doesn't define foo, B.foo is identical to A.foo, so the call would succeed.  In the new system, B.foo is marked as a method requiring a B instance, and a C is not a B, so the call fails.
    - Binary compatibility with old extensions is not guaranteed. We've tightened this during the alpha and beta release cycle for Python 2.2.  As of 2.2b1, Jim Fulton's ExtensionClass works (as shown by a test of Zope 2.4), and I expect that other extensions based on the Don Beaudry hook will work as well.  While the ultimate goal of `PEP 253 <#references>`_ is to do away with ExtensionClass, I believe that ExtensionClass should still work in Python 2.2, breaking it no earlier than Python 2.3.

    Additional Topics

    These topics should also be discussed:

    - descriptors: __get__, __set__, __delete__
    - The specs of the built-in types that are subclassable
    - The 'object' type and its methods
    - <;type 'foo'> vs. <;type 'mod.foo'> vs. <;class 'mod.foo'>
    - What else?

    References

    - `PEP 252 </dev/peps/pep-0252>`_ - Making Types Look More Like Classes
    - `PEP 253 </dev/peps/pep-0253>`_ - Subtyping Built-in Types
    - `Metaclasses in Python 1.5 </doc/essays/metaclasses/>`_ - A.k.a. The Killer Joke
    - Putting Metaclasses to Work: A New Dimension in Object-Oriented Programming, by Ira R. Forman and Scott H. Danforth. Addison-Wesley, 1999, ISBN 0-201-43305-2.
    - A Monotonic Superclass Linearization for Dylan, by Kim Barrett, Bob Cassels, Paul Haahr, David A. Moon, Keith Playford, and P. Tucker Withington.  (OOPSLA 1996)