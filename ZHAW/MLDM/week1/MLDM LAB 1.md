---
lab:
---

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

"""
Task 2:
Question: Were there more infections following people arriving from risk areas
    (in Zurich)

relevant variables chosen: 
- DATE
- CANTON
- NCUMUL_CONF: Reported number of confirmed cases as of date (per canton)
- CURR_Q_RISKAREATRAVEL: Reported number of quarantined persons on date 
            (because of arriving from riskareas)
NNEW_CONF: New confirmed cases on a date (derived from NCUMUL_CONF)

Conclusion:
There is no obvious connection between people arriving from risk areas and new
infections following their arrival
"""
DATE = 'date'
CANTON = 'abbreviation_canton_and_fl'
ZURICH = 'ZH'
NCUMUL_CONF = 'ncumul_conf'
NNEW_CONF = 'nnew_conf'
CURR_Q_RISKAREATRAVEL = 'current_quarantined_riskareatravel'

covid_data = pd.read_csv('lab01_clean_data.csv')
risk_data = covid_data[[DATE, NCUMUL_CONF, CURR_Q_RISKAREATRAVEL, CANTON]]
risk_data.set_index(DATE, inplace=True)
risk_data.sort_index(ascending=True, inplace=True)

# filter out only data for Zurich
risk_data = risk_data.loc[risk_data[CANTON] == ZURICH]

# create new column that contains delta of confirmed infections
risk_data[NNEW_CONF] = risk_data[NCUMUL_CONF].diff()
# re-insert start value
risk_data[0] = risk_data[NCUMUL_CONF][0]

print(risk_data.describe(include='all'))

sns.lineplot(data=risk_data, x=DATE, y=NNEW_CONF, hue=CURR_Q_RISKAREATRAVEL)

plt.show()
```


![[LAB1_result.png]]