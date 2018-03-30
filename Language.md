# Operators

## Clear cell

    [-]     // use loop to clear the current cell

## Move cell to next

    >[-]<   // clear next cell first
    [->+<]  // use loop to move current cell to next

## Copy cell to next

    >[-]>[-]<<      // clear cell #1 and #2
    [->+>+<<]       // use loop to copy cell #0 to #1 and #2
    >>[-<<+>>]<<    // use loop to move cell #2 to #0
