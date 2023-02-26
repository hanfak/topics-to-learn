# Testing Good Practice 

This is a set of pamphlets from google "testing on the toilet" see  https://testing.googleblog.com/

- [Testing Good Practice](#testing-good-practice)
    - [What Makes a Good Test?.](#what-makes-a-good-test)
    - [Effective Testing](#effective-testing)
    - [Keep Tests Focused](#keep-tests-focused)
    - [Cleanly Create Test Data](#cleanly-create-test-data)
    - [Separation of Concerns? That's a Wrap!](#separation-of-concerns-thats-a-wrap)
    - [Exercise Service Call Contracts in Tests](#exercise-service-call-contracts-in-tests)
    - [Testing UI Logic? Follow the User!](#testing-ui-logic-follow-the-user)
    - [Only Verify State-Changing Method Calls](#only-verify-state-changing-method-calls)
    - [Tests Too DRY? Make Them DAMP!](#tests-too-dry-make-them-damp)
    - [Don’t Mock Types You Don’t Own](#dont-mock-types-you-dont-own)
    - [Know Your Test Doubles](#know-your-test-doubles)
    - [Risk-Driven Testing](#risk-driven-testing)
    - [Test Behaviors, Not Methods](#test-behaviors-not-methods)
    - [Avoid Hard coding Values for Better Libraries](#avoid-hard-coding-values-for-better-libraries)
    - [Only Verify Relevant Method Arguments](#only-verify-relevant-method-arguments)
    - [Writing Descriptive Test Names](#writing-descriptive-test-names)
    - [Don't Put Logic in Tests](#dont-put-logic-in-tests)
    - [Test Behavior, Not Implementation](#test-behavior-not-implementation)
    - [Change-Detector Tests Considered Harmful](#change-detector-tests-considered-harmful)
    - [Testing State vs. Testing Interactions](#testing-state-vs-testing-interactions)
    - [Don’t Overuse Mocks](#dont-overuse-mocks)
    - [Keep Cause and Effect Clear](#keep-cause-and-effect-clear)
    - [Web Testing Made Easier: Debug IDs](#web-testing-made-easier-debug-ids)
    - [Fake Your Way to Better Tests](#fake-your-way-to-better-tests)
    - [a fluent assertion framework](#a-fluent-assertion-framework)
## What Makes a Good Test?

Unit tests are important tools for **verifying that our code is correct**. But writing good tests is about much more than just verifying correctness — a good unit test should exhibit several other properties in order to be readable and maintainable.

One property of a **good test is clarity**. 
- Clarity means that a test should serve as **readable documentation for humans, describing the code being tested in terms of its public APIs**. 
- Tests **shouldn't refer directly to implementation details.** 
- The **names of a class's tests should say everything the class does, and the tests themselves should serve as examples for how to use the class.**

Two more important properties are **completeness and conciseness**.
- A test is complete when its **body contains all of the information you need to understand it**
- concise when **it doesn't contain any other distracting information**. 

This test fails on both counts:
```java
@Test public void shouldPerformAddition() {
    Calculator calculator = new Calculator(new RoundingStrategy(), "unused", ENABLE_COSIN_FEATURE, 0.01, calculusEngine, false);
    int result = calculator.doComputation(makeTestComputation());
    assertEquals(5, result); // Where did this number come from?
}
```
Lots of distracting information is being passed to the constructor, and **the important parts are hidden off in a helper method**. 

The test can be made more complete by **clarifying the purpose of the helper method**, and more concise by **using another helper to hide the irrelevant details of constructing the calculator**:
```java
@Test public void shouldPerformAddition() {
    Calculator calculator = newCalculator();
    int result = calculator.doComputation(makeAdditionComputation(2, 3));
    assertEquals(5, result);
}
```
One final property of a good test is **resilience**. 
- **Once written, a resilient test doesn't have to change unless the purpose or behavior of the class being tested changes**. 
- **Adding new behavior should only require adding new tests, not changing old ones**. 
- The original test above isn't resilient since you'll have to update it (and probably dozens of other tests!) whenever you add a new irrelevant constructor parameter. Moving these details into the helper method solved this problem.

## Effective Testing

Whether we are writing an individual unit test or designing a product’s entire testing process, it is important to take a step back and **think about how effective are our tests at detecting and reporting bugs in our code.**
To be effective, there are three important qualities that every test should try to maximize:
- Fidelity 
  - When the code under test is broken, the test fails. 
  - A high-fidelity test is one which **is very sensitive to defects in the code under test**, helping to prevent bugs from creeping into the code.
  - Maximize fidelity by ensuring that your tests **cover all the paths through your code and include all relevant assertions on the expected state**.
- Resilience
  - A test shouldn’t fail if the code under test isn’t defective.
  - A resilient test is one that **only fails when a breaking change is made to the code under test**.
  - **Refactorings and other non-breaking changes to the code under test can be made without needing to modify the test**, reducing the cost of maintaining the tests.
  - Maximize resilience by **only testing the exposed API of the code under test**; avoid reaching into internals. 
  - **Favor stubs and fakes over mocks;** 
  - **don't verify interactions with dependencies unless it is that interaction that you are explicitly validating**. 
  - A flaky test obviously has very low resilience.
- Precision
  - When a test fails, a high-precision test **tells you exactly where the defect lies**. 
  - A well-written unit test can **tell you exactly which line of code is at fault**. 
  - Poorly written tests (especially large end-to-end tests) often exhibit very low precision, telling you that something is broken but not where.
  - Maximize precision by **keeping your tests small and tightly focused**. 
  - Choose **descriptive method names** that convey exactly what the test is validating.
  - For system integration tests, **validate state at every boundary.**
  
These three qualities are **often in tension with each other.** It's easy to write a highly resilient test (the empty test, for example), but writing a test that is both highly resilient and high-fidelity is hard. As you design and write tests, use these qualities as a framework to guide your implementation

##  Keep Tests Focused

What scenario does the following code test?
```
    TEST_F(BankAccountTest, WithdrawFromAccount) {
        Transaction transaction = account_.Deposit(Usd(5));
        clock_.AdvanceTime(MIN_TIME_TO_SETTLE);
        account_.Settle(transaction);
        
        
        EXPECT_THAT(account_.Withdraw(Usd(5)), IsOk());
        EXPECT_THAT(account_.Withdraw(Usd(1)), IsRejected());
        account_.SetOverdraftLimit(Usd(1));
        EXPECT_THAT(account_.Withdraw(Usd(1)), IsOk());
    }
```
Translated to English: 
- I had $5 and was able to withdraw $5;
- then got rejected when overdrawing $1; 
- but if I enable overdraft with a $1 limit, I can withdraw $1.” If that sounds a little hard to track, it is: it is testing three scenarios, not one.

A better approach is to exercise each scenario in its own test:
```
    TEST_F(BankAccountTest, CanWithdrawWithinBalance) {
        DepositAndSettle(Usd(5));  // Common setup code is extracted into a helper method.
        EXPECT_THAT(account_.Withdraw(Usd(5)), IsOk());
    }
    TEST_F(BankAccountTest, CannotOverdraw) {
        DepositAndSettle(Usd(5));
        EXPECT_THAT(account_.Withdraw(Usd(6)), IsRejected());
    }
    TEST_F(BankAccountTest, CanOverdrawUpToOverdraftLimit) {
        DepositAndSettle(Usd(5));
        account_.SetOverdraftLimit(Usd(1));
        EXPECT_THAT(account_.Withdraw(Usd(6)), IsOk());
    }
```
Writing tests this way provides many benefits:
- Logic is easier to understand because there is less code to read in each test method.
- Setup code in each test is simpler because it only needs to serve a single scenario.
- Side effects of one scenario will not accidentally invalidate or mask a later scenario’s assumptions.
- If a scenario in one test fails, other scenarios will still run since they are unaffected by the failure.
- Test names clearly describe each scenario, which makes it easier to learn which scenarios exist.
- One sign that you might be testing more than one scenario: 
  - after asserting the output of one call to the system under test, the test makes another call to the system under test.
  
While a scenario for a unit test often consists of a single call to the system under test, its scope can be larger for integration and end-to-end tests. 
- For example, a test that a web UI can send email might open the inbox, click the compose button, write some text, and press the send button.


## Cleanly Create Test Data

Helper methods make it easier to create test data. But they can become difficult to read over time as you need more variations of the test data to satisfy constantly evolving requirements from new tests:

```java
// This helper method starts with just a single parameter:
Company company = newCompany(PUBLIC);

// But soon it acquires more and more parameters.
// Conditionals creep into the newCompany() method body to handle the nulls,
// and the method calls become hard to read due to the long parameter lists:
Company small = newCompany(2, 2, null, PUBLIC);
Company privatelyOwned = newCompany(null, null, null, PRIVATE);
Company bankrupt = newCompany(null, null, PAST_DATE, PUBLIC);

// Or a new method is added each time a test needs a different combination of fields:
Company small = newCompanyWithEmployeesAndBoardMembers(2, 2, PUBLIC);
Company privatelyOwned = newCompanyWithType(PRIVATE);
Company bankrupt = newCompanyWithBankruptcyDate(PAST_DATE, PUBLIC);
```
Instead, use the **test data builder pattern: create a helper method that returns a partially-built object** (e.g., a Builder in languages such as Java, or a mutable object) whose state can be overridden in tests. The helper method initializes logically-required fields to reasonable defaults, so **each test can specify only fields relevant to the case being tested**:

```java
Company small = newCompany().setEmployees(2).setBoardMembers(2).build();
Company privatelyOwned = newCompany().setType(PRIVATE).build();
Company bankrupt = newCompany().setBankruptcyDate(PAST_DATE).build();
Company arbitraryCompany = newCompany().build();

// Zero parameters makes this method reusable for different variations of Company.
// It also doesn’t need conditionals to ignore parameters that aren’t set (e.g. null
// values) since a test can simply not set a field if it doesn’t care about it.
private static Company.Builder newCompany() {
  return Company.newBuilder().setType(PUBLIC).setEmployees(100); // Set required fields
}
```

**tests should never rely on default values that are specified by a helper method** since that forces readers to read the helper method’s implementation details in order to understand the test.

```java
// This test needs a public company, so explicitly set it.
// It also needs a company with no board members, so explicitly clear it.
Company publicNoBoardMembers = newCompany().setType(PUBLIC).clearBoardMembers().build();
```

## Separation of Concerns? That's a Wrap!

The following function decodes a byte array as an image using an API named SpeedyImg. What maintenance problems might arise due to referencing an API owned by a different team?
```java
SpeedyImgImage decodeImage(List<SpeedyImgDecoder> decoders, byte[] data) {
    SpeedyImgOptions options = getDefaultConvertOptions();
    for (SpeedyImgDecoder decoder : decoders) {
        SpeedyImgResult decodeResult = decoder.decode(decoder.formatBytes(data));
        SpeedyImgImage image = decodeResult.getImage(options);
        if (validateGoodImage(image)) { return image; }
    }
    throw new RuntimeException();
}
```
Details about how to call the API are mixed with domain logic, which can make the code harder to understand. 
- For example, the call to decoder.formatBytes() is required by the API, but how the bytes are formatted isn’t relevant to the domain logic.

Additionally, if this API is used in many places across a codebase, then all usages may need to change if the way the API is used changes. 
- For example, if the return type of this function is changed to the more generic SpeedyImgResult type, usages of SpeedyImgImage would need to be updated.

To avoid these maintenance problems, **create wrapper types to hide API details behind an abstraction**:
```java
Image decodeImage(List<ImageDecoder> decoders, byte[] data) {
    for (ImageDecoder decoder : decoders) {
        Image decodedImage = decoder.decode(data);
        if (validateGoodImage(decodedImage)) { return decodedImage; }
    }
    throw new RuntimeException();
}
```
**Wrapping an external API follows the Separation of Concerns principle**, since the logic for how the API is called is separated from the domain logic. 

This has many benefits, including:
- If the way the API is used changes, encapsulating the API in a wrapper insulates how far those changes can propagate across your codebase.
- You can modify the interface or the implementation of types you own, but you can’t for API types.
- It is easier to switch or add another API, since they can still be represented by the introduced types (e.g. ImageDecoder/Image).
- Readability can improve as you don’t need to sift through API code to understand core logic.

Not all external APIs need to be wrapped. 
    - For example, if an API would take a huge effort to separate or is simple enough that it doesn't pollute the codebase, it may be better not to introduce wrapper types (e.g. library types like List in Java or std::vector in C++). 

When in doubt, keep in mind that a wrapper should only be added if it will clearly improve the code (see the YAGNI principle).

## Exercise Service Call Contracts in Tests

The following test mocks out a service call to CloudService.  Does the test provide enough confidence that the service call is likely to work?
```java

@Test public void uploadFileToCloudStorage(){
        when(mockCloudService.write(
        WriteRequest.newBuilder().setUserId(“testuser”).setFileType(“plain/text”)...))
        .thenReturn(WriteResponse.newBuilder().setUploadId(“uploadId”).build());

        CloudUploader cloudUploader=new CloudUploader(mockCloudService);

        Uri uri=cloudUploader.uploadFile(new File(“/path/to/foo.txt”));
        // The uploaded file URI contains the user ID, file type, and upload ID. (Or does it?)
        assertThat(uri).isEqualTo(new Uri(“/testuser/text/uploadId.txt”));
}
```
Lots of things can go wrong, especially when service contracts get complex. 
- For example, plain/text may not be a valid file type, and you can’t verify that the URI of the uploaded file is correct.

**If the code under test relies on the contract of a service, prefer exercising the service call instead of mocking it out.** This gives you more confidence that you are using the service correctly:
```java
@Test public void uploadFileToCloudStorage() {
    CloudUploader cloudUploader = new CloudUploader(cloudService);
    Uri uri = cloudUploader.uploadFile(”/path/to/foo.txt”);
    assertThat(cloudService.retrieveFile(uri)).isEqualTo(readContent(“/path/to/foo.txt));
}
```

How can you exercise the service call?

- **Use a fake.** 
  - A fake is a fast and lightweight implementation of the service that behaves just like the real implementation. 
  - A fake is usually maintained by the service owners; don’t create your own fake unless you can ensure its behavior will stay in sync with the real implementation. 
- **Use a hermetic server.**  
  - This is a real server that is brought up by the test and runs on the same machine that the test is running on. 
  - A downside of using a hermetic server is that starting it up and interacting with it can slow down tests.  
  - ie wiremock


If the service you are using doesn’t have a fake or hermetic server, mocks may be the only tool at your disposal. 
- But if your tests are not exercising the service call contract, you must take extra care to ensure the service call works, such as by having a **comprehensive suite of end-to-end tests or resorting to manual QA (which can be inefficient and hard to scale)**.

## Testing UI Logic? Follow the User!

After years of anticipation, you're finally able to purchase Google's hottest new product, gShoe*. But after clicking the "Buy" button, nothing happened! Inspecting the HTML, you notice the problem:
```html
<button disabled=”true” click=”$handleBuyClick(data)”>Buy</button>
```

Users couldn’t buy their gShoes because the “Buy” button was disabled. The problem was due to the unit test for handleBuyClick, which passed even though the user interface had a bug:
```
it('submits purchase request', () => {
    controller = new PurchasePage();
    // Call the method that handles the "Buy" button click
    controller.handleBuyClick(data);
    expect(service).toHaveBeenCalledWith(expectedData);
});
```
In the above example, the test failed to detect the bug because it bypassed the UI element and instead directly invoked the "Buy" button click handler. 
To be effective, **tests for UI logic should interact with the components on the page as a browser would, which allows testing the behavior that the end user experiences**. 
- Writing tests against UI components rather than calling handlers directly faithfully simulates user interactions (e.g., add items to a shopping cart, click a purchase button, or verify an element is visible on the page), making the tests more comprehensive.

**The test for the “Buy” button should instead exercise the entire UI component by interacting with the HTML element**, which would have caught the disabled button issue:
```
it('submits purchase request', () => {
    // Renders the page with the “Buy” button and its associated code.
    render(PurchasePage);
    // Tries to click the button, fails the test, and catches the bug!
    buttonWithText('Buy').dispatchEvent(new Event(‘click’));
    expect(service).toHaveBeenCalledWith(expectedData);
});
```
Why should tests be written this way? 
- Unlike end-to-end tests, tests for individual UI components don’t require a backend server or the entire app to be rendered. Instead, these  tests run in the same self-contained environment and take a similar amount of time to execute as unit tests that just execute the underlying event handlers directly. Therefore, the UI acts as the public API, leaving the business logic as an implementation detail (also known as the **"Use the Front Door First**" principle), resulting in better coverage of a feature.

## Only Verify State-Changing Method Calls

Which lines can be safely removed from this test?
```java
@Test public void addPermissionToDatabase() {
    new UserAuthorizer(mockUserService, mockPermissionDb).grantPermission(USER, READ_ACCESS);
    
    // The test will fail if any of these methods is not called.
    verify(mockUserService).isUserActive(USER);
    verify(mockPermissionDb).getPermissions(USER);
    verify(mockPermissionDb).isValidPermission(READ_ACCESS);
    verify(mockPermissionDb).addPermission(USER, READ_ACCESS);
}
```

The answer is that **the calls to verify the non-state-changing methods can be removed.**

Method calls on another object fall into one of two categories:
- State-changing:
  - methods that have side effects and change the world outside the code under test,
  - e.g., sendEmail(), saveRecord(), logAccess().
- Non-state-changing: 
  - methods that return information about the world outside the code under test and don't modify anything,
  - e.g., getUser(), findResults(), readFile().
  
You should **usually avoid verifying that non-state-changing methods are called**:
- It is often redundant: 
  - a method call that doesn't change the state of the world is meaningless on its own. 
  - The code under test will use the return value of the method call to do other work that you can assert.
- It makes tests brittle: 
  - tests need to be updated whenever method calls change. 
  - For example, if a test is expecting mockUserService.isUserActive(USER) to be called, it would fail if the code under test is modified to call user.isActive() instead.
- It makes tests less readable: 
  - the additional assertions in the test make it more difficult to determine which method calls actually affect the state of the world.
- It gives a false sense of security: 
  - just because the code under test called a method does not mean the code under test did the right thing with the method’s return value.
  
  Instead of verifying that they are called, **use non-state-changing methods to simulate different conditions in tests**, 
- e.g., when(mockUserService.isUserActive(USER)).thenReturn(false). Then write assertions for the return value of the code under test, or verify state-changing method calls.

Verifying non-state-changing method calls may be useful if there is no other output you can assert.
- For example, if your code should be caching an RPC result, you can verify that the method that makes the RPC is called only once.

With the unnecessary verifications removed, the test looks like this:
```java
@Test public void addPermissionToDatabase() {
    new UserAuthorizer(mockUserService, mockPermissionDb).grantPermission(USER, READ_ACCESS);
    
    // Verify only the state-changing method.
    verify(mockPermissionDb).addPermission(USER, READ_ACCESS);
}
```
That’s much simpler! 

But remember that instead of using a mock to verify that a method was called, it would be **even better to use a real or fake object to actually execute the method and check that it works properly**. 
- For example, the above test could use a fake database to check that the permission exists in the database rather than just verifying that addPermission() was called. 

## Tests Too DRY? Make Them DAMP!

The test below follows the DRY principle (“Don’t Repeat Yourself”), a best practice that encourages code reuse rather than duplication, e.g., by extracting helper methods or by using loops. But is it a well-written test?
```python
def setUp(self):
    self.users = [User('alice'), User('bob')]  # This field can be reused across tests.
    self.forum = Forum()
    
    def testCanRegisterMultipleUsers(self):
    self._RegisterAllUsers()
    for user in self.users:  # Use a for-loop to verify that all users are registered.
        self.assertTrue(self.forum.HasRegisteredUser(user))

def _RegisterAllUsers(self):  # This method can be reused across tests.
    for user in self.users:
        self.forum.Register(user)
```
While the test body above is concise, the **reader needs to do some mental computation to understand it**, e.g., by following the flow of self.users from setUp() through _RegisterAllUsers(). **Since tests don't have tests, it should be easy for humans to manually inspect them for correctness, even at the expense of greater code duplication.** This means that the DRY principle often isn’t a good fit for unit tests, even though it is a best practice for production code.

In tests we can **use the DAMP principle (“Descriptive and Meaningful Phrases”)**, which emphasizes **readability over uniqueness**. Applying this principle can introduce code redundancy (e.g., by repeating similar code), but it makes tests more obviously correct. Let’s add some DAMP-ness to the above test:
```python
def setUp(self):
    self.forum = Forum()
    
    def testCanRegisterMultipleUsers(self):
    # Create the users in the test instead of relying on users created in setUp.
    user1 = User('alice')
    user2 = User('bob')
    
    # Register the users in the test instead of in a helper method, and don't use a for-loop.
    self.forum.Register(user1)
    self.forum.Register(user2)

    # Assert each user individually instead of using a for-loop.
    self.assertTrue(self.forum.HasRegisteredUser(user1))
    self.assertTrue(self.forum.HasRegisteredUser(user2))
```

Note that the DRY principle is still relevant in tests; 
- for example, using a helper function for creating value objects can increase clarity by removing redundant details from the test body. 
Ideally, test code should be both readable and unique, but sometimes there’s a trade-off. When writing unit tests and faced with a choice between the DRY and DAMP principles, lean more heavily toward DAMP.

## Don’t Mock Types You Don’t Own

The code below mocks a third-party library. What problems can arise when doing this?
```java
// Mock a salary payment library
@Mock SalaryProcessor mockSalaryProcessor;
@Mock TransactionStrategy mockTransactionStrategy;
...
when(mockSalaryProcessor.addStrategy()).thenReturn(mockTransactionStrategy);
when(mockSalaryProcessor.paySalary()).thenReturn(TransactionStrategy.SUCCESS);
MyPaymentService myPaymentService = new MyPaymentService(mockSalaryProcessor);
assertThat(myPaymentService.sendPayment()).isEqualTo(PaymentStatus.SUCCESS);
```

Mocking types you don’t own can **make maintenance more difficult**:

- It can make it harder to upgrade the library to a new version: 
  - The expectations of an API hardcoded in a mock can be wrong or get out of date.
  - This may require time-consuming work to manually update your tests when upgrading the library version. 
  - In the above example, an update that changes addStrategy() to return a new type derived from TransactionStrategy (e.g. SalaryStrategy) requires the mock to be updated to return this type, even though the code under test doesn’t need to be changed since it can still reference TransactionStrategy.
- It can make it harder to know whether a library update introduced a bug in your code:
  - The assumptions built into mocks may get out of date as changes are made to the library, resulting in tests that pass even when the code under test has a bug. 
  - In the above example, if a library update changes paySalary() to instead return TransactionStrategy.SCHEDULED, a bug could potentially be introduced due to the code under test not handling this return value properly. However, the maintainer wouldn’t know because the mock would not return this value so the test would continue to pass.
  
Instead of using a mock, **use the real implementation, or if that’s not feasible, use a fake implementation that is ideally provided by the library owner**. This reduces the maintenance burden since the issues with mocks listed above don’t occur when using a real or fake implementation. 

For example:
```java
FakeSalaryProcessor fakeProcessor = new FakeSalaryProcessor(); // Designed for tests
MyPaymentService myPaymentService = new MyPaymentService(fakeProcessor);
assertThat(myPaymentService.sendPayment()).isEqualTo(PaymentStatus.SUCCESS);
```
If you can’t use the real implementation and a fake implementation doesn’t exist (and library owners aren’t able to create one), **create a wrapper class that calls the type, and mock this instead.** 
- This reduces the maintenance burden by avoiding mocks that rely on the signatures of the library API. 
  - For example:
  ```java
    @Mock MySalaryProcessor mockMySalaryProcessor; // Wraps the SalaryProcessor library
    ...
    // Mock the wrapper class rather than the library itself
    when(mockMySalaryProcessor.sendSalary()).thenReturn(PaymentStatus.SUCCESS);

    MyPaymentService myPaymentService = new MyPaymentService(mockMySalaryProcessor);
    assertThat(myPaymentService.sendPayment()).isEqualTo(PaymentStatus.SUCCESS);
  ```
To avoid the problems listed above, **prefer to test the wrapper class with calls to the real implementation**. 
- The downsides of testing with the real implementation (e.g. tests taking longer to run) are limited only to the tests for this wrapper class rather than tests throughout your codebase.

## Know Your Test Doubles

A test double is **an object that can stand in for a real object in a test**, similar to how a stunt double stands in for an actor in a movie. 
- These are sometimes all commonly referred to as “mocks”, but it's important to distinguish between the different types of test doubles since they all have different uses. 
- The most common types of test doubles are stubs, mocks, and fakes.
  - A stub has **no logic, and only returns what you tell it to return**. 
    - Stubs can be used when you need an object to return specific values in order to get your code under test into a certain state. 
    - While it's usually easy to write stubs by hand, using a mocking framework is often a convenient way to reduce boilerplate.
    ```java
    // Pass in a stub that was created by a mocking framework.
    AccessManager accessManager = new AccessManager(stubAuthenticationService);
    // The user shouldn't have access when the authentication service returns false.
    when(stubAuthenticationService.isAuthenticated(USER_ID)).thenReturn(false);
    assertFalse(accessManager.userHasAccess(USER_ID));
    // The user should have access when the authentication service returns true.
    when(stubAuthenticationService.isAuthenticated(USER_ID)).thenReturn(true);
    assertTrue(accessManager.userHasAccess(USER_ID));
    ```
    
  - A mock has **expectations about the way it should be called**, and a test should fail if it’s not called that way. 
    - Mocks are used to test interactions between objects, and are **useful in cases where there are no other visible state changes or return results that you can verify**
    - (e.g. if your code reads from disk and you want to ensure that it doesn't do more than one disk read, you can use a mock to verify that the method that does the read is only called once).
    ```java
    // Pass in a mock that was created by a mocking framework.
    AccessManager accessManager = new AccessManager(mockAuthenticationService);
    accessManager.userHasAccess(USER_ID);
    // The test should fail if accessManager.userHasAccess(USER_ID) didn't call
    // mockAuthenticationService.isAuthenticated(USER_ID) or if it called it more than once.
    verify(mockAuthenticationService).isAuthenticated(USER_ID);
    ```
- A fake doesn’t use a mocking framework: **it’s a lightweight implementation of an API that behaves like the real implementation, but isn't suitable for production** (e.g. an in-memory database). 
  - Fakes can be used when you can't use a real implementation in your test (e.g. if the real implementation is too slow or it talks over the network). 
  - You shouldn't need to write your own fakes often since fakes should usually be created and maintained by the person or team that owns the real implementation.
  ```java
  // Creating the fake is fast and easy.
  AuthenticationService fakeAuthenticationService = new FakeAuthenticationService();
  AccessManager accessManager = new AccessManager(fakeAuthenticationService);
  // The user shouldn't have access since the authentication service doesn't
  // know about the user.
  assertFalse(accessManager.userHasAccess(USER_ID));
  // The user should have access after it's added to the authentication service.
  fakeAuthenticationService.addAuthenticatedUser(USER_ID);
  assertTrue(accessManager.userHasAccess(USER_ID));
  ```
 The term “test double” was coined by Gerard Meszaros in the book xUnit Test Patterns. You can find more information about test doubles in the book, or on the book’s website. You can also find a discussion about the different types of test doubles in this article by Martin Fowler.

## Risk-Driven Testing

We are all conditioned to write tests as we code: unit, functional, UI—the whole shebang. We are professionals, after all. Many of us like how small tests let us work quickly, and how larger tests inspire safety and closure. Or we may just anticipate flak during review. We are so used to these tests that often we no longer question why we write them. This can be wasteful and dangerous.

Tests are a means to an end: 
  - To **reduce the key risks of a project**, and to **get the biggest bang for the buck.** 
  - This bang may not always come from the tests that standard practice has you write, or not even from tests at all.

Two examples:
  - “We built a new debugging aid. We wrote unit, integration, and UI tests. We were ready to launch.”
    - Outstanding practice. Missing the mark.
    - Our key risks were that we'd corrupt our data or bring down our servers for the sake of a debugging aid. None of the tests addressed this, but they gave a false sense of safety and “being done”.
    - We stopped the launch.
  - “We wanted to turn down a feature, so we needed to alert affected users. Again we had unit and integration tests, and even one expensive end-to-end test.”
    - Standard practice. Wasted effort.
    - The alert was so critical it actually needed end-to-end coverage for all scenarios. But it would be live for only three releases. The cheapest effective test? Manual testing before each release.
    - A Better Approach: Risks First

For every project or feature, think about testing. **Brainstorm your key risks and your best options to reduce them.** Do this at the start so you don't waste effort and can adapt your design. Write them down as a QA design so you can point to it in reviews and discussions.

To be sure, standard practice remains a good idea in most cases (hence it’s standard). **Small tests are cheap and speed up coding and maintenance, and larger tests safeguard core use-cases and integration.**

Just remember: Your tests are a means. The bang is what counts. It’s your job to maximize it.

## Test Behaviors, Not Methods

After writing a method, it's easy to write just one test that verifies everything the method does. But it **can be harmful to think that tests and public methods should have a 1:1 relationship.** 
What we really **want to test are behaviors**, where a single method can exhibit many behaviors, and **a single behavior sometimes spans across multiple methods.**

Let's take a look at a bad test that verifies an entire method:
```java
@Test public void testProcessTransaction() {
  User user = newUserWithBalance(LOW_BALANCE_THRESHOLD.plus(dollars(2));
  transactionProcessor.processTransaction(
  user,
  new Transaction("Pile of Beanie Babies", dollars(3)));
  assertContains("You bought a Pile of Beanie Babies", ui.getText());
  assertEquals(1, user.getEmails().size());
  assertEquals("Your balance is low", user.getEmails().get(0).getSubject());
}
```

Displaying the name of the purchased item and sending an email about the balance being low are two separate behaviors, but this test looks at both of those behaviors together just because they happen to be triggered by the same method. 
  - Tests like this very often become massive and difficult to maintain over time as additional behaviors keep getting added in eventually it will be very hard to tell which parts of the input are responsible for which assertions. 
  - The fact that the test's name is a direct mirror of the method's name is a bad sign.

It's a much better idea to use separate tests to verify separate behaviors:
```java
@Test 
public void testProcessTransaction_displaysNotification() {
  transactionProcessor.processTransaction(new User(), new Transaction("Pile of Beanie Babies"));
  
  assertContains("You bought a Pile of Beanie Babies", ui.getText());
}

@Test 
public void testProcessTransaction_sendsEmailWhenBalanceIsLow() {
  User user = newUserWithBalance(LOW_BALANCE_THRESHOLD.plus(dollars(2));
  transactionProcessor.processTransaction(user, new Transaction(dollars(3)));
  
  assertEquals(1, user.getEmails().size());
  assertEquals("Your balance is low", user.getEmails().get(0).getSubject());
}
```
Now, **when someone adds a new behavior, they will write a new test for that behavior**. 

Each test will remain focused and easy to understand, no matter how many behaviors are added. This will make your tests more resilient since adding new behaviors is unlikely to break the existing tests, and clearer since each test contains code to exercise only one behavior.

## Avoid Hard coding Values for Better Libraries

You may have been in a situation where you're using a value that always remains the same, so you define a constant. This can be a good practice as it removes magic values and improves code readability. 
But be mindful that **hardcoding values can make usability and potential refactoring significantly harder.**

Consider the following function that relies on hardcoded values:
```
// Declared in the module.
constexpr int kThumbnailSizes[] = {480, 576, 720};

// Returns thumbnails of various sizes for the given image.
std::vector<Image> GetThumbnails(const Image& image) {
  std::vector<Image> thumbnails;
  for (const int size : kThumbnailSizes) {
    thumbnails.push_back(ResizeImage(image, size));
  }
  return thumbnails;
}
```
Using hardcoded values can make your code:
- Less predictable: 
  - The caller might not expect the function to be relying on hardcoded values outside its parameters; 
  - a user of the function shouldn’t need to read the function’s code to know that. 
  - it is difficult to predict the product/resource/performance implications of changing these hardcoded values.
- Less reusable: 
  - The caller is not able to call the function with different values and is stuck with the hardcoded values. 
  - If the caller doesn’t need all these sizes or needs a different size, the function has to be forked or refactored to avoid aforementioned complications with existing callers.
   
**When designing a library, prefer to pass required values**, such as through a function call or a constructor. The code above can be improved as follows:
```html
std::vector<Image> GetThumbnails(const Image& image, absl::Span<const int> sizes) {
  std::vector<Image> thumbnails;
  for (const int size : sizes) {
    thumbnails.push_back(ResizeImage(image, size));
  }
  return thumbnails;
}
```
**If most of the callers use the same value for a certain parameter, make your code configurable** so that this value doesn't need to be duplicated by each caller. 
  - For example, you can define a **public constant that contains a commonly used value, or use default arguments** in languages that support this feature (e.g. C++ or Python).
  ```
   // Declared in the public header.
  inline constexpr int kDefaultThumbnailSizes[] = {480, 576, 720};
  
  // Default argument allows the function to be used without specifying a size.
  std::vector<Image> GetThumbnails(const Image& image, absl::Span<const int> sizes = kDefaultThumbnailSizes);
  ```
## Only Verify Relevant Method Arguments

What makes this test fragile?
```java
@Test
public void displayGreeting_showSpecialGreetingOnNewYearsDay() {
  fakeClock.setTime(NEW_YEARS_DAY);
  fakeUser.setName("Fake User”);
  userGreeter.displayGreeting();
  // The test will fail if userGreeter.displayGreeting() didn’t call  
  // mockUserPrompter.updatePrompt() with these exact arguments.
  verify(mockUserPrompter).updatePrompt("Hi Fake User! Happy New Year!", TitleBar.of("2018-01-01"), PromptStyle.NORMAL);
}
```
The test specifies exact values for all arguments to mockUserPrompter.
  - These arguments may need to be updated when the code under test is changed, even if the changes are unrelated to the behavior being tested. 
  - For example, if additional text is added to TitleBar, every test in the codebase that specifies this argument will need to be updated. 

In addition, **verifying too many arguments makes it difficult to understand what behavior is being tested** since it’s not obvious which arguments are important to the test and which are irrelevant.

Instead, **only verify arguments that affect the correctness of the specific behavior being tested.** **You can use argument matchers (e.g., any() and contains() in Mockito) to ignore arguments that don't need to be verified**:
```java
@Test 
public void displayGreeting_showSpecialGreetingOnNewYearsDay() {
  fakeClock.setTime(NEW_YEARS_DAY);
  userGreeter.displayGreeting();
  verify(mockUserPrompter).updatePrompt(contains("Happy New Year!"), any(), any()));
}
```
Arguments ignored in one test can be verified in other tests.
Following this pattern allows us to **verify only one behavior per test, which makes tests more readable and more resilient to change.** 
  - For example, here is a separate test that we might write:
  ```java
  @Test 
  public void displayGreeting_renderUserName() {
    fakeUser.setName(“Fake User”);
    userGreeter.displayGreeting();
    // Focus on the argument relevant to showing the user's name.
    verify(mockUserPrompter).updatePrompt(contains("Hi Fake User!"), any(), any());
    }
  ```

## Writing Descriptive Test Names

How long does it take you to figure out what behavior is being tested in the following code?
```java
@Test
public void isUserLockedOut_invalidLogin() {
  authenticator.authenticate(username, invalidPassword);
  assertFalse(authenticator.isUserLockedOut(username));
  
  authenticator.authenticate(username, invalidPassword);
  assertFalse(authenticator.isUserLockedOut(username));
  
  authenticator.authenticate(username, invalidPassword);
  assertTrue(authenticator.isUserLockedOut(username));
}
```
You probably had to read through every line of code (maybe more than once) and understand what each line is doing.

But how long would it take you to figure out what behavior is being tested if the test had this name?
`isUserLockedOut_lockOutUserAfterThreeInvalidLoginAttempts`

You should now be **able to understand what behavior is being tested by reading just the test name**, and you **don’t even need to read through the test body.**

The test name in the above code sample **hints at the scenario being tested** (“invalidLogin”), but it doesn’t actually say what the expected outcome is supposed to be, so you had to read through the code to figure it out.

**Putting both the scenario and the expected outcome in the test name** has several other benefits:

- If you **want to know all the possible behaviors a class has**, all you need to do is read through the test names in its test class, compared to spending minutes or hours digging through the test code or even the class itself trying to figure out its behavior. 
  - This can also be useful during code reviews since you can quickly tell if the tests cover all expected cases.
- By giving tests more explicit names, it **forces you to split up testing different behaviors into separate tests.** 
  - Otherwise you may be tempted to dump assertions for different behaviors into one test, which over time can lead to tests that keep growing and become difficult to understand and maintain.
- The exact behavior being tested might not always be clear from the test code.
  - If the test name isn’t explicit about this, sometimes you might have to guess what the test is actually testing.
- You can easily **tell if some functionality isn’t being tested**. 
  - If you don’t see a test name that describes the behavior you’re looking for, then you know the test doesn’t exist.
- When a test fails, you can **immediately see what functionality is broken** without looking at the test’s source code.

There are several common patterns for structuring the name of a test
- (one example is to name tests like an English sentence with “should” in the name, e.g., shouldLockOutUserAfterThreeInvalidLoginAttempts).
- Whichever pattern you use, the same advice still applies: Make sure test names contain both the scenario being tested and the expected outcome.
- Sometimes just specifying the name of the method under test may be enough, especially if the method is simple and has only a single behavior that is obvious from its name.

## Don't Put Logic in Tests

Programming languages give us a lot of expressive power. Concepts like operators and conditionals are important tools that allow us to write programs that handle a wide range of inputs. But this **flexibility comes at the cost of increased complexity**, which makes our programs harder to understand.

Unlike production code, **simplicity is more important than flexibility in tests**. Most unit tests verify that a single, known input produces a single, known output. Tests can a**void complexity by stating their inputs and outputs directly rather than computing them.** Otherwise it's easy for tests to develop their own bugs.

Let's take a look at a simple example. Does this test look correct to you?
```java
@Test
public void shouldNavigateToPhotosPage() {
  String baseUrl = "http://plus.google.com/";
  Navigator nav = new Navigator(baseUrl);
  nav.goToPhotosPage();
  assertEquals(baseUrl + "/u/0/photos", nav.getCurrentUrl());
}
```
The author is trying to avoid duplication by storing a shared prefix in a variable. Performing a single string concatenation doesn't seem too bad, but what happens if we simplify the test by inlining the variable?
```java
@Test
public void shouldNavigateToPhotosPage() {
  Navigator nav = new Navigator("http://plus.google.com/");
  nav.goToPhotosPage();
  assertEquals("http://plus.google.com//u/0/photos", nav.getCurrentUrl()); // Oops!
}
```
After eliminating the unnecessary computation from the test, the bug is obvious—we're expecting two slashes in the URL! This test will either fail or (even worse) incorrectly pass if the production code has the same bug. We never would have written this if we **stated our inputs and outputs directly instead of trying to compute them**. And this is a very simple example—when a test adds more operators or includes loops and conditionals, it becomes increasingly difficult to be confident that it is correct.

Another way of saying this is that, **whereas production code describes a general strategy for computing outputs given inputs, tests are concrete examples of input/output pairs (where output might include side effects like verifying interactions with other classes).** It's usually easy to tell whether an input/output pair is correct or not, even if the logic required to compute it is very complex. For instance, it's hard to picture the exact DOM that would be created by a Javascript function for a given server response. So the ideal test for such a function would just compare against a string containing the expected output HTML.

When tests do need their own logic, **such logic should often be moved out of the test bodies and into utilities and helper functions**. 
- Since such helpers can get quite complex, it's usually a good idea for **any nontrivial test utility to have its own tests.**

## Test Behavior, Not Implementation

Your trusty Calculator class is one of your most popular open source projects, with many happy users:
```java
public class Calculator {
  public int add(int a, int b) {
      return a + b;
  }
}
```
You also have tests to help ensure that it works properly:
```java
public void testAdd() {
  assertEquals(3, calculator.add(2, 1));
  assertEquals(2, calculator.add(2, 0));
  assertEquals(1, calculator.add(2, -1));
}
```
However, a fancy new library promises several orders of magnitude speedup in your code if you use it in place of the addition operator. You excitedly change your code to use this library:
```java
public class Calculator {
  private final AdderFactory adderFactory;
  
  public Calculator(AdderFactor adderFactory) { this.adderFactory = adderFactory; }
  
  public int add(int a, int b) {
    Adder adder = adderFactory.createAdder();
    ReturnValue returnValue = adder.compute(new Number(a), new Number(b));
    return returnValue.convertToInteger();
  }
}
```
That was easy, but what do you do about the tests for this code? 
- None of the existing tests should need to change since you only changed the code's implementation, but its user-facing behavior didn't change. In most cases, **tests should focus on testing your code's public API, and your code's implementation details shouldn't need to be exposed to tests.**

**Tests that are independent of implementation details are easier to maintain** since they don't need to be changed each time you make a change to the implementation. 
- They're also easier to understand since they basically act as code samples that show all the different ways your class's methods can be used, so even someone who's not familiar with the implementation should usually be able to read through the tests to understand how to use the class.

There are many cases where you do want to test implementation details (e.g. you want to ensure that your implementation reads from a cache instead of from a datastore), but this should be less common since in most cases your tests should be independent of your implementation.

Note that **test setup may need to change if the implementation changes** (e.g. if you change your class to take a new dependency in its constructor, the test needs to pass in this dependency when it creates the class), but the **actual test itself typically shouldn't need to change if the code's user-facing behavior doesn't change.**

## Change-Detector Tests Considered Harmful

You have just finished refactoring some code without modifying its behavior. Then you run the tests before committing and… a bunch of unit tests are failing. While fixing the tests, you get a sense that you are wasting time by mechanically applying the same transformation to many tests. Maybe you introduced a parameter in a method, and now must update 100 callers of that method in tests to pass an empty string.

What does it look like to write tests mechanically? Here is an absurd but obvious way:

```html
// Production code:
def abs(i: Int)
return (i < 0) ? i * -1 : i

// Test code:
for (line: String in File(prod_source).read_lines())
switch (line.number)
1: assert line.content equals "def abs(i: Int)"
2: assert line.content equals "  return (i < 0) ? i * -1 : i"
```

That test is clearly not useful: it contains an exact copy of the code under test and acts like a checksum. A correct or incorrect program is equally likely to pass a test that is a derivative of the code under test. No one is really writing tests like that, but how different is it from this next example?
```html

// Production code:
def process(w: Work)
firstPart.process(w)
secondPart.process(w)

// Test code:
part1 = mock(FirstPart)
part2 = mock(SecondPart)
w = Work()
Processor(part1, part2).process(w)
verify_in_order
was_called part1.process(w)
was_called part2.process(w)
```

It is tempting to write a test like this because it requires little thought and will run quickly. This is a **change-detector test—it is a transformation of the same information in the code under test—and it breaks in response to any change to the production code, without verifying correct behavior of either the original or modified production code**.

Change detectors provide negative value, since the tests do not catch any defects, and the added maintenance cost slows down development. These tests should be re-written or deleted.

## Testing State vs. Testing Interactions

There are typically two ways a unit test can verify that the code under test is working properly: 
   **by testing state or by testing interactions**. What’s the difference between these?

- Testing state means you're **verifying that the code under test returns the right results.**
```java
public void testSortNumbers() {
  NumberSorter numberSorter = new NumberSorter(quicksort, bubbleSort);
  // Verify that the returned list is sorted. It doesn't matter which sorting
  // algorithm is used, as long as the right result is returned.
  assertEquals(new ArrayList(1, 2, 3), numberSorter.sortNumbers(new ArrayList(3, 1, 2)));
}
```
- Testing interactions means you're **verifying that the code under test calls certain methods properly**.
```java
public void testSortNumbers_quicksortIsUsed() {
  // Pass in mocks to the class and call the method under test.
  NumberSorter numberSorter = new NumberSorter(mockQuicksort, mockBubbleSort);
  numberSorter.sortNumbers(new ArrayList(3, 1, 2));
  // Verify that numberSorter.sortNumbers() used quicksort. The test should
  // fail if mockQuicksort.sort() is never called or if it's called with the
  // wrong arguments (e.g. if mockBubbleSort is used to sort the numbers).
  verify(mockQuicksort).sort(new ArrayList(3, 1, 2));
}
```
  - The second test may result in good code coverage, but it **doesn't tell you whether sorting works properly,** only that quicksort.sort() was called. 
  - Just because a test that uses interactions is passing doesn't mean the code is working properly. 
  - This is why in **most cases, you want to test state, not interactions.**
  - In general, **interactions should be tested when correctness doesn't just depend on what the code's output is, but also how the output is determined**.
  - In the above example, you would only want to test interactions in addition to testing state if it's important that quicksort is used (e.g. **the method would run too slowly with a different sorting algorithm**), otherwise the test using interactions is unnecessary.
  - What are some other examples of cases where you want to test interactions?
      - The code under test **calls a method where differences in the number or order of calls would cause undesired behavior, such as side effects** (e.g. you only want one email to be sent), 
        - **latency** (e.g. you only want a certain number of disk reads to occur) 
        - or **multithreading issues** (e.g. your code will deadlock if it calls some methods in the wrong order).
      - Testing interactions ensures that your tests will fail if these methods aren't called properly.
      - You're testing a UI where the rendering details of the UI are abstracted away from the UI logic (e.g. using MVC or MVP). 
        - In tests for **your controller/presenter, you only care that a certain method of the view was called, not what was actually rendered,** so you can test interactions with the view. 
        - Similarly, when testing the view, you can test interactions with the controller/presenter.

## Don’t Overuse Mocks

When writing tests for your code, it can seem easy to ignore your code's dependencies by mocking them out.
```java
@Test
public void testCreditCardIsCharged() {
  paymentProcessor = new PaymentProcessor(mockCreditCardServer);
  when(mockCreditCardServer.isServerAvailable()).thenReturn(true);
  when(mockCreditCardServer.beginTransaction()).thenReturn(mockTransactionManager);
  when(mockTransactionManager.getTransaction()).thenReturn(transaction);
  when(mockCreditCardServer.pay(transaction, creditCard, 500)).thenReturn(mockPayment);
  when(mockPayment.isOverMaxBalance()).thenReturn(false);
  paymentProcessor.processPayment(creditCard, Money.dollars(500));
  verify(mockCreditCardServer).pay(transaction, creditCard, 500);
}
```
However, not using mocks can sometimes result in tests **that are simpler and more useful.**
````java
@Test
public void testCreditCardIsCharged() {
  paymentProcessor = new PaymentProcessor(creditCardServer);
  paymentProcessor.processPayment(creditCard, Money.dollars(500));
  assertEquals(500, creditCardServer.getMostRecentCharge(creditCard));
}
````

Overusing mocks can cause several problems:
- **Tests can be harder to understand.** 
  - Instead of just a straightforward usage of your code (e.g. pass in some values to the method under test and check the return result), you need to include extra code to tell the mocks how to behave.
  - Having this **extra code detracts from the actual intent of what you’re trying to test**, and very often this code is hard to understand if you're not familiar with the implementation of the production code.
- Tests can be **harder to maintain**. 
  - **When you tell a mock how to behave, you're leaking implementation details of your code into your test.** 
  - When implementation details in your production code change, you'll need to update your tests to reflect these changes. 
  - Tests should typically know little about the code's implementation, and **should focus on testing the code's public interface.**
- Tests can **provide less assurance that your code is working properly.** 
  - When you tell a mock how to behave, the only assurance you get with your tests is that your code will work if your mocks behave exactly like your real implementations. 
  - This can be very hard to guarantee, and the problem gets worse as your code changes over time, as the **behavior of the real implementations is likely to get out of sync with your mocks**.
    
Some signs that you're overusing mocks are if **you're mocking out more than one or two classes**, or **if one of your mocks specifies how more than one or two methods should behave**. If you're trying to read a test that uses mocks and find yourself mentally stepping through the code being tested in order to understand the test, then you're probably overusing mocks.

Sometimes you can't use a real dependency in a test (e.g. if it's too slow or talks over the network), but there may better options than using mocks, such as **a hermetic local server** (e.g. a credit card server that you start up on your machine specifically for the test) or a **fake implementation** (e.g. an in-memory credit card server).

## Keep Cause and Effect Clear

Can you tell if this test is correct?
```java 
@Test public void testIncrement_existingKey() {
  assertEquals(9, tally.get("key1"));
}
```
It’s impossible to know without seeing how the tally object is set up:
```java
private final Tally tally = new Tally();

@Before public void setUp() {
   tally.increment("key1", 8);
   tally.increment("key2", 100);
   tally.increment("key1", 0);
   tally.increment("key1", 1);
}

// 200 lines away
        
@Test public void testIncrement_existingKey() {
  assertEquals(9, tally.get("key1"));
}
```
The problem is that the modification of key1's values occurs 200+ lines away from the assertion. Otherwise put, the cause is hidden far away from the effect.

Instead, write tests **where the effects immediately follow the causes**. It's how we speak in natural language: “If you drive over the speed limit (cause), you’ll get a traffic ticket (effect).” Once we **group the two chunks of code, we easily see what’s going on:**
```java
private final Tally tally = new Tally();
@Test
public void testIncrement_newKey() {
  tally.increment("key", 100);
  assertEquals(100, tally.get("key"));
}
@Test
public void testIncrement_existingKey() {
  tally.increment("key", 8);
  tally.increment("key", 1);
  assertEquals(9, tally.get("key"));
}
@Test
public void testIncrement_incrementByZeroDoesNothing() {
  tally.increment("key", 8);
  tally.increment("key", 0);
  assertEquals(8, tally.get("key"));
}
```
This style may require a bit more code. **Each test sets its own input and verifies its own expected output.** The payback is in more readable code and lower maintenance costs.

## Web Testing Made Easier: Debug IDs

**Adding ID attributes to elements can make it much easier to write tests that interact with the DOM** (e.g., WebDriver tests). Consider the following DOM with two buttons that differ only by inner text:
```html
<!--Save button	Edit button-->
<div class="button">Save</div>
<!--Edit button-->
<div class="button">Edit</div>
```
How would you tell WebDriver to interact with the “Save” button in this case? 

You have several options. 
- One option is to **interact with the button using a CSS selector**:
  ```css
  div.button
  ```
  - However, this approach is not sufficient to identify a particular button, and there is no mechanism to filter by text in CSS. 
- Another option would be to **write an XPath, which is generally fragile and discouraged**:
  ```xpath
  div[@class='button' and text()='Save']
  ```
- Your best option is to **add unique hierarchical IDs where each widget is passed a base ID that it prepends to the ID of each of its children**. The IDs for each button will be:
  ```html
  contact-form.save-button
  contact-form.edit-button
  ```
  
Consider another example. Let’s set IDs for repeated UI elements in Angular using ng-repeat. Setting an index can help differentiate between repeated instances of each element:
```html
<tr id="feedback-{{$index}}" class="feedback" ng-repeat="feedback in ctrl.feedbacks" 
```
In GWT you can do this with ensureDebugId(). Let’s set an ID for each of the table cells:
@UiField FlexTable table;
UIObject.ensureDebugId(table.getCellFormatter().getElement(rowIndex, columnIndex),
    baseID + colIndex + "-" + rowIndex);

Take-away: **Debug IDs are easy to set and make a huge difference for testing. Please add them early**.

## Fake Your Way to Better Tests

After many years of blogging, you decide to try out your blog platform's API. You start playing around with it, but then you realize: 

how can you tell that your code works without having your test talk to a remote blog server?
```java
public void deletePostsWithTag(Tag tag) {
  for (Post post : blogService.getAllPosts()) {
      if (post.getTags().contains(tag)) {
          blogService.deletePost(post.getId()); 
      }
  }
}
```
**Fakes to the rescue!** 
- A fake is a lightweight implementation of an API that behaves like the real implementation, but isn't suitable for production.
- In the case of the blog service, all you care about is the ability to retrieve and delete posts. 
  - While a real blog service would need a database and support multiple frontend servers, you don’t need any of that to test your code, all you need is any implementation of the blog service API. You can achieve this with a simple in-memory implementation:
    ```java
    public class FakeBlogService implements BlogService {  
    
      private final Set<Post> posts = new HashSet<Post>(); // Store posts in memory
      public void addPost(Post post) { posts.add(post); }
      public void deletePost(int id) {
        for (Post post : posts) {
         if (post.getId() == id) { 
              posts.remove(post); return; 
            }
        }
        throw new PostNotFoundException("No post with ID " + id);
      }
    
       public Set<Post> getAllPosts() { return posts; }
    }
    ```
Now your tests can swap out the real blog service with the fake and the code under test won't even know the difference.
  
**Fakes are useful for when you can't use the real implementation in a test**, 
- such as if the real implementation is too slow (e.g. it takes several minutes to start up) 
- or if it's non-deterministic (e.g. it talks to an external machine that may not be available when your test runs).
- **You shouldn't need to write your own fakes often since each fake should be created and maintained by the person or team that owns the real implementation**. 
  - If you’re using an API that doesn't provide a fake, it’s often easy to create one yourself: 
    - **write a wrapper around the part of the code that you can't use in your tests**, and create a fake for that wrapper. 
    - Remember to **create the fake at the lowest level possible** (e.g. if you can't use a database in your tests, fake out the database instead of faking out all of your classes that talk to the database), that **way you'll have fewer fakes to maintain**, and **your tests will be executing more real code for important parts of your system.**
- Fakes should **have their own tests to ensure that they behave like the real implementation** (e.g. if the real implementation throws an exception when given certain input, the fake implementation should also throw an exception when given the same input). 
  - One way to do this is to **write tests against the API's public interface, and run those tests against both the real and fake implementations.**
  
If you still don't fully trust that your code will work in production if all your tests use a fake, you can **write a small number of integration tests to ensure that your code will work with the real implementation.**

## a fluent assertion framework

As engineers, we spend most of our time reading existing code, rather than writing new code. Therefore, **we must make sure we always write clean, readable code.** The **same goes for our tests;** we need a way to clearly express our test assertions.

Truth is an open source, fluent testing framework for Java designed to make your test assertions and failure messages more readable. The fluent API makes **reading (and writing) test assertions much more natural, prose-like, and discoverable in your IDE via autocomplete.**
- For example, compare how the following assertion reads with JUnit vs. Truth:
```java
assertEquals("March", monthMap.get(3));          // JUnit
assertThat(monthMap).containsEntry(3, "March");  // Truth
```

  - Both statements are asserting the same thing, but the assertion written with Truth can be **easily read from left to right**, while the JUnit example requires "mental backtracking".
  - Another benefit of Truth over JUnit is the addition of **useful default failure messages**. For example:
  ```java
    ImmutableSet<String> colors = ImmutableSet.of("red", "green", "blue", "yellow");
    assertTrue(colors.contains("orange"));  // JUnit
    assertThat(colors).contains("orange");  // Truth
  ```

   - In this example, both assertions will fail, but JUnit will not provide a useful failure message. 
     - However, Truth will provide a clear and concise failure message:
     ```java
      AssertionError: <[red, green, blue, yellow]> should have contained <orange>
     ```
   - Truth already supports specialized assertions for most of the common JDK types (Objects, primitives, arrays, Strings, Classes, Comparables, Iterables, Collections, Lists, Sets, Maps, etc.), as well as some Guava types (Optionals). Additional support for other popular types is planned as well (Throwables, Iterators, Multimaps, UnsignedIntegers, UnsignedLongs, etc.).
   - Truth is also **user-extensible**:
     - you can easily write a Truth subject to make fluent assertions about your own custom types. By creating your own custom subject, both your assertion API and your failure messages can be domain-specific.
   - Truth's goal is not to replace JUnit assertions, but to improve the readability of complex assertions and their failure messages. JUnit assertions and Truth assertions can (and often do) live side by side in tests.

Also AssertJ is similar

https://github.com/google/truth

##