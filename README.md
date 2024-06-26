[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Base case, $n \leq 1$: $T(n) = 1$  
Recursive case: $T(n) = 3T(n/3)+n^5+1$  

By expanding the recursive case to $i$ recursive levels:  
$T(n) = 3 T(n/3^i)+3\left[n^5+(n/3)^5+(n/9)^5+\cdots\right]+3(i-1)+1$

$n/3^i \leq 1$ gives $i=\log_3 n$

By subsitution $i$ in the expanding recursive case, the sum of $(n/3^j)^5$ terms dominates. At $i=\log_3 n$, this sum is asympotically $O(n^5)$.  
Therefore, the time complexity of `mystery(n)` is $O(n^5)$.
