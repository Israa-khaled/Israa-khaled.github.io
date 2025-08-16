---
title: Is it possible to measure spatial interference using only angular information? 
date: 2025-07-23
author: admin
tags: [mmWave, Interference, Massive MIMO, Angular Information, Beamforming]
categories: [Research, Wireless Communication]
draft: false
summary: Learn how angular information can be used to estimate inter-user interference in mmWave massive MIMO systems without full channel state information.
---

# MIMO and 3GPP Standards

The MIMO (Multiple Input Multiple Output) technology uses multiple antennas at both the transmitter and receiver to send and receive several signals at the same time over the same radio channel. This wireless technology can exploit the beamforming gain, the spatial multiplexity, and diversity gains to improve the reliability of data reception and increase the spectral efficiency. To meet the ever-increasing data traffic and future demands, Thomas Marzetta has shown the efficiency of implementing a large number of transmit antennas, \( M \gg 1 \), to serve a finite number of users, \( K \), at the same time-frequency resources. This design is commonly referred to as massive MIMO or large-scale antenna arrays.

In the 3GPP standards, MIMO first appeared in LTE (Release 8) with basic 2×2 MIMO, later growing to 4×4 and 8×8 with LTE-Advanced (Releases 10–12), along with features like carrier aggregation and coordinated multi-point (CoMP). Release 13 introduced Full-Dimension MIMO (FD-MIMO) with 3D beamforming, paving the way for Massive MIMO. The real breakthrough came with 5G NR (Release 15), where large antenna arrays, beamforming, and support for both sub-6 GHz and mmWave made MIMO central to 5G performance. Newer releases (16–18, 5G-Advanced) refine this further with smarter beam management, better feedback, and multi-point transmission, making MIMO one of the core technologies driving today’s mobile networks.

## Inter-User Interference in MIMO

MIMO systems often face strong inter-user interference, which is usually managed with precoding or beamforming. These methods rely on full channel state information (CSI) at the base station, but with many antennas, obtaining full CSI is impractical. In mmWave systems, this challenge is eased because the channels are highly directional and very sensitive to blockages—so non-line-of-sight paths are weak compared to the line-of-sight link. This means a user’s spatial position (angle and distance from the base station) can effectively describe the channel.

The objective is to define an angle-based interference metric that reflects the spatial interference between users using only their direction angles. This metric could be used to cluster users with high interference into the same groups. Some works utilize angular distance for clustering; however, this does not properly describe inter-user interference because beamwidth depends on the number of antennas and the steering angle of the beam.

We define the normalized inter-user spatial interference metric \( \beta_{k,u} \) in a mono-path environment as follows:

\[
\beta_{k,u}\stackrel{\text{def}}{=} \frac{1}{M}|\mathbf{a}^H_{1,k}\mathbf{a}_{1,u}|, \quad k,u \in \mathcal{K},
\]

where \( \mathbf{a}_{1,u} \) is the array steering vector of the beam generated toward UE \( u \) spatial direction, i.e., \( \vec{\Theta}_{1,u} \), and \( \mathbf{a}^H_{1,k} \) is the array steering vector of the LoS path in UE \( k \) channel. Thus, \( \beta_{k,u} \) is the normalized spatial interference of the beam generated toward UE \( u \) with the LoS path in UE \( k \) channel.

Using a \( M_x\times M_z\)-URA array, the spatial interference \( \beta_{k,u} \) can be rewritten as:

\[
\begin{aligned}
\beta_{k,u} & = \frac{1}{M}\left| \sum_{m_z=1}^{M_z}\sum_{m_x=1}^{M_x} e^{j\left\{ (m_x-1)(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k})) + (m_z-1)(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k})) \right\}} \right| \\
& = \left| \frac{\sin(M_z(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k}))}{M_z \sin(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k}))} \right| 
\left| \frac{\sin(M_x(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k}))}{M_x \sin(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k}))} \right|
\end{aligned}
\]

\( \beta_{k,u} \) only depends on the spatial directions \( \vec{\Theta}_{1,k} \) and \( \vec{\Theta}_{1,u} \). According to the equation above, \( \beta_{k,u} = \beta_{u,k} \in (0,1) \), and represents the normalized array factor \( AF_{(\vec{\Theta}_{1,u})}(\vec{\Theta}) \) of the beam pointed at \( \vec{\Theta}_{1,u} \) for \( \vec{\Theta} = \vec{\Theta}_{1,k} \):

\[
\beta_{k,u} = |AF_{(\vec{\Theta}_{1,u})}(\vec{\Theta}_{1,k})|.
\]

For a ULA along the \( x \)-axis, this simplifies to \( AF_{(\theta_{1,u})}(\theta) \).

![Normalized array factor](/uploads/featured.jpg)
*Illustration of the normalized array factor \( AF_{(\theta_{1,u})}(\theta) \) of the beam pointed toward UE \( u \) and the value for UE \( k \).*

Thus, \( \beta \) is an important metric to determine inter-user spatial interference using only the users’ spatial directions \( \vec{\Theta}_{1,k} \). We define an interference threshold \( \beta_0 \), such that \( \beta_{k,u} \ge \beta_0 \) indicates the LoS path of UE \( k \) lies in the UE \( u \) beam. The \( \beta_0 \)-beamwidth \( \Omega_u^{\beta_0} \) defines the angular distance satisfying \( |AF_{(\vec{\Theta}_{1,u})}(\vec{\Theta}_0)| = \beta_0 \).

### Lemma 1

UE \( k \), having \( \beta_{k,u} \ge \beta_0 \), is located in the \( \beta_0 \)-width of the main lobe of the UE \( u \) beam, only if \( \beta_0 > 0.217 \).

**Proof:**  
With \( d = \frac{\lambda}{2} \), a single main lobe exists in \( (0, \pi) \), surrounded by side lobes [Visser, 2005]. \( \beta_{k,u} \ge \beta_0 \) ensures UE \( k \) belongs to \( \Omega_u^{\beta_0} \). To select only users covered by the main lobe, \( \beta_0 \) must exceed the first side lobe level \( \beta^{\text{FSL}} = 0.217 \).

![First side lobe](/uploads/featured.jpg)
*Normalized array factor of the beam generated toward UE \( u \) for \( \theta_{1,u} \in \{50^\circ, 110^\circ\}, M = 32$.*

This metric will be used in the UC algorithm described in Section \ref{sec:userclustering}, and the threshold value 0.217 will be confirmed in simulations (Section \ref{sec:DBF_NOMA_simres}).



![Angular interference illustration](/uploads/featured.jpg)

Feel free to refer to my article and/ or chapter 4 of phd manuscript for more details ! 
---
