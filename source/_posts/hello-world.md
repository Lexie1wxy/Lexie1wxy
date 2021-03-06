## 第二章 C/C++快速入门

### 2.1 基本数据类型及输入输出

#### 2.1.2 变量类型及输入输出

| 类型      | 取值范围              | 占用字节      | 格式符            |
| --------- | --------------------- | ------------- | ----------------- |
| int       | 10的9次方以内整数     | 4字节（32位） | %d                |
| long long | 10的10次方~10的18次方 | 8字节（64位） | %lld              |
| float     | 6~7位有效精度         | 32字节        | %f                |
| double    | 15~16位有效精度       | 64字节        | %lf               |
| char      | -128~127              | -128~127      | %c(字符串%s不加&) |
| bool      | 0/1                   | 0/1           |                   |

#### 2.1.3 注意事项：

1. 整型

long long赋值后要加LL；

整型加unsigned表示无符号，会把法术范围挪到正数上来；

2. 浮点型

用double，放弃float；

3. char型

ASCII码——0~9（48~57)、A~Z(65~90)、a~z(97~122) 小写字母比大写大32；

输出字符串格式scanf("%s",str);

#### 2.1.4 三种实用输出格式

1. %md

   不足m位的int变量右对齐输出，高位**空格**补齐；如果本身超过m位，则保持原样

2. %0md

   不足m位的int变量右对齐输出，高位**加0**补齐；如果本身超过m位，则保持原样

3. %.mf

   浮点数保留m位小数输出

#### 2.1.5 getchar/putchar和typedef

1. gerchar()——输入单个字符（一般用来识别换行符）
2. putchar()——输出单个字符
3. typedef long long LL;——起别名

### 2.2 常用math函数

$$
fabs(double x)——取绝对值
$$

$$
pow(double r，double p)——r的p次方
$$

$$
floor(double x) /  ceil(double x)——向/下上取整
$$

$$
pow(double r，double p)——返回r^p
$$

$$
sqrt(double x)——算术平方根
$$

$$
log(double x)——取e的对数（log_ab=log_eb/log_ea）
$$

$$
sin(double x)/cos(double x)  / tan(double x) /asin(double x)  /  acos(double x)   /atan(double x) 正余弦
$$

$$
round(double x)——四舍五入
$$

### 2.3 结构体（struct）的使用

#### 2.3.1 格式

```C++
struct 类型名{

//除自己外的所有数据类型

}结构体变量名；
```

#### 2.3.2访问方法

"."（普通变量）or"->''（指针

#### 2.3.3 初始化

结构体内部可以自定义初始化函数，示例

```c++
struct studenInfo{
int id;
char gender;
studenInfo(int _id,char _gender){
id=_id;
gender=_gender;
}
//可以简化为一行
//studenInfo(int _id,char _gender):id(_id),gender(_gender){}
}stu,*p；
```

### 2.4 memset赋值

对每个元素赋相同的值（0/-1）

格式：memset（a，-1，sizeof（a））；

### 2.5 补充

#### 2.5.1 浮点数的比较

```C++
const double eps=1e-8；
#define Equ(a,b) (fabs((a)-(b))<(eps))
```

#### 2.5.2 各种复杂度

1. 时间复杂度
   $$
   O(1)<O(logn)<O(n)<O(n^2)
   $$

   $$
   ps:两个for循环的n不能超过1000，因为空间复杂度运算次数n^2不能超过10^7
   $$

   ps:两个for循环的n不能超过1000，因为空间复杂度不能超过

2. 空间复杂度

   看数组大小或者其他数据结构大小

3. 编码复杂度

   算法冗长，复杂度就大

## 第三章 入门：入门模拟

### 3.1 简单模拟

题目怎么说就·怎么做，不涉及算法

### 3.2 查找元素

给定元素，然后查找某个满足条件的元素。一般简单查找就是两个for遍历，查找算法第四章涉及

### 3.3 图形输出

1. 找规律输出

2. 定义二维数组输出

### 3.4 日期处理*

平年闰年/大月小月问题，需要细心

```C++
//判断闰年函数
bool isLeap(int year){
    return (year%4==0&&year%100!=0)||(year%400==0)//整除400或者整除4但不整除100
}
```

### 3.5 进制转换*

1. P进制转换成十进制

```C++
//公式法
int y=0,pro=1;//y为最后十进制数，pro为每次的倍数
while(x!=0){
y=y+(x%10)*pro;//获得每次x的个位数
x=x/10;//去掉x的个位数
pro=pro*P;//倍数增长
}
```

2. 十进制转换成Q进制

```c++
//除基取余法
int z[40],num=0;//z存放Q进制y的每一位，num为位数
do{
z[num++]=y%Q;
y=y/Q;
}while(y!=0)//商不为0时才循环，z数组从高位到低位为q进制数
```



### 3.6 字符串处理

#### 3.6.1 相关函数

仔细分析输入输出格式，会有一些细节和边界情况，积累经验，熟练相关函数

| gets              | ges(str)                | puts              | puts(str) |
| ----------------- | ----------------------- | ----------------- | --------- |
| strcmp(str1,str2) | 比较字符串大小（1<2(-)) | strcpy(ste1,str2) | 复制2—>1  |
| strcat(str1,str2) | str2拼接到str1后面      | strlen(str)       | 字符个数  |

#### 3.6.2 sscanf和sprintf

```c++
sscanf(str,"%d",&n);
sprintf(str,"%d",n);
//可以复杂一点，格式和scanf/printf差不多
```

## 第四章 入门：算法初步

### 4.1 排序

#### 4.1.1 选择排序

```c++
//i从[0,n-1]枚举，待排序部分[i,n-1],从小到大，选出最小
int selectSort(){
    for(int i=0,i<n,i++){
        int k=i;
        for(int j=i,j<n,j++){
            if(a[j]<a[k])
                k=j;
        }
        int temp=a[i];//交换位置
        a[i]=a[k];
        a[k]=temp;
    }
    return 0;
}
```

#### 4.1.2 冒泡排序

```C++
//相邻元素比较，从小到大，有序输出
int bubbleSort(){
    for (int i=0; i<n-1; i++){
         for (int j = 0; j < n - 1 - i; j++){
                        if (a[j] > a[j + 1]){
                            int temp=a[j];//交换位置
                            a[j]=a[j+1];
                            a[j+1]=temp;
                        }//左边数更大就换  
                } 
    }
     return 0;              
}
```

#### 4.1.3 插入排序

```C++
//将数组无序部分插入已有序部分
int insertSort(){
 for(int i=1;i<len;i++){
                int key=a[i];
                int j=i;
                while((j>=0) && (key<a[j-1])){
                        a[j]=a[j-1];//数组后移
                        j--;
                }
                a[j]=key;//插入
        }
     return 0;               
}
```

#### 4.1.4归并排序

2-路归并排序思想:------将序列不断两两分组,组内单独排序,然后不断合并.

```C++
const int maxn=100;
//将数组的[L1,R1]与[L2,R2]区间合井为有序区间(此处L2即为R1 +1)
void merge(int A[],int L1,int R1,int L2,int R2){
    int i=L1,j=L2;//i指向A[L1],j指向A[L2]
    int temp[maxn],index=0;//temp临时存放合并后的数组，index为下标    
    while(i <= R1&&j<=R2){
       if(A[i] <= A[j]) {
           temp[index++] = A[i++];//将A[i]加入序列temp
       }else{
           temp[index++] = A[j++];//将A[j]加入序列temp
       }
    }
    while(i <= R1) temp[index++] = A[i++]; //将[L1, R1]的剩余元素加人
    while(j <= R2) temp[index++] = A[j++]; //将[L2, R2]的剩余元素加入
    for(i = 0; i < index; i++) {
        A[L1+i]=temp[i];//将合并后的序列赋值回数组A
    }
}
void mergeSort(int A[],int left,int right){
    if(left<right){
        int mid=(left+right)/2;//取中点
        mergeSort(A,left,mid);//递归
        mergeSort(A,mid+1,right);//递归
        merge(A,left,mid,mid+1,right);//合并
    }
}
```

#### 4.1.5快速排序

把A[1]存入temp,让A[1]左边数都比他小,右边数都比他大的问题:

```C++
//递归实现
int Partition(int A[],int left,int right){
    int temp=A[left];
    while(left<right){
        while(left<right&&A[right]>temp) right--;
        A[left]=A[right];
        
        while(left<right&&A[left]<=temp) left++;
        A[right]=A[left];
    }
    A[left]=temp;
    return left;
}
void quickSort(int A[],int left,int right){
    if(left<right){
        int pos=Partition(A,left,right);
        quickSort(A,left,pos-1);
        quickSort(A,pos+1,right);//反复递归排序直到全部有序
    }
}
```

###

#### 4.1.4 排序题和sort函数的应用

```c++
#include<algorithm>
编写bool cmp()函数
sort(首地址，尾地址的下一个，cmp)
```

### 4.2散列

#### 4.2.1散列(hash)定义和整数散列

将元素通过一个函数转换为整数,时该整数可以尽量唯一的代表这个元素

```c++
const int maxn=10010;
bool hashTable[maxn]={false};
```

key是整数:

1.直接定址法 2.平方取中法 3. 除留余数法

冲突三种方法:

1.线性探查法 2.平方探查法 3.链地址法

####  4.2.2字符串hash初步

举例:将二维坐标P映射成整数H(P)=x*Range+y;

字符串hash是指将字符串S映射成整数 A~Z=0~25,a~z=26~51,整数52~62或者直接拼接

```C++
int hashFunc(char S[],int len){
    int id=0;
    for(int i=0;i<len;i++){
        if(S[i]<='A'&&S[i]>='Z'){
            id=id*52+(S[i]-'A');
        }else if(S[i]<='a'&&S[i]>='z'){
            id=id*52+(S[i]-'a')+26;
        }
    }
    return 0;
}
```

### 4.3递归

#### 4.3.1 分治

分解--------解决---------合并

#### 4.3.2 递归

1. 递归边界:分解的尽头
2. 递归式:将原问题分解成子问题的手段

3. 相关问题:---------全排列------n皇后问题

### 4.4贪心

--------考虑当前状态下局部最优

总的来说,贪心是用来解决一类最优化问题,并希望由局部最优解来推得全局最优解的算法思想.贪心算法适用的问题一定满足最优子结构性质,即一个问题的最优解可以由子问题的最优解有效构造出来.

### 4.5二分

#### 4.5.1二分查找

```c++
#include<stdio.h>
//a[]严格递增,一般采用非递归
int binarySearch(int a[],int left,int right,int x){
    int mid;
    while(left<=right){
        mid=(left+right)/2;
        if(a[mid]==x) return mid;
        else if(a[mid]>x){
            right=mid-1;
        }else{
            left=mid+1;
        }
    }
    return -1;//查找失败
}
int main(){
    const int n=10;
    int a[n]={1,2,3,4,5,6,7,8,9,10};
    printf("%d",binarySearch(a,0,n-1,6));
    return 0;
}
```

ps:如果二分上界超过int数据一半,可能溢出,此时用mid=left+(right-left)/2代替mid=(left+right)/2

#### 4.5.2二分法拓展

求近似平方根问题/装水问题/木棒切割问题

#### 4.5.3快速幂

快速幂又叫二分幂,基于以下事实:
$$
1.如果b是偶数,那么a^b=a*a^{b-1}
$$

$$
2.如果b是奇数,那么a^b=a^{b/2}*a^{b/2}
$$

1. 快速幂的递归写法,时间复杂度O(logb)

```C++
typedef long long LL;
//求a^b%m
LL binaryPow(LL a,LL b,LL m){
    if(b==0) 
        return 1;
    else if(b%2==1) //可以用if(b&1)代替
        return a*binaryPow(a,b-1,m)%m;
    else{
        int mul=binaryPow(a,b/2,m);
        return mul*mul%m;
    }
}
```

2. 快速幂的迭代写法(效率差异不高):

```C++
typedef long long LL;
//求a^b%m
LL binaryPow(LL a,LL b,LL m){
    LL ans=1;
    while(b>0){
        if(b&1){
            ans=ans*a%m;
        }
        a=a*a%m;
        b>>=1;
    }
    return ans;
}
```

### 4.6two points

#### 4.6.1 概念

利用问题本身和序列特性,使用两个下标i,j对序列进行扫描(同向或反向),从而以较低复杂度(一般是O(n))解决问题

```C++
//a[n]递增序列,正整数M,求a[i]+a[j]=M,two points思想示例
while(i<j){
    if(a[i]+a[j]==m){
        ptintf("%d %d\n",i,j);
        i++;
        j--;
    }else if(a[i]+a[j]<m){
        i++;
    }else{
        j--;
    }
}//序列合并问题在下一小节有递归和非递归实现
```

#### 4.6.2归并排序

2-路归并排序思想:------将序列不断两两分组,组内单独排序,然后不断合并.

```C++
const int maxn=100;
//将数组的[L1,R1]与[L2,R2]区间合井为有序区间(此处L2即为R1 +1)
void merge(int A[],int L1,int R1,int L2,int R2){
    int i=L1,j=L2;//i指向A[L1],j指向A[L2]
    int temp[maxn],index=0;//temp临时存放合并后的数组，index为下标    
    while(i <= R1&&j<=R2){
       if(A[i] <= A[j]) {
           temp[index++] = A[i++];//将A[i]加入序列temp
       }else{
           temp[index++] = A[j++];//将A[j]加入序列temp
       }
    }
    while(i <= R1) temp[index++] = A[i++]; //将[L1, R1]的剩余元素加人
    while(j <= R2) temp[index++] = A[j++]; //将[L2, R2]的剩余元素加入
    for(i = 0; i < index; i++) {
        A[L1+i]=temp[i];//将合并后的序列赋值回数组A
    }
}
void mergeSort(int A[],int left,int right){
    if(left<right){
        int mid=(left+right)/2;//取中点
        mergeSort(A,left,mid);//递归
        mergeSort(A,mid+1,right);//递归
        merge(A,left,mid,mid+1,right);//合并
    }
}
```

