---
title: Wwise Spatial Audio Workflow in Unreal Engine
tags: [Audio, Unreal Engine 5, Wwise]
style:
color:
comments: true
description: The integration of Wwise spatial audio into game development, particularly with Unreal Engine, involves a comprehensive workflow that leverages various features and technologies to create immersive audio experiences.
---

The integration of Wwise spatial audio into game development, particularly with Unreal Engine, involves a comprehensive workflow that leverages various features and technologies to create immersive audio experiences. Let's delve into some key aspects of this process:

## Rooms and Portals
* **Concept:** This feature simulates sound propagation in enclosed spaces, such as how sound transmits through walls and exits through openings. It's pivotal for enhancing acoustic realism in games.
* **Creating Rooms:** In Wwise, Auxiliary Busses are created for each room, allowing customization of effects like RoomVerb.
* **Integration with Unreal:** Utilize AkSpatialAudioVolume objects in Unreal Engine to model sound propagation from different rooms effectively.

## Reverb Parameter Estimation
* **Automation:** This Wwise feature automates the assignment of reverb Aux Busses based on the physical characteristics of the UPrimitiveComponent in Unreal Engine.
* **Functionality:** It estimates the decay time of a reverb and maps it to corresponding Aux Busses, ensuring reverb characteristics align with the simulated space.

## Authoring Audio Objects
* **3D Audio and Audio Objects:** Enable 3D audio by configuring the Master Audio Bus and System Audio Device in Wwise.
* **Sound Routing:** Different mixes are used for various audio content, like routing ambient sounds to the Main Mix and music to the Passthrough Mix.

## Game-Defined Auxiliary Sends
* **Dynamic Assignment:** This feature allows dynamic assignment of sounds to different Auxiliary Busses based on game logic and object positioning.
* **Workflow Integration:** Sound designers define Auxiliary Bus objects for various game environments, which are then mapped to in-game geometry by developers.

## Ambisonics
* **Usage:** Ambisonics is employed for dynamic ambiences, offering a multichannel audio format for representing spatial audio.
* **Manipulation:** Ambisonic audio can be rotated and manipulated, ideal for dynamic, spatialized ambiences in games.

## Spatialized Foley and Ambiences
* **Enhancing Realism:** Implementing spatialized foley and ambiences, like footsteps and ambient noises, adds realism, with sounds positioned and processed to reflect their real-world behavior.
* **Dynamic Ambiences:** These can be aligned with visual elements and rotate according to the listener’s orientation, maintaining visual-audio coherence.
Additional Technologies
* **Ak Geometry with Diffraction and Transmission Loss:** This feature in Wwise models how sound interacts with physical objects, including diffraction (bending around obstacles) and transmission loss (reduction through objects).
* **Wwise Reflect:** It simulates realistic reflections of sound, enhancing the spatial and environmental audio effects.

# Conclusion
Spatialization in Wwise, especially when integrated with Unreal Engine, offers a framework for crafting immersive audio environments in games. By leveraging features like Rooms and Portals, Reverb Parameter Estimation, Audio Objects, Ambisonics, and additional technologies like Ak Geometry and Wwise Reflect, sound designers can create rich, dynamic audio experiences that significantly elevate the player's immersion in the game world.