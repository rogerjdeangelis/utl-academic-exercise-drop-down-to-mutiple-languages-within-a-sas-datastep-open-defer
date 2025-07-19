# utl-academic-exercise-drop-down-to-mutiple-languages-within-a-sas-datastep-open-defer
Academic exercise drop down to multiple languages within a sas datastep
    %let pgm=utl-academic-exercise-drop-down-to-mutiple-languages-within-a-sas-datastep-open=defer;

    %stop_submission;

    Academic exercise drop down to multiple languages within a sas datastep

    see related repose for dropping down to r inside a sas datastep.

      Correction

          Added 'if a=0;' to prevent unwanted output record
          Keintz, Mark
          mkeintz@outlook.com

    github
    https://tinyurl.com/ysey572x
    https://github.com/rogerjdeangelis/utl-academic-exercise-drop-down-to-mutiple-languages-within-a-sas-datastep-open-defer

    INPUT
    =====

    data heart;
     set sashelp.heart(obs=15 keep=age:);
    run;quit;


    /**************************************************************************************************************************/
    /*  AGECHDDIAG    AGEATSTART    AGEATDEATH                                                                                */
    /*                                                                                                                        */
    /*       .            29            55                                                                                    */
    /*       .            41            57                                                                                    */
    /*       .            57             .                                                                                    */
    /*       .            39             .                                                                                    */
    /*       .            42             .                                                                                    */
    /*       .            58             .                                                                                    */
    /*       .            36             .                                                                                    */
    /*       .            53            77                                                                                    */
    /*       .            35             .                                                                                    */
    /*       .            52            82                                                                                    */
    /*       .            39             .                                                                                    */
    /*      57            33             .                                                                                    */
    /*      55            33             .                                                                                    */
    /*      79            57             .                                                                                    */
    /*      66            44             .                                                                                    */
    /**************************************************************************************************************************/

    PROCESS
    =======

    data mis2zro;
      set heart(obs=1 in=a) heart0 open=defer;
      if a then do;
         rc=dosubl('
           proc stdize data=heart(obs=15) out=heart0 reponly missing=0;
           run;quit;
        ');
      end;
      if a=0;
      drop rc;
    run;quit;

    /**************************************************************************************************************************/
    /* AGECHDDIAG    AGEATSTART    AGEATDEATH                                                                                 */
    /*                                                                                                                        */
    /*      0            29            55                                                                                     */
    /*      0            41            57                                                                                     */
    /*      0            57             0                                                                                     */
    /*      0            39             0                                                                                     */
    /*      0            42             0                                                                                     */
    /*      0            58             0                                                                                     */
    /*      0            36             0                                                                                     */
    /*      0            53            77                                                                                     */
    /*      0            35             0                                                                                     */
    /*      0            52            82                                                                                     */
    /*      0            39             0                                                                                     */
    /*     57            33             0                                                                                     */
    /*     55            33             0                                                                                     */
    /*     79            57             0                                                                                     */
    /*     66            44             0                                                                                     */
    /**************************************************************************************************************************/



    RELATED REPOS

    https://github.com/rogerjdeangelis/utl-academic-pipes-dosubl-open-defer-and-dropping-dowm-to-multiple-languages-in-one-datastep
    https://github.com/rogerjdeangelis/utl-output-the-student-with-the-highest-grade-hash-defer-open
    https://github.com/rogerjdeangelis/utl-within-a-datastep-call-r-and-create-a-dataset-and-modify-that-dataset-with-sas-defer
    https://github.com/rogerjdeangelis/utl_using_open_defer_to_access_a_dataset_created_in_the_same_datastep
