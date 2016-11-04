.. _theory:

Background theory
=================

**UNDER CONSTRUCTION**

Inversion methodology
---------------------

Let the set of extracted anomaly data be :math:`\mathbf{d} = (d_1,d_2,...,d_N)^T` and the density contrast of cells in the model be :math:`\mathbf{\rho} = (\kappa_1,\kappa_2,...,\kappa_M)^T`. The two are related by the sensitivity matrix

.. _sens_:
.. math::
   \mathbf{d}= \left[\mathbf{G}_x ~~ \mathbf{G}_y ~~\mathbf{G}_z\right] \left[
       \begin{array}[c]{l}
           \kappa_x \\
           \kappa_y \\
           \kappa_z 
       \end{array}
       \right]


Each matrix has elements :math:`g_{ij}` which quantify the contribution to the :math:`i^{th}` datum due to a unit susceptibility in the :math:`j^{th}` cell. The ``mvisen`` program performs the calculation of each sensitivity matrix, which are used by the subsequent inversion. The sensitivity matrix provides the forward mapping from the model to the data during the entire inverse process. We will discuss its efficient representation via the wavelet transform in a separate section. 

For the inversion, the first question that arises concerns definition of the "model". We choose a vector of susceptibility, :math:`\rho`, as the model for since the anomalous field is directly proportional to the density contrast. The inverse problem is formulated as an optimization problem where a global objective function, :math:`\phi`, is minimized subject to the constraints in equation :eq:`sens`. The global objective functions consists of two components: a model objective function, :math:`\phi_m`, and a data misfit function, :math:`\phi_d`, such that

.. _globphi_:
.. math::
    \begin{aligned}
    \min \phi = \phi_d+\beta\phi_m \\
    \mbox{s. t. } \rho^l\leq \rho \leq \rho^u, \nonumber
    \end{aligned}
    :label: globphi

where :math:`\beta` is a trade off parameter that controls the relative importance of the model smoothness through the model objective function and data misfit function. When the standard deviations of data errors are known, the acceptable misfit is given by the expected value :math:`\phi_d` and we will search for the value of :math:`\beta` via an L-curve criterion :cite:`Hansen00` that produces the expected misfit. Otherwise, a user-defined value is used. Bound are imposed through the projected gradient method so that the recovered model lies between imposed lower (:math:`\rho^l`) and upper (:math:`\rho^u`) bounds.

We next discuss the construction of a model objective function which, when minimized, produces a model that is geophysically interpretable. The objective function gives the flexibility to incorporate as little or as much information as possible. At the very minimum, this function drives the solution towards a reference model :math:`\rho_o` and requires that the model be relatively smooth in the three spatial directions. Here we adopt a right handed Cartesian coordinate system with positive north and positive down. Let the model objective function be

.. _mof:
.. math::
     \begin{aligned} \phi_m(\rho) &=& \alpha_s\int\limits_V w_s\left\{w(\mathbf{r})[\rho(\mathbf{r})-{\rho}_o] \right\}^2dv + \alpha_x\int\limits_V w_x \left\{\frac{\partial w(\mathbf{r})[\rho(\mathbf{r})-{\rho}_o]}{\partial x}\right\}^2dv \\ \nonumber
     &+& \alpha_y\int\limits_V w_y\left\{\frac{\partial w(\mathbf{r})[\rho(\mathbf{r})-{\rho}_o]}{\partial y}\right\}^2dv +\alpha_z\int\limits_V\ w_z\left\{\frac{\partial w(\mathbf{r})[\rho(\mathbf{r})-{\rho}_o]}{\partial z}\right\}^2dv, \end{aligned}
     :label: mof

where the functions :math:`w_s`, :math:`w_x`, :math:`w_y` and :math:`w_z` are spatially dependent, while :math:`\alpha_s`, :math:`\alpha_x`, :math:`\alpha_y` and :math:`\alpha_z` are coefficients, which affect the relative importance of different components in the objective function. The reference model is given as :math:`\rho_o` and :math:`w(\mathbf{r})` is a generalized depth weighting function. The purpose of this function is to counteract the geometrical decay of the sensitivity with the distance from the observation location so that the recovered density contrast is not concentrated near the observation locations. The details of the depth weighting function will be discussed in the next section.

