# techniques

## Updating dependencies

## Exploratory Refactoring

## Documentation

## Testing

(move to new file)

### Extract side effect code to protected then sub class and override in test


- Useful for
  - non injected dependencies, ie calls to static methods
  - static method calls to databases or http calls etc, which cannot be stubbed out (ie controlled)
- https://understandlegacycode.com/blog/quick-way-to-add-tests-when-code-does-side-effects/
