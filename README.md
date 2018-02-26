# utl_find_common_observations_that_are_in_three_tables
Find common observations that are in three tables. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverfl SAS community.
    Find common observations that are in three tables

      Original Topic: Merge using Proc SQL natural join and intersect

      Find the observarions that are common to all three tables

      Three Solutions

         1. Natural Join (failed in WPS with error)
            ERROR: Multiple tables on one side of a NATURAL JOIN contain the variable name)

         2. Intersect  (same results in WPS and SAS)
         3. Combine and sort and look for duplicate groups od size three (not presented)

    github
    https://github.com/rogerjdeangelis/utl_find_common_observations_that_are_in_three_tables

    see
    https://communities.sas.com/t5/Base-SAS-Programming/Re-Merge-using-Proc-SQL/m-p/440238


    INPUT
    =====

      RULES
        Find the intersection oftables cls1st cls2nd cls3rd

      In this case WORK.CLS3RD  is in all three tables


      WORK.CLS1ST total obs=6

      Obs    NAME       SEX    AGE    HEIGHT    WEIGHT

       1     Henry       M      14     63.5      102.5
       2     James       M      12     57.3       83.0
       3     Jane        F      12     59.8       84.5
       4     Janet       F      15     62.5      112.5
       5     Jeffrey     M      13     62.5       84.0
       6     John        M      12     59.0       99.5


      WORK.CLS2ND  total obs=4

      Obs    NAME       SEX    AGE    HEIGHT    WEIGHT

       1     James       M      12     57.3       83.0
       2     Jane        F      12     59.8       84.5
       3     Janet       F      15     62.5      112.5
       4     Jeffrey     M      13     62.5       84.0


      WORK.CLS3RD total obs=2

      Obs    NAME     SEX    AGE    HEIGHT    WEIGHT

       1     Jane      F      12     59.8       84.5
       2     Janet     F      15     62.5      112.5


    PROCESS
    =======

        1. Natural join

           proc sql;
              create
                table want as
              select
                l.*
              from
                cls1st as l
                natural join cls2nd as c
                natural join cls3rd as r
           ;quit;


        2. Intersect

            proc sql;
              create
                table want as
              select
                *
              from
                cls1st

              intersect
              select
                *
              from
                cls2nd

              intersect
              select
                *
              from
                cls3rd
            ;quit;

    OUTPUT
    ======

      WORK.WANT total obs=2

      Obs    NAME     SEX    AGE    HEIGHT    WEIGHT

       1     Jane      F      12     59.8       84.5
       2     Janet     F      15     62.5      112.5

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    data cls1st cls2nd cls3rd;
      set sashelp.class;
      if  4  < _n_ < 11 then output cls1st;
      if  5  < _n_ < 10  then output cls2nd;
      if  6  < _n_ < 9 then output cls3rd;
    run;quit;


    NOTE: The data set WORK.CLS1ST has 12 observations and 5 variables.
    NOTE: The data set WORK.CLS2ND has 6 observations and 5 variables.
    NOTE: The data set WORK.CLS3RD has 2 observations and 5 variables.

    *
     ___  __ _ ___
    / __|/ _` / __|
    \__ \ (_| \__ \
    |___/\__,_|___/

    ;

    proc sql;
       create
         table want as
       select
         l.*
       from
         cls1st as l
         natural join cls2nd as c
         natural join cls3rd as r
    ;quit;

     proc sql;
       select
         *
       from
         cls1st

       intersect
       select
         *
       from
         cls2nd

       intersect
       select
         *
       from
         cls3rd
     ;quit;
    ');

    *
    __      ___ __  ___
    \ \ /\ / / '_ \/ __|
     \ V  V /| |_) \__ \
      \_/\_/ | .__/|___/
             |_|
    ;

    %utl_submit_wps64('
    libname wrk "%sysfunc(pathname(work))";
     proc sql;
       select
         *
       from
         wrk.cls1st

       intersect
       select
         *
       from
         wrk.cls2nd

       intersect
       select
         *
       from
         wrk.cls3rd
     ;quit;
    ');


    * WPS;
    %utl_submit_wps64('
    libname wrk "%sysfunc(pathname(work))";
    proc sql;
       select
         l.*
       from
         wrk.cls1st(rename=name=nam) as l
         natural join wrk.cls2nd
         natural join wrk.cls3rd
    ;quit;
    ');

    ERROR: Multiple tables on one side of a NATURAL JOIN contain the variable name


