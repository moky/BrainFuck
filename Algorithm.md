# Algorithm functions

## swap(left, right) : Swap two cells #0 and #1
    /**
     *  INPUT:  left & right
     *  CODES:
     *          var temp;
     *          temp  = right;
     *          right = left;
     *          left  = temp;
     */
    
    >
        >[-]<       // clear cell #2
        [->+<]      // move cell #1 to next
    <
    [->+<]          // move cell #0 to next
    >>[-<<+>>]<<    // move cell #2 to #0

## max(a, b) : Compare cell #0 and #1, save the maximum in #2
    /**
     *  INPUT: cells { a b 0 0 0 0 0 }
     *  CODES:
     *      prepare cells { a b 0 0 0 0 0 } to { a b a b a b 0 }
     *      compare cells #4 and #5 { a b a b(a b)0 }
     *      if cell #5 not 0(means #4 smaller than #5) {
     *          use cell #3 to cover #2
     *          erase cell #5
     *      } else {
     *          erase cell #3
     *      }
     */
    
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

## min(a, b) : Compare cell #0 and #1, save the minimum in #2
    /**
     *  INPUT: cells { a b 0 0 0 0 0 }
     *  CODES:
     *      prepare cells { a b 0 0 0 0 0 } to { a b b a a b 0 }
     *      compare cells #4 and #5 { a b b a(a b)0 }
     *      if cell #5 not 0(means #4 smaller than #5) {
     *          use cell #3 to cover #2
     *          erase cell #5
     *      } else {
     *          erase cell #3
     *      }
     */
    
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

## sort(array) : Sort the array starts from cell #1, head(#0) and tail are 0
    /**
     *  INPUT:  array & count
     *  CODES:
     *          int flag = count;
     *          for (int k; k = flag;) {
     *              flag = 0;
     *              for (int j = 1; j SMALLER THAN k; INC j) {
     *                  if (ITEM LEFT GREATER THAN ITEM j) {
     *                      swap(LEFT AND J);
     *                      flag = j;
     *                  }
     *              }
     *          }
     */
