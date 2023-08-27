---
hide:
  - navigation
---

# Cortex CLI (corcli) documentation

[Cortex] is a Powerful Observable Analysis and Active Response Engine. While it is usually used along with [TheHive Project], why not using it on a daily basis in a CLI fashion.

`corcli` was built in Python for this specific purpose.

---

**Documentation:** [https://0xFustang.github.io/corcli-docs](https://0xFustang.github.io/corcli-docs)

**Source Code:** [https://github.com/0xFustang/corcli](https://0xFustang.github.io/corcli-docs)

---

## Features

Key features are:

- **Fast job submission**: Submit one or multiple observables to Cortex with a different set of analyzers
- **Bulk submission**: Submit multiple observables from a text file
- **Extract artifacts**: Display only the extracted artifacts (.e.g IOCs)
- **Download files**: Download extraced files when available
- **Use aliases for analyzers**: Map your own aliases to launch your favorite analyzers
- **Define alias presets**: Define analysers presets that will call a group of analysers
- **Multi instance config**: Submit your jobs to another Cortex instance

[TheHive Project]: https://thehive-project.org/
[Cortex]: https://github.com/TheHive-Project/Cortex