[TOC]

[TOC]

## C语言

#### C语言语法 

- 请注意c语言的**编译系统**，非常的灵活，并不会严格的帮你控制，你所写代码的内容是否出现错误。因此，写c代码的时候应该**如履薄冰，步步小心**。

#### 关键字

- c语言中一共有32个关键字
  - char ,short , int , long int , long long int
  - const, static 
  - if  ,if..else ,if...elseif,
  - while , do..while  , for
  - free, malloc
  - signed , unsigned
  - switch...case ,break, continue ,default
- 分号很重要，一条语句

#### void

- 作为函数的返回值，如果不使用void作为函数的返回值，这个函数可能会随机整数

- 作为函数的fun(void) //说明函数没有参数，不显示声明就可以传递任何参数

- 定义一个空类型的指针void *ptr;  这个表示可以转换成**任意类型的指针变量**

  - 如**malloc**的原型就是返回一个(void *) 以便申请内存时可以转换成任意类型的内存申请

- 在不使用参数和返回值的时候，一定要显示声明

  ~~~C
  //当不使用void作为参数时，那么test01中的括号就可以写入任意参数
  //因此在c中使用函数时，请明确指定函数的输入和返回类型参数
  void test01()
  {
      printf("hello world\n");
  }
  
  void  test01(void)
  {
      printf("hello world\n");
  }
  int main()
  {
      int a = 10;
      test01(a);
      return 0;
  }
  ~~~



### c变量存储位置

- 只有三个地方，
  - 主存 -- 静态变量，这些变量使用的**内存空间**在编译的时候就被**静态分配完成**，并且在整个程序运行期间不**会被别人使用**。-全局变量 、静态变量
  - 堆栈（主存中一块特殊的区域）后两个地方存储的变量可能是**临时变量**
  - cpu的寄存器中 

####  static 关键字

- c编译器在编译的时候是，**单独c文件编译的**，当你使用别的文件的内容是，你需要**extern**先**告诉编译器**这个东西存在，因此编译的时候就不会报错。但是也不能无中生有，因为在编译完了之后会有链接环节，连接环节找不到所定义的内容依然会报错的。

- c中，全局变量和函数，都是默认（缺省）**static** 意味着
  - 在编译时，内存分配好，且在整个程序的运行过程中，占用**的内存不会被重用**
  - 定义的变量和函数只能在当前文件使用，如果其他文件想使用则需**在文件中加入extern关键字**
- 而当使用static修饰一个变量或者函数时，就是告诉读程序的人，这个变量或者**函数不要被extern到其他文件中使用**。只给当前的文件使用。类似**const**告诉读程序的人，这个变量**只读**，不要去修改他。

#### extern关键字

- 使用**头文件**配合extern来应用其他文件中的**全局变量**和**全局函数**

#### 操作运算符

![](E:\Cplusplus\C语言操作符优先级.png)

- *，++单目运算符的小例子

- ~~~C
     char *p = "357";
        
     for(int i=0; i<3; i++)
     {
         printf("%c\n",*p); //先输出
         *(p++);  //* 作为解引用的时候是和++ -- 同一优先级的 而且是右到左
     }
  ~~~

  

- 

### 通用算数转化

- signed 会 
  - int a = -20;
  - unsigned int b = 6; a + b  此时a就会转换成unsigned  （为啥在我的编译器上没有进行转换呢）

#### 指针

- 指针的概念
  - 指针变量的**值**  -->  **存放的地址**   ==(指针变量的值就是指针--也就是地址，地址就是指针)
  - 指针地址**存放的值** 
  - **存放**这个指针变量的地址

![](E:\Cplusplus\指针示意图.png)

- 指针变量的指向类型
  - int *p -- 则指针变量**指向的类型**就是int （相当于去掉 * p 留下的内容）， 而指针的类型是去掉变量名，也就是int *（整型指针）
  - note:  void * malloc() 返回值是一个空指针类型，也就意味着他可以指向任意个类型的指针，只需要手动进行类型转换即可。
  - **#define NULL  ((void *)0) 将整数0强制转换为一个空指针**
  - #define NUL  '\0' 代表字符串（字符数组）结束   （c语言中是没有字符串类型的）
  - 以下的两个定义都是合法的
    - int *ptr = 0;
    - int *ptr = NULL; //推荐使用
- 指针的算术运算
  - 同类型的指针可以做减法，两个同类型的指针相减的结果是个整数（两个指针的距离  这个指针指向的类型的size） 如 int *a; int *b a-b=1 则a和b差4 * 1个字节
    - Note: 函数名和函数地址是一样的。 都是函数的入口地址
  - 除空类型之外，指针可以做加减操作，int *p;  p+1 、p++等实际走的是object的sizeof
- 指针和字符串
  - c中没有字符串操作，使用字符数组进行操作，以`\0`结尾
  - printf("hello world!"); //编译器会给这个字符串开辟一个**字符常量区**，传入这个函数的参数时字符**首地址**
  - 第一段代码中的字符串可以认为是一个**没有名字**的字符数组，因此你无**法访问和改变**
  - 而第二段代码中不仅存放了字符串数组，还有对应的名称，可以使用指针修改和访问
  - ![](E:\Cplusplus\字符指针.png)
  - 字符指针数组
    - ![](E:\Cplusplus\字符指针数组.png)

#### 函数

- 定义分配内存 int i;  void fun(int a,char * p) ；就是定义，编译器会分配内存给变量和函数
- 声明不分配内存 extern int i;  void fun(int ,char *)（函数原型） 这个和函数就是声明，编译器知道他的存在但是没有给他分配内存
- 函数原型和函数实现最大的不同是函数原型后面跟的是； 而函数实现是花括号
- 函数调用，传值不传地址。只有参数的值传给了被调函数，不会影响原来的值，也就是所谓的值传递

#### c文件链接

![](E:\Cplusplus\C文件链接示意图.png)

- 依赖：
  - 如果所依赖的文件被修改，就需要重新编译这些源文件

####  数组

- 数组名恒等于数组第一个元素取地址
  - int a[10];  则a ==  &a[0]; 
  - 数组名是一个常量const；
  - **int *p; p=a; a++;(这一句错误 数组名是常量不能++) p++没有问题，因为是变量。**
  - 当使用sizeof(a)时  此时a就代表数组 大小就是4*byte * 10 = 40,sizeof(p)=4,因为指针的大小和系统的位数相关32位系统就是 **4** 因为指针就是**地址**

#### 函数的入口参数

- 数组作为**形参**的时候，看上去是数组实际上已经转化成**指针**了（**数组的首地址**），最好不要用数组作为函数的参数的入口，易产生误解

#### 函数指针

- int  *fp(int a); 不是一个函数指针 因为他的函数名是fp(int ) 取内容返回的是一个整数

- int  (* fp)(int a)这是一个函数指针，函数名是(*fp) 所以就是指向函数名的指针

- int * (* fp[10] ( int a)); 的解释**** 

- **函数指针的例子**

- ~~~
  //回头再补吧
  ~~~

- 

- **功能**

  - 多态------一个名字多个接口

    - 多态的例子

    - ~~~C
      //伪代码  使用switch case 实现类似多态功能
      switch(oper)
      {
          case ADD:
              result = add(op1,op2);
              break;
          case SUB:
              result = sub(op1,op2);
              break;
          default:
              break;
      }
      
      //使用函数指针实现
      
      double add(double , double); //声明
      double sub(double, double);
      
      //函数指针 数组里面都是指针 且指针指向相应的函数 
      double (*oper_fun[])(double, double ) = {add,sub...};
      
      //根据想要的操作，使用下标访问相应的函数
      result = oper_fun[oper](op1,op2);
      
      ===============完整的例子==================
      double add(double op1,double op2)
      {
          return op1 + op2;
      }
      
      double sub(double op1,double op2)
      {
          return op1 - op2;
      }
      
      void test05()
      {
          double (*oper_fun[])(double,double) = {add,sub};  //函数指针
      
          double result= 0;
          double op1 = 3;
          double op2 = 2;
      
          result = oper_fun[1](op1,op2);
          printf("%f \n",result);
      }
      
      ~~~

  - callback 回调 下层软件调用上层函数

  - 多任务

#### 指针的经典题目-用变量a给出下面的定义

- 一个整型数（An  integer）
  - int a;
- 一个指向整型数的指针( A pointer to a integer)
  - int *a;
- 一个有10个整型数的数组（An array of integers）
  - int a[10];
- 一个有10个指针的数组，该指针是指向一个整型数的（An array of 10 pointers to integers）
  - int *a[10]; 
- 一个指向有10个整型数的数组指针（A pointer to an array of integers）
  - int (*a)[10];
- 一个指向函数的指针，该函数有一个整型参数和一个整型数（A pointer to a function that takes an integers an argument and returns an integer）
  - int (*a)(int )
- 一个有10个指针的数组，该指针指向一个函数，该函数有一个整型参数并且返回一个整型数（An array of ten pointers to function that takes an integer as an argument and return an integer）
  - int (*a[10]) (int )

#### 循环展开

#### 循环展开

- 将少量的循环直接展开 翻译成汇编的代码**要少**

#### 局部变量存放

- 只有两个地方存放局部变量 (因此，在开辟局部变量空间的时候要格外注意)
  - **寄存器**
  - **堆栈中**

#### 堆栈的作用

- 传递参数
- 保存返回值的**地址** 和**程序状态字**
- 保存调用函数已经使用过**寄存器**
- 保存能使用到的**局部变量**

#### 栈帧

- 一次函数传递就是一个会生成一个栈帧

- 栈帧的四个部分：参数传递、返回地址、保存的寄存器、局部变量
- 考虑调用**深度**时的**堆栈溢出**

####  内存的申请和释放

- 问题

  -  申请一块空间，并且将**指针**的**地址**返还给调用者

- 内存分配的时候是根据系统维护的空闲链表去寻找大小合适的内存块。被申请过得内存块是不在**free list**里面的 ，但是在释放后会**插入**到空闲列表里面

- free list的本质就是**单向循环队列（链表）构成的一个环**

- 内存分配和释放的策略

  - 使用粒度进行分配，一个粒度可能是8个字节，作为最小的分配单元，有利于做合并和管理
  - 当找到一个可用内存块时，总是从其**高地址**开始分配内存
  - 分配好的内存块的**头地址 总是指向自己的**，方便在做free的时候释放的是本块的内存
  - 总是试图将被释放的块 相邻之间进行**合并**，避免内存碎片
  - free list中的每一块内存的第一个blk的指针都是指向自己，以便free在释放空间的时候进行判断。因此，如果进行free的时候，这块空间指向自己的内存被其他操作重用了，那么这块内存就不能被释放，因此会造成**内存泄漏**。

