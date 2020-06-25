# Data Races

- One of the main challenges of writing concurrent programs is identifying the possible dependencies between threads to make sure they don't interfere with each other and cause problems.
- Data races are a common problem that can occur when two or more threads are concurrently accessing the same location in memory and at least one of those threads is writing to that location to modify it's value.
- Fortunately, you can protect your program against data races by using synchronization techn|
- iques.
- But, to eventually use those techniques, you'll first need to know how to recognize the data race.
  - Olivia and I are two concurrent threads working together to figure out what we need to buy from the grocery store. I'll take inventory of the pantry and when I see that we're running low on something, I'll add more of that item to our shared shopping list.
  - While Barren does that, I'll look through my recipe book and I'll add ingredients to our shopping list for the meals that I wanted us to cook this week.
  - Even though we're two separate threads doing different tasks, we run the risk of a data race because we're both accessing and modifying the same shared resource. Our shopping list.
  - Now, to the panty! - Oh! This garlic mashed potato recipe looks delicious, I'll need five potatoes for it. I see that our shopping list already has three potatoes on it. Three plus five is eight. So, I'll erase three (pencil scribbles) and write down eight.
  - First, I had to read the existing value of the item from the shopping list. Then, I modified the value by adding what I needed to it. Finally, I wrote the result back to the shopping list.
  - It looks like we're running low on garlic in the pantry. I think we should restock it with two more cloves. I see that there is currently one clove of garlic on the list. One plus two is uh... - My garlic mashed potato recipe calls for five cloves of garlic. I see there's currently one clove of garlic on the list, one plus five is six. So, I'll update the list to have six cloves on it. (pencil scribbles) - Three! One plus two is three. We need three cloves of garlic. (pencil scribbles) - Now, we have a problem.
  - The shopping list started with one clove of garlic. Barren wanted to add two more and I needed to add five more. One plus two plus five means we should've ended up with eight cloves of garlic on this list. But somehow, we only have three. I need more garlic for my mashed potatoes. - We just had a data race.
- As concurrent threads, it's up to the operating system to schedule when we each get to execute.
  - Right after I read the value of one from that shared shopping list, my thread got paused. - Then my thread became active and changed the number of garlic from one to six. - And finally, my thread became active again and at that point, I was operating with old data in my local memory because I thought the existing value of garlic on the shopping list was still one.
  - So, I finished my operation by changing it to three.
  - In this example, it was the unfortunate timing of when our threads were scheduled that caused the problem.
- **But, the unpredictability of when threads get scheduled means sometimes the data race will occur and cause problems but other times, everything might work just fine. That inconsistency makes data races a real challenge to recognize and debug.**

-  A data race occurs when 2 instructions from different threads access the same memory location, at least one of these accesses is a write and there is no synchronization that is mandating any particular order among these accesses.
- You risk a data race whenever a thread writes a variable that might next be read by another thread or reads a variable that might have last been written by another thread if both threads do not use synchronization;

## Dealing with Data Races

- Compiler tools, part of IDE
- But in general, very hard to find
- Focus on prevention
  - Since a data race only occurs when at least one of the concurrent threads is modifying the value of a memory location, pay close attention to anywhere you use an assignment operation or an operator like the ++ which increments and changes the variable's value.
  - If there is a potential that two or more threads could access that variable, then you will almost certainly need to use some form of synchronization.
  - Avoid using mutable data,
  - dont use ++,
  - avoid chaning class fields
