---
layout: post
title: Decompress zip file in rust
date: 2025-01-15 21:20:54
tags: [Rust, flate2, ZipArchive]
categories: Solana
---

This program allow user to input a path of a zip file. Then it will automatically extracts the contents of the zip file and outputs all files to the root directory.

<!-- more -->

## Step-by-Step Guide

**First, we will need to use Cargo to initialize the base structure of the project:**

```bash
cargo new Rust-Decompress
cd Rust-Decompress
```

**We will delete all the default code in the `main.rs` file and import the necessary libraries, particularly `flate2` and `ZipArchive`.**

```bash
use flate2::write::GzEncoder;
use flate2::Compression;
use std::env;
use std::env::args;
use std::fs::File;
use std::io;
use std::io::copy;
use std::io::BufReader;
use std::time::Instant;
use zip::ZipArchive;
```

