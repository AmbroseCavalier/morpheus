# This Makefile uses the sources of morpheus to build libraries into
# this directory. This is useful for cross-platform builds, such
# as emscripten, by editing the CC and CFLAGS.

.POSIX:
# POSIX makefiles are portable but limited. Lack of
# - GNU make pattern rules (%.c)
# - secondary expansion/late expansion
# - prefix substitution
# - internal macros in prerequisites
# - support for directory in implicit rules E.g (.c.o:)
# all prevent defining sources as prereqs unless we list
# an inference and build rule for each .o file.
#
# Instead, this Makefile assumes that cross-platform builds
# will be infrequent. Using the sources in a different
# directory is done in this makefile by not specifying
# prereqs and making the "clean" rule the first prereq for
# the first target.

INCLUDE=../src/includes
CFLAGS= -g -O2 -I${INCLUDE} -std=gnu89 -Wno-error=return-type -Wno-error=implicit-function-declaration
RM=rm
#CC=cc
CC=emcc

GENERLIB=./gener.a
GENERLIB_BUILD=./build
GENERLIB_SOURCE=../src/gener

ENDLIB=./gkends.a
ENDLIB_BUILD=./build
ENDLIB_SOURCE=../src/gkends

DICTLIB=./gkdict.a
DICTLIB_BUILD=./build
DICTLIB_SOURCE=../src/gkdict

ANALLIB=./anal.a
ANALLIB_BUILD=./build
ANALLIB_SOURCE=../src/anal

MORPHLIB=./morphlib.a
MORPHLIB_BUILD=./build
MORPHLIB_SOURCE=../src/morphlib

GREEKLIB=./greeklib.a
GREEKLIB_BUILD=./build
GREEKLIB_SOURCE=../src/greeklib

#First in LIBS must have clean rule as it's first prereq.
LIBS= ${GENERLIB} ${ENDLIB} ${DICTLIB} ${MORPHLIB} ${GREEKLIB}

#In target all, GENERLIB MUST BE FIRST TARGET because it has the clean rule as it's first prereq.
all: ${GENERLIB} ${ENDLIB} ${DICTLIB} ${ANALLIB} ${MORPHLIB} ${GREEKLIB} cruncher

