# Instructor Reference: Session 3.1 — Colab, Variables and Condition Logic

[Duration: 90 min teaching (5 segments) + 10 min Common Mistakes + 2×5-min breaks + 10 min final recap block = 120 min total | Domain: Coding | Tools: Google Colab | Prior: AI for Documents and Research (2.2) | Next: Loops and Tracing What Runs (3.2) | Visual load: Medium]

> **Note for the Industry Mentor — Tracked Learning Objectives for This Session:**
> This session is formally tracked against the following LO Statements from the curriculum LO bank. Please ensure each one gets substantive, identifiable coverage during delivery — a student should be able to point to the specific moment each was taught:
> - **CLI-037:** Write and run code in a notebook cell, separating code cells from markdown cells
> - **PY-001:** Write a script that stores values in named variables following Python naming conventions
> - **PY-002:** Classify a value as int, float, str or bool
> - **PY-003:** Convert a value between string, integer and float types
> - **PY-005:** Compute a result using arithmetic operators, including integer division and modulo
> - **PY-007:** Construct a boolean expression using comparison and logical operators
> - **PY-011:** Implement branching logic for a stated business rule using if/elif/else

**Goal:** Take a student from zero code written to confidently running a Colab notebook that stores values, computes with them, and branches on a stated business rule.

**Student profile:** A learner who has only ever prompted AI tools in plain English up to this point, and has never written or run a line of Python.

**Key outcome:** By the end, a student can run a code cell, store values in correctly named variables, identify and convert between data types, compute with arithmetic/comparison/logical operators, and implement an if/elif/else rule for a real business scenario.

---

## SEGMENT 1 — Running Your First Colab Cell: Code vs. Markdown `(18 min)`

> Instructor note: Last session (2.2) was the last purely conversational session with AI tools. Today is the first time a student writes and runs their own code.

**Hook-in** `(30 sec)`
Every tool you've used in this course so far has been a text box you type a prompt into. What's different about a notebook where you write actual code?

**Concept** `(3–5 min)`
A lab notebook has two kinds of entries: the experiment steps you actually run, and the notes explaining why you ran them — mixing the two together makes the notebook hard to follow later. **A Google Colab notebook is built from cells, and every cell is either a code cell, which Python actually executes when you run it, or a markdown cell, which renders formatted text and is never executed.** This matters because treating the two interchangeably — writing explanation as an unstructured code comment, or expecting a markdown cell to run — is the single most common first-day confusion.

**Visual** `(visual only, no extra time)`
```
[ CODE CELL ]                 [ MARKDOWN CELL ]
print("Hello, Colab!")        # My Notes
                               This explains what the
-> runs, shows output          cell below it does.
   directly underneath        -> renders as formatted
                                  text; nothing executes
```
> **Say while pointing:** "Press Shift+Enter on the left cell and Python runs it top to bottom. Press it on the right and nothing executes — it just displays."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor creates a code cell with `print("Hello, Colab!")`, runs it with Shift+Enter, then creates a markdown cell with a heading and explanatory text, runs that too, and compares what appears on screen for each.

Expected:
```
>>> print("Hello, Colab!")
Hello, Colab!
```
(the markdown cell shows formatted text with no output line, since nothing is executed)

**Key point**
**A code cell executes and can produce output; a markdown cell only displays formatted text — confusing the two is the fastest way to lose track of what a notebook actually does.**

**Room check** `(30 sec)`
> **Ask:** "You want to leave a note in your notebook explaining why the next three cells exist, without it being treated as code. What kind of cell do you use?"
> **Answer:** A markdown cell — it displays the explanation as formatted text and is never executed, unlike a code comment buried inside a code cell.

**Student try** `(2–3 min)`
Create one markdown cell with a one-line title describing today's notebook, then create one code cell below it that prints your own name.

Success: Running the code cell prints the student's name as output; the markdown cell renders as formatted text with no output line.

---

## SEGMENT 2 — Variables and Data Types: Naming, Storing, and Classifying Values `(18 min)`

