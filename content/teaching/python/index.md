---
title: Is it possible to measure spatial interference using only angular information? 
date: 2025-07-23
author: admin
tags: [mmWave, Interference, Massive MIMO, Angular Information, Beamforming]
categories: [Research, Wireless Communication]
draft: false
summary: Learn how angular information can be used to estimate inter-user interference in mmWave massive MIMO systems without full channel state information.
---

## Introduction

The MIMO (Multiple Input Multiple Output) technology uses multiple antennas at both the transmitter and receiver to send and receive several signals at the same time over the same radio channel. This wireless technology can exploit the beamforming gain, the spatial multiplexity and diversity gains to improve the reliability of data reception and increase the spectral efficiency. To meet the ever-increasing of data traffic and the future demands, Thomas Marzetta  has shown the efficiency of implementing a large number of transmit antennas, M ≫ 1, to serve  a finite number of users, K, at the same time-frequency resources. This design is commonly referred to as massive MIMO or large-scale antenna arrays.

In the 3GPP standards, it first appeared in LTE (Release 8) with basic 2×2 MIMO, later growing to 4×4 and 8×8 with LTE-Advanced (Releases 10–12), along with features like carrier aggregation and coordinated multi-point (CoMP). Release 13 introduced Full-Dimension MIMO (FD-MIMO) with 3D beamforming, paving the way for Massive MIMO. The real breakthrough came with 5G NR (Release 15), where large antenna arrays, beamforming, and support for both sub-6 GHz and mmWave made MIMO central to 5G performance. Newer releases (16–18, 5G-Advanced) refine this further with smarter beam management, better feedback, and multi-point transmission, making MIMO one of the core technologies driving today’s mobile networks. 

MIMO systems often face strong inter-user interference, which is usually managed with precoding or beamforming. These methods rely on full channel state information (CSI) at the base station, but with many antennas, obtaining full CSI is impractical. In mmWave systems, this challenge is eased because the channels are highly directional and very sensitive to blockages—so non-line-of-sight paths are weak compared to the line-of-sight link. This means a user’s spatial position (angle and distance from the base station) can effectively describe the channel. 

The objective is to define angle-based interference metric that could reflects the spatial interference between the users using only their direction angles. This metric could be implemented to cluster the users with high interference together in the same groups. Note that some works utilize the angular distance for the clustering. However, this metric does not describe properly the inter-user interference. Indeed, the beamwidth is very dependent on the antennas’ number and the steering angle of the beam. 


---

## What is Spatial Inter-User Interference?

In a multi-user system, especially one relying on spatial multiplexing, **inter-user interference** refers to the **unintended leakage** of the signal meant for one user into the channel of another. This results from imperfect spatial separation between users when served simultaneously by the same base station.

For example, in mmWave systems, where multiple users are served using highly directional beams, the beam intended for user A may partially overlap with the direction of user B, causing **angular domain interference**.

---

## Why Focus on Angular Information?

Measuring interference traditionally requires **full channel state information (CSI)**, which is costly to obtain and maintain, especially in large antenna systems. Fortunately, **mmWave channels** are highly directional and **sparse in the angular domain**, meaning most of the energy is concentrated in a small number of directions.

This property allows us to **approximate or estimate interference levels** using only the **angular location of users**—without needing full CSI. This is a significant advantage in mmWave systems where acquiring and updating full CSI is both complex and resource-intensive.

---

## How to Measure Interference Using Angular Information

Here are several methods:

### 1. Angular Separation Metric

- Define the angular position of each user (e.g., angle-of-departure from the base station).
- Calculate the **angular difference** between users.
- If the separation is small, there is a higher risk of interference.

### 2. Beam Pattern Analysis

- Use the beamwidth and steering angle of the transmitter to model how much energy spills into other users' directions.
- The **power overlap** between two beams can serve as a proxy for spatial interference.

### 3. Interference Correlation Functions

- Use spatial correlation or array response functions to model how much energy from one user’s beam leaks into another’s path.
- For a uniform linear array (ULA), this can be modeled using **sinc functions** of angular differences.

---

## Application in mmWave Massive MIMO

In **mmWave massive MIMO**, where the base station uses hundreds of antennas, the angular domain becomes a natural framework for analyzing spatial interference:

- **Low-rank channels** in mmWave enable the use of angular metrics instead of full channel matrices.
- **Beamforming algorithms** (e.g., angle-domain digital or hybrid precoding) rely on angular separation to serve users simultaneously.
- Clustering users based on angular compatibility can **reduce inter-user interference**.

---

## A Simple Angular Interference Metric

Here’s a simplified example:

If two users have estimated angles θ₁ and θ₂, the interference metric \( \mathcal{I}(\theta_1, \theta_2) \) can be defined as:


Where `a(θ)` is the array response vector at angle θ. A value close to 1 indicates high spatial overlap (more interference), while a value near 0 suggests minimal interference.

---

## Conclusion

Measuring spatial inter-user interference using only angular information is not only feasible but also practical in mmWave and massive MIMO systems. By leveraging angular sparsity, we can estimate interference, cluster users, and optimize beamforming—all without requiring full CSI.

This angular-based analysis is a powerful tool for designing next-generation wireless networks that are more efficient, scalable, and interference-aware.


![Angular interference illustration](/uploads/featured.jpg)

Feel free to refer to my article and/ or chapter 4 of phd manuscript for more details ! 
---
