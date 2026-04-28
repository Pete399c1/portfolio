+++
date = '2026-04-16T23:33:47+02:00'
draft = false
title = 'Første oplevelse af KodeAgenter'
+++

## Kodeagenter -> Codex

Mit første indtryk af kodeagenter og brugen af dem i en arbejdsproces er, at det kan gøre udviklingen meget hurtigere. Når man ved, hvilke teknologier der skal bruges til at bygge en hjemmeside, kan man lave en prompt, som specificerer kravene til løsningen. Det kan være en stor fordel for mange virksomheder, da værktøjet ofte kan kode hurtigere end os.

Samtidig er det også lidt skræmmende, fordi jeg ikke selv havde brugt værktøjet før og heller ikke kendte særlig meget til det.

Kodeagenter kan gøre vores arbejde som programmører nemmere og mere simpelt. På den anden side er jeg også ret glad for selv at kode, så det er jeg lidt ærgerlig over, at der bliver mindre af.

## Prompts

Da jeg skulle lave en prompt til en meditation quiz-webside, gjorde jeg det med ChatGPT.

1. Hey Chat, kan du hjælpe mig med at lave en prompt til Codex? Jeg vil gerne gøre det specifikt, at jeg skal have lavet en webpage med JavaScript og React. Det skal være en meditation quiz, gerne i step-by-step-format. 

Svar 1:

Create a complete React + JavaScript single-page web app for a guided meditation quiz.

The app should feel calm, premium, and modern. The quiz must be step-by-step, showing one question at a time with a progress bar and smooth transitions. The purpose is to help the user discover which meditation style suits them best.

Build:
- A welcome screen
- 6–8 step-by-step quiz questions
- Multiple choice answer cards
- Back/Next navigation
- Progress indicator
- Final personalized result screen
- Restart quiz button

Meditation result categories:
- Mindfulness
- Breathwork
- Sleep meditation
- Body scan
- Loving-kindness
- Focus meditation

Each result should include:
- Result name
- Short personalized explanation
- Recommended duration
- Small practical tip

Use:
- React functional components
- Hooks for state management
- Clean reusable component structure
- Responsive layout
- High-quality UI styling
- Soft calming wellness aesthetic

Please output:
1. Full code
2. Component structure
3. CSS/styling
4. Example quiz data and scoring logic

Important:
Do not make it overly complex. Keep the code clean, maintainable, and easy to run.

2. Quizen skal have check bokse med flere forskellige svar tilføj også dette til prompten

Svar 2:
Build a modern, polished single-page meditation quiz web app using JavaScript and React.

Requirements:
- Use React with functional components and hooks.
- Build it as a single-page experience.
- The design should feel calm, soft, minimal, and wellness-focused.
- Use clean spacing, rounded cards, subtle shadows, and soothing typography.
- The app should be fully responsive for desktop and mobile.

Main concept:
Create a “Meditation Quiz” that guides the user step by step and recommends a meditation style at the end.

Flow:
1. Show a welcome screen with:
   - Title
   - Short calming intro text
   - A “Start Quiz” button

2. Present the quiz one question at a time in a step-by-step format.
   - Show progress indicator (example: Step 2 of 6)
   - Only one question visible at a time
   - Smooth transition between steps
   - Include Back and Next buttons
   - Disable Next until at least one answer is selected

3. IMPORTANT: Answer format
   - Each question should use checkboxes (multi-select)
   - Users must be able to select multiple answers per question
   - Visually display selected states clearly
   - Use card-style selectable options with checkbox indicators

4. Include around 6–8 questions such as:
   - How stressed do you feel today?
   - How much time do you have?
   - What do you want most right now? (focus, sleep, calm, energy, emotional balance)
   - Do you prefer silence, nature sounds, music, or guided voice?
   - Are you new to meditation?
   - When do you usually meditate? (morning, afternoon, evening, before sleep)

5. Logic:
   - Each answer can contribute to one or more meditation types
   - Because multiple answers can be selected, calculate a weighted score
   - Combine selected answers to determine the best matching meditation type

6. Meditation result types:
   - Mindfulness meditation
   - Breathing meditation
   - Sleep meditation
   - Body scan
   - Loving-kindness meditation
   - Focus meditation

7. Result page should include:
   - Personalized result title
   - Short explanation of why this meditation matches the user
   - Suggested session length
   - A calming tip
   - A “Retake Quiz” button

Technical expectations:
- Keep the code organized and readable.
- Store quiz questions in a structured data array.
- Store answers as arrays (since multiple selections are allowed).
- Manage quiz state cleanly with React hooks.
- Separate components where it makes sense:
  - WelcomeScreen
  - QuestionCard
  - CheckboxOption
  - ProgressBar
  - ResultScreen

- Implement logic for:
  - Selecting/deselecting answers
  - Handling multiple selections per question
  - Aggregating scores across all selected answers

Styling:
- Use a calming color palette such as soft green, beige, lavender, pale blue, or off-white.
- Avoid harsh colors.
- Selected answers should have a clear visual highlight (border, background, check icon).
- Add subtle hover effects and transitions.

Deliverables:
- Full React component code
- Any supporting CSS
- Clear structure so the app can run immediately
- Example quiz data including scoring logic for multiple selections

Extra:
- Add a progress bar at the top
- Add smooth transitions between questions
- Add a restart option
- Make the UI feel premium and modern