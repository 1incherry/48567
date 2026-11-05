# Secure FPGA Vision NPU with Qwen Interaction

This dual-FPGA prototype combines camera capture, lightweight object detection, fine-grained Vision Transformer (ViT) classification, and authenticated inference. The demonstration uses cat images to show how the system locates an object, classifies its breed, and retrieves earlier results.

[简体中文](README.md)

## Architecture

| Component | Role |
| --- | --- |
| Artix-7 (XC7A100T) | OV5640 camera capture, board-to-board image transfer, and Qwen interaction logic |
| Zynq-7000 (XC7Z035) | DDR buffering, vision and audio inference, authentication, and HDMI display |
| ESP32-C3 | Wi-Fi SSH access and serial communication |
| Digital microphone | I²S audio input |

The Artix-7 board sends frames over Ethernet to the Zynq board. A lightweight detector locates candidate regions, which are cropped and resized for a 12-block ViT classifier. HDMI displays the live preview and saved detection results. The audio pipeline extracts features from microphone samples and uses an audio Transformer to map recognized commands to supported actions. The SSH interface supports remote requests and Qwen-assisted queries for system status and image history.

The security design verifies the model manifest during initialization or model changes and authenticates model data at runtime. See the delivery notes for the protection and test coverage of each build.

## Downloads

- [Source and IP delivery archive](https://github.com/1incherry/48567/blob/weight_parts/fpgachina2026-48657.rar) includes FPGA sources, IP configurations, constraints, scripts, PS code, and a migration guide.
- [Model weights and reconstruction instructions](https://github.com/1incherry/48567/tree/weight_parts/weights) include split Qwen and NPU weights and a SHA-256 manifest. The Qwen weights are a hardware reference. Check compatibility with the target board build before loading them.

## Reproduction

1. Extract the delivery archive and follow the included Vivado and Vitis 2026.1 migration guide.
2. Open a copy of the target board project and check the device, sources, constraints, block design, and IP status. Generate IP output products and review clocks, reset, DDR settings, and address mappings.
3. Run synthesis and implementation, export the hardware platform, and build the matching PS application and boot files as applicable.
4. Reassemble and verify the model files, then check device and path settings in the JTAG scripts before deployment.

The Artix-7 migration copy passed the block design check after the IP upgrades. Refer to the included logs and notes for synthesis, implementation, and board-test status. Third-party tools, IP, and models are subject to their respective licenses.
