---
name: scientific-plots
description: Make or restyle a scientific matplotlib figure for a paper, talk or poster: shared style sheet, colour, labelling and clutter rules, and a checklist before showing it.
---

# Making a scientific plot

A figure is not a data dump. It is a visual statement of one quantitative result.
Before writing code, say in one sentence what the reader should take away, then
design every element to support that sentence and remove anything that doesn't.
(General rules adapted from C. O'Hare, "How to make a plot", University of
Sydney.)

## 1. Style sheet (always)

Load the shared style before plotting instead of setting `rcParams` by hand:

```python
plt.style.use('paper')   # or a path to paper.mplstyle
```

Its settings:

```
font.family      : serif
mathtext.fontset : dejavuserif
font.size        : 16
axes.linewidth   : 1.2
xtick.direction  : in
ytick.direction  : in
xtick.major.size : 5
ytick.major.size : 5
legend.frameon   : False
savefig.dpi      : 300
```

If the style file is missing, set exactly these values and say so. Never
override them per figure except for font size (section 2) and colours
(section 3).

## 2. Size for where it will be used

- Ask or decide first: paper column, full page, talk slide, or poster. A paper
  figure is not a slide figure; redraw rather than copy one into the other.
- Draw the figure at its final printed size, so 10 pt in the file is 10 pt on
  the page. Typical widths: single column about 3.5 in, two-column page about
  7.2 in.
- 16 pt is the default, but text must always be legible where the
  figure goes. No text (ticks, legend, labels, annotations) may print smaller
  than the body text of the paper or slide; bigger is better. For a figure
  drawn at print size in a paper, that usually means 9 to 10 pt.
- Keep the file small (well under 1 MB). Save vector (PDF or SVG) for papers;
  use `rasterized=True` on `pcolormesh`, `imshow` or dense `scatter` layers.
  PNG at 300 dpi is fine for drafts.

## 3. Colour

- There is no default colour cycle. Choose colours for each figure
  from what the data are:
  - Distinct categories: a qualitative palette with well-separated hues and
    lightness.
  - An ordered parameter: a perceptually uniform sequential map sampled over
    a limited range (drop the near-white end), plus one marker shape per
    value (`'os^Dv<>'`) so neighbours stay distinguishable and the figure
    survives greyscale.
  - Signed quantities centred on zero: a diverging map with the centre at 0.
    Phase or angle: a cyclic map.
- Never use `jet`, `hsv`, `rainbow` or other maps with perceptual jumps.
- About 4% of readers are colour-blind: never let the message depend on fine
  hue differences, and never put red next to green. Use marker, line style or
  a direct label as a second cue.
- Use colour consistently across a paper or talk: the same quantity keeps the
  same colour in every figure.

## 4. Remove clutter

Every mark is something the reader's eye processes in the first instant, so
none may be accidental. Check for and remove:
- Tick labels that collide at the corners, labels or text overlapping data,
  and legends sitting on data.
- Mixed greys and blacks, or one stray coloured label: one colour per role.
- Text that isn't aligned with anything, and uneven gaps between panels or
  labels (`fig.align_ylabels`, shared axes, `constrained_layout` or explicit
  gridspec).
- Titles on paper figures: use none; the caption carries it.
- Grids heavier than `alpha=0.3`, frames on legends, unused axes and spines.

## 5. Labels

- Spell out quantities in words, then symbol and unit, e.g.
  `'Frequency, $f$ (MHz)'`, `'Power (dB)'`. Don't make the reader hunt
  through the caption for what a symbol means.
- Title Case axis labels with units in brackets; maths in LaTeX
  (`$\sigma$`, not "sigma"); dB vs linear and amplitude vs power always
  explicit.
- State any reference value a quantity depends on (e.g. the scale at which a
  roughness or variance is measured) in the label or caption.
- Label curves directly on the plot when there are few of them; use a legend
  (frameless, outside the data) when there are many.
- Show inequalities and exclusions as shaded regions, not bare lines.

## 6. Data honesty

- Error bars always say what they are (standard error, standard deviation,
  credible interval) in the caption, with a note when points share samples
  and are correlated.
- If you smooth (KDE, running mean), also show the underlying data.
- If the message is only in a table of numbers, turn it into a figure.

## 7. Keep it simple

- Avoid complicated plots. If several layers are unavoidable, order them so
  the main message reads first (weight, colour, position) and detail second.
  Prefer shared axes and small multiples over one crowded panel.
- An uninteresting-looking result can still be a clear figure: use an inset
  (`ax.inset_axes`) to zoom where the curves differ, annotate directly.
- Corner plots: only when the full posterior structure is the point.

## 8. Process

1. Draft at the final size, render the image and look at it yourself before
   showing it to anyone.
2. Show the draft to the person you are working with and ask before changing
   tracked plotting code.
3. Before showing any figure, check:
   - [ ] Style sheet loaded; font legible at the final size
   - [ ] Every element intentional; no overlaps, collisions or stray colours
   - [ ] Axis labels in words with units; reference values stated
   - [ ] Colours chosen for the data type, colour-blind safe, consistent
   - [ ] Error bars defined; no hidden smoothing
   - [ ] One clear takeaway someone could name at first glance
