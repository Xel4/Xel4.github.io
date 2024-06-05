---
title: Emotional Component in “InfeStation”
tags: [InfeStation, Unreal Engine 5, Programming]
style:
color:
comments: true
description: This document provides a high-level overview of the emotional component integrated into “InfeStation,” a survival horror FPS developed with Unreal Engine 5.2. It focuses on the implementation of the PAD (Pleasure, Arousal, Dominance) emotional model and its consequential impact on both gameplay and narrative.
---

# Introduction
This document provides a high-level overview of the emotional component integrated into “InfeStation,” a survival horror FPS developed with Unreal Engine 5.2. It focuses on the implementation of the PAD (Pleasure, Arousal, Dominance) emotional model and its consequential impact on both gameplay and narrative.

FPS games are known for their immersive experiences, where players perceive the game world through the character's perspective. The integration of the PAD model amplifies this immersion by aligning the player's emotional state with that of the game environment and character. In a survival horror context, this leads to a more intense and personal experience of fear, tension, and excitement, as players not only navigate the game world but also experience its emotional depth.

# Theoretical Framework
## PAD Dimensional Model of Emotion
The PAD model, a psychological framework for describing and measuring emotional states, serves as the core of the emotional component in the game. It considers three dimensions:

* **Pleasure (P):** Reflects how pleasant or unpleasant one feels. In a survival horror game, this axis would typically oscillate between negative (displeasure, fear, disgust) and neutral states. This axis impacts how players perceive the environment, encounters, and narrative elements.

* **Arousal (A):** Indicates the level of alertness or stimulation. Arousal in survival horror is key to maintaining suspense and excitement. High arousal could be triggered by chase sequences, jump scares, or intense combat, leading to heightened alertness and adrenaline. Low arousal moments, on the other hand, would be used for building tension and giving players a brief respite, enhancing the impact of subsequent high arousal situations.

* **Dominance (D):** Relates to the feeling of control or powerlessness. The Dominance axis in survival horror can dictate a player’s sense of control or helplessness within the game. High dominance might be experienced when players effectively manage resources, combat enemies successfully, or solve puzzles, giving a sense of empowerment. Low dominance, conversely, manifests in feelings of vulnerability and powerlessness, common in horror games to intensify fear and uncertainty.

The PAD model is rooted in psychological research, offering a scientifically informed approach to game design. This empirical basis can lend greater credibility to the emotional aspects of game design, allowing for a more structured and validated approach to creating emotional experiences in games.

### Cognitive Axis
While robust, the traditional PAD model focuses on the affective dimensions of emotions and does not explicitly address the cognitive processes underpinning emotional experiences. Emotions are not just affective states; they also involve cognitive appraisal and processing. The way we interpret a situation can significantly influence our emotional response. A cognitive axis could capture this aspect, which is particularly relevant for emotions like surprise and anticipation.

* **Surprise:** This emotion typically results from an unexpected event. A cognitive axis could represent the degree to which an emotion is influenced by new, unexpected information, which is a core aspect of surprise.

* **Anticipation:** This involves looking forward to or expecting something in the future. A cognitive axis would be useful in quantifying this forward-looking aspect of anticipation.

Both surprise and anticipation may have similar scores on the traditional PAD dimensions, as they can vary in pleasure, arousal, and dominance. The cognitive axis provides an additional dimension to differentiate them more clearly based on the cognitive underpinnings of these emotions.

The Cognitive axis plays a crucial role in a player's strategic planning and reaction to unexpected events. Surprise elements might include unforeseen enemy encounters or plot twists, leading to immediate, intense emotional reactions. Anticipation builds tension over time, as players expect something to happen based on environmental cues or narrative foreshadowing. This axis manipulates the player’s expectations and reactions, creating a more psychologically engaging experience.

## Plutchik's Wheel of Emotions
Plutchik's Wheel of Emotions is a model that conceptualizes emotions in a wheel-like structure, showing primary emotions and their derivatives, including mixtures (or dyads) of these primary emotions. The model suggests that more complex emotions can arise from combinations of basic ones. An emotion map quantifies these complex emotions by blending the PAD vectors of the constituent emotions. This aligns well with Plutchik's theory.

