# Staff-Attendance-Analysis-in-PowerBI
This repository utilizing Power BI, analyzes staff attendance data, uncovering insights into work from home preferences, sick leave patterns, and overall presence rates.


## Data
The dataset consist of the four sheets for different months and abbreviation reference:  
* **Apr 2022**   
* **May 2022**
* **June 2022**     

* Columns in these sheets are:   
  * Employee Code
  * Name 
  * Corresponding date columns for each month(`1-Apr` to `30-Apr`)
  * Total Present Days
  * Present
  * Work from home
  * Paid Leave
  * Sick Leave
  * Birthday Leave(ignored, not much data:)
  * Floating festival(ignored)
  * Bereavement Leave(ignored)
  * Leave without pay
  * Weekly Off
  * Holiday Off
  * Menstrual Leave

* **Attendance Key**   
**P** - Present  
**PL** - Paid Leave  
**SL** -Sick Leave   
**HPL** - Half day PL   
**HSL** - Half day SL  
**WFH** - Work from home   
**FFL** - Floting festival leave   
**HFFL** - Half Day Floting festival leave   
**BL** - Birthday Leave   
**LWP** - Leave without pay  
**HLWP** - Half day Leave without pay  
**BRL** - Bereavement Leave    
**HBRL** - Half Bereavement Leave  
**HWFH** - Half Work From Home  
**WO** - Weekly Off  
**HO** - Holiday Off  
**ML** - Menstrual Leave  
**HML** - Half Day ML  


All date and leave columns were transposed and combined(unpivoted) to a single column named `date`, and the `value` column comprising of entries based on attendance (P, SL, WFH, ML, etc.). Afterwards, the leave rows were removed.


* Calculated entries:  
  * `Total Working Days =   Var totalDays = COUNT('Final Data'[Value])   Var nonWorkDays = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value] IN {"WO", "HO"})   RETURN totalDays - nonWorkDays`
  * `WFH Count = SWITCH(TRUE(), 'Final Data'[Value] = "WFH", 1, 'Final Data'[Value] = "HWFH", 0.5, 0)`  
  * `WFH Count = SUM('Final Data'[WFH Count])`
  * `Present Days =   VAR Presentdays = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value] = "P")    RETURN Presentdays + [WFH Count]`
  * `SL Count = SWITCH(TRUE(), 'Final Data'[Value] = "SL", 1, 'Final Data'[Value] = "HSL", 0.5, 0)`
  * `SL Count = SUM('Final Data'[SL Count])`
  * `WFH % = DIVIDE([WFH Count], [Present Days], 0)`
  * `SL % = DIVIDE([SL Count], [Total Working Days], 0)`
  * `Presence % = DIVIDE([Present Days], [Total Working Days], 0)`
  * `Month = STARTOFMONTH('Final Data'[Date])`
  * `Day of Week = FORMAT('Final Data'[Date], "ddd")`    






## Power BI


### Dashboard:

![Screenshot 2024-04-21 013636](https://github.com/animesshhh/Staff-Attendance-Analysis-in-PowerBI/assets/97463808/9b380e67-cda0-41a2-929e-639445cbf159)


### Key Insights:
1. **Total Working Days** : Calculates the total number of work days for all employees across three months. It also provides a breakdown by month, allowing you to pinpoint periods of high or low activity.
2. **Employee Presence by Month**:  Analyze the total number of days employees were present  across each month. This helps identify seasonal trends in attendance and potential areas for improvement.
3. **Employee Present Percentage**: Overall percentage of time employees were present compared to the total number of working days. This provides a quick snapshot of employee engagement.
4. **Work From Home (WFH) Preference**: Percentage of times employees choose WFH compared to their total in-office presence. This data is valuable for planning employee coordination activities and can inform decisions about future remote work policies.
5. **Sick Leave vs. Total Working Days**: Analyzes the percentage of workdays taken as sick leave. This information helps predict potential staffing shortages and allows for better project planning to avoid delays due to unforeseen absences.
6. **Presence Trend**: Visual representations of employee presence trends over time. You can easily identify periods of high and low presence, helping you understand seasonal or project-related fluctuations.
7. **Work From Home Trend**: Visualize the usage of WFH options over time. This allows you to analyze trends and preferences for WFH arrangements.
8. **Sick Leave Trend**: Visual representation of sick leave trends over time. This can help identify potential health concerns within the workforce or seasonal spikes in illness.
9. **Presence % by Day of Week**: Analyzing the percentage of employees present on each day of the week. With this data, you can identify the days with the highest employee engagement, which can be helpful for scheduling meetings or important announcements.
10. **Work From Home % by Day of Week**: Analyzes the percentage of employees choosing WFH on each day of the week. It reveals potential patterns in WFH preferences, which can be valuable when considering a more permanent shift to remote work models.
11. **Sick Leave % by Day of Week**: Analyzing the percentage of sick leave taken on each day of the week allows you to identify potential causes for increased absences. This could be due to seasonal illnesses or suggest a larger workforce health concern.
