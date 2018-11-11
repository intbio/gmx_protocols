# gmx_protocols
Protocols for running MD simulations in Gromacs

## Notes on simulation parameters
### AMBER ff14SB paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4821407/pdf/nihms772276.pdf



### CHARMM36 paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3549273/pdf/nihms395902.pdf

Electrostatic interactions were computed with PME using a real-space cut-off of 12 Å and a 1 Å grid spacing and Lennard-Jones interactions were switched off smoothly between 10 and 12 Å. A Langevin thermostat with a friction coefficient of 1 ps−1 was used, with a time step of 2 fs to integrate the equations of motion. 

The equations of motion were integrated with a 2 fs time step while SHAKE was used to constrain covalent bonds involving non-water hydrogen bonds and SETTLE33 was used to maintain rigid water geometries. 

Pressure was regulated by a Parinello-Rahman barostat52 with a coupling time of 2.5 ps

## Notes on equilibration protocols
### AMBER ff14SB paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4821407/pdf/nihms772276.pdf


Except where otherwise indicated, equilibration was performed with a weak- coupling (Berendsen) thermostat33 and barostat targeted to 1 bar with isotropic position scaling as follows. With 100 kcal mol−1 Å−2 positional restraints on protein heavy atoms, structures were minimized for up to 10000 cycles and then heated at constant volume from 100 K to 300 K over 100 ps, followed by another 100 ps at 300 K. The pressure was equilibrated for 100 ps and then 250 ps with time constants of 100 fs and then 500 fs on coupling of pressure and temperature to 1 bar and 300 K, and 100 kcal mol−1 Å−2 and then 10 kcal mol−1 Å−2 Cartesian positional restraints on protein heavy atoms. The system was again minimized, with 10 kcal mol−1 Å−2 force constant Cartesian restraints on only the protein main chain N, Cα, and C for up to 10000 cycles. Three 100 ps simulations with temperature and pressure time constants of 500 fs were performed, with backbone restraints of 10 kcal mol−1 Å−2, 1 kcal mol−1 Å−2, and then 0.1 kcal mol−1 Å−2. Finally, the system was simulated unrestrained with pressure and temperature time constants of 1 ps for 500 ps with a 2 fs time step, removing center-of-mass translation and rotation every picosecond.



### CHARMM36 paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3549273/pdf/nihms395902.pdf
Each protein was solvated in a truncated octahedron simulation cell filled with TIP3P water, with nearest distance between images of 45 Å for all proteins except for lysozyme, for which the distance was 60 Å. Sodium and chloride ions were added as needed to yield a final salt concentrations of ~100 mM, with adjustments to ensure charge neutrality. For each protein, a 100-step SD energy minimization of the whole system was performed, followed by 200 ps of MD at a constant pressure of 1 bar and temperature of 300 K, in which harmonic positional restraints of 2.39 kcal/mol/Å2 were applied to each Cartesian component of each protein non-hydrogen atom using the minimized structure as a reference. Each protein was then simulated at a constant pressure of 1 bar and a temperature of 300 K for 200 ns. Pressure was regulated by a Parinello-Rahman barostat52 with a coupling time of 2.5 ps; otherwise all details were as described for Ac-(AAQAA)3-NH2 above.


### Shaytan et al. JMB 2016

All  systems  were  initially  subjected  to  energy  minimization  and  initial  equilibration  via  the  following  protocol:  (i)  1000  steps  of  energy  minimization  with  all  protein,  DNA  and  crystallographic  waters  fixed,  (ii)  10  000  minimization  steps  without  atom  fixation,  (iii)  four  rounds  of  200  ps  simulations  with  elastic  constraints  on  C-alpha  atoms  of  protein  and  N1,  N9  atoms  of  DNA  bases  which  are  gradually  relaxed  as  follows:  300->150->30->0.9  kcal/mol/A2. 

Here is NAMD file [min_equil.conf](https://github.com/intbio/MolModEdu/blob/master/MD/NAMD/nucl/nucleosome_CHARMM/simul/input/min_equil.conf)
