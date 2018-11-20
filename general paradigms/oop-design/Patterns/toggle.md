- https://martinfowler.com/articles/feature-toggles.html
- https://dzone.com/articles/feature-toggles-are-one-worst

## Api version toggles

A toggle which is kept in configuration, that allows a new version of some api the app is using to be used at some time later, while keeping the exisiting behaviour so if any issues occur the toggle can be switched back to the older version.

Thus allowing changes to version used during next release, or subsequent release if some other app is not ready.

Always good to have property/config management to handle property changes when there is no release of the app (dynamic properties). But at a later date, this property change must be added as part of the app for the next release.

Thus when the new version is working, the old version needs to be cleared up from the code base. The toggle needs to be removed, or parts of it.
