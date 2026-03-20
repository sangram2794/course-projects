# VLSI Course Project – OpenRAM 1KB SRAM Memory Design

A step-by-step guide to setting up a virtual machine with Ubuntu 22.04 and using OpenRAM to generate a 1KB SRAM memory.

---

## Table of Contents

- [Part A – Environment Setup](#part-a--environment-setup)
- [Part B – OpenRAM Installation & Memory Design](#part-b--openram-installation--memory-design)
- [Output Files](#output-files)
- [Viewing the GDS Layout](#viewing-the-gds-layout)
- [Notes & Tips](#notes--tips)

---

## Part A – Environment Setup

### 1. Install Oracle VM VirtualBox

Download and install VirtualBox from the official site:
👉 https://www.virtualbox.org/wiki/Downloads

Select the appropriate platform package for your host OS (e.g., **Windows hosts**).

### 2. Download Ubuntu 22.04 ISO

Search for `ubuntu 22.04 iso download` or go directly to:
👉 https://releases.ubuntu.com/jammy/

Download the **64-bit PC (AMD64) desktop image** (`ubuntu-22.04.5-desktop-amd64.iso`).

### 3. Configure the Virtual Machine

Once VirtualBox and the ISO are downloaded, create a new VM with the following settings:

| Setting | Value |
|---|---|
| Name | Ubuntu_22.04 |
| OS | Ubuntu (64-bit) |
| Base Memory | 8192 MB |
| Processors | 4 |
| Boot Order | Floppy, Optical, Hard Disk |
| Acceleration | Nested Paging, KVM Paravirtualization |
| Video Memory | 16 MB |
| Graphics Controller | VMSVGA |
| Storage | Ubuntu_22.04.vdi (Normal, 25.00 GB) |
| Network | Intel PRO/1000 MT Desktop (NAT) |

> ⚠️ **Important:** Only Ubuntu 22.04 or 20.04 is compatible with OpenRAM. Other versions are NOT supported.

---

## Part B – OpenRAM Installation & Memory Design

Open the terminal inside Ubuntu and follow the steps below.

**Useful shortcuts:**
- `Ctrl+O` then `Enter` → Save file (in nano)
- `Ctrl+X` → Exit file (in nano)
- `Ctrl+Shift+C` / `Ctrl+Shift+V` → Copy / Paste in terminal

---

### Step 1 – Update System Packages

```bash
sudo apt update
```

### Step 2 – Install Python Dependencies

```bash
pip3 install numpy matplotlib
```

### Step 3 – Clone the OpenRAM Repository

```bash
git clone https://github.com/VLSIDA/OpenRAM.git
```

### Step 4 – Navigate into the Repository

```bash
cd OpenRAM
ls
```

### Step 5 – Create the SRAM Configuration File

```bash
nano sram_1kb.py
```

Paste the following configuration for a 1KB SRAM using the FreePDK45 technology node:

```python
word_size = 8          # Number of bits per word
num_words = 1024       # Total number of words
tech_name = "freepdk45"  # Use FreePDK45 instead of sky130

output_path = "output"   # Directory to store all output
output_name = "sram_1kb" # Prefix for output files

process_corners = ["TT"]   # Typical process corner
supply_voltages = [1.0]    # Nominal VDD for FreePDK45
temperatures = [25]        # Room temperature

nominal_corner_only = True
```

Save with `Ctrl+O` + `Enter`, then exit with `Ctrl+X`.

### Step 6 – Patch the Compiler Modules

Navigate to the compiler modules directory and edit `__init__.py`:

```bash
cd compiler/modules/
nano __init__.py
```

Find the line:
```python
from .rom_bank import *
```

Comment it out by adding a `#` at the start:
```python
#from .rom_bank import *
```

Save and exit (`Ctrl+O` → `Enter` → `Ctrl+X`).

> ℹ️ This fix is necessary for proper output file generation.

### Step 7 – Set Environment Variables

Navigate back to the home directory and export the required paths:

```bash
cd ../..
export OPENRAM_HOME="$HOME/OpenRAM/compiler"
export OPENRAM_TECH="$HOME/OpenRAM/technology"
export PYTHONPATH="$OPENRAM_HOME:$OPENRAM_TECH"
```

> ⚠️ **Important:** These environment variables must be set every time you open a new terminal session, unless added to your `~/.bashrc`.

### Step 8 – Run the SRAM Compiler

```bash
cd OpenRAM/
python3 sram_compiler.py sram_1kb.py
```

This will take approximately **3–5 minutes** for a 1KB memory. Larger memory sizes will take proportionally longer.

---

## Output Files

After successful compilation, all output files are saved in the `output/` directory:

| File | Description |
|---|---|
| `sram_1kb.gds` | GDSII physical layout file |
| `sram_1kb.lef` | Library Exchange Format (placement/routing) |
| `sram_1kb.v` | Verilog netlist |
| `sram_1kb.sp` | SPICE netlist |
| `sram_1kb.lvs.sp` | LVS SPICE netlist |
| `sram_1kb.lib` | Liberty timing library |
| `sram_1kb.html` | Datasheet |
| `sram_1kb.log` | Compilation log |
| `sram_1kb.py` | Config copy |
| `sram_1kb_TT_1p0V_25C.lib` | Corner-specific Liberty file |

---

## Viewing the GDS Layout

### Install KLayout

KLayout is an open-source tool for viewing and verifying GDSII layout files.

```bash
sudo apt install klayout
```

### Open the GDS File

```bash
cd output/
klayout sram_1kb.gds
```

This opens the physical layout in a KLayout window, where you can inspect the memory array, address decoders, sense amplifiers, and other circuit components.

---

## Notes & Tips

- The OpenRAM version used in this project is **v1.2.49**, developed by the VLSI Design and Automation Lab at UC Santa Cruz.
- The technology used is **FreePDK45** (45nm predictive PDK). You can substitute `sky130` or `freepdk45` depending on your target.
- Memory size = `word_size × num_words` = `8 × 1024` = **8192 bits = 1KB**.
- The `nominal_corner_only = True` flag skips multi-corner simulation to speed up compilation.
- DRC/LVS checking is disabled by default. Enable it by setting `check_lvsdrc = True` in the config.
- To make environment variables persistent, add the `export` commands to `~/.bashrc` and run `source ~/.bashrc`.

---

## References

- OpenRAM GitHub: https://github.com/VLSIDA/OpenRAM
- Ubuntu 22.04 LTS: https://releases.ubuntu.com/jammy/
- VirtualBox: https://www.virtualbox.org/
- KLayout: https://www.klayout.de/