The objective function in equation :eq:`mof` has the flexibility to incorporate many types of prior knowledge into the inversion. The reference model may be a general background model that is estimated from previous investigations or it will be a zero model. The reference model would generally be included in the first component of the objective function but it can be removed if desired from the remaining terms; often we are more confident in specifying the value of the model at a particular point than in supplying an estimate of the gradient. The choice of whether or not to include :math:`\rho_o` in the derivative terms can have significant effect on the recovered model as shown through the synthetic example. The relative closeness of the final model to the reference model at any location is controlled by the function :math:`w_s`. For example, if the interpreter has high confidence in the reference model at a particular region, he can specify :math:`w_s` to have increased amplitude there compared to other regions of the model. The weighting functions :math:`w_x`, :math:`w_y`, and :math:`w_z` can be designed to enhance or attenuate gradients in various regions in the model domain. If geology suggests a rapid transition zone in the model, then a decreased weighting on particular derivatives of the model will allow for higher gradients there and thus provide a more geologic model that fits the data.

Numerically, the model objective function in equation :eq:`mof` is discretized onto the mesh defining the density contrast model using a finite difference approximation. This yields:

.. _modobjdiscr_:
.. math::
    \begin{aligned}
    \phi_m(\mathbf{\rho}) = (\mathbf{\rho}-\mathbf{\rho}_o)^T(\alpha_s \mathbf{W}_s^T\mathbf{W}_s+\alpha_x \mathbf{W}_x^T\mathbf{W}_x+\alpha_y \mathbf{W}_y^T\mathbf{W}_y+\alpha_z \mathbf{W}_z^T\mathbf{W}_z)(\mathbf{\rho}-\mathbf{\rho}_o), \nonumber\\
    \equiv(\mathbf{\rho}-\mathbf{\rho}_o)^T\mathbf{W}_m^T\mathbf{W}_m(\mathbf{\rho}-\mathbf{\rho}_o), \nonumber\\
    =\left \| \mathbf{W}_m(\mathbf{\rho}-\mathbf{\rho}_o) \right \|^2,\end{aligned}
    :label: modobjdiscr


where :math:`\mathbf{\rho}` and :math:`\mathbf{\rho}_o` are :math:`M`-length vectors representing the recovered and reference models, respectively. Similarly, there is an option to remove to the reference model from the spatial derivatives in equation :eq:`modobjdiscr` such that

.. _modobjdiscrOut_:
.. math::
     \begin{aligned}
     \phi_m(\mathbf{\rho}) = (\mathbf{\rho}-\mathbf{\rho}_o)^T(\alpha_s \mathbf{W}_s^T\mathbf{W}_s)(\mathbf{\rho}-\mathbf{\rho}_o) + \mathbf{\rho}^T(\alpha_x \mathbf{W}_x^T\mathbf{W}_x+\alpha_y \mathbf{W}_y^T\mathbf{W}_y+\alpha_z \mathbf{W}_z^T\mathbf{W}_z)\mathbf{\rho}, \nonumber \\
     \equiv (\mathbf{\rho}-\mathbf{\rho}_o)^T\mathbf{W}_s^T\mathbf{W}_s(\mathbf{\rho}-\mathbf{\rho}_o) + \mathbf{\rho}^T\mathbf{W}_m^T\mathbf{W}_m\mathbf{\rho}, \nonumber\\
     =\left \| \mathbf{W}_s(\mathbf{\rho}-\mathbf{\rho}_o) + \mathbf{W}_m\mathbf{\rho}\right \|^2.
     \end{aligned}
     :label: modobjdiscrOut

In the previous two equations, the individual matrices :math:`\mathbf{W}_s`, :math:`\mathbf{W}_x`, :math:`\mathbf{W}_y`, and :math:`\mathbf{W}_z` are straight-forwardly calculated once the model mesh and the weighting functions :math:`w(\mathbf{r})` and :math:`w_s` , :math:`w_x`, :math:`w_y`, :math:`w_z` are defined. The cumulative matrix :math:`\mathbf{W}_m^T\mathbf{W}_m` is then formed for the chosen configuration.

The next step in setting up the inversion is to define a misfit measure. Here we use the :math:`l_2`-norm measure

.. _phid_:
.. math::
    \phi_d = \left\| \mathbf{W}_d(\mathbf{G}\mathbf{\rho}-\mathbf{d})\right\|^2.
    :label: phid

For the work here, we assume that the contaminating noise on the data is independent and Gaussian with zero mean. Specifying :math:`\mathbf{W}_d` to be a diagonal matrix whose :math:`i^{th}` element is :math:`1/\sigma_i`, where :math:`\sigma_i` is the standard deviation of the :math:`i^{th}` datum makes :math:`\phi_d` a chi-squared distribution with :math:`N` degrees of freedom. The optimal data misfit for data contaminated with independent, Gaussian noise has an expected value of :math:`E[\chi^2]=N`, providing a target misfit for the inversion. We now have the components to solve the inversion as defined in equation :eq:`globphi`.

