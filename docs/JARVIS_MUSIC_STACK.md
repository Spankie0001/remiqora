# Jarvis music stack

Recorded October 2, 2026 (America/Chicago).

## Scope and evidence

Remiqora is the music application identified by Jason for the Jarvis AI-server inventory. Component names and capabilities below are grounded in this repository's linux-headless README. This documentation update did not access Jarvis, inspect downloaded model weights, check running processes, change GPU assignments, install software or restart services. Repository support for a component is not proof that its weights are installed or that it is currently loaded. Verify deployment details on the host before treating this as a live inventory.

## Generation engines

| Component | Role |
| --- | --- |
| ACE-Step 1.5 | Music generation from descriptions, style tags and lyrics; covers, section repainting and part editing; optional LoRA training. |
| YuE2-3B through audio.cpp | Full-length music generation with optional symbolic melody/chord planning. |

These are the two music-generation engines. Remiqora itself is their browser interface and orchestrator, with a built-in multitrack editor; it is not a separate music model.

## Supporting tools

| Component | Role |
| --- | --- |
| Demucs / htdemucs | Separates vocals, drums, bass and other stems. |
| SheetSage2 | Extracts melody and harmony into ABC notation for reference-guided generation. |
| MuScriptor | Transcribes audio into MIDI; the documented workflow requires YuE2 to be active. |

Suno is a separate hosted service, not a locally installed Jarvis music model. Qwen3 chat and Jarvis Voice are separate services and should not be listed as these music-generation engines.

## Platform and configuration

The documented stack is a Python/FastAPI backend, Vue 3/TypeScript frontend, SQLite track registry and shared audio files. Linux NVIDIA CUDA setup is provided by setup_linux.sh; prod_run_linux.sh serves the built UI and API. See [the README](../README.md) for requirements, model setup, configuration and known limitations.

The README's default production port is 9000, with REMIQORA_HOST and REMIQORA_PORT overrides. This is a repository default, not a verified Jarvis endpoint. Likewise, actual Jarvis installation directories, service names, engine ports, weight variants and GPU assignments remain unverified here. The defaults for other AI services must not be assumed compatible without checking for port conflicts.

**Security:** Remiqora has no built-in authentication. The default host is 127.0.0.1 (local only). Setting REMIQORA_HOST=0.0.0.0 exposes the full UI and API to anyone on the network, so only do that on a trusted network or behind an authenticated reverse proxy.

Linux can opt into separate-GPU engine residency by setting ACE_STEP_DEVICE and YUE2_DEVICE to different explicit device values. Otherwise the documented default is exclusive engine switching. The example 0/1 assignments in the README are examples, not a confirmation of Jarvis configuration.

## Next host verification

Record the actual checkout revision, installation paths, downloaded checkpoints, enabled service and UI URL, configured engine ports, GPU assignments and date/results of a short generation test for each engine. Check supporting tools separately, since weights may download on first use. Distinguish installed, service running, model loaded and generation tested in the inventory.

This is a documentation checkpoint only; no runtime changes were made.
