---
layout: post
title: T-SQL&#58; IF NOT EXISTS versus @@ROWCOUNT
date: 2008-02-01 18:50
author: John
comments: true
categories: [All]
---
<P><FONT size=2><FONT face="Trebuchet MS"><SPAN class=843211217-19072005>I was asked a good question the other day regarding&nbsp;why&nbsp;I chose to use "IF NOT EXISTS" in my <A href="http://msdn.microsoft.com/msdnmag/issues/03/11/DataPoints/">Nov 2003 MSDN article on User Defined Functions</A> to check to see if a declared table variable had any rows in it versus checking @@ROWCOUNT. Mostly I chose to use IF NOT EXISTS because I know that I find it less apt to break on me in case I do something silly. For example, if I chose to check @@ROWCOUNT in the SQL sample code below instead of using "IF NOT EXISTS", it works just fine. But what happens if I (or someone else) adds another SQL statement at line 15 that alters the @@ROWCOUNT? For example, If I augment this code in the future to inlcude an UPDATE statement at line 15, the ROWCOUNT will no longer represent the number of rows affected by the INSERT statement (lines 10-14). Is this likely to happen? Probably not. Has it happened to me? Oh yeah, I was burnt once on this. Is it bad to use ROWCOUNT? Not at all! I was being overly careful in this code example and also wanted to show how "IF NOT EXISTS" works. So the answer is that both ways work. </SPAN></FONT></FONT></P> <P><FONT size=2><FONT face="Trebuchet MS"><SPAN class=843211217-19072005></SPAN></FONT></FONT><SPAN class=cb1><FONT color=#0000ff>&nbsp;</P> <DIV class=cf> <DIV style="BORDER-RIGHT: windowtext 1pt solid; PADDING-RIGHT: 0pt; BORDER-TOP: windowtext 1pt solid; PADDING-LEFT: 0pt; FONT-SIZE: 8pt; BACKGROUND: white; PADDING-BOTTOM: 0pt; BORDER-LEFT: windowtext 1pt solid; COLOR: black; PADDING-TOP: 0pt; BORDER-BOTTOM: windowtext 1pt solid; FONT-FAMILY: Courier New"> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;1</SPAN>&nbsp;<SPAN style="COLOR: blue">CREATE </SPAN>FUNCTION fnGetEmployeesByCity3 (@sCity <SPAN style="COLOR: blue">VARCHAR</SPAN>(30))</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;2</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; RETURNS @tblMyEmployees <SPAN style="COLOR: blue">TABLE</SPAN></P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;3</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; (</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;4</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; FirstName <SPAN style="COLOR: blue">VARCHAR</SPAN>(20),</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;5</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; LastName <SPAN style="COLOR: blue">VARCHAR</SPAN>(40),</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;6</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; Address <SPAN style="COLOR: blue">VARCHAR</SPAN>(120)</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;7</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; )</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;8</SPAN>&nbsp;<SPAN style="COLOR: blue">AS</SPAN></P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;&nbsp;9</SPAN>&nbsp;<SPAN style="COLOR: blue">BEGIN</SPAN></P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;10</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">INSERT </SPAN>&nbsp; @tblMyEmployees</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;11</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">SELECT </SPAN>&nbsp; FirstName, LastName, Address</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;12</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">FROM </SPAN>&nbsp;&nbsp;&nbsp; Employees</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;13</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">WHERE </SPAN>&nbsp;&nbsp; City = @sCity </P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;14</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">ORDER BY </SPAN>LastName</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;15</SPAN>&nbsp;</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;16</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">IF NOT EXISTS </SPAN>(<SPAN style="COLOR: blue">SELECT </SPAN>* <SPAN style="COLOR: blue">FROM </SPAN>@tblMyEmployees)</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;17</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">INSERT </SPAN>@tblMyEmployees (Address)</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;18</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">VALUES </SPAN>(<SPAN style="COLOR: maroon">'No matching employees found in the specified city'</SPAN>)</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;19</SPAN>&nbsp;</P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;20</SPAN>&nbsp;&nbsp;&nbsp;&nbsp; <SPAN style="COLOR: blue">RETURN</SPAN></P> <P style="MARGIN: 0px"><SPAN style="COLOR: teal">&nbsp;&nbsp;&nbsp;21</SPAN>&nbsp;<SPAN style="COLOR: blue">END</SPAN></P></DIV><!--EndFragment--></FONT></SPAN></DIV><!--EndFragment-->