#### 4.6.3快速排序

把A[1]存入temp,让A[1]左边数都比他小,右边数都比他大的问题:

```C++
//递归实现
int Partition(int A[],int left,int right){
    int temp=A[left];
    while(left<right){
        while(left<right&&A[right]>temp) right--;
        A[left]=A[right];
        
        while(left<right&&A[left]<=temp) left++;
        A[right]=A[left];
    }
    A[left]=temp;
    return left;
}
void quickSort(int A[],int left,int right){
    if(left<right){
        int pos=Partition(A,left,right);
        quickSort(A,left,pos-1);
        quickSort(A,pos+1,right);//反复递归排序直到全部有序
    }
}
```

#### 4.6.4生成随机数

```C++
#include<stdio.h>//程序必备
#include<stdlib.h>//随机数必备
#include<time.h>//随机数必备
int main(){
    srand((unsigned)time(null));//main方法第一句,生成随机数种子
    for(int i=0;i<10;i++){
        printf("%d",rand());
    }
    return 0;
}
```

注意:

1. 生成的是[0,RAND_MAX]范围内整数,如果想输出[a,b]范围内,需要使用rand()%(b-a+1)+a;显然rand()%(b-a+1)的范围是[0,b-a],再加上a就是[a,b]

2. 想生成更大范围的随机数

   (int)(round(1.0*rand()/RAND_MAX*(b-a)+a)

### 4.7其他高效技巧与算法

#### 4.7.1打表

1. 在程序中一次性计算出所有需要用到的结果,之后的查询直接取这些结果;
2. 在程序B中分一次或多次计算出所有需要用到的结果,写在程序A中结果集中,然后在程序A中就可以直接使用这些结果;
3. 先暴力计算小范围数据,再找规律.

#### 4.7.2 活用递推

一种思想,细心考虑找出题目中递推关系.

#### 4.7.3随机选择算法

原理:类似于随即快速排序算法,

问题:从一个无序数组中求得第K大的数字

```C++
//递归实现
int randPartition(int A[],int left,int right){
    int temp=A[left];
    while(left<right){
        while(left<right&&A[right]>temp) right--;
        A[left]=A[right];
        
        while(left<right&&A[left]<=temp) left++;
        A[right]=A[left];
    }
    A[left]=temp;
    return left;
}
int randSelect(int a[],int left,int right,int K){
    if(left==right) return a[left];
    int p=randPartition(a,left,right);
    int M=p-left+1;//主元是a[p],第p-left+1大的数
    if(K==M) return a[p]
    else if(K<M){
        randSelect(a,left,p-1,K);//往左找
    }else{
        randSelect(a,p+1,right,K-M);//往右找
    }
}
```



## 第五章 入门：数学问题

### 5.1简单数学

掌握简单的数理逻辑,就是些水题,ccf第一题那种.

### 5.2最大公约数与最小公倍数

#### 5.2.1最大公约数

--------------------实现原理:欧几里得算法(辗转相除法)

1. 递归式:        gcd(a,b)=gcd(b,a%b)
2. 递归边界:     gcd(a,0)=a
3. 代码实现:

```C++
int gcd(int a,int b){
        if(b==0) return a;
        else return gcd(b,a%b);
}
//更简洁的写法
int gcd(int a,int b){
    return !b?a:gcd(b,a%b);
}
```

#### 5.2.2最小公倍数

1. 公式:a*b/d
2. 代码实现

```c++
int main(){
    int d=gcd(a,b);
    printf("%d",(a*b/d));
}
```

### 5.3分数的四则运算

所谓的分数的四则运算是指,给定两个分数的分子和分母,求他们加减乘除的结果

#### 5.3.1分数的表示和化简.

1. 分数的表示-------对个分数来说， 最简洁的写法就是写成假分数的形式， 即无论分子比分母大或者小，都保留其原数。因此可以使用一个结构体来存储这种只有分子和分母的分数:

   于是就可以定义Fraction 类型的变量来表示分数，或者定义数组来表示一堆分数。其中需要对这种表示制订三项规则:
          ①使down为非负数。如果分数为负，那么令分子up为负即可。
          ②如果该分数恰为0，那么规定其分子为0，分母为1。
          ③分子和分母没有除了1以外的公约数。

   ```C++
   struct Fraction{//分数
   int up, down;//分子、分母
   }
   ```

2. 分数的化简-------分数的化简主要用来使Fraction变量满足分数表示的三项规定，因此化简步骤也分为以下三步:
          ①如果分母down为负数，那么令分子up和分母down都变为相反数。
          ②如果分子up为0，那么令分母down为1.
          ③约分:求出分子绝对值与分母绝对值的最大公约数d,然后令分子分母同时除以d.
           代码如下:

   ```c++
   Fraction reduction (Fraction result){
   if(result.down < 0) {
   //分母为负数，令分子和分母都变为相反数
   result.up = -result.up;
   result.down = - result.down;
   }
   //如果分子为0,令分母为1
   if (result.up == 0) {
   result.down = 1;
   }
   //如果分子不为0，进行约分
   else {
   int d=gcd(abs (result .up), abs (result dow)); //分子分母的最大公约数
   result.up /= d;//约去最大公约数
   result.down /= d;
   return result; 
   }
   ```

   

#### 5.3.2分数的四则运算

1. 加减:

result=(f1.up\*f2.down+f1.down\*f2.up)/(f1.down*f2.down)

result=(f1.up\*f2.down-f1.down\*f2.up)/(f1.down*f2.down)

2. 乘除

result=(f1.up\*f2.up)/(f1.down*f2.down)

result=(f1.up\*f2.down)/(f1.down*f2.up)

3. ps:必须当心判断除数不为0

#### 5.3.3分数的输出

1. 分数的输出根据题目的要求进行，但是大体上有以下几个注意点: 
   ①输出分数前，先化简
   ②如果分数r的分母down为1,该分数是整数,一般来说题目会要求直接输出分子而省略分母。
   ③如果分数r的分子up的绝对值>分母down (想一想分子为什么要取绝对值? )，说明该分数是假分数，此时应按带分数的形式输出，即整数部分为r.up /r.down,分子部分为
   abs(r.up) % r.down,分母部分为r.down.
   ④以上均不满足时说明分数r是真分数，按原样输出即可。

2. 以下是一个输出示例:

   ```c++
   void showResult (Fraction r) {
   //输出分数,先分数化简
   r=reduction(r) ;
   //整数
   if(r.down==1) printf("%lld", r.up) ;
   //假分数
   else if(abs(r.up) > r.down) {
   printf("%d %d/%d", r.up / r.down, abs(r.up) %r.down, r.down) ;
   } else {
   //真分数
   printf ("%d%d", r.up,r.down) ;
   /*强调一点:由于分数的乘法和除法的过程中可能使分子或分母超过int型表示范围，因
   此一般情况下，分子和分母应当使用long long型来存储。*/
   ```

### 5.4素数

**1不是素数,也不是合数**

#### 5.4.1素数判断

如果存在被整除的数，一定有一个小于sqrt(n),一个大于sqrt(n)

```C++
bool isPrime(int n){
    if(n==1) return false;
    int sqr=(int)sqrt(n*1.0);
    for(int i=2;i<=sqr;i++){
        if(n%i==0) return false;
    }
    return ture;
}
```

#### 5.4.2素数表

```C++
//n为10的5次方以内的范围
const int maxn=101;
int Prime[maxn],pNum=0;
bool p[maxn]={0};
int Find_Prime(){
    for(int i=1;i<maxn;i++){
        if(isPrime[i]){
            Prime[pNum++]=i;
            p[i]=1;
        }
    }
}
```

#### 5.4.3埃氏筛法:

------------如果要求更大的数，则启用

```C++
//n为10的5次方以内的范围
const int maxn=101;
int Prime[maxn],pNum=0;
bool p[maxn]={0};
int Find_Prime(){
    for(int i=2;i<maxn;i++){
        if(p[i]==false){
            Prime[pNum++]=i;
            for(int j=i+i;j<maxn;j+=i){
                //筛去所有i的倍数，循环条件不能写成j<=maxn
                p[j]=1;
            }
        }
    }
}
```

### 5.5 质因子分解

------------将一个正整数分解成一个或多个质数的乘积的形式,分解步骤：

1. 创建一个结构体：

   ```c++
   struct factor{
       int x,cnt;//x_质因子，cnt_其个数
   }fac[10];//fac数组开到10就可以了，不论题目
   ```

2. 枚举1~sqrt(n)所有质因子p，判断是否是n的质因子

   ```C++
   int num=0;
   if(n%prime[i]==0){//如果是质因子
       fac[num].x=prime[i];//增加质因子
       fac[num].cnt=0;//初始化个数
       while(n%prime[i]==0){
           fac[num].cnt++;//计算个数
           n/=prime[i];
       }
       num++;//检查下一个质因子
   }
   ```

3. 上述步骤结束后仍然大于1，还有个大于sqrt(n)的质因子n

   ```C++
   if(n!=1){//无法被除尽
       fac[num].x=n;//把n放进去
       fac[num++].cnt=1;
   }
   ```

### 5.6大整数运算

-----------定义：高精度的整数，就是无法用基础数据类型存储其精度的整数

#### 5.6.1大整数的存储

1. 定义一个整数数组存储，高位存高位，低位存低位的顺序存储，为了方便获取长度，一般定义一个结构体：

```C++
struct bign{
    int len;
    int d[1000];
    bign(){
        memset(d,0,sizeof(d));
        int len=0;
    }//每次结构体变量被定义都会自动初始化
}
```

2. 但每次输入大整数一般用字符串先读入，然后再把字符串另存为bign结构体。由于char数组读入会翻转，高位存低位，低位存高位的顺序存储，即我们需要再翻转回来

```c++
bign change(char str[]){
    bign a;
    a.len=strlen(str);
    for(int i=0;i<a.len;i++){
        a.d[i]=str[a.len-i-1]-'0';//逆着赋值
    }
    return 0；
}
```

3. 如果要比较两个大整数大小的规则：1.判断len大小；2.从高到低比较数字大小。

#### 5.6.2大整数的四则运算

类似于列竖式：

```c++
//高精度加法
bign add(bign a,bign b){
    bign c;
    int carry=0;
    for(int i=0;i<a.len||i<b.len;i++){
        int temp=a.d[i]+b.d[i]+carry;
        c.d[c.len++]=temp%10;//个位为结果
        carry=temp/10；//10位为进位
    }if(carry!=0){
        c.d[c.len++]=carry;
    }
    return c
}
//注意point：这个模板针对非负整数，如果有单个负数，可以转换时去负号，用减法
//如果都是负数，取绝对值用加法，然后结果加上负数
```

```c++
//高精度减法
bign sub(bign a,bign b){
    bign c;
    int carry=0;
    for(int i=0;i<a.len||i<b.len;i++){
        if(a.d[i]<b.d[i]){//不够减
            a.d[i+1]--;//向高位借位
            a.d[i]+=10;//加10
        }
        c.d[c.len++]=a.d[i]-b.d[i];//减法结果为当前位结果
        while(c.len-1>=1&&c.d[c.len-1]==0){//去除最高位的0且至少保留一位最低位
            c.len--;
        }
    }
    return c
}
//注意point：使用sub前比较两个数的大小，如果被减数小于减数，则调换数组相减，结果加上负号
```

```c
//高精度与低精度乘法
bign multi(bign a,int b){
    bign c;
    int carry=0;
    for(int i=0;i<a.len;i++){
        int temp=a.d[i]*b+carry;
        c.d[c.len++]==temp%10;
        carry=temp/10;
    }whiel(carry!=0){
        c.d[c.len++]=carry%10;
        carry=carry/10;
    }
    return c
}
```

```c
////高精度与低精度除法
bign multi(bign a,int b，int &r){//r为余数
    bign c;
    c.len=a.len;//被除数与商位数一一对应，长度相等
    for(int i=a.len-1;i>=0;i--){
        r=r*10+a.d[i];
        if(r<b) c.d[i]=0//不够除
        else{//够除
             c.d[i]=r/b;
             r=r%b;
            }
    }
    while(c.len-1>=1&&c.d[c.len-1]==0){//去除最高位的0且至少保留一位最低位
        c.len--;
    }
    return c
}
```

### 5.7扩展欧几里得算法

暂时不学，有需要再回来

### 5.8组合数

#### 5.8.1关于n!的一个问题

$$
n!中有（n/p+n/p^2+n/p^3+...)个质因子
$$



```c
//n!中有多少个质因子p
int cal(int n,int p){
    int ans=0;
    while(n){
        ans+=n/p;
        n/=p;  
    }
    return ans;
}
```

上面这个可以推广计算**n!的末尾有多少个0（等于n!中因子10的个数）**

一个概念：

**n！中质因子p的个数，实际上等于1~n中p的倍数的个数n/p加上n/p！中质因子p的个数**

```c
//因此得出cal的递归版本
int cal(int n,int p){
   if(n<p) return 0;//n<p时，不可能再存在质因子
    else return n/p+cal(n/p,p)//返回n/p！中质因子p的个数**
}
```

#### 5.8.2组合数的计算

方法一：根据定义式计算------暴力破解，容易溢出，忽略

方法二：根据递推式计算
$$
递归公式：C_n^m=C_{n-1}^m+C_{n-1}^{m-1}
$$

$$
递归边界：C_n^0=C_n^n=1
$$

```C++
#define long long LL;
LL res[67][67]={0};
LL C(LL n,LL m){ 
    if(m==0||n==m) return 1;
    else if(res[n][m]!=0) return res[n][m];//记录已经计算过的C[n][m],防止重复计算
    else return res[n][m]=C(n-1,m)+C(n-1,m-1);//赋值并返回
}
```

