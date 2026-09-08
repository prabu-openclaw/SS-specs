# Intent — declare the fog layers

**Author:** prabu-openclaw
**Date:** 2026-09-07
**Status:** draft
**Next stage:** `spec.md`

## Problem

`civic-seam-visual-direction.md` §7 specifies fog as two layered presentation
passes — a low layer that "reveals beams and tires/feet" and a high layer that
"softens distant architecture" — and `visual-assets.md` §5 lists fog overlays
among the required modular families. Neither exists, and neither can exist,
because no contract names an asset ID for them.

This is the same shape as the gap `musicAssetIds` closed: the runtime bundle
filter ships what the contracts declare, so art nothing names is unreachable by
construction however well it is produced. Fog is currently unbuildable rather
than unbuilt.

It matters now because fog is the most-cited element of the art direction — it
is named in the setting description of every environment prompt written so far —
and the game has none of it.

## Proposed outcome

- `presentation-assets-001` declares `env_fog_low` and `env_fog_high`.
- Delivered fog art is admitted and reaches the runtime bundle by the same route
  as every other environment group.
- Nothing changes for a build with no fog art: the group is unbacked, and the
  all-or-nothing rule leaves the air clear.

## Affected users/systems

Player (presentation only), `presentation-assets-001`, the runtime bundle
filter, and the environment intake script.

## Constraints/non-goals

- **Presentation only.** §7 says any gameplay visibility change is
  simulation-authored and versioned separately. Declaring these IDs must not
  imply one, and the runtime renderer for them reads no state and writes none.
- The two IDs are one group. A ground haze with nothing above it reads as a
  rendering fault rather than as weather, so all-or-nothing applies as it does
  to ground, solids, cameras, props and motifs.
- Not a new fog *system*: no volumetrics, no occlusion, no visibility rules.
- Does not reopen §7's readability floor. Fog may not conceal authoritative
  collision, lethal telegraphs, or required Camera boundaries; that is enforced
  in the runtime by draw order and asserted there.

## Open questions

- Should fog density vary by zone? §7 does not say, and the Transit Cut reading
  foggier than the Civic Plaza would be an easy win — but it is a spec decision,
  not a renderer one, and nothing here assumes an answer.

## Verified claims

- §7 specifies exactly two layers, low and high, with those two jobs.
  `[verified: civic-seam-visual-direction.md §7]`
- `visual-assets.md` §5 lists "fog overlays" as a required modular family, and
  it is one of only three entries in that list with no delivered asset.
  `[verified: cross-check of the §5 list against environmentAssetIds]`
- Art not named by a contract cannot reach the bundle.
  `[verified: RuntimeBundleFilter unions the declared ID lists; RuntimeBundleTests requires every bundled asset to be reachable]`
- The runtime renderer for these layers is already written and ships inert
  without them, so this declaration is the only thing between the art and the
  screen. `[verified: SS-runtime render/fog-layers, App tests green with the group unbacked]`

## Assumed claims

- 512 × 512 tiling is the right authoring size. `[assumed: matches the existing
  ground tile treatment scaled for a slower-moving layer; no contract fixes a
  size for fog, and the intake does not check one for this group]`
