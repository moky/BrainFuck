# Math functions

## add(summand, addend, sum) : Add cell #0 with #1, save the result in #2
    /**
     *  INPUT:  summand & addend
     *  CODES:
     *          int sum = 0;
     *          int temp = 0;
     *
     *          // 1st: copy #0 to #2
     *          while (summand) {
     *              decrease(summand);
     *              increase(sum);
     *              increase(temp);
     *          }
     *          while (temp) {
     *              decrease(temp);
     *              increase(summand);
     *          }
     *
     *          // 2nd: add #1 to #2
     *          while (addend) {
     *              decrease(addend);
     *              increase(sum);
     *              increase(temp);
     *          }
     *          while (temp) {
     *              decrease(temp);
     *              increase(addend);
     *          }
     */
    
    >>[-]>[-]<<<        // clear cell #2 and #3
    [->>+>+<<<]         // copy cell #0 to #2 and #3
    >
        >>[-<<<+>>>]<<  // move cell #3 back to #0
        [->+>+<<]       // add cell #1 to #2
        >>[-<<+>>]<<    // move cell #3 back to #1
    <

## minus(minuend, subtrahend, difference) : Minus cell #0 with #1, save the result in #2
    /**
     *  INPUT:  minuend & subtrahend
     *  CODES:
     *          int difference = 0;
     *          int temp = 0;
     *
     *          // 1st: copy #0 to #2
     *          while (minuend) {
     *              decrease(minuend);
     *              increase(difference);
     *              increase(temp);
     *          }
     *          while (temp) {
     *              decrease(temp);
     *              increase(minuend);
     *          }
     *
     *          // 2nd: minus #2 with #1
     *          while (subtrahend) {
     *              decrease(subtrahend);
     *              decrease(difference);
     *              increase(temp);
     *          }
     *          while (temp) {
     *              decrease(temp);
     *              increase(subtrahend);
     *          }
     */
    
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
