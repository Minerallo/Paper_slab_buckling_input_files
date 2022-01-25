 
This repository gives the necessary instruction to run the models from the Pons et al., 2022  "Central Andes formation controlled by trench migration and slab buckling". Nature communication

The repository includes the parameter files (*.prm) ran with the ASPECT code that are necessary to reproduce the results of the paper as well as the initial temperature and composition files.

The adress of the ASPECT branch is  https://github.com/Minerallo/aspect/tree/Paper_slab_buckling_Andes

The branch is derived from ASPECT version 2.3.0-pre lastly rebased the 02/09/2021. 

Modifications where done to the following files : 
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

The surface mesh deformation is handled by the coupling with the Landscape Evolution Model FASTSCAPE thats is accessible at the following link. 

https://github.com/fastscape-lem/fastscape

The coupling is described in Neuharth, D., Brune, S., Glerum, A. C., Morley, C. K., Yuan, X., & Braun, J. (2021). Flexural strike-slip basins. 
We advise a person that want to take advantage of this coupling with the most recent feature from ASPECT to contact us. 


Information relevant to achieve same results.
-- This is ASPECT, the Advanced Solver for Problems in Earth's ConvecTion.
--     . version 2.3.0-pre (Paper_slab_buckling_Andes, commit : 07a2146586508321cada3a2d8fdd4431a3220a8f)
--     . using deal.II 9.2.0
--     .       with 32 bit indices and vectorization level 1 (128 bits)
--     . using Trilinos 12.18.1
--     . using p4est 2.2.0
--     . running in OPTIMIZED mode
--     . running with 96 MPI processes






