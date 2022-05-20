# python-ultimate-guide
Python language concepts guide

## Multitasking

- [x] **GIL, Multiprocessing, Threading, Asyncio**
- https://realpython.com/python-gil/
- https://realpython.com/python-concurrency/
- https://realpython.com/async-io-python/
- https://realpython.com/intro-to-python-threading/  

pre-emtive multitasking (threading) - os decides to switch tasks external to Python  
cooperative multitasking (asyncio) - tasks decide when to give up control  
multiprocessing - different processes

multithreading: ThreadPoolExecutor, executor.map, thread_local = threading.local(), race conditions, with threading.Lock() RLock(), 		Event, Semaphore, Timer, Barrier
thread.start() thread.join()

async io: event loop (uvloop), Asyncio.run(), Async with, async for

## Memory and GC

- [x] **Garbage collection, 3 generations, weakref**
- https://stackify.com/python-garbage-collection/
- https://devguide.python.org/garbage_collector/
- https://www.geeksforgeeks.org/weak-references-in-python/
- https://dev.nextthought.com/blog/2018/05/python-weakref-cython-slots.html  

reference cycle, gen gc (generations, threshold), gc module (1gen -> 2gen -> 3gen)

- [x] **Memory management: arenas, pools, blocks**
- https://realpython.com/python-memory-management/

Arenas: 256kb, double linked list of usable_arenas (sorted by number of free pools available, the most data closer). Only arenas can truly free memory  
Pools: 4kb, dbl linked list to pools with same size class: usedpools (contain data), freepools, full pools  
Blocks: linked list - all the same size within pool: untouched, free, allocated  

## Classes and OOP

- [x] **Duck Typing** https://machinelearningmastery.com/duck-typing-python/

- [x] **Multiple inheritance, MRO, __mro__, Mixin** https://realpython.com/python-super/

- [x] **Metaclass** https://realpython.com/python-metaclasses/  
Inherit ‘type’ in Meta + class Bar(metaclass=Meta) __new__  __init__

- [x] **Virtual classes, implementing interfaces, __subclasshook()__**
- https://realpython.com/python-interface/
- https://www.demo2s.com/python/python-virtual-subclasses.html
- https://medium.com/analytics-vidhya/abc-in-python-abstract-base-class-35808a9d6b32

ABC.register() make virtual class (not inherited but becomes issubclass()) doesn’t appear in MRO and can’t call super()  
_abc_registry - attr in ABC: weakset containing registered virtual classes of current abstract class  
ABC.register() cancels __subclasshook__

- [x] **Data Classes** https://realpython.com/python-data-classes/  
@dataclass(order, frozen) decorator  
implement __repr__ and __eq__  
field(default_factory=func())  
__slots__

- [x] **Descriptors** https://realpython.com/python-descriptors/  
Descriptor protocol (__get__ __set__ __delete__ __set_name__)  
Lookup chain: data descriptor -> obj.__dict__ -> non-data descriptor -> type(obj).__dict__ -> parent.type(obj).__dict__ -> MRO


## Scopes, functions, variables

- [x] **Functions considered first class objects** https://dbader.org/blog/python-first-class-functions

- [x] **PyObjects** https://realpython.com/pointers-in-python/  
Names instead of variables -> PyObject (C struct) {Type, Value, RefCount}, CPython interns (preallocates) numbers between -5 and 256 and strings < 20 chars  
Can emulate pointers with mutable type (dict, list, set)  

- [x] **Lambda, closure** https://realpython.com/python-lambda/

- [x] **Scopes LEGB, free variables, global, nonlocal** https://realpython.com/python-scope-legb-rule/

- [x] **Arguments in Python get passed by assignment** not by reference and not by value  https://realpython.com/python-pass-by-reference/

- [x] **Iterator vs generator, coroutine**
- https://realpython.com/python-for-loop/
- https://realpython.com/introduction-to-python-generators/
- http://www.dabeaz.com/coroutines/

Iterator protocol: __iter()__ __next()__ raise StopIteration  
Generators also have .send() .throw() .close()  
i = (yield num) - example of send  
coroutine - generator function into which you can pass data  

- [x] **Dict internal ordering, changing a mutable object while iterating it**
- https://mail.python.org/pipermail/python-dev/2012-December/123028.html
- https://riptutorial.com/python/example/949/changing-the-sequence-you-are-iterating-over
- https://docs.python-guide.org/writing/gotchas/#mutable-default-arguments

As of Python 3.6, for the CPython implementation of Python, dictionaries remember the order of items inserted. This is considered an implementation detail in Python 3.6;  
As of Python 3.7, this is a guaranteed language feature, not merely an implementation detail.  


## Other

- [x] **Functools** https://docs.python.org/3/library/functools.html
	
- [x] **Imports absolute vs relative** https://realpython.com/absolute-vs-relative-python-imports/

- [x] **Data Structures** https://realpython.com/python-data-structures

- [x] **Compilation and linking in Python** http://net-informations.com/python/iq/linking.htm

- [x] **Decorators, Class decorators** https://realpython.com/primer-on-python-decorators/  
@functools.wraps decorator will preserve information about the original function  
Example of non-trivial class decorator (register class as virtual class):
1. define class Double(metaclass=abc.ABCMeta):  
2. @Double.register  
    class CustomDouble:  
3. issubclass(CustomDouble, Double) == True

- [x] **Context managers** https://www.geeksforgeeks.org/context-manager-in-python/  
__enter()__ __exit()__

- [x] **List and Dict comprehensions** https://realpython.com/list-comprehension-python/  
Gen comprehensions:  
nums_squared_lc = [num**2 for num in range(5)]  
nums_squared_gc = (num**2 for num in range(5))  
list compr faster but gen compr memory efficient  

- [x] **args, kwargs, unpacking operators** https://realpython.com/python-kwargs-and-args/

- [x] **Copy vs deepcopy** https://realpython.com/copying-python-objects/


## New Python Features

- [x] **New python 3.10 lang features** https://realpython.com/python310-new-features/

friendlier error messages  
structural pattern matching  
type hint improvements (unioin with | list[float | int], TypeAlias, TypeGuards  
zip strict param (matching lists are equal)  
new funcs in statistics module  
modern SSL  


## Tools 

Pympler is a development tool to measure, monitor and analyze the memory behavior of Python objects in a running Python application.  
https://pythonhosted.org/Pympler/  
cProfile outputs all function calls with timing  
import cProfile  
cProfile.run('sum([i * 2 for i in range(10000)])')  

Bandit - linter for security holes  
https://github.com/PyCQA/bandit
