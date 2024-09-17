<p align="center">
  <img src="images/LernaAI.png" alt="Lerna AI" />
</p>

# Lerna AI MPC Service
Lerna AI MPC Service is a privacy service, implemented in ANSI C, that can
be adapted to run on an Intel® Software Guard Extensions (Intel® SGX).

Provides:

* Differential Privacy

* End-to-end Property Preserving Encryption

* Secure Computations

## Execution

MPC service can run as stand-alone docker container [[1]](#references) or by executing the commands in [[2]](#references).
In both cases, it requires valid certificate files under the respective paths - please check [[3]](#references) for more info.

## Requires

N/A

## Required by

* FL-API (port 31337)

* MPC Gateway (port 31337)

* Android Native SDK (Legacy) (port 31337)

## References

[1] [MPC Repository](https://github.com/lerna-ai/mpc)

[2] [MPC Readme File](https://github.com/lerna-ai/mpc/blob/master/README.md)

[3] [Lerna Keys Readme File](https://github.com/lerna-ai/infra/blob/master/LernaKeys/README.md)
