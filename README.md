# Marketing Mix Modeling (MMM) Mathematical Framework

## Overview

This document outlines a mathematical model that is firstmost a work in progress. The purpose of this work is to demonstrate a sophisticated Marketing Mix Modeling (MMM) system that I've developed. My method leverages granular data at a sub-daily level, incorporates linear regression techniques, and explicitly accounts for historical predictions, seasonality, and overlap among channels. Fast Fourier Transforms attempt to harmonize/deharmonize poor predictions and keep what I'm referring to as the *'system'* stable.

> [!CAUTION]
> This is not proven, nor validated.
> This is primarily built to support brand awareness and reach efficacy
---

## Core Predictive Model

The primary regression model I've established is:

$$
 y_i \approx \sum_{z=1}^{n} \beta_z(Q_{y_i}^{x})
$$

Where:
- $y_i$ represents the dependent variable (e.g., incremental reach, conversions, ROI) at observation $i$.
- $\beta_z$ are regression coefficients that I'm estimating.
- $Q_{y_i}^{x}$ is a carefully vectorized set of granular-level channel measurement metrics, such as reach, frequency, spend, efficiency, and overlap.

### Example
For example, observation $i$ might represent a specific ad placement on a particular day and hour:

$$
Q_{y_i}^{x} = [Reach_{Facebook,i}, Freq_{YouTube,i}, Spend_{Google,i}, Efficiency_{TikTok,i}, Overlap_{YT\cap FB,i}]
$$

Each element is a measurable data point collected in real-time or near-real-time granularity.

---

## Regression Structure (Vectorized Form)

Formally, I express this regression as:

$$
Y = X\beta + \epsilon
$$

Where:
- $Y$ is the vector of observed outcomes.
- $X$ is the matrix containing independent variables (channel metrics and derived variables).
- $\beta$ is the parameter vector I estimate.
- $\epsilon$ is the residual error vector, assumed normally distributed and independent.

### Example
A clear example of this matrix form is:

![equation](https://latex.codecogs.com/svg.image?%5Cbg%7Bwhite%7D%25%5Clarge%20%5Cbegin%7Bbmatrix%7D%20y_1%20%5C%5C%20y_2%20%5C%5C%20%5Cvdots%20%5C%5C%20y_m%20%5Cend%7Bbmatrix%7D%20=%20%5Cbegin%7Bbmatrix%7D%20Reach_%7B1%7D%20&%20Spend_%7B1%7D%20&%20Efficiency_%7B1%7D%20%5C%5C%20Reach_%7B2%7D%20&%20Spend_%7B2%7D%20&%20Efficiency_%7B2%7D%20%5C%5C%20%5Cvdots%20&%20%5Cvdots%20&%20%5Cvdots%20%5C%5C%20Reach_%7Bm%7D%20&%20Spend_%7Bm%7D%20&%20Efficiency_%7Bm%7D%20%5Cend%7Bbmatrix%7D%20%5Cbegin%7Bbmatrix%7D%20%5Cbeta_%7BReach%7D%20%5C%5C%20%5Cbeta_%7BSpend%7D%20%5C%5C%20%5Cbeta_%7BEfficiency%7D%20%5Cend%7Bbmatrix%7D%20+%20%5Cbegin%7Bbmatrix%7D%20%5Cepsilon_1%20%5C%5C%20%5Cepsilon_2%20%5C%5C%20%5Cvdots%20%5C%5C%20%5Cepsilon_m%20%5Cend%7Bbmatrix%7D)

---

## Channel Efficiency and Overlap Decomposition

When channels overlap, their combined effect might be nonlinear. I've introduced an overlap term $\Phi_{xy}$, using trigonometric decomposition for clear interpretation:

$$
E_{xy} = E_x + S_y \cdot \cos(\Phi_{xy}), \quad E_x + S_y \cdot \sin(\Phi_{xy})
$$

Where:
- $E_{xy}$ represents the combined efficiency or performance metric for channels $x$ and $y$.
- $E_x$ is the individual efficiency of channel $x$.
- $S_y$ is spend or intensity on channel $y$.
- $\Phi_{xy}$ quantifies measurable overlap between channels.

### Example
If a Facebook and YouTube campaign overlap significantly, I can empirically determine the overlap angle $\Phi_{YT,FB}$:

$$
Reach_{YT,FB} = Reach_{YT} + Spend_{FB} \cdot \cos(\Phi_{YT,FB})
$$

This explicitly accounts for channel interaction effects.

---

## Accounting for Predictions in Future Observations

Given that my predictions influence future marketing actions, it's crucial to include past predictions explicitly. To harmonize this recursive relationship, I've chosen to use Fourier transformations, ensuring smooth cyclical predictions and filtering out poor-quality forecasts:

$$
P_{harmonized} = \mathcal{F}^{-1}\left(\mathcal{F}(P_{past})\cdot\Gamma\right)
$$

Where:
- $\mathcal{F}$ is the Fourier transform.
- $P_{past}$ is the vector of previous predictions.
- $\Gamma$ is a frequency-space filter to eliminate anomalous past predictions.

### Example
Forthcoming exmaples. 

---


This framework I've built provides a robust foundation for sophisticated MMM, explicitly handling granular metrics, channel interactions, and predictive influences. Continued validation of overlap and harmonization methods will further refine and enhance predictive accuracy.

---

