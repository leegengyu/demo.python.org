**MISSING**
**MISSING**

Suzanne: Python Handles Critical Data in a Domain Name Landrush
===============================================================

**MISSING**
**MISSING**
**Category:**  Business, Software Development

**Keywords:**  High Availability, Testing, Ecommerce, Quality, Network Development

**Title:**  Suzanne: Python Handles Critical Data in a Domain Name Landrush

**Author:**   Stephane Bortzmeyer

**Date:**   2004-05-29

**Website:**  `http://www.afnic.fr/ <http://www.afnic.fr/>`_

**Summary:**  Python helps AFNIC manage over 10,000 internet domain name registration requests per minute in a landrush for the &quot;.fr&quot; top-level internet domain.

**Logo:**  .. image:: /files/success/suzanne/afnic-logo.gif    :alt: /files/success/suzanne/afnic-logo.gif

Introduction
------------

`AFNIC <http://www.afnic.fr/>`_ is the registry of the French **.fr** top-level internet domain. For
many years, registration rules in **.fr** were very strict. On May 11th, 2004,
`the rules changed <http://www.afnic.fr/actu/nouvelles/nommage/CP20040120>`_ to a more liberal model, allowing many registrations
that were not possible before. As a consequence of this change, the registry
was faced with receiving a potentially unmanageable burst of requests. This is
a problem known as a &quot;landrush&quot; faced by every DNS registry which changes its
rules or introduces a new service, like Unicode domain names.

Since the rule of registries is &quot;first come, first served&quot;, everybody wants to
have their submission arrive immediately after the new domain space is
available, in this case May 11th, 09:00, local time. In this context, some
domain names were requested by three different clients within the very same
second.

Machine crashes are a sad tradition at registries resulting in unexpected
delays, clients frantically hitting Submit while trying to send a completed
Web form, and bad press for the registry afterwards.

For a variety of reasons, this particular landrush was a technical success,
with zero crashes.  This article focuses on the role that Python played
in this success.

Buffering the Requests
----------------------

The AFNIC registration system was written years ago, mostly in Perl. It
responds to registration requests, satisfies them, and then returns
confirmation to the web client, all in one synchronous request/response cycle.
Although this system works well during normal load, it simply cannot handle
the load of a landrush. Even more modern systems that are parallelized across
many machines will fail under the impossible load of a landrush, where web
requests from clients must be answered in a synchronous manner.

To avoid this bottleneck without attempting to rebuild the whole registration
system, AFNIC decided to place an asynchronous buffer between the client and
the main registration application. This buffer was not a full-fledged system,
it just received the requests, stored them in FIFO order, acknowledged them
and later handed them over to the real registration system within the limits
of its processing capacity.

This asynchronous buffer was written in Python and is named Suzanne, from the
novel *Un barrage contre le Pacifique* by Marguerite Duras, where the hero's
mother tries to protect her land from the waves of the Pacific ocean.

The requirements for Suzanne were simple: it had to be fast, robust, reliable,
and it had to work the first time around, because there was no second chance.
Protecting the data was extremely critical: while the big frenzy of domain
name speculation is over, many companies are still ready to spend a lot of
money for a domain name. If they miss the domain name they want because buggy
software dropped a request, the registry is faced with bad press at the
minimum, and possibly expensive litigation.

Why Python?
-----------

AFNIC uses many programming languages (Perl, Java, PHP, PL/SQL, and Ruby) but
this was the first use of Python. Like Perl and Ruby, Python includes the
standard libraries that were required by this project. Python was chosen for
its readability and ease of use.

Implementation
--------------

Most of the brutal load was handled by the Postfix mail system. All requests
were received by email, which is asynchronous and thus avoids the
above-mentioned limitations of synchronous processing. Suzanne was in charge of
rotating mailboxes to keep them at a manageable size, and emitting
acknowledgement emails. This process used Python's standard library modules
**mailbox**, **email**, and **smtplib**, and the `Cheetah <http://www.cheetahtemplate.org/>`_ templating system
was used to create the acknowledgement messages.

When dealing with critical data accessed by several programs, all running at
full speed under a heavy load, it is critical to to prevent hidden race
conditions. Since Python currently lacks a standard global locking module, the
`glock <http://rgruet.free.fr/glock.py>`_ module by Richard Gruet was used to lock the mailboxes.

Once messages had been processed and acknowledged, Suzanne had to send
requests to the real registration system. Since SOAP is the standard in-house
inter-application protocol, AFNIC created a Web service in Python, using `ZSI <http://pywebsvcs.sourceforge.net/zsi.html>`_
and the standard library's `BaseHTTPServer <http://www.python.org/doc/current/lib/module-BaseHTTPServer.html>`_. The SOAP client was the
registration system, running Perl.

This project used Python version 2.3 and various Unix platforms. Suzanne is
very small: Just 2290 lines of Python, including the testing programs and the
statistics programs.

Testing was the key to success in this application, which had to perform
flawlessly during its first production run. Many bugs were uncovered by
testing Suzanne under load, first in-house, with several machines sending as
many requests as possible, and later by volunteers sending requests from the
outside.

Problems Encountered
--------------------

Some problems were encountered during the implementation.  Working with mail
boxes and email messages in Python is somewhat complicated by the many modules
in the standard library provided for this purpose.  For this application,
these modules were often too low-level, requiring somewhat more work that
was initially expected.

ZSI also caused some trouble, and was sometimes difficult to use. The authors
used `SOAPpy <http://sourceforge.net/project/showfiles.php?group_id=26590&package_id=18246>`_ on other projects, which in hindsight may have been a better
choice. Some of these problems stem from the fact that SOAP is complicated and
difficult to deal with in general, and were not always the fault of Python or ZSI.

Successes
---------

Nevertheless, development of the system was quite fast, the resulting code
is simple and readable, and the system performed well.

Suzanne was able to handle the required processing with acceptable system
load. Mail boxes were parsed and acknowledgements sent at a very satisfactory
rate. And best of all, nothing crashed during the landrush, even with 12,000
messages in the first minute, a result of the fact that many clients developed
custom programs to start submitting requests at exactly 09:00.

Suzanne performed so well that AFNIC is considering making it a permanent part
of its infrastructure. If this is done, every request would go through
Suzanne, allowing the registration system to work at its own pace regardless
of unexpected peaks in future request activity.

About the Author
----------------

*Stephane Bortzmeyer <;bortzmeyer@nic.fr> is network and systems architect at
AFNIC. He has worked for many Internet companies, from network operators to
Web agencies, and developed software in Perl, Ada and C before adopting
Python as well.*