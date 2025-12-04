# Kiro Mob Vibing Workshop: Vibe vs Spec Sessions

Welcome to our hands-on exploration of Kiro's two development modes! To get started with Kiro you can check out http://kiro.dev/.  
We'll build the same project twice to see how each approach handles complexity.

## Workshop Overview

**Goal**: Build a spooky 4x4 tic-tac-toe game using both Vibe and Spec sessions  
**Time**: ~20 minutes  
**Model**: Claude Sonnet 4.5  
**Mode**: Autopilot (for speed and flow)

---

## Part 1: Vibe Session - Quick Iteration (10 min)

### What is Vibe Mode?
Kiro's take on traditional AI coding — pure iteration without structure. Just keep prompting until you get what you want. Perfect for quick prototypes and exploration.

### Setup
1. Open Kiro chat panel
2. Select **Vibe Session**
3. Enable **Autopilot mode** (no approval needed for changes)
4. Create a fresh directory for the project

### The Prompt

```
I want to build a 4x4 tic-tac-toe game that can be played in the browser.

Requirements:
- Two players taking turns (X and O)
- Detect wins in rows, columns, and diagonals
- Handle draw conditions
- Spooky theme with purple color scheme, not just black and white
- Minimalistic design
- Smooth animations and hover effects

Make it feel haunted but playable!
```

### Iteration ideas
As the game builds, try these follow-up prompts:
- "Add ghost emoji for X and skull emoji for O"
- "Make the winning line glow with a purple animation"
- "Add a creepy sound effect on win"
- "Display a spooky message when someone wins"
- "Customize names for players"
- "Update color theme to use more black"

### Observe
- How quickly does Kiro scaffold the project?
- How does it handle ambiguity?
- What happens when you ask for changes?

---

## Part 2: Spec Session - Structured Development (10 min)

### The Challenge
Vibe sessions are great for simple projects, but what about complex features? This is where **Spec Sessions** shine.

### What is Spec Mode?
Other tools call it SOLO, plan, or architect mode. Kiro calls it Spec-driven development: create a detailed plan before writing code. It's incremental, controlled, and perfect for complex features.

### Setup
1. **Delete or move** the vibe session project
2. Open Kiro chat panel
3. Select **Spec Session**
4. Keep **Autopilot mode** enabled

### The Spec Prompt

```
I want to create a spec for a 4x4 spooky tic-tac-toe game.

Core Features:
- 4x4 grid (not standard 3x3)
- Two-player turn-based gameplay
- Win detection: 4 in a row (horizontal, vertical, diagonal)
- Draw detection when board is full
- Spooky purple theme with minimalistic design
- Smooth animations and visual feedback

Additional Requirements:
- Game state management
- Reset functionality
- Score tracking across multiple rounds
- Responsive design for mobile and desktop
- Accessibility considerations (keyboard navigation, screen readers)
- Add ghost emoji for X and skull emoji for O
- Make the winning line glow with a purple animation
- Add a creepy sound effect on win
- Display a spooky message when someone wins
- Customize names for players
- Update color theme to use more black

Let's start with requirements gathering.
```

### The Spec Flow
1. **Requirements Phase**: Kiro will help define acceptance criteria
2. **Design Phase**: Kiro creates technical design with properties
3. **Task Breakdown**: Implementation tasks are generated
4. **Implementation**: Kiro works through tasks incrementally

### Iteration During Spec
- Review requirements and suggest changes
- Ask Kiro to add new acceptance criteria
- Request design clarifications
- Approve or modify tasks before implementation

### Observe
- How does the planning phase help?
- What's different about the code structure?
- How does incremental development feel?

---

## Part 3: Discussion & Comparison (10 min)

### Questions to Explore
- When would you use Vibe vs Spec?
- How did autopilot affect the experience?
- What surprised you about each approach?
- How would you handle a production feature?

### Vibe Session Best For:
- Quick prototypes
- Exploratory coding
- Simple features
- Learning new technologies
- Hackathons and demos

### Spec Session Best For:
- Complex features
- Team collaboration
- Production code
- Features requiring planning
- When you need documentation

---

## Bonus Challenges

If time permits, try these:

1. **Add AI Opponent**: "Add a simple AI player that makes random moves"
2. **Multiplayer**: "Make it work over WebSockets for remote play"
3. **Themes**: "Add a theme switcher between spooky, retro, and neon"
4. **Leaderboard**: "Add storage to track wins/losses"

---

## Key Takeaways

- Vibe = Speed and flexibility
- Spec = Structure and control
- Autopilot = Trust the agent
- Both modes can have their place in your workflows.