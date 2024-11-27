---
date: 2024-09-28
authors:
  - saeidamiri1
title: Cheat sheet for markdown.  
description: Cheat sheet for markdown.
categories:
  - Markdown
---

# Cheat sheet for markdown (Basics)

This Markdown cheat sheet provides a basic overview of all the Markdown.
<!-- more -->

- - - -
## Heading 1
How: 
```
 # Heading 1
```
### Heading 2
How: 
```
 ## Heading 2
```
#### Heading 3
How: 
```
 ### Heading 3
```
##### Heading 4
How: 
```
 #### Heading 4
```
###### Heading 5
How: 
```
 ##### Heading 5
```

## Emphasis 
*Italic text*
How:
```
 *Italic text* or _Italic text_
```
**Bold text**
How:
```
 **Bold text** or __Bold text__
```

==Highlight==

How:
```
==Highlight==
```

~~Strikethrough~~

How:
```
~~Strikethrough~~
```

> blockquote
>> nested blockquote

How:
```
> blockquote
>> nested blockquote
```

<span style="color:red">Color</span>

How: 
```
<span style="color:red">Color</span>
```

## Link 

[Link](http://www.google.com/)

How: 
```
[Link](http://www.google.com/)
```

## Code
inline `code`
multiple lines of ```codes```

How:
```
 `code`   
    ```
       codes
    ```
```

## List

Unordered List <br>
<ul>
  <li> Bullet
    <ul>
      <li>sub bullet</li>
       <ul>
          <li>sub sub bullet</li>
       </ul>
      <li>sub bullet</li>
    </ul>
  </li>
</ul>


How:
```
Unordered List
- Bullet
  - sub bullet
    -  sub sub bullet
  - sub bullet
```

1. Numbered list
    1. Sub numbered list
    2. Sub numbered kist


How:
```
1. Numbered list
    1. Sub numbered list
    2. Sub numbered kist
```

Task List
- [ ] An uncompleted task
- [x] A completed task

How:
```
- [ ] An uncompleted task
- [x] A completed task
```

_Horizontal line :_

-----

How:
```
-----
```

## Latex
LATEX

![E_0=mc^2](https://latex.codecogs.com/svg.latex?E_0=mc^2)


<img src="https://tex.s2cms.ru/svg/E_0=mc^2" alt="E_0=mc^2" />

How:
```
![E_0=mc^2](https://latex.codecogs.com/svg.latex?E_0=mc^2)

<img src="https://tex.s2cms.ru/svg/E_0=mc^2" alt="E_0=mc^2" />
```

## Table
Table:

header 1  | header 2
-------   | -------
Row 1     |  Values
Row 2 <br> continue    |  Values

How:
```
header 1  | header 2
-------   | -------
Row 1     |  Values
Row 2 <br> continue    |  Values
```

## Image
_Image:_

![picture](https://raw.githubusercontent.com/saeidamiri1/saeidamiri1.github.io/master/public/favicon.ico)

How:
```
![picture](https://raw.githubusercontent.com/saeidamiri1/saeidamiri1.github.io/master/public/favicon.ico)
```

## Foldable text

<details>
<summary>Hidden materials</summary>
<p> Put text here </p>
</details>
How:
```
<details>
<summary>Hidden materials</summary>
<p> Put text here </p>
</details>
```

## Emoji and Hotkey

:+1:

How:
```
  :+1:
```
The complete list can be found at [emoji list](https://www.webfx.com/tools/emoji-cheat-sheet/)


Hotkey:
<kbd>⌘C</kbd>

How:
```
  <kbd>⌘C</kbd>
```

common hotkey:
⌥(Option)⌃(Control)⌘(Command)⇧(Shift)⇪(Caps Lock)
⇥(Tab) ↩(Return) ⌫(Delete)↑(Up)↓(Down)←(Left)→ (right)

## miscellaneous
### Comment
<!--
Does not show
-->

How:
```
<!--
 Does not show
-->
```

### indent
&nbsp; with indent 

How: 
```
&nbsp; with indent 
```

### Footnotes
Need more [^1] to say.<br>
[^1]: This is the Footnote.

### New line 
<br/>
How: 
```
<br/>
```

## Useful references
-[ref1]:  https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
