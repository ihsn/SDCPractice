Glossary and list of acronyms
===============================

List of Acronyms
-------------------

AFR       
    Sub Saharan Africa
COICOP    
    Classification of Individual Consumption by Purpose         
CRAN      
    Comprehensive R Archive Network
CTBIL     
    Contingency Table-Based Information Loss               
DHS       
    Demographic and Health Surveys 
DIS       
    Data Intrusion Simulation      
EAP       
    East Asia and the Pacific      
ECA       
    Europe and Central Asia        
EU        
    European Union                 
GIS       
    Geographical Information System
GPS       
    Global Positioning System      
GUI       
    Graphical User Interface       
HIV/AIDS  
    Human Immunodeficiency Virus/Acquired Immune Deficiency Syndrome  
I2D2      
    International Income Distribution Database  
IHSN      
    International Household Survey Network   
LAC       
    Latin America and the Caribbean
LSMS      
    Living Standards Measurement Survey    
MDAV      
    Maximum Distance Average Vector
MDG       
    Millennium Development Goal    
MENA      
    Middle East and North America  
MICS      
    Multiple Indicator Cluster Survey
MME       
    Mean Monthly Expenditures      
MMI       
    Mean Monthly Income            
MSU       
    Minimal Sample Uniques         
NSI       
    National Statistical Institute 
NSO       
    National Statistical Office    
OECD      
    Organization for Economic Cooperation and Development 
PARIS21   
    Partnership in Statistics for Development in the 21\ :sup:`st` century   
PRAM      
    Post Randomization Method      
PC        
    Principal Component            
PUF       
    Public Use File                
SA        
    South Asia                     
SDC       
    Statistical Disclosure Control 
SSE       
    Sum of Squared Errors          
SHIP      
    Survey-based Harmonized        
    Indicators Program             
SUDA      
    Special Uniques Detection Algorithm 
SUF       
    Scientific Use File            
UNICEF    
    United Nations Children’s Fund 


Glossary
-----------

Administrative data  
   Data collected for administrative purposes by government agencies.  Typically, administrative data require specific SDC methods.  
Anonymization 
   Use of techniques that convert confidential data into anonymized data/ removal or masking of identifying information from   datasets.  
Attribute disclosure 
   Attribute disclosure occurs if an intruder is able to determine new characteristics of an individual  or organization based on the   information available in the   released data. 
Categorical variable 
   A variable that takes values over a finite set, e.g., gender. Also  called factor in *R*.  
