[![CRAN
Version](http://www.r-pkg.org/badges/version/pollstR)](http://cran.r-project.org/package=pollstR)
![Downloads](http://cranlogs.r-pkg.org/badges/pollstR) [![Build
Status](https://travis-ci.org/rOpenGov/pollstR.svg?branch=master)](https://travis-ci.org/rOpenGov/pollstR)

**IMPORANT:** The Pollster API is no longer actively maintained. As of now, no new polls are being added to it. See this [Google Group message](https://groups.google.com/d/msg/pollster-users/9ECuy8AG5TA/eiCNMutfCQAJ) for more information. This package should still work to retrieve any historical polls that had been entered.

pollstR: An R Client for the HuffPost Pollster API
==================================================

The **pollster** package provides an R client for the Huffpost Pollster
API. [Huffpost Pollster](http://elections.huffingtonpost.com/pollster)
tracks and aggregates US public polls on elections and political
opinions. The [API](http://elections.huffingtonpost.com/pollster/api)
provides programmatic access to the data.

This package is part of the [ROpenGov](http://ropengov.github.io/)
project.

Install
-------

You can install the stable version on
[CRAN](http://cran.r-project.org/package=pollstR):

    install.packages('pollstR', dependencies = TRUE)

To install the latest version:

    library("devtools")
    install_github("rOpenGov/pollstR")

Usage
-----

    library("pollstR")

The function `pollster_api` provides a thin wrapper to the make requests
of the API:

    pollster_api("polls")

For more information, see full documentation for the
[API](https://app.swaggerhub.com/api/huffpostdata/pollster-api/2.0.0).

### API Methods

There is also a function for each API method.

Return a list of polls:

    pollster_polls()

Get a specific poll by its identifier

    pollster_polls_slug("gallup-26892")

Return a list of questions:

    pollster_questions()

Return a specific question by its identifier

    pollster_questions_slug("17-VA-Gov-GE-SvP")

Return a table with one row of response values per poll question +
subpopulation of a given question and columns are responses:

    pollster_questions_responses_clean("17-VA-Gov-GE-SvP")

Return a table with one row of response values per poll question +
subpopulation + response of a given question

    pollster_questions_responses_raw("17-VA-Gov-GE-SvP")

Return a list of charts

    pollster_charts()

Return a chart

    pollster_charts_slug("2016-general-election-trump-vs-clinton")

Return a table with one row per poll for the chart

    pollster_charts_polls("2016-general-election-trump-vs-clinton")

Return a table with the trendline for a chart

    pollster_charts_trendlines("2016-general-election-trump-vs-clinton")

Return a list of tags used in charts, polls, and questions

    pollster_tags()

### Pagination

Several of the Pollster API methods are paginated, with limits the the
number or results returned with each request. The paginated methods are
ones with a `cursor` argument. The function `pollster_iter` iterates
over multiple pages of API results,

    pollster_iter(pollster_charts, .max_pages = 2)

There are wrappers for the paginated API methods:

    pollster_charts_iter(.max_pages = 2)

    pollster_polls_iter(.max_pages = 2)

    pollster_questions_iter(.max_pages = 2)

Bugs
----

If you encounter an error when using one of the functions it is likely
that there was an error in converting the data as returned by the API
into data structures more usable in R. This may happen when the Huffpost
Pollster API changes, and **pollstR** has not been updated yet.

1.  Install the latest version of **pollstR** from github and see if the
    bug has been fixed.
2.  Open a new issue on
    [github](https://github.com/rOpenGov/pollstR/issues)

License
-------

The package is released under GPL-2 and the API data it accesses is
released under the [Creative Commons
Attribution-NonCommercial-ShareAlike 3.0 Unported
License](http://creativecommons.org/licenses/by-nc-sa/3.0/deed.en_US).
