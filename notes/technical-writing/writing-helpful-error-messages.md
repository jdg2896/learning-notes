# Writing Helpful Error Messages

[Course link](https://developers.google.com/tech-writing/error-messages)

Error messages should answer:

- What went wrong?
- How does the user fix that problem?

## Key Takeaways

- Identify the cause of the error.
  - If the user entered an invalid value, specify the invalid value.
  - Specify requirements and constraints, such as required permissions or minimum RAM.
- Explain how to fix the problem.
  - When appropriate, provide an example to help demonstrate the fix.
- Write clearly.
  - Be concise, not wordy. However, don't be so concise that the resulting error message becomes cryptic.
  - Avoid double negatives and exceptions to exceptions.
  - Aim the message at the appropriate target audience. Words appropriate for software engineers are often inappropriate for non-technical users.
  - Use terminology consistently. For example, don't use the term _directory_ in one part of an error message and _folder_ in another part.
  - Format long error messages carefully, possibly using progressive disclosure or links to expanded documentation.
  - Set a positive tone.
  - Don't be overly apologetic.

## General Error Handling Rules

- Don't fail silently
- Follow style guides
  - Google C++ Style Guide
  - Google Java Style Guide
  - Google Python Style Guide, particularly the Error Messages section
  - Google JavaScript Style Guide
- Implement the full error model
- Avoid swallowing the root cause
- Log the error codes
- Raise errors immediately

## Explain the Problem

- Identify the cause
- Identify the user's invalid inputs
- Specify requirements and constraints

## Explain the Solution

- Explain how to fix the problem
- Provide examples

## Write Clearly

- Be concise
- Avoid double negatives
- Write for the target audience
- Use terminology consistently
- Format error messages
  - Link to more detailed documentation
  - Use progressive disclosure
  - Place error messages close to the error
  - Handle font colors carefully
- Set the right tone
  - Be positive
  - Don't be overly apologetic
  - Avoid humor
  - Don't blame the user

## Additional Guidelines for Back-end Engineers

- Supply error codes
- Include an error identifier
