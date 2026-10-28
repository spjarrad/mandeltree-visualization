# Mandeltree — Recursive Fractal Animation

**A Python visualization of Benoît Mandelbrot's snowflake sweep, from a single segment to an increasingly intricate fractal curve.**

## Watch the Animation

[![Mandeltree Fractal | Recursive Geometry Animation](mandeltree-preview.png)](https://youtu.be/6RIS5AWMGHY)

[Download MP4](https://raw.githubusercontent.com/spjarrad/mandeltree-visualization/main/mandeltree.mp4)

## What is the Mandeltree?

The **Mandeltree** or **Mandelbrot's Sweep of the Koch Snowflake** is a Peano-type fractal construction introduced by mathematician Benoît Mandelbrot. It is related to the Koch snowflake: under indefinite recursive substitution, the limiting curve is space-filling, with Hausdorff dimension 2. 

This project implements the recursive geometry using the published segment lengths, turning-angle relationships, and reflection rules. The generator and its successive recursive stages are calculated through complex-number transformations.

The animation also introduces continuous geometric transitions and optional circular-arc rendering to visualize how the fractal develops. These presentation features are additions to the original straight-segment construction.

Circular-arc rendering can be enabled or disabled using the `USE_CURVED_ARCS` configuration variable. Setting it to `True` produces smooth circular arcs, while `False` preserves the underlying straight-segment geometry. Experimenting with both modes reveals two distinct visual interpretations of the same recursive construction. Try out both to experience all the beauty!

## How it's constructed

The animation begins with a single segment and reveals how a small geometric rule creates increasingly complex structure:

1. **Seven-segment generator:** A prescribed path of seven segments establishes the initial branching geometry.
2. **Thirteen-segment generator:** The exceptional fifth segment is replaced by a scaled and oriented copy of the seven-segment pattern, producing 13 segments.
3. **Recursive substitution:** Each segment is replaced by a rotated, scaled, or reflected copy of the 13-segment generator, with orientation tracked through a parity rule.
4. **Successive levels:** The recursive segment count grows as **13ⁿ**: 1, 13, 169, 2,197, and so on.

The seven-segment figure is an introductory construction milestone, not an additional level in the 13-fold recursion. The animation deliberately shows **1 → 7 → 13 → 169 → …** so viewers can see how the recursive rule is assembled.

The 13-segment generator has seven pieces scaled by **1/3** and six by **1/(3√3)**, consistent with the dimension-2 scaling relation:

**7(1/3)² + 6(1/(3√3))² = 1**

## Implementation

Built with **Python, NumPy, Matplotlib, and FFmpeg**, the animation uses:

- Complex-number transformations for scaling, rotation, and translation, with conjugation-based reflection.
- Vectorized NumPy operations to construct and sample many segments efficiently.
- Interpolation of vertices and signed angular sweeps to unfold the geometry continuously between recursive levels.
- Smoothstep easing, fixed camera framing, stage labels, and progress-tracked MP4 export.

The renderer supports straight segments and circular-arc representations of the underlying geometry.

## Validation

The geometry was checked for generator segment counts and lengths, reflection/parity behavior, and continuity between successive segments. Additional numerical tests checked rendered arc endpoints and confirmed that the end of an animated transition matches the corresponding completed recursive stage.

## Running the project

Install the Python dependencies:

```bash
python -m pip install numpy matplotlib jupyter
```

Install **FFmpeg** separately and ensure it is available on your system's `PATH`. Open the project notebook in Jupyter and run its cells in order. Key settings include `MAX_LEVEL`, `FPS`, `TRANSITION_SECONDS`, `HOLD_SECONDS`, `INITIAL_HOLD_SECONDS`, and `ARC_SAMPLES`.

Beware! Start with a low `MAX_LEVEL` when experimenting: the number of segments grows exponentially, so higher levels can require substantial memory and rendering time.

## Author

Spencer Jarrad

Python implementation, recursive geometry, and animation.

This project is based on the mathematical constructions of Benoît Mandelbrot, with additional references credited below.

## Mathematical references

- Mandelbrot, Benoît. “Des monstres de Cantor et de Peano à la géométrie fractale de la nature.” In Penser les mathématiques, edited by François Guénard and Gilbert Lelièvre, pp. 226–251. Paris: Éditions du Seuil, 1982.

- Kern, Jane F. “Mandelbrot’s Sweep of the Koch Snowflake.” *Logo Exchange*, vol. 9, no. 6, March 1991, pp. 20–24. International Society for Technology in Education (ISTE). [Read the article (PDF)](https://el.media.mit.edu/logo-foundation/resources/nlx/v9/Vol9No6.pdf).

This repository presents a computational visualization of Mandelbrot's construction, not a new fractal definition.

For a visual reference to the construction and its scaling ratios, see the [Courbe remplissant le flocon de Koch](https://fr.wikipedia.org/wiki/Courbe_remplissant_le_flocon_de_Koch). Des notions de français peuvent être nécessaires !
