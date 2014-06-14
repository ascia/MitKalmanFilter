#  Makefile for kalman filtering code
#
#  J. Watlington, 11/7/95
#

OBJS   = matmath.o random.o
TEST_OBJS   = test.o kalman.o kalman_camera.o eval_camera.o mrqmin.o $(OBJS)
LEV_OBJS    = lev.o eval_camera.o mrqmin.o $(OBJS)
MOTEST_OBJS = motest.o kalman.o kalman_motion.o $(OBJS)

LIBS   = -lm
CCOPTS = -fp_reorder -std1 -warnprotos -fptm n -g

# The -fptm sui and -g flags are both needed to avoid getting floating point
# exceptions.
#
# Other Cool DEC Alpha compiler flags                             Default
# -g           - include symbol tables for dbx                     (OFF)
# -g3          - include symbol tables for dbx (optimizer friendly) (OFF)
# -trapuv      - encourages traps caused by uninit'ed data         (OFF)
# -fp_reorder  - allows reordering of floating point insts         (OFF)
# -std1        - enforce full ANSI compliance                      (OFF)
# -fptm sui    - handle fp traps in sftwe, requires -g flag too    (OFF)
# -fptm n      - no floating point traps                           (OFF)
# -ifo         - interfile optimizations applied                   (OFF)
# -ansi_alias  - assumes that pts to data are same type            (ON)
# -O2          - optimize more than normal
# -O3          - optimize as much as possible
# -O4          - O3 but portable
# -O5          - balls to the wall

test:    $(TEST_OBJS)
	cc ${CCOPTS} $(TEST_OBJS) -o test $(LIBS)

lev:  $(LEV_OBJS)
	cc ${CCOPTS} $(LEV_OBJS) -o lev $(LIBS)

motest:  $(MOTEST_OBJS)
	cc ${CCOPTS} $(MOTEST_OBJS) -o motest $(LIBS)

all: motest test lev

clean:
	/bin/rm -f *.o *~ camera test motest core

${TEST_OBJS}: Makefile test.h kalman.h matmath.h
${MOTEST_OBJS}: Makefile motest.h kalman.h matmath.h
${LEV_OBJS}: Makefile test.h matmath.h

.c.o:
	cc -c $(CCOPTS) $(INCLUDES) -o $@ $<
