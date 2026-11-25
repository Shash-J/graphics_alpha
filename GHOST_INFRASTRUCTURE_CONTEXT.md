# Ghost Infrastructure — Project Handoff

## Start here

**Ghost Infrastructure — Evidence-Based 3D Visualization of Concealed Plumbing** is a proposed Computer Graphics and Virtual Reality (CGVR) course project for a final-year CSE team at RV College of Engineering, Bengaluru. This handoff treats **Ghost Pipeline** as the name for that concealed-plumbing proposal.

Build a browser app that helps someone reviewing a renovation or maintenance plan answer three questions. Where did the drawing show a pipe? Where was part of it actually observed? What should someone inspect next to resolve the discrepancy?

The project’s contribution is the connection between **3D pipe geometry, the evidence behind each segment, and the limits of that evidence**. An old plan establishes design intent. A dated photo with a location measurement can establish where a visible span was observed. Several concealed routes can fit the same visible clues, so the viewer must make the distinction obvious.

### Repository and project status

- Use [Shash-J/graphics_alpha](https://github.com/Shash-J/graphics_alpha), default branch `main`. The team asked for project work to be committed and pushed there.
- At handoff, the repository contained an ideas README and this document. No application, model assets, inspection dataset, or tests had been committed.
- The README also describes **House Rehearsal**, a later proposal for evaluating daily routes through the student’s rough Blender house. Its inputs are household routines and walkable geometry. Its outputs are route distances and bottlenecks. This handoff covers the concealed-plumbing proposal.
- The course rubric, deadline, headset requirement, available evidence, and final choice between project directions were still open. The scope and stack below are recommendations for continuing Ghost Infrastructure.

## Proposed deliverable

Use **one floor, two adjacent rooms, one plumbing line, and one discrepancy** between a dated design drawing and a later observation. Show part of the line directly observed, one plausible continuation, and a section whose route is unresolved.

### Inputs

| Input | Minimum information |
| --- | --- |
| Dimensioned floor plan | Two rooms, the shared wall or service chase, and a known reference corner and dimension. |
| Original plumbing record | A drawing or sketch showing the intended route, with a source date and a clearly marked excerpt. |
| Inspection evidence | A dated photo and a note identifying the visible span. Measure its location from a fixed reference such as the corner and floor. |
| Curated JSON scene | Room and wall geometry, pipe segment coordinates, evidence references, and the explanation behind any inference. The team prepares this file manually. |

Use a measured teaching mock-up if suitable building records are unavailable. A pipe layout with a removable panel lets the team photograph the exposed section and independently document the complete route for later validation. Mark all staged records accordingly. A rough Blender house export can provide room geometry if its scale is known and it fits the case. Its meshes alone establish only the modeled layout.

### Viewer behavior

| Evidence state | Representation |
| --- | --- |
| **Planned** | A labelled route in the **Original plan** view. Selecting the segment opens the relevant drawing excerpt and date. |
| **Observed** | A solid pipe in the **Inspection** view. Selecting it opens the dated photo and the measurement or note for the visible span. |
| **Inferred** | A dashed path labelled **Inferred**. The evidence panel names the supporting clues and the assumption that connects them. |
| **Unknown** | A visible gap with a labelled marker at the last known point or a known access point. The markers identify an unresolved question while the hidden geometry remains unspecified. |

Provide orbit, pan, zoom, and a reset view. Add a movable section plane to reveal the route inside the architectural shell. Give the evidence panel a short source title, date, excerpt or photo, and a description of what it supports. Use line styles and text labels so users can distinguish evidence states without relying on color.

### A demo case the team can author

1. The original plan shows a pipe penetration 0.60 m from a reference corner along the shared wall.
2. A later mock inspection identifies the corresponding branch at an exposed penetration, 1.20 m from the same corner. A photo and measurement show the exposed portion. The numbers in this example are proposed mock data.
3. The viewer lets the user compare both positions and check the source for each. Show a plausible continuation from the exposed span as dashed, then leave the next unresolved interval open.
4. End the demo by asking whether the utility-side access panel would let the inspector trace the rest of the line. A later panel-off photo can show what was actually there.

Keep the plan and observation available together. Record the dates on their respective sources. A discrepancy establishes a difference between the records. Installation or rerouting dates stay unknown unless a separate record establishes them.

## Suggested implementation

- Use **TypeScript, Vite, and Three.js** with a desktop browser, a bundled JSON dataset, and local evidence images. Check the course rubric early and confirm hardware availability if headset interaction is assessed.
- Use **metres and one shared origin** for all scene coordinates. Put the floor in X/Z and use Y for height. Calibrate against a known dimension and check a second distance against the plan or mock-up.
- Build **simple meshes** for walls, floors, and solid pipe spans. Use a dashed line or dashed tube for an inference. Keep walls and floors visually subdued so the pipe states are easy to see.
- Give each selectable rendered object or gap marker a **stable model ID**. Use raycasting to select it and resolve its source in the evidence panel. Exclude hidden routes and intersections on clipped surfaces from picking where applicable.
- Move a **Three.js clipping plane** on the architectural shell with a slider. Confirm that a visible pipe can still be selected when the cutaway exposes it.
- Keep **dataset editing in source files** for the first prototype.

### Suggested data contract

| Record | Fields to establish in the first dataset |
| --- | --- |
| Building shell | Metre units, origin, room IDs, and wall/floor geometry in scene coordinates. |
| Pipe segment or route claim | Stable ID, pipe ID, view, evidence state, route points where supported, linked evidence IDs, and an explanation for any inferred geometry. A planned and an observed segment can share a pipe ID and retain independent geometry and evidence. |
| Evidence item | Stable ID, source type, title, source date when known, a local asset or text excerpt, and the exact observation or plan detail that supports the claim. |
| Unknown section | Stable ID, a known marker location if available, a note about missing evidence, and a proposed inspection point if the case supports one. |

Keep planned and observed claims independent. A photo showing one end of the pipe can support that span, while the next span remains inferred or unknown. Resolve evidence references by ID so changing views or rebuilding meshes leaves the connection to the source intact.

## Build sequence and checks

1. **Prepare one evidence case.** Draw the two rooms, pick one reference corner, and identify the planned position, observed position, inference, and unknown interval. Write down the source for every claim before modeling it.
2. **Build one complete interaction.** Render the rooms and a single observed pipe span. Add the cutaway and click-to-source interaction. Validate the location against the known measurement.
3. **Add the comparison.** Support the two views, the remaining evidence states, and the gap marker. Check that selecting a component after switching views shows the correct source and that hidden or clipped geometry cannot intercept a click.
4. **Test with known answers.** Check dimensions, evidence IDs, and the expected appearance of each state. If there is a mock-up, keep the complete panel-off record out of the initial dataset and use it to check the modeled positions after the demo. Ask classmates to identify what was observed, say where the two records disagree, and choose what to inspect next. Record any case where a participant treats an inferred route as observed.
5. **Package the submission.** Deliver the runnable app, sample inputs, setup instructions, a short report covering method and limitations, and a short demo video. Use a sample dataset the team can share with the public repo.

The first coding milestone is complete when someone can load the scene, reveal a pipe through the cutaway, click the visible span, and open the exact source that establishes its position. The final demo should also make it easy for the same person to explain what the model leaves uncertain and why.

## References

- Background on why real building records can be incomplete and how multiple observations can capture otherwise concealed services. [Constructing as-is BIMs from progressive scan data](https://www.iaarc.org/publications/fulltext/Constructing_as-is_BIMs_from_progressive_scan_data.pdf)
- Background on tracing a claim or artifact to its sources. [W3C PROV Model Primer](https://www.w3.org/TR/prov-primer/)
- Three.js APIs for the proposed viewer and interaction. [OrbitControls](https://threejs.org/docs/pages/OrbitControls) · [Material clipping planes](https://threejs.org/docs/pages/Material.html) · [Raycaster](https://threejs.org/docs/pages/Raycaster)
- If using Blender for the shell, export the relevant section as a `.glb`. [Blender glTF export guide](https://docs.blender.org/manual/en/latest/addons/scene_gltf2.html)
