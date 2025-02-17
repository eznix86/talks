---
theme: default
background: ./images/splash.png
title: Welcome to Slidev
info: |
  ## An exploration of PHP's capabilities with native code through FFI and extensions
  ## Laravel Moris 15 Feb 2025 
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# An exploration of PHP's capabilities with native code through FFI and extensions

Laravel Moris 15 Feb 2025

<div class="abs-bl m-6 text-xl">
  <a href="#" class="slidev-icon-btn text-blue">
    <carbon:logo-twitter />
  </a>
  <a href="#" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
  <a href="#" class="slidev-icon-btn">
    <carbon:logo-linkedin />
  </a>
</div>

---
transition: fade-out
layout: intro
---

## `$~ whoami`

# Bruno Bernard
Consultant | Software Engineer | Open Source Enthusiast

<div class="leading-8 opacity-80">
  <p>Worked with <b v-mark.underline.blue="1">~20 companies</b> worldwide</p>
  <p>Loves <span v-mark.highlight.red="1">Traveling and Hiking</span></p>
  <p>Likes to talk ....<span v-mark.circle.orange="1">a lot</span></p>
  <p>Discovered Laravel <span v-mark.strike-through.red="1">from Technical Debt</span> and Love it</p>
</div>

<div class="my-10 grid grid-cols-[40px_1fr] w-min gap-y-4">
  <carbon:logo-github/>
  <div><a href="https://github.com/eznix86" target="_blank">eznix86</a></div>
  <carbon:logo-twitter class="text-blue"/>
  <div><a href="https://twitter.com/eznix86" target="_blank">eznix86</a></div>
</div>

<img src="https://avatars.githubusercontent.com/u/26553194?v=4" class="rounded-full w-40 abs-tr mt-16 mr-12"/>
<img src="./images/qr-bruno.png" class="rounded-5 w-40 abs-tr mt-80 mr-12"/>

---
transition: slide-up
level: 2
layout: center
---

# “PHP <span class="text-bold" v-mark.box.green> isn’t limited</span> to the web!”

- It can integrate deeply with external libraries
- and It is not dead

---
transition: slide-up
level: 2
layout: center
---

# What can you with PHP <span v-mark.highlight.blue>`#Today`</span> ?

---
transition: slide-up
level: 2
layout: image-right
image: ./images/lambo.jpeg
---

# Web
<br>
<br>

## Your Million Dollar SaaS
<br>
<br>

- Everybody knows that...

- $ in PHP stands for money


---
transition: slide-up
level: 2
layout: image-right
image: ./images/asciinema.gif
backgroundSize: contain
---

# Command-Line
<br>
<br>

## Laravel Zero
<br>
<br>

- Those who live only in the terminal

- Why buttons when you can do it with commands?

---
transition: slide-up
level: 2
layout: image-right
image: ./images/desktop.png
backgroundSize: cover
---

# Desktop Application
<br>
<br>

## Native PHP
<br>
<br>

- Applications that run on your desktop
- Windows, Linux, or Mac


---
transition: slide-up
level: 2
layout: image-right
image: ./images/app.png
backgroundSize: contain
---

# Mobile Apps ?

Simon Hamp from Native PHP

- He did it !

<Youtube id="wRIPYEwa8G4" class="full"/>

---
transition: slide-up
level: 2
layout: center
---

# How he <span v-mark.highlight.blue>did it</span> ?


---
transition: slide-up
level: 2
layout: center
---

# Laravel <span v-mark.highlight.red="1">Extensions</span> and <span v-mark.highlight.blue="1">FFI</span>


---
layout: image-right
image: https://cover.sli.dev
---
# PHP Extensions

A PHP extension is compiled code (typically written in C) that hooks directly into PHP’s core.

But you can use Rust.

```rs{all|2|4,5,6,7|9|10}{lines:true}
#![cfg_attr(windows, feature(abi_vectorcall))]
use ext_php_rs::prelude::*;

#[php_function]
pub fn hello_world(name: &str) -> String {
    format!("Hello, {}!", name)
}

// compile the extension
// update php.ini to load the extension
```

```php{hide|all}{lines:true}
<?php

  var_dump(hello_world("Laravel Moris"));
```

---
level: 2
---

# Extensions You Know

## Déjà vu

- `php-mysql`: MySQL database integration for PHP.
- `php-zip`: ZIP archive support for PHP.
- `php-gd`: GD extension for PHP (image processing).
- `php-curl`: cURL extension for PHP (URL transfers).
- `php-xml`: XML support for PHP.
- `openssl`: OpenSSL toolkit (used by PHP for encryption).

... Many more, it can be C or Rust or Anything!

---
layout: image-right
image: https://cover.sli.dev
---
# PHP FFI (as of PHP 7.4)

- Means <span v-mark.highlight.red="1">Foreign Function Interface</span>
- Bind directly to libraries.

You don't have to think about PHP, just write your library and call what you need.

```c{all|3,4,5|all}{lines:true}
#include <stdio.h>

int multiply(int a, int b) {
    return a * b;
}
// compile the extension
```

```php{hide|3,4,5|7,8,9|all}{lines:true}
<?php
// Load the C function into PHP
$ffi = FFI::cdef("
    int multiply(int a, int b);
", "./mylib.so");

$result = $ffi->multiply(6, 7);
echo "Result: $result\n";  // Result: 42
?>
```

---
layout: image-right
image: ./images/libsql.png
backgroundSize: contain
---
# PHP FFI in the Wild

- Laravel LibSQL (new version)
  - SQLite On steroids
- Gameboy Emulator
- SNES Emulator
- Mobile App by Native PHP
- and many more: [Awesome PHP FFI](https://github.com/gabrielrcouto/awesome-php-ffi)

---

# FFI or Not to FFI ?

<div grid="~ cols-2 gap-4">
<div>

## FFI

- ✅ Library is already there, just use it
- ✅ No need to learn PHP internals

</div>
<div>

## PHP Extension

- ✅ Faster
- ✅ You are writing PHP using another language (C or Rust or any other)

</div>
</div>

---

# Summary


- PHP is not limited to the web
- You can use <b v-mark.red="1">PHP for Desktop, CLI, and Mobile Apps</b>

- PHP Extensions and FFI are powerful tools to <span v-mark.circle.orange="2">extend</span> PHP capabilities

- You can write PHP extensions in Rust, C and many more languages as long they <span v-mark.underline.orange="3">support PHP API</span>
  - including `php.h` and `ext_php_rs`

- PHP FFI allows you to call functions directly from <span v-mark.underline.blue="4">PHP (uses C shared libraries)</span>
  - Can use C, Rust, Golang, Python, etc.

---

# Q and A

```php
<?php

  echo "Thank you!";
  echo wave(); // call from FFI
```

<div>
    <img src="https://avatars.githubusercontent.com/u/26553194?v=4" class="rounded-full w-40 abs-tr mt-16 mr-12"/>
    <img v-mark.circle.orange src="./images/qr-bruno.png" class="rounded-5 w-40 abs-tr mt-80 mr-12"/>
</div>

<div class="my-10 grid grid-cols-[40px_1fr] w-min gap-y-4">
    <carbon:logo-github/>
    <div><a href="https://github.com/eznix86" target="_blank">eznix86</a></div>
    <carbon:logo-twitter class="text-blue"/>
    <div><a href="https://twitter.com/eznix86" target="_blank">eznix86</a></div>
</div>