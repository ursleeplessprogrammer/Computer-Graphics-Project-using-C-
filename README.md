
# 🎮 3D Computer Graphics Project — C#

<p align="center">
  <strong>A Collaborative 3D Computer Graphics Project</strong><br>
  Developed using C# and Visual Studio 2022
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Language-C#-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" />
  <img src="https://img.shields.io/badge/IDE-Visual%20Studio%202022-5C2D91?style=for-the-badge&logo=visualstudio&logoColor=white" />
  <img src="https://img.shields.io/badge/Graphics-OpenGL-5586A4?style=for-the-badge&logo=opengl&logoColor=white" />
  <img src="https://img.shields.io/badge/3D%20Modeling-Blender-E87D0D?style=for-the-badge&logo=blender&logoColor=white" />
</p>

---

## 📌 About the Project

This project was developed as part of a Computer Graphics course at Petra Christian University in 2022. It was a collaborative project focused on applying fundamental 3D computer graphics concepts through the development of an interactive 3D environment.

The application combines camera manipulation, lighting techniques, collision detection, and 3D model rendering to create an environment that users can explore from different perspectives.

Rather than focusing solely on the visual result, the project provided practical experience in understanding how different graphics components work together, from processing 3D models to rendering objects and handling user interaction.

## ✨ Key Features

- **Multiple Camera Perspectives** — Third-person, first-person, CCTV, and fixed viewpoints.
- **Interactive Character Movement** — Camera-relative movement and character switching.
- **Dynamic Lighting** — Point lights, spotlights, and a player-controlled flashlight.
- **Collision Detection** — Bounding-box-based collision handling for environmental objects.
- **Custom 3D Model Loading** — Loading and processing Wavefront OBJ models.
- **GPU-Based Rendering** — Vertex Buffer Objects (VBOs), Vertex Array Objects (VAOs), and shaders.
- **Interactive Environment** — Keyboard and mouse controls for navigating and modifying the scene.

---

## ⚙️ Technical Implementation

### 1. Camera System

The application implements multiple camera perspectives, each with its own position, orientation, and movement behavior.

#### Third-Person Camera

The third-person camera follows the player character while maintaining a defined distance and viewing angle.

- Uses the character as its reference point.
- Mouse movement controls horizontal and vertical camera rotation.
- Horizontal rotation is handled through yaw, while vertical rotation uses pitch or angle constraints.
- Vertical camera movement is restricted by upper and lower angle limits.
- Character movement is calculated relative to the camera's horizontal orientation.
- Uses directional vector calculations to translate keyboard input into world-space movement.

#### First-Person Camera

The first-person camera provides a viewpoint from the player's perspective.

- Uses yaw and pitch values to determine the viewing direction.
- Calculates forward and right movement directions using camera vectors.
- Uses cross-product calculations to derive perpendicular directional vectors.
- Allows movement relative to the camera's current orientation.

#### CCTV Camera System

Four fixed CCTV viewpoints are implemented to observe different areas of the environment.

| Key | Camera Location |
|---|---|
| H | Storage Room |
| J | Hall / Stage |
| K | Right Hallway |
| L | Left Hallway |

Each CCTV camera has a predefined position and viewing direction. Mouse movement can adjust its viewing direction within the permitted range.

#### Additional Camera Perspectives

- **Freddy POV:** A fixed camera viewpoint positioned around the stage.
- **Character Switching:** Allows switching between the player character and Freddy while maintaining their respective camera positions.

### 2. Lighting System

The environment uses multiple lighting sources to illuminate objects and create different lighting conditions across the scene.

#### Point Lighting

Point lights illuminate surrounding objects from specific positions. They are distributed across several areas:

- Office
- Left and right hallways
- Storage room
- Room 1 and Room 2
- Main hall
- Stage area

#### Spot Lighting

Spotlights provide directional illumination within a defined area.

- Three spotlights illuminate the stage and Freddy.
- Two red point lights are positioned behind the stage.
- A separate yellow spotlight functions as the player's flashlight.

#### Dynamic Flashlight

The flashlight follows the player's position and viewing direction.

- Its position changes according to the player's movement.
- Its illumination direction follows the camera's orientation.
- Can be independently enabled or disabled.

#### Lighting Controls

The application supports interactive lighting controls:

- Toggle environmental lighting.
- Toggle the player's flashlight.
- Adjust the main hall light position along the X, Y, and Z axes.

These controls allow the lighting configuration to be changed while observing the effect on the rendered environment.

### 3. Collision Detection

Collision detection is implemented to prevent the player character from moving through environmental objects.

