# Gromacs mdp files, that can be used with amber force field

These files are compiled for Gromacs v 2018, using
the following reference manual
http://manual.gromacs.org/documentation/current/manual-2018.3.pdf


 ## Generic minimization and equlibration protocols 
 
 We follow Shaytan et al. JMB 2016 paper protocol (see below).
- 10 000 minimization steps with all crystal atoms fixed (prtotein, DNA, crystal waters, etc).
-  four  rounds  of  200  ps  simulations  with  elastic  constraints  on  C-alpha  atoms  of  protein  and  N1,  N9  atoms  of  DNA  bases  which  are  gradually  relaxed  as  follows:  300->150->30->0.9  kcal/mol/A2. 

## Force filed specific options


## MDP-files

### minimization.mdp
- 10 000 minimization steps with all crystal atoms fixed (prtotein, DNA, crystal waters, etc).
- 

### production_npt.mdp





## Equilibraion protocol from JMB 2016 paper
All  systems  were  initially  subjected  to  energy  minimization  and  initial  equilibration  via  the  following  protocol:  (i)  1000  steps  of  energy  minimization  with  all  protein,  DNA  and  crystallographic  waters  fixed,  (ii)  10  000  minimization  steps  without  atom  fixation,  (iii)  four  rounds  of  200  ps  simulations  with  elastic  constraints  on  C-alpha  atoms  of  protein  and  N1,  N9  atoms  of  DNA  bases  which  are  gradually  relaxed  as  follows:  300->150->30->0.9  kcal/mol/A2. 

Here is NAMD file [min_equil.conf](https://github.com/intbio/MolModEdu/blob/master/MD/NAMD/nucl/nucleosome_CHARMM/simul/input/min_equil.conf)