Java多线程
==================

ThreadPoolExecutor
-------------------------

ThreadPoolExecutor构造方法参数详解
`````````````````````````````````````````

.. code-block:: java:
    
    /**
     * Creates a new {@code ThreadPoolExecutor} with the given initial
     * parameters.
     *
     * @param corePoolSize the number of threads to keep in the pool, even
     *        if they are idle, unless {@code allowCoreThreadTimeOut} is set
     * @param maximumPoolSize the maximum number of threads to allow in the
     *        pool
     * @param keepAliveTime when the number of threads is greater than
     *        the core, this is the maximum time that excess idle threads
     *        will wait for new tasks before terminating.
     * @param unit the time unit for the {@code keepAliveTime} argument
     * @param workQueue the queue to use for holding tasks before they are
     *        executed.  This queue will hold only the {@code Runnable}
     *        tasks submitted by the {@code execute} method.
     * @param threadFactory the factory to use when the executor
     *        creates a new thread
     * @param handler the handler to use when execution is blocked
     *        because the thread bounds and queue capacities are reached
     * @throws IllegalArgumentException if one of the following holds:<br>
     *         {@code corePoolSize < 0}<br>
     *         {@code keepAliveTime < 0}<br>
     *         {@code maximumPoolSize <= 0}<br>
     *         {@code maximumPoolSize < corePoolSize}
     * @throws NullPointerException if {@code workQueue}
     *         or {@code threadFactory} or {@code handler} is null
     */
    public ThreadPoolExecutor(int corePoolSize,
                              int maximumPoolSize,
                              long keepAliveTime,
                              TimeUnit unit,
                              BlockingQueue<Runnable> workQueue,
                              ThreadFactory threadFactory,
                              RejectedExecutionHandler handler)

- **int corePoolSize** 线程池核心线程数，初始线程数为0，在不超过此值的情况下，每次提交一个任务，就新起一个线程。

- **int maximumPoolSize** 线程池最大线程数，核心线程都在运行，又有新任务提交进来时且当前线程池线程数不超过此值时，新起线程执行任务。

- **long keepAliveTime** 当前线程池数目大于核心线程数，且有线程处于idle状态时，当线程处于idle的时间超过keepAliveTime和TimeUnit指定的时间时，线程就会被回收。

- **BlockingQueue<Runnable> workQueue** 阻塞队列，当线程池中线程数处于最大且都处于执行状态时，再提交进来任务放在此队列中

- **ThreadFactory threadFactor** 提供线程池新起线程的方法。

- **RejectedExecutionHandler handler** 当线程池满且阻塞队列也满的情况下，提交进来的任务，由此对象处理，需要自定义处理策略