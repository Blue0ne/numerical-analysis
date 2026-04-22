### I don't think this is anything other than mere guidelines we (the publishers of this) agreed on to implement in this project so we're just documenting our thoughts so we can follow the same style of code while working.
> #### *So, in other words if you ever happen to come across this: Basically don't really mind this readme file unless you're thinking of contributing ツ*

---

## Project Overview

This project is a **Root Finding & Numerical Methods GUI application** built using Tkinter.  
It allows users to solve nonlinear equations using multiple numerical methods and visualize iteration results step-by-step.

Supported methods:
- Bisection Method
- False Position Method
- Newton-Raphson Method
- Secant Method
- Simple Fixed Point Method

---

## **Basic Guidelines**

### + Installing Dependencies

This project uses:

- `sympy` → symbolic math (derivatives, equation parsing)

Install dependencies using:

```bash
pip install sympy
```

Or if needed:

```bash
py -m pip install sympy
```

> If it didn't throw an error, you already have it installed → ignore this.

---

### + Global Variables Convention

The program heavily depends on shared global state:

- `new_eq`
- `i`
- `target_error`

So inside any function that uses them, always declare:

```python
global new_eq, i, target_error
```

This ensures consistency across all numerical methods.

---

### + Iteration Counter Reset

The variable `i` is shared across multiple methods.

Always reset it before starting a new computation:

```python
i = 0
```

Otherwise, iteration counts will carry over and break results.

---

### + Error Handling (VERY IMPORTANT)

Numerical methods may fail due to:

- division by zero
- bad initial guesses
- non-converging functions

Always handle safely using checks like:

```python
if abs(denominator) < 1e-12:
    return None
```

---

### + GUI Result Handling

All methods return a **list of strings**, which are displayed in the GUI:

```python
for line in result:
    result_text.insert(tk.END, line + "\n")
```

Final results can be highlighted using **tags (bold/color)** in the Text widget.

---

### + Input System Design

The GUI supports multiple input styles depending on method:

#### 📌 Function input:
- Equation entry (string)
- Error tolerance (%)

#### 📌 Interval-based methods:
- Bisection / False Position:
  - XL
  - XU

#### 📌 Single-point methods:
- Newton:
  - X0
- Fixed Point:
  - X0 + G(X)

#### 📌 Secant method:
- X0 (previous guess)
- X1 (current guess)

---

### + Functions Layout

Functions are separated into:

- Core utilities (parsing, validation, derivatives)
- Root-finding methods
- GUI wrappers (methods ending in `_gui`)

---

### + UI Behavior Rules

- Result box hides automatically when inputs change
- Method switching dynamically updates input fields
- Only relevant fields are shown per method
- “Calculate” triggers computation based on selected method

---

### + Styling Rules

- Output is displayed step-by-step (iteration logs)
- Final answer is highlighted (bold / colored text)
- Errors should be clearly shown instead of crashing the app

---

## Future Improvements (optional ideas)

- Add convergence graphs
- Add function plotting
- Add save/export results to file
- Add iteration speed control
