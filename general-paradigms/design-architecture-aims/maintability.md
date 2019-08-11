Over time, many different people will work on the system (engineering and oper‐ ations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively.

Types of ongoing maintance:

- fixing bugs
- keeping its systems operational
- investigating failures
- adapting it to new platforms
- modifying it for new use cases
- repaying technical debt
- adding new features

Minimise pain of doing maintaince

Make software have the following to avoid being "legacy" and dreaded to work on:

- **Operability: Making life easy for operations**

Make it easy for operations teams to keep the system running smoothly.

Operation teams (ie tech ops/dbas/devops/release) responisbility (some of these might be the purview of the engineers):

• Monitoring the health of the system and quickly restoring service if it goes into a bad state
• Tracking down the cause of problems, such as system failures or degraded performance
• Keeping software and platforms up to date, including security patches
• Keeping tabs on how different systems affect each other, so that a problematic change can be avoided before it causes damage
• Anticipating future problems and solving them before they occur (e.g., capacity planning)
• Establishing good practices and tools for deployment, configuration management, and more
• Performing complex maintenance tasks, such as moving an application from one platform to another
• Maintaining the security of the system as configuration changes are made
• Defining processes that make operations predictable and help keep the production environment stable
• Preserving the organization’s knowledge about the system, even as individual people come and go

Engineers help with these by providing the following:

• Providing visibility into the runtime behavior and internals of the system, with good monitoring
• Providing good support for automation and integration with standard tools
• Avoiding dependency on individual machines (allowing machines to be taken down for maintenance while the system as a whole continues running uninter‐ rupted)
• Providing good documentation and an easy-to-understand operational model (“If I do X, Y will happen”)
• Providing good default behavior, but also giving administrators the freedom to override defaults when needed
• Self-healing where appropriate, but also giving administrators manual control over the system state when needed
• Exhibiting predictable behavior, minimizing surprises

- **Simplicity: Managing complexity**

Make it easy for new engineers to understand the system, by removing as much complexity as possible from the system.

Code can become complex as it grows. Which will slow down development and thus increasing time & cost of maintance. I.E. Big ball of Mud. This leads to budgets and plans to overrun

When making changes to complext systems, can lead to bugs. As the system is harder for developers to understand and reason about, hidden assumptions, unintended consequences, and unexpected interactions are more easily overlooked.

Symptons of complexity:

- explosion of the state space
- tight coupling of modules
- tangled dependencies
- inconsistent naming and terminology
- hacks aimed at solving performance problems
- special-casing to work around issues elsewhere

Simplicity does not mean reducing functionality.

Simpilicity should remove *accidental complexity*, complexity as accidental if it is not inherent in the problem that the software solves (as seen by the users) but arises only from the implementation.

Use of *abstraction* to hide details behind a *facade*, it can be reused. DRY.

Conflict between abstracting/drying out and readability.

- **Evolvability: Making change easy**

Make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change. Also known as extensibility, modifiability, or plasticity.

System never remains constant, always in flux due to:

- you learn new facts
- previously unanticipated use cases emerge
- business priorities change
- users request new features
- new platforms replace old platforms
- legal or regulatory requirements change
- growth of the system forces architectural changes
- Out of date secruity protocols (ie certificates/passwords)

Use of Agile/XP, to help with constant change and gettting it out there. Easy to use in single project, but more difficult with whole systems of lots of applications