**Hook-in** `(30 sec)`
You can already run a line of code. How do you make Python remember a value so you can use it again two cells later?

**Concept** `(3–5 min)`
A labelled storage box lets you find the right item again later without re-describing it every time; an unlabelled pile does not. **A variable is a name you choose that points to a value, and Python automatically assigns that value one of four everyday data types — str (text), int (a whole number), float (a decimal number), or bool (True/False) — based on what was assigned.** This matters because every later segment, and every later session in this course, depends on values being stored in clearly named variables of the correct type.

**Visual** `(visual only, no extra time)`
```
student_name = "Aisha"     ->  str   (text, in quotes)
course_fee   = 45000        ->  int   (whole number)
attendance   = 92.5         ->  float (decimal number)
is_enrolled  = True          ->  bool  (True / False)
```
> **Say while pointing:** "Python decided each type automatically from the value on the right — nobody declared 'this is a string' anywhere."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor assigns a student name, city, course fee, and scholarship status to four variables, prints all four, then prints `type()` of three of them to confirm Python's automatic classification.

```python
student_name = "Aisha"
student_city = "Delhi"
course_fee = 45000
is_scholarship = False
print(student_name, student_city, course_fee, is_scholarship)
print(type(student_name), type(course_fee), type(is_scholarship))
```

Expected:
```
Aisha Delhi 45000 False
<class 'str'> <class 'int'> <class 'bool'>
```

**Key point**
**A variable's name should describe what it holds — `student_city` tells the next reader exactly what's inside; `x` or `temp1` costs them real time figuring it out.**

**Room check** `(30 sec)`
> **Ask:** "You assign `is_passing = True`. What data type did Python just give `is_passing`, and how do you know without running `type()`?"
> **Answer:** `bool` — because the value assigned is exactly `True` or `False`, which Python always classifies as a boolean regardless of context.

**Student try** `(2–3 min)`
Store your own age in one variable and whether you are currently a student in another, printing the `type()` of each.

Success: Two variables are created with clearly descriptive names, and printing `type()` of each correctly shows `int` and `bool`.

---

## Break 1 `(5 min)`

Re-entry hook: "You can now run a cell and store values in clearly named, correctly typed variables. Next: what happens when a value arrives in the wrong type, and how do arithmetic and comparisons actually compute with it?"

---

## SEGMENT 3 — Type Conversion: Moving Between String, Int and Float `(18 min)`

**Hook-in** `(30 sec)`
A value sometimes arrives in the wrong type for what you need — a form answer comes in as text even when it's really a number. How do you fix that?

**Concept** `(3–5 min)`
A price tag written in words ("four ninety-nine") can't be added up the way the number 499 can, even though a person reads both the same way. **Type conversion means explicitly changing a value from one data type to another — most commonly `int()`, `float()`, and `str()` — and Python will not silently do this for you in arithmetic.** This matters because a value that looks like a number but is stored as `str` will cause an error, or silently misbehave, the moment you try to compute with it.

**Visual** `(visual only, no extra time)`
```
marks_text   = "87"            (str)
marks_number = int(marks_text)  -> 87      (now str -> int)
gpa          = 8.75             (float)
gpa_text     = str(gpa)         -> "8.75"  (now float -> str)
rounded_gpa  = int(gpa)          -> 8       (float -> int: TRUNCATES)
```
> **Say while pointing:** "`int(gpa)` doesn't round 8.75 to 9 — it just chops off everything after the decimal point."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor converts a text score to an integer, a float GPA to a string, and the same GPA to an integer, printing all three results.

```python
marks_text = "87"
marks_number = int(marks_text)
gpa = 8.75
gpa_text = str(gpa)
rounded_gpa = int(gpa)
print(marks_number, gpa_text, rounded_gpa)
print(int(8.99))
```

Expected:
```
87 8.75 8
8
```

**Key point**
**Converting a `float` to an `int` truncates rather than rounds — `int(8.99)` gives `8`, not `9`, because the decimal part is simply dropped.**

