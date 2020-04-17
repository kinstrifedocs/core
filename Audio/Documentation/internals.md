# Internal Implementation

This is not relevant if you only plan to use this package. This is mostly meant for the sake of posteriority, for when changes will need to be made to the system.

## Sound & SoundCategory

These are meant as data holding/authoring objects, referenced in config and database data. Sounds contain multiple `SoundVariation` instances; both can generate a `PlayableClip` which can be used to pass to a `SoundPlayer` to play.
The sound class contains a small in-editor audio system to test/audition sounds and their variations, including random as well as min/max pitch and volume.

In the future we might also utilize sound categories to implement sound-grouping logic.

## SoundSettings

Sound settings contain spatial and configuration data, based on the available settings of the audio source. Settings are split up between sound categories and individual sounds, with a combined SoundSetting struct to combine both data 'halves' again. This combined struct can be applied to AudioSource instances.

## SoundInstance

[`SoundInstance`](xref:Kinstrife.Audio.SoundInstance)s are, well, just that, and also audio source instances. They create dummy game objects with audio sources (which are hidden in the hierarchy and don't get saved), which will reside in the scene specified in the `SoundSystem`. They hide away the interaction with the engine's audio API from the rest of the package.

## SoundSystem

[`SoundSystem`](xref:Kinstrife.Audio.SoundSystem) is the access point for the public API. It is 
1) a wrapper around the internal `SoundPlayer`
2) handles pooling of SoundPlayers and 
3) manages their IDs. 

To this end, it contains a pool class for SoundPlayers and a dictionary of ID/SoundPlayer key-value-pairs.
GameObjects are used as IDs because this allows for a sort of 'fire and forget' approach to looped sounds, 
similar to how an AudioSource would work if it was attached to that game object. Additionally, GameObjects already exist (sorta) as a unique identifier for objects in a scene - might as well reuse that instead of generating and handing out new unique IDs (which would be the alternative).

TODO for the future: Expand with localization in mind (probably by reducing Sound to an ISound interface, allowing for a new LocalizedSound type to also provide a PlayableClip)