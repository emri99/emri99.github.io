---
layout: page
title: "Incomplete download on some browsers"
categories: web-development
permalink: /incomplete-download/
---
## The bug

After updating symfony website, document download fails on some browsers.
It make me feel like connection was stopped during download and/or never finish.

Browsers test result:

|State|Device/Browser|Description|
|---|---|---|
| ✅ | MacOSX Chrome | no problem |
| ❌ | MacOSX Safari | incomplete download. `safari can't open the file because is still being downloaded.`|
| ❌ | MacOSX Firefox | download don't start. Message box indicate that file does not exists or has been moved when download path selector window appears |
| ❌ | IOS Chrome | Page cannot be opened. `ERR_INVALID_RESPONSE` warning |
| ❌ | IOS Safari | failed without much more informations | 
| ❌ | IOS Device | From what I've notice almost every support ticket reporting bug is from IOS mobile, whatever browser used|

Investigation states that:
* no errors in logs files (application, webserver, or php-fpm)
* response http status was 200 in any case
* no noticeable differences can be found in request/response headers between ok & ko responses  

> Weird thing: this does not happens on all our servers, I still haven't figured out why...

## The problem

**The front controller `index.php` was having an empty line outside of php tags at the beginning.**  
Remove it did the trick! Simple as that.  
Noob error ! F*ck...

![image](https://media.giphy.com/media/COYGe9rZvfiaQ/giphy.gif)

---
