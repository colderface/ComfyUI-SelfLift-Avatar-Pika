# Third-party notice

The full-sequence H3 memory-saving modules in this folder are adapted from
[Fish4AI/comfyui-SelfLift-Fish](https://github.com/Fish4AI/comfyui-SelfLift-Fish):

- `h3_global_tiling.py`
- `h3_stream_attention.py`
- `h3_ram_attention.py`
- `h3_output_chunking.py`
- `h3_prepared_weights.py`

Local changes add selflift-Avatar mask propagation, lazy loading, node wiring,
status reporting, input-projection chunking, and CPU/UI tests. The original
SelfLift project is by facok; Fish's global-context work is by the Fish4AI
maintainers. This fork is independent and is not an official release of either
project. Model weights, the H3 backbone, and ComfyUI remain subject to their own
licenses.

## Thanks

Special thanks to [Fish4AI](https://github.com/Fish4AI), author of
[comfyui-SelfLift-Fish](https://github.com/Fish4AI/comfyui-SelfLift-Fish), for
publishing the global-context memory-saving work that this project adapts. The
full-sequence chunking, head-group streaming, host-RAM staging, output chunking,
and prepared-weight reuse modules in this folder originate from that work.

Thanks also to facok for the original comfyui-SelfLift project and to the
SelfLift paper authors.

## This fork: ComfyUI-SelfLift-Avatar-Pika

This repository is a fork of [slmonker/selflift-Avatar](https://github.com/slmonker/selflift-Avatar)
at commit `8fec8ca` (2026-11-24). Every notice above is kept unchanged.

Local additions in this fork:

- LCM support for the resolution transition: instead of completing the Euler
  interval after the corrected high-resolution endpoint, the state is discarded
  and fresh noise is injected at the next sigma, with the auxiliary audio
  streams pinned to the same boundary. The transition-boundary logic follows the
  H3 LCM recipe from the local `ComfyUI-SelfLift-Pika` build; the mask handling
  is upstream's and is untouched.
- A separate `SelfLiftAvatarPikaLcmH3Sampler` node and a `lcm_mode` switch in
  `progressive_sample`. The default Euler path is unchanged.
- All sampler / TST node IDs are prefixed `SelfLiftAvatarPika*` so this plugin
  can be installed alongside the packaged upstream release
  `v0.1.4-experimental`, which registers the unprefixed names.

Neither the upstream project nor this fork declares a license. Redistribution
and reuse stay subject to the original authors' terms; this fork grants no
additional rights to upstream code. Model weights, the H3 backbone, and ComfyUI
remain subject to their own licenses.
