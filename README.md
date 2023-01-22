# Results of multithreading tutorial

Research is based on video [**Python Multiprocessing Tutorial: Run Code in Parallel Using the Multiprocessing Module**](https://www.youtube.com/watch?v=fKl2JW_qrso&ab_channel=CoreySchafer)

**To run these files and verify the correctness of the programs yourself, you can use the following commands**:

on **macOS**/**linux**:

```
python3 <filename>
```

on **windows**:

```
python <filename>
```

<br />

## Test example

1. [Initial example](initial_example.py)

   First, consider a test case in which we call a function that sleeps for one second twice.

   The result of the program will be:

   ```
    Sleeping for 1 second...
    Done sleeping!
    Sleeping for 1 second...
    Done sleeping!
    Finished in 2.01 second(s)
   ```

   These functions are run one after the other, running for 1 second each, so the script takes 2 seconds to execute in this case.

2. [Initial example with threads](initial_example_with_threads.py)

   Let's add threads to the previous program.

   The result of the program will be:

   ```
    Sleeping for 1 second...
    Sleeping for 1 second...
    Done sleeping!
    Done sleeping!
    Finished in 1.01 second(s)
   ```

   As we can see, in this case both function calls occur simultaneously and the execution is parallel.

   > Not really in parallel, because due to the python implementation, it can't run in parallel. This is the so-called pseudo-parallelism, when threads switch between each other and only one thread can be active at a time.

3. [Initial example with threads using loop](initial_example_with_threads_in_loop.py)

   If we need to run many threads in order not to write all these structures manually, we can use loops. In this case, we create 10 threads in the loop and run them "simultaneously".

   In this case the result of the program will be:

   ```
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Sleeping for 1 second...
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Finished in 1.0 second(s)
   ```

   As we can see in this case, we started 10 threads that run for 1 second each, but the whole program also took 1 second to run because all the functions were running in different threads.

4. [Initial example with threads using loop with args](initial_example_with_threads_in_loop_with_args.py)

   If we need to pass parameters to a function, we can use the **args** parameter and pass an array of arguments there.

   The result of the program will be:

   ```
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Sleeping for 1.5 second(s)...
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Done sleeping!
    Finished in 1.51 second(s)
   ```

   As we can see, the result is the same as in the previous case, but now we can specify how long to sleep for each function run.

5. [Initial example with threads using thread pool executor](initial_example_with_threads_with_pool.py)

   To simplify the work, you can use a tool called ThreadPoolExecutor.

   The result of the program will be:

   ```
    Sleeping for 5 second(s)...
    Sleeping for 4 second(s)...
    Sleeping for 3 second(s)...
    Sleeping for 2 second(s)...
    Sleeping for 1 second(s)...
    Done sleeping 1!
    Done sleeping 2!
    Done sleeping 3!
    Done sleeping 4!
    Done sleeping 5!
    Finished in 5.01 second(s)
   ```

   In this case, an instance of this class becomes available to us, with which we can easily create and manage threads.

   In this case, the **submit** function does the same as **start** and **join** for us. And to get the value of the thread after its execution, we can use **as_completed** and **result**.

6. [Initial example with threads using thread pool executor and map function](initial_example_with_threads_with_pool_with_map.py)

   Also, for simplification, and for the case when you need to get the result of the execution of threads in the same order in which they were called, you can use the map function.

   It also makes it easier to get the execution result from a code point of view.

   The result of the program will be:

   ```
    Sleeping for 5 second(s)...
    Sleeping for 4 second(s)...
    Sleeping for 3 second(s)...
    Sleeping for 2 second(s)...
    Sleeping for 1 second(s)...
    Done sleeping 5!
    Done sleeping 4!
    Done sleeping 3!
    Done sleeping 2!
    Done sleeping 1!
    Finished in 5.01 second(s)
   ```

## Real world example

In this case, we will consider a more real-world example of using multithreading.

Here we will look at a program that downloads heavy images from the Internet and stores them in a folder on your disk.

**Note**: The speed of the following programs will directly depend on the speed of your Internet, but the version with threads will be much faster.

1. [Real world example](real_worlds_example.py)

   In this case, the download is completely synchronous, that is, one image is downloaded first, after which the next one starts to download.

   The result of the program will be:

   ```
    images/photo-1516117172878-fd2c41f4a759.jpg was downloaded!
    images/photo-1532009324734-20a7a5813719.jpg was downloaded!
    images/photo-1524429656589-6633a470097c.jpg was downloaded!
    images/photo-1530224264768-7ff8c1789d79.jpg was downloaded!
    images/photo-1564135624576-c5c88640f235.jpg was downloaded!
    images/photo-1541698444083-023c97d3f4b6.jpg was downloaded!
    images/photo-1522364723953-452d3431c267.jpg was downloaded!
    images/photo-1513938709626-033611b8cc03.jpg was downloaded!
    images/photo-1507143550189-fed454f93097.jpg was downloaded!
    images/photo-1493976040374-85c8e12f0c0e.jpg was downloaded!
    images/photo-1504198453319-5ce911bafcde.jpg was downloaded!
    images/photo-1530122037265-a5f1f91d3b99.jpg was downloaded!
    images/photo-1516972810927-80185027ca84.jpg was downloaded!
    images/photo-1550439062-609e1531270e.jpg was downloaded!
    images/photo-1549692520-acc6669e2f0c.jpg was downloaded!
    Finished in 71.57 second(s)!
   ```

2. [Real world example with threads](real_worlds_example_with_threads.py)

   However, if we rewrite the program above to use threads, we get a significant speedup because disk read/write operations are also multi-threaded.

   In case of threads the result of the program will be:

   ```
   images/photo-1507143550189-fed454f93097.jpg was downloaded!
   images/photo-1513938709626-033611b8cc03.jpg was downloaded!
   images/photo-1516117172878-fd2c41f4a759.jpg was downloaded!
   images/photo-1564135624576-c5c88640f235.jpg was downloaded!
   images/photo-1549692520-acc6669e2f0c.jpg was downloaded!
   images/photo-1516972810927-80185027ca84.jpg was downloaded!
   images/photo-1504198453319-5ce911bafcde.jpg was downloaded!
   images/photo-1530224264768-7ff8c1789d79.jpg was downloaded!
   images/photo-1550439062-609e1531270e.jpg was downloaded!
   images/photo-1524429656589-6633a470097c.jpg was downloaded!
   images/photo-1530122037265-a5f1f91d3b99.jpg was downloaded!
   images/photo-1522364723953-452d3431c267.jpg was downloaded!
   images/photo-1532009324734-20a7a5813719.jpg was downloaded!
   images/photo-1541698444083-023c97d3f4b6.jpg was downloaded!
   images/photo-1493976040374-85c8e12f0c0e.jpg was downloaded!
   Finished in 44.97 second(s)!
   ```

## Conclusions

As we can see on a real example, using threads for operations that require loading, writing to disk, etc., gives an increase in speed of about two times.
