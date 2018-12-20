#第16章 外部接口技术

MATLAB外部程序接口(API)函数库例如MEX函数库，MX函数库，MAT函数库和Engine函数库等包含丰富的接口函数，利用这些接口函数可以轻松地实现C，C++，FORTRAN等语言调用Matlab命令和数据文件，通过使用C或者FORTRAN语言编写MEX文件，利用Matlab开发环境的MEX编译命令，可以极大提高M语言程序的运行速度和代码执行效率。通过调用MATLAB引擎，实现后台MATLAB函数的调用。利用MATCOM以及MATLAB环境下的COM编译器，可以独立与MATLAB开发平台进行应用程序开发。本章主要内容包括以下四个方面：
*  创建C语言MEX文件
*  MAT文件应用
*  MATLAB引擎技术
*  Visual C++与MATLAB接口


## 16.1 概述

MATLAB开发环境提供了丰富的应用接口程序(API)函数库包括MAT函数库，MEX函数库，MX函数库，Engine函数库实现与其他工作环境的接口，提供了不同的编译命令如MEX命令，MCC命令等将M文件编译成独立与MATLAB工作环境的动态链接库文件(DLL)文件，C++语言直接调用的.cpp，.h文件以及可执行.exe文件等。通过组件对象模型(COM) 实现将MATLAB工作环境的M文件和MEX文件封装为组件，在其他兼容COM组件的编译环境包括Visual C++，Visual Basic，Java等直接进行调用。

#### 1\. MATLAB编译器(Compiler)

使用MATLAB Compiler可以将M文件转化为C, C++和MEX文件。首先使用mex –setup和mbuild –setup命令配置MATLAB Compiler的编译环境，使用mcc命令将M文件转化为可独立与MATLAB开发环境的动态链接库文件(DLL文件)和exe文件。使用MATLAB自带的编译器将M文件转化为Dll文件和exe文件，一方面可以保持MATLAB强大的数学运算功能，同时编译生成的C, C++代码，可以加快程序的运行速度，也可以实现纯文本 (Script)的M文件代码的隐蔽性。但是使用mcc命令编译后生成的.cpp文件，一般程序冗长，代码可读性比较差，但对于应用程序使用者而言，程序代码是隐蔽的，因此也不太影响应用程序的使用。在读者充分熟悉MATLA开发环境的C/C++数学库的前提下，读者可以实现在C++语言中直接调用MATLAB的C/C++数学库相关命令，从而优化mcc命令自动编译生成的C，C++程序代码。

#### 2\. MATLAB引擎技术

MATLAB应用程序接口(API)同时提供了一组引擎函数来启动和调用MATLAB函数。通过MATLAB引擎技术，可以兼顾两方面的优点，一是保持C++编程语言的高效性，二是可以直接调用MATLAB丰富的工程应用函数，包括复杂的数学分析和信号处理函数等。在一些特定的应用场合中，前台可以使用C++，C或者FORTRAN语言编写人机接口界面，实现前台的用户界面接口以及后台的数据通信，而后台则使用MATLAB引擎实现复杂的数学分析和信号分析处理功能，这样可以极大简化使用C++，C或者FORTRAN语言编写复杂运算函数的难度，缩短应用程序的开发周期，同时可以保证应用程序具备较高的可靠性。

#### 3\. MAT文件

在MATLAB开发环境中，数据的存储通常以一种特殊的二进制文件MAT数据文件来进行存储。与其他语言环境进行数据通信中，也通常使用MAT文件数据格式。在MATLAB应用程序接口(API)函数库中提供了丰富的接口函数实现对MATLAB不同格式的数据进行读取和存储。在其他语言环境中，可以使用MAT函数库，MEX函数库和MX函数库相关函数进行数据文件的操作，从而实现MATLAB语言与外部编程环境的数据接口。

#### 4\. MEX文件

MEX文件是一种MATLAB可执行的程序文件，通过编写mexFunction函数入口，将C，C++和FOTRAN等语言的程序代码嵌入到MEX文件中，实现在MATLAB开发环境中调用其他语言程序代码。使用MEX函数库和MX函数库，可以实现不同数据格式的创建，赋值和矩阵基本操作，通过MEX命令将M文件直接编译成动态链接库文件或者其他MATLAB可直接运行的可执行文件。使用MEX文件，可以直接嵌入其他语言功能程序代码段，而不需要重新编写相应功能的M文件代码，这无疑为程序代码的移植和重用提供了一种非常有效而且高效的途径。

#### 5\. MATCOM实现MATLAB与Visual C++接口

