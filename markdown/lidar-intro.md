LiDAR (Light Detection and Ranging) sensors work by emitting laser pulses toward a target and measuring the time it takes for the reflected pulses to return.

#### **Step-by-Step Process of LiDAR Scanning**

1. The scanning process begins in the environment.
2. The LiDAR sensor emits laser pulses toward a target object.
3. The pulses reflect off the object and return to the sensor.
4. The sensor calculates the time taken for the pulse to travel and determines the 3D coordinates of the point.
5. This process loops millions of times to collect all necessary points.
6. The sensor records and stores these points in a '.las' file.
7. Metadata ( timestamps, sensor position, scanning settings etc.) is added to the `.las` file.
8. The final `.las` file is outputted

![LIDAR Capturing Sequence Diagram](../images/blog/uml-sequence.png)

In the context of LAS files, LiDAR sensors capture multiple returns per pulse.

Each captured point is assigned attributes like X, Y, Z coordinates, intensity, classification and return number. 

All of which are needed for accurate digital representations of real objects.
 
---

### **LiDAR Sensors Types and Their Special Properties**

LiDAR sensors come in different types, each optimized for specific applications:

- **Airborne LiDAR** – Mounted on drones. Ideal for large-scale topographic mapping and flood modeling.
- **Terrestrial LiDAR** – Used on tripods or vehicles. Captures high resolution ground level scans.
- **Mobile LiDAR** – Typically mounted on moving vehicles. Allows rapid 3D mapping. (Usually for roads and railways)
- **Bathymetric LiDAR** – Uses green wavelength lasers which can penetrate water. Used to map underwater terrains and coastal regions.
- **Solid-State LiDAR** – A compact, mechanically simple alternative to traditional LiDAR. Used in EV's for real-time object detection.

Each type of LiDAR have their own advantages. The choice depends on the specific application. Key factors that influence the selection are usually the level of detail needed, the scale of the project and the minimum capture time.

Thank you for reading !