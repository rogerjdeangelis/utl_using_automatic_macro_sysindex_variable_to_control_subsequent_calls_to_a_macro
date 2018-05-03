# utl_using_automatic_macro_sysindex_variable_to_control_subsequent_calls_to_a_macro
Using the automatic macro sysindex variable to control subsequent calls to a macro. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Using the automatic macro sysindex variable to control subsequent calls to a macro

    "I am using ods excel and I do not want the title repeated in subsequent 'proc print'
    ods output.

    There may be an option but this may work for other ods/general problems and is a nice example
    of sysindex."

    github
    https://tinyurl.com/yawdob63
    https://github.com/rogerjdeangelis/utl_using_automatic_macro_sysindex_variable_to_control_subsequent_calls_to_a_macro

    SAS Forum
    https://communities.sas.com/t5/Base-SAS-Programming/ODS-excel-Title-appears-only-once/m-p/459753


    PROBLEM
    =======

      d:/xls/class.xlsx

          +----------------------------------------------------
          |     A      |    B       |     C      |    D       |
          +----------------------------------------------------
          |    SUBSEQUENT PUPILS IN MY MATH CLASS             |
          +----------------------------------------------------
       1  | NAME       |   SEX      |    AGE     |  HEIGHT    |
          +------------+------------+------------+------------+
       2  | ALFRED     |    M       |    15      |    69      |
          +------------+------------+------------+------------+
       3  | ALICE      |    F       |    13      |    58      |
          +------------+------------+------------+------------+
       4
          +----------------------------------------------------
       5  |    SUBSEQUENT PUPILS IN MY MATH CLASS             |  ** REMOVE THIS
          +----------------------------------------------------
       6  | NAME       |   SEX      |    AGE     |  HEIGHT    |
          +------------+------------+------------+------------+
       7  | MARY       |    M       |    15      |    69      |
          +------------+------------+------------+------------+
       8  | JOE        |    F       |    13      |    58      |
          +------------+------------+------------+------------+
       9
          +----------------------------------------------------
      10  |    SUBSEQUENT PUPILS IN MY MATH CLASS             |  ** REMOVE THIS
          +----------------------------------------------------
      11  | NAME       |   SEX      |    AGE     |  HEIGHT    |
          +------------+------------+------------+------------+
      12  | SAM        |    M       |    15      |    69      |
          +------------+------------+------------+------------+
      13  | KATE       |    F       |    13      |    58      |
          +------------+------------+------------+------------+


    PROCESS
    =======

      Algorithm

          1. Set global macro variable containing the count of previously
             called macros.

          2. When the macro is called sysindex increases by 1.

          3. Check inside the macro to see if difference between
             the incremented sysindx and the base saved sysindex > 1.
             If greater than 1 then the macro was previously called
             and turn titles and footnotes off.

      ods listing close;
      ods excel file="d:/xls/class.xlsx";
      ods excel options(
         sheet_name =' hdm_providers'
         embedded_titles='yes'
         embedded_footnotes= 'yes'
         sheet_interval="none"
        );

      title 'SUBSEQUENT PUPILS IN MY MATH CLASS';
      run;quit;

      %macro vlob(obs);

         %put &=sysindex &=savinx;

        %if %eval( (&sysindex - &savinx) > 1 ) %then %do;
          title;
          footnote;
        %end;

        proc print data=sashelp.class(obs=&obs) noobs;
        run;quit;

      %mend vlob;

      * set base value;
      %let savinx=&sysindex;

      %vlob(2);
      %vlob(3);
      %vlob(4);

      ods excel close;
      ods listing;
      run;quit;

    OUTPUT
    ======

      d:/xls/class.xlsx

          +----------------------------------------------------
          |     A      |    B       |     C      |    D       |
          +----------------------------------------------------
          |    SUBSEQUENT PUPILS IN MY MATH CLASS             |
          +----------------------------------------------------
       1  | NAME       |   SEX      |    AGE     |  HEIGHT    |
          +------------+------------+------------+------------+
       2  | ALFRED     |    M       |    15      |    69      |
          +------------+------------+------------+------------+
       3  | ALICE      |    F       |    13      |    58      |
          +------------+------------+------------+------------+
       4
          +----------------------------------------------------
       5  | NAME       |   SEX      |    AGE     |  HEIGHT    |
          +------------+------------+------------+------------+
       6  | MARY       |    M       |    15      |    69      |
          +------------+------------+------------+------------+
       7  | JOE        |    F       |    13      |    58      |
          +------------+------------+------------+------------+
       8
          +----------------------------------------------------
       9  | NAME       |   SEX      |    AGE     |  HEIGHT    |
          +------------+------------+------------+------------+
      10  | SAM        |    M       |    15      |    69      |
          +------------+------------+------------+------------+
      11  | KATE       |    F       |    13      |    58      |
          +------------+------------+------------+------------+

    *                _                          _     _
     _ __ ___   __ _| | _____   _ __  _ __ ___ | |__ | | ___ _ __ ___
    | '_ ` _ \ / _` | |/ / _ \ | '_ \| '__/ _ \| '_ \| |/ _ \ '_ ` _ \
    | | | | | | (_| |   <  __/ | |_) | | | (_) | |_) | |  __/ | | | | |
    |_| |_| |_|\__,_|_|\_\___| | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
                               |_|
    ;

      ods listing close;
      ods excel file="d:/xls/class.xlsx";
      ods excel options(
         sheet_name =' hdm_providers'
         embedded_titles='yes'
         embedded_footnotes= 'yes'
         sheet_interval="none"
        );

      title 'SUBSEQUENT PUPILS IN MY MATH CLASS';
      run;quit;

      %macro vlob(obs);

        proc print data=sashelp.class(obs=&obs) noobs;
        run;quit;

      %mend vlob;

      %vlob(2);
      %vlob(3);
      %vlob(4);

      ods excel close;
      ods listing;
      run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    see above

