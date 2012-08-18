**MISSING**
**MISSING**

IronPython at Resolver Systems: Python Learns New Tricks
========================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  ironpython, spreadsheet, web

**Title:**  IronPython at Resolver Systems: Python Learns New Tricks

**Author:**   Jonathan Hartley

**Date:**   2008/06/02 01:00:00

**Website:**  `http://www.resolversystems.com <http://www.resolversystems.com>`_

**Summary:**  Resolver Systems uses IronPython and .NET for Resolver One, a desktop and web-accessible spreadsheet aimed primarily at the financial services market.

**Logo:**  .. image:: /files/success/resolver/resolversystems-logo-web.png    :alt: /files/success/resolver/resolversystems-logo-web.png

Introducing IronPython
----------------------

Pairing the Python language's expressivity with the seamless availability of
the extensive .NET class libraries makes `IronPython <http://www.codeplex.com/IronPython>`_ a powerful combination
for Resolver Systems.

About Resolver Systems
----------------------

Resolver Systems is a two year-old start-up based on the outskirts of London's
financial district. Our first product, Resolver One, is a desktop and
web-accessible spreadsheet aimed primarily at the financial services market. It
is written entirely in IronPython, and directly exposes end-users to Python,
both as expressions in cell formulae, and as an embedded scripting language
which provides programmatic access to spreadsheet content.

Resolver One launched in Spring of 2008, by which time the team had grown to
fourteen people, and the codebase to 40k lines of product and 140k lines of
tests.

Why IronPython?
---------------

From the outset, it was clear that it would be good to use an existing language
as our embedded scripting language, rather than inventing one. A dynamic
language would confer appropriate type semantics on the spreadsheet formulae.
It would be advantageous if this same language could also be used for
development of the Resolver One application itself. There was also a
requirement for .NET interoperability, so that both our own development team
and our users could invoke existing .NET libraries, especially the powerful
Graphical User Interface (GUI) components in the System.Windows.Forms module of
the .NET class libraries themselves.

Python was regarded fondly by our founders, but could not directly fulfil the
requirement for .NET interoperability. `Python for .NET <http://pythonnet.sourceforge.net/>`_ was considered,
allowing Python developers to call .NET assemblies, but in the end this lost
out to IronPython, a reimplementation of Python as a .NET language, which runs
directly on the Common Language Runtime (CLR). At the time, IronPython felt
like a somewhat risky proposition. At v0.7 it was still relatively young, and
had an extremely low profile. The acquisition of IronPython by Microsoft also
raised uncertainties about the project's future, should it be deemed contrary
to Microsoft's strategy.

However, our initial experiments with IronPython went well. It turned out to be
trivially easy to create a GUI using the excellent design tool in Visual
Studio, then inherit from these classes in Python code and implement all
behaviour in Python, in the Integrated Development Environment (IDE) of one's
choice. (Developers choose their own IDE, so we sport an entertaining diversity
of them, currently: Eclipse, Vi, Emacs, Wing, Komodo and the lightweight but
surprisingly useful Textpad.)

For example, IronPython code can easily display a .NET Form, using: 

.. code-block::

    # Add a reference to the required .NET assembly
    # This only need be done once per application
    import clr
    clr.AddReference(&quot;System.Windows.Forms&quot;)

    # Then import symbols from the assembly, as if from a Python module
    from System.Windows.Forms import Application, Form

    # Then use the imported symbols as though they were native Python types
    form = Form()
    form.Text = &quot;Hello World&quot;
    Application.Run(form)

Which displays this fully-functional Windows application: 

.. image:: /files/success/resolver/helloworld-web.png
   :alt: 'Hello World' GUI application created from IronPython

*Figure 1. &quot;Hello World&quot; GUI application created from IronPython.* 
`Zoom in </files/success/resolver/helloworld.tiff>`_

