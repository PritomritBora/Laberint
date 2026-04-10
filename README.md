# Maze Escape

A first-person 3D maze game built in Unity where players must solve riddles and escape before being caught by an AI-driven enemy.

## Overview

Maze Escape combines puzzle-solving, stealth, and adaptive AI into a single experience. The player navigates a procedurally structured maze, encounters holographic riddles, and must reach the exit — all while being hunted by an enemy that uses a scent-tracking system to find them.

The game features a dynamic difficulty system powered by a Behaviour Tree that monitors player progress and adjusts the challenge in real time.

## Features

- Adaptive difficulty via a Behaviour Tree (FluentBehaviourTree) — walls are removed to help a struggling player or to give the enemy an advantage if the player is progressing too fast
- Enemy AI using a Finite State Machine with scent-based player tracking via NavMesh
- Holographic riddles that animate when the player approaches, solved using voice input
- IBM Watson integration for Speech-to-Text and Tone Analysis, feeding into a chatbot assistant
- Multiple scenes: Start Menu, Maze, Mirror Maze, and End Menu
- Post-processing effects and hologram shaders for visual polish

## Scenes

| Scene | Description |
|---|---|
| StartMenu | Main menu entry point |
| NewMaze | Primary gameplay maze |
| MirrorMaze | Secondary maze variant |
| EndMenu | Game over / win screen |

## Tech Stack

- Unity (C#)
- IBM Watson SDK (Speech-to-Text, Tone Analyzer, Assistant)
- FluentBehaviourTree for enemy/game logic
- Unity NavMesh for enemy pathfinding
- ProBuilder for level geometry
- TextMesh Pro for UI text

## Project Structure

```
Assets/
├── Scripts/
│   ├── Assistant/        # Watson chatbot, speech-to-text, tone analysis
│   ├── Controller/
│   │   ├── Enemy/        # Enemy FSM, scent tracking, NavMesh movement
│   │   └── Player/       # Player health, scent, UI
│   ├── MazeAgent/        # Behaviour Tree, wall management, game state
│   ├── Riddles/          # Riddle logic and proximity detection
│   └── TimeController/   # Game timer
├── Scenes/               # Unity scene files
├── Prefab/               # Reusable game objects
├── Sounds/               # Audio assets
└── Watson/               # IBM Watson SDK
```

## Getting Started

### Prerequisites

- Unity 2019.x or later
- IBM Watson Unity SDK
- An IBM Cloud account with the following services configured:
  - Speech to Text
  - Tone Analyzer
  - Watson Assistant

### Setup

1. Clone the repository
2. Open the project in Unity
3. Add your IBM Watson credentials to the relevant components in the Inspector:
   - `SpeechToTextController` — Speech to Text credentials
   - `ChatBotController` — Tone Analyzer credentials + chatbot URL
4. Open `StartMenu.unity` and press Play

## Gameplay

- Move with `WASD`, look with the mouse
- Approach a holographic riddle to activate it — answer it using your voice
- Avoid the enemy, which tracks you by scent
- Reach the exit gate to win
- If the enemy catches you, the game ends

## Adaptive Difficulty

Every 10 seconds the Behaviour Tree evaluates player progress:

- If the player is stuck or moving away from the goal, a wall is removed to open a shorter path
- If the player is advancing too quickly, a wall is removed near the enemy to give it a shortcut
- If the enemy reaches the player, the game ends immediately
