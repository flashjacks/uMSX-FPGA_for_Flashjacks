# Firmware for uMSX-FPGA and Flashjacks version 1.0

For the FPGA:
Starting point OCM-PLD Pack v3.9.1 (11/27/2022).
Config in onechip.
Compile in Quartus II 11.0sp1
Then Convert program files: emsx_top_304k.cof / emsx_top_304k.hex source / iplrom_304k.hex source
Crush the emsx_top.pof. Dump all the pof to the FPGA.

Changes for the FJ:
- FM removed (OPLL ROM+FM).
- Kanji removed
- ESE-SCC1 and 2 were removed.
- Only 64/512 kb of RAM for full compatibility with all MSX. For the rest use RAM Flashjacks.
- Bidir for PSG bus slot. This is to inject data from the Flashjacks cassette.
- Spanish keymap
- Added scan lines. Control by jumper 4. Luminance compensated in scanlines mode.
- Force VIDEOOUTX to 1. Eliminates error lines in VGA, SC12 interpolation mode.
- Central image in VGA systems.
- Autoboot BIOS with internal flash. No SD card needed.
- Dip Switch and Led reconfigured for the new Flashjacks configuration.
- Turbo CPU at 4.29 Mhz for compatibility with Flashjacks.

For SD card:
- Create one with the OCM-SDBIOS Pack v3.7 from kdl. make folder. make-sdb.cmd --> will create the OCM-BIOS.DAT. Then make a new-sdcard.cmd if we do not have the microSD formatted.
- Parameters for the OCM-BIOS.DAT for Flashjacks: Option 2 MSX2+ Backslash / Option 1 MSX2+ logo fix / Option 1 No option ROM / Option 1 No extra ROM

For BIOS boot. No SD card needed:
- To create the BIOS boot from the FPGA itself without the need for an SD card: emsx_top_304k.hex. Run 20240113 OCM-SDBIOS Pack v3.7 by KdL\make\bin2hex the file 2_get-epbios-304k-k34-msx2p.cmd with the options from the previous point.
- The emsx_top_304k.hex is then copied to the FPGA compiler in the existing file and executed in convert programming files and it outputs the .pof with everything.

Upload Firmware to FPGA:
- Upload the firmware named emsx_top.pof via cable using Quartus and the USB-Blaster.