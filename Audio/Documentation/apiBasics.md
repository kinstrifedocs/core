# API basics

The API is contained in the `Kinstrife.Audio` namespace. To access it, get the application's [`SoundSystem`](Scripts/Runtime/SoundSystem.cs) instance - most likely via dependency injection. In this class, you will find four methods to play [`Sound`](Scripts/Data/Sound.cs)s (so you need a reference to one of those as well):

- `PlayOneshot`: Play the sound once in a 'fire and forget' way
- `PlayOneshotAttached`: Same as above, except the sound follows the specified transform
- `PlayWithId`: Play the sound with an ID; this allows you to later on adjust the pitch and volume of the sound as well as pause and stop the sound. If a sound is already playing with a certain ID and another sound plays, the conflict is resolved by priority.
- `PlayWithIdAttached`: Same as above, except the sound follows the specified transform

In order to update the volume or pitch of an already playing identifiable sound, call the methods `UpdateVolume` and `UpdatePitch`. Sounds with an ID can be stopped with the `StopSound` method. To check whether a specific sound is playing with a certain ID, use the `IsPlayingWithId` method.