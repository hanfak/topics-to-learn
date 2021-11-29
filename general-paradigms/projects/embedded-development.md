# Embedded Software development

To deal with:
- Limited hardware. CPU power can be low, memory sizes can be small - down to kilobytes or bytes
- Device drivers. You’ll be writing, testing and debugging code that directly interacts with electronics. You’ll need an appreciation of how that stuff works, electrical safety, test equipment like oscilloscopes.
- Concurrency. Your code is responding to events. Many from external hardware, some from the passage of time
- Limited languages. At the low end of 8 bit chips, the C language is your only available choice. This relaxes with 32 bit chips somewhat
- Error handling. Often, there’s nothing you can do in response to an error. You try to make things fail safe, but the whole approach to error handling is different
