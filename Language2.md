# Advance functions

## compare: compare cell#0 and cell#1
`cell#2 = 0` if cell#0 equals cell#1;

`cell#2 = 1` if cell#0 larger than cell#1;

`cell#2 = -1 = 255` if cell#0 smaller than cell#1;

```
[-]>[-]>[-]>[-]>[-]>[-]>[-]<<<<<<   // clear cell#0~6

// px means the pointer value after executing this line
++++++++                           // p0; cell#0
>
+++++++++                          // p1; cell#1
<[->>+>+<<<]>>>[-<<<+>>>]          // p3; cell#2 = #0
<<[->>+>+>+<<<<]>>>[-<<<+>>>]      // p4; cell#5 = cell#3 = cell#1
+                                  // p4; cell#4 flag
                                   // p4; cell#5 = cell#3 = cell#1
                                   // p4; cell#6; buffer
<<                                 // p2

// p2
[
->-                                // p3; sub cell#2 and cell#3
>-                                 // p4; clear the flag
<[>+<[-]]                          // p3; cell#3 not 0; then set the flag and clear cell#3 to break the loop; else continue 
[-]>>-[->+<<<+>>]>[-<+>]           // p6; copy cell#5 sub 1 to cell#3
<<<<                               // p2
]

// if flag is set; then cell#0 smaller than cell#1; else cell#0 lager equals cell#1
// and if cell#3 equals 0; then cell#0 equals cell#2
>>                                 // p4
-[                                 // p4; if flag is not set;
<[<+>>[-]]<<+>>                    // p4; then if cell#3 not 0; then cell#2 = 2; else cell#2 = 1;
]
<<-                                // p2; cell#2 sub 1
<<                                 // p0;

// clear cell#3~6
>>>[-]>[-]>[-]>[-]<<<<<<
```
