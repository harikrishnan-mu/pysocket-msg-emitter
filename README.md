# PySocket-msg-emitter

PySocket-msg-emitter is a Python library for emitting events and messages over different channels, with support for Redis and Kafka.

## Installation

You can install PySocket-msg-emitter using pip:

```bash
pip install PySocket-msg-emitter
```

You can also install PySocket-msg-emitter for specific client using pip.

To install PySocket-msg-emitter only for Redis Client:

```bash
pip install PySocket-msg-emitter[redis]
```

To install PySocket-msg-emitter only for Redis Client:

```bash
pip install PySocket-msg-emitter[kafka]
```

## Motivation
The motivation behind creating PySocket-msg-emitter was to provide a reliable and up-to-date solution for emitting events to Socket.IO clients in Python projects. Given the lack of maintenance and updates for the socket.io-emitter package, there was a need for a modern alternative that supports current Python versions and integrates well with popular libraries and frameworks.


## Features
Emit events to specific rooms or namespaces
Support for binary and JSON payloads
Integration with Redis and Kafka for scalable event broadcasting
Easy-to-use API for seamless integration into existing projects

## Usage

### Basic Usage of Redis Emitter

```python
from pysocket_msg_emitter import Emitter
from socket_io_emitter import Emitter

io.Emit('broadcast event','Hello from socket.io-python-emitter')

# Create an Emitter instance
emitter = Emitter(
    engine="redis",
    host="localhost",
    port=6379,
    key="socket.io_emitter",
)

# Emit an event broadcast event
emitter.emit("event_name", "Hello from PySocket-msg-emitter!")
```

### Basic Usage of Kafka Emitter

```python
from pysocket_msg_emitter import Emitter
from socket_io_emitter import Emitter

io.Emit('broadcast event','Hello from socket.io-python-emitter')

# Create an Emitter instance
emitter = Emitter(
    engine="kafka",
    host="localhost",
    port=9092,
    key="socket.io_emitter",
)

# Emit an event broadcast event
emitter.emit("event_name", "Hello from PySocket-msg-emitter!")
```

## Emitter Options

The following options are allowed:

client: is a redis-py compatible client
This argument is optional.
engine: the name of the client you want to use (redis/kafka)
key: the name of the key to events on as prefix (socket.io_emitter)
host: host to connect to redis/kafka on (localhost)
port: port to connect to redis/kafka on (6379/9092)

If you don't want to supply a redis client object, and want PySocket-msg-emitter to initialize one for you, make sure to supply engine option.


# API

## in_room()
You can emit messages to different rooms:

```
# Emit message to specific room
emitter.in_room("room1").emit("event_name", "Hello from PySocket-msg-emitter!")

# Emit message to multiple rooms
emitter.in_room("room1","room2").emit("event_name", "Hello from PySocket-msg-emitter!")

# Emit message to list of rooms
emitter.in_room(["room1","room2"]).emit("event_name", "Hello from PySocket-msg-emitter!")


```


## of_namespace()

You can emit messages to different namespaces:

```python
# Emit message to specific namespace
emitter.of_namespace("/nsp").in_room("room1").emit("event_name", "Hello from PySocket-msg-emitter!")

# Emit message to multiple namespaces
emitter.of_namespace("/nsp1", "/nsp2").in_room("room1").emit("event_name", "Hello from PySocket-msg-emitter!")

# Emit message to list of namespaces
emitter.of_namespace(["/nsp1", "/nsp2"]).in_room("room1").emit("event_name", "Hello from PySocket-msg-emitter!")
```

## Different type of event

You can emit different type of events like text event, binary event and JSON event.

```python

# Emit test message to multiple rooms
emitter.of_namespace("/nsp").in_room("room1","room2").emit("event_name", "Test message from PySocket-msg-emitter!")

# Emit binary message to multiple rooms
emitter.of_namespace("/nsp").in_room("room1","room2").emit("event_name", b"Binary message from PySocket-msg-emitter!")

# Emit JSON message to multiple rooms
emitter.of_namespace("/nsp").in_room("room1","room2").emit("event_name", {"key": "value"})
```

## Supported Channels

Currently, PySocket-msg-emitter supports emitting events over Redis and Kafka channels.

## Contributing

Contributions are welcome! If you encounter any issues, have feature requests, or would like to contribute code, please open an issue or submit a pull request on the GitHub repository.

## Credits
This project was inspired by the socket.io-emitter (https://pypi.org/project/socket.io-emitter/) package, which provided a similar functionality but was last updated 6 years ago and is no longer maintained.
