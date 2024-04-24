    %let pgm=utl-substituting-name-and-label-to-column-headings-in-excel;

    Substituting name and label to column headings in excel

    github
    https://tinyurl.com/yv7dthtn
    https://github.com/rogerjdeangelis/utl-substituting-name-and-label-to-column-headings-in-excel

    /*******************************************************************************************************************************/
    /*                              |                               |                                                              */
    /*           INPUT              |        PROCESS                |                            OUTPUT                            */
    /*           =====              |        =======                |                            ======                            */
    /*                              |                               |                                                              */
    /* SASHELP.IRIS                 | proc sql;                     | d:/xls/namlbl.xlsx                                           */
    /*                              |    select                     |                                                              */
    /* Variables in Creation Order  |      cats(name,'="'           | +-------------------+-------------------+------------------+ */
    /*                              |        ,label,'/'             | |   |       A       |          B        |        C         | */
    /* Variable    Label            |        ,name,'"')             | +---+---------------+-------------------+------------------+ */
    /*                              |   into                        | |   |  Iris Species | Sepal Length (mm) | Sepal Width (mm) | */
    /* SPECIES     Iris Species     |     :namlbl separated by ' '  | | 1 |    SPECIES    |    SEPALLENGTH    |    SEPALWIDTH    | */
    /* SEPALLENGTH Sepal Length(mm) |   from                        | +---+---------------+-------------------+------------------+ */
    /* SEPALWIDTH  Sepal Width(mm)  |      sashelp.vcolumn          | | 2 |  Setosa       |       50          |       33         | */
    /*                              |   where                       | +---+---------------+-------------------+------------------+ */
    /*                              |          libname='SASHELP'    | | 3 |  Setosa       |       46          |       34         | */
    /*                              |      and  memname='IRIS'      | +---+---------------+-------------------+------------------+ */
    /*                              |      and  name eqt "S"        | | 4 |  Setossa      |       46          |       36         | */
    /*                              | ;quit;                        | +---+---------------+-------------------+------------------+ */
    /*                              |                               | |.. |   ...         |      ...          |      ...         | */
    /*                              | ods excel                     | +-------------------+-------------------+------------------+ */
    /*                              |  file="d:/xls/namlbl.xlsx"    | [IRIS]                                                       */
    /*                              |  options(sheet_name="Iris");  |                                                              */
    /*                              | proc report data=sashelp.iris |                                                              */
    /*                              |   (keep=S: obs=3)             |                                                              */
    /*                              |   split="/";                  |                                                              */
    /*                              |   label &namlbl.;             |                                                              */
    /*                              | run;quit;                     |                                                              */
    /*                              | ods excel close;              |                                                              */
    /*                              |                               |                                                              */
    /*******************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */


































|








































































Iris Species    Sepal Length (mm)    Sepal Width (mm)
  SPECIES          SEPALLENGTH          SEPALWIDTH

 Setosa                 50                  33
 Setosa                 46                  34
 Setosa                 46                  36
 Setosa                 51                  33
 Setosa                 55                  35




 d:/xls/namlbl.xlsx

 +-------------------+-------------------+------------------+
 |   |       A       |          B        |        C         |
 +---+---------------+-------------------+------------------+
 |   |  Iris Species | Sepal Length (mm) | Sepal Width (mm) |
 | 1 |    SPECIES    |    SEPALLENGTH    |    SEPALWIDTH    |
 +---+---------------+-------------------+------------------+
 | 2 |  Setosa       |       50          |       33         |
 +---+---------------+-------------------+------------------+
 | 3 |  Setosa       |       46          |       34         |
 +---+---------------+-------------------+------------------+
 | 4 |  Setossa      |       46          |       36         |
 +---+---------------+-------------------+------------------+
 |.. |   ...         |      ...          |      ,,,         |
 +-------------------+-------------------+------------------+

 [IRIS]













proc tabulate data=class;class sex age;table age,sex*(n pctn<age>)/rts=8
























                   ;;;;%end;%mend;/*'*/ *);*};*];*/;/*"*/;run;quit;%end;end;run;endcomp;%utlfix;



SPECIES     ="[SPECIES] Iris Species "
SEPALLENGTH ="[SEPALLENGTH] Sepal Length (mm) "
SEPALWIDTH  ="[SEPALWIDTH] Sepal Width (mm) "
PETALLENGTH  ="[PETALLENGTH] Petal Length (mm) "
PETALWIDTH=  "[PETALWIDTH] Petal Width (mm) "











/* T1002600 Adding name and label to column headings in excel

Adding name and label to column headings in excel

inspired by
https://goo.gl/MBFXuP
https://communities.sas.com/t5/Base-SAS-Programming/SAS-9-4-dblabel-error/m-p/335388/highlight/false#M75897


HAVE
====

Up to 40 obs from sashelp.iris total obs=150

Obs    SPECIES    SEPALLENGTH    SEPALWIDTH    PETALLENGTH    PETALWIDTH

  1    Setosa          50            33             14             2
  2    Setosa          46            34             14             3
  3    Setosa          46            36             10             2
  4    Setosa          51            33             17             5
  5    Setosa          55            35             13             2


             Variables in Creation Order

#    Variable       Type    Len    Label

1    SPECIES        Char     10    Iris Species
2    SEPALLENGTH    Num       8    Sepal Length (mm)
3    SEPALWIDTH     Num       8    Sepal Width (mm)
4    PETALLENGTH    Num       8    Petal Length (mm)
5    PETALWIDTH     Num       8    Petal Width (mm)


WANT in EXCEL
=============


       [SPECIES]    [SEPALLENGTH]    [SEPALWIDTH]    [PETALLENGTH]    [PETALWIDTH]
         Iris        Sepal Length     Sepal Width     Petal Length     Petal Width
Obs     Species          (mm)            (mm)             (mm)            (mm)

123    Virginica          61              30               49              18
124    Virginica          61              26               56              14
125    Virginica          64              28               56              21
126    Virginica          62              28               48              18
127    Virginica          77              30               61              23


WORKING CODE
============

 SQL
    proc sql;
      select
        catx(' ',cats(name,'="[',name,']'),label,'"')
        sashelp.vcolumn
 PRINT
    proc print data=sashelp.iris label;
    label &namlbl.;

FULL SOLUTION
=============

proc sql;
  select
    catx(' ',cats(name,'="[',name,']'),label,'"')
  into
    :namlbl separated by ' '
  from
    sashelp.vcolumn
  where
         libname='SASHELP'
    and  memname='IRIS'
;quit;

ods excel file="d:/xls/namlbl.xlsx";
proc print data=sashelp.iris label;
label &namlbl.;
run;quit;
ods excel close;
