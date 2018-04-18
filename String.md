# String functions

## gets(str) : Get string from stdin(with End Marker in cell #0), save the input string(starts from cell #0) and move the pointer to the end(new position the of End Marker)
    /**
     *  INPUT:  char *buffer
     *  CODES:
     *          char *p0 = buffer;
     *          char *p1 = NEXT_TO p0;
     *          char *p2 = NEXT_TO p1;
     *          while (*p0) {
     *              *p2 = *p1 = *p0;            // move EOT forward
     *              *p0 = getch();
     *              if (*p0 NOT_EQUALS *p1) {   // the input char is not EOT
     *                  RESTORE INPUT VALUE TO *p0;
     *                  MOVE ALL POINTERS FORWARD;
     *                  *p0 = EOT;
     *                  *p1 = *p2 = 0;
     *              } else {
     *                  *p0 = *p1 = 0;
     *                  *p2 = EOT;
     *              }
     *          }
     *          *p0 = *p2;                      // EOT
     */
    
                        // 13*                              set the End Marker(EOT) in the cell #0
    
    >[-]<               // 13*  (0)                         clear cell #1
    [
        >>[-]<<         // 13*   0   (0) | 49  13*  0  (0)  clear cell #2
        [->+>+<<]       //  0*  13   13  | 49   0* 13  13   move EOT forward
        ,               // 49*  13   13  | 49  13* 13  13   get char from stdin
        [->-<]          //  0* ~36   13  | 49   0*  0  13   check difference with EOT
        >[              //  0  ~36*  13  | 49   0   0* 13   if (char <> EOT)
            [+<+>]      // 36    0*  13                         move the difference back
            >           // 36    0   13*                        (DO NOT reset the pointer for next round)
            [-<+<+>>]   // 49   13    0*                        restore the input char
        ]<              // 49   13*   0  | 49   0*  0  13   move the pointer back to cell #0(next round)
    ]
    >>[-<<+>>]<<        //               | 49  13*  0   0   move the EOT back

## getstring(str) : Get string from stdin, save the input string starts from cell #1 and retore the pointer to #0
    /**
     *  INPUT:  char *buffer
     *  CODES:
     *          char *p0 = buffer;
     *          char *p1 = NEXT_TO p0;
     *          *p0 = 0;
     *          *p1 = 13;   // EOT
     *          gets(p1);   // store the input string from cell #1
     *          KEEP the pointer pointing to p0(buffer);
     */
    
    [-]>                // clear cell #0
    [-]+++++ +++++ +++  // set the End Marker(EOT) in the cell #1
    gets(str)
    [<]                 // back to cell #0