**Room check** `(30 sec)`
> **Ask:** "A form field gives you `"25"` as text and you need to add 5 to it. What has to happen before the addition will work?"
> **Answer:** Convert it first with `int("25")` to get the whole number `25` — adding 5 directly to the text `"25"` raises an error rather than computing `30`.

**Student try** `(2–3 min)`
Convert the text `"4.5"` into a float, store it in a variable, and print both the value and its `type()`.

Success: `float("4.5")` is used, the printed value is `4.5`, and `type()` correctly shows `<class 'float'>`.

---

## SEGMENT 4 — Arithmetic, Comparison and Logical Operators `(18 min)`

**Hook-in** `(30 sec)`
You can now store and convert values. How do you actually compute with them, and get a yes/no answer out of a condition?

**Concept** `(3–5 min)`
Splitting a restaurant bill among friends needs more than one kind of division — how much each person owes exactly, how many whole currency notes that covers, and what's left over as change. **Arithmetic operators (`+ - * / // %`) compute with numeric values — `/` always gives a float, `//` gives the whole-number (floor) result, and `%` gives the remainder — while comparison operators (`== != > < >= <=`) and logical operators (`and`, `or`, `not`) combine values into a single `True`/`False` result.** This matters because almost every later business rule in this course is built from exactly this combination: a computed number, compared against a threshold, combined with another condition.

**Visual** `(visual only, no extra time)`
```
cart_total = 3400, num_items = 6

cart_total / num_items    -> 566.666...   (true division, float)
cart_total // num_items   -> 566          (floor division, whole part)
cart_total % num_items    -> 4            (remainder)

(cart_total >= 1000) and is_prime_member  -> True / False
```
> **Say while pointing:** "`/` and `//` answer two different questions — 'exactly how much' versus 'how many whole ones' — and `%` tells you what's left over from the second question."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor computes true division, floor division, and remainder on a cart total split across items, then builds a boolean expression combining a numeric comparison with a membership flag.

```python
cart_total = 3400
num_items = 6
print(cart_total / num_items)
print(cart_total // num_items)
print(cart_total % num_items)
is_prime_member = True
qualifies_free_delivery = (cart_total >= 1000) and is_prime_member
print(qualifies_free_delivery)
```

Expected:
```
566.6666666666666
566
4
True
```

**Key point**
**`=` assigns a value to a variable; `==` checks whether two values are equal — mixing the two up is one of the most frequent early Python mistakes.**

**Room check** `(30 sec)`
> **Ask:** "A cart qualifies for free delivery only if the total is at least ₹1000 AND the customer is a Prime member. The total is ₹1200 but the customer is not a Prime member. Does it qualify?"
> **Answer:** No — `and` requires both sides to be true; the total condition is true but the membership condition is false, so the combined expression is `False`.

**Student try** `(2–3 min)`
Store a bank balance and a minimum-balance requirement in two variables, then write a single boolean expression that checks whether the balance meets or exceeds the minimum.

Success: A comparison expression using `>=` correctly evaluates to `True` or `False` based on the two stored values.

---

## Break 2 `(5 min)`

Re-entry hook: "You can now store values, convert them, and turn a condition into True or False. The rest of today is about using that True/False to actually make the program behave differently."

---

## SEGMENT 5 — If/Elif/Else: Branching Logic for a Business Rule `(18 min)`

**Hook-in** `(30 sec)`
A `bool` value tells you True or False — but how does the program actually do something different depending on which one it is?

**Concept** `(3–5 min)`
A pharmacy's heat-advisory signage doesn't show every possible message at once — it checks the day's temperature against a set of bands and displays exactly one. **Python's `if`, `elif`, and `else` check conditions from top to bottom and execute the first branch whose condition is `True`, skipping every branch after it, even if a later condition would also have been true.** This matters because real business rules — a grading band, a shipping fee, a discount tier — are almost always expressed as exactly this shape: several conditions, apply only the first one that matches.

