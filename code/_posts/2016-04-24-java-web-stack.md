---
title: "Java web-stack"
ref: java-web-stack
layout: post
lang: en
---

#### Article is not inished yet! Because the topic is so huge. Try finished russian-language page


Hello there, today i do want to summarize my whole JavaEE Course called "Programming of internet Applications"
in my lovely university, i want to tell where the Java is used and how it works.

### What is Java
Java - general purpose explicit language which can everything :)
I always wanted to describe a whole language by one piece of code. Alright, let's try.

Java is:

```Java
class Chart {
  private List<Point> points = new ArrayList<>();

  public void addPoint(Point point) {
    points.add(0, point);

    // free lst if it' filled
    if (points.size() > 10)
        points.remove(points.size() - 1);
  }
  public List<Point> getPoints() {
    return points;
  }
}

public class Program {
  public static void main(String[] args) {
    Chart chart1 = new Chart();
    Chart chart2 = new Chart();

    // do some logic here
  }
}
```

Java platform is divided from Java Standard Edition and Java Enterprise Edition.

### Java Standard Edition
Java standard edition(JavaSE further) - It's kind of language itself plus standard class library.
JavaSE defines wide general purpose API's.  

JavaSE includes:

* Java Language Specification - Language description, so you can write your own compiler.
* Java Class Library - Library you can use, there are ArrayList, Pair, Map classes and more.
* Java Virtual Machine Specification - Bytecode runtime environment description, so you can write your own Virtual machine.

Everyone familiar with Java knows the Oracle's Java Development Kit - canonical JavaSE realization.

### Java Enterprise Edition
Java Enterprise edition(JavaEE further) - It's JavaSE extension, huge web-development platform.
JavaEE includes API(different tier frameworks) and runtime environments(java-application-servers) for development and executing enterpirse-applications.
Enterprise application in general is an applications that helps company's business. Enterprise application can be a
complex site or mobile(JavaEE is only web) application.

Developers of JavaEE tried to achieve next goals:

* Huge applications - well, it's obvious
* Multi-tier applications - so different developers can work on their own piece(frontend, backend).
* Extensibility - so app can grow with company.
* Security - so no secrets can be exposed because of platform vulnerability.
* Reliability - so application can do everything.
