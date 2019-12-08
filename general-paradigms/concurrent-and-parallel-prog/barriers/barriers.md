# Barriers

- **To prevent our race condition from occurring, we need a way to synchronize our actions so we execute our respective multiplication and addition operations in the correct order.**
- And we can do that with something called a barrier.
- **A barrier is a stopping point for a group of threads that prevents them from proceeding until all or enough threads have reached the barrier. **
  - I like to think of threads waiting on a barrier like players on a sports team coming together for a huddle. Before they join the huddle, the players might be doing other things, putting on their equipment, or getting a drink of water. As they finish those individual activities, they join their teammates at the huddle. Players in the huddle wait there until all of their fellow teammates arrive, then then all yell break, and then they scatter about to continue playing their game.
  - We can use a similar strategy here to solve our race condition. Huddling together to synchronize when we each execute our operations to add and multiply items on the shopping list.
  - I should complete my operation of adding three bags of chips to the list before we huddle together. Then, afterwards, Barron can double the amount.
  - I'm scheduled to execute first this time, so I'll acquire the pencil. I'll add my three bags of chips to the list. (erasing) And release my lock on the pencil. And then meet you at the huddle. Don't leave me hangin'. - I don't have anything to do before the huddle, so - [Together] Break! - Now we're past the barrier, so I'll double the number of chips. That gives us eight, which is the right amount.
- By using a barrier, the order in which our threads actually get scheduled to execute doesn't matter because the barrier synchronizes us.
- Olivia always adds three bags before the barrier, and I multiply by two after it.
- If we were to run that program again and I happened to get scheduled first, well, I don't have anything to do before the barrier, so I'll wait for Olivia. - When I eventually get scheduled to execute, I'll complete my operations, then join the barrier. - [Together] Break! - Now I'm free to continue doing whatever else I need to do. I'm going to see if we have any salsa. - And I can double the chips on our shopping list.
- Although the order in which our threads got scheduled was different, the end result is the same. We need eight bags of chips for the party.
