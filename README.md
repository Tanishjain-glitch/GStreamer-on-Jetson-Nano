# GStreamer-on-Jetson-

# 🚀 GStreamer on Jetson Nano: Real-Time Camera Streaming with Hardware Acceleration

## Why GStreamer on Jetson Nano?

GStreamer enables real-time, hardware-accelerated video pipelines on NVIDIA Jetson Nano—ideal for AI, computer vision, or robotics at the edge. With NVIDIA’s GPU plugins (like `nvv4l2decoder` and `nvarguscamerasrc`), you can capture, decode, and process video streams efficiently in Python or C++.

---

## 🌟 TL;DR

Want to stream, decode, or process video on Jetson Nano using its GPU?  
This repo gives you:
- A robust, ready-to-run GStreamer+OpenCV RTSP pipeline
- Explanation of Jetson-accelerated plugins
- Troubleshooting steps for common Nano video issues
- Example output and key resource links

---

## 🧐 What’s Inside?

- Minimal Python example:  
  RTSP IP camera ➔ accelerated decode ➔ OpenCV frame access
- Jetson-specific GStreamer elements explained
- Screenshot of real output on Jetson Nano
- Links to official docs & troubleshooting tips

---

## 🔥 Quickstart

1. **Clone this repo**
    ```
    git clone https://github.com/<youruser>/jetson-gstreamer-rtsp-opencv.git
    cd jetson-gstreamer-rtsp-opencv
    ```

2. **Install dependencies**
    - OpenCV with GStreamer (check with `python3 -c "import cv2; print(cv2.getBuildInformation())"`)
    - GStreamer plugins:
      ```
      sudo apt-get install python3-opencv gstreamer1.0-tools gstreamer1.0-plugins-{good,bad,ugly} gstreamer1.0-libav
      ```

3. **Set your RTSP camera URL** in `rtsp_gst_opencv.py`:
    ```
    RTSP_URL = "rtsp://username:password@<camera-ip>/stream1"
    ```

4. **Run the script:**
    ```
    python3 rtsp_gst_opencv.py
    ```

---

## 📷 Example Output

Running the pipeline displays periodic logs and opens the camera stream.  
Sample screenshot below confirms hardware decoding and real-time streaming:

![Sample output: Jetson Nano hardware-accelerated RTSP stream]("https://drive.google.com/file/d/1IadntjC9QQ52tQba8-c5ZGKbNP-3Hu3J/view?usp=sharing")

*Output of the Jetson Nano GStreamer pipeline decoding an RTSP stream in hardware (see timestamp on monitor in the video feed).*

---

## 🛠️ Troubleshooting & Tips

- **`Failed to open RTSP via GStreamer.`**
    - Confirm GStreamer plugins are present (`gst-inspect-1.0 nvv4l2decoder`)
    - Make sure OpenCV is built with GStreamer enabled
    - Test parts of your pipeline with `gst-launch-1.0` to isolate problems
- For best performance, use NVIDIA-accelerated elements: `nvv4l2decoder`, `nvarguscamerasrc`, `nvvidconv`, `nveglglessink`.
- Capabilities/caps errors? Make sure each pipeline element is compatible; use explicit `video/x-raw` caps as shown in the code.

---

## 🏃 Key GStreamer Commands

- **Prototype a camera/decode pipeline:**
    ```
    gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM),width=1280,height=720,framerate=30/1' ! nvoverlaysink -e
    ```
- **Inspect plugins (does Jetson acceleration work?):**
    ```
    gst-inspect-1.0 nvv4l2decoder
    ```
- **Debug pipeline issues:**
    ```
    GST_DEBUG="*:3" gst-launch-1.0 videotestsrc ! autovideosink
    ```

---

## 📚 Resources

- [GStreamer Basic Tutorials](https://gstreamer.freedesktop.org/documentation/tutorials/basic/index.html)
- [GStreamer Application Development Basics](https://gstreamer.freedesktop.org/documentation/application-development/introduction/basics.html)
- [gst-launch-1.0 Manual](https://gstreamer.freedesktop.org/documentation/tools/gst-launch.html)
- [gst-inspect-1.0 Manual](https://gstreamer.freedesktop.org/documentation/tools/gst-inspect.html)
- [NVIDIA Accelerated GStreamer for Jetson](https://docs.nvidia.com/jetson/archives/r34.1/DeveloperGuide/text/SD/Multimedia/AcceleratedGstreamer.html)
- [Enabling OpenCV+GStreamer on Jetson](https://forums.developer.nvidia.com/t/how-to-install-opencv-with-gstreamer-capabilities/108774)
- [Community Issue: Missing nvv4l2decoder Plugin](https://github.com/dusty-nv/jetson-inference/issues/1727)

---

## ✍️ Authors

Tanish Jain

---

## 📜 License

MIT license

