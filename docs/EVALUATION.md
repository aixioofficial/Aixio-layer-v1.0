# Evaluation and Comparison Notes

## What should be measured

Image-to-layer systems should not be judged only by whether they can cut out visible objects. A useful evaluation needs to cover four separate questions:

1. **Recognition:** Did the system find the meaningful elements?
2. **Separation:** Are the alpha boundaries clean enough to edit?
3. **Reconstruction:** Is there usable content behind removed elements?
4. **Editability:** Did text, order, transforms, and visual hierarchy survive?

A system can perform well on object extraction while still returning a composition that has to be rebuilt manually.

## Internal quantitative benchmark

Aixio's internal model materials describe the following protocol:

| Item | Description |
| --- | --- |
| Ground truth | Original layers from real PSD and Figma files |
| Model input | A raster image flattened from each layered source file |
| Evaluation size | 10,000 images |
| Coverage | 36 design categories |
| Primary metric | Mean intersection over union between predicted and ground-truth alpha |
| Reported Layer v1 result | 94% decomposition accuracy |

This construction avoids asking a model or human annotator to invent the ground truth after the fact: the source layer structure already exists before the image is flattened.

The 94% figure should be labeled **Aixio-reported** until the dataset split, matching procedure, scoring code, per-category scores, and failure analysis are publicly released. IoU also does not fully measure typography fidelity, layer naming, correct grouping, or the visual plausibility of reconstructed hidden regions, so those qualities need separate evaluation.

## Supplied qualitative comparison

The public Aixio comparison uses the same retail poster in Picell, Lovart, and Aixio Layer v1. The observations below apply only to those supplied runs.

### Aixio Layer v1

![Aixio Layer v1 supplied result](../assets/cap2-aixio.png)

The result separates the headline, offer badge, logo, food groups, checkerboard, terms, border, and paper field. Typography and background structure remain available for continued editing.

### Lovart

![Lovart supplied result](../assets/cap2-lovart.png)

The supplied run recognizes some text and imagery, but portions of the display type and background structure require rework.

### Picell

![Picell supplied result](../assets/cap2-picell.png)

The supplied run extracts several visible pieces, but fragments the offer and does not return a reconstructed composition ready for direct editing.

## Reading a comparison honestly

When reviewing any image-to-layer result, inspect the following:

- **Clean plate:** What remains after foreground elements are hidden?
- **Text:** Is it editable, correctly transcribed, and visually close to the source?
- **Alpha:** Do edges show halos, clipped detail, or background contamination?
- **Layer logic:** Are meaningful objects grouped correctly and ordered correctly?
- **Transforms:** Do rotation, scale, skew, and perspective remain usable?
- **Edit test:** Can an element be moved or removed without forcing a manual rebuild?

## Reproducibility checklist for future benchmark releases

Before presenting comparative scores as reproducible, publish or document:

- evaluation set construction and licensing;
- category distribution and train/test deduplication;
- exact input resolution and preprocessing;
- layer-matching procedure for different predicted layer counts;
- alpha-IoU aggregation and treatment of empty layers;
- text transcription and typography metrics;
- reconstruction metrics or blinded human review protocol;
- inference settings and product/model versions;
- failure cases, not only best examples; and
- the date each competing system was tested.

Competitor products change frequently. Every comparison should therefore name the tested version or date and avoid turning observations from one run into universal claims.

## Sources

- [Aixio Layer v1 vs. Lovart vs. Picell: What Actually Comes Back](https://aixio.app/blog/aixio-layer-v1-vs-lovart-picell-image-to-layers/)
- [Introducing Aixio Layer v1.0](https://youtu.be/BkdkW2nn3b0)
- Local Aixio Layer v1 model-capability materials supplied with this documentation
