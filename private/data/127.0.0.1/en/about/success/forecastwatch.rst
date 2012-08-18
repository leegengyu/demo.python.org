**MISSING**
**MISSING**

ForecastWatch.com Uses Python To Help Meteorologists
====================================================

**MISSING**
**MISSING**
**Category:**  Software Development, Business, Scientific

**Keywords:**  Database, Data Mining, Web2.0, Knowledge Management, Quality, Scientific Programming, Weather

**Title:**  ForecastWatch.com Uses Python To Help Meteorologists

**Authors:**   Eric Floehr

**Date:**   2004-05-26

**Website:**  `http://www.intellovations.com/ <http://www.intellovations.com/>`_

**Summary:**  ForecastWatch.com uses Python to help meteorologists create more accurate weather forecasts.

**Logo:**  .. image:: /files/success/forecastwatch/forecastwatch-logo.png    :alt: /files/success/forecastwatch/forecastwatch-logo.png

Introduction
------------

`ForecastWatch.com <http://www.forecastwatch.com/>`_, a service of `Intellovations <http://www.intellovations.com/>`_, is in the business of
rating the accuracy of weather reports from companies such as `Accuweather <http://www.accuweather.com/>`_,
`MyForecast.com <http://www.myforecast.com/>`_, and `The Weather Channel <http://www.weather.com/>`_. Over 36,000 weather forecasts
are collected every day for over 800 U.S. cities, and later compared with
actual climatological data. These comparisons are used by meteorologists to
improve their weather forecasts, and to compare their forecasts with others.
They are also used by consumers to better understand the probable accuracy of
a forecast.

The Architecture
----------------

ForecastWatch.com is built from four major architectural components:  An
input process for acquiring forecasts, an input process for acquiring measured
climatological data, the data aggregation engine, and the web application framework.

There are two main input processes in the system: The forecast parser, and the
actuals parser. The forecast parser is responsible for requesting forecasts
from the web for each of the forecast providers ForecastWatch.com tracks. It
parses the forecast from the page and inserts the forecast data into a
database until it can be compared to the actual data. The actuals parser takes
actual data from the National Climatic Data Center of the National Weather
Service, which provides high, low, precipitation, and significant weather
events for over 800 United States cities and inserts the data into the
database. This process also scores the forecasts with the actual weather data,
and places that information in the database.

Once the data has been collected and scored, it is processed by the
aggregation engine, which combines the scores into yearly and monthly blocks,
sliced by provider, location, and the number of days into the future for which
the forecasts were predicting. In its first year, 2003, the system only
gathered forecasts for 20 U.S. cities, or about 250,000 individual forecasts,
so most of the data output was based on the raw scoring data. The aggregation
engine was added once the system was scaled up to 800 cities, increasing the
data stream by almost 4000%. In the first half of 2004, the system has already
scored over 4 million forecasts, all collected, parsed, and displayed on the
web.

.. image:: /files/success/forecastwatch/screenshot-web.png
   :alt: Screenshot of ForecastWatch.com

*ForecastWatch.com can be used to determine the accuracy of weather forecasts,
for example by reviewing maps of error magnitude in forecast low and high
temperatures* `Zoom in </files/success/forecastwatch/screenshot.png>`_

The last component in ForecastWatch.com's architecture is the website itself.
This is the interface through which customers access the collected and
aggregated forecast accuracy information.

Implemented with Python
-----------------------

ForecastWatch.com is a 100% pure Python solution.  Python is used in all
its components, from the back-end to the front-end, including also the
more performance-critical portions of the system.

Python was chosen initially because it comes with many standard libraries
useful in collecting, parsing, and storing data from the web. Among those
particularly useful in this application were the regular expression library,
the thread library, the object serialization library, and gzip data
compression library. Other libraries, such as an HTTP client capable of
accepting cookies (`ClientCookie <http://wwwsearch.sourceforge.net/ClientCookie/>`_), and an HTML table parser
(`ClientTable <http://wwwsearch.sourceforge.net/ClientTable/>`_) were available as third party modules. These proved
invaluable and were easy to use.

