#  Cleaning and Analyzing TAFE_and_DETE_Exit_Responses_Survey

In this project I was given a task as a data analyst to clean and analyze two Employee survey dataset responses[TAFE survey and DETE survey] concerning resignation. 
i was told to show my workings and answer the following questions
- Are employees who only worked for the institutes for a short period of time resigning due to some kind of dissatisfaction? what about employees who have been there longer
- Are younger employees resigning due to some kin of dissatisfaction ? what about older employees

To start the project i began with the following
- data exploration
- data cleaning will be done to ensure te important columns and there relative records arenot dropped
- data analysis using data analysis expression and visualization
Data exploration  and cleaning wiil be done using python and analysis and visualization will be tackled with based on the volume of the cleaned data

# DATA EXPLORATION
- i loaded both dataset and combed through them to identify possible hinderance to my Analysis
from my EXPLORATION, i noticed that  
  - some rows are filled with "Not stated" meaning there is no value, especially in the DETE survey.
  - most columns does not concern my analysis 
  - some columns in both TAFE and DETE columns are different but with similar records
  - most columns have inconsistent data formats


# DATA CLEANING
- I ensured Missing values remained missing values by replacing any records which states "not_stated" with NaN
- removed unwanted columns from both survey, columns that are not necessary to my Analysis
- narrowed down both dataset to records that concerns only RESIGNATION
- standardized the column of DETE survey since the field name are easier to read compared to the TAFE survey
   - i made tthe columns lower case, removed leading and trailing spaces and replaced spaces with underscore.
- renamed columns with same datatype and data similarity from both tables to establish relationship when merging
- Changed inconsistent data format for cease_date in DETE from MM/YYYY to prevalent "YYYY" with datatype
- created a new column in DETE survey to represent the duration of years spent in institute and named it institute_tenure, then inserted records by subtracting the dete_start_date record from the cease_date record
- identified columns that corresponded to employee dissatisfaction in both survey. i ensured they both match in consistency and created a new column named general_dissatisfaction with a boolean datatype(True or false).
  and i merged all the reaons for dissatisfaction into these column.
- since most employees did not resign due to dissatisfationi made all missing values in this new created column false.
- Corrected incosistent format in "institute_tenure" column of TAFE survey, 01-feb, more than 20 years etc. i extracted the years using regular expression function and saved it in another column
- deleted the "institute_tenure" Column and renamed the new_column, "institute_tenure"
- merged both survey
- deleted all columns that have higher number of missing values by ensuring the non-missing values in a columnn be more than 500 from the total of 615  records
- the ages column was filled with insonsistent records like 31-35, 56 or older, 36 40. i extracted the first numerical integer and created a new columns to store the values
- i categorized the ages into ranges to get a clear read of the values and stored it in a new column
   - 20 or younger
   - 21 - 25
   - 26 - 30
   - 31 - 35
   - 36 - 40
   - 41 - 50
   - 51 - 60
   - 60 or older
- i also categorized  the institute_tenure to make filtering easier an stored it in a column
   - employee with "less than 3 years" of institute service will be called Novice
   - 3-6 years called junior
   - 7- 10 years intermediate
   - 11 or more years Senior


  # DATA VISUALIZATION AND REPORT
-  i made use of a python library called matplotlib for my pivot table analysis and graphical visualization
      # Analysis of Employee Dissatisfaction Based on period of time spent in the institute
   ![dat_1](https://github.com/hassanzuxh/TAFE_and_DETE_survey_Dissatsfaction_Analysis/assets/125826092/4db8c30f-d348-49d9-8288-efa9f4ca4d67)
   ![datchart](https://github.com/hassanzuxh/TAFE_and_DETE_survey_Dissatsfaction_Analysis/assets/125826092/e7d4b61e-9f5e-4bfa-b4b0-8e8add54f320)
   - the graphical representation above illustrates a clear correlation between service_tenure at either of the institutes and the likelihood of resigning due to dissatisfaction.
        - less thans 3 years: employees with less than 3 years of service_tenure cite dissatisfaction in 30% of resignations.
        - 4-7 years: Dissatisfaction slightly increases to 34% for employees with 4-7 years of service_tenure.
        - 7+ years: significantly , employees with 7 or more years of service_tenure report dissatisfaction in approximately 50% of resignations.

    This suggests a progressive rise in dissatisfaction as employees extends there stay in the institution .

     # Age Category and Dissatisfaction Trends
   ![age1](https://github.com/hassanzuxh/TAFE_and_DETE_survey_Dissatsfaction_Analysis/assets/125826092/961ef0f1-e90a-4591-a449-969fe83f01fb)
![agechart](https://github.com/hassanzuxh/TAFE_and_DETE_survey_Dissatsfaction_Analysis/assets/125826092/471d9d63-5ec7-4f10-a91b-b1d3c856c2fd)

   - from the graph i can say that there is a consistent trend along the axes.
        - General Trend: Older employees tend to resign more often citing dissatisfaction, which is consistent across various Age-ranges. This trend remains fairly consistent, emphasizing that as employees age, they become more inclined to attribute their resignations to dissatisfaction.
        - Exception: Notable deviation in dissatisfaction trends for the 26-30 and 31-35 Age Range, indicates the unique factors at play. judging from the age range, this can majorly be due to career development, job roles or workplace dynamics.

the fact that older people in different age-ranges tend to quit their jobs more often because of some kind of dissatisfaction shows how important it is to understand what different employees need at various points in their careers. But their are some younger age-ranges where this is not as clear. from my findings higher number of young age-range of employee(26-30) seems to express dissatisfaction which seems strange, deviating from the consisent trend. further exploration needs to be done to uncover this deviation.


in summary, we can confidently say that employees who have stayed at either one of the institutions for a while are much more likely to quit because of some kind of dissatisfaction. this is simply true for older employees as well, except for those in the 26-30 age-range who actually show some of the highest dissatisfaction rates. 

some challenges faced when cleaning the data include :

- having to fill up the missing values for general_dissatifaction columns with false value due to it being prevalent in the column 

- also on the TAFE survey the institute _tenure column records was not properly formatted. the dates was not formatted to have years. My cleanng on that particular column might impede the intent of the survey manager on what those records represent

