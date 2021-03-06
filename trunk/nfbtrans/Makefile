#
#PURPOSE: The purpose of this file is to make nfbtrans, the braille
#translation software written by the National Federation of the Blind
#compile under unix, MSVC, or djgpp
#
#The source and object files are as follows:

SRCFILES=nfbtrans.c nfbpatch.c
OBJFILES=nfbtrans.o nfbpatch.o
LIBS= -ltermcap

#Compiler and linking flags are as follows:
CFLAGS=-O
CC=gcc
LDFLAGS=-Bdynamic

default:
	@echo "Please specify a target by entering one of the following:"
	@echo "make sunos"
	@echo "make sunos-insight"
	@echo "make ultrix"
	@echo "make aix"
	@echo "make linux"
	@echo "make djgpp"
	@echo "make msvc"
all: nfbtrans

djgppall: nfbtrans.exe

nfbtrans: $(OBJFILES)
	$(CC) $(CFLAGS) $(OBJFILES) $(LIBS) -o nfbtrans

nfbtrans.exe:$(OBJFILES)
	$(CC)  $(CFLAGS) $(OBJFILES) -o nfbtrans.exe

ultrix:
	$(MAKE) CFLAGS=-O

linux:
	$(MAKE) all CFLAGS="-O -Dlinux"

sunos:
	$(MAKE) all CFLAGS="-O -Dsunos"

insight:
	insight -fno-builtin -fwritable-strings \
	$(CFLAGS) $(OBJFILES) $(LIBS) -o nfbtrans

aix:
	$(MAKE) all CC=cc CFLAGS="-o -Dunix -Daix"

djgpp:
	$(MAKE) djgppall  CFLAGS="-mpentium -O2 -ggdb"

msvc:
	$(MAKE) msvcall

lowercase:
#remove files used only for dos
	rm *.ASM NFBTRANS *.EXE *.BAT
#copy files to lowercase names
	mv README.TXT readme.txt
	mv NFBTRANS.C nfbtrans.c
	mv NFBPATCH.C nfbpatch.c
	mv NFBTRANS.FMT nfbtrans.fmt
	mv NFBTRANS.CNF nfbtrans.cnf
	mv MAKEDOC makedoc
	chmod 755 makedoc
	mv BRAILLE.TAB braille.tab
	mv BACK.TAB back.tab
	mv TABLES.ZIP tables.zip
	mv TVFREQS.FMT tvfreqs.fmt
	mv ENGLISH.DIC english.dic
	mv SPELL.DAT spell.dat
	mv MENU.CNF menu.cnf
	mv BCOMP.C bcomp.c

clean:
	rm -f $(OBJFILES) nfbtrans
install:
	install -m 755 nfbtrans /usr/local/bin
	install tables/german2.tab /usr/local/lib/braille.tab
	install tables/back.tab /usr/local/lib
	install dict/english.dic /usr/local/lib
	install nfbtrans.cnf /usr/local/lib
	install spell.dat /usr/local/lib
	rm *.o nfbtrans
	