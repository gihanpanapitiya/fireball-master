# copyright info:
#
# @Copyright 2016
# Fireball Committee
# West Virginia University - James P. Lewis, Chair
# Arizona State University - Otto F. Sankey
# Universidad Autonoma de Madrid - Jose Ortega
# Academy of Sciences of the Czech Republic - Pavel Jelinek

# Previous and/or current contributors:
# Auburn University - Jian Jun Dong
# Caltech - Brandon Keith
# Dublin Institute of Technology - Barry Haycock
# Pacific Northwest National Laboratory - Kurt Glaesemann
# University of Texas at Austin - Alex Demkov
# Ohio University - Dave Drabold
# Washington University - Pete Fedders
# West Virginia University - Ning Ma and Hao Wang
# also Gary Adams, Juergen Frisch, John Tomfohr, Kevin Schmidt,
#      and Spencer Shellman

#
# RESTRICTED RIGHTS LEGEND
# Use, duplication, or disclosure of this software and its documentation
# by the Government is subject to restrictions as set forth in subdivision
# { (b) (3) (ii) } of the Rights in Technical Data and Computer Software
# clause at 52.227-7013.

# Choose the COMPILER
#COMPILER = gfortran-mp-5
COMPILER = gfortran-4.8
#COMPILER = ifort

#LINALG = MKL
LINALG = LAPACK

# Do you use DEBUG or Optimization Mode? (DEBUG/OPT)
MODE = OPT
#MODE = DEBUG

# Turn on omp?
OPENMP = NO

# Choose the MACHINE file
MACHINE = GENERIC
#MACHINE = FIREBALL
#MACHINE = MOUNTAINEER
#MACHINE = SPRUCE

# Choose HARRIS or DOGS
#THEORY = HARRIS
THEORY = DOGS
#THEORY = KS

# Choose the METHOD - GAMMA, KPOINTS, or MDET (which is also GAMMA)
METHOD = GAMMA
#METHOD = KPOINTS
#METHOD = MDET
#METHOD = KS

# Choose the XC functional
XC = LDA
#XC = BLYP

# Use of MPI (Comment to disable)
#MPI = TRUE

# Note: These are the machines files used by the Lewis Research Group. You need
# to create a MACHINES file specific to your architecture.  You can use one of
# the machines file below as a starting point.
include MACHINES/FIREBALL
include MACHINES/MOUNTAINEER
include MACHINES/SPRUCE
include MACHINES/GENERIC


######################################################################
###
### BEGIN LISTING OBJECTS:
###
### This is the old way, the different object files are selected
### and grouped in variables that are used as dependencies for
### the different executables
###
### We are transitioning into a library-based compilation where
### this way of listing object files will be deprecated
###
######################################################################

DIRS = a.GLOBAL b.FUNCTIONS c.SYSTEM d.FUNCTIONS_EXTRA e.FDATA f.MPI g.XC_FUNCTIONALS h.DASSEMBLERS i.GRID h.SOLVESH j.ASSEMBLERS k.DASSEMBLERS l.SCF m.MD n.NAC o.OUTPUT p.HARRIS q.DOGS u.UTIL v.BEGIN x.DRIVERS

# Objects from a.CONFIG
CONFIG = M_precision.o welcome.o M_assemble_blocks.o

# Objects from b.FUNCTIONS
FUNCTIONS = clebsch_gordan.o clm.o factorial.o simpson.o distance.o magnitude.o smoother.o Ylm.o a_cross_b.o Depsilon_2c.o Depsilon_3c.o invert3x3.o mult3x1.o mult3x3.o Dsmoother.o

# Objects from c.SYSTEM
SYSTEM_BEGIN =  M_species.o M_atom_functions.o M_atomPP_functions_KB.o M_atomPP_ion_functions_KB.o M_integrals_2c.o
SYSTEM_LOOPRC = M_species.o M_atom_functions.o M_atomPP_functions_KB.o M_integrals_2c.o
SYSTEM_CREATE = M_species.o M_atom_functions.o M_integrals_2c.o M_integrals_3c.o M_atomPP_functions_KB.o M_atomPP_ion_functions_KB.o
SYSTEM_LIGHTNING = M_species.o M_kpoints.o M_configuraciones_McWEDA.o M_atom_functions.o M_neighbors.o M_neighbors_PP.o M_rotations.o
SYSTEM = M_species.o M_kpoints.o M_configuraciones_McWEDA.o M_neighbors.o M_neighbors_PP.o M_atom_functions.o M_rotations.o M_integrals_2c.o

BEGIN = M_psi.o M_rcatms_Coulomb.o M_rcatms_Coulomb_DMOL_excited.o M_rcatms_DMOL_excited.o M_rcatms.o orthogonalize_psi.o M_vnn.o
BEGIN_LOOPRC = M_psi.o M_rcatms_Coulomb.o M_rcatms.o M_looprc.o

FUNCTIONS_CREATE = initialize_noMPI.o finalize_noMPI.o
FUNCTIONS_LIGHTNING = make_cells.o cl.o epsilon.o

MD = M_gear_quench.o

NAC = M_non_adiabatic_gamma.o M_Goverlap.o

OUTPUT = writeout_energies.o writeout_xyz.o

SOLVESH = M_diagonalization_Lowdin_gamma.o M_kspace_Lowdin.o M_density_matrix.o

UTIL = absorption_gamma.o dos_gamma.o M_isosurfaces.o

