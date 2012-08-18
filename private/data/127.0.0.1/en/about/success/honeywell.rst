**MISSING**
**MISSING**

Honeywell Avoids Documentation Costs with Python and other Open Standards
=========================================================================

**MISSING**
**MISSING**
**Category:**  Business, Software Development

**Keywords:**  XML, Fortune 500, ROI Case Study, Documentation Development

**Title:**  Honeywell Avoids Documentation Costs with Python and other Open Standards

**Author:**   Andrew Jonathan Fine

**Date:**   2005-06-13

**Website:**  `http://www.honeywell.com/ <http://www.honeywell.com/>`_

**Summary:**  Honeywell integrates Python, COM, DocBook, OpenJade, and Word to create a documentation tool that yields substantial return on investment.

**Logo:**  .. image:: /files/success/honeywell/honeywell_logo.gif    :alt: /files/success/honeywell/honeywell_logo.gif

Introduction
------------

This article shows how I integrated Python, COM, DocBook, OpenJade, and Word
together to create a documentation tool for BEACON, a visual programming
environment. This documentation tool was used for code reviews in the software
development methodology at my company, and led to significant (>$1M) in cost
savings.

Before starting this project, I had no prior experience using SGML, XML, or
other document markup languages. It was only when I was perilously close to
reinventing the concept of markup languages, by adapting direct
PythonCOM-to-Word interfaces from Mark Hammond's book Python Programming on
Win32, that I decided there had be a better way to do this from a design
and maintenance standpoint.

A Web search provided me with a crash course on markup languages such as XML,
HTML, and SGML. My search also provided insight into DocBook SGML, a popular
open standard, and OpenJade, an open source package that can translate DocBook
SGML into Word Rich Text.

This arrangement wasn't perfect but I quickly realized that I could use it to
save a year in development and maintenance costs, and to respond more quickly
to new assignments.

The Core Data Flow
------------------

My primary task was to translate arbitrary data mined from various sources
scattered throughout my organization into sensible-looking Microsoft Word 97
reports.

I decided that this was best handled through a core pipeline of applications
that cooperated with each other using common data conventions. This pipeline
would be controlled by a Python generator application that would drive a set
of front end translators, a content inserter, and a post-processing formatter
to generate the reports.  Python had recently been chosen as our department's
successor language for automated test scripts. I noticed Python's potential
beyond use for testing, so I obtained permission from my manager to use it
for this task.

The front end translators in this application harvest content (pictures,
tables, paragraphs) from various data sources and place it into a dictionary.
The content inserter creates a Word document and inserts values from the
dictionary into it. The post-processing formatter takes the result and
modifies it according to the latest corporate Word format style template.

This flow was designed to cope with changes in requirements by the different
teams within our department, and by corporate-level standards. For example,
the layout of reports was determined by the generator application in a layout
class that could be replaced with other classes to support new types of
reports.

The first front-end translator I needed to create was to take pictures,
tables, and data from recursive property lists constructed by an aerospace
industry software visual programming tool called BEACON. From this translator
I was able to obtain a huge amount of sample data fit for testing the Word
content inserter.

Problems with the Inserter
--------------------------

The first version of the content inserter was based on principles demonstrated
in *Python Programming on Win32*, which contains a detailed description of how
Python can create and manipulate Word documents with the Word 97 COM object
model.  This implementation inserted the content into Word documents by
driving Word directly through its COM interface.

Unfortunately, the COM interface was much too slow to handle the massive
number of table cells that were extracted from the BEACON source code.

Worse were the reuse issues with the classes I was writing for dealing with
the different stylistic requirements at the different levels of sections,
headings, paragraphs, and phrases.

To address these problems, I considered writing ASCII text files to specify
margins, font, heading level, and insertion points for standard forms. But
inventing my own standard for text-specified typesetting would have been time
consuming and costly both to develop and to maintain.

What I really needed was a Python API to quickly generate nicely typeset copy
in Word 97 for a limited set of documents, but in 2001 there was nothing
available to do this. My only alternative was to find an open standard for
typesetting that could be translated into Word 97 format after documents had
been generated.

Shopping for a Standard
-----------------------

To find a solution, I spent some time surveying available open source
typesetting solutions. The two most popular are `TeX <http://www.math.upenn.edu/TeX.html>`_ and `DocBook <http://www.docbook.org/>`_, both of
which are supported by open source implementations written in C.

DocBook was chosen because it had more clearly defined and documented
production rules for typesetting elements. `DocBook, The Definitive Guide <http://www.docbook.org/tdg/en/html/docbook.html>`_
is a real treasure when it comes to explaining these rules in detail.

DocBook provides a set of Document Type Definition (.DTD) and Document
Stylesheet (.DSL) files written in DSSSL, the Document Style Semantics and
Specification Language.  DocBook comes packaged in two flavors, one for SGML
and the other for XML document encoding.  Both SGML and XML have similar nested
structures of tags and the same logical structure for the DTDs and DSLs.
However, the XML rules were still under development during 2001, so I chose
the more reliable and mature SGML rule set.

