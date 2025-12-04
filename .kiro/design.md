# Design Document

## Overview

The Spooky 4x4 Tic-Tac-Toe game is implemented as a self-contained HTML file with embedded CSS and JavaScript. The architecture follows a simple Model-View-Controller pattern where the game state (model) is managed separately from the DOM manipulation (view) and user interaction handling (controller). The game features emoji marks (👻 ghost for X, 💀 skull for O), score tracking across multiple rounds, customizable player names, creepy sound effects, and full accessibility support including keyboard navigation and screen reader compatibility. The design emphasizes clean separation of concerns while maintaining simplicity appropriate for a single-file browser application.

## Architecture

The application uses a modular JavaScript architecture with the following layers:

1. **Game State Layer**: Manages the core game logic, board state, win/draw detection, score tracking, and player names
2. **UI Layer**: Handles DOM manipulation, animations, visual feedback, and accessibility features
3. **Event Handler Layer**: Processes user interactions (mouse, keyboard, touch) and coordinates between state and UI
4. **Audio Layer**: Manages sound effect playback for game events
5. **Accessibility Layer**: Provides ARIA labels, announcements, and keyboard navigation support

The single-file structure bundles all HTML, CSS, and JavaScript together for easy deployment and sharing. The JavaScript code is organized into logical modules using object literals and closures to maintain encapsulation. Audio files are embedded as data URIs or generated programmatically to maintain the single-file architecture.

## Components and Interfaces

### GameState

Manages the core game state and logic.

**Properties:**
- `board`: 2D array (4x4) representing cell states (null, 'X', or 'O')
- `currentPlayer`: String indicating active player ('X' or 'O')
- `gameOver`: Boolean indicating if game has ended
- `winner`: String indicating winner ('X', 'O', or 'draw')
- `scores`: Object tracking wins for each player (`{X: number, O: number}`)
- `playerNames`: Object storing custom names (`{X: string, O: string}`)

**Methods:**
- `makeMove(row, col)`: Attempts to place current player's mark, returns success boolean
- `checkWin()`: Checks all win conditions, returns winner or null
- `checkDraw()`: Checks if board is full with no winner
- `reset()`: Resets board for new round while preserving scores and names
- `resetAll()`: Resets everything including scores and names
- `isValidMove(row, col)`: Validates if a move can be made at position
- `incrementScore(player)`: Increments the score for the specified player
- `setPlayerName(player, name)`: Sets custom name for a player

### UIController

Handles all DOM manipulation and visual updates.

**Methods:**
- `renderBoard()`: Creates or updates the 4x4 grid in the DOM with emoji marks
- `updateCell(row, col, value)`: Updates a specific cell with animation
- `showMessage(text)`: Displays game status messages
- `showSpookyVictoryMessage(winner)`: Displays random spooky victory message
- `highlightWinningCells(cells)`: Applies glowing purple animation to winning cells
- `updateTurnIndicator()`: Updates the current player display with custom names
- `updateScoreDisplay()`: Updates the score display for both players
- `enableRestartButton()`: Shows and enables the restart button
- `applyHoverEffects()`: Attaches hover event listeners to cells
- `removeHoverEffects()`: Removes hover event listeners when game ends
- `renderPlayerNameInputs()`: Creates input fields for custom player names
- `getEmojiForPlayer(player)`: Returns appropriate emoji (👻 or 💀) for player

### EventHandler

Coordinates user interactions with game state and UI updates.

**Methods:**
- `handleCellClick(row, col)`: Processes cell click events
- `handleCellKeyPress(event, row, col)`: Processes keyboard input on cells
- `handleRestart()`: Processes restart button clicks
- `handleCellHover(row, col, isEntering)`: Manages hover preview effects
- `handlePlayerNameChange(player, name)`: Updates player name in game state
- `setupKeyboardNavigation()`: Initializes keyboard navigation support
- `moveFocus(direction)`: Moves focus between cells for keyboard navigation

### AudioController

Manages sound effect playback.

**Methods:**
- `playWinSound()`: Plays creepy sound effect when a player wins
- `generateCreepySound()`: Generates or loads the creepy sound effect
- `handleAudioError()`: Gracefully handles audio playback failures

### AccessibilityController

Provides accessibility features for assistive technologies.

**Methods:**
- `announceToScreenReader(message)`: Announces game state changes to screen readers
- `updateCellAriaLabels()`: Updates ARIA labels for all cells
- `setFocusIndicators()`: Applies visible focus indicators for keyboard navigation
- `announceTurn()`: Announces current player's turn to screen readers
- `announceGameResult(result)`: Announces win or draw to screen readers