方法三：定义式变形

```c
#define long long LL;
LL C(LL n,LL m){
    LL ans=1;
    for(LL i=1;i<=m;i++){
        ans=ans*(n-m+1)/i;
    }
    return ans;
}
```

#### 5.8.2 组合数%p的计算

1. 方法一：通过递推式(只要在源代码合适的地方对p取模就行)

```c
#define long long LL;
LL res[67][67]={0};
LL C(LL n,LL m){ 
    if(m==0||n==m) return 1;
    else if(res[n][m]!=0) return res[n][m];//记录已经计算过的C[n][m],防止重复计算
    else return res[n][m]=C(n-1,m)+C(n-1,m-1)%p;//赋值并返回
}
```

2. 方法二：根据定义式(原理P186，比较复杂，看书吧)

```c
//使用筛法得到素数表prime,注意表中最大素数不得小于n
int prime[maxn];
//计算C(n,m)%p
int C(int n,int m,int p){
int ans = 1;
//遍历不超过n的所有质数
for(int i = 0; prime[i] <= n;i++) {
//计算C(n,m)中prime[i]的指数c，cal (n,k)为n!中含质因子k的个数
int C = cal(n, prime[i]) - cal (m, prime[i]) -cal(n - m, prime[i]);
//快速幂计算prime[i]^c%p
ans = ans * binaryPow(prime[i], C，p)%p;
return ans;
```

3. 方法四：lucas定理（需要结合方法2使用）

```c
int lucas(int n,int m){
    if(m==0) return 1;
    else return C(n%p,m%p)*Lucas(n/p,m/p)%p;
}//原理没看，代码不长可以死记，或者看书189页

```

4. 方法数据范围

| 示例  | n       | m       | p               | 方法   |
| ----- | ------- | ------- | --------------- | ------ |
| case1 | <=10^4  | <=10^4  | <=10^9          | 方法一 |
| case2 | <=10^6  | <=10^6  | <=10^9          | 方法二 |
| case3 | <=10^18 | <=10^18 | <=10^9(p是素数) | 方法四 |

方法三太长了，以后再看，一般情况下方法一就够用了。

## 第六章 C++标准模板库STL

---------------------------------------------***（Standard Template Library）***

-----------------------------------------------#include<stdlib.h>//标准库函数

### 6.1vector

#### 6.1.1 定义

中文译名：“向量”，容易理解的叫法：“变长数组”，即“长度根据需要自动改变的数组”

```c
#include<vector>
//格式
vector<typename> name;
//基本数据类型举例
vector<int> array[arraySize];
//注意：typename是STL容器是，>>之间必须加空格，举例
vector<vector<int> > vi;
```

#### 6.1.2元素访问

1. 下标访问 

   范围0~v.size-1,比如v[0],v[1]等

2. 迭代器访问

   迭代器iterator类似于指针,通过*it来访问

```c
//格式
vector<typename>::iterator it;
//举例
vector<int>::iterator it=vi.begin();
it++;it--;
//*(it+1)等价于vi[i]
```

3. 注意：
   1. vi.begin()指向首地址，vi.end()指向尾地址下一个空地址，因为美国人习惯左闭右开
   2. 只有vector和string中，才允许vi.begin()+3这种整数加迭代器的写法

#### 6.1.3常用函数

```c
vi.push_back(x);//尾部添加元素
vi.pop_back(x);//删除尾元素
vi.size();//获得元素个数
vi.clear();//清除所有元素
vi.insert(it,x);//向it位置插入x
vi.erase(it);//删除迭代器为it位置的元素
vi.erase(first,last)//删除[first,last)范围内的所有元素
```

#### 6.1.4常见用途

1. 存储数据
2. 用邻接表存储图——10.2.2节

### 6.2set

#### 6.2.1定义

中文译名：“集合”，即“内部自动有序且不含重复元素的容器”，字面理解可知set内元素自动递增，且自动去除重复元素

```c
#include<set>
//格式
set<typename> name;
//基本数据类型举例
set<int> array[arraySize];
//注意：typename是STL容器是，>>之间必须加空格，举例
set<set<int> > st;
```

#### 6.2.2元素访问

只能用迭代器访问，不支持*（it+i）来访问，只能枚举

#### 6.2.3常用函数

```c
st.size();//获得元素个数
st.clear();//清除所有元素
st.insert(x);//插入x
st.find(x);//返回对应值为x的迭代器
//删除单个元素-------------------------------------------------
st.erase(st.find(x));//删除迭代器为it位置的元素，可以搭配find(x)
st.erase(x);//直接删除值为x的set元素
//删除多个元素-------------------------------------------------
st.erase(first,last)//删除[first,last)范围内的所有元素，可以搭配find(x)
```

#### 6.2.4常见用途

自动去重以及升序排序。

延申：set元素唯一，不唯一用multiset。另外C++ 11中·增加了unordered_set,只去重不排序。

### 6.3string

#### 6.3.1定义

```c
#include<string>//注意和string.h不一样
string str="str";
```

#### 6.3.2元素访问

1. 通过下标访问和迭代器访问都可以，而且迭代器可支持直接+i；

