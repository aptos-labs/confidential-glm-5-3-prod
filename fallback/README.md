# DCP=8 fallback runtime

`tinfoil-config.dcp8.yml` is the fallback for the GLM-5.3 v0.30.0 rollout. It is the same runtime as the
root `tinfoil-config.yml` except `--decode-context-parallel-size=8` (instead of 4). Its sha256 is
`cd58b1d06f53b1c1976a2430318150781ce780c56ddd98815f17db3192d12969`.

The release workflow measures only the root `tinfoil-config.yml`. To fall back, copy this file over the
root `tinfoil-config.yml`, merge, and cut the next release (planned v0.0.12). Then apply the host spec
`/etc/atlas-host1/glm-production-v0.0.12-dcp8.yaml`.
