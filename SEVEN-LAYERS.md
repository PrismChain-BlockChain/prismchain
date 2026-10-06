# 🌈 PrismChain — Seven Layers

> **PrismChain is the seven-layer blockchain.**

PrismChain is built around seven spectral layers:

**RED · ORANGE · YELLOW · GREEN · BLUE · INDIGO · VIOLET**

These seven layers form the computational structure of PrismChain.

Each layer maintains its own block state and block integrity. The current implementation demonstrates seven independently operating layer processes whose latest block hashes are collected by the White Light Block process.

The seven layers are not seven separate blockchains.

They are the seven participating layers of a single PrismChain architecture.

---

## 1. The Seven-Layer Model

The fundamental PrismChain structure is:

```text
                    PRISMCHAIN

       ┌──────────┬──────────┬──────────┬──────────┐
       │   RED    │  ORANGE  │  YELLOW  │  GREEN   │
       ├──────────┼──────────┼──────────┼──────────┤
       │   BLUE   │  INDIGO  │  VIOLET  │          │
       └──────────┴──────────┴──────────┴──────────┘
                         │
                         ▼
                 WHITE LIGHT BLOCK
```

The seven colors are the fundamental spectral components of the chain.

They participate in a common computational architecture and contribute their current layer state to the formation of a White Light Block.

The White Light Block is therefore not an eighth layer.

It is the unified block produced from the participating seven layers.

---

## 2. The Seven Spectral Layers

| Layer      | Current implementation |
| ---------- | ---------------------- |
| **RED**    | Spectral layer         |
| **ORANGE** | Spectral layer         |
| **YELLOW** | Spectral layer         |
| **GREEN**  | Spectral layer         |
| **BLUE**   | Spectral layer         |
| **INDIGO** | Spectral layer         |
| **VIOLET** | Spectral layer         |

The current public implementation does not establish seven different application-specific roles for these colors.

That distinction matters.

PrismChain's architecture defines seven spectral layers, but the present implementation should be documented according to what the code actually demonstrates rather than assigning theoretical functions that have not yet been established through implementation and testing.

Therefore:

> **RED is RED. ORANGE is ORANGE. YELLOW is YELLOW. GREEN is GREEN. BLUE is BLUE. INDIGO is INDIGO. VIOLET is VIOLET.**

Their deeper computational relationships remain part of PrismChain's ongoing research and development.

---

# 3. Layer Independence

Each spectral layer currently operates as an individual layer process.

The implementation provides each layer with its own latest-block file:

```text
layers/
├── red_latest.json
├── orange_latest.json
├── yellow_latest.json
├── green_latest.json
├── blue_latest.json
├── indigo_latest.json
└── violet_latest.json
```

Each layer maintains its own block lifecycle.

At the current implementation level, that lifecycle includes:

1. Creating a block
2. Recording a timestamp
3. Recording block data
4. Recording the previous block hash
5. Computing a block hash
6. Validating the block
7. Saving the latest block
8. Advancing the layer's previous hash

This provides an important architectural property:

> **Each spectral layer maintains its own local chain state before contributing to the unified White Light Block.**

---

# 4. Layer Block Structure

The current layer implementation uses a common block structure.

A representative layer block contains:

```json
{
  "block_number": 0,
  "timestamp": 0,
  "data": "...",
  "previous_hash": "...",
  "hash": "..."
}
```

The exact values vary as the layer operates.

The important structural fields are:

### `block_number`

Identifies the layer block position.

### `timestamp`

Records when the block was produced.

### `data`

Contains the data produced by the layer process.

### `previous_hash`

Links the current layer block to the preceding block in that layer's chain.

### `hash`

Provides the integrity value calculated from the block contents.

---

# 5. Layer Integrity

The current layer implementation calculates a SHA-256 hash from selected block fields.

The calculation is based on:

```text
timestamp
previous_hash
data
```

The resulting hash is stored with the block.

The layer then validates the block by checking:

* required fields are present,
* the block hash can be reproduced from the block contents,
* the reproduced hash matches the stored hash.

Conceptually:

```text
Layer Data
    │
    ├── timestamp
    ├── previous_hash
    └── data
          │
          ▼
      SHA-256
          │
          ▼
      block hash
          │
          ▼
      validation
```

This creates a basic integrity boundary for each spectral layer.

---

# 6. Independent Layer Chains

The seven layers do not simply write seven unrelated snapshots.

Each layer maintains its own previous-hash relationship.

Conceptually:

```text
RED

Block₁ → Block₂ → Block₃ → Block₄ → ...


ORANGE

Block₁ → Block₂ → Block₃ → Block₄ → ...


YELLOW

Block₁ → Block₂ → Block₃ → Block₄ → ...


GREEN

Block₁ → Block₂ → Block₃ → Block₄ → ...


BLUE

Block₁ → Block₂ → Block₃ → Block₄ → ...


INDIGO

Block₁ → Block₂ → Block₃ → Block₄ → ...


VIOLET

Block₁ → Block₂ → Block₃ → Block₄ → ...
```

