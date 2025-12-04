# Implementation Plan

- [x] 1. Set up HTML structure and spooky styling





  - Create single HTML file with embedded CSS and JavaScript
  - Implement purple color scheme with dark backgrounds
  - Add CSS for 4x4 grid layout with proper spacing
  - Style player marks (X and O) with high contrast
  - Add CSS animations for fade-in, glow effects, and transitions
  - Implement hover effect styles with opacity previews
  - Make layout responsive for different viewport sizes
  - _Requirements: 7.1, 7.2, 7.3, 7.4, 7.5, 8.1, 8.2, 8.4_






- [ ] 2. Implement core game state management
  - [ ] 2.1 Create GameState module with board representation
    - Implement 4x4 board as 2D array
    - Add currentPlayer tracking (X/O)
    - Add gameOver and winner state properties
    - Implement isValidMove validation function
    - _Requirements: 1.1, 1.2_

  - [ ]* 2.2 Write property test for valid move placement
    - **Property 1: Valid move placement**
    - **Validates: Requirements 1.1**



  - [ ]* 2.3 Write property test for invalid move rejection
    - **Property 2: Invalid move rejection**
    - **Validates: Requirements 1.2**

  - [ ] 2.4 Implement makeMove function with player switching
    - Add logic to place mark in cell
    - Implement automatic player turn switching
    - Return success/failure boolean


    - _Requirements: 1.1, 1.3_

  - [ ]* 2.5 Write property test for player turn alternation
    - **Property 3: Player turn alternation**
    - **Validates: Requirements 1.3**

  - [x] 2.6 Implement reset function

    - Clear all board cells to null

    - Reset currentPlayer to 'X'
    - Reset gameOver to false
    - Reset winner to null
    - _Requirements: 6.2, 6.3_

  - [ ]* 2.7 Write property test for reset functionality
    - **Property 7: Reset to initial state**
    - **Validates: Requirements 6.2, 6.3**

- [ ] 3. Implement win detection logic
  - [ ] 3.1 Create WinDetector module
    - Implement checkRows function for all 4 rows
    - Implement checkColumns function for all 4 columns
    - Implement checkDiagonals for main and anti-diagonal
    - Implement helper checkLine function
    - Return winning player and cell positions

    - _Requirements: 3.1, 3.2, 3.3, 3.4_

  - [x]* 3.2 Write property test for row and column wins

    - **Property 5: Row and column win detection**

    - **Validates: Requirements 3.1, 3.2**

  - [ ]* 3.3 Write unit tests for diagonal wins
    - Test main diagonal win detection
    - Test anti-diagonal win detection
    - _Requirements: 3.3, 3.4_

  - [ ] 3.4 Integrate win detection into makeMove
    - Call checkWin after each move

    - Update gameOver and winner state when win detected
    - _Requirements: 3.1, 3.2, 3.3, 3.4_

- [ ] 4. Implement draw detection
  - [ ] 4.1 Create checkDraw function
    - Check if all 16 cells are filled
    - Verify no win condition exists

    - Update gameOver and winner to 'draw'
    - _Requirements: 4.1_



  - [ ]* 4.2 Write property test for draw detection
    - **Property 6: Draw detection**
    - **Validates: Requirements 4.1**

  - [x] 4.3 Integrate draw detection into makeMove

    - Call checkDraw after win check
    - Update game state appropriately
    - _Requirements: 4.1, 4.3_

  - [x]* 4.4 Write property test for game over move prevention

    - **Property 4: Game over move prevention**
    - **Validates: Requirements 1.5, 4.3**

- [ ] 5. Checkpoint - Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.


- [ ] 6. Implement UI rendering and updates
  - [ ] 6.1 Create UIController module
    - Implement renderBoard to create 4x4 grid DOM elements
    - Add data attributes for row/col to each cell
    - Apply initial styling classes

    - _Requirements: 8.1, 8.2_

  - [ ] 6.2 Implement cell update with animations
    - Create updateCell function to add marks to DOM

    - Apply fade-in animation when mark appears
    - Update cell styling based on state
    - _Requirements: 1.4_

  - [ ] 6.3 Implement game status display
    - Create showMessage function for status text

    - Implement updateTurnIndicator for current player
    - Display victory messages with winner identification
    - Display draw messages
    - _Requirements: 5.1, 5.2, 5.3, 5.4, 4.2_

  - [ ] 6.4 Implement winning cell highlighting
    - Create highlightWinningCells function
    - Apply glow animation to winning sequence
    - Add visual distinction for winning cells
    - _Requirements: 3.5_

  - [ ] 6.5 Implement restart button
    - Create and show restart button when game ends
    - Style button with spooky theme
    - _Requirements: 6.1_

