# Decoder Project
---
Provided files with lists of strings, this project aims to make a script that will turn it into a readable csv file with the following header columns:
- ID (Hexadecimal)
- CUSTOMER_NAME (String)
- YEAR_OPENED (Integer: YYYY)
- MONTH_OPENED (String: January-December)
- DATE_OPENED (String: 01-31)
- ITEM_ID (String: XXXX-XX)
- ITEM_CODE (String: XXXX-XXXX-XXXX-XXXX)
- YEAR_CLOSED (Integer: YYYY)
- MONTH_CLOSED (String: January-December)
- DATE_CLOSED (String: 01-31)
- FLAG (Boolean: True/False)

---

The files to be used in this project can be found in ```./decoder_project/src/*```.
These files include:
- ```data_10000.txt``` (10000 lines of data)
- ```data_100000.txt``` (100000 lines of data)
- ```data_750000.txt``` (750000 lines of data)

It should be noted that it is better to use the smaller files first in development before using the largest file to optimise the development time.

---

Sample of data:
> 2202abc_sPc%EPQad_2022622_NSjaSn9jmqEOOX11lqYdAR_2029922

The data is separated by the character "_" (underscore)
From the example above, the division of data is described below:
- __2202abc__ - The ```ID``` in ```hexadecimal``` form
- __sPc%EPQad__ - This string is the ```CUSTOMER_NAME``` encoded. When decoded this is equivalent to ```Dan Pablo```. The way to decode is listed below:
  - For each of the ```character``` in the string, do the conditions below
  - Replace ```%``` into ```" " (space)``` differentiating the first name and the surname
  - Using the ```ID```, get its ```modulus 16 + 1```. Then add it to the index of the character in the string from this key ```abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ```
  - Then switch the case setting of the character ```(lowercase -> uppercase and uppercase -> lowercase)```
- __202262__ - This string holds the following data:
  - _2022_ - Year for ```YEAR_OPENED```
  - _6_ - Month for ```MONTH_OPENED```; Note that for months January-September, only 1 character is used; October-December use 2 characters
  - _2_ - Date for ```DATE_OPENED```; Note that for days 1-9, only 1 characters is used; 10-31 use 2 characters.
- __NSjaSn9jmqEOOX11lqYdAR__ - This string has the following data:
  - _NSjaSn_ - Is the ```ITEM_ID```
  - _9jmqEOOX11lqYdAR_ - Is the ```ITEM_CODE```
- __20291122__ - This string holds the following data:
  - _2029_ - Year for ```YEAR_CLOSED```
  - _11_ - Month for ```MONTH_CLOSED```; Note that for months January-September, only 1 character is used; October-December use 2 characters
  - _22_ - Date for ```DATE_CLOSED```; Note that for days 1-9, only 1 characters is used; 10-31 use 2 characters.
  - For the ```FLAG``` column, simply check if the encoded name and the decoded name are similar (besides the character %)
---
##### Sample
[Example 1]
INPUT: ```2202abc_sPc%EPQad_2022622_NSjaSn9jmqEOOX11lqYdAR_2029922```
<br/>OUTPUT:
| ID | CUSTOMER_NAME | YEAR_OPENED | MONTH_OPENED | DATE_OPENED | ITEM_ID | ITEM_CODE | YEAR_CLOSED | MONTH_CLOSED | DATE_CLOSED | FLAG |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 2202abc | Dan Pablo | 2022 | June | 02 | NSja-Sn | 9jmq-EOOX-11lq-YdAR | 2029 | September | 22 | False |

[Example 2]
INPUT: ```6778799bd_John%Seidel_20021017_5BA5wQrdv4nFMSQ7XmcbRP_2008510```
OUTPUT:
| ID | CUSTOMER_NAME | YEAR_OPENED | MONTH_OPENED | DATE_OPENED | ITEM_ID | ITEM_CODE | YEAR_CLOSED | MONTH_CLOSED | DATE_CLOSED | FLAG |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 6778799bd | John Seidel | 2002 | October | 17 | 5BA5-wQ | rdv4-nFMS-Q7Xm-cbRP | 2008 | May | 10 | True |

---
Save file as .csv files to individual directory
Example:
```./decoder_project/devs/<dev_name>/output_10000.csv```

Check ```./decoder_project/src/sample_output.csv``` for the expected .csv output format