**Visual** `(visual only, no extra time)`
```
temperature = 38

if temperature >= 40:      -> False, skip
elif temperature >= 35:    -> True, STOP HERE
elif temperature >= 20:    -> never checked
else:                      -> never checked
```
> **Say while pointing:** "Python stops at the first True condition — the two branches below it are never even evaluated once a match is found."

**Implementation / Demonstration** `(5–10 min)`
Live demo: the instructor writes a four-band heat-advisory rule and traces it by hand for a specific temperature before running it, confirming the branch Python actually takes.

```python
temperature = 38
if temperature >= 40:
    alert = "Severe Heat Warning"
elif temperature >= 35:
    alert = "Heat Advisory"
elif temperature >= 20:
    alert = "Normal"
else:
    alert = "Cold Advisory"
print(alert)
```

Expected:
```
Heat Advisory
```

**Key point**
**Order your `elif` conditions from most specific (or highest threshold) to least specific — once Python finds a match it stops checking, so a looser condition placed too early silently catches cases meant for a stricter one below it.**

**Room check** `(30 sec)`
> **Ask:** "If the `temperature >= 20` branch were written first in this example, before the `>= 40` and `>= 35` branches, what would `alert` incorrectly become for a temperature of 42?"
> **Answer:** `"Normal"` — Python would stop at the first matching condition (`42 >= 20` is True) and never reach the `>= 40` branch that should have matched instead.

**Student try** `(2–3 min)`
Write an if/else rule: a student is "Eligible" for an exam if their attendance is 75% or higher, otherwise "Not Eligible." Test it with an attendance value of 68.

Success: The code correctly prints `"Not Eligible"` for an attendance value of 68, using a single `if`/`else` (no `elif` needed for just two outcomes).

---

## SEGMENT 6 — Common Mistakes `(10 min)`

### Mistake 1: Writing Explanation as a Code Comment Instead of a Markdown Cell

**Wrong:**
Burying a paragraph of reasoning inside `#` comments at the top of a code cell instead of using a separate markdown cell.

**Right:**
Use a markdown cell for explanation and keep the code cell focused on code that actually runs (Segment 1).

**Why it matters:**
A notebook that mixes the two becomes much harder for anyone — including the author, later — to scan and understand.

---

### Mistake 2: Using a Vague Variable Name

**Wrong:**
`x = 45000` with no indication anywhere of what `x` actually represents.

**Right:**
`course_fee = 45000` — the name alone tells the next reader what the value is (Segment 2).

**Why it matters:**
Vague names cost real debugging time later, especially once a notebook has dozens of variables in play.

---

### Mistake 3: Assuming `int()` Rounds Instead of Truncates

**Wrong:**
Writing `int(8.99)` and expecting `9`.

**Right:**
Know that `int()` always truncates toward zero — use `round()` instead when actual rounding is needed (Segment 3).

**Why it matters:**
A silent truncation can shift a calculated grade, fee, or score down by a full point without raising any error.

---

### Mistake 4: Confusing `=` and `==`

**Wrong:**
Writing `if balance = 1000:` when checking equality.

**Right:**
Use `=` only to assign a value, and `==` only to compare two values for equality (Segment 4).

**Why it matters:**
This single-character mix-up is one of the most common sources of early Python errors and confusing bugs.

---

### Mistake 5: Ordering `elif` Conditions From Loosest to Strictest

**Wrong:**
Checking a broad condition (`score >= 60`) before a narrower one (`score >= 90`), so a 95 incorrectly matches the broad band first.

**Right:**
Order conditions from the highest threshold down to the lowest, so the most specific match is checked first (Segment 5).

**Why it matters:**
Python stops at the first `True` condition — a misordered chain silently produces the wrong branch with no error raised.

---

## SEGMENT 7 — Session Recap

