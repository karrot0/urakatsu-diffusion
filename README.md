# urakatsu-diffusion

CUDA builds of [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp)'s
`sd-server` for Linux, which upstream does not publish (its Linux releases are Vulkan, ROCm and
CPU only). [Urakatsu](https://github.com/karrot0/Urakatsu) installs them as its `linux-cuda-13`
build of stable-diffusion.cpp.

Every few hours `.github/workflows/release.yml` checks for a new upstream release and, if it is
not built yet, builds it and releases it under the same tag:

| Asset | Contents |
| --- | --- |
| `sd-<tag>-bin-linux-x64-cuda-13.tar.gz` | `sd-server`, statically linked against stable-diffusion.cpp and ggml, looking for its libraries next to itself |
| `cudart-sd-<tag>-bin-linux-x64-cuda-13.tar.gz` | The CUDA 13 libraries it loads (cudart, cuBLAS, cuBLASLt) |

Extract both into one folder. It needs an NVIDIA driver from the 580 branch or newer, and glibc
2.39 (Ubuntu 24.04 or newer). Code is built for Turing (T4) through Blackwell.

The recipe follows Koharu's [koharu-rs/diffusion](https://github.com/koharu-rs/diffusion), with
the server example added. Run the workflow by hand (Actions, Diffusion, Run workflow) to build a
specific tag.

stable-diffusion.cpp is MIT licensed (its license ships in the archive). The CUDA libraries are
NVIDIA's, redistributed under the CUDA Toolkit EULA.
