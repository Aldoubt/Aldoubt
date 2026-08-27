# Profile Media Assets

This directory stores lightweight visual evidence used by the GitHub profile README.

## Recommended files

```text
assets/
├── navigation_runtime.gif
├── navigation_runtime.png
├── map_reconstruction.png
├── lio_benchmark.png
└── traversability.png
```

## Media rules

- Prefer **PNG/WebP** for static comparison figures.
- Prefer a short **GIF (6–12 s)** only when motion is necessary to understand the result.
- Keep GIF resolution around **960 px width** or lower and reduce frame rate to **8–12 fps**.
- For longer demonstrations, upload an MP4 to a GitHub Release, Bilibili, or another video host and use a preview image/GIF in the README.
- Crop terminal/UI noise whenever possible; the first frame should already show the robot/result clearly.
- Each visual should prove one claim: navigation execution, map reconstruction, trajectory benchmark, or traversability.

## Suggested naming

Use stable semantic names rather than dates so README links do not need frequent updates.

```text
navigation_runtime.gif
map_reconstruction.png
lio_benchmark.png
traversability.png
```
