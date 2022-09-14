# PyBer Analysis

## Oerview

To assess performance, the rideshare company PyBer requested that metrics collected for both rides and cities be combined and categorized by the classification or type of the city. The classifications are Urban, Suburban, and Rural.

PyBer has asked for a summary of the data by city type and a direct comparison of weekly fare totals for set period. The comparison of weekly fare totals is presented as a chart.

### Methods

#### Tools
- Python 3.7
    - pandas
    - matplotlib
#### Data
The data sets were provided by the company. One based on cities and the other on rides provided.

#### Process Overview

#### Part 1: Creating a Summary by City Type

- The data was read from .csv files and a Pandas DataFrame created for each.
- DataFrames were merged on the city column resulting in a new DataFrame with the required metrics preserved:
![Merged DataFrame](/assets/merged_frame.png)
- A summary dataframe was created from a dictionary a Series, primarily created using groupby() to determine values based on the type of city:
    total_drivers_type = city_data_df.groupby(['type']).sum()['driver_count']

- The summary DataFrame was formatted, the columns reordered, and the index label removed. The completed Frame is shown in the Results section.

#### Part 2: Direct Comparison Chart

- A new DataFrame was created using the "type", "date", and "fare" columns from the merged DataFrame shown above.
- From the newly created DataFrame, groupby() was used to create a new DataFrame containing the sum of the fares for each date in each type of city:
        pyber_td_fare_df = pd.DataFrame(pyber_type_date_df.groupby(["Type","Date"]).sum()["Fare"])
- This frame was then pivoted and used in the creation of another frame specifically from a date range using the .loc[] method.
- The index of this frame was then set to be a DateTimeIndex.
- The new idex allowed the use of resample() by week.
- The DataFrame used to populate the chart was then formed using the sum of each week.

## Results

### Summary Table
![Summary Table](/assets/PyBer_Summary.png)

### Total Fare Chart

![Total Fare by City Type](/analysis/PyBer_fare_summary.png)

### Discussion

From the table it is clear that each city type is different, but Rural and Urban the most different. More rides were taken in Urban areas and uniquely, there seem to be more drivers availible than are needed. 

The Average Fare per Ride is also lowest in Urban areas, as is Average Fare per Driver. Although the Urban areas have the highest Total Fares, doubling that of Suburban, the Average Fare per Driver in Suburban areas is more than double that of Urban areas while the Average Fare per Ride is is not substatially larger than that of urban areas.

From the chart, each city type appears to have a spike in demand near the end of February, though perhaps most prominent in the Suburban cities. This assumes that demand for the rides is related to change in the sum of the weekly fares.

Given the relativley short time period it is difficult to speculate on the relative stabilty of any of the markets.

## Recommendations

Although Rural is the smallest market for PyBer, it generated the most in Average Fare Revenue per Driver. Focusing more marketing effort on Rural cities could provide the largest revenue increase on a per driver basis.

The Urban areas appear saturated, adding more drivers to these areas may not be cost effective until overall demand increases.

Expantion into additional Suburban cities or increasing PyBer's visibility in those areas may yield an appreciable increase in revenue if a sufficient number of riders is sustained. The chart suggests that, during the limited time period, the sum of the Suburban cities fares does not appear to stabilize in the same way Urban and Rural do. Increasing recurring ridership would make this more predictible.




