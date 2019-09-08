# Plan

## Simulation

- Find if can be run inside docker. (YES)
    - Write requirements for sending bots
- Run simulations on demand in the cloud.
    - Evaluate Fargate (NO)
    - EC2 instances (OK)
- Prepare a visualization tool for the results. (DONE)


Required

- Players must be able to :
  - upload their bot. (OK)
  - old bots should be removed. (OK)
  - download their own game logs. (OK)
  - check the global ranking. (OK)

## Material

- Prepare instructions to install (OK)
  - Halite (OK)
  - Visualizer (OK)
- Prepare some material (videos/ documents) for the sessions
  - Base game logic
  - Vector math
  - Path finding
  - Game strategies

### Video

#### Presentation

Halite is an open source artificial intelligence programming challenge, created by Two Sigma, where players build bots using the coding language of their choice to battle on a two-dimensional virtual board.

This contest will be based on Halite 2, Your mission is to extract Halite. Bots control ships that dock on and mine planets, producing more ships to defeat opponents. To achieve victory, you will need optimal pathfinding and swarm control to move efficiently from planet to planet and destroy enemy ships.

#### Tutorial

This is the game map, (show map) and you can see identify two player ships and different sized planets.

At the begging of the match, you start with 3 ships at the opposite side of you opponent in a symmetric randomly generated map. You move the ships around the map using three commands

- Move in a given angle and velocity.
- Dock in a planet
- Undock from the planet

You can conquer planets by docking ships on them. Planets ship production is relative to the number of docked ships. As big planets allow more docked ships, the production of a big planet is higher than a small planet.

When ships enter in shotting range, they fire to each other. After 3 shots, the ships die. In case of having multiple ships in shotting range, the damage is evenly spread between targets. Also if two ships collide, both ships are destroyed independently of the remaining life. Ships docked in a planet can not defend themselves, so other ships must protect them.

When all the docked ships in a planet die. the planet can be conquered again by any of the player.

The game finishes when there is only one player left.

#### Challenges

The game provides two main challenges.

##### Pathfinding

Finding the path from the ship position to the desired location is the first challenge that must be resolved. Knowing the position of every obstacle in the game, your algorithm must be able to generate the next step movement

#### Technics

With this simple rule set, there can be a lot of possibilities. I would like to see the strategies developed by the participants and to learn a lot in the process.

## Organization

- Find the appropriate community to host the event.

### Schedule

#### 4th September - Kickoff

This session will cover the following topics

- Game rules
- Development environment setup
- Basic vector math oriented to 2D game development.

#### 18th September - First Checkpoint

This session will cover the following topics

- First match between bots.
- Sharing bots with other players.
- Sharing "learns" from the first two weeks development
- Path finding in 2D worlds.

#### 9th October - Round 1

This session will cover the following topics

- First competition
- Talk about different game strategies from the most successfully bots
- Sharing bots with other players.

#### 6h November - Round 2

This session will cover the following topics

- Second competition
- Talk about different game strategies from the most successfully bots
- Sharing bots with other players.

#### 4th December - Round 3

This session will cover the following topics

- Third competition
- Talk about different game strategies from the most successfully bots
- Sharing bots with other players.
- Winner will be declared.
  - Best Bot.
    - Winner of the last round.
  - Most Amazing winning replay.
    - From the downloaded replays, each player will be able to submit one for ranking and the most amazing wining based on popular opinion will be chosen.
