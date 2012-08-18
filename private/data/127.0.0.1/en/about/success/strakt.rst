**MISSING**
**MISSING**

Rapid Application Development with Python
=========================================

**MISSING**
**MISSING**
**Category:**  Software Development, Business

**Keywords:**  Groupware, Rapid Application Development, Collaboration Support, Quality

**Title:**  Rapid Application Development with Python

**Authors:**   Laura Creighton and Alex Martelli

**Date:**   2003/01/17 15:59:01

**Web site:**  `http://www.strakt.com/ <http://www.strakt.com/>`_

**Summary:**  Strakt uses Python to develop the next generation collaborative environment for the workflow intensive workplace.

**Logo:**  .. image:: /files/success/strakt/strakt_logo.gif    :alt: /files/success/strakt/strakt_logo.gif

Introduction
------------

`Strakt <http://www.strakt.com/>`_ is a Swedish company which specializes in developing scalable and
secure products for collaboration in workflow intensive workplaces. Our
vision is to empower professionals to collaborate in an enjoyable,
intuitive, and efficient way that is tailored to their and their
organisations' needs, while simultaneously developing and maintaining
digitally stored organisational memory.

In 2001, AB Strakt embarked on a large software development project
aimed at providing modular collaboration and workflow solutions to
improve case handling, bug tracking, project management, customer or
employee relationship management, asset management, and many other
types of workflow intensive applications. With insights from research
in Library and Information Sciences, the four founders of AB Strakt
believed they could create a product which would greatly improve the
way large organizations collaborate and share information.

The basis for this effort was CAPS, the Collaborative Approach to
Problem Solving, which is a framework for a completely general,
extensible, scalable case handling system that provides instantaneous
real-time updates, general autonomous event handling, and improved
security at the attribute (as opposed to file, or case) level.

Architecture
------------

CAPS is divided into three parts: (1) the Infinite Filing Cabinet, (2)
the Business Logic, and (3) several client packages.

.. image:: /files/success/strakt/CAPS_figure_web.gif
   :alt: The CAPS Architecture

*The CAPS Architecture* `Zoom in </files/success/strakt/CAPS_figure.gif>`_ 

The Infinite Filing Cabinet (IFC) is a general Object Relational
database engine with a Python API. The IFC is built on top of Postgres,
with an Oracle version in the works, but it is possible to use any
full-function RDBMS, as we took care to avoid non-standard SQL
functionality and isolated the DB-specific idioms into a separate
portability layer. Production IFCs currently run only under Linux, with
others planned.

The Business Logic is a layer of rules which handle data validation,
access control, and customizable business-specific knowledge held by
the customer organization. The Business Logic Modules are designed to
be changed to quickly develop applications on top of the CAPS
framework.

The various clients are front-ends which talk to the Business Logic,
which mediates all client communication with the IFC. Our customizable
GUI-client, written using `PyQt <http://www.riverbankcomputing.co.uk/pyqt/>`_, currently runs under Linux, Windows,
and Solaris. Our web-client uses WebWare and Apache and supports
Mozilla, Lynx, and Internet Explorer, with Opera, Galeon and Konqueror
support planned. There are also Python scripting front-ends, and an
SMTP Mail client which permits users to communicate with the system
using their favorite email reader.

Our subsystems communicate securely, thanks to `OpenSSL <http://www.openssl.org/>`_. We wrote our own
python wrapper, called it `PyOpenSSL <http://pyopenssl.sourceforge.net/>`_ and released it under the GNU Lesser
General Public License. We also use an asynchronous architecture based on
`Twisted <http://www.twistedmatrix.com/>`_ to achieve high scalability and responsiveness. Brett Cannon's
```strptime()``` module, scheduled for inclusion in the language for Python
2.3, made BSD style date-handling work portably across architectures.

Existing applications based on CAPS, developed in-house, include a
help-desk case-handling system and a bug-tracking system.
Additional applications will be developed in the future, through
partnerships with companies that are interested in developing specific
capabilities and marketing them to end-user customers.

.. image:: /files/success/strakt/GUI_capscase_web.gif
   :alt: CAPScase, a CAPS-based case handling application

*CAPScase, a CAPS-based case handling application* `Zoom in 
</files/success/strakt/GUI_capscase.gif>`_

Why Python?
-----------

Python was chosen for this project for a number of carefully considered
reasons:

- **Portability:** We knew that we needed an extremely portable language - and Python runs everywhere.

- **Access to Source:** We knew that we wanted the source code for whatever language we chose. Forming a startup is risky enough without having to worry about being completely dependent upon somebody else to fix bugs in your tool set. Python is open source with an unrestrictive license.

- **Ability to Integrate:** We had no desire to reinvent the wheel. We needed a language that would play nicely with existing programs, such as relational databases, web software, and whatever other existing applications we might need to integrate into our applications in the future. Python is well suited for this.