- 内存分配base block 的定义

  - ~~~c
    union header   // union 是个大盒子 只能装成员变量中的一种要么是struct 要么是c
    {
        struct 
        {
            union header *prt;  //头部指针 用于释放时定位的
            unsigned long size;
        }s;
        char c[8];
        
    };
    typedef union header HEADER   //定义一个用户自定义的类型  套路写法
    ~~~

    

  - 系统关闭任务调度之后，进入临界区之后，下面的代码是不能被打断的。

- 内存释放的例子

  ~~~C
  void FreeMemo(char * ptr)
  {
      char *p;
      int i;
      if(prt == NULL)return ;//入口参数合法性检查
      if((p=(char *)malloc(1024))==NULL)  //内存申请失败时，返回的是NULL
          return; //申请空间，并且检查合法性
      
      for(int i=0; i<1024; i++)
      {
          *p++ = *prt++;//*作为解引用的时候和++是统一优先级，而这种单目运算符是从右到左计算的
      }
      free(p); //无效释放  //因为p的位置已经发生变化 头部的q指针已经发生了变化
      return; 
  }
  ~~~

#### 中断和驱动

- 中断
  - 操作系统的入口就是**中断**
- 可重入  （信号量  锁 自旋锁来避免）
  - 由中断引起的重入
  - 由于任务切换而引起的重入  （关调度  防止重入）
  - 由于递归引起的重入 （所有的重入都是类似递归，一个函数还没有执行完又再次调用这个函数）
- 函数可重入的安全条件
  - 当代码访问临界资源的时候没有被互斥保护，那么就是不安全重入的

#### NULL

- NULL --> #define NULL (void *) (0x0)
- NUL -->  相当于是 ’\0‘
- 0x0 就是16进制的0

#### 头文件的重复引用的检查

~~~C
避免都头文件重复引用 
#ifndef _SAMPLE_H   SAMPLE就是头文件的名字 习惯在前面加“—”
#define _SAMPLE_H

......

#endif   //
~~~

#### 命名规则

- 宏定义
  - 全部都大写 名称可以加下划线 #define STUDENT_NUM 10
- 全局函数和全局变量
  - 动宾结合 或者动词短语 不使用下划线首字母大写 CreateWindow
- 局部函数和局部变量
  - 动宾，名词短语，一般缩写 有下划线，全小写，保留辅音字母

### 程序书写、调试

- 在c语言中，出问题的哪一行代码可能不是造成问题的代码。造成这一行出问题的代码可能在很遥远的地方

- bug的定位
  - 关注接口，参数的传入和函数的返回值
  - 对软件的层次要清晰，
- 关注堆栈的申请和释放
  - 堆栈的溢出   冲掉了其他任务使用的堆栈
    - 可能冲掉其他位置的数据，现象为其他数据莫名其妙的被修改
    - 局部变量不要开大的数据 ，因为**局部变量**是存放到**堆栈**中的，而程序的堆往往比较小。
- 堆栈缓冲区溢出
  - C语言对数组的越界是不做检查的，因此使用数组时应格外注意数组的使用
- 全局变量和动态变量的数据溢出
- Note：一定要关注**寄存器**和**存储器** 才能竟可能少犯错

#### 递归的坏处

- 占用**堆栈**空间
- 效率不高

#### 语言基础规则

- **谨慎使用**goto语句
  - 只有在使用goto时能让代码变的可读性更强且goto只能出来不能进去且goto最好都到一个地方
- 不要修补那些风格差的代码，重写他们
- 不要比较两个浮点数是否相等
- 优化或者调试一些旧版本的代码时，注意要备份他们
- 将编译器设置为最高警告水平，将每一个警告当做错误来处理，如果处理不了应该对其进行说明
- 不要再程序中直接使用常量，应该使用宏定义（有助于代码的可读性、可扩展性）
- 避免#include的文件没有被使用，就不应该包含进来
- 避免同一c文件重复引用同一个头文件
- 虽然全局变量默认已经是static了，但是为了能够显示告诉读者这个全局变量不要被extern所以应该加static关键字
- 若进行赋值时，两边的数据类型不一样，应该显示的进行转换（易读）
- 不要删除switch..case中的break语句，除非相连的case处理的代码需要进行连续，且都要进行处理
- **变量**
  - 每个变量都应该进行说明，且说明要和变量声明相邻
  - 尽可能在变量说明行中，将变量进行初始化
  - 尽量避免全局变量，容易出现问题
  - 当一个变量只进行读时，应使用const进行说明
- 依赖关系
  - 尽量少使用全局变量，当仅限一个c文件使用时应显示使用static修饰
  - 函数间的参数传递越少越好，模块间的耦合性越低越好
  - 对一组在逻辑上相关的参数，应该封装到struct中

#### 程序中需要考虑的数组边界问题

- 数组的上限
- 循环次数
- 链表在头部、尾部进行插入或者删除一个节点时，特殊情况的处理，一定要清晰，不然易错
- 要**注意判断输入参数**的极限情况

#### 堆栈缓冲区溢出错误

- 现象
  - 某些局部变量，莫名被修改
  - 函数返回时程序出现崩溃
- 主要原因（本质就是，某些**数据的内存**被其他程序运行时**重用**导致错误）
  - 临时数组越界 （**如图**）
  - 注意**strcpy**(),**sprintf**(),**memcpy**()函数的目的缓冲区是否越界。
  - **strcpy**()函数原字符串是否已“\0”正常结束
  - **memcpy**()的拷贝数是否正常

![](E:\Cplusplus\堆栈图.png)

#### 关于动态内存

- 在分配动态内存时，总是先要检查动态内存分配是否成功后，再引用指针。
- 在分配struct空间时，应该使用sizeof操作符
- 分配内存空间是，宁缺毋滥，在进行计算时别忘记+1
- 总是要free 由malloc函数返回的指针
- 错误处理时，不要忘记释放其他已分配的内存

#### 关于临时变量

- 不要对临时变量进行取址操作，因为临时变量可能是在寄存器里面的。这样很危险。临时变量指存放在堆栈和寄存器中。
- 函数不要返回临时变量的地址，或临时指针变量，因为堆栈中的内容是不确定的，可能这个函数执行完之后，这块内存就被其他程序使用了。（因为出了这个函数，存放在堆栈中的临时变量就没有意义了）
- 不要再函数中申请大的临时数组，因为他会存放到你的堆栈中，堆栈本身就不会很大。

#### 关于bug的修正

- 别着急改，先想想，再想想，想清楚然后再改，修改是要做好记录。
- 考虑每一次修改后，对系统会造成什么样的影响
- 我的修改会对其他人的代码造成什么样的影响
- 当对全局的变量、函数、数据结构做修改时，思考如何通知其他开发者，避免使用时出现问题
- 修改后，应有相应的注释，并且做回归测试

## C/CPP提高-->(WBM)  

- **一次偶然的成功，比必然的失败更可怕**
- 从**编译器**的角度思考问题、代码、流程

#### 要求

- 对资料进行时间和空间的管理、积累、记录
- 每个事物的认知都是有规律的，需要的是时间。
- 要关注所有的文件信息

#### 形参

- 写在**函数括号里面**和写在**函数里面的变量，**从c++/c编译器来说是没有任何区别的。只不过写在**括号里**面的具有**对外使用**的属性

- ~~~~C
  void init(int a,int b[10])
  {}
  void init()
  {
  int a;
  int b[10];
  }
  ~~~~

- 

#### 数据类型

- 分两种

  - 简单数据类型   int short ......
  - 复杂数据类型  struct、数组、、、、
  - 指针数据类型

- 数据类型的本质是**固定大小的内存**的**别名**

  - ~~~C
    int a; //告诉编译器，分配一个int行大小的内存给a（作用）  就是一个内存的别名
    ~~~

- 变量本质：一段连续内存空间的**标号**

  - 修改内存中数值的两种方法 如int a;

    - 使用这个内存分配时的变量名，也就是a = 10;。 直接修改

    - 得到这一块内存的地址，int *p=&a; p = 10; 即可。 间接修改 或者 *** ((int * ) &a) = 12;** 也是可以修改的

    - c++中的引用&，也是一块内存的别名 多用于对象复杂的数据结构。

    - 总结：1.对内存可读可写。2，通过变量向内存中读写数据，3.是向变量对应的内存中读写，不是向变量中读写。4.**变量放在代码区**

    - ~~~c
      int main()
      {
          int a;
          a = 10;
          printf("%d \n",a);  //10
          printf("%d \n",&a); //得到a的变量的地址 也就是标号  6356748
          //通过这个内存标号去修改这个变量的值
          //&a = 6356748; a取址 = 6356748;
          //解引用这个内存存放的地址，然后对地址再解引用得到内存的值，直接进行修改，间接修改
          *((int *)6356748) = 20; 
          /* //相当于使用了一个指针
          int *p 
          p = &a;
          *p = 30;
          printf("%d \n",a);
          */
          printf("%d \n",a);  //20
          return 0;
      }
      ~~~

    - 

- ~~~c
  int a[10];
  printf("a = %d,&a = %d",a,&a); //此时的值是一样的
  //前者是加了4个字节 后者加了10*4个字节  
  //本质是因为数据类型不一样
  //a的本质是数组首元素的地址 而对a取地址就表示整个数组的地址
  printf("a = %d,&a = %d",a+1,&a+1); //此时的值是不一样的
  ~~~

#### void 作用（万能类型）

- 作为参数时表示不需要传入任何形参
- （void*）表示无类型指针，可以**指向任何数据类型**
- 数据类型的封装，只给使用者提供一个地址不告诉使用者具体的实现细节（断层的思想）
- void没有定义内存的大小



### 内存四区

![](E:\Cplusplus\Cplusplus\四区.png)

- 指针指向谁，就把谁的地址赋给指针
- 指针变量和它所指向的内存空间变量里面是两个不同的变量。
- 没有内存就没有指针---**学习指针的关键是掌握内存的分配**
- 调用函数里面申请的空间想传递给其他函数使用，有两种方法
  - 使用return返回值
  - 使用指针参数
- **规则1：主调用函数分配的内存（堆、栈、全局区），可以被住调用函数里面被调用的函数使用。**
- **规则2：而被调用函数分配的内存，只有分配到堆、全局区，才能被其他主函数调用、stack区的函数是不能调用的**
- 申请堆时，注意释放。不然容易出现内存泄漏。
- 在内存分配的时候栈区和堆区的方向可能是不一样的，但是数据的存储方向始终是一致的