MATCOM是MathTool公司推出的一种MATLAB编译平台，可以对MATLAB函数进行文本编译，直接运行，或者将MATLAB开发环境的M文件编译成.exe文件和.dll文件。当前MATCOM的最高版本是MATCOM4.5版本，可以支持与Visual VC++的混合代码编译。MATCOM提供了Visual MATCOM工具来实现在Visual C++环境下编译运行MATLAB的M文件。在Visual C++中启用Visual MATCOM Add-in插件，可以直接将MATLAB的M文件导入Visual C++环境中，并自动转化为对应的.h头文件和.cpp文件，相比与MATLAB自带的编译器(Compiler)而言，MATCOM将M文件转化后的.cpp文件简单易读，程序代码可读性好。MATCOM同时也提供了自带的Matrix<LIB>C++数学库，该数学库使用Mm数据类型，包含众多的数学函数，可以实现在Visual C++中使用这些数据函数进行数学分析，信号处理，图像处理等，使用Matrix<LIB>的C++数学库进行C++编程，可以极大提高程序代码效率。

#### 6\. MATLAB COM Builder

MATLAB COM Builder为MATLAB6.5版本后提供的另外一种强大的接口编程方式。COM(Component Object Model)即组件对象模型是微软公司提出的以组件为发布单元的软件开发技术。将不同语言，函数封装为基本的组件，独立与语言环境运行。而MATLAB COM Builder正式基于COM概念而开发的组件编译界面。使用MATLAB COM Builder可以把MATLAB环境中开发的M文件，MEX文件等编译为组件，使之成为独立的COM对象，可以被其他支持COM语言的开发环境使用，如VC，JAVA，VB，Microsoft EXCEL等。

## 16.2 创建C语言MEX文件

MATLAB通过MEX文件可以实现与C，C++和FORTRAN语言的接口，在MATLAB开发环境中，非常方便地嵌入C，C++和FORTRAN语言函数。对于不同的操作系统，通过MEX编译命令，创建不同文件扩展名的MATLAB可执行MEX文件。
###16.2.1 MEX文件简介

MEX文件可以方便实现在MATLAB开发环境下直接编写C, C++或者FORTRAN语言程序，通过MATLAB应用程序接口(API)接口函数，将文件编译成可独立执行的应用程序或者MATLAB函数可以直接调用的MEX程序，极大提高了计算机应用程序代码的可移植性，代码的执行速度和执行效率，极大扩展MATLAB语言的应用场合。MEX文件主要在以下几个场合中应用：
* 通过MATLAB应用程序接口(API)函数库，把用C, C++或者Fortran等程序设计语言编写的函数或者子程序，编译成MEX文件后，在MATLAB工作环境中直接调用，而不必重新编写函数或子程序对应功能的M文件，实现计算机不同语言程序代码的移植；

*  由于MATLAB为解释性语言，在执行M文件的过程中，边解释边执行，执行速度慢，因此对于一些计算复杂，运算时间长的功能程序代码，可以编写相应的C, C++或者Fortran程序，编译成MEX文件后，提高MATLAB程序代码的运行速度和执行效率；

*  利用MEX文件可以直接编写硬件驱动程序，实现与底层硬件设备的接口，极大扩展MATLAB开发环境的应用场合；

MATLAB与外部程序的接口主要通过应用程序接口(API)函数库来实现。MEX文件编程中使用比较频繁的函数库包括MEX函数库和MX函数库。在16.3节MAT文件的应用一节中，将详细介绍MAT函数库，在16.4节MATLAB引擎技术一节中，将重点介绍Engine函数库。

#### 1\. MEX文件的基本结构

首先创建以下简单的mexSimpleDemo.c文件，放置与Matlab当前的工作路径下，同时建立一个同名的mexSimpleDemo.m文件，以便验证MATLAB在调用MEX文件和M文件的优先顺序。
```C++
/*
 * mexSimpleDemo.c
*/

#include "mex.h"
double mexSimpleDemo (double *y, double a, double b);

void mexFunction(int nlhs, mxArray *plhs[],
				  int nrhs, const mxArray *prhs[])
{
	//变量声明
	double *y;
	double m,n;
	
	//输入输出参数个数检测
	if (nlhs != 1)
		mexErrMsgTxt("Error: At least one output parameter is required!");
	if (nrhs > 2)
		mexErrMsgTxt("Error: No more than two input parameters");
			
	//获取输入变量的数值大小
	m = mxGetScalar( prhs[0] );
	n = mxGetScalar( prhs[1] );
	
   //获取输出变量的指针和建立初始值。
	plhs[0] = mxCreateDoubleMatrix(1,1,mxREAL);
	y = mxGetPr(plhs[0]);
	
	//调用子函数
	mexSimpleDemo (y, m ,n);
	
}

//算法子程序
double mexSimpleDemo(double *y, double a, double b)
{
    return *y = (a>b)?a:b;
}
```

从算法子程序可以看出，mexSimpleDemo程序实现求解两个输入变量的最大值，即max函数的功能。在Matlab命令行窗口中，输入以下命令：
```matlab
>> mex mexSimpleDemo.c
```
编译成功后，就可以直接在Matlab命令行窗口中调用mexSimpleDemo文件：
```
>> a=mexSimpleDemo(5,3)
a =     
5
```
为了验证MATLAB在调用MEX文件, DLL文件和M文件的优先级，在MATLAB当前工作窗口中建立一个同名的mexSimpleDemo.m文件。
```matlab
function c=mexSimpleDemo(a,b)
if(a>b)
    c = a;
else
    c = b;
```
通过which命令，可以查看Matlab调用mexSimpleDemo文件的优先顺序：
```matlab
>> which mexSimpleDemo
C:\Program Files\MATLAB\R2006a\work\mexSimpleDemo.mexw32
```

