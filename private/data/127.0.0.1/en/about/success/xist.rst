**MISSING**
**MISSING**

XIST:  An XML Transformation Engine Written in Python
=====================================================

**MISSING**
**MISSING**
**Category:**  Software Development

**Keywords:**  Web2.0, XML

**Title:**  XIST:  An XML Transformation Engine Written in Python

**Authors:**   Dr. Walter D?rwald and Dr. Alois Kastner-Maresch

**Date:**   2003/01/17 15:59:02

**Web site:**  `http://www.livinglogic.de/Python/xist/ <http://www.livinglogic.de/Python/xist/>`_

**Summary:**  XIST is a XML transformation engine written completely in Python at LivingLogic AG, a software development company specializing in web technology.  XIST was designed to facilitate the task of creating and maintaining large web sites.

**Logo:**  .. image:: /files/success/xist/livinglogic.gif    :alt: /files/success/xist/livinglogic.gif

Summary
-------

`XIST <http://www.livinglogic.de/Python/xist/>`_ is a XML transformation engine written completely in Python at
LivingLogic AG, a software development company specializing in web technology.
XIST was designed to facilitate the task of creating and maintaining large web
sites.

Background
----------

Soon after we began creating web pages in 1994, it became clear that
typing HTML files by hand is tedious and cumbersome, and we began to
search for tools to simplify the repetitive task of HTML generation.

Early on, we discovered and started to use an HTML preprocessor named `hsc <http://www.giga.or.at/~agi/hsc/>`_.
This tool supported generation of pages from templates by defining new markup
tags and controlling how these tags would be transformed into HTML, somewhat
like XML/XSL does now.

Unfortunately hsc had certain limitations: It didn't support local
variables, and there were no control structures except conditionals.
Even arithmetic was not possible. Our first web sites developed with this
system consisted of a mix of hsc macros and Perl scripts that generated
hsc source files.

In 1998, hsc's author halted further development, and we became quite
motivated to find an alternative. At first we decided to continue
development of hsc ourselves, and planned to make it compatible with
XML, which was beginning to become popular at the time. But extending
hsc, which is written in C, proved quite difficult. For example, adding
Unicode support required rewriting the entire I/O system. It became
clear that we needed to find another toolset for our web development.

XIST is Born
------------

Around this time we discovered Python and decided that it might be a
good way to completely rewrite hsc from scratch. Python includes XML
parsing capabilities that we felt could be used as the basis for our
work: Instead of writing macros in hsc, we could write XML that could
be processed through a simple mapping from XML element types to Python
classes.

In this approach, XIST generates an extended Document Object Model
(DOM) on parsing each XML file. Classes defined for each element in the
file are instantiated as the DOM is generated, and methods on the
classes are used to perform the necessary XML transformations during
page generation. This allows us to realize our web templates with the
full power of an object-oriented scripting language.

During implementation, we found that all of the key features of hsc
could be supported quite easily in Python:

    - Automatically calculate image sizes? The Python Imaging Library does this with ease.

    - Parse XML files?  There are several XML parsers available in Python.

    - Load and store XML to and from databases?  The Python DB-API is standardized and modules exist for MySQL, Postgres, Interbase, Oracle, ODBC, Sybase, and others.

    - Fetch XML from the web? Python's urlparse and urllib standard libraries were made for that.

    - Handle Unicode? Python 2.0 fully supports Unicode out of the box.

Implementing the first prototype version took a few weeks of spare time
programming and turned out to be very successful. Python provided a
much shorter path from concept to implementation than any of the other
programming languages we have used. And so XIST was born.

XIST's development continued in Python and today XIST is the basis of a
successful company which employs 15 people. XIST is now used in all of
our web projects at LivingLogic AG.

Content Management with Python and JSP
--------------------------------------

On top of XIST, LivingLogic has developed a content management system
called XIST4C (4C means Content, Community, Collaboration and
Commerce). This system combines the advantages of XIST's abstracted
page layouts with pre-compilation of page templates to Java Server Pages
that are ultimately used to deliver the content to the web.

By using XIST tag libraries instead of JSP tag libraries we are able to
build optimized Java Server Pages that run considerably faster than
their JSP tag library counterparts, without any changes to the JSP
files. This performance gain is a result of the fact that the XIST
preprocessor takes care of many compute-intensive operations,
that might require dynamic type introspection, string processing etc.
and would be executed by the Java tag library code during page load.

Fast development combined with low hardware requirements makes XIST4C
especially suitable for small and medium sized enterprises. This has
allowed us to achieve a unique competitive advantage, and to realize
projects at much lower cost.

Prototyping Java Systems with Python
------------------------------------

In 2000, LivingLogic was engaged to develop a product for modeling
business process work flow and to automate business processes. Inspired
by our earlier successes with XIST, we decided to develop a Python
prototype. This decision was made even though our contract required us
to produce a Java-based prototype for delivery to a large group of
developers that would turn it into a marketable product.

The approach of using Python early in prototyping made it possible for
us to study concepts using working code almost from the start of this
project. Although we had to rewrite our Python prototype in Java, the
overall time spent on prototyping was lower than we have seen in other
projects that used only Java.

Conclusion
----------

Python is easy to learn and use, produces maintainable code, and packs
enough power to make it a suitable choice for many application domains
and project sizes.

Some of the features that we like best about Python include: 

    - Python's extensive standard library and a considerable range of available third party packages support development in many application domains.

    - An unsurprising syntax and the widespread and consistent use of a few basic concepts, like namespaces, help to make Python code readable and maintainable.

    - Extensive and easy to use introspection facilities make Python easy to learn interactively by discovering its capabilities, including documentation, from the command prompt.

    - Python is readily extensible in C or C++, so it is easy to incorporate non-Python modules into an application.

Python has played an important role in the success of LivingLogic AG,
and will continue to be the basis for most of our software development
efforts.

About the Authors
-----------------

*Before receiving his Ph.D. in 2000, Dr. Walter D?rwald researched
forest growth simulations and artificial life at BIT?K (the Bayreuth
Institute of Forest Ecosystem Research), and developed a large C++
framework for simulation and visualization. In 2000, he co-founded
LivingLogic AG, and has been responsible for the company's fundamental
tools and technologies ever since.*

*After getting his Ph.D. in Mathematics in 1990, Dr. Alois
Kastner-Maresch lead the Forest Ecosystem Simulation research team at
BIT?K.  In 2000, he co-founded LivingLogic AG, where he is CEO.*