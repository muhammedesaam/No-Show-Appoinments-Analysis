::: {#notebook .border-box-sizing tabindex="-1"}
::: {#notebook-container .container}
::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
Project: Investigate a Dataset - No Show Appointments[¶](#Project:-Investigate-a-Dataset---No-Show-Appointments){.anchor-link} {#Project:-Investigate-a-Dataset---No-Show-Appointments}
==============================================================================================================================

Table of Contents[¶](#Table-of-Contents){.anchor-link} {#Table-of-Contents}
------------------------------------------------------

-   [Introduction](#intro)
-   [Data Wrangling](#wrangling)
-   [Exploratory Data Analysis](#eda)
-   [Conclusions](#conclusions)
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
[]{#intro}

Introduction[¶](#Introduction){.anchor-link} {#Introduction}
--------------------------------------------

### Dataset Description[¶](#Dataset-Description){.anchor-link} {#Dataset-Description}

This dataset collects information from 100k medical appointments in
Brazil and is focused on the question of whether or not patients show up
for their appointment. A number of characteristics about the patient are
included in each row.

**- ScheduledDay:** tells us on what day the patient set up their
appointment.

**- Neighborhood:** indicates the location of the hospital.

**- Scholarship:** indicates whether or not the patient is enrolled in
Brasilian welfare program Bolsa Família.

**- No-Show:** it says 'No' if the patient showed up to their
appointment, and 'Yes' if they did not show up.

### Question(s) for Analysis[¶](#Question(s)-for-Analysis){.anchor-link} {#Question(s)-for-Analysis}

> **Q1**:Dose The Age affect the attendance ?
>
> **Q2**:Does Age and Diseases factor affect the attendance?
>
> **Q3**:Which gender have more no-show?
>
> **Q4**:Does Sending SMS affect attendance?
>
> **Q5**:Does Neighbourhood affect attendance?
>
> **Q6**:Is Having a Scholarship affects attendance?
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Importing Libraries[¶](#Importing-Libraries){.anchor-link} {#Importing-Libraries}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[1\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #importing Libraries which will be used
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    import seaborn as sns

    %matplotlib inline
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
[]{#wrangling}

Data Wrangling[¶](#Data-Wrangling){.anchor-link} {#Data-Wrangling}
------------------------------------------------

> load in the data check for cleanliness

### General Properties[¶](#General-Properties){.anchor-link} {#General-Properties}
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Loading Data[¶](#Loading-Data){.anchor-link} {#Loading-Data}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[2\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #load my data and print some rows to check it
    df = pd.read_csv('noshowappointments-kagglev2-may-2016.csv')
    df.head()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[2\]:
:::

::: {.output_html .rendered_html .output_subarea .output_execute_result}
<div>

      PatientId      AppointmentID   Gender   ScheduledDay           AppointmentDay         Age   Neighbourhood       Scholarship   Hipertension   Diabetes   Alcoholism   Handcap   SMS\_received   No-show
  --- -------------- --------------- -------- ---------------------- ---------------------- ----- ------------------- ------------- -------------- ---------- ------------ --------- --------------- ---------
  0   2.987250e+13   5642903         F        2016-04-29T18:38:08Z   2016-04-29T00:00:00Z   62    JARDIM DA PENHA     0             1              0          0            0         0               No
  1   5.589978e+14   5642503         M        2016-04-29T16:08:27Z   2016-04-29T00:00:00Z   56    JARDIM DA PENHA     0             0              0          0            0         0               No
  2   4.262962e+12   5642549         F        2016-04-29T16:19:04Z   2016-04-29T00:00:00Z   62    MATA DA PRAIA       0             0              0          0            0         0               No
  3   8.679512e+11   5642828         F        2016-04-29T17:29:31Z   2016-04-29T00:00:00Z   8     PONTAL DE CAMBURI   0             0              0          0            0         0               No
  4   8.841186e+12   5642494         F        2016-04-29T16:07:23Z   2016-04-29T00:00:00Z   56    JARDIM DA PENHA     0             1              1          0            0         0               No

</div>
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[3\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    df.shape
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[3\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    (110527, 14)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Check datatypes[¶](#Check-datatypes){.anchor-link} {#Check-datatypes}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[4\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #check dtypes to find if there's incorrect data type
    df.dtypes
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[4\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    PatientId         float64
    AppointmentID       int64
    Gender             object
    ScheduledDay       object
    AppointmentDay     object
    Age                 int64
    Neighbourhood      object
    Scholarship         int64
    Hipertension        int64
    Diabetes            int64
    Alcoholism          int64
    Handcap             int64
    SMS_received        int64
    No-show            object
    dtype: object
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Checking if there is null data[¶](#Checking-if-there-is-null-data){.anchor-link} {#Checking-if-there-is-null-data}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[5\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #check if there is a null values
    df.isnull().sum()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[5\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    PatientId         0
    AppointmentID     0
    Gender            0
    ScheduledDay      0
    AppointmentDay    0
    Age               0
    Neighbourhood     0
    Scholarship       0
    Hipertension      0
    Diabetes          0
    Alcoholism        0
    Handcap           0
    SMS_received      0
    No-show           0
    dtype: int64
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
There\'s no missing Values
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Checking for Duplicated Values[¶](#Checking-for-Duplicated-Values){.anchor-link} {#Checking-for-Duplicated-Values}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[6\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #check if there is a duplicated values with patient id
    df['PatientId'].duplicated().sum()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[6\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    48228
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[7\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #checking if duplicated Patients has change in No-show status
    df.duplicated(['PatientId','No-show']).sum()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[7\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    38710
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
So, here we have **9,518** Patient with Different status
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Get in details with our data[¶](#Get-in-details-with-our-data){.anchor-link} {#Get-in-details-with-our-data}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[8\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    ## using describe method we will get deeply in dataset
    df.describe()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[8\]:
:::

::: {.output_html .rendered_html .output_subarea .output_execute_result}
<div>

          PatientId      AppointmentID   Age             Scholarship     Hipertension    Diabetes        Alcoholism      Handcap         SMS\_received
  ------- -------------- --------------- --------------- --------------- --------------- --------------- --------------- --------------- ---------------
  count   1.105270e+05   1.105270e+05    110527.000000   110527.000000   110527.000000   110527.000000   110527.000000   110527.000000   110527.000000
  mean    1.474963e+14   5.675305e+06    37.088874       0.098266        0.197246        0.071865        0.030400        0.022248        0.321026
  std     2.560949e+14   7.129575e+04    23.110205       0.297675        0.397921        0.258265        0.171686        0.161543        0.466873
  min     3.921784e+04   5.030230e+06    -1.000000       0.000000        0.000000        0.000000        0.000000        0.000000        0.000000
  25%     4.172614e+12   5.640286e+06    18.000000       0.000000        0.000000        0.000000        0.000000        0.000000        0.000000
  50%     3.173184e+13   5.680573e+06    37.000000       0.000000        0.000000        0.000000        0.000000        0.000000        0.000000
  75%     9.439172e+13   5.725524e+06    55.000000       0.000000        0.000000        0.000000        0.000000        0.000000        1.000000
  max     9.999816e+14   5.790484e+06    115.000000      1.000000        1.000000        1.000000        1.000000        4.000000        1.000000

</div>
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
**-First** we find that min age is -1 , so we have to correct this
mistake in our data cleaning section .. our Patients have Age between
**18 and 55 yrs**

**-Second** As we see , there is 75% of our Patient received SMS to Come
Back again
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Data Cleaning[¶](#Data-Cleaning){.anchor-link} {#Data-Cleaning}

> Change data types(if any) of incorrect types
>
> Drop na values(if any) and any duplicated values
>
> Check that columns if written in correct words and rename if there is
> something needs.
>
> Replace age values (-ve or zero) with age average
>
> Drop Columns which is not used in our analysis
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Drop duplicated data for The Same patients and the same No-show Status[¶](#Drop-duplicated-data-for-The-Same-patients-and-the-same-No-show-Status){.anchor-link} {#Drop-duplicated-data-for-The-Same-patients-and-the-same-No-show-Status}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[9\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    df.drop_duplicates(['PatientId','No-show'],inplace=True)
    df.shape
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[9\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    (71817, 14)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Rename Columns to the write Spelling[¶](#Rename-Columns-to-the-write-Spelling){.anchor-link} {#Rename-Columns-to-the-write-Spelling}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[10\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #rename columns with correct names and No-show to No_show
    df.rename(columns = {'Handcap': 'Handicap',
                         'Hipertension': 'Hypertension','No-show':'No_show'}, inplace = True)
    #show data rows to confirm that columns names changed
    df.head(1)
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[10\]:
:::

::: {.output_html .rendered_html .output_subarea .output_execute_result}
<div>

      PatientId      AppointmentID   Gender   ScheduledDay           AppointmentDay         Age   Neighbourhood     Scholarship   Hypertension   Diabetes   Alcoholism   Handicap   SMS\_received   No\_show
  --- -------------- --------------- -------- ---------------------- ---------------------- ----- ----------------- ------------- -------------- ---------- ------------ ---------- --------------- ----------
  0   2.987250e+13   5642903         F        2016-04-29T18:38:08Z   2016-04-29T00:00:00Z   62    JARDIM DA PENHA   0             1              0          0            0          0               No

</div>
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Replace Age Data (-ve or Zero)[¶](#Replace-Age-Data-(-ve-or-Zero)){.anchor-link} {#Replace-Age-Data-(-ve-or-Zero)}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[11\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #check if there is age in -ve or zero 
    df[df['Age'] <= 0].head()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[11\]:
:::

::: {.output_html .rendered_html .output_subarea .output_execute_result}
<div>

       PatientId      AppointmentID   Gender   ScheduledDay           AppointmentDay         Age   Neighbourhood       Scholarship   Hypertension   Diabetes   Alcoholism   Handicap   SMS\_received   No\_show
  ---- -------------- --------------- -------- ---------------------- ---------------------- ----- ------------------- ------------- -------------- ---------- ------------ ---------- --------------- ----------
  59   7.184428e+13   5638545         F        2016-04-29T08:08:43Z   2016-04-29T00:00:00Z   0     CONQUISTA           0             0              0          0            0          0               No
  63   2.366233e+14   5628286         M        2016-04-27T10:46:12Z   2016-04-29T00:00:00Z   0     SÃO BENEDITO        0             0              0          0            0          0               No
  64   1.885174e+14   5616082         M        2016-04-25T13:28:21Z   2016-04-29T00:00:00Z   0     ILHA DAS CAIEIRAS   0             0              0          0            0          1               No
  65   2.718818e+14   5628321         M        2016-04-27T10:48:50Z   2016-04-29T00:00:00Z   0     CONQUISTA           0             0              0          0            0          0               No
  67   8.647128e+13   5639264         F        2016-04-29T08:53:02Z   2016-04-29T00:00:00Z   0     NOVA PALESTINA      0             0              0          0            0          0               No

</div>
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[12\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #calculate age average
    av_age = df['Age'].mean()
    av_age
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[12\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    36.526978292047843
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[13\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #replace zero and -1 values and replace them with average
    df.replace({'Age': {0: av_age}},inplace=True)
    df.replace({'Age': {-1: av_age}},inplace=True)

    #check if there is 0 age again 
    df[df['Age'] <= 0]
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[13\]:
:::

::: {.output_html .rendered_html .output_subarea .output_execute_result}
<div>

     PatientId   AppointmentID   Gender   ScheduledDay   AppointmentDay   Age   Neighbourhood   Scholarship   Hypertension   Diabetes   Alcoholism   Handicap   SMS\_received   No\_show
  -- ----------- --------------- -------- -------------- ---------------- ----- --------------- ------------- -------------- ---------- ------------ ---------- --------------- ----------

</div>
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Removing PatientId , AppointmentID ,ScheduledDay, AppointmentDay Columns[¶](#Removing-PatientId-,-AppointmentID-,ScheduledDay,-AppointmentDay-Columns){.anchor-link} {#Removing-PatientId-,-AppointmentID-,ScheduledDay,-AppointmentDay-Columns}

Not Used in Our Analysis
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[14\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #drop PatientId and AppointmentID columns , print some rows 
    df.drop(columns=["PatientId","AppointmentID",
                    "ScheduledDay","AppointmentDay"],axis = 1,inplace=True)
    df.head()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[14\]:
:::

::: {.output_html .rendered_html .output_subarea .output_execute_result}
<div>

      Gender   Age    Neighbourhood       Scholarship   Hypertension   Diabetes   Alcoholism   Handicap   SMS\_received   No\_show
  --- -------- ------ ------------------- ------------- -------------- ---------- ------------ ---------- --------------- ----------
  0   F        62.0   JARDIM DA PENHA     0             1              0          0            0          0               No
  1   M        56.0   JARDIM DA PENHA     0             0              0          0            0          0               No
  2   F        62.0   MATA DA PRAIA       0             0              0          0            0          0               No
  3   F        8.0    PONTAL DE CAMBURI   0             0              0          0            0          0               No
  4   F        56.0   JARDIM DA PENHA     0             1              1          0            0          0               No

</div>
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
Wrangling Data Summary[¶](#Wrangling-Data-Summary){.anchor-link} {#Wrangling-Data-Summary}
----------------------------------------------------------------
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
we gathered our data from a CSV file , we make it clean and ready for
Exploratory Data Analysis as follows:

> Drop duplicated values with Patient ID with the same No-Show status.
>
> renamed columns with the right syntax.
>
> Replaced age values (-ve or zero) with age average.
>
> Drop Columns which is not used in our analysis
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
[]{#eda}

Exploratory Data Analysis[¶](#Exploratory-Data-Analysis){.anchor-link} {#Exploratory-Data-Analysis}
----------------------------------------------------------------------

Here our data is ready for exploartory with some visualizations.

### OverAll Visualization for our Data[¶](#OverAll-Visualization-for-our-Data){.anchor-link} {#OverAll-Visualization-for-our-Data}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[15\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    #using hist function , let's visual our data brefily
    df.hist(figsize=(15,8));
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt}
:::

::: {.output_png .output_subarea}
![](data:image/png;base64,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%0A)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[16\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    show = df.query("No_show == 'No'")
    not_show = df.query("No_show == 'Yes'")

    show['No_show'].count() , not_show['No_show'].count()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[16\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    (54154, 17663)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[17\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    show.mean() , not_show.mean()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[17\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    (Age             38.462142
     Scholarship      0.091332
     Hypertension     0.202940
     Diabetes         0.072866
     Alcoholism       0.023599
     Handicap         0.020903
     SMS_received     0.297226
     dtype: float64, Age             35.561227
     Scholarship      0.108419
     Hypertension     0.170922
     Diabetes         0.065108
     Alcoholism       0.029440
     Handicap         0.017777
     SMS_received     0.453094
     dtype: float64)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Research Question 1 (Dose The Age affect the attendance ?)[¶](#Research-Question-1--(Dose-The-Age-affect-the-attendance-?)){.anchor-link} {#Research-Question-1--(Dose-The-Age-affect-the-attendance-?)}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[18\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    def attendance(col_name ,x_label ,y_label):
        plt.figure(figsize=[11,6])
        show[col_name].hist(bins=10, color='paleturquoise', label='Show Patients')
        not_show[col_name].hist(bins=10, color='teal', label = 'No Show Patients')
        plt.legend();
        plt.title('Age Attendance',fontsize=18)
        plt.xlabel(x_label,fontsize=18)
        plt.ylabel(y_label,fontsize=18);
    attendance('Age','Age','Number of Patients')
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt}
:::

::: {.output_png .output_subarea}
![](data:image/png;base64,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Vb7/lClTWLRo0Spf30jOgZUkST3K9QsWdGl7hwwY0O75P/zhD/z85z9n+vTprLfeerz44ou8/vrrXRpDW971rncxc+ZMlixZwt57783111/PoYceWrXusgT2lFNOAWDzzTfnmmuuWeV7T5kyhaOPPpoNNthgldtoFEdgJUnSWu3ZZ59l4MCBrLfeegAMHDiQzTfffPn5Cy+8kDFjxjBy5EgefvhhAF566SUOOeQQRo0axS677MJ9990HwMiRI3n55ZfJTDbZZBMuv/xyAI455hh+85vftBlDnz592G233Zg9ezYLFy5kn332WX7PG264AYBzzjmHxx9/nNGjR/OZz3yGuXPnMmLECACWLl3KZz7zGXbccUdGjRrFd7/7XeAfO14ddthhbL311hx11FFkJhdccAHPPPMMe+21F3vttRdLly7l+OOPZ8SIEYwcOZLJkyd38U+5a5nASpKktdp+++3HU089xVZbbcUpp5zCb3/72xXODxw4kOnTp/OJT3yCSZMmAXDeeeexww47cN999/HVr36VY489FoDdd9+d3/3udzz44IMMHz6cO+64A4C77rqLXXbZpc0YFi1axC233MLIkSPp27cv1113HdOnT+e2227j7LPPJjP52te+tnzE9hvf+MYK11966aW89a1v5Z577uGee+7hf/7nf3jiiScAmDFjBlOmTOGhhx5izpw5/O53v+P0009n880357bbbuO2225j5syZPP300zzwwAPcf//9nHDCCV32860HE1hJkrRW23DDDZk2bRqXXHIJm266KUcccQQ/+MEPlp9f9if997znPcydOxeAO++8k2OOOQaAvffem/nz5/PKK68wbtw4br/9dm6//XY+8YlPcP/99/P000+z8cYbs+GGG65072Ujqrvvvjsf+MAHOOCAA8hMPv/5zzNq1Cj23Xdfnn76aZ577rl238P//d//cfnllzN69Gh23nln5s+fz2OPPQbATjvtxJAhQ+jVqxejR49e/h4qDR8+nDlz5nDaaadx00030b9//1X4SXYf58BKkqS1Xu/evRk/fjzjx49n5MiRTJ06leOPPx5g+dSC3r17s2TJEqBY17S1iGDPPffkoosu4sknn+T888/nuuuu45prrmHcuHFV77tsRLXSlVdeyQsvvMC0adNYZ511GDp0aIfLT2UmF154IRMmTFihvKWlZXn8rd9DpQEDBvCnP/2JX//611x00UVcffXVXHbZZe3es5FMYKW1XFc/LLGCpUvr234HOnpwQ5IAHnnkEXr16sWWW24JwMyZM3nnO9/Z7jV77rknV155JV/4whdoaWlh4MCB9O/fn/79+y9/CGz48OHsscceTJo0iW9961udjueVV17hbW97G+ussw633XYbf/7znwHo168fr776atVrJkyYwMUXX8zee+/NOuusw6OPPsrgwYPbvc+y9gYOHMiLL77Iuuuuy4c//GHe9a53LU/eeyoT2G7QyH/Au4NJgiSpmS1cuJDTTjuNl19+mT59+rDFFltwySWXtHvNxIkTOeGEExg1ahQbbLABU6dOXX5u5513ZunSpQCMGzeOc889lz322KPT8Rx11FEcdNBBjB07ltGjR7P11lsDsMkmm7D77rszYsQIDjjgAE499dTl13zsYx9j7ty5jBkzhsxk00035frrr2/3PieddBIHHHAAm222GVOmTOGEE05YvozXf/zHf3Q63kaIakPga7qxY8fmvffeW5e2lz3tV8kEtvtV6wdVV9ffz+nTYcyY+rXfgZ74u9kIfh56BvuhbbNmzWKbbbbplnu5lWxjLevrys9DREzLzLG1tONDXJIkSWoqJrCSJElqKiawkiRJaiomsJIkSWoqJrCSJElqKiawkiRJaiomsJIkaa0XEZx99tnLjydNmsTEiRM7ff1zzz3HgQceyPbbb8+2227L+9//fqBYPu3AAw/s6nCXmzhxIoMHD2b06NGMGDGCG2+8sd36LS0t/P73v19+/J3vfIfLL798le49d+5cfvjDH67StavLjQwkSVKPEl/6Upe2l+ed12Gd9dZbj2uvvZZzzz2XgQMH1nyPL37xi7zvfe/jjDPOAOC+++6ruY1VddZZZ/HpT3+aWbNmMW7cOJ5//nl69ao+RtnS0sKGG27IbrvtBsDJJ5+8yvddlsB+5CMfWeU2VpUjsJIkaa3Xp08fTjrpJCZPnrzSuT//+c/ss88+jBo1in322Ycnn3xypTrPPvssQ4YMWX48atSo5d8vXLiQww47jK233pqjjjqKZZtI3XLLLeywww6MHDmSj370o7z22mv88Y9/5NBDDwXghhtuYP311+f1119n8eLFDB8+vN33sM0229CnTx9efPFFfvazn7Hzzjuzww47sO+++/Lcc88xd+5cvvOd7zB58mRGjx7NHXfcwcSJE5k0aRIAjz/+OPvvvz/vec97GDduHA8//DAAxx9/PKeffjq77bYbw4cP55prrgHgnHPO4Y477mD06NFMnjyZBx98kJ122onRo0czatQoHnvssVq6oCYmsJIkScCpp57KlVdeySuvvLJC+Sc/+UmOPfZY7rvvPo466ihOP/30qteeeOKJ7LXXXpx//vk888wzy8/NmDGDKVOm8NBDDzFnzhx+97vfsXjxYo4//niuuuoq7r//fpYsWcLFF1/MmDFjmDFjBgB33HEHI0aM4J577uHuu+9m5513bjf+u+++m169erHpppuyxx57cNdddzFjxgyOPPJI/vM//5OhQ4dy8sknc9ZZZzFz5kzGjRu3wvUnnXQSF154IdOmTWPSpEmccsopy889++yz3Hnnnfz85z/nnHPOAeBrX/sa48aNY+bMmZx11ll85zvf4YwzzmDmzJnce++9KyT0Xc0pBJIkSUD//v059thjueCCC1h//fWXl//hD3/g2muvBeCYY47hs5/97ErXTpgwgTlz5nDTTTfxq1/9ih122IEHHngAgJ122ml5Mjd69Gjmzp1Lv379GDZsGFtttRUAxx13HBdddBFnnnkmW2yxBbNmzeKPf/wjn/rUp7j99ttZunTpSgnnMpMnT+Z///d/6devH1dddRURwbx58zjiiCN49tlnef311xk2bFi7733hwoX8/ve/5/DDD19e9tprry3//pBDDqFXr15su+22PPfcc1Xb2HXXXTn//POZN28ehx56KFtuuWW791wdjsBKkiSVzjzzTC699FL+9re/tVknIqqWb7zxxnzkIx/hiiuuYMcdd+T2228Hivm1y/Tu3ZslS5Ysn0ZQzbhx4/jVr37FOuusw7777sudd97JnXfeyZ577lm1/rIR1TvuuGN5knvaaafxyU9+kvvvv5/vfve7LF68uN33/eabb7LRRhsxc+bM5a9Zs2YtP1/5HtqK/SMf+Qg33ngj66+/PhMmTODWW29t956rwwRWkiSptPHGG/PP//zPXHrppcvLdtttN3784x8DcOWVV7LHHnusdN2tt97KokWLAHj11Vd5/PHHecc73tHmfbbeemvmzp3L7NmzAbjiiit473vfC8Cee+7JlClT2HXXXdl0002ZP38+Dz/8MNttt12n38crr7zC4MGDAZg6dery8n79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%0A)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
**Here** We see that age affect the Attendance as data is skweed to the
right

where age is **between 1 and 5** is the highest number of show pateint
so , parents are care about there kids
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Research Question 2 (Does Age and Diseases factor affect the attendance!)[¶](#Research-Question-2--(Does-Age-and-Diseases-factor-affect-the-attendance!)){.anchor-link} {#Research-Question-2--(Does-Age-and-Diseases-factor-affect-the-attendance!)}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[19\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    def attendance(col_name ,x_label ,y_label):
        plt.figure(figsize=[14,6])
        show.groupby(['Hypertension','Diabetes']).mean()[col_name].plot(kind='bar', color='rosybrown',label='Show Patients')
        not_show.groupby(['Hypertension','Diabetes']).mean()[col_name].plot(kind='bar', color='maroon', label = 'No Show Patients')
        plt.legend();
        plt.title('Age, Diseases Attendance',fontsize=18)
        plt.xlabel(x_label,fontsize=18)
        plt.ylabel(y_label,fontsize=18);
    attendance('Age','Diseases','Age Average')
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt}
:::

::: {.output_png .output_subarea}
![](data:image/png;base64,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U6asrL/pe2hs880357777uO3v/0tF198MT/72c/44Q9/2OIxJUmSpHoyIHWQRx55hG7durHDDjsAMHPmTN7ylre0uM0BBxzAlVdeyec+9zmmTJlC37596dOnD3369Fk5ycOgQYPYf//9ueiii/j2t7/d6nqeffZZttpqK3r06MHkyZN5/PHHAejduzfPPfdcs9uMHj2a73znOxx00EH06NGDP//5z2y77bYtHqdhf3379mXJkiVsuOGG/Pu//zvbb7/9ynAoSZJUi/aebEu1W9MEZesTA1IHef755znrrLNYtmwZ3bt3561vfSuXXnppi9uMGzeO0047jaFDh7LxxhszadKklev22msvVqxYAcCIESP49Kc/zf7779/qek444QSOOuoohg8fzrBhw9hxxx0B2HLLLdlvv/0YPHgwhx9+OB/5yEdWbvPBD36QefPmsfvuu5OZ9OvXj1/84hctHmfMmDEcfvjhbL311kyYMIHTTjtt5TTj//3f/93qeiVJkqR6iOaGda1rhg8fntOmTXvNstmzZ7PTTjvVqSJ1Jr9rSZLWb/Yg1d/60IMUEdMzc/ia2jlJgyRJkiQVBiRJkiRJKrwGSZIkSWu1qeecU+8Surz1YYhda9mDJEmSJEmFAUmSJEmSCgOSJEmSJBUGpA4UEZx77rkrX1900UWMGzeu1dsvWrSII488kl133ZWdd96Zd73rXQBMmTKFI488sr3LXWncuHFsu+22DBs2jMGDB3PDDTe02H7KlCn86U9/Wvn6u9/9Lpdffnmbjj1v3jx+8pOftGlbSZIk6fXqMpM0nB/Rrvv7QivuH7XRRhtx7bXX8ulPf5q+ffvWfIzPf/7zHHLIIXzsYx8D4P777695H211zjnn8IlPfILZs2czYsQInnrqKbp1az5PT5kyhU022YR9990XgDPOOKPNx20ISMcff3yb9yFJkiS1lT1IHah79+6MGTOG8ePHr7Lu8ccfZ9SoUQwdOpRRo0bxxBNPrNJm4cKF9O/ff+XroUOHrvz5+eef59hjj2XHHXfkhBNOoOGGvzfffDO77bYbQ4YM4QMf+AAvvvgid999N8cccwwA119/Pb169eKll15i+fLlDBo0qMX3sNNOO9G9e3eWLFnCjTfeyF577cVuu+3GwQcfzKJFi5g3bx7f/e53GT9+PMOGDeO2225j3LhxXHTRRQA89thjHHbYYbzjHe9gxIgRPPzwwwCceuqpnH322ey7774MGjSIa665BoDzzjuP2267jWHDhjF+/HgefPBB9txzT4YNG8bQoUOZM2dOLV+BJEmSVBMDUgf7yEc+wpVXXsmzzz77muUf/ehHOfnkk7n//vs54YQTOPvss5vd9vTTT+fAAw/kggsuYMGCBSvXzZgxgwkTJvDQQw8xd+5cbr/9dpYvX86pp57K1VdfzaxZs3j55Zf5zne+w+67786MGTMAuO222xg8eDD33HMPd911F3vttVeL9d91111069aNfv36sf/++3PnnXcyY8YM3v/+9/PVr36VAQMGcMYZZ3DOOecwc+ZMRowY8Zrtx4wZw7e+9S2mT5/ORRddxIc//OGV6xYuXMjUqVP55S9/yXnnnQfAhRdeyIgRI5g5cybnnHMO3/3ud/nYxz7GzJkzmTZt2msCoyRJktTeuswQu3rp06cPJ598Mt/85jfp1avXyuV33HEH1157LQAnnXQSn/rUp1bZdvTo0cydO5ff/OY33HTTTey222488MADAOy5554rw8KwYcOYN28evXv3ZuDAgbztbW8D4JRTTuHiiy9m7NixvPWtb2X27NncfffdfPzjH+fWW29lxYoVqwSaBuPHj+fHP/4xvXv35uqrryYimD9/Pu973/tYuHAhL730EgMHDmzxvT///PP86U9/4rjjjlu57MUXX1z589FHH023bt3YeeedWbRoUbP72GeffbjggguYP38+xxxzDDvssEOLx5QkSZJeD3uQOsHYsWOZOHEi//jHP1bbJlZzjdQWW2zB8ccfzxVXXMEee+zBrbfeClTXNzXYYIMNePnll1cOs2vOiBEjuOmmm+jRowcHH3wwU6dOZerUqRxwwAHNtm/oEbrttttWhqizzjqLj370o8yaNYvvfe97LF++vMX3/corr7DZZpsxc+bMlY/Zs2evXN/4Payu9uOPP54bbriBXr16MXr0aG655ZYWjylJkiS9HnUNSBGxWURcExEPR8TsiNgnIraIiN9HxJzyvHk9a2wPW2yxBe9973uZOHHiymX77rsvV111FQBXXnkl+++//yrb3XLLLbzwwgsAPPfcczz22GNst912qz3OjjvuyLx583j00UcBuOKKK3jnO98JwAEHHMCECRPYZ5996NevH0uXLuXhhx9ml112afX7ePbZZ9l2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%0A)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
Here we Show that diseases doesn\'t affect attendance even if with
old-aged cases
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Research Question 3 (Which gender have more no-show?)[¶](#Research-Question-3--(Which-gender-have-more-no-show?)){.anchor-link} {#Research-Question-3--(Which-gender-have-more-no-show?)}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[20\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    def attendance(col_name ,x_label ,y_label):
        plt.figure(figsize=[10,10])
        show[col_name].value_counts().plot(kind='pie',label='Show Patients')
        plt.legend();
        plt.title('Comparisson Between Gender in Attendance',fontsize=18)
        plt.xlabel(x_label,fontsize=18)
        plt.ylabel(y_label,fontsize=18);
    attendance('Gender','Gender','Number of Patients')
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt}
:::

::: {.output_png .output_subarea}
![](data:image/png;base64,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J//cCV94eifyvDz+XX/pPst9f3+vI/hpT/6Kf23tfS6OA7YoWW+peL1CvN5HcabfAmOqeW7oUt1F5/6TmjF/kt5/4IvL+LBpREREhpf2qRIRERGpAZUqERERkRpQqRIRERGpAe1TJSIiIlIDGqkSERERqQGVKhEREZEaUKkSERERqQGVKhEREZEaUKkSERERqQGd+09ERETq5pFHHlmkra3tfPwpnxp5MKcHeHrmzJn7rr322h8M5gZUqkRERKRu2trazl9sscVWHj169MctLS0NO49TT0+PTZgwYZX33nvvfOA7g7mNRm6MIiIiknyrjR49+tNGLlQALS0tbvTo0d34EbXB3UYN84iIiIiUamn0QtUrzjnobqRSJSIiIlID2qdKREREhk0mF61dy9sr5LOPDLROa2vr2ssvv/zU3q+vu+66l1dcccXptcwBKlUiIiKScp2dnT3PP//8s/W+H23+ExEREakBjVSJiIhIqk2bNq1lpZVWWgVgzJgx02699dZX6nE/KlUiIiKSatr8JyIiIpIgKlUiIiIiNaDNfyIiIjJsKpkCIak0UiUiIiKpNmXKlMeG435UqkRERERqQKVKREREpAZUqkRERERqQKVKREREpAZUqkRERERqQKVKREREpAY0T5WIiIgMn6751q7t7XUPOO+Vma294447Trz22mtfA5gxYwaLLLLI19Zcc83J//vf/16uVRSNVImIiEiqjRw5sueFF14Y+dlnnxnANddcM++iiy46o9b3o1IlIiIiqbfFFlt0X3XVVfMDXHbZZQvusssuE2t9HypVIiIiknp77LHHxCuuuGKBKVOm2HPPPTfXBhtsMLnW96FSJSIiIqm3/vrrT33rrbc6zzvvvAW33HLL7nrch0qViIiINIVtttnmk+OOO27MnnvuWfNNf6Cj/0RERKRJHHDAAR/ON998s9Zbb72pN9544zy1vn2VKhERERk+FUyBUC/LLrvsjGOOOeaDet2+Nv+JiIhIqk2ZMuWx0mXbb7/9pFrOUQUqVSIiIiI1oVIlIiIiUgMqVSIiIlJPPT09PRY6RCXinD2D/X6VKhEREamnpydMmDBfoxernp4emzBhwnzA04O9DR39JyIiInUzc+bMfd97773z33vvvdVo7MGcHuDpmTNn7jvYGzDnXA3ziIiIiDSnRm6MIiIiIomhUiUiIiJSAypV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%0A)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[21\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    show['Gender'].value_counts()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[21\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    F    34961
    M    19193
    Name: Gender, dtype: int64
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
As We See here **Females** are more attendance than **Males**

**- Females Attendance %:** 34961 Patient From Total with precentage
**65%**

**- Males Attendance %:** 19193 Patient From Total with precentage
**35%**
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Research Question 4 (Does Sending SMS affect attendance?)[¶](#Research-Question-4--(Does-Sending-SMS-affect-attendance?)){.anchor-link} {#Research-Question-4--(Does-Sending-SMS-affect-attendance?)}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[22\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    plt.figure(figsize=[12,4])
    show.query('SMS_received >= 0')['SMS_received'].plot(kind='hist', color='lightgray',label='Show Patients')
    not_show.query('SMS_received >= 0')['SMS_received'].plot(kind='hist', color='salmon', label = 'No Show Patients')
    plt.legend();
    plt.title('Attendance According to Sent SMS',fontsize=18)
    plt.xlabel('SMS Received',fontsize=18)
    plt.ylabel('Number of Patients',fontsize=18);
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt}
:::

::: {.output_png .output_subarea}
![](data:image/png;base64,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DLuZmZk1h48//pjq6moWLVrU0qFYE+rQoQNdu3alffv2nymXNCkiqsrZRmvsYTczMzNb5VVXV9OxY0e6detGmqnaVjURwbx586iurqZ79+4rvJ3WcOMkMzMzs9XOokWL6Ny5s5P1VZgkOnfu3OBfUZywm5mZmbUQJ+urvsY4x07YzczMzMxaMY9hNzMzM2sFpk6d2qjb69WrV71tLrjgAm6++Wbatm1LmzZtuPrqq+nbty/dunVj4sSJbLjhho0aE8CsWbPYZptt+NKXvsTixYvZc889ueKKK2jTpnQ/8oIFC7j55ps59dRTAXjzzTc544wzuP3221do/5dccglDhw5l7bXXXuFjaG5O2FuJxv4jXRmU8w+JmZmZNY0nnniCu+66i2eeeYY111yTuXPnsnjx4mbZ9xe/+EUmT57MkiVL2GefffjrX//KIYccUrLtggULuOKKK5Yl7JtssskKJ+uQEvZjjjlmpUrYPSTGzMzMbDU0e/ZsNtxwQ9Zcc00ANtxwQzbZZJNl9Zdddhk77bQT22+/PS+++CIA8+fP5+CDD6Z3797069ePKVOmALD99tuzYMECIoLOnTtzww03AHDsscdy//331xpDu3bt2G233ZgxYwYLFy5k3333XbbPMWPSvTPPOeccXnnlFfr06cPZZ5/NrFmzlnX6LV26lLPPPptddtmF3r17c/XVVwMwfvx49tprLw499FC23nprjj76aCKCSy+9lDfffJO9996bvffem6VLlzJ48GB69erF9ttvz8iRIxv5XW4cTtjNzMzMVkP7778/r7/+OltttRWnnnoqDz300GfqN9xwQ5555hlOOeUURowYAcC5557LjjvuyJQpU7jwwgs57rjjANh999157LHHmDZtGj169OCRRx4B4Mknn6Rfv361xvDhhx/ywAMPsP3229OhQwfuvPNOnnnmGcaNG8dZZ51FRHDRRRct65H/zW9+85n1r732Wj73uc8xYcIEJkyYwO9//3teffVVAJ599lkuueQSXnjhBWbOnMljjz3GGWecwSabbMK4ceMYN24ckydP5o033mDq1Kk8//zznHDCCY32/jYmJ+xmZmZmq6F1112XSZMmcc0119ClSxcOP/xwrr/++mX1NUNUdt55Z2bNmgXAo48+yrHHHgvAPvvsw7x583j33Xfp378/Dz/8MA8//DCnnHIKzz//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%0A)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
#### Here We can see that Sending SMS doesn\'t make patients come again , so it\'s not the correct action here to increase number of send messages or call them again.[¶](#Here-We-can-see-that-Sending-SMS-doesn't-make-patients-come-again-,-so-it's-not-the-correct-action-here-to-increase-number-of-send-messages-or-call-them-again.){.anchor-link} {#Here-We-can-see-that-Sending-SMS-doesn't-make-patients-come-again-,-so-it's-not-the-correct-action-here-to-increase-number-of-send-messages-or-call-them-again.}
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Research Question 5 (Does Neighbourhood affect attendance?)[¶](#Research-Question-5--(Does-Neighbourhood-affect-attendance?)){.anchor-link} {#Research-Question-5--(Does-Neighbourhood-affect-attendance?)}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[23\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    def attendance(col_name,x_label,y_label):
        plt.figure(figsize=[20,7])
        show[col_name].value_counts().plot(kind='bar', color='rosybrown',label='Show Patients')
        not_show[col_name].value_counts().plot(kind='bar', color='maroon', label = 'No Show Patients')
        plt.legend();
        plt.title('Attendance According to Neighbourhood',fontsize=18)
        plt.xlabel(x_label,fontsize=18)
        plt.ylabel(y_label,fontsize=18);
    attendance('Neighbourhood','Neighbourhood','Number of Patients')
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt}
:::

::: {.output_png .output_subarea}
![](data:image/png;base64,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d96i3y+//DIHHHBAu/c/btw43nvvvXav3xmcQ0qSJEmSJHWI28eNq+v2ho0cWbH+b3/7GzfeeCOPPPIIK6ywAnPmzOGDDz6oawzlrLfeekyePJn58+ezyy67cN1117H//vuXbNuWkDr++OMBWGuttbj66qvbve9x48bxla98hZVWWqnd22g0e0hJkiRJkqSmMGvWLHr37s0KK6wAQO/evVlrrbUW1Z9zzjlsscUWDBo0iKeffhqA1157jf3224+Wlha22WYbpkyZAsCgQYN44403SCnRq1cvLr30UgAOO+wwbrvttrIxdOvWje22245p06bxzjvvMGzYsEX7vP766wE4/fTTee6552htbeVb3/oWM2bMYODAgQAsWLCAb33rW2y11Va0tLTwq1/9CoCJEyey0047ccABB7DRRhtx6KGHklLi7LPP5uWXX2bnnXdm5513ZsGCBYwYMYKBAwcyaNAgxo4dW+ezXB8mpCRJkiRJUlPYfffdefHFF9lwww05/vjjueuuuz5S37t3bx555BGOO+44xowZA8BZZ53F5ptvzpQpU/jRj37E4YcfDsD222/Pfffdx5NPPsmAAQO45557ALj//vvZZpttysbw3nvvcfvttzNo0CB69OjBtddeyyOPPMKdd97JaaedRkqJn/zkJ4t6VP3sZz/7yPrjx4/nk5/8JA899BAPPfQQv/71r3n++ecBePTRRxk3bhxPPfUU06dP57777uPkk09mrbXW4s477+TOO+9k8uTJvPTSSzzxxBM8/vjjHHnkkXU7v/VkQkqSJEmSJDWFVVZZhYcffpgLL7yQPn36cNBBB3HJJZcsqm8bQrflllsyY8YMAO69914OO+wwAHbZZRfmzp3Lm2++ydChQ7n77ru5++67Oe6443j88cd56aWXWGONNVhllVUW23dbj6ftt9+eL3zhC+y5556klDjzzDNpaWlh11135aWXXuKVV16peAx/+ctfuPTSS2ltbWXIkCHMnTuXZ599FoCtt96avn370qVLF1pbWxcdQ6EBAwYwffp0TjrpJG6++WZWXXXVdpzJjuccUpIkSZIkqWl07dqVnXbaiZ122olBgwYxYcIERowYAbBoKF/Xrl2ZP38+ACmlxbYREey4446ce+65vPDCC4wePZprr72Wq6++mqFDh5bcb1uPp0KXX345s2fP5uGHH6Z79+7069ePefPmVYw/pcQ555zD8OHDP1I+ceLERfEXH0Oh1Vdfnccee4xbbrmFc889l6uuuoqLLrqo4j47gz2kJEmSJElSU3jmmWcW9SYCmDx5Muuuu27FdXbccUcuv/xyIEv69O7dm1VXXZV11lmHOXPm8OyzzzJgwAB22GEHxowZUzYhVcqbb77Jpz71Kbp3786dd97JP/7xDwB69uzJ22+/XXKd4cOHc/755/Phhx8C8Pe//51333234n4KtzdnzhwWLlzIl770JX7wgx/wyCOPVB1vI9lDSpIkSZIkNYV33nmHk046iTfeeINu3bqx/vrrc+GFF1ZcZ9SoURx55JG0tLSw0korMWHChEV1Q4YMYcGCBQAMHTqUM844gx122KHqeA499FD23ntvBg8eTGtrKxtttBEAvXr1Yvvtt2fgwIHsueeenHDCCYvWOfroo5kxYwZbbLEFKSX69OnDddddV3E/xxxzDHvuuSdrrrkm48aN48gjj2ThwoUA/PjHP6463kaKUl3Tmt3gwYPTpEmTOjsMSZIkSZKaytSpU9l44407Oww1QKlrHREPp5QGV7O+PaSA28eNK1s3bOTIBkYiSZIkSZLU/JxDSpIkSZIkSQ1lQkqSJEmSJEkNZUJKkiRJkiRJDWVCSpIkSZIkSQ1lQkqSJEmSJEkNZUJKkiRJkiQ1jYjgtNNOW/R7zJgxjBo1qur1X3nlFfbaay8222wzNtlkEz7/+c8DMHHiRPbaa696h7vIqFGjWHvttWltbWXgwIHccMMNFdtPnDiRv/71r4t+X3DBBVx66aXt2veMGTP43e9+165126tbQ/cmSZIkSZKWG9+LqOv2zkppiW1WWGEFrrnmGs444wx69+5d8z6++93vsttuu3HKKacAMGXKlJq30V6nnnoq3/zmN5k6dSpDhw7l1VdfpUuX0n2JJk6cyCqrrMJ2220HwLHHHtvu/bYlpA455JB2b6NW9pCSJEmSJElNo1u3bhxzzDGMHTt2sbp//OMfDBs2jJaWFoYNG8YLL7ywWJtZs2bRt2/fRb9bWloWfX/nnXc44IAD2GijjTj00ENJeYLs9ttvZ/PNN2fQoEF89atf5f333+fBBx9k//33B+D6669nxRVX5IMPPmDevHkMGDCg4jFsvPHGdOvWjTlz5vDHP/6RIUOGsPnmm7PrrrvyyiuvMGPGDC644ALGjh1La2sr99xzD6NGjWLMmDEAPPfcc+yxxx5sueWWDB06lKeffhqAESNGcPLJJ7PddtsxYMAArr76agBOP/107rnnHlpbWxk7dixPPvkkW2+9Na2trbS0tPDss8/WcgmqYkJKkiRJkiQ1lRNOOIHLL7+cN9988yPlJ554IocffjhTpkzh0EMP5eSTTy657lFHHcXOO+/M6NGjefnllxfVPfroo4wbN46nnnqK6dOnc9999zFv3jxGjBjBlVdeyeOPP878+fM5//zz2WKLLXj00UcBuOeeexg4cCAPPfQQDzzwAEOGDKkY/wMPPECXLl3o06cPO+ywA/fffz+PPvooBx98MD/96U/p168fxx57LKeeeiqTJ09m6NChH1n/mGOO4ZxzzuHhhx9mzJgxHH/88YvqZs2axb333suNN97I6aefDsBPfvIThg4dyuTJkzn11FO54IILOOWUU5g8eTKTJk36SIKuXhyyJ0mSJEmSmsqqq67K4Ycfztlnn82KK664qPxvf/sb11xzDQCHHXYY3/72txdbd/jw4UyfPp2bb76ZP//5z2y++eY88cQTAGy99daLkjOtra3MmDGDnj170r9/fzbccEMAjjjiCM4991xGjhzJ+uuvz9SpU3nwwQf5xje+wd13382CBQsWSyC1GTt2LL/97W/p2bMnV155JRHBzJkzOeigg5g1axYffPAB/fv3r3js77zzDn/961858MADF5W9//77i77vt99+dOnShU022YRXXnml5Da23XZbRo8ezcyZM9l///3ZYIMNKu6zPewhJUmSJEmSms7IkSMZP3487777btk2UWaOqzXWWINDDjmEyy67jK222oq7774byOanatO1a1fmz5+/aNheKUOHDuXPf/4z3bt3Z9ddd+Xee+/l3nvvZccddyzZvq3H0z333LMoaXXSSSdx4okn8vjjj/OrX/2KefPmVTzuhQsXstpqqzF58uRFy9SpUxfVFx5DudgPOeQQbrjhBlZccUWGDx/OHXfcUXGf7WFCSpIkSZIkNZ011liDL3/5y4wfP35R2XbbbccVV1wBwOWXX84OO+yw2Hp33HEH7733HgBvv/02zz33HJ/5zGfK7mejjTZixowZTJs2DYDLLruMz33ucwDsuOOOjBs3jm233ZY+ffowd+5cnn76aTbddNOqj+PNN99k7bXXBmDChAmLynv2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iIjpJml14DVAq17UMuAY23c1MZ5VmzhoRERERERERETUx/ZfJJ0F3AgY+FVTwShIhlRERERERERExFSTtA7wZeBplAYEqwBbUKbvvcH2rbWPKQGpiIiIiIiIiIjpJelrwDXAgbbvrZYJ+CCwie29ax9TAlIREREREREREdNL0m9tP26u60ZplboPGBERERERERERtVLTA+iUgFRERERERERExHQ7R9I/VtP0lpP0QeC8JgaUKXsREREREREREVOsKmr+FWArSlFzA1sCF1OKmv+p9jElIBURERERERERMf0kbQw8iTKFb5nt3zU2lgSkIiIiIiIiIiKiTqkhFRERERERERERtUpAKiIiIiIiIiIiarVq0wOIiIiIiIiIiIjRkfQ3wN22764ePx7YAbjW9olNjCkZUhERERERERER0+1UYCMASZsAPwMWAUslfayJAaWoeURERERERETEFJN0me2nVF9/GFjX9lJJ9wcuaq2rUzKkIiIiIiIiIiKmW3s20hLgdADb/w+4t4kBpYZURERERERERMR0u1TSocAfgE2A0wAkPaipASVDKiIiIiIiIiJiur0JuIlSR+rFtu+olj8JOLSJASVDKiIiIiIiIiJiitm+Ezi4y6rrgMU1DwdIhlRERERERERExIIh6aGS/l7ST4GzgPWbGEcypCIiIiIiIiIippiktYGdgdcAmwInAYtsb9DYmGzPvFVEREREREREREwkSXcCFwAfAM62bUlX2V7U1JgyZS8iIiIiIiIiYrodAKwBfBF4n6SNGx5PMqQiIiIiIiIiIhYCSYuAPYDdgccBHwJOsn1F7WNJQCoiIiIiIiIiYmGR9BRKTandbNeeMZWAVERERERERERE1Cpd9iIiIiIiIiIippik24BuGUkCbHudmoeUDKmIiIiIiIiIiIVC0sW2t2x6HOmyFxERERERERGxcIxFZlICUhERERERERERUavUkIqIiIiIiIiImGKSdml7+KCOx9g+seYhpYZURERERERERMQ0k/TVPqtt+/W1DaaSgFRERERERERExAIlaVfbJ9R+3ASkIiIiIiIiIiIWJkm/t71h3cdNUfOIiIiIiIiIiIVLTRw0AamIiIiIiIiIiIWrkalz6bIXERERERERETHFJF1G98CTgPVrHk45cGpIRURERERERERML0mP6bfe9rV1jaUlAamIiIiI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%0A)
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
### Research Question 6 (Does Scholarship affect attendance?)[¶](#Research-Question-6--(Does-Scholarship-affect-attendance?)){.anchor-link} {#Research-Question-6--(Does-Scholarship-affect-attendance?)}
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[24\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    scholar_ship = df.query('Scholarship == 1')
    scholar_ship['No_show'].value_counts()
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[24\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    No     4946
    Yes    1915
    Name: No_show, dtype: int64
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[25\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    total = 4946 + 1915
    scholarship_show = 4946 / total
    scholarship_not_show = 1915 / total
    print(scholarship_show , scholarship_not_show)
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt}
:::

::: {.output_subarea .output_stream .output_stdout .output_text}
    0.7208861681970559 0.2791138318029442
:::
:::
:::
:::
:::

::: {.cell .border-box-sizing .text_cell .rendered}
::: {.prompt .input_prompt}
:::

::: {.inner_cell}
::: {.text_cell_render .border-box-sizing .rendered_html}
[]{#conclusions}

Conclusions[¶](#Conclusions){.anchor-link} {#Conclusions}
------------------------------------------

Data Wrangling Summary:[¶](#Data-Wrangling-Summary:){.anchor-link} {#Data-Wrangling-Summary:}
------------------------------------------------------------------

we gathered our data from a CSV file , we make it clean and ready for
Exploratory Data Analysis as follows:

> Drop duplicated values with Patient ID with the same No-Show status.
>
> renamed columns with the right syntax.
>
> Replaced age values (-ve or zero) with age average.
>
> Drop Columns which is not used in our analysisas polished as possible.

Findings:[¶](#Findings:){.anchor-link} {#Findings:}
--------------------------------------

> where age is **between 1 and 5** is the highest number of show pateint
> so , parents are care about there kids.
>
> Diseases doesn\'t affect attendance even if with old-aged cases.
>
> As We See here **Females** are more attendance than **Males**.
>
> Sending SMS doesn\'t make patients come again.
>
> Most of people who has Scholarship are most likely to show with
> precentage of 75%

limitations:[¶](#limitations:){.anchor-link} {#limitations:}
--------------------------------------------

Missing features that could be useful to get more sure what is the most
feature that impacts showing to the appointment such as if the patient
is employeed or not , or whether the patient have a series medical issue
or not.

Submitting your Project[¶](#Submitting-your-Project){.anchor-link} {#Submitting-your-Project}
------------------------------------------------------------------
:::
:::
:::

::: {.cell .border-box-sizing .code_cell .rendered}
::: {.input}
::: {.prompt .input_prompt}
In \[26\]:
:::

::: {.inner_cell}
::: {.input_area}
::: {.highlight .hl-ipython3}
    from subprocess import call
    call(['python', '-m', 'nbconvert', 'Investigate_a_Dataset.ipynb'])
:::
:::
:::
:::

::: {.output_wrapper}
::: {.output}
::: {.output_area}
::: {.prompt .output_prompt}
Out\[26\]:
:::

::: {.output_text .output_subarea .output_execute_result}
    0
:::
:::
:::
:::
:::
:::
:::
