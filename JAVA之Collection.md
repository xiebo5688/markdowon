---
enable html: true
---
# **JAVA之Collection**
java各集合之间的关系
![](http://img.blog.csdn.net/20160706172512559?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

## Collection主要方法：

`boolean add(Object o)添加对象到集合`
`boolean remove(Object o)删除指定的对象`
`int size()返回当前集合中元素的数量`
`boolean contains(Object o)查找集合中是否有指定的对象`
`boolean isEmpty()判断集合是否为空`
`Iterator iterator()返回一个迭代器`
`boolean containsAll(Collection c)查找集合中是否有集合c中的元素`
`boolean addAll(Collection c)将集合c中所有的元素添加给该集合`
`void clear()删除集合中所有元素`
`void removeAll(Collection c)从集合中删除c集合中也有的元素`
`void retainAll(Collection c)从集合中删除集合c中不包含的元素`
## collection主要子接口对象
### List(抽象接口，可重复有序)
list主要方法：
`void add(int index,Object element)在指定位置上添加一个对象`
`boolean addAll(int index,Collection c)将集合c的元素添加到指定的位置`
`Object get(int index)返回List中指定位置的元素`
`int indexOf(Object o)返回第一个出现元素o的位置.`
`Object remove(int index)删除指定位置的元素`
`Object set(int index,Object element)用元素element取代位置index上的元素,返回被取代的元素
void sort()`
List主要子接口对象
`LinkedList没有同步方法`
`ArrayList非同步的（unsynchronized）`
`Vector(同步) 非常类似ArrayList，但是Vector是同步的`