###############
clean:
	rm -f ${GENERLIB_BUILD}/*.o
	rm -f ${ENDLIB_BUILD}/*.o
	rm -f ${DICTLIB_BUILD}/*.o
	rm -f ${ANALLIB_BUILD}/*.o
	rm -f ${MORPHLIB_BUILD}/*.o
	rm -f ${GREEKLIB_BUILD}/*.o

###############
GENEROBJ= ${GENERLIB_BUILD}/genwd.o

${GENERLIB}: clean ${GENEROBJ}
	ar rv ${GENERLIB} ${GENEROBJ}
	ranlib ${GENERLIB}

${GENEROBJ}:
	$(CC) $(CFLAGS) -c -o $@ ${GENERLIB_SOURCE}/$(*F).c

###############
ENDOBJ= ${ENDLIB_BUILD}/acccompos.o \
${ENDLIB_BUILD}/checkforbreath.o \
${ENDLIB_BUILD}/contract.o \
${ENDLIB_BUILD}/countendtables.o \
${ENDLIB_BUILD}/endindex.o \
${ENDLIB_BUILD}/euphend.o \
${ENDLIB_BUILD}/expendtable.o \
${ENDLIB_BUILD}/fixeta.o \
${ENDLIB_BUILD}/getcurrend.o \
${ENDLIB_BUILD}/indexendtables.o \
${ENDLIB_BUILD}/lcontr.o \
${ENDLIB_BUILD}/merge.o \
${ENDLIB_BUILD}/mkend.o \
${ENDLIB_BUILD}/nextsufftab.o \
${ENDLIB_BUILD}/retrends.o \
${ENDLIB_BUILD}/stor.o

${ENDLIB}: ${ENDOBJ}
	ar -rv ${ENDLIB} ${ENDOBJ}
	ranlib ${ENDLIB}

${ENDOBJ}:
	$(CC) $(CFLAGS) -c -o $@ ${ENDLIB_SOURCE}/$(*F).c


###############
DICTOBJ=${DICTLIB_BUILD}/dictio.o \
${DICTLIB_BUILD}/derivio.o \
${DICTLIB_BUILD}/compnoun.o

${DICTLIB}: ${DICTOBJ}
	ar rv ${DICTLIB} ${DICTOBJ}
	ranlib ${DICTLIB}

${DICTOBJ}:
	${CC} $(CFLAGS) -c -o $@ ${DICTLIB_SOURCE}/$(*F).c


###############
ANALOBJ= ${ANALLIB_BUILD}/checkcrasis.o \
${ANALLIB_BUILD}/checkdict.o \
${ANALLIB_BUILD}/checkgenwds.o \
${ANALLIB_BUILD}/checkhalf1.o \
${ANALLIB_BUILD}/checkindecl.o \
${ANALLIB_BUILD}/checkirreg.o \
${ANALLIB_BUILD}/checknom.o \
${ANALLIB_BUILD}/checkpreverb.o \
${ANALLIB_BUILD}/checkstem.o \
${ANALLIB_BUILD}/checkstring.o \
${ANALLIB_BUILD}/checkverb.o \
${ANALLIB_BUILD}/checkword.o \
${ANALLIB_BUILD}/dictstems.o \
${ANALLIB_BUILD}/prntanal.o \
${ANALLIB_BUILD}/prvb.o

${ANALLIB}: ${ANALOBJ}
	ar rv ${ANALLIB} ${ANALOBJ}
	ranlib ${ANALLIB}

${ANALOBJ}:
	$(CC) $(CFLAGS) -c -o $@ ${ANALLIB_SOURCE}/$(*F).c

###############
MORPHOBJ= ${MORPHLIB_BUILD}/adddomain.o \
${MORPHLIB_BUILD}/addninfix.o \
${MORPHLIB_BUILD}/antepenform.o \
${MORPHLIB_BUILD}/augment.o \
${MORPHLIB_BUILD}/beta2rtf.o \
${MORPHLIB_BUILD}/beta2smarta.o \
${MORPHLIB_BUILD}/cmpend.o \
${MORPHLIB_BUILD}/conjstem.o \
${MORPHLIB_BUILD}/endio.o \
${MORPHLIB_BUILD}/errormess.o \
${MORPHLIB_BUILD}/fixacc.o \
${MORPHLIB_BUILD}/gkstring.o \
${MORPHLIB_BUILD}/gktoasc.o \
${MORPHLIB_BUILD}/indkeys.o \
${MORPHLIB_BUILD}/is_thirdmono.o \
${MORPHLIB_BUILD}/loadeuph.o \
${MORPHLIB_BUILD}/markstem.o \
${MORPHLIB_BUILD}/morphflags.o \
${MORPHLIB_BUILD}/morphkeys.o \
${MORPHLIB_BUILD}/morphpath.o \
${MORPHLIB_BUILD}/morphstrcmp.o \
${MORPHLIB_BUILD}/new_val.o \
${MORPHLIB_BUILD}/nextkey.o \
${MORPHLIB_BUILD}/numovable.o \
${MORPHLIB_BUILD}/penultform.o \
${MORPHLIB_BUILD}/pres_redup.o \
${MORPHLIB_BUILD}/preverb.o \
${MORPHLIB_BUILD}/preverb2.o \
${MORPHLIB_BUILD}/preverb3.o \
${MORPHLIB_BUILD}/retrentry.o \
${MORPHLIB_BUILD}/setlang.o \
${MORPHLIB_BUILD}/smk2beta.o \
${MORPHLIB_BUILD}/standphon.o \
${MORPHLIB_BUILD}/trimwhite.o \
${MORPHLIB_BUILD}/ultform.o \
${MORPHLIB_BUILD}/ulttakescirc.o \
${MORPHLIB_BUILD}/sprntGkflags.o

${MORPHLIB}: ${MORPHOBJ}
	ar rv ${MORPHLIB} ${MORPHOBJ}
	ranlib ${MORPHLIB}

${MORPHOBJ}:
	$(CC) $(CFLAGS) -c -o $@ ${MORPHLIB_SOURCE}/$(*F).c

###############
GREEKLIBOBJ = ${GREEKLIB_BUILD}/Fclose.o \
${GREEKLIB_BUILD}/addaccent.o \
${GREEKLIB_BUILD}/addbreath.o \
${GREEKLIB_BUILD}/aspirate.o \
${GREEKLIB_BUILD}/beta_tolower.o \
${GREEKLIB_BUILD}/binlook.o \
${GREEKLIB_BUILD}/checkaccent.o \
${GREEKLIB_BUILD}/cinsert.o \
${GREEKLIB_BUILD}/do_dissim.o \
${GREEKLIB_BUILD}/endsinstr.o \
${GREEKLIB_BUILD}/getaccent.o \
${GREEKLIB_BUILD}/getaccp.o \
${GREEKLIB_BUILD}/getbreath.o \
${GREEKLIB_BUILD}/getquantity.o \
${GREEKLIB_BUILD}/getsyll.o \
${GREEKLIB_BUILD}/gkstrlen.o \
${GREEKLIB_BUILD}/hasaccent.o \
${GREEKLIB_BUILD}/hasdiaer.o \
${GREEKLIB_BUILD}/hasquant.o \
${GREEKLIB_BUILD}/isblank.o \
${GREEKLIB_BUILD}/isdiphth.o \
${GREEKLIB_BUILD}/issubstring.o \
${GREEKLIB_BUILD}/keyio.o \
${GREEKLIB_BUILD}/longbyposition.o \
${GREEKLIB_BUILD}/naccents.o \
${GREEKLIB_BUILD}/normucase.o \
${GREEKLIB_BUILD}/nsylls.o \
${GREEKLIB_BUILD}/quantprim.o \
${GREEKLIB_BUILD}/shortanalog.o \
${GREEKLIB_BUILD}/standalpha.o \
${GREEKLIB_BUILD}/standword.o \
${GREEKLIB_BUILD}/stripacc.o \
${GREEKLIB_BUILD}/stripacute.o \
${GREEKLIB_BUILD}/stripbreath.o \
${GREEKLIB_BUILD}/stripchar.o \
${GREEKLIB_BUILD}/stripdiaer.o \
${GREEKLIB_BUILD}/stripmeta.o \
${GREEKLIB_BUILD}/stripquant.o \
${GREEKLIB_BUILD}/stripstemsep.o \
${GREEKLIB_BUILD}/stripzeroend.o \
${GREEKLIB_BUILD}/strsqz.o \
${GREEKLIB_BUILD}/subchar.o \
${GREEKLIB_BUILD}/vaxwords.o \
${GREEKLIB_BUILD}/xstrings.o \
${GREEKLIB_BUILD}/zap2ndbreath.o

#removed ${GREEKLIB_BUILD}/sprntGkflags.o because it has conflicting definitions to file in MORPHLIB and is unused

${GREEKLIB}: ${GREEKLIBOBJ}
	ar rv ${GREEKLIB} ${GREEKLIBOBJ}
	ranlib ${GREEKLIB}

${GREEKLIBOBJ}:
	$(CC) $(CFLAGS) -c -o $@ ${GREEKLIB_SOURCE}/$(*F).c

###############
# Example for building one of the utilities, cruncher.

build/stdiomorph.o:
	$(CC) $(CFLAGS) -c -o $@ ${ANALLIB_SOURCE}/$(*F).c

cruncher:${LIBS} ${ANALLIB} build/stdiomorph.o build/genwd.o
	${CC} $(CFLAGS) -o cruncher build/stdiomorph.o build/genwd.o ${ANALLIB} ${LIBS}
