# Gromacs mdp files, that can be used with charmm force field

These files are compiled for Gromacs v 2018, using
the following reference manual
http://manual.gromacs.org/documentation/current/manual-2018.3.pdf


## Simulation parameters

For CHARMM ff defaults vary (see [../README.md](../README.md)), but some consensus is:
- vdW cut-off: smothed switching between 10 and 12.
- Contimuum correction to energy and pressure outside cut-off - NOT USED
- Electrostatics: PME with  12 A real space cut-off, 1 A grid spacing, 4th order interpolation.
- Integration step 2 fs with LINCS or SHAKE only on X-H bonds.
- Thermostat: velocity rescaling or andersen (collision freq 1 ps^-1) or Nose-Hoover or Langevin themostat (fric coef. 1 ps^-1)
- Barostat: Parinello-Rahman (coupling time 2.5 ps) or Langevin piston or Monte Carlo barostat.

### Comments to the protocol


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
For CHARMM some typical protocol are decribed above (see [../README.md](../README.md)):

We'll go with the same cutom protocol we have implemented in amber example for setup consitensy.




