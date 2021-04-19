

## How in-depth can you answer these as an experienced Android engineer?

> https://saumyesrivastava.medium.com/how-in-depth-can-you-answer-these-as-an-android-engineer-f61a7c2d736c

### **Questions**

1.  How does layout inflation work from xml tags to view reference in memory? How are attributes read and drawn and how many passes does a view before it’s completely shown on screen?
: 

2.  How would you go about implementing findViewById? Given 2 view references, how would you go about finding their ancestor view?
:

3.  Explain in complete detail on when you tap on a position/coordinate on phone say (140, 250), to the types of listeners fired, their priority on execution and event handling mechanism between child and parent layouts.
:

4.  What is a thread, handler, looper and message queue?
:

5.  What are the different methods of concurrency on Android? Can you explain the difference between ExecutorService vs CachedThreadPool vs FixedThreadPool vs AsyncTasks vs HandlerThreads?
:

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
17.  Describe how you could implement observable SharedPrefs or observable Databases i.e. Observe a certain key/table/query?
18.  How is sharing data and sharing control between process on Android different? How would you do both?
19.  What is the difference between Serializable and Parcelable? What are the disadvantages of Serializable?
20.  What are the different ways to protect api key inside a shipped apk?
21.  What is a man in the middle attack, how do you secure your apis from it and other attacks?
22.  What are the steps in Android build process from java/kt files to packaging? Explain in detail what is R.java, resources.arsc, manifest merging & signing etc.
23.  How is app bundle different from apk? What are build flavours and how are they different from product flavours and splits?
24.  How would you communicate between an Activity & Activity, Fragment & Fragment and Activity & Fragment?
25.  What are the different activity launch modes?
26.  What is the viewholder pattern, how will you implement it on a ListView? Explain the best practice to specify the listeners on the items inside the RecyclerView?
27.  What are the steps you can think of optimising RecyclerView performance?
28.  How would you implement a Sticky header in a RecyclerView from scratch.
29.  How is change in the dataset reflected in the RecyclerView? What is DiffUtil?
30.  What is Reflection in Java and why is it advised to use minimally?
31.  What are Generics in Java? In what cases are they useful and how do you restrict them?
32.  What is a Content Provider in Android and how do you access the content it provides?
33.  Implement an Android Content Provider on top of a dataset of comma separated files. Is it possible?
34.  How is data stored on databases on Android? What is an ORM & a Data Access Object? What are some ways to optimise Database read, write and update?
35.  How thread safe is SQLite? Table-level lock or DB-level lock?
36.  What is Dependency Injection Pattern? How does it compare to Service Registry Pattern?
37.  What are Dagger and Koin and how do they internally work?
38.  What are the problems around security when dealing with webviews.
39.  What is the different between unit and instrumentation tests? Mockito vs RoboElectric?
40.  What is CI/CD in context of Android? What are the pipelines and their guard-rails you have encountered in your experience before code merge, testing, release & rollout?
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxMTY5NjQwNF19
-->