~~~c
char *getstr1()
{
    char *p = "abc";  //左边放在栈区，右边放到全局区
    return p;
}
char *getstr2()
{
    char *p1 = "abc";  //分配到全局区 可以被这个函数以外的函数访问这个内存空间
    return p1;
}
//不能正常返回
char *getstr3()
{
    char buf[100];  //不能作为地址返回，因为buf是分配到栈里面的
    memset(buf,0,sizeof(buf));
    strcpy(buf,"abc");
    return buf;
}
int main()
{
    printf("s1 = %s\n",getstr1());
    printf("s2 = %s\n",getstr2());
    printf("a1 = %d\n",getstr1());  //4206628
    printf("a2 = %d\n",getstr2());  //4206628
    
    //printf("getstr3: %s\n",getstr3());  //是不能正常返回的  输出getstr3: (null)
    system("pause");
    return 0;
}


~~~

### 经验话语

1. c和java的最大区别，在内存分配时，c语言可以在**栈区（临时区）分配内存**，而java则不行。

2. 给指针变量**不断的赋值**就是不断的修改**指针的指向**。在申请和释放内存的时候，注意使用指针修改内存里的内容时，应该先保存头指针，以便后面使用free释放

3. int  a[10]; **a-->数组首元素地址-->a常量指针（不能被改变）** --> 因为会出现在内存释放的时候要用到每一块内存的头结点里面的东西进行释放，为了避免内存释放失败c++编译器，不允许直接a++的操作。可以使用int *p =a;p++的操作来遍历内存中的数值

4. 概念不清晰和概念清晰但是训练不到位都是产生bug的根源，因此需要做到**概念清晰，训练到位**，**训练到极致**

5. malloc内存时如果存放的是字符串，而是通过strlen确定长度的，一定在malloc申请内存的时候增加1，不然容易冲刷掉其他内存

   1. ~~~c
      char *p = (char *)malloc(strlen("abc")); //并没有申请到'\0'这个结束符的内存
      char *p =(char *)malloc(strlen("abc")+1);
      strcpy(p,"abc"); //会出现错误
      ~~~

6. 要深入理解各种语法现象

7. ->和.操作只是获得相对于结构体的偏移地址 a->name a.age在cpu中运行，并没有操作内存，只有用=时才操作指针

#### 经典程序推演

~~~c
//字符串指针复制的推演过程
int copyStr1(char *from ,char *to)
{
    char *p1 = from;
    char *p2 = to;
    int ret = 0;

    if(p1 == NULL || p2 == NULL)
    {
        ret = -1;
        printf("func copyStr1 is err: %d\n",ret);
        return ret;
    }

    for(; *p1!='\0'; p1++,p2++)
    {
        *p2 = *p1;
    }
    *p2 = '\0';
     return ret;
}

int copyStr2(char *from ,char *to)
{
    char *p1 = from;
    char *p2 = to;
    int ret = 0;

    if(p1 == NULL || p2 == NULL)
    {
        ret = -1;
        printf("func copyStr1 is err: %d\n",ret);
        return ret;
    }
    while(*p1!='\0')
    {
        *p2++ = *p1++;
    }
    *p2 = '\0';
     return ret;
}

int copyStr3(char *from ,char *to)
{
    char *p1 = from;
    char *p2 = to;
    int ret = 0;

    if(p1 == NULL || p2 == NULL)
    {
        ret = -1;
        printf("func copyStr1 is err: %d\n",ret);
        return ret;
    }

    while((*p2++ = *p1++)!='\0');
    return ret;
}
~~~



~~~c
//去除字符串两端的空格
//注意的点：1. 操作字符数组时，注意是不是'\0'结尾。2.输入in指针，注意是不是可修改的内存，最好自己
int trimSpaceStr(char *p1,char *p2)
{
    char *s1 = p1;
    char *s2 = p2;
    int ret = 0;
    int i = 0;
    int j = strlen(p1)-1;
    int n = 0;
    if(s1 == NULL || s2 == NULL)
    {
        ret = -1;
        printf("func trimSpaceStr is err: %d\n",ret);
        return ret;
    }
    //左
    while(isspace(s1[i]) && s1[i]!='\0')i++;
    //右
    while(isspace(s1[j]) && j>0)j--;
    //找到i和j
    n = j - i + 1; //字符串的长度

    strncpy(s2,s1+i,n); //将s1拷贝到s2里面去，这里是加上可'\0'了,没有加上'0';

    *(s2 + n) = '\0';
    printf("s2.len = %d\n",n);

    return ret;
}

//一种不好的做法
//只用一个p重复复制到原来p指向的空间
//但是使用这种方法要注意，对于传入in指针指向的内存要能修改才可以 若不能修改则出现问题
int trimSpaceStr2(char *p)
{
    int ret = 0;
    int i = 0;
    int j = strlen(p)-1;
    int n = 0;
    if(p == NULL)
    {
        ret = -1;
        printf("func trimSpaceStr is err: %d\n",ret);
        return ret;
    }
    //左
    while(isspace(p[i]) && p[i]!='\0')i++;
    //右
    while(isspace(p[j]) && j>0)j--;
    //找到i和j
    n = j - i + 1; //字符串的长度

    strncpy(p,p+i,n); //将s1拷贝到s2里面去，这里是加上可'\0'了,没有加上'0';

    *(p + n) = '\0';
    printf("s2.len = %d\n",n);

    return ret;
}
int main(void)
{
    char buf1[] = "   abcd   ";
   {
        //写在这里面就相当于是局部变量
        char buf2[1024];  //这个要比memset速度快，这样在接收字符串的时候就可以不用自己添加'\0'了
        //char buf2[1024] = {0}; //是一种偷懒的行为，这样初始化之后，就只会覆盖'\0'里面的数值了
        //memset(buf2,0,sizeof(buf2));
        trimSpaceStr(buf1,buf2);
        printf("buf2 = %s\n",buf2);
   }
   {
        trimSpaceStr2(buf1);//而buf1中的内容是拷贝了一份到栈中的 是可以修改，且可以直接进行输出的
        printf("buf1 = %s\n",buf1);

        char *p = "   abcd   "; //p指向的是全局区，所以使用trimSpaceStr2修改全局区是不允许的
        trimSpaceStr2(p);  //能够编译通过 但是运行就不行 因为他修改的是全局区中的内容，肯定是不行的
        printf("p = %s\n",p);
   }
    return 0;
}
~~~



~~~c
//子串查找
int getSubstrCount(char *src,char *sub,int *count)
{
    char  *p1 = src;
    char *p2 = sub;  //定义临时变量接收，是最好的结果，因为可能后期使用时不易出错，修改是页方便
    int ret = 0;
    int n = 0;


    if(p1 == NULL || p2 == NULL)
    {
        ret = -1;
        return ret;
    }
    do
    {
        p1 = strstr(p1,p2);
        if(p1 == NULL)
        {
            break;
        }
        p1 = p1 + strlen(p2);
        n ++;
        //*count++; //由于优先级的原因只是对地址进行了++,要注意这种现象 （*count）++; //这样也可以

    }while(p1!='\0');
    *count = n;
    return ret;
}

int main(void)
{
    char *p1 = "abcd2312312abcd444abcd31235";
    int num = 0;
    char *p2 = "abcd";
    int ret = 0;
    ret = getSubstrCount(p1,p2,&num);
    if(ret != 0)
    {
        printf("func getSubstrCount  is err: %d \n",ret);
        exit(1);
    }
    printf("num = %d\n",num);
    return 0;
}

~~~



### 指针铁律一

- 指针是一种**数据类型**，这个数据类型就是其**指向的内存空间分配时的数据类型**

- 指针也是一个变量，用来保存地址的 指针==地址
- 1.使用变量对内存直接进行读写操作
  - int a; a= 10;
- 2.使用指针间接对内存进行读写操作
  - int *p; int a; p = &a; *p = 10; 
  - *(谁的地址)就是间接对其对应的内存进行读写操作
  - *p在**左边**是写内存，  *p放在等号的**右边**是读内存
- 3.指针变量和他指向的内存空间不一样，例如，int a = 10; int *p =  &a; 
  - 有以下几个含义
  - p = 0x5511；只是改变了指针变量的值，完全不会影响指针所指的内存里的数值
  - 给*p赋值只会改变指针指向内存的值，不会改变指针变量的值
  - *p在=**左边**是写内存，  *p放在=的**右边**是读内存
- 4.指针是一种**数据类型**，这个数据类型就是其**指向的内存空间分配时的数据类型**
  - int *p; 执行的数据类型就是int 则**步长**就是sizeof(int);
- 5.指针就是一个存放4个字节地址的变量，啥也不是 ，不过是几个字节
  - 站在c++/c语言的编译器去看指针，指针就是一个变量，就是一个存放地址的变量，可能4或者8个字节
  - 当c++编译器看到**一个**  ‘  * ’的时候就认为他是指针，就会分配4或者8个字节
  - 当我们使用的时候，采取考虑指针指向的内容是几维的
  - 永远记住：c语言规定**数组名**代表**数组首元素**的地址，如果对数组取地址&，就代表整个数组
- 6.使用*p作为参数，在被调函数里面使用这个指针修改内存时，一定要保证指向的内存能够修改。比如指针指向常量区（全局区），修改其空间内的数据时，是不允许的，程序会出现错误。**不要轻易改变指针输入特性中in内存块的内存...** ，一般不修改

### 指针铁律二

- 指针的间接赋值，也就是不传入特点参数，直接通过**指针间接进行赋值**。指针的最大意义就是**间接赋值**
  1. 定义实参、形参
  2. 建立实参和形参之间的关联，将实参的地址赋值给形参
  3. 形参间接的去修改实参的地址
  4. 三个条件的组合
     1. 123在一个函数
     2. 1 23在一个函数
     3. 12在一个函数 3   主要还是理解内存的分配
- 应用场景
  1. 一个函数内修改内存的值
  2. 在两个函数之间修改一个内存里的值
- 指针间接修改内存的值
  - 1级指针可以修改0级指针的值
    - int a; int *p = &a; *p = 1;
  - 2级指针可以修改1级指针的值。。。。。依次类推

~~~c
void getLen(int *p)
{
    *p = 200; //3.形参间接修改实参变量的值
}
void test06(void)
{
    int a;  //1.定义一个变量--通常是实参
    a = 10;  //通过内存别名，变量改变内存数据
    printf("直接改变a = %d \n", a);
    int *p;   //1.定义一个变量通常是实参
    p = &a;    //2.建立关联
    *p = 100;  //通过地址改变
    printf("间接改变和访问*p = %d \n", a);
    getLen(&a); //通过实参取地址传入 
    printf("函数调用后a = %d \n", a);
}
~~~

- **下面的特别重要**

  - 多级指针做函数参数的时候，不管是一个* 还是8个*我们只需要知道编译器只给他跟配4个字节的内存即可。只有在使用的时候才去关心内容是什么

