<p align="center">
  <img src="images/LernaAI.png" alt="Lerna AI" />
</p>

# Lerna AI Dashboard
Lerna AI Dashboard is a UI component, implemented based on Vue.js [[3]](#references) and AdminLTE [[4]](#references).

Provides:

* Login form for Customers

* Registration form for new Customers

* Dashboard view with ML statistics
  * Prediction success rate
  * Total amount of data used for training
  * Total number of devices with Lerna AI SDK
  * Number of ML iterations
  * Model accuracy per iteration
  * Percentage of devices participating on the training tasks

* Configuration page for integrating with 3rd party tools (e.g., slack, firebase, etc.)

* Model view
  * Display the models with their ML parameters
  * Display the accuracy per model
  * Export latest model weights

* Profile page

* Contact information page

## Execution

The dashboard's [[1]](#references) static content should be served by a web server. 
To build the static content from the dashboard source code you can run 
```shell
npm run build
```
please check [[2]](#references) for more info.

You can also build and run as stand-alone docker container by executing
```shell
docker-compose up --build
```

## Requires

* nginx to serve the static content [[5]](#references)

* FL-API (port 5000)

## Required by

N/A

## References

[1] [Dashboard](https://github.com/lerna-ai/dashboard)

[2] [Dashboard Readme File](https://github.com/lerna-ai/dashboard/blob/master/README.md)

[3] [Vue.js](https://vuejs.org/)

[4] [AdminLTE](https://adminlte.io/)

[5] [nginx configuration](Component_NGINX.md#Dashboard)
