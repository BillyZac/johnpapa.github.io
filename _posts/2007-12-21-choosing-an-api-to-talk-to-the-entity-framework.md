---
layout: post
title: Choosing an API to Talk to the Entity Framework
date: 2007-12-21 15:18
author: John
comments: true
categories: [All]
---
<p><a href="http://blogs.msdn.com/diego/">Diego Vega</a> started me thinking about the differences between the different API's to the Entity Framework. I am currently doing a lot of writing about the Entity Framework and preparing many sessions on the topic so it obviously interests me :).&nbsp; I had asked Diego about some of the differences between Entity SQL and using the strongly typed syntax of LINQ. <a href="http://blogs.msdn.com/diego/archive/2007/12/20/some-differences-between-esql-and-linq-to-entities-capabilities.aspx">He posted a quick list</a> of some of the differences and similarities in <a href="http://blogs.msdn.com/diego/archive/2007/12/20/some-differences-between-esql-and-linq-to-entities-capabilities.aspx">this post</a> today. (Thanks Diego)</p> <p>That's a nice hit list of differences. I had not thought about how you can navigate with Entity SQL even without a Navigation property. Going further on this train of thought I figured I would post my interpretation of a similar question I get from people a lot.</p> <p><strong>In what situations would I choose 1 over the other? </strong></p> <p>The options being:</p> <ol> <li>Entity SQL with Entity Client  <li>Entity SQL with Object Services  <li>LINQ with Object Services </li></ol> <p>This is obviously an involved question/answer as the situation has to take into account several factors to make that determination. But overall here is a high level barometer you can use: </p> <ul> <li>Entity SQL with Entity Client  <ul> <li>when you need to read data and not write to it  <li>when you need dynamic queries </li></ul> <li>Entity SQL with Object Services  <ul> <li>when you need to retrieve entities you can interact with and persist, using a dynamic query </li></ul> <li>LINQ with Object Services  <ul> <li>when you need to retrieve entities you can interact with and persist, using strongly typed syntax </li></ul></li></ul> <p>&nbsp;</p> <p>I intentionally left this post very short as a means to help those who are just trying to wade through the deluge of information that is available on the Entity Framework. My general style is to keep blog posts to a quick and easily digestible piece of information. Deep dark details of topics I usually reserve for articles as I know personally when I read a blog post that goes on and on I start to lose focus ... which means I have a short attention span :)</p>
