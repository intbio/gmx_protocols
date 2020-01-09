# gmx_protocols
Protocols for running MD simulations in Gromacs

## Notes on simulation parameters from original papers
### AMBER ff14SB paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4821407/pdf/nihms772276.pdf

equilibration was performed with a weak- coupling (Berendsen) thermostat33 and barostat targeted to 1 bar with isotropic position scaling as follows.

Finally, the system was simulated unrestrained with pressure and temperature time constants of 1 ps for 500 ps with a 2 fs time step, removing center-of-mass translation and rotation every picosecond.
SHAKE34 was performed on all bonds including hydrogen with the AMBER default tolerance of 10−5 Å for NVT and 10−6 Å for NVE. Non-bonded interactions were calculated directly up to 8 Å. Beyond 8 Å, electrostatic interactions were treated with cubic spline switching and the particle-mesh Ewald approximation35 in explicit solvent, with direct sum tolerances of 10−5 for NVT or 10−6 for NVE. A continuum model correction for energy and pressure was applied to long-range van der Waals interactions. The production timesteps were 2 fs for NVT and 1 fs for NVE.

NOTE: Amber manual is in agreement with this - cutoff 8A no switching.

### CHARMM36 paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3549273/pdf/nihms395902.pdf

Electrostatic interactions were computed with PME using a real-space cut-off of 12 Å and a 1 Å grid spacing and Lennard-Jones interactions were switched off smoothly between 10 and 12 Å. A Langevin thermostat with a friction coefficient of 1 ps−1 was used, with a time step of 2 fs to integrate the equations of motion. 

The equations of motion were integrated with a 2 fs time step while SHAKE was used to constrain covalent bonds involving non-water hydrogen bonds and SETTLE33 was used to maintain rigid water geometries. 

Pressure was regulated by a Parinello-Rahman barostat52 with a coupling time of 2.5 ps

### CHARMM36 DNA ff paper
https://pubs.acs.org/doi/10.1021/ct200723y
Simulated in CHARMM and NAMD. 
Unless noted, MD simulations were performed for 100 ns (Table 1) at 298 K and a pressure of 1 atm, using Hoover temperature control and the Langevin piston to maintain the pressure. The integration time step was 2 fs, and SHAKE was used to constrain X-H bonds during the simulations. For selected systems (Table 1), a lookup table was used in the evaluation of nonbonded interactions in order to speed up the simulations.48 Electrostatic interactions were calculated using the particle mesh Ewald method (PME) with a k value of 0.36 and a real space cutoff of 10 or 12 Å (Table 1). Lennard-Jones interactions were truncated at the same distance as the PME real space cutoff in the respective simulations, with smoothing over the last 2 Å using the force switch method. Nonbond atom pair lists were updated heuristically whenever any atom moved more than half the distance between the list cutoff (CUTNB) and the interaction cutoff (CTOFNB) distances.


### CHARMM36m paper - Nature Methods 2016
http://dx.doi.org/10.1038/nmeth.4067

GROMACS version 4.6.31 was used. The lengths of bonds with hydrogen atoms were constrained using the LINCS algorithm. An integration time step of 2 fs was used. A cutoff of 9.5 Å was used for the Lennard-Jones interactions and short-range electrostatic interactions. Long-range electrostatic interactions were calculated by particle-mesh Ewald summation with a grid spacing of 1.2 Å and a fourth order interpolation. The velocity rescaling thermostat was used. 

OR

MD simulations were carried out using OpenMM39 in the NPT ensemble at 300 K and 1 atm. Temperature control is performed using the Andersen thermostat with a collision frequency of 1 ps-1, and pressure control performed based on a Monte Carlo barostat. Periodic boundary conditions were applied and Lennard-Jones interactions were truncated at 12 Å with a potential switching function from 10 to 12 Å. Electrostatic interactions were calculated using the particle mesh Ewald method with a real space cutoff of 12 A on an approximately 1 Å grid with a 4th-order spline. Covalent bonds to hydrogen atoms were constrained using the constant constraint matrix approximation. The integration time step equals 2 fs and coordinates were saved every 100 ps.


