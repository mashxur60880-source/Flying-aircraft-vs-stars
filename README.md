# Flying-aircraft-vs-stars
Browser-based sci-fi arcade shooter featuring a futuristic aircraft, hostile stars, five campaign missions, boss battles, and virtual rewards. Built with Phaser 3, TypeScript, and Vite.
Flying Aircraft vs. Stars
Game Design Document & Technical Specification
Project Version: 1.0
Platform: Web Browser (HTML5)
Genre: Space Arcade Shooter
Visual Style: Realistic Science Fiction
Game Modes: Campaign Levels and Boss Battles
Rewards: Virtual In-Game Rewards
Project Status: Pre-development / Technical Planning
⸻
1. Project Overview
Flying Aircraft vs. Stars is a browser-based space arcade shooter in which the player controls a futuristic combat aircraft traveling through dangerous regions of the galaxy.
Hostile stellar entities attack the player’s ship, block flight paths, and use different movement patterns and projectile attacks.
The player must dodge enemies, shoot them down, collect bonuses, defeat bosses, earn virtual currency, upgrade the aircraft, and unlock new missions.
Main Objectives
Create an easy-to-learn but challenging arcade experience.
Implement responsive controls for desktop and mobile browsers.
Provide five progressive campaign missions with unique bosses.
Introduce a virtual reward and upgrade system.
Save local player progress.
Deliver a performant, browser-based game without requiring installation.
Core Gameplay Loop
Open the main menu.
Select an available mission.
Fly through the level and destroy enemies.
Collect bonuses and virtual coins.
Fight and defeat the level boss.
Calculate the mission score and grant rewards.
Upgrade the aircraft and unlock new content.
Start the next mission.
Core design principle: The game should be easy to start, increasingly challenging, and rewarding through clear objectives, progression, and unlockable content.
⸻
2. Technical Stack
The recommended technology stack for the first release is a browser-based game built with TypeScript and Phaser.
Component	Recommended Technology
Programming language	TypeScript
Game framework	Phaser 3
Rendering	WebGL with Canvas fallback
User interface	HTML5 and CSS
Build tool	Vite
Version control	Git
Local progress storage	localStorage, with save-data versioning
Unit testing	Vitest
Browser testing	Playwright
Hosting	Static web hosting with HTTPS
Why Phaser?
Phaser is suitable for a 2D arcade shooter with smooth movement, collision detection, animations, particle effects, and responsive controls.
A realistic science-fiction appearance can be achieved through detailed aircraft artwork, dynamic lighting, layered parallax backgrounds, high-quality textures, and visual effects. A full 3D engine is not required for the initial version.
Browser Compatibility
The game should support modern desktop and mobile browsers.
Initial targets:
Google Chrome
Microsoft Edge
Mozilla Firefox
Safari
Mobile Chrome on Android
Mobile Safari on iOS
The first release will be a single-player game. An application server and account registration are not required at this stage.
⸻
3. Gameplay Mechanics
3.1. Player Aircraft
Entity: PlayerShip
The player controls a futuristic combat aircraft equipped with laser weapons and an energy-based defense system.
Controls
Mouse movement on desktop.
Touch movement on mobile devices.
Optional WASD and arrow-key controls.
Automatic firing by default.
A dedicated button for activating special abilities.
Movement restricted to the boundaries of the playable area.
Temporary invulnerability after taking damage.
Initial Balancing Parameters
Parameter	Initial Value
Player health	100 HP
Movement speed	360 px/s
Laser damage	10 HP per hit
Firing interval	0.25 seconds
Invulnerability after damage	1.2 seconds
Special ability cooldown	12 seconds
These values are provisional balancing parameters and must be validated through gameplay testing.
3.2. Enemy Types
Class A — Stellar Drone
Role: Basic enemy
Health: 20 HP.
Movement speed: Low.
Moves in a straight line or a smooth curved trajectory.
Designed to introduce basic combat mechanics.
Appears in the first mission.
Awards 10 score points when destroyed.
Class B — Hunter Star
Role: Fast and maneuverable enemy
Health: 35 HP.
Movement speed: High.
Changes trajectory periodically.
Attempts to intercept or pursue the player’s aircraft.
Introduced in the second mission.
Awards 25 score points when destroyed.
Class C — Stellar Overlord
Role: Main boss
Initial health: 1,500 HP.
Uses multiple attack phases.
Fires projectile spreads.
Creates hazardous areas.
Summons additional enemies.
Awards a major reward when defeated.
Boss health, attack damage, and attack frequency must be adjusted during balancing and playtesting.
3.3. Shooting and Collision Detection
The combat system must follow these rules:
The aircraft fires laser projectiles at a configurable interval.
Each projectile travels in the appropriate direction.
Projectiles are removed when they hit a target or leave the playable area.
A successful hit reduces the target’s health.
When an enemy is destroyed, a destruction animation plays.
Defeated enemies may drop rewards according to configurable probabilities.
Collisions damage the player’s aircraft.
A visual damage effect and temporary invulnerability period are triggered after a hit.
When player health reaches zero, the game pauses and displays the defeat screen.
Object pooling should be used for frequently created objects such as projectiles, particles, and standard enemies to reduce unnecessary allocations and improve performance.
3.4. Power-Ups
Energy Shield
Grants temporary protection.
Absorbs incoming damage for 5 seconds.
Displays a visual shield effect while active.
Weapon Enhancement
Activates triple-shot firing.
Lasts 8 seconds.
Uses a distinct visual effect.
Space Coins
Virtual currency used to purchase upgrades and cosmetic aircraft skins.
Collected during missions.
Repair Module
Restores 25 HP.
Cannot increase player health above 100 HP.
All power-up durations, effects, and drop probabilities should be configurable through game data.
⸻
4. Campaign Progression: Five Missions and Five Bosses
Mission	Location	New Mechanics	Boss
1	Earth Orbit	Basic enemies and movement tutorial	Stellar Drone
2	Nebula	Pursuing and fast-moving enemies	Hunter
3	Asteroid Belt	Obstacles and narrow flight paths	Destroyer
4	Outer Galaxy	Dense enemy waves and hazardous zones	Plasma Guardian
5	Stellar Core	Multi-phase boss encounters	Stellar Overlord
Each mission should contain:
An introductory sequence.
Several waves of enemies.
A short transition before the boss fight.
A boss encounter.
A victory or defeat screen.
Mission rewards and progression updates.
Defeating a boss unlocks the next mission and its associated rewards.
Boss Battle Design
Phase 1 — Introduction
The boss uses basic projectile attacks to teach the player how to read attack trajectories.
Phase 2 — Increased Pressure
The boss fires projectile spreads and summons additional enemies.
Phase 3 — Final Assault
Attack speed increases, hazardous zones become more dangerous, and the safe movement area becomes more restricted.
Boss phase transitions should be triggered by health thresholds rather than timers. This makes encounters more predictable and prevents sudden difficulty spikes unrelated to player performance.
⸻
5. Project Directory Structure
Recommended source-code organization:
flying-aircraft-vs-stars/
├── public/
│   ├── assets/
│   │   ├── backgrounds/
│   │   ├── ships/
│   │   ├── enemies/
│   │   ├── bosses/
│   │   ├── projectiles/
│   │   ├── effects/
│   │   ├── powerups/
│   │   ├── ui/
│   │   └── audio/
│   └── favicon.ico
├── src/
│   ├── main.ts
│   ├── config/
│   │   └── gameConfig.ts
│   ├── scenes/
│   │   ├── BootScene.ts
│   │   ├── PreloadScene.ts
│   │   ├── MenuScene.ts
│   │   ├── HangarScene.ts
│   │   ├── MissionScene.ts
│   │   ├── BossScene.ts
│   │   ├── ResultsScene.ts
│   │   └── UpgradeScene.ts
│   ├── entities/
│   │   ├── PlayerShip.ts
│   │   ├── Enemy.ts
│   │   ├── Boss.ts
│   │   ├── Projectile.ts
│   │   └── PowerUp.ts
│   ├── systems/
│   │   ├── CombatSystem.ts
│   │   ├── CollisionSystem.ts
│   │   ├── SpawnSystem.ts
│   │   ├── RewardSystem.ts
│   │   ├── ProgressionSystem.ts
│   │   └── SaveSystem.ts
│   ├── ui/
│   ├── data/
│   │   ├── missions.ts
│   │   ├── enemies.ts
│   │   └── rewards.ts
│   ├── types/
│   └── styles/
├── tests/
│   ├── combat.test.ts
│   ├── rewards.test.ts
│   └── saves.test.ts
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
Architecture Responsibilities
scenes/ — Game screens and scene transitions.
entities/ — Aircraft, enemies, bosses, projectiles, and power-ups.
systems/ — Combat, spawning, rewards, progression, and saving.
data/ — Mission, enemy, and reward configuration.
tests/ — Automated checks for critical gameplay systems.
Separating configuration from gameplay logic makes it possible to adjust enemy speed, boss health, reward amounts, and upgrade prices without rewriting the core systems.
⸻
6. Graphics and Audio Asset Inventory
The following inventory defines the assets required for the MVP. It is a production checklist, not a statement that these assets have already been created.
Asset Category	Required Assets	Estimated MVP Quantity
Backgrounds	Space, nebula, asteroid belt, galaxy, stellar core	5
Player aircraft	Main hull, engine effect, damaged state	3
Aircraft skins	Dark and premium variants	2
Standard enemies	Stellar Drone and Hunter Star	2
Bosses	Five visually distinct bosses	5
Projectiles	Player laser and three enemy attack types	4
Power-ups	Coin, shield, weapon boost, repair module	4
Visual effects	Explosion, hit, boost, shield, boss destruction	5
UI components	Icons, health bars, buttons, panels	15–25
Game screens	Menu, hangar, mission, pause, victory, defeat, upgrades	7
Audio	Lasers, explosions, coin collection, damage, victory, menu, boss	10–15 files
Asset Specifications
Design the primary gameplay layout around a 16:9 aspect ratio while supporting portrait mobile screens.
Use WebP or PNG for backgrounds and transparent game sprites.
Use texture atlases with JSON frame metadata for animated sprites.
Prefer sprite-based and particle-based effects over heavy video assets.
Use OGG audio files with an appropriate fallback format.
Select readable UI fonts with full Cyrillic support if Russian localization is planned.
Maintain consistent naming conventions and asset dimensions.
Example filenames:
player_fighter_idle.webp
enemy_hunter_move.webp
boss_overlord_phase2.webp
fx_ship_explosion.webp
ui_health_bar.webp
sfx_laser.ogg
Texture atlases and compressed assets should be used where appropriate to reduce loading overhead and improve performance on mobile networks.
All third-party assets must have appropriate usage and redistribution rights. Custom-created assets should be stored with their source files and relevant licensing information when applicable.
⸻
7. Virtual Reward Economy
The in-game currency has no real-world monetary value and cannot be exchanged for real money.
Reward Table
Action	Reward
Destroy a standard star	10 score points
Destroy a fast star	25 score points
Collect a coin	5 coins
Complete a mission	100 coins
Defeat a boss	300 coins
Complete a mission without losing health	150 bonus coins
Complete all five missions	Unique aircraft skin
The reward system must prevent players from receiving duplicate completion rewards after refreshing or reloading the page.
Persistent Player Data
The local save system should store:
Save-data schema version.
Unlocked missions.
Current coin balance.
Purchased upgrades and skins.
Best scores.
Completed achievements.
Save-System Limitations
localStorage is suitable for local progress in a single-player browser game, but it does not prevent users from modifying their saved data.
A server-side validation system will be required if the project later introduces competitive online tournaments or a global leaderboard that must resist score manipulation.
⸻
8. Implementation Roadmap
Estimated schedule for one developer familiar with TypeScript and Phaser, assuming graphics are ready or sourced separately.
Week 1 — Project Setup
Tasks:
Create the Git repository.
Configure TypeScript, Phaser, and Vite.
Set up the game canvas and responsive layout.
Implement asset loading.
Create the initial menu.
Deliverable: A runnable project skeleton.
Week 2 — Core Gameplay
Tasks:
Implement player movement.
Add automatic shooting.
Create enemy spawning.
Implement projectiles and collision detection.
Add player health, defeat, and restart logic.
Deliverable: A playable combat prototype.
Week 3 — Missions and Bosses
Tasks:
Implement five campaign missions.
Configure enemy waves.
Add boss health bars and attack phases.
Implement mission transitions.
Add victory and defeat conditions.
Deliverable: A complete playable campaign structure.
Week 4 — Graphics, Rewards, and Progression
Tasks:
Integrate final graphics and visual effects.
Add sound effects.
Implement coins and power-ups.
Add aircraft upgrades and skins.
Implement local save functionality.
Deliverable: A complete gameplay loop.
Week 5 — Testing and Release Preparation
Tasks:
Test desktop and mobile browsers.
Validate save and reward logic.
Balance difficulty and combat.
Check performance and loading times.
Fix gameplay and UI defects.
Prepare deployment over HTTPS.
Deliverable: A release candidate ready for final review.
The five-week schedule is an estimate, not a guarantee. Creating original realistic artwork, animation, and audio may extend the development period.
⸻
9. Acceptance Criteria
The first release is considered ready for acceptance when the following requirements are satisfied.
☐ The game launches from a browser URL without installation.
☐ Mouse, keyboard, and touch controls work correctly.
☐ The aircraft can shoot, receive damage, and be destroyed.
☐ Enemies and projectiles are removed correctly after collisions.
☐ All five missions and five bosses are playable and completable.
☐ Power-ups, coins, and upgrades follow the defined rules.
☐ Player progress persists after reloading the page.
☐ Pause, victory, defeat, and restart flows work correctly.
☐ The UI adapts to different screen sizes.
☐ No critical runtime errors remain in the browser console.
Automated tests should cover combat calculations, reward distribution, progression, and save-data handling.
⸻
10. Recommended Next Development Step: MVP Vertical Slice
The next step is to create a working prototype rather than immediately building the entire campaign.
The initial MVP vertical slice should include:
A Phaser + TypeScript + Vite source project.
Instructions for running the game locally.
One functional gameplay scene.
One controllable aircraft.
Two standard enemy types.
Working shooting and collision mechanics.
Collectible coins and at least one power-up.
One functional boss encounter.
Victory and defeat screens.
Automated tests for damage and reward calculations.
Once the prototype has been tested and the core gameplay has been validated, the project can expand to all five missions, additional bosses, final realistic artwork, and the full upgrade system.
Avoid purchasing or commissioning a large quantity of final artwork before confirming that the core gameplay is enjoyable and technically stable. Temporary placeholder assets can be used during the initial implementation.
⸻
11. Project Status and Scope
This document defines the proposed technical architecture, gameplay mechanics, asset requirements, development roadmap, and acceptance criteria.
The game has not yet been implemented. The next deliverable should be a runnable source-code prototype that can be tested in a browser.
Initial Release Scope
Browser-based single-player gameplay.
Five campaign missions.
Five boss encounters.
Responsive desktop and mobile controls.
Virtual currency and power-ups.
Aircraft skins and upgrades.
Local progress saving.
No mandatory user accounts.
No real-money rewards or cash-out mechanics.
No online leaderboard in the initial MVP.
Future Enhancements
Possible post-release features include:
Global leaderboards backed by a server.
Daily missions and challenges.
Additional aircraft and enemy types.
More campaign chapters.
Cloud saves and player accounts.
Additional localization options.
Performance and accessibility improvements.
⸻
12. Definition of Done
The project is ready for its initial public release when:
The production build completes successfully.
The game is deployed to a public HTTPS URL.
All five missions are playable.
Boss battles, rewards, upgrades, and saving work correctly.
Desktop and mobile browser testing is complete.
Critical bugs have been resolved.
The repository contains setup instructions and project documentation.
All distributed assets have appropriate usage rights.
Final objective: Deliver a stable, visually polished browser game with engaging space combat, progressive difficulty, boss battles, and a reliable virtual reward system.