2. 读入与输出一般cin/cout，如果想用printf，可以str.c_str(）将string类型强制转换为字符数组。

#### 6.3.3常用函数

```c
operator +;//字符串拼接，str1+str+2
compare operator：包括==,!=,<,<=,>,>=//按字典序比较
str.size() / str.length();//字符串长度

str.insert();//插入
str.insert(pos,string);//pos位置插入string
str.insert(it,it2,it3);//[it2,it3)位置字符串插入it位置

//删除单个元素-------------------------------------------------
str.erase(it);//删除迭代器为it位置的元素
//删除多个元素-------------------------------------------------
str.erase(first,last);//删除[first,last)范围内的所有子串
str.erase(pos,length);//pos插入位，length删除长度
    
str.clear();//清除所有元素
str.substr(pos,len);//返回pos位置长度为len的字符串
str.find(str);//寻找字符串str,没找到返回string:npos;
str.find(str，pos);//寻找pos开始往后的字符串str,没找到返回string:npos;
string:npos;//常数，-1

str.replace(pos,len,str2);//把pos位置开始长度为len的字符串替换为str2
str.replace(it1,it2,str2);//把[it1，it2)的字符串替换成str2
```

### 6.4map

#### 6.2.1定义

中文译名：“映射”，即“将任何基本类型（包括STL容器）映射到任何基本类型（包括STL容器）”，map会以键值从小到大排序，键值对唯一。

```c
#include<map>
//格式
map<typename1,typename2> name;//将typename1（键key）映射到typename2（值value）
//基本数据类型举例
map<set<int>,string> mp;
```

#### 6.2.2元素访问

1. 下标：mp[key]

2. 迭代器：it->first访问key，it-second访问value

#### 6.2.3常用函数

```c
mp.find(key);//寻找键值为key的迭代器

//删除单个元素-------------------------------------------------
mp.erase(it);//删除迭代器为it位置的元素
mp.erase(key);//删除key对应的元素
//删除多个元素-------------------------------------------------
mp.erase(first,last);//删除[first,last)范围内的所有子串
    
mp.size();//获得映射对数
mp.clear();//清除所有元素
```

#### 6.2.4常见用途

1. 字符串与整数映射题目
2. 判断大整数或者其他类型数据是否存在的题目，把map当bool数组用
3. 字符串和字符串的映射
4. 延申：map元素唯一，不唯一用multimap。另外C++ 11中·增加了unordered_map,只映射不排序。

### 6.5queue

#### 6.2.1定义

先进先出，类似排队，队首指针front，队尾指针rear

#### 6.2.2元素访问

1. 队首指针front——队首元素，初始-1
2. 队尾指针rear——队尾元素，初始-1

#### 6.2.3常用函数

```C++
//先进先出，类似排队，队首指针front，队尾指针rear
#include<queue>
queue<Type> q; //其中Type为数据类型（如 int，float,char等）
q.push(item)           //q[++rear];         将item压入队列尾部  
q.pop()                //front++;           删除队首元素，但不返回  
q.front()              //q[front+1];        返回队首元素，但不删除  
q.back()               //q[rear];           返回队尾元素，但不删除  
q.size()               //return rear-front; 返回队列中元素的个数  
q.empty()              //if(front==rear){}; 检查队列是否为空，如果为空返回true，否则返回false  
```

#### 6.2.4常见用途

需要实现广度优先搜索时，不手动实现而是用queue做代替

注意：使用front()和pop()之前，必须用empty（）判断队列是否为空，否则可能因此出现错误。

### 6.6priority_queue

#### 6.4.1定义

优先队列，底层是堆，队首元素是优先级最高的那一个

#### 6.4.2元素访问

没有front()/back()函数，只能通过top()来访问队首元素

#### 6.4.3常用函数

```C++
//先进先出，类似排队，队首指针front，队尾指针rear
#include<queue>
priority_queue<Type> q; //其中Type为数据类型（如 int，float,char等）
q.push(item)           //q[++rear];         将item压入队列尾部  
q.pop()                //front++;           删除队首元素，但不返回  
q.top()              //q[front+1];        返回队首元素，但不删除  
q.size()               //return rear-front; 返回队列中元素的个数  
q.empty()              //if(front==rear){}; 检查队列是否为空，如果为空返回true，否则返回false  
```

#### 6.4.4常见用途

解决一些贪心问题（9.8节），或者对Dijkstra算法进行优化

注意：使用top()之前，必须用empty（）判断队列是否为空，否则可能因此出现错误。

#### 6.4.5元素优先级的设置

1. 基础类型

```c
//格式
priority_queue<typename,vector<typename>,less<typename> > q;
//less<typename>表示数字大的优先级大，而greater<typename>表示数字小的优先级大

//示例
priority_queue<int,vector<int>,less<int> > q;
priority_queue<double,vector<double>,less<double> > q;
```

2. 结构体类型

```c
struct fruit{
    string name;
    int price;
    friend bool operater < (fruit f1,fruit f2){
        return f1.price>f2.price;
    }
};//此时水果价格低的，优先级高
-----------------------------------------------------------
    另一种方法看书，暂时准备只记这个
```

可以推出：

如果基本数据类型或者其他STL容器，也可以通过同样的方式来定义优先级

如果结构体数据较为庞大，建议使用引用提供效率，此时要加上const和&

```c
struct fruit{
    string name;
    int price;
    friend bool operater < (const fruit &f1,const fruit &f2){
        return f1.price>f2.price;
    }
};//此时水果价格低的，优先级高
```

### 6.7stack

#### 6.7.1定义

栈，后进先出，类似盒子，栈顶指针TOP=-1

#### 6.7.2元素访问

s.top();

#### 6.7.3常用函数

```c
//后进先出，类似盒子，栈顶指针TOP=-1
#include<stack>
stack<Type> s;//其中Type为数据类型（如 int，float,char等）。
s.push(item);       //st[++TOP]=item;  将item压入栈顶  
s.pop();            //TOP--;           删除栈顶的元素，但不会返回  
s.top();            //return st[TOP];  返回栈顶的元素，但不会删除  
s.size();           //return TOP+1;    返回栈中元素的个数  
s.empty();          //if(TOP==-1){};   检查栈是否为空，为空返回true，否则返回false   
```

#### 6.7.4常见用途

模拟递归，防止栈内存溢出

### 6.8pair

#### 6.8.1定义

"对"，实用的小玩意儿，把两个元素绑定成为一个元素------类似于内部有两个元素的结构体

```c
#include<map>//可以用utility
pair<typename1,typename2> name;
```

初始化方法：

```c
1. pair<string,int> p("haha",5);
代码中想临时构建的话---------------------------------
1. pair<string,int>("haha",5);
2.make_pair("haha",5);//自带的make_pair函数
```

#### 6.8.2元素访问

```
p.first();            p.second();
```

#### 6.2.3常用函数

compare operator:

<font color="red">**==/!=/</<=/>/>=**</font>--------------------直接比较first元素，不能比较大小就second

#### 6.2.4常见用途

1. 代替二元结构体及构造函数；
2. 作为map键值对来给map插入。

### 6.9algorithm头文件下常用函数

#### 6.9.1max() / min() / abs()

```c
max(int/double x,int/double y);//返回x，y中最大值
min(int/double x,int/double y);//返回x，y中最小值
abs(int x);//返回绝对值
//fabs(double x);返回浮点数绝对值，它在math头文件下
```

#### 6.9.2swap()

```c
swap(x,y);//交换
```

#### 6.9.3reverse()

```c
reverse(it1,it2);//将数组指针在[it1,it2)的元素进行反转
```

#### 6.9.4next_permutation()

```c
next_permutation()//给出一个序列在全排列中的下一个序列
//示例
int a[10]={1,2,3};
do{
printf("%d %d %d\n",a[0],a[1],a[2]);
}while(next_permutation(a,a+3))
//memset到达全排列最后一个时会返回false，必须得用do while
```

#### 6.9.5fill()

```c
fill()//把某段区间赋值为相同的值
//示例
int a[10]={1,2,3};
fill(a,a+10,233);//a[0]~a[4]都赋值为233
```

#### 6.9.6sort()

```c
sort(首地址，尾地址的下一个地址，cmp比较函数);//默认递增排序
cmp();//cmp函数定义根据要比较的规则来写
注意：容器的比较只涉及vector，string，deque可以使用sort，因为set和map本身有序（红黑树实现）
```

#### 6.9.7lower_bound() /  upper_bound()

````c
lower_bound(first,last,val);//范围内大于等于val的第一个值的坐标（指针或者迭代器）
upper_bound(first,last,val);//范围内大于val的第一个值的坐标（指针或者迭代器）
````

## 第七章 提高：数据结构专题（1）

### 7.1栈stack

1. 数组实现栈时，TOP指针int型     2. 链表实现栈时，TOP指针int*型；
2. TOP指针始终指向栈最上方一个元素

```C++
//后进先出，类似盒子，栈顶指针TOP=-1
#include<stack>
stack<Type> s;//其中Type为数据类型（如 int，float,char等）。
s.clear();          //return TOP=-1；  清空栈——注意！STL中没有实现栈的清空，需要自己写
s.push(item);       //st[++TOP]=item;  将item压入栈顶  
s.pop();            //TOP--;           删除栈顶的元素，但不会返回  
s.top();            //return st[TOP];  返回栈顶的元素，但不会删除  
s.size();           //return TOP+1;    返回栈中元素的个数  
s.empty();          //if(TOP==-1){};   检查栈是否为空，为空返回true，否则返回false   
```

### 7.2队列queue

1. 队首指针front——队首元素前一个位置，初始-1
2. 队尾指针rear——队尾元素，初始-1

```C++
//先进先出，类似排队，队首指针front，队尾指针rear
#include<queue>
queue<Type> q; //其中Type为数据类型（如 int，float,char等）
q.clear();             //front=clear=-1;    清空栈——注意！STL中没有实现栈的清空，需要自己写
q.push(item)           //q[++rear];         将item压入队列尾部  
q.pop()                //front++;           删除队首元素，但不返回  
q.front()              //q[front+1];        返回队首元素，但不删除  
q.back()               //q[rear];           返回队尾元素，但不删除  
q.size()               //return rear-front; 返回队列中元素的个数  
q.empty()              //if(front==rear){}; 检查队列是否为空，如果为空返回true，否则返回false  
```

### 7.3链表

#### 7.3.1链表概念

- 不连续的由若干个结点连接成的表，每个结点代表一个元素，由数据域和指针域组成

- 分为有头结点和无头结点，我们一般创建的时有头结点的

- 头结点的数据域为空，指向的第一个结点保存第一个data

<img src="/../images/%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0/image-20200629032529825.png" alt="image-20200629032529825" style="zoom: 25%;" />

```c
struct node{
    typename data;//数据域
    node* next;//指针域
};//定义结点
```

#### 7.3.2为链表node分配内存空间

1.new运算符（推荐）

```c
//格式
typename* p=new typename;
//举例
node* p=new node;
//定义后要释放内存，否则可能造成内存泄漏
delete(p);
```

2.malloc函数

```c
//格式
typename* p=(typename*)malloc(sizeof(typename));
//举例
node * p=(node*)malloc(sizeof(node));
//定义后要释放内存，否则可能造成内存泄漏
free(p);
```

#### 7.3.3链表基本操作

1. 创建链表

```c
#include<stdio.h>//标准输入输出
#include<stdlib.h>//标准库函数
struct node{
    int data;
    node* next;
};
//创建链表
node* create(int a[]){
    node *p,*pre,*head;//p---临时结点，pre----临时结点的前置结点
    head=new node;
    head->next=null;
    pre=head;//把前置结点设置为头结点
    for(int i=0;i<5;i++){
        p=new node;
        p->data=a[i];
        p->next=null;
        pre->next=p;//前驱节点的指针域指向p
        pre=p;
    }
    return head;//返回创建完成的头结点
}
int main(){
    int a[5]={1,2,3,4,5}
    node* L=create(a);
    L=L->next;//第一个结点才有数据
    while(L!=null){//指针不指向空地址
        printf("%d",L->data);
        L=L->next;
    }
    return 0;
}
```

2. 查找元素

```c
从头结点开始遍历查找就行，代码很简单
```

3. 插入元素

```c
void insert(node *head,int pos,int x){//把x插入以head为头结点的链表的第pos位置上
    node *p=head;
    for(int i=0;i<pos-1;i++){//只到pos的前一个停下
        p=p->next;
    }
    node *q=new node;//新建插入结点
    q->data=x;//数据x
    q->next=p->next;//新结点指向插入前原先pos位置的结点
    p->next=q;//前一个位置的结点指向新结点
}
```

4. 删除元素

```c
void del(node *head,int x){
    node *p=head->next;
    node *pre=head;
    while(p!=null){
      if(p->data==x){
        pre->next=p->next;
        delete(p);
        p=pre->next;
      }else{
        pre=p;
        p=p->next;
      }
    }
}
```

#### 7.3.4静态链表

实现原理是hash，不需要头结点，其他和动态链表差不多

```c
/* 线性表的静态链表存储结构 */
struct Node
{
    typename data;//数据域
    int cur; //游标，指向下一个数组下标，类似于指针域
}node[size]
//要用到的时候再看细节
```

## 第八章 提高：搜索专题

### 8.1深度优先搜索DFS

#### 8.1.1DFS概念、思路及实现方法

1. 全称：“Depth First Search”

2. 概念：是一种枚举所有路径以遍历所有情况的搜索方法。

3. 思路：类似于走迷宫时，一条路一直往前走，走到死胡同折返到前一个岔路口选另一个结点继续往下走，如此往复知道走出迷宫；
4. 实现方法：递归（在递归时系统调用系统栈存放递归每层的状态，所以本质是用栈实现。）

#### 8.1.2代码格式及举例

1. 举例题目：

   有n件物品，每件物品重量w[i],价值c[i],选若干个物品放入容量为V的背包，求价值最高的组合,0<n<=30

2. 代码示例

#### 8.1.3相关问题及注意Point

1. 相关问题：**和迷宫三个关键点（岔路口---选择，死胡同---掉头边界，出口---最终解决方案）**

   比如：给定一个序列，枚举这个序列的所有子序列（可以不连续），这个问题也等价于枚举从N个整数中选择K个数的所有方案。

2. 注意：假设每个岔路口（选择点）都可以被选择多次的话，只要根据题目更改代码中选择index号岔路口的部分就行了

### 8.2广度优先搜索BFS

#### 8.2.1BFS概念、思路及实现方法

1. 全称：“Breadth First Search”

2. 概念：是一种按层次顺序以遍历所有情况的搜索方法。

3. 思路：类似于迷宫时，一条路走到一个岔路口，就把这个岔路口的下一个节点都标记一下，然后再从下一层结点依次这么做，只到找到出口位置。像是石子投入水面，水纹以同心圆方式扩散开来。
4. 实现方法：队列，先进后出

#### 8.2.2代码格式及举例

1. 代码模板：

```c
void BFS(int s){
    queue<int> q;
    q.push(s);
    while(!q.empty()){
        //取出队首元素top；
        //访问队首元素；
       // 队首元素出队；
       // top下一层结点全部入队；
    }
}
```

2. 举例题目：

给出一个矩阵，矩阵元素0/1，称位置（x，y）与其上下左右四个位置是相邻的，若矩阵有若干个相邻的1，称这些1构成了一个块，求这个矩阵有几个块？

3. 代码示例

```c
const int maxn=100;
int X[4]={0,0,1,-1};//增量数组
int Y[4]={1,-1,0,0};//竖着看，表示上下左右四个方向
int n,m;
int matrix[maxn][maxn];
bool inq[maxn][maxn]={0};
bool judge(int x,int y){
    //判断（x，y）是否需要访问
}
void BFS(int x,int y){
    queue<node> q;
    Node.x=x,Node.y=y;
    q.push(Node);
    inq[x][y]=true;
    while(!q.empty){
        node top=q.front();//取出队首元素
        q.pop();
        for(int i=0;i<4;i++){//得到4个相邻位置
            int newx=topx+X[i];
            int newy=topy+Y[i];
            if(judge(newx,newy)){//如果新位置需要访问
                Node.x=newx,Node.y=newy;
                q.push(Node);
                inq[newx][newy]=1;//新结点入队
            }
        }
    }
}
int main(){
    //读入矩阵
    //枚举位置
    int ans=0;//存放块数
    for(0~n-1)
        for(0~m-1){
            //如果元素为且未入过队
            if(matrix[x][y]==1&&inq[x][y]==0){
                ans++;//块数加一
                BFS(x,y);//访问整个块，该块所有q都标记inq
            }
        }
    //.......
    return 0;
}
```

#### 8.2.3相关问题及注意point

1. 相关问题：求最少步数，最小路径，最低耗费时间等等

2. 注意：队列实现时，要注意元素入队的push操作时创建了一个元素二点副本入队，因此对这个元素的修改不会影响本元素，如果题目要求改本身元素时，我们可以换个思路：即，把元素所在的数组下标入队，而不是元素本身。

## 第九章 提高： 数据结构专题 (2)

### 9.1树与二叉树

#### 9.1.1 树的定义与性质

1. 关键名词

| 树（tree） | 结点（node）    | 叶子结点（leaf） | 根结点（noot）     |
| ---------- | --------------- | ---------------- | ------------------ |
| 边（edge） | 子结点（child） | 子树（subtree）  | 空树（empty tree） |

| 树的层次（layer）  | 从根结点为第一层开始算，向下逐层加一，以此类推 |
| ------------------ | ---------------------------------------------- |
| 结点的度（degree） | 结点的子树棵数                                 |
| 结点深度（depth）  | 从根节点（深度为1）自顶向下逐层累加            |
| 结点高度（height） | 从最底层叶节点（高度为一）自底向上逐层累加     |
| 森林（forest）     | 若干棵树集合                                   |

2. 经常用来作为边界数据的性质：
   - 树可以没有结点，此时是空树(empty tree)
   - 叶子节点度为0，当树中只有一个结点，root=leaf

#### 9.1.2二叉树的递归定义

1. 要么二叉树没有根节点，是空树
2. 要么二叉树由root，左子树、右子树组成，且左子树和右子树都是二叉树
3. 特殊二叉树：
   - 满二叉树：每层结点个数都达到了当层最大结点数
   - 完全二叉树：只有最底层没达到当层最大结点数,且最底层从左至右连续存在若干结点
4. 几个树的概念

孩子节点、父亲结点、兄弟结点

祖先结点(包括父亲结点和自己)、子孙结点(包括孩子结点和自己）

#### 9.1.3二叉树的存储结构与基本操作

1. 二叉树的存储结构：

```c
//二叉链表
struct node{
    int data;      //数据域
    node* lchild;  //指向左子树
    node* rchild;  //指向右子树
};
//建树前一般根结点不存在，所以地址设为null；
node* root=null;
```

二叉树的常用操作有几个，建立/查找/修改/插入/删除——其中删除对不同的二叉树差别比较大，这里就不介绍了；

2. 新建结点

```c
node* newNode(int v){
    node* Node=new node;
    Node->data=v;
    Node->lchild=Node->rchild=null;
    return Node;
}
```

3. 查找并修改结点

```c
//递归实现
void search(node* root,int x,int newdata){
    if(root==null){
        return;//死胡同，空树
    }
    if(root->data==x){
        root->data==newdata;
    }
    search(root->lchild,x,newdata);//往左子树递归
    search(root->rchild,x,newdata);//往右子树递归
}
```

4. 插入节点

```c
//insert函数要注意必须对根节点root使用引用，否则无法插入（对root本身修改）
void insert(node* &root,int x){
    if(root==null){;//空树，查找失败，插入
        root=newNode(x);
        return;
    }
    if(由于二叉树性质，应该插在left subtree){
        insert(root->lchild,x);
    }else{
        insert(root->rchild,x);
    }
}
```

5. 二叉树创建

````c
node* createTree(int data[],int n){
    node* root=null;
    for(int i=0;i<n;i++){
        insert(root,data[i]);
    }
    return root;
}
````

6. 完全二叉树的存储结构

$$
可以直接建立一个2^k大小的数组存放完全二叉树，其中k为二叉树的最大高度
$$

性质：

1. 完全二叉树任何一个编号为x的结点，它的左孩子编号一定是2x，右孩子编号一定是2x+1;

2. 此外，该数组存放的顺序恰好为完全二叉树的层序遍历序列。
3. 而判断某个结点是否为叶结点的标志为：该结点的左节点2x大于结点总个数n；
4. 判断某个结点是否为空的标志：该结点下标大于结点总数

### 9.2二叉树的遍历

#### 9.2.1先序遍历

```c
//根节点——左子树——右子树
void preOrder(node* root){
    if(root==null){
        return;
    }
    //最先访问根节点
    printf("%d\n",root->data);
    preOrder(root->lchild);
    preOrder(root->rchild);
}
```

#### 9.2.2中序遍历

```c
//左子树——根节点——右子树
void inOrder(node* root){
    if(root==null){
        return;
    }
    //最先访问左子树
    inOrder(root->lchild);
    printf("%d\n",root->data);
    inOrder(root->rchild);
}
```

#### 9.2.3后序遍历

```c
//左子树——右子树——根节点
void postOrder(node* root){
        if(root==null){
        return;
        }
        postOrder(root->lchild);
        postOrder(root->rchild);
        printf("%d\n",root->data);
        }
```

#### 9.2.4层序遍历

```c
//层序遍历经常要求计算每个结点所处的层次，因此结构体可以直接添加一个layer变量
//二叉链表
struct node{
    int data;      //数据域
    int layer;
    node* lchild;  //指向左子树
    node* rchild;  //指向右子树
};
void LayerOrder(node* root){
    queue<*node> q;//注意这里队列是存地址
    root->layer=1;
    q.push(root);
    while(!q.empty){
        node* now=q.front();
        q.pop();
        printf("%d\n",root->data);//访问队首元素
        if(now->lchild!=null){
            now->lchild->layer=now->layer+1;
            q.push(now->lchild);
        }
        if(now->rchild!=null){
        now->rchild->layer=now->layer+1;
        q.push(now->rchild);
        }
    }
}
```

#### 9.2.5给定先序遍历序列和中序遍历序列，重建二叉树例题

![image-20200630164506472](/../images/%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0/image-20200630164506472.png)

```c
//当前先序序列区间为[preL,preR]， 中序列区间为[inL,inR]，返回根结点地址
node* create(int preL, int preR, int inL, int inR){
    if(preL > preR) {
        return NULL;//先序序列长度小于等于0时，直接返回
        node* root = new node; //新建 一个新的结点，用来存放当前二又树的根结点
        root->data - pre[preL]; //新结点的数据域为根结点的值
        int k;
        for(k = inL; k <= inR; k++) {
            if(in[k]==pre[preL]) { //在中序序列中找到in[k] == pre[L]的结点
               break;
            }
            int numLeft = k-inL; //左子树的结点个数
            //左子树的先序区间为[preL+1, preL+numLeft], 中序区间为[inL, k-1]
            //返回左子树的根结点地址，赋值给root的左指针
            root->lchild = create(preL + 1, preL + numLeft,inL, k - 1) ;
            //右子树的先序区间为[preL + numLeft + 1, preR], 中序区间为[k+1, inR]
           
            //返回右子树的根结点地址，赋值给root的右指针
            root->rchild = create(preL + numLeft + 1, preR, k + 1, inR);
            return root;
            //返回根结点地址
        }
}
```

**注意：只有中序序列可以和其他序列的任意一个来构建唯一的二叉树，其他无论是两两搭配还是三个一起上都不行，因为中序可以区分出左右子树。**

#### 9.2.6二叉树的静态实现

就是把结点的左右指针域改成int型，所有对指针的操作都改为对数组下标的访问，了解一下即可，我还是喜欢指针。

### 9.3树的遍历

#### 9.3.1树的静态写法

一般意义上的树的结点是散乱而没有顺序的，所以我们不使用动态指针而是一个vector数组存放所有字节点的地址——即，考试遇到一般树使用静态写法

```c
struct node
{
    int data;
    vector<int> child;//存放所有子节点的下标
}Node[maxn];
//如果题目不涉及数据，这个结点结构体可以简化为：
vector<int> child[maxn];//即图的邻接表示法在树的应用
```

新建结点

````c
int index=0;
int newNode(int v){
    Node[index].data=v;
    Node[index].child.clear();//清空子节点
    return index++;
}
````

#### 9.3.2树的先根遍历

```c
void preOrder(int root){
    printf("%d\n",Node[root].data);
    for(int i=0;i<Node[root].child.size;i++){
        preOrder(Node[root].child[i]);//递归访问所有子节点
    }
}
```

#### 9.3.3树的层序遍历

````c
//层序遍历与二叉树的类似
struct node{
    int data;      //数据域
    int layer;
    vector<int> child;
}Node[maxn];

void LayerOrder(int root){
    queue<int> q;
    q.push(root);
    NOde[root].layer=0;//根结点的层号为0（这里看题目吧）
    while(!q.empty){
        int front=q.front();
        q.pop();
        printf("%d\n",Node[front].data);//访问队首元素
       
        for(int i=0;i<Node[front].child.size;i++){
            int child=Node[front].child[i];
            Node[child].layer=Node[front].layer+1;
            q.push(child);//将当前所有子节点入队
        }
    }
}
````

#### 9.3.4从树的遍历看DFS与BFS

- DFS与先根遍历-------------------- - 二者问题都可以相互转化。

- BFS与层序遍历-------------------- - 二者问题都可以相互转化。

### 9.4二叉查找树(BST)

#### 9.4.1二叉查找树的定义

"Binary Search Tree",又叫二叉排序树、二叉搜索树

递归定义如下：

①要么二叉查找树是- -棵空树。

②要么二叉查找树由根结点、左子树、右子树组成，其中左子树和右子树都是二叉查找树，且左子树上所有结点的数据域<=根结点的数据域，右子树上所有结点的数据域>=根结点的数据域。

#### 9.4.2二叉查找树的基本操作

1. 查找操作

   ①如果当前根结点root为空，说明查找失败，返回。
   ②如果需要查找的值x= root->data,说明查找成功，访问之。
   ③如果需要查找的值x< root->data,说明应该往左子树查找，因此向root->lchild 递归。
   ④说明需要查找的值x> root->data，则应该往右子树查找，因此向root->rchild递归。

```c
//search函数查找二又查找树中数据域为x的结点
void search (node* root, int x) {
if(root == NULL) { //空树，查找失败
printf ("search failed\n") ;
return;
}
if(x == root->data){ //查找成功，访问之
printf("&d\n"", root->data);
} else if(x< root->data) { //如果 x比根结点的数据域小，说明x在左子树
search (root->lchild, x); //往左子树搜索x 
} else
(//如果x比根结点的数据域大，说明x在右子树
search (root->rchild,x);//往右子树搜索x
}
```

2. 插入操作

```c
//insert函数将在二叉树中插入-一个数据域为x的新结点(注意参数root要加引用&)
void insert(node* &root, int x)
if(root == NULL) [ //空树， 说明查找失败，也即插入位置
root = newNode(x) ;
//新建结点， 权值为x
return;
if(x == root->data) { //查找成功， 说明结点已存在，直接返回
return;
} else if(x < root->data){ //如果x比根结点的数据域小，说明x需要插在左子树
insert (root->lchild, x); //往左子树搜索 x
} else { //如果x比根结点的数据域大，说明x需要插在右子树
insert (root->rchild, x); //往右子树搜索x
}
```

3. 建立操作

```c
//二叉查找树的建立
node* Create(int data[],int n) {
node* root = NULL; // 新建根结点 root
for (int i =0;1< n; i++) {
insert (root, data[i]);
//将data[0]~data[n-1]插入二叉查找树中
}
return root; 
//返回根结点
}//和普通二叉树没有什么区别
```

4. 删除操作

- **前驱：需要删除的根节点的左子树中的最右结点：即比权值小的最大结点**

- **后继：需要删除的根节点的右子树中的最左结点：即比权值大的最小结点**
- 做删除操作时，用这两种的某一个数据域覆盖根节点，并删除自身。

下面两个函数用来寻找以root为根的树中最大或最小权值结点，用以辅助寻找结点的前驱和后继: .

````c
//寻找以root为根结点的树中的最大权值结点
node* findMax(node* root){
while (root->rchild != NULL) {
root = root->rchild; //不断往右， 直到没有右孩子
return root;
}
//寻找以root为根结点的树中的最小权值结点
node* findMin(node* root): {
while(root->lchild!= NULL) {
root = root->lchild;//不断往左， 直到没有左孩子
return root;
}
````

**删除操作的基本思路如下:** 

①如果当前结点root为空，说明不存在权值为给定权值x的结点，直接返回。

②如果当前结点root的权值恰为给定的权值x，开始删除
a)如果当前结点root不存在左右孩子，说明是叶子结点，直接删除。
b)如果当前结点root存在左孩子，那么在左子树中寻找结点前驱pre,然后让pre的数据覆盖root,接着在左子树中删除结点pre。
c)如果当前结点root存在右孩子，那么在右子树中寻找结点后继next, 然后让next的数据覆盖root,接着在右子树中删除结点next。

③如果当前结点root的权值大于给定的权值x,则在左子树中递归删除权值为x的结点。

④如果当前结点root的权值大于给定的权值x,则在右子树中递归删除权值为x的结点。
删除操作的代码如下(如果需要，可以在删除叶子结点的同时释放它的空间):

```c
void deleteNode(node*&root，int x) {//删除以root为根结点的树中权值为x的结点
        if (root == NULL) return;//不存在权值为x的结点

        if (root -> data == x) { // 找到欲删除结点
            if (root -> lchild == NULL && root -> rchild == NULL) { //叶子结点直接删除
                root = NULL;
            }//把root地址设为NULL,父结点就引用不到它了
            else if (root -> lchild != NULL) {//左子树不为空时
                node * pre = findMax(root -> lchild); //找root前驱
                root -> data = pre -> data;//用前驱覆盖root
                deleteNode(root -> lchild, pre -> data);//在左子树中删除结点pre
            } else {//右子树不为空时
                node * next = findMin(root -> rchild);// 找root后继
                root -> data = next -> data; //用后继覆盖root
                deleteNode(root -> rchild, next -> data); //在右子树中删除结点next
            }
        } else if (root -> data > x) {
                deleteNode(root -> lchild, x); //在左子树中删除x
        } else {
                deleteNode(root -> rchild, x); //在右子树中删除x
        }
}
```

这个有很多优化方式，只是最初的模板，之后刷leetcode时要注意

但是也要注意，总是优先删除前驱(或者后继)容易导致树的左右子树高度极度不平衡，使得二叉查找树退化成一条链。 解决这一问 题的办法有两种:

- 一种是每次交替删除前驱或后继。
- 另一种是记录子树高度，总是优先在高度较高的一棵子树里删除结点。

#### 9.4.3二叉查找树的性质

**对二叉查找树进行中序遍历，遍历的结果是有序的。**

### 9.5 平衡二叉树(AVL树)

#### 9.5.1平衡二叉树的定义

**AVL仍然是一颗平衡二叉树，但他所有结点左右子树的高度之差（平衡因子）的绝对值不超过1**

```c
//需要对每个结点都得到平衡因子，因此需要在树的结构中加入一一个变量height,
structnode {
    int V, height;//v为结点权值，height 为当前子树高度
    node *lchild， *rchild;//左右孩子结点地址
};

//在这种定义下，如果需要新建一个结点，就可以采用如下写法:
//生成一个新结点，v为结点权值
node* newNode (int v){
        node*Node=new node;
        //申请一个node型变量的地址空间
        Node->v=v; //结点权值为v
        Node->height=1;//结点高度初始为1
        Node->lchild=Node->rchild=NULL;//初始状态下没有左右孩子
        return Node;
        //返回新建结点的地址
}

//获取以root为根结点的子树的当前height
        int getHeight (node* root){
        if(root==NULL)return 0;/ /空结点高度为0
        return root->height;
        }

//计算结点 root的平衡因子
        int getBalanceFactor (node* root){//左子树高度减右子树高度
        return getHeight(root->1child)一getHeight(root->rchild);
        }
//更新结点root的height
        void updateHeight (node* root){//max(左孩子的height,右孩子的height)+1
        root->height.=max(getHeight(root->lchild),getHeight(root->rchild))+1;
        }
```

#### 9.5.2平衡二义树的基本操作

**包括插入、查找及建立，删除太复杂暂时不说**

1. 查找、建立和二叉树没区别

- 首先介绍一下左旋和右旋的概念

![image-20200703203200793](/../images/%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0/image-20200703203200793.png)

```c
//左旋(Left Rotation)
/*1.让A的右子树◆成为B的左子树。
  2.让B成为A的右子树。
  3.将根结点设定为结点A。*/
void L(node* &root){
        node*temp=root->rchild;//root指向结点A, temp 指向结点B
        root->rchild=temp->lchild;//步骤1
        temp->lchild=root;//步骤2
        updateHeight(root);//更新结点A的高度
        updateHeight(temp);//更新结点B的高度
        root=temp;s //步骤3
        }
```

![image-20200703203551838](/../images/%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0/image-20200703203551838.png)

```c
//右旋(Right Rotation)
/*①让A的右子树◆成为B的左子树。
②让B成为A的右子树。
③将根结点设定为结点A。*/
void R (node* &root){
        node*temp=root->lchild; //root 指向结点B，temp 指向结点A
        root->lchild=temp->rchild;//步骤1
        temp->rchild二root;//步骤2
        updateHeight(root);//更新结点B的高度
        updateHeight(temp);
//更新结点A的高度
        root=temp;//步骤3
        }
```

- **平衡二叉树的插入操作可能导致树的平衡因子失衡（>=2）**

**可以证明，只要把最靠近插入结点的失衡结点调整到正常，路径上的所有结点就都会平衡。**

- **失衡情况：LL，LR，RR，RL**

![image-20200703204207856](/../images/%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0/image-20200703204207856.png)

![image-20200703204222130](/../images/%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0/image-20200703204222130.png)

![image-20200703204252883](/../images/%E7%AE%97%E6%B3%95%E7%AC%94%E8%AE%B0/image-20200703204252883.png)

由于我们需要从插入的结点开始从下往上判断结点是否失衡，因此需要在每个insert函数之后更新当前子树的高度，并在这之后根据树型是LL型、LR型、RR型、RL型之一来进行平衡操作，代码如下:

```c
//插入权值为v的结点
void insert (node* &root, int v) {
        if(root = NULL){ //到达空结点
        root=newNode(v);
        return;
        }
    
        if(v<root->v) { //v 比根结点的权值小
        insert(root->lchild, v); //往左子树插入
        updateHeight(root); //更新树高
        if (getBalanceFactor(root)== 2) {
            if (getBalanceFactor (root->lchild)==1) {//LL型
              R(root) ;
            }else if (getBalanceFactor (root->lchild) == -1) {//LR型
                 L(root->lchi1d);
                 R(root) ;
            }
        else (//v比根结点的权值大
        insert (root->rchild, v);//往右子树插入
        updateHeight (root);//更新树高
        if (getBalanceFactor (root)==2) {
        if (getBalanceFactor (root->rchild) = -1) ( //RR型
        L(root);
        } else if (getBalanceFactor (root->rchild) == 1){ //RL型
        R(root->rchild);
        L(root);
        }
        }
}
```









### 9.6并查集

#### 9.6.1并查集的定义

1. **并查集是一种维护集合的数据结构，它的名字中“并”“查”“集”分别取自Union (合并)、Find (查找)、Set (集合)这3个单词。也就是说，并查集支持下面两个操作:**
   **①合并:合并两个集合。**
   **②查找:判断两个元素是否在一个集合。**

2. **实现方式：int father[N];**

3. **其中，fahter[i]表示元素i的父亲结点，而父亲结点本身也是这个集合内的元素(1≤i≤N)。例如father[1] = 2就表示元素1的父亲结点是元素2，以这种父系关系来表示元素所属的集合。**

   **另外，如果father[i]=i,则说明元素i是该集合的根结点，但对同一个集合来说只存在-一个根结点，且将其作为所属集合的标识。**

4. **并查集产生的每一个集合都是一棵树**

#### 9.6.2并查集的基本操作

1. 初始化

```c
for(int i=1;i<=n;i++){
    father[i]=i;//每个元素初始都是一个独立的集合
}
```

2. 查找(根节点)

```c
int findFather(int x){
    while(x!=father(x)){
        x=father[x];
    }
    return x;
}
```

3. 合并

- 先判断两个集合是否属于同一个集合

- 合并两个集合

```c
void Union(int a,int b){
    int faA=findFather(a);
    int faB=findFather(b);
    if(faA!=faB){
        father[faA]=faB
    }
}
```

#### 9.6.3路径压缩(查找递归优化)

上面讲的查找函数没有优化，如果查找时把当前结点路径上的所有结点的父亲都指向根结点，那之后查找就不用一直回溯了：

````c
int findFather(int a){
    if(a==father(a)) return a;
    else{
        int F=findFather(father(a));
        father(a)=F;
        return F;
    }
        
}
````

### 9.7堆

#### 9.7.1堆的定义

**堆是一棵完全二叉树，树中每个节点都不小于或不大于其左右孩子，根据每个结点的父亲结点是大还是小分为大顶堆和小顶堆。**

所以和完全二叉树一样用数组存储

````c
const int maxn=100;
int heap[maxn],n=10;//10为堆元素个数
````

#### 9.7.2堆的基本操作

1. 向下调整：

```c
//heap数组在[low,high]范围向下调整
//low为需要调整的数组下标，high为最后一个元素的下标
void downAdjust(int low,int high){
    int i=low,j=i*2;//j为其左孩子
    while(j<=high){//存在孩子结点
        if(j+1<=high&&heap[j+1]>heap[j]){
            j=j+1
        }
        if(heap[j]>heap[i]){//孩子比父亲大就换
            swap(heap[i],heap[j]);
            i=j;//保持i=欲调整结点
            j=i*2;//孩子也保持
        }else{
            break;
        }
     
    }
}
```

2. 建堆

```c
void createHeap(){
    for(int i=n/2;i>0;i++){
        downAdjust(i,n);
    }
}
```

3. 删除堆顶元素

```c
void deleteTop(){
    heap[1]=heap[n--];//用最后一个元素覆盖堆顶然后向下调整
    downAdjust(1,n);
}
```

4. 添加元素

```c
//向上调整，low一般设为1，high是需要调整的下标
void upAdjust(int low,int high){
    int i=high,j=i/2;//和父亲比较
    while(j>=low){
        if(heap[j]<heap[i]){//和父亲比较
            swap(heap[j],heap[i]);
            i=j;
            j=i/2;
        }else{
            break;
        }
    }
}
void insert(int x){
    heap[++n]=x;
    upAdjust(1,n);
}
```

#### 9.7.3堆排序

```c
void heapSort(){
    createHeap();
    for(int i=n;i>1;i--){
        swap(heap[i],heap[1]);
        downHeap(1,i-1);
    }
}//原理挺长的不写了，去看书P341
```

### 9.8哈夫曼树

#### 9.8.1哈夫曼树

构建思想：反复选择两个最小的元素合并，直到只剩下最后一个元素

以合并果子为例

```c
//优先队列实现
priority_queue<long long,vector<long,long>,greater<long,long> > q;
int main(){
    for(...){
        //将初始重量压入优先队列
        q.push(temp);
    }
    while(q.size()>1)//至少得有俩才能合并
    {
        x=q.top();
        q.pop();
        y=q.top();
        q.pop(); 
        q.push(x+y);
        ans+=x+y;
    }
    ...
    return 0;
}
```

#### 9.8.2哈弗曼编码

**即令任何一个叶子结点（字符），其编码一定不会成为其他任何一个结点（字符）编码的前缀，满足这种编码方式的编码成为前缀编码**

**前缀编码的存在意义在于不产生混淆，使解码正常进行。**

**哈夫曼编码是能使给定字符串编码成01串后长度最短的前缀编码。**

## 第十章 提高: 图算法专题.

### 10.1图的定义和相关

由顶点Vertex和边Edge组成

| name     | explanation                          |
| -------- | ------------------------------------ |
| 有向图   | 所有边都有单个方向                   |
| 无向图   | 所有边都是双向的                     |
| 顶点的度 | 和该顶点相连的边数（分为入度和出度） |
| 权值     | （点权和边权）代表某个属性           |

### 10.2图的存储

#### 10.2.1邻接矩阵

**——————二维数组，顶点数目比较少时用这个**

```c++
//G[i][j]=1表示顶点i，j之间有边，G[i][j]=0表示顶点i，j之间无边
```

#### 10.2.2邻接表

**——————链表或者vector，顶点数目比较多时用这个**

```C++
//Adj[i][0]表示当前访问的顶点标号为i，int v=Adj[i][0].v(得到可以到达的顶点标号)
Struct Node{
int v;//边编号
int w;//边权
Node(int _v,int _w):v(_v),w(_w){}//构造函数
}
vector<Node> Adj[N];
Adj[1].push_back(Node(3,4));
```

### 10.3图的遍历

#### 10.3.1采用深度优先搜索(DFS)法遍历图

| 连通分量   | 无向图：两顶点可以相互到达，就称为连通；如果图任意两个顶点都联通，就称图为连通图；否则，称非连通图中的极大连通子图为连通分量 |
| ---------- | ------------------------------------------------------------ |
| 强连通分量 | 有向图：两顶点可以各自相互到达，就称为强连通；如果图任意两个顶点都联通，就称图为强连通图；否则，称非强连通图中的极大强连通子图为强连通分量 |

1. 伪代码

````c
DFS(u){//访问顶点u
    vis[u]=true;//设置已被访问
    for(从u出发能到达的所有顶点v){
        if(vis[v]==flase){
            DFS(v);//递归访问v
        }
    }
}
DFSTrave(G){//遍历图G
    for(G的所有顶点u){
        if(vis(u)==flase)
            DFS(u);//访问u所在的连通块
    }
}
````

2. 邻接矩阵版

````c
const int MAXV=1000;//最大顶点数
const int INF=1000000000//INF设为一个很大的树
    
int n,G[MAXV][MAXV];//n为顶点数
bool vis[MAXV]={false};//如果顶点已被访问，就是true

void DFS(int u,int depth){
    vis[u]=true;
    for(int v=0;v<n;v++){//对所有顶点遍历一遍
        if(vis[v]==flase&&G[u][v]==1){//如果未被访问且u可以到达v
            DFS(v,depth+1);//递归
        }
    }
}
void DFSTrave(){//遍历图G
    for(int u=0;u<n;u++){
        if(vis[u]==false)
            DFS(u,1)//访问u所在的连通块,1表示初始为第一层
    }
}
````

3. 邻接表版

````c
const int MAXV=1000;//最大顶点数

vectos<int> Adj[MAXV];
int n//n为顶点数
bool vis[MAXV]={false};//如果顶点已被访问，就是true

void DFS(int u,int depth){
    vis[u]=true;
    for(int i=0;v<Adj[u].size;i++){//对所有顶点遍历一遍
        int v=Adj[u][i];//u可以到达v
        if(vis[v]==flase){//如果未被访问
            DFS(v,depth+1);//递归
        }
    }
}
void DFSTrave(){//遍历图G
    for(int u=0;u<n;u++){
        if(vis[u]==false)
            DFS(u,1)//访问u所在的连通块,1表示初始为第一层
    }
}
````

#### 10.3.2采用广度优先搜索(BFS) 法遍历图

1. 伪代码

```c
BFS(u){//访问顶点u
    queue q;//定义队列q
    inq[u]==true;//将顶点u入队
    while(q非空){
        for(从u出发能到达的所有顶点v){
             if(inq[v]==flase){//如果v没有入过队，将v入队
                inq[v]=true;
              }
        }
    }
}
BFSTrave(G){//遍历图G
    for(G的所有顶点u){
        if(vis(u)==flase)
            BFS(u);//访问u所在的连通块
    }
}
```

2. 邻接矩阵版

```c
const int MAXV=1000;//最大顶点数
    
int n,G[MAXV][MAXV];//n为顶点数
bool inq[MAXV]={false};//如果顶点已入队，就是true

void BFS(int u){
    queue<int> q;//定义队列q
    q.push(u);
    inq[u]=true;
    while(!q.empty){
        int u=q.front();
        q.pop();//
        for(int v=0;v<n;v++){
             if(inq[v]==flase&&G[u][v]==1){//如果v没有入过队且v是u的临接点，将v入队
                 q.push(v);
                inq[v]=true;
              }
        }
    }
}
BFSTrave(G){//遍历图G
    for(int u=0;u<n;++u){
        if(inq(u)==flase)//u没入过队
            BFS(u);//访问u所在的连通块
    }
}
```

3. 邻接表版

````c
const int MAXV=1000;//最大顶点数

vectos<int> Adj[MAXV];
int n//n为顶点数
bool vis[MAXV]={false};//如果顶点已被访问，就是true

void BFS(int u){
    queue<int> q;//定义队列q
    q.push(u);
    inq[u]=true;
    while(!q.empty){
        int u=q.front();
        q.pop();//
        for(int i=0;i<Adj[u].size;i++){
            int v=Adj[u][i];
             if(inq[v]==flase){//如果v没有入过队且v是u的临接点，将v入队
                 q.push(v);
                inq[v]=true;
              }
        }
    }
}
void BFSTrave(){//遍历图G
    for(int u=0;u<n;u++){
        if(vis[u]==false)
            DFS(u)//访问u所在的连通块,1表示初始为第一层
    }
}
//要求层号就用结构体，加点代码就行
````

### 10.4最短路径

#### 10.4.1 Dijkstra 算法

1. 作用:解决单源最短路径问题(边权均为非负数)
2. 伪代码

设置数组S存放已经被访问的顶点，循环n次下面的步骤（n为顶点个数）

- 每次从集合V-S中（未访问的顶点）中·选择与起点s距离最短的一个点记为u，访问它并加入集合S
- 之后令顶点为中介点，优化起点s与所有从u能到达的顶点v的最短距离

```c
//G为图，一般设置成全局变量；数组d为源点到达各点最短路径长度；s为起点
Dijkstra(G,d[],s){
    初始化；
    for(循环n次){
        for(){
            u=使d[u]最小的还未访问的顶点;
        }
        标记u被访问;
        for(u出发可以访问的所有顶点v){
            if(v未被访问&&以u到达v的路径可以使d[v]更优)
                优化d[v];
        }
    }  
}
```

3. 邻接矩阵版

`````c
const int MAXV=1000;//最大顶点数
const int INF=1000000000;//INF为一个很大的数
    
int n,G[MAXV][MAXV];//n为顶点数
int d[MAXV];
bool vis[MAXV]={false};//如果顶点已入队，就是true

//G为图，一般设置成全局变量；数组d为源点到达各点最短路径长度；s为起点
void Dijkstra(int s){
    //初始化；
    fill(d,d+MAXV,INF);//fill给整个d数组复制，慎用memset数组
    d[s]=0;//起点s到达自己的距离为0
    for(int i=0;i<n;i++){
        int u=-1,MIN=INF;//u使d[u]最小，MIN存最小d[u]值；
        for(int j=0;j<n;j++){//循环n次找到未访问的顶点;
            if(vis[j]==flase&&d[j]<MIN){
                u=j;//u=使d[u]最小的还未访问的顶点;
                MIN=d[j];
            }
        }
        if(u==-1) return;//找不到小于INF的d[u],说明剩下的顶点和起点s不流通；
        vis[u]=true;// 标记u被访问;
        for(int v=0;v<n;v++){
            if(vis[v]==flase&&G[u][v]!=INF&&d[u]+G[u][v]<d[v])
                d[v]=d[u]+G[u][v];//优化d[v];
        }
    }  
}
`````

4. 邻接表版

````c
const int MAXV=1000;//最大顶点数

struct Node{
    int v,dis;//v=目标顶点；dis=边权
}
vectos<Node> Adj[MAXV];
int n//n为顶点数
bool vis[MAXV]={false};//如果顶点已被访问，就是true
int d[MAXV];

//G为图，一般设置成全局变量；数组d为源点到达各点最短路径长度；s为起点
void Dijkstra(int s){
    //初始化；
    fill(d,d+MAXV,INF);//fill给整个d数组复制，慎用memset数组
    d[s]=0;//起点s到达自己的距离为0
    for(int i=0;i<n;i++){
        int u=-1,MIN=INF;//u使d[u]最小，MIN存最小d[u]值；
        for(int j=0;j<n;j++){//循环n次找到未访问的顶点;
            if(vis[j]==flase&&d[j]<MIN){
                u=j;//u=使d[u]最小的还未访问的顶点;
                MIN=d[j];
            }
        }
        if(u==-1) return;//找不到小于INF的d[u],说明剩下的顶点和起点s不流通；
        vis[u]==true;// 标记u被访问;
        for(int j=0;j<Adj[u].size();j++){
            int v=Adj[u][j].v;
            if(vis[v]==flase&&d[u]+Adj[u][j].dis<d[v])
                d[v]=d[u]+Adj[u][j].dis;//优化d[v];
        }
    }  
}
````

5. 题目变化：
   1. 得到全路径——>设pre[MAXV]存放前驱节点，递归输出
   2. 第二标尺——>新增点权//新增边权//求最短路径条数

#### 10.4.2 Bellman-Ford 算法和SPFA算法

**——解决单源路径最短且有负边权**

还没看懂原理，之后刷到这种题就重新回P393看一遍

#### 10.4.3 Floyd 算法

**——全源最短路径,即找到任意两点之间最短的路径**

1. 伪代码

```c
枚举顶点k属于[1,n]
    以顶点k作为中介点，枚举所有顶点对i和j（i属于[1,n],j属于[1,n]
       如果dis[i][k]+dis[k][j]<dis[i][j]成立
           赋值dis[i][j]=dis[i][k]+dis[k][j]
```

2. 实现代码

````c
void Floyd(){
    for(int k=0;k<n;k++)
        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++){
                if(dis[i][k]!=INF&&dis[k][j]!=INF&&dis[i][k]+dis[k][j]<dis[i][j])
                    dis[i][j]=dis[i][k]+dis[k][j]
            }
}
````

