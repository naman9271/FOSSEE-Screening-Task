# Examples of AI Debugging Assistant in Action

This document provides practical examples of how the AI debugging assistant prompt would work in real scenarios with different types of student code and skill levels.

## Example 1: Beginner Student - Infinite Loop

### Student's Code:
```python
# Program to count from 1 to 10
count = 1
while count < 10:
    print(count)
```

### Student's Problem:
"My code is supposed to count from 1 to 10 but it just keeps printing 1 forever. I don't understand why it won't stop."

### AI Response (Following the Prompt):

Hi! I can see you're working on a counting program - that's a great way to practice loops! 

Let me ask a few questions to help us figure this out together:

1. Can you tell me what you expect this program to do step by step?
2. Right now, what's happening when you run it?

I notice something interesting about your while loop. Let's trace through it together:
- When the program starts, what value does `count` have?
- After the first time through the loop, what value should `count` have?
- Looking at your loop body, what happens to the `count` variable each time through?

Try adding a print statement to see what's happening to `count`. What do you think you might need to add inside your loop to make `count` change each time?

### Why This Response Works:
- Starts with encouragement
- Asks clarifying questions
- Guides through step-by-step thinking
- Hints at the solution without giving it away
- Suggests a debugging technique (print statements)

---

## Example 2: Intermediate Student - Type Error

### Student's Code:
```python
# Calculate average of user inputs
numbers = []
while True:
    user_input = input("Enter a number (or 'done' to finish): ")
    if user_input == 'done':
        break
    numbers.append(user_input)

if len(numbers) > 0:
    average = sum(numbers) / len(numbers)
    print(f"Average: {average}")
else:
    print("No numbers entered.")
```

### Student's Problem:
"I'm getting a TypeError when trying to calculate the average. The error says something about unsupported operand types for +: 'int' and 'str'. I don't understand because I'm only entering numbers."

### AI Response (Following the Prompt):

Great job on handling the empty list case and using a clean loop structure! The error message you're seeing is actually giving us a valuable clue.

Let's think about this step by step:

1. When you call `input()`, what type of data does it return? You can test this by adding `print(type(user_input))` right after the input line.

2. You mentioned you're "only entering numbers" - that's true from your perspective, but how does Python see what you're typing?

3. Look at the line `numbers.append(user_input)` - what type of data are you adding to your list?

4. Now think about the `sum()` function - it's trying to add these items together. What would happen if you tried to add the string "5" to the string "3" versus adding the number 5 to the number 3?

Try running your code with that print statement I mentioned and see what type `user_input` is. Once you figure that out, what do you think you might need to do before adding it to your list?

### Why This Response Works:
- Acknowledges what the student did well
- Uses the error message as a learning opportunity
- Asks leading questions about data types
- Suggests a specific debugging technique
- Builds understanding of the underlying concept

---

## Example 3: Advanced Student - Logic Error

### Student's Code:
```python
def find_prime_factors(n):
    """Find all prime factors of a number."""
    factors = []
    divisor = 2
    
    while divisor * divisor <= n:
        while n % divisor == 0:
            factors.append(divisor)
            n //= divisor
        divisor += 1
    
    if n > 1:
        factors.append(n)
    
    return factors

# Test
print(find_prime_factors(60))  # Expected: [2, 2, 3, 5]
print(find_prime_factors(17))  # Expected: [17]
```

### Student's Problem:
"My prime factorization function works for most numbers, but it's really slow for large numbers with small prime factors. For example, find_prime_factors(100000) takes forever. The algorithm seems correct, but the performance is terrible."

### AI Response (Following the Prompt):

Nice implementation! Your algorithm is mathematically correct, and I can see you're handling the edge cases well. The performance issue you're experiencing is a great observation.

Let's analyze the efficiency:

1. What's the current time complexity of your algorithm? Think about how many iterations your outer while loop performs for a number like 100000.

2. Consider the case where n = 100000 = 2^5 × 5^5. How many times does your divisor increment from 2 to sqrt(100000)?

3. After you've found all factors of 2, what values does divisor take on as it searches for the next prime factor (3)?

Here's a question to guide your optimization thinking: After you've completely factored out a prime (like 2), do you really need to check every even number as a potential divisor?

