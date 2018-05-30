Lists
=====

May no longer be needed in this format or need to be automated


List of Tables
---------------

Table 4.1: Example dataset showing sample frequencies, population
frequencies and individual disclosure risk 20

Table 4.2: Example dataset to illustrate the effect of missing values on
k-anonymity 25

Table 4.3: l-diversity illustration 26

Table 4.4: Sample uniques and special uniques 28

Table 4.5: Illustrating the calculation of SUDA and DIS-SUDA scores 30

Table 5.1: SDC methods and corresponding functions in *sdcMicro* 39

Table 5.3: Illustration of the effect of recoding on the theoretically
possible number of combinations an a dataset 40

Table 5.3: Illustration of the effect of recoding on the theoretically
possible number of combinations an a dataset 41

Table 5.4: Local suppression illustration - sample data before and after
suppression 49

Table 5.5: How importance vectors and k-anonymity thresholds affect
running time and total number of suppressions 52

Table 5.6 Effect of the all-\ *m* approach on k-anonymity 53

Table 5.7: Sample data before and after perturbation 56

Table 5.8: Tabulation of variable “region” before and after PRAM 57

Table 5.9: Tabulation of variable “region” before and after (invariant)
PRAM 58

Table 5.10: Cross-tabulation of variable “region” and variable “gender”
before and after invariant PRAM 59

Table 5.11: Illustrating the effect of choosing mean vs. median for
microaggregation where outliers are concerned 62

Table 5.12: Illustration of multivariate microaggregation 63

Table 5.13: Grouping methods for microaggregation that are implemented
in *sdcMicro* 64

Table 5.14: Simplified example of the shuffling method 72

Table 6.1: Description of anonymization methods by scenario 90

Table 7.1: Packages and functions for reading data in *R* 95

Table 7.2: Slot names and slot description of *sdcMicro* object 100

Table 7.3 Illustration of randomizing order of records in a dataset 104

Table 7.4: Computation times of different methods on datasets of
different sizes 106

Table 7.5: Number of categories (complexity), record uniqueness and
computation times 106

Table 8.1: Illustration of merging variables without information loss
for SDC process 111

Table 9.1 Overview of variables in dataset 122

Table 9.2: List of selected quasi-identifiers 126

Table 9.3: Overview of selected utility measures 127

Table 9.4: Number and proportion of households violating k-anonymity 129

Table 9.5: Percentiles 90-100 of the variable LANDSIZE 131

Table 9.6: 50 largest values of the variable LANDSIZE 131

Table 9.7: Frequencies of variable HHSIZE (household size) 132

Table 9.8: Number and proportion of households violating k-anonymity
after anonymization 137

Table 9.9: Univariate frequencies of the PRAMmed variable before and
after anonymization 139

Table 9.10: Multivariate frequencies of the variables WATER with RURURB
before and after anonymization 139

Table 9.11: GINI point estimates and bootstrapped confidence intervals
for sum of expenditure components 139

Table 9.12: Mean monthly expenditure and mean monthly income per capita
by rural/urban 140

Table 9.13 Shares of expenditures components 140

Table 9.14: k-anonymity violations 142

Table 9.15: Number of suppressions by variable for different variations
of local suppression 145

Table 9.16: k-anonymity violations 145

Table 9.17: Net enrollment in primary and secondary education by gender
145

Table 9.18: Overview of the variables in the dataset 149

Table 9.19: Overview of selected key variables for PUF file 152

:math:`k`\ Table 9.20: Number and proportion of households violating
-anonymity 155

Table 9.21: Number of suppressions by variable after local suppression
with and without importance vector 158

Table 9.22: Comparison of utility measures 163

Table 9.23: Number of records violating k-anonimity 164

Table 9.24: Overview of recodes of categorical variables at individual
level 166

Table 9.25: k-anonymity violations 170

List of Figures
-----------------

Figure 2.1: Risk-utility trade-off 7

Figure 4.1 Classification of variables 17

Figure 4.2: Visualizations of DIS-SUDA scores 32

Figure 5.1 Effect of recoding – frequency counts before and after
recoding 43

Figure 5.2 Age variable before and after recoding 44

Figure 5.3 Age variable before and after recoding 45

Figure 5.4: Utilizing the frequency distribution of variable age to
determine threshold for top coding 47

Figure 5.5: Changes in labor market indicators after anonymization of
I2D2 data 51

Figure 5.6: Illustration of effect of noise addition to outliers 66

