**MISSING**
**MISSING**

Enovad Used Python to Deliver its Armadillo Commercial Anti-Spam Software
=========================================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  cpython, ide, spam

**Title:**  Enovad Used Python to Deliver its Armadillo Commercial Anti-Spam Software

**Author:**   Marcus Low

**Date:**   2009/04/08 02:03:48

**Website:**  `http://www.enovad.com/ <http://www.enovad.com/>`_

**Summary:**  Python helps Enovad deliver the feature-rich Armadillo commercial anti-spam product ahead of schedule.

**Logo:**  .. image:: /files/success/enovad/enovad-logo.gif    :alt: /files/success/enovad/enovad-logo.gif

Introduction
------------

I have been programming in C and C++ since 1994 and have led many teams in
Windows system programming. In 2007, in the context of the Armadillo anti-spam
software project at `Enovad <http://www.enovad.com/>`_, I was given the
requirement that the software must run both under Windows and Linux.

To do this, I had to re-train my team of seasoned Windows system developers to
also be able to deliver a product on Linux. I chose to re-evaluate the tools
and programming language available to me, and this led to my investigation of
Python as a cross-platform development solution.

About Armadillo
---------------

The Armadillo project is an SMTP email filtering proxy that works across
multiple domains and platforms. The project came into being to satisfy the
needs of partner businesses that produce Windows email servers and provide
email hosting with an anti-spam and virus filtering proxy.

We considered using and improving on an open source email server but ran into
trouble making them work on Windows. Most of the mail servers with significant
anti-spam development (see `milter.org <http://milter.org>`_) are strictly
Unix/Linux-based.  Porting them to Windows looked too difficult.  SendMail, for
example, uses a process instance model that won't work well on Windows, while
some of the mail storage formats employed (such as `maildir <http://en.wikipedia.org/wiki/Maildir>`_) rely on characteristics of
Unix filesystem implementations to perform well.

Armadillo is based on some filtering components that we had written previously
and some that we could license from a third party. All of these were written
in C and available only as a C library.

The filtering SMTP proxy consists of a smart spooler, plugin architecture for
filtering libraries, spam/virus report generator, receiver, relayer, policy
object for multiple independent domains, monitor object, and a web configuration
GUI that runs on PHP in Apache and IIS.

.. image:: /files/success/enovad/armadillo-web.gif
   :alt: Armadillo Filtering Process

*Overview of the Armadillo Spam Filtering Process* `Zoom in 
</files/success/enovad/armadillo-full.gif>`_

Why Python?
-----------

We did consider C# since &quot;Mono&quot; supports it and the guys here were already
well-versed in C# development on Windows. However, we lacked confidence that
code developed on Windows would work equally well on Mono, and all development
would need to actively avoid API that would be missing on Mono. The
differences in stability and feature set of the IDEs on Windows and Linux was
also an issue. As a result, we looked at other options, including Python.

At the time of our investigation, Python had reached version 2.5, and a what
we felt was a credible level of maturity. While not a &quot;main-stream&quot; choice,
Python was attractive because of its cross-platform abilities and the
productivity I felt the language could bring to the team.

Some of my team members were skeptical and preferred the tried-and-true power
of C/C++ for systems programming. We decided that those members would work on
the web GUI for configuration of the product, while the rest of us would use
Python for the other components.

Implementation
--------------

We chose to implement Armadillo in an asyncronous style, rather than using
threads. Initially we planned to use `Twisted <http://twistedmatrix.com>`_, a
popular framework for asyncronous programming. However, upon conducting some
stress tests, we found that the Python standard library module ``asyncore`` was
not only robust and fast enough but also easy enough to use for our purposes.

A number of the other standard libraries were also used, and we made use of
some of the `Python recipes <http://code.activestate.com/recipes/langs/python/>`_ provided by
ActiveState. The C filtering libraries that we integrated into the project
were wrapped as extension modules.

For a development environment, we used `Wing IDE <http://wingware.com>`_ as
the preferred IDE. While our test machines ran both on Linux and Windows, we
were able to do all our primary development on Windows, with Wing IDE.

.. image:: /files/success/enovad/architecture-web.gif
   :alt: Armadillo Architectural Overview

*Overview of the Armadillo Architecture* `Zoom in 
</files/success/enovad/architecture.jpg>`_

`Nose tests <http://somethingaboutorange.com/mrl/projects/nose/>`_ and the
standard library module `unittest <http://docs.python.org/library/unittest.html>`_ gave the project a strong
unit testing foundation. This was a crucial component of our development
process that helped us maintain high code quality.

One minor feature of Python development that was really a blessing was the
ability to quickly test text processing code or coding assumptions in the
interactive Python shell.

Outcome
-------

Four months later, the team was surprized to see the filtering product completed
three months earlier than we expected had we used C/C++ for the whole project.

The feature set at this time included: Filtering anti-spam/virus with support
for independent policies across multiple domains, robust 24x7 operation with
low resource usage, self-generated spam reporting, anti-DoS (denial of
service) capabilities, plug-ins for English and Chinese anti-spam as well as
localized spam filters, SMTP-authentication proxy for AUTH LOGIN/PLAIN that
could relay to popular SMTP servers transparently, and it all ran on both
Windows and Linux.

We have since successfully licensed the product to a number of companies and
beat popular branded competitor products in reviews. The product stands as a
testament, at least to the team here, that Python is viable for commercial
systems-level development and not just a scripting language.

Python is now a preferred language at our company for any systems
development projects -- except, of course, device drivers!

About the Author
----------------

*Marcus Low (marcus at enovad dot com) is the R&D Director for
Enovad, Malaysia.  Marcus is the co-founder of InternetNow and
have been actively involved in anti-virus and personal firewall
development with C/C++ since 1994.  He is also the founder of
the Malaysia Python User Group.*