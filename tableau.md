

# TABLEAU

<img align="center" width="850" height="500" src="https://miro.medium.com/max/700/0*knbe-bXPrpJR5-nb">

<img align="center" width="850" height="500" src="https://miro.medium.com/max/700/0*XeUtoj3vZWNWaOUU">

When you launch Tableau Desktop, the data connectors that are available to you are listed on the Connect pane, which is the left pane on the Start page. File types are listed first, then common server types, or servers that you’ve recently connected to. Click More to see the complete list of data connectors you can use. UnderOpen, you can open workbooks that you have already created. Under Sample Workbooks, view sample dashboards and worksheets that come with Tableau Desktop. Under Discover, find additional resources like video tutorials, forums

___________________________________________________________________________________________________________________________

## Connecting to the Sample-Superstore data set
For convenience, let's use the sample data set that comes with Tableau installation named sample superstore.xls.However, in this tutorial, we will download it from here and load it as an excel sheet. The data is that of a United States Superstore. It contains information about products, sales, profits, and so on that you can use to identify key areas for improvement within this fictitious company.
Steps
- Import the Data into tableau workspace from the computer.
- Under the Sheets Tab, three sheets will become visible namely Orders, People, and Returns. However, we will focus only on Orders data. Double click on Orders Sheet and it opens up just like a spreadsheet.
- We observe the first three rows of data looks a bit different and is not in the desired format. Here we make use of Data Interpreter, also present under Sheets Tab. By clicking on it we get a nicely formatted sheet. If you wish to view the exact changes that it made, click on Review the results, and choose the Orders tab in the opened Excel sheet. it will show, it simply removed the erroneous data.


<img align="center" width="950" height="500" src="https://miro.medium.com/max/700/0*cI1bKAw15o7AMbXF">

___________________________________________________________________________________________________________________________

## Creating a View
We will start by creating a simple chart. In this section, we will get to know our data and will start to ask questions about the data to gain insights There are some important terms that we will encounter in this section.
- Dimension
- Measures
- Aggregation
Dimensions are qualitative data, such as a name or date. By default, Tableau automatically classifies data that contains qualitative or categorical information as a dimension, for example, any field with text or date values. These fields generally appear as column headers for rows of data, such as Customer Name or Order Date, and also define the level of granularity that shows in the view.
Measures are quantitative numerical data. By default, Tableau treats any field containing this kind of data as a measure, for example, sales transactions or profit. Data that is classified as a measure can be aggregated based on a given dimension, for example, total sales (Measure) by region (Dimension).
Row-level data rolled up to a higher category, such as the sum of sales or total profit. Tableau does this automatically so you can break data down to the level of detail that you want to work with.

Go to the worksheet. Click on the tab Sheet 1at the bottom left of the tableau workspace.

Once, you are in the worksheet, from Dimensions in the Data pane, drag Order Date to the Columns shelf.
When you drag Order Date to the columns shelf, Tableau creates a column for each year in your data set. Under each column is an Abc indicator. This indicates that you can drag text or numerical data here, like what you might see in an Excel spreadsheet. If you were to drag Sales to this area, Tableau creates a cross-tab (like a spreadsheet) and displays the sales totals for each year.
From Measures, drag Sales to the Rows shelf.
Tableau generates a chart with sales rolled up as a sum (aggregated). Total aggregated sales for each year by order date is displayed.Tableau always generates a line chart for a view that includes time (in this case Order Date)


<img align="center" width="950" height="500" src="https://miro.medium.com/max/700/0*aCDnCV7ZRoKK1rpq">

<img align="center" width="950" height="500" src="https://miro.medium.com/max/700/0*jYjPA98DRPPZqQGj">

___________________________________________________________________________________________________________________________

## Adding filters to the view
Filters can be used to include or exclude values in the view. Here we try to add two simple filters to the worksheet to make it easier to look at product sales by sub-category for a specific year.
Steps
In the Data pane, under Dimensions, right-click Order Date and select Show Filter.Repeat for Sub->category field also.
Filters are card types and can be moved around on the canvas by clicking on the filter and dragging it to another location in the view

Steps
In the Data pane, under Measures, drag Profit to Color on the Marks card.
<img align="center" width="950" height="500" src="https://miro.medium.com/max/700/0*z6Y-ZvsC8N0neYEt">

<img align="center" width="950" height="500" src="https://miro.medium.com/max/700/0*7iLN8uLcwgeyyzAy">

Key Findings
Let’s take a closer look at the filters to find out more about the unprofitable products.
Steps
In the view, in the Sub-Category filter card, clear all of the check boxes except Bookcases, Machines, and Tables. This throws an interesting fact. While in some years, Bookcases and Machines were actually profitable. However, in 2016, Machines became unprofitable.
Select All in the Sub-Category filter card to show all sub-categories again.
From Dimensions, drag Region to the Rowsshelf and place it to the left of Sum(Sales). We notice that machines in the South are reporting a higher negative profit overall than in your other regions.
Let us now give a name to the sheet. At the bottom-left of the workspace, double-clickSheet 1 and type Sales by Product and Region.
In order to preserve the view, Tableau allows us to duplicate our worksheet so that we can continue in another sheet from where we left off.
In your workbook, right-click the Sales by Product and Region sheet and selectDuplicate and rename the duplicated sheet toSales-South.
In the new worksheet, from Dimensions, dragRegion to the Filters shelf to add it as a filter in the view.
In the Filter Region dialogue box, clear all check boxes except South and then click OK. Now we can clearly focus on sales and profit in theSouth. We find that machine sales had a negative profit in 2014 and again in 2016. We will investigate this in the next section
Lastly, do not forget to save the results by selecting File > Save As. Give your workbook a name, like Regional Sales and Profits.


<img align="center" width="950" height="500" src="https://miro.medium.com/max/700/0*go7tV7tYNIxQ7Fd0">
