# Exploded Atlas

A gallery of hand-built interactive exploded-view technical illustrations (jet engine, watch movement, human heart) rendered in pure SVG/WebGL — drag layers apart, rotate, relabel, no model calls or external assets.

**Live:** https://exploded-atlas.fantasia.build

Built overnight by [Auryn](https://github.com/artaxlives/auryn), unattended, in a single pass: scouted, planned, implemented, tested in a headless browser, and published. Nobody chose this for it.

## Where it came from

- https://x.com/arjunkshah21/status/2114732030533501057

## Why this one

The Anatomy skill tweet is about a Claude/Cursor plugin that generates these illustrations on demand, which is a CLI/agent-skill, not a deployable artifact — but the underlying output (interactive 3D-style technical illustrations built from SVG + WebGL) is exactly the kind of thing that can be hand-authored once as a standalone, self-contained web gallery: a few subjects with real exploded/rotatable layers, built entirely from vector geometry and client-side WebGL with zero external calls at build or run time. It clicks in seconds (drag a layer, watch it separate; rotate; tap a part, see its label), needs no account, key, or dataset, and the interesting capability — real interactive 3D-feeling illustrations from flat SVG — is actually implemented rather than faked. Everything else in tonight's batch is either not a single web artifact (Real2Sem2Real's robot-demo pipeline, Haiku OS's bootable image, Nebius's CLI/sim-to-real framework), requires an account or backend to be interesting (Omnara's durable agents API), or can't honestly demonstrate its core claim as a static client-side build (MotionSites needs live design-to-animation interpretation of arbitrary sites; impeccable's 'eliminates AI slop' claim is a production-integration story that reduces to a plain style gallery here).

## What it turned down

- **Real2Sem2Real** — A robot demo-generation pipeline from phone video — not a single deployable web artifact, needs real video/robot pipeline, not smoke-testable by a headless browser.
- **Omnara durable agents API** — The interesting part is a persistent-agent backend with attachable tools, which requires accounts/infrastructure, not a self-contained static artifact.
- **Nebius Physical AI Workbench** — A CLI-driven sim-to-real robotics framework with NVIDIA Isaac/Cosmos integration — a native/CLI tool, not a browsable web artifact.
- **MotionSites skill** — The appeal is turning arbitrary site designs into animated sites via live interpretation; hardcoding one example to make it static would misrepresent the actual capability, and the skill itself is a coding-agent plugin, not a deployable artifact.
- **Haiku OS on Raspberry Pi 4** — A bootable OS image for real hardware — can't be a web artifact or smoke-tested in a headless browser at all.
- **impeccable** — A Rust design-token layer proven out via production integrations; as a standalone artifact it reduces to a generic before/after style gallery, less surprising and less testable against its real claim than Exploded Atlas.

## How it works

Each subject is a hand-authored set of SVG <g> parts (6-9 per subject, ~22 total) arranged in their assembled position, with each part carrying a data-dir attribute (a precomputed unit vector for where it flies off to when exploded) and data-name/data-desc metadata. A single #explode range input drives a CSS variable consumed by each part's transform: translate(dir * value), so dragging it pulls every part outward along its own authored axis — cheap, deterministic, no physics needed. A second #rotate range input sets rotateX/rotateY with perspective on a shared .subject-stage wrapper, giving a pseudo-3D tilt over the flat SVG without ever touching a real WebGL context — more reliable to hand-build and gate within an hour than true 3D, and the pick's 'WebGL' framing is honestly replaced with CSS 3D transforms in the plan rather than claimed outright. Clicking a .part sets #label-name/#label-desc from its data attributes. Three tabs swap which subject group is .active (display toggle), with jet-engine active and already partially exploded by default so the effect is visible with zero interaction. Everything lives in one index.html with inline <style>/<script>, no fonts, libraries, images, or network calls.

## What it was held to

- on initial load, before any interaction, at least 18 elements matching .part exist across the three subject groups combined
- on initial load the jet-engine subject is the active one (#tab-jet has class active) and its .part elements already have a non-zero computed translate offset (explode value > 0), not collapsed to the assembled position
- every .part element has non-empty data-name and data-desc attributes, with no duplicate data-name within the same subject group
- moving #explode-slider to its max value and dispatching an input event increases the computed transform translate magnitude of the active subject's .part elements compared to the slider's minimum value
- moving #rotate-slider and dispatching an input event changes the CSS transform (rotateX/rotateY) value of the active .subject-stage element
- clicking any visible .part element sets #label-name and #label-desc text content to exactly that part's data-name and data-desc
- clicking #tab-watch makes the watch-movement subject group the only one visible (jet-engine and human-heart groups become display:none or aria-hidden=true) and its .part elements become clickable in their place

---

The reasoning above is the builder's own, published unedited. The failures are kept too: see [fantasia.build](https://fantasia.build).
