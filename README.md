# OpenCircuit PCB Semantic Diff

Semantic comparison for KiCad `.kicad_pcb` files. It parses the board structure and reports electrical and physical design changes instead of overwhelming reviewers with S-expression text movement.

## Compared entities

- Nets and net renames.
- Footprint additions/removals, library identifiers, values, layers, positions, and rotations.
- Pad additions/removals, nets, types, shapes, dimensions, and drills.
- Copper tracks, widths, layers, and nets.
- Vias, sizes, drills, layers, and nets.
- Edge.Cuts outline segments.
- Copper-zone count.
- Before/after design statistics.

Changes are classified as `critical`, `warning`, or `info`. Position, rotation, and size tolerances suppress insignificant serialization noise.

## CLI

```bash
pcb-semantic-diff main.kicad_pcb proposed.kicad_pcb
pcb-semantic-diff main.kicad_pcb proposed.kicad_pcb --format markdown --output review.md
pcb-semantic-diff main.kicad_pcb proposed.kicad_pcb --format json --position-tolerance 0.01
```

Exit status is `2` for critical changes, `1` for warnings, and `0` for identical or informational-only results.

## Library

```js
import { parseKiCadPCB, diffBoards, toMarkdown } from '@opencircuitlabs/pcb-semantic-diff';

const report = diffBoards(parseKiCadPCB(before), parseKiCadPCB(after));
console.log(toMarkdown(report));
```

## Scope

This release covers the review-critical subset of modern KiCad PCB files. Text graphics, dimensions, rule definitions, 3D models, teardrops, tuning patterns, and full zone polygon geometry remain visible through file-level Git diffs until dedicated semantic extractors are added.

## License

MIT © 2026 OpenCircuitLabs
