# Tablyx Figma component inventory (live, 2026-08-18)

Measured via the Figma Plugin API over the Molecule + Organism pages of
**Tablyx – Design System** (fileKey `SznEOiskoPnC0o9GWd7DS9`). 24 top-level reusable
components (component sets + standalone components). Variant axes shown in `[...]`;
`TEXT`/`INSTANCE_SWAP` are component properties.

## Molecules

- **Button** `1:361` (SET) — `Label:TEXT`, `Type[Primary|Secondary|Ghost|Destructive|Destructive · outline]`, `Size[lg|md|sm]`, `State[Default|Hover|Focus|Pressed|Disabled]`
- **Icon button** `1:398` (SET) — `Icon:INSTANCE_SWAP`, `Size[lg|md|sm]`, `State[Default|Hover|Pressed|Disabled|Focus]`
- **Input** `1:508` (SET) — `Value:TEXT`, `Size[lg|md|sm]`, `State[Default|Hover|Focus|Disabled]`, `Filled[No|Yes]`, `Validity[None|Error]`
- **Form field** `1:532` (SET) — `Label:TEXT`, `State[Default|Error|Disabled]`
- **Switch** `1:407` (SET) — `Value[Off|On]`, `State[Default|Disabled|Focus]`
- **Checkbox** `1:420` (SET) — `Value[Unchecked|Checked|Indeterminate]`, `State[Default|Disabled|Focus]`
- **Radio** `1:425` (SET) — `Value[Unselected|Selected]`, `State[Default|Disabled|Focus]`
- **Tab** `1:439` (SET) — `Label:TEXT`, `Icon:INSTANCE_SWAP`, `State[Rest|Hover|Selected]`, `Focus[No|Yes]`
- **Counter badge** `1:446` (SET) — `Count:TEXT`, `Tone[Neutral|Accent|Destructive]`
- **Status stamp** `1:471` (SET) — `Label:TEXT`, `Status[Preparing|Ready|Delayed|Paid|Unpaid|Sold out]`, `Density[comfortable|compact]`

## Organisms

- **Sidebar row** `1:551` (SET) — `Label:TEXT`, `Icon:INSTANCE_SWAP`, `State[Rest|Hover|Selected]`, `Focus[No|Yes]`
- **Top bar** `1:552` (COMPONENT) — no props
- **Table row** `1:622` (SET) — `State[Rest|Hover|Selected]`, `Focus[No|Yes]`
- **Filter bar** `1:623` (COMPONENT) — no props
- **Table header** `1:637` (COMPONENT) — no props
- **Pagination** `1:660` (COMPONENT) — no props
- **Selection bar** `1:676` (COMPONENT) — `Count:TEXT`
- **Table** `1:687` (COMPONENT) — no props
- **Dialog** `1:959` (SET) — `Heading:TEXT`, `Description:TEXT`, `Width[lg|md|sm]`, `Tone[Neutral|Destructive]`
- **Side panel** `1:1052` (SET) — `Heading:TEXT`, `Meta:TEXT`, `Width[lg|md]`
- **Toast** `1:1087` (SET) — `Title:TEXT`, `Detail:TEXT`, `Status icon:INSTANCE_SWAP`, `Action icon:INSTANCE_SWAP`, `Tone[Success|Warning|Error|Undo]`
- **Empty state** `1:1106` (SET) — `Heading:TEXT`, `Description:TEXT`, `Icon:INSTANCE_SWAP`, `Tone[Empty|Error]`
- **Kitchen ticket** `1:1215` (SET) — `Order:TEXT`, `Timer:TEXT`, `State[New|Preparing|Delayed]`
- **Table skeleton** `1:1107` (COMPONENT) — no props

Excluded from mapping: Atoms (token/specimen pages), Templates/Screens (assembled
compositions of instances), Utilities (file-components tail).