- 通过二级指针修改一级指针，申请内存并且作为输出，四区图看process

- ~~~C
  //p2就是一个变量 他来接收实参的地址
  //如果实参是0级 就用1级 如果是1级就用二级
  //*就是一把钥匙
  int getMem22(char **p2)
  {
      *p2 = 200; //
      *p2 = (char *)malloc(100); //申请一个内存并将这个内存的地址分配给p2
      return 0;
  }
  
  char **getMem();//也行 但是不好，占用了函数返回状态
  void main(void)
  {
      //一级指针变量的值 需要用二级指针变量来修改
      char *p = NULL;
      //直接修改p的值 p是指针所以是存放的值的意义就是地址
      p = 0x1;
      p = 0x2;
      printf("%d\n",p);
      getMem22(&p);
      printf("%d\n",p);
      system("pause");
  }
  ~~~

- 通过三级指针修改二级指针，并申请二级内存作为输出，四区图看process
  
- ~~~c
  //通过三级指针修改二级指针
  int modifyP(char ***p3)
  {
      int i=0;
      *p3 = 200;
      char **temp = (char **)malloc(10 *sizeof(char*));
      memset(temp,0,10*sizeof(char*));
      for(i=0; i<3; i++)
      {
          temp[i] = (char *)malloc(100);
      }
  
      *p3 = temp;
      return 0;
  }
  
  void main(void)
  {
      char **p2 = NULL;
      char ***p3= NULL;
      //
      p2 = 1;
      p2 = 3;
      printf("p2: %d \n",p2);
      p3 = &p2;  //通过p3间接修改
      *p3 = 100;
      printf("p2: %d\n",p2);
  
      modifyP(&p2);
      printf("p2: %d\n",p2);
  }
  ~~~
  
- 
  
- c++编译器编译数组数组访问的技术推演
  
  - int a[10]; 使用下标访问就是利于理解
  - a[10] --> a[0+i]-->a(0+i)-->*(a+i)  //

### 指针铁律三

- 主调函数、被调函数
  - 主调函数可以将其分配的堆区、栈区、全局区作为参数传递给被调函数。
  - 被调函数只能返回堆区、全局区的数据
- 内存分配方式
  - 指针作为形参时，是具有输入、输出特性的
- 要求自己
  - 即使是简单的业务模型也要去训练抽象的思想，就类似java一样
- 看函数声明时，一定要想的事，特别是指针作为参数时
  - int copyStr2(char *from ,char *to，int *len)
    - 参数是由主调函数传入，则主调函数是不是应该分**配内存空间**
    - 主调函数分配的内存空间的生命周期是否在被调函数未完成前被占用或者释放
    - 被调函数接收到的参数，要进行判断是否正确
    - 参数中那几个是**传入参数**，那几个是**需要返回的参数**。如from，to均是传入参数。len则可能是需要返回的参数，也就是在给调函数里面进程逻辑处理之后的处理结果通过地址修改，**传给主调函数**。为什么不用返回值，因为，**返回值**只能有**一个参数**，而**返回参数可能是多个**，**为啥不用数组呢？？**  数组的使用最后也是退化成**指针**
- 数组指针的规定：
  - **int a[10];  sizeof(a) == 40个字节 4*10 这是规定，不用去理解**
  - **而sizeof(&a) = 4;//首元素的地址**
  - **C语言规定&a代表整个数组，而&a+1 跳40个单元 这是规定** 

### const专题

- **const**定义的变量，为了**明确**表示的是调用者只能够对这个变量或者对象进行读操作。

- ~~~c
  //两者意义完全相同
  char const a;
  const char a;
  char * const p; //表示地址变量的内容不能被改变，也就是指向不能被改变，但指向的内容可以被改变
  char const * p; //表示指针指向的内容不能被改变，指针可以改变
  const char const * p; //指向和指向的内容均不能被改变
  //表示指针指向的内容不能被改变，指针可以改变
  int get1(const char *p)
  {
      p[0] = 1;//错误正确
      p=0x01;
      return 0;
  }
  //表示地址变量的内容不能被改变，也就是指向不能被改变，但指向的内容可以被改变
  int get2(char * const p)
  {
      p[0] = 5; //正确
      p = 0x02; //错误
      return 0;
  }
  //指向和指向的内容均不能被改变
  int get2(char * const p)
  {
      p[0] = 5; //错误
      p = 0x02; //错误
      return 0;
  }
  int main(void)
  {
      return 0;
  }
  
  ~~~
  

### 二级指针

- **一个入口多个出口时，内存释放的方法**

  ~~~c
  1.//在每一个出口前，将申请的内存空间进行释放
  
  int main(void)
  {
  	int ret = 0;
  	....
  	char *p1 = getMem(10);
  	...
  	if(ret != 0)
  	{
  		free(p1);
  		return -1;
  	}
  	
  	char *p2 = getMem(20);
  	
  	if(ret != 0)
  	{
  		free(p1);
  		free(p2);
  		return -1;  //出口
  	}
  	
  	free(p1);
  	free(p2);
  	return 0;
  }
  2.//当内存释放过于繁琐的时候可以使用goto ，使用goto一定是要出口，不能作为进入
  int main(void)
  {
  	int ret = 0;
  	....
  	char *p1 = getMem(10);
  	...
  	if(ret != 0)
  	{
  		goto End;
  	}
  	char *p2 = getMem(20);
  	if(ret != 0)
  	{
  		goto End;
  	}
     End:
      if(p1!=NULL)
  		free(p1);
      if(p2 != NULL)
  		free(p2);
  	return 0;
  }
  ~~~

  

- 二级指针的三种内存模型

- ~~~c
      int i=0;
      //二级指针的三种内存模型
      //1.数组指针
      char * p1[] = {"123","456","789"};
      //2.二维数组
      char p2[3][3] = {"abc","def","hij"}; 
      //3.手工的二级指针
      char **p3 = (char **)malloc(3*sizeof(char *));
      
      for(i=0; i<3; i++)
      { 
          p3[i] = (char *)malloc(10*sizeof(char));
      }
      return 0;
  ~~~

- ![](E:\Cplusplus\Cplusplus\二级指针模型图.png)

- 二级指针第一种模型和第三种模型的程序对比

  ~~~c
  #include <stdlib.h>
  #include <stdio.h>
  #include <string.h>
  //交换变量对应的内容时有两种方法
  //1.更改变量的指向 2.直接更改变量指向的内存里面的内容
  //分配堆内存
  char **getMemory(int num)
  {
      int i=0;
      //内存中存放的还是地址
      char **temp = (char **)malloc(num * sizeof(char *));
      for(i=0; i<num; i++)
      {
          temp[i] = (char *)malloc(100); //每个分配100个字节
      }
  
      return temp; //由于是在堆中申请的 因此可以返回给主调函数使用
  }
  //在申请内存的是时候多申请一个，在处理这个内存的时候可以不用传长度的
  char **getMemory01(int num)
  {
      int i=0;
      char **tep = (char **)malloc((num+1) * sizeof(char *));
      for(i=0; i<num; i++)
      {
          tep[i] = (char *)malloc(100);
      }
      tep[num] = '\0'; //结束符
  //    tep[num] = NULL;
  //    tep[num] = 0;
      return tep;
  }
  
  void sortArray03(char **myArray)
  {
      int i=0,j=0;
      char *p;
      for(i=0;myArray[i]!='\0'; i++ )
      {
          for(j=i+1;myArray[j]!='\0' ; j++)
          {
              if(strcmp(myArray[i],myArray[j])>0)
              {
                  p = myArray[i];
                  myArray[i] = myArray[j];
                  myArray[j] = p;
              }
          }
      }
  }
  int testNoLen(void)
  {
      int i=0;
      char **p = NULL;
      p = getMemory01(3);  //这里多申请了一个存放结束符的内存，如果不申请，程序运行的时候直接挂掉
      strcpy(p[0],"bbb");
      strcpy(p[1],"ccc");
      strcpy(p[2],"aaa");
      for(i=0; i<3; i++)
      {
          printf("%s\n",p[i]);
      }
  
      printf("=====================\n");
      sortArray03(p);
      for(i=0; i<3; i++)
      {
          printf("%s\n",p[i]);
      }
      return 0;
  
  }
  void sortArray(char **myArray,int num)
  {
      int i=0,j=0;
      char *temp;
      for(i=0; i<num; i++)
      {
          for(j=i+1; j<num; j++)
          {
              //直接更改指针的指向
              if(strcmp(myArray[i],myArray[j])>0)
              {
                  temp = myArray[i];
                  myArray[i] = myArray[j];
                  myArray[j] = temp;
              }
          }
      }
  }
  void sortArray02(char **myArray,int num)
  {
      char temp[200];
      int i=0,j=0;
      for(i=0; i<num; i++)
      {
          for(j=i+1; j<num; j++)
          {
              if(strcmp(myArray[i],myArray[j])>0)
              {
                  //直接操作内存
                  strcpy(temp,myArray[i]);
                  strcpy(myArray[i],myArray[j]);
                  strcpy(myArray[j],temp);
              }
          }
      }
  }
  int test02(void)
  {
      char **p = NULL;
      int i=0;
      p = getMemory(3); //申请内存
      strcpy(p[0],"bbbb");
      strcpy(p[1],"aaaa");
      strcpy(p[2],"cccc");
  
      printf("before: \n");
      for(i=0; i<3; i++)
      {
          printf("%s \n",p[i]);
      }
  
      sortArray02 (p,3);
      printf("after: \n");
      for(i=0; i<3; i++)
      {
          printf("%s \n",p[i]);
      }
      //释放内存
      for(i=0; i<0; i++)
      {
          free(p[i]);
      }
      free(p);
      return 0;
  }
  int main(void)
  {
      printf("二级指针1和3模型的比较\n");
      test02();
      //testNoLen();
      return 0;
  }
  
  ~~~

  

### 指针的本质

- 数组最终在做参数或者访问内存的时候依然是会退化到指针的表现形式的。这是c编译器自己做的事。

- **一维数组的本质**

  - int a[10];  //a表示数组首元素的地址
  - 且a的类型是 int *,也就是指向int 的指针

- 二维数组的本质

  - int a[4] [5];  //a表示首行的地址，类型为int (*)[5]  指向一个5个元素的数组
  - a[0] [0] //其实和a是地址是一样的 但是表达的意思不一样
  - a[0] //得到的是列元素的地址 也就是0行的第0个元素的地址

