# Answers - finPOWER Assessment

## Part 1 - Basic Scripting Concepts

### Snippet 1: `Dim accountStatus As String`

**1. What does `Dim accountStatus As String` mean?**\
It declares a variable named `accountStatus` and specifies that it can only hold string data. `Dim` allocates the variable, and `As String` specifies to the compiler its data type upfront so that any value assigned to it later must be a string and catch anything that is not text.

**2. What type of data can be stored in a String?**\
Text is the only value that can be stored as a String.

**3. Why do you think systems like finPOWER use strongly typed variables (e.g. As
String, As Integer)?**\
It's simply to enforce strict boundaries on these types of variables, preventing unexpected errors and making code safer and easier to maintain.

### Snippet 2: `LoadAccount` function

**1. In your own words, what is this script doing?**\
Creates a function called `LoadAccount` that takes in a integer parameter called `AccountPk`. This function declares two variables `balance` as a decimal and `status` as a string. `balance` calls a separate function `GetAccountBalance()` this returns the balance of the account associated to the accounts primary key integer `AccountPk` similarly `status` also calls a separate function `GetAccountStatus()` that returns the status of the associated account `AccountPk`. If the status of the account is `"Closed"` it exits the function and doesn't load the account associated with `AccountPk`. If the status is `"Open"`,  or another return value similar, it fails the exit function conditional and creates a new account log that details the balance of the associated `AccountPk` account.

**2. What happens if the account status is "Closed"?**\
It simply exits the function `LoadAccount()` and doesn't create a new balance log for the account.

**3. Why is logging important in systems like this?**\
It's important because it creates a chronological, time-stamped digital record of events, errors, and other user activities that enables easier troubleshooting and security analysis. Without logging, system admins and developers would be operating blindfolded when issues occured.

---

## Part 2 - Database Thinking

**1. What does `INNER JOIN` do?**\
`INNER JOIN` combines rows from two or more tables by matching the values that are in a shared column, in this case, the `AccountPk` that they both share.

**2. Why does the Workflow table store `AccountPk`?**\
So that the associated unique `AccountPk` can be linked to one or more workflows enabling joins.

**3. What would happen if an account had no workflow record - would it appear in
this query?**\
No rows would be returned because there are no corresponding entries in the `Workflow` table for the join condition to return true and therefore no accounts would be returned.

---

## Part 3 - AI Awareness

**1. What AI tools have you used for coding, problem-solving, or learning?**
My main AI tool that I use is Claude as I've found it to perform the best in the tasks that I use it for whether it be coding related or some other use case in a given day. Although I have used other tools such as ChatGPT, Google Gemini and Copilot when I have run out of free tokens with Claude.

**2. Give an example of a prompt you might ask an AI tool to help explain or write a piece of finPOWER logic.**
>You are an expert developer in finPOWER that has deep knowledge of its syntax and how it works. Explain the following finPOWER logic: [insert code sample]

---

## AI Test 1 - Safe Tool + Safe Prompt

**1. Which AI tool would you choose for this task, and why?**\
My first instinct is to go straight to Claude, however since the crux of this task is to create a draft email and suggest script changes in finPOWER, I would go with the tool that has the most accurate and performant result while also not including any hallucinations for these two tasks. Which is why I would still go with Claude because it satisfies these requirements majority of the time.

**2. Rewrite the prompt so it is safe and still useful, removing or generalising
anything sensitive.**
> Write a draft email for a arrears notice that involves sensitive customer information (AccountNumber, customer name, address and balance) and then suggest any script changes to the finPOWER script that prevents this issue from occurring again.

**3. What is the one key risk if someone pasted this into a public AI tool?**\
The key risk is for the sensitive customer data being permanetly exposed to the public as many AI platforms use the data from prompts to train their models leading to the sensitive data becoming accessible to others.

---

## AI Test 2 - Spot the Risk / Hallucination

**1. Identify two problems with this advice (think: safety, auditability, correctness).**
- Bypasses the business logic of already existing (assuming) update queries. Using a direct `UPDATE` query on a financial systems tables would bypass any built-in logic, triggers and any audit logs that are present.
- In terms of correctness there is no guarantee that the UI updates safely or immediately to the change of data this would also cause misalignments to any other linked data to these changes which would cause errors.

**2. List two ways you would verify the correct approach before implementing
anything in production.**
- Refer to documentation on existing business/application logic.
- Test in a non-production environment using non-production data such as a dev or UAT environment to verify changes and any ripple effects from the changes.

---

## AI Test 3 - Write a Good finPOWER Prompt

**Prompt:**
> You are an expert in finPOWER with deep knowledge of it's syntax and how it's system works. You are required to write a script that loads an account using AccountPk that reads the balance and status of that account associated with AccountPk. Then create a log entry only if the account's status is not CLOSED if it is CLOSED do nothing, otherwise continue with the log.