<p align="center">
  <img src="images/LernaAI.png" alt="Lerna AI" />
</p>

# Lerna AI MPC Gateway Service
Lerna AI MPC Gateway Service is a NodeJS application that exposes a REST API for the MPC Service.

## Execution

MPC Gateway service can run as a stand-alone docker container [[1]](#references) or by executing the commands in [[2]](#references).

In both cases, it requires valid certificate files under the respective paths - please check [[3]](#references) for more info.

## Requires

* MPC Service (port 31337)
  
## Required by

* Lerna SDK (port 8080)

## References

[1] [MPC Gateway Repository](https://github.com/lerna-ai/mpc-gateway)

[2] [MPC Gateway File](https://github.com/lerna-ai/mpc-gateway/blob/master/README.md)

[3] [Lerna Keys Readme File](https://github.com/lerna-ai/infra/blob/master/LernaKeys/README.md)