- **Rapid Development:** We knew that we were going to have to do a lot of prototyping before we were satisfied with our design, so we wanted an interpreted, dynamically typed language. For expressive power, we wanted a high-level object-oriented language. Speed of development, not application runtime speed, was most critical for us. Python is a very productive way to write code.

- **Support for Selective Optimization:** We knew there was a chance that profiling would later reveal that small portions of our application *were* time-critical, and therefore might need to be re-coded in C or C++. Python integrates seamlessly with these languages, so you truly can &quot;have your cake and eat it too&quot; by coding only small profiler-identified portions of your code in C or C++, and using the built-in higher-level abstractions of Python for rapid development of the rest of your application.

- **Scriptability:** Since our intention was to have our partners develop their own applications by writing their own Business Logic Modules, we wanted our language choice to provide scriptability for our solution. Python is already well suited to scripting.

Experiences with Python
-----------------------

Although many of us had never used Python before, our technical
analysis of the language convinced us that it was the right choice. As
we started to work with it, we found that Python is extremely easy to
learn. We were actually able to become productive with it almost
immediately at a level comparable to the development speeds we were
used to in each of our most familiar languages. It took us somewhat
longer to become familiar with Python's unique approach, much of which
is important to understand in order to use the language to its fullest
potential. But there was never a period of painful adjustment, and we
never felt we needed to fight the syntax or fumble for ways to
implement our algorithms.

More pleasant surprises were in store for us. Until we used Python, we
were not aware of what a difference programming in such a readable
language would make. Some of us already had extensive experience
programming in other interpreted dynamically typed languages. We
believed, at the time, that Python's reputation as a good language
for rapid development rested solely on the fact that it is intepreted
and dynamically typed. But by programming in Python we became more
productive than with those other languages. We now believe part of the
elegance of Python can be attributed to the fact that it lies in the
&quot;sweet spot&quot; between tediously verbose and arcanely terse languages.
This and perhaps other factors that we haven't consciously identified
make for a language that indeed &quot;fits your brain&quot;.

We soon discovered that even our approach to design was altered and
facilitated by Python. Because code is so fast to develop, and
relatively easy to change once written, fewer design decisions needed
to be made based on general principles, and more could be made
empirically, on the basis of how well the code actually performs. This
resulted for us in lower risk of committing to or perpetuating an
inferior design. Sometimes the only way to find out if approach A is
better than approach B is to code them both and see. Python more often
gives you the time to try both, or at least the flexibility to switch
if trying the first one doesn't work out.

The fact that Python impacts the entire development process was also
illustrated for us in our policy of performing periodic code reviews.
Because of the development speeds we were seeing, our code base could
change a *lot* in a week, and we had to change our code reviews to
a more frequent schedule.  On the other hand, since Python code tends
to be very uniform and readable, we found that reviews were better able
to concentrate on the substance of changes made and were generally more
efficient.

Another positive but unexpected experience came in our use of the
Python standard library. Our initial analysis of the language had not
revealed to us just how rich it was, and we were delighted to discover
that third party Python bindings already existed for many convenient
library packages written in other languages.

Perhaps the greatest pleasant surprise of all was the Python user
community itself, which is rich in knowledgeable and helpful people who
go out of their way to answer questions about Python and its use at all
levels of expertise. The level of technical support we have received
for free from this resource has been quite astounding.

We develop using CVS and `tortoiseCVS <http://www.tortoisecvs.org/>`_, a plug-in for Windows Explorer, and a
mix of editors and development environments, including emacs, vim, sam, and
`Wing IDE <http://wingide.com/>`_.

Results
-------

The CAPS project has been very successful. Four of us were able to
design and write a prototype of the system over the period of about a
year. Once the prototype had been written, we expanded our company to 8
full-time developers and 4 part-time developers. Strakt currently
supports a total of 18 people.

As of October 2002, we have deployed our software to our first beta
customer, a major Swedish university, where it has been running for
three months. Other organizations have expressed interest in becoming
reference customers. We could not have done it without Python.

About the Authors
-----------------

Laura Creighton has 20 years experience in software training, and Human
Factors Engineering. She is a founder of AB Strakt, and a founder and
Treasurer of The Python Business Forum, an international non-profit trade
association for businesses which develop in Python.

Alex Martelli has a Laurea degree in Electronic Engineering and a quarter
century of professional experience in SW development -- as Systems Analyst for
IBM Research, Senior Software Consultant for think3 Inc, Senior System
Developer for AB Strakt, and now as Uber Technical Lead for Google Inc. Alex
is a co-editor of the &quot;Python Cookbook&quot;, and the author of &quot;Python in a
Nutshell&quot;, published by `O'Reilly Associates <http://www.oreilly.com/>`_. He's a member of the Python
Software Foundation, and also serves on the board of The Python Business
Forum.