# Pathlib Library Usage

This guide covers common use cases of the `pathlib` library in Python for handling file paths, directories, and files.

## Table of Contents
- [Getting Current Working Directory](#getting-current-working-directory)
- [Listing Files and Directories](#listing-files-and-directories)
- [Working with Relative Paths](#working-with-relative-paths)
- [Working with File Extensions and Names](#working-with-file-extensions-and-names)
- [Joining Paths](#joining-paths)
- [Checking if a File Exists](#checking-if-a-file-exists)
- [Working with Absolute Paths](#working-with-absolute-paths)
- [Expanding User Paths](#expanding-user-paths)
- [Finding Files](#finding-files)
- [Reading Files](#reading-files)
- [Creating and Removing Directories](#creating-and-removing-directories)
- [Creating, Renaming, and Deleting Files](#creating-renaming-and-deleting-files)

---

## Getting Current Working Directory
To get the current working directory:
```python
from pathlib import Path

print(Path.cwd())
```

## Listing Files and Directories
To list all files and directories in the current working directory:
```python
from pathlib import Path

for p in Path().iterdir():
    print(p)
```

## Working with Relative Paths
You can create relative `Path` objects for directories and files:
```python
my_dir = Path("using_pathlib")
my_file = Path("test.py")

print(my_dir.name)  # Output: using_pathlib
print(my_file.name)  # Output: test.py
```

## Working with File Extensions and Names
To get the file extension and the name without the extension:
```python
print(my_file.suffix)  # Output: .py
print(my_file.stem)  # Output: test
```

## Joining Paths
To join paths similar to `os.path.join`:
```python
new_file = my_dir / "main.py"  # Alternative: my_dir.joinpath("main.py")
print(new_file)
```

## Checking if a File Exists
To check if a file exists:
```python
print(new_file.exists())  # True if file exists
print((my_dir / "mainss.py").exists())  # False if file does not exist
```

## Working with Absolute Paths
To get the absolute path of a directory or file:
```python
print(my_dir.absolute())
print(my_dir.resolve())  # Resolves relative path
print(Path("..").resolve())  # Resolves parent directory
```

## Expanding User Paths
To expand a user's home directory:
```python
p = Path("~/dotfiles")
print(p.expanduser())  # Expands to /home/username/dotfiles
```

## Finding Files
To search for specific files:
```python
# Find all files containing 'vscode' in the name (case-insensitive)
dotfiles = Path("~/dotfiles").expanduser()
dotfiles.rglob("*vscode*")
dotfiles.rglob("*.json", case_sensitive=False)  # Find all JSON files
```

## Reading Files
To read a file directly:
```python
txt_file = Path(__file__).resolve().parent.parent / "name.txt"
with open(txt_file) as f:
    print(f.read())
```

## Creating and Removing Directories
To create a directory:
```python
p = Path("TempDir")
p.mkdir()
```
To remove a directory:
```python
p.rmdir()  # Only works for empty directories
```
To create a directory with subdirectories:
```python
p = Path("TempSubDir/sub")
p.mkdir(parents=True)
```

## Creating, Renaming, and Deleting Files
To create a new file:
```python
p = Path("Temp.txt")
p.touch()  # Creates an empty file
```
To rename a file:
```python
p.rename("temp_file.txt")
```
To delete a file:
```python
p = Path("temp_file.txt")
p.unlink()  # Deletes the file
```