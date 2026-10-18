# Parser revision 3: unmatched LNOBJ at the start of a visible lane

When an LNOBJ has no preceding visible note on its lane, revision 3 keeps it
as a normal note. Hidden notes do not become LN starts. This changes geometry;
do not repair only an exported total-note count.

The default decoder selects revision 3. `setCompatibilityRevision(1|2)` restores
the recorded historical geometry; `setLegacyCompatibility(true)` still selects
revision 1. Original MD5/SHA-256 values remain unchanged.

Decoder-owned flags distinguish the new geometry from revision-2-only changes.
Conditional LNOBJ sources conservatively share a namespace across selected
RANDOM branches. Consumers must isolate changed local PB/replay keys and keep
the prior interpretation available; the matching Arena body implements this.

Regression fixtures live in the paired Arena body: BMSLegacyCompatibilityTest,
OrphanLnobjIdentityTest and ParserStorageCompatibilityTest. They cover initial
LNOBJ on both sides and scratches, hidden notes, normal LN/CN/HCN, forced LN,
RANDOM branches, unchanged public hashes and historical score/replay isolation.