显示结果表明，MATLAB优先调用编译后的MEX文件，而不是m文件。从以上简单的程序实例可以看到一般编写C语言MEX文件的基本结构，首先头文件中必须包含mex.h，然后是C语言编写的算法子程序声明，在这里可以直接利用C语言编写程序代码，将C语言编写的算法函数直接移植到MATLAB开发环境中。
```
#include "mex.h"   //mex.h头文件
double mexSimpleDemo (double *y, double a, double b); //C语言算法程序声明
```
使用C语言编写的MEX文件均以mexFunction命名，输入参数列表中包括两个整数变量和两个mxArray数据结构的指针标量。
```
void mexFunction(int nlhs, mxArray *plhs[],
				  int nrhs, const mxArray *prhs[])
```
其中，输入参数nlhs和nrhs分别表示输入参数个数和输出参数个数；指针plhs和prhs分别指向输出矩阵和输入参数矩阵的头指针。通过mxGetScalar或者mxGetPr来获取输入参数和地址。在定义程序相关变量后，需要对输入输出参数列表的变量类型，参数个数进行检测：
```
if (nlhs != 1)   //输出变量个数检测
		mexErrMsgTxt("Error: At least one output parameter is required!");
	if (nrhs > 2)    //输入变量个数检测
		mexErrMsgTxt("Error: No more than two input parameters");
```
在C语言MEX文件中，通过mxGetScalar来获取输入变量的数值，使用mxGetPr来获取实数输出参数的指针，需要获取虚数的输出参数指针时使用mxGetPi函数，输出参数需要使用mxCreate前缀函数进行初始化。 在后续的相关章节中，将会详细介绍C语言编写MEX文件中常用的相关函数。
```
//获取输入变量的数值大小
	m = mxGetScalar( prhs[0] );
	n = mxGetScalar( prhs[1] );
   //获取输出变量的指针和建立初始值。
	plhs[0] = mxCreateDoubleMatrix(1,1,mxREAL);
	y = mxGetPr(plhs[0]);
```
获取输入参数数值和输出参数列表的指针后，就可以直接调用C语言程序：
```
//调用子函数
	mexSimpleDemo (y, m ,n);
```
#### 2\. MEX文件的扩展名类型

在不同的操作系统下，使用MEX命令编译后的文件扩展名不相同，表13.1所示为不同操作系统平台下编译MEX文件后的扩展名。

表16.1  不同操作系统平台下编译MEX文件后的扩展名
|操作系统平台	|文件扩展名|
|---|---|
HP-UX	|.mexhpux
Linux(32位)	|.mexglx
Linux X86-64	|.mexa64
Macintosh	|.mexmac
Solaris	|.mexsol
Windows(32位)	|.mexw32
Windows X64	|.mexw64

#### 3\. C语言MEX文件常用函数

使用MATLAB应用程序接口(API)函数库编写MEX文件时，使用比较频繁的是MEX函数库和MX函数库。两个函数库的功能不同，MEX函数库主要实现与MATLAB工作环境进行接口，例如mexEvalString函数就可以在MATLAB的命令行窗口中执行对应的字符串语言，MX函数库主要是矩阵操作函数库，例如mxGetScalar为获取参数数值，mxCreateDoubleMatrix为创建浮点类型的矩阵等。表16.2和表16.3列出了常用MEX函数库函数和MX函数库函数。在表16.3中，由于MX函数库函数众多，相同前缀的MX函数功能和调用方法类似，在这里不一一列出相关函数的调用方法，读者可以参阅MATLAB的函数帮助文档。在下一节中，也会通过实例来具体演示相关函数的使用。

表16.2  常用MEX函数库函数 
|函数名称	|功能描述|
|---|-----|
`mexCallMATLAB`	|调用Matlab函数
`mexEvalString`	|在Matlab窗口中执行字符串命令
`mexFunction`|	C语言MEX文件的定义
`mexGet`|	获取图形对象特定属性值
`mexGetVariable`	|将工作窗口中的变量拷贝给定义变量
`mexPutVariable`	|把mxArray临时变量拷贝到给定的工作窗口中
`mexErrMsgTxt`	|在工作窗口中显示错误信息
`mexWarnMsgTxt`	|在工作窗口中显示警告信息

表16.3  常用MX函数库函数

| 函数名称| 功能描述 |
|----|-----|
`mxCalloc`	|给矩阵分配临时内存空间
`mxDestroyArray`	|释放临时分配的内存空间
`mxGet前缀函数`	|获取变量数值，类型，指针等
`mxCreate前缀函数`|	创建不同数据类型的矩阵，向量等
`mxIs前缀函数	`|数据类型，内存空间等判断函数
`mxSet前缀函数`	|设置变量数据维数，大小指针等函数
