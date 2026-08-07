# Aixio Layer v1 — Model Card

## Model summary

Aixio Layer v1 is a 52B-parameter image-to-layer model trained in-house for the reconstruction of editable design structure from a single flat raster image. It separates visual elements, recovers text as editable type, reconstructs regions hidden behind foreground objects, and returns an ordered composition that can be continued in Aixio Studio.

| Field | Description |
| --- | --- |
| Model name | Aixio Layer v1 |
| Developer | Aixio |
| Release year | 2026 |
| Primary task | Image-to-layer reconstruction |
| Input | PNG, JPEG, screenshot, export, or other raster image |
| Output | Ordered visual layers, editable text, reconstructed background, and composition metadata |
| Model size | 52B parameters |
| Availability | Aixio Studio |
| Weights | Not publicly released |

## What the model is designed to do

Layer v1 addresses a different problem from ordinary foreground segmentation. A useful editable reconstruction requires the model to recover several kinds of information at once:

1. **Recognition** — identify the meaningful visual and textual elements in the design.
2. **Layer separation** — isolate elements with usable transparency.
3. **Ordering and grouping** — infer which elements belong together and how they stack.
4. **Amodal completion** — predict the parts of backgrounds or objects hidden in the input.
5. **Typography recovery** — return copy as editable strings with visual styling when available.
6. **Detail reconstruction** — preserve useful texture and edge detail during decomposition.

The model is described as task-specific and end-to-end rather than a user-visible chain of independent segmentation and inpainting tools.

## Intended uses

- Recover editable structure when the original design file is missing.
- Revise or localize text in posters, ads, slides, and social graphics.
- Move, remove, resize, or restyle elements in a flattened composition.
- Recover reusable visual assets from exports, screenshots, or AI-generated imagery.
- Prepare existing visuals for continued editing in Aixio Studio.

## Uses requiring care

- High-stakes forensic, scientific, journalistic, or legal reconstruction.
- Any workflow that treats generated hidden regions as a factual record.
- Trademark, copyright, or identity-sensitive reuse without appropriate rights.
- Automated publication without a human review of text, layout, and reconstructed areas.

## Output semantics

### Visual layers

Visual elements are returned with RGBA transparency and placement information. The goal is a usable editable part, not merely a binary mask.

### Text layers

Recognized copy can be returned as editable text with recovered attributes such as font family, weight, size, color, alignment, tracking, and placement. Exact recovery depends on image quality, typography complexity, and font availability.

### Reconstructed background

Areas hidden by foreground elements are synthesized from the visible context. This makes common design operations possible, but the reconstruction is a model prediction rather than recovered source data.

### Composition structure

Layers are organized in an inferred order and may include grouping, orientation, perspective, and other transform information needed to preserve the visual hierarchy.

## Evaluation

Aixio's internal materials describe an evaluation set built from real layered PSD and Figma designs. The files are flattened to form model inputs while their original layers serve as ground truth. The reported evaluation covers 10,000 images across 36 categories and scores predicted alpha against ground-truth alpha using mean intersection over union.

The currently reported internal result is **94% layer-decomposition accuracy**. Treat this as an Aixio-reported result until the evaluation set, scoring code, and full per-category results are publicly linked. See [Evaluation and comparison notes](EVALUATION.md).

## Known limitations

- Low-resolution or heavily compressed sources can reduce boundary and text quality.
- Dense compositions may contain ambiguous groupings or layer order.
- Stylized, curved, distorted, or partially hidden typography can require correction.
- Exact font recovery depends on the original font being identifiable and available.
- Reflections, shadows, translucency, hair, fine texture, and motion blur remain difficult cases.
- Occluded content is inferred and may differ from the original source artwork.
- Output should be reviewed before production use, especially for small copy and brand-critical details.

## Access and release status

Layer v1 is currently delivered through [Aixio Studio](https://aixio.app/studio). This documentation does not imply that model weights, training data, training code, or a local inference package are public. Any future API or downloadable release should include separate versioning, usage terms, and technical documentation.

## Versioning

This card describes **Layer v1**. Material changes to the model, supported outputs, evaluation protocol, or availability should be recorded as a new version or dated revision rather than silently replacing the claims here.
