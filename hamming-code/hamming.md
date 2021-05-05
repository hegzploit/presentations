---
title: "Hamming Code"
subtitle: "An Error Correction Method"
author: "Yusuf Hegazy -- 2018005"
institute: "Under the Supervision of Dr. Mohammed Safi"
topic: "Error Correction"
theme: "copenhagen"
aspectratio: 169
date: May 5, 2021
lang: en-US
section-titles: false
---
## Historical Background
- It was invented by Richard Hamming
- He worked at Bell Labs in the 1940s on The Bell Model V computer 
- It was an electromechanical relay machine which produced a lot of errors
- Whenever it detected an error it stopped, and needed to be restarted manually
- He said to himself "If the machine can detect an error, why can't it locate the position of the error and correct it?"

## Error Correction
::: columns
:::: {.column width=70%}
- A simple way to get error-free data, is to send the message 3 times in a row.
::::
:::: {.column width=30%}
Example:
\
```
1 1 0 1
1 0 0 1
1 1 0 1
```
::::
:::

## Parity
- However the previous method is very ineffecient and waste a lot of potential space
- A better way to spot errors that is widely used to this dat is **Parity Checks**

## Parity: Method

### Types of Parity
1. Even Parity:

    We add a parity bit to our message which is set if the sum of the 1's are an **odd** number.

2. Odd Parity:

    We add a parity bit to our message which is set if the sum of the 1's are an **even** number.

## Parity: Example
Let's use even parity, since It's used the most.

### Message
```
1 1 0 1
```

### Message (With Parity Bit)
```
1 1 0 1 1
```

## Parity In Hardware
::: columns
:::: {.column width=60%}
XOR Gates are sometimes called parity gates since they compute the even parity of their inputs.

### i.e
the inputs and outputs will always sum to an even number

::::
:::: {.column width=40%}
![XOR Truth Table](xor.jpeg)
::::
:::
 
## Hamming Code
::: columns
:::: {.column width=70%}
- Richard Hamming thought of a clever way to use multiple parity bits on a single message.
- He arranged the parity bits in a way so that each parity bit covers certain bits of the message that is to be sent.
- This made the bit's that are covered overlap with one another.
- This will let us locate and even correct 1-bit errors very effeciently with so little space wasted.
::::
:::: {.column width=30%}
![Parity Distribution](overlap.png){ width=70% }
::::
:::

## Hamming(7,4): A Practical Example
Let's Say we have the following message:
```
D4  D3  D2  D1
1   1   0   1
```
We will start by placing the parity bits according to the relation $`2^n`$ (where n is the bit position)

at n = 0 : $2^0=$ **1**

at n = 1 : $2^1=$ **2**

at n = 2 : $2^2=$ **4**

at n = 3 : $2^3= 8$ (Out of range so we will stop at n = 2)

## Hamming(7,4): A Practical Example
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
D4  D3  D2  P3  D1  P2  P1
```

## Hamming(7,4): A Practical Example

```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   D3  D2  P3  D1  P2  P1
```

## Hamming(7,4): A Practical Example

```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1   D2  P3  D1  P2  P1
```

## Hamming(7,4): A Practical Example

```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1   0   P3  D1  P2  P1
```

## Hamming(7,4): A Practical Example
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1   0   P3  1   P2  P1
```
## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
            P3      P2  P1
```
::::
:::: column
P1 = ?\
P2 = ?\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example
![Parity Distribution](overlap.png){ width=30% }

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
D4      D2      D1      P1
```
::::
:::: column
P1 = ?\
P2 = ?\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1       0       1       P1
```
::::
:::: column
P1 = ?\
P2 = ?\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1       0       1       0
```
::::
:::: column
P1 = 0\
P2 = ?\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
D1  D2          D4  P2   
```
::::
:::: column
P1 = 0\
P2 = ?\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1           1   P2   
```
::::
:::: column
P1 = 0\
P2 = ?\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1           1   1    
```
::::
:::: column
P1 = 0\
P2 = 1\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
D4  D3  D2  P3            
```
::::
:::: column
P1 = 0\
P2 = 1\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1   0   P3            
```
::::
:::: column
P1 = 0\
P2 = 1\
P3 = ?\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1   0   0             
```
::::
:::: column
P1 = 0\
P2 = 1\
P3 = 0\
::::
:::

## Hamming(7,4): A Practical Example

::: columns
:::: column
```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   1   0   0   1   1   0 
```
::::
:::: column
P1 = 0\
P2 = 1\
P3 = 0\
::::
:::

## Hamming(7,4): A Practical Example

```
Data: 1 1 0 1
```
```
7   6   5   4   3   2   1
1   0   0   0   1   1   0 
```

## Hamming(7,4): A Practical Example

![Parity Distribution](overlap.png){ width=30% }

## Hamming(7,4): A Practical Example

::: columns
:::: column

```
Data: 1 1 0 1
```

### Hamming Code with Error Inserted
```
7   6   5   4   3   2   1
D4  D3  D2  P3  D1  P2  P1
1   0   0   0   1   1   0 
```

::::
:::: column

### Parity Groups Table
| D4 | D3 | D2 | P3 | D1 | P2 | P1 |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| X  |    | X  |    | X  |    | X  |
| X  | X  |    |    | X  | X  |    |
| X  | X  | X  | X  |    |    |    |

::::
:::

##
###
Simulation

## The End
Thanks for your attention.
