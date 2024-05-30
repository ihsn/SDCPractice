Release Types
=============

This section discusses data release. Rather than rewriting work that has
already been conducted through the World Bank and its partners at the
IHSN, this section extracts from an excellent guide published by `DuBo10`_.

The trade-off between risk and utility in the anonymization process
depends greatly on who the users are [#foot19]_ and under
what conditions a microdata file is released. Generally, three types of
data release methods are practiced and apply to different target groups.

-  **Public Use File (PUF)**: the data “are available to anyone agreeing
   to respect a core set of easy-to-meet conditions. Such conditions
   relate to what cannot be done with the data (e.g. the data cannot be
   sold), upon gaining access to the data. In some cases PUFs are
   disseminated with no conditions; often being made available on-line,
   [e.g. on the website of the statistical agency]. These data are made
   easily accessible because the risk of identifying individual
   respondents is considered minimal. Minimising the risk of disclosure
   involves eliminating all content that can identify respondents
   directly—for instance, names, addresses and telephone numbers. In
   addition this requires purging relevant indirect identifiers from the
   microdata file. These vary across survey designs, but
   commonly-suppressed indirect identifiers include geographical
   information below the sub-national level at which the sample is
   representative. Occasionally, certain records may be suppressed also
   from PUFs, as might variables characterised by extremely skewed
   distribution or outliers. However, in lieu of deleting entire records
   or variables from microdata files, alternative SDC methods can
   minimise the risk of disclosure while maximizing information content.
   Such methods include top-and-bottom coding, local suppression or
   using data perturbation techniques [(see the Section
   `Anonymization methods <anon_methods.html>`__ for an overview of
   anonymization methods)]. PUFs are typically generated from census
   data files using a sub-set [or sample] of records rather than the
   entire file and [from sample surveys, such as] household surveys.”
   (`DuBo10`_).

-  **Scientific Use File (SUF)** (also known as a licensed file,
   microdata under contract or research file): the “dissemination is
   restricted to users who have received authorization to access them
   after submitting a documented application and signing an agreement
   governing the data’s use. While typically licensed files are also
   anonymised to ensure the risk of identifying individuals is minimised
   when used in isolation, they may still [potentially] contain
   identifiable data if linked with other data files. Direct identifiers
   such as respondents’ names must be removed from a licensed dataset.
   The data files may, however, still contain indirect variables that
   could identify respondents by matching them to other data files such
   as voter lists, land registers or school records. When disseminating
   licensed files, the recommendation is to establish and sign an
   agreement between the data producer and external bona fide users –
   trustworthy users with legitimate need to access the data. Such an
   agreement should govern access and use of such microdata
   files [#foot20]_. Sometimes, licensing agreements are only
   entered into with users affiliated to an appropriate sponsoring
   institution. i.e., research centers, universities or development
   partners. It is further recommended that, before entering into a data
   access and use agreement, the data producer asks potential users to
   complete an application form to demonstrate the need to use a
   licensed file (instead of the PUF version, if available) for a stated
   statistical or research purpose” (`DuBo10`_). This also
   allows the data producer to learn which characteristics of the data
   are important for the users, which is valuable information for
   optimizing future anonymization processes.

-  **Microdata available in a controlled research data center** (also
   known as data enclave): “Some files may be offered to users under
   strict conditions in a data enclave. This is a facility [(often on
   the premises of the data provider)] equipped with computers not
   linked to the internet or an external network and from which no
   information can be downloaded via USB ports, CD-DVD or other drives.
   Data enclaves contain data that are particularly sensitive or allow
   direct or easy identification of respondents. Examples include
   complete population census datasets, enterprise surveys and certain
   health related datasets containing highly-confidential information.
   Users interested in accessing a data enclave will not necessarily
   have access to the full dataset – only to the particular data subset
   they require. They will be asked to complete an application form
   demonstrating a legitimate need to access these data to fulfill a
   stated statistical or research purpose […] The outputs generated must
   be scrutinised by way of a full disclosure review before release.
   Operating a data enclave may be expensive – it requires special
   premises and computer equipment. It also demands staff with the
   skills and time to review outputs before their removal from the data
   enclave in order to ensure there is no risk of disclosure. Such staff
   must be familiar with data analysis and be able to review the request
   process and manage file servers. Because of the substantial operating
   costs and technical skills required, some statistical agencies or
   other official data producers opt to collaborate with academic
   institutions or research centres to establish and manage data
   enclaves.”

There are other data access possibilities besides these, such as
teaching files, files for other specific purposes, remote execution or
remote access. Obviously, the required level of protection depends on
the type of release; a PUF file must be protected to a much larger
extent than a SUF file, which in turn has to be protected more than a
file which is only available in an on-site facility. 
The Section `Step 3: Type of release <process.html#Step 3: Type of release>`__ gives
more guidance on the choice of the release type and its implications for
the anonymization process. The same microdata set can be released in
different ways for different users, e.g., as SUF and teaching file.
The Section `Step 3: Type of release <process.html#Step 3: Type of release>`__ discusses the particular issues of multiple releases of one
dataset.

The first step for any agency that wants to release data would be
formulation of clear data dissemination policies for the release of
microdata. We will see later that deciding on the level of anonymization
needed will depend partly on knowing under what conditions the data will
be released. Access policies and conditions provide the framework for
the whole release process.

The following sections further specify the conditions under which
microdata should be provided under different release types.

Conditions for PUFs
-------------------

“Generally, data regarded as public are open to anyone with access to an
[National Statistical Office] (NSO) website. It is, however, normally
good practice to include statements defining suitable uses for and
precautions to be adopted in using the data. While these may not be
legally binding, they serve to sensitise the user. Prohibitions such as
attempts to link the data to other sources can be part of the ‘use
statement’ to which the user must agree, on-line, before the data can be
downloaded. […] Dissemination of microdata files necessarily involves
the application of rules or principles. [The info-box] below [taken from
`DuBo10`_] shows basic principles normally applying to
PUFs.” (`DuBo10`_).

.. admonition:: Info-box - Conditions for accessing and using PUFs

	1. Data and other material provided by the NSO will not be redistributed or sold to other individuals, institutions or organisations without the NSO’s written agreement.
	2. Data will be used for statistical and scientific research purposes only. They will be employed solely for reporting aggregated information, including modelling, and not for investigating specific individuals or organisations.
	3. No attempt will be made to re-identify respondents, and there will be no use of the identity of any person or establishment discovered inadvertently. Any such discovery will be reported immediately to the NSO.
	4. No attempt will be made to produce links between datasets provided by the NSO or between NSO data and other datasets that could identify individuals or organisations.
	5. Any books, articles, conference papers, theses, dissertations, reports or other publications employing data obtained from the NSO will cite the source, in line with the citation requirement provided with the dataset.
	6. An electronic copy of all publications based on the requested data will be sent to the NSO.
	7. The original collector of the data, the NSO, and the relevant funding agencies bear no responsibility for the data’s use or interpretation or inferences based upon it.

	Note: Items 3 and 6 in the list require that users be provided with an easy way to communicate with the data provider. It is good practice to provide a contact number, an email address, and possibly an on-line “feedback provision” system.

	Source: `DuBo10`_

Conditions for SUFs
-------------------

“For [SUFs], terms and conditions must include the basic common
principles plus some additional ones applying to the researcher’s
organisation. There are two options: firstly, data are provided to a
researcher or a team for a specific purpose; secondly, data are provided
to an organization under a blanket agreement for internal use, e.g., to
an international body or research agency. In both cases, the
researcher’s organisation must be identified, as must suitable
representatives to sign the licence” (`DuBo10`_).

*Access to a researcher or research team for a specific purpose*

“If data are provided for an individual research project, the research
team must be identified. This is covered by requiring interested users
to complete a formal request to access the data (a model of such a
request form is provided in Appendix 1 [in `DuBo10`_]).
The conditions to obtain the data (see example in the info-box below) will specify
that the files will not be shared outside the organisation and that data
will be stored securely. To the possible extent, the intended use of the
data – including a list of expected outputs and the organisation’s
dissemination policy – must be identified. Access to licensed datasets
is only granted when there is a legally-registered sponsoring agency,
e.g., government ministry, university, research centre or national or
international organization” (`DuBo10`_).

.. admonition:: Info-box - Conditions for accessing and using SUFs

	Note: Items 1 to 8 below are similar to the conditions for use of public use files in the info-box above. Items 9 and 10 would have to be adapted in the case of a blanket agreement.
	
	1. Data and other material provided by the NSO will not be redistributed or sold to other individuals, institutions or organisations without the NSO’s written agreement.
	2. Data will be used for statistical and scientific research purposes only. They will be employed solely for reporting aggregated information, including modelling, and not for investigating specific individuals or organisations.
	3. No attempt will be made to re-identify respondents, and there will be no use of the identity of any person or establishment discovered inadvertently. Any such discovery will be reported immediately to the NSO.
	4. No attempt will be made to produce links between datasets provided by the NSO or between NSO data and other datasets that could identify individuals or organisations.
	5. Any books, articles, conference papers, theses, dissertations, reports or other publications employing data obtained from the NSO will cite the source, in line with the citation requirement provided with the dataset.
	6. An electronic copy of all publications based on therequested data will be sent to the NSO.
	7. The NSO and the relevant funding agencies bear no responsibility the data’s use or for interpretation or inferences based upon it.
	8. An electronic copy of all publications based on the requested data will be sent to the NSO.
	9. The researcher’s organisation must be identified, as must the principal and other researchers involved in using the data must be identified. The principal researcher must sign the licence on behalf of the organization. If the principal researcher is not authorized to sign on behalf of the receiving organization, a suitable representative must be identified.
	10. The intended use of the data, including a list of expected outputs and the organisation’s dissemination policy must be identified.
	
	(Conditions 9 to 11 may be waved in the case of educational institutions)
	
	Source: `DuBo10`_

*Blanket agreement to an organization*

“In the case of a blanket agreement, where it is agreed the data can be
used widely but securely within the receiving organisation, the licence
should ensure compliance, with a named individual formally assuming
responsibility for this. Each additional user must be made aware of the
terms and conditions that apply to data files: this can be achieved by
having to sign an affidavit. Where such an agreement exists, with
security in place, it is not necessary for users to destroy the data
after use” (`DuBo10`_). 
`Appendix B <appendices.html#Appendix B: Example of Blanket Agreement for SUF>`__
provides an example of the formulation of such an agreement.

Conditions for microdata available in a controlled research data center
-----------------------------------------------------------------------

Access to microdata in research data centers is “used for particularly
sensitive data or for more detailed data for which sufficient
anonymisation to release them outside the NSO premises is not possible.
These can be referred to also as data laboratories or research data
centres. A [research data centre] may be located at the NSO headquarters
or in major centres such as universities close to the research
community. They are used to give researchers access to complete data
files but without the risk of releasing confidential data. In a typical
[research data centre], NSO staff supervise access and use of the data;
the computers must not be able to communicate outside the [research data
centre]; and the results obtained by the researchers must be screened
for confidentiality by an NSO analyst before taken outside. A model of a
data enclave access policy is provided in Appendix 2 [in `DuBo10`_], 
and a model of a data enclave access request form is in
Appendix 3 [in `DuBo10`_]” (`DuBo10`_).

Research data centers “have the advantage of providing access to
detailed microdata but the disadvantage of requiring researchers to work
at a different location. And they are expensive to set up and operate.
It is, however, quite likely that many countries have used on-site
researchers as a way of providing access to microdata. These researchers
are sworn in under the statistics’ acts in the same way as regular NSO
employees. This approach tends to favour researchers who live near NSO
headquarters.” (`DuBo10`_)

.. admonition:: Recommended Reading Material on Release Types

	Dupriez, O., & Boyko, E. (2010). *Dissemination of Microdata Files;
	Principles, Procedures and Practices.* International Household Survey
	Network (IHSN).
	
.. [#foot19]
   See Section 5 in `DuBo10`_ as to who the users of
   microdata are and to whom microdata should be made available.

.. [#foot20]
   `Appendix B <appendices.html#Appendix B: Example of Blanket Agreement for SUF>`__ 
   provides an example of a blanket agreement.

.. rubric:: References

.. [DuBo10] Dupriez, O., & Boyko, E. (2010). 
	**Dissemination of Microdata Files; Principles, Procedures and Practices.**
	International Household Survey Network (IHSN).