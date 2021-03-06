# 图形打印  

## 1.打印十字图  
>小明为某机构设计了一个十字型的徽标（并非红十字会啊），如下所示：  
>
>对方同时也需要在电脑dos窗口中以字符的形式输出该标志，并能任意控制层数。   
>
>输入格式  
>一个正整数 n (n<30) 表示要求打印图形的层数。  
>输出格式  
>对应包围层数的该标志。  
>样例输入1  
>1  
>样例输出1  
>  
>样例输入2  
>3  
>样例输出2  
>
>提示  
>请仔细观察样例，尤其要注意句点的数量和输出位置。  

---

题目分析：  
1. 初始化图像  
2. 确立一个点，通过哪个点绕一圈  
3. 确立下一个点  

```java
static char[][] arr;
static int bian;
static int mid;
public static void main(String[] args) {
	Scanner input=new Scanner(System.in);
	int num=input.nextInt();
	bian=num*4+5;   //层数和边的关系
	mid=bian/2;    //确定中间位置
	arr=new char[bian][bian];
	
	init();
	add(num);
	show();

}

private static void add(int num) {
	int x=mid-2;
	int y=mid-2;
	int index=1;
	for (int i = 0; i < num; i++) {  //一层层画
		arr[x][y]='$';
		for (int j = 0; j < 2; j++) {
			y--;
			arr[x][y]='$';
		}
		for (int j = 0; j < index*4; j++) {   //其数量跟index有关
			x++;
			arr[x][y]='$';
		}
		for (int j = 0; j < 2; j++) {
			y++;
			arr[x][y]='$';
		}
		for (int j = 0; j < 2; j++) {
			x++;
			arr[x][y]='$';
		}
		for (int j = 0; j < index*4; j++) {
			y++;
			arr[x][y]='$';
		}
		for (int j = 0; j < 2; j++) {
			x--;
			arr[x][y]='$';
		}
		for (int j = 0; j < 2; j++) {
			y++;
			arr[x][y]='$';
		}
		for (int j = 0; j < index*4; j++) {
			x--;
			arr[x][y]='$';
		}
		for (int j = 0; j < 2; j++) {
			y--;
			arr[x][y]='$';
		}
		for (int j = 0; j < 2; j++) {
			x--;
			arr[x][y]='$';
		}
		for (int j = 0; j < index*4; j++) {
			y--;
			arr[x][y]='$';
		}
		for (int j = 0; j < 2; j++) {
			x++;
			arr[x][y]='$';
		}
		index++;
		x=x-2;    //起点变化
		y=y-2;
	}
}
//构造完数组内容之后，统一打印数组的内容
public static void show() {
	for (int i = 0; i < arr.length; i++) {
		for (int j = 0; j < arr[i].length; j++) {
			System.out.print(arr[i][j]);
		}
		System.out.println();
	}
}
//初始化固定的背景
public static void init() {
	for (int i = 0; i < arr.length; i++) {
		for (int j = 0; j < arr[i].length; j++) {
			arr[i][j]='.';
		}
	}
	for (int i = 0; i < 5; i++) {
		arr[mid-2+i][mid]='$';
		arr[mid][mid-2+i]='$';
	}
}
```
要点注意：  
1. 画线的方式采用定义x，y。对x，y改变位置所得   
2. 因为长度涉及到圈数，为了方便运算，定义一个独立的index随圈数的遍历进行变化(不能直接用num ),记得用index来表示当前圈数  

[源码](../SourceCode/Graph10.java)

---

## 2.打印大X    
>小明希望用星号拼凑，打印出一个大X，他要求能够控制笔画的宽度和整个字的高度。  
>为了便于比对空格，所有的空白位置都以句点符来代替。  
>要求输入两个整数m n，表示笔的宽度，X的高度。用空格分开(0<m<n, 3<n<1000, 保证n是奇数)  
>要求输出一个大X  
>  
>例如，用户输入：  
>3 9  
>程序应该输出：  
> ![](../image/p1.png)  
>  
>再例如，用户输入：  
>4 21  
>程序应该输出  
>![](../image/p2.png)  
>  
>资源约定：  
>峰值内存消耗（含虚拟机） < 256M  
>CPU消耗  < 1000ms  

---

题目分析：  
1. 先初始化图形背景  
2. 确定一个起始点，利用高的变化打印\  
3. 同上打印/，注意起始点-1:由高度确定的起点位置  

```java
	public static void main(String[] args) {
			Scanner input=new Scanner(System.in);
			int kuan=input.nextInt();
			int height=input.nextInt();
			int width=height-1+kuan;
			
			char[][] arr=new char[height][width];
			for (int i = 0; i < arr.length; i++) {
				for (int j = 0; j < arr[i].length; j++) {
					arr[i][j]='.';
				}
			}
			
			for (int i = 0; i < arr.length; i++) {
				for (int j = 0; j < kuan; j++) {
					arr[i][j+i]='*';
				}
				for (int j = 0; j < kuan; j++) {
					arr[i][width-kuan-i+j]='*';
				}
			}
			//打印图案
			for (int i = 0; i < arr.length; i++) {
				for (int j = 0; j < arr[i].length; j++) {
					System.out.print(arr[i][j]);
				}
				System.out.println();
			}
		}
```
[源码](../SourceCode/GraphX.java)

---


