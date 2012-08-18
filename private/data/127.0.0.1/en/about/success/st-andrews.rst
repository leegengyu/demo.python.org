**MISSING**
**MISSING**

Python Enterprise-Wide at the University of St Andrews in Scotland
==================================================================

**MISSING**
**MISSING**
**Category:**  Software Development, Business, Education,

**Keywords:**  Database, Web Development, Document Managment, Human Resources, Systems Administration,

**Title:**  Python Enterprise-Wide at the University of St Andrews in Scotland

**Author:**   Hamish Lawson

**Date:**   2003/01/17 15:59:01

**Website:**  `http://www.st-andrews.ac.uk/ <http://www.st-andrews.ac.uk/>`_

**Summary:**  Python is adopted by the IT Services department at the University of St Andrews, Scotland, and results in better code quality and shorter development times.

**Logo:**  .. image:: /files/success/st-andrews/st-andrews-logo.gif    :alt: /files/success/st-andrews/st-andrews-logo.gif

.. image:: /files/success/st-andrews/university-web.jpg
   :alt: View of The University of St Andrews

*The University of St Andrews, founded in 1411, is Scotland's oldest
university* `Zoom in </files/success/st-andrews/university-print.png>`_

Introduction
------------

The IT Services department at the University of St Andrews, Scotland,
develops and maintains software systems used in a variety of capacities
throughout the university.

I had several years of experience working with Perl when I took my first
serious look at Python back in 1999. Our team's projects were becoming
bigger and more complex, and it was obvious that we needed to bring to
them more structure and clarity. I had been looking at Java for some
time, but its potential benefits seemed to come at the cost of a steep
learning curve, and an overall increase in development time. In
contrast, Python appeared to offer the prospect of having both clarity
*and* productivity at the same time. And if we ever needed to make use
of Java's class libraries there was always Jython, an implementation of
Python for the JVM. The increasing number of Python books being
published testified to the language's growing popularity, and the number
of available libraries was beginning to rival Perl's. This convinced me
to give Python a try.

Python Finds a Home
-------------------

Soon thereafter, I introduced Python to my fellow developers in the IT
Services department at the University of St Andrews, Scotland. It is
now the mainstay of our software development efforts.

Python has been used successfully by IT Services for a number of
projects. These have included systems administration scripts, where it
is used alongside Perl and shell scripts, and also sizeable enterprise
systems deployed across the university.

By using it on a number of projects, we have come to understand that
Python's dynamic nature, support for high-level data structures, and easy
object-orientation all lower the barrier to writing well-structured
reusable code in less time. The language's clear and simple syntax
helps to reveal the sense (or otherwise!) of our code. This makes it
easier to understand and reason about code during development and -
more critically - during later maintenance. The fact that Python is so
easy to learn has been quite useful as well.

Job Vacancies Facility
----------------------

One of our earliest Python projects was a facility for University job
vacancies. This was implemented using Zope, an innovative Python-based
web application server that provides a range of web components plus
powerful facilities for templating and integration. I started the
project with a colleague who had more experience in web design than
programming. After some time, we found that Python's powerful simplicity
enabled my colleague to improve his programming skills rapidly, to the
point where he was able to continue development of the system by
himself. Zope itself also helped in this regard, by reducing the amount
of programming that needed to be done in the first place.

Student Record System
---------------------

.. image:: /files/success/st-andrews/document-mgmt-web.jpg
   :alt: Document-management system for student records

*Document-management system for student records* `Zoom in 
</files/success/st-andrews/document-mgmt-print.png>`_ 

One of our larger projects was a system for managing student records.
It employs a model-view-controller architecture in order to promote
reuse. Presentation is handled by Cheetah, an open-source templating
technology for Python. The interface between Python and the underlying
Oracle database is handled by the high-quality DCOracle2 driver made
freely available by Zope Corporation.

Matching Students with Classes
------------------------------

Python was also used for a web-based system that managed the process of
matching students with the classes they wish to take in the coming
year. The system was used by most of our students and a number of our
staff for various stages of the process - from selecting preferences in
the spring and summer, through to final validation during matriculation
at the start of the new academic year. The system implemented work-flow
and notification mechanisms.

Because of the number of concurrent users that the system was expected
to support, particularly during matriculation, we felt that a
traditional CGI approach could lead to performance problems. Instead,
we employed mod_scgi, an Apache module that implements the client end
of the SCGI protocol for long-running web processes (similar to
FastCGI). The server end of the SCGI protocol was implemented by
Quixote, a Python-based web framework. Quixote also provided a URL
mapping mechanism that simplified the job of publishing objects on the
web. Cheetah was again used for handling presentation, and Oracle was
used for storage.

We were assigned this project somewhat late in the process, and it was
clear that it would come into active use while parts of it were still
being developed. To support this, we planned to deliver the system in
stages, but we were aware from the outset that many of the system
requirements still had to be discovered and understood. We knew this
would lead us to rewrite parts of the system as we went along and
worked to obviate this with design decisions aimed at decoupling the
system's components. Python's dynamic nature and supreme flexibility
made it easier to write generic interfaces, which later facilitated the
rewriting and refactoring tasks we had to undertake.

Conclusion
----------

Since switching to Python, we are writing better structured and more
readable code in less time ... and it's fun! I can't think of a better
testament to a programming tool.

About the Author
----------------

*Hamish Lawson is a software developer in the IT Services department at
the University of St Andrews, Scotland. He specializes in web-based
information systems.*