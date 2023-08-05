# The RAM Model of Computation

## Definition
The RAM model or *Random Access Machine* model, specifies that every computer is made of statements of an instruction set, where every statement takes one unit of time.

Calculating the time needed for an algorithm is summing the number of units of time for the algorithm statements.

Subroutine calls such as loops are not one statement, but the number of statements the subroutine executes, a loop that loops  $x$  times over $c$ statements costs $cx$ units of time.

## Complexity Cases

![time complexity](https://wiki.dhruvs.space/cc9cbf65aa70f301d5a8cf9abdfb8db1/complexities.png)

### Worst-Case Complexity
The worst case complexity of an algorithm is the function defined by the maximum number of steps taken on any instance of size $n$ represented by $O(f(n))$ when thinking in terms of the [[Big O Notation]]. 

### Best-Case Complexity
The best case complexity of an algorithm is the function defined by the minimum number of steps taken on any instance of size $n$ represented by $\Omega(f(n))$  when thinking in terms of the [[Big O Notation]].

### Average-Case Complexity 
The average case complexity of an algorithm is the function defined by the average number of steps taken on any instance of size $n$ represented by $\Theta(f(n))$ when thinking in terms of the [[Big O Notation]].

## Complexity Analysis
Generally the **worst-case** complexity is the preferred measure of algorithm efficiency because it's the easiest to reason with and usually reflects the average case.

