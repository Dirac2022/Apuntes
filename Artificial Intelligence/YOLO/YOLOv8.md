
# Plan
1. **Convolutional Architectures**
2. **Feature Pyramid Networks (FPN)**
3. **Path Aggregation Network (PANet)**
4. **Residual Blocks**
5. **CSPNet (Cross Stage Partial Networks)**
6. **Darknet53 and CSPDarknet53**
7. **How it All Fits Together in YOLOv8**


# 1. Convolutional Architectures

[[CNN (Convolutional Neural Networks)|CNN]]
![](https://miro.medium.com/v2/resize:fit:1100/format:webp/0*1lgnoaKSwxyKlEl6)

# 2. Feature Pyramid Networks (FPN)
The **Feature Pyramid Network (FPN)** is an architecture designed to ==enhance object detection and image segmentation performance==. It leverages outputs from various convolutional layers to create a pyramid representation of features, allowing for better detection objects at different scales.

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*geMPKTA65dBfAe5h-YfXQg.png)
*Diagram illustrating the architecture of a Feature Pyramid Network (FPN) for multi-scale object detection*
[[1612.03144] Feature Pyramid Networks for Object Detection](https://arxiv.org/abs/1612.03144)

As we progress though the layers of a convolutional network, deeper layers tend to capture fine details, such as small objects, while earlier layers focus on patterns, shapes, and edges of larger objects. The goal of FPN is to use not only the output from the final convolutional layer but also outputs from several intermediate layers to detect objects at multiple scales. This multiscale detection capability is key to FPN's effectiveness.

# 3. Path Aggregation Network (PANet)
In **Path Aggregation Network (PANet)** is an improvement over the **Feature Pyramid Network (FPN)** architecture. PANet strengthens the connections between different feature scales and introduces additional mechanism for better information aggregation.

To better understand the difference
**Continuar**
[YOLOv8 Explained: Understanding Object Detection from Scratch | by Mélissa Colin | Medium](https://medium.com/@melissa.colin/yolov8-explained-understanding-object-detection-from-scratch-763479652312)
