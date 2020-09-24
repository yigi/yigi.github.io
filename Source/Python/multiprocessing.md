Global Interpreter Lock is a boolean value in the Python interpreter protected by a mutex

How to deal with Python’s GIL problem

- Using multi-processing — The most popular way is to use a multi-processing approach where you use multiple processes instead of threads. Each Python process gets its own Python interpreter and memory space so that GIL won’t be a problem.

- Using a different interpreter — Python has multiple interpreter implementations. GIL exists only in the original Python implementation that is CPython. If your program with its libraries is available for one of the other implementations then you can try them out as well.

```python
import time
def is_prime(n):
      if (n <= 1) : 
          return 'not a prime number'
      if (n <= 3) : 
          return 'prime number'
          
      if (n % 2 == 0 or n % 3 == 0) : 
          return 'not a prime number'
    
      i = 5
      while(i * i <= n) : 
          if (n % i == 0 or n % (i + 2) == 0) : 
              return 'not a prime number'
          i = i + 6
    
      return 'prime number'
    
starttime = time.time()
for i in range(1,10):
    time.sleep(2)
    print('{} is {} number'.format(i, is_prime(i)))
print()    
print('Time taken = {} seconds'.format(time.time() - starttime))
```

<img align="center" width="400" height="250" src="https://miro.medium.com/max/487/1*y49uIX5VXBWmNoe6v-540g.png">


### Advantages of Multiprocessing

- Increased Throughput − By increasing the number of processors, more work can be completed in the same time.

- Cost Saving − Parallel system shares the memory, buses, peripherals etc. Multiprocessor system thus saves money as compared to multiple single systems. Also, if a number of programs operate on the same data, it is cheaper to store that data on one single disk and shared by all processors of the system instead of using many copies of the same data.

- Increased Reliability − In this system, as the workload is distributed among several processors which results in increased reliability. If one processor fails then its failure may slightly slow down the speed of the system but system will work smoothly.

## Using Process class

The process class stores the processes in memory and allocates the jobs to the available processors using a FIFO scheduling. When the process is ended, it pre-empts and plans the new process for execution.

```python
import time
import multiprocessing
def is_prime(n):
      if (n <= 1) : 
          return 'not a prime number'
      if (n <= 3) : 
          return 'prime number'
          
      if (n % 2 == 0 or n % 3 == 0) : 
          return 'not a prime number'
    
      i = 5
      while(i * i <= n) : 
          if (n % i == 0 or n % (i + 2) == 0) : 
              return 'not a prime number'
          i = i + 6
    
      return 'prime number'
def multiprocessing_func(x):
    time.sleep(2)
    print('{} is {} number'.format(x, is_prime(x)))
    
if __name__ == '__main__':
    starttime = time.time()
    processes = []
    for i in range(1,10):
        p = multiprocessing.Process(target=multiprocessing_func, args=(i,))
        processes.append(p)
        p.start()
        
    for process in processes:
        process.join()
        
    print()    
    print('Time taken = {} seconds'.format(time.time() - starttime))
```

<img align="center" width="400" height="250" src="https://miro.medium.com/max/468/1*44lINvP-3XntPe7nR4kgTQ.png">

## Using Pool class

The pool class schedules execution using FIFO policy. It workings like a map reduce design. The input are mapped from different processors and bring together the output from all the processors. After the running the code, it restores the output in the form of a list or array. It waits for all the jobs to finish and then returns the output. The processes in execution are put in memory and other non-executing processes are puts away out of memory.

```python
import time
import multiprocessing
def is_prime(n):
      if (n <= 1) : 
          return 'not a prime number'
      if (n <= 3) : 
          return 'prime number'
          
      if (n % 2 == 0 or n % 3 == 0) : 
          return 'not a prime number'
    
      i = 5
      while(i * i <= n) : 
          if (n % i == 0 or n % (i + 2) == 0) : 
              return 'not a prime number'
          i = i + 6
    
      return 'prime number'
def multiprocessing_func(x):
    time.sleep(2)
    print('{} is {} number'.format(x, is_prime(x)))
    
if __name__ == '__main__':
    starttime = time.time()
    pool = multiprocessing.Pool()
    pool.map(multiprocessing_func, range(1,10))
    pool.close()
    print()
    print('Time taken = {} seconds'.format(time.time() - starttime))
```

<img align="center" width="400" height="250" src="https://miro.medium.com/max/463/1*ubuThDHEEP9Cn2vBT3FS9g.png">