Over time, other strengths of IronPython have become apparent. Using the .NET
threading model means that applications are able to overcome CPython's global
interpreter lock. Resolver One uses this to run background recalculation
threads on different cores, to remain responsive during lengthy calculations.

Meanwhile, the concerns about the IronPython project have diminished. The
viability and visibility of IronPython has gone from strength to strength.
Today, with dynamic languages getting ever more attention, IronPython forms the
flagship language for Microsoft's recent Dynamic Language Runtime (DLR), upon
which future versions of Visual Basic will be based, and a healthy future seems
assured.

The success of IronPython is well deserved. It has proven to be a very capable
implementation, with transparent mappings between Python and .NET types, and
very few differences between it and CPython to catch out unwary developers.
Pairing up the expressivity and power of the Python language with the highly
functional and extensive .NET class libraries is a powerful combination.

Mixing Generated and User-Written Code
--------------------------------------

Resolver One pre-processes users' cell expressions to convert common
spreadsheet idioms into legal Python statements. These statements are
executed to determine the values displayed in the GUI's grid. The order in
which the statements are executed depends upon the dependencies between them.
For example, if cell A1 references the value of B1, then B1 must be evaluated
first. This provides us with the basic spreadsheet model that has proven so
valuable for ad-hoc investigation of numerical models.

.. image:: /files/success/resolver/basic-spreadsheet-eval-web.png
   :alt: Evaluation of cell formulae

*Figure 2. The basic steps Resolver One uses to evaluate cell formulae.* `Zoom 
in </files/success/resolver/basic-spreadsheet-eval.eps>`_

However, using this method, it is difficult for users to create spreadsheets of
any complexity without using cell expressions that are enormous and unwieldy,
mixing data, business logic and presentation information. These expressions get
duplicated (and almost-duplicated) many times. Any model which is more than
trivial quickly degenerates into an unmaintainable 'Frankensheet'.

To combat this, Resolver One allow users to intersperse the evaluation of cell
formulae with arbitrary code of their own. This is done by displaying the code
that is generated from cell expressions in a pane of the GUI. The user is free
to insert any Python of their own devising, to be executed before, during or
after the evaluation of the spreadsheet cell values.

.. image:: /files/success/resolver/resolverone-codepane-web.png
   :alt: Resolver One's code pane

*Figure 3. The code pane within the Resolver One application.* `Zoom in 
</files/success/resolver/resolverone-codepane.tiff>`_

So the spreadsheet, with all its data, expressions and user-customised
functions and algorithms, becomes a single, executable Python script. The GUI
and the code are two interchangeable views of the same underlying mathematical
model - editing one automatically updates the other. This retains the
accessibility and experimental immediacy of a traditional spreadsheet user
interface, while allowing the user to tame the spreadsheet's complexity using
the same techniques that software engineers have been inventing for the last
few decades: elimination of redundancies; functional decomposition; object
orientation; external libraries; and other high-level abstractions - all in a
modern, fully-featured programming language.

An important feature of Python that we were rely on heavily for this, and which
we were happy to see supported in IronPython, was the execution of cell
formulae and user code in a separate instance of the underlying Python engine.
This isolates the user's spreadsheet code from the running instance of the
Resolver One application, preventing us from polluting each other's namespace,
or from having to share global settings such as the Python recursion limit.

Supporting Agile Development
----------------------------

Python is a modern, expressive language, which supports many aspects of a 
modern, agile software development process. 

Small Code Base
~~~~~~~~~~~~~~~

Python's high level of abstraction and expressivity allows our developers to
produce complex functionality using a minimal amount of code. This has enabled
a small team of engineers - linearly growing from two to fourteen employees
over two years - to create a fully-featured solution with a manageable codebase.

Unit and Acceptance Testing
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Python's built-in 'unittest' module provides everything needed to get started
with most unit testing, and has proven extendible enough for us to gradually
build our own acceptance test framework on top of it. This uses the .NET API to
directly stimulate mouse and keyboard input events to manipulate the
application's GUI, and then asserting the existence and content of various GUI
components like windows and textboxes, to provide automated assurance of
end-to-end functionality.

