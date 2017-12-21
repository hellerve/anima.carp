# anima

[WIP: stay tuned]

A simple drawing and animation framework for Carp. It is designed to be simple
to use, expressive, and empowering.

```clojure
(load "anima.carp")
(use Anima)

(defn setup [app rend]
  (framerate 0)) ; shortcut for a static sketch

(defn draw [app rend]
  (do
    (color app rend 255)
    (line app rend 0 0 800 800)))

(defsketch "One line to rule them all" 800 800
  setup
  draw)
```