### 10.5最小生成树
#### 10.5.1最小生成树及其性质.

最小生成树拥有无向图的所有顶点且满足整棵树的边权之和最小

下面两种算法都采用了贪心法，只是贪心的策略不太一样;

**稠密图（边多）用prim算法；稀疏图（边少）用krustal算法**

#### 10.5.2 prim 算法

——解决最小生成树问题

思想和Dijkstra几乎完全相同，区别仅在于d[]的含义不同//ans记录了最小生成树的总路径

1. 伪代码

```c
//G为图，一般设置成全局变量；数组d为源点到达各点最短路径长度；s为起点
Prim(G,d[]){
    初始化；
    for(循环n次){
        for(){
            u=使d[u]最小的还未访问的顶点;
        }
        标记u被访问;
        for(u出发可以访问的所有顶点v){
            if(v未被访问&&以u为中介点使得v与集合S的最短路径可以使d[v]更优)
                将G[u][v]赋值给v与集合S的最短路径d[v];
        }
    }  
}
```

2. 邻接矩阵版

```c
const int MAXV=1000;//最大顶点数
const int INF=1000000000;//INF为一个很大的数
    
int n,G[MAXV][MAXV];//n为顶点数
int d[MAXV];//顶点与集合的最短距离
bool vis[MAXV]={false};//如果顶点已访问，就是true

//G为图，一般设置成全局变量；数组d为源点到达各点最短路径长度；s为起点
int Prim(){
    //初始化；
    fill(d,d+MAXV,INF);//fill给整个d数组复制，慎用memset数组
    d[s]=0;//起点s到达集合S的距离为0
    int ans=0;//存放最小生成树的边权之和
    for(int i=0;i<n;i++){
        int u=-1,MIN=INF;//u使d[u]最小，MIN存最小d[u]值；
        for(int j=0;j<n;j++){//循环n次找到未访问的顶点;
            if(vis[j]==flase&&d[j]<MIN){
                u=j;//u=使d[u]最小的还未访问的顶点;
                MIN=d[j];
            }
        }
        if(u==-1) return -1;//找不到小于INF的d[u],说明剩下的顶点和起点s不流通；
        vis[u]=true;// 标记u被访问;
        ans+=d[u];//将于集合S距离最小的边加入最小生成树
        for(int v=0;v<n;v++){
            if(vis[v]==flase&&G[u][v]!=INF&&G[u][v]<d[v])
                d[v]=G[u][v];//优化d[v];
        }
    }  
    return ans;
}
```

