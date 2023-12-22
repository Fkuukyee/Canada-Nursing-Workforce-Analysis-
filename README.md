# Canada Nursing Workforce Analysis 
This project report encompasses a thorough investigation into the nursing workforce dynamics in Canada to achieve following;
- Workforce Planning Strategy: To conduct an evaluation of staffing requirements to ensure that the Canadian healthcare system is adequately equipped with the appropriate number of skilled nursing professionals.
- Prioritizing Patient Safety: The goal is to proactively identify and prevent avoidable incidents through informed workforce management.
- Enhancing Resource Allocation: Our focus will extend to optimizing the allocation of nursing staff, aligning the skills and expertise of nurses with the specific demands of healthcare units and shifts, with the aim to improving resource utilization.

## DATASETS
The datasets encompass a wealth of information spanning supply, workforce, demographic, characteristics, education, and employment trends within Canada's nursing workforce.
Source: “Canadian Institute for Health Information. Nursing in Canada, 2022"
Time-Span: 2013 to 2022

## DATA CLEANING
Excel was employed for preliminary cleaning tasks. Subsequently, pandas was utilized to transform tables, rename columns, and ensure consistency in strings. To refine the numeric columns, SQL was employed to remove commas and extraneous symbols. Additionally, non-essential columns were dropped using SQL, resulting in a streamlined and cleaned dataset for further analysis.
### Preliminary Cleaning Using Excel:
- Removed duplicate entries
- Corrected the formatting inconsistencies.
- Standardized date formats.

### Transformed Tables Using Pandas:
Performed transformations such as reshaping the data to meet analysis requirements.
Dropped Non-Required Columns Using SQL DROP COLUMN clause.

### SQL QUERY
```
with ct1 as (
select t1.Year,t1.`Type of professional`,
sum(t1.Supply_number_of_nurses) as total_supply_nurses,
sum(t2.`Workforce_ number_of_nurses`) as total_workforce_nurses,
sum(t2.`Workforce_ employed_full time`) as y_workforce_employed_fulltime,
sum(t2.`Workforce_ employed_part_time`) as y_workforce_employed_parttime,
from table1 t1
join table2 t2
on t1.Year = t2.Year
and t1.Jurisdiction = t2.Jurisdiction
group by t1.Year,t1.`Type of professional`
)
select ct1.Year,
ct1.`Type of professional`,
ct1.total_supply_nurses,
ct1.total_workforce_nurses,
round((ct1.total_workforce_nurses/ct1.total_supply_nurses),2) as workforce_to_supply_ratio,
ct1.y_workforce_employed_fulltime,
ct1.y_workforce_employed_parttime,
round((ct1.y_workforce_employed_fulltime/ct1.total_workforce_nurses),2) as workforce_fulltime_to_total_workforce_ratio,
round((ct1.y_workforce_employed_parttime/ct1.total_workforce_nurses),2) as workforce_parttime_to_total_workforce_ratio
from ct1
```

### Guiding questions
- What variations exist in the nurse-to-supply ratio across different jurisdictions?
- Which regions exhibit a favorable nurse-to-supply ratio, indicating an adequate workforce, and which regions have the lowest ratios, suggesting a potential shortage?
- How does the distribution of nurses across different work types change over the years?
- what insights can be derived from the detailed breakdown of the contributions of part-time and full-time nurses to the overall nurse workforce?

### VISUALISATON
![dasboard](https://github.com/Fkuukyee/Fkuukyee/assets/147086232/2fec6ec9-a4bb-4669-b051-4d149913f419)

![geodistribution](https://github.com/Fkuukyee/Fkuukyee/assets/147086232/555f8c38-8817-454d-a59e-79f48ea8920a)

### Findings




