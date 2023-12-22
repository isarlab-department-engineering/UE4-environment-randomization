# UE4 Indoor Environment Randomization
UE4 blueprint for indoor environment randomization. Rooms and corridors shapes, walls and floor textures, furniture can be easily randomized at the beginning of the experiment or at run-time.

### Blueprint
Download the blueprint `DomainRandomizer.uasset` and move it into you `Content` folder (in your UE4 project).

### Event Graph
Everytime a new experiment starts (i.e., when Play is pressed), the `RandomizeAll` function is called. If `Debug Mode` and `Enable Tick` are both set to True, `RandomizeAll` is called every tick. `Debug Mode` and `Enable Tick` can be enabled or disabled inside the Blueprint.

### Functions
#### 1) RandomizeAll
The main component of the blueprint. It is called when Play is pressed or every tick, depending on the chosen mode. If `Debug Mode` is True, a random seed is set. Otherwise, the seed is set according to the `Seed` variable (initialized to 0, but may be changed via Python). This function autonomously call the following functions for the randomization.

#### 2) SpawnAndRandomizeRoom
This function's aim is to spawn the floor, the external walls and the ceiling, setting a random material. It contains the following variables:
- `Room Size`: environment size (in UE4 meters).
- `Floor/Wall/Plane Mesh`: mesh for the floor, the external wall and the ceiling.
- `Gather Train Set`: a different array of meshes can be used if this boolean value is set to True or to False.
- `Train/Test Materials`: material arrays (train and test materials can be different if needed).

#### 3) SpawnWalls
This function allows spawning internal walls and doors according to a grid, and avoids the creation of closed rooms. It contains several variables, but the following helps in building an appropriate room, depending on the task:
- `Wall Grid Size`: the room size increases by increasing this grid size.
- `Door Placement Change`: probability value to spawn a wall.

#### 4) SpawnDoors
This function adds the doors where walls have not been spawned (with a fixed probability). 
- `Door Placement Chance`: doors spawning probability.
- `Door Meshes`: meshes array for the doors.

#### 5) SpawnWallDecoBorders
The main function in charge of spawning external wall decorations.

#### 6) SpawnWallDecoBordersN
For the N-th external wall, this function spawns decorations so that they do not overlap and they are far enough from the doors.
- `Chance To Spawn Wall Deco`: probability value to spawn a wall decoration.
- `Wall Deco Height Ratio`: the height for the wall decorations.
- `Object Grid Ratio`: ratio between the object grid size and the wall grid size.

#### 7) SpawnWallDecoCentral
The main function in charge of spawning internal wall decorations.

#### 8) SpawnWallDecoCentral (HorizontalUp/Down, VerticalLeft/Right)
Four functions to spawn the decorations on the internal walls with a fixed probability and following the same constraints as before (the objects are spawned far enough each other and far enough from the doors).

#### 9) SpawnWallObjectsBorders
The main function in charge of spawning objects close to the external walls.

#### 10) SpawnWallObjectsBordersN
For the N-th external wall, this function spawns objects so that they do not overlap and they are far enough from the doors.
- `Change To Spawn Wall Object`: probability value to spawn an object close to the N-th external wall.
- `Wall Object Margin Factor`: if higher than 1, the objects will be a bit detached from the wall.
- `Train/Test Wall Object Meshes`: meshes array for the objects close to the walls. These meshes may vary for train and test sets.

#### 11) SpawnWallObjectsCentral
The main function in charge of spawning objects close to the internal walls.

#### 12) SpawnWallObjectsCentralX
Four functions to spawn the objects in the X internal wall.

#### 13) SpawnFloorObjects
This function is in charge of spawning objects in the middle of the free grid cells, with a random probability and a random yaw orientation (and far enough from the doors).
- `Change To Spawn Floor Object`: spawn probability for an object.
- `Train\Test Floor Object Meshes`: the object meshes may vary for train and test sets.

#### 14) SpawnRoofObjects
This function is in charge of spawning objects hanging from the ceiling.
- `Change To Spawn Roof Object`: spawn probability for an object.
- `Train\Test Roof Object Meshes`: the object meshes may vary for train and test sets.

#### 15) RandomizeLight
This functions randomizes the intensity and the orientation of the light.

### Usage
1) Open the UE4 project and drag the blueprint from the `Content` folder into an UE4 empty environment. 
2) Rename it `DomainRandomizer_PORT` (e.g., `DomainRandomizer_9734`).
3) From the menu, some parameters may be changed. To modify the other parameters, the meshes or the materials, access the blueprint (double click) > `Components` > `DomainRandomizer (self)`.
4) Set the parameter `Directional Light` to have the reference to the environment `Light Source`.
5) Blueprint is ready: press Play to create a randomized environment!

### Reference
If you find this work useful in your research, please cite:
```
@article{felicioni2023vision,
  title={Vision-based Topological Localization for MAVs},
  author={Felicioni, Simone and Rizzo, Biagio Maria and Tortorici, Claudio and Costante, Gabriele},
  journal={IEEE Robotics and Automation Letters},
  year={2023}
}
```
