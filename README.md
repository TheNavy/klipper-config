# My custom Klipper macros

All credit goes to @dudeofawesome -> https://github.com/dudeofawesome/klipper-config
He created the Marcos!


### Slicer Settings to use the Macros
**Note**: Cura Users!

*(Cura slicer plugin) To make the macro to work in Cura slicer, you need to install the post process plugin `MeshPrintSize.py` (original credit: [frankbags](https://gist.github.com/frankbags/c85d37d9faff7bce67b6d18ec4e716ff), I just made only slight modification)
- In cura menu `Help` -> `Show configuration folder`
- Copy `MeshPrintSize.py` into `scripts` folder
- Restart Cura
- In cura menu `Extensions` -> `Post processing` -> `Modify G-Code` and select `Mesh Print Size`.

**CONFIG**

- [`START_PRINT`](./print_start.cfg)

  - Slicer configuration

    - SuperSlicer

      `Printer Settings` → `Custom G-Code` → `Start G-Code`

      ```lisp
      ;Klipper start print macro
      START_PRINT HOTEND={first_layer_temperature[initial_extruder]+extruder_temperature_offset[initial_extruder]} BED={first_layer_bed_temperature} RELATIVE_E_MODE={use_relative_e_distances} PROBE=true PROBE_AREA_START={first_layer_print_min[0]},{first_layer_print_min[1]} PROBE_AREA_END={first_layer_print_max[0]},{first_layer_print_max[1]}
      ```

    - Cura

      **Note**: `PROBE_AREA_START` and `PROBE_AREA_END` rely on a non-official
      Cura plugin. Look at Note from the beginning!

      `Settings` → `Printers` → `Machine Settings` → `Start G-code`

      ```lisp
      ;Klipper start print macro
      START_PRINT HOTEND={material_print_temperature_layer_0} BED={material_bed_temperature_layer_0} RELATIVE_E_MODE={relative_extrusion} PROBE=true PROBE_AREA_START_X=%MINX% PROBE_AREA_START_Y=%MINY% PROBE_AREA_END_X=%MAXX% PROBE_AREA_END_Y=%MAXY%
      ```

- [`END_PRINT`](./print_end.cfg)

  - Slicer configuration

    - SuperSlicer

      `Printer Settings` → `Custom G-Code` → `End G-Code`

      ```lisp
      END_PRINT ;Klipper end print macro
      ```

    - Cura

      `Settings` → `Printers` → `Machine Settings` → `End G-code`

      ```lisp
      END_PRINT ;Klipper end print macro
      ```

- [`BEFORE_LAYER_CHANGE`](./layer_before_change.cfg)

  - Slicer configuration

    - SuperSlicer

      `Printer Settings` → `Custom G-Code` → `Before layer change G-Code`

      ```lisp
      BEFORE_LAYER_CHANGE
      ;{layer_z}
      ```

    - Cura

      `Extensions` → `Post Processing` → `Modify G-Code` → `Add a script` →
      `Insert at layer change`

      ```lisp
      BEFORE_LAYER_CHANGE
      ```
