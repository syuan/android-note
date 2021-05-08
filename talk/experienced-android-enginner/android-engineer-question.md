

## How in-depth can you answer these as an experienced Android engineer?

> https://saumyesrivastava.medium.com/how-in-depth-can-you-answer-these-as-an-android-engineer-f61a7c2d736c

// 찾아보지 않고 일단 생각나는대로 적어보기

### **Questions**

1.  How does layout inflation work from xml tags to view reference in memory? How are attributes read and drawn and how many passes does a view before it’s completely shown on screen?
: layout resource id 로 xml layout file 를 가져와서 파싱 작업 수행
xml 파싱 작업은 속도의 이유로 jni (c++) 로 파싱 하여 뷰를 생성 
Activity 의 content view 가 inflate 된 경우, Activity Window deco 뷰에 attach
onCreate() 에서 생성된 뷰는 onResume 시점에 사용자에게 보여짐 
// TODO 이 사이에 과정은 무엇을 더 설명하면 좋을까? rendering 과정? frame buffer?

2.  How would you go about implementing findViewById? Given 2 view references, how would you go about finding their ancestor view?
: findViewById 는 구현은 해당 ViewGroup 에서 자식을 순회하면서 탐색하면서 해당하는 id 를 탐색, 부모뷰를 찾는 방식은 parent 를 위로 따라 올라가면서 찾기 같은 부모 뷰를 발견하면 되는거 아닌가?

3.  Explain in complete detail on when you tap on a position/coordinate on phone say (140, 250), to the types of listeners fired, their priority on execution and event handling mechanism between child and parent layouts.
: layout 은 view 와 view group 으로 구성되며, touch event 전달은 최상위 부모 뷰에서 자식 뷰/뷰 그룹으로 전달된다. event 은 dispatch touch event 로 전달되며, view group 이 intercept touch event 함수를 통해서 intercept 할 할 기회를 먼저 가진다. view group 이 intercept 하지 않은 경우에 최 하단의 뷰의 touch event 부터 순차로 불리게 된다. touch event 를 해당 뷰가 핸딜하고 true 로 값을 반환하는 경우 event 는 더 이상 위로 전달되지 않고 event 전달이 마감된다.

4.  What is a thread, handler, looper and message queue?
: android 에서 thread 간의 동기화 문제를 해결하기 위해서 전통적인 방식인 producer- consumer 방식인 message handling 방식을 사용하고 있음
thread 는 하나의 looper 를 가질 수 있으며, thread local 에 하나의 looper 를 저장해 두고 사용
looper 는 message queue 를 가지고 있으며, 해당 thread 에서 처리하기 위한 message 를 queue 에 담아 두었다가 하나씩 순차적으로 처리함
handler 는 2가지의 역할이 있음, 해당 thread 로 message 를 보내는 역할과 message 를 처리하는 역할 
(message 처리 동작은 runnable (callback) 을 넣는 경우는 runnable 을 사용하고 넣지 않는 경우 handler 의 handle 함수가 호출됨)


5.  What are the different methods of concurrency on Android? Can you explain the difference between ExecutorService vs CachedThreadPool vs FixedThreadPool vs AsyncTasks vs HandlerThreads?
: 
- ExecutorService 는 thread pool 과 queue 로 구성된 로 전통적인 thread 동기화 모델인 producer-consumer 방식인 interface 
- CachedThreadPool 은 최대 thread 개수를 가지고 있으며, 요청이 많은 경우 최대까지 thread 를 증가 시키고 alive time 까지 thread 를 유지/종료함?
요청이 적은 경우 최소의 thread 를 유지하고, 요청이 많은 경우 최대 thread 만큼을 유지하는 유동적으로 thread 수를 조절하는 기능
- FixedThreadPool 은 고정된 thread 수만큼의 pool 에 유지하는 방식
- AsyncTask 는 안드로이드에서 thread 사용을 용이하게 하기 위해 제공하는 유틸 클래스
내부적으로는 위의 ExecutorService 사용함, 초기에는 매우큰 thread pool 을 사용하는 executor 의 동작만 제공하였으나, 버전이 올라가면서 pool 크기를 줄이고 single executor 를 사용할 수 있도록, 2가지 executor 를 제공, 현재는 rxjava, coroutine 같은 더 모던한 방식들이 제공되면서 deprecate 되었음
- 

6.  How does Garbage Collection work on Android? Explain the terms reference counting, mark and sweep?
:

7.  Think and list down all the different ways to communicate between an application component and a service?
:

8.  When should you bind to a service, what is a ServiceConnection & how does binding work internally?
:

9.  What is the difference between using Messenger and AIDL? What are the advantages of using AIDL for interprocess communication?
: 
 
10.  In-memory vs Bundle vs SharedPrefs vs Database? What state do you persist in where?
:

11.  List down all the ways that you can think of to reduce the apk size.
:

12.  How is ANR, frame drop and frozen frames caused, how are they all different?
:

13.  What are the 3 steps of Proguard/R8, how to enable and disable them?
:

14.  What is consumer proguard, how is it different from Proguard?
:

15.  How do we unobfuscate a stack trace of a Proguard/R8 obfuscated apk?
:

16.  What is the difference between commit and apply in SharedPrefs? Which is more performant SharedPrefs vs Databases?
:

17.  Describe how you could implement observable SharedPrefs or observable Databases i.e. Observe a certain key/table/query?
:

18.  How is sharing data and sharing control between process on Android different? How would you do both?
:

19.  What is the difference between Serializable and Parcelable? What are the disadvantages of Serializable?
:

20.  What are the different ways to protect api key inside a shipped apk?
:

21.  What is a man in the middle attack, how do you secure your apis from it and other attacks?
:

22.  What are the steps in Android build process from java/kt files to packaging? Explain in detail what is R.java, resources.arsc, manifest merging & signing etc.
:

23.  How is app bundle different from apk? What are build flavours and how are they different from product flavours and splits?
:

24.  How would you communicate between an Activity & Activity, Fragment & Fragment and Activity & Fragment?
:

25.  What are the different activity launch modes?
:

26.  What is the viewholder pattern, how will you implement it on a ListView? Explain the best practice to specify the listeners on the items inside the RecyclerView?
:

27.  What are the steps you can think of optimising RecyclerView performance?
:

28.  How would you implement a Sticky header in a RecyclerView from scratch.
:

29.  How is change in the dataset reflected in the RecyclerView? What is DiffUtil?
:

30.  What is Reflection in Java and why is it advised to use minimally?
:

31.  What are Generics in Java? In what cases are they useful and how do you restrict them?
:

32.  What is a Content Provider in Android and how do you access the content it provides?
:

33.  Implement an Android Content Provider on top of a dataset of comma separated files. Is it possible?
:

34.  How is data stored on databases on Android? What is an ORM & a Data Access Object? What are some ways to optimise Database read, write and update?
:

35.  How thread safe is SQLite? Table-level lock or DB-level lock?
:

36.  What is Dependency Injection Pattern? How does it compare to Service Registry Pattern?
:

37.  What are Dagger and Koin and how do they internally work?
:

38.  What are the problems around security when dealing with webviews.
:

39.  What is the different between unit and instrumentation tests? Mockito vs RoboElectric?
:

40.  What is CI/CD in context of Android? What are the pipelines and their guard-rails you have encountered in your experience before code merge, testing, release & rollout?
:

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk5OTYwMDc0MCwxNTI5OTYwNzAzLDE1MT
QyNzcwMTksMjA4NzA4MTE2NCwtMjExNDU2MjY0Ml19
-->