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
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
