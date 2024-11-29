<!-- TOC start (generated with https://github.com/derlin/bitdowntoc) -->

- [Client SDK Pattern ](#client-sdk-pattern)
    * [What](#what)
    * [Why? ](#why)
    * [Usage](#usage)
    * [To avoid](#to-avoid)
    * [How? ](#how)
        + [Tips ](#tips)
    * [Examples ](#examples)
    * [Advantages](#advantages)
    * [Disadvantage](#disadvantage)
    * [Links](#links)

<!-- TOC end -->

<!-- TOC --><a name="client-sdk-pattern"></a>
# Client SDK Pattern

<!-- TOC --><a name="what"></a>
## What

- a library or package that encapsulates all the logic required to interact with a service or application, including:
    - Handling network communication (e.g., HTTP requests/responses).
    - Serialization and deserialization (marshalling and unmarshalling) of data.
    - Error handling and retry logic.
    - API versioning management.

<!-- TOC --><a name="why"></a>
## Why?

- Instead of the client/consumer manually crafting API requests,
    - consumers can integrate the provided library into their applications, making development faster, more consistent, and less error-prone.

<!-- TOC --><a name="usage"></a>
## Usage
- The service is complex and has many endpoints or nuanced behavior (e.g., authentication, retries).
- You have multiple consumers across different teams or languages.
- You want to reduce the risk of consumers misusing the API.
- Backward compatibility and ease of integration are priorities.

<!-- TOC --><a name="to-avoid"></a>
## To avoid
- Lightweight APIs:
    - For simple APIs with minimal endpoints, the SDK might add unnecessary complexity.
- Highly Customizable Use Cases:
    - If consumers have highly varied needs, a generalized SDK might not be flexible enough.
- Frequent API Changes:
    - For rapidly evolving APIs, maintaining the SDK across multiple languages and versions can be a significant burden.
- Niche Languages:
    - Supporting niche programming languages with smaller user bases may not justify the cost and effort.
<!-- TOC --><a name="how"></a>
## How?

1. Define the Service Contract:
    - Use OpenAPI/Swagger, Protocol Buffers (for gRPC), or similar tools to define the service's endpoints, inputs, and outputs.
2. Generate or Write the SDK:
    - Auto-generation: Use tools like Swagger Codegen or gRPC tools to generate client libraries for various programming languages.
    - Manual Implementation: For custom functionality or highly optimized libraries, you may need to write the SDK manually.
3. Abstract Core Features:
    - Implement logic for authentication (e.g., API keys, OAuth tokens).
    - Handle marshalling and unmarshalling of request/response payloads.
    - Include error handling, retries, and logging.
4. Document and Distribute:
    - Provide clear documentation and examples for using the SDK.
    - Publish the SDK to package managers (e.g., Maven Central for Java, npm for JavaScript).
5. Version and Maintain:
    - Use semantic versioning to manage updates and ensure backward compatibility.

<!-- TOC --><a name="tips"></a>
### Tips
- understand requirements
    - Understand usage scenarios: Will the SDK be used in high-throughput environments, batch processing, or low-latency systems?
    - Determine supported platforms/languages: Prioritize languages most used by your consumers (e.g., Java, Python, JavaScript, etc.). Follow idiomatic conventions for each language.
    - Identify the target audience: Are the consumers developers, DevOps teams, or other services? Multi language?
- Ensure the SDK aligns with the API's design principles. For instance, if the API follows RESTful principles, the SDK should reflect RESTful semantics.
- Provide a High-Level Abstraction
    - Avoid exposing raw API details directly (e.g., HTTP methods or endpoints).
    - Provide domain-specific functions that map closely to user workflows:
        - Example: Instead of POST /users, provide createUser(userDetails)
    - Use clear, human-readable naming conventions for methods, objects, and parameters.
- Auto generate via opanapi or grpc
- Abstract Common Concerns
    - Authentication
        - Include built-in support for API keys, OAuth, or other authentication methods.
        - Example: Handle token refresh seamlessly for OAuth.
    - Error Handling
        - Implement consistent and predictable error handling mechanisms.
        - Define custom exception classes or error codes that map to your API's errors.
        - Provide retry logic for transient errors (e.g., HTTP 429 or 503).
    - Data Marshalling
        - Handle serialization/deserialization (e.g., JSON, XML) transparently.
        - Use typed objects or models for request and response data instead of raw strings or maps.
    - Logging
        - Include configurable logging for debugging API requests and responses.
        - Example: Allow users to enable debug logging to trace HTTP calls.
- Make It Easy to Use
    - use builders with defaults
        - Sensible Defaults
            - Use reasonable defaults for timeout, retries, and other settings.
            - Allow consumers to override defaults if needed.
    - The API should guide the user on how to proceed
        - you want your users to make as few mistakes as possible when they call the library in their code
        -  adding phases to the step builder pattern (introduced in the previous section) that constrict the available options on the next phase according to choice of the current phase can come in very handy.
    - Provide clear and minimal configuration options, such as:
        - api_key, base_url, and environment settings (e.g., production vs. staging).
    - Documentation and Examples
        - Include detailed documentation:
            - Installation steps.
            - Code examples for common use cases.
            - API reference.
        - Publish documentation on popular platforms like GitHub, ReadTheDocs, or a dedicated website.
- Test Extensively
    - Unit and Integration Tests
        - Cover all core SDK functionality with unit tests.
        - Test SDK behavior against a live or mock version of the service.
    - Multi-Environment Testing
        - Test across supported languages, platforms, and operating systems.
    - Backward Compatibility Testing
        - Ensure new SDK versions do not break existing integrations.
- Versioning and Compatibility
    - Semantic Versioning
        - Follow Semantic Versioning: MAJOR.MINOR.PATCH.
            - Increment MAJOR for breaking changes.
            - Increment MINOR for new features.
            - Increment PATCH for bug fixes.
    - Deprecation Strategy
        - Clearly communicate deprecated methods or features.
        - Provide migration guides for breaking changes.
- Version Pinning
    - Encourage consumers to pin specific SDK versions to avoid unexpected changes.
- Developer Experience (DX)
    - Clear Documentation
        - Create a dedicated README with:
        - Installation steps.
        - Quick-start examples.
        - Common troubleshooting tips.
    - Interactive Tools
        - Provide utilities or CLIs for testing and interacting with the API.
    - Open Source
        - Consider open-sourcing the SDK to gain feedback and contributions from the developer community.
- Provide Long-Term Maintenance
    - Regularly update the SDK to match API changes or enhancements.
    - Monitor user feedback for issues and feature requests.
    - Ensure strong support for debugging and issue resolution.
- Check if it is available via opensource
- A Multi-Layer design for various kinds of users
    - to have a basic API that exposes the “bare bones” features with maximum amount of configurability and customization, and provide additional “simpler” APIs on top for the most common use cases with presets built in.
- Don’t be afraid to rewrite bad APIs
    - backward compatibility guidelines have their limit and will sometimes involve compromises. The resulting APIs will become less clear over time, as more fields and methods are added in non-optimal places.
    -

<!-- TOC --><a name="examples"></a>
## Examples
- AWS SDK
    - https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/get-started.html
- Kafka Clients

<!-- TOC --><a name="advantages"></a>
## Advantages

- Ease of Use:
    - Consumers don’t need to handle low-level details like URL formation, headers, or payload serialization.
    - They use high-level, domain-specific methods provided by the library.
    - For example: Instead of writing raw HTTP calls, a consumer might call createUser() or fetchOrderDetails().
- Consistency:
    - A centralized library ensures that all consumers interact with the service in a standardized way, reducing discrepancies or misuse of the API.
- Encapsulation of Complexity:
    - The library abstracts complexities like authentication, pagination, rate-limiting, and retry policies.
- Versioning and Upgrades:
    - Changes to the API can be managed within the SDK, allowing consumers to adopt updates with minimal effort by upgrading the library version.
- Error Management:
    - The SDK can provide consistent error formats and handle common error scenarios (e.g., retries for transient failures).
- Code Reusability:
    - The library eliminates duplication of client-side logic across different consumers.

<!-- TOC --><a name="disadvantage"></a>
## Disadvantage

- Maintenance Overhead:
    - The library must be actively maintained to keep up with API changes and consumer needs.
    - Ongoing Support:
        - The SDK needs regular updates to stay in sync with API changes, feature additions, or bug fixes.
        - Supporting multiple versions of the SDK (for backward compatibility) increases complexity.
    - Bug Fixes and Patches:
        - Any bugs in the SDK can disrupt multiple consumers, requiring immediate fixes and redeployment.
    - Multi-Language Support:
        - If the SDK is offered in multiple languages, each version must be updated and maintained individually, often with language-specific expertise.
- Consumer Lock-In
    - Tight Coupling:
        - Consumers become dependent on the SDK, making it harder for them to switch to direct API calls or another service.
        - Any significant breaking change in the SDK can create friction for consumers.
- Language Support:
    - Supporting multiple programming languages can be resource-intensive.
- Cross-Language Consistency
    - Inconsistencies Across SDKs:
        - SDKs in different languages may end up with inconsistent features, behaviors, or documentation, creating confusion among consumers.
    - Feature Parity:
        - Achieving feature parity across multiple SDKs can be challenging, especially if certain languages require custom implementations for advanced functionality.
- Misalignment with Consumer Use Cases
    - Overgeneralization:
        - The SDK may focus on general use cases, making it less useful for edge cases or advanced scenarios.
    - Underutilization
        - Consumers might only use a subset of the SDK's features, resulting in wasted development effort.
- Dependency Management
    - Versioning Issues:
        - Consumers must upgrade their SDK versions to access new features or fixes, which can lead to compatibility challenges, especially in tightly regulated environments.
    - Dependency Bloat:
        - The SDK may introduce additional dependencies into the consumer’s project, which can cause version conflicts or increase the application's footprint
- Backward Compatibility:
    - Ensure that SDK updates don’t break existing consumers.
- Testing Challenges
    - Complex Test Scenarios:
        - The SDK must be tested against various versions of the underlying API and in diverse environments.
    - Integration Testing:
        - Changes to the SDK require extensive integration testing to ensure compatibility with real-world use cases.
- Risk of SDK Becoming Outdated
    - If the SDK fails to keep pace with API updates, consumers may encounter:
        - Missing functionality.
        - Deprecated methods.
        - Security vulnerabilities.
- Performance Concerns
    - Overhead:
        - The SDK’s abstraction layers (e.g., serialization/deserialization, retries) can introduce latency compared to raw API calls.
    - One-Size-Fits-All Design:
        - Optimizations for general use cases may not align with specific performance-critical scenarios.
    - Introduce as little latency as possible, especially for critical or high-frequency use cases.
- Configuration:
    - Issues when wanting to use your own libraries or way of doing things which are incompatible with the sdk
        - might need to use an adapter
        - For example, wanting to log specific things, but cannot unless monkey patching.
        - For example, not being able to use your logging framework but the sdk's one
-  Lack of Flexibility for Consumers
- Abstraction Limitations:
    - The SDK might not cover all use cases or provide fine-grained control over API interactions, forcing some consumers to bypass the SDK and use raw API calls.
- Customization Challenges:
    - Consumers may find the SDK’s built-in logic too rigid, limiting their ability to customize behavior like retries, timeouts, or error handling.
- Documentation and Usability Risks
    - Complex APIs:
        - If the underlying API is complex, translating it into an easy-to-use SDK can be difficult.
    - Inadequate Documentation:
        - Poorly documented SDKs can frustrate users, leading them to abandon the library or misuse it.
- Resource Intensity
    - Time and Expertise:
        - Developing a robust SDK takes time, requires skilled engineers, and diverts resources from other projects.
    - Third-Party Tool Dependencies:
        - If the SDK depends on tools like Swagger Codegen or OpenAPI Generator, the quality of the generated SDK can vary, and custom modifications may require significant effort.
-
<!-- TOC --><a name="links"></a>
## Links