# Hydraulic Design of a Sedimentation Basin: Tracer Experiments and CFD in ANSYS Fluent

Study project (module MHSE09) in the M.Sc. Hydro Science and Engineering at TU Dresden, Chair of Process Engineering in Hydrosystems. Supervisor: Dr.-Ing. Masoud Haghshenasfard. I did this project together with Arjun Parajuli.

> **Status:** the results are being prepared for a journal paper. This README gives the idea, the method and the headline outcome. The full results, figures, report and replication materials will be added after publication.

---

## Question

Sedimentation basins are designed as if water moved through them like a plug. In real basins, short-circuiting, recirculation and stagnant zones waste part of the volume. We asked: **how much does an internal baffle improve the flow in a small laboratory basin, and can a 3D CFD model reproduce what we measure?**

## Project overview

| | |
|---|---|
| **Basin** | Plexiglass model, 526 × 200 × 243 mm, volume 23.46 L |
| **Experiment** | Pulse of methylene blue injected in front of the inlet at a steady flow of 460 mL/min; the run lasted about 175 minutes |
| **Measurement** | Video of the tracer, analysed frame by frame in FIJI (ImageJ) |
| **Model** | 3D CFD in ANSYS Fluent: single-phase, laminar, free-slip top surface, no energy equation |
| **Configurations** | Basin with and without a deflector baffle |
| **Analysis** | Residence time distribution (RTD), hydraulic indicators, velocity fields, and a study of the inlet velocity |

## Who did what

This is taken from the acknowledgement in the report.

| Part | Author |
|---|---|
| Introduction, literature review, theoretical background | Fashli (me) |
| Laboratory experimental setup | Fashli (me) |
| Image processing in FIJI | Fashli (me) |
| CFD model configuration, mesh independence study | Fashli (me) |
| Experimental and numerical results and discussion: RTD analysis, model validation, velocity and pathline evaluation, operational sensitivity analysis | Arjun Parajuli |
| Conclusions and engineering implications | Arjun Parajuli |

---

## Method

### 1. Tracer experiment
We filled the basin until the flow was steady, injected a small pulse of dye and filmed the basin until the dye had left. The theoretical detention time is τ = V/Q = 51 min.

### 2. From video to concentration (FIJI), my part
The dye absorbs light, so the brightness of the water changes with the dye concentration. We used the mean light intensity in a region near the outlet as a proxy for concentration (Beer–Lambert law):

1. Extract frames with adaptive timing: dense at the start, sparse in the slow tail.
2. Select the area of interest near the outlet, where reflections from the walls are weak.
3. Split the colour channels and keep the one where the dye absorbs most.
4. Invert the image, so that more dye means a higher value.
5. Stack the frames and subtract a background frame taken before the injection.
6. Extract the mean grey value of the region for each frame, giving the time series used for the RTD curves.

### 3. CFD model, my part
- The geometry is the experimental basin, built in ANSYS Design Modeller.
- A mesh independence study gave **773,744 tetrahedral cells** with inflation layers in selected regions.
- Single-phase laminar flow, justified by an inlet Reynolds number of about 1,400 at 0.2 m/s, with a free-slip top surface and a constant temperature.
- A monitor at the outlet records the tracer over time. A simulation took about 12–13 hours on an HPC cluster.

---

## Visual gallery

| Laboratory setup | CFD mesh (773,744 cells) |
|---|---|
| ![Laboratory setup](assets/laboratory-setup.png) | ![CFD mesh](assets/mesh-generation.png) |

### Tracer transport in the CFD model
![CFD tracer transport](assets/cfd-fluid-flow.gif)

## Headline outcome

- The CFD model reproduced the laboratory tracer experiment for the basin with a baffle: the mean residence time within 6% and the peak time within 12% of the measured values.
- The baffle deflects the inlet jet downward and brings the mean residence time of the basin much closer to the theoretical detention time.
- The inlet velocity changes both the stagnant zones and the mixing in the basin, so flow rate alone is not enough to optimise the design.

The numbers, curves and the discussion will be published in the paper.

## Limitations

- One experimental run per configuration.
- Concentration is inferred from light intensity near the outlet, not from outflow samples.
- The CFD model is single-phase, so it shows the hydraulics and not the removal of solids.
- The CFD model was compared with the experiment for the baffled basin at one inlet velocity only.

## Skills shown

- Setting up a 3D CFD model in ANSYS Fluent (geometry, mesh independence, boundary conditions, flow regime check).
- Turning video into a measurement: adaptive frame sampling and background-corrected intensity in FIJI.
- Residence time distribution analysis and hydraulic indicators (with my co-author).
- Working in a team with a clear split of work.

## Folder contents

```text
.
├── README.md
└── assets/          # laboratory-setup.png, mesh-generation.png, cfd-fluid-flow.gif
```

## Authors

Fashli Adli Wal Ikhsan · [github.com/fashliadli](https://github.com/fashliadli)
Arjun Parajuli (co-author)
