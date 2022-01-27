 
This repository gives the necessary instruction to run the models from the Pons et al., 2022  "Tench migration and slab buckling control the formation of the Central Andes". Nature communications
co-author :  Stephan Sobolev, Sibiao Liu , Derek Neuharth

The repository includes the parameter files (*.prm) ran with the ASPECT code that are necessary to reproduce the results of the paper as well as the initial temperature and composition files.

The adress of the ASPECT branch is  https://github.com/Minerallo/aspect/tree/Paper_slab_buckling_Andes

The branch is derived from ASPECT version 2.3.0-pre lastly rebased the 02/09/2021. 

#########  Modifications where done to the following files : 

aspect/material_model/equation_of_state/multicomponent_incompressible.cc
aspect/material_model/equation_of_state/multicomponent_incompressible.h
aspect/source/material_model/utilities.cc
aspect/source/material_model/utilities.h
aspect/source/material_model/visco_plastic.cc
aspect/source/material_model/visco_plastic.h

Additionally we implemented few custom plugins required for the model set up, the extraction of the data and the postprocessing:
aspect/source/postprocess/trench.cc (depracted)
aspect/source/postprocess/topolayer.cc
aspect/source/postprocess/composition_depth.cc
aspect/source/postprocess/composition_extent.cc
aspect/source/postprocess/subduction_velocity.cc
aspect/source/postprocess/underthrusting.cc
aspect/source/postprocess/sinking_vel_depth.cc
aspect/source/mesh_refinement/subduction.cc
aspect/source/mesh_refinement/strain_rate_abs.cc
aspect/source/mesh_deformation/fastscape.cc
aspect/source/mesh_deformation/fastscape.h
aspect/Named_VTK.f90

#########  Fastscape 

The surface mesh deformation is handled by the coupling with the Landscape Evolution Model FASTSCAPE (fortran) cloned from the master branch at commit 18f25888b16bf4cf23b00e79840bebed8b72d303 accessible at the following link. 

https://github.com/fastscape-lem/fastscapelib-fortran

The coupling is described in Neuharth, D., Brune, S., Glerum, A. C., Morley, C. K., Yuan, X., & Braun, J. (2021). Flexural strike-slip basins. 
We advise a person that want to take advantage of this coupling with the most recent feature from ASPECT to contact us. 

To install aspect with fastscape
make sure than Named_VTK.f90 is similar to our branch and placed to the aspect repository
cmake -DFASTSCAPE_DIR=/repository/of_the/fastscape_build -DCMAKE_BUILD_TYPE=repository/of/aspect
then   make 


########   Additional informations and packages relevant to achieve same results:


-- This is ASPECT, the Advanced Solver for Problems in Earth's ConvecTion.
--     . version 2.3.0-pre (Paper_slab_buckling_Andes, commit : 07a2146586508321cada3a2d8fdd4431a3220a8f)
--     . using deal.II 9.2.0
--     .       with 32 bit indices and vectorization level 1 (128 bits)
--     . using Trilinos 12.18.1
--     . using p4est 2.2.0
--     . running in OPTIMIZED mode
--     . running with 96 MPI processes

Before installing make sure to install these packages. The installation these packages can be done using "candi" at accessible on github 
https://github.com/dealii/candi/tree/dealii-9.2
then use the following command ./candi.sh --packages="p4est trilinos dealii" -j ncores
make sure than p4est trilinos are installed before dealii

#########  Models Parameter files
The repository contains the following parameter files :
.Initialzation
.S1  - Reference model (Friction 0.05)
.S2a - Subduction interface friction 0.015
.S2b - Subduction interface friction 0.035
.S2c - Subduction interface friction 0.06
.S3  - No eclogitization of the lower crust
.S4  - High thermal conduction of the upper crust

The model needs to be run first with the initalization file before restarting with the other parameter files. 
In order to initialize the model you need to indicate the adress in the parameter files of the initial compositional and themal files that are in the directory "Initial_composition_and_temperature"
#########  Statistics

With this set up for the reference model (S1) you should get the folowing statistic the following statistics at the end of the simulation with a total of 15036 timesteps.
(The HLRN had a wall time of 12 hours so the model was restarted every 12 hours until reaching 40 My of evolution)

Number of active cells: 53,247 (on 6 levels)
Number of degrees of freedom: 3,621,137 (445,644+55,985+222,822+222,822+222,822+222,822+222,822+222,822+222,822+222,822+222,822+222,822+222,822+222,822+222,822+222,822)

Number of mesh deformation degrees of freedom: 111970
Termination requested by criterion: end time
*** Snapshot created!



+----------------------------------------------+------------+------------+
| Total wallclock time elapsed since start     |  3.43e+04s |            |
|                                              |            |            |
| Section                          | no. calls |  wall time | % of total |
+----------------------------------+-----------+------------+------------+
| Assemble Stokes system           |      1524 |  1.15e+03s |       3.4% |
| Assemble composition system      |     13481 |  1.98e+04s |        58% |
| Assemble temperature system      |      1037 |  1.57e+03s |       4.6% |
| Build Stokes preconditioner      |      1524 |  1.22e+03s |       3.6% |
| Build composition preconditioner |     13481 |      93.6s |      0.27% |
| Build temperature preconditioner |      1037 |       7.3s |         0% |
| Create snapshot                  |       104 |       382s |       1.1% |
| Fastscape 1 proc                 |      1037 |       800s |       2.3% |
| Fastscape plugin                 |      1037 |       804s |       2.3% |
| Initialization                   |         1 |      19.4s |         0% |
| Mesh deformation                 |      1037 |       871s |       2.5% |
| Mesh deformation initialize      |         1 |     0.173s |         0% |
| Postprocessing                   |      1037 |   1.9e+03s |       5.5% |
| Refine mesh structure, part 1    |      1037 |       156s |      0.46% |
| Refine mesh structure, part 2    |      1037 |       117s |      0.34% |
| Setup dof systems                |      1038 |       134s |      0.39% |
| Setup matrices                   |      1037 |  1.19e+03s |       3.5% |
| Solve Stokes system              |      1524 |  4.95e+03s |        14% |
| Solve composition system         |     13481 |       440s |       1.3% |
| Solve temperature system         |      1037 |      32.3s |         0% |
+----------------------------------+-----------+------------+------------+







