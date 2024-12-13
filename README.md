## Stata Code for GIS Data Manipulation and Visualization

## TABLE OF CONTENT
- [DATA FILTERING](#data-filtering)
- [SAVING FILTERED DATA](#saving-filtered-data)
- [COLLAPSING DATA](#collapsing-data)
- [BY MUNICIPALITY GROUP](by-municipality-group)
- [GRAPHICAL ANALYSIS](#graphical-analysis)
- [SAVING GRAPHS](#saving-graphs)
- [EXPORTING DATA](#exporting-data)
- [FILE DESCRIPTIONS](#file-descriptions)

### Step-by-Step Breakdown of Code

# DATA FILTERING
```
drop if cty_code < 22
```
This line filters out observations where the cty_code is less than 22.

# SAVING FILTERED DATA
```
save "Northern region data.dta"
```
The filtered dataset is saved as a Stata data file for further processing.

# COLLAPSING DATA
By County Name:
```
collapse (mean) mean_empl_intern_org = empl_intern_org (sd) Standard_D_empl_intern_org = empl_intern_org [aweight = pop1664], by(cty_name)
```
This calculates:

The mean of empl_intern_org by cty_name.

The standard deviation of empl_intern_org weighted by the population aged 16-64 (pop1664).

# BY MUNICIPALITY GROUP
```
collapse (mean) mean_empl_intern_org = empl_mining (sd) Standard_D_empl_intern_org = empl_mining [aweight = pop1664], by(muni_group)
```
This calculates:

The mean and standard deviation of empl_mining by muni_group.

# GRAPHICAL ANALYSIS
- Boxplots:

By Municipality Group:
```
graph box empl_mining, over(muni_group)
```
By County Code:
```
graph box empl_mining, over(cty_code)
```
- Scatter Plot:
```
twoway (scatter empl_mining educ)
```
This plot visualizes the relationship between mining employment (empl_mining) and education level (educ).

# SAVING GRAPHS
Each graph is saved for documentation and reporting:
```
graph save "Graph for Muni group.gph"
graph save "Graph for cty_code.gph"
graph save "Scattered plots for mining and education.gph"
```

# EXPORTING DATA
To CSV:
```
export delimited using "Exported Data for GIS.csv", replace
```
This exports the prepared dataset in CSV format for GIS applications.

To Excel:
```
export excel using "excel file for gis to delete leta.xls", firstrow(variables)
```
This exports the dataset to Excel with variable names as the first row.


# File Descriptions
- Northern region data.dta: Cleaned dataset containing data specific to the Northern region.
- Mean Mining and standard deviation.dta: Aggregated dataset with mean and standard deviation of mining employment by county.
- Graphs:
Boxplot by Municipality Group.
Boxplot by County Code.
Scatter Plot for Mining Employment vs. Education.
- Exported Data for GIS.csv: Final dataset prepared for GIS analysis.
- Excel file for GIS.xls: Final dataset exported in Excel format.
