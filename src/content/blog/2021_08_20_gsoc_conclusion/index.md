---
title: "A Summer in Pull Requests"
tags: ["GSoC", "Molecular Dynamics", "Message"]
description: "My summer written in the language of pull requests."
author: "Orion Cohen"
date: "2020-08-20"
---

Yesterday, I pushed [solvation_analysis](https://pypi.org/project/solvation-analysis/) to PyPI, the culmination of a summer of work and my first python package. This is the story of my Google Summer of Code written in the language of Pull Requests. 

---

## Template for a snazzy package
PR [#7](https://github.com/MDAnalysis/solvation-analysis/pull/7) and [#20](https://github.com/MDAnalysis/solvation-analysis/pull/20)

My summer began with a duo of pull requests. PRs #7 and #20 filled out the template generated by the [MolSSI cookiecutter](https://orioncohen.com/blog/2021_07_23_gsoc_template/), creating a fashionable scaffold that my code could fit into. PR #6 gave me fancy badges to announce my affiliation with MDAnalysis and to convince users that my code really did work. PR #20 brought a real README, explaining what `solvation_analysis` is supposed to do. In essence, the PRs set up the trappings of a real package, assuring users (and myself) of certain core competence in the development.

---

## Testing, testing, one-two-three
PR [#6](https://github.com/MDAnalysis/solvation-analysis/pull/6), [#16](https://github.com/MDAnalysis/solvation-analysis/pull/16),  and [#17](https://github.com/MDAnalysis/solvation-analysis/pull/17)

A package isn't really complete without robust testing. PR #6 introduced the initial code base and some rudimentary testing. With PR #16, I started using pytest, which made writing and using tests much easier. I made use of pytest fixtures to easily feed state into unit tests and pytest parameterization to loop over values. In PR #17, I integrated this work into GitHub CI, finalizing a critical component of my development workflow. 

---

## Cutting off Radial Distribution Functions
PR [#25](https://github.com/MDAnalysis/solvation-analysis/pull/25)

PR #25 was a science challenge in addition to a software challenge. I needed a method to robustly find the first minima of noisy RDF data. This was needed to automate the instantiation of the solution class. I settled on a polynomial interpolation of the RDF followed by 2nd-order differentiation to find the minima. This worked well for smooth RDFs but failed for RDFs with noise. As quick fix, I added in several hokey heuristics to get the solvation distances identified on my noisy test data. For now, the RDF parser works for reasonably smooth data and warns users when it fails.

---

## Analysis: the mega-PR
PR [#29](https://github.com/MDAnalysis/solvation-analysis/pull/29)

For better or worse, this is where my good intentions of small, self-contained PRs went out the window. PR #29 is responsible for the majority of functionality in solvation_analysis. It implemented the Solution class and all of the analysis functions, reaching 250 comments from myself and my mentors. The upside of a massive PR is that keeping feedback in one place gave me an opportunity to iterate. I tried several designs before settling on the Solution-centered package, which provides a very clean API. I also iterated through several underlying data structures, eventually settling on a simple Pandas.DataFrame that allowed me to vectorize all of the analysis operations.

---

## In pursuit of user number one
PR [#36](https://github.com/MDAnalysis/solvation-analysis/pull/36)

Learning from a tutorial is substantially easier than learning from documentation. People tend to respond much better to examples than specifications. The tutorial introduced in PR #36 walks users through the basic functionality of solvation_analysis and how to respond to common errors. 

## Release and versioning!
PR [#37](https://github.com/MDAnalysis/solvation-analysis/pull/37)

Releasing a package to PyPI is actually pretty easy. For this PR, I learned to use Versioneer and Twine for Python release management. With just a few terminal commands and file edits, I was able to set up a functioning release management system and put version 0.1.1 on PyPI.

---

## The Future
PR [#39](https://github.com/MDAnalysis/solvation-analysis/pull/39) and [#40](https://github.com/MDAnalysis/solvation-analysis/pull/40)

While GSoC is ending, development of solvation_analysis is not. PR #39 adds solvent correlation analysis, statistics on uncoordinated solvents, and a new Valency class. PR #40 introduces a tutorial on interactive visualization.  These are all features I am excited for and look forward to developing. 

---

I am thankful for Google's generous support of open source software, my mentors kind and helpful feedback, and the whole MDAnalysis team's support and advice.