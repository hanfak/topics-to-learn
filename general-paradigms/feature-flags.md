  # Feature Flags/toggle

- Pattern that allows ease of working with master/trunk based development and allowing continous integration
- Provide us with a mechanism to selectively enable and disable features without requiring a production code deployment
- When several stories are in play, and one story needs to be release, but anout story is still in development (has not been tested and code shouldnt be in the release).
  - We get around this problem by using a feature flag.
  - This allows the first story to be released while the other stories that are still in development can continue to be worked on.
- Other areas a feature flag can be used for,
  - are a/b testing - can turn on the flag for different production environments which will cater for select customers
  - When the feature needs to be roled out to all users, it can be turned with just a property change and no code changes, thus no QA
  - Allow for easy roll back
    - ie new version of downstream api is being used, after release the new api has issues. Release team can then do an immediate release with changed toggle or use dynamic properties to go back to using the old api
  - A feature is being created, but it realies on a service not createdy, yet. Can use toggle, to turn off feature, but release it. When new service is ready can turn on toggle and start to consume the service
- A feature flag or toggle, is a property (in some property/config file).
  - The code changes which might affect the user is placed in an `if` statement. So only when the toggle is turned on, then the code will be implemented
  - The toggle in config could be true/false, yes/no, etc
  - We can set the method to get the feature flag property to have a default, in case this was missing from the property file.
  - The code that is implemented under the feature flag, does not have to be the whole code that was added.
    - The processing can still be kept, but the return value of the output will be under the feature flag
- Acceptance tests should test should have cases with toggle on and off.
- Testing should also be done to see toggle can be turned on and off

## Best Practices

- Use feature flags to create a kill switch for features. Simply turn it off if it doesn’t work and fix it on Monday (instead of on the weekend). No big rollbacks needed.
- We can use feature flags in a single branch instead of one branch for each feature. This enables trunk-based development.
- Use feature flags to create controlled rollouts. At first, only expose a fraction of the users to the new feature and progressively increase this fraction to make sure the feature works as expected.
  - A side-effect of controlled rollouts is that we can let users opt-in to a beta test and only activate certain features for the beta testers without having to set up a whole new environment for the tests.
  - Inversely, we can block a feature for certain users if we need to.
- With feature flags, we can test in production if we activate the features only for ourselves. “We always test in production - sometimes we’re just lucky enough to have tested before that”. Instead of trying (and failing) to reproduce errors in a staging environment, make the production environment observable enough to support error analysis.
- In subscription models, we can wrap features that are available for a certain subscription level with long-lived feature flags. This way we can easily move features between subscription levels.
- Feature flags easily allow the sunsetting of features that we no longer want to have in the system.

## Anti patterns

- Ambiguously named feature flags lead to misunderstandings and activation of deactivation of the wrong feature. Think long and deep when naming feature flags. Have a naming pattern
- Overused feature flags, i.e. using a single feature flag for multiple things, can lead to feature flags with mixed responsibilities and unwanted side effects. We don’t understand what the feature flag does anymore.
- Overlapping feature flags might conflict with each other and may have unwanted side effects on each other.
- Dangerous feature flags are feature flags that wrap a very important feature without which many users couldn’t work with the software anymore. Either remove the feature flag completely or at least don’t make it too easy to disable (e.g. don’t put a button on a dashboard that allows to disable it - there’s a true story behind that).
- Leftover feature flags are feature flags that stay in the system and are not maintained anymore. They become technical debt. What’s worse: when the feature flag server isn’t available for some reason, the feature flags fall back to the default value we defined 2 years ago, which might not be the value we want anymore.

## Links

- https://completedeveloperpodcast.com/episode-25/
- https://trunkbaseddevelopment.com/feature-flags/
- https://martinfowler.com/articles/feature-toggles.html
- https://www.youtube.com/watch?v=2lAF3_vd0k0  Feature Flags are more than just Toggles 
