# Shadow Lantern - 2D Arcade Game
Multimedia Systems Lab - Lab Test 2
Built with HTML5 Canvas + JavaScript in a single file (`shadow-lantern.html`). No external assets.

## How to Run
Double-click `shadow-lantern.html` (Chrome / Edge / Firefox). Press ENTER or click to start.
To host online, rename the file to `index.html` and deploy it on Vercel / Netlify.

## Story and Rules
You carry a lantern through a dark haunted forest.
- **Fireflies (glowing yellow dots):** +10 points and they refill your lantern light.
- **Ghosts (hidden in the dark):** they chase you. Touching one costs 1 life. They are visible only inside your light.
- **Moon Shard (special object):** lights up the whole forest and freezes all ghosts for 3.5 seconds, +25 points.
- Your lantern light **keeps shrinking**. When it gets very small, ghosts become 40% faster ("enrage").
- You have 3 lives. After a hit you are protected for 1.5 seconds. The game ends at 0 lives.

## Controls
| Action | Input |
|---|---|
| Move | Mouse / touch (player follows), or WASD / Arrow keys |
| Start / Restart | Enter, Space, click or tap |
| Pause | P |
| Mute | M |

## Customization (assigned features)
1. **Unique visual theme and character:** dark forest, a lantern-carrying character, ghosts, fog and a moon.
2. **Collectible and hazard:** Firefly (collect) and Ghost (avoid).
3. **Custom mechanic - shrinking light:** the visible area is the lantern radius. It drains over time and is refilled by fireflies. This changes how the game is played, because the player must keep hunting fireflies to see the ghosts.
4. **Special object:** Moon Shard (reveal + freeze).
5. **Difficulty progression:** every 100 points the level rises. More ghosts, faster ghosts and faster light drain.
6. **Limited lives + invulnerability:** 3 lives with a short protection after a hit.

All values are in the `CONFIG` object at the top of the script.

## Multimedia Elements
- **Graphics:** forest, trees, grass, moon, ghosts, character and lantern are drawn with the Canvas API.
- **Animation:** wandering fireflies, floating ghosts, drifting fog, flickering lantern, particles, popups, screen shake.
- **Sound:** collect, hit, shard, level-up and game-over effects; looping ambient music; a heartbeat sound that speeds up when a ghost is close. All generated with the Web Audio API.

## Algorithm
1. `requestAnimationFrame` loop calls `update(dt)` and `draw()` every frame (`dt` = time since last frame).
2. `update`: move the player, drain the light, spawn fireflies / ghosts / shards, move each object, check collisions, update score / lives / level.
3. Ghost movement: each ghost moves in a straight line towards the player (vector from ghost to player divided by its length gives the direction), plus a small wobble.
4. `draw`: background, fog, ghosts, **darkness layer**, glowing items, player, HUD.
5. Darkness layer: an offscreen canvas is filled with a dark colour, then a radial gradient is cut out around the lantern using `destination-out`. Ghosts are drawn before this layer, so they are hidden wherever it is dark.

## Collision Detection (circle vs circle)
Every object is treated as a circle. Two circles collide when the distance between their centres is less than the sum of their radii:

```
dx = a.x - b.x
dy = a.y - b.y
collision if  dx*dx + dy*dy < (ra + rb)^2
```
Squared values are compared so no square root is needed. The same function is used for fireflies, ghosts and the Moon Shard.

## Screenshots
Put `gameplay.png` and `gameover.png` in a `screenshots/` folder.
