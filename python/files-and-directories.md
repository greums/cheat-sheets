# Files and directories

![](https://images.unsplash.com/photo-1583521214690-73421a1829a9?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80)
📷 by [Wesley Tingey](https://unsplash.com/@wesleyphotography)

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
