# Processing

This service follows the following steps:

1. It reads the sensor data from the INA226 sensor over I2C
2. When it receives the sensor data, it will wrap this data in an [`EnergySensorOutput` message](https://github.com/VU-ASE/rovercom/blob/c1d6569558e26d323fecc17d01117dbd089609cc/definitions/outputs/energy.proto#L11), which it will  write to its `energy` stream, as defined in its [*service.yaml*](https://github.com/VU-ASE/energy/blob/4df7bf7ba43504b9b88995285472f2c3a59ace77/service.yaml#L14C5-L14C11)

## Refresh Rate

You will most likely want to use this service together with another service to measure energy consumption of a pipeline on the Rover. Be aware that the refresh rate of this sensor is quite low: 5 Hz (but this is [configurable](https://github.com/VU-ASE/energy/blob/4df7bf7ba43504b9b88995285472f2c3a59ace77/service.yaml#L17)), so you might slow down your service if you read from this service in your main loop.

We advise to use a threaded solution in case you want to use this service. See the "knowing more" series on the ASE website for more information.