Try tracing through your algorithm with a number like 60 and count how many times you check each divisor value. What pattern do you notice in the divisors that actually divide n?

Also, consider: what mathematical property could you use to make the divisor increment more efficient after handling the factor of 2?

### Why This Response Works:
- Acknowledges the correct implementation
- Asks analytical questions about complexity
- Provides a specific example to work through
- Hints at optimization without giving the solution
- Encourages mathematical thinking about the problem

---

## Example 4: Beginner Student - Syntax Error

### Student's Code:
```python
name = input("What's your name? ")
age = input("What's your age? ")

if age >= 18
    print(f"Hello {name}, you are an adult!")
else:
    print(f"Hello {name}, you are a minor.")
```

### Student's Problem:
"I keep getting a SyntaxError on line 4. I don't see what's wrong!"

### AI Response (Following the Prompt):

Hi! Syntax errors can be tricky, but they're usually small things that are easy to fix once you spot them.

Let's look at line 4 together: `if age >= 18`

In Python, when you write an `if` statement, what punctuation mark should you put at the end of the line? Think about other `if` statements you've seen before.

Also, I notice you're comparing `age` (which comes from `input()`) with the number 18. We talked about data types in an earlier example - what type of data does `input()` give you? And what type is 18?

Try fixing the punctuation first and see what happens, then we can address the comparison if you run into another issue!

### Why This Response Works:
- Reassuring about syntax errors being common
- Directs attention to the specific line
- Asks a guiding question about Python syntax
- Mentions a potential follow-up issue without overwhelming
- Suggests fixing one thing at a time

---

## Example 5: Advanced Student - Design Problem

### Student's Code:
```python
class BankAccount:
    def __init__(self, balance=0):
        self.balance = balance
    
    def deposit(self, amount):
        self.balance += amount
        return self.balance
    
    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            return self.balance
        else:
            print("Insufficient funds")
            return self.balance

# Usage
account = BankAccount(100)
print(account.withdraw(150))  # Prints "Insufficient funds" and returns 100
```

### Student's Problem:
"My bank account class works, but I feel like the design could be better. The withdraw method seems to do too many things, and I'm not sure if printing messages is the right approach. How can I improve this?"

### AI Response (Following the Prompt):

Excellent question! You're thinking like a good software engineer by considering design principles and maintainability.

Let's think about the responsibilities and interface design:

1. **Single Responsibility Principle**: You mentioned that `withdraw` seems to do too many things. What are the different responsibilities you can identify in that method?

2. **Return Values vs. Side Effects**: Currently, `withdraw` both prints messages and returns values. What problems might this cause if someone wants to use your class in different contexts (web app, mobile app, etc.)?

3. **Error Handling**: How do you think users of your class should know when an operation fails? Consider the difference between expected failures (like insufficient funds) vs. unexpected errors.

4. **Consistency**: Compare your `deposit` and `withdraw` methods. Do they handle success and failure in similar ways?

Some questions to guide your redesign:
- Should the class be responsible for user communication, or just for managing account state?
- How could you indicate success/failure in a way that gives the caller flexibility in how to respond?
- What happens if someone tries to deposit a negative amount?

Try sketching out what you think the interface should look like before implementing. What would make this class easy and intuitive for other developers to use?

### Why This Response Works:
- Validates the student's design thinking
- Introduces relevant design principles
- Asks analytical questions about responsibilities
- Compares different approaches without prescribing solutions
- Encourages systematic design thinking

---

## Key Patterns in These Examples

### Common Elements Across All Responses:
1. **Positive opening** - Acknowledging something done well
2. **Clarifying questions** - Understanding the student's perspective
3. **Guided discovery** - Leading them to insights
4. **Specific debugging suggestions** - Actionable next steps
5. **Educational focus** - Building understanding, not just fixing code

### Adaptation for Different Levels:
- **Beginners**: More encouragement, simpler language, step-by-step guidance
- **Intermediate**: Focus on concepts and common patterns
- **Advanced**: Design principles, efficiency, and best practices

### Debugging Techniques Demonstrated:
- Adding print statements for visibility
- Tracing through code execution
- Understanding error messages
- Testing with simple inputs
- Analyzing time complexity
- Considering edge cases

These examples show how the prompt successfully guides students toward solutions while building their debugging skills and programming understanding.