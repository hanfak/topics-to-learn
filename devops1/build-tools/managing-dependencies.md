# Managing dependecies

- Build tools allows project manage and import dependencies.
  - Helps with stopping conflicts with different versions and transient dependencies
- Always validate them
  - Understand the other dependencies that one dependency defined in config that will be brought in to the class path
  - check that these dependecies can be trusted
    - Do they meet requirements for app, deployment, environments, security, legal etc
  - Do not just trust them
    - They are still code
    - Most will come from open source
    - Are they being maintained?
      - ow you will need to do this?
    - How many contributors?
    - Documentation?
    - Are tests passing? Code coverage?
    - Maturity?
    - Check Issues? Are they resolved?
- Vulnerable Dependencies
  - From a security point of view, you should scan your dependencies for known vulnerabilities.
  - Always update version which fixes these issues
    - There should be a plugin
    - Check issues on github
  - If cannot, make sure application can replace library easily
  - This applies to code in production
- Always fix dependencies
  - And have schedule to update
  - Have a way of monitoring when an update is needed due to a vulnerabilities
## Bill of materials (BOM)

- http://java.jonathangiles.net/JBP-1

## Minimise Dependencies

- http://java.jonathangiles.net/JBP-2

## Versioning

- Have fixed versions
- http://java.jonathangiles.net/JBP-3

## Maintance

- Always keep depencies up to date
- http://java.jonathangiles.net/JBP-4

## Better to copy

- depending on the license, it might be better to copy the functionality then import the whole library which contains lots of unneeded code and transitive dependencies
- http://java.jonathangiles.net/JBP-8

## Links

- https://pointersgonewild.com/2022/02/11/code-that-doesnt-rot/
