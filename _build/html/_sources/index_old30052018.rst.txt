Statistical Disclosure Control for Microdata: A Practice Guide
===========================================================================

**Thijs Benschop**

**Cathrine Machingauta**

**Matthew Welch**

Affiliations: Thijs Benschop, Consultant The World Bank, Cathrine
Machingauta, The World Bank, Matthew Welch, The World Bank

Correspondence: Matthew Welch, mwelch@worldbank.org

Acknowledgments: The authors thank Olivier Dupriez (The World Bank) for
his technical comments and inputs throughout the process.

The production of this guide was made possible through a World Bank
Knowledge for Change II Grant: KCP II - A microdata dissemination
challenge: Balancing data protection and data utility. Grant number: TF
015043, Project Number P094376. As well as from United Kingdom - DFID
funding to the World Bank Multi-Donor Trust Fund - International
Household Survey and Accelerated Data Program – TF071804/TF011722.

.. toctree::
   :maxdepth: 2
   :caption: Practice guide
   
   intro
   glossary_acr
   SDC_intro
   measure_risk
   anon_methods
   utility
   sdcMicro
   process
   appendices
   bibliography
   lists
     
.. toctree::
   :maxdepth: 2
   :caption: Case studies
   
   case_studies
   
   
.. [#foot1]
   http://www.nss.gov.au/nss/home.nsf/pages/Confidentiality+-+Glossary

.. [#foot2]
   http://stats.oecd.org/glossary

.. [#foot3]
   Australian Bureau of Statistics,
   http://www.nss.gov.au/nss/home.nsf/pages/Confidentiality+-+Glossary

.. [#foot4]
   Australian Bureau of Statistics,
   http://www.nss.gov.au/nss/home.nsf/pages/Confidentiality+-+Glossary

.. [#foot5]
   http://stats.oecd.org/glossary

.. [#foot6]
   OECD, http://stats.oecd.org/glossary

.. [#foot7]
   http://www.nss.gov.au/nss/home.nsf/pages/Confidentiality+-+Glossary

.. [#foot8]
   http://stats.oecd.org/glossary

.. [#foot9]
   Australian Bureau of Statistics,
   http://www.nss.gov.au/nss/home.nsf/pages/Confidentiality+-+Glossary

.. [#foot10]
   Australian Bureau of Statistics,
   http://www.nss.gov.au/nss/home.nsf/pages/Confidentiality+-+Glossary

.. [#foot11]
   http://stats.oecd.org/glossary

.. [#foot12]
   OECD, http://stats.oecd.org/glossary

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
   http://cran.r-project.org/web/packages/sdcMicro/index.html\ \ \ https://github.com/alexkowa/sdcMicro

.. [#foot15]
   μ-ARGUS is available at: http://neon.vb.cbs.nl/casc/mu.htm. The
   software was recently ported to open source.

.. [#foot16]
   There are many free resources for learning *R* available on the web.
   One place to start would be the CRAN *R* Project page:
   http://cran.r-project.org/other-docs.html

.. [#foot17]
   The developers of *sdcMicro* have also developed a graphical user
   interface (GUI) for the package, which is contained in the *R*
   package *sdcMicroGUI* and available from the CRAN mirrors. The GUI,
   however, does not implement the full functionality of the *sdcMicro*
   package and is not discussed in this guide.

.. [#foot18]
   There is another strand of literature on the anonymization of tabular
   data, see e.g., Hundepool et al. (2012).

.. [#foot19]
   See Section 5 in Dupriez and Boyko (2010) as to who the users of
   microdata are and to whom microdata should be made available.

.. [#foot20]
   Appendix B provides an example of a blanket agreement.

.. [#foot21]
   Recoding a continuous variable is sometimes useful in cases where the
   data contains only a few continuous variables. We will see in Section
   3 that many methods used for risk calculation depend on whether the
   variables are categorical. We will also see that it is easier for the
   measurement of risk if the data contains only categorical or only 
   continuous variables.
   
.. [#foot22]
   This is discussed in greater detail in the following sections. In
   cases where the number of possible values is large, recoding the
   variable, or parts of the set it takes values on, to obtain fewer
   distinct values is recommended.

.. [#foot23]
   Besides variables collected at the higher hierarchical level, also
   variables collected at the lower level but with no (or little)
   variation within the groups formed by the hierarchical structure
   should be treated as higher level variables. An example could be
   mother tongue, where most households are monolingual, but the
   variable is collected at the individual level.

.. [#foot24]
   Religion, for example, can be shared by all household members in
   some countries, whereas in other countries this variable is measured
   at the individual level and mixed-religion households exist.

.. [#foot25]
   The code examples in this guide are based on *sdcMicro* objects. An
   *sdcMicro* object contains, amongst others, the data and identifies
   all the specified key variables. The code below creates a data.frame
   with the data from Table 4.1 and the *sdcMicro* objects “sdcInitial”
   used in most examples in this section.

   .. code-block R
   
       library(sdcMicro)
       
       # Set up dataset
       
       data <- as.data.frame(cbind(as.factor(c('Urban',
       'Urban', 'Urban', 'Urban', 'Rural', 'Urban', 'Urban', 'Urban',
       'Urban', 'Urban')),
       as.factor**\ \ (**c**\ \ ('Female', 'Female', 'Female', 'Male',
       'Female', 'Male', 'Female', 'Male', 'Female', 'Female')),
       as.factor(c('Sec in', 'Sec in', 'Prim in', 'Sec com', 'Sec com', 'Sec com', 'Prim com', 'Post-sec', 'Sec in', 'Sec in')), 
       as.factor(c('Emp', 'Emp', 'Non-LF', 'Emp', 'Unemp', 'Emp', 'Non-LF', 'Unemp', 'Non-LF','Non-LF')),
       as.factor(c('yes', 'yes', 'yes', 'yes', 'yes', 'no', 'no', 'yes', 'no', 'yes')),
       c(180, 180, 215, 76, 186, 76, 180, 215, 186, 76)))
       
       # Specify variable names*
       
       names(data) <- c('Residence', 'Gender', 'Educ', 'Lstat', 'Health', 'Weights')
       
       # Set up sdcMicro object with specified quasi-identifiers and weight variable
       
       sdcInitial <- createSdcObj(dat = data, 
       keyVars = c('Residence', 'Gender', 'Educ', 'Lstat'), weightVar = 'Weights')

.. [#foot26]
   The assumptions for this risk measure are strict and the risk is
   estimated in many cases higher than the actual risk. Among other
   assumptions, it is assumed that all individuals in the sample are
   also included in the external file used by the intruder to match
   against. If this is not the case, the risk is much lower; if the
   individual in the released file is not contained in the external
   file, the probability of a correct match is zero. Other assumptions
   are that the files contain no errors and that both sets of data were
   collected simultaneously, i.e. they contain the same information.
   These assumptions will often not hold generally, but are necessary
   for computation of a measure. An example of a violation of the last
   assumptions is could occur if datasets are collected at different
   points in time and records have changed. This could happen when
   people move or change jobs and makes correct matching impossible. The
   assumptions assume a worst-case scenario.

.. [#foot27]
   See Section 7.5 for more information on slots and the *sdcMicro*
   object structure.

.. [#foot28]
   In *sdcMicro* it is important to use the standard missing value code
   NA instead of other codes, such as 9999 or strings. In Chapter 6, we
   further discuss how to set other missing value codes to NA in *R*.
   This is necessary to ensure that the methods in *sdcMicro* function
   properly. When missing values have codes other than NA, the missing
   value codes are interpreted as a distinct factor level in the case of
   categorical variables.

.. [#foot29]
   Alternatively, the sensitive variables can be specified when
   creating the *sdcMicro* object using the function createSdcObj() in
   the *sensibleVar* argument. This is further explained in Section 7.5.
   In that case, the argument *ldiv_index* does not have to be specified
   in the ldiversity() function. and the variables in the *sensibleVar*
   argument will automatically be used to compute :math:`l`-diversity.

.. [#foot30]
   Besides distinct :math:`l`-diversity, there are other
   :math:`l`-diversity methods: entropy and recursive. Distinct
   :math:`l`-diversity is most commonly used.

.. [#foot31]
   There are more combinations of quasi-identifiers that make record 5
   unique (e.g., {‘Rural’, ‘Female’} and {‘Female’, ‘Secondary
   Complete’, ‘Unemployed’}. These combinations, however, are not
   considered MSUs because they do not fulfill the **minimal** subset
   requirement. They contain subsets that are MSUs.

.. [#foot32]
   OECD, http://stats.oecd.org/glossary

.. [#foot33]
   The third record has one MSU, {‘Primary incomplete’}; the seventh
   record has one MSU, {‘Primary complete’}; and the eighth record has
   three MSUs, {‘Urban, Unemployed’}, {‘Male, Unemployed’} and
   {‘Post-secondary’}.

.. [#foot34]
   We also show code examples in *R,* which are drawn from findings we
   gathered by applying these methods to a large collection of datasets.

.. [#foot35]
   Here the *sdcMicro* object “sdcIntial“ contains a dataset with 2,500
   individuals and 103 variables. We selected five quasi-identifiers:
   “sizeRes”, “age”, “gender”, “region”, and “ethnicity”.

.. [#foot36]
   This approach works only for semi-continuous variables, because in
   the case of continuous variables, there might be values that are
   between the lower interval boundary and the lower interval boundary
   minus the small number. For example, using this for income, we would
   have an interval (9999, 19999] and the value 9999.5 would be
   misclassified as belonging to the interval [10000, 19999].

.. [#foot37]
   In *R* suppressed values are recoded NA, the standard missing value
   code.

.. [#foot38]
   In *R* suppressed values are recoded NA, the standard missing value
   code.

.. [#foot39]
   Here the *sdcMicro* object “sdcIntial“ contains a dataset with 2,500
   individuals and 103 variables. We selected five quasi-identifiers:
   “sizeRes”, “age”, “gender”, “region”, and “ethnicity”.

.. [#foot40]
   This can be assessed with utility measures.

.. [#foot41]
   I2D2 is a dataset with data related to the labor market.

.. [#foot42]
   The 5,045 is the expectation computed as 5,000 \* 1 + 500 \* 0.05 +
   400 \* 0.05.

.. [#foot43]
   This means that the vector with the tabulation of the absolute
   frequencies of the different categories in the original data is an
   eigenvector of the transition matrix that corresponds to the unit
   eigenvalue.

.. [#foot44]
   In this example and the following examples in this section, the
   *sdcMicro* object “sdcIntial“ contains a dataset with 2,000
   individuals and 39 variables. We selected five categorical
   quasi-identifiers and 9 variables for PRAM: “ROOF”, “TOILET”,
   “WATER”, “ELECTCON”, “FUELCOOK”, “OWNMOTORCYCLE”, “CAR”, “TV”, and
   “LIVESTOCK”. These PRAM variabels were selected according to the
   requirements of this particular dataset and for illustrative
   purposes.

.. [#foot45]
   The PRAM method in *sdcMicro* sometimes produces the following
   error: Error in factor(xpramed, labels = lev) : invalid 'labels';
   length 6 should be 1 or 5. Under some circumstances, changing the
   seed can solve this error.

.. [#foot46]
   This can also be achieved with multidimensional transition matrices.
   In that case, the probability is not specified for ‘male’ ->
   ‘female’, but for ‘male’ + ‘rural’ -> ‘female’ + ‘rural’ and for
   ‘male’ + ‘urban’ -> ‘female’ + ‘urban’. This is not implemented in
   sdcMicro but can be achieved by PRAMming the males and females
   separately. In the example here, this could be done by specifying
   gender as strata variable in the pram() function in *sdcMicro*.

.. [#foot47]
   Microaggregation can also be used for categorical data, as long as
   there is a possibility to form groups and an aggregate replacement
   for the values in the group can be calculated. This is the case for
   ordinal variables.

.. [#foot48]
   Here all groups can have different sizes (i.e., number of
   individuals in a group). In practice, the search for homogeneous
   groups is simplified by imposing equal group sizes for all groups.

.. [#foot49]
   In this example and the following examples in this section, the
   *sdcMicro* object “sdcIntial“ contains a dataset with 2,000
   individuals and 39 variables. We selected five categorical
   quasi-identifiers and three continuous quasi-identifiers: “INC”,
   “EXP” and “WEALTH”.

.. [#foot50]
   Also the homogeneity in the groups will be generally lower, leading
   to larger changes, higher protection, but also more information loss,
   unless the strata variable correlates with the microaggregation
   variable.

.. [#foot51]
   Common values for :math:`\alpha` are between 0.5 and 2. The default
   value in the *sdcMicro* function addNoise() is 150, which is too
   large for most datasets; the level of noise should be set in the
   argument ‘noise’.

.. [#foot52]
   In this example and the following examples in this section, the
   *sdcMicro* object “sdcIntial“ contains a dataset with 2,000
   individuals and 39 variables. We selected five categorical
   quasi-identifiers and 12 continuous quasi-identifiers. These are the
   expenditure components “TFOODEXP”, “TALCHEXP”, “TCLTHEXP”,
   “THOUSEXP”, “TFURNEXP”, “THLTHEXP”, “TTRANSEXP”, “TCOMMEXP”,
   “TRECEXP”, “TEDUEXP”, “TRESTHOTEXP”, “TMISCEXP“.

.. [#foot53]
   The Shapiro-Wilk test is implemented in the function shapiro.test()
   from the package *stats* in *R*. The Jarque-Bera test has several
   implementations in *R*, for example, in the function
   jarque.bera.test() from the package *tseries*.

.. [#foot54]
   In *sdcMicro*, there are several other methods for shuffling
   implemented, including ‘ds’, ‘mvn’ and ‘mlm’. See the Help option for
   the shuffle function in *sdcMicro* for details on methods ‘ds’, ‘mvm’
   and ‘mlm’.

.. [#foot55]
   Even if the dataset does not contain an explicit variable with
   household size, this information can be easily extracted from the
   data and should be taken into account. Section 7.6 shows how to
   create a variable “household size” based on the household IDs.

.. [#foot56]
   More information on census microdata at ONS is available on their
   website:
   http://www.ons.gov.uk/ons/guide-method/census/2011/census-data/census-microdata/index.html

.. [#foot57]
   More information on the anonymization of these files is available on
   the website of the U.S. Census Bureau:
   https://www.census.gov/population/www/cen2000/pums/index.html

.. [#foot58]
   It is possible to release data files for different groups of users,
   e.g., PUF and SUF. All information in the less detailed file,
   however, must also be included in the more detailed file to prevent
   unintended disclosure. Datasets released in data enclaves can be
   customized for the user, since the risk that they will be combined
   with other version is zero.

.. [#foot59]
   Here the *sdcMicro* object “sdcIntial“ contains a dataset with 2,500
   individuals and 103 variables. We selected three categorical
   quasi-identifiers: “URBRUR”, “REGION”, “RELIG” and “MARITAL” and
   several continuous quasi-identifiers relating to income and
   expenditure. To illustrate the utility loss, we also applied several
   SDC methods to this *sdcMicro* object, such as local suppression,
   PRAM and additive noise addition.

.. [#foot60]
   Often it is also useful to search the internet for help on specific
   functions in *R*. There are many fora where *R* users discuss issues
   they encounter. One particularly useful site is stackoverflow.com.

.. [#foot61]
   A dataframe is an object class in *R*, which is similar to a data
   table or matrix.

.. [#foot62]
   Not all functions are compatible with all versions of the respective
   software package. We refer to the help files of the read and write
   functions for more information.

.. [#foot63]
   The function read.dta() in the package *foreign* does not support
   the *STATA* file format from *STATA* 13 and *STATA* 14. Two solutions
   are to use the ‘saveold’ command in *STATA* 13 or 14 that saves the
   file in the old format that can be read by the function read.dta().
   Alternatively, one could use the function read.dta13() from the
   package *readstata13*.

.. [#foot64]
   The function read.dta() in the package *foreign* does not support
   the *STATA* file format from *STATA* 13 and *STATA* 14. Two solutions
   are to use the ‘saveold’ command in *STATA* 13 or 14 that saves the
   file in the old format that can be read by the function read.dta().
   Alternatively, one could use the function read.dta13() from the
   package *readstata13*.

.. [#foot65]
   This is regardless of the class of the variable in *R*. See Section
   7.4 for more on classes in *R*.

.. [#foot66]
   Class *sdcMicroObj* has S4 objects, which have slots or attributes
   and allow for object-oriented programming.

.. [#foot67]
   Unless otherwise specified in the arguments of the function.

.. [#foot68]
   Here a scenario refers to a combination of SDC methods and their
   parameters.

.. [#foot69]
   The server has 512 GB RAM and four processors each with 16 cores,
   translating to 64 cores total.

.. [#foot70]
   The following website provides an overview of parallelization
   packages and solutions in *R*:
   http://cran.r-project.org/web/views/HighPerformanceComputing.html.
   **NOTE: Solutions are platform-dependent and therefore our solution
   is not further presented.**

.. [#foot71]
   Other methods and guidance on treating datasets where household size
   is a quasi-identifier are discussed in Section 5.5.

.. [#foot72]
   For illustrative purposes, we only show this evaluation for the
   expenditure variables. It can be easily copied for the income
   variables. The results are similar.

.. [#foot73]
   To compute the GINI coefficient, bootstrap to construct the
   confidence intervals and plot the Lorenz curve we used the *R*
   packages *laeken, reldist, bootstrap* and *ineq*.

.. |Macintosh HD:Users:thijsbenschop:Copy:World Bank:Guidelines:Case studies:Rplot11.pdf| image:: media/image1.png
   :width: 6.03524in
   :height: 4.3072in
.. |Macintosh HD:Users:thijsbenschop:figure51.png| image:: media/image3.png
   :width: 6.5in
   :height: 3.25556in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure52.png| image:: media/image4.png
   :width: 6.5in
   :height: 3.25556in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure53.png| image:: media/image5.png
   :width: 6.5in
   :height: 3.25556in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure54.png| image:: media/image6.png
   :width: 6.5in
   :height: 3.25556in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure55.png| image:: media/image7.png
   :width: 6.5in
   :height: 3.25556in
.. |figure56| image:: media/image8.png
   :width: 6.48958in
   :height: 3.23958in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure61.png| image:: media/image11.png
   :width: 6.5in
   :height: 3.25556in
.. |figure63| image:: media/image13.png
   :width: 6.48958in
   :height: 3.23958in
.. |figure64| image:: media/image14.png
   :width: 6.48958in
   :height: 3.23958in
.. |figure67| image:: media/image16.png
   :width: 6.48958in
   :height: 3.23958in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure62.png| image:: media/image17.png
   :width: 6.5in
   :height: 3.25556in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure68.png| image:: media/image18.png
   :width: 6.5in
   :height: 3.25in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure69.png| image:: media/image19.png
   :width: 6.5in
   :height: 3.25in
.. |image19| image:: media/image20.png
   :width: 6.55208in
   :height: 8.60417in
.. |Macintosh HD:Users:thijsbenschop:Onedrive:World Bank:Guidelines:Plots:figure91.png| image:: media/image21.png
   :width: 6.5in
   :height: 3.25in
.. |image22| image:: media/image23.png
   :width: 6.5in
   :height: 6.53056in