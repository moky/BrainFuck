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
