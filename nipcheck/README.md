[pickit table of content](https://github.com/blizzhackers/pickits/#pickits)

[Nipper](https://github.com/blizzhackers/pickits/nipper/readme.md)

---

# NipCheck
by [@noah-](https://github.com/noah-)

### features

* detect and report syntax errors. Detect and report unknown keywords. Fully offline checker, no need to run d2bs.
* auto-complete Syntax Highlighting
* all unrecognized syntax will show up as red text with underline.

### download

* <https://github.com/noah-/NipCheck/archive/master.zip>
* <https://github.com/blizzhackers/pickits/raw/master/nipcheck/notepad++.zip>

### download includes

* NipCheck.dll
* NIP.xml
* userDefineLanguage.xml

### installation

1. extract NipCheck.dll in a new created subfolder ...\Notepad++\plugins\NipCheck\

1. extract NIP.xml in ...\Notepad++\plugins\APIs\

1. extract and rename userDefineLang.xml in ...\Notepad++\userDefineLangs\userDefineLang-nipcheck.xml

### check settings

Once you open Notepad++, go to Settings > Preferences... and set the following settings to see auto-complete:
![nipcheck1](assets/nipcheck1.png)

### using NipCheck

Open a nip file in np++. Go to Plugins > NipCheck > Run. Alternative way to start it is to use the diablo 2 icon on your np++ commands bar.
If NipCheck plugin isn't listed, that can happen after you upgrade np++ to a newer version, go to > Settings > Import pluging(s)... and browse to the NipCheck.dll, restart np++ and it's ok.

Here is an image showing auto-complete, syntax highlighting, and error checking:
![nipcheck2](assets/nipcheck2.png)

For viewing nip files, you can choose **NIP** from the Language np++ menu.

### known bugs

If you get this error:
```
Syntax Errors: Argument invalid in ArithmeticOperator.Eval - Invalid Expression: lhs
```
be sure if you downloaded the latest NipCheck files. 
If the error persists and you are sure about the validity of the expression, maybe some updates should be made to NIP.xml and Constants.cs (and also a new compiled NipCheck.dll).

### history

* [initial shared topic](https://web.archive.org/web/20180324041959/http://www.blizzhackers.cc:80/viewtopic.php?f=182&t=495129)
