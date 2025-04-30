# TopDownTankGame
This project is a simple top-down 2D tank battle game implemented in C++, featuring object-oriented programming (OOP) principles, file I/O, polymorphism, and dynamic memory management. The game allows two players to control tanks based on the game "Tank Trouble".

Gameplay Highlights
⚔️ Dual-Player Combat
Player 1: Controls their tank with WASD (movement) + SPACE (shoot).
Player 2: Uses Arrow Keys (movement) + ENTER (shoot).
10 lives per player – last tank standing wins!

Progression & Persistence
GameState is stored in a file, allowing the players to pick up where they left off.

Inheritance Hierarchy Implementation
The project implements a three-level inheritance hierarchy to maintain clean object relationships. The GameObject abstract base class defines core game loop methods (update(), render()) but cannot be instantiated directly. The Tank class inherits from GameObject and provides shared functionality like movement, collision detection, and health management. Finally, PlayerOneTank and PlayerTwoTank (filenames: playerOne, playerTwo) derive from Tank, specializing controls for:

Player 1: WASD + SPACE (file: playerOne.o)
Player 2: Arrow Keys + ENTER (file: playerTwo.o)

This hierarchy ensures polymorphic behavior—e.g., both player tanks are stored in a std::vector<GameObject*> and processed identically during updates.

Polymorphism & Abstract Classes
The GameObject abstract class (files: Tank, Tank.o) enforces a consistent interface via:
virtual void update() = 0;  // Handles input/movement (files: movement.o, playerOne.o, playerTwo.o)  
virtual void render() = 0;  // Draws tank sprites (files: tankBlue, tankRed, tankBarrelBlue, tankBarrelRed)  
Polymorphism is demonstrated when the game loop calls these methods on all GameObject instances (players, projectiles) without knowing their concrete types.

Dynamic Memory Management
Heap memory manages projectiles (files: Shooting, Shooting.o):
Allocation: Projectile* bullet = new Projectile() when players fire.
Storage: Active bullets are tracked in a std::vector<Projectile*>.
Cleanup: Bullets are deleted upon hitting a tank or leaving bounds (collision logic in movement.o).
This ensures efficient memory use during rapid firing.

Key File References
Tank Assets: tankBlue, tankRed, tankBarrelBlue, tankBarrelRed (player sprites)
Game Logic: game, game_data, GameData.o (manages scores/rounds)
UI: menu.o, endScreen.o (menus and win/loss screens)
Testing: test_movement, test_playerOne, test_playerTwo (validation)
