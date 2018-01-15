# fp smalltalks

Some sessions I do in @KeyweeLabs to embrace some functional programming concepts and patterns that I like.

### Small assumptions

I’m no expert in functional programming - It’s just a fun hobby, therefore I might have some mistakes. This is fine,
just correct me if I have any errors. There is a lot of theory behind functional programming, and I'm probably not going
to touch it - Algebra, Lambda Calculus, Category theory. Why? because it's interesting but we need to be practical.
There is a lot of code smell in our codebase that could be avoided using fp patterns. In any time, if you find code
smells in our codebase, share them!

### Setting up

* `yarn`
* Remap `<CR>` in vim while on visual mode to run the code blocks in node: `vnoremap <CR> :!node<CR>`

### Libraries in use

* [Ramda](http://ramdajs.com)

## [Session 1](talk01/)

Introduction and Lenses

* [First class functions](talk01/01_first-class-functions.md) - introduction
* [Function purity](talk01/02_purity.md) - introduction
* [Function composition](talk01/03_function_composition.md) - introduction
* [Lenses](talk01/04_lenses.md) - pattern

# Thanks

Most of the files here are based on @drboolean's great
[mostly adequate guide](https://drboolean.gitbooks.io/mostly-adequate-guide/) and lots of other material I found online
(Medium, etc). Thank you, community! :heart:
