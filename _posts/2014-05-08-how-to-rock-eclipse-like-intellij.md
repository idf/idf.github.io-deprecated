---
layout: post
title: "How to Rock Eclipse Like IntelliJ"
description: "Handy configurations in Eclipse"
category: Computer Science 
tags: []
---
{% include JB/setup %}
## IntelliJ
Okay okay, IntelliJ is great and almost perfect, but at the price USD $499. Additionally, The company I am interning does not offer IntelliJ but Eclipse. To make the things worse, most of the professors are using Eclipse, and my peers are using Eclipse writing their projects. There is little [Network Effect](http://en.wikipedia.org/wiki/Network_effect) using IntelliJ. However, IntelliJ is great, auto-completion, smart-saving, out-of box class file viewers, and etc. 

## Do Some Tinkering on Eclipse 

All IDEs have good parts and bad parts. Let me bring the good parts of IntelliJ to mitigate the bad parts of Eclipse. 

### IntelliJ-like auto-completion
Go to `Window -> Preferences -> Java -> Editor -> Content Assits`. In the column "Auto activation triggers for Java", enter this: `.qwertyuioplkjhgfdsazxcvbnm_QWERTYUIOPLKJHGFDSAZXCVBNM`

### Emacs Key Binding
Keymap scheme choose "Emacs" (or whatever you prefer).

### Save on Build
`Window -> Preferences -> General -> Workspace` and there you can check "Save automatically before build" + "Build automatically"  

As well as: `Preferences -> Run/Debug -> Launching` "Save dirty editors before launching".

### IntelliJ-like Auto Save
Plug-in from marketplace: [smartsave](http://marketplace.eclipse.org/content/smart-save#.U1Nle_mSz0B).

### Mark Variable occurrences
`Window -> preferences -> java -> editor -> mark occurrences`. And check all available options.  

Also need to change the coloring: `Preferences -> General -> Editors -> Text Editors -> Annotations`.  
In there compare the settings for "Occurences" and "Write Occurrences" and ensure that you don't have the "Text as highlighted" options checked for one of them. 

### View Class File 
Use the Jd [plug-in](http://jd.benow.ca/#jd-eclipse).

Additionall, to add file association: 

* `General -> Editors -> File Associationn`  
* Select "*.class" and mark "Class File Editor" as default  
* Select "*.class without source" -> Add -> "Class File Editor" -> Make it as default  

### Export Settings
Settings can be exported to a file using `File -> Export -> Preferences`, and you can import it to another Eclipse workspace.

## You are here
Yeah, Rock the Eclipse!!!