- **二级指针和数组作为函数参数的技术推演**

  - ~~~c
    int a[3][10];
    a[i][j] ===> *(*(a+i)+j)
    a-->相当于二维数组的首行数组的地址，对于一维数组相当于是首元素的地址
    a+i --->表示第i行的数组的地址
    *(a+i) --->表示第i行数组第0个元素的地址
    *(a+i)+j--->表示第i行数组第j个元素的地址
    *(*(a+i)+j)--->第i行第j列元素的值
    
    //二维数组的退化
    int fun1(char arr[3][5]);
    int fun1(char arr[][5]);
    int fun1(char (*arr)[5]);  //使用数组指针
    
    //多维数组的存储也是连续的 只要知道首行0列元素的地址就可以得到后面的所有元素
    
    //指针数组的推演过程
    void fun2(char *p[3]);  //编译器只是需要分配4个字节即可 ，你怎么用并不关心
    void fun2(char *p[]);
    void fun2(char **p);
    ~~~

- **多维数组作为函数参数时，做多只能表达到二维。如果是三维的就没有意义了**。

- 如果有超过三级以及三级以上的指针，则不代表几维的内存了，

- 指针数组的应用场景

  - 做菜单
  - 做命令行

- main中形参指针传入的时候是不传入长度的

  - ~~~c
    int main(void)
    {
        printf("指针混合练习\n");
        //不传入长度，就需要对传入的字符串参数进行特殊的处理
        char *p[]={"123","456","678",NULL}; //在末尾加入NULL,0,'\0'之后不需要加入长度
        int i=0;
        for(i=0; p[i]!=NULL; i++)  //这里NULL 0 '\0'注意使用替换
        {
            printf("%s\n",p[i]);
        }
        return 0;
    }
    ~~~

### 野指针产生的原因和避免的方法（三个步骤）

- 一级指针与野指针问题和避免

  - 定义指针变量时，将其复制为NULL
  - 释放指针指向的内存时，将其复制为NULL或者重新为其他的
  - 

- 二级指针与野指针问题和避免

  - 和一级指针一样

- 释放内存使用函数调用的问题

  - 当想通过调用函数释放主调函数中指针的内存时，虽然指向的指针内存释放了，但是这个指针依然指向这个位置的内存，这个指针在下次判断释放时，不能有作用，具体代码如下

  - ~~~c
    #include <string.h>
    #include <stdio.h>
    #include <stdlib.h>
    //1.定义指针时，现将其指向NULL
    //2.申请内存之后，先判断是否申请成功在使用
    //3.释放内存先判断，释放之后让其为NULL;
    
    //可以成功申请内存
    char *getM1(int num)
    {
        char *tmp = NULL;
        tmp = (char *)malloc(100);
        return tmp;
    }
    
    //不利用返回 利用指针作为参数的应用场景
    void getM2(int count , char *p)  //思考内存场景就能知道
    {
        char *tmp = NULL;
        tmp = (char *)malloc(100);
        p = tmp;  //其实并没有改变实参 也就接收这个函数的指针依然是NULL
    }
    
    //使用指针间接赋值
    void getM3(int count , char **p)
    {
        char *tmp = NULL;
        tmp = (char *)malloc(100);
        *p = tmp; //直接通过地址间接修改实参的值
    }
    
    //释放内存
    void freeM(char *p)
    {
        if(p != NULL)
        {
            free(p); // 只是释放了实参和形参指向的同一个内存块的内存
            p = NULL; //这里并不能让实参的值为NULL
        }
    }
    int main(void)
    {
        /*
        char *p = NULL;
        p = (char *)malloc(100);
        free(p);
        p = NULL;
        */
        char *p = NULL;
        getM2(10,p); //p作为实参依然是NULL
        if(p == NULL)
        {
            printf("p == NULL\n");
        }
    
        getM3(10,&p);
        strcpy(p,"123");
    
        printf("%s\n",p);
        if(p==NULL)
        {
            printf("p == NULL\n");
        }
        else
        {
            printf("p != NULL\n");
        }
    
        freeM(p);  //确实free了但是为什么 还能二次free
        p = NULL;
        printf("free after");
        printf("%s\n",p);  //输出了乱码
        if(p==NULL)
        {
            printf("p == NULL\n");
        }
        else
        {
            printf("p != NULL\n");
        }
        freeM(p); //并没有报错  按道理来说是不是应该报错
    
    
        return 0;
    }
    
    ~~~

  - 

### 问题

~~~c
day04 
1.一维数组的本质？
	int a[10]; a &a a[0] *a都表示什么？
2.数组类型，数组指针类型，数组指针类型变量
    定义数组类型 int a[3][10]; //数组类型  
	typedef int myArray[5];
	myArray a; == int a[5];
    定义数组指针类型  int (*p)[10]; //数组指针类型
	typedef int (*myPArray)[5];
	myPArray myP; == int (*a)[5]; 
	myP = &a;
	(*myP)[i] = 10; //通过数组指针变量操作数组内存
    定义数组指针类型变量 
    int (*myArray)[5]; //告诉编译器开辟四个字节的内存，将这个指针指向[5]的数组
	myArray = &a;
	(*myArray)[i] = 10;//依然是通过指针操作内存
3.多维数组本质技术推演
        char arr[3][5] 和 char *p[5]; 两者表示的是一样的 都是一个二维指针
        arr表示二维数组的首行元素指针代表第一个[5]的整个一维数组arr+1步长1*5
        arr[3][5]-->arr[][5]-->*arr[5] -->**arr
        arr[i][j] --> *(*(a+i)+j)  表示一样的
4.多维数组作为函数参数时，会退化成指针
    本质是因为程序员眼中的二维内存，其实在物理内存中是连续存储的，二维内存会出现失真
        主要原因是提高效率，一切都是内存，都是指针。
5.二级指针的三种内存模型的建立
6.唯有训练、一遍一遍的训练，愚人的做法而已
7.想让一个整数数组、字符数组、指针数组等具有自我结束的能力，除了提供相应的长度之外，可以在申请内存的时候多分配一个单位的内存，且存入'\0'用来作为判断条件自我结束
~~~

### 结构体

- 三种形式

- ~~~c
  struct Dog1
  {
      char name[20];
      int age;
  };
  struct Dog2
  {
      char name[20];
      char sex;
  }d2;
  typedef struct Dog3  //常用这种形式
  {
      char name[12];
      int age;
  }dog;
  //捆绑分配 捆绑释放
  //如果结构体里面有对应的指针变量 就需要通过访问结构体变量进行free他的指向内存
  int main(void)
  {
      printf("结构体\n");
      struct Dog1 d1;
      dog d3 ;
      printf("d1 = %d\n",sizeof(d1));
  
      printf("d2 = %d\n",sizeof(d2));
  
      printf("d3 = %d\n",sizeof(d3));
     	//访问方式
      d1.name = "adf"; 
      struct Dog1 *p = &d1;
      p->name; //本质上是寻址 往结构里面的内容进行寻址
      system("pause");
      return 0;
  }
  ~~~

- 结构体做函数参数

- ~~~c
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>
  typedef struct _Teacher
  {
      char name[20];
      int age;
      char sex;
  }Teacher;
  
  int printTArray(Teacher *tArray,int num)
  {
      int i=0;
      for(i=0; i<num; i++)
      {
          printf("%d %s\n",tArray[i].age,tArray[i].name);
      }
      return 0;
  }
  
  int sortTArray(Teacher *tArray,int num)
  {
      int i=0,j=0;
      Teacher tep;  //临时区分配内存进行内存块的操作
      for(i=0; i<num-1; i++)
      {
          for(j=0; j<num-i-1; j++)
          {
              if(tArray[j].age > tArray[j+1].age)
              {
                  tep = tArray[j];  //直接使用编译器提供的结构体复制行为
                  tArray[j] = tArray[j+1];
                  tArray[j+1] = tep;
              }
          }
      }
      return 0;
  }
  
  //使用分配到堆里面的内存 satck操作 结构体
  //这种场景是不能修改实参的
  int createTArray(Teacher *tArray,int num) //这里是形参 如果
  {
      tArray = (Teacher *)malloc(num* sizeof(Teacher)); //分配内存
      if(tArray == NULL)
      {
          return -1;
      }
      return 0; //
  }
  
  //这种场景是可以修改实参的,缺点是不能返回，这个函数的状态
  Teacher *createTArray01(int num)
  {
      Teacher *temp = NULL;
      temp = (Teacher *)malloc(num * sizeof(Teacher));
      if(temp == NULL)
      {
          return NULL;
      }
      return temp;
  }
  
  int mainHeap(void)
  {
      int i=0;
      //int ret = 0;
      Teacher *pArray = NULL;  //分配到heap区,然后
      //ret = createTArray(pArray,3); //pArray 和 tArray 一个是形参和实参是不一样，因此出现pArray是空的
      pArray = createTArray01(3); //pArray 和 tArray 一个是形参和实参是不一样，因此出现pArray是空的
      if(pArray == NULL)
      {
          printf("pArray = NULL\n");
  
          return 0;
      }
      for(i=0; i<3; i++)
      {
          printf("please enter %d age value:", i+1);
          scanf("%d",&pArray[i].age);
          printf("please enter %d name value:", i+1);
          scanf("%s",pArray[i].name);
      }
      printf("sort before..........\n");
      printTArray(pArray,3);
  
      sortTArray(pArray,3);
  
      printf("sort before..........\n");
  
      printTArray(pArray, 3);
      free(pArray);
      pArray = NULL;
      return 0;
  }
  int mainStack(void)
  {
      int i=0;
      Teacher tArray[3];  //分配到栈区
      for(i=0; i<3; i++)
      {
          printf("please enter %d age value:", i+1);
          scanf("%d",&tArray[i].age);
  
      }
      printf("sort before..........\n");
      printTArray(tArray,3);
  
  
      sortTArray(tArray,3);
  
      printf("sort before..........\n");
  
      printTArray(tArray, 3);
      return 0;
  }
  
  ~~~

- 