Figure 5.7: Frequency distribution of a continuous variable before and
after noise addition 68

Figure 5.8: Noise levels and the impact on the value range (percentiles)
69

Figure 6.1: The trade-off between risk and utility in a hypothetical
dataset 77

Figure 6.2: Effect of anonymization on the point estimates and
confidence interval of the gender coefficient in the Mincer equation 86

Figure 6.3: Histograms of income before and after anonymization 87

Figure 6.4: Density plots of income before and after anonymization 88

Figure 6.5: Example of box plots of an expenditure variable before and
after anonymization 89

Figure 6.6: Mosaic plot to illustrate the changes in the WATER variable
90

Figure 6.7: Comparison of treated vs. untreated gender and relationship
status variables with mosaic plots 91

Figure 6.8: Mosaic plot of the variables ROOF and TOILET before
anonymization 92

Figure 6.9: Mosaic plot of the variables ROOF and TOILET after
anonymization 92

Figure 8.1: Overview of the SDC process 118

Figure 9.1: Lorenz curve based on positive total expenditures values 140

List of Examples
-----------------

:math:`f_{k}`\ Example 4.1: Calculating using *sdcMicro* 21

Example 4.2: Calculating the sample and population frequencies using
*sdcMicro* 22

Example 4.3: The individual risk slot in the *sdcMicro* object 23

Example 4.4: Using the print() function to display observations
violating k-anonymity 24

Example 4.5: Computing k-anonymity violations for other values of k 25

:math:`l`\ Example 4.6: -diversity function in *sdcMicro* 27

Example 4.7: Evaluating SUDA scores 31

Example 4.8: Histogram and density plots of DIS-SUDA scores 31

Example 4.9 Example with the function dRisk() 33

Example 4.10: Computing 90 % percentile of variable income 34

Example 4.11: Computation of the global risk measure 34

Example 4.12: Computation of expected number of re-identifications 35

Example 4.13: Number of individuals with individual risk higher than the
threshold 0.05 35

Example 4.14: Computation of household risk and expected number of
re-identifications 36

Example 5.1: Using the sdcMicro function groupVars() to recode a
categorical variable 42

Example 5.2: Using the *sdcMicro* function globalRecode() to recode a
continuous variable (age) 43

Example 5.3: Using globalRecode() to create intervals of unequal width
44

Example 5.4: Constructing right-open intervals for semi-continuous
variables using built-in *sdcMicro* function globalRecode() 46

Example 5.5: Constructing intervals for semi-continuous and continuous
variables using manual recoding in *R* 46

Example 5.6: Top coding and bottom coding in *sdcMicro* using
topBotCoding() function 47

Example 5.7: Application of local suppression with and without
importance vector 50

:math:`m`\ Example 5.8 The all- approach in sdcMicro 53

Example 5.9: Manually suppressing values in linked variables 54

Example 5.10: Suppressing values in linked variables by specifying ghost
variables 54

Example 5.11: Application of built-in *sdcMicro* function localSupp() 55

Example 5.12: Producing reproducible PRAM results by using set.seed() 58

Example 5.13: Selecting the variable “toilet” to apply PRAM 59

Example 5.14: Specifying minimum values for diagonal entries in PRAM
transition matrix 59

Example 5.15: Minimizing unlikely combinations by applying PRAM within
strata 60

Example 5.16: Applying univariate microaggregation with *sdcMicro*
function microaggregation() 62

Example 5.17: Multivariate microaggregation with the Maximum Distance to
Average Vector (MDAV) algorithm in *sdcMicro* 64

Example 5.18: Specifying strata variables for microaggregation 64

Example 5.19: Uncorrelated noise addition 67

Example 5.20: Correlated noise addition 69

Example 5.21: Noise addition for outliers using the ‘outdect’ method 70

Example 5.22: Noise addition to aggregates and their components 70

Example 5.23: Rank swapping using *sdcMicro* 71

Example 5.24: Shuffling using a specified regression equation 73

Example 6.1: Using the print() function to retrieve the total number of
suppressions for each categorical key variable 78

Example 6.2: Displaying the number of missing values for each
categorical key variable in an *sdcMicro* object 78

Example 6.3: Computing number of records changed per variable 79

Example 6.4: Comparing contingency tables of categorical variables 79

Example 6.5: Comparing the means of continuous variables 80

Example 6.6: Comparing covariance structure and correlation matrices of
numeric variables 81

Example 6.7: Using dUtility() to compute IL1s data utility measure in
*sdcMicro* 82

