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
- truncated octahedra unit cell is used for PBC
### Comments to the protocol
- Clearly, we need to think of changing Brendsen thermostat to something else, and probably barostat too.

### Excerpts from Gromacs manual
- The default MD integrator in GROMACS is the so-called leap-frog algorithm [22] for the inte-
gration of the equations of motion. When extremely accurate integration with temperature and/or
pressure coupling is required, the velocity Verlet integrators are also present and may be preferable
(see 3.4.5).
- Because the velocity and position are both defined at the same time t the velocity Verlet integrator can be used for some methods, especially rigorously correct pressure control methods, that are not actually possible with leap-frog. The integration itself takes negligibly more time than leap-frog, but twice as many communication calls are currently required. In most cases, and especially for large systems where communication speed is important for parallelization and differences between thermodynamic ensembles vanish in the 1/N limit, and when only NVT ensembles are required, leap-frog will likely be the preferred integrator. For pressure control simulations where the fine details of the thermodynamics are important, only velocity Verlet allows the true ensemble to be calculated. In either case, simulation with double precision may be required to get fine details of thermodynamics correct.
- Several other simulation packages uses multiple time stepping for bonds and/or the PME mesh forces. In GROMACS we have not implemented this (yet), since we use a different philosophy.
- GROMACS can use the weak-coupling scheme of Berendsen [26], stochastic randomization through the Andersen thermostat [27], the extended ensemble Nosé-Hoover scheme [28, 29], or a velocity-rescaling scheme [30] to simulate constant temperature, with advantages of each of the schemes laid out below.
- Just as for the Nosé-Hoover thermostat, you should realize that the Parrinello-Rahman time con- stant is not equivalent to the relaxation time used in the Berendsen pressure coupling algorithm. In most cases you will need to use a 4–5 times larger time constant with Parrinello-Rahman cou- pling.
- For Coulomb interactions we advise against using a shifted potential and for use of a reaction field or a proper long-range method such as PME.

### Suggested protocol
- Parameter description is here http://manual.gromacs.org/documentation/current/user-guide/mdp-options.html
- leap-frog
- velocity-rescale


## Equilibration parameters 
For AMBER ff the typical protocol is (see [../README.md](../README.md)):

- Berendsen thermostat and barostat targeted to 1 bar with isotropic position scaling.
- With 100 kcal mol−1 Å−2 positional restraints on protein heavy atoms, structures are minimized for up to 10000 cycles.
- Then heated at constant volume from 100 K to 300 K over 100 ps, followed by another 100 ps at 300 K.
- The pressure was equilibrated for 100 ps and then 250 ps with time constants of 100 fs and then 500 fs on coupling of pressure and temperature to 1 bar and 300 K, and 100 kcal mol−1 Å−2 and then 10 kcal mol−1 Å−2 Cartesian positional restraints on protein heavy atoms.
- The system was again minimized, with 10 kcal mol−1 Å−2 force constant Cartesian restraints on only the protein main chain N, Cα, and C for up to 10000 cycles. 
- Three 100 ps simulations with temperature and pressure time constants of 500 fs were performed, with backbone restraints of 10 kcal mol−1 Å−2, 1 kcal mol−1 Å−2, and then 0.1 kcal mol−1 Å−2.
- Finally, the system was simulated unrestrained with pressure and temperature time constants of 1 ps for 500 ps with a 2 fs time step, removing center-of-mass translation and rotation every picosecond.

### Suggested protocol
Protocol may look as an overkill.
I'd probably go with the  modified JMB protocol:
- 10 000 minimization steps with 500 kJ/mol/A2 restraints on protein heavy atoms.
- Four rounds of 200 ps simulations with elastic constraints on heavy atoms which are gradually relaxed as follows: 100->10->1->0.1 kcal/mol/A2. Due to kJ, we go with 500->50->5->0.5 kJ/mol/A2
- 200 p unrestrained

## MDP-files

- 1_minim.mdp
- 2_equil.mdp
- ...