- 结构体中包含一级指针

  - ~~~
    #include <stdio.h>
    #include <stdlib.h>
  #include <string.h>
    //结构体里面套指针是学习的重点
    typedef struct _Teacher
    {
        char name[62];
        char *title;
        char c;
        int age;
    } Teacher;
    
    int printTArray(Teacher *tArray,int num)
    {
        int i=0;
        for(i=0; i<num; i++)
        {
            printf("%d %s %s\n",tArray[i].age,tArray[i].name,tArray[i].title);
        }
        return 0;
    }
    
    int sortTArray(Teacher *tArray,int num)
    {
        int i=0,j=0;
        Teacher tep;  //临时区分配内存进行内存块的操作
        for(i=0; i<num-1; i++)
        {
            for(j=0; j<num-i-1; j++)
            {
                if(tArray[j].age > tArray[j+1].age)
                {
                    tep = tArray[j];  //直接使用编译器提供的结构体复制行为
                    tArray[j] = tArray[j+1];
                    tArray[j+1] = tep;
                }
            }
        }
        return 0;
    }
    
    //使用分配到堆里面的内存 satck操作 结构体
    //这种场景是不能修改实参的
    int createTArray(Teacher *tArray,int num) //这里是形参 如果
    {
        tArray = (Teacher *)malloc(num* sizeof(Teacher)); //分配内存
        if(tArray == NULL)
        {
            return -1;
        }
        return 0; //
    }
    
    //这种场景是可以修改实参的,缺点是不能返回，这个函数的状态
    Teacher *createTArray01(int num)
    {
        int i=0;
        Teacher *temp = NULL;
        temp = (Teacher *)malloc(num * sizeof(Teacher));
        if(temp == NULL)
        {
            return NULL;
        }
        for(i=0; i<num; i++)
        {
            temp[i].title = (char *)malloc(100); //分配num个内存块
        }
        return temp;
    }
    
    int main(void)
    {
        int i=0;
        //int ret = 0;
        Teacher *pArray = NULL;  //分配到heap区,然后
        //ret = createTArray(pArray,3); //pArray 和 tArray 一个是形参和实参是不一样，因此出现pArray是空的
        pArray = createTArray01(3); //pArray 和 tArray 一个是形参和实参是不一样，因此出现pArray是空的
        if(pArray == NULL)
        {
            printf("pArray = NULL\n");
    
            return 0;
        }
        for(i=0; i<3; i++)
        {
            printf("please enter %d age value:", i+1);
            scanf("%d",&pArray[i].age);
            printf("please enter %d name value:", i+1);
            scanf("%s",pArray[i].name);
    
            printf("please enter %d title value:", i+1);
            scanf("%s",pArray[i].title);
        }
        printf("sort before..........\n");
        printTArray(pArray,3);
    
        sortTArray(pArray,3);
    
        printf("sort before..........\n");
    
        printTArray(pArray, 3);
        free(pArray);
        pArray = NULL;
        return 0;
    }
    
    ~~~
    
  - 

- 结构体包含二级指针

  - ~~~c
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    //结构体里面套指针是学习的重点
    typedef struct _Teacher
    {
        char name[64];
        char *title;
        char **pStuArray;
        int age;
    } Teacher;
    
    int printTArray(Teacher *tArray,int num)
    {
        int i=0,j=0;
        for(i=0; i<num; i++)
        {
            printf("老师信息: ");
            printf("%d %s %s\n",tArray[i].age,tArray[i].name,tArray[i].title);
            printf("学生信息: ");
            for(j=0; j<3; j++)
            {
                printf("%s ", tArray[i].pStuArray[j]);
            }
            printf("\n");
        }
        return 0;
    }
    
    int sortTArray(Teacher *tArray,int num)
    {
        int i=0,j=0;
        Teacher tep;  //临时区分配内存进行内存块的操作
        for(i=0; i<num-1; i++)
        {
            for(j=0; j<num-i-1; j++)
            {
                if(tArray[j].age > tArray[j+1].age)
                {
                    tep = tArray[j];  //直接使用编译器提供的结构体复制行为
                    tArray[j] = tArray[j+1];
                    tArray[j+1] = tep;
                }
            }
        }
        return 0;
    }
    
    //使用分配到堆里面的内存 satck操作 结构体
    //这种场景是不能修改实参
    //这种场景是可以修改实参的,缺点是不能返回，这个函数的状态
    Teacher *createTArray01(int num)
    {
        int i=0;
        Teacher *temp = NULL;
        temp = (Teacher *)malloc(num * sizeof(Teacher));
        if(temp == NULL)
        {
            return NULL;
        }
        for(i=0; i<num; i++)
        {
            temp[i].title = (char *)malloc(100); //分配num个内存块
        }
    
        for(i=0; i<num; i++)
        {
            //先申请内存 再将内存的首地址挂到需要分配的内存指针上
            //这样结构清晰明了
            char **ptmp = (char **)malloc(3*sizeof(char *));
            for(int j=0; j<3; j++)
            {
                ptmp[j] = (char *)malloc(100);
            }
            temp[i].pStuArray = ptmp;
        }
        return temp;
    }
    
    int freeArray(Teacher *tArray,int num)
    {
    
        int i=0,j=0;
        if(tArray == NULL)
        {
            return -1;
        }
    
        for(i=0; i<num; i++)
        {
            char **tep = tArray[i].pStuArray;
            if(tep==NULL)continue;
    
            for(j=0; j<3; j++)
            {
                if(tep[j]!=NULL)
                {
                    free(tep[j]);
                }
            }
            free(tep);
        }
    
        for(i=0; i<num; i++)
        {
            free(tArray[i].title);
            tArray[i].title = NULL; //垃圾语句 因为形参不能改变实参
        }
        free(tArray);
        tArray = NULL;
        return 0;
    
    }
    
    int main18(void)
    {
        int i=0,j=0;
        //int ret = 0;
        Teacher *pArray = NULL;  //分配到heap区,然后
        //ret = createTArray(pArray,3); //pArray 和 tArray 一个是形参和实参是不一样，因此出现pArray是空的
        pArray = createTArray01(3); //pArray 和 tArray 一个是形参和实参是不一样，因此出现pArray是空的
        if(pArray == NULL)
        {
            printf("pArray = NULL\n");
    
            return 0;
        }
        for(i=0; i<3; i++)
        {
            printf("请输入第%d个老师的年龄:", i+1);
            scanf("%d",&pArray[i].age);
            printf("请输入第%d个老师的姓名:", i+1);
            scanf("%s",pArray[i].name);
    
            printf("请输入第%d个老师的职称", i+1);
            scanf("%s",pArray[i].title);
            printf("学生信息: \n");
            for(j=0; j<3; j++)
            {
                printf("请输入第%d学生的姓名: ",j+1);
                scanf("%s",pArray[i].pStuArray[j]);
            }
        }
        printf("sort before..........\n");
        printTArray(pArray,3);
    
        sortTArray(pArray,3);
    
        printf("sort after..........\n");
    
        printTArray(pArray, 3);
        //free(pArray);
        freeArray(pArray,3);
        pArray = NULL;
        return 0;
    }
    
    ~~~

  - 

- 结构体高级话题

  - &属于cpu的逻辑计算并没有对内存进行读写

- 结构体中存在的深拷贝和浅拷贝问题

  - 如果结构体里面有开辟空间的指针就需要自己定义函数进行深拷贝，如果使用的是stack空间深拷贝和浅拷贝是一样的

### 动态库（day07）

- 如果在动态库里分配内存，那么主调函数中就应该调用动态库中的free函数释放内存
- 两个工程文件
  - 测试动态库工程
  - 开发动态库工程
  - 两个文件夹里面的dll、lib来回拷贝进行测试。

### 链表

- 静态链表，内存分配在栈中

- 指针节点名称pHead,pCurrent,pPrior,pNext,pMalloc

- 链表编程关键

  - 指针指向谁，就把谁的地址赋值给指针
  - 辅助指针变量和逻辑操作关系

- 链表的操作

  - ~~~c
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    typedef struct Node
    {
        int data;
        struct Node *next;
    }SLIST;
    //删除链表 释放链表的所有节点，用于创建链表失败时，和链表使用完之后
    //失败时，可能还会存在其他的节点存在，所以要清除掉
    int SLIST_Destory(SLIST *pHead)
    {
        SLIST *p = NULL,*temp = NULL;
        if(pHead == NULL)
        {
            printf("destory is failed\n");
            return -1;
        }
    
        p = pHead;
        while(p)
        {
            temp = p->next;
            free(p);
            p = temp;
        }
        return 0;
    }
    
    //通过返回值创建
    SLIST *SLIST_create()
    {
        SLIST *pHead = NULL,*pCur=NULL,*pMal = NULL;
        int data;
        pHead = (SLIST *)malloc(sizeof(SLIST));
        if(pHead == NULL)
        {
            printf("malloc failed \n");
            return NULL;
        }
        pHead->data = 0;
        pHead->next = NULL;
    
        //pCur = (SLIST *)malloc(sizeof(SLIST));
        printf("please input data:\n");
        scanf("%d",&data);
        //pHead->next = pCur;
    
        pCur = pHead;
        while(data != -1)
        {
            pMal = (SLIST *)malloc(sizeof(SLIST));
            if(pMal == NULL) //当申请某个节点失败之后，前面的节点要全部释放 不然造成内存泄漏
            {
                //可以增加日志
                SLIST_Destory(pHead);
                return NULL;
            }
    
            pMal->data = data;
            pMal->next = NULL;
    
    
            pCur->next = pMal;
            pCur = pMal;
            printf("please input data:\n");
            scanf("%d",&data);
        }
        return pHead;
    
    }
    //利用二级指针作为内存输出 二级指针间接修改一级内存
    //2年工作经验 是上面创建链表的升级版本
    int SLIST_create2(SLIST **myHead)
    {
        SLIST *pHead = NULL,*pCur=NULL,*pMal = NULL;
        int data;
        pHead = (SLIST *)malloc(sizeof(SLIST));
        if(pHead == NULL)
        {
            printf("malloc failed \n");
            return NULL;
        }
        pHead->data = 0;
        pHead->next = NULL;
        printf("please input data:\n");
        scanf("%d",&data);
    
        pCur = pHead;
        while(data != -1)
        {
            pMal = (SLIST *)malloc(sizeof(SLIST));
            if(pMal == NULL) //当申请某个节点失败之后，前面的节点要全部释放 不然造成内存泄漏
            {
                //可以增加日志
                SLIST_Destory(pHead);
                return NULL;
            }
            pMal->data = data;
            pMal->next = NULL;
            pCur->next = pMal;
            pCur = pMal;
            printf("please input data:\n");
            scanf("%d",&data);
        }
        *myHead = pHead;
        return 0;
    
    }
    
    //打印链表
    int SLIST_print(SLIST *pHead)
    {
        SLIST *p = NULL;
        if(pHead == NULL)
        {
            printf("pHead failed\n");
            return -1;
        }
        p = pHead->next;
    
        printf("begin\n");
        while(p!=NULL)
        {
            printf("%d ",p->data);
            p = p->next;
        }
        printf("\nend\n");
        return 0;
    }
    
    
    
    //在值为x的节点前插入一个节点
    int SLIST_Insert(SLIST *pHead,int x,int y)
    {
        SLIST *pPre=NULL,*pCur=NULL;
        SLIST *pMal = NULL;
        if(pHead == NULL)
        {
            return -1;
        }
        pPre = pHead;
        pCur = pHead->next;
    
        pMal = (SLIST *)malloc(sizeof(SLIST));
        pMal->data = y;
        pMal->next = NULL;
    
        while(pCur)
        {
            if(pCur->data == x)
            {
                break;//出去进行交换
            }
            pPre = pCur;
            pCur = pCur->next;
        }
    
        pMal->next = pCur;
        pPre->next = pMal;
        return 0;
    }
    
    
    //删除数值为x的节点
    int SLIST_Del(SLIST *pHead,int x)
    {
        SLIST *pPre = NULL,*pCur = NULL;
        if(pHead == NULL)
        {
            return -1;
        }
        pPre = pHead;
        pCur = pHead->next;
        while(pCur)
        {
            if(pCur->data == x)
            {
                pPre->next = pCur->next;  //找到了就删除
                free(pCur);
                break;
            }
            pPre = pCur;
            pCur = pCur->next;
        }
        //没找到不用操作
    
        return 0;
    }
    //反转链表
    int SLIST_Reverse(SLIST *pHead)
    {
        SLIST *p=NULL,*q=NULL,*t=NULL;
        if(pHead == NULL)
        {
            return -1;
        }
        if(pHead->next == NULL || pHead->next->next == NULL)
        {
            return -2;
        }
    
        p = pHead->next;
        q = pHead->next->next;
        while(q)
        {
            t = q->next;
            q->next = p;
            p = q;
            q = t;
        }
    
        pHead->next->next = NULL;
        pHead->next = p;
        return 0;
    }
    
    int main33(void)
    {
        SLIST *p = NULL;
        //p = SLIST_create();
        SLIST_create2(&p);  //使用二级指针创建内存 被调用函数分配内存
        SLIST_print(p);
        SLIST_Insert(p,2,20);
        SLIST_print(p);
    
        SLIST_Del(p,3);
        SLIST_print(p);
    
        SLIST_Reverse(p);
    
        printf("反转之后\n");
        SLIST_print(p);
    
        SLIST_Destory(p);
    
        system("pause");
        return 0;
    }
    
    ~~~

    

  - 

