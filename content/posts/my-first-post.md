+++
title = "Test"
date = 2015-07-23
categories = ["Example"]
tags = ["Markdown"]
+++
## dsfsd
史蒂夫
士大夫
撒旦咖啡师
> esf
- sdf
```python
print("asd")
```

```rust
fn main(){
println!("hello")
}
```
```c
int main(){
printf("asd");
}
```
```java
public class HelloWorld { 
public static void main(String[] args) { 
System.out.println("Hello World!");
} 
}
```
```java
class Solution {
    public int t1(int[][] costs, int a, int b) { // 添加参数 a 和 b
        Arrays.sort(costs, (x, y) -> {
            return Math.abs(y[0] - y[1]) - Math.abs(x[0] - x[1]); // 绝对差值降序
        });
        int total = 0;
        int countA = 0; // 已送城市 A 的人数
        int countB = 0; // 已送城市 B 的人数
        for (int[] co : costs) {
            if (countA == a) { // 城市 A 已满，必须送 B
                total += co[1];
                countB++;
            } else if (countB == b) { // 城市 B 已满，必须送 A
                total += co[0];
                countA++;
            } else {
                if (co[0] <= co[1]) { // 送 A 更便宜或相等
                    total += co[0];
                    countA++;
                } else { // 送 B 更便宜
                    total += co[1];
                    countB++;
                }
            }
        }
        return total;
        
    }
    public int t2(int[][] costs, int a, int b) {
    Arrays.sort(costs, new Comparator<int[]>() { @Override public int compare(int[] o1, int[] o2) { return o1[0] - o1[1] - (o2[0] - o2[1]); } }); 
    int total = 0; int n = costs.length;  
    for (int i = 0; i < a; ++i) 
    total += costs[i][0] ; 
    for(int i = a;i<n;++i){
    total+=costs[i][1];
    }
    return total;
    }
    public static void main(String[] argvs){
    int[][] cos = new int[][]{}
    }
}
```