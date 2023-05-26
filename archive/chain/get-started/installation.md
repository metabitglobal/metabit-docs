---
id: installation
title: Installation
description: "How to install Metabit Chain."
keywords:
  - docs
  - metabit
  - chain
  - install
  - installation
---

Please refer to the installation method more applicable to you.

Our recommendation is to use the pre-built releases and verify the provided checksums.

## Pre-built releases

Please refer to the [GitHub Releases](https://github.com/metabitglobal/metabit_chain) page for a list of releases.

Metabit Chain comes with cross-compiled AMD64/ARM64 binaries for Darwin and Linux.

---

## Building from source

Prior to using `go install` make sure that you have Go `>=1.18` installed and properly configured.

The stable branch is the branch of the latest release.

```shell
git clone https://github.com/metabitglobal/metabit_chain.git
cd metabit_chain/
go build -o metabit_chain main.go
sudo mv metabit_chain /usr/local/bin
```