DocBook also provides the ability to write local document type definitions
and style sheets, called ``Local.DTD`` and ``Local.DSL``, respectively.
These allow for the introduction of additional document elements, and
their renderings, on top of those provided by DocBook.

For example, some of the teams at my company wanted features in the final Word
document that amounted to arbitrary Word field-code support in the SGML.

To support this, I wrote a local DocBook stylesheet and definition file pair
``(Local.DSL, Local.DTD)`` to emit the sequences in RTF corresponding to the
desired field codes. RTF requires unescaped characters ``{``, ``}``, and
``\\``, so I modified OpenJade to map Unicodes ``0xFFFD``, ``0xFFFE``, and
``0xFFFF`` in the stylesheet to these unescaped characters.

I also found an `archived post <http://lists.oasis-open.org/archives/docbook-apps/200011/msg00183.html>`_ on the docbook-apps mailing list that was
extremely helpful for aligning the contents of DocBook download components
into a workable hierarchy.

An Example Python API for DocBook
---------------------------------

To support development of the necessary content inserter with DocBook, I
needed a Python API that could be used to quickly generate the SGML formatted
documents. The design chosen for this API provides abstract classes for each
document element type in a `DocBook <http://www.python.org/pycon/2005/papers/14/Paper14/HTML/paper/Paper14.mht>`_ Python module. These abstract classes
can be inherited in code that defines particular document structures, and can
be nested arbitrarily, so that each maps to a different level or part of the
output document's structure.

As an example, suppose we want to generate the following table as part of a
Word document:

    **MISSING**
    **Name**   **Type**
    *statex*   Integer

    *statey*   Long

The SGML text used for this table is written in terms of ``Local.DSL`` and
``Local.DTD`` as follows:

.. code-block::

    <;!DOCTYPE informaltable SYSTEM &quot;C:\Local.dtd&quot;>
    <;informaltable frame='all'>
    <;tgroup cols='2' colsep='1' rowsep='1' align='center'>
    <;colspec colname='Name' colwidth='75' align='left'><;/colspec>
    <;colspec colname='Type' colwidth='64' align='center'><;/colspec>
    <;thead>
    <;row>
    <;entry><;emphasis role='bold'>Name<;/emphasis><;/entry>
    <;entry><;emphasis role='bold'>Type<;/emphasis><;/entry>
    <;/row>
    <;/thead>
    <;tbody>
    <;row>
    <;entry><;phrase role='xe' condition='italic'>statex<;/phrase><;/entry>
    <;entry>Integer<;/entry>
    <;/row>
    <;row>
    <;entry><;phrase role='xe' condition='italic'>statey<;/phrase><;/entry>
    <;entry>Long<;/entry>
    <;/row>
    <;/tbody>
    <;/tgroup>
    <;/informaltable>

Here is the Python listing that generates the above SGML by basing on the
DocBook class tree:

.. code-block::

    from DocBook import DocBook

    class ItalicIndexPhrase (DocBook.Rules.Phrase):

        &quot;italic indexible text phrase&quot;
        TITLE    = DocBook.Rules.Phrase
        def __init__        (self, text):
            DocBook.Rules.Phrase.__init__ (self, 'xe', 'italic')
            self.data = [ text ]

    class NameCell          (DocBook.Rules.Entry):

        &quot;table row cell describing name of identifier (italic and indexible text!)&quot;
        TITLE    = DocBook.Rules.Entry

        def __init__        (self, text):
            DocBook.Rules.Entry.__init__ (self)
            self.data = [ ItalicIndexPhrase (text) ]

    class StorageCell       (DocBook.Rules.Entry):

        &quot;table row cell describing storage type of identifier (ordinary text)&quot;
        TITLE    = DocBook.Rules.Entry
        def __init__        (self, text):
            DocBook.Rules.Entry.__init__ (self)
            self.data = text

    class TRow              (DocBook.Rules.Row):

        &quot;each row in application's informal table body&quot;
        TITLE    = DocBook.Rules.Row
        def __init__        (self, binding):
            (identifier, storage) = binding
            DocBook.Rules.Row.__init__ (self, [ NameCell    (identifier),
                                                StorageCell (storage)
                                              ])

    class TBody             (DocBook.Rules.TBody):

        &quot;application's informal table body&quot;
        TITLE    = DocBook.Rules.TBody

        def __init__        (self, items):
            DocBook.Rules.TBody.__init__ (self, map (TRow, items))

    class TGroup            (DocBook.Rules.TGroup):

        &quot;application's informal table group&quot;

        COLSPECS = [ DocBook.Rules.ColSpec ('Name', 75, 'left'),
                     DocBook.Rules.ColSpec ('Type', 64, 'center')
                   ]

        SHAPE    = [ '2', '1', '1', 'center' ]
        TBODY    = TBody

    class InformalTable     (DocBook.Rules.InformalTable):

        &quot;application's informal table&quot;
        TGROUP   = TGroup

    class Example           (DocBook):

        'example application of DocBook formatting class'
        SECTION  = str  (InformalTable)
        def __call__    (self):
            self.data = [ InformalTable ()(self.data) ]
            return DocBook.__call__ (self)

    if __name__ == '__main__':
        print Example ([('statex', 'Integer'), ('statey', 'Long')]) ()

