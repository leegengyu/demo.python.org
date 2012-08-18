**MISSING**
**MISSING**

Python On Guard
===============

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  rapid, application, development, building, wireless, messaging, automation, alarm, notification

**Title:**  Python On Guard

**Author:**   Ivan Lehecka

**Date:**   2007/05/23 13:00:00

**Web site:**  `http://www.vahnzcontrols.com/ <http://www.vahnzcontrols.com/>`_

**Summary:**  VAHNZ Controls uses Python to monitor sensors and generate alerts delivered as text messages to cell phones.

**Logo:**  .. image:: /files/success/guards/logo.gif    :alt: /files/success/guards/logo.gif

Introduction
------------

Internet connectivity is omnipresent, finding new applications and giving old
designs a new lease on life. In this age of small IC devices boasting TCP/IP
stacks and wireless connectivity, one no longer needs a standalone PC to
harness the Web.

VAHNZ Controls developed its eBukal`[1] <#id6>`_ remote alarm device to leverage their
knowledge of microcontroller interfacing and Internet protocols, creating an
innovative solution for the field of building automation.

Remote Event Dial-up Internet Notification
------------------------------------------

The idea grew out of one client's need to monitor the temperature of an office
building's air conditioning during one long hot summer in Portland. The office
property manager wanted to be alerted before the temperature in offices became
unbearable and the tenants complained. The application is not limited to only
detecting temperature changes, but has been used with a variety of input
devices such as proximity switches and flood sensors.

Version one of the design used DTMF tones to leave the numeric message on the
office manager's phone. Besides the crudeness of deciphering the meaning of
the digits, the calling device also had to negotiate the timing pitfalls in
the recipient's voicemail system to select the one option for leaving the
digital feedback. The resulting system was neither robust nor pretty.

Text messaging seemed to be the right way to go, because messages are easily
received by any mobile phone. Most wireless providers maintain email to SMS
gateways, and many off-the-shelf devices can generate email messages. I was
only limited by the necessity of dial-up connectivity -- many locations
containing monitored equipment proved impervious to wireless signals.

After coming up with the basic idea to use text messages and selecting the
components, I had to figure out how to make the individual parts work
together.

Email messages coming from the eBukal device had to be parsed on the server
to determine the recipient(s) to be notified and the online logbook that
should receive the entry. New devices had to be added to the configuration
file. Parameters such as the threshold, phone number to dial, and so forth,
had to be sent to eBukal via serial port. A graphical user interface (GUI)
had to be written to enable personnel in the field to set the device.

.. image:: /files/success/guards/system-diagram.png
   :alt: Diagram: eBukal used to monitor water conditions in a basement

*How eBukal is used to monitor water conditions in a basement* `Zoom in 
</files/success/guards/system-diagram-large.png>`_

I knew how to write command line scripts and PHP to do the server coding and
used Perl for CGIs and Visual Basic for the GUI, but I wanted to do it
better this time. I wanted to do it right.

Python - one stop shopping development plus platform independence
-----------------------------------------------------------------

I used Python before and it seemed to have the potential to do all the
required coding and was a programming language that I enjoyed using. I was not
entirely confident about some parts of the task, especially building a
graphical user interface, but decided to face my fears, trusting to Python's
maturity, powerful libraries, and third-party support.  The SPE editor together
with Python's interpreted nature proved especially valuable.

.. image:: /files/success/guards/gui-screenshot.gif
   :alt: A screen shot of the eBukal user interface

*Screen shot of the eBukal messaging configuration user interface, based on
wxPython*

After some trial and error I settled on the final concept using the
following standard library and third party modules:

- **email, time, and ConfigParser** -- for email parsing, phone message generation and log book entry on the server side

- **cgi and sha** -- for a CGI module to edit the server configuration file

- **wxPython and wx.xrc** -- for the GUI written in XRCed

- **serial, pickle, ConfigParser, and time** -- for the serial-communication library for eBukal setpoint download

Unfortunately there is no PIC compiler using Python syntax; if such a tool
existed, the circle would have been completed.  As a result, the microcontroller
code is written in PicBasic Pro, a popular commercial product from MicroEngineering
Labs, Inc.

.. image:: /files/success/guards/onlinelog.gif
   :alt: Screen shot of the eBukal online log

*Screen shot of the online log of events from eBukal, with alerts in red
and informational messages for daily diagnostics* `Zoom in </files/success/guards/onlinelog-large.gif>`_

The gamble paid off. The system works well and many bells and whistles
could be added:  A server logging feature, daily diagnostics, and online
configuration. Python delivered more than I was asking, and some features were
added based on availability of the functionality in the library modules being
used.

Summary
-------

This may not yet be VAHNZ Controls' killer application, but I feel that the
selection of the Python programming language is a move in the right direction.
Technology is always evolving and no one knows what comes next, but I am
confident that Python will be there ready for the challenge. Platform
independence is another aspect to feel good about -- betting all the
chips on one player might be riskier than ever in today's climate.

For more information, visit VAHNZ Controls on-line at `eBukal.vahnzcontrols.com <http://eBukal.vahnzcontrols.com/>`_
or contact `info at vahnzcontrols.com <mailto:info%40vahnzcontrols.com>`_.

About the Author
----------------

*Ivan Lehecka is founder of VAHNZ Controls, a company that strives to bring
intelligence to building automation and other fields, where suitable.*

**MISSING**
`[1] <#id1>`_  eBukal is a trademark of VAHNZ Controls.