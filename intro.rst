Introduction
================

National statistics agencies are mandated to collect
microdata [#foot13]_ from surveys and censuses to inform and
measure policy effectiveness. In almost all countries, statistics acts
and privacy laws govern these activities. These laws require that
agencies protect the identity of respondents, but may also require that
agencies disseminate the results and, in appropriate cases, the
microdata. Data producers who are not part of national statistics
agencies are also often subject to restrictions, through privacy laws or
strict codes of conduct and ethics that require a similar commitment to
privacy protection. This has to be balanced against the increasing
requirement from funders that data produced using donor funds be made
publically available.

This tension between complying with confidentiality requirements while
at the same time requiring that microdata be released means that a
demand exists for practical solutions for applying Statistical
Disclosure Control (SDC), also known as microdata anonymization. The
provision of adequate solutions and technical support has the potential
to “unlock” a large number of datasets.

The `International Household Survey Network <http://ihsn.org>`__ (IHSN)
and the World Bank have contributed to successful programs that have
generated tools, resources and guidelines for the curation, preservation
and dissemination of microdata and resulted in the documentation of
thousands of surveys by countries and agencies across the world. While
these programs have ensured substantial improvements in the preservation
of data and dissemination of good quality metadata, many agencies are
still reluctant to allow access to the microdata. The reasons are
technical, legal, ethical and political, and sometimes involve a fear of
being criticized for not providing perfect data. When combined with the
tools and guidelines already developed by the IHSN/World Bank for the
curation, preservation and dissemination of microdata, tools and
guidelines for the anonymization of microdata should further reduce or
remove some of these obstacles.

Working with the IHSN, PARIS21 (OECD), Statistics Austria and the Vienna
University of Technology, the World Bank has contributed to the
development of an open source software package for SDC, called
*sdcMicro*. The package was developed for use with the open source *R*
statistical software, available from the Comprehensive R Archive Network
(CRAN) at http://cran.us.r-project.org. The package includes numerous
methods for the assessment and reduction of disclosure risk in
microdata.

Ensuring that a free open source solution is available to agencies was
an important step forward, but not a sufficient one. There is still
limited consolidated and reported knowledge on the impact of disclosure
risk reduction methods on data utility. This limited access to knowledge
combined with a lack of experience in using the tools and methods makes
it difficult for many agencies to implement optimal solutions, i.e.,
solutions that meet their obligations towards both privacy protection
and the release of data useful for policy monitoring and evaluation.
This practice guide attempts to fill this critical gap by:

(i)  consolidating knowledge gained at the World Bank through
     experiments conducted during a large-scale evaluation of
     anonymization techniques

(ii) translating the experience and key results into practical
     guidelines

It should be stressed that SDC is only one part of the data release
process, and its application must be considered within the complete data
release framework. The level and methods of SDC depend on the laws of
the country, the sensitivity of the data and the access policy (i.e.,
who will gain access) considered for release. Agencies that are
currently releasing data are already using many of the methods described
in this guide and applying appropriate access polices to their data
before release. The primary objective of this guide is to provide a
primer to those new to the process who are looking for guidance on both
theory and practical implementation. This guide is not intended to
prescribe or advocate for changes in methods that specific data
producers are already using and which they have designed to fit and
comply with their existing data release policies.

The guide seeks to provide practical steps to those agencies that want
to unlock access to their data in a safe way and ensure that the data
remain fit for purpose.

Building a knowledge base
----------------------------

The release of data is important, as it allows researchers and
policymakers to replicate officially published results, generate new
insights into issues, avoid duplication of surveys and provide greater
returns to the investment in the survey process.

Both the production of reports, with aggregate tables of indicators and
statistics, and the release of microdata result in privacy challenges to
the producer. In the past, for many agencies, the only requirement was
to release a report and some key indicators. The recent movement around
Open Data, Open Government and transparency means that agencies are
under greater pressure to release their microdata to allow broader use
of data collected through public and donor funds. This guide focuses on
the methods and processes for the release of microdata.

Releasing data in a safe way is required to protect the integrity of the
statistical system, by ensuring agencies honor their commitment to
respondents to protect their identity. Agencies do not widely share, in
substantial detail, their knowledge and experience using SDC and the
processes for creating safe data with other agencies. This makes it
difficult for agencies new to the process to implement solutions. To
fill this experience and knowledge gap, we evaluated the use of a broad
suite of SDC methods on a range of survey microdata covering important
development topics related to health, labor, education, poverty and
inequality. The data we used were all previously treated to make them
safe for release. Given that their producers had already treated these
data, it was not possible, nor was it our goal, to pass any judgment on
the safety of these data, many of which are in the public domain The
focus was rather on measuring the effects that various methods would
have on the risk-utility trade-off for microdata produced to measure
common development indicators. We used the experience from this
large-scale experimentation to inform our discussion of the processes
and methods in this guide.

.. admonition:: Important

	At no point was any attempt made to re-identify, through
	matching or any other method, any respondents in the surveys we used in
	building our knowledge base. All risk assessments were based on
	frequencies and probabilities.

Using this guide
----------------

The methods discussed in this guide originate from a large body of
literature on SDC. The processes underlying many of the methods are the
subject of extensive academic research and many, if not all, of them are
used extensively by agencies experienced in preparing microdata for
release.

Where possible, for each method and topic, we provide elaborate
examples, references to the original or seminal work describing the
methods and algorithms in detail and recommended readings. This, when
combined with the discussion of the method and practical considerations
in this guide, should allow the reader to understand the methods and
their strengths and weaknesses. It should also provide enough detail for
readers to use an existing software solution to implement the methods or
program the methods in statistical software of their choice.

For the examples in this guide, we use the open source and free package
for SDC called *sdcMicro* as well as the statistical software *R*.
*sdcMicro* is an add-on package to the statistical software *R*. The
package was developed and is maintained by Matthias Templ, Alexander
Kowarik and Bernhard Meindl. [#foot14]_ The statistical software *R* and the *sdcMicro*
package, as well as any other packages needed for the SDC process, are
freely available from the Comprehensive R Archive Network (CRAN) mirrors
(http://cran.r-project.org/). The software is available for Linux,
Windows and Macintosh operating systems. We chose to use *R* and
*sdcMicro* because it is freely available, accommodates all main data
formats and is easy to adapt by the user. The World Bank, through the
IHSN, has also provided funding towards the development of the
*sdcMicro* package to ensure it meets the requirements of the agencies
we support.

This guide does not provide a review of all other available packages for
implementing the SDC process. Our concern is more with providing
practical insight into the application of the methods. We would,
however, like to highlight one particular other software package that is
commonly used by agencies: μ-ARGUS [#foot15]_. μ-ARGUS is
developed by Statistics Netherlands. *sdcMicro* and μ-ARGUS are both
widely used in statistics offices in the European Union and implement
many of the same methods.

The user needs some knowledge of *R* to use *sdcMicro*. It is beyond the
scope of this guide to teach the use of *R*, but we do provide
throughout the guide code examples on how to implement the necessary
routines in *R*. [#foot16]_ We also present a number of case
studies that include the code for the anonymization of a number of demo
datasets using *R*. Through these case studies, we demonstrate a number
of approaches to the anonymization process in *R*. [#foot17]_ 

Outline of this guide
------------------------

This guide is divided into the following main sections:

(i)   the Section `Statistical Disclosure Control (SDC): An Introduction <SDC_intro.html>`__ is a primer on SDC.

(ii)  the Section `Release Types <release_types.html>`__ gives an introduction to different release types for
      microdata.

(iii) the Sections `Anonymization Methods <anon_methods.html>`__ , `Measuring Risk <measure_risk.html>`__ and `Measuring Utility and Information Loss <utility.html>`__ cover SDC methods, risk and utility measurement.
      The goal here is to provide knowledge that allows the reader to
      independently apply and execute the SDC process. This section is
      enriched with real examples as well as code snippets from the
      *sdcMicro* package. The interested reader can also find more
      information in the references and recommended readings at the end
      of each section.

(iv)  the Section `SDC with sdcMicro in R: Setting Up Your Data and more <sdcMicro.html>`__ gives an overview of issues encountered when carrying
      out anonymization with the *sdcMicro* package in *R*, which exceed
      basic *R* knowledge. This section also includes tips and solutions
      to some of the common issues and problems that might be
      encountered when applying SDC methods in *R* with *sdcMicro.*

(v)   the Section `The SDC Process <process.html>`__ provides a step-by-step guide to disclosure control,
      which draws upon the knowledge presented in the previous sections.

(vi)  the Section `Case Studies (Illustrating the SDC Process) <case_studies.html>`__ presents a number of detailed case studies that
      demonstrate the use of the methods, their implementation in
      *sdcMicro* and the process that should be followed to reach the
      optimal risk-utility solution.


.. [#foot13]
   Microdata are unit-level data obtained from sample surveys, censuses
   and administrative systems. They provide information about
   characteristics of individual people or entities such as households,
   business enterprises, facilities, farms or even geographical areas
   such as villages or towns. They allow in-depth understanding of
   socio-economic issues by studying relationships and interactions
   among phenomena. Microdata are thus key to designing projects and
   formulating policies, targeting interventions and monitoring and
   measuring the impact and results of projects, interventions and
   policies.

.. [#foot14]
   See http://cran.r-project.org/web/packages/sdcMicro/index.html and the GitHub
   https://github.com/sdcTools/sdcMicro of the developers. The
   GitHub repository can also be used to submit bugs found in the package.

.. [#foot15]
   μ-ARGUS is available at: http://neon.vb.cbs.nl/casc/mu.htm. The
   software was recently ported to open source.

.. [#foot16]
   There are many free resources for learning *R* available on the web.
   One place to start would be the CRAN *R* Project page:
   http://cran.r-project.org/other-docs.html

.. [#foot17]
   The developers of *sdcMicro* have also developed a graphical user
   interface (GUI) for the package, which is contained in the *sdcMicro* package available from the CRAN mirrors. The GUI,
   however, does not implement the full functionality of the *sdcMicro*
   package and is not discussed in this guide. The GUI can be called after loading sdcMicro by typing sdcApp() at the prompt.
 
