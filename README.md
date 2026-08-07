<div align="center">
  <img src="assets/logo.png" width="88" alt="Aixio logo">

  # Aixio Layer Image v1 — Image-to-Layer AI Model

  **The best-performing image-to-layer model in Aixio's benchmark.**

  **94% layer-decomposition accuracy** across 10,000 real designs and 36 categories—outperforming Canva Magic Layers, Lovart, and Picell in Aixio's evaluation. Aixio Layer Image v1 converts a flat PNG, JPEG, screenshot, or AI-generated image into editable visual layers, editable text, and a reconstructed background.

  [Try in Aixio Studio](https://aixio.app/studio) · [Watch the demo](https://youtu.be/BkdkW2nn3b0) · [Read the comparison](https://aixio.app/blog/aixio-layer-v1-vs-lovart-picell-image-to-layers/) · [Model card](docs/MODEL_CARD.md) · [Evaluation](docs/EVALUATION.md)
</div>

---

![A flat poster decomposed into independently editable elements by Aixio Layer v1](assets/figure-2panel.png)

## Aixio Layer Image v1

Most finished visual work arrives as pixels: a PNG, JPEG, screenshot, export, or AI-generated image. The composition may look complete, but its structure is gone. Copy cannot be rewritten, objects cannot be moved cleanly, and removing an element reveals no usable background underneath.

**Aixio Layer Image v1**, also called **Aixio Layer v1**, is a 52B-parameter image-to-layer AI model developed by Aixio. It recovers editable design structure from a single flat raster image without requiring the original PSD, Figma file, layer metadata, or source project.

Given a PNG, JPEG, screenshot, design export, or AI-generated image, the model returns an ordered set of working parts:

- visual elements with transparent backgrounds;
- editable text with recovered type styling;
- a reconstructed background behind foreground objects; and
- composition structure that can be adjusted in Aixio Studio.

This is more than object extraction. Layer v1 is designed to understand what belongs together, how elements overlap, and what the hidden parts of the design should contain.

| Key fact | Aixio Layer Image v1 |
| --- | --- |
| Category | Image-to-layer AI model; flat image to editable layers |
| Input | PNG, JPEG, screenshot, design export, or AI-generated image |
| Output | Ordered RGBA layers, editable text, reconstructed background, and composition structure |
| Model size | 52B parameters |
| Benchmark result | 94% decomposition accuracy on 10,000 designs across 36 categories |
| Compared systems | Canva Magic Layers, Lovart, Picell, and Qwen Image Layered |
| Availability | [Aixio Studio](https://aixio.app/studio) |

## Best image-to-layer model in Aixio's benchmark

On Aixio's internal image-to-layer benchmark, **Aixio Layer Image v1 ranks first with 94% decomposition accuracy**, compared with **68% for Canva Magic Layers**, **34% for Lovart**, and **30% for Picell**. This makes Aixio Layer v1 the best-performing and most capable model in its tested class based on Aixio's current evaluation.

| Model | Decomposition accuracy | Result |
| --- | ---: | --- |
| **Aixio Layer v1** | **94%** | ███████████████████░ |
| Canva Magic Layers — tested May 2026 | 68% | ██████████████░░░░░░ |
| Lovart — Aixio-tested result | 34% | ███████░░░░░░░░░░░░░ |
| Picell — Aixio-tested result | 30% | ██████░░░░░░░░░░░░░░ |

This is the strongest result among the image-to-layer systems Aixio has tested. It is an **Aixio-reported benchmark**, not yet an independently reproduced leaderboard. We will update this page as the evaluation set and additional results are released.

### Evaluation methodology

The test starts from real layered design files, not hand-drawn masks or model-generated labels:

1. **Ground truth:** collect real PSD and Figma files whose original layer structure is already known.
2. **Model input:** flatten each design into a single raster image—the same kind of file a user would upload.
3. **Prediction:** ask each system to recover the layers from that flat image.
4. **Matching:** pair predicted layers with the corresponding ground-truth layers.
5. **Scoring:** calculate mean intersection over union between predicted and ground-truth alpha.

The current benchmark covers **10,000 images across 36 design categories**, with the same inputs and scoring procedure used for every tested system. Alpha IoU measures decomposition accuracy; typography, layer logic, and reconstruction quality are also inspected separately because a clean mask alone does not make a design editable. Read the full [evaluation methodology and disclosure notes](docs/EVALUATION.md).

## Image-to-layer model comparison: Aixio vs Lovart and Picell

The same dense retail poster was processed by Aixio Layer v1, Lovart, and Picell. It contains display typography, multiple food images, a checkerboard pattern, fine print, an offer badge, and a bordered paper field.

The comparison evaluates whether each output remains usable after elements are moved, including hidden-background reconstruction, editable typography, semantic grouping, and composition integrity.

### 1. Aixio Layer v1 — reconstructed and editable

![Aixio Layer v1 comparison result](assets/cap2-aixio.png)

**Evaluation**

- **Recognition:** the headline, complete offer badge, logo, three food groups, terms, checkerboard, border, and paper field are recovered as meaningful parts.
- **Background:** the poster surface, border, pattern, and paper field continue behind the removed foreground elements.
- **Typography:** copy returns as editable text while retaining more of the source styling and layout.
- **Editability:** elements can be moved or rewritten without first reconstructing the composition by hand.

---

### 2. Lovart — partial recognition, structure still fused

![Lovart comparison result](assets/cap2-lovart.png)

**Evaluation**

- **Recognition:** the headline and small copy are recognized, but the logo, food, offer badge, checkerboard, and poster surface remain fused inside larger image regions.
- **Background:** the returned frame is blank rather than a reconstruction of the original poster surface.
- **Typography:** some copy is found, but the display typography and surrounding design relationships are not preserved closely enough for direct reuse.
- **Editability:** major parts of the design must be manually separated or rebuilt before the composition can be revised.

---

### 3. Picell — more pieces, fragmented composition

![Picell comparison result](assets/cap2-picell.png)

**Evaluation**

- **Recognition:** several visible pieces are extracted, but the `BUY 5 GET 1` offer is broken into disconnected fragments.
- **Background:** removed content leaves checkerboard holes, text remnants, and incomplete regions rather than a reconstructed poster surface.
- **Typography:** words are separated from the composition, but styling, grouping, and original line relationships are lost.
- **Editability:** the extracted pieces exist, but the design has to be reassembled before it can be used as a working composition.

These observations describe the supplied runs shown here, not every possible output from each product. Results vary with product version, source resolution, and design complexity. See the [full comparison article](https://aixio.app/blog/aixio-layer-v1-vs-lovart-picell-image-to-layers/) and [evaluation notes](docs/EVALUATION.md) for context.

## Feature comparison: Aixio, Canva, Lovart, Picell, and Qwen

This image-to-layer model comparison covers the capabilities required to convert a flattened image into a genuinely editable composition. “Partial,” “Degraded,” and “Inaccurate” denote outputs that required material rework in the supplied evaluation; “Not disclosed” denotes capabilities not established by the available product information or test results.

| Capability | **Aixio Layer v1** | Canva Magic Layers (May 2026) | Lovart | Picell | Qwen Image Layered (Jan 2026) |
| --- | :---: | :---: | :---: | :---: | :---: |
| Background reconstructed behind objects | **Yes** | Partial | No | No | Partial |
| Text returned as editable type | **Yes** | Breaks on dense text | Degraded | Degraded | No |
| Typeface identified | **Yes** | Yes | Inaccurate | Inaccurate | No |
| Orientation and perspective understood | **Yes** | No | No | No | No |
| Native super-resolution | **Yes** | No | No | No | No |
| User-directed manual extraction | **Yes** | No | No | No | No |
| Deterministic output | **Yes** | No | Not disclosed | Not disclosed | Not disclosed |
| Output can leave the platform | **Yes** | Canva only | Not disclosed | Not disclosed | Yes |

This matrix reflects Aixio testing, the supplied comparison runs, and product information available when the capability report was prepared. Competitor products change, so results should be read with the named versions and test dates rather than as permanent claims. See [Evaluation and Comparison Notes](docs/EVALUATION.md).

## Aixio Layer v1 capabilities

- **Complete recognition:** recovers meaningful design units rather than a loose collection of crops.
- **Amodal reconstruction:** predicts the content hidden behind foreground elements so objects can be moved without leaving holes.
- **Native typography:** returns copy as editable strings with recovered font and styling attributes when available.
- **Composition logic:** preserves grouping, stacking order, placement, orientation, and perspective.
- **Usable RGBA output:** returns transparent visual layers with practical boundaries, not only approximate masks.
- **Detail retention:** applies native super-resolution during decomposition to preserve texture and edge information.
- **Manual control:** lets users direct extraction when an automatic pass misses an important element.
- **Portable structure:** returns organized output that can continue through a broader creative workflow.

## See it in action

<div align="center">
  <a href="https://youtu.be/BkdkW2nn3b0">
    <img src="https://i.ytimg.com/vi/BkdkW2nn3b0/maxresdefault.jpg" alt="Watch Introducing Aixio Layer v1.0" width="820">
  </a>
  <br>
  <sub>Introducing Aixio Layer v1.0 — click to watch on YouTube</sub>
</div>

## Where to use Aixio Layer v1

Aixio Layer Image v1 is available in **[Aixio Studio](https://aixio.app/studio)** through the **Edit Layers** workflow. No local installation or model download is required: upload a finished image in the browser, run Layer v1, and continue editing the returned composition on the Studio canvas.

### Use Layer v1 in Aixio Studio

1. Open Aixio Studio and add a finished image.
2. Choose **Edit Layers**.
3. Let Layer v1 identify the background, visual assets, text, and composition structure.
4. Select any returned layer to rewrite copy, restyle type, move objects, or continue building on the canvas.
5. Export the result for handoff when the composition is ready.

No source design file, original layer data, or embedded metadata is required.

## News

- **2026-08-04** — Aixio published the Layer v1 comparison across recognition, spatial reconstruction, font fidelity, and native upsampling.
- **2026** — Aixio Layer v1 became available in Aixio Studio.

## Designed for real creative work

Layer v1 is useful when the source file is missing or never existed:

- revise copy in a flattened campaign asset;
- localize a poster or social graphic;
- move or remove a product, badge, or subject;
- recover reusable elements from a screenshot or export;
- convert AI-generated artwork into a composition with editable structure; or
- prepare an existing visual for continued work in Studio.

## Model overview

| Property | Layer v1 |
| --- | --- |
| Task | Flat image to editable design layers |
| Input | One raster image |
| Model | 52B-parameter dense model, trained in-house for image-to-layer reconstruction |
| Visual output | Ordered RGBA elements and reconstructed background |
| Text output | Editable strings with recovered typography attributes |
| Access | Aixio Studio |

For intended use, evaluation methodology, limitations, and release details, read the [model card](docs/MODEL_CARD.md).

## Current release scope

This repository is a product and model reference. It does not currently contain downloadable model weights, training code, or a local inference package. Layer v1 can be used through Aixio Studio; public programmatic access should be described here only when an official API is released.

## Limitations

- Results vary with source resolution, compression, visual density, and design complexity.
- Highly stylized, distorted, or partially obscured text may require manual correction.
- A recovered font may need substitution if the original family is unavailable or unlicensed in the working environment.
- Fine transparency, motion blur, reflections, and tightly fused elements can require review.
- Reconstructed regions are model predictions and should not be treated as evidence of what existed outside the visible source image.

## Documentation

- [Model card](docs/MODEL_CARD.md)
- [Evaluation and comparison notes](docs/EVALUATION.md)
- [Frequently asked questions](docs/FAQ.md)
- [Aixio Layer v1 comparison article](https://aixio.app/blog/aixio-layer-v1-vs-lovart-picell-image-to-layers/)
- [Introducing Aixio Layer v1.0](https://youtu.be/BkdkW2nn3b0)

## Citation

If you reference Layer v1 in a publication, report, or product comparison, you can use:

```bibtex
@software{aixio_layer_v1_2026,
  title  = {Aixio Layer v1},
  author = {{Aixio}},
  year   = {2026},
  url    = {https://aixio.app/}
}
```

## Rights and availability

Aixio Layer v1 is an Aixio model delivered through Aixio Studio. Unless a separate license is published, the model, service, and included Aixio assets should not be presented as open source or open weights. Third-party names and marks belong to their respective owners.

---

<div align="center">
  <strong>Image in. Editable file out.</strong><br><br>
  <a href="https://aixio.app/studio">Try Aixio Layer v1 in Studio</a>
</div>
