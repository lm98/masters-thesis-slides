---
theme: default
title: Welcome
class: text-center
layout: cover
transition: slide-left
---

## Design and development of a Rust-based execution platform for Aggregate Computing

*candidate: Micelli Leonardo*  
*supervisor: Prof. Viroli Mirko*  
*co-supervisor: Dr. Aguzzi Gianluca*  
*academic year: 2023-2024*

---
transition: slide-left
---

# Table of contents
<Toc maxDepth="1"></Toc>

---
transition: slide-left
---

# A new IoT landscape: the Pervasive Computing world

- The expansion of the IoT has led to the spread of computational power, embedded in our everyday environment.
- In this new landscape, computation is pervasive and almost invisible to the user.
- A new type of system emerges from this context: the Collective System.

## Collective Systems

- CSs are systems composed by many components.
- These components accomplish a *collective task*, strongly relying on the interaction between them.
- CSs can show inherent adaptiveness, namely: the ability to *adapt in* and *evolve with* the environment.
- Collective Adaptive Systems (CASs) become a relevant case study. 
  
---
layout: image
image: ./images/crowd.jpg
transition: slide-left
---
# A case study for CASs
---
transition: slide-left
---
# How to engineer CASs?
- This novel situation highlights the need to tackle the complexity of designing and developing such systems.
- Aggregate Computing is a paradigm that brings a 

---
transition: slide-left
---
# State of the art in AC frameworks
## ScaFi
- Based on the *highly expressive* and powerful Scala language.
- JVM-based framework.
```scala
def gradient(): Double = rep(Double.PositiveInfinity) { d =>
    mux(isSource)(0.0)(foldhoodPlus(Double.PositiveInfinity)(Math.min)(nbr(d) + 1.0))
  }
```

## FCPP
- Based on the *highly efficient* and fast C++ language.
- Can run on most devices, included thin devices.

```c++
DEF() double gradient(ARGS, bool source) { CODE
    return nbr(CALL, INF, [&] (field<double> d) {
        double v = source ? 0.0 : INF;
        return min_hood(CALL, d + node.nbr_dist(), v);
    });
}
```

---
transition: slide-left
---
# The RuFi project
Has the objectives of:
- providing a high-level DSL for Aggregate Computing, akin to ScaFi;
- support a vast number of devices, even resource-constrained ones, akin to FCPP.

```rust
pub fn gradient() -> fn(&RoundVM) -> f64 {
    rep!(|_| f64::INFINITY, |vm1, d| {
        mux(
            vm1,
            is_source,
            |_| 0.0,
            foldhood_plus!(|_| f64::INFINITY, |a, b| a.min(b), |vm2| {
                nbr(vm2, |_| d) + 1.0
            }),
        )
    })
}
```