# drift2hcl 🚀

> Autonomous open-source engine converting live cloud infrastructure drift and JSON state diffs back into clean Infrastructure as Code (IaC) patches.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Go Version](https://img.shields.io/github/go-mod/go-version/YOUR_USERNAME/drift2hcl)](https://golang.org)
[![Build Status](https://github.com/YOUR_USERNAME/drift2hcl/actions/workflows/ci.yml/badge.svg)](https://github.com/YOUR_USERNAME/drift2hcl/actions)

---

## 🧐 The Problem: The 2 AM Drift Trap

Every engineering team encounters production emergencies. An engineer logs into the cloud console at 2 AM, applies a hotfix to a network security group or scales a resource, and resolves the incident. 

However, this creates an immediate **Infrastructure Drift**: your live production environment no longer matches your Git repository or your `terraform.tfstate`. 
* Traditional tools (like `terraform plan` or driftctl) can *detect* the drift, but leave the tedious reverse-engineering and coding work to humans.
* Forcing an automated revert (`terraform apply`) during an incident can break things further.

**`drift2hcl` bridges live cloud changes back into immutable Git workflows.**

---

## 🏗️ How It Works (Architecture)

`drift2hcl` avoids fragile regex or raw string replacement. Instead, it combines AST (Abstract Syntax Tree) parsing with local state verification:

```text
[ Live Cloud Diff / tfplan.json ]
              │
              ▼
    1. INGEST & NORMALIZE
              │
              ▼
    2. AST MUTATION (hclwrite) ──► Preserves human comments & formatting
              │
              ▼
    3. SANDBOX VERIFICATION ───► Runs `terraform validate` & `terraform plan` (0 diff check)
              │
              ▼
    4. AUTOMATED PR DISPATCH ──► Opens a clean Pull Request for review