Test-Driven Development
~~~~~~~~~~~~~~~~~~~~~~~

Dynamic languages like Python complement automated testing, by allowing the
patching of modules, classes, methods or attributes with arbitrary objects at
runtime. This allows tests to easily eliminate dependencies of the code under
test, and thus concentrating on testing one thing at at time. Additionally, it
makes it easy to stimulate particular behaviours or failure modes during the
test. For example, by patching the file 'open' function with another function
which simply raises an exception, a test can easily verify how the code under
test reacts if it is unexpectedly unable to open a file.

Distributed Testing Infrastructure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Resolver Systems also uses Python extensively for their internal
infrastructure, from IDE scripting to a distributed test runner, which spreads
the load of running many unit and acceptance tests over however many machines
in the office are currently idle.

The distributed test mechanism became necessary as our test suite grew in size.
We would rather over-test than under-test, and our test suites contain several
hundred acceptance tests that fire up the application and pummel the GUI to put
it through its paces, including performance tests on large data sets. Running
all these tests takes a significant amount of time. When it grew to one hour,
we developed procedures to work around it. When it grew to two or three hours,
it was seriously impacting our developer's feedback cycle, so we vowed to
reduce the amount of time taken to run the test suite, without compromising the
coverage provided by all the diverse tests. The distributed test runner was the
result.

Notably, this wasn't our first attempt at a distributed test runner. One of our
genius interns had attempted a similar project the previous summer, using .NET
remote procedure calls. Unfortunately, the complexity of this proved too much
to nail down in the time available. In the end, in true agile style, it was a
less ambitious architecture which actually got completed, by a different genius
intern the following summer. This has been refined gradually ever since, and
now forms an invaluable part of our daily routine.

Initiating a distributed build from a developer's PC will enumerate the tests,
marking them as 'to be run' in a database, and then copy the build to shared
directories on a manually listed set of 'slave' machines. Forcing developers to
manually specify which machines to use was initially created as the 'simplest
thing that could possibly work.' Contrary to our expectations, we have since
had little motivation to automate this. It turns out that negotiation between
developers over which machines to use during builds is a valuable excuse to
touch base with each other about what we're up to through the day. It also
provides an opportunity to fine-tune the allocation of free machines between
more than one simultaneous build, when the need arises.

Once slave machines have received their copy of the build, they grab the ID of
a few unallocated tests from the database, and run those tests locally,
updating the database with the results. Test results are visible at any time
using a web interface, which also makes it easy to ask a particular machine to
drop out of the build once it has finished running it's current batch of tests.
Once all test records are marked as either pass or fail, we know the build is
complete.

Problems
--------

3rd Party GUI Components with Win32 API calls means Windows Only
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IronPython is a Microsoft .NET Language, and as such, is ostensibly limited to
running on Windows only.

The Mono project is a fantastic effort to improve that situation, and many .NET
projects will run without recompilation under Mono on Linux, Mac OS X and
others. However, in our case, Resolver One uses a 3rd party grid component in
our GUI, which makes direct Win32 API calls. This precludes us running on
different platforms for the time being.

We are, however, working on a Mono-compatible version of Resolver Server, which
is a version of Resolver One which publishes editable spreadsheets over the
web, without displaying any GUI on the server.

No Python C Extension Modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IronPython scripts can in general import and use regular Python modules.
However, IronPython cannot import C extension modules. Such modules generally
have a .pyd extension, and consist of compiled C or C++, exposing an API to
let them be imported like a Python library.

Such modules include some of the Python standard library, such as cmath, array,
parser, and subprocess. Much of this missing functionality is compensated for
by the availability of equivalent .NET libraries, however this obviously
damages the credibility of IronPython as a plug-in alternative implementation.

Perhaps more significantly for us, this also precludes some commonly-used
3rd-party modules such as `NumPy and SciPy <http://www.scipy.org/>`_. Many of our clients would like
to use these with Resolver One.