Employing a dyads approach to map Plutchik's Wheel of Emotions to PAD vectors attempts to capture the complexity of human emotions. However, it's important to note that while this approach is theoretically sound, its practical effectiveness depends on the accuracy of the PAD values assigned to each emotion and the method used to combine these values for dyads. The interpretation of these combined PAD vectors should be carefully considered, as emotional experiences can be subjective and context dependent.

# Implementation Strategy
## Emotional Mapping and Dyads
Based on Plutchik's Wheel of Emotions, the system focuses on primary emotions and their dyadic interactions, to effectively translate complex emotional concepts into measurable and programmable game elements.

The emotion map is calculated in a spreadsheet (PlutchikEmotionMap.xlsx) that contains three sheets: “Vectors,” “Dyads,” and “Mapping.” Here's a brief overview of each:

* **Vectors:** Lists all primary and secondary emotions on Plutchik's Wheel. Each emotion is associated with a normalized vector to map to the PAD model, which is calculated from the dyads sheet.

* **Dyads:** Combines emotions to form dyads (pairs of primary emotions). Each row lists an emotion (or a pair) and provides values for Pleasure, Arousal, Dominance, Cognitive dimensions, along with a 'Magnitude' value for vector normalization.

* **Mapping:** Like the Vectors sheet, it lists Plutchik's primary emotions with associated values for Pleasure, Arousal, Dominance, and Cognitive dimensions as the basis for calculating the values for Plutchik's secondary emotions.

These sheets provide a comprehensive mapping of emotions in the context of the PAD model, with the addition of a Cognitive dimension. The Dyads sheet introduces an aspect of combining emotions to analyze complex emotional states. The inclusion of a Cognitive dimension across these sheets supports the idea of incorporating cognitive processes into the understanding of emotions, as previously discussed.

## Streamlining Emotional Variables
The dimensional model simplifies the process of tracking emotions by reducing the number of separate variables required. However, directly assigning emotions from this model to gameplay elements can be non-intuitive. To address this, designers can utilize the emotion map, which allows the input of any of Plutchik's thirty-two primary and secondary emotions. The corresponding output will then be mapped onto the four axes of the dimensional model. This method enables designers to select emotions that are most relevant to the game's thematic and narrative elements, while maintaining consistency in implementation using the same four variables. The choice of central emotions is aligned with the game's core themes, with an emphasis on fear and surprise to enhance the horror genre experience.

## Combining Emotions
Utilizing a sigmoid function to combine dimensional emotions from the PAD model and the Cognitive axis ensures that the resulting emotional output remains within a manageable and interpretable range. The hyperbolic tangent (tanh) function, a type of sigmoid function, is adept at mapping any real-valued number to a value between negative one and one. This is particularly advantageous in scenarios that require a normalized bipolar output. For example, a high combined emotional score, reflecting intense emotions such as extreme fear or excitement, will be normalized by the tanh function to a magnitude approaching one. In contrast, lower emotional intensities will be scaled down to magnitudes nearer to zero.

Each emotional axis—Pleasure, Arousal, Dominance, and Cognitive—encompasses varying degrees of intensity. Prior to the application of the tanh function, these values can be scaled to reflect their relative intensities. The method of combining emotional states can range from simple linear combinations to more intricate formulas, depending on the relationship between different emotions. The normalized output is then used to influence various game aspects. For instance, with music, a magnitude close to one could activate more intense music, aligning the auditory experience with the game’s emotional landscape.

# Technical Integration
## Ambience Zones
Ambience zones utilize collision boxes to associate base emotional states with designated game areas, thereby influencing player mood based on location.

## Scripted Triggers
Narrative events in “InfeStation” are scripted triggers to evoke specific emotional responses from the player. These triggers are integrated at pivotal narrative junctures, eliciting immediate shifts in the player’s emotional state. For instance, interactions with the spaceship's AI, SILAS, are designed to spike the player's emotional state towards trust, fostering a sense of companionship. Following such triggers, emotional states are programmed to decay back to baseline levels, mirroring a natural emotional response cycle.

## Auditory Feedback
Incorporation of generative ambient music in MetaSounds influenced by emotional conditions serves to reinforce the intended emotional atmosphere.

