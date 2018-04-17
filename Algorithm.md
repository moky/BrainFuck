# Algorithm functions

## swap(left, right) : Swap two cells #0 and #1
    >
        >[-]<       // clear cell #2
        [->+<]      // move cell #1 to next
    <
    [->+<]          // move cell #0 to next
    >>[-<<+>>]<<    // move cell #2 to #0

## max(a, b) : compare cell #0 and #1, save the maximum in #2
    >>[-]>[-]>[-]>[-]>[-]<<<<<< // clear cell #2~6
    [->>+>+>+<<<<]              // copy cell #0 to #2 #3 #4
    >>>[-<<<+>>>]<<<            // move cell #3 back to #0
    >[->>+>>+>+<<<<<]<          // copy cell #1 to #3 #5 #6
    >>>>>>[-<<<<<+>>>>>]<<<<<<  // move cell #6 back to #1
    >>>>                        // check cells: a b a b(a b 0)
        [->                     // decrease cell #4
                [               // if cell #5 not 0
                    -[->+<]     //     decrease and move to #6
                ]
                >[-<+>]<        // move cell #6 back to #5
        <]
        >[                      // if cell #5 not equls 0
            <<<[-]>[-<+>]       //     move cell #3 to #2
            >>[-]               //     clear cell #5
        ]<
        <[-]>                   // clear cell #3
    <<<<

## min(a, b) : compare cell #0 and 1, save the minimum in #2
    >>[-]>[-]>[-]>[-]>[-]<<<<<< // clear cell #2~6
    [->>+>+>+<<<<]              // copy cell #0 to #2 #3 #4
    >>[-<<+>>]<<                // move cell #2 back to #0
    >[->+>>>+>+<<<<<]<          // copy cell #1 to #2 #5 #6
    >>>>>>[-<<<<<+>>>>>]<<<<<<  // move cell #6 back to #1
    >>>>                        // check cells: a b b a(a b 0)
        [->                     // decrease cell #4
                [               // if cell #5 not 0
                    -[->+<]     //     decrease and move to #6
                ]
                >[-<+>]<        // move cell #6 back to #5
        <]
        >[                      // if cell #5 not equls 0
            <<<[-]>[-<+>]       //     move cell #3 to #2
            >>[-]               //     clear cell #5
        ]<
        <[-]>                   // clear cell #3
    <<<<