- [x] 7. Implement event handling

  - [x] 7.1 Create EventHandler module

    - Implement handleCellClick function
    - Extract row/col from clicked element
    - Call GameState.makeMove
    - Trigger UI updates on successful move
    - _Requirements: 1.1, 1.2, 1.5_

  - [x] 7.2 Implement hover effects

    - Create applyHoverEffects function
    - Add mouseenter/mouseleave listeners to cells
    - Show preview mark with reduced opacity on hover
    - Only show preview for empty cells during active game
    - Remove preview on mouse leave with smooth transition
    - _Requirements: 2.1, 2.2, 2.3, 2.4_


  - [ ] 7.3 Implement restart handler
    - Create handleRestart function
    - Call GameState.reset
    - Clear all UI elements and animations
    - Re-render board in initial state
    - Hide restart button
    - Re-enable hover effects
    - _Requirements: 6.2, 6.3, 6.4_


  - [ ] 7.4 Wire up all event listeners
    - Attach click listeners to all cells

    - Attach click listener to restart button

    - Initialize hover effects on game start
    - _Requirements: 1.1, 6.2_

- [ ] 8. Initialize and wire everything together
  - [ ] 8.1 Create main initialization function
    - Initialize GameState

    - Render initial board
    - Set up all event handlers
    - Display initial turn indicator
    - _Requirements: 5.1, 8.3_

  - [ ] 8.2 Add DOMContentLoaded listener
    - Call initialization when page loads
    - Ensure all DOM elements are ready
    - _Requirements: 8.1_



  - [ ]* 8.3 Write unit test for initial game state
    - Verify board starts empty
    - Verify Player X starts first
    - Verify game is not over initially
    - _Requirements: 5.1_

- [ ] 9. Final checkpoint - Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.

