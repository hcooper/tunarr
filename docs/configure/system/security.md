# Security

!!! warning "Do not expose Tunarr to the public internet"

    Tunarr should not be exposed to the public internet via port forwarding. While security is taken seriously, streaming and administration endpoints are not currently separated or authorized, making public exposure unsafe. Expose Tunarr at your own risk.

## Updating sensitive settings

Tunarr protects against RCE exploits by using `execFile()` instead of `exec()` when executing child processes, combined with proper input sanitization. As of v0.21.0, FFmpeg executable paths can be edited directly in the UI (this was previously restricted to "admin mode" which has been removed).

For advanced users, settings can also be updated via the CLI:

### Standalone binary

```bash
./tunarr settings update --settings.ffmpeg.ffmpegExecutablePath="FFMPEG_PATH" --settings.ffmpeg.ffprobeExecutablePath="FFPROBE_PATH"
```

### Docker

```bash
docker run --rm \
  -v /path/to/tunarr/data:/config/tunarr \
  chrisbenincasa/tunarr -- /tunarr/tunarr \
  settings update \
  --settings.ffmpeg.ffmpegExecutablePath="FFMPEG_PATH" \
  --settings.ffmpeg.ffprobeExecutablePath="FFPROBE_PATH"
```

## Trust proxy

When running Tunarr behind a reverse proxy server for HTTPS support, you will need to enable "trust proxy" for the generated XMLTV and M3U files to contain the correct protocol (e.g., `http` or `https`) and host. Without "trust proxy" enabled, Tunarr will not honor the `X-Forwarded-Proto` and `X-Forwarded-Host` headers forwarded from the reverse proxy.

There are several ways to enable "trust proxy".

### Standalone script

Pass the `--trustProxy` flag when running the script, e.g.:

```bash
 ./tunarr --trustProxy
```

or on Windows:

```powershell
.\tunarr.exe --trustProxy
```

You can also use an environment variable:

```bash
TUNARR_SERVER_TRUST_PROXY=true ./tunarr
```

and again on Windows (Powershell):

```powershell
$Env:TUNARR_SERVER_TRUST_PROXY='true'
.\tunarr.exe
```

or Command Prompt:

```
set TUNARR_SERVER_TRUST_PROXY=true
.\tunarr.exe
```

### Docker

Start Tunarr server with the `trustProxy` argument

```bash
docker run ... chrisbenincasa/tunarr:latest -- /tunarr/tunarr --trustProxy
```

or with the environment variable

```bash
docker run -e 'TUNARR_SERVER_TRUST_PROXY=true' ... chrisbenincasa/tunarr
```