### WinDetector

Utility module for checking win conditions.

**Methods:**
- `checkRows(board)`: Returns winning row cells or null
- `checkColumns(board)`: Returns winning column cells or null
- `checkDiagonals(board)`: Returns winning diagonal cells or null
- `checkLine(cells)`: Helper to check if four cells contain same non-null value

## Data Models

### Board State

```javascript
// 2D array representing the 4x4 grid
board = [
  [null, null, null, null],
  [null, null, null, null],
  [null, null, null, null],
  [null, null, null, null]
]
```

Each cell can be:
- `null`: Empty cell
- `'X'`: Player X's mark (displayed as 👻)
- `'O'`: Player O's mark (displayed as 💀)

### Cell Position

```javascript
{
  row: number,    // 0-3
  col: number     // 0-3
}
```

### Win Result

```javascript
{
  winner: string,           // 'X' or 'O'
  winningCells: Array<{row, col}>  // Array of 4 cell positions
}
```

### Score State

```javascript
{
  X: number,  // Number of wins for Player X
  O: number   // Number of wins for Player O
}
```

### Player Names

```javascript
{
  X: string,  // Custom name for Player X (default: "Player X")
  O: string   // Custom name for Player O (default: "Player O")
}
```

### Spooky Victory Messages

Array of message templates with placeholder for winner name:
```javascript
[
  "{winner} has summoned victory from the shadows! 👻",
  "The spirits favor {winner}! 💀",
  "{winner} emerges from the darkness victorious! 🌙",
  "A haunting win for {winner}! 🕷️",
  "{winner}'s dark powers prevail! ⚡"
]
```


## Correctness Properties

*A property is a characteristic or behavior that should hold true across all valid executions of a system—essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.*

### Property 1: Valid move placement

*For any* board state and any empty cell position, when a valid move is made, the board should contain the current player's mark at that position.

**Validates: Requirements 1.1**

### Property 2: Invalid move rejection

*For any* board state and any occupied cell position, attempting to place a mark should be rejected and the board state should remain unchanged.

**Validates: Requirements 1.2**

### Property 3: Player turn alternation

*For any* board state and any valid move, after the move is executed, the current player should switch to the other player.

**Validates: Requirements 1.3**

### Property 4: Game over move prevention

*For any* board state where the game has ended (win or draw), attempting to make any move should be rejected and the board should remain unchanged.

**Validates: Requirements 1.5, 4.3**

### Property 5: Row and column win detection

*For any* board state where four consecutive cells in a single row or column contain the same player's mark, the game should detect a win for that player.

**Validates: Requirements 3.1, 3.2**

### Property 6: Draw detection

*For any* board state where all sixteen cells are filled and no win condition exists, the game should detect a draw.

**Validates: Requirements 4.1**

### Property 7: Reset to initial state

*For any* game state (in-progress, won, or draw), calling reset should clear all marks from the board, set the current player to X, and set the game status to in-progress.

**Validates: Requirements 6.2, 6.3**

### Property 8: Score increment on win

*For any* game state where a win is detected, the score for the winning player should increment by exactly one.

**Validates: Requirements 9.1**

### Property 9: Score persistence across rounds

*For any* sequence of game rounds, the scores should accurately accumulate, with each win adding one to the appropriate player's score.

**Validates: Requirements 9.3**

### Property 10: Custom name display

*For any* custom player name that is set, that name should appear in all UI displays including status messages, score displays, and victory messages.

**Validates: Requirements 10.2**

### Property 11: Emoji mark display for X

*For any* cell where Player X places a mark, the UI should display the ghost emoji (👻).

**Validates: Requirements 11.1**

### Property 12: Emoji mark display for O

*For any* cell where Player O places a mark, the UI should display the skull emoji (💀).

**Validates: Requirements 11.2**

### Property 13: Animation application to emoji marks

*For any* mark placement, the same animation classes should be applied regardless of whether the mark is displayed as a letter or emoji.

**Validates: Requirements 11.4**

### Property 14: Sound playback on win

*For any* win condition that is detected, the audio system should attempt to play the creepy sound effect exactly once.

**Validates: Requirements 12.1, 12.2**

### Property 15: Victory message display

*For any* win, a spooky victory message from the predefined list should be displayed, and it should include the winning player's name.

**Validates: Requirements 13.1, 13.2**

