# wooden-cubes

All my design files for wooden cubes

These projects are designed in Fusion 360, however, some of them have input files that make it a whole lot easier to do, rather than design it from scratch using the Fusion360 sketch primitives.

Text is a particular problem, it's really hard to size and move, and in particular, centre.

The best way I've come up with to get text into Fusion360 is a vaguely useful way that doesn't require days of clicking, is to import an SVG. In particular, we can auto-generate the SVG using the fact that an SVG file can call a function when it loads to generate the DOM. Naturally, Fusion360 doesn't do anything with this, but we can load it in a browser such as Chrome, and then copy the resultant DOM from the developer console, and save that to a file.

Using a SVG gets you all your primitives such as lines and other shapes, but the text gets mangled. It is converted to Fusion360 text, which is then not in the same position. To get around this with the least amount of work I've found that creating additional lines in the SVG where the text should be allows it to be quickly moved by eye to roughly the right place, a compromise, but not too bad.

Dimensions are another funny thing. Fusion360 imports everything as 96 units per inch. I work in mm, like any sane person, so this is particular awkward, but given that I'm auto-generating the SVG anyway, it's not too bad - everything just comes out to 10 decimal places, and Fusion360 seems to get something that comes up with the right dimension.

On top of all of this, Fusion360 also currently (as of November 2018), doesn't like spaces in styles, and just throws a non-specific error if you try to import an SVG with them included. For example:

```
// Need to search and replace (with appropriate text size):
// font-size: 56.693px; font-family: Helvetica; font-weight: bold; alignment-baseline: alphabetic;
// with
// font-size:56.693px;font-family:Helvetica;font-weight:bold;alignment-baseline:alphabetic;
```

### Current workflow

1. Write a function to generate the SVG you want, checking that it comes out right in a browser.
1. In the browser, look in the developer console (inspect view) and copy the outerHTML for the svg tag, and save it into a new file.
1. Do a search and replace with any spaces in style tags
1. Import into Fusion360 and cross your fingers!
