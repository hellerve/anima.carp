# anima

A Processing-style drawing and animation framework for Carp, backed by
[Cairo](https://www.cairographics.org/) via
[cairo.carp](https://github.com/carpentry-org/cairo.carp). Read
[my blog post](https://blog.veitheller.de/Introducing_anima.html) about the
original version or browse [the docs](https://veitheller.de/anima/).

## Dependencies

Cairo must be installed and discoverable via `pkg-config`:

```
brew install cairo        # macOS
apt install libcairo2-dev # Debian / Ubuntu
```

SDL2 is still used for windowing and events in `defsketch`.

## Example

```clojure
(load "anima.carp")
(use Anima)

(defn setup [cr]
  (framerate 0)) ; static sketch, draws once

(defn draw [cr]
  (do
    (stroke-color 255)
    (line cr 0.0 0.0 800.0 800.0)))

(defsketch "One line to rule them all" 800 800
  setup
  draw)
```

Callbacks receive a `(Ptr CairoContext)`. Drawing coordinates are `Double`.

## Drawing model

Anima tracks fill and stroke colors as module-level state. Each shape function
builds a Cairo path and applies fill then stroke automatically, matching
Processing's behavior.

```clojure
(fill-color 255 0 0)       ; red fill
(stroke-color 0)            ; black stroke
(stroke-weight 2.0)
(rect cr 10.0 10.0 80.0 80.0) ; filled red, stroked black
```

Available shapes: `line`, `rect`, `circle`, `ellipse`, `arc`, `triangle`,
`point`, `bezier`. State: `fill-color`, `stroke-color`, `no-fill`, `no-stroke`,
`stroke-weight`, `background`. Transforms: `push`, `pop`, `translate`, `rotate`,
`scale`. Text: `text`, `text-size`, `text-font`. Color: `hsb-to-rgb`.

`defpicture` writes a PNG directly via Cairo, no SDL window needed:

```clojure
(defn render [cr]
  (do
    (background cr 255)
    (stroke-color 0)
    (line cr 10.0 10.0 190.0 190.0)))

(defpicture "MyPic" 200 200 render)
```

## Tests

```
carp -x test/anima.carp
```
