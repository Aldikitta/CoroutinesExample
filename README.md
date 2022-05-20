# CoroutinesExample 

# How Suspendinf functions works
Let's say we have a function named myFunction.



fun myFunction(){

Code block 1

Code block 2 //this one has a long running operation

Code block 3

Code block 4

}



Usually these code blocks execute like block1, block2, block3, block4 . So code block 3 and 4 might execute while code block 2 is still running. (synchronously) Because of that reason there can be problems. (screen might freeze, app might crash)

(assume code block 3 is a click event code of a button,..)

But if we make this function suspend.



suspend fun MyFunction(){

Code block 1

Code block 2 //this one has a long running operation

Code block 3

Code block 4

}



Now, this function can get paused when code block 2(long running operation) starts executing and get resumed when it is done. Code block 3 and 4 will execute after that. So there will be no unexpected thread sharing issues.





Functions marked with the suspend keyword are transformed at compile time to be made asynchronous under the hood, even though they appear synchronous in the source code.



A suspending function doesn't block a thread,

but only suspends the coroutine itself. (one thread can have more coroutines)

The thread is returned to the pool while the coroutine is waiting,

and when the waiting is done, the coroutine resumes on a free thread in the pool.
