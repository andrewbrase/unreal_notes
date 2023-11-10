### Class
- *A Class defines the behaviors and properties of a particular Actor or Object in Unreal Engine*. Classes are hierarchical, meaning a Class inherits information from its parent Class (that is, the Class it was derived or "sub-classed" from) and passes that information to its children. Classes can be created in C++ code or in Blueprints.
---
### Objects
- Objects are the most basic class in Unreal Engine - in other words, *they act like building blocks and contain a lot of the essential functionality for your Assets*. Almost everything in Unreal Engine inherits (or gets some functionality) from an Object.

- `Uobject` - the base class of all objects in Unreal Engine
    - it implements features such as 
        - garbage collections
        - metadata (UProperty) support for exposing variables to Unreal Editor
        - serialization for loading and saving
---
### Actors
- *An Actor is any object that can be placed into a level*, such as a Camera, static mesh, or player start location. Actors support 3D transformations such as translation, rotation, and scaling. They can be created (spawned) and destroyed through gameplay code (C++ or Blueprints).

- `AActor` - the base class of all Actors in Unreal Engine
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