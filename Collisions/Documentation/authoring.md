#### Authoring tips & guidelines

It usually makes sense to check and set all values in a material. If a material should not play (for example) sliding VFX, it is also possible to simply leave a field empty and no effect will be played.

TODO: Some examples for ranges of common collision velocities

**Sounds:**
Pitch for collision sounds is adjusted based on object size. The relevant size is not the _volume_ of the object, but rather the largest area of the largest side of the object's bounding box. You can specify the min and max area for modulation in the material in _square decimeters_. A value of 1 means objects with a bounding box size of 0.1m by 0.1m by <0.1m will have the highest pitch for that sound. Objects smaller than that will have the lowest pitch. It works the same for large objects, an area of 400 sq decimeters corresponds to an object that has a bounding box side that is 2 by 2 meters.
Also note that the curve for pitch modulation is quadratic, which means that the lerping of the pitch is more fine-grained on the lower end of the scale, i. e. for smaller objects.
For impact sounds, only the part of the velocity that is orthogonal to the surface is considered. Similarly, sliding sounds only respect tangential velocity.

**VFX:**

VFX objects are placed with the following orientation:
Z axis: Along surface normal
Y axis: Along other partner's forward axis for impacts; along velocity for sliding effects (both projected to be orthogonal to surface normal)
X axis: Cross product of Y and Z axis 

This means that for sliding VFX, a negative velocity along Y will mean that particles will be 'trailing behind' if simulated in local space.

However, simulation in global space is preferable for most situations.

**Decals:**

Modulation of decal size and opacity is based on impact velocity and is optional.

Decal objects are placed with the following orientation:
Z axis: Along *negative* surface normal
Y axis: Along other partner's forward axis
X axis: Cross product of Y and Z axis

This means that e. g. footprint textures should have the heel at the bottom of the texture and toes at the top.