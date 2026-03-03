# counterx.fscss

Simple FSCSS percentage counter animation plugin.

Counterx generates full @keyframes percentage steps (0% → 100%) using FSCSS arrays. It allows you to create animated text counters without JavaScript.

---

### 📦 implementation 

1. Include FSCSS or via CLI 

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.14/exec.min.js" async></script>
```

2. Import Counterx

```css
@import(exec(_init counterx))
```

Since Counterx is a .fscss file, you do NOT need to include the extension.

Note: If a plugin uses another extension like .css or .xfscss, you must specify it:

```css
@import(exec(_init myplugin/css))
```

---

### 🚀 Basic Usage

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.14/exec.min.js" async></script>

<style>
@import(exec(_init counterx))

h2:after {
  content: "...";
  animation: count 10s steps(100) forwards;
}

@keyframes count {
  counter-init
}
</style>

<h2>Process</h2>
```

**This generates:**

```
0%
1%
2%
...
100%
```

With smooth step-based animation using steps(100).

---

#### ⚙️ How It Works**

**Counterx uses:**

```scss
@arr numlist[count(99)]
```

**And internally expands to:**

· 0%
· 1–99%
· 100%

**Using special array helpers:**

· array!.first → 0%
· array[2] → 1–99%
· array!.last → 100%

---

**✏️ Customizing Text Output**

Counterx uses an internal array:

```scss
@arr counter-before[ing...,ing...,ed]
```

**Index meaning:**

· first → applied at 0%
· second → applied at 1–99%
· last → applied at 100%

**Default output:**

```
ing...0%
ing...1%
...
ing...99%
ed
```

---

#### 🎯 Remove Prefix / Suffix

If you want only pure numbers:

```css
@import(exec(_init counterx))

/* Override the counter-before array */
@arr counter-before[,,100%]

h2:after {
  content: "...";
  animation: count 10s steps(100) forwards;
}

@keyframes count {
  counter-init
}
```

**Now it becomes:**

```
0%
1%
2%
...
100%
```

---

## 💡 Why Counterx?

Feature Benefit
No JavaScript Pure CSS solution
No manual keyframes Write 1 line, generate 100+
Compile-time generation Zero runtime overhead
CSS `steps()` compatible Smooth tick-by-tick animation
Lightweight Minimal code footprint
Fully customizable Arrays for complete control

---

### ⏱️ Recommended Animation

```css
animation: count 10s steps(100) forwards;
```

Using steps(100) makes the counter tick like a real progress indicator—one step per percentage point.

---

### 🌟 Complete Example

```html
<!DOCTYPE html>
<html>
<head>
  <script src="https://cdn.jsdelivr.net/npm/fscss@1.1.14/exec.min.js" async></script>
  <style>
  @import(exec(_init counterx))
  
  body {
    background: #121212;
    padding: 20px;
    color: #ddd;
    font-family: system-ui, sans-serif;
  }
  
  h2:after {
    content: "...";
    animation: count 5s steps(100) forwards;
  }
  
  @keyframes count {
    counter-init
  }
  </style>
</head>
<body>
  <h2>Download</h2>
</body>
</html>
```

---

## 🔧 Custom Counter Array

Want different text? Override the counter-before array:

```css
@import(exec(_init counterx))

/* Format: [0% text, 1-99% text, 100% text] */
@arr counter-before[Starting...,Loading...,Complete!]

h2:after {
  content: "...";
  animation: count 5s steps(100) forwards;
}

@keyframes count {
  counter-init
}
```

Output:

```
Starting...0%
Loading...1%
Loading...2%
...
Loading...99%
Complete!
```

---

## 📁 Source Code
https://github.com/fscss-ttr/FSCSS/blob/main/xf/styles/counterx.fscss
```scss
/* name "counterx/fscss" use "counter\-init" */

@arr numlist[count(99)]
@arr counter-before[ing...,ing...,ed] 

str(counter-init, "
    0%{
      content: '@arr.counter-before!.first0%'
    } 
    @arr.numlist[]%{
      content: '@arr.counter-before[2]@arr.numlist[]%';
    } 
    100%{
      content: '@arr.counter-before!.last';
    }"
)
```

---

🎨 Plugin Info

- Name: counterx
- Extension: .fscss (no need to specify when importing)
- Directive: counter-init
- ependencies: FSCSS v1.1.14+

---

## 📋 Summary

Counterx is part of the FSCSS plugin ecosystem. It transforms this:

```css
@keyframes count {
  counter-init
}
```

Into 101 keyframes automatically.

Simple. Declarative. Generated. 🎯

---

## 🔗 Related

- fscss.devtem.org
- More coming soon!

---

**Made with ❤️**
