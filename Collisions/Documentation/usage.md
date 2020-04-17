# Usage

Before trying to use the API, make sure that the collision system is being [installed in your scene.]("Collision Installer.asset")

## How to set up GameObjects

1. Add an appropriate velocity tracker if the object moves:
  - If it is simulated through the physics system (has a non-kinematic rigidbody), add a [RigidbodyVelocityTracker](Velocity/RigidbodyVelocityTracker.cs)
  - If it is being animated, add a regular [VelocityTracker](Velocity/VelocityTracker.cs). The required PoseTracker will be added automatically for you.
2. Your object now has its velocities tracked. This is not necessary for static objects.
3. If it should also be part of the collision system, add a [CollisionParticipant](CollisionData/CollisionParticipant.cs) component.
4. You will see that a [PhysicalMaterial](CollisionData/PhysicalMaterial.cs) has also been added - if you don't assign this value through code, make sure to assign a material here!
5. You're done! Contacts with this GameObject will now be available in `Contacts`, along with corresponding collision data. It will also trigger collision effects (sound, VFX and decals) as specified in the physical material and collision effects config.

## Setting up materials

The central (authoring) data type for the collision effects is the `Material`, located in the _Config/Physics_ folder of the _Kinstrife Data_ package. By adding sounds, VFX and decals, the visualization of collisions can be customized. Additionally, you can set threshold velocities, under which no effects are triggered, and how the intensity of the effect should change depending on the velocity.

By default, the collision system plays effects for both collision participants or picks an effect based on priority. However, effects can be overridden for material pairs in an instance of the `CollisionEffectsConfig' (also located in the _Config/Physics_ folder of the _Kinstrife Data_ package). Note that this is config data, only a single instance should exist - try searching for it before creating a new one. Once you have an instance, you can add new material pairs and choose how to override effects. You can do this per effect type (sound, decal or VFX). The default is no override, which results in the default behaviour. You can choose to disable effects for this material pair where nothing is played. With OnlyTargetMaterial, only effects of the target material (as specified for that pair) will be played, with Override you can create entirely new settings.