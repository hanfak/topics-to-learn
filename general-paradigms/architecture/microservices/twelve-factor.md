# 12 Factor applications

- offers a set of best practices for building modern software applications
- created by the platform heroku

1. Codebase:
- Have one place to keep all your code, and manage it using version control like Git.

2. Dependencies:
- List all the things your app needs to work properly, and make sure they're easy to install.
- maven/gradle

3. Config:
- Keep important settings like database credentials separate from your code, so you can change them without rewriting code.
- Spring config/custom remote config, config maps, secrets

4. Backing Services:
- Use other services (like databases or payment processors) as separate components that your app connects to.
- Other connected microservices

5. Build, Release, Run:
- Make a clear distinction between preparing your app, releasing it, and running it in production.
- Jenkins/teamcity/github actions CI/CD, Blue-Green/Canary

6. Processes:
- Design your app so that each part doesn't rely on a specific computer or memory. It's like making LEGO blocks that fit together.
- Stateless APIs

7. Port Binding:
- Let your app be accessible through a network port, and make sure it doesn't store critical information on a single computer.
- NAT Gateway/Service discovery/Service Mesh

8. Concurrency:
- Make your app able to handle more work by adding more copies of the same thing, like hiring more workers for a busy restaurant.
- Docker/Podman containers, idempotancy, immutability

9. Disposability:
- Your app should start quickly and shut down gracefully, like turning off a light switch instead of yanking out the power cord.
- Kubernetes orchestration for containers


10. Dev/Prod Parity:
-  Ensure that what you use for developing your app is very similar to what you use in production, to avoid surprises.
- Separate PreProd/Prod pipelines and environments

11. Logs:
-  Keep a record of what happens in your app so you can understand and fix issues, like a diary for your software.
- Fluentd/Splunk
    

12. Admin Processes:
-  Run special tasks separately from your app, like doing maintenance work in a workshop instead of on the factory floor.

## Links 
- https://12factor.net/
- https://www.bmc.com/blogs/twelve-factor-app/
- https://cloudposse.com/12-factor-app/
- https://reflectoring.io/spring-boot-12-factor-app/
