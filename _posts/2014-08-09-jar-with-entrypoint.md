---
layout: post
title: JAR with entrypoint
published: true
categories: [linux, programming]
tags: [jar, java]
---

Create a lightweigt sample project, for simplicity, we only have two files in the project.

```bash
$ mkdir jar_application
$ cd jar_application
$ touch Main.java
$ touch SampleBean.java
$ touch Manifest.txt
```

```text
# Manifest.txt
Main-Class: Main ↵
```

```java
// Main.java
public class Main {
  public static void main(String[] args) { 
    // TODO Auto-generated method stub
    SampleBean bean = new SampleBean("Jozsi", 2);
    
    System.out.println("Entry point of class Main");
    System.out.println(bean.getName());
  }
}
```

```java
// SampleBean.java
public class SampleBean {
  private String name;
  private int number;

  public SampleBean(String name, int number){
    this.name = name;
    this.number = number;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getNumber() {
    return number;
  }

  public void setNumber(int number) {
    this.number = number;
  }
}
```
---

In the manifest file, mind the CR (carriage return, enter, ↵). Next, enter these commands in the terminal.

```bash
$ jar cfm MyJar.jar Manifest.txt *.class
$ java -jar MyJar.jar
```