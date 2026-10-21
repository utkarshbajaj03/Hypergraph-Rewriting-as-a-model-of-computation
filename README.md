# Hypergraph Rewriting as a Model of Computation

This project started at the **Wolfram Summer School 2022**. The question behind it: can hypergraph rewriting
(the rewriting systems behind the Wolfram model) serve as a general model of computation? To test this, I compile
standard models of computation into hypergraph rewriting systems, so that running the rewriting system step by
step simulates the original machine.

Write-up on Wolfram Community:
[[WSS22] Compiling different models of computation into hypergraph rewriting](https://community.wolfram.com/groups/-/m/t/2575623)

## How the encoding works

- A machine's **states** and **alphabet symbols** become vertices, built from small state and alphabet graphs.
- The **input** (a word for an automaton, a tape for a Turing machine) is encoded as a chain of hyperedges.
- Each **transition** of the machine becomes a local hypergraph rewriting rule, so one rewriting step corresponds
  to one step of the machine.
- The result can be decoded back into the machine's configuration, which makes it possible to check the
  compiled system against the original.

## Contents

| Notebook | What it does |
|---|---|
| `DFA to Hypergraph.nb` | Compiles deterministic finite automata into hypergraph rewriting rules (`DFAtoHypergraph`, `DFARule`). Encodes input words as hypergraphs (`initialWordToHypergraph`) and decodes them back (`HypergraphToWord`). Includes first steps towards non-deterministic automata (`NFAtoHypergraph`). |
| `Turing -> Hypergraph.nb` | Compiles Turing machines into hypergraph rewriting (`TuringToHypergraph`, `TuringRule`), with the tape encoded by `initialTapeToHypergraph`. Extends this to non-deterministic Turing machines as multiway systems (`MultiwayTuringToHypergraph`). Includes tests and examples, including busy beaver machines. |
| `Faux Racket.nb` | A small LISP-style arithmetic language ("Faux Racket"): a parser, an applicative-order compiler and a normal-order evaluator, which compile programs into hypergraphs (`compileAST`). |

## Requirements

Wolfram Language 13.1 or later (Mathematica or Wolfram Desktop). The notebooks use functions from the
[Wolfram Function Repository](https://resources.wolframcloud.com/FunctionRepository/) through `ResourceFunction`,
including `WolframModel`, so they need an internet connection the first time they run.

## Status and open questions

- Compiling non-deterministic finite automata this way is computationally expensive. Finding a more efficient
  encoding is an open question.
- The register machine compiler described in the write-up is not yet included in this repository.
- The notebooks are research notebooks and include working notes alongside the code.

## Author

Utkarsh Bajaj, University of Oxford.
