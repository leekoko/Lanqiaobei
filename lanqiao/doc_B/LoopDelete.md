# 循环删除

## 1.猜字母
>把abcd...s共19个字母组成的序列重复拼接106次，得到长度为2014的串。  
>接下来删除第1个字母（即开头的字母a），以及第3个，第5个等所有奇数位置的字母。  
>得到的新串再进行删除奇数位置字母的动作。如此下去，最后只剩下一个字母，请写出该字母。  

---

题目分析：  
1. 怎么删除奇数：利用规律，当前数字的2倍就是下一个偶数项  
2. 怎么确定偶数项个数：因为删除的是奇数，所以不用考虑+1，直接/2即可  
3. 怎么确定字母：用数字表示，最后%19的值即是对应字母位数

```java
	public static void main(String[] args) {
		int[] arr=new int[2015];
		for (int i = 1; i < 2015; i++) {
			arr[i]=i;
		}
		int num=2015;
		while(num>1){
			num=num/2;   //删去奇数不用考虑+1
			for (int i = 1; i < arr.length; i++) {
				arr[i]=arr[i]*2;   //！其数的2倍就是下一个偶数项
			}
		}
		System.out.println(arr[1]%19);  //%19表示字母循环，得数17可以算出是字母q
	}
```
[源码](../SourceCode/GuessWords.java)

---


