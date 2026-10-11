# 1. Background & Motivation

[← Back to README](../README.md) · Next: [2. Hardware →](02_hardware.md)

> Summary of thesis chapters 1–2. Numbers in brackets refer to the [references](REFERENCES.md).

## Why VR for neurosurgical training?

Neurosurgery needs extreme precision, and small mistakes can have severe consequences. Traditional training has clear limits:

- **Cadaver dissection** doesn't reproduce live tissue: no realistic elasticity, no bleeding.
- **The apprenticeship model** depends on limited mentorship, restricted access to cadaver labs and inconsistent patient availability. The often-quoted goal is 10,000 hours of practice [1].
- **There aren't enough neurosurgeons**: in some low- and middle-income countries there is about one per million people [2].

**Virtual reality** offers a risk-free environment where trainees can repeat complex procedures as often as they like, with measurable performance feedback [3]:

- A meta-analysis of 14 studies found simulation-based training more effective than traditional apprenticeship [4].
- In a study with operating-room nurses, VR training raised confidence in recognising intra-operative bleeding from **42.9 % to 71.5 %** and in assisting during craniotomies from **57.2 % to 85.7 %** [12].
- VR lowers cognitive load and stress for novice surgeons [13], allows remote guidance (tele-proctoring) [14], and can simulate rare cases without limit [15].
- Commercial platforms already exist: **Dextroscope**, **NeuroTouch** (with haptic feedback), **ImmersiveTouch**, NeuroVR, Surgical Theater, Osso VR. Many of them lack thorough scientific validation [24–33].

## Why haptics and hand tracking matter

Without realistic touch feedback, VR surgical simulators feel less real and training assessments become less accurate [38].
A human hand has **21 degrees of freedom**: each finger has three joints (MCP, PIP, DIP) and the thumb has two [39]. A useful glove has to track these movements and push back on them.

### Types of force-feedback gloves [40]

| Type | Example | Strength | Weakness |
|---|---|---|---|
| **Ground-based** | HIRO III [41] | Strong force feedback | Mounted to a base, so little mobility |
| **Dorsal-based** | CyberGrasp, Sensor Glove II [42, 43] | Portable, wearable | Hard to simulate multi-directional forces |
| **Palm-based** | Rutgers Master II [44] | Simulates grip | Restricted motion |
| **Digit-based** | DESR [45] | Precise force between fingers | Complex |

Examples from research: rotary sensors at the MCP joints reach a 3.09° error at 4 ms latency [46]; McKibben-muscle gloves increase immersion [47]; MR-brake gloves cut task time by 79 % [48]; FBG strain sensors achieve a 1.63° error [49]; and the SenseGlove NOVA with Vive trackers has been used in a neurosurgery simulator [50].

### Shortcomings of commercial gloves

Commercial gloves (Manus VR, Senso, CaptoGlove, Noitom Hi5, VRfree, HaptX, SenseGlove Nova, …) mostly combine 9-DoF IMUs with flex sensors. Their shortcomings:

- **Expensive**, so hard to roll out widely
- Mostly **vibration only**: little real force feedback (Dexmo is an exception)
- Objects don't feel like real objects
- Often **not wireless**, which adds latency
- **Not designed to be assembled from a kit**

## The proposed system

The glove builds on the open-source **LucidGloves** design [58]: potentiometers, strings and 3D-printed parts track the fingers cheaply.
The original design needs an **HTC Vive tracker or Valve Index controller** for the hand's position and rotation, which adds cost and complexity.

**This thesis replaces that external tracker with an IMU** and compares two sensors:

| | MPU6050 | ICM20948 |
|---|---|---|
| Degrees of freedom | 6 (accel + gyro) | 9 (accel + gyro + magnetometer) |
| Question | Is a 6-DoF IMU enough? | Does the magnetometer improve tracking? |

IMUs suffer from **drift** and **gimbal lock**, so the thesis also builds and compares sensor-fusion algorithms to deal with both (see [chapter 3](03_sensor_fusion.md)).

---

[← Back to README](../README.md) · Next: [2. Hardware →](02_hardware.md)
