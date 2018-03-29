# anima

A simple drawing and animation framework for Carp. It is designed to be simple
to use, expressive, and empowering. It is also very minimal at the moment. Read
[my blog post](https://blog.veitheller.de/Introducing_anima.html) about it or
browse [the docs](https://veitheller.de/anima/).

```clojure
(load "anima.carp")
(use Anima)

(defn setup [rend]
  (framerate 0)) ; shortcut for a static sketch

(defn draw [rend]
  (do
    (color rend 255)
    (line rend 0 0 800 800)))

(defsketch "One line to rule them all" 800 800
  setup
  draw)
```
