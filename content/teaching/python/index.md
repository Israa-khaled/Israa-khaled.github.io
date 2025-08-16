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

The MIMO (Multiple Input Multiple Output) technology uses multiple antennas at both the transmitter and receiver to send and receive several signals at the same time over the same radio channel. This wireless technology can exploit the beamforming gain, the spatial multiplexity, and diversity gains to improve the reliability of data reception and increase the spectral efficiency. To meet the ever-increasing data traffic and future demands, Thomas Marzetta has shown the efficiency of implementing a large number of transmit antennas, to serve a finite number of users, at the same time-frequency resources. This design is commonly referred to as massive MIMO or large-scale antenna arrays.

In the 3GPP standards, MIMO first appeared in LTE (Release 8) with basic 2×2 MIMO, later growing to 4×4 and 8×8 with LTE-Advanced (Releases 10–12), along with features like carrier aggregation and coordinated multi-point (CoMP). Release 13 introduced Full-Dimension MIMO (FD-MIMO) with 3D beamforming, paving the way for Massive MIMO. The real breakthrough came with 5G NR (Release 15), where large antenna arrays, beamforming, and support for both sub-6 GHz and mmWave made MIMO central to 5G performance. Newer releases (16–18, 5G-Advanced) refine this further with smarter beam management, better feedback, and multi-point transmission, making MIMO one of the core technologies driving today’s mobile networks.

## Inter-User Interference in MIMO

MIMO systems often face strong inter-user interference, which is usually managed with precoding or beamforming. These methods rely on full channel state information (CSI) at the base station, but with many antennas, obtaining full CSI is impractical. In mmWave systems, this challenge is eased because the channels are highly directional and very sensitive to blockages—so non-line-of-sight paths are weak compared to the line-of-sight link. This means a user’s spatial position (angle and distance from the base station) can effectively describe the channel.

The objective is to define an angle-based interference metric that reflects the spatial interference between users using only their direction angles. This metric could be used to cluster users with high interference into the same groups. Some works utilize angular distance for clustering; however, this does not properly describe inter-user interference because beamwidth depends on the number of antennas and the steering angle of the beam.

We define the normalized inter-user spatial interference metric {{< math >}}$ \beta_{k,u} $ {{< /math >}} in highly directional mmWave environmnt as follows:

{{< math >}}
$$
\beta_{k,u}\stackrel{\text{def}}{=} \frac{1}{M}|\mathbf{a}^H_{1,k}\mathbf{a}_{1,u}|, \quad k,u \in \mathcal{K},
$$
{{< /math >}}

{{< math >}}$ \mathbf{a}_{1,u} ${{< /math >}} is the array steering vector of the beam generated toward UE {{< math >}}$ u ${{< /math >}} spatial direction, i.e., {{< math >}}$ \vec{\Theta}_{1,u} ${{< /math >}}, and {{< math >}}$ \mathbf{a}^H_{1,k} ${{< /math >}} is the array steering vector of the LoS path in UE {{< math >}}$ k ${{< /math >}} channel.

Using a {{< math >}}$ M_x\times M_z $ {{< /math >}} URA array, the spatial interference {{< math >}}$ \beta_{k,u} $ {{< /math >}} can be rewritten as:

{{< math >}}
$$
\begin{aligned}
\beta_{k,u} &= \frac{1}{M}\left| \sum_{m_z=1}^{M_z}\sum_{m_x=1}^{M_x} 
e^{j\left\{ (m_x-1)(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k})) + (m_z-1)(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k})) \right\}} \right| \\
&= \left| \frac{\sin\big(M_z(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k}))\big)}{M_z \sin(\omega_z(\vec{\Theta}_{1,u})-\omega_z(\vec{\Theta}_{1,k}))} \right| 
\left| \frac{\sin\big(M_x(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k}))\big)}{M_x \sin(\omega_x(\vec{\Theta}_{1,u})-\omega_x(\vec{\Theta}_{1,k}))} \right|
\end{aligned}
$$
{{< /math >}}

{{< math >}}
$$
\beta_{k,u} = \beta_{u,k} \in (0,1), \quad \beta_{k,u} = |AF_{(\vec{\Theta}_{1,u})}(\vec{\Theta}_{1,k})|
$$
{{< /math >}}

For a ULA along the {{< math >}}$$ x $$ {{< /math >}}-axis, this simplifies to {{< math >}}$$ AF_{(\theta_{1,u})}(\theta) $$ {{< /math >}}.

![Normalized array factor](/uploads/pattern_beta.jpg)  
*Illustration of the normalized array factor {{< math >}}$$ AF_{(\theta_{1,u})}(\theta) $$ {{< /math >}} of the beam pointed toward UE {{< math >}}$$ u $$ {{< /math >}} and the value for UE {{< math >}}$$ k $$ {{< /math >}}.*

Thus, {{< math >}}$$ \beta $$ {{< /math >}} is an important metric to determine inter-user spatial interference using only the users’ spatial directions {{< math >}}$$ \vec{\Theta}_{1,k} $$ {{< /math >}}. We define an interference threshold {{< math >}}$$ \beta_0 $$ {{< /math >}}, such that {{< math >}}$$ \beta_{k,u} \ge \beta_0 $$ {{< /math >}} indicates the LoS path of UE {{< math >}}$$ k $$ {{< /math >}} lies in the UE {{< math >}}$$ u $$ {{< /math >}} beam. The {{< math >}}$$ \beta_0 $$ {{< /math >}}-beamwidth {{< math >}}$$ \Omega_u^{\beta_0} $$ {{< /math >}} defines the angular distance satisfying {{< math >}}$$ |AF_{(\vec{\Theta}_{1,u})}(\vec{\Theta}_0)| = \beta_0 $$ {{< /math >}}.

### Lemma 1

UE {{< math >}}$$ k $$ {{< /math >}}, having {{< math >}}$$ \beta_{k,u} \ge \beta_0 $$ {{< /math >}}, is located in the {{< math >}}$$ \beta_0 $$ {{< /math >}}-width of the main lobe of the UE {{< math >}}$$ u $$ {{< /math >}} beam, only if {{< math >}}$$ \beta_0 > 0.217 $$ {{< /math >}}.

**Proof:**  
With {{< math >}}$$ d = \frac{\lambda}{2} $$ {{< /math >}}, a single main lobe exists in {{< math >}}$$ (0, \pi) $$ {{< /math >}}, surrounded by side lobes [Visser, 2005]. {{< math >}}$$ \beta_{k,u} \ge \beta_0 $$ {{< /math >}} ensures UE {{< math >}}$$ k $$ {{< /math >}} belongs to {{< math >}}$$ \Omega_u^{\beta_0} $$ {{< /math >}}. To select only users covered by the main lobe, {{< math >}}$$ \beta_0 $$ {{< /math >}} must exceed the first side lobe level {{< math >}}$$ \beta^{\text{FSL}} = 0.217 $$ {{< /math >}}.

![First side lobe](/uploads/pattern_beta.jpg)  
*Normalized array factor of the beam generated toward UE {{< math >}}$$ u $$ {{< /math >}} for {{< math >}}$$ \theta_{1,u} \in \{50^\circ, 110^\circ\}, M = 16 $$ {{< /math >}}.*



![Angular interference illustration](/uploads/featured.jpg)

Feel free to refer to my article and/ or chapter 4 of phd manuscript for more details ! 
---
