# Gromacs mdp files, that can be used with amber force field

These files are compiled for Gromacs v 2018, using
the following reference manual
http://manual.gromacs.org/documentation/current/manual-2018.3.pdf


## Simulation parameters

For AMBER ff the defaults are (see [../README.md](../README.md)):
- vdW cut-off 8A
- Contimuum correction to energy and pressure outside that cut-off
- Electrostatics: 8A real space cut-off, beyond cubic spline switching and the particle-mesh Ewald approximation in explicit solvent, with direct sum tolerances of 10−5 for NVT.
- Integration step 2 fs with SHAKE performed on all bonds including hydrogen with the AMBER default tolerance of 10−5 Å for NVT.
- Looks like in AMBER Berendsen thermostat and barostat are still used with coupling constant of 1 ps.
### Comments to the protocol
- Clearly, we need to think of changing Brendsen thermostat to something else, and probably barostat too.

## Equilibration parameters 
For AMBER ff the typical protocol is (see [../README.md](../README.md)):

- Berendsen thermostat and barostat targeted to 1 bar with isotropic position scaling.
- With 100 kcal mol−1 Å−2 positional restraints on protein heavy atoms, structures are minimized for up to 10000 cycles.
- Then heated at constant volume from 100 K to 300 K over 100 ps, followed by another 100 ps at 300 K.
- The pressure was equilibrated for 100 ps and then 250 ps with time constants of 100 fs and then 500 fs on coupling of pressure and temperature to 1 bar and 300 K, and 100 kcal mol−1 Å−2 and then 10 kcal mol−1 Å−2 Cartesian positional restraints on protein heavy atoms.
- The system was again minimized, with 10 kcal mol−1 Å−2 force constant Cartesian restraints on only the protein main chain N, Cα, and C for up to 10000 cycles. 
- Three 100 ps simulations with temperature and pressure time constants of 500 fs were performed, with backbone restraints of 10 kcal mol−1 Å−2, 1 kcal mol−1 Å−2, and then 0.1 kcal mol−1 Å−2.
- Finally, the system was simulated unrestrained with pressure and temperature time constants of 1 ps for 500 ps with a 2 fs time step, removing center-of-mass translation and rotation every picosecond.

### Comments to the protocol
Protocol may look as an overkill.
I'd probably go with the  modified JMB protocol:
- 1000 steps of energy minimization with all protein, DNA and crystallographic waters fixed - to adjust ions and added waters.
- 10 000 minimization steps with 100 kcal/mol/A2 restraints on protein heavy atoms.
- Four rounds of 200 ps simulations with elastic constraints on C-alpha atoms of protein and N1, N9 atoms of DNA bases which are gradually relaxed as follows: 100->10->1->0.1 kcal/mol/A2.

## MDP-files

### minimization.mdp
- 10 000 minimization steps with all crystal atoms fixed (prtotein, DNA, crystal waters, etc).
- 

### production_npt.mdp





## Equilibraion protocol from JMB 2016 paper
All  systems  were  initially  subjected  to  energy  minimization  and  initial  equilibration  via  the  following  protocol:  (i)  1000  steps  of  energy  minimization  with  all  protein,  DNA  and  crystallographic  waters  fixed,  (ii)  10  000  minimization  steps  without  atom  fixation,  (iii)  four  rounds  of  200  ps  simulations  with  elastic  constraints  on  C-alpha  atoms  of  protein  and  N1,  N9  atoms  of  DNA  bases  which  are  gradually  relaxed  as  follows:  300->150->30->0.9  kcal/mol/A2. 

Here is NAMD file [min_equil.conf](https://github.com/intbio/MolModEdu/blob/master/MD/NAMD/nucl/nucleosome_CHARMM/simul/input/min_equil.conf)
