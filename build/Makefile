# Makefile for BOB to compile hello.pgm.rpgle
PGM = HELLO
SRCS = ../hello.pgm.rpgle
LIB = ROBKRAUDY2  # Replace with your PUB400 library (e.g., MYLIB)
TGTCCSID = *SOURCE

all: $(PGM)

$(PGM): $(SRCS)
    system "CRTBNDRPG PGM($(LIB)/$@) SRCSTMF('$<') TGTCCSID($(TGTCCSID))"