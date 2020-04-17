# Authoring audio assets

Authoring is based on scriptable objects, allowing for a modular library of sounds and categories.

### Sound

Create a [sound](xref:Kinstrife.Audio.Sound) via the context menu (right-click in project tab), then Kinstrife->Audio->Sound.

Sounds define individual sounds on a 'logical' level. This can be anything from a 'metal hits wood' to a UI button press sound. Each sound has one or more _variations_, which are, well, variations of a sound, including custom pitch and volume ranges. Also make sure to adjust the *settings* of each sound accordingly (UI sounds probably should not be spatialized, for example.)

### SoundCategory

Create a [sound category](xref:Kinstrife.Audio.SoundCategory) via the context menu (right-click in project tab), then Kinstrife->Audio->Sound Category.

Sound categories hold information that is common to a number of sounds, e. g. which audio mixer to use or which priority the sounds have and whether they should bypass scene audio effects (for example collision sounds and UI sounds could be two categories).