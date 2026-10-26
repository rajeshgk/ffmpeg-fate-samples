# Legacy spherical UUID and vexu precedence fixtures

These fixtures cover FFmpeg PR #25168:
https://code.ffmpeg.org/FFmpeg/FFmpeg/pulls/25168

Both contain a legacy Google spherical UUID at track level, no sv3d box,
and vexu/proj/prji with projection type hequ. The UUID describes a 1280x720
crop of a 2560x720 panorama, with left offset 640 and top offset 0.

- spherical-uuid-before-vexu.mp4: the UUID precedes mdia.
- spherical-uuid-after-vexu.mp4: the UUID follows mdia.

Expected ffprobe spherical side data for both:

```text
projection=half equirectangular
yaw=0
pitch=0
roll=0
```

At original PR head b881fc8a78c7b718d079892e4c053ed890a89ebf,
the UUID-before variant incorrectly reports equirectangular and emits a
conflict warning. Commit 864ee841b99bb3472012fa88ed444cee73fd4e29 fixes that
regression while retaining the original dual-box orientation correction.

Each file is 2621 bytes. SHA-256:

```text
b64928fba39402bcb84a079026e70b7a2d331ebd1daaaba7c2cb433771c56fac  spherical-uuid-before-vexu.mp4
c18e9d13973bd4b43fcbc57385bdd37cbd941600df4cdfc60e9717d5d3905e24  spherical-uuid-after-vexu.mp4
```

Requested official FATE destinations:

- mov/spherical-uuid-before-vexu.mp4
- mov/spherical-uuid-after-vexu.mp4

Corresponding FATE targets:

- fate-mov-spherical-uuid-before-vexu
- fate-mov-spherical-uuid-after-vexu

The fixtures are derived from spherical-vexu-orientation.mp4 (1818 bytes;
SHA-256 0010a2578048b8099dd35058b6c14bd7085155d03dd7639308e1eccdbcc733d5).
Enclosing box sizes and chunk offsets are adjusted; the media payload is
unchanged. The source track dimensions are preserved.

Local validation passed on Linux x86-64 and macOS 26.7.2 arm64: the original
regression is reproduced, twelve directed metadata cases pass with the fix,
and all three focused spherical FATE targets pass. The new fixtures also
decoded successfully with the system FFmpeg during Linux validation.

This repository makes the samples available for installation by a FATE sample
maintainer. Availability here does not mean they are installed in the official
FATE collection.
