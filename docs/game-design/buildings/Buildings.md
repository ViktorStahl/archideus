---
aliases:
  - Building
---
## Construction
Buildings are placed as foundations, either as a fixed-size foundation or alternatively zoned into a rectangular foundation of a size the player chooses. Buildings always have the following attributes related to their construction:
- **Resource cost** - The amount of [Wood](Wood.md), [Stone](Stone.md), etc. reserved when placing the foundation. If player doesn't have the resources available the placement is not allowed.
- **Labour time** - The amount of labour required to finish the construction which is used to measure the progress of construction.
- **Required research** - Some buildings are locked behind a research.
- **Priority** - Is connected to a foundation during its construction. There are 5 priority levels: Highest, High, Medium, Low, Lowest. Medium being the default priority.
The resource cost is reserved as soon as the building foundation is placed. If a foundation is deleted/destroyed before being constructed a percentage of the reserved resources are returned equal to the remaining labour time.
### Progress
Progress is added based on the labour available at the [Core Frequency](Simulation.md#Core%20Frequency) to a maximum of 1 % progress per increment. Additional labour is simply not used. This ensures [Oikos](Oikos.md) are not instantly constructed even if they have no required labour time.
When multiple buildings are constructed at the same time the labour is first allocated to the buildings with the highest priority, divided equally, and then if there is labour to spare allocated to the next priority level, and so fourth.
## Consumption and Production
Some buildings produce goods. To do this they often consume [Labour](Labour.md) or a resource, sometimes both.