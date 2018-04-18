# Basic functions

## clean(current) : Clear current cell
    /**
     *  INPUT:  cell
     *  CODES:
     *          while (cell NOT 0) {
     *              decrease(cell);
     *          }
     */
    
    [-]     // use loop to clear the current cell

## one(current) : Set current cell to 1
    /**
     *  INPUT:  cell
     *  CODES:
     *          clean(cell);
     *          increase(cell);
     */
    
    [-]+    // clean first and then set it to 1

## forward(current) : Move cell forward
    /**
     *  INPUT:  cell
     *  CODES:
     *          clean(next);
     *          while (cell NOT 0) {
     *              decrease(cell);
     *              increase(next);
     *          }
     */
    
    >[-]<   // clear next cell first
    [->+<]  // use loop to move current cell to next

## backward(current) : Move cell backward
    /**
     *  INPUT:  cell
     *  CODES:
     *          clean(previous);
     *          while (cell NOT 0) {
     *              decrease(cell);
     *              increase(previous);
     *          }
     */
    
    <[-]>   // clear previous cell first
    [-<+>]  // use loop to move current cell to previous

## copy(source, target) : Copy cell to next
    /**
     *  INPUT:  source AND *target
     *  CODES:
     *          var temp;
     *          clean(*target);
     *          clean(temp);
     *
     *          while (source NOT 0) {
     *              decrease(source);
     *              increase(*target);
     *              increase(temp);
     *          }
     *
     *          while (temp NOT 0) {
     *              decrease(temp);
     *              increase(source);
     *          }
     */
    
    >[-]>[-]<<      // clear cell #1 and #2
    [->+>+<<]       // use loop to copy cell #0 to #1 and #2
    >>[-<<+>>]<<    // use loop to move cell #2 to #0
