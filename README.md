# utl-unix-and-windows-operating-system-file-compares
Unix and windows operating system file compares
    Unix and windows operating system file compares

        Not great but mmay help

        Two Solutions
           1. Windows "cmd /c fc /A /N d:\txt\class1.txt d:\txt\class2.txt > d:\txt\class3.txt"
           2. unix "diff -s /txt/class1.txt /txt/class2.txt > /txt/class3.txt"

    http://tinyurl.com/y4zzfb4r
    https://github.com/rogerjdeangelis/utl-unix-and-windows-operating-system-file-compares

    SAS-L
    https://listserv.uga.edu/cgi-bin/wa?A2=SAS-L;9dbc8a09.1902c

    appear to be multiple Perl/Python and R utilities.

    WINDOWS File Compare’s Switches and Parameters
    -----------------------------------------------

    /B  This switch will perform a binary comparison.
    /C  If you need to do a case insensitive comparison, use this switch.
    /A  This switch will make FC show only the first and last lines for each group of differences.
    /U  Use this switch to compare files as Unicode text files.
    /L  This will compare your files as ASCII text.
    /N  This switch can only be used with ASCII but it will show all the corresponding line numbers.
    /LBn  Replace the “n” with a number to limit the amount of consecutive different
    lines that FC will read before it will abort. The default, if you do not specify a
    number is 100 lines of mismatched text.

    /nnnn  Replacing the “n’s” here will tell FC that when it finds mismatched lines,
           it can only continue if it finds “n” consecutive matching lines after the mismatch.
           This is useful if you want to prevent two files from becoming extremely out of sync.

    /T  This switch will tell FC not to expand tabs to spaces.
    /W  If you use this switch, FC will compress white space (tabs and spaces) during
        its comparison of your files

    Unix diff man page
    ------------------
    http://man7.org/linux/man-pages/man1/diff.1.html

    INPUT
    =====

    filename ft15f001 "d:\txt\class1.txt";
    parmcards4;
    Alfred M 14 69 112.5
    Alice F 13 56.5 84
    Barbara F 13 65.3 98
    Carol F 14 62.8 102.5
    Henry M 14 63.5 102.5
    ;;;;
    run;quit;

    filename ft15f001 "d:\txt\class2.txt";
    parmcards4;
    Alfred M 14 69 112.5
    Alice F 13 56.5 84
    Barbara F 13 65.3 98
    Carol F 14 62.8 102.5
    yrneH M 14 63.5 102.5
    ;;;;
    run;quit;

    PARMCARDS does not appear to work in Unix, so do this

    data _null_;

      set sashelp.class(obs=5);

      file "&_r/txt/class1.txt";
      put (_all_) ($);

      if _n_=5 then name=left(reverse(name));

      file "&_r/txt/class2.txt";
      put (_all_) ($);

    run;quit;


    WINDOWS EXAMPLE OUTPUT
    ----------------------

    Comparing files D:\TXT\class1.txt and D:\TXT\CLASS2.TXT

    ***** D:\TXT\class1.txt
        4:  Carol F 14 62.8 102.5
        5:  Henry M 14 63.5 102.5
    ***** D:\TXT\CLASS2.TXT
        4:  Carol F 14 62.8 102.5
        5:  yrneH M 14 63.5 102.5     ** does not match name is different


    UNIX EXAMPLE OUTPUT
    -------------------
    5c5

    >  Henry M 14 63.5 102.5
    ------
    >  yrneH M 14 63.5 102.5     ** does not match name is different


    SOLUTIONS
    =========

    WINDOWS
    -------

    For some reason I could not get command pipe to work.

    x "cmd /c fc /A /N d:\txt\class1.txt d:\txt\class2.txt > d:\txt\class3.txt";

    data _null_;
       infile "d:\txt\class3.txt";
       input;
       put _infile_;
    run;quit;


    UNIX
    ----

    x "diff -s /txt/class1.txt /txt/class2.txt > /txt/class3.txt";

