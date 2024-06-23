# utl-improved-r-script-to--create-a-sas-dataset-sas7bdat-without-sas-using-r-and-stattransfer
R creating a sas dataset without sas using r and stattransfer 
    %let pgm=utl-improved-r-script-to--create-a-sas-dataset-sas7bdat-without-sas-using-r-and-stattransfer;

    R creating a sas dataset without sas using r and stattransfer

      At the end of this message are all the macros you need to drop down
      from SAS to R and create a sas dataset with R and stattransfer, without sas
      anywhere.

      Problem
         Roundtrip from sas dataset -> to R dataframe -> back to SAS dataset (sas7bdat)
         Convert sas dataset to R dataframe then convert dataframe back to sas

      Five solutions

          0 final r create sas7bdat with stattransfer

      Hardcoding to simple R function solution (used to defelop 0 step above

          1. Hard coded parmcards calling R
          2  Hard coded submit macro calling R
          3  macro wrapper call R sumit macro arbitrary inputs and outputs
          4  inline r function

    github
    https://tinyurl.com/wt2shvwt
    https://github.com/rogerjdeangelis/utl-improved-r-script-to--create-a-sas-dataset-sas7bdat-without-sas-using-r-and-stattransfer

    SOAPBOX ON

    Despite Circle Systems claim that their free version is identical to the paid version,
    except for a limit on observations, this is not entirely accurate.
    In fact, to transfer an R dataframe to SAS datasetet, you need a paid version.
    It took me an entire day and numerous emails to discover this crucial information.
    Circle systems said the would retyrn my payment if I could not get the conversion to work.

    SOAPBOX OFF

    REQUIREMENTS
    ============

    Prices are online - refreshing

    All these support calling statransfer from R (or python)

    https://stattransfer.com/ordering/prices/

    $249 per year  Business                 Single-User Subscription (Includes upgrades during term)
    $249 per year  Gov Research Non Profit  Single-User Subscription (Includes upgrades during term)
    $179 per year  Academic                 Single-User Subscription (includes upgrades during term)
    $99  per year  Student                  Single-User Subscription (includes upgrades during term)

    Related repos
    https://github.com/rogerjdeangelis/utl-creating-a-sas-dataset-within-python-using-stattransfer
    https://github.com/rogerjdeangelis/utl-creating-a-sas-dataset-within-r-using-stattransfer
    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /***********************************************************************************************************************************/
    /*                                     |                                                  |                                        */
    /*  INPUT(d:/sd1/have.sas7bdat)        | PROCESS(need function in c:/oto/fn_tosas9x.R)    | OUTPUT (d:/sd1/want.sas7bdat)          */
    /*  ==========================         | ===============================================  | ================================       */
    /*                                     |                                                  |                                        */
    /*  SD1.HAVE total obs=19              | %utl_submit_r64x('                               | SD1.WANT total obs=19                  */
    /*                                     | library(haven);                                  |                                        */
    /*  NAME       SEX    AGE              | source("c:/oto/fn_tosas9x.R");                   | ROWNAMES NAME    SEX AGE               */
    /*                                     | have<-read_sas("d:/sd1/have.sas7bdat");          |                                        */
    /*  Alfred      M      14              | print(have);                                     |     1    Alfred   M   14               */
    /*  Alice       F      13              | fn_tosas9x(                                      |     2    Alice    F   13               */
    /*  Barbara     F      13              |       inp    = have                              |     3    Barbara  F   13               */
    /*  Carol       F      14              |      ,outlib ="d:/sd1/"                          |     4    Carol    F   14               */
    /*  Henry       M      14              |      ,outdsn ="want"                             |     5    Henry    M   14               */
    /* ...                                 |      );                                          |                                        */
    /*                                     | ');                                              |                                        */
    /* options validvarname=upcase;        | libname sd1 "d:/sd1";                            |                                        */
    /* libname sd1 "d:/sd1";               | proc print data=sd1.want;                        |  Data Set Page Size     4096           */
    /* data sd1.have;                      | run;print;t data=sd1.want;                       |  Number of Data  Pages  1              */
    /*   set sashelp.class                 |                                                  |  First Data Page        1              */
    /*    (keep=name sex age);             |--------------------------------------------------|  Max Obs per Page       288            */
    /* run;quit;                           |  YOU NEED TO SAVE THE FUNCTION SOMEWHERE.        |  Obs in First Data Page 19             */
    /*                                     |  I SAVED IT IN MY AUTOCALL LIBRARY.              |  Number of Data Repairs 0              */
    /*                                     |                                                  |  Filename      d:\sd1\want.sas7bdat    */
    /* Engine/Host Dependent Information   |  filename ft15f001 "c:/oto/fn_tosas9x.R";        |  Release Created        9.0000M0       */
    /*                                     |  parmcards4;                                     |  Host Created           WIN            */
    /* Data Set Page Size     65536        |   fn_tosas9x<-function(                          |  Owner Name             T7610\Roger    */
    /* Number of Data  Pages  1            |     inp    =NULL                                 |  File Size              5KB            */
    /* First Data Page        1            |    ,outlib =NULL                                 |  File Size (bytes)      5120           */
    /* Max Obs per Page       2715         |    ,outdsn =NULL                                 |                                        */
    /* Obs in First Data Page 19           |    )                                             |  Note:                                 */
    /* Number of Data Repairs 0            |   {                                              |                                        */
    /* ExtendObsCounter       YES          |   rds <- tempfile(fileext = ".rds");             |  ExtendObsCounter    YES is missing    */
    /* Filename      d:\sd1\have.sas7bdat  |   saveRDS(inp, file = rds);                      |                                        */
    /* Release Created        9.0401M7     |   stcmd <- tempfile(fileext = ".stcmd");         |                                        */
    /* Host Created           X64_10PRO    |   writeLines(c(                                  |                                        */
    /* Owner Name             T7610\Roger  |   "set numeric-names      n              "       |                                        */
    /* File Size              128KB        |  ,"set log-level          e              "       |                                        */
    /* File Size (bytes)      131072       |  ,"set in-encoding        system         "       |                                        */
    /*                                     |  ,"set out-encoding       system         "       |                                        */
    /*  Variables in Creation Order        |  ,"set enc-errors         sub            "       |                                        */
    /*                                     |  ,"set enc-sub-char       _              "       |                                        */
    /* #    Variable    Type    Len        |  ,"set enc-error-limit    100            "       |                                        */
    /*                                     |  ,"set var-case-ci        preserve-always"       |                                        */
    /* 1    NAME        Char      8        |  ,"set preserve-str-widths n             "       |                                        */
    /* 2    SEX         Char      1        |  ,"set preserve-num-widths n             "       |                                        */
    /* 3    AGE         Num       8        |  ,"set recs-to-optimize   all            "       |                                        */
    /*                                     |  ,"set factor-as-string   n              "       |                                        */
    /*                                     |  ,"set sas-date-fmt       mmddyy         "       |                                        */
    /*                                     |  ,"set sas-time-fmt       time           "       |                                        */
    /*                                     |  ,"set sas-datetime-fmt   datetime       "       |                                        */
    /*                                     |  ,"set write-file-label   none           "       |                                        */
    /*                                     |  ,"set write-sas-fmts     n              "       |                                        */
    /*                                     |  ,"set sas-outrep         windows_64     "       |                                        */
    /*                                     |  ,"set write-old-ver      18             "       |                                        */
    /*                                     |  ,paste("copy",rds,"sas9",                       |                                        */
    /*                                     |    paste0(outlib,outdsn,".sas7bdat"),"-T<outdsn")|                                        */
    /*                                     |  ,"quit"),stcmd);                                |                                        */
    /*                                     |   unlink(paste0(outlib,outdsn,".sas7bdat"));     |                                        */
    /*                                     |   system(                                        |                                        */
    /*                                     |    paste("c:/PROGRA~1/StatTransfer17-64/st.exe"  |                                        */
    /*                                     |   ,stcmd));                                      |                                        */
    /*                                     |    };                                            |                                        */
    /*                                     |  ;;;;                                            |                                        */
    /*                                     |  run;quit;                                       |                                        */
    /*                                     |                                                  |                                        */
    /***********************************************************************************************************************************/


    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      set sashelp.class(keep=mane sex age);
    run;quit;

    /*___     __ _             _                          _                       _____ _         _       _
     / _ \   / _(_)_ __   __ _| |  _ __   _ __ ___   __ _| | _____   ___  __ _ __|___  | |__   __| | __ _| |_
    | | | | | |_| | `_ \ / _` | | | `__| | `_ ` _ \ / _` | |/ / _ \ / __|/ _` / __| / /| `_ \ / _` |/ _` | __|
    | |_| | |  _| | | | | (_| | | | |    | | | | | | (_| |   <  __/ \__ \ (_| \__ \/ / | |_) | (_| | (_| | |_
     \___/  |_| |_|_| |_|\__,_|_| |_|    |_| |_| |_|\__,_|_|\_\___| |___/\__,_|___/_/  |_.__/ \__,_|\__,_|\__|
                            __                  _   _                        __    _          ____          _                       ___
     ___  __ ___   _____   / _|_   _ _ __   ___| |_(_) ___  _ __    ___ _   / /__ | |_ ___   / / _|_ __    | |_ ___  ___  __ _ ___ / _ \__  __   _ __
    / __|/ _` \ \ / / _ \ | |_| | | | `_ \ / __| __| |/ _ \| `_ \  / __(_) / / _ \| __/ _ \ / / |_| `_ \   | __/ _ \/ __|/ _` / __| (_) \ \/ /  | `__|
    \__ \ (_| |\ V /  __/ |  _| |_| | | | | (__| |_| | (_) | | | || (__ _ / / (_) | || (_) / /|  _| | | |  | || (_) \__ \ (_| \__ \\__, |>  < _ | |
    |___/\__,_| \_/ \___| |_|  \__,_|_| |_|\___|\__|_|\___/|_| |_| \___(_)_/ \___/ \__\___/_/ |_| |_| |_|___\__\___/|___/\__,_|___/  /_//_/\_(_)|_|
                                                                                                       |_____|
    */

    filename ft15f001 "c:/oto/fn_tosas9x.R";
    parmcards4;
     fn_tosas9x<-function(
       inp    =NULL
      ,outlib =NULL
      ,outdsn =NULL
      )
     {
     rds <- tempfile(fileext = ".rds");
     saveRDS(inp, file = rds);
     stcmd <- tempfile(fileext = ".stcmd");
     writeLines(c(
     "set numeric-names      n              "
    ,"set log-level          e              "
    ,"set in-encoding        system         "
    ,"set out-encoding       system         "
    ,"set enc-errors         sub            "
    ,"set enc-sub-char       _              "
    ,"set enc-error-limit    100            "
    ,"set var-case-ci        preserve-always"
    ,"set preserve-str-widths n             "
    ,"set preserve-num-widths n             "
    ,"set recs-to-optimize   all            "
    ,"set factor-as-string   n              "
    ,"set sas-date-fmt       mmddyy         "
    ,"set sas-time-fmt       time           "
    ,"set sas-datetime-fmt   datetime       "
    ,"set write-file-label   none           "
    ,"set write-sas-fmts     n              "
    ,"set sas-outrep         windows_64     "
    ,"set write-old-ver      18             "
    ,paste("copy",rds,"sas9",
      paste0(outlib,outdsn,".sas7bdat"),"-T<outdsn")
    ,"quit"),stcmd);
     unlink(paste0(outlib,outdsn,".sas7bdat"));
     system(paste("c:/PROGRA~1/StatTransfer17-64/st.exe"
       ,stcmd));
      };
    ;;;;
    run;quit;

    /*                   _                      _____ _         _       _
      ___ _ __ ___  __ _| |_ ___   ___  __ _ __|___  | |__   __| | __ _| |_
     / __| `__/ _ \/ _` | __/ _ \ / __|/ _` / __| / /| `_ \ / _` |/ _` | __|
    | (__| | |  __/ (_| | ||  __/ \__ \ (_| \__ \/ / | |_) | (_| | (_| | |_
     \___|_|  \___|\__,_|\__\___| |___/\__,_|___/_/  |_.__/ \__,_|\__,_|\__|

    */

    proc datasets lib=sd1 nodetails nolist; /* not needed because deleted in script */
     delete want;
    run;quit;

    %utl_submit_r64x('
     library(haven);
    source("c:/oto/fn_tosas9x.R");
    have<-read_sas("d:/sd1/have.sas7bdat");
    print(have);
    fn_tosas9x(
          inp    = have
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         );
    ');

    /***********************************************************************************************************************************/
    /*                                                                                                                                 */
    /*                                                                                                                                 */
    /*  OUTPUT (d:/sd1/want.sas7bdat)                                                                                                  */
    /*  ================================                                                                                               */
    /*                                                                                                                                 */
    /*  SD1.WANT total obs=19                                                                                                          */
    /*                                                                                                                                 */
    /*  ROWNAMES NAME    SEX AGE                                                                                                       */
    /*                                                                                                                                 */
    /*      1    Alfred   M   14                                                                                                       */
    /*      2    Alice    F   13                                                                                                       */
    /*      3    Barbara  F   13                                                                                                       */
    /*      4    Carol    F   14                                                                                                       */
    /*      5    Henry    M   14                                                                                                       */
    /*                                                                                                                                 */
    /*                                                                                                                                 */
    /*                                                                                                                                 */
    /*   Data Set Page Size     4096                                                                                                   */
    /*   Number of Data  Pages  1                                                                                                      */
    /*   First Data Page        1                                                                                                      */
    /*   Max Obs per Page       288                                                                                                    */
    /*   Obs in First Data Page 19                                                                                                     */
    /*   Number of Data Repairs 0                                                                                                      */
    /*   Filename      d:\sd1\want.sas7bdat                                                                                            */
    /*   Release Created        9.0000M0                                                                                               */
    /*   Host Created           WIN                                                                                                    */
    /*   Owner Name             T7610\Roger                                                                                            */
    /*   File Size              5KB                                                                                                    */
    /*   File Size (bytes)      5120                                                                                                   */
    /*                                                                                                                                 */
    /*   Note:                                                                                                                         */
    /*                                                                                                                                 */
    /*   ExtendObsCounter    YES is missing                                                                                            */
    /*                                                                                                                                 */
    /*---------------------------------------------------------------------------------------------------------------------------------*/
    /*   _                                                                                                                             */
    /*  | | ___   __ _                                                                                                                 */
    /*  | |/ _ \ / _` |                                                                                                                */
    /*  | | (_) | (_| |                                                                                                                */
    /*  |_|\___/ \__, |                                                                                                                */
    /*           |___/                                                                                                                 */
    /*                                                                                                                                 */
    /*  > library(haven);source("c:/oto/fn_tosas9x.R");have<-read_sas("d:/sd1/have.sas7bdat");                                         */
    /*   print(have);fn_tosas9x(      inp    = have     ,outlib ="d:/sd1/"     ,outdsn ="want"                                         */
    /*       );                                                                                                                        */
    /*  # A tibble: 19 x 3                                                                                                             */
    /*     NAME    SEX     AGE                                                                                                         */
    /*     <chr>   <chr> <dbl>                                                                                                         */
    /*   1 Alfred  M        14                                                                                                         */
    /*   2 Alice   F        13                                                                                                         */
    /*   3 Barbara F        13                                                                                                         */
    /*   4 Carol   F        14                                                                                                         */
    /*   5 Henry   M        14                                                                                                         */
    /*   6 James   M        12                                                                                                         */
    /*   7 Jane    F        12                                                                                                         */
    /*   8 Janet   F        15                                                                                                         */
    /*   9 Jeffrey M        13                                                                                                         */
    /*  10 John    M        12                                                                                                         */
    /*  11 Joyce   F        11                                                                                                         */
    /*  12 Judy    F        14                                                                                                         */
    /*  13 Louise  F        12                                                                                                         */
    /*  14 Mary    F        15                                                                                                         */
    /*  15 Philip  M        16                                                                                                         */
    /*  16 Robert  M        12                                                                                                         */
    /*  17 Ronald  M        15                                                                                                         */
    /*  18 Thomas  M        11                                                                                                         */
    /*  19 William M        15                                                                                                         */
    /*    [1] 0                                                                                                                       */
    /*  >                                                                                                                              */
    /*  NOTE: 26 lines were written to file PRINT.                                                                                     */
    /*  Stderr output:                                                                                                                 */
    /*  Warning message:                                                                                                               */
    /*  package 'haven' was built under R version 4.1.3                                                                                */
    /*  Stat/Transfer - Command Processor (c) 1986-2024 Circle Systems, Inc.                                                           */
    /*  www.stattransfer.com                                                                                                           */
    /*  Version 17.0.1688.0331 - 64 Bit Windows (10.0.19041)                                                                           */
    /*                                                                                                                                 */
    /*  Serial: HBRC-NEYA-UXDV-ELMT                                                                                                    */
    /*  User: Roger DeAngelis - CompuCraft                                                                                             */
    /*  License Type: Single User Commercial Subscription                                                                              */
    /*  Status: License OK - Expires March 1, 2025                                                                                     */
    /*  Transferring from R Single object: C:\Users\Roger\AppData\Local\Temp\RtmpUDXue2\file165858c95f18.rds                           */
    /*  Input file has 4 variables                                                                                                     */
    /*  The input file contains string variables and although optimization is not required by the output format,                       */
    /*  S/T will enable it to make sure that the output strings will not                                                               */
    /*  get truncated.                                                                                                                 */
    /*  Optimizing (All records) ...                                                                                                   */
    /*  Transferring to SAS Data File - Version Nine: d:/sd1/want.sas7bdat                                                             */
    /*                                                                                                                                 */
    /*  19 cases were transferred(0.02 seconds)                                                                                        */
    /*                                                                                                                                 */
    /***********************************************************************************************************************************/


    /*   _                   _               _                                                     _
    / | | |__   __ _ _ __ __| | ___ ___   __| | ___   _ __   __ _ _ __ _ __ ___   ___ __ _ _ __ __| |___
    | | | `_ \ / _` | `__/ _` |/ __/ _ \ / _` |/ _ \ | `_ \ / _` | `__| `_ ` _ \ / __/ _` | `__/ _` / __|
    | | | | | | (_| | | | (_| | (_| (_) | (_| |  __/ | |_) | (_| | |  | | | | | | (_| (_| | | | (_| \__ \
    |_| |_| |_|\__,_|_|  \__,_|\___\___/ \__,_|\___| | .__/ \__,_|_|  |_| |_| |_|\___\__,_|_|  \__,_|___/
                                                     |_|
    */

    /* not needed because deleted in script */
    libname tmp "c:/temp";
    proc datasets lib=tmp nodetails nolist;
     delete want;
    run;quit;

    %utlfkil(c:/temp/rdsdat.rds);
    %utlfkil(c:/temp/cmds.stcmd);

    filename ft15f001 clear; /* not needed */
    %utl_rbeginx;
    parmcards4;
     library(haven)
     want<-read_sas("d:/sd1/have.sas7bdat")
     file.remove("c:/temp/rdsdat.rds")
     saveRDS(want, file="c:/temp/rdsdat.rds")
     fileConn<-file("c:/temp/cmds.stcmd")
     writeLines(c(
     "set numeric-names      n              "
    ,"set log-level          e              "
    ,"set in-encoding        system         "
    ,"set out-encoding       system         "
    ,"set enc-errors         sub            "
    ,"set enc-sub-char       _              "
    ,"set enc-error-limit    100            "
    ,"set var-case-ci        preserve-always"
    ,"set preserve-str-widths n             "
    ,"set preserve-num-widths n             "
    ,"set recs-to-optimize   all            "
    ,"set factor-as-string   n              "
    ,"set sas-date-fmt       mmddyy         "
    ,"set sas-time-fmt       time           "
    ,"set sas-datetime-fmt   datetime       "
    ,"set write-file-label   none           "
    ,"set write-sas-fmts     n              "
    ,"set sas-outrep         windows_64     "
    ,"set write-old-ver      18             "
    ,"copy  C:/temp/rdsdat.rds sas9 C:/temp/want.sas7bdat -T<want"
    ,"quit"),fileConn)
     close(fileConn)
     unlink("c:/temp/want.sas7bdat")
     system("c:/PROGRA~1/StatTransfer17-64/st.exe c:/temp/cmds.stcmd")
    ;;;;
    %utl_rendx;

    libname tmp "c:/temp";
    proc print data=tmp.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  c:/temp/want,sas7bdat                                                                                                 */
    /*                                                                                                                        */
    /*   ROWNAMES    NAME       SEX    AGE    HEIGHT    WEIGHT                                                                */
    /*                                                                                                                        */
    /*       1       Alfred      M      14     69.0      112.5                                                                */
    /*       2       Alice       F      13     56.5       84.0                                                                */
    /*       3       Barbara     F      13     65.3       98.0                                                                */
    /*       4       Carol       F      14     62.8      102.5                                                                */
    /*       5       Henry       M      14     63.5      102.5                                                                */
    /*       6       James       M      12     57.3       83.0                                                                */
    /*    ...                                                                                                                 */
    /*                                                                                                                        */
    /*  > library(haven)                                                                                                      */
    /*  > want<-read_sas("d:/sd1/have.sas7bdat")                                                                              */
    /*  > file.remove("c:/temp/rdsdat.rds")                                                                                   */
    /*  [1] TRUE                                                                                                              */
    /*  > saveRDS(want, file="c:/temp/rdsdat.rds")                                                                            */
    /*  > fileConn<-file("c:/temp/cmds.stcmd")                                                                                */
    /*  > writeLines(c(                                                                                                       */
    /*  + "set numeric-names      n              "                                                                            */
    /*  + ,"set log-level          e              "                                                                           */
    /*  + ,"set in-encoding        system         "                                                                           */
    /*  + ,"set out-encoding       system         "                                                                           */
    /*  + ,"set enc-errors         sub            "                                                                           */
    /*  + ,"set enc-sub-char       _              "                                                                           */
    /*  + ,"set enc-error-limit    100            "                                                                           */
    /*  + ,"set var-case-ci        preserve-always"                                                                           */
    /*  + ,"set preserve-str-widths n             "                                                                           */
    /*  + ,"set preserve-num-widths n             "                                                                           */
    /*  + ,"set recs-to-optimize   all            "                                                                           */
    /*  + ,"set factor-as-string   n              "                                                                           */
    /*  + ,"set sas-date-fmt       mmddyy         "                                                                           */
    /*  + ,"set sas-time-fmt       time           "                                                                           */
    /*  + ,"set sas-datetime-fmt   datetime       "                                                                           */
    /*  + ,"set write-file-label   none           "                                                                           */
    /*  + ,"set write-sas-fmts     n              "                                                                           */
    /*  + ,"set sas-outrep         windows_64     "                                                                           */
    /*  + ,"set write-old-ver      18             "                                                                           */
    /*  + ,"copy  C:/temp/rdsdat.rds sas9 C:/temp/want.sas7bdat -T<want"                                                      */
    /*  + ,"quit"),fileConn)                                                                                                  */
    /*  > close(fileConn)                                                                                                     */
    /*  > file.remove("c:/temp/want.sas7bdat")                                                                                */
    /*  [1] TRUE                                                                                                              */
    /*  > system("c:/PROGRA~1/StatTransfer17-64/st.exe c:/temp/cmds.stcmd")                                                   */
    /*  >                                                                                                                     */
    /*  NOTE: 34 lines were written to file PRINT.                                                                            */
    /*  Stderr output:                                                                                                        */
    /*  Stat/Transfer - Command Processor (c) 1986-2024 Circle Systems, Inc.                                                  */
    /*  www.stattransfer.com                                                                                                  */
    /*  Version 17.0.1688.0331 - 64 Bit Windows (10.0.19041)                                                                  */
    /*                                                                                                                        */
    /*  Serial: HBRC-NEYA-UXDV-ELMT                                                                                           */
    /*  User: Roger DeAngelis - CompuCraft                                                                                    */
    /*  License Type: Single User Commercial Subscription                                                                     */
    /*  Status: License OK - Expires March 1, 2025                                                                            */
    /*  Transferring from R Single object: C:/temp/rdsdat.rds                                                                 */
    /*  Input file has 6 variables                                                                                            */
    /*  The input file contains string variables and although optimization is not required by the output                      */
    /*  format, S/T will enable it to make sure that the output strings will not                                              */
    /*  get truncated.                                                                                                        */
    /*  Optimizing (All records) ...                                                                                          */
    /*  Transferring to SAS Data File - Version Nine: C:/temp/want.sas7bdat                                                   */
    /*                                                                                                                        */
    /*  19 cases were transferred(0.01 seconds)                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/
    /*___    _                   _               _                  _               _ _
    |___ \  | |__   __ _ _ __ __| | ___ ___   __| | ___   ___ _   _| |__  _ __ ___ (_) |_   _ __ ___   __ _  ___ _ __ ___
      __) | | `_ \ / _` | `__/ _` |/ __/ _ \ / _` |/ _ \ / __| | | | `_ \| `_ ` _ \| | __| | `_ ` _ \ / _` |/ __| `__/ _ \
     / __/  | | | | (_| | | | (_| | (_| (_) | (_| |  __/ \__ \ |_| | |_) | | | | | | | |_  | | | | | | (_| | (__| | | (_) |
    |_____| |_| |_|\__,_|_|  \__,_|\___\___/ \__,_|\___| |___/\__,_|_.__/|_| |_| |_|_|\__| |_| |_| |_|\__,_|\___|_|  \___/
    */

    /* not needed because deleted in script */
    libname tmp "c:/temp";
    proc datasets lib=tmp nodetails nolist;
     delete want;
    run;quit;

    %utlfkil(c:/temp/rdsdat.rds);
    %utlfkil(c:/temp/cmds.stcmd);

    %utl_submit_r64x('
     library(haven);
     want<-read_sas("d:/sd1/have.sas7bdat");
     file.remove("c:/temp/rdsdat.rds");
     saveRDS(want, file="c:/temp/rdsdat.rds");
     fileConn<-file("c:/temp/cmds.stcmd");
     writeLines(c(
     "set numeric-names      n              "
    ,"set log-level          e              "
    ,"set in-encoding        system         "
    ,"set out-encoding       system         "
    ,"set enc-errors         sub            "
    ,"set enc-sub-char       _              "
    ,"set enc-error-limit    100            "
    ,"set var-case-ci        preserve-always"
    ,"set preserve-str-widths n             "
    ,"set preserve-num-widths n             "
    ,"set recs-to-optimize   all            "
    ,"set factor-as-string   n              "
    ,"set sas-date-fmt       mmddyy         "
    ,"set sas-time-fmt       time           "
    ,"set sas-datetime-fmt   datetime       "
    ,"set write-file-label   none           "
    ,"set write-sas-fmts     n              "
    ,"set sas-outrep         windows_64     "
    ,"set write-old-ver      18             "
    ,"copy  C:/temp/rdsdat.rds sas9 C:/temp/want.sas7bdat -T<want"
    ,"quit"),fileConn);
     close(fileConn);
     unlink("c:/temp/want.sas7bdat");
     system("c:/PROGRA~1/StatTransfer17-64/st.exe c:/temp/cmds.stcmd");
    ');

    libname tmp "c:/temp";
    proc print data=tmp.want;
    run;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  c:/temp/want,sas7bdat                                                                                                 */
    /*                                                                                                                        */
    /*   ROWNAMES    NAME       SEX    AGE                                                                                    */
    /*                                                                                                                        */
    /*       1       Alfred      M      14                                                                                    */
    /*       2       Alice       F      13                                                                                    */
    /*       3       Barbara     F      13                                                                                    */
    /*       4       Carol       F      14                                                                                    */
    /*       5       Henry       M      14                                                                                    */
    /*       6       James       M      12                                                                                    */
    /*    ...                                                                                                                 */
    /*                                                                                                                        */
    /*  > library(haven); want<-read_sas("d:/sd1/have.sas7bdat"); file.remove("c:/temp/rdsdat.rds");                          */
    /*  saveRDS(want, file="c:/temp/rdsdat.rds"); fileConn<-file("c:/temp/cmds.stcmd")                                        */
    /*  ; writeLines(c( "set numeric-names      n              ","set log-level          e              ",                    */
    /*  "set in-encoding        system         ","set out-encoding       system                                               */
    /*         ","set enc-errors         sub            ","set enc-sub-char       _              ",                           */
    /*  "set enc-error-limit    100            ","set var-case-ci        preserve-always                                      */
    /*  ","set preserve-str-widths n             ","set preserve-num-widths n             ",                                  */
    /*  "set recs-to-optimize   all            ","set factor-as-string   n              ","set                                */
    /*  sas-date-fmt       mmddyy         ","set sas-time-fmt       time           ",                                         */
    /*  "set sas-datetime-fmt   datetime       ","set write-file-label   none           ","set write-s                        */
    /*  as-fmts     n              ","set sas-outrep         windows_64     ",                                                */
    /*  "set write-old-ver      18             ","copy  C:/temp/rdsdat.rds sas9 C:/temp/want.sas7bdat -T<want                 */
    /*  ","quit"),fileConn); close(fileConn); file.remove("c:/temp/want.sas7bdat");                                           */
    /*  system("c:/PROGRA~1/StatTransfer17-64/st.exe c:/temp/cmds.stcmd");                                                    */
    /*  [1] TRUE                                                                                                              */
    /*  [1] TRUE                                                                                                              */
    /*  >                                                                                                                     */
    /*  NOTE: 11 lines were written to file PRINT.                                                                            */
    /*  Stderr output:                                                                                                        */
    /*  Warning message:                                                                                                      */
    /*  package 'haven' was built under R version 4.1.3                                                                       */
    /*  Stat/Transfer - Command Processor (c) 1986-2024 Circle Systems, Inc.                                                  */
    /*  www.stattransfer.com                                                                                                  */
    /*  Version 17.0.1688.0331 - 64 Bit Windows (10.0.19041)                                                                  */
    /*                                                                                                                        */
    /*  Serial: HBRC-NEYA-UXDV-ELMT                                                                                           */
    /*  User: Roger DeAngelis - CompuCraft                                                                                    */
    /*  License Type: Single User Commercial Subscription                                                                     */
    /*  Status: License OK - Expires March 1, 2025                                                                            */
    /*  Transferring from R Single object: C:/temp/rdsdat.rds                                                                 */
    /*  Input file has 6 variables                                                                                            */
    /*  The input file contains string variables and although optimization is not required by the output                      */
    /*  format, S/T will enable it to make sure that the output strings will not                                              */
    /*  get truncated.                                                                                                        */
    /*  Optimizing (All records) ...                                                                                          */
    /*  Transferring to SAS Data File - Version Nine: C:/temp/want.sas7bdat                                                   */
    /*                                                                                                                        */
    /*  19 cases were transferred(0.00 seconds)                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____
    |___ /   _ __ ___   __ _  ___ _ __ ___   __      ___ __ __ _ _ __  _ __   ___ _ __
      |_ \  | `_ ` _ \ / _` |/ __| `__/ _ \  \ \ /\ / / `__/ _` | `_ \| `_ \ / _ \ `__|
     ___) | | | | | | | (_| | (__| | | (_) |  \ V  V /| | | (_| | |_) | |_) |  __/ |
    |____/  |_| |_| |_|\__,_|\___|_|  \___/    \_/\_/ |_|  \__,_| .__/| .__/ \___|_|
                                                                |_|   |_|
    */

    /* not needed because deleted in script. Used in testing */
    libname tmp "c:/temp";
    proc datasets lib=sd1 nodetails nolist;
     delete want;
    run;quit;

    %utlfkil(d:/wrk/cmds.stcmd);
    %utlfkil(d:/wrk/rdsdat.rds);

    %symdel inp outlib dsn stcmds rds / nowarn;/* not needed */

    %macro wrapper(
       inp     =
       ,outlib =
       ,dsn    =
       ,stcmds =
       ,rds    =
       )/ des="submit r64 with arbitrary inputs and outputs";

    %utl_submit_r64x('
     library(haven);
     want<-read_sas("&inp");
     file.remove("&rds");
     saveRDS(&dsn, file="&rds");
     fileConn<-file("&stcmds");
     writeLines(c(
     "set numeric-names      n              "
    ,"set log-level          e              "
    ,"set in-encoding        system         "
    ,"set out-encoding       system         "
    ,"set enc-errors         sub            "
    ,"set enc-sub-char       _              "
    ,"set enc-error-limit    100            "
    ,"set var-case-ci        preserve-always"
    ,"set preserve-str-widths n             "
    ,"set preserve-num-widths n             "
    ,"set recs-to-optimize   all            "
    ,"set factor-as-string   n              "
    ,"set sas-date-fmt       mmddyy         "
    ,"set sas-time-fmt       time           "
    ,"set sas-datetime-fmt   datetime       "
    ,"set write-file-label   none           "
    ,"set write-sas-fmts     n              "
    ,"set sas-outrep         windows_64     "
    ,"set write-old-ver      18             "
    ,"copy  &rds sas9 &outlib.&dsn..sas7bdat -T<&dsn"
    ,"quit"),fileConn);
     close(fileConn);
     file.remove("&outlib.&dsn..sas7bdat");
     system("c:/PROGRA~1/StatTransfer17-64/st.exe &stcmds")
    ',resolve=Y);

    %mend wrapper;

    %wrapper(
       inp     =d:/sd1/have.sas7bdat
       ,outlib =d:/sd1/
       ,dsn    =want
       ,stcmds =d:/wrk/cmds.stcmd
       ,rds    =d:/wrk/rdsdat.rds
       );

    libname tmp "c:/temp";
    proc print data=tmp.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  c:/temp/want,sas7bdat                                                                                                 */
    /*                                                                                                                        */
    /*   ROWNAMES    NAME       SEX    AGE                                                                                    */
    /*                                                                                                                        */
    /*       1       Alfred      M      14                                                                                    */
    /*       2       Alice       F      13                                                                                    */
    /*       3       Barbara     F      13                                                                                    */
    /*       4       Carol       F      14                                                                                    */
    /*       5       Henry       M      14                                                                                    */
    /*       6       James       M      12                                                                                    */
    /*    ......                                                                                                              */
    /*                                                                                                                        */
    /*  MLOGIC(WRAPPER):  Beginning execution.                                                                                */
    /*  MLOGIC(WRAPPER):  Parameter INP has value d:/sd1/have.sas7bdat                                                        */
    /*  MLOGIC(WRAPPER):  Parameter OUTLIB has value d:/sd1/                                                                  */
    /*  MLOGIC(WRAPPER):  Parameter DSN has value want                                                                        */
    /*  MLOGIC(WRAPPER):  Parameter STCMDS has value &wrk/cmds.stcmd                                                          */
    /*  MLOGIC(WRAPPER):  Parameter RDS has value &wrk/rdsdat.rds                                                             */
    /*  MLOGIC(UTL_SUBMIT_R64X):  Beginning execution.                                                                        */
    /*  MLOGIC(UTL_SUBMIT_R64X):  Parameter PGMX has value ' library(haven); want<-read_sas("&inp");                          */
    /*  file.remove("&rds"); saveRDS(&dsn, file="&rds"); fileConn<-file("&stcmds");                                           */
    /*        writeLines(c( "set numeric-names      n              ","set log-level          e              ",                */
    /*  "set in-encoding        system         ","set out-encoding                                                            */
    /*        system         ","set enc-errors         sub            ","set enc-sub-char       _              "              */
    /*  ,"set enc-error-limit    100            ","set var-case-ci                                                            */
    /*        preserve-always","set preserve-str-widths n             ","set preserve-num-widths n             "              */
    /*  ,"set recs-to-optimize   all            ","set factor-as-string                                                       */
    /*        n              ","set sas-date-fmt       mmddyy         ","set sas-time-fmt       time           "              */
    /*  ,"set sas-datetime-fmt   datetime       ","set write-file-label                                                       */
    /*        none           ","set write-sas-fmts     n              ","set sas-outrep         windows_64     "              */
    /*  ,"set write-old-ver      18             ","copy  &rds sas9                                                            */
    /*        &outlib.&dsn..sas7bdat -T<&dsn","quit"),fileConn); close(fileConn);                                             */
    /*  file.remove("&outlib.&dsn..sas7bdat"); system("c:/PROGRA~1/StatTransfer17-64/st.exe &stcmds")'                        */
    /*  MLOGIC(UTL_SUBMIT_R64X):  Parameter RESOLVE has value Y                                                               */
    /*  MLOGIC(UTL_SUBMIT_R64X):  Parameter RETURN has value N                                                                */
    /*  MLOGIC(UTLFKIL):  Beginning execution.                                                                                */
    /*  MLOGIC(UTLFKIL):  This macro was compiled from the autocall file c:\oto\utlfkil.sas                                   */
    /*  MLOGIC(UTLFKIL):  Parameter UTLFKIL has value f:\wrk\_TD14528_T7610_/r_pgm.txt                                        */
    /*  MLOGIC(UTLFKIL):  %LOCAL  URC                                                                                         */
    /*  MLOGIC(UTLFKIL):  %LET (variable name is URC)                                                                         */
    /*  SYMBOLGEN:  Macro variable UTLFKIL resolves to f:\wrk\_TD14528_T7610_/r_pgm.txt                                       */
    /*  SYMBOLGEN:  Macro variable URC resolves to 0                                                                          */
    /*  SYMBOLGEN:  Macro variable FNAME resolves to #LN00795                                                                 */
    /*  MLOGIC(UTLFKIL):  %IF condition &urc = 0 and %sysfunc(fexist(&fname)) is TRUE                                         */
    /*  MLOGIC(UTLFKIL):  %LET (variable name is URC)                                                                         */
    /*  SYMBOLGEN:  Macro variable FNAME resolves to #LN00795                                                                 */
    /*  MLOGIC(UTLFKIL):  %PUT xxxxxx &fname deleted xxxxxx                                                                   */
    /*  SYMBOLGEN:  Macro variable FNAME resolves to #LN00795                                                                 */
    /*  xxxxxx #LN00795 deleted xxxxxx                                                                                        */
    /*  MLOGIC(UTLFKIL):  %LET (variable name is URC)                                                                         */
    /*  MPRINT(UTLFKIL):   run;                                                                                               */
    /*  MLOGIC(UTLFKIL):  Ending execution.                                                                                   */
    /*  MPRINT(UTL_SUBMIT_R64X):  ;                                                                                           */
    /*  MPRINT(UTL_SUBMIT_R64X):   filename _clp clipbrd;                                                                     */
    /*  MPRINT(UTL_SUBMIT_R64X):   data _null_;                                                                               */
    /*  MPRINT(UTL_SUBMIT_R64X):   file _clp;                                                                                 */
    /*  MPRINT(UTL_SUBMIT_R64X):   put " ";                                                                                   */
    /*  MPRINT(UTL_SUBMIT_R64X):   run;                                                                                       */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  > library(haven); want<-read_sas("d:/sd1/have.sas7bdat"); file.remove("c:/temp/rdsdat.rds");                          */
    /*  saveRDS(want, file="c:/temp/rdsdat.rds"); fileConn<-file("c:/temp/cmds.stcmd")                                        */
    /*  ; writeLines(c( "set numeric-names      n              ","set log-level          e              ",                    */
    /*  "set in-encoding        system         ","set out-encoding       system                                               */
    /*         ","set enc-errors         sub            ","set enc-sub-char       _              ",                           */
    /*  "set enc-error-limit    100            ","set var-case-ci        preserve-always                                      */
    /*  ","set preserve-str-widths n             ","set preserve-num-widths n             ",                                  */
    /*  "set recs-to-optimize   all            ","set factor-as-string   n              ","set                                */
    /*  sas-date-fmt       mmddyy         ","set sas-time-fmt       time           ",                                         */
    /*  "set sas-datetime-fmt   datetime       ","set write-file-label   none           ","set write-s                        */
    /*  as-fmts     n              ","set sas-outrep         windows_64     ",                                                */
    /*  "set write-old-ver      18             ","copy  C:/temp/rdsdat.rds sas9 C:/temp/want.sas7bdat -T<want                 */
    /*  ","quit"),fileConn); close(fileConn); file.remove("c:/temp/want.sas7bdat");                                           */
    /*  system("c:/PROGRA~1/StatTransfer17-64/st.exe c:/temp/cmds.stcmd");                                                    */
    /*  [1] TRUE                                                                                                              */
    /*  [1] TRUE                                                                                                              */
    /*  >                                                                                                                     */
    /*  NOTE: 11 lines were written to file PRINT.                                                                            */
    /*  Stderr output:                                                                                                        */
    /*  Warning message:                                                                                                      */
    /*  package 'haven' was built under R version 4.1.3                                                                       */
    /*  Stat/Transfer - Command Processor (c) 1986-2024 Circle Systems, Inc.                                                  */
    /*  www.stattransfer.com                                                                                                  */
    /*  Version 17.0.1688.0331 - 64 Bit Windows (10.0.19041)                                                                  */
    /*                                                                                                                        */
    /*  Serial: HBRC-NEYA-UXDV-ELMT                                                                                           */
    /*  User: Roger DeAngelis - CompuCraft                                                                                    */
    /*  License Type: Single User Commercial Subscription                                                                     */
    /*  Status: License OK - Expires March 1, 2025                                                                            */
    /*  Transferring from R Single object: C:/temp/rdsdat.rds                                                                 */
    /*  Input file has 6 variables                                                                                            */
    /*  The input file contains string variables and although optimization is not required by the output                      */
    /*  format, S/T will enable it to make sure that the output strings will not                                              */
    /*  get truncated.                                                                                                        */
    /*  Optimizing (All records) ...                                                                                          */
    /*  Transferring to SAS Data File - Version Nine: C:/temp/want.sas7bdat                                                   */
    /*                                                                                                                        */
    /*  19 cases were transferred(0.00 seconds)                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*  _             __                  _   _
    | || |    _ __   / _|_   _ _ __   ___| |_(_) ___  _ __
    | || |_  | `__| | |_| | | | `_ \ / __| __| |/ _ \| `_ \
    |__   _| | |    |  _| |_| | | | | (__| |_| | (_) | | | |
       |_|   |_|    |_|  \__,_|_| |_|\___|\__|_|\___/|_| |_|
    */

    /* not needed because deleted in script. Used for testing */

    libname tmp "c:/temp";
    proc datasets lib=sd1 nodetails nolist;
     delete want;
    run;quit;

    %utlfkil(d:/wrk/cmds.stcmd);
    %utlfkil(d:/wrk/rdsdat.rds);

    %symdel inp outlib outdsn stcmds rds / nowarn;/* not needed */

    %utl_submit_r64x('
     library(haven);
     fn_tosas9x<-function(
       inp    =NULL
      ,outlib =NULL
      ,outdsn =NULL
      ,stcmds =NULL
      )
     {
     temp_file <- tempfile(fileext = ".rds");
     print(temp_file);
     saveRDS(inp, file = temp_file);
     fileConn<-file(stcmds);
     writeLines(c(
     "set numeric-names      n              "
    ,"set log-level          e              "
    ,"set in-encoding        system         "
    ,"set out-encoding       system         "
    ,"set enc-errors         sub            "
    ,"set enc-sub-char       _              "
    ,"set enc-error-limit    100            "
    ,"set var-case-ci        preserve-always"
    ,"set preserve-str-widths n             "
    ,"set preserve-num-widths n             "
    ,"set recs-to-optimize   all            "
    ,"set factor-as-string   n              "
    ,"set sas-date-fmt       mmddyy         "
    ,"set sas-time-fmt       time           "
    ,"set sas-datetime-fmt   datetime       "
    ,"set write-file-label   none           "
    ,"set write-sas-fmts     n              "
    ,"set sas-outrep         windows_64     "
    ,"set write-old-ver      18             "
    ,paste("copy",temp_file,"sas9",paste0(outlib,outdsn,".sas7bdat"),"-T<outdsn")
    ,"quit"),fileConn);
     close(fileConn);
     file.remove(paste0(outlib,outdsn,".sas7bdat"));
     system(paste("c:/PROGRA~1/StatTransfer17-64/st.exe",stcmds));
      };
    have<-read_sas("d:/sd1/have.sas7bdat");
    print(have);
    fn_tosas9x(
          inp    = have
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         ,stcmds ="d:/wrk/cmds.stcmd"
         );
    ');

    libname sd1 "d:/sd1";
    proc print data=sd1.want;
    run;quit;

    /*
     _ __ ___   __ _  ___ _ __ ___  ___
    | `_ ` _ \ / _` |/ __| `__/ _ \/ __|
    | | | | | | (_| | (__| | | (_) \__ \
    |_| |_| |_|\__,_|\___|_|  \___/|___/

    */

    %macro utl_submit_r64x(
          pgmx
         ,return=N
         ,resolve=N
         )/des="Semi colon separated set of R commands - drop down to R";
      %utlfkil(%sysfunc(pathname(work))/r_pgm.txt);
      /* clear clipboard */
      filename _clp clipbrd;
      data _null_;
        file _clp;
        put " ";
      run;quit;
      * write the program to a temporary file;
      filename r_pgm "%sysfunc(pathname(work))/r_pgm.txt" lrecl=32766 recfm=v;
      data _null_;
        length pgm $32756;
        file r_pgm;
        if substr(upcase("&resolve"),1,1)="Y" then do;
            pgm=resolve(&pgmx);
         end;
        else do;
            pgm=&pgmx;
         end;
         if index(pgm,"`") then pgm=tranwrd(pgm,"`","27"x);
        put pgm;
        /*putlog pgm;*/
      run;
      %let __loc=%sysfunc(pathname(r_pgm));
      * pipe file through R;
      filename rut pipe "D:\r412\R\R-4.1.2\bin\r.exe --vanilla --quiet --no-save < &__loc";
      data _null_;
        file print;
        infile rut recfm=v lrecl=32756;
        input;
        put _infile_;
        putlog _infile_;
      run;
      filename rut clear;
      filename r_pgm clear;
      * use the clipboard to create macro variable;
      %if %upcase(%substr(&return.,1,1)) ne N %then %do;
        filename clp clipbrd ;
        data _null_;
         infile clp;
         input;
         putlog "macro variable &return = " _infile_;
         call symputx("&return.",_infile_,"G");
        run;quit;
      %end;
    %mend utl_submit_r64x;

    %macro utl_rbeginx/des="utl_rbeginx uses parmcards and must end with utl_rendx macro";
    %utlfkil(c:/temp/r_pgmx);
    %utlfkil(c:/temp/r_pgm);
    filename ft15f001 "c:/temp/r_pgm";
    %mend utl_rbeginx;

    %macro utl_rendx(return=)/des="utl_rbeginx uses parmcards and must end with utl_rendx macro";
    run;quit;
    * EXECUTE R PROGRAM;
    data _null_;
      infile "c:/temp/r_pgm";
      input;
      file "c:/temp/r_pgmx";
      lyn=resolve(_infile_);
      put lyn;
    run;quit;
    options noxwait noxsync;
    filename rut pipe "D:\r414\bin\r.exe --vanilla --quiet --no-save < c:/temp/r_pgmx";
    run;quit;
    data _null_;
      file print;
      infile rut;
      input;
      put _infile_;
      putlog _infile_;
    run;quit;
    data _null_;
      infile " c:/temp/r_pgm";
      input;
      putlog _infile_;
    run;quit;
    %if "&return" ne ""  %then %do;
      filename clp clipbrd ;
      data _null_;
       infile clp;
       input;
       putlog "xxxxxx  " _infile_;
       call symputx("&return.",_infile_,"G");
      run;quit;
      %end;
    filename ft15f001 clear;
    %mend utl_rendx;


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
