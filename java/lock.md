# 线程锁

- [**可重入内置锁**](#可重入内置锁)
- **[公平锁和非公平锁](#公平锁和非公平锁)**
- bb
- cc



------

### 可重入内置锁

每个Java对象都可以用作实现同步的锁 (*因为Object有notify()和wait()*), 这些锁被成为内置锁或者监视器锁.

内置锁是一种互斥锁, 同一时刻只允许一个线程执行内置锁保护的代码. 所以, 一旦程序执行到synchronized锁包括的代码时, 就会去拿内置锁, 如果内置锁没有被别的线程占用, 则拿到锁, 待执行完相关的代码后, 释放锁. 如果内置锁已经被其他线程占用, 则等待.

线程在进入同步代码块之前会自动获取锁, 并且在退出同步代码块时自动释放锁. 获得内置锁的唯一途径就是进入由这个锁保护的同步代码或方法.

当某个线程请求一个由其他线程持有的锁时，发出请求的线程就会阻塞。然而，由于内置锁是可重入的，因此如果摸个线程试图获得一个已经由它自己持有的锁，那么这个请求就会成功。“重入”意味着获取锁的操作的粒度是“线程”，而不是调用。重入的一种实现方法是，为每个锁关联一个获取计数值和一个所有者线程。当计数值为0时，这个锁就被认为是没有被任何线程所持有，当线程请求一个未被持有的锁时，JVM将记下锁的持有者，并且将获取计数值置为1，如果同一个线程再次获取这个锁，计数值将递增，而当线程退出同步代码块时，计数器会相应地递减。当计数值为0时，这个锁将被释放。

```java
/**
 * 主要为了测试，子类覆盖父类方法后，调用子类方法时，也获取父类的锁
 *
 * @author ChenHui
 *
 */
public class TestWidget {

    public static void main(String[] args) throws InterruptedException {

        final LoggingWidget widget = new LoggingWidget();
        Thread th1 = new Thread("th1") {
            @Override
            public void run() {
                System.out.println(super.getName() + ":start\r\n");
                widget.doSometing();
            }
        };

        Thread th2 = new Thread("th2") {
            @Override
            public void run() {
                System.out.println(super.getName() + ":start\r\n");
                /** 为了说明子类复写父类方法后，调用时也持有父类锁*/
                widget.doAnother();
                /**证明了内置锁对那些没有加synchronized修饰符的方法是不起作用的*/
                // widget.doNother();
                /**为了说明子类复写父类方法后，调用时也持有父类锁，也持有自己本类的锁*/
                // widget.doMyLike();
                /**这是两个线程，这是需要等待的，并不是继承的关系，不是重入，重入是发生在一个线程中的*/
                // widget.doSometing();
            }
        };

        th1.start();
        Thread.sleep(1000);
        th2.start();
    }
}

class Widget {
    public synchronized void doSometing() {
        System.out.println("widget ... do something...");
    }

    public synchronized void doAnother() {
        System.out.println("widget... do another thing...");
    }

    public void doNother() {
        System.out.println("widget... do Nothing...");
    }
}

class LoggingWidget extends Widget {

    @Override
    public synchronized void doSometing() {
        try {
            System.out.println("loggingwidget do something...");
            Thread.sleep(3000);
            System.out.println("end loggingwidget do something...");
        } catch (InterruptedException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        super.doSometing();
    }

    public synchronized void doMyLike() {
        System.out.println("loggingwidget do my like...");
    }
}
```

在例子中，子类覆盖了父类的synchronized 类型的方法，并调用父类中的方法。如果没有可重入的锁，子类中可能就会产生死锁，因为Widget和LoggingWidget中的dosomething方法都是synchronized 类型的，都会在处理前试图获得Widget的锁。倘若内部锁不是可重入的，super.doSomething的调用者就永远无法获得Widget的锁。因为锁已经被占用，导致线程永久的延迟，等待着一个永远无法获得的锁。



### 公平锁和非公平锁

