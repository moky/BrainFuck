# Basic functions

## clean(current) : Clear current cell
    [-]     // use loop to clear the current cell

## one(current) : Set current cell to 1
    [-]+    // clean first and then set it to 1

## forward(current) : Move cell forward
    >[-]<   // clear next cell first
    [->+<]  // use loop to move current cell to next

## backward(current) : Move cell backward
    <[-]>   // clear previous cell first
    [-<+>]  // use loop to move current cell to previous

## copy(source, target) : Copy cell to next
    >[-]>[-]<<      // clear cell #1 and #2
    [->+>+<<]       // use loop to copy cell #0 to #1 and #2
    >>[-<<+>>]<<    // use loop to move cell #2 to #0

## swap(left, right) : Swap two cells #0 and #1
    >
        >[-]<       // clear cell #2
        [->+<]      // move cell #1 to next
    <
    [->+<]          // move cell #0 to next
    >>[-<<+>>]<<    // move cell #2 to #0

# Math functions

## add(summand, addend, sum) : Add cell #0 with #1, save the result in #2
    >>[-]>[-]<<<        // clear cell #2 and #3
    [->>+>+<<<]         // copy cell #0 to #2 and #3
    >
        >>[-<<<+>>>]<<  // move cell #3 back to #0
        [->+>+<<]       // add cell #1 to #2
        >>[-<<+>>]<<    // move cell #3 back to #1
    <

## minus(minuend, subtrahend, difference) : Minus cell #0 with #1, save the result in #2
    >>[-]>[-]<<<        // clear cell #2 and #3
    [->>+>+<<<]         // copy cell #0 to #2 and #3
    >
        >>[-<<<+>>>]<<  // move cell #3 back to #0
        [->->+<<]       // minus cell #2 by #1
        >>[-<<+>>]<<    // move cell #3 back to #1
    <

## multiply(multiplicand, multiplier, product) : Multiply cell #0 with #1, save the result in #2
    >>[-]>[-]>[-]<<<<       // clear cell #2 and #3 and #4
    [
        ->
        [->+>+<<]           // add cell #1 to #2
        >>
            [-<<+>>]        // move cell #3 back to #1
            >+<             // copy cell #0 to #4
        <<
        <
    ]
    >>>>[-<<<<+>>>>]<<<<    // move cell #4 back to #0

## divide(numerator, denominator, quotient, remainder) : Divide cell #0 with #1, save quotient in #2 and remainder in #3
    >>[-]>[-]>[-]>[-]>[-]<<<<<< // clear cells #2~6
    [->>+>+<<<]                 // copy cell #0 to #2 and #3
    >>[-<<+>>]<<                // move cell #2 back to #0
    >
        >>[                     // check #3: remainder
            <<[->>>+>+<<<<]>>   // copy cell #1 to #4 #5
            >[-<<<+>>>]<        // move cell #4 back to #1
            >>[-                // decrease #5: divisor
                <<
                [-              // decrease #3: remainder
                    [->+<]      // move cell #3 to #4
                    >>
                    >>[-]<<     // clear cell #7
                    [->+>+<<]   // move cell #5 to #6 and #7
                    <<
                ]
                >
                [-<+>]          // move cell #4 back to #3
                >>
                [-<+>]          // move cell #6 back to #5
                <
            ]<<
            <+>                 // increase #2: quotient
        ]<<
        >>>>>>[<<<<<<           // check #7
            [->>+>+<<<]         // copy cell #1 to #3 and #4
            >>>
            [-<<<+>>>]          // move cell #4 back to #1
            >>>[-<<<<->>>>]<<<  // minus cell #3 with #7
            <<-<
        >>>>>>]<<<<<<
    <

## pow(x, n) : Multiply x(#0) for n(#1) times, save the result in #2
    >>[-]>[-]>[-]<<<<    // clear cells #2~5
    [->>+>>+<<<<]        // copy cell #0 to #2 #4
    >>[-<<+>>]<<         // move cell #2 back to #0
    >
        >>+<<            // set cell #3 to 1
        [                // use loop to do the math
            ->+>         // move cell #1 to #2
                multiply(#3, #4, #5)    // do the multiply from cell #3 and #4
                [-]                     // clear cell #3
                >>[-<<+>>]<<            // move cell #5(the result) back to #3
            <<
        ]                // calculate done! the result is saved in cell #3
        >
            backward(#2) // move cell #2 backward
            >
            backward(#3) // move cell #3 backward
            >[-]<        // clear cell #4
            <
        <
    <

## mod(dividend, divisor, remainder) : Divide cell #0 with #1, save remainder(mod) in #2
    divide(dividend, divisor, *quotient, *remainder)
    >>>
    backward(*remainder)
    <<<

## ceil(dividend, divisor, quotient) : Divide cell #0 with #1, save the ceil in #2
    >>[-]>[-]>[-]>[-]>[-]<<<<<< // clear cells #2~6
    [->>+>+<<<]                 // copy cell #0 to #2 and #3
    >>[-<<+>>]<<                // move cell #2 back to #0
    >
        >>[                     // check #3: remainder
            <<[->>>+>+<<<<]>>   // copy cell #1 to #4 #5
            >[-<<<+>>>]<        // move cell #4 back to #1
            >>[-                // decrease #5: divisor
                <<
                [-              // decrease #3: remainder
                    [->+<]      // move cell #3 to #4
                    >>[->+<]<<  // move cell #5 to #6
                ]
                >
                [-<+>]          // move cell #4 back to #3
                >>
                [-<+>]          // move cell #6 back to #5
                <
            ]<<
            <+>                 // increase #2: quotient
        ]<<
    <

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
