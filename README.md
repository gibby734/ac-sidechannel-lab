# AC & Side-Channel Lab

A single-file, offline teaching app for SE/CprE 4210 (Iowa State University) that lets you poke at three classic software security failures: a timing side channel, catastrophic regex backtracking (ReDoS), and an algorithmic complexity bug caused by a shared static pointer. Everything is simulated in plain JavaScript inside `index.html`. No real C, Java, or regex engine code runs, and nothing is sent anywhere.

## What it teaches

### 1. Timing side channel: cracking a password one character at a time
A simulated C password checker rejects wrong-length guesses instantly and, for right-length guesses, sleeps one second per mismatched character. That delay is a Hamming-distance oracle. The module lets you set the secret, send guesses by hand and watch the simulated response time, then run an animated **Auto-crack** that first finds the length (the only length that sleeps) and then solves each position by looking for the candidate that makes the sleep drop by one. A **Fixed (constant-time)** toggle makes every wrong guess look identical, and the same attack fails.

### 2. ReDoS: catastrophic backtracking
A tiny backtracking regex matcher, written by hand so each recursive call can be counted, runs the vulnerable email pattern `([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+)*` and the classic `(a+)+$` against generated benign and malicious inputs. A slider sets the input length, buttons run each input, a sweep fills in a log-scale chart of steps versus length, and a 5,000,000 step cap keeps the page responsive. The explanation covers why the overlap between the group's tail class and the next group's head class creates ambiguity, and why `*` over the group multiplies those choices into exponential work.

### 3. AC bug: a shared static pointer makes a linked list loop
A simulation of the course game: six shape nodes (Circle, Hexagon, Oval, Rectangle, Square, Triangle) linked by `build()`. The Rectangle class keeps its `next` in a static field shared by every Rectangle, so building the list overwrites it. Pick the shape for each slot, randomize, or run 100 random rounds and count how many hit the loop. An SVG diagram shows the real pointers after `build()` (instance pointers, shared static pointers, and cycle-closing pointers are color coded), and an animated traversal stops at the seventh visit with `TimeLimitExceeded`.

## How to run

- **Locally:** download or clone the repository and double-click `index.html`. It works from the file system in any modern browser with no server, build step, or network access. It respects your system light/dark preference.
- **GitHub Pages:** push the repository to GitHub, enable Pages for the main branch (root), and open the published URL. Nothing else needs to be configured because the app is one static file.

All controls are keyboard operable: the tabs respond to the left and right arrow keys, and every input has a label.

## Files

- `index.html`: the entire app (HTML, CSS, and commented JavaScript).
- `README.md`: this file.
- `reflection.md`: a short student reflection on building the app with an AI-assisted workflow.

## AI-assisted workflow

This app was built with Claude (Anthropic) through the Claude desktop app. The author wrote the specification for the three modules, iterated on the prompts as the app took shape, and tested each build in the browser, feeding back bugs and design changes (for example the step cap on the backtracking matcher and the color-coded pointer diagram) until the simulations behaved and taught the way the course material describes. See `reflection.md` for details.

## Author and license

Griffin Yocum (GitHub: [gibby734](https://github.com/gibby734))

Released under the MIT License.