GRID = M_grid.o writeout_xsf.o

# LDA is default - we change later if we want something other than LDA
XC_FUNCTIONALS = M_xc_option3_1c.o M_xc_option3_2c.o

# ****************************** HARRIS ******************************
ifneq (,$(findstring HARRIS, ${THEORY}))
CREATE = M_overlap.o M_kinetic.o M_vna_Harris.o M_vnl_KB.o M_rho_2c_McWEDA_Harris.o M_rhoS_2c_McWEDA_Harris.o M_vxc_McWEDA_Harris.o M_bcna_3c_Harris.o M_rho_3c_McWEDA_Harris.o M_rhoS_3c_McWEDA_Harris.o M_Coulomb.o
ASSEMBLERS = lda_ceperley_alder.o M_assemble_2c_Harris.o M_assemble_3c_Harris.o M_assemble_ewald_Harris.o M_assemble_rho_McWEDA_Harris.o M_assemble_usr_McWEDA_Harris.o M_assemble_vxc_McWEDA_Harris.o M_assemble_PP_2c.o M_assemble_PP_3c.o rotate_PP.o
DFDATA = M_Fdata_1c_McWEDA_Harris.o M_DFdata_2c.o M_DFdata_3c.o
FDATA = M_Fdata_1c_McWEDA_Harris.o M_Fdata_2c.o M_Fdata_3c.o
SCF = M_charges_Lowdin.o Qmixer_Anderson_Harris.o
DASSEMBLERS = M_Drotations.o M_Drotations_PP.o M_Dassemble_rho_McWEDA_Harris.o M_Dassemble_2c_Harris.o M_Dassemble_PP_2c.o M_Dassemble_usr_McWEDA_Harris.o M_build_forces.o M_Dassemble_3c_Harris.o M_Dassemble_vxc_McWEDA.o
endif

# ****************************** DOGS ********************************
ifneq (,$(findstring DOGS, ${THEORY}))
CREATE = M_overlap.o M_kinetic.o M_vna_Harris.o M_vnl_KB.o M_rho_2c_McWEDA_Harris.o M_rhoS_2c_McWEDA_Harris.o M_vxc_McWEDA_Harris.o M_bcna_3c_Harris.o M_rho_3c_McWEDA_Harris.o M_rhoS_3c_McWEDA_Harris.o M_Coulomb.o M_dipole_z.o M_vna_DOGS.o M_vxc_McWEDA_DOGS.o M_bcna_3c_DOGS.o
ASSEMBLERS = lda_ceperley_alder.o M_assemble_2c_DOGS.o M_assemble_3c_DOGS.o M_assemble_ewald_DOGS.o M_assemble_rho_McWEDA_DOGS.o M_assemble_usr_McWEDA_DOGS.o M_assemble_vxc_McWEDA_DOGS.o M_assemble_PP_2c.o M_assemble_PP_3c.o rotate_PP.o
DFDATA = M_Fdata_1c_McWEDA_DOGS.o M_DFdata_2c.o M_DFdata_3c.o
FDATA = M_Fdata_1c_McWEDA_DOGS.o M_Fdata_2c.o M_Fdata_3c.o
SCF = M_charges_Lowdin.o Qmixer_Anderson_DOGS.o
DASSEMBLERS = M_Drotations.o M_Drotations_PP.o M_Dassemble_2c_DOGS.o M_Dassemble_PP_2c.o M_Dassemble_rho_McWEDA_DOGS.o M_Dassemble_vxc_McWEDA.o M_Dassemble_usr_McWEDA_DOGS.o M_build_forces.o M_Dassemble_3c_DOGS.o
endif

# ****************************** KS ********************************
ifneq (,$(findstring KS, ${THEORY}))
	ASSEMBLERS = lda_ceperley_alder.o M_assemble_2c_grid.o M_assemble_3c_Harris.o M_assemble_ewald_DOGS.o M_assemble_rho_McWEDA_DOGS.o M_assemble_vxc_McWEDA_grid.o M_assemble_PP_2c.o M_assemble_PP_3c.o rotate_PP.o M_assemble_usr_grid.o
	FDATA = M_Fdata_1c_McWEDA_DOGS.o M_Fdata_2c.o M_Fdata_3c.o
SCF = M_charges_Lowdin.o Qmixer_Anderson_grid.o
endif

# *********************** GAMMA, KPOINTS, MDET, or KS ********************
ifneq (,$(findstring KPOINTS, ${METHOD}))
SOLVESH = M_diagonalization_Lowdin_kpoints.o M_kspace_Lowdin.o M_density_matrix.o
UTIL = dos_kpoints.o
endif
ifneq (,$(findstring MDET, ${METHOD}))
SOLVESH = M_diagonalization_Lowdin_gamma.o M_kspace_Lowdin.o M_density_matrix_MDET.o
SYSTEM = M_species.o M_kpoints_MDET.o M_configuraciones_McWEDA.o M_neighbors.o M_neighbors_PP.o M_atom_functions.o
endif
ifneq (,$(findstring KS, ${METHOD}))
GRID = M_grid.o M_project_grid.o M_fft_grid.o writeout_xsf.o
SOLVESH = M_diagonalization_kpoints.o M_kspace.o M_density_matrix_grid.o
endif

SOLVESH_GRID = M_diagonalization_kpoints.o M_kspace.o M_density_matrix_grid.o M_project_grid.o M_fft_grid.o

