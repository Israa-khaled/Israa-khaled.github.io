---
title: Is it possible to measure spatial interference using only angular information? 
date: 2025-07-23
author: admin
tags: [mmWave, Interference, Massive MIMO, Angular Information, Beamforming]
categories: [Research, Wireless Communication]
draft: false
summary: Learn how angular information can be used to estimate inter-user interference in mmWave massive MIMO systems without full channel state information.
---

## MIMO and 3GPP Standards

The MIMO (Multiple Input Multiple Output) technology uses multiple antennas at both the transmitter and receiver to send and receive several signals at the same time over the same radio channel. This wireless technology can exploit the beamforming gain, the spatial multiplexity, and diversity gains to increase spectral efficiency and reliability. To meet the ever-increasing data traffic and future demands, Thomas Marzetta has shown the efficiency of implementing a large number of transmit antennas, to serve a finite number of users, at the same time-frequency resources. This design is commonly referred to as massive MIMO or large-scale antenna arrays.

In the 3GPP standards, MIMO first appeared in LTE (Release 8) with basic 2×2 MIMO, later growing to 4×4 and 8×8 with LTE-Advanced (Releases 10–12), along with features like carrier aggregation and coordinated multi-point (CoMP). Release 13 introduced Full-Dimension MIMO (FD-MIMO) with 3D beamforming, paving the way for Massive MIMO. The real breakthrough came with 5G NR (Release 15), where large antenna arrays, beamforming, and support for both sub-6 GHz and mmWave made MIMO central to 5G performance. Newer releases (16–18, 5G-Advanced) refine this further with smarter beam management, better feedback, and multi-point transmission, making MIMO one of the core technologies driving today’s mobile networks.

## Inter-User Interference in MIMO

MIMO systems often experience **inter-user interference**, typically managed through precoding or beamforming. These techniques require full **channel state information (CSI)** at the base station, but acquiring full CSI becomes impractical as antenna counts increase. In mmWave systems, this challenge is mitigated because channels are highly directional and line-of-sight (LOS) paths dominate, while non-LOS paths are weak. This allows a user’s spatial position (angle and distance from the base station) to effectively characterize the channel.

The goal is to define an **angle-based interference metric** that quantifies spatial interference between users using only their directional angles. This metric can help cluster users likely to interfere with one another. Previous approaches relying solely on angular distance fail to capture true interference, as beamwidth depends on the number of antennas and the beam steering angle.

During my PhD thesis, I defined the **normalized inter-user spatial interference metric** {{< math >}}$ \beta_{k,u} ${{< /math >}} in highly directional mmWave environments as:  

{{< math >}}
$ \beta_{k,u} \stackrel{\text{def}}{=} \frac{1}{M}|\mathbf{a}^H_{1,k}\mathbf{a}_{1,u}|, \quad k,u \in \mathcal{K}, $
{{< /math >}}

where {{< math >}}$ \mathbf{a}_{1,u} ${{< /math >}} is the array steering vector pointing toward UE {{< math >}}$ u ${{< /math >}} spatial direction {{< math >}}$ \vec{\Theta}_{1,u} ${{< /math >}}, and {{< math >}}$ \mathbf{a}^H_{1,k} ${{< /math >}} corresponds to the LoS path of UE {{< math >}}$ k ${{< /math >}}.

For a {{< math >}}$M_x \times M_z${{< /math >}} uniform rectangular array (URA), {{< math >}}$ \beta_{k,u} ${{< /math >}} can be expressed as:  

{{< math >}}
\[
\begin{aligned}
\beta_{k,u} &= \frac{1}{M}\left| \sum_{m_z=1}^{M_z}\sum_{m_x=1}^{M_x} 
e^{j\left\{ (m_x-1)(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k})) + (m_z-1)(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k})) \right\}} \right| \\
&= \left| \frac{\sin\big(M_z(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k}))\big)}{M_z \sin(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k}))} \right| 
\left| \frac{\sin\big(M_x(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k}))\big)}{M_x \sin(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k}))} \right|
\end{aligned}
\]
{{< /math >}}

This metric is symmetric and bounded: {{< math >}}$ \beta_{k,u} = \beta_{u,k} \in (0,1) ${{< /math >}}, and can also be written as {{< math >}}$ \beta_{k,u} = |AF_{(\vec{\Theta}_{1,u})}(\vec{\Theta}_{1,k})| ${{< /math >}}. For a uniform linear array (ULA) along the {{< math >}}$ x ${{< /math >}}-axis, it simplifies to {{< math >}}$ AF_{(\theta_{1,u})}(\theta) ${{< /math >}}.

![Normalized array factor](/uploads/pattern_beta.jpg)  

During my work, I found that the $\beta_{k,u}$ metric is crucial for estimating inter-user interference using only the spatial directions $\vec{\Theta}_{1,k}$. This metric accounts for both the angular distance and the beamwidth, which depend on the steering angle and the number of antennas. Based on this metric, I developed user clustering algorithms for scenarios where the base station applies either digital or hybrid beamforming using only the estimated spatial directions. 

## For more details, please refer to my IEEE Access 2021 paper and Chapter 4 of my PhD thesis.
