# AngryBird
Unity Game School portfolio : Angry Birds (Production time : 4 days)
## Demo Video
[![Video Label](https://img.youtube.com/vi/Cj3ggTdfJUs/0.jpg)](https://www.youtube.com/watch?v=Cj3ggTdfJUs)
## Goals for the portfolio
- Re-familiarize myself with Unity
- Apply what I learned in class
  - Manage and use hash values as static readonly data
  - Manage objects with C# List
  - Manage UI structure (using `transform.Find, onClick.AddListener`)
  - Optimize (`rigidbody.velocitiy.sqrMagnitude`)
- Using advanced syntax
  - Managing logic with Delegates
  - Using Lambda Expressions
- Using Cinemachine
## Things to fix and improve
- Consolidate data related to Bird into a [Dictionary](https://assetstore.unity.com/packages/tools/utilities/serialized-dictionary-243052?locale=ko-KR) and manage it in the inspector
  - Remove Switch statements using Enum
## Assets
### BGM
- Created by hand with AIVA
- Prompts : not heavy, fun, old west
- Theme : heavy rock ensemble
- Some direct modifications afterward for a natural loop
### 3D models (bird, pig)
- [External link](https://www.models-resource.com/mobile/angrybirdsgo/)
- 2D Angry Birds used for the button UI in the bottom right corner were taken and shared by a student at Unity Game School
### Sounds (excluding background music)  
- [External link](https://www.sounds-resource.com/mobile/angrybirdsepic/sound/3940/)
### Effects (skills, fire)
- Cartton FX Remaster Free [Asset Store (Free)](https://assetstore.unity.com/packages/vfx/particles/cartoon-fx-remaster-free-109565)
- Low Poly Fire [Asset Store (Free)](https://assetstore.unity.com/packages/vfx/particles/fire-explosions/low-poly-fire-244190)
### Map
- Low Poly Atmospheric Locations Pack [Asset Store (Free)](https://assetstore.unity.com/packages/3d/environments/landscapes/low-poly-atmospheric-locations-pack-278928)
- FREE Skybox Extended Shader [Asset Store (Free)](https://assetstore.unity.com/packages/vfx/shaders/free-skybox-extended-shader-107400)
- Map stages are placed by hand
### UI
- UI Ultimate Clean GUI Pack [Asset Store (Paid)](https://assetstore.unity.com/packages/2d/gui/ultimate-clean-gui-pack-154574)
## Description
- When the user presses the UI in the bottom right, the corresponding bird is added to the spawn list (top left toggle)
- Birds are created in order, and when one flies away, the next one is created.
- The yellow, black, and blue birds each have a skill and can be used by left-clicking while flying.
### BirdManager.cs
- Since we are creating birds dynamically, we have the data we need to do so.
- We use `Resources.Load` to get the bird prefab as a static structure and use it to create the bird.
- The `BirdColor` class and `BirdType` enumeration are used to interact with the created bird objects. (sounds, effects, etc.)
- Use the Queue structure to manage the creation of birds.
### BirdsUI.cs
- Uses a Queue structure to manage the toggle (list of birds to create).
- We need a parameter for the function to pass to the AddListener, so we wrapped it in a lambda expression once and then added it.
- Each time a bird is created, we move the toggle one space to the left. 
### BirdThrow.cs
- The default script attached to each bird's prefab. It is responsible for functions related to the behavior of throwing the bird. (before, during, and after flight).
- Checks the status of the bird using the bird's tags and releases it.
- Shows the expected path to the user in advance. The objects displayed as paths are created with Instantiate and managed with List.
