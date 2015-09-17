---
layout: post
title: Tip&#58; Side by Side Installation of SQL Server 2005 and SQL Server 2000
date: 2008-02-01 18:51
author: John
comments: true
categories: [All]
---
<P><FONT color=#800080>Tip: when installing SQL Server, consider using named instances.</FONT></P> <P>I recently installed SQL Server 2005&nbsp;on my&nbsp;PC.&nbsp;It went&nbsp;fairly quick and installed with 0 issues. I was also quite pleased that it&nbsp;installed very nicely side by side with a SQL Server 2000 installation already on my PC. Now when I installed SQL Server 2000 on my PC way back when, I installed it as a named instance called SQL2000. Thus, my server name is MYSERVERNAME\SQL2000 in all of my connection strings and so on. One of the nice things about installing all of your SQL Server instances as named instances is that they stay isolated from one another pretty well. </P> <P>OK, to better demosntrate how named instances work ... For example all of my folder in the C:\Program Files\Microsoft SQL Server directory are as follows:&nbsp;</P> <UL> <LI>\80&nbsp;&nbsp;// This folder seems to have assorted SQL 2000 files in it <LI>\90&nbsp;&nbsp;// This folder seems to have assorted SQL 2005 files in it <LI>\MSSQL&nbsp;&nbsp;// This folder contains SQL 2000 SQL instance's reporting services <LI>\MSSQL$SQL&nbsp;// This folder contains SQL 2000's SQL instance's system files &amp; data <LI>\MSSQL.1&nbsp;// This folder contains SQL 2005 system files &amp; data <LI>\MSSQL.2&nbsp;// This folder contains SQL 2005 reporting services</LI></UL> <P>Notice that all of the folders are segregated from each other so that the SQL 2000 and&nbsp;SQL 2005 installation do no interfere with each other. Also, the Reporting Services installations for both 2000 and 2005 have separate virtual web sites and separate services. </P> <P>While this isn't earth shatterring news, its still pretty darn cool. I certainly don't take for granted that these products work side by side nor that Visual Studio.NET 2005 and Visual Studio.NET 2003 work side by side. I've been through too many backward incompatible and version incompatible nightmares. Side by side is a good thing. Virtual PC is nice, but side by side is better.</P> <P>&nbsp;</P>