To solve the optimization problem when constraints are imposed we use the projected gradients method :cite:`CalamaiMore87,Vogel02`. This technique forces the gradient in the Krylov sub-space minimization (in other words a step during the conjugate gradient process) to zero if the proposed step would make a model parameter exceed the bound constraints. The result is a model that reaches the bounds, but does not exceed them. This method is computationally faster than the log-barrier method because (1) model parameters on the bounds are neglected for the next iteration and (2) the log-barrier method requires the calculation of a barrier term. Previous versions of Â used the logarithmic barrier method :cite:`Wright97,NocedalWright99`.

The weighting function is generated by the program that is in turn given as input to the sensitivity generation program . This gives the user full flexibility in using customized weighting functions. This program allows user to specify whether to use a generalized depth weighting or a distance-based weighting that is useful in regions of largely varying topography. Distance weighting is required to be used when borehole data are present.

Depth Weighting and Distance Weighting
--------------------------------------

It is a well-known fact that vertical gravity data have no inherent depth resolution. A numerical consequence of this is that when an inversion is performed, which minimizes :math:`\int m(\mathbf{r})^2 dv`, subject to fitting the data, the constructed density contrast is concentrated close to the observation locations. This is a direct manifestation of the kernel's decay with the distance between the cell and observation locations. Because of the rapidly diminishing amplitude, the kernels of gravity data are not sufficient to generate a function, which possess significant structure at locations that are far away from observations. In order to overcome this, the inversion requires a weighting to counteract this natural decay. Intuitively, such a weighting will be the inverse of the approximate geometrical decay. This give cells at all locations equal probability to enter into the solution with a non-zero density contrast.

.. _depthWeight:

Depth weighting for surface or airborne data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The sensitivity decays predominantly as a function of depth for surface data. Numerical experiments indicate that a function of the form :math:`(z+z_o)^{-2}` closely approximates the kernel's decay directly under the observation point provided that a reasonable value is chosen for :math:`z_o`. The value of 2 in the exponent is consistent with the fact that, to first order, a cuboidal cell acts like a dipole source whose magnetic field decays as inverse distance cubed. The value of :math:`z_o` can be obtained by matching the function 1/\ :math:`(z+z_o)^2` with the field produced at an observation point by a column of cells. Thus we use a depth weighting function of the form

.. math:: w(\mathbf{r}_j)=\left[\frac{1}{\Delta z_{j}}\int\limits_{\Delta z_{ij}}\frac{dz}{(z+z_o)^\alpha}\right]^{1/2}, ~~ j=1,...,M.
     :label: depthw

For the inversion of surface data, where :math:`\alpha=2`, :math:`\mathbf{r}_j` is used to identify the :math:`j^{th}` cell, and :math:`\Delta z_j` is its thickness. This weighting function is normalized so that the maximum value is unity. Numerical tests indicate that when this weighting is used, the susceptibility model constructed by minimizing the model objective function in equation [eq:mof], subject to fitting the data, places the recovered anomaly at approximately the correct depth.

If the data set involves highly variable observation heights the normal depth weighting function might not be most suitable. Distance weighting used for borehole data may be more appropriate as explained in the next section.

.. _distWeight:

Distance weighting for borehole data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For data sets that contain borehole measurements, the sensitivities do not have a predominant decay direction, therefore a weighting function that varies in three dimensions is needed. We generalize the depth weighting used in surface data inversion to form such a 3D weighting function called distance weighting: 

.. math::
      w(\mathbf{r}_j)=\frac{1}{\sqrt{\Delta V_{j}}} \left\{\sum_{i=1}^{N}\left[\int\limits_{\Delta V_{j}}\frac{dv}{(R_{ij}+R_o)^\alpha}\right]^{2}\right\}^{1/4}, ~~j=1,...,M,
      :label: distw

where :math:`\alpha=2`, :math:`V_j` is the volume of :math:`j^{th}` cell, :math:`R_{ij}` is the distance between a point within the source volume and the :math:`i^{th}` observation, and :math:`R_o` is a small constant used to ensure that the integral is well-defined (chosen to be a quarter of the smallest cell dimension). This weighting function is also normalized to have a maximum value of unity. For inversion of borehole data, it is necessary to use this more general weighting. This weighting function is also advantageous if surface data with highly variable observation heights are inverted.


