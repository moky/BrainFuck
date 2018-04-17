# String functions

## gets(str) : Get string from stdin(with End Marker in cell #0), save the input string(starts from cell #0) and move the pointer to the end(new position the of End Marker)
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
    [-]>                // clear cell #0
    [-]+++++ +++++ +++  // set the End Marker(EOT) in the cell #1
    gets(str)
    [<]                 // back to cell #0