3. 邻接表版

```c
const int MAXV=1000;//最大顶点数

struct Node{
    int v,dis;//v=目标顶点；dis=边权
}
vectos<Node> Adj[MAXV];
int n//n为顶点数
bool vis[MAXV]={false};//如果顶点已被访问，就是true
int d[MAXV];

//G为图，一般设置成全局变量；数组d为源点到达各点最短路径长度；s为起点
int Prim(){
    //初始化；
    fill(d,d+MAXV,INF);//fill给整个d数组复制，慎用memset数组
    d[s]=0;//起点s到达集合S的距离为0
    int ans=0;//存放最小生成树的边权之和
    for(int i=0;i<n;i++){
        int u=-1,MIN=INF;//u使d[u]最小，MIN存最小d[u]值；
        for(int j=0;j<n;j++){//循环n次找到未访问的顶点;
            if(vis[j]==flase&&d[j]<MIN){
                u=j;//u=使d[u]最小的还未访问的顶点;
                MIN=d[j];
            }
        }
        if(u==-1) return -1;//找不到小于INF的d[u],说明剩下的顶点和起点s不流通；
        vis[u]=true;// 标记u被访问;
        ans+=d[u];//将于集合S距离最小的边加入最小生成树
        for(int v=0;v<n;v++){
            int v=Adj[u][j].v;
            if(vis[v]==flase&&Adj[u][j].dis<d[v])
                d[v]=Adj[u][j].dis;//优化d[v];
        }
    }  
    return ans;
}
```

