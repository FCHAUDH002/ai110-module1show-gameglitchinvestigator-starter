# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?

When I first opened the game, there was the title, text about guessing range and attempts left, the developer debug info section, the textbox for the user to enter thier guess, and buttons to submit guess, start a new game, and view hints. The developer debug info section expands to specify which specified the secret number, attempt number, score, difficult, and history of previous attempts. There is also a settings sidebar that can be used to change the difficulty of the game which changes the range of numbers and number of attempts. One inconsistancy I noticed is that the sidebar said "Attempts allowed: 8" while the main game area already showed "Attempts left: 7" before I had even guessed. I also noticed that when playing the game, I had to click the submit guess button twice to see the hint.

- List at least two concrete bugs you noticed at the start  
  1. The hints were reversed. For example, if the number guessed is smaller than the secret number, the hint would say go lower instead of higher and vise-versa. 
  2. The game allowed hints that were outside of the specified range. For example, it would accept the number 0 as an attempt and give a hint despite being out of range. 
  3. The score did not reset and no guesses were able to be made after pressing the new game button.

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

The secret number was 6 and the difficulty setting was normal.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
|   1   |  go higher hint   |  go lower hint  |         none           |
|   10  |   go lower hint   |  go higher hint |         none           |
|   9   |   go lower hint   |  go higher hint |         none           |
|   90  |   go lower hint   |  go higher hint |         none           |
|   7   |   go lower hint   |  go higher hint |         none           |
|   0   | out of range error| attempt accepted|         none           |
|  101  | out of range error| attempt accepted|         none           |

Although there are 8 attempts allowed in the normal game, I was only allowed 7 attempts. 

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?

I used Claude Code in VS Code for this project.

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).

I asked Claude Code why the hints were backwards, and it found the exact problem in check_guess in app.py: the "Too Low" branch said "Go LOWER!" when it should've said "Go HIGHER!" I checked this myself by running the game and guessing both above and below the secret, and the hints made sense afterward.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

When I asked Claude Code to move check_guess into logic_utils.py, it didn't warn me that logic_utils.py already had an empty placeholder version of check_guess that just threw an error. My tests ended up calling that empty version instead of my actual fix, so pytest failed even though my code was right. I figured this out from the pytest error message and had Claude Code swap in my real function instead.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?

For the hint bug, I played the game multiple times after the fix and checked that every hint matched the actual direction (guessing low said "Go Higher," guessing high said "Go Lower"). For the New Game bug, I played a full round until I lost, clicked New Game, and confirmed the score went back to 0 and I could actually submit a new guess afterward instead of getting stuck.

- Describe at least one test you ran (manual or using pytest) and what it showed you about your code.

I ran the test_new_game_button_resets_state test, which simulates losing a round and then clicking New Game to check that score, status, and history all reset properly. The first time I ran the full test suite, it actually showed me a separate problem I hadn't noticed. The starter tests were failing because check_guess now returns a tuple instead of a plain string, which I had to fix in the test file before everything passed.

- Did AI help you design or understand any tests? How?

Yes, Claude Code wrote the actual test code for both bugs. For the New Game test, it used Streamlit's AppTest tool to simulate losing a round and clicking New Game, then checked that the score, status, and history all reset correctly. I reviewed the test step by step to make sure I understood what it was actually checking before I accepted it.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
