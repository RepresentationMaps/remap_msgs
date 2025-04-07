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

### remap_msgs/srv/Query

`remap_msgs/srv/Query`: a service message used to query reMap. It is defined as:
```
# a set of partially bound statements (ie, some terms in the statement(s) are
# variables, starting with a '?')
string[] patterns

# the variables you want to be returned. If empty, all variables found in the
# patterns are returned
string[] vars

string[] models

# if dynamic is True, the query will be dinamically updated
bool dynamic

# the amount of time the point cloud result will be available.
# If duration is 0, the result will be available indefinitely.
builtin_interfaces/Duration duration

# the frequency at which the query will be updated
builtin_interfaces/Duration frequency

# if publish_tf is True, a transform will be published for each variable in the
# query; the transform will locate a frame (<id>/<variable>) placed in the
# centroid of the retrieved point cloud.
bool publish_tf

string id
---
bool success

# a JSON-encoded list of dictionaries, representing the result of the FIND
# method. Each key in the dictionaries correspond to one variable.
string json

# if success = False, error_msg might contain additional information about the
# failure.
string error_msg
```

It takes inspiration from the [`kb_msgs/srv/Query`](https://gitlab.pal-robotics.com/interaction/kb_msgs/-/blob/main/srv/Query.srv) service message.
Let's deep dive in each of these fields:

- `patterns`, `vars` and `models` are equivalent to the field with the same name defined in `kb_msgs/srv/Query`:
	- `patterns`: a list of strings, each one representing a partially bound statement. Each statement can contain variables, which are indicated with a `?`.
	- `vars`: a list of strings, each one representing a variable. If empty, all variables found in the patterns are returned.
	- `models`: a list of strings, each one representing a model. If empty, all models are returned.
- `dynamic`: a flag to indicate if the query should be updated dynamically. If `true`, it will be continously computed, according to the `frequency` parameter. If `false`, it will be computed only once.
- `duration`: the amount of time the point cloud result will be available.
- `frequency`: the frequency at which the query will be updated. It is only used if `dynamic` is `true`.
- `publish_tf`: a flag to indicate if a transform should be published for each variable in the query. The transform will locate a frame (`<id>/<variable>`) placed in the centroid of the retrieved point cloud.
- `id`: a string that identifies the query.

The result fields are exactly the same as in `kb_msgs/srv/Query`:

- `success`: a flag that indicates if the query was successful.
- `json`: a JSON-encoded list of dictionaries, representing the result of the query.
- `error_msg`: if `success` is `false`, this field might contain additional information about the failure.

### remap_msgs/srv/RemoveQuery

`remap_msgs/srv/RemoveQuery`: a service message used to remove a query. It is defined as:
```
string id
---
bool success

builtin_interfaces/Duration exec_left
```

Where:
- `id`: a string that identifies the query to remove.
- `success`: a flag that indicates if the query was successfully removed.
- `exec_left`: the amount of time left for the query to be executed.

## License

This package is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.

## Authors

Developed by **PAL Robotics, S.L.**