#### 10.5.3 kruskal 算法

1. 伪代码

`````c
int kruskal(){
    令最小生成树的边权之和为ans，最小生成树的当前边数Num_Edge
    将所有边按边权从大到小排序；
        for(从大到小枚举所有边){
            if(当前测试边的两个端点在不同的连通块中){
                将该测试边加入最小生成树中；
                    ans+=测试边的边权；
                    最小生成树的当前边数Num_Edge+1；
                    当Num_Edge=顶点数-1时结束循环；
            }
        }
    return ans;
}
判断两个端点是否在一个连通块中的方法是使用并查集
`````

2. 实现代码

````c
struct edge{
    int u,v;//边的两个端点
    int cost;//边权
}E[MAXE];//最多MAXE条边

bool cmp(edge a,rdge b){
    return a.cost<b.cost;//从小到大对边权排序
}

int father[N];//并查集数组

int findFather(int x){//并查集查询函数
    while(x!=father(x)){
        x=father[x];
    }
    return x;
}
//krustal函数返回最小生成树的边权之和，参数n为顶点个数，m为图的边数
int krustal(int n,int m){
    //令最小生成树的边权之和为ans，最小生成树的当前边数Num_Edge
    int ans=0,Num_edg=0;
    for(int i=0;i<=n;i++){
        father[i]=i;//并查集初始化
    }
    sort(E,E+m,cmp);//对边排序
    for(int i=0;i<m;i++){//枚举所有边
        int faU=findFather(E[i].u);
        int faV=findFather(E[i].v);
        if(faU!=faV){
            father[faU]=faV;//合并集合
            ans+=E[i].cost;
            Num_edge++;
            if(Num_edge==n-1) break;
        }
    }
    if(Num_edge!=n-1) return -1;//最终也无法联通就返回-1
    else return ans;
}

````

### 10.6拓扑排序

#### 10.6.1有向无环图DAG

**如果一个有向图的任意顶点都无法通过一些有向边回到自身，这个图被称为有向无环图DAG**

#### 10.6.2拓扑排序

拓扑排序是将有向无环图G的所有顶点排成一个线性序列，使得图G中的任意两个点u，v，如果存在边u->v,那么在序列中u一定在v的前面。这个序列就叫做拓扑序列。

1. 伪代码

```c
1、定义队列q，所有入度为0的顶点加入队列；
2、输出队首结点，删除所有由它出发的边，并且令对应的顶点入度减一，如果这是某个顶点入度=0，就将此顶点加入队列；
3、反复2操作，直到队列为空，此时如果入过队的结点刚好=N，则拓扑排序成功，图是DAG，否则说明存在闭环
```

2. 实现代码（邻接表）

````c
vector<int> G[MAXV];//邻接表
int n,m,inDegree[MAXV];

bool topologicalSort(){
    int num=0;//记录加入拓扑排序的顶点数
    queue<int> q;
    for(int i=0;i<n;i++){
        if(inDegree[i]==0){
            q.push(i);//所有入度为0的顶点加入队列；
        }
    }
    while(!q.empty){
        int u=q.front();
        q.pop();
        for(int i=0;i<G[u].size;i++){
            int v=G[u][i].v;
            inDegree[v]--;
            if(inDegree[v]==0){
                q.push(v);
            }
        }
        G[u].clear();//清空u的所有出边（不必要可以不写）
        num++;
    }
    if(num==n)
        return true;
    else 
        return false;
}
````

3. **ps**:如果要求有多个入度为0的顶点，选择编号最小的顶点，那么把queue改成priority_queue，并保持队首元素是优先队列最小的元素即可。（遇到具体的问题再说吧）

### 10.7关键路径

#### 10.7.1 AOV网和AOE网

| AOV网 | Acticity On Vertex——顶点表示活动，而用边集表示活动间优先关系的有向图； |
| ----- | :----------------------------------------------------------- |
| AOE网 | Activity On Edge——带圈的边集表示活动，顶点表示事件的有向图； |
| 源点  | 入度为0的点（或者创建一个新点连接所有入度为0的点）           |
| 汇点  | 出度为0的点（或者创建一个新点连接所有出度为0的点）           |

**AOE网的最长路径就是关键路径，关键路径上的活动称为关键活动，所需时间就是最短时间**

**AOV转换为AOE的方法就是拆解顶点，边视为空活动。**

#### 10.7.2最长路径

对于一个没有正环的图，求最长路径，就所有边乘以-1再用Bellman-Ford算法或者SPFA算法求最短路径再取反。

#### 10.7.3关键路径

**AOE是有向无环图，所以这里的方法实际上是求解有向无环图DAG中最长路径的方法。**

如下——活动示意图：
$$
事件V_i-----------------活动a_r--------------------事件V_j
$$
由于关键活动是那些不允许拖延的活动，因此这些活动的最早开始时间必须等于最迟开始时间。因此可以设置数组e和l，其中e[r]和l[r]分别表示活动a_r的最早开始时间和最迟开始时间。于是，当我们求出这两个数组之后，就可以通过判断e[r]==l[r]是否成立来确定活动r是否是关键活动。

那么，如何求解数组e和l？

我们看上面的活动示意图可以知道——

**事件最早发生时间==旧活动的最早结束时间，事件的最迟发生时间==新活动的最迟开始时间。？（事件的最迟发生时间==旧活动的最迟结束时间。）**所以，可以再设置数组ve[i],vl[i]分别表示事件i的最早发生时间和最晚发生时间，然后我们就可以根据下面的公式转换得出e[r]和l[r]了。

ps：事件可以拖延，所以没有结束时间。

````c
1、事件Vi最早发生时间=新活动a_r最早开始时间
e[r]=ve[i];
2、事件Vj最晚发生时间-length[r]=活动a_r最晚开始时间
l[r]=vl[j]-length[r];
3、假设已知k个事件V_i1~~V_ik的最早发生时间,要求事件V_j的最早发生时间，此时由于只有所有事件都到达后，事件j才能开始，所以取最大值
ve[j]=max{ve[ip]+length[rp]}
4、假设已知k个事件V_j1~~V_jk的最晚发生时间,要求事件V_i的最晚发生时间，此时由于必须保证所有后续结点的最晚到达时间都能被满足，所以取最小值
vl[i]=min{vl[jp]-length[rp]}
5、用上面的结果计算各边的结果
最早：e[i->j]=ve[i]
最晚：l[i->j]=vl[j]-length[i->j]
````

**主题代码如下：**

````c
------------------------------------------------------------------------------------------
已知所有前驱结点的ve，求结点的ve：-------------------------------------------------------------
int n,m,inDegree[MAXV];
//拓扑序列
stack<int> topOrder;
//拓扑序列排序，顺便先求ve数组（每个事件的最早发生时间是根据前一个事件的最早发生时间+边的长度得出的。
bool topologicalSort(){
    queue<int> q;
    for(int i=0;i<n;i++){
        if(inDegree[i]==0){
            q.push(i);//所有入度为0的顶点加入队列；
        }
    }
    while(!q.empty){
        int u=q.front();
        q.pop();
        topOrder.push(u);//将u加入拓扑序列
        for(int i=0;i<G[u].size;i++){
            int v=G[u][i].v;
            inDegree[v]--;
            if(inDegree[v]==0){
                q.push(v);
            }
        }
        //用ve[u]来更新u的所有后继结点v
        if(ve[u]+G[u][i].w>ve[v]){
            ve[v]=ve[u]+G[u][i].w;
        }
    }
    if(topOrder.size()==n) return true;
    else return false;
}

------------------------------------------------------------------------------------------
已知所有后继结点的vl，求结点的vl--------------------------------------------------------------
适用于汇点确定且唯一的情况，以n-1为汇点为例
//关键路径，不是有向无环图返回-1，否则返回关键路径长度，顺便把vl数组的值求了
int CriticalPath(){
    memset(ve,0,sizeof(ve));//ve数组初始化
    if(topologicalSort==false) return -1;//不是有向无环图，退出
    fill(vl,vl+n,ve[n-1]);//vl数组初始化，初始值为汇点的ve值
    //直接使用topOrder出栈即为逆拓扑排序，求解vl数组
    while(!topOrder.empty()){
        int u=topOrder.top();
        topOrder.pop();
        for(int i=0;i<G[u].size();i++){
            int v=G[u][i].v;//u的后继结点v
            //用u的所有后继节点v的vl值来更新vl[u]
            if(vl[v]-G[u][i].w<vl[u]){
                vl[u]=vl[v]-G[u][i].w;
            }
        }
    }
//遍历邻接表的所有边，计算活动的最早活动开始时间e和最迟开始时间l
   for(int u=0;u<n;u++){
      for(int i=0;i<G[u].size();i++){
        int v=G[u][i].v,w=G[u][i].w;
        int e=ve[u],l=vl[v]-w;
        //如果e==1，说明活动u->v是关键活动
        if(e==l){
            printf("%d->%d\n",u,v);//输出关键活动
        }
       }
    }
    return ve[n-1];//返回关键路径长度
}
------------------------------------------------------------------------------------------
    ps：
    1、如果实现不知道汇点编号，就取ve数组的最大值，因为ve最大的肯定是最后一个
    2、如果想要存下关键活动并输出，就设置一个邻接表存一下就好。
````

## 第十一章 提高：动态规划专题

### 11.1动态规划的递归和递推

动态规划是一种用来解决一类最优化问题的算法思想，简单来说，就是将一个复杂的问题分解为若干个子问题，通过综合子问题的最优解来得到原问题的最优解，这个过程中动态规划会把每个子问题的最优解记录下来。

