# dimod

[![Build Status](https://travis-ci.org/dwavesystems/dimod.svg?branch=master)](https://travis-ci.org/dwavesystems/dimod)

A shared API for QUBO/Ising samplers.

## Included Samplers

dimod comes with a few samplers that are useful as reference implementations and for unit testing.

* SimulatedAnnealingSampler: A reference implementation of a simulated annealing algorithm.
* ExactSolver: determines the energy for every possible sample, but is extremely slow.
* RandomSampler: Generates random samples. Used for testing.

## Basic Usage

```python
>>> import dimod
>>> sampler = dimod.SimulatedAnnealingSampler()
>>> Q = {(0, 0): 1, (1, 1): 1, (0, 1): -1}
>>> response = sampler.sample_qubo(Q)
>>> h = {0: 1, 1 : 1}
>>> J = {(0, 1): -1}
>>> spin_response = sampler.sample_ising(h, J)
```

The response object returned has many ways to access the information

```python
>>> list(response)  # your results might vary
[{0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 1.0, 1: 0.0}, {0: 1.0, 1: 0.0}, {0: 0.0, 1: 1.0}, {0: 0.0, 1: 1.0}, {0: 1.0, 1: 1.0}]
>>> list(response.samples())
[{0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 0.0, 1: 0.0}, {0: 1.0, 1: 0.0}, {0: 1.0, 1: 0.0}, {0: 0.0, 1: 1.0}, {0: 0.0, 1: 1.0}, {0: 1.0, 1: 1.0}]
>>> list(response.energies())
[0.0, 0.0, 0.0, 0.0, 0.0, 1.0, 1.0, 1.0, 1.0, 1.0]
>>> list(response.items())  # samples and energies
[({0: 0.0, 1: 0.0}, 0.0), ({0: 0.0, 1: 0.0}, 0.0), ({0: 0.0, 1: 0.0}, 0.0), ({0: 0.0, 1: 0.0}, 0.0), ({0: 0.0, 1: 0.0}, 0.0), ({0: 1.0, 1: 0.0}, 1.0), ({0: 1.0, 1: 0.0}, 1.0), ({0: 0.0, 1: 1.0}, 1.0), ({0: 0.0, 1: 1.0}, 1.0), ({0: 1.0, 1: 1.0}, 1.0)]
```

See documentation for more examples.

## Install

Compatible with Python 2 and 3.

`python setup.py install`

## License

Released under the Apache License 2.0. See LICENSE.txt

