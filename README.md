# DyCoFit

**Version 1.0.0** (2026-10-28)

High-speed video analysis tool for Behind Armour Blunt Trauma (BABT) assessment
using SEBS gel block impact testing.

![DyCoFit Logo](icons/Dycofit_logo_name.png)

## Description

Video analysis software for Behind Armour Blunt Trauma (BABT) evaluation in SEBS gel impact testing.

Balistics tests on SEBS gel blocks measure body armour deformation to assess blunt trauma risk. High-speed imaging captures the dynamic cone formation, from which DBFD and ETP are derived as injury criteria:
- **DBFD** (Dynamic Back Face Deformation): peak deformation depth in mm — primary indicator of blunt trauma risk
- **ETP** (Energy Transmission Parameter): pseudo-viscous criterion in m/s, combining displacement and velocity

The software provides a complete workflow from image import through analysis to export of results in multiple formats.

## Installation

### First-time Installation

The compiled version distributed by the French ministry of the interior is the official release of DyCoFit and should be used for all runs of the program. No MATLAB licence is required.

1. Run the DyCoFit installer (`DycoFit_Setup.exe`)
2. The installer will set up DyCoFit and the MATLAB Runtime automatically
3. Launch DyCoFit from the Start menu or desktop shortcut

### Running DyCoFit

- Execute `DyCoFit.exe` from the installation directory
- No additional setup required

## Example Dataset

An example dataset is provided in the example_dataset/ folder to help you practice and verify your results. The dataset contains:

- TIFF image sequence from a test impact
- Test parameters in test_parameters.txt
- Reference results (DBFD: ~54.39 mm, ETP: ~6.38 m/s) and screenshots

How to use it

1. Open DyCoFit
2. Navigate to the example_dataset/ folder
3. Select any .tif file and click Open
4. Follow the standard procedure to analyze the video
5. Compare your results with the reference values

This example demonstrates a typical impact test.

## How to Use

### Overview

This tool processes high-speed video recordings from SEBS gel block impact testings. It imports image sequences (`.tif`), computes wall displacement, and exports results in multiple formats.

### Input Files

1. Place all `.tif` files from a single test in one folder
2. The folder name will be used to create sub-directories where output files are saved

### Procedure

#### 1. Launch DyCoFit

- Run the compiled executable (`DyCoFit.exe`)
- In the file-selection dialog, choose **File type → .tif** and select any image from the folder; all images will be loaded automatically

An "Image processing" interface will open.

#### 2. Image Pre-processing

Adjust the following if needed to improve analysis quality:

- **Gain**: Accentuates contours (default: 1)
- **Gamma**: Adjusts contrast factor (default: 1)

##### Trim Video

Limit the analysis to frames containing relevant impact events:
- **Start**: First frame with the projectile positioned in front of the protective equipment and block (pre-impact)
- **End**: Frame soon after maximum displacement, when the cone begins to reduce

When adjustments are complete, click **OK**.

#### 3. Define Coordinate System and ROI

A video window will appear with display controls:

1. Enable **Display axes** and **Display Ruler**
2. Click **Enlarge** to zoom the frame
3. Align the X-axis (horizontal) with the projectile trajectory
4. Align the Z-axis (vertical) with the interface between the tested equipement and the block 
5. Position the ruler on the calibration marks of the scale

6. Use **Cursor → ROI** to delimit the region containing the entire cone of penetration (full width and depth)

#### 4. Experimental Parameter Settings

An "Experimental Parameters" interface will appear:

| Parameter | Description | Typical Value |
|-----------|-------------|---------------|
| Deformation threshold | Minimum displacement to determine the sart of the real displacement; set near first point after impact | ~2 mm |
| Volume deformation | X-value where cone becomes regular without noise (default: 10 mm) | ~10 mm |
| Gel block thickness | Thickness of SEBS block (default: 300 mm) | 300 mm |
| Camera-to-block distance | Distance from camera to block face (default: 1300 mm) | 1300 mm |
| Optical system | Select your lens from dropdown (or fill custom value) | 85 mm |

Click **OK** to validate and compute results.

#### 5. View Results

- Maximum wall displacement
- Velocity
- ETP

##### Time Alignment & Fitting

If needed, adjust results:
1. Click **Options** in the results window
2. Modify **Time shift** to align start of deformation with t=0
3. Choose a **Fitting option** for the displacement curve
4. Use **Local max** if there is a deformation wave that distorts the measurement of maximum displacemnt depth

#### 6. Export Results

The program provides multiple export options:

##### Main Report Export (Excel + PDF)

Click the main export button in the results window to generate:
- **Excel file (.xlsx)**: Complete data with all metrics, graphs embedded. Requires Microsoft Excel installed and activated.
- **PDF report**: Professional report with unique ID, date, program version, parameters table, and all key metrics

##### Graphs Export and Data (FIG, JPEG, CSV)

- **FIG files**: MATLAB figure files for re-editing
- **JPEG images**: Static plots for reports and presentations  
- **CSV data**: Raw numerical data (time, displacement, velocity, ETP)

## Key Output Metrics

### DBFD (Dynamic Back Face Deformation)

The maximum deformation depth in millimeters. This is the primary measurement used to assess BABT.

### ETP (Energy Transmission Parameter)

A pseudo-viscous criterion expressed in m/s, derived from the gel wall displacement and its rate of change (velocity). The mathematical equation is:

```
ETP = 1.3 * displacement * velocity / 255.5
```

Where:
- **1.3** is a pre-factor
- **255.5 mm** is chest depth of the average adult male
- **displacement** is the gel wall deformation in mm
- **velocity** is the rate of displacement in m/s

ETP time history provides insight into the energy transfer dynamics during impact. This metric, along with DBFD, is used to evaluate injury risk according to French Ministry of the Interior standards for ballistic protection testing.

> Bolduc M., Anctil B., Improved test methods for better protection, a BABT protocol proposal for STANAG 2920, Personal Armour Systems Symposium, Quebec, Canada, 2010

## Lens Correction

Optical correction values for different camera lenses:

| Camera Lens | Correction [mm] |
|-------------|-----------------|
| 50 mm       | 63.56           |
| 85 mm       | 180.4           |
| 55 mm       | 65.1            |
| Custom      | User-defined    |

## Requirements

- Windows 11
- Microsoft Excel (for .xlsx export) - must be installed and activated
- MATLAB Runtime included with compiled version

## Contact / Support

For questions or bug reports, contact:

- Gabriel Starzak-Tomon, CREL French ministry of the interior
- Email: gabriel.starzak-tomon@interieur.gouv.fr
- Generic email : sailmi-crel@interieur.gouv.fr

## License

This project is distributed under the BSD 3-Clause License. See the LICENSE file for details.
