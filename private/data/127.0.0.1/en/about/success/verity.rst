**MISSING**
**MISSING**

Verity Ultraseek: Building Successful Enterprise Solutions with Python
======================================================================

**MISSING**
**MISSING**
**Category:**  Business, Software Development

**Keywords:**  Business Information, Document Management, ROI Case Study, Web Development,

**Title:**  Verity Ultraseek: Building Successful Enterprise Solutions with Python

**Author:**   Ryan Weisenberger; Software Developer; Verity Inc.

**Date:**   2003/03/15 03:58:14

**Web site:**  `http://www.verity.com/ <http://www.verity.com/>`_

**Summary:**  Python was used to write many parts of the original Infoseek Internet search service, and the enterprise search software product Ultraseek Server, now known as Verity Ultraseek.

**Logo:**  .. image:: /files/success/verity/verity-logo.gif    :alt: /files/success/verity/verity-logo.gif

Background
----------

Successful information search is mission-critical. It increases worker
efficiency and saves money. On an external web site, it also increases customer
satisfaction and helps retain users to the web site. The average company can
waste millions of dollars because its employees cannot locate and retrieve the
information that is needed for their jobs.

Infoseek released the original version of Ultraseek Server on March 31, 1997. It
was built by wrapping Infoseek's core search technology with Python, in order to
make it a complete search engine for enterprises. Verity Inc. acquired the
Ultraseek product through its recent acquisition of Inktomi's enterprise search
business in December 2002. The product is now known as `Verity Ultraseek <http://www.verity.com/products/ultraseek/index.html>`_.

.. image:: /files/success/verity/verity-small.jpg
   :alt: Screenshot of Verity Ultraseek

*The New Verity Ultraseek* `Zoom in </files/success/verity/verity.jpg>`_

Verity Ultraseek is an advanced search engine that gives employees of
departments and small to mid-size enterprises the power to quickly find the
information they need to get their jobs done.

Downloadable for free 30-day trials, Verity Ultraseek can be downloaded and
installed on a corporate intranet or website typically within 20 minutes, and
delivers extremely low total cost of ownership.  The software's administrative
and user interfaces are also extremely user-friendly.

Choice of Python
----------------

Python, a language that was previously used to build the Ultraseek Server and
several back-end tasks at Infoseek, was used in creating the Ultraseek spider,
as well as the GUI that provides the end-user search box, results pages, and all
administrative functions.

Python was chosen for several reasons: 

- Python (like Java) is a modern language with objects, modules, threads, exceptions, and automatic memory management. At the time, both C and C++ were rejected as missing at least some of these features.

- The solution needed to be multi-threaded. Neither Perl nor Java was chosen as the solution at the time. Perl was not considered to be as robust. Java did not allow control over the core interpreter. The language was subject to the quirks of the particular Java Runtime Environment (JRE) installed on each system. Although a JRE could have been bundled with the product, it would have substantially bloated the size of the download.

- Python reference counting was found to be superior to Java garbage collection, especially in an environment where response time was critical. Java's approach resulted in brief periods where the search engine was unavailable for several seconds at a time. Python's reference counting method allowed incremental recovery of unused memory, which meant that server threads would always be available to do a search.

- From previous experience with the language, we knew that Python can provide faster development, smaller code volume, access to a rich set of libraries, and fewer memory management bugs to deal with.  Python's built-in serialization features would also simplify saving and restoring state in the engine.

- Python could be used to build a set of internal interfaces, and as a scripting language would allow customers to programmatically alter the behavior of the indexing spider and parser to meet local requirements. This extensibility without the need to learn proprietary scripting languages or API's has been highly regarded by many customers.

- Python could be embedded into the HTML pages that make up the product's user interface, and used during page generation. This was before JSP existed, so our evaluation of Java didn't include that technology.

Some other Python benefits: 

- Python is open source which means we can fix bugs in the interpreter ourselves.

- Ease of integration with C allows for connections to complex C functionality.

- High syntax readability helps decrease development time.

Implementation
--------------

Verity Ultraseek now runs on Windows NT, Linux, and Solaris. 

The overall architecture includes a built-in HTTP server with an underlying
spider to collect web documents, and a query engine to serve search results back
to the user. The interface, including the administrative console, is served over
the built-in HTTP server using Python-scripted HTML. Some of the modules, such
as the search spider, GUI, and HTTP server, were written in Python. For
performance reasons, others, such as the query engine, indexer, and HTML parser,
use the Python/C API to incorporate functionality written in C. The C-based
search engine core was also wrapped as a Python extension module. Some C++ is
used in the interfaces to key third party technologies. Python's flexibility in
this regard gave us a wide degree of flexibility in integration.

Other software packages that are integrated into the product include:
Basistech's JMA, KMA, and Rosette, DataDirect's ODBC Connect, XLT from InXight,
KeyView document filters from Verity, and Adobe Acrobat libraries.

Results
-------

Python was facilitated in a cost competitive environment. Today, more than 2,500
worldwide customers have deployed Verity Ultraseek that uses the Python
language.

The source code, not including third party technology, is approximately 80,000
lines of Python, and less than 150,000 lines of code overall. This includes the
Python-scripted HTML that makes up the user and administrative interfaces which
represents approximately 40,000 lines of the total.

Conclusion
----------

This project has been incredibly successful. 

The Verity Ultraseek development team has been flexible and responsive in
developing, implementing and improving features according to customer feedback.
Python has been very useful in keeping the development environment simple,
flexible, and easy to learn.

During the course of development, only a few disadvantages were found in Python.
One was inability to detect some errors that would typically be uncovered during
compilation (although static error checking tools like PyChecker are now
available for this problem). Another was a result of the very seamless way in
which Python casts between object and data types. While this feature allows for
quick and flexible code, it is the responsibility of the programmer to make
explicit the data types that a function expects. A standard coding style that
names variables according to their expected data type is an easy way to address
this problem.

A 30-day evaluation of Ultraseek 5.2 is available for download at
`http://www.verity.com/ <http://www.verity.com/>`_.

About the Author
----------------

*Ryan Weisenberger is a software developer and project lead for Verity Ultraseek.
He has been involved with the product for four years. Ryan is originally from
southern California, and has been working in the high-tech industry for seven
years.*