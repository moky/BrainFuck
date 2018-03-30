# Operators

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

## add(summand, addend, sum) : Add cell #0 with #1, save the result in #2
    >>[-]>[-]<<<        // clear cell #2 and #3
    [->>+>+<<<]         // copy cell #0 to #2 and #3
    >>>[-<<<+>>>]<<<    // move cell #3 back to #0
    >[->+>+<<]<         // add cell #2 with #1
    >>>[-<<+>>]<<<      // move cell #3 back to #1

## minus(minuend, subtrahend, difference) : Minus cell #0 with #1, save the result in #2
    >>[-]>[-]<<<        // clear cell #2 and #3
    [->>+>+<<<]         // copy cell #0 to #2 and #3
    >>>[-<<<+>>>]<<<    // move cell #3 back to #0
    >[->->+<<]<         // minus cell #2 with #1
    >>>[-<<+>>]<<<      // move cell #3 back to #1

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

## devide(dividend, divisor, quotient, remainder) : Devide cell #0 with #1, save quotient in #2 and remainder in #3