### Property 16: Victory message variety

*For any* sequence of multiple wins, the victory messages should show variety and not always be identical.

**Validates: Requirements 13.4**

### Property 17: Winning cell animation

*For any* win condition, all cells in the winning line should have the glowing purple animation class applied, and this class should persist until the game is restarted.

**Validates: Requirements 14.1, 14.3**

### Property 18: Keyboard cell activation

*For any* cell that has focus, pressing Enter or Space should place a mark in that cell if the move is valid.

**Validates: Requirements 16.2**

### Property 19: Screen reader state announcements

*For any* game state change (turn change, win, draw), an announcement should be made to screen readers via ARIA live regions.

**Validates: Requirements 17.1, 17.4**

### Property 20: Cell ARIA labels

*For any* cell on the board, the ARIA label should correctly describe the cell position and current content (empty, X, or O).

**Validates: Requirements 17.2**

## Error Handling

The game handles errors gracefully through validation:

1. **Invalid Move Attempts**: When a player attempts to place a mark in an occupied cell or after the game has ended, the move is silently rejected without changing state or displaying error messages. This maintains the clean, minimalistic UI.

2. **Out of Bounds Access**: Cell click handlers validate row and column indices before processing. Invalid indices are ignored.

3. **State Consistency**: The game state is the single source of truth. UI updates are always derived from state changes, preventing desynchronization.

4. **Audio Playback Failures**: When audio playback is blocked by the browser or fails for any reason, the game continues to function normally without the sound effect. Errors are caught and logged but do not interrupt gameplay.

5. **Empty Player Names**: When a player name input is empty or contains only whitespace, the game uses default names ("Player X" or "Player O") to ensure the UI always displays valid names.

6. **Keyboard Navigation Edge Cases**: When keyboard focus reaches the last cell and Tab is pressed, focus wraps to the first interactive element. Focus management is robust across all game states.

7. **Browser Compatibility**: The code uses standard DOM APIs and CSS features supported by modern browsers. Emoji rendering is handled by the browser's native emoji support. No polyfills are required for the target audience.

## Testing Strategy

The testing approach combines unit tests for core game logic with property-based tests for universal game rules.

### Unit Testing

Unit tests will verify specific examples and edge cases:

- Initial game state (empty board, player X starts)
- Specific win scenarios (example boards with wins in each direction)
- Diagonal win detection (main diagonal and anti-diagonal examples)
- Draw scenario (full board with no winner)
- Reset functionality from various end states

### Property-Based Testing

Property-based tests will verify universal properties across many randomly generated game states:

- **Library**: fast-check (JavaScript property-based testing library)
- **Iterations**: Minimum 100 iterations per property
- **Tagging**: Each test will include a comment with format: `**Feature: spooky-tictactoe, Property {number}: {property_text}**`

Property tests will cover:

1. Valid moves always place marks correctly (Property 1)
2. Invalid moves never modify board state (Property 2)
3. Player turns always alternate after valid moves (Property 3)
4. No moves possible after game ends (Property 4)
5. Win detection works for all rows and columns (Property 5)
6. Draw detection works for all full boards without wins (Property 6)
7. Reset always returns to initial state (Property 7)

### Test Generators

Custom generators will create:
- Random board states (empty, partially filled, full)
- Random valid positions (empty cells)
- Random invalid positions (occupied cells)
- Random winning configurations (rows, columns, diagonals)
- Random draw configurations (full boards with no wins)

### Integration Testing

While the focus is on unit and property tests for game logic, manual testing will verify:
- Visual appearance matches dark theme with purple accents
- Emoji marks (👻 and 💀) render correctly across browsers
- Animations and transitions are smooth
- Hover effects work correctly
- Sound effects play on win (when not blocked by browser)
- Responsive layout adapts to different screen sizes
- Keyboard navigation works smoothly
- Screen reader announcements are clear and timely
- Score tracking persists across multiple rounds
- Player name customization works correctly
- Cross-browser compatibility (Chrome, Firefox, Safari, Edge)

### Accessibility Testing

Specific accessibility testing will include:
- Keyboard-only navigation through all game functions
- Screen reader testing with NVDA, JAWS, or VoiceOver
- Focus indicator visibility and clarity
- ARIA label accuracy and completeness
- Color contrast verification for dark theme
- Touch target sizes for mobile devices

The property-based tests provide high confidence in correctness by testing the game logic across thousands of randomly generated scenarios, while unit tests document specific important cases and serve as examples.
