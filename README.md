# Photocatalytic hydrogen from hydrous hydrazine: experiments and a coupled CFD model

**BSc thesis · Chemical Engineering · Cyprus University of Technology · May 2026**
Supervisor: Prof. Achilleas Konstantinou. Experimental work at the Department of Industrial Chemistry, University of Milan (Prof. Alberto Villa).

*Full title: Experimental and Computational Investigation of Photocatalytic Hydrous Hydrazine Decomposition for Hydrogen Production over Rh-Based Catalysts in Stirred Batch Photoreactors.*

## In short

I made a Rh/TiO₂ photocatalyst, tested it in two stirred batch photoreactors, and set up a 2D COMSOL model that couples turbulent flow, UV radiation transport and reaction kinetics. The model shows where in each reactor the reaction happens. A parametric study shows that more lamp power stops helping at the irradiance used in the experiments.

## Key numbers

| What | Result |
|---|---|
| Catalyst screening (dark, 18 mL reactor) | 0.5% Rh/TiO₂-P25 reached 1.072 bar peak pressure, about 6× the next best catalyst (1% Cu/TiO₂, 0.167 bar) |
| Effect of UV on Rh/TiO₂-NiO | 1.798 bar in the dark, 2.095 bar under UV (+17%) |
| 150 mL photoreactor, 120 min, UV | 73.6% hydrazine conversion, 127 mL of gas (H₂ + N₂) collected |
| Irradiance sweep (model) | The minimum hydrazine concentration stops falling at the experimental irradiance: 2.98 M at both 13,918 and 15,000 W m⁻² sr⁻¹ |

## Why this problem

Hydrous hydrazine (N₂H₄·H₂O) holds a lot of hydrogen and produces no carbon-containing products, so it is studied as a chemical hydrogen carrier. Rh on TiO₂ is very active, and UV light can add a photocatalytic contribution on top of the thermal one.

In a stirred photoreactor, three things decide performance together: how the flow distributes the catalyst, how far light penetrates the suspension, and the reaction kinetics. The literature review in the thesis found no model that combined all three for hydrazine decomposition over Rh/TiO₂-P25 in a stirred batch reactor, so that is what I set out to build.

## Experiments

- **Catalyst:** 0.5 wt% Rh on TiO₂-P25 by wet impregnation (RhCl₃), dried at 80 °C, then reduced in H₂ at 400 °C.
- **Reactor 1, 18 mL sealed flask:** magnetic stirrer at 1400 RPM, 150 µL of 3.3 M hydrous hydrazine in 5 mL water. Gas evolution from the headspace pressure (ideal gas law). Dark runs in a heated oil bath, UV runs with an external lamp.
- **Reactor 2, 150 mL cylindrical photoreactor:** UV lamp submerged on the axis, water-cooled. Hydrazine followed every 30 min by UV-vis (DMAB colorimetric method), total gas volume by water displacement.
- **Screening:** four catalysts, three TiO₂ phases (anatase, rutile, P25), stirring rate (250 to 1000 RPM) and catalyst loading (1:8 to 1:40).

## Model

A 2D cross-section of each reactor in COMSOL Multiphysics 5.5, with three physics solved in sequence:

1. **Flow:** k-ε RANS turbulence with the frozen-rotor approach for the stirrer. Gives the velocity field and turbulent viscosity.
2. **Radiation:** P1 approximation in participating media. Gives the local volumetric rate of photon absorption (LVREA).
3. **Species transport:** convection-diffusion-reaction with power-law kinetics (order 0.33 in hydrazine, 1 in catalyst), Arrhenius temperature dependence and a photocatalytic term proportional to the LVREA.

**Mesh independence:** four refinement levels, peak velocity 0.4358, 0.4748, 0.4897 and 0.4896 m/s from Normal to Extra Fine. The Finer mesh was used for all runs.

## What the model showed

- **Dark:** the concentration field is radially symmetric and the light term is zero everywhere, as it should be. I used this as a consistency check.
- **18 mL flask with a quarter-arc UV boundary:** consumption is confined to the lit sector (minimum 2.98 M after 75 min, from 3.3 M), and hydrogen builds up in the same place, consistent with the stoichiometry.
- **150 mL reactor:** consumption forms a ring around the lamp, and the outer region barely reacts.
- **Irradiance sweep (5,000, 10,000, 13,918 and 15,000 W m⁻² sr⁻¹):** the minimum hydrazine concentration drops from 3.08 M to 2.98 M, then does not improve at 15,000.

## Takeaway

Past a point, more light does not help. The model suggests the limit is how well charge carriers reach the Rh sites, and that most of the reactor volume gets little or no UV. Gains should come from better charge separation (for example heterojunction supports like TiO₂-NiO, or better Rh dispersion) and from a different lighting geometry, not from a stronger lamp.

It is the kind of finding I like most: find the real constraint before adding capacity.

## Limits and what is not done

- **2D model with a frozen rotor.** It neglects axial effects such as catalyst settling and does not capture transient stirrer dynamics.
- **Optical coefficients come from the literature**, not from measurements on these catalysts.
- **Catalyst characterization (XRD, TEM, DRS UV-vis) was not complete** when the thesis was written, so its properties are discussed from the literature on similar catalysts.
- **No UV run with Rh/TiO₂-P25 in the 18 mL reactor.** The UV picture there comes from the model, compared against the dark experiments.
- **Quantitative validation of the model against the UV-vis concentration data is still to do.** The agreement so far is qualitative: where the consumption zone is and how the fields look in each geometry.

Next steps in the thesis: a 3D model, a transient stirrer model, measured optical properties, and the quantitative validation.

## Credits

The model builds on earlier CFD work of the supervising group (Adamou et al., 2024 and 2025). The thesis acknowledges doctoral researcher Panagiota Adamou for help with the computational stages.

## Tools

COMSOL Multiphysics 5.5 (Turbulent Flow k-ε, Radiation in Participating Media, Transport of Diluted Species) · catalyst synthesis (wet impregnation, H₂ reduction) · UV-vis spectrophotometry · pressure-based gas monitoring

Full thesis available on request: [LinkedIn](https://www.linkedin.com/in/charilaos-p-stavrou-648a25249)
