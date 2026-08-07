<div align="center">
  <img src="assets/logo.png" width="88" alt="Aixio logo">

  # Aixio Layer v1

  **Turn a flat image into editable design material.**

  Layer v1 reconstructs the background, separates visual elements, and recovers text as selectable, editable type—so a finished image can become a file you can keep designing.

  [Try in Aixio Studio](https://aixio.app/studio) · [Watch the demo](https://youtu.be/BkdkW2nn3b0) · [Read the comparison](https://aixio.app/blog/aixio-layer-v1-vs-lovart-picell-image-to-layers/) · [Model card](docs/MODEL_CARD.md) · [Evaluation](docs/EVALUATION.md)
</div>

---

![A flat poster decomposed into independently editable elements by Aixio Layer v1](assets/figure-2panel.png)

## Introduction

Most finished visual work arrives as pixels: a PNG, JPEG, screenshot, export, or AI-generated image. The composition may look complete, but its structure is gone. Copy cannot be rewritten, objects cannot be moved cleanly, and removing an element reveals no usable background underneath.

Aixio Layer v1 is an image-to-layer model built to recover that structure. Given one flat raster image, it returns an ordered set of working parts:

- visual elements with transparent backgrounds;
- editable text with recovered type styling;
- a reconstructed background behind foreground objects; and
- composition structure that can be adjusted in Aixio Studio.

This is more than object extraction. Layer v1 is designed to understand what belongs together, how elements overlap, and what the hidden parts of the design should contain.

## News

- **2026-08-04** — Aixio published the Layer v1 comparison across recognition, spatial reconstruction, font fidelity, and native upsampling.
- **2026** — Aixio Layer v1 became available in Aixio Studio.

## See it in action

<div align="center">
  <a href="https://youtu.be/BkdkW2nn3b0">
    <img src="https://i.ytimg.com/vi/BkdkW2nn3b0/maxresdefault.jpg" alt="Watch Introducing Aixio Layer v1.0" width="820">
  </a>
  <br>
  <sub>Introducing Aixio Layer v1.0 — click to watch on YouTube</sub>
</div>

## What Layer v1 recovers

### Separated visual elements

Distinct elements are returned as independently editable layers with RGBA transparency and a usable stacking order. Instead of treating the composition as one picture, Layer v1 gives each meaningful part its own handle.

<p align="center">
  <img src="assets/cap-layer-rgba.png" width="300" alt="Example RGBA layer with a transparent background">
</p>

### Reconstructed backgrounds

Removing an object is only useful if the space behind it is restored. Layer v1 reconstructs occluded regions so elements can be moved, resized, or removed without leaving obvious holes in the composition.

### Live, editable text

Layer v1 returns recognized copy as text—not only as pixels. It recovers typography information such as font family, weight, size, color, alignment, and placement when available, making copy changes and localization much faster.

<p align="center">
  <img src="assets/cap-layer-text.png" width="500" alt="Example text recovered as editable type">
</p>

### Spatial structure

The model reasons about layer order, grouping, orientation, and perspective. This helps preserve the original visual hierarchy instead of returning a loose collection of disconnected crops.

### Native upsampling

Layer v1 rebuilds useful detail as it decomposes the image. The goal is to keep extracted assets practical for continued design work rather than making them softer than the source.

## Quick start

Layer v1 is available inside [Aixio Studio](https://aixio.app/studio).

1. Open Aixio Studio and add a finished image.
2. Choose **Edit Layers**.
3. Let Layer v1 identify the background, visual assets, text, and composition structure.
4. Select any returned layer to rewrite copy, restyle type, move objects, or continue building on the canvas.
5. Export the result for handoff when the composition is ready.

No source design file, original layer data, or embedded metadata is required.

## Showcase

The example below starts with a dense retail poster containing display type, multiple food images, a checkerboard pattern, fine print, and a bordered paper field.

### Aixio Layer v1

![Aixio Layer v1 result for the retail poster](assets/cap2-aixio.png)

Layer v1 separates the headline, offer badge, logo, three food groups, checkerboard, terms, border, and paper field into working parts. The composition remains recognizable while the returned elements become individually editable.

### Why reconstruction matters

The most revealing part of image-to-layer output is not whether visible objects can be cut out. It is whether the background and design structure survive after those objects are removed.

<table>
  <tr>
    <th>Aixio Layer v1</th>
    <th>Lovart — supplied run</th>
    <th>Picell — supplied run</th>
  </tr>
  <tr>
    <td><img src="assets/cap2-aixio.png" alt="Aixio Layer v1 comparison result"></td>
    <td><img src="assets/cap2-lovart.png" alt="Lovart comparison result"></td>
    <td><img src="assets/cap2-picell.png" alt="Picell comparison result"></td>
  </tr>
  <tr>
    <td>Meaningful elements, typography, and background structure are recovered.</td>
    <td>Some elements are found, but parts of the background and display typography require rework.</td>
    <td>Several visible pieces are extracted, but the composition is fragmented and the background is not reconstructed.</td>
  </tr>
</table>

These observations describe the supplied runs shown here. Results can vary with source resolution and design complexity. See the [full comparison article](https://aixio.app/blog/aixio-layer-v1-vs-lovart-picell-image-to-layers/) and [evaluation notes](docs/EVALUATION.md) for context.

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
