:tocdepth: 3

.. _case_settings:

Case Settings
=====================

There are two important files that define the case, **cice.settings** and 
**ice_in**.  **cice.settings** is a list of env variables that define many
values used to setup, build and run the case.  **ice_in** is the input namelist file
for CICE.  Variables in both files are described below.

.. _tabsettings:

Table of CICE Settings
--------------------------

The **cice.settings** file is reasonably well self documented.  Several of
the variables defined in the file are not used in CICE.  They exist
to support the CICE model.

.. csv-table:: *CICE settings*
   :header: "variable", "options/format", "description", "recommended value"
   :widths: 15, 15, 25, 20

   "ICE_CASENAME", "string", "case name", "set by cice.setup"
   "ICE_SANDBOX", "string", "sandbox directory", "set by cice.setup"
   "ICE_MACHINE", "string", "machine name", "set by cice.setup"
   "ICE_COMPILER", "string", "environment name", "set by cice.setup"
   "ICE_MACHCOMP", "string", "machine_environment name", "set by cice.setup"
   "ICE_SCRIPTS", "string", "scripts directory", "set by cice.setup"
   "ICE_CASEDIR", "string", "case directory", "set by cice.setup"
   "ICE_RUNDIR", "string", "run directory", "set by cice.setup"
   "ICE_OBJDIR", "string", "compile directory", "${ICE_RUNDIR}/compile"
   "ICE_RSTDIR", "string", "unused", "${ICE_RUNDIR}/restart"
   "ICE_HSTDIR", "string", "unused", "${ICE_RUNDIR}/history"
   "ICE_LOGDIR", "string", "log directory", "${ICE_CASEDIR}/logs"
   "ICE_DRVOPT", "string", "unused", "cice"
   "ICE_IOTYPE", "string", "I/O format", "set by cice.setup"
   " ", "netcdf", "serial netCDF"
   " ", "pio", "parallel netCDF"
   " ", "none", "netCDF library is not available"
   "ICE_CLEANBUILD", "true, false", "automatically clean before building", "true"
   "ICE_CPPDEFS", "user defined preprocessor macros for build", "null"
   "ICE_QUIETMODE", "true, false", "reduce build output to the screen", "false"
   "ICE_GRID", "string (see below)", "grid", "set by cice.setup"
   " ", "gx3", "3-deg displace-pole (Greenland) global grid", " "
   " ", "gx1", "1-deg displace-pole (Greenland) global grid", " "
   " ", "tx1", "1-deg tripole global grid", " "
   " ", "gbox80", "80x80 box", " "
   " ", "gbox128", "128x128 box", " "
   "ICE_NTASKS", "integer", "number of tasks, must be set to 1", "set by cice.setup"
   "ICE_NTHRDS", "integer", "number of threads per task, must be set to 1", "set by cice.setup"
   "ICE_TEST", "string", "test setting if using a test", "set by cice.setup"
   "ICE_TESTNAME", "string", "test name if using a test", "set by cice.setup"
   "ICE_BASELINE", "string", "baseline directory name, associated with cice.setup -bdir ", "set by cice.setup"
   "ICE_BASEGEN", "string", "baseline directory name for regression generation, associated with cice.setup -bgen ", "set by cice.setup"
   "ICE_BASECOM", "string", "baseline directory name for regression comparison, associated with cice.setup -bcmp ", "set by cice.setup"
   "ICE_BFBCOMP", "string", "location of case for comparison, associated with cice.setup -td", "set by cice.setup"
   "ICE_SPVAL", "string", "special value for cice.settings strings", "set by cice.setup"
   "ICE_RUNLENGTH", "integer (see below)", "batch run length default", "set by cice.setup"
   " ", "-1", "15 minutes (default)", " "
   " ", "0", "30 minutes", " "
   " ", "1", "59 minutes", " "
   " ", "2", "2 hours", " "
   " ", "other :math:`2 < N < 8`", "N hours", " "
   " ", "8 or larger", "8 hours", " "
   "ICE_ACCOUNT", "string", "batch account number", "set by cice.setup, .cice_proj or by default"
   "ICE_QUEUE", "string", "batch queue name", "set by cice.setup or by default"
   "ICE_THREADED", "true, false", "force threading in compile, will always compile threaded if ICE_NTHRDS :math:`> 1`", "false"
   "ICE_BLDDEBUG", "true, false", "turn on compile debug flags", "false"
   "ICE_CODECOV", "true,false", "turn on code coverage flags", "false"


