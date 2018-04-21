# On call/ 2nd line support

When a release of some version your team's app is pushed on the pipeline to a new environment (ie production/live), then there needs to be eyes and ears on the process to check everything goes through correctly.

What to do
- Be on call
- Laptop is able to connect remotely to the intranet
- Be able to connect to the boxes where the app is being deployed so that the logs can be read
  - ssh on to them
- Be able to access the database to diagnose any problems
- Be able to access the property manager to check properties and see if it can be changed

The aim is not to do any  coding but to see if there is a quick solution. ie

- if there is mistyped property, change it
- If something more serious, then if there is a toggle in the property, change it back
- Otherwise look to roll back to previous version
