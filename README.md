# Rust File Compressor Comand Line Tool

## What does the app do
The program takes the arguments passed by user in the following manner:
```bash
cargo run source destination
```
Example:
```bash
cargo run input.txt output.zip
```
Where the *source* & *destination* are valid file paths. After the program finishes its execution successfully, the user will have:
- the time the operation took to run (only the operation, all necessary objects are being instantiated before) displayed in the standard output
- the size of the source file
- the size of the output (compressed) file

## Languages:
- Rust

## Frameworks & Libraries:
- falte2 - https://docs.rs/flate2/latest/flate2/ | https://crates.io/crates/flate2

## Implementation:
First step is to check if the number of program arguments is correct:
```rust
let program_arguments = env::args().collect::<Vec<String>>();
    if 3 != program_arguments.len() {
        eprintln!("Usage: cargo run <source> <destination>");
        return;
    }
```
Second step is to check if the path for the input file is valid and initialize an object that lets us read the file:
```rust
// input file & reader initialization
    let source_file = match File::open(&program_arguments[1]) {
        Ok(file) => file,
        Err(error) => {
            eprintln!("Cannot open the source file because of an error: {}.", error);
            return;
        }
    };
```
We do the almost same thing for the output file, validating its path, then we start encoding operation by copying the content of the input file in the encoder object. After that, we copy the encoded bytes in the output file and print the results, or throw an error if there is the case.