# Frequently Asked Questions

## What is Aixio Layer v1?

Aixio Layer v1 is an image-to-layer model. It takes a flat raster image and reconstructs editable visual elements, live text, background content, and composition structure for continued work in Aixio Studio.

## How is this different from background removal?

Background removal typically separates one foreground subject from one background. Layer v1 aims to recover a complete composition: multiple elements, their stacking order, text, design structure, and the areas hidden behind objects.

## How is this different from segmentation?

Segmentation identifies which visible pixels belong to an object. It does not necessarily recover clean standalone assets, editable text, or the invisible content behind foreground objects. Layer v1 is designed around the editable reconstruction of the whole composition.

## Does it recover text as real text?

Yes. When text can be recognized, Layer v1 can return it as an editable string with recovered styling such as font family, weight, size, color, alignment, and placement. Difficult or stylized typography may still require correction.

## Can it restore what was behind an object?

Layer v1 predicts occluded regions from visible context so an element can be moved or removed without leaving an empty hole. Because those pixels were not present in the flattened input, the result is a reconstruction—not a factual recovery of the original hidden artwork.

## What kinds of images work well?

Posters, social graphics, ads, slides, product compositions, and other designed visuals are natural use cases. Results depend on source quality and complexity; clean, higher-resolution inputs generally provide more information for the model to work with.

## Does it require the original PSD, Figma file, or metadata?

No. The input can be a single PNG, JPEG, screenshot, export, or other raster image.

## Where can I use it?

Layer v1 is available in [Aixio Studio](https://aixio.app/studio). Add an image and choose **Edit Layers** to start decomposition.

## Are the model weights or source code available?

Not currently. The public release described here is a model capability delivered through Aixio Studio. This repository should not be described as open source or open weights unless Aixio publishes a separate release and license.

## Is there an API?

This documentation does not announce a public Layer v1 API. Add official endpoint, authentication, pricing, limits, and SDK documentation here only after programmatic access is released.

## How should I evaluate the output?

Do a real edit. Hide or move an element, rewrite a text layer, and inspect the clean plate and alpha boundaries. A visually impressive layer gallery is less meaningful than whether the returned composition can survive the next edit.

## Can the reconstructed background be trusted as the original?

No. Hidden areas are inferred. They are useful creative material, but they should not be treated as evidence of what the source file originally contained.

## Where can I see a full comparison?

Read [Aixio Layer v1 vs. Lovart vs. Picell: What Actually Comes Back](https://aixio.app/blog/aixio-layer-v1-vs-lovart-picell-image-to-layers/) or watch [Introducing Aixio Layer v1.0](https://youtu.be/BkdkW2nn3b0).
