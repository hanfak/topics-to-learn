# Environments

Aim is to have several environments where testing can be seen before going into prod. These environments should match prod, with option of getting back ups of data. Of course cannot get the same level of requests as prod. Get fast feedback, before going into prod. Not waiting for environment to be setup to do some testing

Need

- Local development, where devs  can run app locally in an environment similar to prod on the local machine (docker/vm) or in special server.
- Test
  - All apps running, some might be stubs (ie for 3rd party)
- Stage
  - Can have all the apps running, and have 3rd party apps running, maybe going to a test version
- Prod
  - App is deployed
