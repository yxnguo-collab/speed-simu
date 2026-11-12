# LOH3 (SCEC LOH.3 benchmark)

Mazzieri's LOH3 inputs: layer over half-space with attenuation (DAMPING 2), point
dislocation Mxy = 1e18 N m at 2000 m depth, FUNC 14 (T = 0.1 s), degree 4,
369,120 elements, 10 surface receivers (LS.input). Used to check the SPEED build
(master 1c6ed48 + apptainer/patches) against the semi-analytical reference
solution at receiver 10 (Day et al. 2003; reference `LOH.3_prose_corrected`, not
in this repository).

Changes to Mazzieri's SPEED.input: STOPTIME 8.0 (9.0; the comparison uses
1.5-8 s), MONFILE MONITOR (MONITORS). The .mate already has `EXPN 0.0`, which the
new master needs.

The mesh is `LOH1_TEST.mesh.zst` in this folder (4.5 MB, 50 MB unpacked);
run_case.sh unpacks it next to itself on the first run.

Run with the case's own time step (0.0005 s), not the CFL fraction:

    apptainer/submit.sh -- bash run_case.sh -c case -n 48 cases/loh3

Size: about 23 million GLL nodes, 16,000 steps. One run is long: about 2.9
million nodes per process with 8 processes. Only displacement monitors are
written (OPTIOUT 1 0 0 0 0 0), no VTK.
