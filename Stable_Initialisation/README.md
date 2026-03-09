# Nozzle OpenFOAM Case (Fine Grading)

This case uses `rhoCentralFoam` with an imported Gmsh mesh.

## Boundary conditions
- `INLET`: fixed static pressure `p = 5e6 Pa` (50 bar)
- `OUTLET`: fixed static pressure `p = 1e5 Pa` (1 bar)
- `FARFIELD`: fixed static pressure `p = 101325 Pa` (1 atm)
- `AXIALSYMMETRY`: `symmetryPlane`
- `SOLID_WALL`: no-slip wall for velocity, zero-gradient pressure/temperature
- `FRONT` and `BACK`: `empty` (single-cell thickness in z, 2D simulation)

## Run
From this folder:

```bash
./Allclean
./Allrun
```

`Allrun` steps:
1. Build 3D one-cell-thick mesh from `../data_clean/nozzle_geometry/nozzle_cfd_structured.geo`
2. Import via `gmshToFoam`
3. Stitch internal interfaces (`IFACE12/14/15`)
4. Apply patch types using `changeDictionary`
5. Run `checkMesh`
6. Run `rhoCentralFoam`
