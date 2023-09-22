
![[Pasted image 20230920193912.png]]

# Supervised
- klassifikation nach manuell bestimmten Label
- model mapped input zu label

# Unsupervised 
- keine Labels, trotzdem "klassifiziert"

Zusammenhänge/Struktur in Daten erkennen


# Reinforcement Learning

![[Pasted image 20230920193548.png]]



# Data

Typen:
- Categorical (is it a cow?)
	- Nominal(no ordering/quantification): gender, hair color ...
	- Ordinal(has ordering): military rank, difficulty of a recipe 
- Numerical
	- Continuous: lifetime of a battery \[0, ...\[
	- Discrete: number of people in a room
- Structured: csv, database
- Unstructured: txt, jpeg
- Semi-Structured(structured in their syntax but variable contents): json, xml


## Data Cleaning

### Detect (near) duplicates:
- numeric: cosine similarity
- text: pairwise Levensthein distance
![[Pasted image 20230920195637.png]]
![[Pasted image 20230920195827.png]]

### Outlier Detection

Outliers:
- are single datapoints with very abnormal values
- should be removed because they could significantly affect results


### Missing values

sometimes fillable with interpolation / median