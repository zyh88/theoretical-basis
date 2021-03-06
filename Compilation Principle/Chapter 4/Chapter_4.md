# Chapter 4 语法分析

## 4.1 自顶向下分析概述

- 从分析树的顶部向底部方向构造分析树
- 可以看成是从文法开始符号S推导出词率W的过程
- 每一步推导中，需要做两个选择
  - 替换当前句型中的哪个非终结符
  - 用该非终结符的哪个候选式进行替换

### 最左推导 

- 最左推导中，总是选择每个句型的最左非终结符进行替换

- 最左推导得到的是最左

### 最右推导

- 最右推导中，总是选择每个句型的最右非终结符进行替换

### 自顶向下的语法分析采用最左推导方式

- 总是选择每个句型的最左非终结符进行替换
- 根据输入流中的写一个终结符，选择最左非终结符的一个候选式

#### 例子：【详解】

### 自顶向下语法分析的通用形式

- 递归下降分析
  - 由一组过程组成，每个过程对应一个非终结符
  - 由文法符号S对应的过程开始，其中递归调用文法中其它非终结符对应的过程。如果S对应的过程体恰好扫描了整个输入串，则成功完成语法分析。

```
void A（）{
    for(i=1 to k){
        if(X是一个非终结符号)
        	调用过程X（）；
        	else if(X,等于当前的输入符号)
        		读入下一个输入符号;
        	else  错误;
    }
}
```

#### 预测分析

- 预测分析是递归下降分析奇数的一个特例，通过在输入中向前看固定个数（通常为1）符号来选择正确的产生式。
  - 可以对某些文法构造出向前看k个输入符号的预测分析器，该类文法有时也称为LL（k）文法类
- 预测分析不需要回溯，是一种确定的自顶向下分析方法
  - 回溯会导致效率较低
  - 回溯就是退回上一步重新尝试
  - 需要回溯的叫不确定分析器

## 4.2 文法转换

- 当同一非终结符的多个候选式存在共同前缀，将导致回溯现象【无法预测】
- 含有A定义为Aa形式产生式的文法称为直接左递归的。【左递归文法会使递归下降分析器陷入无限循环】
  - 如果一个文法中有一个非终结符A使得对某个串a存在推导出A开头的串，那么这个文法就是左递归的。
  - 经过两步或两步以上推导产生的左递归称为式简介左递归的。

### 消除左递归

#### 消除直接左递归

- 把左递归转换成右递归
- 付出代价：引进了一些非终结符和空产生式

#### 消除间接左递归

- 代入法
- 提取左公因子法

#### 代入算法

- 输入：不含循环推导和空产生式的文法G

- 输出：等价的无左递归文法

- 方法：

  ```
  按照某个顺序将非终结符号排序为A1,A2,…An
  for(1到n){
      for(1到i-1的每个j){
          将每个形如A
      }
      消除产生式之间的直接左递归
  }
  ```

  #### 提取左公因子算法

