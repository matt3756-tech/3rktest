3RK RACING SLOT — LOCAL HTML5 / JAVASCRIPT BUILD
=================================================

QUICK START
1. Keep this entire folder together.
2. Double-click index.html to test it locally.
3. Click anywhere once to unlock browser audio and start the looping background music.
4. Open EDITOR in the upper-right corner to fine-tune the game.

For the most consistent browser behavior, run start-local-server.bat on Windows or
start-local-server.command on macOS, then open http://localhost:8000.

GAME RULES
- Five paylines: top, middle, bottom, diagonal down, and diagonal up.
- WILD substitutes for every regular symbol.
- Three scattered WHEEL symbols anywhere trigger the wheel-pick bonus.
- Pick one of eight wheels to reveal 5–12 free spins.
- All free-spin line wins are doubled.
- Three WHEEL symbols during free spins retrigger the originally picked amount.
- BIG WIN begins at 10x bet. MEGA WIN begins at 25x bet.
- Pays and weights are placeholders and are intentionally easy to change.

EDITOR
- Drag and resize the cyan selection box for reels, readouts, status text, buttons, and popup cards.
- Adjust reel acceleration, full-speed travel, stagger, deceleration, overshoot,
  rebound, stop timing, blur, and anticipation duration.
- Adjust each symbol's scale, X/Y offset, opacity, and rotation independently.
- Adjust each button's exact art mask source, mask radius, press depth, brightness,
  scale, cover opacity, and press duration.
- Preview each popup using the checkboxes.
- Adjust all supplied audio and synthesized fanfare volumes.
- Force the bonus on the next spin for testing.
- Export or import the complete settings JSON.

CACHE CONTROL
index.html injects the stylesheet, scripts, artwork, and audio with a fresh timestamp
query on every load. It also unregisters service workers. This prevents an old build
from being reused during local testing.

MODULES
js/math.js       — five-payline evaluation and pays
js/outcomes.js   — weighted reel outcomes and forced-bonus outcomes
js/rendering.js  — symbols, reel windows, visual layout
js/animation.js  — reel acceleration/cruise/deceleration/overshoot/bounce behavior
js/audio.js      — music, supplied sounds, synthesized bonus/big/mega fanfares
js/ui.js         — buttons, readouts, popups, leaderboard, paytable
js/editor.js     — visual editor, previews, import/export, drag/resize
js/game.js       — game flow, credits, free spins, retriggers, feature locking

ARTWORK
Every supplied artwork file was copied byte-for-byte into assets/artwork. The game
uses the supplied SLOT UI JPEG as-is. Reel symbols are layered over its black reel
windows. Button press masks use exact crops from that same UI at runtime, so the
source art itself is never re-encoded or altered.

MISSING SOUND NOTE
No separate bonus-won, big-win, or mega-win audio file was included in the upload.
Those fanfares are generated with Web Audio so the requested timing and flow work
now. BIG WIN and MEGA WIN use the supplied go-kart art inside a tire/checkered-flag graphic. They can later be replaced in js/audio.js without changing game logic.

V3 UPDATE
- Restored a persistent extra symbol row above each reel so the same incoming symbols remain visible through the bounce and into the next spin.
- Regular win amounts can be dismissed early by pressing SPIN; the next spin begins immediately after the popup transitions away.
- Added editor control for Bonus land sound lead ms.
- Limited WHEEL to one symbol per reel in generated outcomes.
- WHEEL and CARD symbols pop forward slightly when they land.
- Added the entertainment-only notice to the pay table.

V4 UPDATE
- Reel rolling appearance restored to the original v1 per-frame strip behavior.
- Extra top-row symbols remain visible during bounce but never receive WHEEL/CARD landing-pop effects.
- WHEEL/CARD landing pops now begin slightly earlier; adjust Reel behavior > Symbol pop lead ms in the editor.

V5 UPDATE
- Reduced empty space in the retrigger and total bonus win panels.
- Fixed WHEEL and CARD landing-pop visibility and preserved the editor timing control.
- Preloads and decodes all artwork before enabling gameplay.
- Reel animation now reuses each visible symbol strip between row changes instead of rebuilding it every frame, preserving the existing reel look while reducing garbage collection and frame stutter.


V6 CHANGES
- Restored the persistent extra top symbol row and corrected incoming top-edge spacing.
- Symbol landing pop duration is now adjustable in the editor.
- WHEEL and CARD pop effects begin earlier and persist through the stop/bounce redraw.


V7 FIX
- Diagnosed the missing top row: its cell was placed at -0.94 rows while artwork is centered with a 90% max height, leaving effectively only about 1% of the image visible after clipping.
- The persistent top carry symbol now visibly peeks into the reel window and remains unchanged into the next spin.
- Added Top row visible fraction to the Reel Behavior editor section.

V9 REEL TOP-ENTRY FIX
- Restored the original V1 per-symbol rolling coordinates instead of moving the entire cached strip.
- Incoming symbols now originate at the same top-edge position and follow the same vertical path as V1.
- The persistent extra top row remains available during stopping and bounce-back.


V9 PERFORMANCE FIX
- Reels preserve the exact V8/V1 coordinates, top-entry path, symbol spacing, bounce and stop behavior.
- The seven already-existing symbol elements per reel are now reused instead of allocating and decoding new DOM/image objects every animation frame.
- Artwork is kept strongly referenced after preload so decoded graphics are not discarded mid-session.
- This removes the intermittent garbage-collection/decode spike that caused random reel stutter.
