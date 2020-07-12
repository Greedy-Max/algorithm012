## 1.Queue源码分析：
### 简述
 Queue是java中实现队列的接口，继承自Collection类，是一个FIFO队列，其实现类包含两种：
   线程不安全：LinkedList、Priority Queue
   线程安全：LinkedBlockingQueue、BlockingQueue、ArrayBlockingQueue、PriorityBlockingQueue
   
   接口中包含六个方法：
     添加元素：
       add(E e):未超出容量，从队尾压入元素，当超出队列容量时抛出异常
       offer(E e):未超出容量，从队尾压入元素，当超出队列容量时不抛异常，返回false
     删除元素：
       remove():删除并返回队头元素，当队列容量为0时，抛出NoSuchElementException异常
       poll():删除并返回队头元素，当队列容量为0时，返回null
     获取头部元素：
       element():容量大于0的时候，都返回队头元素，但是不删除；当容量为0时会抛出NoSuchElementException
       peek():容量大于0的时候，都返回队头元素，但是不删除；当容量为0时返回null
       
       
## 2.PriorityQueue源码分析：
### 简述    
 PriorityQueue是优先队列，Queue接口的实现类，通过比较器实现元素的处理优先级，默认优先级按照自然顺序；提供了七个构造方法：
     PriorityQueue():无参构造器，默认队列大小为11，默认优先级按照自然顺序
     PriorityQueue(int initialCapacity):
     PriorityQueue(Comparator<? super E> comparator):
     PriorityQueue(int initialCapacity,Comparator<? super E> comparator):
     PriorityQueue(Collection<? extends E> c):
     PriorityQueue(PriorityQueue<? extends E> c):
     PriorityQueue(SortedSet<? extends E> c):
     
  底层通过数组标识的小顶堆实现
  提供的相关方法：
     添加元素(时间复杂度为O(logn))：
        add(E e):底层调用了offer()方法
        offer(E e):未超出容量，从队尾压入元素，当超出队列容量时不抛异常，返回false（会调用siftUp（）方法对数据进行调整）
             执行步骤：1）判断添加的元素是否为空，为空抛异常
                     2）队列的操作次数+1
                     3）如果队列元素个数超过队列长度进行扩容（扩容类似于ArrayList中的扩容）
                     4）如果首次添加，直接加入队列，返回true；如果非首次添加则进行优先级调整，将元素放入队列
                        此时会判断比较器是否为空，如果非空使用当前比较器进行处理，如果为空则使用默认比较器进行处理
     删除元素：
        remove():父类的方法，删除并返回队头元素，当队列容量为0时，抛出NoSuchElementException异常
        poll():删除并返回队头元素，当队列容量为0时，返回null，同时会调用siftDown（）方法对数据进行调整，时间复杂度为O(logn)
        remove(Object o):删除指定元素（如果有多个相等，只删除一个），该方法不是Queue接口内的方法，而是Collection接口的方法。
                         由于删除操作会改变队列结构，所以要进行调整；并且删除元素的位置可能是任意的，所以调整过程比其它函数稍加繁琐。
                         具体来说，remove(Object o)可以分为2种情况：
                            1. 删除的是最后一个元素。直接删除即可，不需要调整。
                            2. 删除的不是最后一个元素，从删除点开始以最后一个元素为参照调用一次siftDown()即可
                         该方法的时间复杂度为O(n)
     获取头部元素（时间复杂度为O(1)）：
        element():容量大于0的时候，都返回队头元素，但是不删除；当容量为0时会抛出NoSuchElementException
        peek():容量大于0的时候，都返回队头元素，但是不删除；当容量为0时返回null;
     包含元素：
        contains(Object o):需要遍历队列中所有元素，返回相等元素的下标，然后跟-1作比较，时间复杂度为O(n)
  
     

