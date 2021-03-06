# **简述 ArrayList 与 LinkedList 的底层实现以及常见操作的时间复杂度**

**ArrayList**

先说说Arraylist，Arraylist是基于动态数组实现的，所以查找速度快，但是增删操作的速度会比较慢，但是为什么会这样？我解释一下动态数组，基本就可以明白这个问题了。

先说说静态数组是怎么来存储数据的，当我们使用new来创建一个数组，实际上是在堆上申请了一段连续的大内存，我们知道我们在java中创建数组的时候，会给他一个固定的大小，不能适应数据的动态增删，那么这个时候就有了所谓的动态数组，动态数组的本质就是，当数据超出当前数组的内存范围，会先试着比较数据长度和数组长度的1.5倍的大小，如果1.5倍大于元素长度(小于的话，则创建一个长度为数据长度的数组)，那么直接通过Arrays.copyOf得到一个新长度的数组，把原数据拷贝过去，释放掉旧的数组， 这个时候内存有很多是没有使用的，这个时候就可以执行增删操作。

在动态数组中，存储数据用的是一段连续的大内存，所以如果我们要在某一个位置添加或者删除一个元素，剩下的每个元素都要相应地往前或往后移动。如果该动态数组中的元素很多，那么，每当我们添加或删除一个元素后，需要移动的元素就非常多，因此，效率就比较低。而查找的时候，由于每个元素占用内存相同，可以通过下标迅速访问数组中任何元素。

这就是为什么ArrayList的查找效率高，而增删操作的效率低了。

**LinkedList**

LinkedList是基于双向链表的数据结构实现的，链表是可以占用一段不连续的内存空间的，双向链表有前驱节点和后驱节点，里面存储的是上一个元素和后一个元素所在的位置，中间的黄色部分就是业务数据了，当我们需要执行插入的任务，比如第一个元素和第二个元素之间，只需要改变他们的前驱节点和后驱节点的指向就可以了，不要像动态数组那么麻烦，删除也是同样的操作，但是因为是不连续的内存空间，当需要执行查找，需要从第一个元素开始查找，直到找到我们需要的数据。

![img](https://img-blog.csdn.net/20180105104402234?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4NDIyMjc2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

这就是为什么LinkedList查找效率低，增删效率更高。

上面的分析也能看出，其实LinkedList更加节省内存空间，而ArrayList需要预留部分空间出来增加数据。



**总结** 
ArrayList和LinkedList在性能上各有优缺点，都有各自所适用的地方，总的说来可以描述如下： 
1．对ArrayList和LinkedList而言，在列表末尾增加一个元素所花的开销都是固定的。对ArrayList而言，主要是在内部数组中增加一项，指向所添加的元素，偶尔可能会导致对数组重新进行分配；而对LinkedList而言，这个开销是统一的，分配一个内部Entry对象。


2．在ArrayList的中间插入或删除一个元素意味着这个列表中剩余的元素都会被移动；而在LinkedList的中间插入或删除一个元素的开销是固定的。


3．LinkedList不支持高效的随机元素访问。


4．ArrayList的空间浪费主要体现在在list列表的结尾预留一定的容量空间，而LinkedList的空间花费则体现在它的每一个元素都需要消耗相当的空间


可以这样说：当操作是在一列数据的后面添加数据而不是在前面或中间,并且需要随机地访问其中的元素时,使用ArrayList会提供比较好的性能；当你的操作是在一列数据的前面或中间添加或删除数据,并且按照顺序访问其中的元素时,就应该使用LinkedList了。



**tips：**

ArrayList 是线性表（数组）
get() 直接读取第几个下标，复杂度 O(1)
add(E) 添加元素，直接在后面添加，复杂度O（1）
add(index, E) 添加元素，在第几个元素后面插入，后面的元素需要向后移动，复杂度O（n）
remove（）删除元素，后面的元素需要逐个移动，复杂度O（n）

LinkedList 是链表的操作
get() 获取第几个元素，依次遍历，复杂度O(n)
add(E) 添加到末尾，复杂度O(1)
add(index, E) 添加第几个元素后，需要先查找到第几个元素，直接指针指向操作，复杂度O(n)
remove（）删除元素，直接指针指向操作，复杂度O(1)