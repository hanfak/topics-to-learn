# Codifying architecture

- What ever rules or pattern you use for building your app to some sort of architecture. It is good to codify them, and use them as way to maintain and warn us that they have been broken
- Best way to do this is through tests
  - can create static analysis tests, which check the package structure
  - use Archunit (https://github.com/TNG/ArchUnit) for example (https://github.com/TNG/ArchUnit-Examples)
- Can run these tests in build, to get fast feedback
- Other architecture properties agreed for this application outside of package structure can also be coded as tests
  - called fitness functions which test the non functional requirements of an application
  - Can have a set of metrics, which can be displayed
  - Useful when building agile projects
  - See https://www.amazon.co.uk/Building-Evolutionary-Architectures-Neal-Ford/dp/1491986360/ref=sr_1_1?crid=30YQY2NSZI30&dchild=1&keywords=evolutionary+architecture&qid=1606635691&sprefix=evolutionary+arch%2Caps%2C193&sr=8-1
  -
