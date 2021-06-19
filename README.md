# XSS-Reflector [<img src="https://raw.githubusercontent.com/duckstroms/xss-reflector/8fd48776a6d577af1c3e701ea240ea8135dc2d6d/screenshot/release-v2.0-blue.svg">](https://github.com/duckstroms/xss-reflector/releases/tag/xss) 
    

# Description
Burp Suite extension is able to find reflected XSS on page in real-time while browsing on web-site and include some features as:
* Highlighting of reflection in the response tab.
* Test which symbols is allowed in this reflection.
* Analyze  of reflection context.
* Content-Type whitelist.
 
 
 # How to use
After plugin install you just need to start work with the tested web-application. Every time when reflection is found, reflector defines severity and generates burp issue.
![reflector usage](https://raw.githubusercontent.com/duckstroms/xss-reflector/main/screenshot/reflector_demo1.gif)

Each burp issue includes detailed info about reflected parameter, such as:
* Symbols that allowed in this reflection.
* Highlighting of reflection value in response.
* Reflection context analyze.

# Allowed symbols analyse
![reflector usage](https://raw.githubusercontent.com/duckstroms/xss-reflector/main/screenshot/symbols_analyse.png)
When the reflection is found and option "Aggressive mode" is activated, the reflector will check which of special-symbols are displayed on this page from vulnerable parameters. For this action, reflector compose additional requests for each reflected parameter. In example, while we were working with elkokc.ml website reflector are generated issue with a detailed information about reflection. There are 3 reflection for "search" parameter and each of them pass special symbols. Because of the possibility of displaying special characters issue severity is marked as high. Every time when reflection is found reflector define severity and generate burp issue.

# Context analyse
In the "Check context" mode  reflector it's not only show special characters that are reflected to the page, but also figure out a character that allows to break the syntax in the page code. In example you may see server response by reflector extension. Parameter "search" was send with a payload  - p@y<"'p@y. As a result, it was reflected a few times in a different contexts. 
* reflection with next characters - ',", <  and the double quote  allow to exit from this context and write HTML code.
* reflection with next characters - ", <  and the bracket allow to inject HTML-tags. 
* reflection with next characters -  ',", < and the single quote allow to exit from js variable context and write malicious code.

![reflector usage](https://raw.githubusercontent.com/duckstroms/xss-reflector/main/screenshot/aggressivemode_context.png)

In the issue information it's marked as: 
* Context char - character that allows to breake the syntax.
* Other chars - other chars that are reflected without context.
![reflector usage](https://raw.githubusercontent.com/duckstroms/xss-reflector/main/screenshot/aggressivemode_context_burp.png)

# Reflection navigation
Navigation by arrow buttons in the response tab.
![reflector usage](https://raw.githubusercontent.com/duckstroms/xss-reflector/main/screenshot/navigation.gif)

# Settings
* Scope only - allow reflector to work only with a scope added websites.
* Agressive mode - reflector generates additional request with a test payload .
* Check context - activate check context mode.

Moreover you can manage content-types whitelist with which  reflector plugin should work. But if you will use another types except text/html,  this can lead to slowdowns in work.
![reflector usage](https://raw.githubusercontent.com/duckstroms/xss-reflector/main/screenshot/settings.png)

# How to compile
Compiled by jdk 1.7

Example:

* javac.exe -d build src/burp/*.java

* jar.exe cf plugin.jar -C build burp

# Authors
*  Andri Wahyudi (GitHub: ! [duckstroms](https://github.com/duckstroms))
*  Stregh Streek  (GitHub: ! [streghstreek](https://github.com/streghstreek))