.. _tabnamelist:


Table of namelist options
-------------------------------

.. csv-table:: *Namelist options*
   :header: "also in Icepack","variable", "options/format", "description", "recommended value"
   :widths: 5, 15, 15, 30, 15 

   "","", "", "", ""
   "","*setup_nml*", "", "", ""
   "","", "", "**Time, Diagnostics**", ""
   "\*","``days_per_year``", "``360`` or ``365``", "number of days in a model year", "365"
   "\*","``use_leap_years``", "true/false", "if true, include leap days", ""
   "\*","``year_init``", "yyyy", "the initial year, if not using restart", ""
   "\*","``istep0``", "integer", "initial time step number", "0"
   "\*","``dt``", "seconds", "thermodynamics time step length", "3600."
   "\*","``npt``", "integer", "total number of time steps to take", ""
   "\*","``ndtd``", "integer", "number of dynamics/advection/ridging/steps per thermo timestep", "1"
   "","", "", "**Initialization/Restarting**", ""
   "","``runtype``", "``initial``", "start from ``ice_ic``", ""
   "","", "``continue``", "restart using ``pointer_file``", ""
   "\*","``ice_ic``", "``default``", "latitude and sst dependent", "default"
   "","", "``none``", "no ice", ""
   "","", "path/file", "restart file name", ""
   "","``restart``", "true/false", "initialize using restart file", "``.true.``"
   "","``use_restart_time``", "true/false", "set initial date using restart file", "``.true.``"
   "","``restart_format``", "string", "restart file format", "default"
   "","", "default", "read/write restart files in default format", ""
   "","", "pio_pnetcdf", "read/write restart files with pnetcdf in pio", ""
   "","``lcdf64``", "true/false", "if true, use 64-bit  format", ""
   "","``numin``", "integer", "minimum internal IO unit number", "11"
   "","``numax``", "integer", "maximum internal IO unit number", "99"
   "\*","``restart_dir``", "path/", "path to restart directory", ""
   "","``restart_ext``", "true/false", "read/write halo cells in restart files", ""
   "","``restart_file``", "filename prefix", "output file for restart dump", "‘iced’"
   "","``pointer_file``", "pointer filename", "contains restart filename", ""
   "\*","``dumpfreq``", "``y``", "write restart every ``dumpfreq_n`` years", "y"
   "","", "``m``", "write restart every ``dumpfreq_n`` months", ""
   "","", "``d``", "write restart every ``dumpfreq_n`` days", ""
   "","", "``h``", "write restart every ``dumpfreq_n`` hours", ""
   "","", "``1``", "write restart every ``dumpfreq_n`` time step", ""
   "","``dumpfreq_n``", "integer", "frequency restart data is written", "1"
   "\*","``dump_last``", "true/false", "if true, write restart on last time step of simulation", ""
   "","", "", "**Model Output**", ""
   "","``bfbflag``", "off/lsum4/lsum8/lsum16/ddpdd/reprosum", "global sum methods", "off"
   "\*","``diagfreq``", "integer", "frequency of diagnostic output in ``dt``", "24"
   "","", "*e.g.*, 10", "once every 10 time steps", ""
   "\*","``diag_type``", "``stdout``", "write diagnostic output to stdout", ""
   "","", "``file``", "write diagnostic output to file", ""
   "","``diag_file``", "filename", "diagnostic output file (script may reset)", ""
   "","``conserv_check``", "true/false", "check conservation", "``.false.``"
   "","``print_global``", "true/false", "print diagnostic data, global sums", "``.false.``"
   "","``print_points``", "true/false", "print diagnostic data for two grid points", "``.false.``"
   "","``latpnt``", "real", "latitude of (2) diagnostic points", "" 
   "","``lonpnt``", "real", "longitude of (2) diagnostic points", ""
   "","``dbug``", "true/false", "if true, write extra diagnostics", "``.false.``"
   "","``histfreq``", "string array", "defines output frequencies", ""
   "","", "``y``", "write history every ``histfreq_n`` years", ""
   "","", "``m``", "write history every ``histfreq_n`` months", ""
   "","", "``d``", "write history every ``histfreq_n`` days", ""
   "","", "``h``", "write history every ``histfreq_n`` hours", ""
   "","", "``1``", "write history every ``histfreq_n`` time step", ""
   "","", "``x``", "unused frequency stream (not written)", ""
   "","``histfreq_n``", "integer array", "frequency history output is written", ""
   "","", "0", "do not write to history", ""
   "","``hist_avg``", "true", "write time-averaged data", "``.true.``"
   "","", "false", "write snapshots of data", ""
   "","``history_dir``", "path/", "path to history output directory", ""
   "","``history_file``", "filename prefix", "output file for history", "‘iceh’"
   "","``history_precision``", "integer", "history file precision: 4 or 8 byte", "4"
   "","``history_format``", "string", "history file format", "default"
   "","", "default", "read/write restart files in default format", ""
   "","", "pio_pnetcdf", "read/write restart files with pnetcdf in pio", ""
   "","``write_ic``", "true/false", "write initial condition", ""
   "","``incond_dir``", "path/", "path to initial condition directory", ""
   "","``incond_file``", "filename prefix", "output file for initial condition", "‘iceh’"
   "","``runid``", "string", "label for run (currently CESM only)", ""
   "","", "", "", ""
   "","*grid_nml*", "", "", ""
   "","", "", "**Grid**", ""
   "","``grid_format``", "``nc``", "read  grid and kmt files", "‘bin’"
   "","", "``bin``", "read direct access, binary file", ""
   "","``grid_type``", "``rectangular``", "defined in *rectgrid*", ""
   "","", "``displaced_pole``", "read from file in *popgrid*", ""
   "","", "``tripole``", "read from file in *popgrid*", ""
   "","", "``regional``", "read from file in *popgrid*", ""
   "","``grid_file``", "filename", "name of grid file to be read", "‘grid’"
   "","``bathymetry_file``", "filename", "name of bathymetry file to be read", "‘grid’"
   "","``use_bathymetry``", "true/false", "use read in bathymetry file for basalstress option", ""
   "","``kmt_file``", "filename", "name of land mask file to be read", "‘kmt’"
   "","``gridcpl_file``", "filename", "input file for coupling grid info", ""
   "\*","``kcatbound``", "``0``", "original category boundary formula", "0"
   "","", "``1``", "new formula with round numbers", ""
   "","", "``2``", "WMO standard categories", ""
   "","", "``-1``", "one category", ""
   "","``dxrect``", "real", "x-direction grid spacing (cm) for rectangular grid", ""
   "","``dyrect``", "real", "y-direction grid spacing (cm) for rectangular grid", ""
   "","``ncat``", "integer", "number of ice thickness categories", "5"
   "","``nfsd``", "integer", "number of floe size categories", "12 for prognostic FSD; 1 otherwise"
   "","``nilyr``", "integer", "number of vertical layers in ice", "7"
   "","``nslyr``", "integer", "number of vertical layers in snow", "1"
   "","``nblyr``", "integer", "number of zbgc layers", "7"
   "","", "", "", ""
   "","*domain_nml*", "", "", ""
   "","", "", "**Domain**", ""
   "","``nprocs``", "integer", "number of processors to use", ""
   "","``nx_global``", "integer", "global grid size in x direction", ""
   "","``ny_global``", "integer", "global grid size in y direction", ""
   "","``block_size_x``", "integer", "block size in x direction", ""
   "","``block_size_y``", "integer", "block size in y direction", ""
   "","``max_blocks``", "integer", "maximum number of blocks per MPI task for memory allocation", ""
   "","``processor_shape``", "``slenderX1``", "1 processor in the y direction (tall, thin)", ""
   "","", "``slenderX2``", "2 processors in the y direction (thin)", ""
   "","", "``square-ice``", "more processors in x than y, :math:`\sim` square", ""
   "","", "``square-pop``", "more processors in y than x, :math:`\sim` square", ""
   "","``distribution_type``", "``cartesian``", "distribute blocks in 2D Cartesian array", ""
   "","", "``roundrobin``", "1 block per proc until blocks are used", ""
   "","", "``sectcart``", "blocks distributed to domain quadrants", ""
   "","", "``sectrobin``", "several blocks per proc until used", ""
   "","", "``rake``", "redistribute blocks among neighbors", ""
   "","", "``spacecurve``", "distribute blocks via space-filling curves", ""
   "","", "``spiralcenter``", "distribute blocks via roundrobin from center of grid outward in a spiral", ""
   "","", "``wghtfile``", "distribute blocks based on weights specified in ``distribution_wght_file``", ""
   "","``distribution_wght``", "``block``", "full block size sets ``work_per_block``", ""
   "","", "``latitude``", "latitude/ocean sets ``work_per_block``", ""
   "","``distribution_wght_file``", "filename", "distribution weight file when distribution_type is ``wghtfile``", ""
   "","``ew_boundary_type``", "``cyclic``", "periodic boundary conditions in x-direction", ""
   "","", "``open``", "Dirichlet boundary conditions in x", ""
   "","``ns_boundary_type``", "``cyclic``", "periodic boundary conditions in y-direction", ""
   "","", "``open``", "Dirichlet boundary conditions in y", ""
   "","", "``tripole``", "U-fold tripole boundary conditions in y", ""
   "","", "``tripoleT``", "T-fold tripole boundary conditions in y", ""
   "","``maskhalo_dyn``", "true/false", "mask unused halo cells for dynamics", ""
   "","``maskhalo_remap``", "true/false", "mask unused halo cells for transport", ""
   "","``maskhalo_bound``", "true/false", "mask unused halo cells for boundary updates", ""
   "","", "", "", ""
   "","*tracer_nml*", "", "", ""
   "","", "", "**Tracers**", ""
   "","``n_aero``", "integer", "number of aerosol tracers", "1"
   "","``n_iso``", "integer", "number of isotope tracers", "1"
   "","``n_zaero``", "0,1,2,3,4,5,6", "number of z aerosol tracers in use", "0"
   "","``n_algae``", "0,1,2,3", "number of algal tracers", "0"
   "","``n_doc``", "0,1,2,3", "number of dissolved organic carbon", "0"
   "","``n_dic``", "0,1", "number of dissolved inorganic carbon", "0"
   "","``n_don``", "0,1", "number of dissolved organize nitrogen", "0"
   "","``n_fed``", "0,1,2", "number of dissolved iron tracers", "0"
   "","``n_fep``", "0,1,2", "number of particulate iron tracers", "0"
   "\*","``tr_iage``", "true/false", "ice age", ""
   "","``restart_age``", "true/false", "restart tracer values from file", ""
   "\*","``tr_FY``", "true/false", "first-year ice area", ""
   "","``restart_FY``", "true/false", "restart tracer values from file", ""
   "\*","``tr_lvl``", "true/false", "level ice area and volume", ""
   "","``restart_lvl``", "true/false", "restart tracer values from file", ""
   "\*","``tr_pond_cesm``", "true/false", "CESM melt ponds", ""
   "","``restart_pond_cesm``", "true/false", "restart tracer values from file", ""
   "\*","``tr_pond_topo``", "true/false", "topo melt ponds", ""
   "","``restart_pond_topo``", "true/false", "restart tracer values from file", ""
   "\*","``tr_pond_lvl``", "true/false", "level-ice melt ponds", ""
   "","``restart_pond_lvl``", "true/false", "restart tracer values from file", ""
   "\*","``tr_aero``", "true/false", "aerosols", ""
   "","``restart_aero``", "true/false", "restart tracer values from file", ""
   "\*","``tr_iso``", "true/false", "isotopes", ""
   "","``restart_iso``", "true/false", "restart tracer values from file", ""
     "\*","``tr_fsd``", "true/false", "floe size distribution", ""
   "","``restart_fsd``", "true/false", "restart floe size distribution values from file", ""
   "","", "", "", ""
   "","*thermo_nml*", "", "", ""
   "","", "", "**Thermodynamics**", ""
   "\*","``kitd``", "``0``", "delta function ITD approximation", "1"
   "","", "``1``", "linear remapping ITD approximation", ""
   "\*","``ktherm``", "``0``", "zero-layer thermodynamic model", ""
   "","", "``1``", "Bitz and Lipscomb thermodynamic model", ""
   "","", "``2``", "mushy-layer thermodynamic model", ""
   "","", "``-1``", "thermodynamics disabled", ""
   "\*","``conduct``", "``Maykut71``", "conductivity :cite:`Maykut71`", ""
   "","", "``bubbly``", "conductivity :cite:`Pringle07`", ""
   "\*","``ksno``", "real", "snow thermal conductivity", "0.3"
   "\*","``a_rapid_mode``", "real", "brine channel diameter", "0.5x10 :math:`^{-3}` m"
   "\*","``Rac_rapid_mode``", "real", "critical Rayleigh number", "10"
   "\*","``aspect_rapid_mode``", "real", "brine convection aspect ratio", "1"
   "\*","``dSdt_slow_mode``", "real", "drainage strength parameter", "-1.5x10 :math:`^{-7}` m/s/K"
   "\*","``phi_c_slow_mode``", ":math:`0<\phi_c < 1`", "critical liquid fraction", "0.05"
   "\*","``phi_i_mushy``", ":math:`0<\phi_i < 1`", "solid fraction at lower boundary", "0.85"
   "","", "", "", ""
   "","*dynamics_nml*", "", "", ""
   "","", "", "**Dynamics**", ""
   "","``kdyn``", "``-1``", "dynamics OFF", "1"
   "","", "``0``", "dynamics OFF", ""
   "","", "``1``", "EVP dynamics", ""
   "","", "``2``", "EAP dynamics", ""
   "","", "``1``", "dynamics ON", ""
   "","``revised_evp``", "true/false", "use revised EVP formulation", ""
   "","``ndte``", "integer", "number of EVP subcycles", "240"
   "","``advection``", "``remap``", "linear remapping advection", "‘remap’"
   "","", "``upwind``", "donor cell advection", ""
   "\*","``kstrength``", "``0``", "ice strength formulation :cite:`Hibler79`", "1"
   "","", "``1``", "ice strength formulation :cite:`Rothrock75`", ""
   "\*","``krdg_partic``", "``0``", "old ridging participation function", "1"
   "","", "``1``", "new ridging participation function", ""
   "\*","``krdg_redist``", "``0``", "old ridging redistribution function", "1"
   "","", "``1``", "new ridging redistribution function", ""
   "\*","``mu_rdg``", "real", "e-folding scale of ridged ice", ""
   "\*","``Cf``", "real", "ratio of ridging work to PE change in ridging", "17."
   "","``coriolis``", "``latitude``", "Coriolis variable by latitude", "'latitude'"
   "","", "``constant``", "Constant coriolis value = 1.46e-4", ""
   "","", "``zero``", "Zero coriolis", ""
   "","``kridge``", "``1``", "Ridging Enabled", "1"
   "","", "``-1``", "Ridging Disabled", ""
   "","``ktransport``", "``1``", "Transport Enabled", "1"
   "","", "``-1``", "Transport Disabled", ""
   "","``basalstress``", "true/false", "use basal stress parameterization for landfast ice", ""
   "","``k1``", "real", "1st free parameter for landfast parameterization", "8."
   "","``k2``", "real", "2nd free parameter (N/m^3) for landfast parameterization", "15."
   "","``alphab``", "real", ":math:`\alpha_{b}` factor in :cite:`Lemieux16`", "20."
   "","``threshold_hw``", "real", "Max water depth for grounding (see :cite:`Amundrud04`)", "30."
   "","``e_ratio``", "real", "EVP ellipse aspect ratio", "2.0"
   "","``Ktens``", "real", "Tensile strength factor (see :cite:`Konig10`)", "0.0"
   "","", "", "", ""
   "","*shortwave_nml*", "", "", ""
   "","", "", "**Shortwave**", ""
   "\*","``shortwave``", "``ccsm3``", "NCAR CCSM3 distribution method", ""
   "","", "``dEdd``", "Delta-Eddington method", ""
   "\*","``albedo_type``", "``ccsm3``", "NCAR CCSM3 albedos", "‘default’"
   "","", "``constant``", "four constant albedos", ""
   "\*","``albicev``", ":math:`0<\alpha <1`", "visible ice albedo for thicker ice", ""
   "\*","``albicei``", ":math:`0<\alpha <1`", "near infrared ice albedo for thicker ice", ""
   "\*","``albsnowv``", ":math:`0<\alpha <1`", "visible, cold snow albedo", ""
   "\*","``albsnowi``", ":math:`0<\alpha <1`", "near infrared, cold snow albedo", ""
   "\*","``ahmax``", "real", "albedo is constant above this thickness", "0.3 m"
   "\*","``R_ice``", "real", "tuning parameter for sea ice albedo from Delta-Eddington shortwave", ""
   "\*","``R_pnd``", "real", "... for ponded sea ice albedo …", ""
   "\*","``R_snw``", "real", "... for snow (broadband albedo) …", ""
   "\*","``dT_mlt``", "real", ":math:`\Delta` temperature per :math:`\Delta` snow grain radius", ""
   "\*","``rsnw_mlt``", "real", "maximum melting snow grain radius", ""
   "\*","``kalg``", "real", "absorption coefficient for algae", ""
   "","", "", "", ""
   "","*ponds_nml*", "", "", ""
   "","", "", "**Melt Ponds**", ""
   "\*","``hp1``", "real", "critical ice lid thickness for topo ponds", "0.01 m"
   "\*","``hs0``", "real", "snow depth of transition to bare sea ice", "0.03 m"
   "\*","``hs1``", "real", "snow depth of transition to pond ice", "0.03 m"
   "\*","``dpscale``", "real", "time scale for flushing in permeable ice", ":math:`1\times 10^{-3}`"
   "\*","``frzpnd``", "``hlid``", "Stefan refreezing with pond ice thickness", "‘hlid’"
   "","", "``cesm``", "CESM refreezing empirical formula", ""
   "\*","``rfracmin``", ":math:`0 \le r_{min} \le 1`", "minimum melt water added to ponds", "0.15"
   "\*","``rfracmax``", ":math:`0 \le r_{max} \le 1`", "maximum melt water added to ponds", "1.0"
   "\*","``pndaspect``", "real", "aspect ratio of pond changes (depth:area)", "0.8"
   "","", "", "", ""
   "","*forcing_nml*", "", "", ""
   "","", "", "**Forcing**", ""
   "\*","``formdrag``", "true/false", "calculate form drag", ""
   "\*","``atmbndy``", "``default``", "stability-based boundary layer", "‘default’"
   "","", "``constant``", "bulk transfer coefficients", ""
   "\*","``fyear_init``", "yyyy", "first year of atmospheric forcing data", ""
   "\*","``ycycle``", "integer", "number of years in forcing data cycle", ""
   "\*","``calc_strair``", "true", "calculate wind stress and speed", ""
   "","", "false", "read wind stress and speed from files", ""
   "\*","``highfreq``", "true/false", "high-frequency atmo coupling", ""
   "\*","``natmiter``", "integer", "number of atmo boundary layer iterations", ""
   "\*","``calc_Tsfc``", "true/false", "calculate surface temperature", "``.true.``"
   "\*","``default_season``","``winter``", "Sets initial values of forcing and is overwritten if forcing is read in.", ""
   "\*","``precip_units``", "``mks``", "liquid precipitation data units", ""
   "","", "``mm_per_month``", "", ""
   "","", "``mm_per_sec``", "(same as MKS units)", ""
   "","", "``m_per_sec``", "", ""
   "\*","``tfrz_option``", "``minus1p8``", "constant ocean freezing temperature (:math:`-1.8^{\circ} C`)", ""
   "","", "``linear_salt``", "linear function of salinity (ktherm=1)", ""
   "","", "``mushy_layer``", "matches mushy-layer thermo (ktherm=2)", ""
   "\*","``ustar_min``", "real", "minimum value of ocean friction velocity", "0.0005 m/s"
   "\*","``emissivity``", "real", "emissivity of snow and ice", "0.95"
   "\*","``fbot_xfer_type``", "``constant``", "constant ocean heat transfer coefficient", ""
   "","", "``Cdn_ocn``", "variable ocean heat transfer coefficient", ""
   "\*","``update_ocn_f``", "true", "include frazil water/salt fluxes in ocn fluxes", ""
   "","", "false", "do not include (when coupling with POP)", ""
   "\*","``l_mpond_fresh``", "true", "retain (topo) pond water until ponds drain", ""
   "","", "false", "release (topo) pond water immediately to ocean", ""
   "\*","``oceanmixed_ice``", "true/false", "active ocean mixed layer calculation", "``.true.`` (if uncoupled)"
   "\*", "``wave_spec_type``", "``none``", "no wave data provided, no wave-ice interactions", ""
   "", "", "``profile``", "no wave data file is provided, use fixed dummy wave spectrum, for testing", ""
   "", "", "``constant``", "wave data file is provided, constant wave spectrum, for testing", ""
   "", "", "``random``", "wave data file is provided, wave spectrum generated using random number", ""
   "\*","``restore_ocn``", "true/false", "restore sst to data", ""
   "\*","``trestore``", "integer", "sst restoring time scale (days)", ""
   "","``restore_ice``", "true/false", "restore ice state along lateral boundaries", ""
    "","``nfreq``", "25", "number of frequencies in ocean surface wave spectral forcing", ""
   "\*","``atm_data_type``", "``default``", "constant values defined in the code", ""
   "","", "``LYq``", "COREII Large-Yeager (AOMIP) forcing data", ":cite:`Large09`"
   "","", "``JRA55_gx1``", "JRA55 forcing data for gx1 grid :cite:`Tsujino18`", ""
   "","", "``JRA55_gx3``", "JRA55 forcing data for gx3 grid :cite:`Tsujino18`", ""
   "","", "``JRA55_tx1``", "JRA55 forcing data for tx1 grid :cite:`Tsujino18`", ""
   "","", "``monthly``", "monthly forcing data", ""
   "","", "``ncar``", "NCAR bulk forcing data", ""
   "","", "``box2001``", "forcing data for :cite:`Hunke01` box problem", ""
   "","", "``oned``", "column forcing data", ""
   "","", "``hycom``", "HYCOM atm forcing data in netcdf format", ""
   "\*","``ocn_data_type``", "``default``", "constant values defined in the code", ""
   "","", "``clim``", "climatological data", ""
   "","", "``ncar``", "POP ocean forcing data", ""
   "","", "``hycom``", "HYCOM ocean forcing data in netcdf format", "Constant initial forcing"
   "","``bgc_data_type``", "``default``", "constant values defined in the code", ""
   "","", "``clim``", "climatological data", ""
   "","", "``ncar``", "POP ocean forcing data", ""
   "","", "``hycom``", "HYCOM ocean forcing data in netcdf format", "Constant initial forcing"
   "","``fe_data_type``", "``default``", "default forcing value for iron", ""
   "","", "``clim``", "iron forcing from ocean climatology", ""
   "","``ice_data_type``", "string", "ice initialization for special tests", "``default``"
   "","", "``default``", "no special initialization", ""
   "","", "``box2001``", "initialize ice concentration for :ref:`box2001` test (:cite:`Hunke01`)", ""
   "","", "``boxslotcyl``", "initialize ice concentration and velocity for :ref:`boxslotcyl` test (:cite:`Zalesak79`)", ""
   "","``atm_data_format``", "``nc``", "read  atmo forcing files", ""
   "","", "``bin``", "read direct access, binary files", ""
   "","``ocn_data_format``", "``nc``", "read  ocean forcing files", ""
   "","", "``bin``", "read direct access, binary files", ""
   "\*","``oceanmixed_file``", "filename", "data file containing ocean forcing data", ""
   "\*","``wave_spec_file``", "filename", "data file containing wave spectrum forcing data", ""
   "","``atm_data_dir``", "path/", "path to atmospheric forcing data directory", ""
   "","``ocn_data_dir``", "path/", "path to oceanic forcing data directory", ""
   "","``bgc_data_dir``", "path/", "path to oceanic forcing data directory", ""
   "","", "", "", ""
   "","*zbgc_nml*", "", "", ""
   "","", "", "**Biogeochemistry**", "More information about the BGC tuning can be found in the `Icepack Documentation <https://cice-consortium-icepack.readthedocs.io/en/master/science_guide/index.html>`_."
   "\*","``tr_brine``", "true/false", "brine height tracer", ""
   "\*","``tr_zaero``", "true/false", "vertical aerosol tracers", ""
   "\*","``modal_aero``", "true/false", "modal aersols", ""
   "","``restore_bgc``", "true/false", "restore bgc to data", ""
   "","``solve_zsal``", "true/false", "update salinity tracer profile", ""
   "\*","``skl_bgc``", "true/false", "biogeochemistry", ""
   "","``bgc_flux_type``", "``Jin2006``", "ice–ocean flux velocity of :cite:`Jin06`", ""
   "","", "``constant``", "constant ice–ocean flux velocity", ""
   "","``restart_bgc``", "true/false", "restart tracer values from file", ""
   "","``tr_bgc_C_sk``", "true/false", "algal carbon tracer", ""
   "","``tr_bgc_chl_sk``", "true/false", "algal chlorophyll tracer", ""
   "","``tr_bgc_Am_sk``", "true/false", "ammonium tracer", ""
   "","``tr_bgc_Sil_sk``", "true/false", "silicate tracer", ""
   "","``tr_bgc_DMSPp_sk``", "true/false", "particulate DMSP tracer", ""
   "","``tr_bgc_DMSPd_sk``", "true/false", "dissolved DMSP tracer", ""
   "","``tr_bgc_DMS_sk``", "true/false", "DMS tracer", ""
   "","``phi_snow``", "real", "snow porosity for brine height tracer", ""
   "","", "", "", ""
   "","*icefields_nml*", "", "", ""
   "","", "", "*History Fields*", ""
   "","``f_<var>``", "string", "frequency units for writing ``<var>`` to history", ""
   "","", "``y``", "write history every ``histfreq_n`` years", ""
   "","", "``m``", "write history every ``histfreq_n`` months", ""
   "","", "``d``", "write history every ``histfreq_n`` days", ""
   "","", "``h``", "write history every ``histfreq_n`` hours", ""
   "","", "``1``", "write history every time step", ""
   "","", "``x``", "do not write ``<var>`` to history", ""
   "","", "``md``", "*e.g.,* write both monthly and daily files", ""
   "","``f_<var>_ai``", "", "grid cell average of ``<var>`` (:math:`\times a_i`)", ""



