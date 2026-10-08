# Aggregate summary provenance

Generated on 2026-10-08 by reading existing local files. No model was retrained. These are descriptive archive checks, not independently validated experimental results.

## Label counts

`label_counts.csv` counts the `label` column in:

```text
AC1_24_25_Term1_Group01_Gu_Rui/05_Output_Appendix/lable/
  labels_participant_1.csv
  labels_participant_2.csv
  labels_participant_3.csv
```

Each source has 13 records. The three label totals are 11, 23 and 5, summing to 39. Numeric label meanings are unresolved. Aggregate group numbers do not reveal participant identities or establish why the other two collection groups are absent from modelling.

## Similarity statistics

`similarity_summary.json` summarises the numeric `similarity` column in:

```text
AC1_24_25_Term1_Group01_Gu_Rui/02_All_Images_and_Vector_Diagrams/
  03_Clip_Simulation/Similarity_Chart/similarity_results.csv
```

Calculation: arithmetic mean of 13 rows, plus their minimum and maximum. The CSV contains image/text feature filenames but no participant identifier. The statistics therefore apply to this particular file, not all 39 modelling records or all 65 collection trials. Correct feature pairing and participant coverage are not established by these summary statistics.

To reproduce the arithmetic with Python's standard library, use the authorised local CSV:

```python
import csv
from statistics import mean

with open("path/to/similarity_results.csv", encoding="utf-8-sig", newline="") as stream:
    values = [float(row["similarity"]) for row in csv.DictReader(stream)]
print(len(values), mean(values), min(values), max(values))
```
