<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Number Ninja - Puzzle Game (No Ads)</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Rye&family=Metal+Mania&display=swap');

        body {
            font-family: 'Georgia', serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            background-image: url('https://www.transparenttextures.com/patterns/wood-pattern.png');
            color: #F5DEB3;
            position: relative;
            overflow-x: hidden;
        }

        /* --- Common Button Style --- */
        .wooden-button { font-family: 'Rye', cursive; color: #FFF8DC; background-color: #8B4513; border: 2px solid #5C3317; border-radius: 8px; cursor: pointer; transition: background-color 0.2s, transform 0.2s, box-shadow 0.2s; box-shadow: 2px 2px 5px rgba(0,0,0,0.4), inset 1px 1px 2px rgba(255,255,255,0.15); text-shadow: 1px 1px 2px rgba(0,0,0,0.6); padding: clamp(10px, 3vw, 15px) clamp(20px, 5vw, 30px); font-size: clamp(1.1em, 3.5vw, 1.4em); }
        .wooden-button:hover { background-color: #A0522D; transform: scale(1.03); box-shadow: 3px 3px 7px rgba(0,0,0,0.5), inset 1px 1px 3px rgba(255,255,255,0.1); }
        .wooden-button-small { font-size: clamp(0.8em, 2.2vw, 1em) !important; padding: clamp(7px, 1.8vw, 9px) clamp(10px, 2.8vw, 13px) !important; background-color: #704214 !important; border-color: #502f0f !important; }
        .wooden-button-darker { background-color: #693307 !important; border-color: #452205 !important; font-size: clamp(0.9em, 3vw, 1.1em) !important; padding: clamp(7px, 2.2vw, 10px) clamp(15px, 4vw, 22px) !important; }
        .wooden-button-darker:hover { background-color: #502f0f !important; }
        .share-button { 
            background-color: #4CAF50 !important; 
            border-color: #388E3C !important;
            font-size: clamp(0.9em, 2.8vw, 1.1em) !important;
            padding: clamp(8px, 2.5vw, 12px) clamp(15px, 4.5vw, 25px) !important;
            margin-top: 10px;
        }
        .share-button:hover {
            background-color: #388E3C !important;
        }


        /* --- Start Screen Styles --- */
        #start-screen { display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; background-color: rgba(139, 69, 19, 0.85); padding: 30px 40px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.6), inset 0 0 15px rgba(0,0,0,0.4); border: 4px solid #8B4513; color: #FFF8DC; width: auto; max-width: 90vw; }
        #start-screen h1 { font-family: 'Metal Mania', cursive; font-size: clamp(2em, 6vw, 3.5em); margin-bottom: 20px; color: #FFD700; text-shadow: 2px 2px 0px #8B4513, 4px 4px 0px #5C3317, 3px 3px 8px rgba(0,0,0,0.7); letter-spacing: 2px; }
        #start-screen p { font-size: clamp(1em, 3vw, 1.2em); margin-bottom: 20px; max-width: 400px; }
        
        /* --- Level Selection Screen Styles --- */
        #level-selection-screen { display: none; flex-direction: column; align-items: center; justify-content: center; text-align: center; background-color: rgba(139, 69, 19, 0.88); padding: 25px 20px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.6), inset 0 0 15px rgba(0,0,0,0.4); border: 4px solid #8B4513; color: #FFF8DC; width: auto; max-width: 90vw; min-width: 300px; }
        #level-selection-screen h2 { font-family: 'Rye', cursive; font-size: clamp(1.6em, 4.5vw, 2.5em); margin-bottom: 25px; color: #FFD700; text-shadow: 1px 1px 0px #8B4513, 2px 2px 0px #5C3317, 2px 2px 5px rgba(0,0,0,0.6); }
        .level-input-container { margin-bottom: 20px; display: flex; flex-direction: column; align-items: center; gap: 10px; }
        .level-input-container label { font-size: clamp(0.9em, 2.8vw, 1.1em); font-family: 'Rye', cursive; color: #FFEBCD; }
        #level-number-input { padding: 8px; font-size: clamp(0.9em, 2.8vw, 1.1em); border-radius: 8px; border: 2px solid #8B4513; background-color: #DEB887; color: #5C3317; width: 130px; text-align: center; font-family: 'Georgia', serif; box-shadow: inset 1px 1px 3px rgba(0,0,0,0.3); }
        .level-group-buttons { display: flex; flex-wrap: wrap; justify-content: center; gap: 8px; margin-top: 10px; margin-bottom: 15px; }
        #level-select-message { color: #FFD700; font-size: 0.9em; margin-top: 10px; min-height: 1.2em; }
        
        /* --- Game Area Styles --- */
        #game-area { display: none; flex-direction: column; align-items: center; width: 100%; padding-top: 15px; position: relative; }
        #game-back-arrow { position: absolute; top: 12px; left: 12px; font-size: clamp(1.8em, 5vw, 2.5em); font-family: 'Georgia', serif;  color: #FFF8DC; cursor: pointer; text-shadow: 2px 2px 4px rgba(0,0,0,0.8);  z-index: 10; background: rgba(101, 67, 33, 0.5);  border: 1px solid rgba(70, 47, 23, 0.7); border-radius: 50%;  width: clamp(35px, 8vw, 50px);  height: clamp(35px, 8vw, 50px);  display: flex; align-items: center; justify-content: center; line-height: 1;  padding-bottom: 3px;  }
        #game-back-arrow:hover { background: rgba(139, 69, 19, 0.7);  color: #FFD700; }

        #game-area > h1 { font-family: 'Metal Mania', cursive; font-size: clamp(1.5em, 4vw, 2.2em); margin-bottom: 8px; color: #FFD700; text-shadow: 1px 1px 0px #8B4513, 2px 2px 0px #5C3317, 2px 2px 6px rgba(0,0,0,0.7); text-align: center; padding-left: 50px;  padding-right: 50px;  box-sizing: border-box; width: 100%; }
        #level-display { font-family: 'Rye', cursive; font-size: clamp(1.2em, 3.2vw, 1.6em); margin-bottom: 10px; color: #FFEBCD;  font-weight: normal;  text-shadow: 1px 1px 2px rgba(0,0,0,0.6); text-align: center; }
        #game-container { padding: 10px; display: flex; flex-direction: column; align-items: center; background-color: rgba(139, 69, 19, 0.80); border-radius: 15px; box-shadow: 0 10px 20px rgba(0,0,0,0.5), inset 0 0 10px rgba(0,0,0,0.3); border: 3px solid #8B4513; width: auto; max-width: 95vw; z-index: 1; }
        #puzzle-board { display: grid; gap: 4px; background-color: #A0522D; padding: 4px; border-radius: 8px; border: 2px solid #5C3317; box-shadow: inset 0 0 8px rgba(0,0,0,0.5); margin-bottom: 10px; }
        .tile { background-color: #DEB887; color: #5C3317; display: flex; align-items: center; justify-content: center; font-weight: bold; cursor: pointer; border-radius: 4px; transition: background-color 0.1s, transform 0.1s; user-select: none; box-shadow: 1px 1px 3px rgba(0,0,0,0.3), inset 1px 1px 1px rgba(255,255,255,0.1); border: 1px solid #8B4513; font-family: 'Georgia', serif; }
        .tile:hover { background-color: #CDA67F; transform: scale(1.03); }
        .empty { background-color: #A0522D; cursor: default; box-shadow: inset 1px 1px 3px rgba(0,0,0,0.4); border: 1px dashed #654321; }
        .empty:hover { background-color: #A0522D; transform: none; }
        #info-panel { display: flex; justify-content: space-around; width: 100%; margin-bottom: 10px; flex-wrap: wrap; gap: 8px; }
        #moves-counter, #timer-display { font-size: clamp(0.8em, 2.5vw, 0.9em); color: #FFF8DC; background-color: rgba(92, 51, 23, 0.65); padding: 4px 8px; border-radius: 5px; box-shadow: inset 1px 1px 3px rgba(0,0,0,0.5); min-width: 90px; text-align: center; font-family: 'Rye', cursive; }
        #controls { margin-top: 5px; text-align: center; display: flex; flex-direction: column; align-items: center; gap: 10px; }
        .control-buttons { display: flex; gap: 10px; }
        #message { font-size: clamp(1em, 3vw, 1.1em); font-weight: bold; color: #FF8C00; min-height: 20px; text-shadow: 1px 1px 2px rgba(0,0,0,0.7); text-align: center; }

        /* --- Popup Styles --- */
        .popup-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0, 0, 0, 0.7); display: none; justify-content: center; align-items: center; z-index: 1000; padding: 15px; box-sizing: border-box; }
        .popup-content { background-color: #DEB887; padding: clamp(20px, 5vw, 30px) clamp(25px, 6vw, 40px); border-radius: 15px; box-shadow: 0 5px 25px rgba(0,0,0,0.5); text-align: center; color: #5C3317; border: 3px solid #8B4513; width: auto; max-width: 500px; max-height: 90vh; overflow-y: auto; }
        .popup-content h2 { font-family: 'Rye', cursive; color: #8B4513; margin-top: 0; margin-bottom: 15px; font-size: clamp(1.5em, 4.5vw, 1.8em); text-shadow: 1px 1px 1px rgba(0,0,0,0.3); }
        .popup-content p { font-size: clamp(1em, 3vw, 1.1em); margin-bottom: 20px; }
        .popup-buttons { display: flex; justify-content: center; gap: 15px; flex-wrap: wrap;}
    </style>
</head>
<body>
    <audio id="tile-drop-sound" preload="auto">
        <source src="dropsound.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>
    <!-- Ad Overlay HTML removed -->

    <div id="start-screen">
        <h1>Number Ninja</h1>
        <p>Test your mind! Arrange the tiles in order and see how many levels you can conquer.</p>
        <button id="start-game-button" class="wooden-button">Start Game</button>
        <button id="share-game-start-button" class="wooden-button share-button" style="margin-top: 15px;">Share Game</button>
    </div>

    <div id="level-selection-screen">
        <h2>Select Level</h2>
        <div class="level-input-container">
            <label for="level-number-input">Level Number (1 - <span id="max-level-display">10000</span>):</label>
            <input type="number" id="level-number-input" min="1" value="1">
            <button id="go-to-level-button" class="wooden-button">Go to Level</button>
        </div>
        <p>Or choose a range:</p>
        <div class="level-group-buttons">
            <button class="level-group-btn wooden-button wooden-button-small" data-level="1">Level 1</button>
            <button class="level-group-btn wooden-button wooden-button-small" data-level="10">Level 10</button>
            <button class="level-group-btn wooden-button wooden-button-small" data-level="50">Level 50</button>
            <button class="level-group-btn wooden-button wooden-button-small" data-level="101">Level 101</button>
            <button class="level-group-btn wooden-button wooden-button-small" data-level="501">Level 501</button>
            <button class="level-group-btn wooden-button wooden-button-small" data-level="1001">Level 1001</button>
        </div>
        <p id="level-select-message"></p>
        <button id="back-to-start-button" class="wooden-button wooden-button-darker">Back to Main Screen</button>
    </div>

    <div id="game-area">
        <button id="game-back-arrow" title="Select Level">❮</button>
        <h1>Number Ninja</h1>
        <div id="level-display">Level: 1</div>
        <div id="game-container">
            <div id="puzzle-board"></div>
            <div id="info-panel">
                <p id="moves-counter">Moves: 0</p>
                <p id="timer-display">Time: 00:00</p>
            </div>
            <div id="controls">
                <div class="control-buttons">
                    <button id="reset-button" class="wooden-button">Reset Level</button>
                </div>
                <p id="message"></p>
            </div>
        </div>
    </div>

    <div id="congrats-popup" class="popup-overlay">
        <div class="popup-content">
            <h2>Congratulations!</h2>
            <p id="popup-message-content">You completed the level!</p>
            <div class="popup-buttons">
                <button id="popup-share-button" class="wooden-button share-button">Share Score</button>
                <button id="popup-next-level-button" class="wooden-button">Next Level</button>
            </div>
        </div>
    </div>

    <script>
        let currentLevel = 1;
        const MAX_LEVEL = 10000;
        let GRID_SIZE;
        let MAX_BOARD_WIDTH_PX = Math.min(window.innerWidth * 0.9, window.innerHeight * 0.55, 380);
        let board = [], emptyTile = { r: 0, c: 0 }, moves = 0;
        let gameActiveForTimer = false, levelComplete = false;
        let timerInterval = null, elapsedTimeInSeconds = 0;

        const LOCAL_STORAGE_LEVEL_KEY = 'numberPuzzle_currentLevel';

        let startScreen, startGameButton, shareGameStartButton, levelSelectionScreen, gameArea;
        let levelNumberInput, goToLevelButton, levelGroupButtons, levelSelectMessage, backToStartButton, maxLevelDisplay;
        let gameBackArrow, puzzleBoard, resetButton, messageElement, movesCounterElement, timerDisplayElement, levelDisplayElement;
        let congratsPopup, popupMessageContent, popupNextLevelButton, popupShareButton;
        let tileDropSound;
        // Ad related DOM elements removed

        function assignDOMelements() {
            console.log("Assigning DOM elements...");
            startScreen = document.getElementById('start-screen');
            startGameButton = document.getElementById('start-game-button');
            shareGameStartButton = document.getElementById('share-game-start-button');
            
            levelSelectionScreen = document.getElementById('level-selection-screen');
            levelNumberInput = document.getElementById('level-number-input');
            goToLevelButton = document.getElementById('go-to-level-button');
            levelGroupButtons = document.querySelectorAll('.level-group-btn');
            levelSelectMessage = document.getElementById('level-select-message');
            backToStartButton = document.getElementById('back-to-start-button');
            maxLevelDisplay = document.getElementById('max-level-display');
            
            gameArea = document.getElementById('game-area');
            gameBackArrow = document.getElementById('game-back-arrow');
            puzzleBoard = document.getElementById('puzzle-board');
            resetButton = document.getElementById('reset-button');
            messageElement = document.getElementById('message');
            movesCounterElement = document.getElementById('moves-counter');
            timerDisplayElement = document.getElementById('timer-display');
            levelDisplayElement = document.getElementById('level-display');
            
            congratsPopup = document.getElementById('congrats-popup');
            popupMessageContent = document.getElementById('popup-message-content');
            popupNextLevelButton = document.getElementById('popup-next-level-button');
            popupShareButton = document.getElementById('popup-share-button');
            
            tileDropSound = document.getElementById('tile-drop-sound');
            // Ad related DOM elements assignments removed
            console.log("DOM elements assigned.");
        }

        function playTileDropSound() { if (tileDropSound) { tileDropSound.currentTime = 0; tileDropSound.play().catch(error => console.warn("Tile drop sound play failed:", error)); } }
        function saveCurrentLevel(level) { try { localStorage.setItem(LOCAL_STORAGE_LEVEL_KEY, level.toString()); console.log(`Level ${level} saved to localStorage.`); } catch (e) { console.error("Error saving level to localStorage:", e); } }
        function loadSavedLevel() { try { const savedLevel = localStorage.getItem(LOCAL_STORAGE_LEVEL_KEY); if (savedLevel !== null) { const parsedLevel = parseInt(savedLevel); if (!isNaN(parsedLevel) && parsedLevel >= 1 && parsedLevel <= MAX_LEVEL) { console.log(`Loaded level ${parsedLevel} from localStorage.`); return parsedLevel; } } } catch (e) { console.error("Error loading level from localStorage:", e); } return 1; }

        function showStartScreen() { if(startScreen) startScreen.style.display = 'flex'; if(levelSelectionScreen) levelSelectionScreen.style.display = 'none'; if(gameArea) gameArea.style.display = 'none'; /* adOverlay check removed */ document.body.style.justifyContent = 'center'; document.body.style.paddingTop = '0'; console.log("Showing Start Screen"); }
        function showLevelSelectionScreen() { if(startScreen) startScreen.style.display = 'none'; if(levelSelectionScreen) levelSelectionScreen.style.display = 'flex'; if(gameArea) gameArea.style.display = 'none'; /* adOverlay check removed */ document.body.style.justifyContent = 'center'; document.body.style.paddingTop = '0'; currentLevel = loadSavedLevel(); if(levelNumberInput) { levelNumberInput.max = MAX_LEVEL.toString(); levelNumberInput.value = currentLevel.toString(); } if(maxLevelDisplay) maxLevelDisplay.textContent = MAX_LEVEL.toString(); if(levelSelectMessage) levelSelectMessage.textContent = `आपका सहेजा गया लेवल: ${currentLevel}`; console.log("Showing Level Selection Screen, current level:", currentLevel); }
        function showGameScreen() { if(startScreen) startScreen.style.display = 'none'; if(levelSelectionScreen) levelSelectionScreen.style.display = 'none'; if(gameArea) gameArea.style.display = 'flex'; /* adOverlay check removed */ document.body.style.justifyContent = 'flex-start'; document.body.style.paddingTop = '10px'; console.log("Showing Game Screen for level:", currentLevel); }
        
        function getGridSizeForLevel(level) { level = parseInt(level); if (level <= 5) return 3; if (level <= 20) return 4; if (level <= 50) return 5; if (level <= 100) return 6; let size = 6 + Math.floor((level - 101) / 100); return Math.min(size, 10); }
        function getShuffleDifficultyFactor(level) { level = parseInt(level); if (GRID_SIZE <= 3) return 0.8 + (level * 0.05); if (GRID_SIZE === 4) return 1 + (level * 0.01); return 1.2 + (level * 0.005); }
        function getTileSize() { MAX_BOARD_WIDTH_PX = Math.min(window.innerWidth * 0.9, window.innerHeight * 0.55, 380); const totalGapSpace = (GRID_SIZE + 1) * 4; let TILE_SIZE_PX = Math.floor((MAX_BOARD_WIDTH_PX - totalGapSpace) / GRID_SIZE); return Math.max(25, TILE_SIZE_PX); }
        function getFontSize(tileSize) { if (GRID_SIZE >= 7) return Math.max(10, tileSize * 0.35) + 'px'; if (GRID_SIZE >= 5) return Math.max(12, tileSize * 0.4) + 'px'; return Math.max(14, tileSize * 0.45) + 'px'; }
        function formatTime(seconds) { const mins = Math.floor(seconds / 60); const secs = seconds % 60; return `${mins < 10 ? '0' : ''}${mins}:${secs < 10 ? '0' : ''}${secs}`; }
        function updateTimerDisplay() { if(timerDisplayElement) timerDisplayElement.textContent = `समय: ${formatTime(elapsedTimeInSeconds)}`; }
        function startTimer() { if (timerInterval) clearInterval(timerInterval); elapsedTimeInSeconds = 0; updateTimerDisplay(); timerInterval = setInterval(() => { if (!levelComplete) {  elapsedTimeInSeconds++; updateTimerDisplay(); } }, 1000); gameActiveForTimer = true; }
        function stopTimer() { if (timerInterval) clearInterval(timerInterval); }
        function createBoard() { board = []; for (let r = 0; r < GRID_SIZE; r++) { board[r] = []; for (let c = 0; c < GRID_SIZE; c++) { board[r][c] = 0; } } }
        function shuffleBoard() { let count = 1; for (let r = 0; r < GRID_SIZE; r++) { for (let c = 0; c < GRID_SIZE; c++) { if (r === GRID_SIZE - 1 && c === GRID_SIZE - 1) { board[r][c] = null; emptyTile = { r, c }; } else { board[r][c] = count++; } } } const difficultyFactor = getShuffleDifficultyFactor(currentLevel); let baseShuffleMoves; if (GRID_SIZE === 3) baseShuffleMoves = 20; else if (GRID_SIZE === 4) baseShuffleMoves = 80; else if (GRID_SIZE === 5) baseShuffleMoves = 150; else baseShuffleMoves = GRID_SIZE * GRID_SIZE * 5; let shuffleMoves = Math.floor(baseShuffleMoves * difficultyFactor) + Math.floor(Math.random() * GRID_SIZE * 3); shuffleMoves = Math.min(shuffleMoves, GRID_SIZE * GRID_SIZE * 20); for (let i = 0; i < shuffleMoves; i++) { const neighbors = []; if (emptyTile.r > 0) neighbors.push({ r: emptyTile.r - 1, c: emptyTile.c }); if (emptyTile.r < GRID_SIZE - 1) neighbors.push({ r: emptyTile.r + 1, c: emptyTile.c }); if (emptyTile.c > 0) neighbors.push({ r: emptyTile.r, c: emptyTile.c - 1 }); if (emptyTile.c < GRID_SIZE - 1) neighbors.push({ r: emptyTile.r, c: emptyTile.c + 1 }); if (neighbors.length > 0) { const randomNeighbor = neighbors[Math.floor(Math.random() * neighbors.length)]; swapTiles(randomNeighbor.r, randomNeighbor.c, emptyTile.r, emptyTile.c, false); } } moves = 0; updateMovesCounter(); }
        function renderBoard() { if (!puzzleBoard) return; puzzleBoard.innerHTML = ''; const TILE_SIZE_PX = getTileSize(); const FONT_SIZE = getFontSize(TILE_SIZE_PX); puzzleBoard.style.gridTemplateColumns = `repeat(${GRID_SIZE}, ${TILE_SIZE_PX}px)`; puzzleBoard.style.gridTemplateRows = `repeat(${GRID_SIZE}, ${TILE_SIZE_PX}px)`; const boardDimension = (TILE_SIZE_PX * GRID_SIZE) + ((GRID_SIZE -1) * 4) + (2 * 4); puzzleBoard.style.width = `${boardDimension}px`; puzzleBoard.style.height = `${boardDimension}px`; for (let r = 0; r < GRID_SIZE; r++) { for (let c = 0; c < GRID_SIZE; c++) { const tileValue = board[r][c]; const tileElement = document.createElement('div'); tileElement.classList.add('tile'); tileElement.style.width = `${TILE_SIZE_PX}px`; tileElement.style.height = `${TILE_SIZE_PX}px`; tileElement.style.fontSize = FONT_SIZE; if (tileValue === null) { tileElement.classList.add('empty'); } else { tileElement.textContent = tileValue; } tileElement.addEventListener('click', () => handleTileClick(r, c)); puzzleBoard.appendChild(tileElement); } } }
        
        function handleTileClick(r, c) {
            if (levelComplete || board[r][c] === null) return;
            if (!gameActiveForTimer) { startTimer(); }
            const dr = Math.abs(r - emptyTile.r);
            const dc = Math.abs(c - emptyTile.c);
            if ((dr === 1 && dc === 0) || (dr === 0 && dc === 1)) {
                playTileDropSound();
                swapTiles(r, c, emptyTile.r, emptyTile.c, true);
                if (checkWin()) {
                    levelComplete = true;
                    stopTimer();
                    if(puzzleBoard) puzzleBoard.style.opacity = '0.7';
                    saveCurrentLevel(currentLevel + 1 > MAX_LEVEL ? MAX_LEVEL : currentLevel + 1);
                    showCongratsPopup(); // सीधे बधाई पॉप-अप दिखाएं
                }
            }
        }

        // Ad related functions removed: showAdThenCongrats, adFinishedOrFailed, proceedToCongratsAfterAd

        function showCongratsPopup() { if(!popupMessageContent || !popupNextLevelButton || !congratsPopup || !popupShareButton) return; popupMessageContent.textContent = `लेवल ${currentLevel} पूरा! ${moves} चालों में, ${formatTime(elapsedTimeInSeconds)} में।`; if (currentLevel >= MAX_LEVEL) { popupMessageContent.textContent += " आपने सभी लेवल पूरे कर लिए!"; popupNextLevelButton.style.display = 'none'; popupShareButton.textContent = 'Share Game'; } else { popupNextLevelButton.style.display = 'inline-block'; popupNextLevelButton.disabled = false; popupNextLevelButton.textContent = "Next Level"; popupShareButton.textContent = 'Share Score'; } congratsPopup.style.display = 'flex'; }
        function hideCongratsPopup() { if(congratsPopup) congratsPopup.style.display = 'none'; }
        function swapTiles(r1, c1, r2, c2, countMove = true) { [board[r1][c1], board[r2][c2]] = [board[r2][c2], board[r1][c1]]; if (board[r1][c1] === null) emptyTile = { r: r1, c: c1 }; else if (board[r2][c2] === null) emptyTile = { r: r2, c: c2 }; if (countMove) { moves++; updateMovesCounter(); if (gameActiveForTimer) renderBoard(); } }
        function updateMovesCounter() { if(movesCounterElement) movesCounterElement.textContent = `चालें: ${moves}`; }
        function checkWin() { let count = 1; for (let r = 0; r < GRID_SIZE; r++) { for (let c = 0; c < GRID_SIZE; c++) { if (r === GRID_SIZE - 1 && c === GRID_SIZE - 1) { if (board[r][c] !== null) return false; } else { if (board[r][c] !== count) return false; count++; } } } return true; }
        function startGameWithLevel(levelInput) { const targetLevel = parseInt(levelInput); if (isNaN(targetLevel) || targetLevel < 1 || targetLevel > MAX_LEVEL) { if(levelSelectMessage) levelSelectMessage.textContent = `अमान्य लेवल (1-${MAX_LEVEL} के बीच चुनें).`; return; } currentLevel = targetLevel; saveCurrentLevel(currentLevel); showGameScreen(); loadLevel(currentLevel); }
        function loadLevel(levelToLoad) { console.log(`Loading level: ${levelToLoad}`); hideCongratsPopup(); /* adOverlay check removed */ currentLevel = parseInt(levelToLoad); if(levelDisplayElement) levelDisplayElement.textContent = `लेवल: ${currentLevel}`; GRID_SIZE = getGridSizeForLevel(currentLevel); levelComplete = false; gameActiveForTimer = false; moves = 0; updateMovesCounter(); if(messageElement) messageElement.textContent = ''; if(puzzleBoard) { puzzleBoard.style.pointerEvents = 'auto'; puzzleBoard.style.opacity = '1'; } stopTimer(); elapsedTimeInSeconds = 0; updateTimerDisplay(); createBoard(); shuffleBoard(); renderBoard(); console.log(`Level ${currentLevel} loaded and rendered.`); }
        
        async function shareGame(isSharingScore = false) {
            const gameName = "Number Ninja Puzzle Game";
            const gameUrl = window.location.href;
            let textToShare = `मैंने अभी ${gameName} खेला! आप भी आजमाएं: ${gameUrl}`;

            if (isSharingScore) {
                textToShare = `मैंने ${gameName} में लेवल ${currentLevel} को ${moves} चालों और ${formatTime(elapsedTimeInSeconds)} समय में पूरा किया! क्या आप मुझे हरा सकते हैं? ${gameUrl}`;
            }

            if (navigator.share) {
                try {
                    await navigator.share({ title: gameName, text: textToShare, url: gameUrl, });
                    console.log('Game shared successfully');
                } catch (error) {
                    console.error('Error sharing the game:', error);
                    alert(`शेयर करने के लिए टेक्स्ट कॉपी करें:\n${textToShare}`);
                }
            } else {
                console.log('Web Share API not supported, fallback to alert.');
                try {
                    await navigator.clipboard.writeText(textToShare);
                    alert(`गेम का लिंक क्लिपबोर्ड पर कॉपी किया गया! इसे अपने दोस्तों के साथ साझा करें:\n${textToShare}`);
                } catch (err) {
                    alert(`शेयर करने के लिए टेक्स्ट कॉपी करें:\n${textToShare}`);
                }
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            console.log("DOM fully loaded and parsed.");
            assignDOMelements(); 
            
            currentLevel = loadSavedLevel();
            if(maxLevelDisplay) maxLevelDisplay.textContent = MAX_LEVEL.toString();

            function handleGameStartInteraction(level) { startGameWithLevel(level); }

            if (startGameButton) { startGameButton.addEventListener('click', () => { console.log("Start Game button clicked."); showLevelSelectionScreen(); }); } else { console.error("CRITICAL: startGameButton NOT FOUND."); }
            if (shareGameStartButton) { shareGameStartButton.addEventListener('click', () => shareGame(false));} else { console.error("Share Game Start Button not found.");}
            if (goToLevelButton && levelNumberInput) { goToLevelButton.addEventListener('click', () => { console.log("Go To Level button clicked."); handleGameStartInteraction(levelNumberInput.value); }); } else { console.error("Go To Level button or input not found."); }
            if (levelGroupButtons) { levelGroupButtons.forEach(button => { button.addEventListener('click', (e) => { const level = e.target.dataset.level; console.log(`Level group button clicked for level: ${level}`); if (level) { handleGameStartInteraction(level); } }); }); }
            if (gameBackArrow) { gameBackArrow.addEventListener('click', () => { console.log("Game Back Arrow clicked."); saveCurrentLevel(currentLevel); showLevelSelectionScreen(); }); } else { console.error("Game Back Arrow button not found."); }
            if (backToStartButton) { backToStartButton.addEventListener('click', () => { console.log("Back to Start button clicked."); showStartScreen(); }); } else { console.error("Back to Start button not found."); }
            if (resetButton) { resetButton.addEventListener('click', () => { console.log("Reset button clicked."); loadLevel(currentLevel); }); } else { console.error("Reset button not found."); }
            
            // Ad related event listener removed: closeAdButton
            
            if (popupNextLevelButton) {
                popupNextLevelButton.addEventListener('click', () => {
                    console.log("Popup Next Level button clicked.");
                    hideCongratsPopup(); 
                    if (currentLevel < MAX_LEVEL) {
                        startGameWithLevel(currentLevel + 1); // सीधे अगला लेवल शुरू करें
                    } else {
                        showStartScreen(); // या गेम समाप्त स्क्रीन
                    }
                });
            } else { console.error("Popup Next Level button not found."); }

            if (popupShareButton) {
                popupShareButton.addEventListener('click', () => shareGame(true));
            } else { console.error("Popup Share Button not found."); }
            
            showStartScreen();
        });
    </script>
</body>
</html>
