One of the key aspects of working with LiDAR is to understand how pointcloud data is stored, particularly in the LAS file format.

In this article, I will try my best to give a brief introduction on the structure of LAS files, their use and importance in LiDAR data processing applications.

## Why Understanding LAS Structure Matters

For the last of couple months, I have been working with a mining company and my main occupation was to construct a clean, precise mesh model from messy pointcloud inputs.

We were a fresh team back then and I assumed the leader role in the group. We were not sure where to start and how to proceed with the whole thing. Yet we had limited time and countless amounts of setups.

> "Haste makes waste."

One of the worst mistake I did at that time was asking my teammates to assume pointcloud data as a set of X, Y, Z coordinates to start developing immediately. 

I thought we could deal with the r"precision improvements" after we complete the core architecture.

These "minor details" that I overlooked back in the days cost me my entire semester break.


**Here are some special cases where you cannot assume:**

  - **(Example 1) Filtering :** You have the lidar scan of a 3D object. It obviously contains a lot of points from the object but there are also redundant points from the surrounding environment (Noise). What method would you use to seperate them ?

  - **(Example 2) 3D Mapping :** You have the lidar scan of a landscape and you want to create a scaled map. How do you calculate the exact distance between two points?

  - **(Example 3) Mobile Observer :** You have a lidar scan captured by a drone. What if the points you are dealing with are overlapped ?

Understanding the structure of LAS files is crucial for working with LiDAR data especially while working on precise calculations.

## Big Picture

A LAS file consists of several components that organize and store LiDAR data. These components allow standardization across different hardware and software tools.

I think we can examine the .las file under two main sections:

  - Metadata
  - Point Records


### A. Metadata

#### 1. File Header

The file header contains essential metadata about the LAS file, including:

  - File Signature ('LASF' indicating LAS format)
  - System Identifier
  - Version Information (LAS 1.2, 1.3 etc.)
  - Header Size and Offset to Point Data
  - Number of Points
  - Point Format
  - Spatial Reference System (if available)

This section mostly acts as a roadmap for software applications. These selected fields in particular can be very useful for the ones who work with the raw thing.

#### 2. Variable-Length Records (VLRs)

Different LAS versions support different point formats but even the same versions may contain additional custom data. The fields of the LAS file that allow this custom data are VLRs.

These records often contain information such as:

  - Projection and coordinate system definitions
  - Sensor calibration information
  - Processing history or software-specific details

Each VLR consists of an identifier, description and data payload.

VLRs increment the file's usability for different needs since it provides context beyond the standard header fields.

### B. Point Data Records

The core of any LAS file is the point data records.

Each point represents a LiDAR return (Reflected pulse) and includes attributes such as:

  - **X, Y, Z Coordinates:** 3D spatial position of the point
  - **Intensity:** Strength of the return signal
  - **Return Number and Number of Returns:** Whether the point is a first, intermediate or last return
  - **Classification:** Type definition of object the point represents (ground, vegetation, buildings...)
  - **Scan Angle and Flight Line Information:** Stores data about the sensor position during capture
  - **RGB Values(if available):** Stores color information if provided

A point record that contains all the attributes listed above requires 24 bytes in total.
On the extreme case, size can reach up to 64 bytes.

After all this time, I’m still amazed by the allocated space for a single point.

There are millions of them !

(For comparison, coordinate values require 12 bytes in total.)



## LAS 1.3 Additional Features

At the time this article was written, LAS 1.4 was widely available already.
But my work focuses on version 1.2. So I want to mention the updates briefly:

#### Extended Variable-Length Records (EVLRs)

Similar to VLRs but are placed at the end of the file instead of in the header.
They are useful for storing large auxiliary data such as sensor-specific information.

#### Waveform Data Packets (LAS 1.3 and Later)

Waveform packets are used by LiDAR systems that capture full waveform data. These packets contain:

  - Digitized waveform samples
  - Associated timestamps and location

Waveform data allows for more detailed analysis of LiDAR returns.

Commonly used by **Airborne LiDAR systems** but **some advanced drone-based LiDAR sensors** also support it for high-resolution mapping applications.

## Conclusion

Whether processing large-scale airborne LiDAR scans or detailed terrestrial point clouds or constructing a mesh model from scratch... Knowledge of LAS file organization is essential for pointcloud manipulation and analysis. 

It takes the burden of finding "out of the box ideas" to scale a model or filter a messy input. The LAS file content provides the information you probably going to need in a standardized,  structured way already.

Thanks for reading !