# ****************************** XC ********************************
ifneq (,$(findstring BLYP, ${XC}))
XC_FUNCTIONALS = M_xc_option9_1c.o M_xc_option9_2c.o
endif

OBJECTS_LOOPRC =    $(CONFIG) $(FUNCTIONS) $(SYSTEM_BEGIN)     $(FUNCTIONS_BEGIN) $(XC_FUNCTIONALS) M_vxc_McWEDA_Harris.o $(BEGIN_LOOPRC)
OBJECTS_BEGIN =     $(CONFIG) $(FUNCTIONS) $(SYSTEM_BEGIN)     $(FUNCTIONS_BEGIN) $(XC_FUNCTIONALS) M_vxc_McWEDA_Harris.o $(BEGIN)
OBJECTS_CREATE =    $(CONFIG) $(FUNCTIONS) $(SYSTEM_CREATE)    $(FUNCTIONS_CREATE) $(XC_FUNCTIONALS) M_Goverlap.o $(CREATE)
OBJECTS_LIGHTNING = $(CONFIG) $(FUNCTIONS) $(SYSTEM_LIGHTNING) $(FUNCTIONS_LIGHTNING) $(GRID) $(FDATA) $(SOLVESH) $(ASSEMBLERS) $(SCF) $(OUTPUT) $(UTIL)
OBJECTS_FIREBALL =  $(CONFIG) $(FUNCTIONS) $(SYSTEM)  $(FUNCTIONS_LIGHTNING) $(DFDATA) $(GRID) $(SOLVESH) $(ASSEMBLERS) $(DASSEMBLERS) $(SCF) $(MD) $(OUTPUT) $(UTIL)
OBJECTS_MDET =      $(CONFIG) $(FUNCTIONS) $(SYSTEM)  $(FUNCTIONS_LIGHTNING) $(DFDATA) $(SOLVESH) $(ASSEMBLERS) $(DASSEMBLERS) $(SCF) $(MD) $(NAC) $(OUTPUT)
OBJECTS_LIGHTNING_GRID = $(CONFIG) $(FUNCTIONS) $(SYSTEM_LIGHTNING) $(FUNCTIONS_LIGHTNING) $(GRID) $(FDATA) $(ASSEMBLERS) $(SOLVESH_GRID) $(SCF) $(OUTPUT) $(UTIL)

######################################################################
###
### END LISTING OBJECTS
###
######################################################################

######################################################################
###
### LISTING LIBRARIES AND LINKKING FLAGS
###
### This is the new way for compiling the thunder suite.
### We list the libraries needed by each executable and the linking
### flags needed
###
######################################################################

LIBS_COMMON = libthd_GLOBAL.a libthd_FUNCTIONS.a libthd_SYSTEM.a libthd_FUNCTIONS_EXTRA.a
LIBS_BEGIN =  $(LIBS_COMMON) libthd_XC_FUNCTIONALS.a libthd_VXC_MCWEDA.a libthd_BEGIN.a
LIBS_LOOPRC = $(LIBS_COMMON) libthd_XC_FUNCTIONALS.a libthd_VXC_MCWEDA.a libthd_BEGIN_LOOPRC.a
LIBS_CREATE = $(LIBS_COMMON) libthd_XC_FUNCTIONALS.a libthd_NAC.a libthd_HARRIS.a libthd_VXC_MCWEDA.a libthd_DOGS.a
LIBS_DOGS = libthd_FDATA_DOGS.a libthd_ASSEMBLERS_DOGS.a libthd_DASSEMBLERS_DOGS.a libthd_DOGS.a
LIBS_LIGHTNING = $(LIBS_COMMON) libthd_XC_FUNCTIONALS.a libthd_SOLVESH.a libthd_GRID.a libthd_SCF.a libthd_OUTPUT.a libthd_UTIL.a libthd_ASSEMBLERS_PP.a libthd_HARRIS.a $(LIBS_DOGS)
LIBS_LIGHTNING_GRID = $(LIBS_LIGHTNING) libthd_GRID_EXTRA.a
LIBS_FIREBALL = $(LIBS_COMMON) libthd_XC_FUNCTIONALS.a libthd_SOLVESH.a libthd_ASSEMBLERS_PP.a libthd_SCF.a libthd_MD.a libthd_UTIL.a libthd_HARRIS.a $(LIBS_DOGS)

LFLAGS_COMMON = -lthd_FUNCTIONS_EXTRA -lthd_SYSTEM -lthd_FUNCTIONS -lthd_GLOBAL
LFLAGS_LOOPRC = -lthd_BEGIN_LOOPRC -lthd_VXC_MCWEDA -lthd_XC_FUNCTIONALS $(LFLAGS_COMMON)
LFLAGS_BEGIN = -lthd_BEGIN -lthd_VXC_MCWEDA -lthd_XC_FUNCTIONALS $(LFLAGS_COMMON)
LFLAGS_CREATE = -lthd_DOGS -lthd_HARRIS -lthd_VXC_MCWEDA -lthd_XC_FUNCTIONALS $(LFLAGS_COMMON)
LFLAGS_DOGS = -lthd_FDATA_DOGS -lthd_ASSEMBLERS_DOGS -lthd_DASSEMBLERS_DOGS -lthd_DOGS
LFLAGS_LIGHTNING = -lthd_SCF -lthd_SOLVESH -lthd_UTIL -lthd_OUTPUT -lthd_GRID $(LFLAGS_DOGS) -lthd_ASSEMBLERS_PP -lthd_XC_FUNCTIONALS -lthd_FUNCTIONS_EXTRA $(LFLAGS_COMMON)
LFLAGS_LIGHTNING_GRID = -lthd_GRID_EXTRA $(LFLAGS_LIGHTNING)
LFLAGS_FIREBALL = -lthd_UTIL -lthd_SCF -lthd_MD $(LFLAGS_DOGS) -lthd_ASSEMBLERS_PP -lthd_FDATA -lthd_SOLVESH -lthd_XC_FUNCTIONALS $(LFLAGS_COMMON)

