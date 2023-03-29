# Humble Object 

## Aim 

- separating behaviors that are easy to handle from behaviors that are hard to handle 
  - ie  separating external events or dependencies from domain logic

## Why 

- Makes unit testing easier
- Hard to test 3rd party services, randomness, time, io 
  - unit testing these are hard, as cannot control, slow, money etc
  - Can isolate these areas away from the core logic we wish to test
- encapsulated hard-to-test stuff and easy-to-test stuff.

## How 

- Take out the hard - testing parts and put it into a wrapper that you can stub/mock in your test. That wrapper is called Humble object.

## Issues 

- These behaviours still need to be tested, but via integration, E2E or manual tests

