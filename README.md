# utl-rename-all-columns-of-a-database-table
Rename all columns of a database table.
    Rename all columns of a database table

    github
    https://tinyurl.com/y7bbquv7
    https://github.com/rogerjdeangelis/utl-rename-all-columns-of-a-database-table

    see
    https://tinyurl.com/yb2wtkbz
    https://communities.sas.com/t5/SAS-Programming/Rename-all-variables/m-p/500828

    Lets add the suffix _v1 to all variables in sashelp.class

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    INPUT
    =====

     CLASS total obs=19

       NAME       SEX    AGE    HEIGHT    WEIGHT

       Alfred      M      14     69.0      112.5
       Alice       F      13     56.5       84.0
       Barbara     F      13     65.3       98.0
       Carol       F      14     62.8      102.5
      ....


    EXAMPLE OUTPUT
    --------------

     CLASS total obs=19

                                    HEIGHT_    WEIGHT_
     NAME_V1    SEX_V1    AGE_V1       V1         V1

     Alfred       M         14        69.0      112.5
     Alice        F         13        56.5       84.0
     Barbara      F         13        65.3       98.0
     Carol        F         14        62.8      102.5
     Henry        M         14        63.5      102.5
     James        M         12        57.3       83.0
     Jane         F         12        59.8       84.5


     Variables in Creation Order

    #    Variable     Type    Len

    1    NAME_V1      Char      8
    2    SEX_V1       Char      1
    3    AGE_V1       Num       8
    4    HEIGHT_V1    Num       8
    5    WEIGHT_V1    Num       8


    PROCESS
    =======

    %array(cols,values=%varlist(class));

    %put &=cols2;

    proc datasets lib=work;
       modify class;
          rename
            %do_over(cols,phrase=%str(? = ?_v1))
          ;
    run;quit;


    GENERATEDD CODE (if you do not want to use the macro in production.
    see debug macro to get the generated code.


    proc datasets lib=work;
       modify class;
          rename
            NAME = NAME_v1 SEX = SEX_v1 AGE = AGE_v1 HEIGHT = HEIGHT_v1 WEIGHT = WEIGHT_v1
          ;
    run;quit;

    OUTPUT
    ======

    see above

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    data class;
      set sashelp.class;
    run;quit;

