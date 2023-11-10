### Foundational Knowledge
---
### Class
- *A Class defines the behaviors and properties of a particular Actor or Object in Unreal Engine*. Classes are hierarchical, meaning a Class inherits information from its parent Class (that is, the Class it was derived or "sub-classed" from) and passes that information to its children. Classes can be created in C++ code or in Blueprints.
---
### Objects
- Objects are the most basic class in Unreal Engine - in other words, *they act like building blocks and contain a lot of the essential functionality for your Assets*. Almost everything in Unreal Engine inherits (or gets some functionality) from an Object.

- it implements features such as 
    - garbage collections
    - metadata (UProperty) support for exposing variables to Unreal Editor
    - serialization for loading and saving

`Uobject` - the base class of all objects in Unreal Engine

---
### Actors
- *An Actor is any object that can be placed into a level*, such as a Camera, static mesh, or player start location. Actors support 3D transformations such as translation, rotation, and scaling. They can be created (spawned) and destroyed through gameplay code (C++ or Blueprints).

`AActor` - the base class of all Actors in Unreal Engine

---
### Casting
- Casting is an action that *takes an Actor of a specific class and tries to treat it as if it were of a different class*. Casting can succeed or fail. If casting succeeds, you can then access class-specific functionality on the Actor you cast to.

- For example, let's say you're making a game where you have multiple types of Volumes that can affect the player character in different ways. One of these volumes is Fire, which decreases player health over time. When the player overlaps with any Volume in the Level, you can cast that Volume to Fire to try to access its ""damage player health"" functionality.

- Casting is different from simply checking whether an Actor is of a given class, which would return a binary (yes or no) answer, but wouldn't allow you to interact with any specific functionality of that class.
---
### Component
- *A component is a piece of functionality that can be added to an actor*
    - When you add a component to an actor, the actor can use the functionality that the component provides. For example...
        - A Spot Light Component will *make your Actor emit light like a spot light.*
        - A Rotating Movement Component will *make your Actor spin around.*
        - An Audio Component will *give your Actor the ability to play sounds.*
    - **Components must be attached to an Actor and can't exist by themselves.**
---
### Pawn
- Pawns are a subclass actor and server as an in-game avatar or persona (for example, the characters in a game) *Pawns can be controlled by a player* or *by the games AI, as a non-playable character (NPC)*
    - When a pawn is controlled by a human or AI player, it is considered *Possessed*
    - When a pawn is NOT controlled it is considered *Unpossessed*
---
### Character
- A character is a subclass of a Pawn Actor that is intended to be used as a player character.
- The Character subclass includes a collision setup, input bindings for bipedal movement, and additional code for player-controlled movement.
---
### Player Controller
- A *player controller* takes **player input** and *translates it into interactions in the game*.
- Every game has at least one player controller in it.
    - A Player Controller often possesses a Pawn or Character as a representation of the player in game. 
    - The Player Controller is also the primary network interaction point for multiplayer games. During multiplayer play, the server has one instance of a Player Controller for every player in the game since it must be able to make network function calls to each player. Each client only has the Player Controller that corresponds to their player and can only use their Player Controller to communicate with the server.

The associated C++ class is `PlayerController`

---
### AI Controller
- Just as the Player Controller possesses a Pawn as a representation of the player in a game, an AI Controller possesses a Pawn to represent a non-player character (NPC) in a game. By default, Pawns and Characters will end up with a base AI Controller unless they are specifically possessed by a Player Controller or told not to create an AI Controller for themselves.

The associated C++ class is `AIController`

---
### Player State
- A Player State is the state of a participant in the game, such as a human player or a bot that is simulating a player. Non-player AI that exists as part of the game world doesn't have a Player State.

- Some examples of player information that the Player State can contain include:
    - Name
    - Current level
    - Health
    - Score
    - Whether they are currently carrying the flag in a Capture the Flag game.

- For multiplayer games, Player States for all players exist on all machines and can replicate data from the server to the client to keep things in sync. This is different from a Player Controller, which will only exist on the machine of the player it represents.

The associated C++ class is `PlayerState`

---
### Game Mode
- The *Game mode* sets the rules of the game that is being played. These can include...
    - How players join the game
    - Whether or not the game can be paused
    - Any game-specific behavior such as win conditions

*self* Like Fall Guys Game Modes

- *You can set the default Game Mode in the Project Settings and override it for different Levels.* Regardless of how you choose to implement it, you can only have one Game Mode for each Level.

- In a multiplayer game, the Game Mode only exists on the server and the rules are replicated (sent) to each of the connected clients.

The associated C++ class is `GameMode`

---
### Game State
- A Game State is a container that holds information you want replicated to every client in a game. In simpler terms, it is 'The State of the Game' for everyone connected.

*self* Like Score boards

- Some examples of what the Game State can contain include:
    - Information about the game score.
    - Whether a match has started or not.
    - How many AI characters to spawn based on the number of players in the world.

- For multiplayer games, there is one local instance of the Game State on each player's machine. Local Game State instances get their updated information from the server's instance of the Game State.
 
The associated C++ class is `GameState`

---
### Brush
- A Brush is an Actor that describes a 3D shape, such as a cube or a sphere. You can place brushes in a level to define level geometry (these are known as Binary Space Partition or BSP brushes). This is useful if you want to quickly block out a level, for example.

---
### Volume
- Volumes are bounded 3D spaces that have different uses based on the effects attached to them. For example:

    - Blocking Volumes are invisible and used to prevent Actors from passing through them.
    - Pain Causing Volumes cause damage over time to any Actor that overlaps them.
    - Trigger Volumes are programmed to cause events when an Actor enters or exits them.

*self* Fire area

---
### Level
- A Level is a gameplay area that you define. Levels contain everything a player can see and interact with, such as geometry, Pawns, and Actors.

- Unreal Engine saves each level as a separate `.umap` file, which is why you will sometimes see them referred to as Maps.

---
### World
- A World is a container for all the Levels that make up your game. It handles the streaming of Levels and the spawning (creation) of dynamic Actors.
