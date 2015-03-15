---
layout: post
title: PHP Mess Detector 介绍
---

[PHPMD](http://phpmd.org/){:target="_blank"} 可以静态的分析代码，找出代码里面可能存在的问题比如：可能的错误、次优代码、过于复杂的表达式、未使用的参数，方法，属性，帮助我们提高代码质量<!-- more -->

### 通过 PEAR 安装

    $ pear channel-discover pear.phpmd.org
    $ pear channel-discover pear.pdepend.org
    $ pear remote-list -c phpmd
    $ sudo pear install --alldeps phpmd/PHP_PMD

### 使用
    # 可用规则 cleancode, codesize, controversial, design, naming, unusedcode
    $ phpmd /workspace/project/YourCode.php text codesize,controversial,naming,unusedcode

### 规则

#### Clean Code Rules

保持代码干净的基础

- BooleanArgumentFlag：布尔类型的参数违反了单一职责原则，一个方法只做一件事
- ElseExpression：
- StaticAccess：对方法内依赖对象存在静态调用的地方发生警告。

#### Code Size Rules

与代码复杂性或长度相关的规则集。

- CyclomaticComplexity: 复杂性是通过决策点在加上一个用于方法条目的方法的数目来确定, 决策点包括：'if', 'while', 'for', 'case labels'，1-4复杂度低，5-7显示适度的复杂性，8-10是高度复杂的，而11 +有很高的复杂性
- NPathComplexity: NPath 复杂性不能超过阀值
- ExcessiveMethodLength: 方法太长
- ExcessiveClassLength: 类太长
- ExcessiveParameterList: 方法参数过多
- ExcessivePublicCount: 一个类里面存在大量公共方法和属性
- TooManyFields:
- TooManyMethods: 个类有太多的方法
- ExcessiveClassComplexity:

#### Controversial Rules

有争议的规则

- Superglobals: 不要直接访问超全局变量
- CamelCaseClassName: 最好使用CamelCase命名法命名类
- CamelCasePropertyName: 最好使用CamelCase命名法命名属性
- CamelCaseMethodName: 最好使用CamelCase命名法命名方法
- CamelCaseParameterName: 最好使用CamelCase命名法命名参数
- CamelCaseVariableName: 最好使用CamelCase命名法命名变量

#### Design Rules

设计规则

- ExitExpression: 使用错误/异常代码返回代替 exit 表达式
- EvalExpression: 避免使用 eval 表达式
- GotoStatement: 避免使用 goto 语句
- NumberOfChildren: 控制子类数量
- DepthOfInheritance: 控制类继承的层次深度
- CouplingBetweenObjects: 避免过多的外部依赖

#### Naming Rules

命名规则

- ShortVariable: 存在过短的变量命名
- LongVariable: 存在过长的变量命名
- ShortMethodName: 存在过短的方法命名.
- ConstructorWithNameAsEnclosingClass: 构造函数方法不应该和封装的类名相同，考虑用 __construct 方法
- ConstantNamingConventions: 类/接口的常量必须采用大写
- BooleanGetMethodName: 返回布尔类型的 'getX()' 方法，安装该规则应该命名为 'isX()' 或者 'hasX()'

#### Unused Code Rules

未使用代码规则

- UnusedPrivateField: 存在声明了但未使用的私有变量
- UnusedLocalVariable: 存在声明了但未使用的局部变量
- UnusedPrivateMethod: 存在声明了但是未使用的私有方法
- UnusedFormalParameter: 避免传递不使用的参数给方法或者构造函数
