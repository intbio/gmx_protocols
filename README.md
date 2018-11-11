# gmx_protocols
Protocols for running MD simulations in Gromacs

## Notes on equilibration protocols
### AMBER ff14SB paper
Except where otherwise indicated, equilibration was performed with a weak- coupling (Berendsen) thermostat33 and barostat targeted to 1 bar with isotropic position scaling as follows. With 100 kcal mol−1 Å−2 positional restraints on protein heavy atoms, structures were minimized for up to 10000 cycles and then heated at constant volume from 100 K to 300 K over 100 ps, followed by another 100 ps at 300 K. The pressure was equilibrated for 100 ps and then 250 ps with time constants of 100 fs and then 500 fs on coupling of pressure and temperature to 1 bar and 300 K, and 100 kcal mol−1 Å−2 and then 10 kcal mol−1 Å−2 Cartesian positional restraints on protein heavy atoms. The system was again minimized, with 10 kcal mol−1 Å−2 force constant Cartesian restraints on only the protein main chain N, Cα, and C for up to 10000 cycles. Three 100 ps simulations with temperature and pressure time constants of 500 fs were performed, with backbone restraints of 10 kcal mol−1 Å−2, 1 kcal mol−1 Å−2, and then 0.1 kcal mol−1 Å−2. Finally, the system was simulated unrestrained with pressure and temperature time constants of 1 ps for 500 ps with a 2 fs time step, removing center-of-mass translation and rotation every picosecond.

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4821407/pdf/nihms772276.pdf

### Shaytan et al. JMB 2016