.. _waveletSection:

Wavelet Compression of Sensitivity Matrix
-----------------------------------------

The two major obstacles to the solution of a magnetization vector inversion (MVI) problem are the large amount of memory required for storing the three separate sensitivity matrices and the CPU time required for the application of the sensitivity matrices to model vectors. The MVI program library overcomes these difficulties by forming a sparse representation of the sensitivity matrix using a wavelet transform based on compactly supported, orthonormal wavelets. For more details, the users are referred to :cite:`LiOldenburg03,LiOldenburg10`. In the following, we give a brief description of the method necessary for the use of the GRAV3D library.

Each row of the sensitivity matrix in a 3D magnetic inversion can be treated as a 3D image and a 3D wavelet transform can be applied to it. By the properties of the wavelet transform, most transform coefficients are nearly or identically zero. When coefficients of small magnitudes are discarded (the process of thresholding), the remaining coefficients still contain much of the necessary information to reconstruct the sensitivity accurately. These retained coefficients form a sparse representation of the sensitivity in the wavelet domain. The need to store only these large coefficients means that the memory requirement is reduced. Further, the multiplication of the sensitivity with a vector can be carried out by a sparse multiplication in the wavelet domain. This greatly reduces the CPU time. Since the matrix-vector multiplication constitutes the core computation of the inversion, the CPU time for the inverse solution is reduced accordingly. The use of this approach increases the size of solvable problems by nearly two orders of magnitude.

Let :math:`\mathbf{G}` be the sensitivity matrix and :math:`\mathcal{W}` be the symbolic matrix-representation of the 3D wavelet transform. Then applying the transform to each row of :math:`\mathbf{G}` and forming a new matrix consisting of rows of transformed sensitivity is equivalent to the following operation:

.. math::
     \widetilde{\mathbf{G}}=\mathbf{G}\mathcal{W}^T,
     :label: senswvt

where :math:`\widetilde{\mathbf{G}}` is the transformed matrix. The thresholding is applied to individual rows of :math:`\mathbf{G}` by the following rule to form the sparse representation :math:`\widetilde{\mathbf{G}}^S`,

.. math::
     \widetilde{g}_{ij}^{s}=\begin{cases} \widetilde{g}_{ij} & \mbox{if } \left|\widetilde{g}_{ij}\right| \geq \delta _i \\
     0 & \mbox{if } \left|\widetilde{g}_{ij}\right| < \delta _i
     \end{cases}, ~~ i=1,\ldots,N,
     :label: elemg


where :math:`\delta _i` is the threshold level, and :math:`\widetilde{g}_{ij}` and :math:`\widetilde{g}_{ij}^{s}` are the elements of :math:`\widetilde{\mathbf{G}}` and :math:`\widetilde{\mathbf{G}}^S`, respectively. The threshold level :math:`\delta _i` are determined according to the allowable error of the reconstructed sensitivity, which is measured by the ratio of norm of the error in each row to the norm of that row, :math:`r_i(\delta_i)`. It can be evaluated directly in the wavelet domain by the following expression:

.. math:: 
    r_i(\delta_i)=\sqrt{\frac{\underset{\left | {\widetilde{g}_{ij}} \right |<\delta_i}\sum{\widetilde{g}_{ij}}^2}{\underset{j}\sum{\widetilde{g}_{ij}^2}}}, ~~i=1,\ldots,N,
    :label: rhoi


Here the numerator is the norm of the discarded coefficients and the denominator is the norm of all coefficients. The threshold level :math:`\delta_{i_o}` is calculated on a representative row, :math:`i_o`. This threshold is then used to define a relative threshold :math:`\epsilon =\delta_{i_{o}}/ \underset{j}{\max}\left | {\widetilde{g}_{ij}} \right |`. The absolute threshold level for each row is obtained by

.. math::
     \delta_i = \epsilon \underset{j}{\max}\left | {\widetilde{g}_{ij}} \right|, ~~i=1,\ldots,N.
     :label: deltai

The program that implements this compression procedure is :ref:`mvisen`. The user is asked to specify the relative error :math:`r^*` and the program will determine the relative threshold level :math:`\delta_i`. Usually a value of a few percent is appropriate for :math:`r^*`. When both surface and borehole data are present, two different relative threshold levels are calculated by choosing a representative row for surface data and another for borehole data. For experienced users and ones that are re-inverting the data, the program also allows the direct input of the relative threshold level.

