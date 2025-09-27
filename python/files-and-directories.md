# Python Files and Directories - Complete Guide with Examples

Master Python file and directory operations with practical examples and performance optimizations. Learn efficient ways to calculate directory sizes, handle file paths, and work with the filesystem.

![Python file and directory operations examples](https://images.unsplash.com/photo-1583521214690-73421a1829a9?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1200&q=80 "Python programming for file system operations")

📷 by [Wesley Tingey](https://unsplash.com/@wesleyphotography)

> **Quick Reference**: Learn how to efficiently calculate directory sizes in Python using both sequential and concurrent approaches. Perfect for system administration and file management tasks.

## Table of Contents

- [Get Directory Size (Basic)](#get-total-size-of-a-directory)
- [Optimized Directory Size Calculation](#faster-way-to-get-total-size-of-a-directory)
- [Performance Comparison](#performance-analysis)
- [Best Practices](#best-practices)

## Get total size of a directory

Take a folder containing lots of nested subfolders also containing too many files:

```python
from pathlib import Path
from time import time


def get_directory_size(path: Path) -> float:
    return sum(f.stat().st_size for f in path.rglob("*") if f.is_file())


start_time = time()
size = get_directory_size(Path("my big messy fatty folder"))
print(f"size : {round(size / 1024**3, 2)} GB\ntook : {round(time() - start_time, 2)} seconds")
```
```python
size : 55.09 GB
took : 33.11 seconds
```

## Faster way to get total size of a directory

Take the same folder, add some concurrency:

```python
import concurrent.futures
from pathlib import Path
from time import time


def calculate_size(path: Path) -> float:
    return sum(f.stat().st_size for f in path.rglob("*") if f.is_file())


def get_directory_size(path: Path) -> float:
    subpaths = [p for p in path.glob("*/*") if p.is_dir()]
    with concurrent.futures.ProcessPoolExecutor() as executor:
        sizes = executor.map(calculate_size, subpaths)
    return sum(sizes)


start_time = time()
size = get_directory_size(Path("my big messy fatty folder"))
print(f"size : {round(size / 1024**3, 2)} GB\ntook : {round(time() - start_time, 2)} seconds")
```
```python
size : 55.09 GB
took : 8.27 seconds
```

## Performance Analysis

The concurrent approach provides a **4x speed improvement** for large directories with multiple subdirectories. Here's why:

- **Sequential**: Processes files one by one
- **Concurrent**: Utilizes multiple CPU cores for parallel processing
- **Best for**: Large directories with many subdirectories

## Best Practices

### ✅ Do's
- Use `pathlib.Path` for modern, readable path operations
- Implement error handling for permission issues
- Consider memory usage for very large directories
- Use `ProcessPoolExecutor` for CPU-intensive tasks

### ❌ Don'ts
- Don't use string concatenation for paths
- Avoid blocking the main thread for large operations
- Don't ignore file access permissions

## Additional File Operations

### Check if Path Exists
```python
from pathlib import Path

file_path = Path("example.txt")
if file_path.exists():
    print("File exists!")
```

### Create Directories
```python
# Create directory with parents
Path("path/to/new/directory").mkdir(parents=True, exist_ok=True)
```

### List Files with Filter
```python
# Get all Python files
python_files = list(Path(".").glob("**/*.py"))
print(f"Found {len(python_files)} Python files")
```

## Related Topics

- [Python Lists and Dictionaries](lists-and-dictionaries.md) - Data structure operations
- [Python Linting and Configuration](linting-and-configuration.md) - Code quality tools

---

**Keywords**: Python file operations, directory size calculation, pathlib, concurrent processing, filesystem programming, Python system administration
