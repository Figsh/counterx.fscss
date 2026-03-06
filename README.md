# counterx.fscss

*Simple FSCSS percentage counter animation plugin (v1.1.15+)*

Counterx generates full @keyframes percentage steps (0% → 100%) using FSCSS arrays and the new @define system. Create animated text counters without JavaScript.

---

# 📦 Installation

1. Include FSCSS (via CDN or CLI)

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.15/exec.min.js" async></script>
```

2. Import Counterx

```css
@import(exec(_init counterx))
```

Since Counterx is a .fscss file, you do not need to include the extension.

> Note: If a plugin uses another extension like .css or .xfscss, you must specify it:

```css
@import(exec(_init myplugin/css))
```

---

### 🚀 Basic Usage

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.15/exec.min.js" async></script>

<style>
@import(exec(_init counterx))

h2:after {
  content: "...";
  animation: count 10s steps(100) forwards;
}

@keyframes count {
  @counter-init()
}
</style>

<h2>Process</h2>
```

Output Generated:

```
0%
1%
2%
...
99%
100%
```

With smooth step-based animation using steps(100).

---

⚙️ How It Works

Counterx uses FSCSS arrays and the @define system (v1.1.15+):

```scss
@arr numlist[count(99)]           /* Generates 1–99 */

@define counter-init(start: ing..., process: ing..., end: ed) {
  "
  0% {
    content: '@use(start)0%'
  }
  @arr.numlist[]% {
    content: '@use(process)@arr.numlist[]%';
  }
  100% {
    content: '@use(end)';
  }
  "
}
```

### Array Structure:

· @arr.numlist → generates numbers 1–99 using count(99)

---

### ✏️ Customizing Text Output

Default Output:

```
ing...0%
ing...1%
...
ing...99%
ed
```

Customize with Parameters:

```css
@import(exec(_init counterx))

h2:after {
  content: "...";
  animation: count 5s steps(100) forwards;
}

@keyframes count {
  @counter-init( Starting...,Loading...,Complete!)
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

## 💡 Why Counterx?

Feature Benefit
No JavaScript Pure CSS solution
No manual keyframes Write 1 line, generate 100+
Compile-time generation Zero runtime overhead
CSS steps() compatible Smooth tick-by-tick animation
Lightweight Minimal code footprint
Parameter support Fully customizable via @define
Plugin ecosystem Part of FSCSS plugin system

---

### ⏱️ Recommended Animation

```css
animation: count 10s steps(100) forwards;
```

Using steps(100) makes the counter tick like a real progress indicator—one step per percentage point.

---

🌟 Complete Example

```html
<!DOCTYPE html>
<html>
<head>
  <script src="https://cdn.jsdelivr.net/npm/fscss@1.1.15/exec.min.js" async></script>
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
    @counter-init(⏳ Starting..., 📦 Loading..., ✅ Complete!)
  }
  </style>
</head>
<body>
  <h2>Download Progress </h2>
</body>
</html>
```

---

## 📁 Source Code

File: counterx.fscss 
FSCSS: (v1.1.15+)

```scss
/* name "counterx/fscss" use "@counter\-init()" version 1.1.15+ */

exec(_log, "counterx.fscss linked\nUse @counter\-init() inside @keyframes\nSupported version: 1.1.15+")

@arr numlist[count(99)]

@define counter-init(start: ing..., process: ing..., end: ed) {
  "
  0% {
    content: '@use(start)0%'
  }
  @arr.numlist[]% {
    content: '@use(process)@arr.numlist[]%';
  }
  100% {
    content: '@use(end)';
  }
  "
}
```

Repository:
https://github.com/fscss-ttr/FSCSS/blob/main/xf/styles/counterx.fscss

---

## 🎨 Plugin Info

Property Value
Name counterx
Extension .fscss (no need to specify when importing)
Directive @counter-init()
Version 1.1.15+
Dependencies FSCSS v1.1.15+
Parameters start, process, end (all optional)

---

## 📋 Summary

Counterx is part of the FSCSS plugin ecosystem. Using the new @define system (v1.1.15+), it transforms this:

```css
@keyframes count {
  @counter-init(start: "Starting...", process: "Loading...", end: "Done!")
}
```

Into 101 keyframes automatically.

Simple. Declarative. Generated. 🎯

---

🔗 Related

- FSCSS Documentation: https://fscss.devtem.org
- FSCSS @define Method: https://fscss.devtem.org/define 
- FSCSS Arrays: https://fscss.devtem.org/arrays 
- More Plugins Coming Soon!

---

## 📝 Changelog

v1.1.15+ (Current)

· Migrated to @define system
· Added parameter support (start, process, end)
· Improved flexibility and customization
· Better error handling and logging

v1.1.14 (Legacy)

· Original array-based implementation
· Fixed array indexing

---

Made with ❤️
