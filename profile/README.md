<div align="center">

# ASTRA

**Agentic Schema for Transparent Research Analysis**

*An open, declarative format for scientific analyses: what you want to learn, the choices you made along the way, and the evidence behind them.*

<a href="https://astra-spec.org"><img src="https://img.shields.io/badge/docs-astra--spec.org-334155?style=for-the-badge" alt="Documentation"></a>
<a href="https://astra-spec.org/latest/getting-started/"><img src="https://img.shields.io/badge/get_started-quick_start-426b78?style=for-the-badge" alt="Getting started"></a>
<a href="https://astra-spec.org/latest/specification/"><img src="https://img.shields.io/badge/read-the_specification-5b6b7f?style=for-the-badge" alt="Specification"></a>

</div>

---

## What is ASTRA?

Scientific results depend on methodological choices: which data to include, how to handle outliers, which prior to assume, which model to fit. In ordinary research code those choices end up scattered across notebooks, scripts, comments and memory, so by the time a result is published it is hard to say which choices produced it, which alternatives were considered, or why.

ASTRA gives every one of those choices an explicit place. An `astra.yaml` records an analysis's:

- **Inputs and outputs**: the data an analysis reads and the results it produces, with the recipe that builds each one.
- **Decisions**: each methodological choice, with the options that were considered and the rationale for them.
- **Insights and evidence**: the prior claims an analysis builds on and the findings it concludes, each backed by evidence: a paper (by DOI, down to the page or the quoted passage) or one of the analysis's own results.
- **Universes**: one option picked per decision, and so one complete, reproducible set of results. An analysis can carry many universes, which makes the space of defensible alternatives part of the record rather than a footnote.

AI agents are expanding the scale and speed of research, which moves the bottleneck from *producing* results to *trusting* them. ASTRA is the structured record that agents and people can both follow, check and extend. It is deliberately agnostic to how the analysis is executed: an agent, a workflow runner, a notebook or a human can all read the same spec and produce the results.

```yaml
# astra.yaml
spec_version: "0.1.0"
label: Iris Classification

outputs:
  accuracy:
    type: metric
    format: json
    decisions: [scaling, model]
    recipe:
      command: >-
        python src/evaluate.py --scaling {decisions.scaling}
        --model {decisions.model} --out {output}

decisions:
  scaling:
    label: Feature Scaling
    options:
      none:     { label: No Scaling }
      standard: { label: StandardScaler }
  model:
    label: Classification Model
    options:
      random_forest: { label: Random Forest }
      svm:           { label: SVM, requires: [scaling.standard] }

universes:
  baseline:
    decisions: { scaling: standard, model: random_forest }
```

Try it:

```bash
uv tool install astra-tools        # installs the `astra` CLI
astra init my-analysis && cd my-analysis
astra validate
astra plan
```

👉 **[Getting started](https://astra-spec.org/latest/getting-started/)** walks through a full analysis.

> [!WARNING]
> ASTRA is in **early alpha**. Expect breaking changes between minor versions, and pin the schema version in your analyses.

## About this organization

The **ASTRA Project** is the home of the ASTRA standard and its reference tooling.

ASTRA started at [Lightcone Research](https://github.com/LightconeResearch), which still writes most of the code today. From the start, the goal has been for ASTRA to become a **community-owned standard** rather than one organization's product: a format for scientific records in the agentic era should not sit behind any single vendor or tool. This organization is the first step towards that: a neutral home for the specification, independent of any one implementation, where the governance can grow as contributors from other groups, disciplines and tooling stacks join.

> [!NOTE]
> **We are moving in.** The ASTRA repositories are being transferred here from [LightconeResearch](https://github.com/LightconeResearch). Until the move is complete, the links below point to their current location; GitHub will redirect them once they are transferred.

## Repositories

| Repository | What it is |
|---|---|
| [**astra-spec**](https://github.com/LightconeResearch/astra-spec) | The specification: the LinkML schema, the generated JSON Schemas, the conformance suite, the RFCs, and the documentation at [astra-spec.org](https://astra-spec.org). |
| [**astra-tools**](https://github.com/LightconeResearch/astra-tools) | The Python SDK and the `astra` CLI: validation, inspection, planning and evidence verification. [`pip install astra-tools`](https://pypi.org/project/astra-tools/) |
| [**astra-typescript**](https://github.com/LightconeResearch/astra-typescript) | The TypeScript SDK, to validate and resolve ASTRA analyses in Node and the browser. [`npm install @astra-spec/sdk`](https://www.npmjs.com/package/@astra-spec/sdk) |
| [**astra-ui**](https://github.com/LightconeResearch/astra-ui) | Composable, themable React components to display ASTRA analyses. [`npm install @astra-spec/ui`](https://www.npmjs.com/package/@astra-spec/ui) |
| [**MySTRA**](https://github.com/LightconeResearch/MySTRA) | A [MyST](https://mystmd.org) plugin to write publications on top of ASTRA analyses, pulling in decisions, outputs and numbers by reference. |

### Built on ASTRA

ASTRA is meant to be consumed by many tools. If you build one, open an issue or a pull request on this repository and we will list it here.

- [**Lightcone**](https://github.com/LightconeResearch/lightcone-cli) by Lightcone Research: an agentic workflow layer that plans an analysis with an AI agent, records it as an `astra.yaml`, and runs every universe with a provenance record for each output.

## Get involved

ASTRA is intentionally early, and the most valuable thing it can have right now is contact with people trying to use it. Three kinds of contribution matter most during alpha:

- **Real-analysis attempts.** Take an analysis you have actually run and express it in ASTRA. Tell us what fits, what doesn't, and where you had to invent a workaround.
- **Schema review.** Read the [specification](https://astra-spec.org/latest/specification/) with an adversarial eye. Ambiguities and missing constraints are much easier to fix now than once the format has consumers.
- **Downstream tooling.** Build something that reads an `astra.yaml`: a runner, a renderer, an index, an editor. Even a prototype shows what is awkward to consume.

Where to go:

- **Schema and specification**: [astra-spec issues](https://github.com/LightconeResearch/astra-spec/issues).
- **CLI and Python SDK**: [astra-tools issues](https://github.com/LightconeResearch/astra-tools/issues).
- **Significant or contested changes** (new schema concepts, breaking changes, conventions): the [RFC process](https://astra-spec.org/latest/rfc-process/).

See the [Community page](https://astra-spec.org/latest/community/) and each repository's `CONTRIBUTING.md` for the details.

## Governance

All development happens in public, and decisions and their rationale are recorded as RFCs, so the evolution of the format stays auditable. During alpha, ASTRA is stewarded by the Lightcone Research core team. At v0.1 the project commits to a [community governance model](https://astra-spec.org/latest/governance/) with a steering council open to outside contributors, maintainers who earn that role through sustained contribution, and a binding RFC acceptance process. Governance changes are themselves made by RFC.

## License and citation

- **Schema**: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- **Code**: [BSD 3-Clause](https://opensource.org/license/bsd-3-clause)

Both allow unrestricted academic and commercial use. If you use ASTRA in your research or tooling, please cite it with the **"Cite this repository"** button on [astra-spec](https://github.com/LightconeResearch/astra-spec), and include the schema version you targeted.
