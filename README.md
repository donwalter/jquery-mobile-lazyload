jQuery Mobile LazyLoad
------------------------
jQuery Mobile LazyLoad - LazyLoad/Infinite Scrolling plugin for jQuery Mobile listviews, uses Ajax for pulling in more records

Usage
-----
Include the following file:
```html
<script type="text/javascript" src="js/jquery-mobile-lazyload.js"></script>
```

Your listview will consist of 2 parts... the `<ul>` tag, and an include file that generates the `<li>` elements
List file:
```coldfusion
<ul data-role="listview" id="dataList" class="lazyload">
  <cfinclude template="getdata.cfm" />
</ul>
```

Include file:
```coldfusion
<cfsetting showdebugoutput="false">

<cfparam name="url.startrow" default="1">
<cfparam name="url.maxrows" default="20">

<cfset variables.results = objMobile.GetDataList(parameters)>

<cfset variables.inc = url.startrow + 1>
<cfoutput query="variables.results" startrow="#url.startrow#" maxrows="#url.maxrows#">
	<li data-inc="#variables.inc#">
		<a href="details.cfm?#variables.results.dataid#">
			#variables.results.display#
		</a>
	</li>

	<cfset variables.inc++>
</cfoutput>
```

Then add this to initiate the LazyLoad:
```javascript
$(function(){
  $('.lazyload').lazyLoad('getdata.cfm');
});
```

Demo
----


License
-------
Copyright (c) 2013 Don Walter. Licensed under the MIT license.
