**MISSING**
**MISSING**

WordStream Uses Python as Their Platform of Choice
==================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  Internet Marketing, Keyword Tools

**Title:**  WordStream Uses Python as Their Platform of Choice

**Authors:**   Gerard Escalante and Philip Stefou

**Date:**   2009/06/29 16:01:00

**Web site:**  `http://www.wordstream.com/ <http://www.wordstream.com/>`_

**Blog:**  `http://www.wordstream.com/blog <http://www.wordstream.com/blog>`_

**Summary:**  WordStream provides keyword management solutions for search marketers worldwide and uses Python as the basis of their product technology.  Python's increased productivity, reliability and extensibility has enabled WordStream to gain a strategic advantage over its competition.

**Logo:**  .. image:: /files/success/wordstream/wordstream-logo.png    :alt: /files/success/wordstream/wordstream-logo.png

Introduction
------------

`WordStream <http://www.wordstream.com/>`_ is a provider of keyword
management solutions for continuously optimizing and expanding PPC and SEO
efforts, involving large numbers of keywords.  WordStream provides a scalable,
private, online keyword workbench, for conducting keyword discovery, keyword
suggestion, `keyword research <http://www.wordstream.com/keyword-research>`_,
keyword grouping, keyword organization, search marketing workflow, and for
turning research into action.

WordStream has been in development since 2007, and is developed and supported
by an eight person engineering team. The server system is approximately 25,000
lines of Python. The software is deployed to our servers and supports
thousands of users worldwide.

The Architecture
----------------

From a software perspective, WordStream is a high-availability, massively
scalable, distributed, multi-tier client/server database application. The
product is composed of three separate modules:

- The server backend is written in Python, and provides data storage and processing facilities.

- The Graphical User Interface front-end is written in Adobe Flex, and provides aid to the functionality exposed by the server.  It requires a live connection to the server in order to function.

- A JavaScript 'tracking code' is installed on client web pages and provides the server with active web analytics.

Some of the other technologies we're using at the moment for WordStream are
Adobe Flex, Linux, Apache, and C/C++. As for development process tools, we're
using PyDev Extensions, Trac, Buildbot, Review Board, and Git.

The Decision to Use Python
--------------------------

Python was used from the start of this project. It was a bit difficult to
recruit new developers with prior experience in Python, however our experience
so far has been that Python has been a very easy language to pick up. Once you
learn Python, it's hard to go back to using other languages like C/C++.

There were several reasons we decided to user Python as the platform of choice
for WordStream.

First, Python code is extremely and universally readable. Developers from any
language background can read and understand code without having to resort to
much documentation.

Second, Python is a very mature platform, with a wealth of third party
libraries and tools. The Python suite of debugging tools are easy to find and
work extremely well.

Thirdly, Python works seamlessly across platform boundaries, which frees up
our developers so they can use any platform to do their day-to-day
development. It is also very easy to deploy in production, with wide support
from all major Linux distributions.

In addition, Python is suitable for rapid prototyping and development due to
the dynamic type system, native support for common data structures (e.g., hash
maps, sets, and lists), the &quot;batteries-included&quot; standard library, and sane
error handling.

Another reason we chose Python is that it is an excellent language for parsing
as well as operating on collections with ease (iterating, concatenating,
intersecting, etc.).

Last but not least, if performance ever becomes an issue, it is easy to write
extensions using the Python/C API.

Understand that we did evaluate other solutions, which included Ruby and Java.
But our impression of Ruby was that it was too immature at the time and Java
can often be unpleasant to work with.

Project Results
---------------

It is imperative that we provide 24/7/365 availability to our clients, as
WordStream is an online Software as a Service solution used by people all
around the world. Given that prerequisite, Python has performed magnificently.

Python has proven to be a very powerful and flexible language in terms of both
parsing and data manipulation. There are a host of favorable reviews and kudos
online that praise Python and the product definitely delivers.

Being an early stage start-up, it is always a challenge to convince talented
engineers to leave their current positions and sign on with our development
team. One of our most productive engineering hires had a C/C++ programming
background with no prior experience with Python, yet was able to quickly learn
and be productive using the language. In fact, he cited the productivity of
Python language as being one of the reasons for signing on with us!

Python does have some minor shortcomings in the areas of raw processing
performance, and its operation in multi-threaded environments. However, these
concerns are easily addressable using C extensions, or by building on a
multi-process execution model.

Conclusion
----------

In summary, we believe the choice to base our product technology on Python
provides WordStream with a strategic, technological advantage over our
competitors because of the increased productivity, reliability and
extensibility that it enables.

About the Authors
-----------------

`Gerard Escalante <http://www.wordstream.com/gerard-escalante>`_ is Vice
President of Engineering at WordStream. He has a Bachelor of Applied Science
degree in Computer Engineering at the University of Waterloo in Canada.

Philip Stefou is a Sr. Software Engineer at WordStream.