# This line export variables to the Makefiles called inside each
# directory
export

######################################################################
###
### END LISTING LIBRARIES AND LINKING FLAGS
###
######################################################################

all: all_old

.PHONY: clean veryclean cleanall

clean:
	rm -f -r core *.a *.o .nfs* rii_files begin-looprc.x.ip* begin.x.ip* \
			create.x.ip* fireball.x.ip* \
			fireball-MDET.x.ip* lightning.x.ip* *genmod.f90 .#* \
			ldtmp* *.mod *.mod.* *.vo *~ *.il libs/*.a include/*.mod
	for dir in $(DIRS) ; \
	do \
		if [ -e $$dir ]; then echo $$dir && cd $$dir && $(MAKE) clean && cd .. ; fi ; \
	done

cleanall: clean
	rm -f begin-looprc.x begin.x create.x lightning.x lightning-grid.x fireball.x fireball-MDET.x l*.x

veryclean: cleanall

# NEW METHOD:
#
# We are transitioning into a library-based compilation where the object files
# are created inside the respective directories and static libraries are stored
# in libs and module files ('*.mod') are stored in include
#
# In the meantime, new executables are created with a l prefix in front of
# the usual name

# *****************************************************************************
# MAIN
# *****************************************************************************

lbegin-looprc.x : x.DRIVERS/begin-looprc.f90 $(LIBS_LOOPRC)
	$(F90) -o $@ $(FFLAGS) $< -I./include -Llibs $(LFLAGS_LOOPRC) ${LFLAGS}

lbegin.x : x.DRIVERS/begin.f90 $(LIBS_BEGIN)
	$(F90) -o $@ $(FFLAGS) $< -I./include -Llibs $(LFLAGS_BEGIN) ${LFLAGS}

lcreate.x : x.DRIVERS/create.f90 $(LIBS_CREATE)
	$(F90) -o $@ $(FFLAGS) $< -I./include -Llibs $(LFLAGS_CREATE) ${LFLAGS}

llightning.x: x.DRIVERS/lightning.f90 $(LIBS_LIGHTNING)
	$(F90) -o $@ $(FFLAGS) $(OMP) $< -I./include -Llibs $(LFLAGS_LIGHTNING) ${LFLAGS}

llightning-grid.x: x.DRIVERS/lightning-grid.f90 $(LIBS_LIGHTNING_GRID)
	$(F90) -o $@ $(FFLAGS) $(OMP) $< -I./include -Llibs $(LFLAGS_LIGHTNING_GRID) ${LFLAGS} $(LFLAGS_FFT)

lfireball.x: x.DRIVERS/fireball.f90 $(LIBS_FIREBALL)
	$(F90) -o $@ $(FFLAGS) $< -I./include -Llibs $(LFLAGS_FIREBALL) ${LFLAGS}

lfireball-MDET.x: x.DRIVERS/fireball-MDET.f90 $(LIBS_FIREBALL_MDET)
	$(F90) -o $@ $(FFLAGS) $< -I./include -Llibs $(LFLAGS_FIREBALL_MDET) ${LFLAGS}

# *****************************************************************************
# LIBRARIES
# *****************************************************************************

libs:  libthd_GLOBAL.a libthd_FUNCTIONS.a libthd_SYSTEM.a libthd_FUNCTIONS_EXTRA.a libthd_FDATA.a libthd_noMPI.a libthd_XC_FUNCTIONALS.a libthd_SOLVESH.a libthd_GRID.a libthd_ASSEMBLERS_HARRIS.a libthd_ASSEMBLERS_DOGS.a libthd_ASSEMBLERS_KS.a libthd_ASSEMBLERS_PP.a libthd_DASSEMBLERS_HARRIS.a libthd_DASSEMBLERS_DOGS.a libthd_SCF.a libthd_NAC.a libthd_HARRIS.a libthd_DOGS.a libthd_UTIL.a 

libthd_GLOBAL.a:
	cd a.GLOBAL && $(MAKE) $@

libthd_FUNCTIONS.a:
	cd b.FUNCTIONS && $(MAKE) $@

libthd_FUNCTIONS_LIGHTNING.a: libthd_SYSTEM.a libthd_SYSTEM.a
	cd b.FUNCTIONS && $(MAKE) $@

libthd_SYSTEM.a:
	cd c.SYSTEM && $(MAKE) $@

libthd_FUNCTIONS_EXTRA.a:
	cd d.FUNCTIONS_EXTRA && $(MAKE) $@

libthd_FDATA.a: libthd_SYSTEM.a
	cd e.FDATA && $(MAKE) $@

libthd_FDATA_HARRIS.a: libthd_SYSTEM.a
	cd e.FDATA && $(MAKE) $@

libthd_FDATA_DOGS.a: libthd_SYSTEM.a
	cd e.FDATA && $(MAKE) $@

libthd_noMPI.a:
	cd f.MPI && $(MAKE) $@

libthd_XC_FUNCTIONALS.a:
	cd g.XC_FUNCTIONALS && $(MAKE) $@

#One selectio from M_diagonalization
libthd_SOLVESH.a: libthd_SYSTEM.a libthd_FDATA.a
	cd h.SOLVESH && $(MAKE) $@

libthd_GRID.a: libthd_SYSTEM.a libthd_SYSTEM.a
	cd i.GRID && $(MAKE) $@

libthd_GRID_EXTRA.a: libthd_SYSTEM.a
	cd i.GRID && $(MAKE) $@

libthd_ASSEMBLERS_HARRIS.a: libthd_SYSTEM.a libthd_SYSTEM.a libthd_FDATA.a libthd_FDATA_HARRIS.a
	cd j.ASSEMBLERS && $(MAKE) $@

libthd_ASSEMBLERS_DOGS.a: libthd_SYSTEM.a libthd_FDATA.a libthd_SYSTEM.a libthd_ASSEMBLERS_PP.a
	cd j.ASSEMBLERS && $(MAKE) $@

libthd_ASSEMBLERS_KS.a: libthd_SYSTEM.a
	cd j.ASSEMBLERS && $(MAKE) $@

libthd_ASSEMBLERS_PP.a: libthd_SYSTEM.a libthd_FDATA.a libthd_SYSTEM.a
	cd j.ASSEMBLERS && $(MAKE) $@

libthd_DASSEMBLERS_HARRIS.a: libthd_ASSEMBLERS_PP.a
	cd k.DASSEMBLERS && $(MAKE) $@

libthd_DASSEMBLERS_DOGS.a: libthd_SYSTEM.a libthd_SYSTEM.a libthd_FDATA.a libthd_FDATA_DOGS.a
	cd k.DASSEMBLERS && $(MAKE) $@

libthd_SCF.a: libthd_SYSTEM.a libthd_SOLVESH.a libthd_GRID.a
	cd l.SCF && $(MAKE) $@

libthd_NAC.a: libthd_SYSTEM.a libthd_SYSTEM.a
	cd n.NAC && $(MAKE) $@

libthd_MD.a: libthd_SYSTEM.a libthd_SYSTEM.a
	cd m.MD && $(MAKE) $@

libthd_OUTPUT.a: libthd_GRID.a
	cd o.OUTPUT && $(MAKE) $@

libthd_HARRIS.a: libthd_SYSTEM.a libthd_XC_FUNCTIONALS.a
	cd p.HARRIS && $(MAKE) $@

libthd_VXC_MCWEDA.a: libthd_SYSTEM.a
	cd p.HARRIS && $(MAKE) $@

libthd_DOGS.a: libthd_SYSTEM.a libthd_XC_FUNCTIONALS.a libthd_VXC_MCWEDA.a
	cd q.DOGS && $(MAKE) $@

libthd_UTIL.a: libthd_SYSTEM.a libthd_GRID.a libthd_FDATA.a
	cd u.UTIL && $(MAKE) $@

libthd_BEGIN.a: libthd_SYSTEM.a
	cd v.BEGIN && $(MAKE) $@

libthd_BEGIN_LOOPRC.a: libthd_SYSTEM.a
	cd v.BEGIN && $(MAKE) $@

# OLD METHOD:
# The object files ('*.o') are created on the base directory and the binaries ('*.x')
# are created directly from the object files
#
# We are transitioning into a library-based compilation where the object files
# are created inside the respective directories and static libraries are stored
# in libs and module files ('*.mod') are stored in include
#
# When the transition is complete this comment and the lines below it will
# disapear

# ****************************** LINKING ******************************
all_old: begin-looprc.x begin.x create.x fireball.x fireball-MDET.x lightning.x lightning-grid.x

begin-looprc.x : x.DRIVERS/begin-looprc.f90 $(OBJECTS_LOOPRC)
	$(F90) -o $@ $(FFLAGS) $^ $(LFLAGS)

begin.x : x.DRIVERS/begin.f90 $(OBJECTS_BEGIN)
	$(F90) -o $@ $(FFLAGS) $^ $(LFLAGS)

create.x : x.DRIVERS/create.f90 $(OBJECTS_CREATE)
	$(F90) -o $@ $(FFLAGS) $^ $(LFLAGS)

lightning.x: x.DRIVERS/lightning.f90 $(OBJECTS_LIGHTNING)
	$(F90) -o $@ $(FFLAGS) $(OMP) $^ $(LFLAGS)

lightning-grid.x:  x.DRIVERS/lightning-grid.f90 $(OBJECTS_LIGHTNING_GRID)
	$(F90) -o $@ $(FFLAGS) $(OMP) $^ $(LFLAGS) $(LFLAGS_FFT)

fireball.x: x.DRIVERS/fireball.f90 $(OBJECTS_FIREBALL)
	$(F90) -o $@ $(FFLAGS) $^ $(LFLAGS)

fireball-MDET.x: x.DRIVERS/fireball-MDET.f90 $(OBJECTS_MDET)
	$(F90) -o $@ $(FFLAGS) $^ $(LFLAGS)

# *****************************************************************************
# a.GLOBAL
# *****************************************************************************
welcome.o : a.GLOBAL/welcome.f90
	$(F90) $(FFLAGS) -c $^
M_precision.o : a.GLOBAL/M_precision.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_blocks.o : a.GLOBAL/M_assemble_blocks.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# b.FUNCTIONS
# *****************************************************************************
a_cross_b.o : b.FUNCTIONS/a_cross_b.f90
	$(F90) $(FFLAGS) -c $^
clebsch_gordan.o : b.FUNCTIONS/clebsch_gordan.f90
	$(F90) $(FFLAGS) -c $^
clm.o : b.FUNCTIONS/clm.f90
	$(F90) $(FFLAGS) -c $^
distance.o : b.FUNCTIONS/distance.f90
	$(F90) $(FFLAGS) -c $^
erf0.o : b.FUNCTIONS/erf0.f90
	$(F90) $(FFLAGS) -c $^
Depsilon_2c.o : b.FUNCTIONS/Depsilon_2c.f90
	$(F90) $(FFLAGS) -c $^
Depsilon_3c.o : b.FUNCTIONS/Depsilon_3c.f90
	$(F90) $(FFLAGS) -c $^
factorial.o : b.FUNCTIONS/factorial.f90
	$(F90) $(FFLAGS) -c $^
invert3x3.o : b.FUNCTIONS/invert3x3.f90
	$(F90) $(FFLAGS) -c $^
magnitude.o : b.FUNCTIONS/magnitude.f90
	$(F90) $(FFLAGS) -c $^
mult3x1.o : b.FUNCTIONS/mult3x1.f90
	$(F90) $(FFLAGS) -c $^
mult3x3.o : b.FUNCTIONS/mult3x3.f90
	$(F90) $(FFLAGS) -c $^
simpson.o : b.FUNCTIONS/simpson.f90
	$(F90) $(FFLAGS) -c $^
smoother.o : b.FUNCTIONS/smoother.f90
	$(F90) $(FFLAGS) -c $^
Dsmoother.o : b.FUNCTIONS/Dsmoother.f90
	$(F90) $(FFLAGS) -c $^
Ylm.o : b.FUNCTIONS/Ylm.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# c.SYSTEM
# *****************************************************************************
M_atom_functions.o : c.SYSTEM/M_atom_functions.f90
	$(F90) $(FFLAGS) -c $^
M_atomPP_functions_KB.o : c.SYSTEM/M_atomPP_functions_KB.f90
	$(F90) $(FFLAGS) -c $^
M_atomPP_ion_functions_KB.o : c.SYSTEM/M_atomPP_ion_functions_KB.f90
	$(F90) $(FFLAGS) -c $^
M_configuraciones_McWEDA.o : c.SYSTEM/M_configuraciones_McWEDA.f90
	$(F90) $(FFLAGS) -c $^
M_integrals_2c.o : c.SYSTEM/M_integrals_2c.f90
	$(F90) $(FFLAGS) -c $^
M_integrals_3c.o : c.SYSTEM/M_integrals_3c.f90
	$(F90) $(FFLAGS) -c $^
M_kpoints.o : c.SYSTEM/M_kpoints.f90
	$(F90) $(FFLAGS) -c $^
M_kpoints_MDET.o : c.SYSTEM/M_kpoints_MDET.f90
	$(F90) $(FFLAGS) -c $^
M_neighbors.o : c.SYSTEM/M_neighbors.f90
	$(F90) $(FFLAGS) -c $^
M_neighbors_PP.o : c.SYSTEM/M_neighbors_PP.f90
	$(F90) $(FFLAGS) -c $^
M_species.o : c.SYSTEM/M_species.f90
	$(F90) $(FFLAGS) -c $^
write_species.o : c.SYSTEM/write_species.f90
	$(F90) $(FFLAGS) -s $^
M_rotations.o : c.SYSTEM/M_rotations.f90
	$(F90) $(FFLAGS) -c $^
make_cells.o : c.SYSTEM/make_cells.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# d.FUNCTIONS_EXTRA
# *****************************************************************************
cl.o : d.FUNCTIONS_EXTRA/cl.f90
	$(F90) $(FFLAGS) -c $^
epsilon.o : d.FUNCTIONS_EXTRA/epsilon.f90
	$(F90) $(FFLAGS) -c $^
mpairnay.o : d.FUNCTIONS_EXTRA/mpairnay.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# e.FDATA
# *****************************************************************************
M_Fdata_1c_McWEDA_Harris.o : e.FDATA/M_Fdata_1c_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_Fdata_1c_McWEDA_DOGS.o : e.FDATA/M_Fdata_1c_McWEDA_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_Fdata_2c.o : e.FDATA/M_Fdata_2c.f90
	$(F90) $(FFLAGS) -c $^
M_Fdata_3c.o : e.FDATA/M_Fdata_3c.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# f.MPI
# *****************************************************************************
finalize_MPI.o : f.MPI/finalize_MPI.f90
	$(F90) $(FFLAGS) -c $^
finalize_noMPI.o : f.MPI/finalize_noMPI.f90
	$(F90) $(FFLAGS) -c $^
initialize_MPI.o : f.MPI/initialize_MPI.f90
	$(F90) $(FFLAGS) -c $^
initialize_noMPI.o : f.MPI/initialize_noMPI.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# g.XC_FUNCTIONALS
# *****************************************************************************
lda_ceperley_alder.o : g.XC_FUNCTIONALS/lda_ceperley_alder.f90
	$(F90) $(FFLAGS) -c $^
M_xc_option3_1c.o : g.XC_FUNCTIONALS/M_xc_option3_1c.f90
	$(F90) $(FFLAGS) -c $^
M_xc_option3_2c.o : g.XC_FUNCTIONALS/M_xc_option3_2c.f90
	$(F90) $(FFLAGS) -c $^
M_xc_option9_1c.o : g.XC_FUNCTIONALS/M_xc_option9_1c.f90
	$(F90) $(FFLAGS) -c $^
M_xc_option9_2c.o : g.XC_FUNCTIONALS/M_xc_option9_2c.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# h.SOLVESH
# *****************************************************************************
M_density_matrix.o : h.SOLVESH/M_density_matrix.f90
	$(F90) $(FFLAGS) -c $^
M_density_matrix_MDET.o : h.SOLVESH/M_density_matrix_MDET.f90
	$(F90) $(FFLAGS) -c $^
M_kspace_Lowdin.o : h.SOLVESH/M_kspace_Lowdin.f90
	$(F90) $(FFLAGS) -c $^
M_kspace.o : h.SOLVESH/M_kspace.f90
	$(F90) $(FFLAGS) -c $^
M_diagonalization_Lowdin_gamma.o : h.SOLVESH/M_diagonalization_Lowdin_gamma.f90
	$(F90) $(FFLAGS) -c $^
M_diagonalization_Lowdin_kpoints.o : h.SOLVESH/M_diagonalization_Lowdin_kpoints.f90
	$(F90) $(FFLAGS) -c $^
M_diagonalization_kpoints.o : h.SOLVESH/M_diagonalization_kpoints.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# i.GRID
# *****************************************************************************
M_grid.o : i.GRID/M_grid.f90
	$(F90) $(FFLAGS) -c $^
M_project_grid.o : i.GRID/M_project_grid.f90
	$(F90) $(FFLAGS) -c $^
M_fft_grid.o : i.GRID/M_fft_grid.f90
	$(F90) $(FFLAGS) -c $^
M_density_matrix_grid.o : i.GRID/M_density_matrix_grid.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# j.ASSEMBLERS
# *****************************************************************************
M_assemble_2c_Harris.o : j.ASSEMBLERS/M_assemble_2c_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_2c_DOGS.o : j.ASSEMBLERS/M_assemble_2c_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_2c_grid.o : GRID/M_assemble_2c_grid.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_3c_Harris.o : j.ASSEMBLERS/M_assemble_3c_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_3c_DOGS.o : j.ASSEMBLERS/M_assemble_3c_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_ewald_Harris.o : j.ASSEMBLERS/M_assemble_ewald_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_ewald_DOGS.o : j.ASSEMBLERS/M_assemble_ewald_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_rho_McWEDA_Harris.o : j.ASSEMBLERS/M_assemble_rho_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_rho_McWEDA_DOGS.o : j.ASSEMBLERS/M_assemble_rho_McWEDA_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_usr_grid.o : GRID/M_assemble_usr_grid.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_usr_McWEDA_Harris.o : j.ASSEMBLERS/M_assemble_usr_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_usr_McWEDA_DOGS.o : j.ASSEMBLERS/M_assemble_usr_McWEDA_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_vxc_McWEDA_Harris.o : j.ASSEMBLERS/M_assemble_vxc_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_vxc_McWEDA_DOGS.o : j.ASSEMBLERS/M_assemble_vxc_McWEDA_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_vxc_McWEDA_grid.o : GRID/M_assemble_vxc_McWEDA_grid.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_PP_2c.o : j.ASSEMBLERS/M_assemble_PP_2c.f90
	$(F90) $(FFLAGS) -c $^
M_assemble_PP_3c.o : j.ASSEMBLERS/M_assemble_PP_3c.f90
	$(F90) $(FFLAGS) -c $^
rotate_PP.o : j.ASSEMBLERS/rotate_PP.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# k.DASSEMBLERS
# *****************************************************************************
M_Dassemble_blocks.o : k.DASSEMBLERS/M_Dassemble_blocks.f90
	$(F90) $(FFLAGS) -c $^
M_DFdata_2c.o : k.DASSEMBLERS/M_DFdata_2c.f90
	$(F90) $(FFLAGS) -c $^
M_DFdata_3c.o : k.DASSEMBLERS/M_DFdata_3c.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_2c_Harris.o : k.DASSEMBLERS/M_Dassemble_2c_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_2c_DOGS.o : k.DASSEMBLERS/M_Dassemble_2c_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_PP_2c.o : k.DASSEMBLERS/M_Dassemble_PP_2c.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_3c_Harris.o : k.DASSEMBLERS/M_Dassemble_3c_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_3c_DOGS.o : k.DASSEMBLERS/M_Dassemble_3c_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_usr_McWEDA_Harris.o : k.DASSEMBLERS/M_Dassemble_usr_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_Drotations.o : k.DASSEMBLERS/M_Drotations.f90
	$(F90) $(FFLAGS) -c $^
M_Drotations_PP.o : k.DASSEMBLERS/M_Drotations_PP.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_rho_McWEDA_Harris.o : k.DASSEMBLERS/M_Dassemble_rho_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_vxc_McWEDA_Harris.o : k.DASSEMBLERS/M_Dassemble_vxc_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_usr_McWEDA_DOGS.o : k.DASSEMBLERS/M_Dassemble_usr_McWEDA_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_rho_McWEDA_DOGS.o : k.DASSEMBLERS/M_Dassemble_rho_McWEDA_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_Dassemble_vxc_McWEDA.o : k.DASSEMBLERS/M_Dassemble_vxc_McWEDA.f90
	$(F90) $(FFLAGS) -c $^
M_build_forces.o : k.DASSEMBLERS/M_build_forces.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# l.SCF
# *****************************************************************************
M_charges_Lowdin.o : l.SCF/M_charges_Lowdin.f90
	$(F90) $(FFLAGS) -c $^
Qmixer_Anderson_Harris.o : l.SCF/Qmixer_Anderson_Harris.f90
	$(F90) $(FFLAGS) -c $^
Qmixer_Anderson_DOGS.o : l.SCF/Qmixer_Anderson_DOGS.f90
	$(F90) $(FFLAGS) -c $^
Qmixer_Anderson_grid.o : l.SCF/Qmixer_Anderson_grid.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# m.MD
# *****************************************************************************
M_gear_quench.o : m.MD/M_gear_quench.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# n.NAC
# *****************************************************************************
M_non_adiabatic_gamma.o : n.NAC/M_non_adiabatic_gamma.f90
	$(F90) $(FFLAGS) -c $^
M_Goverlap.o : n.NAC/M_Goverlap.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# o.OUTPUT
# *****************************************************************************
welcome_begin.o : o.OUTPUT/welcome_begin.f90
	$(F90) $(FFLAGS) -c $^
welcome_fireball.o : o.OUTPUT/welcome_fireball.f90
	$(F90) $(FFLAGS) -c $^
welcome_lightning.o : o.OUTPUT/welcome_lightning.f90
	$(F90) $(FFLAGS) -c $^
writeout_energies.o : o.OUTPUT/writeout_energies.f90
	$(F90) $(FFLAGS) -c $^
writeout_xsf.o : o.OUTPUT/writeout_xsf.f90
	$(F90) $(FFLAGS) -c $^
writeout_xyz.o : o.OUTPUT/writeout_xyz.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# p.HARRIS
# *****************************************************************************
M_overlap.o : p.HARRIS/M_overlap.f90
	$(F90) $(FFLAGS) -c $^
M_kinetic.o : p.HARRIS/M_kinetic.f90
	$(F90) $(FFLAGS) -c $^
M_vna_Harris.o : p.HARRIS/M_vna_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_vnl_KB.o : p.HARRIS/M_vnl_KB.f90
	$(F90) $(FFLAGS) -c $^
M_rho_2c_McWEDA_Harris.o : p.HARRIS/M_rho_2c_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_rhoS_2c_McWEDA_Harris.o : p.HARRIS/M_rhoS_2c_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_vxc_McWEDA_Harris.o :  p.HARRIS/M_vxc_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_bcna_3c_Harris.o : p.HARRIS/M_bcna_3c_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_rho_3c_McWEDA_Harris.o : p.HARRIS/M_rho_3c_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_rhoS_3c_McWEDA_Harris.o : p.HARRIS/M_rhoS_3c_McWEDA_Harris.f90
	$(F90) $(FFLAGS) -c $^
M_Coulomb.o : p.HARRIS/M_Coulomb.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# q.DOGS
# *****************************************************************************
M_bcna_3c_DOGS.o : q.DOGS/M_bcna_3c_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_dipole_z.o : q.DOGS/M_dipole_z.f90
	$(F90) $(FFLAGS) -c $^
M_vna_DOGS.o : q.DOGS/M_vna_DOGS.f90
	$(F90) $(FFLAGS) -c $^
M_vxc_McWEDA_DOGS.o : q.DOGS/M_vxc_McWEDA_DOGS.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# u.UTIL
# *****************************************************************************
absorption_gamma.o : u.UTIL/absorption_gamma.f90
	$(F90) $(FFLAGS) $(OMP) -c $^
dos_gamma.o : u.UTIL/dos_gamma.f90
	$(F90) $(FFLAGS) -c $^
dos_kpoints.o : u.UTIL/dos_kpoints.f90
	$(F90) $(FFLAGS) -c $^
M_isosurfaces.o : u.UTIL/M_isosurfaces.f90
	$(F90) $(FFLAGS) -c $^

# *****************************************************************************
# v.BEGIN
# *****************************************************************************
M_looprc.o : v.BEGIN/M_looprc.f90
	$(F90) $(FFLAGS) -c $^
M_psi.o : v.BEGIN/M_psi.f90
	$(F90) $(FFLAGS) -c $^
M_rcatms.o : v.BEGIN/M_rcatms.f90
	$(F90) $(FFLAGS) -c $^
M_rcatms_Coulomb.o : v.BEGIN/M_rcatms_Coulomb.f90
	$(F90) $(FFLAGS) -c $^
M_rcatms_Coulomb_DMOL_excited.o : v.BEGIN/M_rcatms_Coulomb_DMOL_excited.f90
	$(F90) $(FFLAGS) -c $^
M_rcatms_DMOL_excited.o : v.BEGIN/M_rcatms_DMOL_excited.f90
	$(F90) $(FFLAGS) -c $^
M_vnn.o : v.BEGIN/M_vnn.f90
	$(F90) $(FFLAGS) -c $^
orthogonalize_psi.o : v.BEGIN/orthogonalize_psi.f90
	$(F90) $(FFLAGS) -c $^
