# Disable AAC/FLAC DSP Offload

On some devices like the LG G5, LineageOS attempts to offload AAC and FLAC
decoding to the DSP even when it is not supported. This manifests as broken
playback for those codecs.

This Magisk module patches the file `/system/etc/audio_policy_configuration.xml`
(and the legacy `audio_policy.conf`) to disable this behaviour. To simplify
parsing with `awk`, some assumptions are made:

- The offloaded mix ports are named `compress_offload`
- The formats to be removed from offloading are not the first in their list in
  the legacy format

It is currently not compatible with other modules that modify the audio policy
files (i.e. it does not use
[AML](https://github.com/Zackptg5/Audio-Modification-Library)). The files are
patched once during the installation and from then on mounted from the module.

Magisk 18 is required.
