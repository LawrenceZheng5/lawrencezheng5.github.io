---
layout: essay
type: essay
title: "Ask Michael or Manuel"
# All dates must be YYYY-MM-DD format!
date: 2025-09-09
published: true
labels:
  - Stack Overflow
  - Smart Questions
  - Smart Answers

---

<figure class="figure float-start pe-4">
  <img src="../img/smart-questions/michael.jpg" 
       class="figure-img img-fluid rounded" 
       width="300px" 
       alt="Michael Bublé for reference">
  <figcaption class="figure-caption text-center">
    Michael Bublé for reference
  </figcaption>
</figure>
The following text is based off reading this [article](http://www.catb.org/esr/faqs/smart-questions.html#intro) on how to ask questions the smart way.

## Personal Experience with "Stupid" and Bad Questions
I've had my fair share of "stupid" questions that lacked context and information, which I directed to my old boss. In the early days of working at the job, I was quickly acclimated to the mindset that "hackers" hold, as described in the article. My questions were often swiftly answered with "Ask *Michael Googlay*" (usually shortened to "Ask *Michael*") or "Ask *Manuel*." Naively, I asked who those people were and was promptly informed that *Michael Googlay* was a play on the singer Michael Bublé, while also referencing "stfw." Learning who *Manuel* was proved more straightforward as it was a reference to "rtfm." Over time, I would start to ask a question and then remember the answer myself before comments of "Ask *Michael*" or "Ask *Manuel*" could ensue.  

Asking good, smart questions is especially important for smart software engineers who seek clarification and solutions for deeply technical or niche problems. By following the guidelines outlined in the article, software engineers can ask questions that are more likely to receive meaningful answers. In addition, phrasing questions in a smart way makes it less likely that one will be publicly shamed on a forum. The following are examples from Stack Overflow of questions asked in a "smart way" and a "not-so-smart way."  


## The Smart Way
[How to fill missing values in a DataFrame with the most frequent value of each group?](https://stackoverflow.com/questions/68849100/how-to-fill-missing-values-in-a-dataframe-with-the-most-frequent-value-of-each-g)

The question is in essence asking for a way to fill in missing data in a panda's dataframe with the most common value for that item. For example, replacing the color for row 3 with "blue" as blue is the most common color for a car.

**Sample Dataset:**
```
      toy  color 
0     car    red 
1     car   blue 
2     car   blue 
3     car    NaN 
4   train  green 
5   train    NaN 
6   train    red 
7   train    red 
8   train    NaN 
9    ball   blue 
10   ball    red 
11   ball    NaN 
12  truck  green 
```
**Code to generate sample dataset:**
```python
import pandas as pd
import numpy as np
df = pd.DataFrame({
    'toy':['car'] * 4 + ['train'] * 5 + ['ball'] * 3 + ['truck'],
    'color':['red', 'blue', 'blue', np.nan, 'green', np.nan,
             'red', 'red', np.nan, 'blue', 'red', np.nan, 'green']
    })
```
The question is very precise and clear about what the original poster (OP) wants to do because they provide an example that is easy to understand. OP also demonstrates that they have researched and searched for similar problems on various forums by linking to another related Stack Overflow question. This shows that OP put effort into solving the problem before posting. Additionally, the way the question is structured allows for concise and efficient answers, making it easier for others with the same issue to learn from it. As a result, another user provides two elegant one-line solutions to this question:
```
df['color']=df['color'].fillna(df.groupby('toy')['color'].transform(lambda x:x.mode().iat[0]))
```
Technically a two line solution if OP wants to pick a random value between two of the most frequent values.
```
from random import choice

df['color']=df['color'].fillna(df.groupby('toy')['color'].transform(lambda x:choice(x.mode())))
```
The solutions provided are straight and to the point because the commenter knew exactly what OP was asking for. 

## The Not-so-Smart Way
[print statement won't print value of my variable](https://stackoverflow.com/questions/56306079/print-statement-wont-print-value-of-my-variable)

The OP provides this code block and is confused as to why the final `print(change)` does not print what they are expecting. The OP writes that no matter what complier they use there is no error code that is raised and the print statement does not print anything to the screen.
```python
import math

luck = 54
justice = 0
compassion = 1
bravery = 1
truth = 2
coreType = "Legendary"
baseChance = 0.01
element = "Light"

import math
valid = True
if coreType == "Common":
    coreRarity = 1
elif coreType == "Rare":
    coreRarity = 1.5
elif coreType == "Legendary":
    coreRarity = 3
else:
    print("Invalid core type")
    valid = False

if justice > compassion and justice > truth and justice > bravery:
    idea = "justice"
elif compassion > justice and compassion > truth and compassion > bravery:
    idea = "compassion"
elif truth > compassion and truth > justice and truth > bravery:
    idea = truth
elif bravery > compassion and bravery > truth and bravery > justice:
    idea = "bravery"
else:
    idea = "all"

if idea == "justice" and (element == "Light" or element == "Shadow"):
    boost = justice
elif idea == "truth" and (element == "Ice" or element == "Wind"):
    boost = truth
elif idea == "compassion" and (element == "Earth" or element == "Lightning"):
    boost = compassion
elif idea == "bravery" and (element == "Fire" or element == "Water"):
    boost = bravery
elif idea == "all":
    boost = bravery #basicly the above determines what the highest idea is and sets it but if the highest is all it means they are all the same so It doesn't matter one one the boost's value is cause its all the same

if valid == True:
    chance = math.max(math.sqrt(luck*0.01*1.3)+0.95,1)*0.01*(0.01*(100+5*idea)*coreRarity*baseChance)
    if coreType == "common":
        chance =* 0.25
    print(chance)
```
Clearly, there are ways to improve how this question was asked. Essentially, OP posted around 50 lines of code and stated that it isn't working. This could be fixed by only  adding relevant parts of the code instead of attaching their entire program. Only attaching the code in the final nested if-statement would bring down the time users waste on reading through their entire program. OP also does not show any signs of previous troubleshooting or effort in solving the problem other than stating that he has the same effect when using different compilers. They must have a fundamental misunderstanding of python because python is an interpreted language and not a compiled one. 

In spite of these pitfalls, a user manages to fix OP's code by using the following fixes:

    - chance =* 0.25 should be chance *= 0.25 (here is a list of all assignment operators)
    - the module math doesn't have a max attribute, so I would recommend you trying max() instead of math.max()

```python
if valid == True:
    chance = max(math.sqrt(luck*0.01*1.3)+0.95,1)*0.01*(0.01*(100+5*idea)*coreRarity*baseChance)
    if coreType == "common":
        chance *= 0.25
    print(chance)
```

In the end, the problem does not lie with the "compiler" that OP uses and rather some minor syntax errors that python did not raise errors for.

## Final Insights
This experience of reading through the article and searching for smart and not-so-smart questions has further reinforced the importance of asking questions the smart way. This is a skill that will be crucial to the toolkit of any software engineer. Looking through some real-world examples shows that it can be harder to phrase questions in a smart way as complexity grows. However, practicing how to ask questions the smart way by showing prior effort, including reproducible examples, and stating the problem precisely will build communication skills. Over time, this habit not only leads to faster and more useful answers but also demonstrates respect for the time of others in the community.
  
  <br>
Grammar and proof reading done with ChatGPT
