## 指针
1. 指针能够指向一个无效的地址，有时被称为悬空指针。
2. 使用指向指针的指针作为参数。
3. void指针表示泛型指针。
4. 指针从地址中取到数据的类型由其自身类型决定。
5. 指针类型转换会破坏计算机本身的对齐方式。
6. 函数指针
## 存储空间
1. 直接声明变量时，编译器会根据变量的类型预留足够的内存空间。
2. 自动变量是一种在进入或离开一个模块或函数时其存储空间能够自动分配和释放的变量。
3. 通过malloc和realloc在运行时动态地分配存储空间，该存储空间是从堆存储中分配的，并且有我们自行管理，除非显式将它释放，不然会一直存在。
4. 内存泄漏问题是由于动态分配了内存空间，但从未释放它造成的。
5. 统一内存管理。
6. memcpy函数将一段数据从内存中的一个地方复制到另一个地方。
## 结构
1. 结构不允许包含自身的实例，但可以包含指向自身实例的指针。
## 数组
1. 数组是在内存中连续排列的同类元素的序列。
2. a[i] <=> *(a + i); a中i元素的地址是a所在的地址加上a中存储数据类型包含的字节数乘以i得到的。
## 递归
1. 递归过程中的两个基本阶段：递推与回归，一步步递推，一步步反向回归。
2. 当递归调用是整个函数体中最后执行的语句并且它的返回值不属于表达式的一部分时，这个递归调用是尾递归。
3. 尾递归在回归过程中不用做任何操作（编译器会对尾递归自动生成优化的代码）。
## 内存组织方式
1. 一个可执行程序由代码段、静态数据区、堆和栈4个区域组成。
  - 代码段包含程序运行时所执行的机器指令。
  - 静态数据区包含在程序生命周期内一直持久的数据，比如全局变量和静态局部变量。
  - 堆包含程序运行时动态分配的存储空间。
  - 栈包含函数调用的信息（输入参数、返回值空间、计算表达式时用到的临时存储空间、函数调用时保存的状态信息以及输出参数）。
## 链表
1. 单链表
2. 双向链表
3. 循环链表
