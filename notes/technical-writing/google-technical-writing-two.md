# Google Technical Writing Two

[Course link](https://developers.google.com/tech-writing/two)

## Key Takeaways

- Adopt a style guide.
- Think like your audience.
- Read documents out loud (to yourself).
- Return to documents well after you've written the draft.
- Find a good peer editor.
- Outline a document. Alternatively, write free form and then organize.
- Introduce a document's scope and any prerequisites.
- Prefer task-based headings.
- Disclose information progressively (in some situations).
- Consider writing the caption _before_ creating the illustration.
- Constrain the amount of information in a single drawing.
- Focus the reader's attention on the relevant part of a picture or diagram by describing the takeaway in the caption or by adding a visual cue to the picture.
- Create concise sample code that is easy to understand.
- Keep code comments short, but prefer clarity over brevity.
- Avoid writing comments about _obvious_ code.
- Focus your commenting energy on anything non-intuitive in the code.
- Provide not only examples but also anti-examples.
- Provide code samples that demonstrate a range of complexity.
- Make a practice of continuous revision.
- Provide different documentation types for different categories of users.
- Compare and contrast with something that readers are already familiar with.
- In tutorials, reinforce concepts with examples.
- In tutorials, note problems that readers may encounter.

## Self-editing

- Adopt a style guide
  - https://developers.google.com/style
- Think like your audience
- Read it out loud
- Come back to it later
- Change the context
- Find a peer editor

## Organizing Large Documents

- Organize a document
  - Create an outline
- Introduce a document
  - What the document covers
  - What prior knowledge you expect readers to have
  - What the document doesn't cover
- Add navigation
- Prefer task-based headings
- Provide text under each heading
- Disclose information progressively

## Illustrating

- Write the caption first
  - brief, explains the takeaway, and focuses the reader's attention
- Constrain the amount of information in a single drawing
  - Complex diagrams overwhelm readers
  - Instead, display the high level first, then the sub-systems
- Focus the reader's attention
  - add visual cues
    - red box/oval
    - arrows
- Illustrating is re-illustrating
- Illustration tools
  - Google Drawings
  - diagrams.net
  - LucidChart
  - Export as SVG

## Creating Sample Code

### Correct

- Builds without errors
- Performs the task it claims to perform
- Is as production-ready as possible
- Follows language-specific conventions

### Running Sample Code

- Install libraries
- Adjust environment variables
- Adjust something in the IDE

### Understandable

- Pick descriptive class, method, and variable names
- Avoid confusing your readers with hard-to-decipher programming tricks
- Avoid deeply nested code
- Optional: Use bold or colored font to draw the reader's attention to a specific section of sample code

### Commented

- Keep comments short, but always prefer clarity over brevity
- Avoid writing comments about obvious code (but remember the "curse of knowledge")
- Focus your commenting energy on anything non-intuitive in the code
- Explain _why_ the code is doing it

### Reusable

- All information needed to run the sample code, including dependencies and setup
- Code that can be extended or customized in useful ways

### Other Qualities

- Concise
- Example and anti-example
- Sequenced