The pleasure axis can influence the tonality and harmony of the music. Negative pleasure could lead to dissonant, minor key music, creating a tense or unsettling atmosphere. Positive pleasure might introduce major keys or consonant harmonies, offering a sense of relief or safety. Use of filters to adjust brightness and color of the sound, modulation of harmony and chord progression complexity.

High arousal states can be mirrored with faster tempos, more rhythmic complexity, and intense dynamics to reflect excitement or panic. Low arousal could translate to slower tempos, minimalistic textures, and softer dynamics, creating a sense of calm or suspense. Tempo modulation, rhythmic pattern generation, dynamic envelope shaping.

High dominance can be expressed through bold, assertive musical themes, major chords, and stable, predictable melodies, conveying a sense of control and power. Low dominance might involve more chaotic, unpredictable, and unresolved musical elements, reflecting vulnerability or confusion. Control over melodic direction, stability in rhythmic patterns vs. randomized sequences, modulation of musical themes.

The element of surprise can be captured with sudden musical changes or unexpected sound elements. Anticipation can be built through repetitive motifs that evolve gradually or using rising tension in harmony and melody. Sudden shifts in timbre or rhythm, gradual modulation of filters, build-up of layers or textures.

In a generative music system, these emotional variables can be mapped to different parameters within the modular environment of MetaSounds. For instance, changes in the game's emotional state could trigger alterations in the synthesis parameters, thus creating a soundtrack that dynamically responds to the gameplay and enhances the emotional impact of the game. This approach not only contributes to a more immersive gaming experience but also allows for a musical score that adapts and evolves based on the player’s journey through the game.

## Enhanced Gameplay Mechanics
Emotional states can influence gameplay mechanics. For example, a high arousal state could make the game more challenging by increasing enemy aggressiveness or reducing resource availability. Conversely, a high dominance state might empower the player with enhanced abilities or control. This integration of emotion into gameplay mechanics creates a more responsive game environment. In survival horror, this means the game can adapt in real-time to the player's emotional state, enhancing unpredictability and suspense.

# Conclusion
The integration of an emotional component in a game, particularly one structured around the PAD (Pleasure, Arousal, Dominance) model and the Cognitive axis, offers benefits to both the player's experience and the storytelling aspect of the game. Here’s how:

## Enhancing Player Experience:

* **Increased Immersion:** Emotional components make the gaming experience more immersive. By aligning the game’s emotional landscape with the player’s responses, the game feels more responsive and engaging. In a survival horror game, this can mean heightened feelings of fear, suspense, or relief at key moments, making the game feel more real and impactful.

* **Dynamic Gameplay:** Emotional states can dynamically influence game mechanics. For instance, high arousal might lead to more aggressive enemies or heightened challenges, while high dominance could empower the player with enhanced abilities. This variability keeps gameplay fresh and unpredictable.

## Contributing to Storytelling:

* **Emotional Narrative Arcs:** The emotional component allows for the creation of complex emotional arcs within the story. Characters and scenarios can be designed to evoke specific emotional responses, adding depth and nuance to the narrative.

* **Enhanced Character Development:** By integrating emotional responses, characters within the game can become more relatable and multi-dimensional. Their reactions in various situations can reflect more complex emotional states, contributing to a more engaging and believable story.

* **Atmospheric Storytelling:** The game’s atmosphere can be adjusted to reflect the narrative’s emotional tone. For example, a tense, fearful atmosphere can be heightened during suspenseful plot points, while a more subdued or melancholic atmosphere can underscore moments of narrative significance or loss.

* **Symbolism and Thematic Depth:** Emotions can be used symbolically to reinforce the game's themes. For instance, a shift from fear to empowerment could mirror the protagonist's growth, adding a layer of thematic depth to the story.

In summary, the integration of an emotional component in a game like “InfeStation” enriches the player’s experience by making the game more immersive, responsive, and personalized. Simultaneously, it enhances the storytelling by allowing for more emotionally resonant narratives, character development, and thematic exploration. This integration represents an approach to game design where emotional nuances play a central role in both gameplay mechanics and narrative construction.
