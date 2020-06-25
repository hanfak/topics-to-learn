# Try Lock

- When multiple threads each have multiple tasks to perform, making those threads block and wait every time they attempt to acquire a lock that's already taken may not be necessary or efficient.
  - if two threads doing several different tasks. My thread will be taking an inventory of the fridge to see what things we're running low on and then add those to the shopping list on our shared notepad. I'll go back and forth between those two tasks.
  - On the other thread is searching through the newspaper for grocery coupons and then adding those items to the shared shopping list. When It finds some deals, it take the pencil, which is our mutex, to lock access to the shared notepad so it can add them.
  - The first thread saw we're low on milk. So now It'll go to acquire the pencil. And I see the other thread has it. If it attempt to lock a mutex in a regular blocking fashion, my thread would enter a waiting state at this point, doing nothing until the other thread unlocks it.
  - If I don't have anything else to do, so I can't continue with other things until after I've accessed the shared notepad, that's okay. It's what has to happen, but in this scenario, I do have other useful things to do that don't require the notepad. I can keep searching the fridge for other things we need.
  - So, rather than using the standard locking method to acquire the mutex, I'll use what's called **try lock, or try enter, which is a non-blocking version of the lock or acquire method.**
    - It returns immediately and one of two things will happen.
      -  If the mutex you're trying to lock is available, it will get locked, and the method with return TRUE.
      - Otherwise, if the mutex is already possessed by another thread, the try lock method will immediately return FALSE.
    - That return value of true or false lets the thread know whether or not it was successful in acquiring the lock.
    - So, if I try to lock the pencil that other thread currently has, I know immediately that my attempt has failed. So I can go back to searching the fridge.
    - When the other thread is done writing for now. So It'll unlock the pencil and go back to searching for coupons. Since the first thread wasn't blocked waiting for this mutex, it's just sitting unlocked available for anyone to take.
  - I think of it more like being at a house party with a bunch of your friends, your fellow threads. There's one restroom at the house that everyone at the party will need to use at some point. But only person can use it at a time. When you try to use it, and try opening the door, you realize it's locked because someone's already inside. You could stand there and wait until they come out or you could go back to the party, keep having fun, and try again later.
