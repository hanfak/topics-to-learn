# Test Types

- White and black box
- One thought
  - unit (class based), integration, E2E, Manual
- One thought
  - Unit (covers multiple layers but no external/db calls)
    - good for refactoring
    - seen in clean/hexagonal arch, for testing the inner/usecases
  - Integration
  - E2E
  - manual
- One Thought - google
  - https://testing.googleblog.com/2010/12/test-sizes.html
||Feature||	Small||	Medium || Large ||
|Network access	|No|	localhost only|	Yes|
|Database	|No|	Yes|	Yes|
|File system access|	No|	Yes|	Yes|
|Use external systems	|No	|Discouraged	|Yes|
|Multiple threads	|No|	Yes|	Yes|
|Sleep statements	|No	|Yes	|Yes|
|System properties	|No|	Yes|	Yes|
|Time limit (seconds)|	60|	300	|900+|
