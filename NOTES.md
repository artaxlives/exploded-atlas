# Changed from the plan

No functional departures. Implemented one self-contained `index.html` with inline styles, script, and hand-authored SVG: eight jet-engine parts, seven watch-movement parts, and seven human-heart parts. The jet engine starts active at 48% explosion. Each part has a unit direction vector and unique descriptive metadata; a shared CSS variable drives translation. Perspective uses CSS rotateX/rotateY. Used the acceptance contract's `explode-slider` and `rotate-slider` IDs rather than the shorthand IDs in the approach description.

Added keyboard activation for components, accessible subject buttons, responsive layout, and a reset-view button. Initial component notes and illustrations are embedded in the HTML. All content is local; no build, dependencies, generated images, or runtime requests are required.

Validation: parsed the complete HTML and checked local asset references; executed the actual inline script in a Node DOM harness. Passed checks for all 22 components and their metadata, default subject and explosion, minimum/maximum explosion variable and part transform bindings, rotation changes, exclusive subject visibility, exact label updates for every component, and reset behavior. This validates state and structure; computed layout is left to the separate gate.

# Could not do

None. All planned functionality is implemented. Illustrations are deliberately schematic, consistent with the plan's accuracy limits.

# Omitted for lack of a service

None. This implementation needs no external service.
