SDC with *sdcMicro* in *R*: Setting Up Your Data and more
=========================================================

Installing *R*, *sdcMicro* and other packages
---------------------------------------------

This guide is based on the software package *sdcMicro*, which is an
add-on package for the statistical software *R*. Both *R* and
*sdcMicro*, as well as other *R* packages, are freely available from the
CRAN (Comprehensive R Archive Network) website for Linux, Mac and
Windows (http://cran.r-project.org). This website also offers
descriptions of packages. Besides the standard version of *R*, there is
a more user-friendly user interface for *R*: *RStudio*. *RStudio* is
also freely available for Linux, Mac and Windows
(http://www.rstudio.com). The *sdcMicro* package is dependent on (i.e.,
uses) other *R* packages that must be installed on your computer before
using *sdcMicro*. Those will automatically be installed when installing
*sdcMicro*. For some functionalities, we use still other packages (such
as *foreign* for reading data and some graphical packages). If so, this
is indicated in the appropriate section in this guide. *R*, *RStudio*,
the *sdcMicro* package and its dependencies and other packages have
regular updates. It is strongly recommended to regularly check for
updates: this requires installing a new version for an update of *R;*
with the update.packages() command or using the menu options in *R* or
*RStudio* one can update the installed packages.

When starting *R* or *RStudio*, it is necessary to specify each time
which packages are being used by loading those. This loading of packages
can be done either with the library() or the require() function. Both
options are illustrated in :numref:`code71`.

.. code-block:: R
   :linenos:
   :caption: Loading required packages
   :name: code71

   library(sdcMicro) # loading the sdcMicro package
   require(sdcMicro) # loading the sdcMicro package

All packages and functions are documented. The easiest way to access the
documentation of a specific function is to use the built-in help, which
generally gives an overview of the parameters of the functions as well
as some examples. The help of a specific function can be called by a
question mark followed by the function name without any arguments.
:numref:`code72` shows how to call the help file for the microaggregation()
function of the *sdcMicro* package. [#foot60]_ The download
page of the each package on the CRAN website also provides a reference
manual with a complete overview of the functions in the package.

.. code-block:: R
   :linenos:
   :caption: Displaying help for functions
   :name: code72
 
   ?microaggregation # help for microaggregation function

When issues or bugs in the *sdcMicro* package are encountered, comments,
remarks or suggestions can be posted for the developers of *sdcMicro* on
their `GitHub <https://github.com/sdcTools/sdcMicro/issues>`__.

Read functions in *R*
---------------------

The first step in the SDC process when using *sdcMicro* is to read the
data into *R* and create a dataframe. [#foot61]_ *R* is
compatible with most statistical data formats and provides read
functions for most types of data. For those read functions, it is
sometimes necessary to install additional packages and their
dependencies in *R*. An overview of data formats, functions and the
packages containing these functions is provided in :numref:`tab71`. These
functions are also available as write (e.g., write_dta()) to save the
anonymized data in the required format. [#foot62]_

.. _tab71:

.. table:: Packages and functions for reading data in *R*
   :widths: auto
   :align: center

   ===========================  ===============  ======================  =============
    Type/software               Extension          Package                Function    
   ===========================  ===============  ======================  =============
    SPSS                         .sav             haven                   read_sav() 
    STATA (v. 5-14)              .dta             haven                   read_dta()  
    SAS                          .sas7bdat        haven                   read_sas()
    Excel                        .csv             utils (base package)    read.csv()  
    Excel                        .xls/.xlsx       readxl                  readxl()  
   ===========================  ===============  ======================  =============

Most of these functions have options that specify how to handle missing
values and variables with factor levels and value labels. :numref:`code73`,
:numref:`code74` and :numref:`code75` provide example code for reading in a
*STATA* (.dta) file, an *Excel* (.csv) file and a *SPSS* (.sav) file.

.. code-block:: R
   :linenos:
   :caption: Reading in a *STATA* file
   :name: code73
   
   setwd("/Users/World Bank") # working directory with data file 
   fname = "data.dta" # name of data file 
   library(haven) # loads required package for read/write function for STATA files 
   file <- read_dta(fname) 
   # reads the data into the data frame tbl called file 

.. code-block:: R
   :linenos:
   :caption: Reading in a *Excel* file
   :name: code74

   setwd("/Users/World Bank") # working directory with data file 
   fname = "data.csv" # name of data file 
   file <- read.csv(fname, header = TRUE, sep = ",", dec = ".")
   # reads the data into the data frame called file, 
   # the first line contains the variable names, 
   # fields are separated with commas, decimal points are indicated with ‘.’

.. code-block:: R
   :linenos:
   :caption: Reading in a *SPSS* file
   :name: code75
   
   setwd("/Users/World Bank") # working directory with data file 
   fname = "data.sav" # name of data file 
   library(haven) # loads required package for read/write function for SPSS files 
   file <- read_sav(fname) 
   # reads the data into the data frame called file

The maximum data size in *R* is technically restricted. The maximum size
depends on the *R* build (32-bit or 64-bit) and the operating system.
Some SDC methods require long computation times for large datasets (see the Section 
on `Computation time`_).


Missing values
--------------

The standard way missing values are represented in *R* is by the symbol
‘NA’, which is different to impossible values, such as division by zero
or the log of a negative number, which are represented by the symbol
‘NaN’. The value ‘NA’ is used for both numeric and categorical
variables. [#foot65]_ Values suppressed by the
localSuppression() routine are also replaced by the ‘NA’ symbol. Some
datasets and statistical software might use different values for missing
values, such as ‘999’ or strings. It is possible to include arguments in
read functions to specify how missing values in the dataset should be
treated and automatically recode missing values to ‘NA’. For instance,
the function read.table() has the ‘na.strings’ argument, which replaces
the specified strings with ‘NA’ values.

Missing values can also be recoded after reading the data into *R*. This
may be necessary if there are several different missing value codes in
the data, different missing value codes for different variables or the
read function for the datatype does not allow specifying the missing
value codes. When preparing data, it is important to recode any missing
values that are not coded as ‘NA’ to ‘NA’ in *R* before starting the
anonymization process to ensure the correct measurement of risk (e.g.,
:math:`k`-anonymity), as well as to ensure that many of the methods are
correctly applied to the data. :numref:`code76` shows how to recode the value
‘99’ to ‘NA’ for the variable “toilet”.

.. code-block:: R
   :linenos:
   :caption: Recoding missing values to NA
   :name: code76
   
   file[file[,'toilet'] == 99,'toilet'] <- NA 
   # Recode missing value code 99 to NA for variable toilet

Classes in R
------------

All objects in *R* are of a specific class, such as integer, character,
matrix, factor or dataframe. The class of an object is an attribute from
which the object inherits. To find out the class of an object, one can
use the function class(). Functions in *R* might require objects or
arguments of certain classes or functions might have different
functionality depending on the class of the argument. Examples are the
write functions that require dataframes and most functions in the
*sdcMicro* package that require either dataframes or *sdcMicro* objects.
The functionality of the functions in the *sdcMicro* package differs for
dataframes and *sdcMicro* objects. It is easy to change the class
attribute of an object with functions that start with “as.”, followed by
the name of the class (e.g., as.factor(), as.matrix(), as.data.frame()).
:numref:`code77` shows how to check the class of an object and change the
class to “data.frame”. Before changing the class attribute of the object
“file”, it was in the class “matrix”. An important class defined and
used in the *sdcMicro* package is the class named *sdcMicroObj*. This
class is described in the next section.

.. code-block:: R
   :linenos:
   :caption: Changing the class of an object in *R*
   :name: code77
   
   # Finding out the class of the object ‘file’ 
   class(file) 
   "matrix" 
   
   # Changing the class to data frame 
   file <- as.data.frame(file) 
   
   # Checking the result class(file) 
   "data.frame"

Objects of class *sdcMicroObj*
------------------------------

The *sdcMicro* package is built around objects [#foot66]_ of
class *sdcMicroObj*, a class especially defined for the *sdcMicro*
package. Each member of this class has a certain structure with slots
that contain information regarding the anonymization process (see :numref:`tab72`
for a description of all slots). Before evaluating risk
and utility and applying SDC methods, creating an object of class
*sdcMicro* is recommended. All examples in this guide are based on these
objects. The function used to create an *sdcMicro* object is
createSdcObj(). Most functions in the *sdcMicro* package, such as
microaggregation() or localSuppression(), automatically use the required
information (e.g., quasi-identifiers, sample weights) from the
*sdcMicro* object if applied to an object of class *sdcMicro*.

The arguments of the function createSdcObj() allow one to specify the
original data file and categorize the variables in this data file before
the start of the anonymization process. 

.. NOTE:: 
	For this, disclosure scenarios must already have been evaluated and quasi-identifiers
	selected. In addition, one must ensure there are no problems with the
	data, such as variables containing only missing values.

In :numref:`code78`, we show all arguments of the function createSdcObj(),
and first define vectors with the names of the different variables. This
practice gives a better overview and later allows for quick changes in
the variable choices if required. We choose the categorical
quasi-identifiers (keyVars); the variables linked to the categorical
quasi-identifiers that need the same suppression pattern (ghostVars, see the 
Section `Local suppression <anon_methods.html#Local suppression>`__); 
the numerical quasi-identifiers (numVars); the variables
selected for applying PRAM (pramVars); a variable with sampling weights
(weightVar); the clustering ID (hhId, e.g., a household ID, see the Section
`Household risk <measure_risk.html#Household risk>`__); 
a variable specifying the strata (strataVar) and the sensitive
variables specified for the computation of :math:`l`-diversity
(sensibleVar , see the Section 
`l-diversity <measure_risk.html#l-diversity>`__). 

.. NOTE:: 
	Most SDC methods in the 
	sdcMicro package are automatically applied within the strata, if the
	‘strataVar’ argument is specified.
	
Examples are local suppression and
PRAM. Not all variables must be specified, e.g., if there is no
hierarchical (household) structure, the argument ‘hhId’ can be omitted.
The names of the variables correspond to the names of the variables in
the dataframe containing the microdata to be anonymized. The selection
of variables is important for the risk measures that are automatically
calculated. Furthermore, several methods are by default applied to all
variables of one sort, e.g., microaggregation to all key
variables. [#foot67]_ After selecting these variables, we can
create the *sdcMicro* object. To obtain a summary of the object, it is
sufficient to write the name of the object.

.. code-block:: R
   :linenos:
   :caption: Selecting variables and creating an object of class *sdcMicroObj* for the SDC process in *R*
   :name: code78
   
   # Select variables for creating sdcMicro object 
   # All variable names should correspond to the names in the data file 
   # selected categorical key variables 
   selectedKeyVars = c('region', 'age', 'gender', 'marital', 'empstat') 
   
   # selected linked variables (ghost variables) 
   selectedGhostVars = c('urbrur') 
   
   # selected categorical numerical variables 
   selectedNumVar = c('wage', 'savings') 
   
   # weight variable 
   selectedWeightVar = c('wgt') 
   
   # selected pram variables 
   selectedPramVars = c('roof', 'wall') 
   
   # household id variable (cluster) 
   selectedHouseholdID = c('idh') 
   
   # stratification variable 
   selectedStrataVar = c('strata') 
   
   # sensitive variables for l-diversity computation 
   selectedSensibleVar = c('health') 
   
   # creating the sdcMicro object with the assigned variables 
   sdcInitial <- createSdcObj(dat         = file, 
   						   keyVars     = selectedKeyVars,
   					       ghostVars   = selectedGhostVars,
   					       numVar      = selectedNumVar,
   					       weightVar   = selectedWeightVar,
   					       pramVars    = selectedPramVars,
   					       hhId        = selectedHouseholdID,
                              strataVar   = selectedStrataVar, 
                              sensibleVar = selectedSensibleVar) 
   
   # Summary of object 
   sdcInitial 
   
   ## Data set with 4580 rows and 14 columns. 
   ## --> Categorical key variables: region, age, gender, marital, empstat 
   ## --> Numerical key variables: wage, savings 
   ## --> Weight variable: wgt 
   ## --------------------------------------------------------------------------- 
   ## 
   ## Information on categorical Key-Variables: 
   ## 
   ## Reported is the number, mean size and size of the smallest category for recoded variables. 
   ## In parenthesis, the same statistics are shown for the unmodified data. 
   ## Note: NA (missings) are counted as seperate categories! 
   ## 
   ## Key Variable Number of categories Mean size 
   ## region 2 (2) 2290.000 (2290.000) 
   ## age 5 (5) 916.000 (916.000) 
   ## gender 3 (3) 1526.667 (1526.667) 
   ## marital 8 (8) 572.500 (572.500) 
   ## empstat 3 (3) 1526.667 (1526.667) 
   ## 
   ## Size of smallest 
   ## 646 (646) 
   ## 16 (16) 
   ## 50 (50) 
   ## 26 (26) 
   ## 107 (107) 
   ## --------------------------------------------------------------------------- 
   ## 
   ## Infos on 2/3-Anonymity: 
   ## 
   ## Number of observations violating 
   ## - 2-anonymity: 157 
   ## - 3-anonymity: 281 
   ## 
   ## Percentage of observations violating 
   ## - 2-anonymity: 3.428 % 
   ## - 3-anonymity: 6.135 % 
   ## --------------------------------------------------------------------------- 
   ## 
   ## Numerical key variables: wage, savings 
   ## 
   ## Disclosure risk is currently between [0.00%; 100.00] 
   ## 
   ## Current Information Loss: 
   ## IL1: 0.00 
   ## Difference of Eigenvalues: 0.000% 
   ## ---------------------------------------------------------------------------
  
:numref:`tab72` presents the names of the slots and their respective contents.
The slot names can be listed using the function slotNames(), which is
illustrated in :numref:`code79`. Not all slots are used in all cases. Some
slots are filled only after applying certain methods, e.g., evaluating a
specific risk measure. Certain slots of the objects can be accessed by
accessor functions (e.g., extractManipData for extracting the anonymized
data) or print functions (e.g., print()) with the appropriate arguments.
The content of a slot can also be accessed directly with the ‘@’
operator and the slot name. This is illustrated for the risk slot in
:numref:`code79`. This functionality can be practical to save intermediate
results and compare the outcomes of different methods. Also, for manual
changes to the data during the SDC process, such as changing missing
value codes or manual recoding, the direct accession of the data in the
slots with the manipulated data (i.e., slot names starting with ‘manip’)
is useful. Within each slot there are generally several elements. Their
names can be shown with the names() function and they can be accessed
with the ‘$’ operator. This is shown for the element with the individual
risk in the risk slot.

.. code-block:: R
   :linenos:
   :caption: Displaying slot names and accessing slots of an S4 object
   :name: code79

   # List names of all slots of sdcMicro object
   slotNames(sdcInitial)
   
   ##  [1] "origData"          "keyVars"           "pramVars"
   ##  [4] "numVars"           "ghostVars"         "weightVar"
   ##  [7] "hhId"              "strataVar"         "sensibleVar"
   ## [10] "manipKeyVars"      "manipPramVars"     "manipNumVars"
   ## [13] "manipGhostVars"    "manipStrataVar"    "originalRisk"
   ## [16] "risk"              "utility"           "pram"
   ## [19] "localSuppression"  "options"           "additionalResults"
   ## [22] "set"               "prev"              "deletedVars"
   
   # Accessing the risk slot
   sdcInitial@risk
   
   # List names within the risk slot
   names(sdcInitial@risk)
   ## [1] "global"  "individual"  "numeric"
   
   # Two ways to access the individual risk within the risk slot
   sdcInitial@risk$individual
   get.sdcMicroObj(sdcInitial, "risk")$individual

.. _tab72:

.. table:: Slot names and slot description of *sdcMicro* object
   :widths: auto
   :align: center

   ==================================  ==================================
    Slotname                           Content                           
   ==================================  ==================================
    origData                           original data as specified in the 
                                       dat argument of the               
                                       createSdcObj() function           
    keyVars                            indices of columns in origData    
                                       with specified categorical key    
                                       variables                         
    pramVars                           indices of columns in origData    
                                       with specified PRAM variables     
    numVars                            indices of columns in origData    
                                       with specified numerical key      
                                       variables                         
    ghostVars                          indices of columns in origData    
                                       with specified ghostVars          
    weightVar                          indices of columns in origData    
                                       with specified weight variable    
    hhId                               indices of columns in origData    
                                       with specified cluster variable   
    strataVar                          indices of columns in origData    
                                       with specified strata variable    
    sensibleVar                        indices of columns in origData    
                                       with specified sensitive          
                                       variables for lDiversity          
    manipKeyVars                       manipulated categorical key       
                                       variables after applying SDC      
                                       methods (cf. keyVars slot)        
    manipPramVars                      manipulated PRAM variables after  
                                       applying PRAM (cf. pramVars slot) 
    manipNumVars                       manipulated numerical key         
                                       variables after applying SDC      
                                       methods (cf. numVars slot)        
    manipGhostVars                     manipulated ghost variables (cf.  
                                       ghostVars slot)                   
    manipStrataVar                     manipulated strata variables (cf. 
                                       strataVar slot)                   
    originalRisk                       global and individual risk        
                                       measures before anonymization     
    risk                               global and individual risk        
                                       measures after applied SDC        
                                       methods                           
    utility                            utility measures (il1 and eigen)  
    pram                               details on PRAM after applying    
                                       PRAM                              
    localSuppression                   number of suppression per         
                                       variable after local suppression  
    options                            options specified                 
    additionalResults                  additional results                
    set                                list of slots currently in use    
                                       (for internal use)                
    prev                               information to undo one step with 
                                       the undo() function               
    deletedVars                        variables deleted (direct         
                                       identifiers)                      
   ==================================  ==================================

There are two options to save the results after applying SDC methods:

-  Overwriting the existing *sdcMicro* object, or

-  Creating a new *sdcMicro* object. The original object will not be
   altered and can be used for comparing results. This is especially
   useful for comparing several methods and selecting the best option.

In both cases, the result of any function has to be re-assigned to an
object with the ‘<-‘ operator. Both methods are illustrated in
:numref:`code710`.

.. code-block:: R
   :linenos:
   :caption: Saving results of applying SDC methods
   :name: code710
   
   # Applying local suppression and reassigning the results to the same sdcMicro object
   sdcInitial <- localSuppression(sdcInitial)
   
   # Applying local suppression and assigning the results to a new sdcMicro object
   sdc1 <- localSuppression(sdcInitial)

If the results are reassigned to the same *sdcMicro* object, it is
possible to undo the last step in the SDC process. This is useful when
changing parameters. The results of the last step, however, are lost
after undoing that step. 

.. NOTE:: 
	The undolast() function can be used to
	go only one step back, not several.
	
The result must also be reassigned
to the same object. This is illustrated in :numref:`code711`.

.. code-block:: R
   :linenos:
   :caption: Undo last step in SDC process
   :name: code711
   
   # Undo last step in SDC process
   sdcInitial <- undolast(sdcInitial)

Household structure
-------------------

If the data has a hierarchical structure and some variables are measured
on the higher hierarchical level and others on the lower level, the SDC
process should be adapted accordingly (see also the Sections 
`Household risk <measure_risk.html#Household risk>`__ and 
`Anonymization of the quasi-identifier household size <anon_methods.html#Anonymization of the quasi-identifier household size>`__). A
common example in social survey data is datasets with a household
structure. Variables that are measured on the household level are, for
example, household income, type of house and region. Variables measured
on the individual level are, for example, age, education level and
marital status. Some variables are measured on the individual level, but
are nonetheless the same for all household members in almost all
households. These variables should be treated as measured on the
household level from the SDC perspective. An example is the variable
religion for some countries.

The SDC process should be divided into two stages in cases where the
data have a household structure. First, the variables on the higher
(household) level should be anonymized; subsequently, the treated
higher-level variables should be merged with the individual variables
and anonymized jointly. In this section, we explain how to extract
household variables from a file and merge them with the individual
levels variables after treatment in *R*. We illustrate this process with
an example of household and individual-level variables.

These steps are illustrated in :numref:`code712`. We require both an
individual ID and a household ID in the dataset; if they are lacking,
they must be generated. The individual ID has to be unique for every
individual in the dataset and the household ID has to be unique across
households. The first step is to extract the household variables and
save them in a new dataframe. We specify the variables that are measured
at the household level in the string vector “HHVars” and subtract only
these variables from the dataset. This dataframe will have for each
household the same number of entries as it has household members (e.g.,
if a household has four members, this household will appear four times
in the file). We next apply the function unique() to select only one
record per household. This argument of the unique function is the
household ID, which is the same for all household members, but unique
across households.

.. code-block:: R
   :linenos:
   :caption: Create a household level file with unique records (remove duplicates)
   :name: code712
   
   # Create subset of file with only variables measured at household level
   HHVars <- c('region', 'hhincome')
   fileHH <- file[,HHVars]
   
   # Remove duplicated rows based on the household ID / only every household once in fileHH
   fileHH <- unique(fileHH, by = c('HID'))
   
   # Dimensions of fileHH (number of households)
   dim(fileHH)

After anonymizing the household variables based on the dataframe
“fileHH”, we recombine the anonymized household variables with the
original variables, which are measured on the individual level. We can
extract the individual-level variables from the original dataset using
“INDVars” – a string vector with the individual-level variable names.
For extracting the anonymized data from the *sdcMicro* object, we can
use the extractManipData() function from the *sdcMicro* package. Next,
we merge the data using the merge function. The ‘by’ argument in the
merge function specifies the variable used for merging – in this case
the household ID, which has the same variable name in both datasets. All
other variables should have different names in both datasets. These
steps are illustrated in :numref:`code713`.

.. code-block:: R
   :linenos:
   :caption: Merging anonymized household-level variables with individual-level variables
   :name: code713
   
   # Extract manipulated household level variables from the SDC object
   HHmanip <- extractManipData(sdcHH)
   
   # Create subset of file with only variables measured at individual level
   fileIND <- file[,INDVars]
   
   # Merge the file by using the household ID
   fileCombined <- merge(HHmanip, fileIND, by = c('HID'))

The file *fileCombined* is used for the SDC process with the entire
dataset. How to deal with data with household structure is illustrated
in the case studies in the Section `Case studies <case_studies.html>`__.

As discussed in the Section
`Anonymization of the quasi-identifier household size <anon_methods.html#Anonymization of the quasi-identifier household size>`__),
the size of a household can also be a
quasi-identifier, even if the household size is not included in the
dataset as variable. For the purpose of evaluating the disclosure risk,
it might be necessary to create such a variable by a headcount of the
members of each household. :numref:`code714` shows how to generate a variable
household size with values for each individual based on the household ID
(HID). Two cases are shown: 1) the file sorted by household ID and 2)
the file not sorted.

.. code-block:: R
   :linenos:
   :caption: Generating the variable household size
   :name: code714
   
   # Sorted by HID
   file$hhsize <- rep(unname(table(file$HID)), unname(table(file$HID)))
   
   # Unsorted
   file$hhsize <- rep(diff(c(1, 1 + which(diff(file$HID) != 0), length(file$HID) + 1)),
                      diff(c(1, 1 + which(diff(file$HID) != 0), length(file$HID) + 1)))

.. NOTE:: 
	In some cases, the order of the individuals within the
	households can provide information that could lead to
	re-identification.
	
An example is information on the relation to the
household head. In many countries, the first individual in the household
is the household head, the second the partner of the household head and
the next few are children. Therefore, the line number within the
household could correlate well with a variable that contains information
on the relation to the household head. One way to avoid this unintended
release of information is to change the order of the individuals within
each household at random. :numref:`code715` illustrates a way to do this in
*R*.

.. code-block:: R
   :linenos:
   :caption: Changing the order of individuals within households
   :name: code715
   
   # List of household sizes by household
   hhsize <- diff(c(1, 1 + which(diff(file$HID) != 0), length(file$HID) + 1))
   
   # Line numbers randomly assigned within each household
   set.seed(123)
   dataAnon$INDID <- unlist(lapply(hhsize,
                                   function(n){sample(1:n, n, replace = FALSE, 
                                                      prob = rep(1/n, n))}))
   
   # Order the file by HID and randomized INDID (line number)
   dataAnon <- dataAnon[order(dataAnon$HID, dataAnon$INDID),]

Randomizing order and numbering of individuals or households
------------------------------------------------------------

Often the order and numbering of individuals, households, and also
geographical units contains information that could be used by an
intruder to re-identify records. For example, households with IDs that
are close to one another in the dataset are likely to be geographically
close as well. This is often the case in a census, but also in a
household survey households close to one another in the dataset likely
share the same low level geographical unit if the dataset is sorted in
that way. Another example is a dataset that is alphabetically sorted by
name. Here, removing the direct identifier name before release is not
sufficient to guarantee that the name information cannot be used (e.g.
first record has a name which likely starts with ‘a’). Therefore, it is
often recommended to randomize the order of records in a dataset before
release. Randomization can also be done within subsets of the dataset,
e.g., within regions. If suppressions were made in the geographical
variable used for creating the subsets, randomization within the
geographical subsets implies that the geographical variable is the same
for all records in the subset and the suppressed value can be easily
derived (for instance, in cases where the geographical unit is included
in the randomized ID). Therefore, if the variable used for the subsets
has suppressed values, randomization should be done at the dataset level
and not at the subset level.

:numref:`tab73` illustrates the need and process of randomizing the order of
records in a dataset. The first three columns in :numref:`tab73` show the
original dataset. Some suppressions were made in the variable
“district”, as shown in columns 4 to 6 (‘NA’ values). This dataset also
already shows the randomized household IDs. The order of the records in
the columns 1-3 and columns 4-6 is unchanged. By the order of the
records, it is easy to guess the values of the two suppressed values.
Both the record before and after have the same value for district as the
suppressed values, respectively 3 and 5. After reordering the dataset
based on the randomized household IDs, we see that it becomes impossible
to reconstruct the suppressed values based on the values of the
neighboring records. Note that in this example the randomization was
carried out within the regions and the region number is included in the
household ID (first digit).

.. _tab73:

.. table:: Illustration of randomizing order of records in a dataset
   :widths: auto
   :align: center
   
   ==============  ========  ==========  ==============  ========  ==========  ================  ========  ==========
    Original dataset                      Dataset with randomized               | Dataset for release ordered by the
                                          household ID                          | new randomized household ID 
   ------------------------------------  ------------------------------------  --------------------------------------
   | Household     | Region  | District  | Randomized    | Region  | District   | Randomized     | Region  | District 
   | ID            |         |           | household ID  |         |            | household ID   |         |
   ==============  ========  ==========  ==============  ========  ==========  ================  ========  ==========
    101              1         1             108          1           1             101              1      4       
    102              1         1             106          1           1             102              1      3       
    103              1         2             104          1           2             103              1      5       
    104              1         2             112          1           2             104              1      2       
    105              1         2             105          1           2             105              1      2       
    106              1         3             102          1           3             106              1      1       
    107              1         3             109          1           NA            107              1      3       
    108              1         3             107          1           3             108              1      1       
    109              1         4             101          1           4             109              1      NA      
    110              1         5             111          1           5             110              1      NA      
    111              1         5             110          1           NA            111              1      5       
    112              1         5             103          1           5             112              1      2       
    201              2         6             203          2           6             201              2      6       
    202              2         6             204          2           6             202              2      6       
    203              2         6             201          2           6             203              2      6       
    204              2         6             202          2           6             204              2      6       
   ==============  ========  ==========  ==============  ========  ==========  ================  ========  ==========

The randomization is easiest if done before or after the anonymization
process with *sdcMicro* and directly on the dataset (data.frame in *R*).
To randomize the order, we need an ID, such as an individual ID,
household ID or geographical ID. If the dataset does not contain such
ID, this should be created first. :numref:`code716` shows how to randomize
households. “HID” is the household ID and “regionid” is the region ID.
First the variable “HID” is replaced by a randomized variable
“HIDrandom”. Then the file is sorted by region and the randomized ID and
the actual order of the records in the dataset is changed. To make the
randomization reproducible, it is advisable to set a seed for the random
number generator.

.. code-block:: R
   :linenos:
   :caption: Randomize order of households
   :name: code716
   
   n <- length(file$HID) # number of households
   
   set.seed(123) # set seed
   # generate random HID
   file$HIDrandom <- sample(1:n, n, replace = FALSE, prob = rep(1/n, n)) 
   
   # sort file by regionid and random HID
   file <- file1[order(file$regionid, file$HIDrandom),]
    
   # renumber the households in randomized order to 1-n
   file$HIDrandom <- 1:n 

Computation time 
-----------------

Some SDC methods can take a very long time to evaluate in terms of
computation. For instance, local suppression with the function
localSuppression() of the *sdcMicro* package in *R* can take days to
execute on large datasets of more than 30,000 individuals that have many
categorical quasi-identifiers. Our experiments reveal that computation
time is a function of the following factors: the applied SDC method;
data size, i.e., number of observations, number of variables and the
number of categories or factor levels of each categorical variable; data
complexity (e.g., the number of different combinations of values of key
variables in the data); as well as the computer/server specifications.

:numref:`tab74` gives some indication of computation times for different
methods on datasets of different size and complexity based on findings
from our experiments. The selected quasi-identifiers and categories for
those variables in :numref:`tab74` are the same in both datasets being
compared. Because it is impossible to predict the exact computation
time, this table should be used to illustrate how long computations may
take. These methods have been executed on a powerful server. Given long
computation times for some methods, it is recommended, where possible,
to first test the SDC methods on a subset or sample of the microdata,
and then choose the appropriate SDC methods. *R* provides functions to
select subsets from a dataset. After setting up the code, it can then be
run on the entire dataset on a powerful computer or server.

.. _tab74:

.. table:: Computation times of different methods on datasets of different sizes
   :widths: auto
   :align: center

   =========================================  =================  =========================================  ================
    Dataset with 5,000 observations                               Dataset with 45,000 obervations
   ------------------------------------------------------------  -----------------------------------------------------------
       Methods                                 Computation        Methods                                    Computation
                                               time (hours)                                                  time (hours)
   =========================================  =================  =========================================  ================
    Top coding age, local suppression (k=3)    11                 Top coding age, local suppression (k=3)    268                                   
    Recoding age, local suppression (k=3)      8                  Recoding age, local suppression (k=3)      143                               
    Recoding age, local suppression (k=5)      10                 Recoding age, local suppression (k=5)      156             
   =========================================  =================  =========================================  ================
   
The number of categories and the product of the number of categories of
all categorical quasi-identifiers give an idea of the number of
potential combinations (keys). This is only an indication of the actual
number of combinations, which influences the computation time to
compute, for example, the frequencies of each key in the dataset. If
there are many categories but not so many combinations (e.g., when the
variables correlate), the computation time will be shorter.

:numref:`tab75` shows the number of categories for seven datasets with the
same variables but of different complexities that were all processed
using the same script on 16 processors, in order of execution time. The
table also shows an approximation of the number of unique combinations
of quasi-identifiers, as indicated by the percentage of observations
violating :math:`k`-anonymity in each dataset pre-anonymization in
relation to processing time. The results in the table clearly indicate
that both the number of observations (i.e., sample size) and the
complexity of the data play a role in the execution time. Also, using
the same script (and hence anonymization methods), the execution time
can vary greatly; the longest running time is about 10 times longer than
the shortest. Computer specifications also influence the computation
time. This includes the processor, RAM and storage media.

.. _tab75:

.. table:: Number of categories (complexity), record uniqueness and computation times
   :widths: auto
   :align: center
   
   =============  =======  ========  ============  ==========  ===========  ========  ==============  ==============  =================  
    Sample size    Number of categories                                                Percentage of observations      Execution time
                   per quasi-identifier (complexity)                                   violating k-anonimity before    in hours
                                                                                       before anonymization
   -------------  ------------------------------------------------------------------  ------------------------------  -----------------
         n         Water    Toilet    Occupation    Religion    Ethnicity    Region        k3             k5                
   =============  =======  ========  ============  ==========  ===========  ========  ==============  ==============  =================  
     20,014         10         4          70            5          7            6           74           88               53.72  
     66,285         15         6          39            4          0            24          40           49               67.19  
     60,747         13         6          70            8          9            4           35           45               74.47  
     26,601         19         6          84            10         10           10          77           87               108.84 
     38,089         17         6          30            5          56           9           70           81               198.90 
     35,820         19         7          67            6          NA           6           81           90               267.60 
     51,976         12         6          32            8          50           12          77           87               503.58  
   =============  =======  ========  ============  ==========  ===========  ========  ==============  ==============  =================  

The large-scale experiment executed for this guide utilized 75 microdata
files from 52 countries, using surveys on topics including health,
labor, income and expenditure. By applying anonymization methods
available in the *sdcMicro* package, at least 20 different anonymization
scenarios [#foot68]_ were tested on each dataset. Most of the
processing was done using a powerful server [#foot69]_ and up
to 16 – 20 processors (cores) at a time. Other processing platforms
included a laptop and desktop computers, each using four processors.
Computation times were significantly shorter for datasets processed on
the server, compared to those processed on the laptop and desktop.

The use of parallelization can improve performance even on a single
computer with one processor with multiple cores. Since *R* does not use
multiple cores unless instructed to do so, our anonymization programs
allowed for parallelization such that jobs/scenarios in each dataset
could be processed simultaneously through efficient allocation of tasks
to different processors. Without parallelization, depending on the
server/computer, only one core is used when running the jobs
sequentially. Running the anonymization program without parallelization
leads to significantly longer execution time. Note however, that the
parallelization itself also causes overhead. Therefore, a summation of
the times it takes to run each task in parallel does not necessarily
amount to the time it may take to run them sequentially. The fact that
the RAM is shared might, however, slightly reduce the gains of
parallelization. If you want to compare the results of different methods
on large datasets that require long computation times, using parallel
computing can be a solution. [#foot70]_

`Appendix D <appendices.html#Appendix D: Execution Times for Multiple Scenarios Tested using Selected Sample Data>`__
zooms in on seven selected datasets from a health survey that
were processed using the same parallelization program and anonymization
methods. Note that the computation times in the appendix are only meant
to create awareness for expected computation time, and may vary based on
the type of computer used. In our case, although all datasets were
anonymized using the parallelization program, computation times were
significantly shorter for datasets processed on the server, compared to
those processed on the laptop and desktop. Among those datasets
processed on the server using the same number of processors (datasets 1,
2 and 6), some variation also exists in the computation times. 

.. NOTE:: 
	Computation time in the table in 
	`Appendix D <appendices.html#Appendix D: Execution Times for Multiple Scenarios Tested using Selected Sample Data>`__
	includes recalculating
	the risk after applying the anonymization methods, which is
	automatically done in sdcMicro when using standard methods/functions.

Using the function groupVars(), for instance, is not computationally
intensive but can still take a long time if the dataset is large and
risk measures have to be recalculated.

Common errors
-------------

In this section, we present a few common errors and their causes, which
might be encountered when using the *sdcMicro* package in *R* for
anonymization of microdata:

-  The class of a certain variable is not accepted by the function,
   e.g., a categorical variable of class numeric should be first recoded
   to the required class (e.g., factor or data.frame). In the Section
   `Classes in R`_ is shown how to do this.

-  After manually making changes to variables the risk did not change,
   since it is not updated automatically and has to be manually
   recomputed by using the function calcRisks().

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

.. [#foot65]
   This is regardless of the class of the variable in *R*. See the Section
   `Classes in R`_ for more on classes in *R*.

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
   
   .. NOTE::
   	   Solutions are platform-dependent and therefore our solution
   	   is not further presented.