- 业务逻辑包含链表，链表要放到业务逻辑的第一个块上

  - ~~~c
    typedef struct _Teacher3
    {
        struct node myNode;
        int age;
        char name[60];
        char **p2;
    }Teacher;
    
    typedef struct node
    {
        struct node *next;
    }node;
    //可以根据node来连接各个业务节点Teacher，因为在分配内存的时候都是连续分配的所以可以直接强转类型
    Teacher t1,t2;
    node d1,d2;
    d1 = (node *)t1;
    t2 = (Teacher *)d2;
    //对应的图片如下
    ~~~

  - ![](E:\Cplusplus\Cplusplus\linux非传统链表.png)

- 企业级别的链表库调用函数实例

- 其中我是没有库的，所以只是展示一些用法，是不能真的调用起来的

- ~~~c
  #include<stdio.h>
  #include <string.h>
  #include <stdlib.h>
  
  //自己定义的不算数的
  typedef struct Node1
  {
     struct Node1 *next;
  }LinkListNode;
  
  
  //业务结构体
  //即使修改业务结构体 只需要在业务结构体中加入NOde即可 所以说
  //业务代码和链表库没有什么关系
  typedef struct _Teacher4
  {
      //必须在业务节点的第一个域包含链表节点
      LinkListNode node;
      char name[32];
      int age;
  }Teacher;
  /*
  //链表库提供的api接口 如何去调用
  int LinkList;
  LinkList *LinkList_Create();
  void LinkList_Destory(LinkList* list);
  void LinkList_Clear(LinkList* list);
  int LinkList_Length(LinkList* list);
  int LinkList_Insert(LinkList* list,LinkListNode *node,int pos);
  LinkListNode *LinkList_Get(LinkList *list,int pos);
  LinkListNode *LinkList_Delete(LinkList *list,int pos);
  
  */
  int main34(void)
  {
      int ret = 0;
      int len = 0;
      int i=0;
      LinkList *list = NULL;
      Teacher t1,t2,t3,t4,t5;
      memset(&t1,0,sizeof(Teacher));
      memset(&t2,0,sizeof(Teacher));
      memset(&t3,0,sizeof(Teacher));
      memset(&t4,0,sizeof(Teacher));
      memset(&t5,0,sizeof(Teacher));
      t1.age = 1;
      t2.age = 2;
      t3.age = 3;
      t4.age = 4;
      t5.age = 5;
      list = LinkList_Create();
      if(list == NULL)
      {
          return -1;
      }
  
      //插入节点 使用尾插法
      //内存申请了得 所以可以直接转
      ret = LinkList_Insert(list,(LinkListNode *)&t1,LinkList_Length(list));
      ret = LinkList_Insert(list,(LinkListNode *)&t2,LinkList_Length(list));
      ret = LinkList_Insert(list,(LinkListNode *)&t3,LinkList_Length(list));
      ret = LinkList_Insert(list,(LinkListNode *)&t4,LinkList_Length(list));
      ret = LinkList_Insert(list,(LinkListNode *)&t5,LinkList_Length(list));
  
      len = LinkList_Length(list);
      for(i=0; i<len; i++)
      {
          //由于Get的返回值是ListNode和也就是这个节点的首地址
          //而Teacher的内存的第一个域就是ListNode所以可以直接转成Teacher
          struct _Teacher4 *tmp = (struct _Teacher4*)LinkList_Get(list,i);
  
          if(tmp != NULL)
          {
              printf("age : %d\n",tmp->age);
          }
      }
      //删除
      while(LinkList_Length(list))
      {
          //从链表库中删除业务节点的时候，把业务节点的指针返回给调用者，
          //以便调用者进行额外的逻辑控制
          struct _Teacher4 *tmp = (struct _Teacher4 *)LinkList_Delete(list,0); //头删
  
          if(tmp != NULL)
          {
              printf("age : %d\n",tmp->age);
          }
      }
  
      LinkList_Destory(list);
  
  
      return 0;
  }
  
  ~~~



## C++

- 定义数据类型的时候是不会分配内存的，例如定义一个结构体编译器不会分配内存，只有使用的时候才会分配内存

- 回答为什么类中要有成员函数，就是为了在修改成员变量之后，可以让逻辑语句重新在赋值后的基础上计算

  - 

  ~~~c++
  #include <iostream>
  
  using namespace std;
  //说明为什么要在类中存在函数调用 成员函数
  
  class Circle
  {
  public:
      double r;
      double pi = 3.14159;
      double s = pi*r*r;
  
      void getS()
      {
          s = pi*r*r;
      }
  };
  int main()
  {
  
      Circle c1;
      cout << "请输入半径\n";
      cin>>c1.r;
      //输出乱码，因为在存入到内存里面的时候c1.s存入的是一个pi*r*r计算好的值，
      //在初始化时，r就没有初始化是乱码，也就是无穷的数，那么pi*r*r也是乱码
      //所以存入到s这个内存的值是乱码
      //当修改r时，调用s这个内存中的值，是不会执行pi*r*r这句语句的；所以依然是乱码
      //只有在修改了r之后，再调用函数gets才能执行相应的语句
      cout << c1.s << endl;
  
      c1.getS();
  
      cout << c1.s << endl; // 314.59
      cout << "Hello world!" << endl;
      return 0;
  }
  
  ~~~

- namespace的使用和定义

  - ~~~c++
    #include<iostream>
    using namespace std; //也就是声明使用std命名空间里的内容 例如下面自己定义的命名空间
    namespace NameA
    {
        int a=0;
    }
    namespace NameB
    {
        int a = 1;
         namespace NameC
        {
            struct A
            {
                char name[10];
                int age;
            };
        }
    }
    int main()
    {
        using namespace NameA;
        using NameB::NameC::A;
        cout << a << endl;
        cout << NameB::a << endl;
    
        A a1 = {"hh",2};
        cout << a1.name << endl;
        cout << a1.age << endl;
        return 0;
    }
    ~~~

- ~~~
  c中可以定义同名的全局变量，最后都会指向同一份内存
  而c++则不能满足这种，编译会报错
  c编译器和c++编译器不一样
  
  
  在c++里面struct做了增强
  c中
  struct T{}; //可以通过只能struct T t1; 
  cpp中 可以通过T t1; 
  
  C++中(a<b?a:b)=30是可以的 因为返回的是a或者b具有内存地址可以作为左值 c语言中不行，因为返回的是变量值，c中使用*（(a<b?&a:&b)=30)是可以的
  
  ~~~

- c++中所有的变量和函数都必须有类型

- 元素当左值的条件，这个元素必须存在地址(内存空间)

- const

  - 在c里面const 是个冒牌货，只是显示的告诉程序员不要修改这个值 
  - c++则是具有真正的作用，当变量被const修饰的时候通过&a或者extern 那么编译器会重新开辟一片内存供程序员使用，而原来的变量则不会存在任何被修改的可能

- 引用

  - int &b = a; b就是a的别名。。注意：引用&是c++的语法，请不要再用c语言的语法去思考

- 引用的本质

  - 引用必须要初始化 、也就是说要赋值。int &b=a; 因为b是一个常量不能被改变。char buf[10]; //buf也是一个常量
  - c++编译器中，使用常量指针实现引用，所以引用占用的内存空间指针一样
  - 引用相当于int * const p; //p不能被改变，但是有内存

- 引用当左值

  - ~~~c
    #include <iostream>
    #include <stdio.h>
    using namespace std;
    
    int getA1()
    {
        int a;
        a = 10;
        return a;
    }
    //& = * const
    int& getA2()
    {
        int a;
        a = 10;
        int &b = a;
        return b;  //相当于做了
    }
    
    int main(void)
    {
    
        cout << "ok" << endl;
    
        int a1=0,a2=0;
        a1 = getA1();
        a2 = getA2();
        int &a3 = getA2();  //执行完=之后
        printf("a1 = %d\n",a1);
        printf("a2 = %d\n",a2);
        printf("a3 = %d\n",a3);//*p的操作所以输出乱码，在栈出完之后。
    
        return 0;
    }
    ~~~

  - 当被调用的函数当左值得时候必须返回一个引用（也就是一个能有内存的值）

  - ~~~c
    /*
    
    int * j1()
    {
        return &a; //相当于 &的作用
    }
    */
    int& j1()
    {
        static int a = 10; //
        a++;
        cout << "a = " << a << endl;
        return a; //用staitc可以这样返回 局部变量则不可以
    }
    int j2()
    {
        static int a = 10; //
        a++;
        cout << "a = " << a << endl;
        return a; //用staitc可以这样返回 局部变量则不可以
    }
    
    int* j3()
    {
        static int a = 10; //
        a++;
        cout << "a = " << a << endl;
        return &a; //用staitc可以这样返回 局部变量则不可以
    }
    int main(void)
    {
    
        j1();
        j1();
        int b = j1();
        cout << "b = " << b << endl;
        //函数做左值
        j1() = 100;
        j1();  //101
    
        *(j3()) = 200;
        j3();  //201
    
        //不分配内存空间的不能做左值
    //    j2() = 200;
    //    j2();
    
    //    int &c = j1();  //全局变量static才可以
    //    cout << "c = " << c << endl;
        return 0;
    }
    
    ~~~

