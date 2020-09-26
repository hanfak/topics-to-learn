# Cookies and Sessions

- https://thoughtbot.com/blog/lucky-cookies
- general https://www.youtube.com/watch?v=sovAIX4doOE

## Why use cookies?

## Same site cookie

- https://www.youtube.com/watch?v=aUF2QCEudPo

## Cookie creation

1. Document.cookie (client side)
2. set-cookie header (server side)


## Cookie scope

- Per domain
- Per scope

## Types

- Session cookie
  - no expires or max-age, once browser close they are “deleted” browsers are being smart and keep them though
- permanent cookie
  - set max-age
- httponly cookie
  - cannot be accessed with document.cookie
- secure cookie
  - only acceptable with https
- Third party cookie
  - page references another page, gets its own cookies.
  - Third Party Cookies https://www.youtube.com/watch?v=m4vatwFryI8
- Zombie Cookies
- recreted even after users delete them, e-tags from the server

## SEcruity

- cross site request forgery
- inject XSS script
- Stealing cookies