The threading library turned out to be very important in scaling
ForecastWatch.com's coverage to over 800 cities. Grabbing web pages is a very
I/O bound process, and requesting a single page at a time for roughly 5000 web
pages a day would have been prohibitively time-consuming. Using Python's
threading library, the web page retrieval loop simply calls
**thread.start_new()** for each request, passing in the necessary class
instance method that retrieves and processes the web page, along with the
parameters necessary to describe the city for the desired forecast. The
request classes use a Python built-in **Event** class instance to communicate
with the main controlling thread when processing is complete. Python made this
application of threading incredibly easy.

Python is also used in the aggregation engine, which runs as a separate
process to combine forecast accuracy scores into monthly and yearly slices. The
aggregation process uses queries via `MySQLdb <http://sourceforge.net/projects/mysql-python>`_ to the `MySQL <http://www.mysql.com/>`_ database
where the input modules have placed the forecast and climatological data they
have harvested. Colorized maps, showing forecast accuracy by geographical
area, are then generated for use on the web site and in printed reports.

.. image:: /files/success/forecastwatch/accuracy_map.png
   :alt: Example Forecast Accuracy Map

*This forecast accuracy map uses intensity of blue and red to indicate
the degree of error in predicting temperatures by geographical area*

ForecastWatch.com's web interface was originally written in PHP but later
changed to Python to simplify the toolset and improve integration with the
other components of the system. `Quixote <http://www.mems-exchange.org/software/quixote/>`_, a Python web application
framework, was selected as the basis for the entirely Python-based web
front-end. The Quixote-based web application runs on Linux using `Apache <http://www.apache.org/>`_
with `mod_scgi <http://www.mems-exchange.org/software/scgi/>`_, and was able to serve pages as fast as the PHP-based
implementation. Python made it easier to make changes and add features than
the PHP implementation. Quixote also provided for more flexible
crafting of URLs, replacing PHP URLs like this one:

.. code-block::

    http://www.forecastwatch.com/drilldown.php?s=2&m=2&d=1&p=1&st=33

With easier to manage URLs like this: 

.. code-block::

    http://www.forecastwatch.com/drilldown/awx/2004/02/1/AL

This is much nicer for the customer to bookmark or share with clients or
potential clients. Finally, Quixote was easy to use and integrates well
with Apache. For example, a redirect in Quixote is simply:

.. code-block::

    request.redirect(path-or-URL)

Python Made It Possible
-----------------------

Python played a significant role in the success of ForecastWatch.com. The
product currently contains over 5,000 lines of Python, most of which are
concerned with implementing the high-level functionality of the application,
while most of the details are taken care of by Python's powerful standard
libraries and the third party modules described above.  Many more lines
of code would have been needed working in, for example, Java or PHP.  The
integration capabilities of those languages are not as strong, and their
threading support is harder to use.

Python is impressive as an object-oriented rapid application development
language. One of Python's key strengths lies in its ability to produce results
quickly without sacrificing maintainability of the resulting code. In
ForecastWatch.com, Python was used for prototyping as well, and those
prototypes were able to evolve cleanly into the production code without
requiring a complete rewrite or switching toolsets. This saved substantial
effort and made the development process more flexible and effective.

Because of the clean design of the language, refactoring the Python code was
also much easier than in other languages; moving code around simply requires
less effort.

Python's interpreted nature was also a benefit: Code ideas can easily be
tested in the Python interactive shell, and lack of a compilation phase makes
for a shorter edit/test cycle.

All of these factors combine to make Python a terrific alternative to C++ and
Java as a general purpose programming language. ForecastWatch.com was made
possible because of the ease of programming complex tasks in Python, and the
rapid development that Python allows.

About the Author
----------------

*Eric Floehr specializes in large-scale data collection & analysis, and
consumer internet software, having worked with such companies as MCI,
Datalytics, and Battelle. He holds a degree in Computer and Information
Science from The Ohio State University. He has been in the technology industry
for over 13 years, and is founder of Intellovations, LLC, a technology
consulting company focused on building software for discovery -- challenging
projects that bring new information and knowledge into businesses for
competitive advantage, higher productivity, and greater profit. Intellovations
has offices in Marysville, Ohio, and can be found on the web at*
`http://www.intellovations.com <http://www.intellovations.com>`_.