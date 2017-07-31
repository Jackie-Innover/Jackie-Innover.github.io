

# Thread

- **[Create Thread](#create-thread)**
- **[Interrupting Thread](#interrupting-thread)**
- **[Suspending and Resuming](#suspending-and-resume)**

extends Thread

implements Runable

start();

run();

interrupt();

interrupted();

isInterrupted();


### Create Thread

There are two ways to create threads: 

- extending the **java.lang.Thread** class 

  write a class extending the Thread class and overriding its run() method.

  The run() method provides the entry point for the thread, It contains codes to be executed concurrently with other threads.

-  implementing the **java.lang.Runable** interface.

  Since Java does not support multiple inheritance for classes, if a class has to extend another class, it cannot extend **Thread**. Fortunately, Java provides an alternative way to create threads where we create a class implementing the **Runnable** interface as follows:

  ```java
  public class SimpleThread2 implements Runnable {
      @Override
      public void run() {
          for (int i = 0; i < 100; i++) {
              System.out.println("In SimpleThread2: "+ i);
          }
      }
  }
  ```

  The class implements the run() method of Runnable interface. Note that an objects of this class is not a thread; it is merely runnable in the sense that its run(), method can be executed concurrently with other codes. The thread object is created using any of the following constructors of Thread class:

  ![Thread Runnable](images/thread_runnable.jpg)

------

### Interrupting Thread

Interrupting a thread means requesting it to stop what it is currently doing and do something else.

The request is sent to a thread using its **interrupt()** method that sets the thread's ***interrupt*** flag.

Note that methods such as sleep(), wait(), join() etc. throw an **InterruptedException** if they find interrupt flag set. So, a thread can use any of these methods in a try block and provide an appropriate catch block which gets executed when it is interrupted. In this way, a thread can determine if it is interrupted or not.

> Note:
>
> ```java
> /**
>  * Causes the currently executing thread to sleep (temporarily cease
>  * execution) for the specified number of milliseconds, subject to
>  * the precision and accuracy of system timers and schedulers. The thread
>  * does not lose ownership of any monitors.
>  *
>  * @param  millis
>  *         the length of time to sleep in milliseconds
>  *
>  * @throws  IllegalArgumentException
>  *          if the value of {@code millis} is negative
>  *
>  * @throws  InterruptedException
>  *          if any thread has interrupted the current thread. The
>  *          <i>interrupted status</i> of the current thread is
>  *          cleared when this exception is thrown.
>  */
> public static native void sleep(long millis) throws InterruptedException;
> ```

> Note:
>
> ```java
> /**
>  * Tests whether the current thread has been interrupted.  The
>  * <i>interrupted status</i> of the thread is cleared by this method.  In
>  * other words, if this method were to be called twice in succession, the
>  * second call would return false (unless the current thread were
>  * interrupted again, after the first call had cleared its interrupted
>  * status and before the second call had examined it).
>  *
>  * <p>A thread interruption ignored because a thread was not alive
>  * at the time of the interrupt will be reflected by this method
>  * returning false.
>  *
>  * @return  <code>true</code> if the current thread has been interrupted;
>  *          <code>false</code> otherwise.
>  * @see #isInterrupted()
>  * @revised 6.0
>  */
> public static boolean interrupted() {
>     return currentThread().isInterrupted(true);
> }
> ```

------

### Suspending and Resume

A thread may be suspended and resumed using the combination of **wait()** and **notify()** methods.

```java
public class SuspendAndResumeThread extends Thread {

    boolean active = true;

    public void Suspend(){
        active = false;
    }

    public synchronized void Resume(){
        active = true;
        notify();
    }

    @Override
    public synchronized void run() {
        try{
            while(true){
                if (active){
                    System.out.println("Running...");
                    Thread.sleep(500);
                }
                else{
                    System.out.println("Suspended...");
                    wait();
                }
            }
        }catch(Exception e){
            e.printStackTrace();
        }
    }
}

```

```java
SuspendAndResumeThread t = new SuspendAndResumeThread();
t.start();
while(true){
    try {
        Thread.sleep(1000);
        t.Suspend();
        Thread.sleep(1000);
        t.Resume();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```

The class SuspendAndResumeThread has a Boolean field active that represents the current status of the thread. The
methods Suspend() and Resume() change this flag to suspend and resume a thread respectively. The
main thread suspends and resumes after every 1 second. Here is a sample output:

```
Running...
Running...
Suspended...
Running...
Running...
Running...
Suspended...
Running...
Running...
Running...
```

> Note
>
> ```java
> /**
>  * Wakes up a single thread that is waiting on this object's
>  * monitor. If any threads are waiting on this object, one of them
>  * is chosen to be awakened. The choice is arbitrary and occurs at
>  * the discretion of the implementation. A thread waits on an object's
>  * monitor by calling one of the {@code wait} methods.
>  * <p>
>  * The awakened thread will not be able to proceed until the current
>  * thread relinquishes the lock on this object. The awakened thread will
>  * compete in the usual manner with any other threads that might be
>  * actively competing to synchronize on this object; for example, the
>  * awakened thread enjoys no reliable privilege or disadvantage in being
>  * the next thread to lock this object.
>  * <p>
>  * This method should only be called by a thread that is the owner
>  * of this object's monitor. A thread becomes the owner of the
>  * object's monitor in one of three ways:
>  * <ul>
>  * <li>By executing a synchronized instance method of that object.
>  * <li>By executing the body of a {@code synchronized} statement
>  *     that synchronizes on the object.
>  * <li>For objects of type {@code Class,} by executing a
>  *     synchronized static method of that class.
>  * </ul>
>  * <p>
>  * Only one thread at a time can own an object's monitor.
>  *
>  * @throws  IllegalMonitorStateException  if the current thread is not
>  *               the owner of this object's monitor.
>  * @see        java.lang.Object#notifyAll()
>  * @see        java.lang.Object#wait()
>  */
> public final native void notify();
> ```
> ```java
> /**
>  * Causes the current thread to wait until another thread invokes the
>  * {@link java.lang.Object#notify()} method or the
>  * {@link java.lang.Object#notifyAll()} method for this object.
>  * In other words, this method behaves exactly as if it simply
>  * performs the call {@code wait(0)}.
>  * <p>
>  * The current thread must own this object's monitor. The thread
>  * releases ownership of this monitor and waits until another thread
>  * notifies threads waiting on this object's monitor to wake up
>  * either through a call to the {@code notify} method or the
>  * {@code notifyAll} method. The thread then waits until it can
>  * re-obtain ownership of the monitor and resumes execution.
>  * <p>
>  * As in the one argument version, interrupts and spurious wakeups are
>  * possible, and this method should always be used in a loop:
>  * <pre>
>  *     synchronized (obj) {
>  *         while (&lt;condition does not hold&gt;)
>  *             obj.wait();
>  *         ... // Perform action appropriate to condition
>  *     }
>  * </pre>
>  * This method should only be called by a thread that is the owner
>  * of this object's monitor. See the {@code notify} method for a
>  * description of the ways in which a thread can become the owner of
>  * a monitor.
>  *
>  * @throws  IllegalMonitorStateException  if the current thread is not
>  *               the owner of the object's monitor.
>  * @throws  InterruptedException if any thread interrupted the
>  *             current thread before or while the current thread
>  *             was waiting for a notification.  The <i>interrupted
>  *             status</i> of the current thread is cleared when
>  *             this exception is thrown.
>  * @see        java.lang.Object#notify()
>  * @see        java.lang.Object#notifyAll()
>  */
> public final void wait() throws InterruptedException {
>     wait(0);
> }
> ```
> ```java
> /**
>  * Thrown to indicate that a thread has attempted to wait on an
>  * object's monitor or to notify other threads waiting on an object's
>  * monitor without owning the specified monitor.
>  *
>  * @author  unascribed
>  * @see     java.lang.Object#notify()
>  * @see     java.lang.Object#notifyAll()
>  * @see     java.lang.Object#wait()
>  * @see     java.lang.Object#wait(long)
>  * @see     java.lang.Object#wait(long, int)
>  * @since   JDK1.0
>  */
> public
> class IllegalMonitorStateException extends RuntimeException
> ```
>
> IllegalMonitorStateException表明当前的线程不是此对象监视器的所有者. 也就是要在当前线程锁定对象, 用锁定对象执行这些方法, 需要用到synchronized. 锁定什么对象就用什么对象来执行.
>
> 从notify()的注释来看, 一个线程成为对象监视器有三种方法:
>
> - 执行实例对象的同步方法
> - 执行类的同步静态方法
> - 执行在此对象上进行同步的[**synchronized**](synchronized.html)语句的正文.
>
> 对于一个对象, 某一时刻只能有一个线程拥有该对象的监视器.
>
> 
------

### Thread Priority

