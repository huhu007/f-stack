TOPDIR?=${CURDIR}/../..

ifeq ($(FF_DPDK),)
	FF_DPDK=${TOPDIR}/dpdk/x86_64-native-linuxapp-gcc
endif

TARGET=libfstack_ipc.a

DPDK_CFLAGS= -g -Wall -Werror -include ${FF_DPDK}/include/rte_config.h
DPDK_CFLAGS+= -march=native -DRTE_MACHINE_CPUFLAG_SSE -DRTE_MACHINE_CPUFLAG_SSE2 -DRTE_MACHINE_CPUFLAG_SSE3
DPDK_CFLAGS+= -DRTE_MACHINE_CPUFLAG_SSSE3 -DRTE_MACHINE_CPUFLAG_SSE4_1 -DRTE_MACHINE_CPUFLAG_SSE4_2
DPDK_CFLAGS+= -DRTE_COMPILE_TIME_CPUFLAGS=RTE_CPUFLAG_SSE,RTE_CPUFLAG_SSE2,RTE_CPUFLAG_SSE3,RTE_CPUFLAG_SSSE3,RTE_CPUFLAG_SSE4_1,RTE_CPUFLAG_SSE4_2
DPDK_CFLAGS+= -I${FF_DPDK}/include

CFLAGS+= ${DPDK_CFLAGS}
CFLAGS+= -I${TOPDIR}/lib

SRCS=ff_ipc.c
OBJS=$(patsubst %.c,%.o,${SRCS})

all: ${TARGET}

${TARGET}: ${OBJS}
	ar -cqs $@ ${OBJS}

${OBJS}: %.o: %.c
	${CC} -c $< ${CFLAGS} -o $@ 


.PHONY: clean
clean:
	rm -f *.o ${TARGET}
