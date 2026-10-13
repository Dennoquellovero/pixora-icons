# Contributing Guidelines

Thank you for your interest in contributing to this project!
Pixora-icons welcomes bug reports, pull and feature requests, and suggestions!

## Bug Reports

Before opening an issue: 
- Search existing issues, your problem may have already been mentioned.
- Make sure you're using the latest version.

Please include in your report: 
- Your distro (Ubuntu, Arch, Fedora... Or  any of their derivatives);
- Your DE (GNOME, KDE, XFce...)
- Theme version;
- Steps to reproduce the bug (if applicable);
- Screenshots (if applicable).

## Icon Requests

Please refrain from adding multiple icon requests into the same issue, as this makes the workflow quite chaotic.

## Pull Requests

Pull Requests must follow the **Design Guidelines** described below. <br>
Please keep PRs small and focused:
- One feature per PR;
- One fix per PR;
- No unrelated changes.

---

# pixora-icons Design Guidelines

***These Guidelines are still work-in-progress and are subject to change!***

If you want to make icons for pixora-icons, these guidelines should point you to the right direction. Although they are not that strict, you should still keep them in mind for consistency reasons. <br>
These guidelines apply to every app, be it Discord, Firefox, Steam (branded apps); or Settings, Accessibility, File Manager (non-branded apps).

## Taking References

You're free to use any version you want from any app icon for reference, besides the really old ones if the app has been through many rebrandings. Also try to keep the designs consistent with existing ones!

