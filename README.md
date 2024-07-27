# preprocessing-tool
A complex geometry isosurface reconstruction algorithm for particle based CFD simulations
Title: "A complex geometry isosurface reconstruction algorithm for particle based CFD simulations"

In this paper, a new isosurface reconstruction tool has been presented for particle-based CFD methods to reconstruct
accurate complex geometry flow field and generate high quality particle distribution. This preprocessing tool using
volume image data and STL model as initial input. For volume image data, the isosurface reconstruction method MC33 
guarantees the topology correctness of the complex geometry isosurface. With the triangular surface mesh that generated 
by MC33, our preprocessing tool has demonstrated remarkable capabilities in dealing with complex geometries coming from 
volume image data. For the STL model, same as the other particle preprocessing tool, our preprocessing tool can generate 
both surface boundary particles and internal fluid particles without extra internal particle filling process. Despite 
the possible uneven particle distribution, it successfully generates an accurate initial particle distribution that covers 
the entire object’s surface, offering potential for further optimisation of particle redistribution methods. Additionally, 
during the MC cube mesh scanning process (refer to Algorithm 1 steps 2 and 3), it not only identifies mesh vertices inside 
and outside the isosurface but also efficiently achieves uniform internal fluidparticle distribution across any complex 
geometry, without incurring additional costs, which is not the case for any other current particle preprocessing tool. 
Meanwhile, the size of the cube mesh of MC33 can be easily adapted to meet the resolution requirement of CFD simulations.

As particle based numerical methods requires evenly distributed particles on the surface boundary and internal computing 
domain, we have developed a systematic mathematical description based on the optimisation theory aiming to generalise particle 
based isosurface reconstruction algorithm for both isosurface shape and particle redistribution optimisation algorithms for 
certain shape. The proposed particle redistribution algorithm not only restricts the motion of particles to the surface, but 
also gradually transforms the distribution of particles from uneven to a uniform distribution through iterations. The iterative 
optimisation algorithm has been tested on a variety of complex geometries, the results shows fast convergence with less than 100 
iterations. Furthermore, in order to quantify the efficiency of the redistribution optimisation algorithm, we use the divergence 
of distance vector and concentration gradient of the particles on the isosurfaces to compare with and without redistribution 
optimisation. The results show that it does not only improve the uniform distribution of the surface particles but also improves 
the quality of the triangular surface mesh. In order to deal with the high fidelity simulations which require tens of billions 
particles, we will start to looking into develop distributed algorithms with heterogeneous computing including GPUs in near future.

In the particle redistribution optimisation algorithm, the surface particles require updating their normal vector in each iteration 
due to the particles movement on the isosurface. We have designed the interpolation algorithm to calculate isosurface particles 
normal calculation for both volume image data and STL modes using gray value or SDF value based scalar field defined on the MC cube 
mesh vertices including updating the normal vectors for the moving boundary particles. With surface particles normal vector, we can 
also generate multi-layer boundary particles which are particularly essential for certain high-precision particle boundary conditions. 
In the mean time, we can also apply the same particle redistribution optimisation algorithm for each particle boundary layer.

We currently provide executables of the preprocessing algorithm programs containing implementations of the algorithms and test cases 
from the paper, as well as exact SDF scalar fields for more than 30 geometries as supplementary cases. The executables are generated 
in the window environment. New features of the preprocessing tool are currently being developed, so the full source code will be 
published in the future.

When you run the executable CMC33.exe, the following prompt will appear:
Which 3D complex particle flow field reconstruction algorithm do you want to choose, the CMC33, STL algorithm or Exact SDF geometry?
1.CMC33; 2.STL model; 3.Exact SDF geometry.
You can choose by entering the numbers 1, 2 and 3, where 1 and 2 correspond to the implementations of Algorithm 1 and Algorithm 2 in the 
article, respectively, and 3 is some additional standard geometry provided, for which we have accurately reconstructed the level set and 
the flow field; subsequently, you can choose the test case, where the initial flow field will be subjected to a constrained optimisation 
algorithm for obtaining a high-quality uniform particle distribution.
The resolution of the flow field can be self-defined as needed, this feature will be open in the nearest future. If you have any specific need,
or discover any problem or bug, please leave a message and we will reply as soon as possible!
