---
layout: post
title: Displaying the Contents (and Row Versions) of an ADO.NET DataSet
date: 2008-02-01 18:50
author: John
comments: true
categories: [All]
---
<P>Was asked for this code a few days ago after a quick demo I did, so I thought I'd throw it out here. Its a&nbsp;quick code snippet that displays the contents of a DataSet for debugging purposes. But first, here is a quick code snippet that grabs a DataSet full of 2 DataTables.</P> <DIV style="BORDER-RIGHT: windowtext 1pt solid; PADDING-RIGHT: 0pt; BORDER-TOP: windowtext 1pt solid; PADDING-LEFT: 0pt; FONT-SIZE: 8pt; BACKGROUND: white; PADDING-BOTTOM: 0pt; BORDER-LEFT: windowtext 1pt solid; COLOR: black; PADDING-TOP: 0pt; BORDER-BOTTOM: windowtext 1pt solid; FONT-FAMILY: Courier New">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">private</SPAN> <SPAN style="COLOR: blue">void</SPAN> GetData()<PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; {</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">string</SPAN> cnStr = <SPAN style="COLOR: maroon">@"server=Mine;database=northwind;integrated security=true;"</SPAN>;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; SqlConnection cn = <SPAN style="COLOR: blue">new</SPAN> SqlConnection(cnStr);</PRE><PRE style="MARGIN: 0px">&nbsp;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; DataSet ds = <SPAN style="COLOR: blue">new</SPAN> DataSet(<SPAN style="COLOR: maroon">"MyDataSet"</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">string</SPAN> customerSql = <SPAN style="COLOR: maroon">"SELECT CustomerID, CompanyName, City, Country"</SPAN></PRE><PRE style="MARGIN: 0px"><SPAN style="COLOR: maroon">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+ " FROM Customers ORDER BY CompanyName"</SPAN>;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; SqlCommand customerCmd = <SPAN style="COLOR: blue">new</SPAN> SqlCommand(customerSql);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; customerCmd.CommandType = CommandType.Text;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; customerCmd.Connection = cn;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; SqlDataAdapter da = <SPAN style="COLOR: blue">new</SPAN> SqlDataAdapter(customerCmd);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; da.Fill(ds, <SPAN style="COLOR: maroon">"Customers"</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">string</SPAN> orderSql = <SPAN style="COLOR: maroon">"SELECT OrderID, CustomerID, OrderDate "</SPAN></PRE><PRE style="MARGIN: 0px"><SPAN style="COLOR: maroon">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+ " FROM Orders ORDER BY OrderDate DESC"</SPAN>;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; SqlCommand orderCmd = <SPAN style="COLOR: blue">new</SPAN> SqlCommand(orderSql);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; orderCmd.CommandType = CommandType.Text;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; orderCmd.Connection = cn;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; da.SelectCommand = orderCmd;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; da.Fill(ds, <SPAN style="COLOR: maroon">"Orders"</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; DisplayDataSet(ds, <SPAN style="COLOR: maroon">"My Data"</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; }</PRE></DIV><!--EndFragment--> <P>And here is the code snippet that iterates through the DataSet to show the DataTables:</P> <DIV style="BORDER-RIGHT: windowtext 1pt solid; PADDING-RIGHT: 0pt; BORDER-TOP: windowtext 1pt solid; PADDING-LEFT: 0pt; FONT-SIZE: 8pt; BACKGROUND: white; PADDING-BOTTOM: 0pt; BORDER-LEFT: windowtext 1pt solid; COLOR: black; PADDING-TOP: 0pt; BORDER-BOTTOM: windowtext 1pt solid; FONT-FAMILY: Courier New">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">private</SPAN> <SPAN style="COLOR: blue">void</SPAN> DisplayDataSet(DataSet ds, <SPAN style="COLOR: blue">string</SPAN> title)<PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; {</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.WriteLine(title);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: green">//--- Loop through the DataTables</SPAN></PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">foreach</SPAN> (DataTable table <SPAN style="COLOR: blue">in</SPAN> ds.Tables)</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; {</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.WriteLine(<SPAN style="COLOR: maroon">"*** DataTable: "</SPAN> + table.TableName + <SPAN style="COLOR: maroon">"***"</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: green">//--- Loop through each DataTable's DataRows</SPAN></PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">foreach</SPAN> (DataRow row <SPAN style="COLOR: blue">in</SPAN> table.Rows)</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; {</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: green">//--- Display the original values, if there are any.</SPAN></PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">if</SPAN> (row.HasVersion(System.Data.DataRowVersion.Original))</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; {</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.Write(<SPAN style="COLOR: maroon">"Original Row Values ===&gt; "</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">foreach</SPAN>(DataColumn column <SPAN style="COLOR: blue">in</SPAN> table.Columns)</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.Write(column.ColumnName + <SPAN style="COLOR: maroon">" = "</SPAN> + </PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;row[column, DataRowVersion.Original] + <SPAN style="COLOR: maroon">", "</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.WriteLine(<SPAN style="COLOR: maroon">""</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; }</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp
; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: green">//--- Display the current values, if there are any.</SPAN></PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">if</SPAN> (row.HasVersion(System.Data.DataRowVersion.Current))</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; {</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.Write(<SPAN style="COLOR: maroon">"Current Row Values ====&gt; "</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">foreach</SPAN>(DataColumn column <SPAN style="COLOR: blue">in</SPAN> table.Columns)</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.Write(column.ColumnName + <SPAN style="COLOR: maroon">" = "</SPAN> + </PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;row[column, DataRowVersion.Current] + <SPAN style="COLOR: maroon">", "</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.WriteLine(<SPAN style="COLOR: maroon">""</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; }</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Debug.WriteLine(<SPAN style="COLOR: maroon">""</SPAN>);</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; }</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; }</PRE><PRE style="MARGIN: 0px">&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; }</PRE></DIV><!--EndFragment--> <P>The code is pretty straightforward for DisplayDataSet. I loop through each table in the DataSet, then through the rows in each table, and finally through the columns in each row. Before checking each column, however, I first check to make sure the row has an Original version and/or a Current version. This is nice for displaying the original and current versions of a column's value when you allow the user to edit multiple rows and send all of the changes to the server in a batch. If you don't check if the row has an original version first and the row happens to have been a new row, then it will throw an exception. </P> <P>I&nbsp;often take this code and modify it for the debugging purpose of the moment. I've used a couple that throw them into hierarchical DataGrids and make everything nice and pretty. But sometimes I just want a quick and dirty method with a quick and drity code base like this.&nbsp;There are tools out there that you can download to do this, but if all you need is a quick method to display the data and its row versions, this will do nicely too.</P> <P>Oh ... and the code above assumes the following <SPAN style="COLOR: blue">using</SPAN> statements:</P> <DIV style="BORDER-RIGHT: windowtext 1pt solid; PADDING-RIGHT: 0pt; BORDER-TOP: windowtext 1pt solid; PADDING-LEFT: 0pt; FONT-SIZE: 8pt; BACKGROUND: white; PADDING-BOTTOM: 0pt; BORDER-LEFT: windowtext 1pt solid; COLOR: black; PADDING-TOP: 0pt; BORDER-BOTTOM: windowtext 1pt solid; FONT-FAMILY: Courier New"><PRE style="MARGIN: 0px"><SPAN style="COLOR: blue">using</SPAN> System;</PRE><PRE style="MARGIN: 0px"><SPAN style="COLOR: blue">using</SPAN> System.Data;</PRE><PRE style="MARGIN: 0px"><SPAN style="COLOR: blue">using</SPAN> System.Diagnostics;</PRE></DIV><!--EndFragment-->