Each chain therefore has its own local continuity.

The White Light Block process then observes the latest state of all seven.

---

# 7. From Seven Layers to White Light

The fundamental transition is:

```text
RED       ─┐
ORANGE    ─┤
YELLOW    ─┤
GREEN     ─┤
BLUE      ─┤──► Seven Layer Hashes
INDIGO    ─┤
VIOLET    ─┘
                 │
                 ▼
          White Light Block
```

The current implementation performs this transition by loading the latest block from each layer and collecting its hash.

The resulting structure is conceptually:

```text
spectral_hashes = {
    "Red":    red_hash,
    "Orange": orange_hash,
    "Yellow": yellow_hash,
    "Green":  green_hash,
    "Blue":   blue_hash,
    "Indigo": indigo_hash,
    "Violet": violet_hash
}
```

These seven spectral hashes become part of the White Light Block.

---

# 8. The Seven-Layer Contribution

The current implementation therefore establishes a specific relationship between the layers and the White Light Block:

```text
Layer state
     ↓
Layer block
     ↓
Layer hash
     ↓
Spectral hash
     ↓
White Light Block
```

The WLB process does not need to reproduce the internal block calculation of each layer.

Instead, it consumes the layer's resulting hash.

This creates a clear computational boundary:

> **The layers produce their own state. The White Light Block combines the resulting spectral state.**

---

# 9. White Light Block Input

The current WLB implementation receives two principal inputs:

```text
Seven spectral hashes
        +
Previous White Light Block hash
        │
        ▼
White Light Block
```

The WLB stores the seven spectral hashes as:

```json
{
  "spectral_hashes": {
    "Red": "...",
    "Orange": "...",
    "Yellow": "...",
    "Green": "...",
    "Blue": "...",
    "Indigo": "...",
    "Violet": "..."
  }
}
```

The seven hashes therefore remain individually identifiable inside the resulting block.

They are not discarded into a single opaque value.

---

# 10. WLB Data Formation

The current implementation constructs the WLB data from the seven spectral hashes.

Conceptually:

```text
Red hash
+
Orange hash
+
Yellow hash
+
Green hash
+
Blue hash
+
Indigo hash
+
Violet hash
        │
        ▼
     WLB data
```

The resulting data is then incorporated into the White Light Block hash calculation together with the previous White Light Block hash and timestamp.

This creates the current demonstrated chain:

```text
Seven Layer Hashes
        │
        ▼
    WLB Data
        │
        ├── previous WLB hash
        ├── timestamp
        │
        ▼
     WLB Hash
```

---

# 11. White Light Block Continuity

The White Light Block itself maintains chain continuity.

The first WLB uses a genesis previous hash:

```text
0000000000000000...
```

Subsequent White Light Blocks use the hash of the preceding WLB.

Conceptually:

```text
WLB₁
  │
  └── hash₁
        │
        ▼
WLB₂
  │
  └── hash₂
        │
        ▼
WLB₃
  │
  └── hash₃
        │
        ▼
...
```

This creates a second level of chain continuity.

---

# 12. Two Levels of Integrity

PrismChain's current implementation therefore demonstrates two related levels of hash continuity.

### Level 1 — Spectral Layer Integrity

Each layer maintains its own block-to-block relationship:

```text
Layer Block
     │
     ▼
Previous Layer Hash
```

### Level 2 — White Light Integrity

The WLB incorporates the current hash from every layer and links itself to the previous WLB:

```text
Seven Layer Hashes
        │
        ▼
White Light Block
        │
        ▼
Previous WLB Hash
```

Together:

```text
Seven Layer Chains
        │
        ▼
Seven Current Layer Hashes
        │
        ▼
White Light Block
        │
        ▼
White Light Chain
```

This is the core structural relationship currently demonstrated by the Clean Version implementation.

---

# 13. Why Seven Layers Matter

The seven-layer architecture creates a computational structure that is different from a conventional single-chain model.

A conventional simplified model can be represented as:

```text
Transactions
     │
     ▼
Block
     │
     ▼
Chain
```

The current PrismChain model can be represented as:

```text
              ┌── RED ────────┐
              ├── ORANGE ─────┤
              ├── YELLOW ─────┤
              ├── GREEN ──────┤
              ├── BLUE ───────┤
              ├── INDIGO ────┤
              └── VIOLET ────┘
                       │
                       ▼
                White Light Block
                       │
                       ▼
                White Light Chain
```

The distinction is architectural.

PrismChain does not begin with a single block and then describe it as spectral.

It begins with seven participating spectral layers and produces a unified White Light Block from their state.

---

