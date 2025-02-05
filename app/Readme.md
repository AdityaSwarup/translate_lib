# Introduction
This Python package allows users to code Python in their native language. The package then translates the syntax and keywords into English, allowing the code to be run as normal. 

**Supported Python Features:** 
- Keywords: Control flow (`if`, `else`, `for`, `while`, etc.), function definitions, class definitions, etc.
- Basic Libraries: `math`
- Basic Syntax: Variables, loops, conditionals, functions, classes, and imports.

[Link to repository](https://github.com/aadityayadav/translate_lib)

# Purpose and Scope
The goal of this project is to enable beginners to learn Python programming in their native language. By being able to use Python syntax and keywords in a more familiar language, learners can focus on understanding programming concepts without being hindered by unfamiliar English terms. This approach ensures that learners can build foundational programming skills before transitioning to English-based Python coding.

**Key Objectives:**

1. Provide a tool to translate Python code from a native language syntax to standard English-based Python.
2. Simplify the learning curve for beginners by removing the language barrier.
3. Support a gradual transition to English-based programming, preparing learners for real-world coding environments.

**This project is designed for:**
1. **Absolute beginners:** By removing the language barrier, we aim to introduce Python as a language, and coding in general, to a wider, non-English speaking population. 
2. **Educational Settings:** We can enable instructors to teach Python in their native language, perhaps in a bootcamp setting.


# Using the CLI tool
The run_cli.py script (located at app/translate_lib/src) includes a command-line interface (CLI) that allows users to translate Python files or directories written in a native language to English-based Python syntax. Below are the available commands and their usage.

## 1. Command syntax:
```
python run_cli.py <command> <input_path> [options]
```
- `<command>`: The action to perform (e.g., translate, run, etc.).
- `<input_path>`: The file or directory to process.
- `[options]`: Additional arguments (e.g., output path, language file, main file).

## 2. Available commands:
a. `translate `: Translates a single Python file from the source language to English and saves it to an output file.
- Usage:
```
python run_cli.py translate <input_file> -o <output_file> -l <language_file>
```
- Example:
```
python run_cli.py translate my_script.py -o translated_script.py -l hindi_to_english.json
```
**Options**:
- `-o`: Path to the output file (default: translated.py).
- `-l`: Path to the language mapping JSON file (default: hindi_to_english.json).
---
b. `run`: Translates a single Python file, saves it to an output file and then executes the translated code.
- Usage:
```
python run_cli.py run <input_file> -o <output_file> -l <language_file>
```
- Example:
```
python run_cli.py run my_script.py -o translated_script.py -l hindi_to_english.json
```
---
c.  `run_direct`: Translates and executes a Python file **without** saving the translated file. 
- Usage:
```
python run_cli.py run_direct <input_file> -l <language_file>
```
- Example:
```
python run_cli.py run_direct my_script.py -l hindi_to_english.json
```
---
d.  `translate_dir`: Translates all Python files in a directory and its subdirectories, saving the results in a new output directory.
- Usage:
```
python run_cli.py translate_dir <input_dir> -o <output_dir> -l <language_file> -m <main_file>
```
- Example:
```
python run_cli.py translate_dir my_project -o translate_project -l hindi_to_english.json -m main.py
```
- Options:
- `-o`: Path to the output directory (default: translated_dir).
- `-l`: Path to the language mapping JSON file (default: hindi_to_english.json).
---
e. `run_dir`: Translates all Python files in a directory and then executes a specified main file from the translated directory. Note: Does not save a translated directory. 
- Usage:
```
python run_cli.py run_dir <input_dir> -l <language_file> -m <main_file>
```
- Example:
```
python run_cli.py run_dir my_project -l hindi_to_english.json -m main.py
```
- Options:

- `-l`: Path to the language mapping JSON file (default: hindi_to_english.json).
- `-m`: Name of the main file to execute after translation (required).

# `PreProcessor` Class functions
a. `translate_file`: Translates a single Python file from the source language to English and saves the translated version to a specified output file.

Definition:
```
def translate_file(self, input_file, output_file):
```
Parameters:

- `input_file`: Path to the Python file in the native language to be translated.
- `output_file`: Path where the translated Python file will be saved.

How It Works:

- Reads the content of the `input_file`.
- Calls `translate_code` to perform the translation.
- Writes the translated code to the `output_file`.

Example:
```
preprocessor = PreProcessor("hindi_to_english.json")
preprocessor.translate_file("my_script.py", "translated_script.py")
```
---
b. `execute_file_directly`: Translates a single Python file and executes the translated code without saving it to a file.

Definition:
```
def execute_file_directly(self, input_file):
```
Parameters:

- `input_file`: Path to the Python file in the native language to be translated and executed.

How It Works:

- Reads the content of the `input_file`.
- Calls `translate_code` to perform the translation.
- Executes the translated code using `exec()`.

Example:
```
preprocessor = PreProcessor("hindi_to_english.json")
preprocessor.execute_file_directly("my_script.py")
```
---
c. `translate_directory`: Translates all `.py` files in a directory and its subdirectories and saves the translated files to a specified output directory.

Definition:
```
def translate_directory(self, input_dir, output_dir):
```
Parameters:
- `input_dir`: Path to the directory containing Python files in the native language.
- `output_dir`: Path to the directory where the translated Python files will be saved.

How It Works:

- Recursively traverses all subdirectories of `input_dir`.
- Identifies `.py` files for translation.
- Translates each file using `translate_file` and saves them in the `output_dir`.

Example:
```
preprocessor = PreProcessor("hindi_to_english.json")
preprocessor.translate_directory("\path\to\native_scripts", "\path\to\translated_scripts")
```
---
d.  `execute_directory`: Translates all Python files in a directory and executes a specified main file from the translated directory.

Definition:
```
def execute_directory(self, input_dir, main_file):
```

Parameters:

- `input_dir`: Path to the directory containing Python files in the native language.
- `main_file`: Name of the main Python file to execute after translation.

How It Works:

- Calls `translate_directory` to translate all files in `input_dir` and save them in a temporary directory (`temp_translated_dir`).
- Locates the translated version of `main_file` in the temporary directory.
- Adds the temporary directory to `sys.path` to allow imports from translated modules.
Reads and executes the translated `main_file`.

Example Usage:
```
preprocessor = PreProcessor("hindi_to_english.json")
preprocessor.execute_directory("native_project", "main.py")
```

# Functionality and Feature Limitations + How To Contribute
Please note the current limitations in this Python package (your help would be greatly appreciated to mitigate these limitations!):

## 1. Limited Language Keyword Mapping
- The tool relies on a JSON-based language mapping file for translations.
- Only the provided or configured keywords, methods, and functions will be translated. Custom keywords or unsupported syntax will remain untranslated.
- If you wish to include a library that you personally find useful, please translate all relevant keywords and update the respective `.json` file for your language.

## 3. Translation Ambiguities
- Context-sensitive keywords or ambiguous mappings may lead to incorrect translations.
- If you notice such ambiguities, please update the respective `.json` files accordingly.

## 3. Limited Language Files
- Arguably the biggest limitation, we require the community's support in translating the main Python keywords in as many languages as possible.
- If you notice that your native language has not been represented yet, please feel free to create a json language mapping. If you would like a reference, please refer to `hindi_to_english.json` and simply replace the hindi words with the respective keyword translations in your language. Save this file to `app/translate_lib/src/lang_map_json`.

## 4. Syntax Errors in Source Files (Feature TBA)
- Files with syntax errors will fail to run after translation. These errors will be displayed in English.
- If you are able to assist in transalting the errors, fork this repository and reach out to us with your solution!
