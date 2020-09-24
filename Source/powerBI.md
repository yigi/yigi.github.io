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

!! In this equation we first select the table and in this case it is ‘Data’.  Then the column we want to summarize or group by is the Segment column noted as Data[Blend].  The next field is the title of the summarized field column, noted as “Sum Sales”.  Then DAX function that calculates the Sum of the column labeled Data[Sales], noted as SUM(Data[Sales]).  It is relevant to point out here that the SUMMARIZE function will only work with building a new table and not as a calculated column or measure.

Add a new Table visual to the report and include the two newly created fields from the Summary table.

<img align="left" width="650" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Summary-Table-Visual.png">


We have a field titled Blend which is our Key for all the summarized groupings.  Next, we will want to parse out the Segments and Items from this blend column.  We will want to use Category 1 & 2 in a slicer and the same for Items 1 to 5.  Highlight the summary table by clicking the grey space next to the word Summary.  Click the New Column button on the Modeling ribbon and enter the following DAX expression.

```DAX
Segment = PATHITEM(
   SUBSTITUTE(Summary[Blend], "-" , "|" ),
   1 )
```

In this expression the Substitute function replaced the dash “-” with a “|” character.  Then the PATHITEM function can then parse the text into segments.  By entering a 1 we select the first item in the sequence.  For our example we only have two items, but when you’re working with file paths you can have multiple items in the path such as “\users\mike\my documents\my folder\”, which would equate to users = position 1, mike = position 2, my documents = position 3, etc..

Add another new column with the following DAX expression for the item column.

```DAX
Item = PATHITEM( 
  SUBSTITUTE(Summary[Blend], "-" , "|" ),
  2 )
```

Note: We changed the PATHITEM position from 1 to 2.

Next add the newly created Segment and Item columns to our summary table visual that we created earlier.

<img align="left" width="650" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Add-New-Fields.png">

 Now we have to modify our slicers to point to the new Item and Segment fields we created in the Summary table.  Select the Segment Slicer Visual and add the Segment Field from the Summary table.
 
 
<img align="left" width="650" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Update-Segment-Slicer.png">

<img align="left" width="650" height="400" src="https://powerbi.tips/wp-content/uploads/2016/10/Update-Item-Slicer.png">
