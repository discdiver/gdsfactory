# GDS Factory 

[![docs](https://github.com/gdsfactory/gdsfactory/actions/workflows/pages.yml/badge.svg)](https://gdsfactory.github.io/gdsfactory/)
[![PyPI](https://img.shields.io/pypi/v/gdsfactory)](https://pypi.org/project/gdsfactory/)
[![PyPI Python](https://img.shields.io/pypi/pyversions/gdsfactory.svg)](https://pypi.python.org/pypi/gdsfactory)
[![Downloads](https://static.pepy.tech/badge/gdsfactory)](https://pepy.tech/project/gdsfactory)
[![MIT](https://img.shields.io/github/license/gdsfactory/gdsfactory)](https://choosealicense.com/licenses/mit/)
[![codecov](https://img.shields.io/codecov/c/github/gdsfactory/gdsfactory)](https://codecov.io/gh/gdsfactory/gdsfactory/tree/main/gdsfactory)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/gdsfactory/binder-sandbox/HEAD)


GDS Factory makes hardware design accessible, intuitive, and fun—empowering everyone to build the future.

GDS Factory is an open source Python library for designing microchips, PCBs, and 3D-printable objects. 
GDS Factory supports the design of integrated circuits that use photonic, analog, quantum, and MEMS technologies, with built-in integrations from popular foundries. 

Write Python code, visualize designs in Jupyter notebooks or KLayout, and export CAD files (GDS, OASIS, STL, GERBER) for production.

![cad](https://i.imgur.com/3cUa2GV.png)

To take your design to the next level with validation and verification of your designs, access the drag-and drop GUI, and collaborate with teammates, use [GDS Factory+](https://docs.google.com/forms/d/e/1FAIpQLSdFav19xw4kMesr4IWj0rUt0myq0fUGlBj09aQuFCuUgd0Dow/viewform).


## Why use GDS Factory?

- **Fast, extensible, and easy to use** – designed for efficiency and flexibility.
- **Free and open-source** – no licensing fees, giving you the freedom to modify and extend it.
- **A thriving ecosystem** – the most popular EDA tool with a growing community of users, developers, and integrations with other tools.
- **Built on the open-source advantage** – just like the best machine learning libraries, GDS Factory benefits from continuous contributions, transparency, and innovation.

GDS Factory is blazing fast thanks to the KLayout C++ library for manipulating GDS objects. This speed is key when reading/writing large GDS files or doing millions of boolean operations.

| Benchmark      |  gdspy  | GDSFactory | Gain |
| :------------- | :-----: | :--------: | :--: |
| 10k_rectangles | 80.2 ms |  4.87 ms   | 16.5 |
| boolean-offset | 187 μs  |  44.7 μs   | 4.19 |
| bounding_box   | 36.7 ms |   170 μs   | 216  |
| flatten        | 465 μs  |  8.17 μs   | 56.9 |
| read_gds       | 2.68 ms |   94 μs    | 28.5 |


## Who's using GDSFactory?

Hundreds of organizations are using GDSFactory. Users include:

![logos](https://i.imgur.com/VzLNMH1.png)

"I've relied on **GDSFactory** for several tapeouts over the years. It's the only tool I've found that gives me the flexibility and scalability I need for a variety of projects."

<div style="text-align: right; margin-right: 10%;">Alec Hammond - <strong>Meta Reality Labs Research</strong></div>

---

"The best photonics layout tool I've used so far and it is leaps and bounds ahead of any commercial alternatives out there. Feels like GDSFactory is freeing photonics."

<div style="text-align: right; margin-right: 10%;">Hasitha Jayatilleka - <strong>LightIC Technologies</strong></div>

---

"As an academic working on large scale silicon photonics at CMOS foundries I've used GDSFactory to go from nothing to full-reticle layouts rapidly (in a few days). I particularly appreciate the full-system approach to photonics, with my layout being connected to circuit simulators which are then connected to device simulators. Moving from legacy tools such as gdspy and phidl to GDSFactory has sped up my workflow at least an order of magnitude."

<div style="text-align: right; margin-right: 10%;">Alex Sludds - <strong>MIT</strong></div>

---

"I use GDSFactory for all of my photonic tape-outs. The Python interface makes it easy to version control individual photonic components as well as entire layouts, while integrating seamlessly with KLayout and most standard photonic simulation tools, both open-source and commercial.

<div style="text-align: right; margin-right: 10%;">Thomas Dorch - <strong>Freedom Photonics</strong></div>


## GDS Factory quickstart

### Cloud
Run GDS Factory inside a Jupyter Notebook in the cloud with [Google Colab](), [Binder](https://mybinder.org/v2/gh/gdsfactory/binder-sandbox/HEAD), or [GitHub Codespaces](). 

If needed, install the GDS Factory package into a notebook:

```python
!pip install gdsfactory
```

Then, restart the notebook and start building your design following the instructions [below](#create-your-first-component).

### Local

Alternatively, run a Jupyter Notebook locally.

We recommend using a Python virtual environment with uv. 

If you don't already have [uv installed](https://docs.astral.sh/uv/getting-started/installation/) download and install for your machine type from the CLI:

```bash
# On macOS and Linux.
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```bash
# On Windows.
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Start a JupyterLab server in your browser:

```bash
uvx --python 3.13 --with  gdsfactory jupyterlab
```

This command creates a disposable virtual environment with Python 3.13 and the gdsfactory and jupyterlab packages installed. 

A browser window should open with JupyterLab running. If it doesn't, copy the URL printed in the terminal and paste it into your browser.

Alternatively install gdsfactory and jupyterlab into a conda or venv-managed Python virtual environment:

```bash
pip install gdsfactory jupyterlab
```

### Create your first component

```python
import gdsfactory as gf

# Create a new component
c = gf.Component()

# Add a rectangle
r = gf.components.rectangle(size=(10, 10), layer=(1, 0))
rect = c.add_ref(r)

# Add text elements
t1 = gf.components.text("Hello", size=10, layer=(2, 0))
t2 = gf.components.text("world", size=10, layer=(2, 0))

text1 = c.add_ref(t1)
text2 = c.add_ref(t2)

# Position elements
text1.xmin = rect.xmax + 5
text2.xmin = text1.xmax + 2
text2.rotate(30)

# Show the result in a notebook cell
c.plot()
```

## Additional workflows

Instead of Jupyter Notebooks, you can use KLayout to render designs defined in Python or YAML.
See the [KLayout section of the docs](./docs/layout.html) for information.

![workflow](https://i.imgur.com/KyavbHh.png)

GDS Factory+ provide a comprehensive end-to-end design flow that enables you to:

- **Design (Layout, Simulation, Optimization)**: Define parametric cell functions in Python to generate components. Test component settings, ports, and geometry to avoid unwanted regressions, and capture design intent in a schematic.
- **Verify (DRC, DFM, LVS)**: Run simulations directly from the layout using our simulation interfaces, removing the need to redraw your components in simulation tools. Conduct component and circuit simulations, study design for manufacturing. Ensure complex layouts match their design intent through Layout Versus Schematic verification (LVS) and are DRC clean.
- **Validate**: Define layout and test protocols simultaneously for automated chip analysis post-fabrication. This allows you to extract essential component parameters, and build data pipelines from raw data to structured data to monitor chip performance.

Input: Python or YAML text.
Output: A GDSII or OASIS file for fabrication, alongside component settings (for measurement and data analysis) and netlists (for circuit simulations) in YAML.

GDS Factory provide a common syntax for design (Ansys, Lumerical, Tidy3d, MEEP, DEVSIM, SAX, MEOW, Xyce, and others), verification, and validation.

![tool interfaces](https://i.imgur.com/j5qlFWj.png)


## Open-Source PDKs (No NDA required)

Integrate the component of these publicly available PDKs that do not require an NDA into your designs:

- [GlobalFoundries 180nm MCU CMOS PDK](https://gdsfactory.github.io/gf180/)
- [ANT / SiEPIC Ebeam UBC PDK](https://gdsfactory.github.io/ubc)
- [SkyWater 130nm CMOS PDK](https://gdsfactory.github.io/skywater130/)
- [VTT PDK](https://github.com/gdsfactory/vtt)
- [Cornerstone PDK](https://github.com/gdsfactory/cspdk)
- [Luxtelligence GF PDK](https://github.com/Luxtelligence/lxt_pdk_gf)


## Foundry PDKs (NDA required)

Access to the following PDKs requires a **GDSFactory+** subscription.
To sign up, visit [GDSFactory.com](https://gdsfactory.com/).

Available PDKs under NDA:

- AIM Photonics
- AMF Photonics
- CompoundTek Photonics
- Fraunhofer HHI Photonics
- Smart Photonics
- Tower Semiconductor PH18
- Tower PH18DA by OpenLight
- III-V Labs
- LioniX
- Ligentec
- Lightium
- Quantum Computing Inc. (QCI)


## GDS Factory+

**GDS Factory+** offers tools for verification and validation of your designs, as well as a Graphical User Interface for chip design. GDS Facttory+ is built on top of GDS Factory and provides a VSCode extension. It provides you:

- Foundry PDK access
- Schematic capture
- Device and circuit Simulations
- Design verification (DRC, LVS)
- Data analytics

Learn more about GDS Factory+ and how it can help you save money and time on chip design [GDSFactory.com](https://gdsfactory.com/).


## Next steps

- Work through the Jupyter Notebooks in the [notebooks folder](../notebooks).
- Watch the [![Video tutorials](https://img.shields.io/badge/youtube-Video_Tutorials-red.svg?logo=youtube)](https://www.youtube.com/@gdsfactory/playlists).
- [![Join the chat at https://gitter.im/gdsfactory-dev/community](https://badges.gitter.im/gdsfactory-dev/community.svg)](https://gitter.im/gdsfactory-dev/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
- [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=250169028)
- Interested in attending a training with GDS Factory+? Let us know here. TK
- [Visit the GDS Factory website](https://gdsfactory.com) to learn more about GDS Factory solutions.


## Contributing

A huge thanks to all the contributors who make this project possible!

We welcome all contributions—whether you're adding new features, improving documentation, or reporting bugs. Every contribution helps make GDS Factory better! See the [contributing guide](../contribution.html). TK check link

 and be part of the community. 🚀

![contributors](https://i.imgur.com/0AuMHZE.png)


## Stargazers

Like GDS Factory? Give us a star! ⭐️

[![Stargazers over time](https://starchart.cc/gdsfactory/gdsfactory.svg)](https://starchart.cc/gdsfactory/gdsfactory)


## Community

Join our growing community:
- [GitHub Discussions](https://github.com/gdsfactory/gdsfactory/discussions)
- [LinkedIn](https://www.linkedin.com/company/gdsfactory)
