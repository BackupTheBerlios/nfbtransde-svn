Welcome to nfbtrans 7.74 November 4, 2002.

     Introduction.  NFBTRANS is a Grade Two braille translator.  It is freeware
and comes with complete C sourse and documentation.  The program converts ascii
text into braille and sends the result to a file or an embossor.  Special
formatting commands may be placed in the text to customize the output.	No
knowledge of braille is required to use this program,  however you must be able
to edit ascii files and be familiar with MSDOS commands.  The program has been successfully
compiled to run in unix and MSDos.  NFBTRANS is suitable for brailling menus, letters, and
manuals.  Many users have found that NFBTRANS serves their translation needs
without having to purchase expensivbe commercial translators.

     Features:	NFBTRANS is a very accurate Grade Two braille translator.
It can also back translate a Grade Two file into normal text.  The program
has many options which allow the user to customize its operation.  Formatting
commands can be used to generate Tables of Contents, ink print page numbers,
running headers and much more.	Translation rules are in a text file and
can easily be modified by the user.  The program can be configured to
hyphenate words to save space.

     Limitations: NFBTRANS can only translate from ascii text.	It cannot
convert binary files such as those produced by Microsoft Word unless they
are first converted to ascii text.  The text may have lines of unlimited
length and they may contain extended graphics characters.  Nfbtrans only
has a partial implementation of Grade 3 braille.

My purpose in releasing this version of nfbtrans is to make a high quality
braille translation program available to anyone who has a use for it.
It is very usable for most situations and will at least give you a
feel for braille translation.

Installing nfbtrans for MSDOS:
1.  Unzip this archive into a scratch directory.
2.  Change to that directory.
3.  Run the install program using the command
   INSTALL drive:\nfbtrans_directory.
4.  Examine the entries in nfbtrans.cnf and
    make changes if you wish.  See nfbtrans.txt for a complete
    description of options.  Include this directory in your path if you want to
    run nfbtrans from anywhere on your disk.

Installing nfbtrans for Unix:
     Unzip nfbtrans into an empty directory.  From the unix shell type
mv MAKEFILE Makefile
Then enter
make lowercase

     This is necessary because the program files were zipped in MSDOS and the
file names are in upper case when unzipped in unix.  Files specifically for
the MSDOS version are also removed at this time.

     Compile nfbtrans by entering make target where target is ultrix, linux,
sunos, djgpp, or aix.  You will have to add the target for your machine to
makefile if it is not one of these. The termcap entry in
the LIB= statement may need to be removed in linux.  When the compile is
successful, copy nfbtrans to usually /usr/local/bin and set permissions
usually chmod 755 nfbtrans.  Copy nfbtrans.cnf, back.tab, english.dic, spell.dat
and braille.tab to /usr/local/lib.  Edit nfbtrans.cnf and change options if
necessary.

Quick Start:
Always use the parallel port to connect with your embossor if possible.
Otherwise use the mode command to redirect lpt1 to whatever com port
you are using.
Examine nfbtrans.cnf paying special attention to the entries pw=, pl= and sp=.
Make sure your printer is configured to output computer braille, skip perfs,
and that it supports the page width and length given in nfbtrans.cnf.
Make sure the DOS print command is resident if you set sp=1.

Nfbtrans can be run in several ways.
The syntax is:
NFBTRANS [option1] [option2] [...] [file1] [file2] [...].
Options are of the form xx=string.  They are fully described in nfbtrans.txt.
There are over 100 options many of which you will never need to use.  They
may be given on the command line, in nfbtrans.cnf, in the translation table,
or in the document to be embossed. The program can also be run with no command
line arguments. The user will be prompted for required information depending
on the options in nfbtrans.cnf.

1.  To emboss a file, enter nfbtrans with no arguments and answer the questions.
2.  Enter nfbtrans pw=42 pl=27 myfile.txt to emboss myfile.txt page width of
42 and page length of 27.
3.  Enter nfbtrans file1.txt file2.txt to emboss file1.txt and file2.txt.
4.  Enter nfbtrans file1.txt file2.txt >outfile to translate file1.txt and
     file2.txt to outfile.