## Color Palette
pixora-icons uses a specific color palette. You can check it out by clicking [here](https://lospec.com/palette-list/resurrect-32)!
This, together with the vectorizing rule, should be the only rule that is very strict. Please refrain from using any color outside of the 32 ones that Resurrect offers, as this would ruin the general aesthetic of your icon when comparing it with the rest.

Be creative with your designs! If you're not that deep into art, many times you'll think that it's impossible to draw an icon without a specific color, but it is very much possible if you try hard enough. 
You're free to tweak the original icon aesthetic as much as you want, as long as it does not make it unrecognizable. Have fun!

Visual representation of the color palette:

![Color Palette](.github/resurrect-32-32x.png)

## Borders

Every app icon has a border. Its purpose is to keep the icons 'away' from any background color and define their own space on the screen. Since they are all drawn on a 16x16 grid, every color matters, and avoiding background fading is super important. 

A border has three simple criteria:
- It should be colored `#3E3546`;
- It should go around the **entire** icon (so avoid coloring the edges of the grid as much as possible);
- If the icon has any "hollow" (transparent) section, or an internal border (think of a donut shape) it should go there as well.

Here you can see examples of GOOD borders and BAD borders:

![Borders Examples](.github/borders-examples.png)

Why are those borders considered 'bad':

1. The first one has the wrong color (`#625565` instead of `#3E3546`);
2. The second one does not go all the way around, since there's a part of the icon on the edge of the grid. It is actually possible to make this border good — the icon width is 14px;
3. The third one only goes around the external part of the icon, leaving the inside region incomplete.

## Shading

Every icon should have some sort of shading, except monochromatic ones (eg.: GitHub, Monochrome, Hydra Launcher), and rare exceptions, like Nvidia's, where it kind of has some shading originally already, and that is enough. This is to keep visual consistency between the icons.

Shading is (most of the time) done assuming the light source is above the object, so a lighter tone on the top part and a darker one on the bottom part should suffice. It is also quite simplistic, so a single-pixel line should be enough.
This is when the limitations of the 32-color palette shine the most!

Example of shaded vs non-shaded versions of the same icon:

![Shade vs No Shade](.github/shading-example.png)

## Glyphs and General Advice

Keep in mind that pixel art is not about taking the full resolution version of an image and resizing it down; it's actually redrawing it from scratch, where every single pixel matters and actually represents a significant portion of the whole image. You can see this clearly on this project, since we're limited to mere 256 pixels IN TOTAL for every single image. 

When drawing the glyph of any app, try to think which portion of the whole image the last pixel(s) you've drawn actually represents. You'll be surprised of how often you notice that the final result is getting distorted, and you'll know exactly why by applying this thought process.

## Vectorizing

Every app icon should be vectorized. Reason being, I think it's way easier to, in this project's case, make every icon a vector and set the  to `scalable`, than having to make 16, 24, 32, 64px and so on versions of every single icon. The entire vectorizing process is automated by a shell script, so it should be a walk in the park. 

### Tutorial:

>[!Note] 
> Claude AI was used to build the entirety of both `vectorizing.sh` and `svgfit.py` scripts, since I don't know how to code myself. They were tested on my own machine before being pushed to the repo, and are of course available for further inspection. They should work without any issues, since it's just a `.png > .svg` process inside a localized group of directories. Each major step of `vectorizing.sh` can be done manually, and `svgfit.py` only exists to replace Inkscape CLI tools, since they're not compatible with GNU Parallel for multi-processing.

1. **[⚠️ IMPORTANT]** After finishing your design on your favorite 16x16 canvas, export the file to any directory named `16x16/`;
2. Make sure to have [imagemagick](https://imagemagick.org/script/download.php#gsc.tab=0), [vtracer](https://github.com/visioncortex/vtracer), [scour](https://deepwiki.com/scour-project/scour/2.1-installation), [python-lxml](https://github.com/lxml/lxml?tab=readme-ov-file), and [parallel](https://www.gnu.org/software/parallel/) installed;
3. Have the provided [vectorizing.sh](/pixora/vectorizing.sh) and [svgfit.py](/pixora/svgfit.py) scripts available ***outside***  the `16x16/` directory with your design(s);
4. Execute `vectorizing.sh` via any way you like, e.g. by doing `./vectorizing.sh`;
5. You should now have a directory named `svg/` containing all the traced files;
6. Read this tutorial again and make sure you understand each step;
7. Done! :)

## Folder Icons and Pixora Accent

Folder contributions now include the original Pixora artwork and its generated **Pixora Accent** version. Pixora Dark shares the original artwork, while Pixora Accent uses KDE's accent color at render time. See the [Pixora Accent documentation](README.md#-pixora-accent-for-kde) for compatibility and activation.

### Prepare the original artwork

Start from an existing folder on the **16×16 grid**, keeping its silhouette and the smaller folders/paper at the top. Draw the new glyph with its dark outline and use the original folder palette:

| Area | Original Pixora color | Pixora Accent behavior |
| --- | --- | --- |
| Folder body, including separate fragments and glyph cutouts | `#E3C896` | Follows the accent color |
| Main glyph | `#AB947A` | Uses a darker shade of the accent color |
| Glyph details | Supported darker tones, such as `#966C6C` | Keep their tonal differences using accent-derived shades |
| Outer borders, glyph outlines and lines between the smaller folders | `#3E3546` | Keep their original color and shape |
| White paper areas | `#FFFFFF` | Stay white |

The original artwork still follows the Resurrect 32 palette. The palette exception applies to the dynamic colors of the generated Accent variant. Preserve the paper and the lines separating the smaller folders when drawing or recoloring a glyph.

### Vectorize and generate the Accent version

1. Follow the vectorizing tutorial above. Save the original PNG as `pixora/16/places/folder-<name>.png` and the SVG as `pixora/scalable/places/folder-<name>.svg`. Keep the existing folder layout and SVG path/transform structure where possible; the generator checks these before adapting an icon.
2. Use a real SVG file for the original `folder-<name>` artwork. Add alternate icon names as **relative symlinks** to it in the appropriate `pixora/scalable/` contexts. The generator creates corresponding Accent aliases across those contexts, so KDE can load the adapted folder under each name.
3. From the repository root, regenerate the Accent artwork and aliases, then check that the generated files match their sources (Python 3.9 or newer):

   ```bash
   python3 scripts/generate-accent.py
   python3 scripts/generate-accent.py --check
   ```

Make artwork changes in the original Pixora files and conversion changes in `scripts/generate-accent.py`, then regenerate `pixora-accent/`. If the script reports that an artwork or palette needs review, review its paths and add an explicit conversion rule for the new structure before regenerating. Custom layouts, mixed glyph/shadow paths and new glyph tones can require this extra step.

### Review before submitting

Review both Pixora and Pixora Accent in KDE Plasma 6, using several accent colors, light and dark backgrounds, normal and selected states, and small and enlarged icon sizes. Inspect the entire folder for leftover beige/brown pixels, especially separate body fragments and glyph cutouts. Check that glyphs use darker matching tones, their details remain visible, and borders, white paper and the lines between the smaller folders retain their original pixels. Check the alternate icon names too.

A browser or another SVG renderer may show the beige fallback; use KDE's color-scheme-aware icon loader to verify recoloring. If an application shows a cached version, reselect the icon theme or reopen it. Changing the user's accent color does not require regenerating the files.

Include the original PNG/SVG, added or updated symlinks, generated Accent files and any necessary generator changes in the same PR. Include screenshots of the original and Accent versions for review, and regenerate again whenever the source artwork or its aliases change.

---

# License Reminder
By contributing, you agree that your contributions will be licensed under the same license as the project.

