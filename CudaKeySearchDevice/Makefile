NAME = CudaKeySearchDevice
CPPSRC := $(wildcard *.cpp)
CUSRC := $(wildcard *.cu)

INCLUDE := -I../util -I../AddressUtil -I../CmdParse -I../CryptoUtil -I../KeyFinderLib -I../CLKeySearchDevice -I../cudaMath -I../clUtil -I../cudaUtil -I../secp256k1lib -I../Logger -I../embedcl -I${CUDA_INCLUDE} -I${CUDA_MATH}

CXXFLAGS := -O2 -std=c++11
NVCCFLAGS := -gencode=arch=compute_75,code="sm_75" -Xptxas="-v" -Xcompiler "-O2 -std=c++11" -rdc=true

LIBDIR := ../lib

all: cuda

cuda:
	for file in ${CPPSRC} ; do\
		${CXX} -c $$file ${INCLUDE} ${CXXFLAGS};\
	done

	for file in ${CUSRC} ; do\
		${NVCC} -c $$file -o $$file".o" ${NVCCFLAGS} ${INCLUDE};\
	done

	${NVCC} -dlink -o cuda_libs.o *.cu.o -lcudadevrt -lcudart

	ar rvs ${LIBDIR}/lib$(NAME).a *.o

clean:
	rm -f *.o *.cu.o
	rm -f *.a
