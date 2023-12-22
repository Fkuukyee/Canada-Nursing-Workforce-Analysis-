# Canada Nursing Workforce Analysis 
This project report encompasses a thorough investigation into the nursing workforce dynamics in Canada to achieve following;
- Workforce Planning Strategy: To conduct an evaluation of staffing requirements to ensure that the Canadian healthcare system is adequately equipped with the appropriate number of skilled nursing professionals.
- Prioritizing Patient Safety: The goal is to proactively identify and prevent avoidable incidents through informed workforce management.
- Enhancing Resource Allocation: Our focus will extend to optimizing the allocation of nursing staff, aligning the skills and expertise of nurses with the specific demands of healthcare units and shifts, with the aim to improving resource utilization.

## Datasets
The datasets encompass a wealth of information spanning supply, workforce, demographic, characteristics, education, and employment trends within Canada's nursing workforce.
Source: “Canadian Institute for Health Information. Nursing in Canada, 2022"
Time-Span: 2013 to 2022

## Data cleaning
Excel was employed for preliminary cleaning tasks. Subsequently, pandas was utilized to transform tables, rename columns, and ensure consistency in strings. To refine the numeric columns, SQL was employed to remove commas and extraneous symbols. Additionally, non-essential columns were dropped using SQL, resulting in a streamlined and cleaned dataset for further analysis.
### Preliminary Cleaning Using Excel
- Removed duplicate entries
- Corrected the formatting inconsistencies.
- Standardized date formats.

### Transformed Tables Using Pandas
Performed transformations such as reshaping the data to meet analysis requirements.
Dropped Non-Required Columns Using SQL DROP COLUMN clause.

### SOME SQL QUERIES
```
-- Summarizing Data by Province (2018)
SELECT Province, 
       SUM(nurse_practitioners) AS Total_Nurse_Practitioners,
       SUM(registered_nurses) AS Total_Registered_Nurses,
       SUM(registered_psychiatric_nurses) AS Total_Registered_Psychiatric_Nurses,
       SUM(licensed_practical_nurses) AS Total_Licensed_Practical_Nurses,
       SUM(Total_nurses) AS Total_Nurses
FROM nurses_data
WHERE Year = 2018
GROUP BY Province;

-- Summarizing Data by Health Region
SELECT [Health Region], 
       SUM(nurse_practitioners) AS Total_Nurse_Practitioners,
       SUM(registered_nurses) AS Total_Registered_Nurses,
       SUM(registered_psychiatric_nurses) AS Total_Registered_Psychiatric_Nurses,
       SUM(licensed_practical_nurses) AS Total_Licensed_Practical_Nurses,
       SUM(Total_nurses) AS Total_Nurses
FROM Table3
GROUP BY [Health Region];

-- Year-over-Year Changes
SELECT Year,
       Total_nurses - LAG(Total_nurses, 1) OVER (ORDER BY Year) AS Yearly_Change
FROM (
    SELECT Year, 
           SUM(Total_nurses) AS Total_nurses
    FROM Table3
    GROUP BY Year
) AS Yearly_Summary;

```

### VISUALISATONS

![image](https://github.com/Fkuukyee/Canada-Nursing-Workforce-Analysis-/assets/147086232/f894e494-7f54-49ae-9a73-ce07cfadb846)

![image](https://github.com/Fkuukyee/Canada-Nursing-Workforce-Analysis-/assets/147086232/0997bacd-faf8-4f56-bcda-8f2e844be987)

![image](https://github.com/Fkuukyee/Canada-Nursing-Workforce-Analysis-/assets/147086232/15a92a0f-9440-40e2-b085-f3470ba4aab2)


### Findings

1. Overall Increase: In most provinces, there is a noticeable increase in the number of nurses from 2018 to 2022. This trend indicates a growth in healthcare resources in terms of nursing staff across Canada.

2. Provincial Variations: Some provinces, such as Ontario and Quebec, show a significant increase in the number of nurses. Other provinces also demonstrate growth, Albelta at a smaller scale.

3. Relative Rankings: The relative rankings of provinces in terms of nursing numbers seem consistent between 2018 and 2022, with Ontario, Quebec, and Alberta remaining the top three in both years.
4. The year-over-year changes in the total number of nurses for the specified periods are as follows:
  - From 2018 to 2019: There was a decrease of 11,490 nurses.
  - From 2019 to 2020: There was an increase of 26,259 nurses.
  - From 2020 to 2021: There was a decrease of 5,432 nurses.
  - From 2021 to 2022: There was an increase of 4,302 nurses.
