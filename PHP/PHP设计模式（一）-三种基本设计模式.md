---
title: PHP设计模式（一）-三种基本设计模式
date: 2019-07-13 22:00:14
tags:
 - 设计模式
 - PHP设计模式
---

# PHP设计模式

## 3种基本设计模式（面向对象中常见的设计模式）

### 工厂模式

使用【工厂方法或者类】生成对象，而不是在代码中直接new对象。

~~~php
<?php
//  工厂模式的实现 Factory.php
namespace IMooc;
class Factory
{
    static function createDatabase()
    {
        $db = new DataBase();
        return $db;
    }
}

// index.php
<?php
    $db = IMooc\Factory::createDatabase();
~~~

【为什么工厂模式比直接new一个对象好呢？】

假如说DataBase这个类在很多个PHP文件中都进行了一个new操作，那这个时候这个DataBase对象发生了变更，比如一些参数变化。不使用工厂模式，则使用DataBase类的PHP文件都需要修改代码。而使用工厂模式之后，只需要在工厂方法中把这个类的名称或者参数修改即可。

工厂模式也是其他设计模式惯用的一个基础的设计模式。

很多高级模式依赖于工厂模式。

### 单例模式

使某个类的对象仅允许创建一次

### 注册模式

解决全局共享和交换对象。





