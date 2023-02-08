---
id: bitesize-dynamicprefabs
title: Dynamic Prefabs Sample
description: Learn more about the dynamic prefab system, which allows us to add new spawnable prefabs at runtime.
---

The [Dynamic Prefabs Sample](https://github.com/Unity-Technologies/com.unity.multiplayer.samples.bitesize/tree/master/Basic/DynamicPrefabs) showcases the available use-cases for the dynamic prefab system, which allows us to add new spawnable prefabs at runtime.

## Dynamically Spawn Prefabs at Runtime
The dynamic prefabs system allows the developer to add a new prefab to the network prefab list at runtime. Each scene in the project showcases a different, isolated feature of the API.
<br><br>

## Dynamic Prefab Manager
Add Text
```csharp reference
Add Code
```
<br>

## Preloading
Add Text
```csharp reference
Add Code
```
<br>

## Spawning Synchronously
Add Text
```csharp reference
Add Code
```
<br>

## Spawning with Network Visibility
Add Text
```csharp reference
Add Code
```
<br>

## Addressables

This sample uses Addressables to load the dynamic prefab, however any GameObject with a NetworkObject component can be used, regardless of its source.
<br>

```csharp reference
Add Code
```
<br>

## Using the Sample UI

This sample also uses in-game UI (created using UI Toolkit) to interface with the dynamic prefabs system with configurable options like artificial latency and network spawn timeout for easy testing.
<br><br><br>

## Limitations of the Dynamic Prefab System

There are several limitations to this API:
- If you have NetworkConfig.ForceSamePrefabs enabled, you can only modify your prefab lists **before** starting
  networking, and the server and all connected clients must all have the same exact set of prefabs
  added via this method before connecting.

- Adding a prefab on the server **does not** automatically add it on the client - it's up to you
  to make sure the client and server are synchronized via whatever method makes sense for your game
  (RPCs, configs, deterministic loading, etc).

- If the server sends a Spawn message to a client that does not yet have the corresponding prefab loaded, the spawn message
  (and any other relevant messages) will be held for a configurable time before an error is logged (default 1 second, configured via
  NetworkConfig.SpawnTimeout). This is intented to enable the SDK to gracefully
  handle unexpected conditions that slow down asset loading (slow disks, slow network, etc). This timeout
  should not be relied upon and code shouldn't be written around it - your code should be written so that
  the asset is expected to be loaded before it's needed.

- It's currently impossible for clients to late join after a dynamic prefab has been spawned by the server - this is because the initial    sync doesn't allow us any time to load prefabs that are aren't yet loaded on the client.