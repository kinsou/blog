title: Clojure 例子（编译后java调用与.clj形式调用）
tags:
  - Clojure
categories:
  - Clojure
date: 2013-05-08 23:14:00
---
在网上找了好久没找到 clojure 入门例子，自己写一个分享一下吧。
## eclipse插件：
URL [http://ccw.cgrand.net/updatesite](http://ccw.cgrand.net/updatesite)
## 一、clojure 代码：

com/test/Demo.clj 
------------------------------------------
```clojure
(require ['com.demo.StringOp]);引入文件 

(ns com.test.Demo ;命名空间
  (:gen-class 
   :name com.test.Demo ;java类
   :methods [#^{:static true} [getStr [String] String]]) ;java 方法类型声明
  );定义头文件

 ;定义方法 getStr 参数 name
(defn -getStr [name](str(com.demo.StringOp/getStr name) " 结束！"))
```
com/demo/StringOp.clj
---------------------------------------------------
```clojure
(ns com.demo.StringOp)
(defn getStr [value] (str "测试字符串：'" value "'"))
```
## 二、java 代码：
```java
package com.kinsou;
 
import java.io.IOException;
import org.junit.Test;
import clojure.lang.RT;
import clojure.lang.Var;
import com.test.Demo;
import static org.junit.Assert.*;
 
/**
 * @author kinsou@gmail.com
 * @version
 * @since Ver 1.1
 * @Date 2012-12-5
 */
public class Main {
 
    /**
     * getStrTest1(class 调用)
     */
    private static String getStrTest1(String value) {
        Object obj = Demo.getStr(value);
        System.out.println(obj);
        return obj.toString();
    }
 
    /**
     * getStrTest2(.clj 调用)
     */
    private static String getStrTest2(String value) throws IOException {
        RT.loadResourceScript("com/test/Demo.clj");
        Var var = RT.var("com.test.Demo", "-getStr");
        Object obj = var.invoke(value);
        System.out.println(obj);
        return obj.toString();
    }
 
    @Test
    public void test() throws IOException {
        String value1="测试1";
        assertEquals(getStrTest1(value1),"测试字符串：'"+value1+"' 结束！");
        String value2="测试2";
        assertEquals(getStrTest2(value2),"测试字符串：'"+value2+"' 结束！");
    }
 
}
```