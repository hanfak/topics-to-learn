# Adaptable Architecture 

- allows the system to be configured, to suit different needs
- ie toggles, feature flags, plugins etc 

## Last 10% trap

- Apps start as success, but end up as total failures 
  - Cannot meet the needs of users, as they want more or specific things
- 80% of the app is easy and fast to build, meets the majority of the needs of the user
- next 10% is harder, possible to do but difficult, need to do some hacky stuff 
  - the system is not built in a way to naturally do this 
- Last 10%, cannot get it to work or the framework prevents you from you doing this
- But the users always want 100%, and never satisfied
- This may not be an issue, esp for prototyping, mvp, as getting the product out there is better, 
  - but eventually it can lead to whole rewrites with high probability of never getting some bugs, and/or having to maintain two systems

### Examples 

- Use of 4GL, ie Borland, Access 
  - programmed/created systems but was tied to the environment 
- Vendors selling an all in one package,which state that you can adapt it completely
  - which is lie, eventually you will hit an issue which can work with it
  - impossible, cause not all scenarios that are possible can be created or tested 
  - Handle all the easy stuff first, but eventually need to write a custom app to meet your own needs
- Possibly Serverless
- low code environments 