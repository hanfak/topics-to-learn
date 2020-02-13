# Other principles

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Other principles](#other-principles)
	- [KISS - Keep it simple stupid](#kiss-keep-it-simple-stupid)
	- [Don’t Repeat Yourself (DRY)](#dont-repeat-yourself-dry)
	- [You Aren’t Gonna Need It (YAGNI)](#you-arent-gonna-need-it-yagni)

<!-- /TOC -->

## KISS - Keep it simple stupid

- that code that is as simple as possible is better than code that is more complex.
- code that is less “elegant”, but more easily maintainable code, is better
- Is this code likely to be easily repairable by an average programmer working under pressure during a production defect/outage?

## Don’t Repeat Yourself (DRY)

- referred to as the “Single Source of Truth” or “Once and Only Once”
- as not doing copy-and-paste coding
- every piece of knowledge must have a single, unambiguous, authoritative representation within a system
  - any given concept or abstraction that the code embodies should be defined only once in one place and should be clear to the reader/maintainer.
- Can apply to hand written code or configuration
- If repeated three times, extract out
  - if the duplicated code represents an important concept/abstraction in the system then any duplication may be unacceptable
- Removing duplication, means you can give it a descriptive name


## You Aren’t Gonna Need It (YAGNI)

- for the resistance of the temptation to second-guess what code might be needed at some future point and adding it now, rather than adding it only when it is actually needed.
- Can result in
  - Bloated code: unused/unrequired code exists now, and may never be removed/refactored
  - Increased Cost: the unrequired code may still need testing and maintaining
  - Slipped dates: the unrequired code takes time away from other features that may impact overall delivery dates
  - Waste: by the time the unrequired code is actually required, it may no longer be valid if business requirements have changed in the meantime
