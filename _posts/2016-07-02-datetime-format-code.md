---
layout: post
title: Cheat Sheet: Date(Time) Format Code for Python
category : 写代码
tagline: "Supporting tagline"
tags : [工具, Cheat Sheet, Python]
---
{% include JB/setup %}

### Python

**Conversion between String and Datetime**

	# string to datetime
	from datetime import datetime
	str = '2016-07-02'
	dt = datetime.strptime(str, '%Y-%m-%d')

	# datetime format string
	str = dt.strftime('%Y-%m-%d')

	# smart parser
	from dateutil.parser import parse
	parse('Jan 31, 1997 10:45 PM')
	parse('6/12/2011', dayfirst=True)

**Datetime Format Code**
	
	Type    Description
	-----   ------------------------------------------
	%Y      4-digit year 
	%y      2-digit year
	%m      2-digit month [01, 12]
	%d      2-digit day [01, 31] 
	%H      Hour (24-hour clock) [00, 23] 
	%I      Hour (12-hour clock) [01, 12]
	%M      2-digit minute [00, 59] 
	%S      Second [00, 61] (seconds 60, 61 account for leap seconds) 
	%w      Weekday as integer [0 (Sunday), 6]
	
	%U      Week number of the year [00, 53]. 
			Sunday is considered the first day of the week, and days before the first Sunday are “week 0”.
	%W      Week number of the year [00, 53]. 
			Monday is considered the first day of the week, and days before the first Monday are “week 0”.
	%z      UTC time zone offset as +HHMM or -HHMM, empty if time zone naive 
	%F      Shortcut for %Y-%m-%d, for example 2012-4-18 
	%D      Shortcut for %m/%d/%y, for example 04/18/12
	
	*Locale-specific date formatting Type
	Type    Description
	-----   ------------------------------------------
	%a      Abbreviated weekday name
	%A      Full weekday name
	%b      Abbreviated month name
	%B      Full month name
	%c      Full date and time, for example ‘Tue 01 May 2012 04:20:57 PM’
	%p      Locale equivalent of AM or PM
	%x      Locale-appropriate formatted date; e.g. in US May 1, 2012 yields ’05/01/2012’
	%X      Locale-appropriate time, e.g. ’04:24:12 PM’
 
 
 




