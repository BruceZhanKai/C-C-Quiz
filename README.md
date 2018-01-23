# C/C++ Programming Quiz 

## C

### const int* p 和 int* const q 兩者差異
`p為指標變數，其指向的記憶體位置的數值無法被更動(宣告為const)。`
`q為常數，宣告為指標變數後，代表q的記憶體無法被更動，無法再指向其他記憶體位置。`

### char s[] 與 char* s 的差別 ex:"Hello World"
`char s[] 是 char arry ，包含 12 byte(含'\0')`
`char* s 是指標指向char，s指向char的起始記憶體位置`

### 指標操作*p++
`Quiz: predict the output`
```
char s[]="0113256";
char* p=s;
printf("%c",*p++);
printf("%c",*(p++));
printf("%c",(*p)++);
printf("%c",*++p);
printf("%c",*(++p));
printf("%c",++*p);
printf("%c",++(*p));
printf("\n");
printf(s);
```

`Ans:`
```
0113234
0123456
```
`Hint:`
|*p++=*(p++)|get->next|
|*++p=*(++p)|next->get|
|++*p=++(*p)|+1->get|
|(*p)++|get->+1|

## C++

### overriding
`Quiz: predict the output`
```
class Base
{
public:
	virtual void run(){cout<<"Base\n";}
};
class Derived : public Base
{
	override void run(){cout<<"Derived\n";}
};
void main(void)
{
	Base* bp = new Derived;
	bp->run();
	Base& br = *bp;
	br.run();
}
```
`Ans: Compile Error`
`Cuz: override寫法錯誤`
`fix: void run override(){cout<<"Devired\n";}`
`Ans after fix:`
```
Derived
Derived
```

### this指針
`Quiz: predict the output`
```
class A
{
private:
	int x;
public:
	A(int x){this->x=x;}
	void set(A* t){this=t;}
	void run(){cout<<"x="<<x<<endl;}
};
void main()
{
	A a1(5);
	A* a2 = new A(10);
	a1.set(a2);
	a1.run();
}
```
`Ans: Compile Error`
`Cuz: it's not a right way to use this in set()`
`Hint: rule of three`
` using operator like that`
```
A& operator=(const A*& t)
{
	if(this!=t) this->x=t->x;
	return *this;
}
```

## Algorithm







## Linked List



## LeetCode

### Reverse Integer

`Quiz: Reverse digits of an integer.`
`Example1: x = 123, return 321`
`Example2: x = -123, return -321`

`Ans:`
```
int Reverse(int x)
{
	int ans = 0;
	int temp = x;
	for(int i=temp;i;)
	{
		i=i/10*10;
		ans=ans*10+temp-i;
		temp=temp/10;
	}
	return ans;
} 

```

### Repeated String Match
`Quiz:`
`Given two strings A and B, find the minimum number of times A has to be repeated such that B is a substring of it. If no such solution, return -1.`
`For example, with A = "abcd" and B = "cdabcdab".`
`Return 3, because by repeating A three times (“abcdabcdabcd”), B is a substring of it; and B is not a substring of A repeated two times ("abcdabcd").`
`Ans:`
```
int repeatStringMatch(string A, string B)
{
	int n = B.size()/A.size()+2;
	string t = A;
	for(int i=0;i<n;i++)
	{
		if(t.find(B)!=string::npos) return i;
		t+=A;
	}
	return -1;
}
```

### Spiral Matrix II
`Quiz:`
`Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.`
`For example,`
`Given n = 3,`
`You should return the following matrix:`
`[`
` [ 1, 2, 3 ],`
` [ 8, 9, 4 ],`
` [ 7, 6, 5 ]`
`]`

`Ans:`

```
vector<vector<int>> generateMatrix(int n)
{
	vector<vector<int>> ans;
	if(n<1)return ans;
	x.resize(n);
	for(int i=0;i<n;i++)
		x[i].resize(n);
	int N=n/2;
	int val=1;
	for(int i=0;i<N;i++)
	{
		int M=val-i-1;
		for(int col=i;col<M;col++)
			ans[i][col]=val++;
		for(int row=i;row<M;row++)
			ans[row][M]=val++;
		for(int col=M;col>i;col--)
			ans[M][col]=val++;
		for(int row=M;row>i;row--)
			ans[row][i]=val++;
	}
	if(n%2==1)ans[N][N]=val;
	return ans;
}
```





