# Wisper::RabbitMQ [WIP]

Relay Wisper events to RabbitMQ.

## Installation

```ruby
gem 'wisper-rabbitmq'
```

## Usage

```ruby
Wisper::RabbitMQ.enable
```

The above will forward all events to RabbitMQ with the following defaults:

* Host: `amqp://guest:guest@localhost:5672`
* VirtualHost: `/`
* Exchange: `fanout`
* Queue: `wisper`

## Configuration

```ruby
Wisper::RabbitMQ.configure do |config|
  config.host = '...'
  # or
  config.connection = my_connection
end
```

`my_connection` must be a [Bunny]() compatible client. This is useful on JRuby
as it allows use of the more performant [Hare]() library.

And the other, optional, configurables:

```ruby
config.virtual_host = 'myapp'
config.queue = 'default'
```

The value for each configurable can also be a callable object, e.g.

```ruby
config.virtual_host = ->(event) { ... }
```

### Whitelisting

You can filter which events are relayed to RabbitMQ using a callable object:

```ruby
Wisper::RabbitMQ.configure do |config|
  config.relay_events = ->(event_name) { %w(:thing_created).include?(event_name) }
end
```

## Contributing

Yes, please.
