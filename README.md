# Human CS9 embryo — Stereo-seq and scRNA-seq processed data

A **verbatim mirror** of [`10.5281/zenodo.14730926`](https://doi.org/10.5281/zenodo.14730926), redistributed under the terms of the licence the depositors chose. No file has been modified.

## Attribution

> Depositors of Zenodo record 14730926
>
> 10X scRNA-seq and Stereo-seq processed data for paper 'Spatial Transcriptomic 3D Reconstruction of the Human Embryo' (2025). Zenodo, doi:10.5281/zenodo.14730926.
>
> DOI: [10.5281/zenodo.14730926](https://doi.org/10.5281/zenodo.14730926) — licensed **CC BY 4.0**

Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); see [`LICENSE`](LICENSE). You may share and adapt this material for any purpose, including commercially, provided you give appropriate credit, link to the licence and indicate if changes were made. **This mirror makes no changes.**

## What this is

Spatial and single-cell transcriptomics of a human embryo at Carnegie stage 9, as .h5ad and .rds. 96,837 Stereo-seq spots across 29,627 genes with 22 annotated cell types, including notochord, neural plate, neuromesodermal progenitors, presomitic and cardiac mesoderm. The only confirmed openly-licensed human embryo spatial transcriptomic dataset this project has found.

## Provenance of the material

A human embryo specimen. The deposit records no ethics statement or consent documentation of its own and this project has not established what applied.

## Contents

4 file(s), 1607.1 MB total.

**2 of these exceed GitHub's 100 MB per-file limit** and are published as assets on the [latest release](../../releases/latest) rather than committed to the tree. The repository holds the manifest and the licence; the release holds the bytes. Fetch them with:

```sh
gh release download --repo embryogenesis/cs9-2025-spatial-transcriptome --dir data
```

| File | Size | SHA-256 |
| --- | --- | --- |
| `data/cs9_scRNA_annotation.h5ad` | 18.0 MB | `59de122e52650370…` |
| `data/cs9_stereo_annotation.rds` _(release asset)_ | 770.1 MB | `3d82fee03956e8c3…` |
| `data/cs9_scRNA_annotation.rds` | 22.1 MB | `ed68ab2f2a6a9f9c…` |
| `data/cs9_stereo_annotation.h5ad` _(release asset)_ | 796.9 MB | `1bc409b870cd8007…` |

Full checksums, original filenames and the source article id for every file are in [`MANIFEST.json`](MANIFEST.json).

(2 smaller file(s) are committed normally.)

## Notes for anyone using this

- IMPORTANT: there is no 3D spatial coordinate in the .h5ad files. /obsm is empty and /uns is absent — no spatial array, no section thickness, no registration transform. The x and y are recoverable only by decoding each spot ID (EF1_<section>_<digits>, stepping by 50 within a row, so Stereo-seq bin50), and the third dimension is a section index with 13 distinct values labelled 2 to 14. Anyone stacking those 13 sections into a volume is inventing the spacing.
- The bin step is 50 in the deposit's own units and the files never state what those units are, so no physical dimension can be taken from the coordinates without establishing the pitch elsewhere.
- The .rds files are R serialisation and may carry section spacing the .h5ad pair lacks; uninspected as of this mirror.
- Read the .h5ad with tools/library/h5read.py, which needs no HDF5 dependency.

## Verifying the mirror

```sh
# every file, against the manifest
python3 -c "import json,hashlib,pathlib;m=json.load(open('MANIFEST.json'));[print(('ok  ' if hashlib.sha256(pathlib.Path(f['path']).read_bytes()).hexdigest()==f['sha256'] else 'BAD ')+f['path']) for f in m['files'] if pathlib.Path(f['path']).exists()]"
```

---

Mirrored 2026-11-22 by `tools/mirror.ts` from [embryogenesis](https://github.com/embryogenesis/embryogenesis). The licence of each source record was checked against the live Zenodo metadata (`metadata.license.id`) before download. A record stating no licence aborts the mirror rather than defaulting to one.
