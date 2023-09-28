##  Problem Statement
Given a `6 x 6` 2D Array, *arr*:
```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```

An hourglass in ***A*** is a subset of values with indices falling in this pattern in *arr*'s graphical representation:
```
a b c
  d
e f g
```
There are `16` hourglasses in *arr*. An hourglass sum is the sum of an hourglass' values. Calculate the hourglass sum for every hourglass in *arr*, then print the maximum hourglass sum. The array will always be `6 x 6`.

**Example**
*arr* `=`
```
-9 -9 -9  1 1 1 
 0 -9  0  4 3 2
-9 -9 -9  1 2 3
 0  0  8  6 6 0
 0  0  0 -2 0 0
 0  0  1  2 4 0
```
The `16` hourglass sums are:

```
-63, -34, -9, 12, 
-10,   0, 28, 23, 
-27, -11, -2, 10, 
  9,  17, 25, 18
```
The highest hourglass sum is `28` from the hourglass beginning at row `1`, column `2`:

```
0 4 3
  1
8 6 6
```
**Note**: If you have already solved the Java domain's Java 2D Array challenge, you may wish to skip this challenge.

***Function Description***

Complete the function hourglassSum in the editor below.

hourglassSum has the following parameter(s):

*   int arr[6][6]: an array of integers
  
***Returns***

*   int: the maximum hourglass sum

***Input Format***

Each of the `6` lines of inputs `arr[i]` contains `6` space-separated integers `arr[i][j]`.

***Constraints***

*   `-9 <= arr[i][j] <= 9`
*   `0 <= i,j <= 5`

***Output Format***

Print the largest (maximum) hourglass sum found in *arr*.

**Sample Input**

```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 2 4 4 0
0 0 0 2 0 0
0 0 1 2 4 0
```

**Sample Output**

```
19
```


**Explanation**

 *arr* contains the following hourglasses:

![alt text](https://s3.amazonaws.com/hr-assets/0/1534256743-35b846ad4a-hourglasssum.png "contains")

The hourglass with the maximum sum (`19`) is:

```
2 4 4
  2
1 2 4
```


##  Solution

```typescript
'use strict';

import { WriteStream, createWriteStream } from "fs";
process.stdin.resume();
process.stdin.setEncoding('utf-8');

let inputString: string = '';
let inputLines: string[] = [];
let currentLine: number = 0;

process.stdin.on('data', function(inputStdin: string): void {
    inputString += inputStdin;
});

process.stdin.on('end', function(): void {
    inputLines = inputString.split('\n');
    inputString = '';

    main();
});

function readLine(): string {
    return inputLines[currentLine++];
}

/*
 * Complete the 'hourglassSum' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts 2D_INTEGER_ARRAY arr as parameter.
 */

function hourglassSum(arr: number[][]): number {
    // Write your code here
    let allHourglass: number[] = [];
    for(let a: number = 0; a <=3 ; a++){
        for(let b: number = 0;b <= 3;b++){
            allHourglass.push([arr[a][b],arr[a][b+1],arr[a][b+2],arr[a+1][b+1],arr[a+2][b],arr[a+2][b+1],arr[a+2][b+2]].reduce((c,d)=> c + d,0))
        }
    }
    return Math.max(...allHourglass)
}

function main() {
    const ws: WriteStream = createWriteStream(process.env['OUTPUT_PATH']);

    let arr: number[][] = Array(6);

    for (let i: number = 0; i < 6; i++) {
        arr[i] = readLine().replace(/\s+$/g, '').split(' ').map(arrTemp => parseInt(arrTemp, 10));
    }

    const result: number = hourglassSum(arr);

    ws.write(result + '\n');

    ws.end();
}

```