## Notes on equilibration protocols from original papers
### AMBER ff14SB paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4821407/pdf/nihms772276.pdf


Except where otherwise indicated, equilibration was performed with a weak- coupling (Berendsen) thermostat33 and barostat targeted to 1 bar with isotropic position scaling as follows. With 100 kcal mol−1 Å−2 positional restraints on protein heavy atoms, structures were minimized for up to 10000 cycles and then heated at constant volume from 100 K to 300 K over 100 ps, followed by another 100 ps at 300 K. The pressure was equilibrated for 100 ps and then 250 ps with time constants of 100 fs and then 500 fs on coupling of pressure and temperature to 1 bar and 300 K, and 100 kcal mol−1 Å−2 and then 10 kcal mol−1 Å−2 Cartesian positional restraints on protein heavy atoms. The system was again minimized, with 10 kcal mol−1 Å−2 force constant Cartesian restraints on only the protein main chain N, Cα, and C for up to 10000 cycles. Three 100 ps simulations with temperature and pressure time constants of 500 fs were performed, with backbone restraints of 10 kcal mol−1 Å−2, 1 kcal mol−1 Å−2, and then 0.1 kcal mol−1 Å−2. Finally, the system was simulated unrestrained with pressure and temperature time constants of 1 ps for 500 ps with a 2 fs time step, removing center-of-mass translation and rotation every picosecond.



### CHARMM36 paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3549273/pdf/nihms395902.pdf
Each protein was solvated in a truncated octahedron simulation cell filled with TIP3P water, with nearest distance between images of 45 Å for all proteins except for lysozyme, for which the distance was 60 Å. Sodium and chloride ions were added as needed to yield a final salt concentrations of ~100 mM, with adjustments to ensure charge neutrality. For each protein, a 100-step SD energy minimization of the whole system was performed, followed by 200 ps of MD at a constant pressure of 1 bar and temperature of 300 K, in which harmonic positional restraints of 2.39 kcal/mol/Å2 were applied to each Cartesian component of each protein non-hydrogen atom using the minimized structure as a reference. Each protein was then simulated at a constant pressure of 1 bar and a temperature of 300 K for 200 ns. Pressure was regulated by a Parinello-Rahman barostat52 with a coupling time of 2.5 ps; otherwise all details were as described for Ac-(AAQAA)3-NH2 above.

### CHARMM36 DNA ff paper
https://pubs.acs.org/doi/10.1021/ct200723y
Simulated in CHARMM and NAMD. 
Systems were first energy minimized for 500 adopted-basis Newton Raphson (ANBR) steps in the presence of harmonic restraints of 5 kcal/mol/Å2 on the solute non-hydrogen atoms, followed by 20 ps NPT simulations in the presence of those restraints. Then, an additional 500 ABNR step minimization in the absence of harmonic restraints was performed, after which the production MD simulations were initiated.


### CHARMM36m paper - Nature Methods 2016
http://dx.doi.org/10.1038/nmeth.4067

Equilibration was performed at 298 K for 1 ns using Berendsen pressure coupling followed by 5 ns of simulation in the NPT ensemble using the Parrinello−Rahman algorithm.  The first 30 ns of simulation were discarded as equilibration (based on radius of gyration and hydrogen bonding).


### Shaytan et al. JMB 2016

All  systems  were  initially  subjected  to  energy  minimization  and  initial  equilibration  via  the  following  protocol:  (i)  1000  steps  of  energy  minimization  with  all  protein,  DNA  and  crystallographic  waters  fixed,  (ii)  10  000  minimization  steps  without  atom  fixation,  (iii)  four  rounds  of  200  ps  simulations  with  elastic  constraints  on  C-alpha  atoms  of  protein  and  N1,  N9  atoms  of  DNA  bases  which  are  gradually  relaxed  as  follows:  300->150->30->0.9  kcal/mol/A2. 

Here is NAMD file [min_equil.conf](https://github.com/intbio/MolModEdu/blob/master/MD/NAMD/nucl/nucleosome_CHARMM/simul/input/min_equil.conf)
