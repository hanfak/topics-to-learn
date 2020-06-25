# Future

- Launching asynchronous tasks is a great way to accomplish multiple things at once.
- Example
   - Olivia, can you go check how many vegetables are in the pantry. While Olivia is busy asynchronously counting veggies, my thread is free to continue doing other work. But now she's gone and I need a way to get that result back from her when she's done.
   - This is where a mechanism called a future can be used.
 -** A future acts as a placeholder for a result for a result that's initially unknown, but will be available at some point in the future**.
 - It provides a mechanism to access the result of an asynchronous operation.
   - I like to think of a future like an IOU note for the result. Hey Oliva! - Hey-o. - Hey, I need you to check how many vegetables are in the pantry and give me back an answer. - Sure, I promise to do that and here's an IOU note that I'll get you that answer. - Thank you. Now I've got a handle to see that future result and I'll hold onto it as I continue doing other work in the kitchen. Eventually, I may reach a point in my work that I need the result from Olivia, perhaps to make a decision or complete some type of computation.
 - The future is read-only and I see that the result isn't ready yet, so all I can do is wait until Olivia finishes. When she finally does, she'll write the result value to that future, which is called resolving or fulfilling it. She's fulfilling her promise to get me an answer
