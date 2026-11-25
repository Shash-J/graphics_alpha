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

## Proposal — Evaluate daily routines

Expand House Rehearsal into a comparison tool for early-stage house layouts. Given the same resident profile and routine frequencies, show which routes are feasible, how far the person would walk, and where the model leaves little clearance. The results describe movement for the selected routines under stated assumptions.

- **Input** is a scaled single-floor Blender export with walls, openings, major furniture, and manually marked standing points. Each routine specifies its stops in order and its expected runs per day. The resident profile specifies the space needed to pass.
- **Feasibility** is checked for every leg. Report blocked or unassessed routines explicitly. Only compare the full daily totals when the same routines are all feasible and assessed in both layouts.
- **Daily walking distance** is the sum of each complete routine's route length multiplied by its runs per day. Record the tightest clearance along each route so the user can see where a shorter layout may feel cramped.
- **Demo** compares two versions of one floor using three routines, such as bed to bathroom, sofa to kitchen and back, and entry to kitchen with groceries. Animate the computed paths and mark bottlenecks in the 3D view.
- **Validation** uses simple plans with measured distances, a blocked passage, a narrow opening, and an obstacle that forces a detour. Then run the same scenarios on both house layouts.

### Related work

- Autodesk Revit calculates obstacle-aware routes and travel distances between two points on one level. [Revit Path of Travel](https://help.autodesk.com/cloudhelp/2025/ENU/Revit-Analyze/files/GUID-84C3AD28-8F10-4468-AD06-D740F81D7FC3.htm)
- Na and colleagues built a prototype that scored apartment kitchen designs using patterns extracted from building models. [Performance evaluation of building designs with BIM-based spatial patterns](https://doi.org/10.1016/j.autcon.2020.103290)
- BIM3DSim uses annotated building models and scripted virtual occupants to generate indoor activity traces for smart-space simulation. [Towards a Simulation Framework for Smart Indoor Spaces](https://www.mdpi.com/1424-8220/20/24/7137)
- A VR housing study evaluated circulation and wheelchair maneuvering in furnished virtual homes. [Evaluation of Universal Accessible Housing Design Using Virtual Reality](https://www.mdpi.com/2076-3417/15/11/5936)