Example 6.8: Using dUtility() to compute eigenvalues in *sdcMicro* 83

Example 6.9: Computing the GINI coefficient from the income variable to
determine income inequality 83

Example 6.10: Estimating the Mincer equation (regression) to evaluate
data utility before and after anonymization 84

Example 6.11: Plotting histograms and kernel densities 87

Example 6.12: Creating boxplots for continuous variables 88

Example 6.13: Creating univariate mosaic plots 89

Example 6.14: Creating multivariate mosaic plots 91

Example 7.1: Loading required packages 94

Example 7.2: Displaying help for functions 94

Example 7.3: Reading in a *STATA* file 95

Example 7.4: Reading in an *Excel* file 95

Example 7.5: Reading in an *SPSS* file 96

Example 7.6: Recoding missing values to NA 96

Example 7.7: Changing the class of an object in *R* 97

Example 7.8: Selecting variables and creating an object of class
*sdcMicroObj* for the SDC process in *R* 98

Example 7.9: Displaying slot names and accessing slots of an S4 object
100

Example 7.10: Saving results of applying SDC methods 101

Example 7.11: Undo last step in SDC process 101

Example 7.12: Create a household level file with unique records (remove
duplicates) 102

Example 7.13 Merging anonymized household-level variables with
individual-level variables 103

Example 7.14 Generating the variable household size 103

Example 7.15 Changing the order of individuals within households 103

Example 7.16: Randomize order of households 105

Example 9.1: Loading required packages 120

Example 9.2: Loading the data 120

Example 9.3: Number of individuals and variables and variable names 120

Example 9.4: Tabulation of the variable ‘gender’ and summary statistics
for the variable ‘total annual expenditures’ in *R* 122

Example 9.5: Recoding missing value codes 124

Example 9.6: Dropping variables with only missing values 125

Example 9.7: Selecting the variables for the household-level
anonymization 127

Example 9.8: Taking a subset with only households 128

Example 9.9: Creating a *sdcMicro* object for the household variables
128

Example 9.10: Showing number of households violating k-anonymity for
levels 2,3 and 5 129

Example 9.11: Showing households that violate k-anonymity 130

Example 9.12: Printing global risk measures 130

Example 9.13: Observations with individual risk higher than 1% 130

Example 9.14 Percentiles of LANDSIZE and listing the sizes of the
largest 50 plots 131

Example 9.15: Removing households with large (rare) household sizes 132

Example 9.16: Local suppression with and without importance vector 134

Example 9.17: Applying PRAM 135

Example 9.18: Anonymizing the variable LANDSIZEHA 135

Example 9.19: Anonymizing continuous variables 137

Example 9.20: Measuring risk of re-identification of continuous
variables 138

Example 9.21: Merging the files with household and individual-level
variables and creating an *sdcMicro* object for the anonymization of the
individual-level variables 141

Example 9.22: Global risk of the individual-level variables 142

Example 9.23: Recoding age in 10-year intervals in the range 15 – 65 and
top code age over 65 years143

Example 9.24: Experimenting with different options in local suppression
144

Example 9.25: Using the report() function for internal and external
reports 146

Example 9.26: Exporting the anonymized dataset 147

Example 9.27: Loading required packages and datasets 148

Example 9.28 Number of individuals and variables and variable names 148

Example 9.29: Selecting the variables for the household-level
anonymization 153

Example 9.30: Taking a subset with only households 154

Example 9.31: Creating a *sdcMicro* object for the household variables
154

:math:`k`\ Example 9.32: Showing number of households violating
-anonymity for levels 2, 3 and 5 155

:math:`k`\ Example 9.33: Showing records of households that violate
-anonymity 156

Example 9.34: Printing global risk measures 156

Example 9.35 Determining the highest individual risk 156

Example 9.36: Local suppression with and without importance vector 158

Example 9.37: Applying PRAM 160

Example 9.38: Anonymization of income and expenditure variables 161

Example 9.39: Measuring risk of re-identification of continuous
variables 162

Example 9.40: Computation of decile dispersion ratio and share of total
consumption by the poorest decile 163

Example 9.41: Merging the files with household and individual-level
variables and creating an *sdcMicro* object for the anonymization of the
individual-level variables 163

Example 9.42: Risk measures before anonymization 165

Example 9.43: Recoding the categorical and continuous variables 166

Example 9.44: Local suppression to reach 5-anonimity 168

Example 9.45: Randomizing the order of records within regions 169

Example 9.46: Exporting the anonymized PUF file 171

