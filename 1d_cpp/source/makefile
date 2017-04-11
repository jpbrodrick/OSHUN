#!/bin/sh
#
# Makefile for OSHUN
# This should work with gcc-6, open-mpi compiled with gcc-6, and HDF5 compiled with c++11 standards

COMPILER = mpicxx.openmpi

# GNU compilers#
OPTFLAGS = -O2 -std=c++0x -ftree-vectorize
DBGFLAGS = -v -g -O0 -Wall -pedantic -std=c++0x

# HDF5 libraries
H5LIB =  -L/usr/lib/openmpi/lib -L/usr/local/lib -I/usr/local/include -lhdf5_cpp -lhdf5 -lmpi 

# INTEL compilers
#OPTFLAGS = -O3
#DBGFLAGS = -g -O0 -Wall

EXEC_DIR = ../bin
TMP_DIR = ./tmp


OBJECTS = input.o state.o formulary.o setup.o vlasov.o nmethods.o functors.o collisions.o fluid.o implicitE.o parallel.o export.o main.o

EXEC = oshun1d.e



BUILDOBJECTS = ${addprefix ${TMP_DIR}/,${OBJECTS}}

BUILDEXEC = ${addprefix ${EXEC_DIR}/,${EXEC}}

${BUILDEXEC} : ${BUILDOBJECTS}
	-${COMPILER} ${OPTFLAGS} -o ${BUILDEXEC} \
	${BUILDOBJECTS} $(H5LIB) 

clean ::
	rm -f ${BUILDOBJECTS}
	rm -f ${BUILDEXEC}
	rm -f ${TMP_DIR}/${BUILDOBJECTS}

debug :
	${COMPILER} ${DBGFLAGS} -o ${BUILDEXEC} \
	${BUILDOBJECTS} $(H5LIB)

./tmp/%.o: %.cpp
	$(COMPILER) $(OPTFLAGS) -c -o $@ $<

