# 9 Rules of Thumb of Dubugging

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [9 Rules of Thumb of Dubugging](#9-rules-of-thumb-of-dubugging)
	- [List of Rules](#list-of-rules)
	- [Understand The system](#understand-the-system)
	- [Make it fail](#make-it-fail)
	- [Quit thinking and look](#quit-thinking-and-look)
	- [Divide and conquer](#divide-and-conquer)
	- [Change one thing at a time](#change-one-thing-at-a-time)
	- [Keep an audit trail](#keep-an-audit-trail)
	- [Check the Plug](#check-the-plug)
	- [Get a fresh view](#get-a-fresh-view)
	- [If you didn't fix it, it ain't fixed](#if-you-didnt-fix-it-it-aint-fixed)

<!-- /TOC -->

- Debugging: Figuring out why a design doesnt work as planned
- troubleshooting: Figuring out what's broken when the design is  known to be good
- Once you have bugs, you have to detect them

## List of Rules

- Understand The system
- Make it fail
- Quit thinking and look
- Divide and conquer
- Change one thing at a time
- Keep an audit trail
- Check the Plug
- Get a fresh view
- If you didn't fix it, it ain't fixed

## Understand The system

- when all else fails, read the instructions
- You need a working knowledge of what the system is supposed to do, how it's designed, and, in some cases, why it was designed that way
  - To solve the problem
- if you don't understand it when you design it, you're more likely to mess up
- you have to understand how things are supposed to work if you want to figure out why they don't.
- Don't necessarily trust this information, of the manuals/specs supplied
- you have to know how the system would normally work
  - Knowledge of what's normal helps you notice things that aren't.
- know a little bit about the fundamentals of your technical field
- Initial guesses about where to divide a system in order to isolate the problem depend on your knowing what functions are where
- system that are "black boxes,"' meaning that you don't know what's inside them, knowing how they're supposed to interact with other parts allows you to at least locate the problem as being inside the box or outside the box. If the problem is inside the box, you have to replace the box, but if it's outside, you can fix it
-  Don't waste your debugging time looking at the wrong stuff.


Tools

- you have to be able to choose the right tool, use the tool correctly, and interpret the results you get properly
- Stepping through source code shows logic errors but not timing or multithread problems; profiling tools can expose timing problems but not logic flaws
- Know the language you're writing software in

Summary

• Read the manual. It'll tell you to lubricate the trimmer head on your weed whacker so that the lines don't fuse together.
• Read everything in depth. The section about the interrupt getting to your microcomputer is buried on page 37.
• Know the fundamentals. Chain saws are supposed to be loud.
• Know the road map. Engine speed can be different from tire speed, and the difference is in the transmission.
• Understand your tools. Know which end of the thermometer is which, and how to use the fancy features on your Glitch−O−Matic logic analyzer.
• Look up the details. Even Einstein looked up the details. Kneejerk, on the other hand,trusted his memory.

## Make it fail

Summary

• Do it again. Do it again so you can look at it, so you can focus on the cause, and so you can tell if you fixed it.
• Start at the beginning. The mechanic needs to know that the car went through the car wash before the windows froze.
• Stimulate the failure. Spray a hose on that leaky window.
• But don't simulate the failure. Spray a hose on the leaky window, not on a different, "similar" one.
• Find the uncontrolled condition that makes it intermittent. Vary everything you can—shake it, rattle it, roll it, and twist it until it shouts.
• Record everything and find the signature of intermittent bugs. Our bonding system always and only failed on jumbled calls.
• Don't trust statistics too much. The bonding problem seemed to be related to the time of day, but it was actually the local teenagers tying up the phone lines.
• Know that "that" can happen. Even the ice cream flavor can matter.
• Never throw away a debugging tool. A robot paddle might come in handy someday.

Notes:

-  "What do you do when you find a failure?" he would answer, "Try to make it fail again."
- Why?
  - So you can look at it.
    - In order to see it fail (and we'll discuss this more in the next section), you have to be able to make it fail. You have to make it fail as regularly as possible
  - So you can focus on the cause.
    - Knowing under exactly what conditions it will fail helps you focus on probable causes
    - Can be misleading
  - So you can tell if you've fixed it.
    - Once you think you've fixed the problem, having a surefire way to make it fail gives you a surefire test of whether you fixed it.
- Make it fail consistently
  - Write down each step as you go. Then follow your own written procedure to make sure it really causes the error.
- Setup system correctly
  - Note the system setup when failure occured
- Automate it
  - Write a test
  - For repetitve tasks
- Simulation
  - stimulating the failure (good) and simulating the failure (not good).
  - Simulating the conditions that stimulate the failure is okay. But try to avoid simulating the failure mechanism itself.
  -  if you have an intermittent bug, you might guess that a particular low−level mechanism was causing the failure, build a configuration that exercises that low−level mechanism, and then look for the failure to happen a lot
  - In cases where you guess at the failure mechanism, simulation is often unsuccessful.
  - don't try to create new ones. Use instrumentation to look at what's going wrong but don't change the mechanism; that's what's causing the failure.
  - If a bug can be re−created on more than one system, you can characterize it as a design bug—it's not just the one system that's broken in some way
  - Being able to re−create it on some configurations and not on others helps you narrow down the possible causes.
  -  But if you can't re−create it quickly, don't start modifying your simulation to get it to happen.
  - When you have a system that fails in any kind of regular manner, even intermittently, go after the problem on that system in that configuration.
  - Bug on customer site
    - The red flag to watch out for is substituting a seemingly identical environment and expecting it to fail in the same way. It's not identical.
- Automation can make an intermittent problem happen much more quickly
-  Amplification can make a subtle problem much more obvious,
- intermittent bugs
  - you don't know exactly how you made it fail. You know exactly what you did, but you don't know all of the exact conditions. There were other factors that you didn't notice or couldn't control
  -  If you can get control of all those conditions, you will be able to make it happen all the time.
    - Cannot control all conditions
  - First of all, figure out what they are.
    - In software, look for uninitialized data (tsk, tsk!), random data input, timing variations, multithread synchronization, and outside devices (like the phone network or the six thousand kids clicking on your Web site)
  - Sometimes you'll find that controlling a condition makes the problem go away. You've discovered something—what condition, when random, is causing the failure.
  - you want to try every possible value of that condition until you hit the one that causes the system to fail.
  - Sometimes you'll find that you can't really control a condition, but you can make it more random
    - If the problem is intermittent because the failure is caused by a low−likelihood event, then making the condition more random increases the likelihood of these events.
    - Watch out that the amplified condition isn't just causing a new error
  - You have to be able to look at the failure. If it doesn't happen every time, you have to look at it each time it fails, while ignoring the many times it doesn't fail. The key is to capture information on every run so you can look at it after you know that it's failed. Do this by having the system output as much information as possible while it's running and recording this information in a "debug log" file.
  - you can easily compare a bad run to a good one
  - When failures are random, you probably can't take enough statistical samples
  - it's far better to find a sequence of events that always goes with the failure—even if the sequence itself is intermittent, when it happens, you get 100 percent failure.
-  is to forget about the assumptions and make it fail in the presence of the engineer.
-




## Quit thinking and look

## Divide and conquer

## Change one thing at a time

## Keep an audit trail

## Check the Plug

## Get a fresh view

## If you didn't fix it, it ain't fixed
