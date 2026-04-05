# Unity Asset Extractor

Unity Asset Extractor is a Unity bundle extraction tool with both GUI and CLI modes.
It supports multiprocessing, progress display, selectable asset types, and configurable source bundle extensions.

## Features

- GUI mode with folder pickers, CPU usage selection, extract-type checkboxes, and target extension input.
- CLI mode for automation and scripting.
- Configurable input bundle extensions (default: `.unity3d`, `.bundle`).
- Multiprocessing extraction with progress bar and live save logs.
- Smart runtime launcher via `run.cmd` with cache to speed up repeated runs.

## Runtime Requirements

- Python 3.7+
- Dependencies from `requirements.txt` are `UnityPy==1.23.0` and `rich`.
- `tkinter` (usually bundled with standard Python on Windows)

## Recommended Start (Windows)

Use `run.cmd` at project root:

```bat
run.cmd
```

`run.cmd` runtime flow:

1. Check existing `.venv` first.
2. If `.venv` exists and requirements are satisfied, run from `.venv` immediately.
3. If `.venv` exists but requirements are not satisfied, install requirements and run.
4. If no usable `.venv`, check system Python.
5. If Python version and requirements are valid, run directly with system Python.
6. If Python exists but version is below requirement.
6.1 If `uv` exists, create/update `.venv` with `uv` and run.
6.2 If `uv` does not exist, create/update `.venv` using installed Python and run.
7. If Python is not available, install/check `uv` and run using `uv run`.

## Cache Behavior

- Launcher cache file: `.run-cache.json`
- Cache file is ignored via `.gitignore`.
- Cache is used to skip repeated environment checks on next runs.

## GUI Usage

Run without CLI arguments:

```bat
run.cmd
```

or directly:

```bat
python assest_extracter.py
```

GUI fields:

- Source Folder
- Output Folder
- CPU Usage (`25`, `50`, `75`, `100`)
- Target Extensions (comma-separated, default `.unity3d,.bundle`)
- Extract Types

## CLI Usage

### Through launcher (recommended)

```bat
run.cmd -s <source_path> -o <output_path> [-c <cpu_percent>] [-t <types...>] [-e <extensions...>]
```

### Direct Python

```bat
python assest_extracter.py -s <source_path> -o <output_path> [-c <cpu_percent>] [-t <types...>] [-e <extensions...>]
```

### Arguments

- `-s`, `--source` Required. Source directory containing bundle files.
- `-o`, `--output` Required. Output directory for extracted assets.
- `-c`, `--cpu` Optional. CPU percent: `25`, `50`, `75`, `100`. Default: `100`.
- `-t`, `--type` Optional. Space-separated extract types: `texture2d`, `textasset`, `audioclip`, `gameobject`, `mesh`, `font`, `sprite`, `shader`, `monobehaviour`.
- `-e`, `--extensions` Optional. Space-separated input file extensions. Default: `.unity3d .bundle`

### CLI Examples

Extract all default types from default extensions:

```bat
run.cmd -s "D:/MyGame/Bundles" -o "D:/MyGame/Extracted"
```

Extract only `texture2d` and `textasset` with 50% CPU:

```bat
run.cmd -s "D:/MyGame/Bundles" -o "D:/MyGame/Extracted" -c 50 -t texture2d textasset
```

Extract with custom input bundle extensions:

```bat
run.cmd -s "D:/MyGame/Bundles" -o "D:/MyGame/Extracted" -e .bundle .unity3d .ab
```
