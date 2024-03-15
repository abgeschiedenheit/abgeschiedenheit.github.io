# introductory regex

2024-02-26

I have been playing with regular expressions (regex, in short) lately:

> Regular expressions (regexes) are patterns that describe strings. We might write a regex for filenames ending in ".jpg". Or we might write one that recognizes phone numbers.

To my surprise, it has been a bit of fun! Although, there is some foreshadowing of headaches in the future. Hmm.

The introductory regex problem I was stuck with an hour or so ago dealt with the following instructions:

> Write a regex that recognizes words that begin and end in "e". (The "e" at the beginning and end of the word must be separate, so the regex should match "ee" but not "e".)

From the outset, this seemed fairly approachable given what I already knew:

- The keywords 'begin' and 'end' meant I was working with *boundaries* and as such, was going to have to use the `^` and `$` anchors.

  - The `^` anchor denotes the beginning of the string, e.g., `/^moon/.test('moonlight')` evaluates to `true` whereas `/^moon/.test('milky moon')` is `false`.

  - The `$` anchor, on the other hand, denotes the end of the string, e.g., for the above two examples, it would evaluate to `false` and `true` respectively, given the regex `/moon$/`.

- Furthermore, the keyword 'separate' infers two things:

  - (1) The character `e` is either going to occur *one or more times* or *zero or more times* – considering the different variety of possible edge cases, the latter seems like the safe bet. In this area, we are dealing with *repetition*.

    - *One or more times* is represented by the `+` quantifier, e.g., `/o+/.test('moon')` is `true`, `/a+/.test('moon')` is `false`, and more complex, `/mo+on/.test('moon')` is `true`.

    - *zero or more times* is represented by the `*` quantifier, e.g., `/o*/.test('')` is true, `/n*/.test('moon')` is true.

  - (2) The clearest generalization: the character `e` must be present.

    - Determining presence is helpful with the wildcard metacharacter, `.`, by factor of matching any character, e.g., `/./.test('moon')` is true but `/./.test('')` is false.

    - The critical part of the wildcard is putting `.` next to another character means that they occur consecutively, e.g., `/o./` matches an "o" followed by any character while `/.o/` matches any character followed by an "o".

And so, we are at our conclusion: the answer to the problem above is `var re = /^e.*e$/`. But why is that? I get the beginning and the end but the meat of it is slightly confusing.

`e.` follows the instructions of seperation, that the `e` beginning character must be seperated from the `e` ending character. This is logical. Using the `node` REPL, `/e./.test('e')` turns out to be `false`. The wildcard metacharacter is indicating another character must follow the character `e` for there to be a match.

The following asterisk operator in `e.*` requires similar thinking. For instance, why doesn't `e.+` suffice? Why does `/e.+e/.test('ee')` evaluate to `false`? On the other hand, why does `/e.*e/.test('ee')` evaluate to `true`? Well, the former requires at least one instance of seperation between `ee` to occur whereas the latter allows for zero instances of seperation between `ee` to occur. 

Above all, I'm looking forward to getting deeper into regex. They might be handy in some particular cases. I'm here instinctively thinking of using regex to mask my e-mail if it's listed on a public website. Who knows? While fun to work through, I'm able to foresee regular expressions becoming exceedingly complex.