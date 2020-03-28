+++
title = "OpenType, Harfbuzz, Qt : Not exactly a love story"
date = 2020-03-15T15:31:10+05:30
tags = ["freetype", "harfbuzz", "text", "font", "krita", "kde", "opentype"]
categories = ["krita"]
+++

Was experimenting with rendering text in Qt, of course for trying to see if I can land some improvements over Krita's existing text tool. And now that as I have played with it a bit, jotting some notes over this blog post.

The text tool in Krita right now is pretty basic for doing advanced typography stuff. By basic I mean you get explicit controls for doing,

- Setting Font
- Setting Font Size
- Setting Font weight
- Adjusting alignment
- Setting Color of the text
- Adjusting letter-spacing and line-height

And that's it, a complete list of controls would also include,

- Horizontal Kerning
- Vertical Shift
- Character Rotation
- TTB and RTL writing mode support
- Superscript and subscript
- Putting text on a path
- Flowing into a frame
- Support for OpenType features like ligatures

So typically we would need complete SVG2 support or at least a part of it. I am sure more controls should be there for easily doing advanced typography but those, for now, are pretty out of scope, including some of the ones I mentioned.

### Why am I calling them out of scope?
If I take a look at the SVG rendering engines available at this point, honestly I will get no better than what Chromium offers. And since Krita is a Qt application, we already have the best rendering engine which would be QtWebEngine but that's not usable. QtWebEngine can't draw on a QPaintDevice just like QtWebKit did. What else? If I take a look at the support offered by open source solutions, the next would be Inkscape.

### Why not just do what Inkscape does?
Umm, it is not that easy, since, like Inkscape, Krita doesn't only do vectors, we have a lot of things to take care of. Also, Inkscape's codebase is quite complicated to understand and since it uses a different stack, Gtk+ + cairo + pango, it is even harder to adapt.

For now, it is quite impossible to get to the ideal situation, that is of course unless someone can patch QtSvg to support SVG2, which for now nobody is interested in doing.

Reducing that down to what is required at this point of time,

- Superscript and subscript
- Ligatures
- TTB and RTL writing mode support

Wait wait wait, where are the other features? They couldn't be implemented, to be honest, and shouldn't be, first as I already said they are difficult and second, the code to render them is easier compared to the code which is required to edit them. Why? only for a single thing, where will you place the cursor in case two glyphs overlap each other? Inkscape does implement them but editing such text is just a nightmare to handle. Browsers render them quite well, of course, they don't have to edit them interactively.

Just FYI, Microsoft which co-authored the OpenType Format has yet to completely support OpenType features in its office suite, so you can guess how hard it is.

### How I plan it to do for Krita?
As far as ideas go there are a couple of approaches one is to follow the way Scribus does, which offloads the rendering to something like `cairo` which could handle this in a much better way. That would also require us to develop a couple of intermediate data structures that could hold the info, but that is not the biggest challenge. The problem here is the text editor dialog cause then you got relay what is being displayed on the canvas to the text editor dialog. And there you have to draw the cursor. Unfortunately drawing the cursor will be the biggest challenge here.

The other way is to write a new Text Engine and hook it up into Qt's API, which is to follow the following interface of [QTextLayout](https://doc.qt.io/qt-5/qtextlayout-members.html) if I going the right way. That way we won't have to worry about the text editor widget stuff. But I haven't explored this route that much and probably unaware of the challenges.

As a basis for both, I do have a basic proof of concept ready, which could be taken for a ride from [here](https://github.com/hellozee/qt-libraqm-test). It uses `libraqm` which a thin wrapper over `HarfBuzz`, `FriBidi` and `FreeType`.

If you are unaware of what are they, a bit of terminology,

- **FreeType**: It is a font rasterizing engine, which means given the glyph id and all the measurements required it would fetch the actual glyph from the glyph table and draw it.
- **OpenType**: Seems like a successor of FreeType, is it? No, it is just format made by Microsoft and Adobe, later adopted by Apple to store fonts, it is a successor of TrueType `(.ttf)` fonts, usually OpenType fonts have the `.otf` extension.
- **HarfBuzz**: It is the shaping engine responsible for handling over the measurements over to FreeType to draw the font. It was a part of the FreeType project but later was separated into its project.
- **FriBiDi**: It is an implementation of the Unicode Bidirectional algorithm, more of which can be read [here](https://www.unicode.org/reports/tr9/).


### Superscript and Subscript
SVG has inbuilt support for them with the `vertical-line` or `baseline-shift` or `alignment-baseline` property, though the later 2 are deprecated in SVG2 as per as [this](https://www.w3.org/2012/01/13-svg-irc#T03-24-06). So as far as I know, there is no automatic way to enable the support for subscript and superscript in `HarfBuzz` but we can always do this manually, though that might require more time to perfectly nail it.

### Ligatures
`HarfBuzz` can automatically substitute ligatures by itself, but we would also need something to disable or enable ligatures which can also be done with `HarfBuzz` as noted [here](https://harfbuzz.github.io/shaping-opentype-features.html). Though I am not sure how is this to be handled in SVG, also how does Qt handle this? Can we disable ligatures in `QTextEdit`?

### Top To Bottom and Right To Left writing mode
We already support Left to Right writing mode, of course, that's the default and only mode available. And thanks to `libraqm`, Right to Left and Top to Bottom would also be trivial. That's the easy part, now the tough part, drawing cursor at the correct positions.

SVG has this `writing-mode` CSS property which takes care of the orientation and has the following values, `horizontal-tb`, `vertical-rl` and `vertical-lr`. Nice, where is the problem? The problem is, it is a CSS property that could be applied to both `<text>` and `<tspan>` elements. How could we avoid that? Simply by ignoring the value of the property for the `<tspan>` elements. And also not drawing it in the text editor window, chances are Qt would mad too.

#### You have to change the UI for introducing these features right?
Ahh yes, not much, though. If I count on my finger that would be 3 buttons and a combo box, for which I think we have enough space in the widget.

#### What next?
Live preview? such that you don't have to press save every time, you want to update the view. On canvas editing maybe? but well, cursor, cursor, cursor, till next post, `:wq`.