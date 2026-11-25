# Graphics Alpha

CGVR project ideas based on an early-stage house model built in Blender. The goal is to use the model to test a design decision while the layout is still easy to change.

## Project shortlist

| Idea | Design question | What we would build |
| --- | --- | --- |
| **House Rehearsal** | Can someone walk through the kitchen while an appliance door is open or a chair is pulled out? | A 3D comparison of two layouts. Replay a short walking route while opening a door, and highlight where the body and door overlap or where the route gets narrow. |
| **Sightline Lab** | Can a visitor at the front door see the sofa or dining area? | An eye-level walkthrough that visualizes what walls, doors, and partitions block. Compare two divider placements using the same viewpoints. |
| **Furniture Move-In Simulator** | Will the sofa clear the entrance and turn through the hallway? | A 3D interaction for moving, rotating, and tilting a dimensioned furniture proxy. Highlight collisions with walls, frames, and ceilings. |
| **Sunlight Explorer** | Which window placement gives a room more direct morning sun? | A date and time slider that visualizes approximate direct sunlight and shadows for a known location and house orientation. |
| **Utility Route Sandbox** | Where could a pipe or conduit pass if the kitchen or utility room moves? | A cutaway that compares two explicitly proposed routes and highlights intersections with modeled walls or beams. |

## Recommended first prototype

Start with **House Rehearsal**. Use the kitchen and dining area, two layout variants, one hinged door, and one walking route. Play the same scenario in both layouts and show the conflict in 3D. Confirm one real dimension to establish scale before showing clearance measurements. Treat the results as comparisons of the modeled geometry and assumed dimensions.

Use Blender as the authoring tool and export the test area as a `.glb` for a browser prototype. Simple boxes and planes are enough for the test. [Blender glTF export guide](https://docs.blender.org/manual/en/latest/addons/scene_gltf2.html)
