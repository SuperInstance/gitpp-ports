# gitpp-ports — the 7 fold ports at a glance

A landing page listing every fold port with version, conformance, and
fuzz-test status. **The single source of truth** for "which port is
on which version".

## 7 ports, one algorithm

| # | Port | Language | Repo | Version | Conformance | Fuzz (500 rec) | Doc-only | Status |
|---|------|----------|------|---------|-------------|----------------|----------|--------|
| 1 | `git.pp-ng` (hub) | TypeScript | [`patchwork-quilt/git.pp-ng`](https://github.com/patchwork-quilt/git.pp-ng) | - | 1,151 / 1,151 | n/a | n/a | in production |
| 2 | `git.pp-ng/referee/` | Python | [`patchwork-quilt/git.pp-ng`](https://github.com/patchwork-quilt/git.pp-ng) (referee/) | - | 1,151 / 1,151 | 500/500 | yes | reference |
| 3 | `gitpp-beam` | Elixir | [`patchwork-quilt/gitpp-beam`](https://github.com/patchwork-quilt/gitpp-beam) | - | (per hub) | n/a | yes | converged |
| 4 | `gitpp-js` | JavaScript (ESM) | [`SuperInstance/gitpp-js`](https://github.com/SuperInstance/gitpp-js) | v0.1.2 | 28 / 28 public | 500/500 | yes | live |
| 5 | `gitpp-cs` | C# / .NET 9 | [`SuperInstance/gitpp-cs`](https://github.com/SuperInstance/gitpp-cs) | v0.3.1 | 28 / 28 public | 500/500 | yes (after v0.3.0) | live |
| 6 | `gitpp-pl` | Perl 5 | [`SuperInstance/gitpp-pl`](https://github.com/SuperInstance/gitpp-pl) | v0.1.3 | 28 / 28 public | 500/500 | yes | live |
| 7 | `gitpp-c` | C99, stdlib | [`SuperInstance/gitpp-c`](https://github.com/SuperInstance/gitpp-c) | v0.1.1 | 28 / 28 public | 500/500 | yes | live |
| - | `gitpp-rust` | Rust | [`SuperInstance/gitpp-rust`](https://github.com/SuperInstance/gitpp-rust) | scaffold | (not yet) | (not yet) | pending | pending cargo |

## Cross-port byte-equivalence

**500/500 random float64 records** produce **byte-identical SHA-256
leaves** across all 5 fold ports (Python, JS, C, C#, Perl). The
17,004-record full corpus is in progress in the background.

The fuzz runner is at [`SuperInstance/gitpp-cross-port/fuzz.mjs`](https://github.com/SuperInstance/gitpp-cross-port/blob/main/fuzz.mjs).

The 4 pinned `cross-port-leafs.json` cases match every port.
The 30-case cross-port canonical test passes every port.
The 1,151-case private conformance corpus matches the hub + Python
+ Elixir.

## How the 5 fold ports agree

Per spec §3 (leaf-number encoding), all 5 ports:
1. Use `, ` and `: ` as separators (not compact).
2. Sort object keys by Unicode code point.
3. Always emit `reason: null` (never omit).
4. Treat `|v| < 1e16` as integer form; else scientific with
   15/16/17 sig-digit fallback to round-trip.
5. Use literal Unicode in strings (no `\uXXXX`).

These rules were validated by the cross-port fuzz: any drift in
(1)-(5) shows up as a different leaf hash.

## Bilingual ports

A port is "bilingual" if it follows the **doc-only discipline**:
written from the public spec alone, not from any other port's
source. All 5 active fold ports are bilingual — the spec is
normative. A future port written from the spec, not from another
port, is a proof that the spec is complete.

## Versions

| Port | v0.1.0 → current | Notable changes |
|------|------------------|-----------------|
| `gitpp-js` | v0.1.0 → v0.1.2 | v0.1.1: `numFormat()` for float precision; v0.1.2: 1e16 integer limit |
| `gitpp-cs` | v0.1.0 → v0.3.1 | v0.3.0: refactor library methods; v0.3.1: 1e16 limit, 15/16/17 sci fallback |
| `gitpp-pl` | v0.1.0 → v0.1.3 | v0.1.1: 5 bug fixes; v0.1.2: 1e16 limit; v0.1.3: integer check uses arithmetic |
| `gitpp-c` | v0.1.0 → v0.1.1 | v0.1.1: 1e16 integer limit (was 1e21) |
| `git.pp-doctor` | v0.1.0 → v0.2.1 | v0.2.1: 1e16 integer limit |

## See also

- **Spec**: [`SuperInstance/git.pp-spec`](https://github.com/SuperInstance/git.pp-spec) v0.3.5
- **Explainer**: [`SuperInstance/what-is-the-quilt`](https://github.com/SuperInstance/what-is-the-quilt)
- **Cross-port artifact**: [`SuperInstance/gitpp-cross-port`](https://github.com/SuperInstance/gitpp-cross-port)
- **Conformance corpus**: [`SuperInstance/gitpp-conformance`](https://github.com/SuperInstance/gitpp-conformance)
- **Doctor** (Python reference): [`SuperInstance/git.pp-doctor`](https://github.com/SuperInstance/git.pp-doctor)