5.  Enter nfbtrans <file.txt to emboss file.txt.  Output goes to stdout in unix.
6.  Enter nfbtrans <file.txt >outfile.txt to translate file.txt to outfile.txt.
7.  Enter type infile.txt | nfbtrans to emboss infile.txt.
8.  Enter nfbtrans d:\progs\*.c c:\pascal\*.pas to emboss the .c and .pas
     files in the given directories.
9. Enter nfbtrans @listfile c:\temp\*.h to emboss the files contained in
listfile and then the .h files in c:\temp.

The file to be translated is assumed to be an ascii text file.	Lines may
be of any length.  Characters from decimal 128-255 are
processed according to the gm= option. gm=0 causes the high bit to be removed,
gm=1 causes the character to be ignored, and gm=2 leaves the character
unmodified.  This character will be translated according to the rules in
braille.tab.  Graphics characters are used primarily with other languages.

For properly formatted braille you must use the nfbtrans formatting commands.
Formatting commands are indicated by a tilde preceeding the actual formatting
command.  For example (tilde)cChapter One
willl center the line Chapter One.
If you don't care if headings are centered or if columns of tables are
aligned properly then don't worry about formatting commands.  Nfbtrans
can determine the start of a paragraph.  If paragraphs are preceeded by a
blank line use block paragraph mode (tilde)5.  If paragraphs are indented use
(tilde)t. Use (tilde)6 if you want nfbtrans to scan the file before
translating to determine how paragraphs are formatted. Nfbtrans can be set
up to rejoin hyphenated words in the file.  You may also use the optional
hyphenation dictionary english.dic to automatically hyphenate words.

Nfbtrans translates files differently depending on their extension.  This is
determined by the ex= and i0= through i9= options in nfbtrans.cnf.
Note that if input is redirected as in nfbtrans <infile.c, the program never
sees the name infile.c.  The input file is set to stdin if input is
redirected which means that infile.c will not be treated as a .c file.
Use the si= option if you want to name it something else.
By default nfbtrans translates files into grade two braille with the
nfbtrans formatting commands enabled.
Files with .arc, .arj, .com, .exe, .obj, .qwk, .zip and .zoo are considered
binary files and are not translated.
Files with .asm, .bas, .bat, .c, .cpp, .h, .mac, and .pas are considered
program files and are output in non-standard computer braille.
.brl files are output in grade two with formatting enabled.  .prt files are
output in 80 column format standard computer braille.  .man files
are considered unix man pages and are output in non-standard computer braille and
block paragraphs.
.fmt files are output in Grade Two with formatting enabled and no file and
date printed at the top of page one. Blank lines within two lines of the
bottom cause nfbtrans to go to the next page.
All other extensions are translated to Grade two with formatting enabled.

     Nfbtrans can easily be run in Windows even if you don't have a DOS
screenreader.  If you plan to use nfbtrans primarily for backtranslating .brf
files, do the following:
Associate the .brf extension with nfbtrans.  This is done using windows
Explorer, view, options, then file types. If .brf is not a registered file type
then click new, Braille Format File as description, content type Application,
check the show extension and confirm download boxes. For action the command line
should be something like this:
c:\command.com /c c:\tools\nfbtrans.exe tm=13 on=2 od=c:\mybooks
and the action can just be Open. Then click close until you get out of explorer
so your changes are saved.  Now when you click on a .brf file in explorer or run
from the run dialog box, nfbtrans automatically backtranslates your .brf file
and returns to windows.  Use the od= option in nfbtrans.cnf to specify where
to store the output. The output file has the same name as the input file
but with a .txt extension. Review the od= and on= options in nfbtrans.fmt.
This also allows you to download .brf files from web braille.

Note that nfbtrans does not support long file names. If a long name is given
as an argument or in a prompt you will get a file not found error. If you click
a long name from windows explorer the program uses the equivilent 8 by 3
MSDOS file name.

Send bug reports to n8kl@mindspring.com.
