# Error Handling Checklist

A program can be regarded a system evolving along time while interacting with the outside world.

It has:
  - input
  - output
  - internal state
  - host environment

An error or an exception is a specific state at which the system is deemed abnormal. We will use the two word interchangeably. Regarding error handling with respect to a certain error, the following questions can be asked:

1. Is it an expected error?

Does the programmer know that such an error might happen while he writes the code?

Yes => expected error
NO => unexpected error.

1.1 It is impossible to eliminate all unexpected errors. Things can go wrong in infinite number of ways.

1.2 There should be an exclusive list of all possible (expected) errors that is explicitly defined by (or implicitly deduced from) functionality specifications. That is, any error not in that list will be simply ignored regardless of possible consequences.

1.3 Software errors can be divided into programming errors (**do-things-wrong type of errors**) and errors of business logic (**do-wrong-things type of errors**).

Lack of do-things-wrong type of errors doesn’t indicate there is no do-wrong-things type of errors. Even if a program has been formal verified and its hosting environment works perfectly, and always has valid user input, it might contain do-wrong-things-type of error.

Do-wrong-things type of errors can only be avoided by a pro doing the job, who has both enough domain specific knowledge of the underlying problem the program tries to solve, and programming skills to understand its implementation details. The one who designs the solution should be also responsible for (or at least in charge of) implementing it.

The error behind the 737 Max accident is of the do-wrong-things type. The software works as intended but works in the wrong way. No programming technique can save a software from its design flaws.

1.4 There are host environment errors, input errors, and software errors.

1.4.1 Host environment raised errors (hardware errors, sensor firmware errors, OS errors, virtual machine errors) usually can’t be handled in the same way as other kinds of errors.

Usually, there is redundancy for hardware errors, sensor cross verification for sensor/firmware errors, interrupts handling for OS errors, and virtual machine specific error handling methods for VM errors.

1.4.2 All inputs must be validated before they can alter the internal state of the program. All possible inputs (inputs that would pass the validation procedure) should cause the exact intended effect on the program state and output.

1.4.3 Programming errors (that is what most people mean by the term software bugs) can be reduced via
  - applying good practices (coding style, language feature selection, modularization, documentation)
  - excessive tests
  - static analyzing (language built-in type checker or plug-in tools)
  - code review
  - formal verification.

2. Is the error recoverable?

If the error is handled properly, the system can recover from that error and back to its normal state, it is said that the error is recoverable. Otherwise, the error is unrecoverable.

2.1 For a recoverable error, is it possible the system be setback to the prior state just before the error happened? (transactional rollback).

Can be done automated or manually (data fix and replaying). Each recovery process depends on the time frames the error needs to be recovered in, or if it can only be done one way.

2.1.1 During the rollback, does the system also emits some output (logging the error, informing the error to other processes, let the host environment know that an error has just occurred.)? If so, is it necessary to inform the host environment that an error has just occurred?

2.1.2 If such a message is sent (by function call, sending a data pack, setting a global environment, or by any IPC facility, etc.), Is it possible that the message is lost or ignored by the receiver (the host system)?

2.1.3 If the message is lost or ignored, is it safe to continue to run the program? If NO, then it must be regarded as an unrecoverable error.

2.2 For an unrecoverable error, is there any clean-up work that needs to be done before the program quitting execution?

2.2.1 Who will be responsible for the clean- up work? The host environment, the program itself, or some other program?

2.2.2 What guarantee does one get if such an error occurs from the clean-up work?

2.2.3 When will a user notice that the program has exited abnormally?

What can he do about it?

2.2.4 Will restarting the program solve the problem? If so, a watchdog program is needed.

3. Speak in terms of modules, assuming that modules interacting via message passing (can be implemented with function calls, shared memory or actual message passing), there are two types of errors, internal error and external error.

An internal error is handled inside the corresponding module, and other modules don’t have to know about its occurrence.

An external error is an error when it occurs, the callee module must let the caller module know what have just happened.

An internal error might as well trigger an external error, that is, after the error is handled in the abiding module, the caller module also must be notified of its occurrence. After being reported, an external error immediately becomes an internal error of the caller module.

3.1 For an external error, how will the error be reported to the caller module? Is it done by return code, throwing an exception, setting a variable, sending a message, etc.?

3.2 Is it OK if the caller forgets checking, postpone checking, or just decides to ignore the error?

3.3 If the error shouldn’t be ignored, is it possible to enforce the caller not to ignore the error and handle it in a timely manner.

3.4 How much information or what information should be contained in the error message for the caller module correctly handle the error?

3.5 How to maintain consensus regarding the meaning of the same error between the caller and the callee, that is, the caller interprets the error message in the same way as the callee does.

3.6 Is an error supposed to be handled by its immediate caller? If so, can it be enforced that the immediate caller always checks all possible errors.
