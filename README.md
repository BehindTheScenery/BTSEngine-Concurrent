# Behind The Scenery Engine: Concurrent
_Performance go brrr._

## What is this?
Behind The Scenery Engine: Concurrent is a massive optimization mod featuring multithreading, deadlock elimination mechanism, lock-free synchronization utilizing CAS/Lock-Free architectures providing significant performance boost on servers.
Instead of many other attempts to recreate multithreading, we were using a more invasive approach. We've tried to optimize everything we could touch without breaking most mods. 

Please note, that this mod is in ALPHA stage of development. Something may break. Something may crash. **Here be dragons, do backups.**

At the moment of writing, performance boost may vary from the modpack and the user's PC setup.

## Known Incompatibilities and Notices
While we aim to make this mod to be compatible with your favourite mods where possible, some mods may require some patches to work with this mods. Feel free to file an issue if there are any other incompatibilities we don't know.

### Somewhat Compatible (see notes)
- [Confluence: Otherworld](https://www.curseforge.com/minecraft/mc-mods/confluence)
  - Proceeds to the Main Menu. The game loads the world successfully.
  - If the mod is present in the modpack, there will be small, or nearly to no performance improvement in the modpack. This happens due to attempt to read `PalettedContainer` data each tick, because the mod have Corruption and Crimson biomes that are mutable and spread all over the world making the game load rates much slower and this whole mod inefficient. However, there won't be any issues with the mod itself, only degraded performance. Requires a bunch of patches to their biome code to resolve this.

### Incompatible
- [Lithium](https://www.curseforge.com/minecraft/mc-mods/lithium)
  - Proceeds to the Main Menu. The game loads the world successfully, but makes it unplayable due to broken mob spawnrates. Sitting in a world around ~3-5 minutes hangs the world out with thousands of newly spawned entities.
  - This is caused by the `toNbt` method being overwritten and destroying the whole ticking pipeline. Requires a patch from the Lithium's side.
  - If this will be patched, then you'll still need to configure Lithium through it's config to disable `PalettedContainer` and `Serialization` patches, so this mod won't crash your game. To resolve this, add to `lithium.properties` these lines: `mixin.chunk.palette=false` and `mixin.chunk.serialization=false`. This will allow the game to run smoothly without any random crashes.
- [Concurrent Chunk Management Engine (C2ME)](https://www.curseforge.com/minecraft/mc-mods/c2me)
  - Does not proceed to the Main Menu.
  - This mod uses various mixins and patches across the chunk management system making this incompatible. This mod aims to do the same thing in a more friendly and compatible way than Behind The Scenery Engine: Concurrent.

## How to use?
For players, just download a mod file called `btsengine-concurrent-x.x.x.jar`, put into the `mods` folder and run the game. That's it!

For mod developers, currently the project is All Rights Reserved. However, the license may be changed at a later time when we will feel that the project is in a more polished state. If you believe that we're doing something wrong, please reach us through Issues section, so we could sort it out and fix it.

## Ports/Backports?
This project is so huge, so it is very hard to maintain this across Minecraft versions. At the moment, 1.21.1 and NeoForge are the only versions/modloaders supported.

- **Fabric?** Maybe if there will be demand.
- **1.7.10**, **1.12.2** or any other version <1.21.1? No. It will require a lot of work from us to port over these versions.
- - The exclusion may be 1.20.1, but it will be discussed later by the whole team, when we will feel that the project is on the state we would like to see.
- **1.22, 1.23?** We're not sure if we want to update the project to newer versions. The time will see. However, if something changes, we'll announce it here and there.

## License
The project is licensed as All Rights Reserved.

```text
All Rights Reserved (c) Behind The Scenery Team.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

You can use this mod in any public modpacks hosted across CurseForge and Modrinth without written permission to mod owner or authors.

You can use this mod in any, original or modified, form in private modpacks as long as they're not released into public. 

You can freely create videos and/or livestreams with this mod, crediting that you are using this mod is advised, but not required.

You cannot modify this mod without written permission from the mod owner or authors if owner is unaccessible. You cannot claim this mod as yours in any possible way.
```
