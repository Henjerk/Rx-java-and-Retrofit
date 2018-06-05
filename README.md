# Rx-java-and-Retrofit
Implementation of Rx java and Retrofit

Retrofit 2 is my go-to library to handle API calls in Android Applications, It allows a simple and cleaner way to define APIs. Below is a step-by-step guide to get Retrofit 2 and RxJava 2 up and running on your android applications.

Add the following dependencies to your gradle file

Retrofit 2

compile 'com.squareup.retrofit2:converter-gson:2.1.0'

Retrofit is compatible with different types of Json parsers(Moshi, Jackson,etc). I like to use Gson which is included as part of the dependency.


RxJava 2

compile 'io.reactivex.rxjava2:rxjava:2.0.2'


RxAndroid adds android specific bindings for RxJava, Specifically AndroidSchedulers.mainThread() which provides a Scheduler that schedules on main thread and can be used to switch between threads in Android.

compile 'io.reactivex.rxjava2:rxandroid:2.0.1'


Retrofit 2 works seamlessly with RxJava 2 using the RxJava 2 adapter for Retrofit 2, add the following dependency to enable the RxJava 2 compatibility

compile 'com.jakewharton.retrofit:retrofit2-rxjava2-adapter:1.0.0'





RxJava 
is all about two key components: Observable and Observer. In addition to these, there are other things like Schedulers, Operators and Subscription.
Observable: Observable is a data stream that do some work and emits data.

Observer: Observer is the counter part of Observable. It receives the data emitted by Observable.

Subscription: The bonding between Observable and Observer is called as Subscription. There can be multiple Observers subscribed to a single Observable.

Operator / Transformation: Operators modifies the data emitted by Observable before an observer receives them.

Schedulers: Schedulers decides the thread on which Observable should emit the data and on which Observer should receives the data i.e background thread, main thread etc.,


RxAndroid 
is specific to Android Platform with few added classes on top of RxJava. More specifically, Schedulers are introduced in RxAndroid (AndroidSchedulers.mainThread()) which plays major role in supporting multithreading concept in android applications. Schedulers basically decides the thread on which a particular code runs whether on background thread or main thread. Apart from it everything we use is from RxJava library only.

Even through there are lot of Schedulers available, Schedulers.io() and AndroidSchedulers.mainThread() are extensively used in android programming. Below are the list of schedulers available and their brief introduction.

* Schedulers.io() – This is used to perform non CPU-intensive operations like making network calls, reading disc / files, database operations etc., This maintains pool of threads.

* AndroidSchedulers.mainThread() – This provides access to android Main Thread / UI Thread. Usually operations like updating UI, user interactions happens on this thread. We shouldn’t perform any intensive operations on this thread as it makes the app glitchy or ANR dialog can be thrown.

* Schedulers.newThread() – Using this, a new thread will be created each time a task is scheduled. It’s usually suggested not to use schedular unless there is a very long running operation. The threads created via newThread() won’t be reused.

* Schedulers.computation() – This schedular can be used to perform CPU-intensive operations like processing huge data, bitmap processing etc., The number of threads created using this scheduler completely depends on number CPU cores available.

* Schedulers.single() – This scheduler will execute all the tasks in sequential order they are added. This can be used when there is necessity of sequential execution is required.

* Schedulers.immediate() – This scheduler executes the the task immediately in synchronous way by blocking the main thread.

* Schedulers.trampoline() – It executes the tasks in First In – First Out manner. All the scheduled tasks will be executed one by one by limiting the number of background threads to one.

* Schedulers.from() – This allows us to create a scheduler from an executor by limiting number of threads to be created. When thread pool is occupied, tasks will be queued.
