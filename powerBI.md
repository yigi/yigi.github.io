charts.powerbi.tips

- glyph can be anything
- use anchor points on glyph


# Pareto chart

information is provided about an individual product or category as a bar, and a cumulative scale as a line which compairs all bars.  This type of visual can be extremely helpful when conducting failure mode analysis, causes of a problem, or even product portfolio balances. 

<img align="left" width="450" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Pareto-Final-Product.png">

<img align="center" width="650" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Load-Data-to-Query-Editor.png">


On the Home ribbon click Close & Apply to complete the data load.
Add a Slicer for the Segment.  Enhance the look of the slicer by changing it from a vertical to a horizontal slicer.  While the slicer is highlighted, click the Paint Roller expand the General section and change the orientation from vertical to Horizontal.

<img align="center" width="650" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Segment-Slicer.png">


Repeat the same process to add a Slicer for the item field. Next, add a table view of all the fields.  Start with Segment, then Item and finally add Sales to the Table Visual. 

<img align="center" width="650" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Data-Table.png">


Notice, now that we added all the Fields, there are a number of repeating values.  We have Category 1 and Item 1 repeated 9 times.  In some cases, it will be necessary to have this level of data brought into the data model within PowerBI.  A common reason is that this level of granularity is required for other report pages, or visuals.  It is OK to bring large amounts of data, but as a method of best practice it is recommended that you bring in the data required to support the visuals.

Now, to address these multiple items that we see in our data.  In the sample Pareto image provided at the beginning of this Tutorial we only had one bar for Category 2 Item 3.  Thus, we need to summarize each grouping of every Category and Item combination.  To do this we will construct a summary table.

First, we will create a unique Key that will be used to summarize each combination of Category and Item pair.  Click the bottom half of the New Measure button located on the Home ribbon.

<img align="left" width="250" height="200" src="http://powerbitips.azurewebsites.net/wp-content/uploads/2016/10/Calculated-Column.png">

Enter the following DAX expression.  This new column titled Blend will be the unique Key that is utilized to summarize the data.

```DAX
Blend = Data[Segment]  &  "-"  &  Data[Item]
```

Select the Modeling ribbon and then click on the New Table button.  Enter the following DAX expression.

```DAX
Summary = SUMMARIZE('Data', Data[Blend], "Sum Sales", SUM(Data[Sales]) )
```
