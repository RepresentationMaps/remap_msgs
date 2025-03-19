# ReMap msgs

A set of reMap related ROS 2 messages.

## Service messages

### remap_msgs/srv/AddPlugin

`remap_msgs/srv/AddPlugin`: a service message used to activate a reMap plugin. It is defined as:
```
string plugin_name
bool threaded
---
bool success
```

Where:
- `plugin_name` is the name of the plugin to activate.
- `threaded` is a flag to indicate if the plugin should use multithreading to accelerate its access to the semantic map (see [`remap_map_handler`](https://gitlab.pal-robotics.com/interaction/remap_map_handler)) (⚠️ *Multithreading not supported yet* ⚠️).
- `success` is a flag that indicates if the plugin was successfully activated.

### remap_msgs/srv/RemovePlugin

`remap_msgs/srv/RemovePlugin`: a service message used to deactivate a reMap plugin. It is defined as:
```
string plugin_name
---
bool success
```

Where:
- `plugin_name` is the name of the plugin to deactivate.
- `success` is a flag that indicates if the plugin was successfully deactivated.

## License

This package is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.

## Authors

Developed by **PAL Robotics, S.L.**