| Learning Outcome | What to Remember |
|---|---|
| Write and run code in a notebook cell, separating code cells from markdown cells | A code cell executes; a markdown cell only displays formatted text — never mix the two jobs |
| Write a script that stores values in named variables following Python naming conventions | A variable's name should describe what it holds — `student_city`, not `x` |
| Classify a value as int, float, str or bool | Python assigns the type automatically from the value — check with `type()` when unsure |
| Convert a value between string, integer and float types | `int()`, `float()`, and `str()` convert explicitly — `int()` truncates, it does not round |
| Compute a result using arithmetic operators, including integer division and modulo | `/` gives a float, `//` gives the whole part, `%` gives the remainder |
| Construct a boolean expression using comparison and logical operators | `=` assigns, `==` compares — and `and` needs both sides true, `or` needs just one |
| Implement branching logic for a stated business rule using if/elif/else | Python stops at the first `True` branch — order conditions from most to least specific |

**Path forward:**
Next session is **Loops and Tracing What Runs (3.2)** — it builds directly on today's variables and conditions, repeating the same kind of logic across many values instead of writing it out one value at a time.

---

## Knowledge Check

Six scenario-based and implementation questions covering Colab cells, variables, types, conversion, operators, and branching logic — use these as a closing quiz, a cold-call set, or a take-home check.

**1.** A student writes a long paragraph explaining their approach as a `#` comment at the very top of a code cell, then writes their actual code below it in the same cell. What would you suggest they change, and why?

> **Answer:** Move the explanation into a separate markdown cell above the code cell. A code cell is meant to execute; burying a long explanation inside it as a comment makes both the explanation and the code harder to scan, and markdown cells exist specifically for this job.

**2.** Given `exam_score = "88"`, what is the data type of `exam_score` right now, and what single line of code would you write to make it usable in arithmetic?

> **Answer:** It's a `str` (text), even though it looks like a number, because it's written in quotes. `exam_score = int(exam_score)` (or `int("88")`) converts it to an `int` so it can be used in calculations.

**3.** What does `print(int(19.9))` output, and why does it surprise students who expect rounding?

> **Answer:** It outputs `19`. `int()` always truncates toward zero rather than rounding to the nearest whole number, so the `.9` is simply dropped — it does not become `20`.

**4.** A cart total is ₹850 and a customer is a Prime member. The free-delivery rule is: total of at least ₹1000 **and** Prime membership. Write the boolean expression for this check and state what it evaluates to.

> **Answer:** `(cart_total >= 1000) and is_prime_member` evaluates to `False` here — even though the customer is a Prime member, the total (₹850) does not meet the ₹1000 threshold, and `and` requires both conditions to be true.

**5.** A grading rule is written as: `if score >= 60: grade = "C"`, followed by `elif score >= 90: grade = "A"`, followed by `elif score >= 75: grade = "B"`. For a score of 95, what grade does this code actually assign, and what's gone wrong?

> **Answer:** It assigns `"C"`. Python checks conditions top to bottom and stops at the first `True` one — since `95 >= 60` is checked first and is true, the program never reaches the `>= 90` or `>= 75` branches. The conditions need to be reordered from highest threshold to lowest.

**6.** A teammate writes `if balance = 500:` to check whether a balance equals 500, and the code fails to run. What's the specific error, and how should the line be written instead?

> **Answer:** `=` is the assignment operator, not a comparison — Python is trying to assign `500` to `balance` inside an `if` statement, which is invalid syntax. The line should use `==` instead: `if balance == 500:`.

**7.** A shipping rule should charge ₹0 for orders of ₹999 or more, ₹49 for orders from ₹500 up to ₹998, and ₹99 for anything below ₹500. A student writes the bands in this order: `order_total >= 500`, then `order_total >= 999`, then `else`. For an order of ₹1200, what fee does this code compute, and why is it wrong?

> **Answer:** It computes ₹49 (the "from ₹500" branch), because `1200 >= 500` is checked first and is already true, so Python never reaches the `>= 999` branch where this order actually belongs. The bands need to be reordered starting from the highest threshold (`>= 999`) down to the lowest.
