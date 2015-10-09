# dsp-chain [![Build Status](https://travis-ci.org/RustAudio/dsp-chain.svg?branch=master)](https://travis-ci.org/RustAudio/dsp-chain)

A simple library for chaining together multiple audio dsp processors/generators, written in Rust!

Use cases for dsp-chain include:
- Designing effects.
- Creating an audio mixer.
- Making a sampler.
- Writing a dsp backend for a DAW.
- Any kind of modular audio synthesis/processing.


Usage
-----

Here's what it looks like:

```Rust
// Construct our dsp graph.
let mut graph = Graph::new();

// Construct our fancy Synth and add it to the graph!
let synth = graph.add_node(DspNode::Synth);

// Add a few oscillators as inputs to the synth.
graph.add_input(DspNode::Oscillator(0.0, A5_HZ, 0.2), synth);
graph.add_input(DspNode::Oscillator(0.0, D5_HZ, 0.1), synth);
graph.add_input(DspNode::Oscillator(0.0, F5_HZ, 0.15), synth);

// Set the synth as the master node for the graph.
graph.set_master(Some(synth));

// Request audio from our Graph.
graph.audio_requested(&mut buffer, settings);
```

Here are [two working examples](https://github.com/PistonDevelopers/dsp-chain/blob/master/examples) of using dsp-chain to create a very basic synth and an oscillating volume.

Add dsp-chain to your Cargo.toml dependencies like so:

```toml
[dependencies]
dsp-chain = "*"
```


PortAudio
---------

dsp-chain uses [PortAudio](http://www.portaudio.com) as a cross-platform audio backend. The [rust-portaudio](https://github.com/jeremyletang/rust-portaudio) dependency will first try to find an already installed version on your system before trying to download it and build PortAudio itself.


License
-------

MIT - Same license as [PortAudio](http://www.portaudio.com/license.html).

