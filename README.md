# LabVIEW PVCAM SubVIs for Photometrics Prime95B

Reusable LabVIEW subVIs and examples for controlling **Photometrics Prime95B** cameras 
via the **PVCAM** SDK.

> ⚠️ **Note on SDK Binaries:** This repo does **not** redistribute PVCAM SDK DLLs. Please install the 
official PVCAM drivers/SDK from Teledyne Photometrics and ensure the DLLs are on your system PATH. 
See **Prerequisites**.

## Features
- Initialize and enumerate PVCAM cameras
- Configure exposure, ROI, binning, gain/EM gain (if applicable), readout rate
- Acquire single frames and continuous sequences
- Basic frame buffering and image output to LabVIEW arrays
- Example VIs demonstrating typical workflows

## Tested Setup (fill these in)
- **LabVIEW:** 2021 (64-bit)
- **OS:** Windows 10/11 (64-bit)
- **PVCAM:** 3.7.3 (64-bit)
- **PVCAM SDK:** 3.10.1.1 (64-bit)
- **Camera:** Photometrics Prime95B

If your setup differs and works, please open a PR to add it here.

## Prerequisites
1. **LabVIEW** installed (matching bitness with your PVCAM DLLs).
2. **PVCAM driver & SDK** installed from Teledyne Photometrics.
3. Ensure `pvcam64.dll` (or corresponding 32-bit) is on your **PATH** or located in a folder LabVIEW can find at runtime.
4. Camera connected and verified with the vendor’s utility (e.g., exposure test).

## Repository Layout

/src # Core subVIs (PVCAM wrappers are in Low_level_subVIs folder, Higher_level_subVIs contain handy combinations of PVCAM functions)
/examples # Ready-to-run examples (open these first)
/docs # Screenshots, diagrams, notes
/data # Optional sample images (gitignored)
/third_party # Placeholder for local SDK DLLs if you must place them (gitignored)
README.md
.gitignore

## Quick Start
1. Install PVCAM driver/SDK and connect your Prime95B.
2. Clone this repo:
   ```bash
   git clone https://github.com/brjak/photometrics-pvcam-labview.git
3. Open examples/Example_sequence+acquisition.vi (or another example) in LabVIEW.
4. Check the Camera control enumerates your device; if not, verify the SDK installation and PATH.
5. Set exposure (e.g., 10 ms), and run the VI.
6. Verify you receive an image; adjust parameters as needed.

Typical Call Sequence (block diagram logic)
1. PVCAM Initialize
2. Get Camera List → select desired camera
3. Open Camera
4. Configure (exposure, ROI, binning, gain/readout)
5. Start Acquisition (single or continuous)
6. Read Frames → LabVIEW image array / display
7. Stop Acquisition
8. Close Camera and Uninitialize

The example VIs mirror this sequence.

## Notes & Tips

 - Bitness matters: LabVIEW 64-bit pairs with 64-bit PVCAM DLLs; 32-bit with 32-bit.
 - Threading: Long acquisitions should run in a dedicated loop; avoid UI blocking.
 - Buffering: For continuous acquisition, allocate buffers sized for your frame rate and disk throughput.
 - Saving data: Consider writing TIFF/RAW with timestamps to avoid UI overhead during acquisition.
 - Error handling: All subVIs propagate error clusters; wire them through. subVIs in Higher_level_subVIs 
actually read PVCAM error codes at the end, look up them in PVCAM 2.7 manual stored in docs/ folder.

## Screenshots
See docs/ for block diagram and front-panel screenshots.
(Add images like docs/example-front-panel.png and reference them here.)

## Known Issues / Limitations
 Parameters of class 3 can not be written or read. class 2 parameters such as sensor temperature 
are read ok. Do not read temperature when cyclic buffer acquisition is started.

## Contributing
PRs and issues are welcome:

 - Keep VIs saved in the oldest LabVIEW version you support (if possible) for wider compatibility.
 - Include a small demo VI when adding new subVIs.
 - Avoid committing vendor SDK DLLs unless redistribution is permitted.

## License
MIT

## Acknowledgements
 - Teledyne Photometrics for PVCAM.
 - Authors thank Kirill Sitnik for fruitfull discussions.

## Citation
If you use this in academic work, please cite this repository.
