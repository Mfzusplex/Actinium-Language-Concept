
---

# Actinium Language (ACTL)

## Introduction

**Actinium**, abbreviated **ACTL**, is a dynamic and extended version of **Markdown**. It expands Markdown’s syntax to add more versatility and power.

It was proposed in **November 2025** by **Absalom74** on GitHub as a conceptual **front-end scripting language** inspired by **HTML** and **Markdown**.

---

## Basic Syntax

### 1. `setup`

Initializes the document and starts the text program:

```txt
setup[title: 'Document 1' author: 'John']
```

### 2. `sector`

Defines a hidden logical sector (similar to a heading):

```txt
sector['sector name']{}
```

### 3. `dis`

Displays text. It accepts several formatting parameters:

```txt
dis 'hello world' >none          ;; no format
dis 'heading 1' >head            ;; heading
dis 'main subtitle' >sub1
dis 'subsubtitle' >sub2
dis 'subsubsubtitle' >sub3
dis 'preformatted' >pf
dis 'code' >code
dis 'basic table element' >table{col1, line1}
dis 'coloured text' >none %hex:FFFFFF%
dis 'variable: &var&' >none      ;; displays variable
```

### 4. `table`

Displays a table. It supports the same parameters as `dis`:

```txt
table['Table Name{hidden/shown}']{n of columns, n of lines}:
  dis 'element 1' >table{col1, line1} %hex:AAAFFF%
  dis 'element 2' >table{col2, line1} >pf
```

---

## Variables

### 1. Creating variables (bunches)

Variables are stored in **bunches** using `assign`:

```txt
assign{'name'<class>'value'}{'name2<class>'value'}
```

### 2. Real-time arithmetic

```txt
'n'++'name'    ;; increase by n  
'n'--'name'    ;; decrease by n
```

### 3. Math plugin

```txt
plugin -math
sqr_to[name]   ;; square of a variable
cos_to[name]   ;; cosine of a variable
```

---

## Functions and Loops

Example loop inside a `thread`:

```txt
assign{'i'<integer>'1'}        ;; create integer

thread{loops=i}['name'] {      ;; 1 loop initially
  1++i                         ;; makes the loop infinite
}

call thread['name']
```

---

## Examples

### 1. Infinite increment

```txt
assign{'i'<integer>'1'}

thread{loops=i}['example'] {
  1++i
  dis 'number: &i&' >head
}
```

### 2. Full Actinium document

```txt
plugin -math

assign{'username'<string>'Michael'}
assign{'number'<integer>'60'}
assign{'spacing'<string>'			'}

thread{loops=1}['MyDocument'] {
  dis 'My Document' >head
  dis 'Hello &username&, welcome to my document' >sub2
  dis 'Here we have the cosine of 60' >sub3
  cos_to['number']                  ;; outputs 0.5

  dis '&number&' >sub2
  dis '&spacing&' >head             ;; separation 1

  dis 'Here we have a basic multiplication table' >sub3

  table['Multiplication{shown}']{3, 2}:
    dis 'x 1' >table{col1, line1} >sub2
    dis 'x 2' >table{col2, line1} >sub2
    dis 'x 3' >table{col3, line1} >sub2
    dis '1'   >table{col1, line2} >sub2
    dis '4'   >table{col2, line2} >sub2
    dis '6'   >table{col3, line2} >sub2

  dis 'Do you like the color cyan?' >sub3 %hex:00FFFF%
  dis '&spacing&' >head             ;; separation 2

  dis 'End of my example document.' >sub1
}
```

---

## Interpreter

Actinium will be executed through a **Python 3.14 interpreter**.

It can also be **converted** naturally into:

* **HTML**
* **Markdown**

---
