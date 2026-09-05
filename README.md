# Stochastic Mathematical Medicine Framework: A Monte Carlo PK/PD Model

## Project Overview
This repository features an open-source computational medicine engine developed in Python to evaluate multi-dose pharmacokinetic drug accumulation across highly variable human populations. While typical pharmaceutical prescription strategies assume deterministic biology, this project utilizes **Stochastic Applied Mathematics** to profile risk thresholds under Gaussian genetic decay variance. 

## The Mathematics
The underlying architecture models human drug absorption and clearance metrics using an inter-compartmental continuous system of **Ordinary Differential Equations (ODEs)**. 

The mathematical rate of change between the stomach compartment ($S$) and the centralized bloodstream matrix ($B$) is governed by:

$$\frac{dS}{dt} = -k_a S$$

$$\frac{dB}{dt} = k_a S - k_e B$$

Where:
* $k_a$ represents the localized biological absorption rate constant.
* $k_e$ represents the structural renal clearance/elimination rate constant.

Because multi-variable calculus equations tracking continuous stacked impulses are analytically complex to resolve by hand, this framework utilizes **Euler's Numerical Method** to iteratively calculate state tracking variables over discrete time step increments ($dt = 0.01$ hours):

$$S_{t+1} = S_t + \left(\frac{dS}{dt} \cdot dt\right)$$
$$B_{t+1} = B_t + \left(\frac{dB}{dt} \cdot dt\right)$$

## Statistical Monte Carlo Architecture
To move past a single static patient profile, the engine wraps the core continuous calculus framework inside an outer **stochastic loop structure** simulating a cohort of 50 distinct individual trials simultaneously. 

Biological parameter distributions are randomly drawn utilizing a Gaussian normal distribution model via NumPy:
* $k_a \sim \mathcal{N}(\mu=1.2, \sigma=0.15)$
* $k_e \sim \mathcal{N}(\mu=0.15, \sigma=0.03)$

The multi-dimensional data array ($50 \times 2400$ metrics) is compressed through matrix axis operations to isolate cohort mean vectors, Standard Deviation boundaries ($\pm 1 \text{ STD}$ representing a 68% statistical confidence interval cloud), and localized algorithmic failure probability rates.

## Core Dependencies
* `numpy` - Multi-dimensional matrix calculations and vector optimization
* `matplotlib` - Scientific visualization coordinate charting
