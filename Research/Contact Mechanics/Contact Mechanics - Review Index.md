---
type: literature-review-index
title: Contact Mechanics — Review Index
reviewed_on: 2026-09-07
topics: [contact-mechanics]
---

# Contact mechanics: reading map

This collection contains **13 full-paper reviews of existing Zotero PDFs**. Each review explains the main contribution, the actual results and assumptions, the mathematical setup, the proof or evidence chain, numerical evidence, and a separately labelled critical assessment. Equations use LaTeX; proof roadmaps use tables and, where useful, Mermaid diagrams. Zotero links return to the source item or PDF.

The reviews cover the complete supplied papers, including their appendices. They are source-grounded reading guides, not independent correctness certifications or reproductions of the experiments. Historical and priority claims have not been checked through a new literature search.

## Where to begin

Start with [Popp and Wall's dual-mortar overview](Popp%20and%20Wall%20%282014%29%20-%20Dual%20mortar%20overview.md) for a map of computational contact: weak constraints, multipliers, active sets, integration, and practical failure modes. Then choose a path according to the question you want to answer. These paths are the reviewer's learning recommendations, not claims that every later paper directly extends the preceding one.

| Your question | Suggested path |
|---|---|
| How do penalty and augmented-Lagrangian formulations enforce contact? | [Simo et al. 1985](Simo%20et%20al.%20%281985%29%20-%20Perturbed%20Lagrangian%20contact.md) → [Simo–Laursen 1992](Simo%20and%20Laursen%20%281992%29%20-%20Augmented%20Lagrangian%20friction.md) → [Laursen–Simo 1993](Laursen%20and%20Simo%20%281993%29%20-%20Large%20deformation%20frictional%20contact.md) |
| How do I follow a rigorous contact error analysis? | [Chouly et al. 2015](Chouly%20et%20al.%20%282015%29%20-%20Nitsche%20contact%20analysis.md) for consistency → stability → error estimates; then [Burman et al. 2016](Burman%20et%20al.%20%282016%29%20-%20Augmented%20Lagrangian%20finite%20elements.md) for stabilized multipliers and [Belgacem et al. 1998](Belgacem%20et%20al.%20%281998%29%20-%20Mortar%20contact%20analysis.md) for nonmatching interfaces |
| How are nonmatching or spline surfaces coupled? | [Popp–Wall 2014](Popp%20and%20Wall%20%282014%29%20-%20Dual%20mortar%20overview.md) → [Seitz et al. 2016](Seitz%20et%20al.%20%282016%29%20-%20Isogeometric%20dual%20mortar.md); compare [Hu et al. 2018](Hu%20et%20al.%20%282018%29%20-%20Skew-symmetric%20Nitsche%20IGA.md) for Nitsche enforcement |
| How can I solve the resulting coupled linear systems? | [Ferronato et al. 2019](Ferronato%20et%20al.%20%282019%29%20-%20Contact%20preconditioning.md), after understanding the displacement–multiplier system |
| How do adhesion, roughness, and cohesive laws change the physical model? | [Derjaguin et al. 1975](Derjaguin%20et%20al.%20%281975%29%20-%20Adhesive%20particle%20contact.md), [Persson 2006](Persson%20%282006%29%20-%20Rough%20surface%20contact.md), and [Salehani–Irani 2018](Salehani%20and%20Irani%20%282018%29%20-%20Three-dimensional%20cohesive%20law.md) address different modelling questions |

For an initial pass, read sections 2, 3, and 8 of each review. For analysis, read section 5 and follow its dependency table back to the cited paper pages. Read section 7 separately so that reviewer criticism does not become confused with the authors' conclusions.

## Reviews by topic

### Lagrangian formulations

| Review | Central question or contribution |
|---|---|
| [Simo, Wriggers and Taylor (1985)](Simo%20et%20al.%20%281985%29%20-%20Perturbed%20Lagrangian%20contact.md) | Mixed contact pressure and perturbed Lagrangian formulation; how local pressure elimination produces a penalty treatment. |
| [Simo and Laursen (1992)](Simo%20and%20Laursen%20%281992%29%20-%20Augmented%20Lagrangian%20friction.md) | Augmented-Lagrangian frictional contact with equilibrium and multiplier-update loops; distinction between normal constraints and incremental tangential updates. |
| [Laursen and Simo (1993)](Laursen%20and%20Simo%20%281993%29%20-%20Large%20deformation%20frictional%20contact.md) | Moving contact geometry, convected friction history, and consistent Newton tangents for large-deformation frictional contact. |
| [Burman, Hansbo and Larson (2016)](Burman%20et%20al.%20%282016%29%20-%20Augmented%20Lagrangian%20finite%20elements.md) | Stability and error analysis for two augmented-Lagrangian scalar contact formulations, including jump-stabilized multipliers. |

### Mortar and isogeometric contact

| Review | Central question or contribution |
|---|---|
| [Belgacem, Hild and Laborde (1998)](Belgacem%20et%20al.%20%281998%29%20-%20Mortar%20contact%20analysis.md) | Error analysis for mortar contact on nonmatching meshes; different results and proof coverage for bilateral and unilateral contact. |
| [Popp and Wall (2014)](Popp%20and%20Wall%20%282014%29%20-%20Dual%20mortar%20overview.md) | Overview of dual mortar, multiplier condensation, active sets, and integration; concrete examples of robustness issues. |
| [Seitz et al. (2016)](Seitz%20et%20al.%20%282016%29%20-%20Isogeometric%20dual%20mortar.md) | Local dual NURBS basis construction; why stability and easy multiplier elimination do not guarantee high-order approximation. |

### Nitsche methods

| Review | Central question or contribution |
|---|---|
| [Chouly, Hild and Renard (2015)](Chouly%20et%20al.%20%282015%29%20-%20Nitsche%20contact%20analysis.md) | How symmetry changes parameter restrictions for well-posedness and error estimates in frictionless elastic contact. |
| [Hu et al. (2018)](Hu%20et%20al.%20%282018%29%20-%20Skew-symmetric%20Nitsche%20IGA.md) | Skew-symmetric Nitsche enforcement in IGA; parameter-free linear constraints versus parameter-dependent frictionless contact. |

### Solvers and preconditioning

| Review | Central question or contribution |
|---|---|
| [Ferronato et al. (2019)](Ferronato%20et%20al.%20%282019%29%20-%20Contact%20preconditioning.md) | Exact block decoupling, Schur complements, and sparse approximations for contact and poromechanical systems. |

### Adhesion, roughness, and cohesive models

| Review | Central question or contribution |
|---|---|
| [Derjaguin, Muller and Toporov (1975)](Derjaguin%20et%20al.%20%281975%29%20-%20Adhesive%20particle%20contact.md) | Adhesion of elastic particles using deformation energy and attraction outside the contact region. |
| [Persson (2006)](Persson%20%282006%29%20-%20Rough%20surface%20contact.md) | Contact mechanics across scales on randomly rough surfaces. |
| [Salehani and Irani (2018)](Salehani%20and%20Irani%20%282018%29%20-%20Three-dimensional%20cohesive%20law.md) | A proposed three-dimensional mixed-mode cohesive traction law, with algebraic checks and explicit validation limits. |

## Keep these distinctions in view

- **Modelling versus discretization versus solution:** an adhesion law defines physics; mortar or Nitsche chooses how to enforce constraints; a preconditioner accelerates an algebraic solve.
- **Different kinds of convergence:** an error bound as the mesh is refined does not guarantee that Newton converges from any initial guess. A faster multiplier iteration does not by itself establish a faster complete simulation.
- **Norms and parameters:** a pressure estimate weighted by the square root of a mesh-dependent parameter is not an unweighted pressure estimate. Parameter admissibility does not imply parameter-independent accuracy.
- **Evidence scope:** an overview can explain theory imported from another paper; a numerical test can explore situations outside a theorem's assumptions. The reviews identify these boundaries explicitly.

## Source coverage and exclusions

Scope was the existing **Contact Mechanics** Zotero collection (key `Z9LGID44`) and the library contact search used to check it. No new PDFs were downloaded. Each note records its exact attachment/version and page coverage. For Seitz et al., the matching attachment `RK67WD7S` was used; the other attachment under that item was an unrelated shell paper.

Three paper records had no existing PDF and therefore were not reviewed:

| Paper | Zotero record |
|---|---|
| Greenwood and Williamson (1966), *Contact of nominally flat surfaces* | [Open item](zotero://select/library/items/MD6TS3I9) |
| Mindlin (1949), *Compliance of Elastic Bodies in Contact* | [Open item](zotero://select/library/items/HCC3UCQI) |
| Johnson, Kendall and Roberts (1971), *Surface energy and contact of elastic solids* | [Open item](zotero://select/library/items/7DQDCWBR) |

The three book records—[Johnson (1985)](zotero://select/library/items/SUXBM7FM), [Wriggers (2006)](zotero://select/library/items/CUMBU85I), and [Laursen (2003)](zotero://select/library/items/7K7G3FWB)—were excluded from this paper-review pass.

## Connections and future graphs

Each review ends with a relationship table distinguishing explicit citations, proved dependencies, and reviewer-inferred conceptual connections. The paper links already create an Obsidian graph; lemma diagrams describe dependencies **within** individual papers. A future cross-paper graph can use the typed relationship tables without treating every conceptual link as a citation or a proof dependency.

The source-extraction archive remains in the workspace at `/Users/dimiao/Documents/New project/output/contact-mechanics-reviews/evidence`. Only reviews and this index are stored here; the original PDFs remain managed by Zotero.