**实现方式有递归(例如斐波那契数列）和递推（树塔问题）**

**注意：一个问题必须拥有重叠子问题和最优子结构才能用DP**

1. 和分治的区别：分治没有重叠子问题
2. 和贪心的区别：贪心不一定是最优解(但他们都拥有最优子结构)

### 11.2最大连续子序列和

1. 问题描述：给定一个数字序列A1~An，求i，j（1<=i<=j),使得A1+...+Aj最大，输出这个最大和
2. 解决步骤：

              - 步骤一：令状态dp[i]表示以A[i]作为末尾的连续序列的最大和
   - 步骤二：根据dp[i]的要求我们可以知道只有两种情况
               - 1、这个最大和序列只有一个元素就是A[i]本身
               - 2、这个最大和序列有多个元素，从前面某处p开始（p<i）开始
               - 于是得到**状态转移方程：dp[i]=max{A[i],dp[i-1]+A[i]}**
               - **边界为dp[0]=A[0]**

3. 代码实现

```c++
#include<cstdio>
#include<algorithm>
using namespace std;
const int maxn =10010;
int A[maxn],dp[maxn];
int main(){
    int n;
    scanf("d%",&n)
    for(int i=0;i<n;i++){
       scanf("d%",&A[i])
    }
    //边界
    dp[0]=A[0];
    //状态转移方程
    for(int i=1;i<n;i++){
        dp[i]=max(A[i],dp[i-1]+A[i]);
    }
    //然后遍历一下dp数组得到的最大值就是最大连续不下降子序列和了。
    .....
}
```

4. 状态后无效性：以及记录了的状态信息之后不会再改变。动态规划必须设计一个拥有后无效性的状态和相应的状态转移方程才能得到正确结果。

### 11.3最长不下降子序列（LIS）

1. 问题描述：Longest Increasing Sequence，在一个数字序列A1~An，中，找到一个最长的子序列（可以不连续），使得这个子序列是不下降（非递减）的。
2. 解决步骤：

   - 步骤一：令状态dp[i]表示以A[i]作为末尾的最长不下降子序列的长度
   - 步骤二：根据dp[i]的要求我们可以知道只有两种情况
        - 1、最长不下降子序列的长度为1，就只有A[i]
        - 2、这个最大和序列有多个元素，从前面某处j开始（j<i）开始,并且所有的A[j]<A[i],遍历前面的dp[j]得到dp[j]+1的最大值。
        - 于是得到**状态转移方程：dp[i]=max{1,dp[j]+1}，(  j 属于[1,n) && A[j]<A[i]  )**
        - **边界为dp[i]=1**

3. 代码实现

   ```c
   const int maxn =100;
   int A[maxn],dp[maxn];
   int main(){
       int n;
       scanf("d%",&n)
       for(int i=1;i<=n;i++){
          scanf("d%",&A[i])
       }
       int ans=-1;//记录最大的dp[i]
       for(int i=1;i<=n;i++){
           //边界
           dp[i]=1;
           for(int j=1;j<i;j++){
               if(A[j]<A[i]&&(dp[i]<dp[j]+1))
                   dp[i]=dp[j]+1;
           }
           ans=max(ans,dp[i]);
       }
       printf("d%",ans);
       return 0;
   }
   ```

### 11.4最长公共子序列（LCS）

1. 问题描述：Longest Common Sequence，在两个字符串（数字）序列A1~An，中，找到最长的公共的的子序列（可以不连续）
2. 解决步骤：

   - 步骤一：令状态dp [i] [j]表示以序列A的i号位和序列B的j号位作为末尾的最长公共子序列的长度
   - 步骤二：根据dp[i] [j]的要求我们可以知道有两种情况
        - 1、A[i]==A[j]时，那么字符串A和B的最长公共子序列的长度要加1
        - 2、A[i]!=A[j]，无法延长，就继承dp[i-1] [j]和dp[i] [j-1]中的较大值。
        - 于是得到**状态转移方程：**
                    - dp[i] [j]=dp[i-1] [j-1]+1，A[i]==B[i]
                        - dp[i] [j]=max(dp[i-1] [j]，dp[i] [j-1])，A[i]!=B[i]
        - **边界为dp[i] [0]=dp[0] [j]=0**

3. 代码实现

```c
const int N =100;
int A[N],B[N];
int dp[N[N];
int main(){
    int n;
    gets(A+1);//从下标为1开始读入
    gets(B+1);
    int lenA=strlen(A+1);
    int lenB=strlen(B+1);
    //边界
    for(int i=1;i<=n;i++){
       d[i][0]=0;
    }
    for(int i=1;i<=n;i++){
       d[0][i]=0;
    }
    for(int i=1;i<=lenA;i++){
        for(int j=1;j<lenB;j++){
            if(A[i]==B[i]){
                 dp[i][j]=dp[i-1][j-1]+1;
            }else{
                dp[i][j]=max(dp[i-1][j],dp[i][j-1])
            }
        }
    }
    printf("d%\n",dp[lenA][lenB]);
    return 0;
}
```

### 11.5最长回文子串

1. 解决步骤： 
   - ​    步骤一：令状态dp [i] [j]表示以序列A的i-1号位和序列B的j-1号位作为末尾的最长公共子串的长度（不是直接i、j号位的原因是字符串下标从零开始，而dp数组的下标表示的是两个字符串当前所在位所占的的实际长度），因此dp数组长度为dp[lenA+1] [lenB+1]],循环从i=1,j=1开始，因为任何一个下标=0的dp数组值显然都等于0。   
   - ​    步骤二：于是，根据dp[i] [j]的要求我们可以知道有两种情况   
     - ​     1、A[i-1]==A[j-1]时，那么字符串A和B的最长公共子串的长度要加1    
     - ​     2、A[i-1]!=A[j-1]，dp[i] [j]=0；    
     - ​     于是得到**状态转移方程：**    
       - ​       dp[i] [j]=dp[i-1] [j-1]+1，A[i]==B[i]      
         - ​         dp[i] [j]=max(dp[i-1] [j]，dp[i] [j-1])，A[i]!=B[i]        
     - ​     **边界为dp[i] [0]=dp[0] [j]=0**

```c
#include<iostream>
#include<cmath>
#include<string>
#include<string.h>
#include<algorithm>
#include<cstdio>
using namespace std;
string lower(string s)
{
 for (int i = 0; i < s.size(); i++)  //把所有字符变成小写
 {
  if (s[i] >= 'A' && s[i] <= 'Z')
   s[i] = s[i] + 32;
 }
 return s;
}
int main(int argc,char *argv[]){
    string str1;
    string str2;
    while(cin>>str1>>str2){
        lower(str1);
        lower(str2);
        int len1=str1.length();
        int len2=str2.length();
        int flag=0,max=0;
        int dp[len1+1][len2+1];
        memset(dp,0,sizeof(dp));
        for(int i=1;i<len1+1;i++)
            for(int j=1;j<len2+1;j++){
                if(str1[i-1]==str2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                    if(max<dp[i][j])
                        max=dp[i][j];
                }
                else 
                    dp[i][j]=0;
            }                
        printf("%d\n",max);
    }
    return 0;
}
```

### 11.6DAG最长路

#### 11.6.1 两个问题

            - 一、求整个DAG中的最长路径（不固定起点和终点）
            - 二、固定终点，求DAG的最长路径

#### 11.6.2 第一题解决方法

1. **先讨论第一个问题，给定一个DAG，怎样求解整个图里所有路径中权值之和最大的那条？**

2. **解决步骤：**

- 步骤一：令状态dp [i] 表示从i号顶点出发所能到达的最长路径的值，这样dp数组的最大值即为所求
- 步骤二：根据dp[i]的要求我们可以知道有两种情况，如果i号顶点可以得到多个下一个顶点j，则
  - dp[i]=max{dp[j]+length[i->j]}
  - **边界为终点dp[i]=0,即没有下一个顶点**

3. 代码实现(可以逆拓扑排序也可以递归，下面是递归)

```c
int DP(int i){
    if(dp[i]>0) return dp[i];
    for(int j=0;j<n;j++)
      if(G[i][j]!=INF){
          dp[i]=max(dp[i],DP(j)+length[i->j]);
      }
    return dp[i];
}
//如果想存下关键路径，开个choice数组记录每个结点的后继节点。
```

#### 11.6.2 第二题解决方法

1. **固定终点，求DAG的最长路径？**
2. **解决步骤**

- 步骤一：令状态dp [i] 表示从i号顶点出发到达终点T最长路径的值，这样dp数组的最大值即为所求
- 步骤二：根据dp[i]的要求我们可以知道有两种情况，如果i号顶点可以得到多个下一个顶点j，则
  - dp[i]=max{dp[j]+length[i->j]}
  - **边界为终点dp[T]=0,即没有下一个顶点**（在这里可能会有顶点无法到达T，所以这里的初始化dp数组需要赋一个负数-INF,此外还有设置一个vis数组记录顶点是否被计算

3. 代码实现

```c
int DP(int i){
    if(vis[i]) return dp[i];
    vis[i]=true;
    for(int j=0;j<n;j++)
      if(G[i][j]!=INF){
          dp[i]=max(dp[i],DP(j)+length[i->j]);
      }
    return dp[i];
}
```

ps:矩形嵌套问题就是一个比较经典的DP问题

### 11.7背包问题

**是一类经典的动态规划问题———比如———01背包问题和完全背包问题**

#### 11.7.1多阶段动态规划问题

一个问题分为多个阶段，且每个阶段的状态只和上一个阶段的状态有关

#### 11.7.2 01背包问题

1. **问题描述：**有n件物品，每件物品重w[i],价值v[i]。现有容量为V的背包，问如何选取物品放入背包，才能使得背包内物品的总价值最大。其中每种物品都只有一件
2. **解决步骤**

- 步骤一：令状态dp[i] [v] 表示前i件物品恰好装入容量为v时所装入所有物品的价值

- 步骤二：根据dp[i]的要求我们可以知道

  1. 不放入第i件物品，dp[i] [v]=dp[i-1] [v]
  2. 放入第i件物品，dp[i] [v]=dp[i-1] [v-w[i]]+c[i]

  - 因此，状态转移方程dp[i] [v]=max{dp[i-1] [v]，dp[i-1] [v-w[i]]+c[i]}
  - 边界dp[0] [v]=0(前0件物品放入任何容量为v的背包都只能获得价值0)

3. 代码实现

````c
for(int i=1;i<=n;i++){
    for(int v=w[i];v<=V;v++){
        dp[i][v]=max(dp[i-1][v],dp[i-1][v-w[i]]+c[i])
    }
}
````

#### 11.7.3 完全背包问题

1. **问题描述：**有n种物品，每件物品重w[i],价值v[i]。现有容量为V的背包，问如何选取物品放入背包，才能使得背包内物品的总价值最大。其中每种物品都有若干件
2. **解决步骤**

- 步骤一：令状态dp[i] [v] 表示前i件物品恰好装入容量为v时所装入所有物品的价值

- 步骤二：根据dp[i]的要求我们可以知道

  1. 不放入第i件物品，dp[i] [v]=dp[i-1] [v]
  2. 放入第i件物品，dp[i] [v]=dp[i] [v-w[i]]+c[i]

  - 因此，状态转移方程dp[i] [v]=max{dp[i] [v]，dp[i-1] [v-w[i]]+c[i]}
  - 边界dp[0] [v]=0(前0件物品放入任何容量为v的背包都只能获得价值0)

- **区别：**

- **放入i物品时转换的是 ：   dp[i] [v-w[i]]+c[i]**

- **而不是之前的  ：              dp[i-1] [v-w[i]]+c[i]了**

3. 代码实现

````c
for(int i=1;i<=n;i++){
    for(int v=w[i];v<=V;v++){
        dp[i][v]=max(dp[i-1][v],dp[i][v-w[i]]+c[i])
    }
}
````

### 11.8总结

| 名称                      | dp数组含义                                                   |
| ------------------------- | ------------------------------------------------------------ |
| 1.最大连续子序列和        | 令dp[i]表示以A【i】作为结尾的连续序列的最大和                |
| 2.最长不下降子序列（LIS） | 令dp[i] 表示以A【i】作为结尾的最长不下降子序列长度           |
| 3.最长公共子序列（LCS）   | 令dp[i] [j]表示以序列A的i号位和序列B的j号位作为末尾的最长公共子序列的长度 |
| 4.最长回文子串            | 令dp [i] [j]表示A[i]到A[j]是否是回文子串                     |
| 5.数塔DP                  | 令dp [i] [j]表示从i行j列数字出发的到达最底层的所有路径上所能得到的最大和 |
| 6.DAG最长路               | 令dp [i] 表示从i顶点出发能获得的最长路径长度                 |
| 7.01背包                  | 令dp[i] [v] 表示前i件物品恰好装入容量为v时所装入所有物品的最大价值 |
| 8.完全背包                | 令dp[i] [v] 表示前i件物品恰好装入容量为v时所装入所有物品的最大价值 |

1. **先看1~4（一般来说，子序列可以不连续，子串必须连续）**

- **分析共同点可知，当题目和序列或者字符串（记为A）有关是，可以考虑这样设计：**
                         - **令dp[i]表示以A【i】作为结尾（或开头）的XXX**
                             - **令dp [i] [j]表示A[i]到A[j]区间的XXX**
                             - **XXX根据原问题表述更改**

2. **再看5~8，状态设计包含了方向的意思**

- **分析题目中的状态需要几维来表示，然后对其中每一维采取以下表述的其中一个**
              - **恰好为i**
              - **前i**
              - **每一维的含义设置完毕后，dp数组的含义就可以设置成“令dp数组表示恰好为i（或前i）...的XXX，接下来通过端点的特点去考虑状态转移方程。**

## 第十二章 提高：字符串专题

## 第十三章 提高：专题扩展

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        