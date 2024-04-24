# -utl-substituting-name-and-label-to-column-headings-in-excel
Substituting name and label to column headings in excel 
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
    /*                              |                               | |.. |   ...         |      ...          |      ,,,         | */       
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
