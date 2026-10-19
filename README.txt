FFmpeg FATE Sample Submission
=============================

Sample:
mov/spherical-vexu-orientation.mp4

Purpose:
Verify preservation of spherical orientation when both
sv3d and vexu metadata boxes are present in an MP4 file.

Expected spherical metadata:
projection=equirectangular
yaw=45
pitch=30
roll=15

FATE test:
fate-mov-spherical-vexu-orientation

Regression behavior:
Patched FFmpeg preserves the orientation.
Unpatched FFmpeg loses the orientation values.

File size:
1818 bytes

SHA-256:
0010a2578048b8099dd35058b6c14bd7085155d03dd7639308e1eccdbcc733d5

Related source commit:
618c862

Note:
This sample must be installed in the official FATE
sample collection for remote CI execution.