The project uses a **bounding-box-based collision detection approach**.

The general process consists of:

1. Calculate the minimum and maximum X and Z coordinates of the character's bounding box.
2. Calculate the corresponding boundaries of the target object.
3. Compare the two bounding boxes to determine whether they overlap.
4. Check the proposed character movement against the collision boundaries.
5. Prevent the movement when an overlap is detected.

This approach provides a straightforward method of handling environmental collisions without requiring a full physics simulation.

### 4. 3D Model Loading and Rendering

The project implements a custom Wavefront OBJ model-loading process to import external 3D objects into the application.

#### Model Processing

The model loader processes vertex positions and normal-vector information from OBJ files.

- Reads vertex position data.
- Processes normal-vector information used for surface lighting.
- Handles normal indices through an additional `indices_n` structure.
- Combines vertex positions and normal vectors into the final vertex data.
- Prepares the processed data for GPU rendering.

#### GPU Rendering Pipeline

The processed model data is transferred to the GPU using OpenGL buffer objects.

| Component | Purpose |
|---|---|
| **VBO (Vertex Buffer Object)** | Stores vertex data for GPU access. |
| **VAO (Vertex Array Object)** | Stores vertex attribute configuration and references the associated buffer data. |
| **Shaders** | Process vertex and fragment information during rendering. |
| **Rendering Pipeline** | Uses the configured geometry and shaders to display 3D objects. |

This implementation allows external 3D models to be loaded and rendered within the application instead of relying entirely on manually defined geometry.

### 5. 3D Asset Creation

Blender was used to design and prepare the 3D objects used throughout the environment.

The modeling process involved:

- Basic mesh manipulation.
- Working with primitive objects such as cubes and spheres.
- Editing and preparing individual 3D objects.
- Exporting objects separately to allow independent usage and color assignment.

Separating the models also made it easier to organize the environment and manage individual objects during rendering.

---

## 🎮 Controls

The following controls are documented for interacting with the application.

| Input | Function |
|---|---|
| `W` `A` `S` `D` | Move the character |
| Mouse | Rotate camera / adjust viewing direction |
| `T` | Switch to first-person camera |
| `Y` | Return to third-person camera |
| `H` | Switch to storage CCTV |
| `J` | Switch to hall / stage CCTV |
| `K` | Switch to right hallway CCTV |
| `L` | Switch to left hallway CCTV |
| `0` | Switch to Freddy POV |
| `U` | Switch to player character |
| `I` | Switch to Freddy |
| `P` | Toggle flashlight |
| `O` | Toggle environmental lighting |
| `Z` / `X` | Adjust hall light position on X-axis |
| `C` / `V` | Adjust hall light position on Y-axis |
| `B` / `N` | Adjust hall light position on Z-axis |

---

## 🧠 Computer Graphics Concepts

This project brought together several fundamental concepts in 3D computer graphics:

| Concept | Application |
|---|---|
| **3D Transformations** | Positioning and orienting cameras, characters, lights, and objects. |
| **Vector Mathematics** | Camera direction, character movement, and lighting calculations. |
| **Camera Coordinate Systems** | Calculating movement and viewing direction relative to the active camera. |
| **Lighting and Shading** | Illuminating objects using point lights and spotlights. |
| **Collision Detection** | Detecting intersections between the player and environmental objects. |
| **3D Model Processing** | Loading OBJ models and preparing vertex and normal data. |
| **GPU Buffer Management** | Organizing geometry data using VBOs and VAOs. |
| **Shader-Based Rendering** | Processing geometry and fragment information through shaders. |

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **C#** | Main programming language |
| **Visual Studio 2022** | Development environment |
| **OpenGL** | 3D graphics rendering |
| **Blender** | 3D modeling and asset preparation |
| **Wavefront OBJ** | 3D model file format |

---

## 📚 What We Learned

Working on this project provided practical experience in implementing computer graphics concepts beyond theoretical exercises.

Some of the key takeaways included:

- Understanding how camera transformations and vector mathematics affect 3D navigation.
- Implementing different lighting sources and observing their effects on a rendered environment.
- Developing a basic collision detection mechanism.
- Understanding the process of loading 3D models and preparing vertex data for GPU rendering.
- Organizing interactive components into a working 3D application.
- Collaborating on a graphics project and integrating different components into a single environment.

---
## 📄 License

Please refer to the repository for applicable licensing information.

## 👨‍💻 Author

**ursleeplessprogrammer**

GitHub: [@ursleeplessprogrammer](https://github.com/ursleeplessprogrammer)

---
