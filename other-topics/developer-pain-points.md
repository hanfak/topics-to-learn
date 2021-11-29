# developer-pain-points

Setting up a new developer environment. Even the most declarative and reproducible environments have leaky abstractions.
Writing Dynamic SQL or using an ORM (Object-Relational Mapping) library. Both are bad solutions to a necessary problem.
Compiling frontend code. Nowadays, even interpreted languages need a compilation step: TypeScript to JavaScript, Sass to CSS, JavaScript modules, minification, uglification, polyfills, and more. It doesn't help that JavaScript tooling doesn't have the most obvious documentation either.
Debugging anything that's cached. Now, we have multiple layers of caching – Cloudfront, S3, and web servers have their own caching rules.
Adding or updating a new dependency. See Nine Circles of Dependency Hell.
Managing changes across multiple repositories.
On the flip side, making tools work with a monorepo.
Tracing requests across microservices.
Sharing a development database.
Running your code through CI/CD and diagnosing real errors vs. flakes.
Managing differences between development and production. (Development/Production parity).
Learning differences across clouds – Identity, APIs, and products.
We've always had to wait for our code to compile. Now we need to wait for the Docker container to be built, pushed to a registry, pulled down by Kubernetes, and everything else too.