- [x] 10. Update color theme to darker palette


  - [x] 10.1 Update CSS color scheme



    - Change primary background to black (#000000)
    - Update secondary backgrounds to dark grays (#0a0a0a, #1a1a1a)
    - Maintain purple accents for highlights (#7c4dff, #9575cd, #b388ff)
    - Update cell backgrounds to very dark purple (#1a0d2e)
    - Ensure sufficient contrast for readability
    - _Requirements: 15.1, 15.2, 15.3_

- [x] 11. Implement emoji marks


  - [x] 11.1 Update UIController to use emoji marks


    - Modify getEmojiForPlayer to return 👻 for X and 💀 for O
    - Update renderBoard to display emoji instead of letters
    - Update hover preview to show emoji
    - Ensure emoji size and styling match design
    - _Requirements: 11.1, 11.2_

  - [ ]* 11.2 Write property test for emoji display
    - **Property 11: Emoji mark display for X**
    - **Property 12: Emoji mark display for O**
    - **Validates: Requirements 11.1, 11.2**

  - [ ]* 11.3 Write property test for emoji animations
    - **Property 13: Animation application to emoji marks**
    - **Validates: Requirements 11.4**

- [x] 12. Implement score tracking


  - [x] 12.1 Add score properties to GameState


    - Add scores object with X and O properties
    - Implement incrementScore method
    - Update reset to preserve scores (only clear board)
    - Add resetAll method to clear scores and board
    - _Requirements: 9.1, 9.3_

  - [x] 12.2 Create score display UI


    - Add score display elements to HTML
    - Style score display with dark theme
    - Position prominently above or beside game board
    - _Requirements: 9.4_

  - [x] 12.3 Integrate score updates


    - Call incrementScore when win is detected
    - Update score display after each round
    - Ensure scores persist across rounds
    - _Requirements: 9.1, 9.2, 9.3_

  - [ ]* 12.4 Write property test for score increment
    - **Property 8: Score increment on win**
    - **Validates: Requirements 9.1**

  - [ ]* 12.5 Write property test for score persistence
    - **Property 9: Score persistence across rounds**
    - **Validates: Requirements 9.3**

- [x] 13. Implement custom player names



  - [x] 13.1 Add player name properties to GameState


    - Add playerNames object with X and O properties
    - Set default names ("Player X" and "Player O")
    - Implement setPlayerName method
    - Handle empty/whitespace names with defaults
    - _Requirements: 10.3_

  - [x] 13.2 Create player name input UI


    - Add input fields for both player names
    - Style inputs with dark theme
    - Position above game board or in header
    - Add labels for accessibility
    - _Requirements: 10.1_

  - [x] 13.3 Integrate player names throughout UI


    - Update status messages to use custom names
    - Update score display to show custom names
    - Update victory messages to use custom names
    - Handle name changes during gameplay
    - _Requirements: 10.2, 10.4_

  - [ ]* 13.4 Write property test for custom name display
    - **Property 10: Custom name display**




    - **Validates: Requirements 10.2**

- [ ] 14. Implement spooky victory messages
  - [x] 14.1 Create victory message system


    - Define array of spooky message templates
    - Implement random message selection
    - Create message formatting with player name substitution
    - _Requirements: 13.1, 13.2_

  - [ ] 14.2 Update UIController for victory messages
    - Create showSpookyVictoryMessage method
    - Replace generic win message with spooky message
    - Ensure message includes winner's custom name
    - Style message with dramatic presentation
    - _Requirements: 13.1, 13.2, 13.3_




  - [ ]* 14.3 Write property test for victory messages
    - **Property 15: Victory message display**
    - **Validates: Requirements 13.1, 13.2**

  - [ ]* 14.4 Write property test for message variety
    - **Property 16: Victory message variety**

    - **Validates: Requirements 13.4**

- [ ] 15. Enhance winning cell animation
  - [ ] 15.1 Update CSS for glowing purple animation
    - Enhance winGlow animation with more dramatic effect
    - Increase glow intensity and color saturation
    - Add pulsing effect to draw more attention




    - Ensure animation loops continuously
    - _Requirements: 14.1, 14.2_

  - [ ] 15.2 Verify animation persistence
    - Ensure animation continues until restart


    - Test that animation doesn't interfere with readability
    - _Requirements: 14.3, 14.4_

  - [ ]* 15.3 Write property test for winning animation
    - **Property 17: Winning cell animation**
    - **Validates: Requirements 14.1, 14.3**





- [ ] 16. Implement creepy sound effect
  - [ ] 16.1 Create AudioController module
    - Implement playWinSound method
    - Generate or embed creepy sound effect as data URI
    - Handle audio playback with try-catch for browser blocking


    - Ensure sound plays only once per win
    - _Requirements: 12.1, 12.2, 12.4_

  - [ ] 16.2 Integrate sound into win detection
    - Call playWinSound when win is detected

    - Ensure game continues if audio fails
    - Log audio errors without disrupting gameplay
    - _Requirements: 12.1, 12.3_

  - [ ]* 16.3 Write property test for sound playback
    - **Property 14: Sound playback on win**
    - **Validates: Requirements 12.1, 12.2**





- [ ] 17. Implement keyboard navigation
  - [ ] 17.1 Add keyboard event handlers
    - Implement handleCellKeyPress for Enter/Space
    - Add Tab navigation support with proper tabindex


    - Implement arrow key navigation between cells
    - Handle focus wrapping at edges
    - _Requirements: 16.1, 16.2_

  - [x] 17.2 Add visible focus indicators


    - Update CSS with clear focus styles
    - Ensure focus outline is visible on dark background
    - Use high-contrast colors for focus indicator
    - Test focus visibility across all states
    - _Requirements: 16.3_

  - [ ] 17.3 Implement focus management
    - Return focus to first cell on restart
    - Manage focus during game state changes
    - Ensure focus doesn't get trapped
    - _Requirements: 16.4_


  - [x]* 17.4 Write property test for keyboard activation

    - **Property 18: Keyboard cell activation**
    - **Validates: Requirements 16.2**

- [ ] 18. Implement screen reader accessibility
  - [ ] 18.1 Create AccessibilityController module
    - Implement announceToScreenReader method
    - Create ARIA live region for announcements
    - Implement updateCellAriaLabels method

    - _Requirements: 17.1, 17.2_

  - [ ] 18.2 Add ARIA labels to all elements
    - Add aria-label to all cells with position and content
    - Add aria-label to restart button
    - Add aria-label to player name inputs

    - Add aria-label to score display
    - _Requirements: 17.3_

  - [ ] 18.3 Implement game state announcements
    - Announce turn changes to screen readers


    - Announce wins and draws
    - Announce score updates
    - Update announcements when names change
    - _Requirements: 17.1, 17.4_

  - [ ]* 18.4 Write property test for screen reader announcements
    - **Property 19: Screen reader state announcements**
    - **Validates: Requirements 17.1, 17.4**

  - [ ]* 18.5 Write property test for cell ARIA labels
    - **Property 20: Cell ARIA labels**
    - **Validates: Requirements 17.2**

- [ ] 19. Final integration and testing
  - [ ] 19.1 Test all features together
    - Verify emoji marks work with all features
    - Test score tracking across multiple rounds
    - Verify custom names appear everywhere
    - Test sound effect with wins
    - Verify keyboard navigation works completely
    - Test screen reader announcements
    - _Requirements: All_

  - [ ] 19.2 Test responsive design
    - Verify layout on mobile devices
    - Test touch interactions
    - Ensure all features work on small screens
    - Verify emoji rendering on different devices
    - _Requirements: 8.2_

  - [ ] 19.3 Cross-browser testing
    - Test on Chrome, Firefox, Safari, Edge
    - Verify emoji rendering across browsers
    - Test audio playback across browsers
    - Verify keyboard navigation across browsers
    - _Requirements: 8.1_

- [ ] 20. Final checkpoint - Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.
