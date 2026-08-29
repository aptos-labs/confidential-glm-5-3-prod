# Confidential GLM-5.3 production runtime

This repository is the public, signed Tinfoil release provenance for the
production GLM-5.3 confidential-inference CVM.

## What is attested

`tinfoil-config.yml` is the exact measured runtime exported from the production
CVM specification. It pins the GLM-5.3 model reference and MPK, the vLLM image
digest, resource allocation, and the complete vLLM command line.

The release workflow uses Tinfoil's pinned measurement action to publish a
Sigstore-signed deployment record and expected TDX measurements. A Tinfoil
verifier compares those expected measurements with a fresh quote from the live
CVM and verifies the attested TLS/HPKE key binding.

## Release process

1. Update the production `cvmctl` spec.
2. Export its exact measured runtime:

   ```bash
   cvmctl export-runtime -f vm-glm-5.3-prod.yml > tinfoil-config.yml
   ```

3. Review and commit the generated `tinfoil-config.yml`.
4. Run the **Tinfoil Release** workflow with a new immutable tag, for example
   `v0.0.1`.
5. Deploy that exact production specification, setting its metadata repository
   and tag to this repository and release.

Any runtime change—including the model, MPK, image digest, or vLLM arguments—
requires a new release before deployment.

## Security boundaries

This repository intentionally contains no credentials. The certificate
authorization token remains only in the protected host-side CVM specification.

The Tinfoil release attestation establishes that the live CVM matches this
signed runtime configuration. It does not independently establish upstream
model-weight-to-MPK provenance unless that mapping is separately provided and
verified by the model packaging process.