Resolver Systems has therefore started an open-source project, `IronClad <http://code.google.com/p/ironclad>`_,
which aims to make C extension modules callable from IronPython. There is still
a lot of work to do before this project will be useful, but obviously such a
technology would be of interest to all users of IronPython. Enough progress has
been made thus far to demonstrate the feasibility of the approach: The bzip C
extension module can currently be called from IronPython, and others will
follow as we implement more of the Python C extension API.

Negative Perceptions of Open-Source
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes we need to remind ourselves that people outside the software industry
don't understand terms such as open source. Personally, I've had more
than one informal dinner party conversation about Resolver One with finance
industry people, who have stopped me to ask why on Earth we chose Python if
it's an open source language? After all, isn't open source the same as
freeware, ie. all rubbish?

It's hard to know how significant this perception is amongst our potential
clients' decision makers, but obviously we do our best to rectify such
impressions wherever we encounter them.

Performance
~~~~~~~~~~~

IronPython performance is generally comparable to CPython - faster in some
regards, slower in others. It seems likely that IronPython will continue to
gain on CPython as their implementation matures. This is not saying much
though - benchmarks clearly show dynamic languages like Python to be
significantly slower than more mainstream, statically typed languages. However,
this result is not as significant as it is sometimes made out to be, for two
reasons.

Firstly, many applications are rarely CPU bound, and simply do not need the
intensive performance that the fastest languages can give you. For interactive
desktop applications, the speed difference between C# and IronPython would
rarely be discernible by the user.

Some programs do require significant CPU performance, either because they are
crunching large data sets or because they must scale across many users on a
server. In such a project, it is often a very small proportion of the code
which actually requires this high performance. Usually it makes sense to
develop the majority of the application in a language which makes it easiest
for the developers to make rapid progress, then measure performance to see
whether optimisation is required, and where. The offending bottleneck can often
be refactored for performance, or alternatively, rewritten in another language.
(C for CPython, or any .NET language for IronPython.)

Secondly, benchmarks give an overly pessimistic view of dynamic language
performance. In significant real-world applications, the data sets and
algorithms are significantly more complex than most benchmarks, and the higher
levels of abstraction afforded by a powerful language like Python will enable
developers to visualise more efficient implementations with less effort. Simply
put, programs take less time to write in Python, leaving you more time
afterwards to refactor for performance if necessary. Then the refactoring is
easier in Python too.

For Resolver One, we do find performance problems from time to time, such as
when loading very large spreadsheets. Generally we schedule a new user story to
address these performance issues, much as we would for any other functionality.
After a day or three of work, we have usually developed a sufficient
improvement in efficiency, and will have created an acceptance test along the
way to measure and monitor this going forward.

Conclusion
----------

Using Python so extensively, for our sole product and our internal development
infrastructure, has made it a mission critical component for our company's
success. Python has admirably supported our requirements, from the robust
features of the language itself, the excellent .NET implementation provided by
the IronPython project, and the thriving community of discussion, support and
tools. On the whole, our clients feel the same, as shown by this quote from
&quot;Credit Cooperatif&quot;, a large French retail bank who are now using Resolver One:

    We use Excel and VBA, but we prefer Python for its combination of
    simplicity and power. We were looking to better link spreadsheets with
    Python programming, and Resolver One seemed to be the most elegant solution
    because it was based on Python but also gave us compatibility with our IT
    team?s architectural choice of Microsoft .NET.

Resolver One is Windows only, and is free for evaluation, or for non-commercial
use.

`http://www.resolversystems.com <http://www.resolversystems.com>`_

About the Author
----------------

Jonathan Hartley originally came into software from a background in digital
electronics. Nowadays, he is delighted to be a developer at Resolver Systems,
alongside people who are all smarter than he is. He lives in London with his
wife Susan and two trusty Guitar Hero controllers.