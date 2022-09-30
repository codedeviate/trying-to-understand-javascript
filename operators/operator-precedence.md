# Operator precedence

The other day I ran into a strange bug. I converted some SQL WHERE statements into javascript and on occasion I got a faulty value.

It all turned out to be a difference in how mathematical expressions are executed between SQL and javascript. (It also turned out to be the same in PHP as it was in javascript.)

I had the following expression 
```mysql
SELECT * FROM DataTable WHERE (binField & 4 != 0);
```
and I wanted to convert the WHERE statement into javascript.

So I more or less took the WHERE statement and used it.
```javscript
const stmt = (binField & 4 != 0);
```
When I did a couple of test runs i produced the equivalent of the following results

| Value of binField | Javascript | MySQL |
|-------------------|------------|-------|
| 2                 | 0          | 0     |
| 4                 | 0          | 1     |
| 7                 | 0          | 0     |
| 15                | 0          | 1     |

This I found rather strange since I expected the results to be either true or false and not 0 or 1.

To not make it all to long I rather quickly found that != has higher precedence than & in javascript but not in MySQL. 

I also tested this in SQLite, PostgresSQL with the same results.

Here you can find more on javscripts [Operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)