# 14. The Layers Are Not Seven Separate Blockchains

It is important not to misunderstand the model.

The seven layers are not intended to represent seven independent blockchains that merely happen to communicate.

They are components of one PrismChain computational architecture.

The relationship is:

```text
RED
ORANGE
YELLOW
GREEN
BLUE
INDIGO
VIOLET
      │
      ▼
PRISMCHAIN
      │
      ▼
WHITE LIGHT BLOCK
```

The seven layers are therefore better understood as **participating computational layers within one blockchain architecture**.

---

# 15. The Layers Are Not an Eighth Layer

The White Light Block is sometimes easier to misunderstand because it is visually represented as white.

White does not represent an additional spectral layer.

The architecture is:

```text
7 Spectral Layers
       │
       ▼
Spectral Combination
       │
       ▼
White Light Block
```

Not:

```text
8 Layers
       │
       ▼
White Light Block
```

The White Light Block is the resulting unified block.

---

# 16. Current Implementation vs. Future Research

The present implementation establishes the structural relationship between seven layer processes and the White Light Block.

It does **not**, by itself, establish every deeper theoretical property associated with the PrismChain research program.

The following distinction is intentional.

### 🟢 Currently demonstrated

* Seven named spectral layers
* Independent layer block generation
* Layer block hashing
* Layer block validation
* Layer-local previous-hash continuity
* Seven latest layer states
* Collection of seven layer hashes
* White Light Block formation
* White Light Block hashing
* Previous White Light Block continuity
* Persistent White Light chain data

### 🔵 Architecture / Development

* Native Conduits
* PrismInput
* PrismOutput
* Ethereum integration
* Rainbow Ring integration
* External chain settlement relationships
* Broader ecosystem interfaces

### 🟣 Experimental

* End-to-end external-chain integration
* New computational relationships discovered through implementation
* Experimental demonstrations beyond the current core runtime

### 🔬 Research

* Deeper Spectral Mathematics
* Spectral relationships
* Resonance
* Geometric relationships
* Computational models derived from those relationships

### 🔴 Private

* Proprietary implementation
* Undisclosed mathematical derivations
* Unreleased optimization techniques
* Unreleased protocol mechanisms

The public documentation follows the rule:

> **Built is built. Research is research. Vision is vision. Secrets stay secret.**

---

# 17. What the Current Seven-Layer Implementation Does Not Claim

The existence of seven layer processes should not automatically be interpreted as proof of:

* production consensus,
* decentralized validator operation,
* production network security,
* economic security,
* production transaction throughput,
* production external-chain settlement,
* Byzantine fault tolerance,
* production interoperability,
* production cryptographic proofs,
* or any specific performance advantage.

Those properties require separate implementation and evidence.

The purpose of this document is to describe the seven-layer architecture and the behavior that is currently demonstrated.

---

# 18. Layer Symmetry

The current implementation uses a common structural pattern across the seven layers.

Each layer has the same fundamental responsibilities:

```text
Create
  ↓
Hash
  ↓
Validate
  ↓
Save
  ↓
Continue
```

This structural symmetry is important.

It means that the seven layers can participate in a common architectural lifecycle without requiring the public documentation to invent seven unrelated computational systems.

The deeper question is not whether every layer has a completely different block implementation.

The deeper question is what relationships between the seven layers can be established as the PrismChain implementation evolves.

That question belongs to ongoing research and experimentation.

---

# 19. Layer Relationships

The seven layers become most significant when considered together.

The current implementation demonstrates the first concrete relationship:

```text
Seven Independent Layer States
              │
              ▼
       Seven Layer Hashes
              │
              ▼
       Unified WLB State
```

Future work can investigate additional relationships between the layers.

Those relationships should be introduced only when they are:

1. mathematically defined,
2. implemented,
3. tested,
4. experimentally validated,
5. and appropriately documented.

This prevents theoretical language from being mistaken for demonstrated protocol behavior.

---

# 20. Seven Layers as the Computational Core

The seven layers form the heart of PrismChain.

The surrounding ecosystem exists around this core.

Conceptually:

```text
                    SPECTRAL DYAD
                 observes and guides
                         │
                         ▼
                ┌─────────────────┐
                │    PRISMCHAIN   │
                │                 │
                │  RED            │
                │  ORANGE         │
                │  YELLOW         │
                │  GREEN          │
                │  BLUE           │
                │  INDIGO         │
                │  VIOLET         │
                │                 │
                │  WHITE LIGHT    │
                │     BLOCK       │
                └─────────────────┘
                         │
                         ▼
                  RAINBOW RING
                    connects
                         │
                         ▼
                External Blockchains
```

This separation of roles is deliberate.

**PrismChain computes.**

The surrounding architecture connects, verifies, settles, observes, and guides according to its respective role.

---

# 21. Seven Layers and Native Conduits

