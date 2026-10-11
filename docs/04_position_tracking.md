# 4. Position Tracking with an IMU

[← 3. IMU sensor fusion](03_sensor_fusion.md) · [README](../README.md) · Next: [5. Evaluation →](05_evaluation.md)

> Summary of thesis chapter 6.

An IMU has no absolute position sensor. Position has to be **estimated from acceleration** in four steps:

```mermaid
flowchart LR
    A[Raw accelerometer] --> B["Remove gravity<br/>(using the fused orientation)"]
    B --> C["Integrate → velocity"]
    C --> D["Integrate → position"]
```

1. **Read** the raw accelerometer data. It contains both movement and gravity.
2. **Remove gravity**: rotate the gravity vector into the sensor frame with the current orientation and subtract it:

   $$a_{linear} = a_{measured} - g, \qquad g = (0,\ 0,\ 9.81\ \text{m/s}^2)$$

3. **Integrate to velocity**:

   $$v_t = v_{t-1} + a_{linear}\,\Delta t$$

4. **Integrate again to position**:

   $$p_t = p_{t-1} + v_t\,\Delta t$$

## Why it drifts

- **Double integration amplifies errors:** a small constant bias in acceleration grows linearly in velocity and **quadratically in position**.
- **Sensor noise and bias** in both the accelerometer and gyroscope; any orientation error also leaves part of gravity in $a_{linear}$.
- **No absolute reference:** the IMU only knows motion relative to where it started.

Techniques like **zero-velocity updates (ZUPT)** and bias estimation reduce the drift but don't remove it. For long-term accuracy, an external reference (optical tracking, visual odometry, …) is needed.
The measured position errors are in [chapter 5](05_evaluation.md#position-tracking).

---

[← 3. IMU sensor fusion](03_sensor_fusion.md) · [README](../README.md) · Next: [5. Evaluation →](05_evaluation.md)
