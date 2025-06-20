# ArrayList源码
## add源码机制
### 1，创建一个测试类
![Image](https://github.com/user-attachments/assets/4cb94f17-007e-4bf6-a2cf-fb0eb749f668)
创建一个无参构造器的ArrayList，for循环10次向集合中添加数据

### 2，第一次添加数据，先将基本数据类型转换对应的包装类型，进入add方法
![Image](https://github.com/user-attachments/assets/c423965e-d3ae-4053-bdc9-d58a10a0ba12)
modCount记录执行add方法的次数；e表示要添加的元素；elementData表示对象数组，size表示数组的大小；
![Image](https://github.com/user-attachments/assets/d72574e1-2dae-4bec-b4e8-5d1d21915c66)

### 3，进入add方法
![Image](https://github.com/user-attachments/assets/6c08e8e1-1178-48a1-9f1a-581188529236)
先判断elelmentData和size是否相等，相等，执行grow方法
![Image](https://github.com/user-attachments/assets/f1e34e47-b41b-4f17-b983-a90f0b91d062)
![Image](https://github.com/user-attachments/assets/25b6936f-9dfa-4698-89b5-7e31e3a61dfd)
1. minCapacity为最小容量，大小为size加1；oldCapacity为实际容量，大小为elementData的大小
2. 在grow方法中，判断实际数组的容量是否大于0或者是否不为null，显然第一次是不满足，执行else方法
3. 初始化elementData，大小为DEFAULT_CAPACITY(默认初始容量为10)和minCapacity的最大值，显然第一次初始化大小为10
4. 返回add方法，将第一个元素添加到数组的索引为0的位置，数组的大小加一，第一次add结束
5. 由于elementData在第一次add时就初始化为10，所以在执行下面的9次add元素都不会执行grow方法，就是依此添加元素到数组

### 4，在上面的基础上我们在添加一次循环，观察第二次数组扩容的机制
![Image](https://github.com/user-attachments/assets/41aed02e-66ba-4d1d-bdde-556e610bcddb)
添加数组10次后，数组的参数情况
![Image](https://github.com/user-attachments/assets/eb71df08-4146-48c5-9ade-c08314b503e3)
执行grow方法
![Image](https://github.com/user-attachments/assets/25b6936f-9dfa-4698-89b5-7e31e3a61dfd)
1，更新minCapacity为11，oldCapacity为10
2，满足if条件，调用ArraysSupport.newLength方法，返回实际数组长度大小+增长量 给newCapaticy
增长量：在满足最小增长量(minCapacity-oldCapaticy)的情况下，使用推荐增长量(oldCapaticy / 2)
因此，数组的第二次扩容就是按照原来的1.5倍扩容
3，通过数组扩容将扩充elementData的大小为newCapaticy
![Image](https://github.com/user-attachments/assets/8aecb9a8-5c9c-4e6b-b913-f80e7fd0576c)
4，返回add方法，将元素添加到数组中数组的大小加一

### 5，可以通过ArrayList的有参构造器手动设置数组的大小，但是第二次扩容还是按原来的1.5倍扩容













