# Memory

## Promoted

- [id:711186 | 2026-07-16 | src:adopted | uses:0] M4.2 — 12km NE of Nicolosi, Sicily (Etna region) TEST
- [id:5e8828 | 2026-07-13 | src:adopted | uses:0] Deadlines, recurring commitments, long-running projects
- [id:b2d2e2 | 2026-07-16 | src:adopted | uses:0] Decisions the user explicitly asked you to remember

## Staged

- [id:5c51ab | 2026-09-15 | src:cloud | uses:0] GALES boundary conditions are compiled, not read: dirichlet_<dof>(node) keys on the NODE flag and neumann_<fn>(sides, side_flag) on the SIDE flag; gmsh_to_gales.py takes each entity's physical TAG from $Entities (a name is not a flag) and refuses a $PhysicalNames block, and a face's group does not reach its curves and points, so every face, edge, corner and embedded point needs a tag.
- [id:420e14 | 2026-09-15 | src:cloud | uses:0] In GALES, side flag 1 is the fluid-solid coupling interface for solid_es, solid_ed, thermoelasticity and heat_conduction (get_fluid_tr / get_fluid_heat_flux): a study with no fluid whose face carries flag 1 segfaults at the first step. The fluid (fluid_sc) is weakly compressible with c = 1/sqrt(rho*beta); beta 0 (the props reader's default for a missing key) is a NaN at the first solve, and the time step is bounded by the acoustics (about 75 sound transits of the model per step runs; 75,000 diverged).
- [id:7c28d3 | 2026-09-15 | src:cloud | uses:0] A GALES simulation is a compiled executable bound to the MPI and Trilinos it was linked against, so it is built on the machine that runs it (a container or ssh target builds from the run's sources); the mesh is converted per rank count (gales_mesh.py N writes input/<mesh>_Ncore.txt, named in setup.txt), and results are results/<field>/<time> as raw little-endian float64 per node, never removed by a re-run. sim/solid_es/mogi_test_2d cannot be cloned (no main.cpp); a 2D solid deck is the 3D reference patched to dim 2.
