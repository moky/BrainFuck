# Advance functions
    1. px means the pointer value after executing this line
    2. #x means the order x of the cell

## compare(x, y, ret): compare #0 and #1

`#2 = 0` if #0 equals #1;

`#2 = 1` if #0 larger than #1;

`#2 = -1 = 255` if #0 smaller than #1;

```
########################### perpare compare ###########################
[-]>[-]>[-]>[-]>[-]>[-]>[-]<<<<<<   // clear #0~#6

++++++++                           // p0; #0
>
+++++++++                          // p1; #1
<[->>+>+<<<]>>>[-<<<+>>>]          // p3; #2 = #0
<<[->>+>+>+<<<<]>>>[-<<<+>>>]      // p4; #5 = #3 = #1
+                                  // p4; #4 flag
                                   // p4; #5 = #3 = #1
                                   // p4; #6; buffer
<<                                 // p2

// p2
[
->-                                // p3; sub #2 and #3
>-                                 // p4; clear the flag
<[>+<[-]]                          // p3; #3 not 0; then set the flag and clear #3 to break the loop; else continue 
[-]>>-[->+<<<+>>]>[-<+>]           // p6; copy #5 sub 1 to #3
<<<<                               // p2
]
########################### perpare compare ###########################

// if flag is set; then #0 smaller than #1; else #0 lager equals #1
// and if #3 equals 0; then #0 equals #2
>>                                 // p4
-[                                 // p4; if flag is not set;
<[<+>>[-]]<<+>>                    // p4; then if #3 not 0; then #2 = 2; else #2 = 1;
]
<<-                                // p2; #2 sub 1
<<                                 // p0;

// clear #3~6
>>>[-]>[-]>[-]>[-]<<<<<<
```

## min(x, y. min{x,y}): put the min value from #0 and #1 to #2

```
perpare_compare(#0, #1, #2, #3, #4, #5, #6);

// if flag is set; then #0 smaller than #1; else #0 lager equals #1
>[-]+>                                   // p4; set #3 = 1
[<-<<<[->>+>+<<<]>>>[-<<<+>>>]>[-]]      // p4; if flag is set; set #3 = 0; copy #0 to #2;
<[-<<[->+>+<<]>>[-<<+>>]]                // p3; if #3 = 1; copy #1 to #2
<<< // p0

// clear #3~6
>>>[-]>[-]>[-]>[-]<<<<<<
```


## max(x, y. max{x,y}): put the max value from #0 and #1 to #2

```
perpare_compare(#0, #1, #2, #3, #4, #5, #6);

// if flag is set; then #0 smaller than #1; else #0 lager equals #1
>[-]+>                                   // p4; set #3 = 1
[<-<<[->+>+<<]>>[-<<+>>]>[-]]            // p4; if flag is set; set #3 = 0; copy #1 to #2;
<[-<<<[->>+>+<<<]>>>[-<<<+>>>]]          // p3; if #3 = 1; copy #0 to #2
<<<                                      // p0

// clear #3~6
>>>[-]>[-]>[-]>[-]<<<<<<
```