Confidentiality   
   Data confidentiality is a property of data, usually resulting from legislative measures, which prevents it from  unauthorized   disclosure. [#foot2]_   
Confidential data 
   Data that will allow   identification of an individual   or organization, either directly  or indirectly. [#foot1]_    
Continuous variable  
   A variable with which numerical   and arithmetic operations can be  performed, e.g., income.  
Data protection   
   Data protection refers to the set of privacy-motivated laws, policies and procedures 
   that aim  to minimize intrusion into respondents’ privacy caused by the collection, 
   storage and dissemination of personal data.  [#foot2]_   
Deterministic methods 
   Anonymization methods that follow a certain algorithm and produce   
   the same results if applied repeatedly to the same data with  the same set of parameters. 
Direct identifier 
   A variable that reveals directly  and unambiguously the identity of a respondent, 
   e.g., names, social identity numbers.  
Disclosure   
   Disclosure occurs when a person   or an organization recognizes or  
   learns something that they did not already know about another person 
   or organization through released data. [#foot1]_  
   See also Identity disclosure,  Attribute disclosure and  Inferential disclosure.   
Disclosure risk   
   A disclosure risk occurs if an unacceptably narrow estimation of a respondent’s 
   confidential information is possible or if  exact disclosure is possible with a high level of   
   confidence. [#foot2]_  Disclosure risk also refers to the probability that successful   
   disclosure could occur.   
End user  
   The user of the released  microdata file after   anonymization. Who is the end  
   user depends on the release type. 
Factor variable   
   Factor variables are one way to   classify categorical variables in *R*.   
Hierarchical structure 
   Data is made up of collections of records that are interconnected   through links, 
   e.g., individuals  belonging to groups/households or employees belonging to companies. 
Identifier   
   An identifier is a variable/   information that can be used to   establish identity 
   of an  individual or organization. Identifiers can lead to direct or indirect identification.  
Identity disclosure  
   Identity disclosure occurs if an  intruder associates a known individual or organization with a released data record.  
Indirect identification   
   Indirect identification occurs when the identity of an   individual or organization is  
   disclosed, not using direct identifiers but through a combination of unique 
   characteristics in key  variables. [#foot1]_   
Inferential disclosure 
   Inferential disclosure occurs if  an intruder is able to determine  
   the value of some characteristic  of an individual or organization  
   more accurately with the released data than otherwise would have been possible. 
Information loss  
   Information loss refers to the reduction of the information   
   content in the released data   relative to the information content in the raw data.  
   Information loss is often measured with respect to common   analytical measures, such as   
   regressions and indicators. See also Utility.  
Interval  
   A set of numbers between two   designated endpoints that may or  may not be included. 
   Brackets  (e.g., [0, 1]) denote a closed interval, which includes the   endpoints 0 and 1. 
   Parentheses (e.g., (0, 1) denote an open   interval, which does not include  the endpoints. 
Intruder  
   A user who misuses released data  by trying to disclose information about an 
   individual or organization, using a set of   characteristics known to the   user.  
:math:`k`-anonymity 
   The risk measure  :math:`k`-anonymity is based on   the principle that the 
   number of  individuals in a sample sharing   the same combination of values (key) 
   of categorical key  variables should be higher than a specified  threshold :math:`k`. 
Key   
   A combination or pattern of key   variables/quasi-identifiers.   
Key variables 
   A set of variables that, in combination, can be linked to  external information to   
   re-identify respondents in the released dataset. Key variables   are also called   
   “quasi-identifiers” or “implicit  identifiers”.  
Microaggregation  
   Anonymization method that is   based on replacing values for a   certain variable 
   with a common value for a group of records. The grouping of records is based on a 
   proximity measure of variables of interest. The groups of records   are also used 
   to calculate the replacement value. 
Microdata 
   A set of records containing information on individual respondents or on  economic 
   entities. Such records   may contain responses to a survey questionnaire or 
   administrative   forms. 
Noise addition 
   Anonymization method based on  adding or multiplying a   stochastic or randomized 
   number   to the original values to protect data from exact matching with  
   external files. Noise addition is typically applied to continuous   variables. 
Non-perturbative methods  
   Anonymization methods that reduce the detail in the data or suppress certain 
   values (masking) without distorting the data structure. 
Observation  
   A set of data derived from an  object/unit of experiment, e.g.,  an individual 
   (in  individual-level data), a household (in household-level  data) or a company 
   (in company data). Observations are also   called “records”.  
Original data 
   The data before SDC/anonymization methods were applied. Also called “raw data” 
   or “untreated data”.   
Outlier   
   An unusual value that is  correctly reported but is not  typical of the rest of the population. 
   Outliers can also be  observations with an unusual   combination of values for variables, 
   such as 20-year-old widow. On their own age, 20 and   widow are not unusual values, but their combination may  be. [#foot1]_ 
Perturbative methods 
   Anonymization methods that alter  values slightly to limit  disclosure risk by creating uncertainty around the true values, while retaining as much   content and structure as  possible, e.g. microaggregation   and noise addition. 
Population unique 
   The only record in the population with a particular set of  characteristics, such that the individual or organization can be distinguished from other units in the population based on that set  of characteristics. 
Post Randomization Method (PRAM)
   Anonymization method for  microdata in which the scores of  a categorical variable 
   are altered according to certain   probabilities. It is thus intentional misclassification  
   with known misclassification   probabilities. [#foot1]_   
Probabilistic methods 
   Anonymization methods that depend on a probability mechanism or a   
   random number-generating  mechanism. Every time a   probabilistic method is used, a   
   different outcome is generated.   
Privacy   
   Privacy is a concept that applies to data subjects while confidentiality applies to data. 
   The concept is defined as   follows: "It is the status accorded to data which has been   
   agreed upon between the person or organization furnishing the data  and the organization 
   receiving it and which describes the degree of protection which will be  provided." [#foot2]_   
Public Use File (PUF) 
   Type of release of microdata   file, which is freely available   to any user, for example on the   internet.  
Quasi-identifiers 
   A set of variables that, in combination, can be linked to  external information to   
   re-identify respondents in the released dataset.  Quasi-identifiers are also called 
   “key variables” or “implicit   identifiers”.  
Raw data  
   The data before SDC/anonymization methods were applied. Also called “original data” 
   or “untreated  data”. 
Recoding  
   Anonymization method for  microdata in which groups of   existing categories/values 
   are replaced with new values, e.g. the values ‘protestant’, and   ‘catholic’ are replaced with   
   ‘Christian’. Recoding reduces the detail in the data. Recoding of   continuous variables leads to a   
   transformation from continuous to categorical, e.g. creating income bands. 
Record 
   A set of data derived from an  object/unit of experiment, e.g.,  an individual 
   (in  individual-level data), a household (in household-level  data) or a company (in company data). Records are also called “observations”.   
Regression   
   A statistical process of  measuring the relation between the mean value of one variable and corresponding values of other variables. 
Re-identification risk 
   See Disclosure risk 
Release   
   Dissemination – the release to users of information obtained  through a statistical activity.   [#foot2]_  
Respondents  
   Individuals or units of   observation whose  information/responses to a survey make up the data file. 
Sample unique 
   The only record in the sample  with a particular set of  characteristics, such that 
   the individual or organization can be distinguished from other units in the sample based on that set of   characteristics.  
Scientific Use File (SUF) 
   Type of release of microdata   file, which is only available to  selected researchers 
   under contract. Also known as “licensed file”, “microdata under contract” or “research file”. 
*sdcMicro*   
   An *R* based package authored by  Templ, M., Kowarik, A. and Meindl, B. with tools for 
   the  anonymization of microdata, i.e.  for the creation of public- and   scientific-use files.  
*sdcMicroGUI* 
   A GUI for the *R* based   *sdcMicro* package, which allows  users to use the *sdcMicro* 
   tools without *R* knowledge. 
Sensitive variables  
   Sensitive or confidential variables are those whose values  must not be discovered for 
   any respondent in the dataset. The determination of sensitive variables is often subject to  legal and ethical concerns. 
Statistical Disclosure Control (SDC)
   Statistical Disclosure Control techniques can be defined as the  set of methods to reduce 
   the risk of disclosing information on   individuals, businesses or other  organizations. 
   Such methods are   only related to the dissemination step and are usually based on  restricting the amount of or   modifying the data released. [#foot2]_   
Suppression  
   Data suppression involves not  releasing information that is  considered unsafe because it   
   fails confidentiality rules being applied. Sometimes this is done   is by replacing values 
   signifying individual attributes with missing values. In the context of this guide, 
   usually to achieve a  desired level of *k*- anonymity.  
Threshold 
   An established level, value,   margin or point at which values   that fall above or 
   below it will  deem the data safe or unsafe. If  unsafe, further action will need  
   to be taken to reduce the risk of identification.   
Utility   
   Data utility describes the value  of data as an analytical  resource, comprising analytical   
   completeness and analytical validity.  
Untreated data 
   The data before SDC/anonymization methods were applied. Also called “raw data” or “original data”. 
Variable  
   Any characteristic, number or  quantity that can be measured or  counted for each unit of  observation.  

.. [#foot1]
   Australian Bureau of Statistics, http://www.nss.gov.au/nss/home.nsf/pages/Confidentiality+-+Glossary

.. [#foot2]
   OECD, http://stats.oecd.org/glossary