The OpenJade Interface
----------------------

`OpenJade <http://openjade.sourceforge.net/>`_ is an open source product that provides a means to get from SGML
encoded documents to Microsoft Rich Text Format (RTF). It reads the DocBook
DSSSL stylesheets and user's local DSSSL stylesheets, if any. The DSSSL is
executed upon the user's SGML source text to write a final document to load
into the user's word processor.

For this project, we wanted to automatically generate files readable by
Microsoft Word, so OpenJade was set to emit Microsoft Word Rich Text files.
OpenJade operates as a command-line application, and thus is simple to control
from Python code with the ``Popen4`` Python standard library call.

Post-Processing using Word Automation with PythonCOM
----------------------------------------------------

The Microsoft Rich Text Format files created by OpenJade are quite attractive
in overall appearance. However, they did not conform with many of the
corporate level standards for formatted Word documentation files.

A local DSSSL stylesheet (Local.DSL) was written to override several of the
default DocBook DSSSL settings and bring them into alignment with corporate
standards. However, this did not address the need to set standardized Word
style identifiers names in the documents.

To solve this problem, a reformatter was needed as the final stage of the
document pipeline. It accesses Word as a COM object in order to traverse the
table, figure, heading, and section level style identifiers at the various
levels of the generated RTF document's object model. During traversal, it
renames style identifiers to conform with those provided in a Microsoft Word
Document Template (.DOT) file handed out as a standard by our local
reprographics department.

After this conversion, the post-processor saves the finished document in
Microsoft Word document format.

None of the post-processing tasks were particularly difficult. Once the COM
interface to a Win32 application is well understood, that application devolves
into just another library in the hands of a Python developer.

Return On Investment
--------------------

The assumptions used to derive the return on investment (ROI) figures
presented here are conservative.

I spent the bulk of 2001 developing a system using the ideas in this paper to
automatically translate content from a BEACON visual programming language file
directly into a Word document. In 2002 I also made significant revisions to
the software. My total effort in development, maintenance, and support was
about half time over a two year period.

Between the years 2002 and 2003, my department had 5 ongoing projects at
various stages of development ranging in complexity from 30 visual programming
files to as many as 150, perhaps 75 on average.

During each of these years for each of those projects, there were at least 2
major mandated releases where the important contents of every file had to be
peer reviewed: examined in detail by no less than 3 engineers simultaneously
(moderator, author, and inspector).

Each of these releases required that every visual programming file be rendered
into a viewable hard copy format containing all of its diagrams; and a
cross-referenced table of all identifiers in every diagram with storage
classes, ranges, initial values, documentation, and other fields.

The visual programming language GUI application, BEACON, has no comprehensive
hardcopy generator. Instead, it would take an entry level engineer working
under moderate supervision to inspect the file with BEACON running on UNIX
over a UNIX to Win32 X terminal emulator, manually transferring text from the
X terminal into an open Word document.

The least complex of these files (about 20%) would take half a day. The bulk
of the files (60%) would take an entire day on average. The most complex of
these files (about 20%) would take at least 2 days.

This stood to waste significant engineering labor that was better spent in
improving the quality of my department's software products.

.. code-block::

    Each project release:       1/5 * 75 *  4 hours     =           60  hours
                                3/5 * 75 *  8 hours     =          360  hours
                                1/5 * 75 * 16 hours     =          240  hours
                                                                -------------
                                                                   660  hours

    Two major releases per year:        * 2             =        1 320  hours
    Five projects needing releases:     * 5             =        6 600  hours
    Two year period (2002-2003)         * 2             =       13 200  hours
    Total effort avoided:                                       13 200  hours

    Automated releases over 2 year period:                         160  hours
    My effort (12 * 140 hours per labor month):                  1 680  hours
    Total investment:                                            1 840  hours

    Net effort avoided, 2002-3:                                 11 360  hours
    Net cost avoided by customers 2002-3 at $100/hour        1 136 000  dollars
    Net labor years avoided at 1680 hours/year:                   6.76  years
    Head count avoided per year:                                  3.38  people

    ROI (Total effort avoided / total invested) 2002-3:           7.17

From the table above, the return on investment for automating the generation
of documentation just for formal releases to customers clearly helped my
department avoid a substantial amount of manual labor cost.

Python and DocBook together proved to be a formidable combination for
eliminating a real-world business process bottleneck.

Conclusion
----------

The decision of my department to adopt Python and to allow me to use it along
with another open standard, DocBook, has been vindicated by a substantial
return on investment over a medium term period of time, even if only in terms
of documentation costs avoided.