# jbms-parser
BMS and BMSON Parser based on Java.

## Arena compatibility revision 2

The Arena fork accepts whitespace after BM98-era `#mmmcc` headers and retains
LNOBJ objects following an already completed LN as normal notes. Source bytes,
MD5, SHA-256, BASE and selected RANDOM branches remain unchanged. Use
`BMSDecoder.setLegacyCompatibility(true)` only to restore previously recorded
replays with the historical note interpretation.

Decoder-owned model values `bmsir.parser.revision` and `bmsir.parser.affected`
allow callers to separate local PB/replay storage without changing public chart
identity. Whitespace is detected across all source branches. Conditional LNOBJ
charts are conservatively marked across all branches, so the storage namespace
cannot change when a different RANDOM branch is selected. Callers must preserve
old PBs instead of rewriting them onto the corrected note count.

BMP00 initializes the default MISS image; explicit channel 06 takes precedence.
Standard BMSON `{y,id}` layer events use the persistent timeline layer.
Undocumented extended sequence/conditional events retain their prior handling.

Compatibility regression tests and integration validation live in
[`oraja` Issue #497](https://github.com/tenP0312-dev/oraja/issues/497), including
legacy replay restoration, unchanged hashes, RANDOM namespace stability, local
PB separation, BMP mapping and standard BMSON layers.
