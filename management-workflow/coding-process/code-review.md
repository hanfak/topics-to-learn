# Code Review

- https://www.youtube.com/watch?v=a9_0UUUNt-Y
- https://google.github.io/eng-practices/review/reviewer/looking-for.html
- https://matt-rickard.com/code-review-checklist/
- pyramid of code review
  - https://www.reddit.com/r/programming/comments/2wau2x/maslows_pyramid_of_code_review/
  - Code should be: (importance going down)
    - Correct: does the code do what it's supposed to? Does it handle edge cases? Is it adequately tested to make sure that it stays correct even when other engineers modify it? Is it performant enough for this use case?
    - Secure: does the code have vulnerabilities? Is the data stored safely? Is personal identification information (PII) handled correctly? Could the code be used to induce a DOS? Is input validation comprehensive enough?
    - Readable: is the code easy to read and comprehend? Does it make clear what the business requirements are (code is written to be read by a human, not by a computer)? Are tests concise enough? Are variables, functions and classes named appropriately? Do the domain models cleanly map the real world to reduce cognitive load? Does it use consistent coding convention?
    - Elegant: does the code leverage well-known patterns? Does it achieve what it needs to do without sacrificing simplicity and conciseness? Would you be excited to work in this code? Would you be proud of this code?
    - Altruist: does the code leave the codebase better than what it was? Does it inspire other engineers to improve their code as well? Is it cleaning up unused code, improving documentation, introducing better patterns through small-scale refactoring?
  - Issues
    - Order
## code review pyramid

- https://www.morling.dev/blog/the-code-review-pyramid/?utm_content=201340967&utm_medium=social&utm_source=twitter&hss_channel=tw-4083531

## Links

- https://simpleprogrammer.com/code-review-trunk-based-development/
- https://simpleprogrammer.com/release-trunk-based-development/
- https://www.michaelagreiler.com/code-review-best-practices/
- https://sizovs.net/2020/07/19/the-code-review/
