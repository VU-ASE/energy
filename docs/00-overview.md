import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Overview

## Purpose 

The `energy` service uses the INA226 current sensor to measure current draw (amps), power consumption (watts), and supply voltage.

:::info

This service requires an extra sensor that does not come preinstalled with every Rover. See the [requirements](#requirements) section.

:::

## Installation

To install this service, the latest release of [`roverctl`](https://ase.vu.nl/docs/framework/Software/rover/roverctl/installation) should be installed for your system and your Rover should be powered on.

<Tabs groupId="installation-method">
<TabItem value="roverctl" label="Using roverctl" default>

1. Install the service from your terminal
```bash
# Replace ROVER_NUMBER with your the number label on your Rover (e.g. 7)
roverctl service install -r <ROVER_NUMBER> https://github.com/VU-ASE/energy/releases/latest/download/energy.zip 
```

</TabItem>
<TabItem value="roverctl-web" label="Using roverctl-web">

1. Open `roverctl-web` for your Rover
```bash
# Replace ROVER_NUMBER with your the number label on your Rover (e.g. 7)
roverctl -r <ROVER_NUMBER>
```
2. Click on "install a service" button on the bottom left, and click "install from URL"
3. Enter the URL of the latest release:
```
https://github.com/VU-ASE/energy/releases/latest/download/energy.zip 
```

</TabItem>
</Tabs>

Follow [this tutorial](https://ase.vu.nl/docs/tutorials/write-a-service/upload) to understand how to use an ASE service. You can find more useful `roverctl` commands [here](/docs/framework/Software/rover/roverctl/usage)

## Requirements

- An INA226 current sensor must be mounted to the Rover over [I2C](https://ase.vu.nl/docs/framework/hardware/Components/carrier-board#wiring-connections). **The sensor's shunt resistor must be connected at the battery's connection terminals.**

## Inputs

As defined in the [*service.yaml*](https://github.com/VU-ASE/energy/blob/main/service.yaml), this service does not depend on any other service.

## Outputs

As defined in the [*service.yaml*](https://github.com/VU-ASE/energy/blob/main/service.yaml), this service exposes the following write streams:

- `energy`:
    - To this stream, [`EnergySensorOutput`](https://github.com/VU-ASE/rovercom/blob/c1d6569558e26d323fecc17d01117dbd089609cc/definitions/outputs/energy.proto#L11) messages will be written. Each message will be wrapped in a [`SensorOutput` wrapper message](https://github.com/VU-ASE/rovercom/blob/main/definitions/outputs/wrapper.proto)
