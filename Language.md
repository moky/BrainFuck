# Operators

## *bzero(current)* : Clear cell

    [-]     // use loop to clear the current cell

## *move(current, next)* : Move cell to next

    >[-]<   // clear next cell first
    [->+<]  // use loop to move current cell to next

## *copy(current, next)* : Copy cell to next

    >[-]>[-]<<      // clear cell #1 and #2
    [->+>+<<]       // use loop to copy cell #0 to #1 and #2
    >>[-<<+>>]<<    // use loop to move cell #2 to #0

## *swap(current, next)* : Swap two cells

    >
        >[-]<       // clear cell #2
        [->+<]      // move cell #1 to next
    <
    [->+<]          // move cell #0 to next
    >>[-<<+>>]<<    // move cell #2 to #0

## *add(current, next, result)* : Add cell #0 and #1, save the result in #2

    >>[-]>[-]<<<        // clear cell #2 and #3
    [->>+>+<<<]         // copy cell #0 to #2 and #3
    >>>[-<<<+>>>]<<<    // move cell #3 back to #0
    >[->+>+<<]<         // add cell #2 with #1
    >>>[-<<+>>]<<<      // move cell #3 back to #1

## *minus(current, next, result)* : Minus cell #0 with #1, save the result in #2

    >>[-]>[-]<<<        // clear cell #2 and #3
    [->>+>+<<<]         // copy cell #0 to #2 and #3
    >>>[-<<<+>>>]<<<    // move cell #3 back to #0
    >[->->+<<]<         // minus cell #2 with #1
    >>>[-<<+>>]<<<      // move cell #3 back to #1

## *multiply(current, next, result)* : Multiply cell #0 with #1, save the result in #2

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



