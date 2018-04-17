# BrainFuck

    >	increment the data pointer (to point to the next cell to the right).
    <	decrement the data pointer (to point to the next cell to the left).
    +	increment (increase by one) the byte at the data pointer.
    -	decrement (decrease by one) the byte at the data pointer.
    .	output the byte at the data pointer.
    ,	accept one byte of input, storing its value in the byte at the data pointer.
    [	if the byte at the data pointer is zero, then instead of moving the instruction pointer forward to the next command, jump it forward to the command after the matching ] command.
    ]	if the byte at the data pointer is nonzero, then instead of moving the instruction pointer forward to the next command, jump it back to the command after the matching [ command.

## "Hello world!"

    >+++ [<++++ >-] <-
    [>>+++ [<+++ >-] < [>>+ >+ >+ [<]<-] >>- - >>++ >++++ >+++ [<]<<-]
    >>>. >--. >. >. >-. >
    >+++ [<+++ >-] <- [>>>+++ [<<+++ >>-] <++++ <<-] >+. >. >
    >+++ [<+++ >-] <
    [>>+++ [<++++ >-]< [>>+ >+ >+ >+ [<]<-] >>>>+ >- [<]<<-]
    >>>. >+++. >+. >++. >
    >+++ [<+++ >-]< [>+++ <-] >+++++. >
    >+++ [<++++ >-] <-
    [>>+++ [<++++ >-] <- [>>+ >+ >+ [<] <-] >>>- >>+++ [<] <<-]
    >>>. >+. >----. >.

## Run it

* http://fatiherikli.github.io/brainfuck-visualizer/
* http://copy.sh/brainfuck/

## Functions

| Class     | Name                 | Description                    |
|-----------|----------------------|--------------------------------|
| Basic     |                      | [Basic functions](Language.md) |
|           | clean(current)       | Clear current cell             |
|           | copy(source, target) | Copy cell to next              |
| Algorithm |                      | [Algorithm functions](Algorithm.md)            |
|           | swap(left, right)    | Swap two cells #0 and #1                       |
|           | max(a, b)            | Compare cell #0 and #1, save the maximum in #2 |
|           | min(a, b)            | Compare cell #0 and #1, save the minimum in #2 |
| Math      |                                                     | [Math functions](Math.md)                             |
|           | add(summand, addend, sum)                           | Add cell #0 with #1, save the result in #2            |
|           | minus(minuend, subtrahend, difference)              | Minus cell #0 with #1, save the result in #2          |
|           | multiply(multiplicand, multiplier, product)         | Multiply cell #0 with #1, save the result in #2       |
|           | divide(numerator, denominator, quotient, remainder) | Divide cell #0 with #1, save quot in #2 and rem in #3 | 
|           | pow(x, n)                                           | Multiply x(#0) for n(#1) times, save the result in #2 |
| String    |                      | [String functions](String.md)                     |
|           | gets(str)            | Get string from stdin(with End Marker in cell #0) |
