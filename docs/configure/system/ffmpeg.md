# FFmpeg

Many settings about how Tunarr transcode content can be configured on the FFmpeg page

## Executable Paths

Configure FFmpeg and FFprobe executable paths. Generally, both executables reside in the same directory.

!!! warning

    On 2024/10/01, an [exploit](https://www.exploit-db.com/exploits/52079) affecting dizqueTV was reported. This mainly affects instances exposed to the public internet. The exploit affected Tunarr as well, and was patched in 0.14.0. As of v0.21.0, additional protections were added by using `execFile()` instead of `exec()` when executing child processes, combined with proper input sanitization.

    **We consider exposing Tunarr publicly to be an unsupported use-case.** While we take security extremely seriously, streaming and administration endpoints are not currently separated or authorized. We would not recommend exposing Tunarr to the public via port forwarding at this point.

FFmpeg executable paths can be configured directly in the Tunarr UI. In Docker containers, overriding FFmpeg paths is disabled for additional security.
