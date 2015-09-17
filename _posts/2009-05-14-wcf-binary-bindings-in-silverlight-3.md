---
layout: post
title: WCF Binary Bindings in Silverlight 3
date: 2009-05-14 22:10
author: John
comments: true
categories: [Silverlight]
---
<p>One of the most common comments I hear form people when they start digging into Silverlight 3 Beta (and Silverlight 2) is the lack of WCF binding options. Some changes have been made to include binary encoding in Silverlight 3, so now we have:</p>  <ul>   <li>customBinding      <ul>       <li>can do things like binary binding with WCF clients </li>        <li>new to Silverlight 3 Beta </li>     </ul>   </li>    <li>basicHttpBinding      <ul>       <li>basic clear text binding </li>     </ul>   </li>    <li>pollingDuplexHttpBinding      <ul>       <li>exactly what it says … a pseudo duplex basic binding that uses polling </li>     </ul>   </li> </ul>  <p>&#160;</p>  <p>Custom binding with binary encoding is nice if you want to do binary encoding of the message. In fact, this is the default binding that is created when you use a Silverlight enabled WCF file template in Visual Studio 2008 to create a WCF service. Binary encoding often offers performance gains over text encoding. Here is a quick glimpse at the config setup for the binding</p>  <div style="border-bottom: silver 1px solid; text-align: left; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">   <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">     <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px"><span style="color: #0000ff">&lt;</span><span style="color: #800000">system.serviceModel</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">&lt;</span><span style="color: #800000">behaviors</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">        <span style="color: #0000ff">&lt;</span><span style="color: #800000">serviceBehaviors</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">            <span style="color: #0000ff">&lt;</span><span style="color: #800000">behavior</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">=&quot;SilverlightApplication2.Web.Service1Behavior&quot;</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">                <span style="color: #0000ff">&lt;</span><span style="color: #800000">serviceMetadata</span> <span style="color: #ff0000">httpGetEnabled</span><span style="color: #0000ff">=&quot;true&quot;</span> <span style="color: #0000ff">/&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">                <span style="color: #0000ff">&lt;</span><span style="color: #800000">serviceDebug</span> <span style="color: #ff0000">includeExceptionDetailInFaults</span><span style="color: #0000ff">=&quot;false&quot;</span> <span style="color: #0000ff">/&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">            <span style="color: #0000ff">&lt;/</span><span style="color: #800000">behavior</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">        <span style="color: #0000ff">&lt;/</span><span style="color: #800000">serviceBehaviors</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">&lt;/</span><span style="color: #800000">behaviors</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">&lt;</span><span style="color: #800000">bindings</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">        <span style="color: #0000ff">&lt;</span><span style="color: #800000">customBinding</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">            <span style="color: #0000ff">&lt;</span><span style="color: #800000">binding</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">=&quot;customBinding0&quot;</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">                <span style="color: #0000ff">&lt;</span><span style="color: #800000">binaryMessageEncoding</span> <span style="color: #0000ff">/&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">                <span style="color: #0000ff">&lt;</span><span style="color: #800000">httpTransport</span> <span style="color: #0000ff">/&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">            <span style="color: #0000ff">&lt;/</span><span style="color: #800000">binding</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">        <span style="color: #0000ff">&lt;/</span><span style="color: #800000">customBinding</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">&lt;/</span><span style="color: #800000">bindings</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">&lt;</span><span style="color: #800000">serviceHostingEnvironment</span> <span style="color: #ff0000">aspNetCompatibilityEnabled</span><span style="color: #0000ff">=&quot;true&quot;</span> <span style="color: #0000ff">/&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">&lt;</span><span style="color: #800000">services</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">        <span style="color: #0000ff">&lt;</span><span style="color: #800000">service</span> <span style="color: #ff0000">behaviorConfiguration</span><span style="color: #0000ff">=&quot;SilverlightApplication2.Web.Service1Behavior&quot;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">            <span style="color: #ff0000">name</span><span style="color: #0000ff">=&quot;SilverlightApplication2.Web.Service1&quot;</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">            <span style="color: #0000ff">&lt;</span><span style="color: #800000">endpoint</span> <span style="color: #ff0000">address</span><span style="color: #0000ff">=&quot;&quot;</span> <span style="color: #ff0000">binding</span><span style="color: #0000ff">=&quot;customBinding&quot;</span> <span style="color: #ff0000">bindingConfiguration</span><span style="color: #0000ff">=&quot;customBinding0&quot;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">                <span style="color: #ff0000">contract</span><span style="color: #0000ff">=&quot;SilverlightApplication2.Web.Service1&quot;</span> <span style="color: #0000ff">/&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">            <span style="color: #0000ff">&lt;</span><span style="color: #800000">endpoint</span> <span style="color: #ff0000">address</span><span style="color: #0000ff">=&quot;mex&quot;</span> <span style="color: #ff0000">binding</span><span style="color: #0000ff">=&quot;mexHttpBinding&quot;</span> <span style="color: #ff0000">contract</span><span style="color: #0000ff">=&quot;IMetadataExchange&quot;</span> <span style="color: #0000ff">/&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">        <span style="color: #0000ff">&lt;/</span><span style="color: #800000">service</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">&lt;/</span><span style="color: #800000">services</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF-->
<pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px"><span style="color: #0000ff">&lt;/</span><span style="color: #800000">system.serviceModel</span><span style="color: #0000ff">&gt;</span></pre>
<!--CRLF--></div>
</div>
<p>&#160;</p>
<p></p>
<p></p>
<p>There is a <a href="http://blogs.msdn.com/silverlightws/archive/2009/03/20/what-s-new-with-web-services-in-silverlight-3-beta.aspx" target="_blank">nice blog post from Yavor Georgiev</a>, (Program Manager on the Connected Framework Team) that explains this in more detail. You can also <a href="http://videos.visitmix.com/MIX09/T42F" target="_blank">view Eugene Ovosvetsky’s (also of Microsoft) presenting his Consuming Web Services in Silverlight 3 session at Mix 2009</a> … this session covers binary encoding as well as other new networking features.</p>
