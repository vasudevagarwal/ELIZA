B01554290, B01554541

Instructions:
For Eliza - the full program Eliza, including the parts written by the TAs,
all you have to do is type in any input that can put/be interpreted into a
string in Ocaml. (We haven't tested, like, emojis, so don't quote us on *all*
possible characters.) The part that we wrote, eliza_respond, takes in a phrase
- a list of strings - and a set of rules we wrote, my_rules. The user doesn't
need to worry about the rules, unless they're aiming to change Eliza's
responses, so interaction only depends on inputting the phrase. The user
should expect a phrase/list of strings in response.

Overview:
eliza_respond:
When eliza_respond is called, it takes in two inputs: a phrase, and my_rules,
a list of rules. eliza_respond first calls extract on the phrase and the first
rule in my_list. If the phrase doesn't fit the pattern in the rule, then
extract produces None and eliza_respond recursively calls itself with the rest
of the list of rules, calling extract to test the second, third, fourth, etc.
rules until it gets a match. After finding an appropriate rule that returns
Some phrase list, it inputs this phrase list, plus the corresponding
response_template of the rule, into make_response. As make_response runs, it
produces a phrase comprised of text from the response template and the phrase
list. 

extract:
extract takes in a phrase and a pattern from a rule. It compares the phrase 
and pattern, outputting None if either list is empty as a form of base case.
It then matches the first element of pattern with the different types of 
response_element. With Any, it checks three possibilities, in order: removing
Any from the list without extracting anything from the phrase (essentially,
that Any represents no more words), extracting one more element and moving on
from Any, or extracting an element and continuing with Any. In other words,
it checks all the potential values in Any, moving on from one to the other if
one possibility ends up leading to a None. If the first element is One, then
the first element of the phrase is extracted, and extract moves on to the next
response element in the pattern. If the element is a Lit, it checks if the
first word in the phrase is equal; if it is, it moves on without actually
extracting the values. If it isn't, it returns None; which means either the
rule doesn't match the input, or that some other length value of Any might
work. As extract runs, it pulls out words and phrases that correspond to One
and Any spots, and eventually cons-es them into a phrase list, which is the 
ultimate output.

make_response:
make_response takes in a phrase list, produced by extract, and a 
response_template. It pattern matches the template; if it is empty, then it
returns an empty list; otherwise, it matches the first response_element to
either Text, in which case the phrases are appended to the recursive call, or
Place, which retrieves the corresponding object in the phrase and cons-es it
onto the recursive call.

Bugs:
Eliza's response may not always be grammatically correct, or entirely
comprehensible, on account of not passing the Turing test, but that's about it.

Collaboration: 
Kushagra Agarwal (both discussed some parts of the functionality but never saw or exchanges each others code)

Extra Features:
Yes 
Please try the following inputs:
"Hi my name is ...(one word)"
  | "Hello"
  | "What does the fox say?"
  | "Hooka chaka  hooka hooka"
  | "Valar morghulis"
  | "Are you dumb?"
  | "What will we do?"
  | "What"
  | "Listen to the captain"
  | "What will you do if I say no?"
  | "I need to work"
  | "Perfectly balanced"
  | "Eliza what can you help with?"
  | "What is the meaning of life"
  | "Life is shit"
In eliza_interactions.ml