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

**We will write the logic code in the main function. First, we need to check how many arguments the user has input. If the number of arguments is less than or greater than two, then we have to quit the program.**

```bash
    # This part of the code should be pasted into the start of the main function
    if args().len() != 2 {
        eprintln!("Usage: `source`");
        return;
    }
```

**Get user input. In this case is the path of the zip file.**

```bash
let args: Vec<String> = env::args().collect();
let zip_path = &args[1];
```

**Try to open the zip file and read it. We need ZipArchive this three party library to help us read the zip file**

```bash
    # open zip file according by the path that user just entered
    let file = File::open(zip_path).unwrap_or_else(|err| {
        eprintln!("Failed to open ZIP file: {}", err);
        std::process::exit(1);
    });

    # new a BufReader obj
    let mut buf_reader = BufReader::new(file);
    # new a ZipArchive obj to read the zip file
    let mut zip = ZipArchive::new(&mut buf_reader).unwrap_or_else(|err| {
        eprintln!("Failed to read ZIP file: {}", err);
        std::process::exit(1);
    });
```

**Then we gonna creat a for loop to extracting every singal file in zip file. Then save it into a dir**

```bash
    # Extract ever file in zip file
    for i in 0..zip.len() {
        let mut file = zip.by_index(i).unwrap();
        let file_path = file.name();

        # print the path to the target file
        println!("Extracting: {}", file_path);

        let output_path = match file.enclosed_name() {
            Some(path) => path.to_owned(),
            None => continue,
        };

        if file.is_dir() {
            std::fs::create_dir_all(&output_path).unwrap();
        } else {
            if let Some(parent) = output_path.parent() {
                std::fs::create_dir_all(parent).unwrap();
            }
            let mut output_file = File::create(&output_path).unwrap();
            io::copy(&mut file, &mut output_file).unwrap();
        }
    }
```

**Congratulations! All done!**

```bash
println!("Done!");
```

## How to run it

**First, we need to ensure that we download all the necessary library files.**

```bash
# Cargo.toml
[package]
name = "decompress"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
flate2 = "1.0.24"
zip = "0.6.2"
```

**Then, run this command in the shell. Remember, you need to provide the path to the zip file on your local system. In this case, since I saved my zip file in the root directory, I can simply enter the file name directly.**

```bash
# "1.zip" is your zip file path
cargo run 1.zip
```

**Once you successfully run the program, you will see that it automatically generates a decompressed file in your root directory.**

## Explore the Project

- [Check the Source Code on GitHub](https://github.com/JzzzzSkr/Rust-Decompress)