When PrismChain connects to an external blockchain, the external blockchain does not become another PrismChain spectral layer.

Instead, the external chain reaches PrismChain through the surrounding integration architecture.

Conceptually:

```text
External Blockchain
        │
        ▼
 Native Conduit
        │
        ▼
   PrismInput
        │
        ▼
    PrismChain
        │
 ┌──────┴──────┐
 ▼             ▼
7 Layers    WLB
 │             │
 └──────┬──────┘
        ▼
   PrismOutput
        │
        ▼
 Rainbow Ring
        │
        ▼
Settlement / Relationship
```

This preserves the identity of the seven-layer PrismChain architecture.

An external blockchain is connected to PrismChain.

It does not become an eighth spectral layer.

---

# 22. The Seven-Layer Boundary

The seven-layer boundary can therefore be summarized as:

```text
              PRISMCHAIN CORE

        ┌───────────────────────┐
        │         RED           │
        │       ORANGE          │
        │       YELLOW          │
        │        GREEN          │
        │        BLUE           │
        │       INDIGO          │
        │       VIOLET          │
        │                       │
        │   WHITE LIGHT BLOCK   │
        └───────────────────────┘
```

Inputs enter the PrismChain computational boundary through the appropriate surrounding architecture.

Outputs leave through the appropriate surrounding architecture.

The seven spectral layers remain the computational core.

---

# 23. Evidence-Driven Development

The seven-layer model is documented according to an evidence-driven development process:

```text
Question
   ↓
Hypothesis
   ↓
Research
   ↓
Architecture
   ↓
Implementation
   ↓
Test
   ↓
Experiment
   ↓
Result
   ↓
Evidence
   ↓
Documentation
```

This process is especially important for PrismChain because the architecture includes both implemented systems and ongoing mathematical research.

A proposed relationship is not presented as a proven relationship.

A specification is not presented as proof.

A prototype is not presented as production.

A successful experiment is documented as an experiment until sufficient evidence exists to establish a stronger claim.

---

# 24. Implementation Is the Source of Demonstrated Behavior

PrismChain development follows:

```text
INSPECT
   ↓
SPECIFY
   ↓
TEST
   ↓
CONNECT
   ↓
TUNE
   ↓
VERIFY
```

Specifications provide architectural guidance.

Actual implementation and testing determine what the system truly does.

When implementation reveals a better or different mechanism, the documentation should be updated to describe the system that actually exists.

This keeps the public architecture synchronized with reality.

---

# 25. What This Document Establishes

This document establishes the public architectural definition of the seven PrismChain layers:

> **PrismChain is composed of seven spectral layers: RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, and VIOLET.**

The current implementation demonstrates that:

> **Each layer can maintain its own block state and integrity, and the resulting seven layer hashes can be collected into a unified White Light Block that continues its own chain.**

That is the current evidence-backed foundation.

The deeper mathematical relationships between the seven layers remain an active area of PrismChain research and development.

---

# 26. The Core Principle

The seven layers are not decorative.

They are not merely seven colors applied to a conventional blockchain.

They define the fundamental computational structure around which PrismChain is built.

```text
RED
ORANGE
YELLOW
GREEN
BLUE
INDIGO
VIOLET
      │
      ▼
   COMPUTE
      │
      ▼
WHITE LIGHT
   BLOCK
```

**PrismChain is the seven-layer blockchain.**

The public goal is not to claim more than has been demonstrated.

The goal is to make the architecture understandable, the implementation behavior inspectable, the research distinguishable from the implementation, and the evidence strong enough that the differences can be discovered rather than merely asserted.

---

## Status

| Component                         | Status                    |
| --------------------------------- | ------------------------- |
| Seven spectral layers             | 🟢 Built                  |
| Independent layer block lifecycle | 🟢 Built                  |
| Layer block hashing               | 🟢 Built                  |
| Layer block validation            | 🟢 Built                  |
| Layer-local hash continuity       | 🟢 Built                  |
| Seven-hash WLB input              | 🟢 Built                  |
| White Light Block formation       | 🟢 Built                  |
| White Light Block continuity      | 🟢 Built                  |
| Deeper spectral relationships     | 🔬 Research               |
| Native Conduits                   | 🔵 Development            |
| Ethereum integration              | 🟣 Experimental           |
| Rainbow Ring                      | 🔵 Development            |
| Spectral Dyad                     | 🔵 Research / Development |
| Fluxlings                         | 🔵 Research / Development |
| Proprietary mechanisms            | 🔴 Private                |

---

## Final Definition

> **PrismChain is the seven-layer blockchain.**

**RED · ORANGE · YELLOW · GREEN · BLUE · INDIGO · VIOLET**

Seven spectral layers.

One computational architecture.

One unified White Light Block.

**Prism computes.**

**The surrounding architecture connects, verifies, settles, observes, and guides according to its respective role.**
