# code is assertive

- It manages it's own responsibilities
- Entities should be assertive instead of inquisitive
- Which classes to put it's responsibilities
  - ie Where should control of printing a document go, in a Document or Printing class
    - Who knows more about the document, it is itself, and it should be in control of printing itself
    - It does not mean the Document class needs to know about the details about the printer. It can delegate the task of printing to the Printer class, but the Document class is in charge
- Make objects self reliant, self responsible, and in charge of themselves
- Objects dont let other objects do their work for them
  - unless there's a good reason
- An object should be in charge of managing it's own state
  - If an object has a field or property it should have behaviour to manage that field or property
  - It can delegate to other objects, by passing information about itself to the delegeate
- Allows object to be well defined
- Objects should be authoritative, not inquisitive, they should be in charge of themselves
- Unassertive code is inquisitive
  - it constantly accesses state of other objects, to do their own work
  - breaks encapsulation
  - this is feature envy or inappropriate intimacy (law of demeter)
  - Leads to rules for a process to become spread amongst multiple objects.
    - Thus objects must be in sync in order for the functionality to occur
    - Increasing coupling
- Assertive code shows that often the best place to put behaviour is with data it depends on
- If the results of my tests are in a different object than the one being tested, I probably have assertiveness issues.