- 指针的引用

- ~~~c
  #include <stdio.h>
  #include <iostream>
  #include <stdlib.h>
  using namespace std;
  struct Teacher
  {
      char name[20];
      int age;
  };
  
  int getT(Teacher **myT)
  {
      Teacher *p = NULL;
      if(myT == NULL)
      {
          return -1;
      }
      p = (Teacher *)malloc(sizeof(Teacher));
     // memset(p,0,sizeof(Teacher));
      if(p == NULL)
      {
          return -1;
      }
      p->age = 10;
  
      *myT = p;
      return 0;
  }
  //指针的引用而已
  //同样达到了一个二级指针的用法
  //看到引用 编译器会做转变为指针处理
  int getT2(Teacher* &myp)
  {
      //这是个引用 对myp修改就是修改p
      myp = (Teacher *)malloc(sizeof(Teacher));
      myp->age = 34;
      return 0;
  }
  
  int main(void)
  {
  
      Teacher *p = NULL;
      getT(&p);
      //调用
      getT2(p);
  
      cout <<  p->age << endl;
      return 0;
  }
  c
  ~~~

- const修饰引用

- ~~~
  const Teacher &p; 就不能通过p来修改p所指向的空间了 等价于const Teacher * const p
  ~~~

- int &a = 19 ; const  int &a = 19; 加const的不会报错，因为编译器自己分配内存了 不加const的会报错，没分配内存。

#### 内联函数

- 内联函数（inline）是一个请求，必须将inline和函数的定义写在一起。作用就是将一段代码插入到调用的地方

#### c++函数扩展

- 默然参数 int fun1(int x = 1),int fun2(int x,int y,int z=10)
- 占位参数inf fun1(int x,int) //不要这样用
- 函数重载至少满足下面的一个条件
  - 参数类型
  - 参数个数
  - 参数顺序
- 函数重载时，如果存在二义性则在调用的时候会失败
- 类做函数参数的区别
  - 可以使用类参数中的属性和方法
- c++中一般类的声明和实现是分开的一个在cpp一个在h文件

#### c++构造函数专题

- 拷贝构造的4种应用场景

- ~~~c
  #include <iostream>
  using namespace std;
  
  class Location
  {
  public:
      Location()
      {
          cout << "无参构造" << endl;
      }
      Location(int a,int b)
      {
          this->x = a;
          this->y = b;
          cout << "有参构造" << endl;
      }
      Location(const Location &p)
      {
          this->x = p.x;  //这里应该能调用吗
          this->y = p.y;
          cout << "拷贝构造"  << endl;
      }
      ~Location()
      {
          cout << "析构函数" << endl;
      }
      int getX(){return x;}
      int getY(){return y;}
  private:
      int x,y;
  };
  
  //场景1（） 2 =
  //应用场景3
  void fun3(Location p)
  {
      cout << p.getX() << endl;
  }
  
  Location getL()
  {
      Location A(2,3);  //这里调用了 没有调用拷贝构造啊
      return A;  //现在return不调用拷贝构造了吗？  返回没有用到拷贝构造啊
  }
  
  
  //拷贝构造应用4   感觉没有调用拷贝构造函数啊
  void test01()
  {
      
  
      //这种在定义b时调用一次无参构造 getL中调用一次有参构造
  //    Location B;
  //    B = getL();
  
      //如果一个匿名对象（return）被一个同类型的对象接收（初始化一个同类型的对象）
      //那么匿名对象会直接转换成新的对象  （这是规定）
      Location B = getL(); //只调用一次有参构造和析构也就是说B时不在调用构造
      cout << B.getX() << endl;
  }
  
  int main()
  {
      Location a(1,2);
  //    Location a1(a);//拷贝构造场景1
      Location a2 = a;//场景2
  
      /*
      =等号操作，和对象初始化操作是不一样的
      */
      //下面这种不会调用拷贝构造 c++直接省略
  //    Location a2;
  //    a2 = a;   //这里就是=运算符重载了吧
  
    //  fun3(a);  //场景3 做参数
     // test01();  //场景4 做返回值return的时候  但是我没实验出来
      return 0;
  }
  
  ~~~

- c++中浅拷贝和深拷贝导致的内存重复释放问题 

  - 目前看来，如果一个内存释放过之后，想再次释放，则会报错。（添加一个cout语句每次释放就不行 如果是浅拷贝）

  - ~~~c
    #include <iostream>
    #include <stdlib.h>
    #include <stdio.h>
    #include <string.h>
    
    using namespace std;
    
    class Name
    {
    public:
        Name( const char *pname)
        {
           pSize = strlen(pname);
            pName = (char *)malloc(pSize + 1);
            strcpy(pName,pname);
        }
    	//没有拷贝构造好像也能正常释放内存。。是不是新的编辑器做出的优化
        Name(const Name &obj)
        {
            cout << "调用析构了"  << endl;
            if(pName != NULL) //用之前一定要判断，然后释放掉原来的内存
            {
                free(pName);
                pName = NULL;
                pSize = 0;
            }
            pName = (char *)malloc(obj.pSize+1);
            strcpy(pName,obj.pName);
            pSize = obj.pSize;
        }
        ~Name()
        {
    
            if(pName != NULL)
            {
                cout << "析构"  << endl; //为什么加这句就不能成功析构,当重复析构的时候
                free(pName);
                pName = NULL;
                pSize = 0;
            }
        }
    public:
        char *pName; //有指针域存在时，一定要考虑是否有浅拷贝问题 =重载  拷贝构造函数
        int pSize;
    };
    int main(void)
    {
        cout << "业务开始...." << endl;
        Name obj1("1244");
        //可以重复释放一个被是放过的内存
        Name obj2 = obj1; //浅拷贝 //添加可拷贝构造函数 就会自己调用拷贝构造函数
        cout <<  "业务结束" << endl;
        return 0;
    }
    
    ~~~

  - 就我当前使用的编译器 是可以重复释放一个已经被释放之后的内存的  这是什么傻逼编译器？？，正常还是要用深拷贝来，防止浅拷贝导致的重复释放

  - 构造函数调用规则

    - 只要写了构造函数，那么编译器就不会提供默认的构造函数。你只能用自己写的构造函数

  - 构造函数调用顺序强化练习

  - ~~~c
    #include <iostream>
    #include <stdio.h>
    #include <stdlib.h>
    using namespace std;
    class ABCD
    {
    public:
        ABCD(int a,int b,int c)
        {
    
            x = a;
            y = b;
            z = c;
            printf("ABCD() = %d,%d,%d\n",x,y,z);
        }
        ~ABCD()
        {
            printf("~ABCD() = %d,%d,%d\n",x,y,z);
        }
        int getX()
        {
            return x;
        }
    private:
        int x;
        int y;
        int z;
    };
    
    class MyD
    {
    public:
        MyD():a1(1,2,3),a2(4,5,6),m(10) //定义
        {
            cout << "MyD()" << endl;
        }
        MyD(const MyD &myd):a1(7,8,9),a2(10,11,12),m(20)
        {
            cout << "MyD(const MyD )" << endl;
        }
        ~MyD()
        {
            cout << "~MyD()" << endl;
        }
    public:
        ABCD a1;
        ABCD a2;
        int m;
    };
    
    int doThing(MyD myd11)  //会调用拷贝构造函数
    {
        cout << "doThing MyD ,myd1.x=" << myd11.a1.getX() << endl;
        return 0;
    }
    int run1()
    {
        MyD myd1;  //调用无参构造
        doThing(myd1);
        return 0;
    }
    //执行过程
    /*
    MyD myd1;  //调用无参构造
        执行MyD():a1(1,2,3),a2(4,5,6),m(10)
        调用a1(1,2,3)构造printf("ABCD() = %d,%d,%d\n",x,y,z);  123
        调用a2(4,5,6)构造printf("ABCD() = %d,%d,%d\n",x,y,z);  456
        调用MyD构造 cout << "MyD()" << endl;
    doThing(myd1);执行
        执行，myd11 ,MyD的拷贝构造MyD(const MyD &myd):a1(7,8,9),a2(10,11,12),m(20)
        调用a1(7,8,9)构造printf("ABCD() = %d,%d,%d\n",x,y,z);  789
        调用a2(10,11,12)构造printf("ABCD() = %d,%d,%d\n",x,y,z);  10 11 12
        调用拷贝构造cout << "MyD(const MyD )" << endl;
        执行cout << "doThing MyD ,myd1.x = " << myd1.a1.getX() << endl;
        执行return 0;
        析构myd11 cout << "~MyD()" << endl;
        析构printf("~ABCD() = %d,%d,%d\n",x,y,z);10 11 12
        析构printf("~ABCD() = %d,%d,%d\n",x,y,z); 789
        执行return 0;
        析构myd1 cout << "~MyD()" << endl;
        析构printf("~ABCD() = %d,%d,%d\n",x,y,z);456
        析构printf("~ABCD() = %d,%d,%d\n",x,y,z); 123
    */
    int  main(void)
    {
        run1();
        return 0;
    }
    
    ~~~
    
  - 
  
#### new malloc free delete
  
- **基础类型new的可以使用free释放** ，也就是说可以混搭。涉及到类的时候不要混搭使用

#### C++内存模型初探

- c++类中成员变量和成员函数是分开存储
  
  - 普通成员变量：存储于对象中，与struct变量有相同的内存布局和字节对齐方式
  - 静态成员变量：存储于全局数据区中
  - 成员函数：存储到代码段中
  
- 很多对象公用一块代码，各个对象之间是如何区分具体的代码呢？

  - c++编译器对普通函数做了内部处理，会添加this参数到对应的函数调用上

  - ~~~c
    #include <iostream>
    #include <stdio.h>
    #include <stdlib.h>
    
    class Test
    {
    public:
        Test(int a)
        {
            this->a = a;
        }
    public:
        int a;
    };
    
    int main(void)
    {
        //c++会自动处理，通过添加一个this指针，则每个对象就能够知道自己调用的代码段
        Test t1(10); // Test t1(this,10) ==> Test t1(&t1,10);
    
        return 0;
    }
    ~~~

- c++内存模型总结

  - c++类对象中成员变量和成员函数是分开存储的。c语言的内存4区模型依然适用。
  - c++中类的普通成员函数隐式包含一个指向对象的this指针
  - 静态成员函数、成员变量属于类
    - 静态成员函数不包含指向具体对象的this指针
    - 普通成员函数包含一个指向具体对象的指针